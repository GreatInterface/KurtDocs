# EquipmentManager

>  `UKurtEquipmentManagerComponent` 主要负责管理角色当前装备的 `UKurtEquipmentInstance`。库存系统中的装备项 (`Equipment`) 均由 `EquipmentManager` 进行管理。

## **主要功能**

- **装备管理**：允许装备 (`EquipItem`)、卸下 (`UnequipItem`)、丢弃 (`DropItem`) 物品
- **可见性控制**：调整装备的可见性 (`SetItemVisible`)
- **查询功能**：提供获取当前已装备物品的 API，例如查找特定类型的装备 (`GetFirstInstanceOfDefinition`, `GetEquipmentsOfType`)

------

## **Public**

### **装备管理**

1. bool `CanEquipmentItem`(TEnumAsByte< EEquipmentVisibilityChannel::Type > Channel) const

	- **描述**: 判断某个 `VisibilityChannel` 是否允许装备物品。

	- **参数**: `Channel` - 需要检查的装备可见性通道。

	- **返回值**: `true` 表示可以装备，`false` 表示不可装备。


2. UKurtEquipmentInstance* `EquipItem`(TSubclassOf< UKurtEquipmentDefinition > EquipmentDefinition)

	- **描述**: 装备指定 `EquipmentDefinition` 生成的装备实例。

	- **参数**: `EquipmentDefinition` - 需要装备的 `EquipmentDefinition` 子类。

	- **返回值**: 返回装备的 `UKurtEquipmentInstance`，如果装备失败则返回 `nullptr`。

	- **权限**: 仅服务器端可调用 (`BlueprintAuthorityOnly`)。


3. void `UnequipItem`(UKurtEquipmentInstance* Instance)

	- **描述**: 卸下指定装备实例，但不会销毁它。

	- **参数**: `Instance` - 需要卸下的 `UKurtEquipmentInstance`。

	- **权限**: 仅服务器端可调用 (`BlueprintAuthorityOnly`)。


4. void `DropItem`(UKurtEquipmentInstance* Instance)

	- **描述**: 将当前装备丢弃。

	- **参数**: `Instance` - 需要丢弃的 `UKurtEquipmentInstance`。

	- **权限**: 仅服务器端可调用 (`BlueprintAuthorityOnly`)。


------

### **可见性控制**

1. void `SetItemVisible`(UKurtEquipmentInstance* Instance)
	- **描述**: 设置装备的可见性，可能影响 `VisibilityChannel` 的其他装备。


------

### **查询装备**

1. UKurtEquipmentInstance* `GetFirstInstanceOfDefinition`(TSubclassOf<UKurtEquipmentDefinition> Definition) const

	- **描述**: 获取第一个匹配 `Definition` 的装备实例。

	- **参数**: `Definition` - 需要查找的 `UKurtEquipmentDefinition` 子类。

	- **返回值**: 返回找到的 `UKurtEquipmentInstance`，如果没有匹配的装备，则返回 `nullptr`。


2. TArray<UKurtEquipmentInstance*> `GetEquipmentsOfType`(TSubclassOf<UKurtEquipmentInstance> Type) const

	- **描述**: 获取所有匹配 `Type` 的装备实例。

	- **参数**: `Type` - 需要查找的 `UKurtEquipmentInstance` 子类。

	- **返回值**: 返回一个 `TArray`，包含所有匹配的 `UKurtEquipmentInstance`。


------

## **私有成员**

 UPROPERTY(Replicated) FKurtEquipmentList `EquipmentList`

- **描述**: 角色当前已装备的装备列表。