# GameplayAbility

## EKurtAbilityActivationPolicy

定义该 Ability 的触发方式：

- OnInputTriggered
	- 当输入触发时，立即尝试激活该 Ability。
- WhileInputActive
	- 在输入保持激活状态时，持续尝试激活该 Ability。
- OnSpawn
	- 在 `InitAbilityActorInfo` 初始化时，立即尝试激活该 Ability。

## EKurtAbilityActivationGroup

定义`Instance Ability`之间的激活关系，特别是**专属能力（Exclusive Ability）**，在每个 GAS 实例中只能存在一个。

- Independent
	- 该 Ability 独立运行，不受其他 Ability 影响，也不会影响其他 Ability。
- Exclusive_Replaceable
	- 该 Ability 为`专属能力`，若另一个专属能力尝试`激活`或`改变其关系`，则该 Ability 会主动取消自身，以让位于新的专属能力。
- Exclusive_Blocking
	- 该 Ability 为`专属能力`，若另一个专属能力尝试激活，则会阻止其`注册`或`改变其关系`（例如：Independent->Blocking），确保自身持续生效。
	- 确保在`ActivateAbility`期间改变该Group为`Exclusive_Blocking`

---

## CanChangeActivationGroup

是否能改变该Ability的ActivationGroup

- 如果已经拥有`Exclusive_Blocking`的Ability，则阻止任何能力更改为`Exclusive_Blocking`
- 如果当前 Ability 不能被取消，不能变为 `Exclusive_Replaceable`。

