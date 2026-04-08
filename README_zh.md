# US Teen 子集发布目录

[English Version](README.md)

该目录发布了一个 TikTok 视频级原始数据表，以及两个面向 US teen 研究的筛选子集，供课程研究与后续分析使用。

## 概览

本目录包含：

- 原始视频级数据
- 质量优先子集：`US_teen_core.csv`
- 规模优先子集：`US_teen_scale.csv`
- 全量最终打分表：`scored_all.csv`

这些子集属于启发式和弱监督筛选结果，不是人工确认的人口统计学 ground-truth 标签。

## 原始数据集

原始文件为：

- `data/tiktok_merged_data_deduplicated.csv`

该表是按视频粒度组织的数据表，共包含 `7,225` 条视频。核心字段包括：

- `description`
- `hashtags`
- `author`
- 互动指标，如 `likes`、`comments`、`shares`、`plays`
- `create_time`
- `video_url`

### 时间范围

该数据集覆盖的时间范围为 `2025-04-13` 到 `2025-05-24`。

其中最密集的时间窗口是 `2025-05-16` 到 `2025-05-23`，正好落在美国高中毕业季和 prom / graduation season 附近。因此，原始数据天然富含毕业季相关表达，例如：

- `class of`
- `graduation`
- `senior year`
- `prom`
- 高中毕业庆祝与阶段性里程碑内容

这一时间背景对于理解本目录中的筛选子集非常重要。

## 我们如何构建这些子集

本发布版使用的是 Round3 keyword expansion 的最终非 LLM 流程。高层步骤包括：

- 对文本与 hashtag 做归一化
- 扩展毕业季和 class-year 相关表达
- 基于高精度正负种子训练排序模型
- 对多种方案结果进行共识聚合

本目录只保留最终发布所需的数据文件，不包含实验过程中的中间产物。

## 发布的数据文件

| 文件 | 行数 | 说明 |
| --- | ---: | --- |
| `data/tiktok_merged_data_deduplicated.csv` | 7,225 | 原始视频级数据 |
| `data/US_teen_core.csv` | 133 | 质量优先、较保守的核心子集 |
| `data/US_teen_scale.csv` | 300 | 规模优先、较宽松的扩展子集 |
| `data/scored_all.csv` | 7,225 | 对全部视频的最终共识打分表 |

## 文件对应关系

- `US_teen_core.csv` 是最终的质量优先推荐集。
- `US_teen_scale.csv` 是最终的规模优先推荐集。
- `scored_all.csv` 是与这两个发布子集对应的全量打分背景表。

如果研究者希望自行调整阈值或构建新的子集，应从 `data/scored_all.csv` 出发。

## 使用建议

- `data/US_teen_core.csv` 适合更保守的主分析。
- `data/US_teen_scale.csv` 适合需要更大样本规模的补充分析。
- `data/scored_all.csv` 适合做阈值调整、稳健性分析或自定义切分。

## 限制说明

原始数据并不包含经过核验的年龄、国籍、地区等人口统计真值字段。因此：

- 本目录中的子集应被视为启发式或弱监督筛选结果
- 不应将其描述为人工确认的人口统计标签

