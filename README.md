# AI 编程重构：F2F 与 SpS

> 面向 AI 编程的两项重构——**F2F 组织输出端（文件）**，**SpS 组织输入端（指令）**。

作者：**Yang Zikun**（杨梓坤）· 独立研究者 · 2026 年 9 月

---

## 两篇论文

|  | 论文 | 视角 | 一句话 |
|:--:|---|---|---|
| 📄 | [**Feature-per-File（F2F）**](feature-per-file/)<br>*以功能为文件：面向 AI 编程的代码组织重构* | 数据工程 | 放弃按技术职责横向分层（Controller→Service→Mapper），以**功能**为最小自治单元，一个文件贯通入口、业务处理到数据访问的完整链路；文件之间零耦合；维护采用**替换式**，并以历史版／运行版／开发版三版本并存支撑。 |
| 📄 | [**Spec-per-Stage（SpS）**](spec-per-stage/)<br>*以阶段为规范：面向 AI 编程的交互界面重构* | 注意力经济学 | 以一套通用规范充当 AI 编程的**“SQL 语法”**：把一次开发任务表达为若干条规范语句，每条由不变的模板骨架 **τ** 与开发者填写的变量细节 **δ** 构成；提交前经轻量校验，每个阶段（产品方案设计→技术方案设计→产品实现）出口设人工评审门禁。 |

两篇是**互补**的两半：SpS 重构**输入端**（人如何向模型下达指令），F2F 重构**输出端**（模型产出的代码如何组织）。实现语句以 F2F 特征文件为输出单元，复杂任务通过语句分解为多个独立文件的增量拼装。

---

## 目录结构

```
.
├── feature-per-file/          # F2F 论文
│   ├── 以功能为文件-AI编程重构论文.tex
│   ├── 以功能为文件-AI编程重构论文.bbl   # 参考文献（已生成，可直接编译）
│   ├── 以功能为文件-AI编程重构论文.pdf   # 编译成品
│   └── references.bib
└── spec-per-stage/            # SpS 论文
    ├── 以阶段为规范-AI编程交互界面重构论文.tex
    ├── 以阶段为规范-AI编程交互界面重构论文.bbl
    ├── 以阶段为规范-AI编程交互界面重构论文.pdf
    └── references-sps.bib
```

每篇论文均为**单文件 LaTeX**（`ctexart` 文档类），无外部图片依赖，`.bbl` 已随源码提供。

---

## 编译

需要 **XeLaTeX**（文档使用 `ctexart`，pdfLaTeX 无法处理中文字体）。

```bash
cd feature-per-file
xelatex 以功能为文件-AI编程重构论文.tex
xelatex 以功能为文件-AI编程重构论文.tex   # 第二遍生成目录与交叉引用编号
```

仓库已附带生成的 `.bbl`，因此**无需运行 bibtex**。若修改了 `references.bib`，则需：

```bash
xelatex <论文>.tex && bibtex <论文> && xelatex <论文>.tex && xelatex <论文>.tex
```

在 [Overleaf](https://www.overleaf.com/) / TeXPage 上选择 XeLaTeX 编译器可直接使用。

---

## 引用

```bibtex
@article{yang2026featureperfile,
  title  = {Feature-per-File: Refactoring Code Organization for AI Programming---A Data-Engineering Perspective},
  author = {Yang, Zikun},
  year   = {2026},
  month  = {9},
  note   = {Preprint}
}

@article{yang2026specperstage,
  title  = {Spec-per-Stage: Refactoring the Interaction Interface of AI Programming---An Attention-Economics Perspective},
  author = {Yang, Zikun},
  year   = {2026},
  month  = {9},
  note   = {Preprint}
}
```

---

## 相关实现

**[sps-console](https://github.com/buyunaihe666/sps-console)** —— 本文所述 SpS 范式的参考实现：一个零依赖的本地控制台，把「模板骨架 + 变量细节」落成可编辑的规范语句，运行时按选中顺序拼成 `system` 消息；模型的产出被约束为 F2F 特征文件，且要求**新增能力 = 新增文件**（不得改动任何已存在的功能文件）。仓库内含一份由它生成的数据看板作为示例产物。

---

## 版权

© 2026 Yang Zikun. All rights reserved. 见 [LICENSE](LICENSE)。
