# TriMate 耐力教练能力包

这个目录只保留可公开的教练能力内容：

- `agent.md`：智能体身份和总规则。
- `skills/`：教练技能。
- `docs/`：随 agent 发布的能力说明。

核心技能包括：

- `runner-assessment`
- `body-assessment`
- `training-memory`
- `workout-feedback`
- `training-load`
- `injury-risk`
- `periodic-training-summary`
- `weekly-review`
- `training-plan`

`body-assessment` 专门处理“当前是否进步、是否过载、还能不能加量”等完整状态评估；它不替代首次建档、单次训练反馈或训练计划。

这里不包含：

- 真实用户训练数据。
- Garmin token。
- 本地存储文件。
- 个人工作区记忆。
- 本地运行脚本。
- 内部实现、部署脚本和项目评估材料。

安装或发布时，只打包本目录即可。技能的唯一来源是本目录下的 `skills/`。
