# AbilitySystemComponent

## OnPawnAvatarSet

在`InitAbilityActorInfo`阶段，对所有Instance Ability都尝试激活OnPawnAvatarSet()事件，该事件为`BlueprintImplementableEvent`，可以在蓝图中实现它

## TryActivateAbilityOnSpawn

在`InitAbilityActorInfo`阶段，`KurtASC`会尝试激活**所有**`ActivationPolicy`为`EKurtAbilityActivationPolicy::OnSpawn`的Ability

## AddDynamicTagGameplayEffect

使用指定的GE添加指定的动态授予Tag，相较于SetLooseGameplayTagCount，使用该方法可以依赖GE实现动态卸载

## RemoveDynamicTagGameplayEffect

立刻卸载Tag

//TODO : RelationshipMapping
