# Zea · 场景格信息 0.2.0

Foundry VTT v12 Pre-release 测试版。独立模组 ID：`zea-scene-inspector`。随包提供 7040 × 3200 的商船四层背景，以及从原 HTML 提取的 2688 个格子的信息。左上 +20 ft、右上 +10 ft、左下 0 ft、右下 −10 ft；每格 80 px / 5 ft。货舱上方立柱已移至 (13,7)、(17,7)，下方保持 (13,10)、(17,10)。

0.2.0增加狼栈码头突堤、仓库地坪及检货夹层，兼容原标注合图和无标注纯底图。进入World仍不自动弹窗，只有手动打开查看器才监听鼠标。原商船场景关联、API和本机GM注记保持兼容，无需迁移或重建。

## 扩展评估与支持地图

**可以直接扩展现有模组，无需另建模组。** 码头数据与商船采用同类逐格结构，包含高程、净空、遮挡、边界和连接。需要解除原有单商船ID、固定图片尺寸与四层布局限制，并处理跨地图通口、分离楼层和本机注记隔离；不是把新PNG替换进旧坐标表。

| 数据集ID | 场景与背景 | 尺寸 | 图格起点 |
|---|---|---|---|
| `sunless-merchant-v2` | 原商船四层标注合图 | 7040×3200 | 保持原四面板布局 |
| `wolfstack-quay-v1` | 狼栈突堤标注图 | 4160×5440 | (80,240) |
| `wolfstack-warehouse-v1` | 仓库地坪与夹层标注合图 | 7040×2560 | (80,240)、(3600,240) |
| `wolfstack-quay-clean-v1` | 狼栈突堤纯底图 | 4000×5120 | (0,0) |
| `wolfstack-warehouse-main-clean-v1` | 仓库地坪纯底图 | 3360×2240 | (0,0) |
| `wolfstack-warehouse-upper-clean-v1` | 仓库夹层纯底图 | 3360×2240 | (0,0) |

全部为80px／5ft。突堤50×64格，仓库每层42×28格；仓库夹层+10ft、岸面0ft、驳船甲板−5ft、水面−10ft，梯道保留逐格实际标高。类型与边界使用陆地／方位文字，不沿用船艏艉称谓。关闭门、攀爬、水格与无地板空域不会被误示为普通通路。

建议战术场景选纯底图，分别建立码头、仓库地坪、仓库夹层；模组为纯底图显示Foundry方格，为已有格线的标注图隐藏重复格线。既有标注图场景也能关联，不必重绘地图。所有坐标均相对各自背景，保留场景外沿留白、画布缩放和平移支持。

## 安装与使用

1. 在 Foundry Setup → Add-on Modules → Install Module 的 Manifest URL 中填写 `https://raw.githubusercontent.com/litchicalpis/zea-scene-inspector/main/module.json`。也可从 [v0.2.0 Release](https://github.com/litchicalpis/zea-scene-inspector/releases/tag/v0.2.0) 下载 `zea-scene-inspector-v0.2.0.zip`，解压到 `Data/modules`，使清单位于 `Data/modules/zea-scene-inspector/module.json`。原安装地址不变；请使用完整安装 ZIP，不使用 GitHub 自动生成的 Source code ZIP。
2. 重启 Foundry，在 World 的“管理模组”启用 **Zea · 场景格信息**。所有客户端刷新。
3. GM 在“配置设置 → 模组设置 → 场景格信息”点击“打开格信息窗口”；或使用左侧 Token 工具组中的“查看格信息”按钮。
4. 展开“场景与 GM 注记”，在“地图与底图版本”选择所需地图，点击“打开 / 创建所选地图场景”。已有对应数据集场景时打开已有场景，否则新建。只切换当前 GM 的视图，不自动将所有玩家拉入场景。GM 可再通过 Foundry 的“激活”切换玩家场景。
5. 窗口打开时，鼠标移入地图格子即显示信息，单击固定；“继续跟随”恢复悬停查看。拖动 Token 和右键平移不会固定格子。关闭窗口即停止监听并清除本机高亮。
6. 通过图层下拉框和“列,行”坐标定位，或点击区域、设备、楼梯入口移动视图。定位不会传送 Token，也不会改变 Token 高程。

已有同款 PNG 场景可选择对应地图，再使用“将当前场景关联至所选地图”。须保持表中尺寸、背景偏移与旋转为0、缩放为1，并确认图像内容和图格起点匹配。仓库两张纯底图尺寸相同，必须人工确认选择正确楼层；模组不会通过尺寸猜测图像内容。关联经GM确认后只写入本模组的数据集引用，不更换背景或改动墙、门、Token。场景方格建议80px、5ft；图像被裁切、改比例或挪动格网后不能直接沿用关联。

同场景楼梯定位本场景；标注码头连接标注仓库，纯底码头连接纯底仓库地坪，纯底仓库楼梯连接另一楼层。GM点击跨场景连接可打开或创建目标场景并定位；玩家可查看连接说明，但跨场景操作须由GM进行。不会激活目标场景、传送Token或改变Token高程，也不接入Multilevel Tokens。已有多个相同数据集场景时默认打开列表中的首个。

展示内容包括原坐标、高程、净空、设备高度、地形、通行说明、视线说明、四边墙门、支座、作业区、房间与设备说明、楼梯连接。船图状态固定为小艇收存、货舱口关闭、空货舱，与随包 PNG 一致。

## GM 注记

源商船HTML和码头数据中的GM注记、遭遇安排不进入安装ZIP、GitHub、公共JSON、场景flags或Journal。商船本地构建保留单独的`dist/merchant-gm-notes.private.json`，码头私有构建产物位于`dist/private/`，请只由GM保存。通过GitHub安装后可直接手工填写本机GM注记，或导入GM自己保留的注记备份；只有格注记文件可导入查看器，遭遇安排不自动载入。

GM在对应场景展开“场景与 GM 注记”，点击“导入本机 GM 注记”并选择该地图的文件。注记存于Foundry的client设置，按World、GM用户、场景和数据集分别保存，仅保存在该浏览器；不同底图版本不会混用注记，其他GM电脑不会自动同步。可在选中格子的“本机 GM 注记”中编辑、保存，并导出备份。导入按格合并，同格替换；错误地图的注记文件会拒绝。换设备或清理浏览器前先导出。

基础地图和普通格说明是公共素材；开启Token视野后，查看器只显示当前可见格子，但随包图片、公开数据及地图连接不具保密性，能够通过资源路径读取。秘密剧情应写入本机GM注记。

## 功能边界

本版提供信息查看，不自动生成Foundry墙、门、灯光、地形规则或Token，也不接入贸易库存或海战裁决。墙门与高程文字描述来自原地图；门的“初始关闭”不是实时Foundry门状态，手动修改实际场景墙门后文字不会自动同步。贸易／海战既有战役、日志和状态均不受影响。

## 为什么独立

推荐独立发布 `zea-scene-inspector`，并在需要时给贸易 / 海战模组添加可选入口。贸易模组负责航行、库存、交易与日期；海战模组负责双方规则和裁决；本模组负责 Foundry 原生场景上的格信息。船图可以单独用于船内战斗，也可以日后扩展其他场景。

若必须并入现有模块，贸易地图的货舱展示与此数据关系更近，但会使不玩贸易的 World 也需要启用整个贸易模组。代码可以放在同一个 GitHub 仓库的不同目录；只要仍作为两个 Foundry 模组安装，就需要各自的 ID、清单与安装包。

发布采用独立仓库 [litchicalpis/zea-scene-inspector](https://github.com/litchicalpis/zea-scene-inspector)、稳定 `main/module.json` 清单和版本固定的 Release ZIP。仓库根目录提供 README 与稳定清单，完整运行代码、船图和公开格数据随安装 ZIP 分发。Release 附件为 `module.json`、完整安装 ZIP、`SHA256SUMS.txt`，不包含私人注记、浏览器测试资料或整个工作区。

## 开发与验证

以下命令用于本地开发工作区，需要Node 22+，不依赖npm下载包。源船图HTML、PNG和布局JSON位于本目录的上一级；码头来源为上一级`wolfstack_docks_scene/output/`中的数据、布局与PNG。开发工具、测试、原始HTML及私有构建产物不在安装包中。安装和运行模组不需要Node。仅构建已有码头结果，不重新生成或修改源地图。

```text
npm run build
npm test
npm run test:browser
```

浏览器测试使用真实模块代码与模拟v12接口，验证商船与码头的悬停、点击固定、拖动不固定、分层定位、跨场景连接、GM创建与关联、玩家权限、私有注记、生命周期清理和界面渲染。它不代替安装后在真实FVTT v12 World的多人验收；本版本继续标记Pre-release，先备份并在测试World检查背景、楼梯、注记和玩家可见性。

运行 API：

```js
await game.modules.get("zea-scene-inspector").api.open();
await game.modules.get("zea-scene-inspector").api.openMerchantScene();
game.modules.get("zea-scene-inspector").api.getDatasets();
await game.modules.get("zea-scene-inspector").api.openDatasetScene("wolfstack-quay-clean-v1");
await game.modules.get("zea-scene-inspector").api.bindCurrentScene("wolfstack-quay-clean-v1");
game.modules.get("zea-scene-inspector").api.inspect("lower", 13, 7);
```

`openMerchantScene`、`openDatasetScene`、`bindCurrentScene`仅限GM。`inspect`要求先打开关联场景的查看器，返回是否成功；只在本机选择并定位。商船保留原layer名称，码头为`main`，仓库为`main`／`upper`；在码头图上请使用对应图层而非示例商船`lower`。

开发依据：[v12 Canvas](https://foundryvtt.com/api/v12/classes/client.Canvas.html)、[v12 ApplicationV2](https://foundryvtt.com/api/v12/classes/foundry.applications.api.ApplicationV2.html)、[模组清单](https://foundryvtt.com/article/module-development/)。
