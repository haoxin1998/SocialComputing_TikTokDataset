# US Teen Subset Release

[中文说明](README_zh.md)

This release packages a video-level TikTok dataset together with two derived US-teen-focused subsets for research use.

## Overview

The repository contains:

- the original video-level dataset
- a quality-first subset: `US_teen_core.csv`
- a scale-first subset: `US_teen_scale.csv`
- a full scored release table: `scored_all.csv`

These subsets are heuristic and weakly supervised research subsets. They are not manually verified demographic ground-truth labels.

## Original Dataset

The original file is:

- `data/tiktok_merged_data_deduplicated.csv`

It is a video-level table with `7,225` videos. Core fields include:

- `description`
- `hashtags`
- `author`
- engagement fields such as `likes`, `comments`, `shares`, and `plays`
- `create_time`
- `video_url`

### Time Window

The dataset covers videos from `2025-04-13` to `2025-05-24`.

Its densest period is `2025-05-16` to `2025-05-23`, which falls in the U.S. high-school graduation-season window. As a result, the raw data is naturally rich in graduation-season language such as:

- `class of`
- `graduation`
- `senior year`
- `prom`
- high-school celebration and milestone content

This temporal concentration is important for interpreting the subsets released here.

## How The Derived Subsets Were Built

This release uses the final non-LLM pipeline from the Round3 keyword-expansion workflow. At a high level, the construction process included:

- text and hashtag normalization
- expansion of graduation-season and class-year expressions
- a ranking model trained from high-precision positive and negative seeds
- multi-scheme consensus aggregation

The final release keeps only the end products of that pipeline.

## Released Files

| File | Rows | Description |
| --- | ---: | --- |
| `data/tiktok_merged_data_deduplicated.csv` | 7,225 | Original video-level dataset |
| `data/US_teen_core.csv` | 133 | Quality-first, more conservative subset |
| `data/US_teen_scale.csv` | 300 | Scale-first, broader subset |
| `data/scored_all.csv` | 7,225 | Final consensus-scored table for all videos |

## File Mapping

- `US_teen_core.csv` is the final quality-first recommendation set.
- `US_teen_scale.csv` is the final scale-first recommendation set.
- `scored_all.csv` is the full scored table aligned with these two released subsets.

If you want to apply a different threshold or build your own subset, start from `data/scored_all.csv`.

## Recommended Use

- Use `data/US_teen_core.csv` for more conservative main analyses.
- Use `data/US_teen_scale.csv` when you need a larger sample for supplementary analyses.
- Use `data/scored_all.csv` for threshold tuning, sensitivity checks, or custom subset construction.

## Limitations

The raw dataset does not contain ground-truth demographic fields such as verified age, nationality, or location. Accordingly:

- these released subsets should be treated as heuristic or weakly supervised subsets
- they should not be described as manually confirmed demographic labels

