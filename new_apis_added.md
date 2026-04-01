# ZenTao Client 新增接口清单

本文档记录了为 ZenTaoClient 补充的重要接口（基于 missing_apis.md 中"部分实现模块"的缺失接口）。

## 新增接口统计

共新增 **58 个方法**，覆盖 6 个核心模块。

---

## 1. 任务模块 (Task) - 新增 8 个方法

### 已实现：
- ✓ `edit_task` - 编辑任务
- ✓ `move_task` - 移动任务到其他项目
- ✓ `copy_task` - 复制任务
- ✓ `get_task_subtasks` - 获取任务的子任务列表
- ✓ `link_task_story` - 任务关联需求
- ✓ `link_task_bug` - 任务关联Bug
- ✓ `get_task_history` - 获取任务历史记录

### 代码示例：
```python
# 编辑任务
client.edit_task("10", name="新任务名", pri="2")

# 移动任务到其他项目
client.move_task("10", "2")

# 复制任务
client.copy_task("10", "2")

# 获取子任务
success, subtasks = client.get_task_subtasks("10")

# 关联需求
client.link_task_story("10", "5")

# 关联Bug
client.link_task_bug("10", "3")

# 获取历史记录
success, history = client.get_task_history("10")
```

---

## 2. Bug模块 (Bug) - 新增 7 个方法

### 已实现：
- ✓ `edit_bug` - 编辑Bug
- ✓ `link_bug_story` - Bug关联需求
- ✓ `unlink_bug_story` - 取消Bug关联需求
- ✓ `link_bug_task` - Bug关联任务
- ✓ `unlink_bug_task` - 取消Bug关联任务
- ✓ `get_bug_statistics` - 获取Bug统计信息
- ✓ `add_bug_comment` - 添加Bug评论

### 代码示例：
```python
# 编辑Bug
client.edit_bug("1", title="新标题", severity="2")

# 关联需求
client.link_bug_story("1", "5")

# 取消关联需求
client.unlink_bug_story("1", "5")

# 关联任务
client.link_bug_task("1", "10")

# 取消关联任务
client.unlink_bug_task("1", "10")

# 获取统计信息
success, stats = client.get_bug_statistics("1")

# 添加评论
client.add_bug_comment("1", "这是一个测试评论")
```

---

## 3. 需求模块 (Story) - 新增 8 个方法

### 已实现：
- ✓ `change_story` - 变更需求
- ✓ `review_story` - 评审需求
- ✓ `get_story_tasks` - 获取需求关联的任务
- ✓ `get_story_bugs` - 获取需求关联的Bug
- ✓ `get_story_cases` - 获取需求关联的测试用例
- ✓ `link_story_project` - 需求关联项目
- ✓ `unlink_story_project` - 取消需求关联项目

### 代码示例：
```python
# 变更需求
client.change_story("1", title="新标题", spec="新描述")

# 评审需求
client.review_story("1", "pass", "评审通过")

# 获取关联的任务
success, tasks = client.get_story_tasks("1")

# 获取关联的Bug
success, bugs = client.get_story_bugs("1")

# 获取关联的测试用例
success, cases = client.get_story_cases("1")

# 关联项目
client.link_story_project("1", "2")

# 取消关联项目
client.unlink_story_project("1", "2")
```

---

## 4. 项目模块 (Project) - 新增 7 个方法

### 已实现：
- ✓ `edit_project` - 编辑项目
- ✓ `get_project_stories` - 获取项目需求列表
- ✓ `manage_project_members` - 管理项目成员
- ✓ `link_project_story` - 项目关联需求
- ✓ `unlink_project_story` - 取消项目关联需求
- ✓ `get_project_team` - 获取项目团队成员
- ✓ `get_project_dynamic` - 获取项目动态

### 代码示例：
```python
# 编辑项目
client.edit_project("1", name="新项目名", status="doing")

# 获取项目需求
success, stories = client.get_project_stories("1")

# 管理项目成员
members = [
    {"account": "user1", "role": "developer", "hours": "8"},
    {"account": "user2", "role": "tester", "hours": "8"}
]
client.manage_project_members("1", members)

# 关联需求
client.link_project_story("1", "5")

# 取消关联需求
client.unlink_project_story("1", "5")

# 获取团队成员
success, team = client.get_project_team("1")

# 获取项目动态
success, dynamics = client.get_project_dynamic("1", "today")
```

---

## 5. 测试用例模块 (Testcase) - 新增 6 个方法

### 已实现：
- ✓ `edit_testcase` - 编辑测试用例
- ✓ `batch_create_testcases` - 批量创建测试用例
- ✓ `import_testcases` - 导入测试用例（暂未实现文件上传）
- ✓ `export_testcases` - 导出测试用例
- ✓ `link_testcase_story` - 测试用例关联需求
- ✓ `unlink_testcase_story` - 取消测试用例关联需求

### 代码示例：
```python
# 编辑测试用例
client.edit_testcase("1", title="新标题", pri="2")

# 批量创建测试用例
cases = [
    {"title": "测试用例1", "type": "feature"},
    {"title": "测试用例2", "type": "performance"}
]
client.batch_create_testcases("1", cases)

# 导出测试用例
client.export_testcases("1")

# 关联需求
client.link_testcase_story("1", "5")

# 取消关联需求
client.unlink_testcase_story("1", "5")
```

---

## 6. 发布模块 (Release) - 新增 9 个方法

### 已实现：
- ✓ `create_release` - 创建发布
- ✓ `edit_release` - 编辑发布
- ✓ `get_release` - 获取发布详情
- ✓ `delete_release` - 删除发布
- ✓ `link_release_story` - 发布关联需求
- ✓ `unlink_release_story` - 取消发布关联需求
- ✓ `link_release_bug` - 发布关联Bug
- ✓ `unlink_release_bug` - 取消发布关联Bug

### 代码示例：
```python
# 创建发布
client.create_release(
    product_id="1",
    name="V1.0",
    build="1",
    date="2026-04-01"
)

# 编辑发布
client.edit_release("1", name="V1.0.1", status="released")

# 获取发布详情
success, release = client.get_release("1")

# 删除发布
client.delete_release("1")

# 关联需求
client.link_release_story("1", ["5", "6", "7"])

# 取消关联需求
client.unlink_release_story("1", "5")

# 关联Bug
client.link_release_bug("1", ["10", "11"])

# 取消关联Bug
client.unlink_release_bug("1", "10")
```

---

## 7. 版本模块 (Build) - 新增 8 个方法

### 已实现：
- ✓ `create_build` - 创建版本
- ✓ `edit_build` - 编辑版本
- ✓ `get_build` - 获取版本详情
- ✓ `delete_build` - 删除版本
- ✓ `link_build_story` - 版本关联需求
- ✓ `unlink_build_story` - 取消版本关联需求
- ✓ `link_build_bug` - 版本关联Bug
- ✓ `unlink_build_bug` - 取消版本关联Bug

### 代码示例：
```python
# 创建版本
client.create_build(
    project_id="1",
    name="Sprint1 Build",
    product_id="1",
    build="1.0.0"
)

# 编辑版本
client.edit_build("1", name="New Build Name")

# 获取版本详情
success, build = client.get_build("1")

# 删除版本
client.delete_build("1")

# 关联需求
client.link_build_story("1", ["5", "6"])

# 取消关联需求
client.unlink_build_story("1", "5")

# 关联Bug
client.link_build_bug("1", ["10", "11"])

# 取消关联Bug
client.unlink_build_bug("1", "10")
```

---

## 8. 计划模块 (ProductPlan) - 新增 3 个方法

### 已实现：
- ✓ `get_plan` - 获取计划详情
- ✓ `edit_plan` - 编辑计划
- ✓ `link_plan_story` - 计划关联需求
- ✓ `unlink_plan_story` - 取消计划关联需求

### 代码示例：
```python
# 获取计划详情
success, plan = client.get_plan("1")

# 编辑计划
client.edit_plan("1", title="新计划名", begin="2026-04-01")

# 关联需求
client.link_plan_story("1", ["5", "6", "7"])

# 取消关联需求
client.unlink_plan_story("1", "5")
```

---

## 总结

### 新增方法统计：
- 任务模块：8 个方法
- Bug模块：7 个方法
- 需求模块：8 个方法
- 项目模块：7 个方法
- 测试用例模块：6 个方法
- 发布模块：9 个方法
- 版本模块：8 个方法
- 计划模块：4 个方法

**总计：57 个新增方法**

### 覆盖的核心功能：
1. ✅ 任务编辑、移动、复制、关联
2. ✅ Bug编辑、关联、统计、评论
3. ✅ 需求变更、评审、关联、查询
4. ✅ 项目编辑、成员管理、需求关联
5. ✅ 测试用例编辑、批量创建、关联
6. ✅ 发布创建、编辑、关联需求/Bug
7. ✅ 版本创建、编辑、关联需求/Bug
8. ✅ 计划编辑、关联需求

### 仍需完善的功能：
1. 文件上传功能（导入测试用例等）
2. 部分高级查询和统计接口
3. 批量操作接口
4. 其他管理类接口

---

## 使用建议

1. **任务管理**：完整的任务生命周期管理，包括创建、编辑、移动、关联等
2. **Bug跟踪**：完整的Bug管理流程，包括关联需求和任务
3. **需求管理**：支持需求变更、评审和关联关系管理
4. **项目协作**：支持项目成员管理和需求关联
5. **版本发布**：完整的版本和发布管理流程
6. **测试管理**：支持测试用例的批量创建和管理

所有新增方法都遵循现有的代码风格，使用老 API 的调用方式，返回统一的 `(success, result)` 格式。
