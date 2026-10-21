---
name: sc2-community-reference
description: Locate the fork's community trigger, UI, inventory, voting and AI source examples, Chinese terminology resources, and legacy local skill mappings. Use for these supplemental references after the project entry router.
---

# 社区与本地补充资料

先从 [资料入口](../../references/local/README.md) 选择主题，再读 [案例索引](../../references/local/examples.md) 对应的一份 `Triggers`、文字或数据文件。不要一次加载整个资料目录。

- GUI/布局案例：读取案例的 `DocumentInfo` 依赖声明，再从 `Triggers` 与 `TriggerStrings.txt` 追踪动作。重复文件的唯一副本由 `manifest.json` 中 `path` 指向；不能假定它与原目录仍一一对应。
- AI：`references/local/ai/TactTerrAI.galaxy` 是既有战术脚本参考，按具体函数查询；参考中的 native、常量和库不保证在目标可用。
- 术语：按具体词查询 `references/local/terminology/`；保留占位符、标记、上下文与目标语言，不把词典匹配自动写成译文。
- 官方参考：继续用上游 catalog/reference 工具；外部共享资料树用现有 `--root` 参数，不复制或连接到开发源。

案例均是只读源码节选；缺少地形、美术、生成脚本及部分地图组件。借鉴机制后回到当前项目的 GUI、XML、本地化技能实现；遵守 GUI 优先与生成文件只读规则。节选 XML 可解析、文件哈希相同，只能证明静态可读和来源一致，不能证明 Editor 或游戏验收。

旧技能名转接：[sc2-units-reference](../sc2-units-reference/SKILL.md)、[sc2-localization-and-text](../sc2-localization-and-text/SKILL.md)。其余本地 Galaxy/物编技能已有上游正文，保持原路由。
