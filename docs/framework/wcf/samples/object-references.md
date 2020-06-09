---
title: 物件參考
ms.date: 03/30/2017
ms.assetid: 7a93d260-91c3-4448-8f7a-a66fb562fc23
ms.openlocfilehash: ba4ee3fd0cc16130f66570891ecc295b2d2c50aa
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599980"
---
# <a name="object-references"></a>物件參考
這個範例會示範如何以傳址 (By Reference) 方式，在伺服器和用戶端之間傳遞物件。 此範例使用模擬的*社交網路*。 社交網路由包含 friend 清單的 `Person` 類別 (Class) 組成，每個 friend 都是一個 `Person` 類別的執行個體 (Instance)，擁有各自的 friend 清單。 這樣可以建立物件圖形。 此服務會公開 (Expose) 這些社交網站上的作業。  
  
 在這個範例中，服務是由網際網路資訊服務 (IIS) 所裝載，而用戶端是主控台應用程式 (.exe)。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
## <a name="service"></a>服務  
 `Person` 類別已套用 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性 (Attribute)，而且 <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A> 欄位設定為 `true` 以便將其宣告為參考型別 (Reference Type)。 所有屬性 (Property) 都已經套用 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性 (Attribute)。  
  
```csharp
[DataContract(IsReference=true)]  
public class Person  
{  
    string name;  
    string location;  
    string gender;  
    int age;  
    List<Person> friends;  
    [DataMember()]  
    public string Name  
    {  
        get { return name; }  
        set { name = value; }  
    }  
    [DataMember()]  
    public string Location  
    {  
        get { return location; }  
        set { location = value; }  
    }  
    [DataMember()]  
    public string Gender  
    {  
        get { return gender; }  
        set { gender = value; }  
    }  
…  
}  
```  
  
 `GetPeopleInNetwork` 作業會採用 `Person` 型別的參數並傳回網路中的所有人員，也就是 `friends` 清單中的所有人員、friend 的 friend 等等，但不包含重複項目。  
  
```csharp
public List<Person> GetPeopleInNetwork(Person p)  
{  
    List<Person> people = new List<Person>();  
    ListPeopleInNetwork(p, people);  
    return people;  
  
}  
```  
  
 `GetMutualFriends` 作業則採用 `Person` 型別的參數，並傳回清單中所有在其 `friends` 清單中亦包含這個人員的 friend。  
  
```csharp
public List<Person> GetMutualFriends(Person p)  
{  
    List<Person> mutual = new List<Person>();  
    foreach (Person friend in p.Friends)  
    {  
        if (friend.Friends.Contains(p))  
            mutual.Add(friend);  
    }  
    return mutual;  
}  
```  
  
 `GetCommonFriends` 作業會採用型別為 `Person` 的清單。 此清單應該會有兩個 `Person` 物件。 此作業會傳回 `Person` 物件的清單，這些物件都位於輸入清單中兩個 `friends` 物件的 `Person` 清單內。  
  
```csharp
public List<Person> GetCommonFriends(List<Person> people)  
{  
    List<Person> common = new List<Person>();  
    foreach (Person friend in people[0].Friends)  
        if (people[1].Friends.Contains(friend))  
            common.Add(friend);  
    return common;  
}  
```  
  
## <a name="client"></a>用戶端  
 用戶端 proxy 是使用 Visual Studio 的**加入服務參考**功能建立的。  
  
 然後建立包含五個 `Person` 物件的社交網路。 這個用戶端會呼叫服務中所有三個方法。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
3. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Data\ObjectReferences`  
  
## <a name="see-also"></a>請參閱

- <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A>
- [互通物件參考](../feature-details/interoperable-object-references.md)
