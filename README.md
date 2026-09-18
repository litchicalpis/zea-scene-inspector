# Zea · 场景格信息 0.1.0

Foundry VTT v12 Pre-release 测试版。独立模组 ID：`zea-scene-inspector`。随包提供 7040 × 3200 的商船四层背景，以及从原 HTML 提取的 2688 个格子的信息。左上 +20 ft、右上 +10 ft、左下 0 ft、右下 −10 ft；每格 80 px / 5 ft。货舱上方立柱已移至 (13,7)、(17,7)，下方保持 (13,10)、(17,10)。

## 安装与使用

1. 在 Foundry Setup → Add-on Modules → Install Module 的 Manifest URL 中填写 `https://raw.githubusercontent.com/litchicalpis/zea-scene-inspector/main/module.json`。也可从 [v0.1.0 Release](https://github.com/litchicalpis/zea-scene-inspector/releases/tag/v0.1.0) 下载 `zea-scene-inspector-v0.1.0.zip`，解压到 `Data/modules`，使清单位于 `Data/modules/zea-scene-inspector/module.json`。请使用完整安装 ZIP，不使用 GitHub 自动生成的 Source code ZIP。
2. 重启 Foundry，在 World 的“管理模组”启用 **Zea · 场景格信息**。所有客户端刷新。
3. GM 在“配置设置 → 模组设置 → 场景格信息”点击“打开格信息窗口”；或使用左侧 Token 工具组中的“查看格信息”按钮。
4. 展开“场景与 GM 注记”，点击“打开 / 创建商船场景”。已有本模组场景时打开已有场景，否则新建。只切换当前 GM 的视图，不自动将所有玩家拉入场景。GM 可再通过 Foundry 的“激活”切换玩家场景。
5. 窗口打开时，鼠标移入地图格子即显示信息，单击固定；“继续跟随”恢复悬停查看。拖动 Token 和右键平移不会固定格子。关闭窗口即停止监听并清除本机高亮。
6. 通过图层下拉框和“列,行”坐标定位，或点击区域、设备、楼梯入口移动视图。定位不会传送 Token，也不会改变 Token 高程。

已有同款 PNG 场景可使用“关联当前场景”，须保持 7040 × 3200 尺寸、背景偏移与旋转为 0、缩放为 1。关联只写入本模组的数据集引用。建议 Foundry 方格设为 80 px、5 ft；背景已印有格线，新建场景默认隐藏重复的 Foundry 格线。支持正常的场景外沿留白、画布平移和缩放。

展示内容包括原坐标、高程、净空、设备高度、地形、通行说明、视线说明、四边墙门、支座、作业区、房间与设备说明、楼梯连接。船图状态固定为小艇收存、货舱口关闭、空货舱，与随包 PNG 一致。

## GM 注记

源 HTML 的 GM 注记不进入安装 ZIP、GitHub、公共 JSON、场景 flags 或 Journal。本地构建时生成单独的 `dist/merchant-gm-notes.private.json`，请只由 GM 保存。通过 GitHub 安装后可直接手工填写本机 GM 注记，或导入 GM 自己保留的注记备份。

GM 在对应船图窗口展开“场景与 GM 注记”，点击“导入本机 GM 注记”并选择该文件。注记存于 Foundry 的 client 设置，按 World、GM 用户、场景分别保存，仅保存在该浏览器；其他 GM 电脑不会自动同步。可在选中格子的“本机 GM 注记”中编辑、保存，并通过“导出本机 GM 注记”备份。导入按格合并，同格替换。换设备或清理浏览器前先导出。

基础船图和普通格说明是公共素材；开启 Token 视野后，查看器只显示当前可见格子，但公共素材并非秘密数据容器。秘密剧情应写入本机 GM 注记。

## 功能边界

本版提供信息查看，不自动生成 Foundry 墙、门、灯光、地形规则或 Token，也不接入贸易库存或海战裁决。墙门与高程文字描述来自原船图；如果之后手动修改实际场景墙门，这些文字不会自动同步。两模组的现有战役、日志、贸易卡和海战状态无需迁移。

## 为什么独立

推荐独立发布 `zea-scene-inspector`，并在需要时给贸易 / 海战模组添加可选入口。贸易模组负责航行、库存、交易与日期；海战模组负责双方规则和裁决；本模组负责 Foundry 原生场景上的格信息。船图可以单独用于船内战斗，也可以日后扩展其他场景。

若必须并入现有模块，贸易地图的货舱展示与此数据关系更近，但会使不玩贸易的 World 也需要启用整个贸易模组。代码可以放在同一个 GitHub 仓库的不同目录；只要仍作为两个 Foundry 模组安装，就需要各自的 ID、清单与安装包。

发布采用独立仓库 [litchicalpis/zea-scene-inspector](https://github.com/litchicalpis/zea-scene-inspector)、稳定 `main/module.json` 清单和版本固定的 Release ZIP。仓库根目录提供 README 与稳定清单，完整运行代码、船图和公开格数据随安装 ZIP 分发。Release 附件为 `module.json`、完整安装 ZIP、`SHA256SUMS.txt`，不包含私人注记、浏览器测试资料或整个工作区。

## 开发与验证

以下命令用于本地开发工作区，需要 Node 22+，不依赖 npm 下载包。源船图 HTML、PNG 和布局 JSON 位于本目录的上一级；开发工具、测试和原始 HTML 不在 GitHub 安装包中。安装和运行模组不需要 Node。

```text
npm run build
npm test
npm run test:browser
```

浏览器测试使用真实模块代码与模拟 v12 接口，验证悬停、点击固定、拖动不固定、四层定位、GM 创建与关联、玩家权限、私有注记、生命周期清理和界面渲染。它不代替安装后在真实 FVTT v12 World 的多人验收。

运行 API：

```js
await game.modules.get("zea-scene-inspector").api.open();
await game.modules.get("zea-scene-inspector").api.openMerchantScene();
game.modules.get("zea-scene-inspector").api.inspect("lower", 13, 7);
```

`openMerchantScene`、`bindCurrentScene` 仅限 GM。`inspect` 要求先打开关联场景的查看器，返回是否成功；只在本机选择并定位。

开发依据：[v12 Canvas](https://foundryvtt.com/api/v12/classes/client.Canvas.html)、[v12 ApplicationV2](https://foundryvtt.com/api/v12/classes/foundry.applications.api.ApplicationV2.html)、[模组清单](https://foundryvtt.com/article/module-development/)。
