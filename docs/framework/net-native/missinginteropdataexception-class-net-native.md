---
title: MissingInteropDataException 類別 (.NET Native)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: eab4bcf8-9f5f-4731-87d8-842748a6062a
ms.openlocfilehash: bbbb484e5cb8060568b321a2a41474d60c9f87f6
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96250914"
---
# <a name="missinginteropdataexception-class-net-native"></a>MissingInteropDataException 類別 (.NET Native)

**適用于 Windows 應用程式的 .NET Windows 10，僅 .NET Native**  
  
 當呼叫手動封送處理方法，但靜態分析或執行階段指示詞檔案中找不到類型的中繼資料時，會擲回這個例外狀況。  
  
 **命名空間：** System.Runtime.CompilerServices  
  
> [!IMPORTANT]
> 類別僅供 `MissingInteropDataException` .NET Native 工具鏈內部使用。 這主要並非用於協力廠商程式碼中，也不應該在應用程式程式碼中處理此例外狀況。 相反地，請藉由將項目新增至[執行階段指示詞檔案](runtime-directives-rd-xml-configuration-file-reference.md)，來消除例外狀況。 如需詳細資訊，請參閱＜備註＞一節。  
  
## <a name="syntax"></a>Syntax  

 [!code-csharp[ProjectN#21](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/missinginteropdataexception_syntax1.cs#21)]
 [!code-vb[ProjectN#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/projectn/vb/missinginteropdataexception_syntax1.vb#21)]  
  
 `MissingInteropDataException` 類別具有下列成員：  
  
## <a name="constructors"></a>建構函式  
  
|建構函式|描述|  
|-----------------|-----------------|  
|`public MissingInteropDataException(String resourceId, Type pertinentType)`|使用系統提供有關錯誤及遺漏資料之類型的說明訊息識別碼，初始化 `MissingInteropDataException` 類別的新執行個體。 這個函式僅供 .NET Native 工具鏈內部使用。|  
  
## <a name="properties"></a>屬性  
  
|屬性|描述|  
|--------------|-----------------|  
|`public IDictionary Data { get; }`|取得鍵值組的集合，這些鍵值組會提供關於例外狀況的其他使用者定義資訊。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public string HelpLink { get; set; }`|取得或設定與這個例外狀況相關聯的說明檔連結。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public int HResult { get; protected set; }`|取得或設定 `HRESULT`，這是指派給特定例外狀況的編碼數值。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public Exception InnerException { get; }`|取得造成目前例外狀況的例外狀況。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public string Message { get; }`|取得描述目前例外狀況的訊息。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public Type MissingType { get; private set; }`|取得或設定遺漏資料的類型。|  
|`public string Source { get; set; }`|取得或設定造成錯誤的應用程式或物件名稱。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public string StackTrace { get; }`|取得呼叫堆疊上即時運算框架的字串表示。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public MethodBase TargetSite { get; }`|取得擲回目前例外狀況的方法。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|`public bool Equals(Object obj)`|判斷指定的物件是否等於目前的物件。  (繼承自 <xref:System.Object>。)|  
|`protected void Finalize()`|允許物件在記憶體回收進行回收之前，嘗試釋放資源並執行其他清除作業。 (繼承自 <xref:System.Object>。)|  
|`public Exception GetBaseException()`|傳回一或多個後續例外狀況之根本原因的例外狀況。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public int GetHashCode()`|傳回 `MissingInteropDataException` 執行個體的雜湊碼。   (繼承自 <xref:System.Object>。)|  
|`public void GetObjectData(SerializationInfo info, StreamingContext context)`|使用例外狀況的相關資訊來設定 <xref:System.Runtime.Serialization.SerializationInfo> 物件。  (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`public Type GetType()`|取得目前執行個體的執行階段類型。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
|`protected Object MemberwiseClone()`|建立目前物件的淺層複本。 (繼承自 <xref:System.Object>。)|  
|`public string ToString()`|傳回目前例外狀況的字串表示。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
  
## <a name="events"></a>事件  
  
|事件|描述|  
|-----------|-----------------|  
|`protected event EventHandler<SafeSerializationEventArgs> SerializeObjectState`|當例外狀況序列化，以建立包含例外狀況相關序列化資料的例外狀況狀態物件時，就會發生此事件。 (繼承自 <xref:System.Exception?displayProperty=nameWithType>。)|  
  
## <a name="usage-details"></a>使用量詳細資料  

 當由於沒有類型資訊而無法順利對 COM 或 Windows 執行階段元件呼叫方法時，會擲回 `MissingInteropDataException` 例外狀況。  
  
 應用程式在執行時間可使用的中繼資料是由執行時間指示詞所定義， (XML 設定) 檔 \*.rd.xml。 若要防止應用程式擲回這個例外狀況，您必須修改這個檔案，定義必須在執行階段有中繼資料。 解決這個錯誤的最常見方式，是將 `MarshalObject`、`MarshalDelegate` 或 `MarshalStructure` 屬性加入至執行階段指示詞檔案中的適當程式項目。 如需此檔案格式的資訊，請參閱[執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)。  
  
> [!IMPORTANT]
> 因為這個例外狀況指出應用程式所需的中繼資料在執行階段無法使用，所以您不應該在 `try`/`catch` 區塊中處理這個例外狀況。 相反地，您應該診斷例外狀況的原因，然後將適當地進入點加入階段指示詞檔案，以去除這項例外狀況。  
  
 `MissingInteropDataException` 類別包含唯一的成員 `MissingType` 屬性，指出需要中繼資料才能成功呼叫方法的類型。 其餘所有成員都是繼承自基底類別 <xref:System.Exception?displayProperty=nameWithType>。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Exception?displayProperty=nameWithType>
- [MissingMetadataException 類別](missingmetadataexception-class-net-native.md)
- [執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)
