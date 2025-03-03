# Experience

>  Experience是一种自定义、可配置的、供游戏初始化时进行资源异步加载的GameState

每个Level都可在对应的`WorldSetting`配置指定的`Experience`，默认为DefaultKurtExperience。

## Experience Definition

> 定义：const PrimaryDataAsset
>
> Experience围绕`ExperienceDefinition`进行资源加载

Experience Definition围绕如下数据进行加载：

1. PawnData
	- 为玩家默认生成的Pawn，包括的InputConfig、CameraMode以及Ability的相关信息
2. GameFeatures
3. GameFeatureActions
4. ExperienceActionSet（GameFeatures + GameFeatureActions）

---

Experience在游戏加载/卸载时会经历以下状态(`EKurtExperienceLoadState`)：

- Unloaded
- Loading
- LoadingGameFeatures
- LoadingChaosTestingDelay
	- 提供控制台变量来测试延迟的体验加载（例如，模拟慢速计算机/网络）。
- ExecutingActions
- Loaded
- Deactivating

