# InventoryManagerComponent

> **概述**：
>
> `UKurtInventoryManagerComponent` 是一个 `UActorComponent`，用于管理角色的物品系统。它提供了添加、移除物品的功能，并支持蓝图调用。

### **方法**

```C++
UFUNCTION(BlueprintPure)
TArray<UKurtItemInstance*> GetItems() const;
```

- **描述**：获取当前所有的物品实例列表。
- **返回值**：包含 `UKurtItemInstance*` 的数组。

------

```CPP
UFUNCTION(BlueprintCallable, Category=Inventory)
UKurtItemInstance* AddItemFromDefinition(TSubclassOf<UKurtInventoryItemDefinition> ItemDefinition, int32 StackCount = 1);
```

- **描述**：根据 `UKurtInventoryItemDefinition` 创建物品实例并添加到库存。
- 参数

	- `ItemDefinition`：物品的类定义。
- `StackCount`：堆叠数量，默认为 `1`。
- **返回值**：返回创建的 `UKurtItemInstance*`。

------

```C++
UFUNCTION(BlueprintCallable, Category=Inventory)
void RemoveItem(UKurtItemInstance* ItemInstance, const int32 StackCount = 1);
```

- **描述**：移除库存中的物品，可以指定移除的堆叠数量。
- 参数

	- `ItemInstance`：要移除的物品实例。
- `StackCount`：要移除的数量，默认为 `1`。
- **返回值**：无。

---

### **属性**

```CPP
UPROPERTY()
FKurtInventoryItemContainer SlotContainer;
```

- **描述**：存储角色的物品容器，内部维护所有持有的物品。