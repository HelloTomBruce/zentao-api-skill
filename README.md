# ZenTao API SKILL

禅道(ZenTao)项目管理系统的 Python API 客户端，支持产品、项目、任务、Bug 全生命周期管理。

## 目录

- [特性](#特性)
- [支持的禅道版本](#支持的禅道版本)
- [安装](#安装)
- [快速开始](#快速开始)
- [配置凭证](#配置凭证)
- [API 参考](#api-参考)
  - [任务管理](#任务管理)
  - [Bug管理](#bug管理)
  - [产品管理](#产品管理)
  - [需求管理](#需求管理)
  - [测试管理](#测试管理)
- [状态流转](#状态流转)
- [注意事项](#注意事项)
- [常见问题](#常见问题)
- [项目结构](#项目结构)
- [许可证](#许可证)

---

## 特性

- 禅道老 API (Legacy API v1.0) 封装
- Session 认证方式
- 支持产品、项目、需求、任务、Bug、测试用例全流程
- 返回格式统一处理（兼容 text/html 返回 JSON 的情况）
- 丰富的类型提示和文档注释

---

## 支持的禅道版本

本客户端基于禅道 **老 API (Legacy API v1.0)** 开发，兼容范围广泛。

### 兼容版本

| 版本类型   | 兼容版本    | 说明                  |
| ---------- | ----------- | --------------------- |
| **开源版** | 12.x - 20.x | 12.x 起全面支持老 API |
| **旗舰版** | 4.x - 7.x   | 全系列支持            |
| **企业版** | 13.x 及以上 | 企业版全系列支持      |
| **IPD版**  | 1.x - 5.x   | IPD 系列全支持        |

> **实测反馈**：禅道 12.3.3 版本测试通过。

### 关于新 API (v2.0)

禅道 **21.7+** 版本引入了全新的 **API v2.0**，采用 RESTful 风格和 Token 认证方式：

- **新 API (v2.0)**：禅道 21.7+ 推荐使用
- **老 API (v1.0)**：本客户端使用，21.7 仍可使用但逐步废弃

### 版本查询

```python
# 查看禅道版本
# 登录禅道后，在 管理 -> 关于 中查看版本号
```

---

## 安装

### 环境要求

- Python 3.8+
- requests 库

### 安装依赖

```bash
pip install -r requirements.txt
```

或直接安装：

```bash
pip install requests>=2.28.0
```

---

## 快速开始

### 1. 配置凭证

在项目根目录创建 `TOOLS.md` 文件：

```markdown
## 禅道 API

- **API 地址：** http://your-zentao-host/
- **用户名：** your-username
- **密码：** your-password
```

### 2. 使用客户端

```python
from pathlib import Path
import sys

# 导入禅道客户端
lib_path = Path(__file__).parent / 'lib'
sys.path.insert(0, str(lib_path))
from zentao_client import ZenTaoClient, read_credentials

# 读取凭证
credentials = read_credentials()

# 创建客户端
client = ZenTaoClient(
    credentials['endpoint'],
    credentials['username'],
    credentials['password']
)

# 获取会话（首次登录，后续自动加载持久化的 Session）
sid = client.get_session()
print(f"登录成功，Session ID: {sid}")
```

### 3. Session 持久化

客户端支持 Session 持久化，无需每次都登录：

```python
client = ZenTaoClient('http://127.0.0.1:8080', 'admin', 'password')

# 首次调用自动登录并保存 Session
sid = client.get_session()  # 登录 + 保存

# 新实例自动加载已有 Session
client2 = ZenTaoClient('http://127.0.0.1:8080', 'admin', 'password')
sid2 = client2.get_session()  # 直接加载，无需登录

# 强制刷新 Session
sid3 = client.get_session(force_refresh=True)  # 重新登录

# 清除保存的 Session
client.clear_session()
```

**存储位置**：项目根目录 `.zentao/sessions/` 目录下

```
项目目录/
├── .zentao/
│   └── sessions/
│       └── {hash}.json  # Session 文件
└── ...
```

**配置选项**：
```python
client = ZenTaoClient(
    endpoint,
    username,
    password,
    session_dir=None,     # Session 存储目录，默认 .zentao/sessions（项目根目录）
    auto_save=True,       # 登录后自动保存
    auto_load=True,       # 启动时自动加载
)
```

---

## 配置凭证

凭证配置支持两种方式：

### 方式一：TOOLS.md 文件

在项目根目录创建 `TOOLS.md`：

```markdown
## 禅道 API

- **API 地址：** http://192.168.1.100/zentao/
- **用户名：** admin
- **密码：** your-password
```

### 方式二：环境变量

```python
import os
os.environ['ZENTAO_ENDPOINT'] = 'http://192.168.1.100/zentao/'
os.environ['ZENTAO_USERNAME'] = 'admin'
os.environ['ZENTAO_PASSWORD'] = 'your-password'
```

---

## API 参考

### 认证

```python
# 获取会话
sid = client.get_session()
if not sid:
    print("认证失败")
```

### 任务管理

```python
# 创建任务
client.create_task(
    project="1",
    name="用户登录功能开发",
    type="devel",
    story="5",
    assignedTo="admin",
    pri="3",
    estimate="8",
    desc="实现用户登录功能"
)

# 批量创建任务
client.create_tasks(
    project="1",
    tasks=[
        {"name": "前端开发", "type": "devel", "assignedTo": "dev1", "estimate": "8"},
        {"name": "后端开发", "type": "devel", "assignedTo": "dev2", "estimate": "16"},
        {"name": "测试", "type": "test", "assignedTo": "qa1", "estimate": "4"}
    ]
)

# 查看我的任务
success, tasks = client.get_my_tasks("assignedTo")

# 查看任务详情
success, task = client.get_task_detail(task_id)
print(f"状态: {task['status']}")  # wait, doing, pause, done, cancel, closed

# 开始任务
client.start_task(task_id, "开始开发")

# 记录工时（批量）
from datetime import datetime
today = datetime.now().strftime("%Y-%m-%d")
client.record_estimate(task_id, [
    {"date": today, "consumed": "3", "left": "5", "work": "完成开发"}
])

# 完成任务（先记录工时 left=0）
client.record_estimate(task_id, [
    {"date": today, "consumed": "8", "left": "0", "work": "全部完成"}
])
client.finish_task(task_id, "开发完成")

# 暂停/继续任务
client.pause_task(task_id, "等待依赖")
client.restart_task(task_id, "继续开发")

# 创建子任务
client.create_subtasks(
    execution_id="1",
    parent_id="100",
    tasks=[
        {"name": "前端开发", "estimate": "8", "assignedTo": "dev1"},
        {"name": "后端开发", "estimate": "16", "assignedTo": "dev2"}
    ]
)
```

### Bug管理

```python
# 查看我的 Bug
success, bugs = client.get_my_bugs("assignedTo")

# 查看 Bug 详情
success, bug = client.get_bug(bug_id)

# 创建 Bug
client.create_bug(
    product_id="1",
    title="登录页面报错",
    severity="3",
    pri="3",
    type="codeerror",
    steps="1.打开登录页\n2.输入账号\n3.点击登录\n4.出现500错误",
    assignedTo="dev1"
)

# 解决 Bug
client.resolve_bug(bug_id, "fixed", "trunk", "已修复")

# 关闭 Bug
client.close_bug(bug_id, "验证通过")

# 激活 Bug
client.activate_bug(bug_id, "问题重现")

# 从测试用例创建 Bug
client.create_bug_from_testcase(
    case_id="8",
    title="登录功能测试发现Bug",
    severity="3",
    pri="3",
    assignedTo="admin"
)

# 或使用 create_bug + case_id 参数
client.create_bug(
    product_id="1",
    title="测试发现Bug",
    case_id="8",  # 关联测试用例
    severity="3",
    pri="3",
    steps="重现步骤",
    assignedTo="admin"
)
```

### 产品管理

```python
# 查询产品列表
success, products = client.get_products()

# 创建产品
client.create_product(
    name="新产品",
    code="NEW",
    po="admin",
    status="normal"
)
```

### 需求管理

```python
# 创建需求
client.create_story(
    product_id="1",
    title="用户登录功能",
    pri="3",
    estimate="8",
    spec="实现用户登录功能"
)

# 查看我的需求
success, stories = client.get_my_stories("assignedTo")

# 编辑需求
client.edit_story(story_id, title="新标题", pri="2")

# 关闭需求
client.close_story(story_id)
```

### 测试管理

```python
# 创建测试用例（字符串格式）
client.create_testcase(
    product_id="1",
    title="登录功能测试",
    case_type="feature",
    pri="3",
    steps="1.打开登录页\n2.输入账号密码\n3.点击登录",
    expect="登录成功"
)

# 创建测试用例（列表格式 - 精确控制步骤和预期结果）
client.create_testcase(
    product_id="1",
    title="注册功能测试",
    case_type="feature",
    pri="2",
    steps_list=["打开注册页面", "填写用户信息", "点击注册按钮", "验证注册成功"],
    expects_list=["显示注册表单", "信息填写成功", "提交成功", "跳转到首页"]
)

# 创建测试任务
client.create_testtask(
    product_id="1",
    name="Sprint1测试",
    begin="2026-03-20",
    end="2026-03-25"
)

# 查询测试用例
success, cases = client.get_testcases(product_id)
for case in cases:
    print(f"[{case['id']}] {case['title']} - {case['type']}")

# 删除测试用例（软删除）
success, result = client.delete_testcase("10", confirm="yes")

# 验证删除
success, case = client.get_testcase("10")
if case.get('deleted') == '1':
    print("测试用例已删除")

# 获取测试用例详情
success, case_detail = client.get_testcase(case_id)
print(f"标题: {case_detail['title']}")
print(f"类型: {case_detail['type']}")
print(f"优先级: {case_detail['pri']}")
```

---

## 状态流转

### 任务状态流转

```
wait ──开始──→ doing ──完成──→ done ──关闭──→ closed
  │              │    ↑
  │              │    │
  │              ↓    │
  │            pause ─┘
  │              ↑    
  │              └── 继续
  └──取消──→ cancel

done/closed ──激活──→ doing
```

### Bug 状态流转

```
active ──解决──→ resolved ──关闭──→ closed
  ↑                │
  │                │
  └──激活──────────┘
```

---

## 注意事项

### 1. 工时记录是批量接口

```python
# ✅ 正确：一次提交多条记录
client.record_estimate(task_id, [
    {"date": "2026-03-27", "consumed": "2", "left": "6", "work": "开发"},
    {"date": "2026-03-28", "consumed": "3", "left": "3", "work": "测试"}
])

# ❌ 错误：多次调用会覆盖之前记录
```

### 2. 完成任务前先记录工时

```python
# ✅ 正确流程
client.record_estimate(task_id, [
    {"date": today, "consumed": "8", "left": "0", "work": "完成"}
])
client.finish_task(task_id, "开发完成")
```

### 3. 验证操作结果

很多 API 返回 HTML 而非 JSON，建议用查询接口验证：

```python
success, result = client.start_task(task_id)
ok, task = client.get_task_detail(task_id)
print(task['status'])  # 验证是否为 'doing'
```

### 4. 解决 Bug 用专用接口

```python
# ✅ 正确
client.resolve_bug(bug_id, "fixed", "trunk", "已修复")

# ❌ 错误：不要用 edit_bug 修改状态
```

---

## 常见问题

### Q: 认证失败怎么办？

```python
credentials = read_credentials()
print(credentials)  # 检查凭证是否正确

sid = client.get_session()
if not sid:
    print("认证失败，请检查用户名密码")
```

### Q: API 返回 success=False 但操作成功？

禅道老 API 有时返回 HTML 而非 JSON。解决方案：

1. 使用查询接口验证操作结果
2. 检查 `get_task_detail` 或 `get_bug` 的状态

### Q: 工时记录不生效？

确保参数格式正确：
- `date` 必须是 `YYYY-MM-DD` 格式
- `consumed` 和 `left` 必须是字符串

```python
from datetime import datetime
today = datetime.now().strftime("%Y-%m-%d")
```

### Q: 创建子任务失败？

确保参数完整：
```python
tasks = [
    {
        "name": "前端开发",      # 必需
        "estimate": "8",         # 必需
        "assignedTo": "admin",   # 必需
        "type": "devel",         # 可选，默认devel
        "pri": "3"              # 可选，默认3
    }
]
```

---

## 项目结构

```
zentao-api/
├── lib/
│   └── zentao_client.py    # 核心客户端
├── docs/
│   └── 测试报告-工单客服系统.md
├── scripts/                  # 辅助脚本
├── SKILL.md                 # AI助手指南
├── README.md                # 本文件
├── package.json             # npm包配置
└── requirements.txt         # Python依赖
```

---

## 参考资料

- [禅道官网](https://www.zentao.net/)
- [禅道 API 文档 v1](https://zentao.net/book/apidoc-v1/apidoc-v1.html)
- [禅道二次开发手册](https://zentao.net/book/api/c634.html)
- [禅道 21.7 新 API v2.0](https://www.zentao.net/download/pms21.7.8-85834.html)

---

## 许可证

MIT License
