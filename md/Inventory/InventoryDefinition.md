# InventoryDefinition

## **UKurtItemFragment**

#### 概述

`UKurtItemFragment` 是一个抽象基类，表示物品的片段（Fragment）。
它允许通过 `EditInlineNew` 和 `DefaultToInstanced` 进行实例化，以便在 `UKurtInventoryItemDefinition` 中编辑。

#### **方法**

```cpp
virtual void OnInstanceCreated(const UKurtItemInstance* Instance) const {}
```

- **描述**：在物品实例被创建时调用，子类可以重写此方法以执行特定的初始化逻辑。
- 参数

	- `Instance`：指向 `UKurtItemInstance` 的常量指针，表示创建的物品实例。

------

## **UKurtInventoryItemDefinition**

> **概述**
>
> `UKurtInventoryItemDefinition` 是物品的定义类，用于描述游戏中的可用物品。它包含物品的基本属性，如名称、标签、是否可堆叠等，并且使用 `UKurtItemFragment` 作为物品的主要信息。

##### **方法**

```cpp
const UKurtItemFragment* FindFragmentByClass(TSubclassOf<UKurtItemFragment> FragmentClass) const;
```

- **描述**：查找指定类型的 `UKurtItemFragment` 片段。

- 参数

	- `FragmentClass`：需要查找的 `UKurtItemFragment` 子类类型。

- **返回值**：找到的 `UKurtItemFragment` 指针，如果不存在该类型的片段，则返回 `nullptr`。

---

##### **属性**

```cpp
UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Display)
FText ItemName;
```

- 描述：物品名字

```cpp
UPROPERTY(EditDefaultsOnly, Category=Display)
FGameplayTag ItemTag;
```

- **描述**：物品的标签，用于分类或标识物品。

```cpp
UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = "Inventory|Setting")
bool bStackable = false;
```

- **描述**：指示该物品是否可堆叠。
- **默认值**：`false`（不可堆叠）。

```cpp
UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = "Inventory|Setting", meta = (EditCondition = "bStackable"))
int32 MaxStackCount = 999;
```

- **描述**：如果物品可堆叠，指定最大堆叠数量。
- **编辑条件**：仅在 `bStackable` 为 `true` 时可编辑 (`EditCondition = "bStackable"`)。
- **默认值**：`999`。

```cpp
UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Display, Instanced)
TArray<TObjectPtr<UKurtItemFragment>> Fragments;
```

- **描述**：物品的片段（`UKurtItemFragment`）数组，可用于扩展物品功能。

