---
name: training-load
version: 0.1.0
description: 根据用户训练记录、Garmin 原始数据、心率、时长和主观疲劳计算单次训练负荷、7日急性负荷、28日周均慢性负荷、ACWR 和风险等级。
categories:
  - running
  - cycling
  - swimming
  - triathlon
  - endurance
  - load
---

# 训练负荷

## 何时使用

当用户问“最近练得重不重”“训练负荷多少”“疲劳风险”“ACWR”“这周负荷高不高”，或系统同步 Garmin 新训练、保存手动训练、生成训练反馈、周报和训练计划调整时使用。

`training-load` 是独立计算能力，不负责制定训练计划，也不单独替代身体状态判断。它应和 `workout-feedback`、`weekly-review`、`periodic-training-summary`、`training-plan` 配合使用。

## 输入来源

优先使用当前用户自己的数据，禁止跨用户读取：

- `workout_logs`：训练日期、项目、距离、时长、心率、功率、主观疲劳。
- `external_imports.raw_json`：Garmin 活动原始数据，例如训练负荷、训练效果、TSS 类字段。
- `body_status_logs`：疲劳、睡眠、压力、疼痛、恢复信号，仅作为风险解释，不直接伪造成负荷分数。

## 计算口径

负荷结果默认写入 `training_loads`：

- `load_score`：单次训练负荷分数。
- `method`：计算方法，例如 `garmin_training_load`、`garmin_tss`、`garmin_training_effect_estimate`、`heart_rate_duration_estimate`、`session_rpe_estimate`、`duration_estimate`。
- `confidence`：`high` / `medium` / `low`。
- `acute_load_7d`：截至该训练日的 7 日急性负荷总和。
- `chronic_load_28d`：截至该训练日的 28 日负荷折算周均。
- `acwr`：7 日急性负荷 / 28 日周均慢性负荷。
- `risk_level`：低 / 中 / 高。

优先级：

1. Garmin 原始训练负荷或 TSS 类字段：高置信度。
2. Garmin 训练效果 + 时长：中置信度，必须说明是估算。
3. 平均心率 + 时长：中置信度，必须说明不是精确 TSS。
4. 时长 + 主观疲劳：低置信度。
5. 仅时长：低置信度，只能作为粗略估算。

## 回复规则

- 可以告诉用户“训练负荷分数”和“趋势风险”，但不要把估算值说成精确生理指标。
- 使用估算时必须说明“估算”或“置信度”。
- 解释 ACWR 时，用普通中文：`>1.3` 表示近期负荷抬升较快，`>1.5` 表示需要更谨慎恢复。
- 不要只看负荷分数下结论；必须结合睡眠、疼痛、疲劳、训练准备度和用户目标。
- 如果缺少足够数据，明确说明“这次只能按时长/心率粗估”，不要编造功率、FTP、阈值心率或 TSS。

## 输出格式

```text
训练负荷：
- 单次负荷：
- 计算方式：
- 置信度：
- 7日急性负荷：
- 28日周均慢性负荷：
- ACWR：
- 风险等级：
- 解释：
- 建议：
```

## 安全边界

- 训练负荷不是医学诊断。
- 如果负荷升高同时出现疼痛、睡眠差、训练准备度低或异常高心率，应保守建议降负荷或恢复。
- 疼痛加重、改变动作、胸部不适、晕厥或异常呼吸时，优先安全建议，必要时建议寻求专业人士帮助。
