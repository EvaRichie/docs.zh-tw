---
title: 實作值物件
description: 容器化 .NET 應用程式的 .NET 微服務架構 | 深入了解使用新 Entity Framework 功能實作值物件的詳細資料與選項。
ms.date: 08/21/2020
ms.openlocfilehash: 1cb7ce04b3ab2f6da25f398e016baf60b863fb6b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169202"
---
# <a name="implement-value-objects"></a>實作值物件

如前面各節中討論的實體和彙總，身分識別是實體的基礎。 不過，系統中有許多物件和資料項目不需要身分識別和身分識別追蹤，例如值物件。

值物件可以參考其他實體。 例如，在產生描述如何從某點到另一點的路由的應用程式中，該路由就是值物件。 它會是特定路由的點快照集，但此建議的路由不會有身分識別，雖然它在內部參考縣 (市)、街道等實體。

圖 7-13 顯示 Order 彙總內的 Address 值物件。

![此圖表顯示 Order 匯總內的 Address 值物件。](./media/implement-value-objects/value-object-within-aggregate.png)

**圖 7-13**。 訂單彙總內的 Address 值物件

如圖 7-13 所示，實體通常是由多個屬性組成。 例如， `Order` 實體可以模型化為具有身分識別的實體，並在內部包含一組屬性，例如 [訂單識別碼]、[日期（日期）]、[OrderItems] 等等。但位址（只是由國家/地區、街道、縣/市組成的複雜值，而且在此網域中沒有任何身分識別）必須模型化並視為值物件。

## <a name="important-characteristics-of-value-objects"></a>值物件的重要特性

值物件有兩個主要特性：

- 它們沒有任何身分識別。

- 它們具有不變性。

第一個特性已討論過。 不變性是重要需求。 物件一旦建立，值物件的值必須不可變。 因此，在建立物件時，您必須提供必要的值，但您不能在物件的存留期內允許它們變更。

值物件因為不可變的本質，可讓您執行某些技巧以提升效能。 特別是在有數千個值物件執行個體的系統中，它們之中許多都有相同的值。 其不可變的本質可讓它們重複使用。它們可以是可互換的物件，因為它們的值相同，而且它們沒有任何身分識別。 這種最佳化有時會造成執行速度緩慢的軟體和效能良好的軟體之間的差異。 當然，所有這些情況都取決於應用程式環境和部署內容。

## <a name="value-object-implementation-in-c"></a>以 C\# 實作值物件

就實方面而言，您可以有一個值物件基類，它有一個基本的公用程式方法，像是根據 (的所有屬性，因為值物件不能以識別) 和其他基本特性為基礎。 下列範例示範 eShopOnContainers 訂購微服務中使用的值物件基底類別。

```csharp
public abstract class ValueObject
{
    protected static bool EqualOperator(ValueObject left, ValueObject right)
    {
        if (ReferenceEquals(left, null) ^ ReferenceEquals(right, null))
        {
            return false;
        }
        return ReferenceEquals(left, null) || left.Equals(right);
    }

    protected static bool NotEqualOperator(ValueObject left, ValueObject right)
    {
        return !(EqualOperator(left, right));
    }

    protected abstract IEnumerable<object> GetEqualityComponents();

    public override bool Equals(object obj)
    {
        if (obj == null || obj.GetType() != GetType())
        {
            return false;
        }

        var other = (ValueObject)obj;

        return this.GetEqualityComponents().SequenceEqual(other.GetEqualityComponents());
    }

    public override int GetHashCode()
    {
        return GetEqualityComponents()
            .Select(x => x != null ? x.GetHashCode() : 0)
            .Aggregate((x, y) => x ^ y);
    }
    // Other utility methods
}
```

實作您實際的值物件時，您可以使用這個類別，如同對待下列範例所示的 Address 值物件一樣：

```csharp
public class Address : ValueObject
{
    public String Street { get; private set; }
    public String City { get; private set; }
    public String State { get; private set; }
    public String Country { get; private set; }
    public String ZipCode { get; private set; }

    public Address() { }

    public Address(string street, string city, string state, string country, string zipcode)
    {
        Street = street;
        City = city;
        State = state;
        Country = country;
        ZipCode = zipcode;
    }

    protected override IEnumerable<object> GetEqualityComponents()
    {
        // Using a yield return statement to return each element one at a time
        yield return Street;
        yield return City;
        yield return State;
        yield return Country;
        yield return ZipCode;
    }
}
```

您可以看到此 Address 的值物件實作沒有身分識別，因此在 Address 類別，甚至是 ValueObject 類別也沒有識別碼欄位。

在 Entity Framework (EF) 的類別中不能有任何識別碼欄位，除非 EF Core 2.0，這可大幅協助您以沒有識別碼的方式來執行更好的值物件。 這正是下一節的說明。

它可能會有人認為該值物件是不可變的，應該是唯讀的 (也就是只有) 的屬性，而且的確如此。 然而，值物件通常會經過序列化和還原序列化，以通過訊息佇列，而且是唯讀的，會使還原序列化程式無法指派值，因此您只需將其保留為 `private set` 唯讀，這就足以實際運作。

## <a name="how-to-persist-value-objects-in-the-database-with-ef-core-20-and-later"></a>如何在具有 EF Core 2.0 和更新版本的資料庫中保存值物件

您只看到如何在您的網域模型中定義值物件。 但是，您要如何使用 Entity Framework Core 將它保存在資料庫中，因為它通常是以身分識別為目標的實體？

### <a name="background-and-older-approaches-using-ef-core-11"></a>使用 EF Core 1.1 的背景和較舊的方法

在使用 EF Core 1.0 和1.1 時，使用的限制是，您無法使用傳統 .NET Framework 中 EF 6.x 所定義的 [複雜類型](xref:System.ComponentModel.DataAnnotations.Schema.ComplexTypeAttribute) 。 因此，如果使用 EF Core 1.0 或 1.1，您需要使用識別碼欄位將您的值物件儲存為 EF 實體。 然後，它會看起來更像是沒有任何身分識別的值物件，您可以隱藏它的識別碼，以便您明白表示值物件的識別碼在網域模型中不重要。 您可以將識別碼當成 [shadow property](/ef/core/modeling/shadow-properties) (shadow 屬性) 使用，隱藏該識別碼。 因為已在 EF 基礎結構層級設定模型中隱藏識別碼的組態，所以對您的網域模型而言，它幾乎是不存在的。

在 eShopOnContainers 的初始版本中 (.NET Core 1.1)，已在基礎結構專案中使用 Fluent API，以下列方式在 DbContext 層級實作 EF Core 基礎結構所需要的隱藏識別碼。 因此，從網域模型的觀點而言，識別碼已隱藏，但仍會出現在基礎結構中。

```csharp
// Old approach with EF Core 1.1
// Fluent API within the OrderingContext:DbContext in the Infrastructure project
void ConfigureAddress(EntityTypeBuilder<Address> addressConfiguration)
{
    addressConfiguration.ToTable("address", DEFAULT_SCHEMA);

    addressConfiguration.Property<int>("Id")  // Id is a shadow property
        .IsRequired();
    addressConfiguration.HasKey("Id");   // Id is a shadow property
}
```

不過，該值物件保存在資料庫中，就像是不同資料表中的一般實體。

在 EF Core 2.0 和更新版本中，有更好的新方法可保存值物件。

## <a name="persist-value-objects-as-owned-entity-types-in-ef-core-20-and-later"></a>在 EF Core 2.0 和更新版本中，將值物件保存為擁有的實體類型

即使在 DDD 中的標準值物件模式與 EF Core 中擁有的實體類型之間有一些差距，目前仍是使用 EF Core 2.0 和更新版本保存值物件的最佳方式。 本節結尾會列出限制。

EF Core 從 2.0 版開始新增擁有的實體類型功能。

自有實體類型可讓您在自己的所有實體內，對應那些自己身分識別未在網域模型中明確定義並用作屬性的類型，例如值物件。 擁有的實體類型與另一個實體類型共用相同的 CLR 類型 (也就是說，它只是) 的一般類別。 包含定義導覽的實體是擁有者實體。 查詢擁有者時，預設包含擁有的類型。

只要查看領域模型，擁有的型別看起來就像它沒有任何身分識別。 不過，在幕後，擁有的類型的確具有身分識別，但擁有者導覽屬性是此身分識別的一部分。

自有類型的執行個體身分識別不完全屬於它們自己。 它包含三個元件：

- 擁有者的身分識別

- 指向它們的導覽屬性

- 在擁有類型集合的情況下，EF Core 2.2 和更新版本) 支援獨立元件 (。

例如，在 eShopOnContainers 的訂購網域模型中，屬於訂單實體的一部分，Address 值物件在擁有者實體內實作為擁有的實體類型，也就是訂單實體。 `Address` 是在網域模型中未定義識別屬性的類型。 它用做訂單類型的屬性，指定特定訂單的送貨地址。

依照慣例，會為擁有的類型建立陰影主索引鍵，而且會使用資料表分割將它對應至與擁有者相同的資料表。 這允許以類似傳統 .NET Framework 的 EF6 使用複雜類型的方式，使用擁有的類型。

請務必注意，EF Core 慣例永遠不會探索到擁有的類型，所以您不必明確宣告它們。

在 eShopOnContainers 中，于 OrderingCoNtext.cs 檔案的方法內 `OnModelCreating()` ，會套用多個基礎結構設定。 其中一個與訂單實體有關。

```csharp
// Part of the OrderingContext.cs class at the Ordering.Infrastructure project
//
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.ApplyConfiguration(new ClientRequestEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new PaymentMethodEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new OrderEntityTypeConfiguration());
    modelBuilder.ApplyConfiguration(new OrderItemEntityTypeConfiguration());
    //...Additional type configurations
}
```

下列程式碼會定義訂單實體的持續性基礎結構：

```csharp
// Part of the OrderEntityTypeConfiguration.cs class
//
public void Configure(EntityTypeBuilder<Order> orderConfiguration)
{
    orderConfiguration.ToTable("orders", OrderingContext.DEFAULT_SCHEMA);
    orderConfiguration.HasKey(o => o.Id);
    orderConfiguration.Ignore(b => b.DomainEvents);
    orderConfiguration.Property(o => o.Id)
        .ForSqlServerUseSequenceHiLo("orderseq", OrderingContext.DEFAULT_SCHEMA);

    //Address value object persisted as owned entity in EF Core 2.0
    orderConfiguration.OwnsOne(o => o.Address);

    orderConfiguration.Property<DateTime>("OrderDate").IsRequired();

    //...Additional validations, constraints and code...
    //...
}
```

在先前的程式碼中，`orderConfiguration.OwnsOne(o => o.Address)` 方法指定 `Address` 屬性是 `Order` 類型的擁有的實體。

根據預設，EF Core 慣例會將擁有的實體類型的屬性資料庫資料行命名為 `EntityProperty_OwnedEntityProperty`。 因此，的內部屬性 `Address` 會出現在資料表中 `Orders` ，其中包含、和) 的名稱 `Address_Street` 、 `Address_City` (`State` 等等 `Country` `ZipCode` 。

您可以附加 `Property().HasColumnName()` fluent 方法重新命名這些資料行。 如果發生 `Address` 是公用屬性的情況，對應會如同下例：

```csharp
orderConfiguration.OwnsOne(p => p.Address)
                            .Property(p=>p.Street).HasColumnName("ShippingStreet");

orderConfiguration.OwnsOne(p => p.Address)
                            .Property(p=>p.City).HasColumnName("ShippingCity");
```

您可以 `OwnsOne` 在流暢的對應中連結方法。 在下列假設性的範例中，`OrderDetails` 擁有 `BillingAddress` 和 `ShippingAddress`，它們兩個都是 `Address` 類型。 然後 `Order` 類型擁有 `OrderDetails`。

```csharp
orderConfiguration.OwnsOne(p => p.OrderDetails, cb =>
    {
        cb.OwnsOne(c => c.BillingAddress);
        cb.OwnsOne(c => c.ShippingAddress);
    });
//...
//...
public class Order
{
    public int Id { get; set; }
    public OrderDetails OrderDetails { get; set; }
}

public class OrderDetails
{
    public Address BillingAddress { get; set; }
    public Address ShippingAddress { get; set; }
}

public class Address
{
    public string Street { get; set; }
    public string City { get; set; }
}
```

### <a name="additional-details-on-owned-entity-types"></a>有關擁有的實體類型的其他詳細資料

- 當您使用 OwnsOne fluent API 將導覽屬性設定為特定類型時，會定義自有類型。

- 在我們的中繼資料模型中，自有類型的定義由下列項目組成：擁有者類型、導覽屬性，以及自有類型的 CLR 類型。

- 在我們的堆疊中，自有類型執行個體的身分識別 (金鑰) 是由擁有者類型的身分識別及自有類型的定義所組成。

#### <a name="owned-entities-capabilities"></a>擁有的實體功能

- 自有類型可以參考其他實體，可以是自有 (巢狀自有類型) 或非自有 (對其他實體的一般參考導覽屬性)。

- 您可以透過個別的導覽屬性，將相同的 CLR 類型對應為同一個擁有者實體中的不同自有類型。

- 資料表分割是依照慣例設定，但您可以選擇使用 ToTable 將擁有的類型對應到不同的資料表。

- 積極式載入會在擁有的類型上自動執行，也就是不需要 `.Include()` 在查詢上呼叫。

- 可以 `[Owned]` 使用 EF Core 2.1 和更新版本的屬性來設定。

- 可以處理所擁有類型的集合 (使用2.2 版和更新版本的) 。

#### <a name="owned-entities-limitations"></a>擁有的實體限制

- 您無法建立 `DbSet<T>` 由設計)  (的擁有類型。

- 您無法 `ModelBuilder.Entity<T>()` 在目前由設計)  (所擁有的類型上呼叫。

- 不支援選擇性的 (也就是，可以是可為 null) 擁有的類型，這些類型會與相同資料表中的擁有者對應 (也就是使用資料表分割) 。 這是因為對應是針對每個屬性進行的，因此 null 複雜值沒有個別的 sentinel。

- 本身的型別不支援繼承對應，但您應該能夠將相同繼承階層的兩個分葉類型對應為不同的擁有類型。 EF Core 不會推論出它們屬於同一階層的事實。

#### <a name="main-differences-with-ef6s-complex-types"></a>EF6 複雜類型的主要差異

- 資料表分割是選擇性的，也就是說，它們可以選擇性地對應到不同的資料表，但仍然是擁有的類型。

- 它們可以參考其他實體 (也就是說，它們可以作為與其他非擁有類型) 關聯性的相依端。

## <a name="additional-resources"></a>其他資源

- **聖馬丁 Fowler。ValueObject 模式** \
  <https://martinfowler.com/bliki/ValueObject.html>

- **Eric Evans。領域驅動設計：解決軟體核心的複雜度。** (書籍；包含值物件的探討) \
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

- **Vaughn Vernon。實施領域導向設計。** (書籍；包含值物件的探討) \
  <https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/>

- **擁有的實體類型** \
  <https://docs.microsoft.com/ef/core/modeling/owned-entities>

- **陰影屬性** \
  <https://docs.microsoft.com/ef/core/modeling/shadow-properties>

- **複雜類型和/或值物件**。 EF Core GitHub 存放庫 ([問題] 索引標籤) 的探討 \
  <https://github.com/dotnet/efcore/issues/246>

- **ValueObject.cs.** eShopOnContainers 中的基底值物件類別。 \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/SeedWork/ValueObject.cs>

- **網址類別。** eShopOnContainers 中的範列值物件類別。 \
  <https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Address.cs>

> [!div class="step-by-step"]
> [上一個](seedwork-domain-model-base-classes-interfaces.md) 
> [下一步](enumeration-classes-over-enum-types.md)
