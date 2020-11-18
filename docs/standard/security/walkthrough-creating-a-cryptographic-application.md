---
title: 逐步解說：建立密碼編譯應用程式
description: 逐步解說如何建立密碼編譯應用程式。 瞭解如何在 Windows Forms 應用程式中加密和解密內容。
ms.date: 07/14/2020
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptography [NET], example
- cryptography [NET], cryptographic application example
- cryptography [NET], application example
ms.assetid: abf48c11-1e72-431d-9562-39cf23e1a8ff
ms.openlocfilehash: 70218d60abb336cdb35fc2e89e62a50b6bd79c67
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830554"
---
# <a name="walkthrough-creating-a-cryptographic-application"></a>逐步解說：建立密碼編譯應用程式

> [!NOTE]
> 本文適用于 Windows。
>
> 如需 ASP.NET Core 的詳細資訊，請參閱 [ASP.NET Core 資料保護](/aspnet/core/security/data-protection/introduction)。

本逐步解說示範如何加密和解密內容。 程式碼範例是針對 Windows Form 應用程式所設計。 此應用程式不會示範真實世界案例，例如使用智慧卡。 相反地，它會示範加密和解密的基本概念。  
  
本逐步解說針對加密使用下列指導方針：  
  
- 使用 <xref:System.Security.Cryptography.Aes> 類別 (一個對稱算法) 來加密和解密資料，使用其自動產生的 <xref:System.Security.Cryptography.SymmetricAlgorithm.Key%2A> 和 <xref:System.Security.Cryptography.SymmetricAlgorithm.IV%2A>。  
  
- 使用 <xref:System.Security.Cryptography.RSA> 非對稱演算法來加密金鑰，並將其解密至加密的資料 <xref:System.Security.Cryptography.Aes> 。 非對稱演算法最適合用於較少量的資料，例如金鑰。  
  
    > [!NOTE]
    > 如果您想要保護電腦上的資料，而不是與其他人交換加密的內容，請考慮使用 <xref:System.Security.Cryptography.ProtectedData> 類別。  
  
 下表摘要說明本主題中的密碼編譯工作。  
  
|工作|說明|  
|----------|-----------------|  
|建立 Windows Form 應用程式|列出執行應用程式所需的控制項。|  
|宣告全域物件|宣告字串路徑變數、<xref:System.Security.Cryptography.CspParameters>，和 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 以擁有 <xref:System.Windows.Forms.Form> 類別的全域內容。|  
|建立非對稱金鑰|建立非對稱公開和私密金鑰值組，並指派金鑰容器名稱給它。|  
|加密檔案|顯示對話方塊以選取要加密的檔案，並且進行加密。|  
|解密檔案|顯示對話方塊以選取要解密的已加密檔案，並且進行解密。|  
|取得私密金鑰|使用金鑰容器名稱取得完整金鑰組。|  
|匯出公開金鑰|將金鑰儲存至僅包含公用參數的 XML 檔案。|  
|匯入公開金鑰|將金鑰從 XML 檔案載入到金鑰容器。|  
|測試應用程式|列出測試此應用程式的程序。|  
  
## <a name="prerequisites"></a>必要條件  

您需要下列元件才能完成這個逐步解說：  
  
- <xref:System.IO> 和 <xref:System.Security.Cryptography> 命名空間的參考。  
  
## <a name="creating-a-windows-forms-application"></a>建立 Windows Forms 應用程式  

在此逐步解說中的大部分程式碼範例，已設計為按鈕控制項的事件處理常式。 下表列出範例應用程式所需的控制項，及其必要名稱以符合程式碼範例。  
  
|控制|名稱|文字屬性 (如有需要)|  
|-------------|----------|---------------------------------|  
|<xref:System.Windows.Forms.Button>|`buttonEncryptFile`|加密檔案|  
|<xref:System.Windows.Forms.Button>|`buttonDecryptFile`|解密檔案|  
|<xref:System.Windows.Forms.Button>|`buttonCreateAsmKeys`|建立金鑰|  
|<xref:System.Windows.Forms.Button>|`buttonExportPublicKey`|匯出公開金鑰|  
|<xref:System.Windows.Forms.Button>|`buttonImportPublicKey`|匯入公開金鑰|  
|<xref:System.Windows.Forms.Button>|`buttonGetPrivateKey`|取得私密金鑰|  
|<xref:System.Windows.Forms.Label>|`label1`|未設定金鑰|  
|<xref:System.Windows.Forms.OpenFileDialog>|`openFileDialog1`||  
|<xref:System.Windows.Forms.OpenFileDialog>|`openFileDialog2`||  
  
 按兩下 Visual Studio 設計工具中的按鈕，以建立其事件處理常式。
  
## <a name="declaring-global-objects"></a>宣告全域物件  

將下列程式碼加入表單的建構函式： 針對您的環境和喜好設定編輯字串變數。  
  
[!code-csharp[CryptoWalkThru#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#1)]
[!code-vb[CryptoWalkThru#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#1)]  
  
## <a name="creating-an-asymmetric-key"></a>建立非對稱金鑰  

此工作會建立非對稱金鑰來加密及解密 <xref:System.Security.Cryptography.Aes> 金鑰。 這個金鑰用來加密內容，且它會在標籤控制項上顯示金鑰容器名稱。  
  
 加入下列程式碼做為 `Create Keys` 按鈕的 `Click` 事件處理常式 (`buttonCreateAsmKeys_Click`)。  
  
 [!code-csharp[CryptoWalkThru#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#2)]
 [!code-vb[CryptoWalkThru#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#2)]  
  
## <a name="encrypting-a-file"></a>加密檔案  

這項工作牽涉到兩個方法：按鈕的事件處理常式方法 `Encrypt File` (`buttonEncryptFile_Click`) 和 `EncryptFile` 方法。 第一種方法會顯示一個對話方塊來選取檔案，並將檔案名稱傳遞給第二個方法，後者則會執行加密。  
  
加密的內容、金鑰和 IV 全都儲存到一個 <xref:System.IO.FileStream>，稱為加密套件。  
  
`EncryptFile` 方法會執行下列動作：  
  
1. 建立 <xref:System.Security.Cryptography.Aes> 對稱演算法來加密內容。  
  
2. 建立 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 物件來加密 <xref:System.Security.Cryptography.Aes> 金鑰。  
  
3. 使用 <xref:System.Security.Cryptography.CryptoStream> 物件以讀取及加密原始程式檔的 <xref:System.IO.FileStream> (以位元組區塊為單位) 成為加密檔案的目的地 <xref:System.IO.FileStream> 物件。  
  
4. 判斷加密金鑰和 IV 的長度，並建立其長度值的位元組陣列。  
  
5. 將金鑰、IV 和其長度值寫入加密套件。  
  
 加密套件使用下列格式：  
  
- 金鑰長度，位元組 0 - 3  
  
- IV 長度，位元組 4 - 7  
  
- 加密的金鑰  
  
- IV  
  
- 加密文字  
  
 您可以使用金鑰和 IV 的長度來決定加密套件所有部分的起始點和長度，這些可以用來解密檔案。  
  
 加入下列程式碼做為 `Encrypt File` 按鈕的 `Click` 事件處理常式 (`buttonEncryptFile_Click`)。  
  
 [!code-csharp[CryptoWalkThru#3](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#3)]
 [!code-vb[CryptoWalkThru#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#3)]  
  
 將下列 `EncryptFile` 方法加入表單。  
  
 [!code-csharp[CryptoWalkThru#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#5)]
 [!code-vb[CryptoWalkThru#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#5)]  
  
## <a name="decrypting-a-file"></a>解密檔案  

這項工作需要兩個方法：`Decrypt File` 按鈕的事件處理常式方法 (`buttonDecryptFile_Click`) 和 `DecryptFile` 方法。 第一種方法會顯示一個對話方塊來選取檔案，並將其檔案名稱傳遞給第二個方法，後者則會執行解密。  
  
`Decrypt` 方法會執行下列動作：  
  
1. 建立 <xref:System.Security.Cryptography.Aes> 對稱演算法來解密內容。  
  
2. 讀取加密套件的 <xref:System.IO.FileStream> 前八個位元組到位元組陣列，以取得加密金鑰和 IV 的長度。  
  
3. 從加密套件將金鑰和 IV 擷取到位元組陣列。  
  
4. 建立 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 物件來解密 <xref:System.Security.Cryptography.Aes> 金鑰。  
  
5. 使用 <xref:System.Security.Cryptography.CryptoStream> 物件以讀取及解密 <xref:System.IO.FileStream> 加密套件的加密文字區段 (以位元組區域為單位 ) 到解密檔案的 <xref:System.IO.FileStream> 物件。 完成後，就會解密完成。  
  
 加入下列程式碼做為 `Decrypt File` 按鈕的 `Click` 事件處理常式。  
  
 [!code-csharp[CryptoWalkThru#4](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#4)]
 [!code-vb[CryptoWalkThru#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#4)]  
  
 將下列 `DecryptFile` 方法加入表單。  
  
 [!code-csharp[CryptoWalkThru#6](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#6)]
 [!code-vb[CryptoWalkThru#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#6)]  
  
## <a name="exporting-a-public-key"></a>匯出公開金鑰

這項工作會將 `Create Keys` 按鈕所建立的金鑰儲存到檔案。 它只會匯出公用參數。  
  
這項工作模擬的案例是 Alice 提供給 Bob 她的公開金鑰，讓他可以為她加密檔案。 他和其他擁有該公開金鑰的使用者將無法解密這些檔案，因為他們沒有具私密參數的完整金鑰組。  
  
加入下列程式碼做為 `Export Public Key` 按鈕的 `Click` 事件處理常式 (`buttonExportPublicKey_Click`)。  
  
[!code-csharp[CryptoWalkThru#8](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#8)]
[!code-vb[CryptoWalkThru#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#8)]  
  
## <a name="importing-a-public-key"></a>匯入公開金鑰

這項工作載入金鑰時只會附帶公用參數，如 `Export Public Key` 按鈕所建立，然後將它設定為金鑰容器名稱。  
  
這項工作模擬的案例是 Bob 載入 Alice 的金鑰且僅包含公用參數，讓他可以為她加密檔案。  
  
加入下列程式碼做為 `Import Public Key` 按鈕的 `Click` 事件處理常式 (`buttonImportPublicKey_Click`)。  
  
[!code-csharp[CryptoWalkThru#9](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#9)]
[!code-vb[CryptoWalkThru#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#9)]  
  
## <a name="getting-a-private-key"></a>取得私密金鑰  

這項工作會將金鑰容器名稱設為使用 `Create Keys` 按鈕所建立的金鑰名稱。 金鑰容器將會包含完整金鑰組和私密參數。  
  
這項工作模擬的案例是 Alice 使用她的私密金鑰來解密 Bob 所加密的檔案。  
  
加入下列程式碼做為 `Get Private Key` 按鈕的 `Click` 事件處理常式 (`buttonGetPrivateKey_Click`)。  
  
[!code-csharp[CryptoWalkThru#7](../../../samples/snippets/csharp/VS_Snippets_CLR/CryptoWalkThru/cs/Form1.cs#7)]
[!code-vb[CryptoWalkThru#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CryptoWalkThru/vb/Form1.vb#7)]  
  
## <a name="testing-the-application"></a>測試應用程式

建立應用程式之後，請執行下列測試案例。  
  
#### <a name="to-create-keys-encrypt-and-decrypt"></a>建立金鑰、加密和解密  
  
1. 按一下 `Create Keys` 按鈕。 標籤會顯示金鑰名稱，並顯示它是完整金鑰組。  
  
2. 按一下 `Export Public Key` 按鈕。 請注意匯出公開金鑰參數時，不會變更目前的金鑰。  
  
3. 按一下 `Encrypt File` 按鈕，然後選取檔案。  
  
4. 按一下 `Decrypt File` 按鈕，然後選取剛才加密的檔案。  
  
5. 檢查剛才解密的檔案。  
  
6. 關閉應用程式，然後重新啟動，以便在下一個案例中測試擷取保存的金鑰容器。  
  
#### <a name="to-encrypt-using-the-public-key"></a>使用公開金鑰加密  
  
1. 按一下 `Import Public Key` 按鈕。 標籤會顯示金鑰名稱，並顯示它只是公開金鑰。  
  
2. 按一下 `Encrypt File` 按鈕，然後選取檔案。  
  
3. 按一下 `Decrypt File` 按鈕，然後選取剛才加密的檔案。 這將會失敗，因為您必須擁有私密金鑰才能解密。  
  
 這個案例示範了只具有公用金鑰來為另一個人加密檔案。 通常那個人只會提供您公開金鑰，並且保留私密金鑰來進行解密。  
  
#### <a name="to-decrypt-using-the-private-key"></a>使用私密金鑰解密  
  
1. 按一下 `Get Private Key` 按鈕。 標籤會顯示金鑰名稱，並顯示它是否為完整金鑰組。  
  
2. 按一下 `Decrypt File` 按鈕，然後選取剛才加密的檔案。 這將會成功，因為您有完整金鑰組可以解密。  
  
## <a name="see-also"></a>請參閱

- [加密模型](cryptography-model.md) -說明如何在基類庫中執行密碼編譯。
- [密碼編譯服務](cryptographic-services.md)
- [跨平臺密碼編譯](cross-platform-cryptography.md)
- [ASP.NET Core 資料保護](/aspnet/core/security/data-protection/introduction)
