# GCP合规Skill

> 基于中国《药物临床试验质量管理规范》（2026 年修订版）的 Cursor Agent Skill。将具体实操问题映射到具体条款，输出**条款级、可追溯、可执行**的合规判定。

[![Release](https://img.shields.io/github/v/release/amon339/gcp-compliance-skill)](https://github.com/amon339/gcp-compliance-skill/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Cursor Skill](https://img.shields.io/badge/Cursor-Agent%20Skill-000000)](https://cursor.com)

**快速开始**：[下载最新 Release](https://github.com/amon339/gcp-compliance-skill/releases/latest) → Cursor Settings → Skills → Import `gcp-compliance.skill`

---

## 这是什么

**GCP合规Skill** 是一个面向 [Cursor](https://cursor.com) 的领域型 Agent Skill，内嵌 2026 版 GCP 全文与结构化判定协议，帮助临床试验从业者把「这个操作行不行」转化为：

- **适用条款**（精确到「第 X 条（X）」）
- **合规判定**（符合 / 违背 / 视情形而定）
- **判定理由**（事实与条款的对应关系）
- **整改与建议**（含上报义务与时限）

面向行业专家设计：不做基础科普，直接给判定。

---

## 适用对象

| 角色 | 典型场景 |
|------|----------|
| CRC | 知情同意瑕疵、源记录、偏离记录 |
| CRA | 监查发现项定性、不依从上报 |
| 主要研究者 | 紧急偏离、SAE 报告、揭盲 |
| 申办者 QA / PV | SUSAR/DSUR、依从性管理、CAPA |
| 数据管理 | EDC 改数权限、稽查轨迹、盲态 |
| 机构 / 药房 | BE 留样、IMP 管理、记录保存 |
| 伦理秘书 | 跟踪审查、ICF 版本合规 |

---

## 核心能力

### 六步闭环判定协议

1. **拆解操作** — 提取谁、何时、做了什么、是否已发生
2. **定位条款** — 1 条核心 + 若干关联条款
3. **核对原文** — 强制查阅内嵌 GCP 全文，禁止凭记忆复述
4. **合规判定** — 符合 / 违背 / 视情形而定
5. **整改建议** — 纠正、预防、是否上报
6. **时限触发** — SAE/SUSAR、重要偏离、严重不依从等

### 固定输出模板

```
【操作】
【适用条款】
【合规判定】
【判定理由】
【建议与整改】
【备注】
```

### 内嵌知识底座

- 《药物临床试验质量管理规范》（2026 年修订版）全文
- 主题 → 条款定位索引（6 章 54 条）
- 数值与时限速查表（伦理跟踪 ≤12 月、SAE 立即报告、BE 留样等）

---

## 安装

### 方式一：导入 `.skill` 包（推荐）

1. 从 [Releases 页面](https://github.com/amon339/gcp-compliance-skill/releases/latest) 下载 `gcp-compliance.skill`
2. 打开 Cursor → **Settings** → **Rules** → **Skills**
3. 点击 **Import**，选择 `gcp-compliance.skill`

### 方式二：手动安装目录

将 `gcp-compliance/` 文件夹复制到以下任一位置：

```bash
# 个人级（所有项目可用）
~/.cursor/skills/gcp-compliance/

# 项目级（仅当前仓库）
<your-project>/.cursor/skills/gcp-compliance/
```

目录结构应为：

```
gcp-compliance/
├── SKILL.md
└── references/
    └── gcp-full-text.md
```

### 方式三：克隆本仓库后复制

```bash
git clone https://github.com/amon339/gcp-compliance-skill.git
cp -r gcp-compliance-skill/gcp-compliance ~/.cursor/skills/
```

---

## 使用示例

安装后，在 Cursor 对话中**直接描述实操问题**，无需说「启用 GCP skill」：

```
受试者上周入组的 ICF 漏签日期，今天补填了上周的日期，可以吗？
```

```
BE 试验结束后申办者来取留样，能给他吗？
```

```
申办者数据管理员直接在 EDC 里改了研究者填的数据，没通知 PI，可以吗？
```

```
伦理跟踪审查超过 12 个月了还在入组，什么问题？
```

涉及知情同意、SAE、方案偏离、源数据、IMP、盲态、电子签名等主题时，Skill 会自动触发。

---

## 仓库结构

```
gcp-compliance-skill/
├── README.md
├── LICENSE
├── gcp-compliance.skill          # Cursor 可导入的技能包
└── gcp-compliance/
    ├── SKILL.md                  # 主技能文件（判定协议 + 索引）
    └── references/
        └── gcp-full-text.md      # GCP 2026 修订版全文
```

---

## 判定哲学

四条贯穿性原则内化于每一次判定：

1. **受试者权益与安全优先**（第四条、第五条）
2. **质量源于设计，控制基于风险**（第六条、第四十条、第四十二条）
3. **可追溯性是合规的底层语法** — ALCOA；没有记录 = 没有发生（第二十九条）
4. **最终责任不可让渡** — PI 与申办者（第十九条、第三十二条、第三十六条）

---

## 重要说明

### 版本与适用范围

- 依据：《药物临床试验质量管理规范》**2026 年修订版**（2026 年 9 月 1 日起施行）
- 辖区：中国法规语境；涉及 FDA、EU CTR、ICH 各地实施差异时会提示
- 施行日前历史事件，需结合版本过渡规则另行判断

### 免责声明

- 本 Skill 输出为基于 GCP 条款的**专业合规分析参考**，**不构成法律意见**
- 具体监管处置、法律责任以药品监督管理部门和相关法律为准
- 内嵌 GCP 条款原文仅供合规判定参考，请以官方发布文本为准
- 涉及处罚、赔偿等法律后果，请咨询机构法务或药事法规事务专家

---

## 重新打包 `.skill` 文件

如需自行打包：

```bash
cd gcp-compliance-skill
zip -r gcp-compliance.skill gcp-compliance/
```

---

## License

- Skill 文档、结构与代码：[MIT](LICENSE)
- 内嵌《药物临床试验质量管理规范》条款原文：版权归国家药品监督管理部门，本仓库仅供合规参考，不主张版权

---

## 更新日志

详见 [CHANGELOG.md](CHANGELOG.md)。

## 贡献

欢迎提交 [Issue](https://github.com/amon339/gcp-compliance-skill/issues) 反馈条款索引遗漏、判定示例补充、措辞优化等。Pull Request 请确保不修改 GCP 原文的准确性表述。

## 相关链接

- [最新 Release 下载](https://github.com/amon339/gcp-compliance-skill/releases/latest)
- [问题反馈](https://github.com/amon339/gcp-compliance-skill/issues/new/choose)

---

**临床试验合规，从检索条文，到即时判定。**
