# ZenTao Client 缺少的 API 接口清单

对比 `docs/` 目录下的 API 文档和 `lib/zentao_client.py` 的实现，列出缺少的接口。

## 统计信息
- docs 中共有 **59 个模块**，约 **800+ 个 API 接口**
- zentao_client.py 已实现约 **80 个方法**

---

## 1. 首页模块 (index.md) - 完全缺失
- [ ] GET `/index.json` - 获取禅道系统首页数据
- [ ] GET `/index-testext.json` - 测试扩展引擎

---

## 2. 我的模块 (my.md) - 大部分缺失
已实现：
- ✓ get_my_tasks - 我的任务
- ✓ get_my_bugs - 我的Bug
- ✓ get_my_stories - 我的需求
- ✓ get_my_projects - 我的项目

缺少：
- [ ] GET `/my.json` - 首页，跳转到待办
- [ ] GET `/my-score-[recTotal]-[recPerPage]-[pageID].json` - 积分列表
- [ ] GET `/my-calendar.json` - 日历视图
- [ ] GET `/my-todo-[type]-[account]-[status]-[recTotal]-[recPerPage]-[pageID].json` - 我的待办
- [ ] GET `/my-testtask.json` - 我的测试版本
- [ ] GET `/my-testcase-[type]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 我的测试用例
- [ ] GET/POST `/my-editProfile.json` - 编辑个人资料
- [ ] GET/POST `/my-changePassword.json` - 修改密码
- [ ] GET/POST `/my-manageContacts-[listID]-[mode].json` - 管理联系人
- [ ] GET `/my-deleteContacts-[listID]-[confirm].json` - 删除联系人
- [ ] GET `/my-buildContactLists.json` - 构建联系人列表
- [ ] GET `/my-profile.json` - 查看个人资料
- [ ] GET `/my-dynamic-[type]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 我的动态
- [ ] GET `/my-unbind-[confirm].json` - 解除绑定

---

## 3. 待办模块 (todo.md) - 完全缺失
- [ ] GET/POST `/todo-create-[date]-[account].json` - 创建待办
- [ ] GET/POST `/todo-batchCreate-[date]-[account].json` - 批量创建待办
- [ ] GET/POST `/todo-edit-[todoID].json` - 编辑待办
- [ ] GET/POST `/todo-batchEdit-[from]-[type]-[account]-[status].json` - 批量编辑待办
- [ ] GET `/todo-activate.json` - 激活待办
- [ ] GET `/todo-close.json` - 关闭待办
- [ ] GET/POST `/todo-assignTo.json` - 分配待办
- [ ] GET `/todo-view-[todoID]-[from].json` - 查看待办
- [ ] GET `/todo-delete-[todoID]-[confirm].json` - 删除待办
- [ ] GET `/todo-finish-[todoID].json` - 完成待办
- [ ] GET/POST `/todo-batchFinish.json` - 批量完成待办
- [ ] GET/POST `/todo-batchClose.json` - 批量关闭待办
- [ ] GET/POST `/todo-import2Today.json` - 导入到今天
- [ ] GET/POST `/todo-export-[productID]-[orderBy].json` - 导出待办
- [ ] GET `/todo-ajaxGetDetail-[todoID].json` - 获取待办详情
- [ ] GET `/todo-createCycle.json` - 创建循环待办

---

## 4. 分支模块 (branch.md) - 完全缺失
- [ ] GET/POST `/branch-manage-[productID].json` - 管理分支
- [ ] GET `/branch-sort.json` - 排序分支
- [ ] GET `/branch-ajaxGetDropMenu-[productID]-[module]-[method]-[extra].json` - 获取下拉菜单
- [ ] GET `/branch-delete-[branchID]-[confirm].json` - 删除分支
- [ ] GET `/branch-ajaxGetBranches-[productID]-[oldBranch].json` - 获取分支列表

---

## 5. 产品模块 (product.md) - 部分缺失
已实现：
- ✓ get_product_list_old - 产品列表
- ✓ get_products - 所有产品
- ✓ get_product - 产品详情
- ✓ create_product - 创建产品
- ✓ edit_product - 编辑产品
- ✓ close_product - 关闭产品
- ✓ delete_product - 删除产品

缺少：
- [ ] GET `/product-index-[locate]-[productID]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 产品列表页
- [ ] GET `/product-project-[status]-[productID].json` - 项目列表
- [ ] GET `/product-browse-[productID]-[browseType]-[param]-[storyType]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 浏览产品
- [ ] GET `/product-roadmap-[productID].json` - 产品路线图
- [ ] GET `/product-dynamic-[type]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 产品动态
- [ ] GET `/product-ajaxGetProjects-[productID]-[projectID]-[number].json` - AJAX获取项目
- [ ] GET `/product-ajaxGetPlans-[productID]-[planID]-[needCreate]-[expired].json` - AJAX获取计划
- [ ] GET/POST `/product-updateOrder.json` - 更新排序
- [ ] GET/POST `/product-export-[status]-[orderBy].json` - 导出产品

---

## 6. 发布模块 (release.md) - 大部分缺失
已实现：
- ✓ get_releases - 发布列表

缺少：
- [ ] GET `/release-commonAction-[productID]-[branch].json` - 通用操作
- [ ] GET/POST `/release-create-[productID]-[branch].json` - 创建发布
- [ ] GET/POST `/release-edit-[releaseID].json` - 编辑发布
- [ ] GET `/release-view-[releaseID]-[type]-[link]-[param]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 查看发布
- [ ] GET `/release-delete-[releaseID]-[confirm].json` - 删除发布
- [ ] GET/POST `/release-export.json` - 导出发布
- [ ] GET/POST `/release-linkStory-[releaseID]-[browseType]-[param]-[recTotal]-[recPerPage]-[pageID].json` - 关联需求
- [ ] GET `/release-unlinkStory-[releaseID]-[storyID].json` - 取消关联需求
- [ ] GET `/release-batchUnlinkStory-[releaseID].json` - 批量取消关联需求
- [ ] GET/POST `/release-linkBug-[releaseID]-[browseType]-[param]-[type]-[recTotal]-[recPerPage]-[pageID].json` - 关联Bug
- [ ] GET `/release-unlinkBug-[releaseID]-[bugID]-[type].json` - 取消关联Bug
- [ ] GET `/release-batchUnlinkBug-[releaseID]-[type].json` - 批量取消关联Bug
- [ ] GET `/release-changeStatus-[releaseID]-[status].json` - 更改状态

---

## 7. 版本模块 (build.md) - 完全缺失
- [ ] GET/POST `/build-create-[projectID]-[productID].json` - 创建版本
- [ ] GET/POST `/build-edit-[buildID].json` - 编辑版本
- [ ] GET `/build-view-[buildID]-[type]-[link]-[param]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 查看版本
- [ ] GET `/build-delete-[buildID]-[confirm].json` - 删除版本
- [ ] GET `/build-ajaxGetProductBuilds-[productID]-[varName]-[build]-[branch]-[index]-[type].json` - 获取产品版本列表
- [ ] GET `/build-ajaxGetProjectBuilds-[projectID]-[varName]-[build]-[branch]-[index]-[needCreate]-[type].json` - 获取项目版本列表
- [ ] GET/POST `/build-linkStory-[buildID]-[browseType]-[param]-[recTotal]-[recPerPage]-[pageID].json` - 关联需求
- [ ] GET `/build-unlinkStory-[storyID]-[confirm].json` - 取消关联需求
- [ ] GET `/build-batchUnlinkStory-[confirm].json` - 批量取消关联需求
- [ ] GET/POST `/build-linkBug-[buildID]-[browseType]-[param]-[recTotal]-[recPerPage]-[pageID].json` - 关联Bug
- [ ] GET `/build-unlinkBug-[buildID]-[bugID].json` - 取消关联Bug
- [ ] GET `/build-batchUnlinkBug-[buildID].json` - 批量取消关联Bug

---

## 8. 用户模块 (user.md) - 完全缺失
- [ ] GET `/user-view-[account].json` - 查看用户
- [ ] GET `/user-todo-[account]-[type]-[status]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 用户待办
- [ ] GET `/user-story-[account]-[type]-[recTotal]-[recPerPage]-[pageID].json` - 用户需求
- [ ] GET `/user-task-[account]-[type]-[recTotal]-[recPerPage]-[pageID].json` - 用户任务
- [ ] GET `/user-bug-[account]-[type]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 用户Bug
- [ ] GET/POST `/user-create-[deptID].json` - 创建用户
- [ ] GET/POST `/user-edit-[userID].json` - 编辑用户
- [ ] GET/POST `/user-delete-[userID]-[confirm].json` - 删除用户
- [ ] GET `/user-logout.json` - 用户登出
- [ ] GET/POST `/user-reset.json` - 重置密码
- [ ] GET/POST `/user-manage.json` - 管理账户
- [ ] GET/POST `/user-link2Company.json` - 关联公司
- [ ] GET/POST `/user-link2Dept.json` - 关联部门
- [ ] GET/POST `/user-link2Group.json` - 关联角色
- [ ] GET/POST `/user-link2Project.json` - 关联项目
- [ ] GET/POST `/user-link2Product.json` - 关联产品
- [ ] GET/POST `/user-linkTestProject.json` - 关联测试项目
- [ ] GET/POST `/user-linkTestProduct.json` - 关联测试产品
- [ ] GET/POST `/user-save.json` - 保存用户信息
- [ ] GET/POST `/user-validateEmail.json` - 验证邮箱
- [ ] GET/POST `/user-validateMobile.json` - 验证手机号
- [ ] GET/POST `/user-unlink.json` - 解除关联
- [ ] GET/POST `/user-savePrivilege.json` - 保存权限
- [ ] GET `/user-getPrivilege.json` - 获取权限
- [ ] GET `/user-getView.json` - 获取视图
- [ ] GET/POST `/user-saveView.json` - 保存视图
- [ ] GET/POST `/user-saveConfig.json` - 保存偏好设置
- [ ] GET `/user-getConfig.json` - 获取偏好设置
- [ ] GET/POST `/user-saveAPIKey.json` - 保存API密钥
- [ ] GET `/user-getAPIKey.json` - 获取API密钥
- [ ] GET/POST `/user-saveAPIConfig.json` - 保存API配置
- [ ] GET `/user-getAPIConfig.json` - 获取API配置

---

## 9. 项目模块 (project.md) - 大部分缺失
已实现：
- ✓ get_project_list_old - 项目列表
- ✓ get_project - 项目详情
- ✓ create_project - 创建项目
- ✓ start_project - 开始项目
- ✓ close_project - 关闭项目
- ✓ get_project_tasks_old - 项目任务列表
- ✓ get_project_bugs - 项目Bug列表

缺少：
- [ ] GET `/project-index-[locate]-[status]-[projectID].json` - 项目首页
- [ ] GET `/project-browse-[projectID].json` - 浏览项目
- [ ] GET `/project-grouptask-[projectID]-[groupBy].json` - 分组任务
- [ ] GET `/project-story-[projectID]-[orderBy].json` - 项目需求
- [ ] GET `/project-burn-[projectID]-[type]-[interval].json` - 项目燃尽图
- [ ] GET/POST `/project-edit-[projectID]-[action]-[extra].json` - 编辑项目
- [ ] GET `/project-kanban-[projectID]-[type]-[orderBy].json` - 项目看板视图
- [ ] GET/POST `/project-manageMembers-[projectID]-[team2Import].json` - 管理项目成员
- [ ] GET/POST `/project-linkStory-[projectID].json` - 关联需求
- [ ] GET `/project-unlinkStory-[projectID]-[storyID].json` - 移除需求
- [ ] GET `/project-batchUnlinkStory-[projectID].json` - 批量移除需求
- [ ] GET `/project-progress-[projectID].json` - 项目进度
- [ ] GET `/project-dynamic-[projectID]-[type]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 项目动态
- [ ] GET `/project-statistic-[projectID]-[by]-[type].json` - 项目统计
- [ ] GET `/project-report-[projectID]-[reportType].json` - 项目报表
- [ ] GET `/project-gantt-[projectID].json` - 项目甘特图
- [ ] GET `/project-risk-[projectID].json` - 项目风险
- [ ] GET `/project-team-[projectID].json` - 项目团队
- [ ] GET `/project-milestone-[projectID].json` - 项目里程碑
- [ ] GET `/project-budget-[projectID].json` - 项目预算
- [ ] GET `/project-document-[projectID].json` - 项目文档
- [ ] GET `/project-attachment-[projectID].json` - 项目附件
- [ ] GET `/project-approval-[projectID].json` - 项目审批

---

## 10. 任务模块 (task.md) - 部分缺失
已实现：
- ✓ get_project_tasks_old - 项目任务列表
- ✓ get_task_detail - 任务详情
- ✓ create_task - 创建任务
- ✓ create_tasks - 批量创建任务
- ✓ create_subtasks - 创建子任务
- ✓ delete_task - 删除任务
- ✓ cancel_task - 取消任务
- ✓ close_task - 关闭任务
- ✓ start_task - 开始任务
- ✓ finish_task - 完成任务
- ✓ pause_task - 暂停任务
- ✓ restart_task - 继续任务
- ✓ activate_task - 激活任务
- ✓ assign_task - 指派任务
- ✓ record_estimate - 记录工时
- ✓ get_estimate - 获取工时详情
- ✓ edit_estimate - 编辑工时
- ✓ delete_estimate - 删除工时

缺少：
- [ ] GET/POST `/task-edit-[taskID].json` - 编辑任务（部分通过 start_task 实现）
- [ ] GET `/task-view-[taskID].json` - 查看任务（已通过 get_task_detail 实现）
- [ ] GET/POST `/task-resume-[taskID].json` - 恢复任务（与 restart_task 功能类似）
- [ ] GET/POST `/task-move-[taskID]-[projectID].json` - 移动任务
- [ ] GET/POST `/task-copy-[taskID]-[projectID].json` - 复制任务
- [ ] GET `/task-viewSubtasks-[taskID].json` - 查看子任务
- [ ] GET/POST `/task-linkStory-[taskID]-[storyID].json` - 任务关联需求
- [ ] GET/POST `/task-linkBug-[taskID]-[bugID].json` - 任务关联Bug
- [ ] GET/POST `/task-linkDoc-[taskID]-[docID].json` - 任务关联文档
- [ ] GET `/task-history-[taskID].json` - 任务历史记录
- [ ] GET `/task-log-[taskID].json` - 任务日志
- [ ] GET/POST `/task-progress-[taskID].json` - 任务进度更新
- [ ] GET/POST `/task-priority-[taskID].json` - 任务优先级
- [ ] GET/POST `/task-tags-[taskID].json` - 任务标签
- [ ] GET/POST `/task-assignTeam-[taskID].json` - 任务分配给团队
- [ ] GET/POST `/task-moveToSprint-[taskID]-[sprintID].json` - 任务移动到迭代
- [ ] GET `/task-swimlane-[projectID].json` - 任务泳道视图

---

## 11. Bug模块 (bug.md) - 部分缺失
已实现：
- ✓ get_bug_list_old - Bug列表
- ✓ get_bug - Bug详情
- ✓ create_bug - 创建Bug
- ✓ create_bug_from_testcase - 从测试用例创建Bug
- ✓ resolve_bug - 解决Bug
- ✓ close_bug - 关闭Bug
- ✓ activate_bug - 激活Bug
- ✓ assign_bug - 指派Bug
- ✓ confirm_bug - 确认Bug
- ✓ delete_bug - 删除Bug

缺少：
- [ ] GET `/bug.json` - Bug首页
- [ ] GET/POST `/bug-edit-[bugID].json` - 编辑Bug
- [ ] GET `/bug-browse-[productID]-[branch]-[browseType]-[param]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 浏览Bug（已通过 get_bug_list_old 部分实现）
- [ ] GET/POST `/bug-linkStory-[bugID]-[storyID].json` - 关联需求
- [ ] GET `/bug-unlinkStory-[bugID]-[storyID].json` - 移除关联需求
- [ ] GET `/bug-batchUnlinkStory-[bugID].json` - 批量移除关联需求
- [ ] GET/POST `/bug-linkTask-[bugID]-[taskID].json` - 关联任务
- [ ] GET `/bug-unlinkTask-[bugID]-[taskID].json` - 移除关联任务
- [ ] GET `/bug-batchUnlinkTask-[bugID].json` - 批量移除关联任务
- [ ] GET/POST `/bug-linkBuild-[bugID]-[buildID].json` - 关联版本
- [ ] GET `/bug-unlinkBuild-[bugID]-[buildID].json` - 移除关联版本
- [ ] GET `/bug-batchUnlinkBuild-[bugID].json` - 批量移除关联版本
- [ ] GET/POST `/bug-changeStatus-[bugID]-[status].json` - 更新Bug状态
- [ ] GET `/bug-statistic-[productID]-[branch].json` - Bug统计
- [ ] GET `/bug-trend-[productID]-[type].json` - Bug趋势分析
- [ ] GET/POST `/bug-export.json` - Bug报告导出
- [ ] GET `/bug-priority-[productID].json` - Bug优先级分析
- [ ] GET `/bug-severity-[productID].json` - Bug严重性分析
- [ ] GET `/bug-resolutionTime-[productID].json` - Bug处理时间分析
- [ ] GET `/bug-duplicate-[bugID].json` - Bug重复检测
- [ ] GET `/bug-attachment-[bugID].json` - Bug附件管理
- [ ] GET `/bug-comment-[bugID].json` - Bug评论管理
- [ ] GET/POST `/bug-addComment-[bugID].json` - 添加Bug评论

---

## 12. 需求模块 (story.md) - 部分缺失
已实现：
- ✓ create_story - 创建需求
- ✓ get_story - 需求详情
- ✓ edit_story - 编辑需求
- ✓ close_story - 关闭需求
- ✓ activate_story - 激活需求
- ✓ delete_story - 删除需求

缺少：
- [ ] GET `/story-view-[storyID]-[version].json` - 查看需求（带版本）
- [ ] GET/POST `/story-change-[storyID].json` - 变更需求
- [ ] GET/POST `/story-review-[storyID].json` - 评审需求
- [ ] GET `/story-tasks-[storyID]-[projectID].json` - 需求关联任务
- [ ] GET `/story-bugs-[storyID].json` - 需求关联Bug
- [ ] GET `/story-cases-[storyID].json` - 需求关联测试用例
- [ ] GET `/story-history-[storyID].json` - 需求变更记录
- [ ] GET/POST `/story-comment-[storyID].json` - 需求评论
- [ ] GET/POST `/story-linkStory-[storyID]-[targetStoryID].json` - 关联需求
- [ ] GET `/story-unlinkStory-[storyID]-[targetStoryID].json` - 移除关联需求
- [ ] GET `/story-batchUnlinkStory-[storyID].json` - 批量移除关联需求
- [ ] GET/POST `/story-linkRelease-[storyID]-[releaseID].json` - 需求关联发布
- [ ] GET `/story-unlinkRelease-[storyID]-[releaseID].json` - 移除关联发布
- [ ] GET/POST `/story-priority-[storyID].json` - 需求优先级
- [ ] GET/POST `/story-estimate-[storyID].json` - 需求估算
- [ ] GET/POST `/story-flow-[storyID].json` - 需求状态流程
- [ ] GET/POST `/story-createChild-[storyID].json` - 需求创建子需求
- [ ] GET `/story-viewChildren-[storyID].json` - 查看子需求
- [ ] GET `/story-statistic-[productID]-[type].json` - 需求统计
- [ ] GET `/story-trend-[productID].json` - 需求趋势分析
- [ ] GET/POST `/story-export-[productID]-[type].json` - 需求导出
- [ ] GET `/story-attachment-[storyID].json` - 需求附件
- [ ] GET/POST `/story-linkProject-[storyID]-[projectID].json` - 关联项目
- [ ] GET `/story-unlinkProject-[storyID]-[projectID].json` - 移除关联项目
- [ ] GET/POST `/story-tags-[storyID].json` - 需求标签

---

## 13. 测试套件模块 (testsuite.md) - 部分缺失
已实现：
- ✓ get_testsuites - 测试套件列表
- ✓ get_testsuite - 测试套件详情
- ✓ create_testsuite - 创建测试套件
- ✓ delete_testsuite - 删除测试套件

缺少：
- [ ] GET `/testsuite.json` - 测试套件首页
- [ ] GET `/testsuite-browse-[productID]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 浏览测试套件
- [ ] GET/POST `/testsuite-edit-[suiteID].json` - 编辑测试套件
- [ ] GET/POST `/testsuite-linkCase-[suiteID]-[param]-[recTotal]-[recPerPage]-[pageID].json` - 关联测试用例
- [ ] GET `/testsuite-unlinkCase-[suiteID]-[rowID]-[confirm].json` - 移除测试用例
- [ ] GET/POST `/testsuite-batchUnlinkCases-[suiteID].json` - 批量移除测试用例

---

## 14. 文档模块 (doc.md) - 完全缺失
- [ ] GET `/doc.json` - 文档首页
- [ ] GET/POST `/doc-browse-[libID]-[moduleID]-[productID]-[projectID]-[orderBy]-[recTotal]-[recPerPage]-[pageID].json` - 浏览文档
- [ ] GET/POST `/doc-createLib-[type]-[objectID].json` - 创建文档库
- [ ] GET/POST `/doc-create-[libID]-[moduleID]-[productID]-[projectID]-[from].json` - 创建文档
- [ ] GET/POST `/doc-edit-[docID].json` - 编辑文档
- [ ] GET `/doc-view-[docID].json` - 查看文档
- [ ] GET `/doc-delete-[docID]-[confirm].json` - 删除文档
- [ ] GET/POST `/doc-version-[docID].json` - 文档版本管理
- [ ] GET `/doc-history-[docID].json` - 文档历史版本
- [ ] GET/POST `/doc-export-[docID]-[format].json` - 文档导出
- [ ] GET `/doc-search-[keyword]-[type].json` - 文档搜索
- [ ] GET `/doc-statistic-[libID].json` - 文档统计
- [ ] GET/POST `/doc-permission-[docID].json` - 文档权限设置
- [ ] GET/POST `/doc-comment-[docID].json` - 文档评论
- [ ] GET `/doc-attachment-[docID].json` - 文档附件
- [ ] GET/POST `/doc-tags-[docID].json` - 文档标签
- [ ] GET `/doc-category-[libID].json` - 文档分类
- [ ] GET `/doc-template-[type].json` - 文档模板
- [ ] GET/POST `/doc-batchAction-[action].json` - 文档批量操作
- [ ] GET `/doc-toc-[libID].json` - 文档目录结构
- [ ] GET `/doc-ref-[docID].json` - 文档引用关系

---

## 15. 部门模块 (dept.md) - 完全缺失
- [ ] GET `/dept-browse-[deptID].json` - 浏览部门
- [ ] GET/POST `/dept-updateOrder.json` - 更新部门排序
- [ ] GET/POST `/dept-manageChild.json` - 管理子部门
- [ ] GET/POST `/dept-edit-[deptID].json` - 编辑部门
- [ ] GET `/dept-delete-[deptID]-[confirm].json` - 删除部门
- [ ] GET `/dept-ajaxGetUsers-[dept]-[user].json` - AJAX获取用户列表
- [ ] GET/POST `/dept-createChild.json` - 创建子部门
- [ ] GET/POST `/dept-move-[deptID]-[parentDeptID].json` - 移动部门
- [ ] GET `/dept-statistic-[deptID].json` - 部门统计
- [ ] GET `/dept-tree.json` - 部门树结构
- [ ] GET/POST `/dept-setManager-[deptID]-[userID].json` - 部门负责人设置
- [ ] GET/POST `/dept-members-[deptID].json` - 部门成员管理
- [ ] GET/POST `/dept-permission-[deptID].json` - 部门权限设置
- [ ] GET/POST `/dept-budget-[deptID].json` - 部门预算设置

---

## 16. API接口模块 (api.md) - 大部分缺失
已实现：
- ✓ get_session - 获取会话ID
- ✓ old_request - 通用API请求方法

缺少：
- [ ] GET `/api-getModel-[moduleName]-[methodName]-[params].json` - 执行模块方法
- [ ] GET/POST `/api-debug-[filePath]-[action].json` - API调试接口
- [ ] GET/POST `/api-sql-[keyField].json` - 查询SQL
- [ ] GET `/api-version.json` - API版本信息
- [ ] GET `/api-doc-[module].json` - API文档
- [ ] GET `/api-checkPermission-[module]-[method].json` - API权限检查
- [ ] GET `/api-log-[date].json` - API日志
- [ ] GET `/api-statistic-[period].json` - API统计
- [ ] GET/POST `/api-rateLimit-[module]-[method].json` - API限流配置
- [ ] GET/POST `/api-cache-[module]-[method].json` - API缓存设置
- [ ] GET/POST `/api-test.json` - API测试工具
- [ ] GET `/api-auth.json` - API认证信息
- [ ] GET/POST `/api-key.json` - API密钥管理
- [ ] GET `/api-errorCodes.json` - API错误码
- [ ] GET `/api-example-[module]-[method].json` - API示例

---

## 17-59. 其他模块 - 完全缺失

以下模块在 docs 中存在，但在 zentao_client.py 中完全缺失：

### 17. webhook.md - WebHook模块（全部缺失）
### 18. cron.md - 定时任务模块（全部缺失）
### 19. block.md - 区块模块（全部缺失）
### 20. tutorial.md - 新手教程模块（全部缺失）
### 21. jenkins.md - Jenkins模块（全部缺失）
### 22. compile.md - 编译模块（全部缺失）
### 23. productplan.md - 产品计划模块（部分实现，缺少编辑、查看、关联需求等）
### 24. qa.md - 测试QA模块（全部缺失）
### 25. testcase.md - 测试用例模块（部分实现，缺少编辑、批量创建、导入导出等）
### 26. testtask.md - 测试版本模块（部分实现，缺少关联测试用例、报告等）
### 27. testreport.md - 测试报告模块（部分实现，缺少创建、编辑、查看、导出等）
### 28. group.md - 用户组模块（全部缺失）
### 29. company.md - 公司模块（全部缺失）
### 30. svn.md - SVN模块（全部缺失）
### 31. repo.md - 代码仓库模块（全部缺失）
### 32. git.md - GIT模块（全部缺失）
### 33. entry.md - 应用模块（全部缺失）
### 34. im.md - 即时通讯模块（全部缺失）
### 35. mail.md - 邮箱模块（全部缺失）
### 36. message.md - 消息模块（全部缺失）
### 37. action.md - 系统日志模块（全部缺失）
### 38. admin.md - 后台管理模块（全部缺失）
### 39. backup.md - 备份模块（全部缺失）
### 40. convert.md - 导入模块（全部缺失）
### 41. custom.md - 自定义模块（全部缺失）
### 42. dev.md - 二次开发模块（全部缺失）
### 43. extension.md - 插件模块（全部缺失）
### 44. score.md - 积分模块（全部缺失）
### 45. file.md - 附件模块（全部缺失）
### 46. search.md - 搜索模块（全部缺失）
### 47. datatable.md - 数据表格模块（全部缺失）
### 48. report.md - 统计报表模块（全部缺失）
### 49. install.md - 安装模块（全部缺失）
### 50. tree.md - 模块关系模块（全部缺失）
### 51. sso.md - 单点登录模块（全部缺失）
### 52. upgrade.md - 更新模块（全部缺失）
### 53. caselib.md - 用例库模块（全部缺失）
### 54. ci.md - 持续集成模块（全部缺失）
### 55. client.md - 客户端模块（全部缺失）
### 56. job.md - 任务调度模块（全部缺失）
### 57. license.md - 授权许可模块（全部缺失）
### 58. misc.md - 杂项模块（全部缺失）
### 59. owt.md - OWT模块（全部缺失）

---

## 优先级建议

### 高优先级（核心功能缺失）
1. **任务模块** - 缺少移动、复制、关联等操作
2. **Bug模块** - 缺少编辑、关联、统计、导出等
3. **需求模块** - 缺少变更、评审、关联、统计等
4. **项目模块** - 缺少编辑、成员管理、需求关联等
5. **测试用例模块** - 缺少编辑、批量创建、导入导出等
6. **用户模块** - 完全缺失（用户管理是核心功能）
7. **文档模块** - 完全缺失（文档管理是常用功能）
8. **搜索模块** - 完全缺失（全局搜索很重要）

### 中优先级（常用功能）
1. **待办模块** - 完全缺失
2. **版本模块** - 完全缺失
3. **发布模块** - 大部分缺失
4. **测试版本模块** - 部分缺失
5. **测试报告模块** - 部分缺失
6. **部门模块** - 完全缺失
7. **附件模块** - 完全缺失
8. **模块关系模块** - 完全缺失

### 低优先级（管理功能）
1. **后台管理模块** - 完全缺失
2. **用户组模块** - 完全缺失
3. **权限管理** - 完全缺失
4. **备份模块** - 完全缺失
5. **插件模块** - 完全缺失
6. **WebHook模块** - 完全缺失
7. **定时任务模块** - 完全缺失
8. **其他管理类模块** - 完全缺失
