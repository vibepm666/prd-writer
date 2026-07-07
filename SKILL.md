---
name: prd-writer
description: |
  帮助用户从零写出高质量 PRD，或评估/改进/增量更新已有需求文档。
  触发词（任一命中即用本 skill）：需求文档、PRD、产品需求、功能文档、写需求、整理需求、补充需求、审查需求、改进需求文档、需求评审、评估 PRD、从零写 PRD、我想做个产品/功能/App/工具、帮我整理需求、AI 写的需求有没有问题、导出 PRD、PRD 导出 Word、需求文档转 Word、PRD 转 Word。
  即使描述很简短也必须触发，不得跳过技能直接写文档。
---

# PRD Writer Skill

把产品经理核心思维封装为可执行工作流：先验证方向，再分两版交付（概念版 → 落地版）；三视角诊断（用户 / 商业 / 技术）；主动补全交互、状态、数据与文案盲区。

## 文件结构

| 文件 | 用途 |
| --- | --- |
| **`SKILL.md`**（本文件） | 门禁、模式、交付路径、执行顺序 |
| **`references/read-first.md`** | 先读再写、模式判断、第零步豁免 |
| **`references/diagnosis-guide.md`** | 三视角诊断与产品形态 |
| **`references/concept-template.md`** | 第一版概念文档模板 |
| **`references/prd-template.md`** | 第二版落地 PRD 模板（含 MVP 闸门） |
| **`references/diagram-handoff.md`** | Mermaid vs diagram-generator |
| **`references/product-type-appendix.md`** | B2B / ToC / 营销站等 §7 补充 |
| **`references/review-checklist.md`** | 模式 B 评审项 |
| **`references/review-output-template.md`** | 模式 B 评审报告模板 |
| **`references/example-prd.md`** | 格式与粒度示例 |
| **`references/self-check.md`** | 写后自检 |

**相关技能**：用户输入为 **Axure 导出 HTML** 或 **线上站点逆向** 时，先用 `prototype-to-prd` 完成盘点，再按本技能模式 A 写概念版/落地版（模板复用本目录 `references/`）。

**写文档前**：按模式 `Read` 对应 `references/` 文件，再落笔。  
**交付模式**：**本技能未声明时默认「标准」**（详见 README「交付模式」；可说「快速模式」降档或「严格模式」升档）。

---

## 0. 交付模式与快路径

| 模式 | 概念版 | MVP 确认 | self-check |
| --- | --- | --- | --- |
| **标准**（**本技能默认**） | 默认分两文件；用户说「快速模式 / 直接写 PRD / 跳过概念版」→ **快路径**（单文件） | 用概念版或 §4 功能树中的 🔴，**不单独口头确认** | 全文勾选 |
| **快速** | **跳过**；单文件 `docs/YYYY-MM-DD-<主题>-PRD.md`，文内用 `## 第一部分 · 概念对齐` 简要概括 | 默认展开 §4 全部 🔴 | 仅 P0 流程项 |
| **严格** | 必须 `-概念版.md` 且用户 **明确确认** | 写 §5 前口头确认 N 个 MVP | 全文勾选 |

**快路径 / 降档触发词**（**标准模式**默认时）：快速模式、直接写 PRD、跳过概念版、先出落地稿、单文件 PRD。

---

## 执行顺序（门禁）

```text
用户消息
  → 1. read-first.md（先读 docs/ 与用户 @ 稿）
  → 2. 第零步（无输入稿时；见下方豁免）
  → 3. 识别模式 A / B / C
  → 4. 按模式读模板并写入 docs/
  → 5. self-check.md
  → 6. （可选）用户要求时导出 Word（见 §9）
```

---

## 1. 启动前：先读已有材料

**必须**按 `references/read-first.md` 执行：扫描 `docs/`、摘录真源、仅补缺口问诊、判断模式。

**第零步豁免**（跳过开场问句，直接进模式）：

| 条件 | 进入 |
| --- | --- |
| 用户 @ / 提供完整 PRD，要评审或改进 | 模式 B |
| 用户指明「只加 / 只改某模块」且已提供文档 | 模式 C |
| 已读材料且足以判断方向与模式 | 对应模式 |

---

## 2. 第零步：是否适合本 skill

> 非头脑风暴工具；适合已有基本想法的用户。  
> **已执行 read-first 且信息足够 → 跳过本步。**

**若无可用输入稿，先问：**

> 在开始之前，能先跟我说说你这个产品/功能的核心想法是什么吗？哪怕一两句话——你想解决什么问题，大概想用什么方式解决？

| 用户回答 | 判断 | 处理 |
| --- | --- | --- |
| 能说出「谁的什么问题，用什么方式解决」 | ✅ | 进入模式 A 第一步 |
| 模糊但有方向，如「做个记账 App」 | ⚠️ | 追问明确核心逻辑 |
| 完全无方向，如「帮我想做什么 App」 | ❌ | 温和引导先想清楚痛点，暂不写 PRD |

---

## 3. 识别模式

| 用户情况 | 模式 |
| --- | --- |
| 有想法，还没有文档 | **A：从零，分两版生成** |
| 已有文档，要检查/改进 | **B：评估 + 改进** |
| 已有文档，追加或细化 | **C：增量融合** |

---

## 4. 交付物：格式与路径

| 项 | 规则 |
| --- | --- |
| 格式 | Markdown；**以文件为准**，聊天可摘要 |
| 路径 | 工作区 **`docs/`**（无则创建） |
| 概念版 | `docs/YYYY-MM-DD-<主题>-概念版.md` |
| 落地版 | `docs/YYYY-MM-DD-<主题>-PRD.md`；文首 **一行链回** 概念版路径 |
| 评审报告 | `docs/YYYY-MM-DD-<主题>-PRD-评审.md`（模式 B 默认落盘） |
| 分版策略 | **默认分文件**；用户坚持单文件时用 `## 第一部分 · 概念对齐（已确认）` / `## 第二部分 · 落地需求` |
| Word 导出 | **可选**；Markdown 落盘并完成自检后，用户要求时用 `req-doc` 模板导出 `.docx`（见 §9） |

文首元数据、章节结构见 `concept-template.md`、`prd-template.md`。格式参考 `example-prd.md`。

---

## 5. 模式 A：从零引导

### 第一步：三视角诊断

按 `references/diagnosis-guide.md`：用户 / 商业 / 开发 + 产品形态；每次 1–2 问。

- **快速模式**：已有清晰方向则 **压缩为 1 轮** 总结，不逐视角追问
- **标准/严格**：完成后口头总结；**严格** 须用户确认后再写概念版

### 第二步：概念版

- **快路径 / 快速模式**：跳过本步，进入第三步（单文件时在 PRD 文首写 8–12 行方向摘要）
- **标准 / 严格**：按 `references/concept-template.md` 写入 `-概念版.md`  
  **唯一目的：对齐方向。** **严格** 下用户 **明确确认** 前不得写落地 §5。「差不多」在 **严格** 下不算确认；**标准** 下用户说「可以/继续」即可进入落地版。

### 第三步：落地版

按 `references/prd-template.md` 写入 `-PRD.md`。

- **MVP 闸门**：默认只展开 🔴 的 §5；**严格** 写前口头确认 N 个 MVP；**标准/快速** 以 §4 功能树 🔴 为准，不另问
- **图表**：按 `references/diagram-handoff.md`（简单 Mermaid 内嵌，复杂用 diagram-generator）
- **§7**：按 `references/product-type-appendix.md` 触发补充

---

## 6. 模式 B：评估 + 改进

1. `Read` → `review-checklist.md`，逐项 ✅ / ❌ / ⚠️
2. 按 `review-output-template.md` 写入 **`-PRD-评审.md`**（用户明确只要对话结论时可不落盘）
3. 问用户：直接补全 vs 自行修改后再评
4. 补全走模式 C 规则，用 `【本次更新】` 标注

---

## 7. 模式 C：增量融合

**原则：融合不覆盖，更新不重写。**

1. 读取现有文档（路径或粘贴）
2. 明确追加/修改范围
3. 定位影响章节（通常：功能清单、动线 §3、§5、文案）
4. 融合进对应位置；冲突列出让用户裁定
5. `【本次更新】` 标注所有改动
6. 检查动线、§5、清单一致性 → `self-check.md`

---

## 8. 通用原则

1. **分阶段**：**严格** 下概念版未确认 → 不写落地 §5 细节；标准快路径/快速模式可合并  
2. **三视角**：**快速** 可压缩；**严格** 三视角均需基本答案  
3. **补盲区**：交互、状态、数据、双受众文案——主动补，不等用户问  
4. **双受众**：开发/AI 规格 vs 终端文案，分开写  
5. **融合不覆盖**：模式 C 不丢原文  
6. **`[待补充]` 不编造**：标清影响范围  
7. **图与表**：动线 Mermaid、状态表、功能树、ASCII 线框（见 diagram-handoff）  
8. **先读再写、MVP 优先**：见 read-first、prd-template MVP 闸门  

**写完必过** `references/self-check.md`（**快速** 模式仅勾选「流程与门禁」「落地版」P0 项）。

---

## 9. 导出 Word（可选）

Markdown 落盘并通过 `self-check.md` 后，若用户要求导出 Word（或消息命中「导出 PRD」「PRD 导出 Word」「需求文档转 Word」等），执行本步；**未明确要求时不主动导出**。

### 适用文件

| 文件 | 模板 | 说明 |
| --- | --- | --- |
| 落地版 `*-PRD.md` | **`req-doc`** | 默认导出对象 |
| 概念版 `*-概念版.md` | `req-doc` 或 `simple` | 用户指定时 |
| 评审报告 `*-PRD-评审.md` | `formal` 或 `simple` | 用户指定时 |

> 模板名 **`req-doc`**（需求说明书），**不是** `prd`。

### 命令

**Windows（PowerShell）：** `.agents/skills/common/export-word.ps1 <markdown文件路径> req-doc`

**跨平台：** `python .agents/skills/common/export-word.py <markdown文件路径> req-doc`

**Git Bash：** `bash .agents/skills/common/export-word.sh <markdown文件路径> req-doc`

**示例**（文件名遵循 §4 落地版命名，`<主题>` 替换为实际项目名）：

```powershell
.agents/skills/common/export-word.ps1 docs/YYYY-MM-DD-<主题>-PRD.md req-doc
```

### 输出与依赖

- **输出路径**：与源 Markdown 同目录，文件名相同、扩展名为 `.docx`
- **本地图片**：脚本自动扫描 MD 内 `![](相对路径)` 并一并上传；远程 URL 图片不处理
- **依赖**：Python 3；可访问 `.agents/skills/config.json` 中 `apiBaseUrl`

导出完成后告知用户 `.docx` 路径；若 API 不可用，说明失败原因并保留 Markdown 为真源。
