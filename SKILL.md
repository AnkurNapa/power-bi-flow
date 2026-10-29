---
name: power-bi-flow
description: Entry point for any Power BI work. Orders the 38 Power BI skills (pbi-dashboard-flow, the pbi-cli power-bi-* skills, dax-modeling-guide and the data-goblin pbip, pbi-desktop, reports, semantic-models, tabular-editor and fabric-cli plugins) into one build flow from data intake to hand-over. It also says which ones run on the Mac and which need the Windows laptop with Power BI Desktop. Use when asked to build, fix, review, document, publish or speed up a Power BI dashboard, report or semantic model, or when unsure which Power BI skill to load.
---

# Power BI flow

One flow, eight stages. Load the skill named at each stage; this file only routes.

Knowledge base: `/Users/ankurnapa/Documents/obsidian/PowerBI_KB_and_Skills/Knowledge Base/`
Error log (read first, append last): `Knowledge Base/PBI Build Flow/PBI Build Error Log.md`

## Where each stage runs

Power BI Desktop, Tabular Editor 2, DAX Studio and pbi-cli are Windows only. On the Mac the flow covers stages 0 to 4 (files and Python) plus stage 6 (service, through `fab`). Stage 5 needs the Windows laptop or a VM. Say which machine a step needs before starting it.

## Stages

| # | Stage | Load | Runs on |
|---|---|---|---|
| 0 | Learn before building | error log Prevention checklist; `dax-modeling-guide`; KB `Topics/` maps; the two dashboard design playbooks in the KB | Mac |
| 1 | Profile the data | `pbi-dashboard-flow` step 1; `semantic-models:power-query` for M | Mac |
| 2 | Model (TMDL) | `pbi-dashboard-flow` step 2; `pbip:tmdl`; `semantic-models:dax`; `semantic-models:standardize-naming-conventions`; RLS with `power-bi-security` | Mac |
| 3 | Report (PBIR) | `pbi-dashboard-flow` step 3; `pbip:pbir-format`; `reports:pbi-report-design`; `reports:create-pbi-report`; theme with `reports:modifying-theme-json`; custom marks with `reports:svg-visuals` or `reports:deneb-visuals` (`python-visuals` and `r-visuals` only when asked) | Mac |
| 4 | Static gates | `pbi-dashboard-flow` step 4 (`check_refs`, `tmdl_lint`, `layout_lint`, `layout_map`); `tabular-editor:bpa-rules`; `semantic-models:review-semantic-model`; `reports:review-report`; `semantic-models:lineage-analysis` when a column or measure is renamed | Mac (BPA run needs TE2 on Windows) |
| 5 | Open, refresh, test live | `pbi-desktop:connect-pbid`; `semantic-models:refreshing-semantic-model`; `power-bi-dax` for reconciliation queries; `power-bi-diagnostics` and `perf_check.py` for speed; bulk fixes with `tabular-editor:te2-cli` or `tabular-editor:c-sharp-scripting` | Windows |
| 6 | Publish | `fabric-cli:fabric-cli` (`fab`); `power-bi-deployment` for TMDL export and version control; service tuning with `fabric-senior-dev`, `fabric-pbi-perf-remediate`, `fabric-pbi-security-remediate` | Mac or Windows |
| 7 | Hand over and learn | `power-bi-docs` or `tabular-editor:te-docs` for the data dictionary; `pbi-dashboard-flow` steps 6 and 7; append every new mistake to the error log | Mac |

## Small jobs

Skip the stages that do not apply. One measure: stage 0 topic map, stage 2, stage 4, stage 5. One visual: stage 3, stage 4. A model review only: stage 4. The pbi-cli skills (`power-bi-modeling`, `power-bi-partitions`, `power-bi-pages`, `power-bi-visuals`, `power-bi-filters`, `power-bi-themes`, `power-bi-report`) edit a live model or report in place on Windows; prefer the generators in `pbi-dashboard-flow` for a full build, since they rebuild from source every time.

## Rules

1. Generate with Desktop closed. Desktop's save prompt overwrites generated files.
2. No stage moves on until its gate shows 0 fail.
3. Every headline number reconciles against the source or the answer key in stage 5.
4. Client data never leaves the client folder. A demo uses the fictional copy steps in `pbi-dashboard-flow`.
