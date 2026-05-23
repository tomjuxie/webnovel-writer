# Webnovel Writer Suite (Google Antigravity Edition)

> 🚀 **面向网文作家的 Agent 智能创作协同套件（Google Antigravity 适配增强版）**

本项目是专为网络小说作家打造的 Agent 智能创作套件。系统通过将**华夏圣贤诸子百家学说**与**玄幻修行体系**深度融合，构建起一套涵盖“项目初始化 ➡️ 卷纲/时间线规划 ➡️ 章节起草 ➡️ 智能审查 ➡️ 事实提取与落库”的完整小说生命周期协同创作流。

---

## 🌟 核心升级：Google Antigravity 深度兼容

我们已将本项目重构，使其完美适配 **Google Antigravity** 双模架构，同时**完整保留了对 Claude Code 的向后兼容性**，实现了双生态无缝转换：

1. **双插件规范支持**：
   * **Antigravity 偏好**：在 [.agents/skills/](file:///.agents/skills) 与 [.agents/agents/](file:///.agents/agents) 中同步集成了 7 大核心智能技能。
   * **Claude Code 兼容**：保留了原有的 `.claude-plugin/` 结构与工作区指针映射。
2. **底层气机重构**：
   * **路径智能解算**：重构了 [project_locator.py](file:///scripts/project_locator.py) 和 [config.py](file:///scripts/data_modules/config.py)，动态感知 `ANTIGRAVITY_PROJECT_DIR` 等环境变量，智能判断当前活动 IDE，免去手动更改配置的痛苦。
   * **自动化测试适配**：重构 [run_tests.ps1](file:///scripts/run_tests.ps1)，自动识别 `.agents` 执行路径，并加入强制 `-p asyncio` 驱动，保障 **570+ 全量测试用例** 100% 稳健通过。
3. **详细大纲解析器缺陷修复（Bug Fix）**：
   * 修复了 [chapter_outline_loader.py](file:///scripts/chapter_outline_loader.py) 中由于 f-string 大括号转义缺陷导致 `#{2,3}` 变性为元组 `(2, 3)` 的 Bug，实现了对 `##` 二级标题章节大纲的**完美结构化解析**。

---

## 📖 活跃创作项目：《道心儒血》

* **书名**：《道心儒血》
* **题材**：百家争鸣 / 玄幻 / 知行反噬
* **篇幅规划**：300 万字 / 1000 章
* **主角**：**顾道儒**（历史系研究生穿越，身怀诸子百家圣贤道藏，兼修道家“清冷出尘”之道心与儒家“担当入世”之儒血，练气二层）
* **女主**：**墨玄机**（墨家天才，机关机甲大师，与主角进行灵魂与理念的激烈交锋）
* **当前进度**：
  * **卷规划**：已完成**第 1 卷《孤城提笔引天光》**的全局规划，生成了完整的 [节拍表](file:///daoxinruxue/大纲/第1卷-节拍表.md) 与 [时间线倒计时](file:///daoxinruxue/大纲/第1卷-时间线.md)。
  * **第一章成稿**：[第0001章-寒蝉清冷道心远.md](file:///daoxinruxue/正文/第0001章-寒蝉清冷道心远.md) 已撰写完成。经过严苛的 Anti-AI 流水线审查，斩获 **100.0 分（完美无瑕）** 的超凡评级，已成功原子化提交，并建立了 `ch0001` Git 标签备份！

---

## 🛠️ 统一命令行使用指南

项目使用位于 `scripts/` 下的统一脚手架命令行入口 `webnovel.py`，无需 `cd` 即可操作：

### 1. 运行环境预检 (Preflight)
```bash
python -X utf8 scripts/webnovel.py --project-root daoxinruxue preflight
```

### 2. 占位符扫描 (扫描待补齐设定与大纲)
```bash
python -X utf8 scripts/webnovel.py --project-root daoxinruxue placeholder-scan --format text
```

### 3. 生成/刷新 Story System 运行合同
```bash
python -X utf8 scripts/webnovel.py --project-root daoxinruxue story-system "第N章写作目标" --genre "玄幻" --chapter N --persist --emit-runtime-contracts --format both
```

### 4. 运行章节质量智能审查 Pipeline (Step 3)
```bash
python -X utf8 scripts/webnovel.py --project-root daoxinruxue review-pipeline \
  --chapter 1 \
  --review-results "daoxinruxue/.webnovel/tmp/review_results.json" \
  --metrics-out "daoxinruxue/.webnovel/tmp/review_metrics.json" \
  --report-file "daoxinruxue/审查报告/第1章审查报告.md" \
  --save-metrics
```

### 5. 章节原子化提交与 SQLite 投影更新 (Step 5)
```bash
python -X utf8 scripts/webnovel.py --project-root daoxinruxue chapter-commit \
  --chapter 1 \
  --review-result "daoxinruxue/.webnovel/tmp/review_results.json" \
  --fulfillment-result "daoxinruxue/.webnovel/tmp/fulfillment_result.json" \
  --disambiguation-result "daoxinruxue/.webnovel/tmp/disambiguation_result.json" \
  --extraction-result "daoxinruxue/.webnovel/tmp/extraction_result.json"
```

### 6. 自动化 Git 版本备份 (Step 6)
```bash
python -X utf8 scripts/webnovel.py --project-root daoxinruxue backup \
  --chapter 1 \
  --chapter-title "寒蝉清冷道心远"
```

---

## 💻 单元测试与质量保障

您可以运行项目集成的自动化测试套件以检验代码健康度：

```powershell
# 运行烟雾测试
powershell .\scripts\run_tests.ps1 smoke

# 运行全量 570+ 测试集
powershell .\scripts\run_tests.ps1 full
```

---

## 🎨 创作技能星图 (Skills Registered)

在 Antigravity 工作区下，您可以使用自带的 7 大技能：
* **`webnovel-init`**：智能收集创作信息，生成全套设定骨架。
* **`webnovel-plan`**：细化节拍表、时间线、结构化章纲。
* **`webnovel-write`**：起草可直接发布的正文。
* **`webnovel-review`**：使用审查 Agent 进行 Anti-AI 词汇和设定一致性审计。
* **`webnovel-query`**：时序查询人物卡与世界观。
* **`webnovel-dashboard`**：查看写作进度与可视化图表。
* **`webnovel-learn`**：记忆提取与学习迭代。
