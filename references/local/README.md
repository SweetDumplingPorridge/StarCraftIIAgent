# 本地补充资料

本 fork 以 RichardM95/StarCraftIIAgent 为基底，保留其项目初始化、技能路由和工具链。这里补充原本分散在本地工作区的参考资料，不迁入战区等具体项目的设计、源码或历史流程。接入基线和逐文件来源见 [manifest.json](manifest.json)。

## 案例源码

[案例索引](examples.md) 按机制列出 11 组社区地图：亚顿之矛 UI、单位出生动画、随机技能、瞭望塔收入、卡牌移动、SCV 建造奥丁模型、物品栏购买/撤销/存档、计分板、建筑刷兵、随机结盟/出生点、难度投票。

仅收录 `Triggers`、`DocumentInfo`、相关本地化、GameData XML 与 SC2Layout；地形 XML、生成的 Galaxy、地形/美术/缓存/二进制组件和打包地图未迁入。它们是研究节选，不是完整可运行地图。原名称注明“编辑器打不开、由 MPQEditor 解包”的出生方式案例保留该来源说明，不视为已修复。

先读案例依赖和 GUI 源，再追踪文字键、布局及关联数据；不要修改这些参考来替代项目实现。文件可解析不代表依赖齐备或运行正确。`manifest.json` 的每条记录将原路径映射到唯一内容副本；相同 SHA-256 的文件只保存一次，因此节选目录并非完整组件布局。

现有战术脚本见 [TactTerrAI.galaxy](ai/TactTerrAI.galaxy)。原始来源为本地 `参考资料/示例地图/TactTerrAI.galaxy`；按函数查阅，先验证目标依赖中的 native 与常量。

## 术语资料

- [星际2词典.csv](terminology/星际2词典.csv)：`Term [zh-CN]`、`Term [en-US]`、`Term [ko]`。
- [星际2翻译记忆（tm）完整版.csv](<terminology/星际2翻译记忆（tm）完整版.csv>)：`zh-CN`、`en-US`、`ko`。

两份文件均已检查为 UTF-8，按原始字节保留。词典和翻译记忆是不同来源的数据集，部分词句可以重叠；不为消除文字重合而删改来源内容。仅作开发文字和术语查询，按具体词检索，不整体塞入上下文，不据此启用自动翻译或整项目汉化。

## 去重与技能兼容

| 本地内容 | 本 fork 使用的唯一入口 | 处理 |
|---|---|---|
| 13 个 `galaxy-*` 技能 | `skills/galaxy/`，先经 `sc2-galaxy-scripting` | 正文已覆盖；保留上游更明确的 GUI/源码和语法兼容边界 |
| 5 个 `sc2data-*` 技能 | `skills/sc2data/`，先经 `sc2-catalog-xml` | 正文已覆盖，不覆盖或复制 |
| `sc2-units-reference` | [兼容入口](../../skills/sc2-units-reference/SKILL.md) → `sc2data-units-reference` | 只保留旧名转接 |
| `sc2-localization-and-text` | [兼容入口](../../skills/sc2-localization-and-text/SKILL.md) → `sc2-localization` | 四类文本、KSP 与检查流程已覆盖，只转接 |
| `_sc2q.py`、`_sc2ref.py` | `tools/sc2-catalog-query.py`、`tools/sc2-reference-query.py` | 不带入旧硬编码路径和按排序猜覆盖值的逻辑 |
| `SC2GameData-master` | 上游内置参考优先；额外版本由 `sc2-reference-query.py --root` 查询 | 外部共享资料，不复制整树 |
| 社区例图、战术 AI、术语 | [补充资料技能](../../skills/sc2-community-reference/SKILL.md) | 按具体主题加载 |

除旧名兼容外，技能文件名不同不等于能力缺失；不把旧技能的限制覆盖到上游修订过的规则上。代码实现与有效值仍以当前项目及活动依赖为准。

## 外部资料与现有工具兼容

在本工作区现有布局中，共享资料树相对本 fork 为 `../参考资料/SC2GameData-master`。其他机器将下面的路径替换为实际位置；不修改默认项目配置或把参考设为活动依赖。

```powershell
python tools/sc2-reference-query.py --root "../参考资料/SC2GameData-master" object Unit:Marine --component liberty.sc2mod --limit 1
```

上游内置参考仍可直接查询：

```powershell
python tools/sc2-reference-query.py object Unit:Marine --component liberty.sc2mod --limit 1
```

这些命令查询参考中的显式 XML，不计算当前项目完整有效值。项目有效值使用已有 catalog 工具，按其依赖/索引检查流程执行。社区地图的 `Triggers` 从本页案例索引直接读取；没有把这些节选冒充为上游官方案例索引。

教学视频 `1-【星际2编辑器】几种单位常见“创建动画”的制作(触发器)-1080P 高清-AV…` 保留在本地 `参考资料/教学视频/`，不重复上传；对应的出生方式触发器可从案例索引查询。其他完整地图与二进制资产也保留在原位置。

## 来源与校验

导入内容来自用户提供的本地 `参考资料/`；准确相对路径、字节数、SHA-256、导入/复用决定和上游提交均在 [manifest.json](manifest.json)。原文件未改动。社区案例、词典及翻译记忆未附可核验的原始下载地址、作者或独立许可，来源待补；保留文件中已有声明，不推定归本 fork 原创。官方脚本也保留原文，不重新声明版权。

SHA-256 去重覆盖接入时的上游已跟踪文件和本次选定文件；工具/技能按能力另行比较并映射。记录中的 `path` 相对仓库根目录，可能指向另一个案例的唯一副本。Git 属性保留导入文件原始字节，以便克隆后再次核对；`manifest.json` 自身不参与自校验。
