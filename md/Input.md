# Input

## 玩家输入由`HeroComponent`进行管理

![](E:/SourceLibrary/GitBook/KurtDocs/image/Input%20diagram-2025-03-04-131043.png)

<div align="left"><figure><img src="../.gitbook/assets/Input diagram-2025-03-04-131043.png" alt=""><figcaption></figcaption></figure></div>

* 当初始化链到达`DataAvailable`状态时，HeroComponent会调用`UKurtHeroComponent::InitializePlayerInput`完成InputAction的绑定，绑定基于以下两步：
  * 绑定InputAction与InputTag(以便于Press/Released Func索引)
  * 绑定InputAction与Press/Released Function
* 当开始处理输入时会进行如下两步：
  1. 生产者： Trigger Press Func （UKurtAbilitySystemComponent::AbilityInputTagPressed）
     * 将任务转发给`AbilitySystemComponent`，ASC会根据InputTag，索引出相应的Ability，并放入`InputPressedSpecHandles`
  2. 消费者：AKurtPlayerController::PostProcessInput（Tick执行）
     * 继续转发给`AbilitySystemComponent`，开始消费`InputPressedSpecHandles`
       * 如果Ability已经处于激活状态，InvokeReplicatedEvent(EAbilityGenericReplicatedEvent::InputPressed)
       * 否则尝试激活能力

## 配置Input Config
