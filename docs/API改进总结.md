# 禅道 API 客户端改进总结

## 1. 测试用例创建接口修复

### 问题
`create_testcase` 方法的 URL 路径参数硬编码为 0：
```python
/testcase-create-{product_id}-0-0-0-0.json
```

### 修复
添加可配置参数：
```python
def create_testcase(
    self,
    product_id: str,
    title: str,
    case_type: str = "feature",
    module: str = "0",      # 模块ID
    story: str = "0",       # 需求ID
    branch: str = "0",      # 分支ID
    **kwargs,
)
```

URL 格式：`/testcase-create-{product_id}-{module}-{story}-{branch}-0.json`

### 增强
支持两种步骤格式：
- **字符串格式**：`steps="步骤1\n步骤2"` 自动按换行分割
- **列表格式**：`steps_list=["步骤1", "步骤2"]` 精确控制

## 2. 其他接口参数修复

共修复 **9个接口** 的硬编码参数：

| 方法 | 新增参数 | URL 格式 |
|------|---------|----------|
| `get_bug_list_old` | `branch` | `/bug-browse-{product}-{branch}-all.json` |
| `get_productplan_list_old` | `branch` | `/productplan-browse-{product}-{branch}-all.json` |
| `get_project_tasks_old` | `module_id`, `limit`, `page` | `/project-task-{project}-{status}-id_desc-{module}-{limit}-{page}.json` |
| `create_story` (第一个) | `module`, `branch` | `/story-create-{product}-{module}-0-{plan}-{execution}-{branch}-{module}-0-story.json` |
| `create_subtasks` | `story_id`, `module_id` | `/task-batchCreate-{execution}-{story}-{module}-{parent}.html` |
| `create_tasks` | `story_id`, `module_id`, `parent_id` | `/task-batchCreate-{project}-{story}-{module}-{parent}.json` |
| `create_testcase` | `module`, `story`, `branch` | `/testcase-create-{product}-{module}-{story}-{branch}-0.json` |
| `create_story` (第二个) | `module`, `plan`, `execution_id`, `branch` | `/story-create-{product}-{module}-0-{plan}-{execution}-{branch}-{module}-0-story.json` |
| `get_testreports` | `project_id` | `/testreport-browse-{product}-product-{project}.json` |

## 3. 从测试用例创建 Bug 功能

### 新增方法：`create_bug_from_testcase`

专门用于从测试用例创建 Bug：

```python
# 方法1: 使用便捷方法
success, result = client.create_bug_from_testcase(
    case_id="8",
    title="登录功能测试发现Bug",
    severity="3",
    pri="3",
    assignedTo="admin"
)

# 方法2: 使用 create_bug + case_id 参数
success, result = client.create_bug(
    product_id="1",
    title="测试发现Bug",
    case_id="8",  # 关联测试用例
    severity="3",
    pri="3",
    assignedTo="admin"
)
```

### 特性
- 自动从测试用例获取产品ID和标题
- 自动将测试用例步骤转换为Bug重现步骤
- 自动关联测试用例（`toBugs` 字段）

### 更新 `create_bug` 方法
添加 `case_id` 参数，支持关联测试用例。

## 4. 测试验证

### 测试文件
- `scripts/test_create_testcase.py` - 测试用例创建测试
- `scripts/test_api_fix.py` - 接口参数修复验证
- `scripts/test_create_bug_from_testcase.py` - 从测试用例创建Bug测试

### 测试结果
✅ 所有接口测试通过
- 创建测试用例：3个成功
- 创建Bug：3个成功，均关联测试用例
- 接口参数修复：9个全部验证通过

## 5. 文档更新

### README.md
- 更新测试用例创建示例，添加列表格式步骤
- 添加从测试用例创建Bug的示例

## 6. 使用示例

### 创建测试用例
```python
# 字符串格式
client.create_testcase(
    product_id="1",
    title="登录功能测试",
    case_type="feature",
    pri="3",
    steps="1.打开登录页\n2.输入账号密码\n3.点击登录",
    expect="登录成功"
)

# 列表格式（精确控制）
client.create_testcase(
    product_id="1",
    title="注册功能测试",
    module="2",
    story="15",
    steps_list=["打开注册页面", "填写用户信息", "点击注册"],
    expects_list=["显示注册表单", "填写成功", "注册成功"]
)
```

### 从测试用例创建Bug
```python
# 简单方式
client.create_bug_from_testcase(
    case_id="8",
    severity="3",
    pri="3"
)

# 完整方式
client.create_bug(
    product_id="1",
    title="发现的Bug",
    case_id="8",
    severity="3",
    pri="3",
    steps="详细步骤",
    assignedTo="admin"
)
```

## 7. 后续建议

### 可继续改进的接口
1. **测试任务相关**：
   - `create_testtask` - 可添加更多参数
   - `link_testcase` - 关联测试用例到测试任务

2. **测试套件相关**：
   - `create_testsuite` - 可添加更多参数

3. **Bug相关**：
   - `edit_bug` - 编辑Bug接口
   - `get_bug_list` - 更灵活的Bug列表查询

### 建议增加的功能
1. **批量操作**：
   - 批量创建测试用例
   - 批量执行测试用例
   - 批量关联测试用例

2. **测试执行**：
   - 执行测试用例
   - 记录测试结果
   - 生成测试报告

3. **统计查询**：
   - 测试用例覆盖率统计
   - Bug统计报表
   - 测试执行进度

## 8. 测试数据

本次测试创建的数据：
- 测试用例：8个（ID: 1-8）
- Bug：5个（ID: 3-5，关联测试用例8）
- 需求：1个（从接口参数测试创建）
