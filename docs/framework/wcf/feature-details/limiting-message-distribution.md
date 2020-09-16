---
title: 限制訊息散發
ms.date: 03/30/2017
ms.assetid: 8b5ec4b8-1ce9-45ef-bb90-2c840456bcc1
ms.openlocfilehash: e736aba60d7d2b39d1b8eb958a8c72e6e8d55e13
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555012"
---
# <a name="limiting-message-distribution"></a>限制訊息散發

對等通道在設計上即是廣播 mesh。 其基本流動模型牽涉到將 mesh 的任何成員所傳送的每個訊息，散發給該 mesh 的所有其他成員。 當成員產生的每個訊息對所有其他成員而言，是相關的且有用的訊息的情況下 (例如聊天室的案例)，這就是理想的方式。 然而，許多應用程式偶爾會需要限制訊息的散發。 例如，在新成員加入 mesh 並想要擷取透過 mesh 傳送的上一個訊息時，這個要求並不需要流向 mesh 的每個成員。 要求可能會限制在接近鄰近的範圍，或是可以篩選出本機產生的訊息。也可以將訊息傳送至網格上的個別節點。 本主題討論使用躍點計數、訊息傳播篩選條件、本機篩選條件或直接連接，控制訊息在整個 mesh 間的轉送方式，並提供用於選擇適當方法的一般方針。

## <a name="hop-counts"></a>躍點計數

`PeerHopCount` 的概念類似於 IP 通訊協定中使用的 TTL (存留時間)。 `PeerHopCount` 的值會繫結到訊息執行個體，並會指定在捨棄訊息前應該轉送幾次訊息。 每當對等通道用戶端收到訊息時，用戶端會檢查訊息是否有指定 `PeerHopCount`。 如果有指定的話，則用戶端會將躍點計數值減一後，才轉送訊息給鄰近節點。 當用戶端所收到訊息的躍點計數值為零時，用戶端會處理該訊息，但不會將訊息轉送給鄰近節點。

只要將 `PeerHopCount` 當做屬性 (Attribute) 加入至訊息類別實作中適當的屬性 (Property) 或欄位中，即可將躍點計數加入至訊息。 您可以在傳送訊息至網狀結構之前，先將此屬性設定為特定值。 因此，必要時您可以使用躍點計數來限制訊息在 mesh 間的散發，或許可以避免不必要的重複訊息。 當 mesh 包含大量的多餘資料，或者要傳送訊息給最近的鄰居或少許躍點內的鄰居時，這個方法會特別有用。

- 如需程式碼片段和相關資訊，請參閱 PeerHopCount 屬性：在對等通道 blog 上 [控制訊息發佈](/archive/blogs/peerchan/the-peerhopcount-attribute-controlling-message-distribution) 貼文。

## <a name="message-propagation-filter"></a>訊息傳播篩選條件

`MessagePropagationFilter` 可以用於訊息流動的自訂控制，特別是在訊息內容或其他特定案例會決定傳播的進行時。 篩選條件可以為通過節點的每個訊息進行傳播決策。 這對於節點所收到的訊息是在 mesh 中任何其他地方產生的，以及應用程式所建立的訊息來說，特別是如此。 篩選條件能夠同時存取訊息及其來源，因此可以根據完整可用的資訊來判斷是否要轉送或捨棄訊息。

<xref:System.ServiceModel.PeerMessagePropagationFilter> 是基底抽象類別，具有單一函式 <xref:System.ServiceModel.PeerMessagePropagationFilter.ShouldMessagePropagate%2A>。 方法呼叫的第一個引數會傳入訊息的完整複本。 對該訊息所進行的任何變更，並不會影響到實際的訊息。 方法呼叫的最後一個引數會識別訊息的來源 (`PeerMessageOrigination.Local` 或 `PeerMessageOrigination.Remote`)。 這個方法的具體實作必須從 <xref:System.ServiceModel.PeerMessagePropagation> 列舉型別傳回常數，此常數表示要將訊息轉送至本機應用程式 (`Local`)、轉送至遠端用戶端 (`Remote`)，或者兩個都要 (`LocalAndRemote`) 或都不要 (`None`)。 您可以存取對應的 `PeerNode` 物件，並在 `PeerNode.MessagePropagationFilter` 屬性中指定衍生傳播篩選條件類別的執行個體，藉此套用這個篩選條件。 請確定您已在開啟對等通道前附加傳播篩選條件。

- 如需程式碼片段和相關資訊，請參閱對等通道 blog 上的 [對等通道和 MessagePropagationFilter](/archive/blogs/peerchan/peer-channel-and-messagepropagationfilter) 文章。

## <a name="contacting-an-individual-node-in-the-mesh"></a>聯繫 Mesh 中的個別節點

藉由設定本機篩選條件或設定直接連接，即可以聯繫 mesh 中的個別節點。

如果 mesh 中的每個節點都有個別的 ID，就可以在訊息實作中指定目的端 ID。 本機篩選條件的設定方式，是藉由在訊息合約中撰寫函式，只有在目前節點的 ID 符合您指定的目的端 ID 時，才顯示訊息給該節點。 由於 mesh 會傳輸該訊息，所以不一定會帶來設定新連接的額外負荷作業。 然而，這樣卻缺乏效率，因為要在 mesh 中傳送許多次訊息。 當傳送給 mesh 的個別成員的訊息不太大而且也不頻繁發生時，這個方法可以運作得很好。

對於持續性、高頻寬的連接，比較適合使用直接連接。 您可以透過 mesh 傳送連接資訊，然後再設定您選擇的直接連接以傳送/接收訊息。

## <a name="choosing-an-approach-for-limiting-message-distribution"></a>選擇限制訊息散發的方法

在探索您需要限制訊息散發的案例時，請詢問您自己下列問題：

- **誰** 需要接收訊息？ 只是一個鄰近節點？ mesh 中其他位置的節點？ 或是 mesh 中一半的節點？

- 傳送此訊息的**頻率為何**？

- 這則訊息會使用何種 **頻寬** ？

這些問題的答案能夠協助您決定該使用躍點計數、訊息傳播篩選條件、本機篩選條件或直接連接。 請考慮下列一般方針：

- **誰**

  - *個別節點*：本機篩選準則或直接連接。

  - *特定區域內的鄰近*專案： PeerHopCount。

  - *網格的複雜子集*： MessagePropagationFilter。

- **頻率**

  - *非常頻繁*： Direct Connection、PeerHopCount、MessagePropagationFilter。

  - *偶然*：本機篩選準則。

- **頻寬使用**

  - *高*：直接連接，較不建議使用 MessagePropagationFilter 或本機篩選。

  - *低*：可能不需要任何直接連接。

## <a name="see-also"></a>另請參閱

- [建置對等通道應用程式](building-a-peer-channel-application.md)
