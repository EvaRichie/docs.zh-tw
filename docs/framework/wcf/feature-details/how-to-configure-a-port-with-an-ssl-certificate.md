---
title: 作法：使用 SSL 憑證設定連接埠
description: 瞭解如何設定具有 x.509 憑證的埠，這是使用傳輸安全性的 WSHttpBinding 類別所需的自我裝載 WCF 服務所需的憑證。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SSL
- WCF, security mode
- WCF, security
ms.assetid: b8abcc8e-a5f5-4317-aca5-01e3c40ab24d
ms.openlocfilehash: 619a893e0973f6691e32446d75f101201a0b6799
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556378"
---
# <a name="how-to-configure-a-port-with-an-ssl-certificate"></a>作法：使用 SSL 憑證設定連接埠

使用使用傳輸安全性的類別來建立自我裝載的 Windows Communication Foundation (WCF) 服務時 <xref:System.ServiceModel.WSHttpBinding> ，您也必須使用 x.509 憑證來設定埠。 如果您沒有建立自我裝載的服務，可以將您的服務裝載在 Internet Information Services (IIS) 上。 如需詳細資訊，請參閱 [HTTP 傳輸安全性](http-transport-security.md)。  
  
 若要設定連接埠，使用的工具取決於電腦上執行的作業系統。  
  
 如果您正在執行 Windows Server 2003，請使用 HttpCfg.exe 工具。 在 Windows Server 2003 上，已安裝此工具。 如需詳細資訊，請參閱 [Httpcfg.exe 總覽](/previous-versions/windows/it-pro/windows-server-2003/cc787508(v=ws.10))。 [Windows 支援工具檔](/previous-versions/windows/it-pro/windows-server-2003/cc781601(v=ws.10))說明 Httpcfg.exe 工具的語法。  
  
 如果您執行的是 Windows Vista，請使用已安裝的 Netsh.exe 工具。
  
> [!NOTE]
> 修改電腦上儲存的憑證需要系統管理許可權。  
  
## <a name="determine-how-ports-are-configured"></a>判斷如何設定埠  
  
1. 在 Windows Server 2003 或 Windows XP 中，請使用 HttpCfg.exe 工具，使用 **查詢** 和 **ssl** 參數來查看目前的埠設定，如下列範例所示。  
  
    ```console
    httpcfg query ssl  
    ```  
  
2. 在 Windows Vista 中，使用 Netsh.exe 工具來查看目前的埠設定，如下列範例所示。  
  
    ```console  
    netsh http show sslcert  
    ```  
  
## <a name="get-a-certificates-thumbprint"></a>取得憑證的指紋  
  
1. 使用憑證 MMC 嵌入式管理單元，尋找目的為用戶端驗證的 X.509 憑證。 如需詳細資訊，請參閱 [做法：使用 MMC 嵌入式管理單元檢視憑證](how-to-view-certificates-with-the-mmc-snap-in.md)。  
  
2. 存取憑證的指紋。 如需詳細資訊，請參閱[做法：擷取憑證的指紋](how-to-retrieve-the-thumbprint-of-a-certificate.md)。  
  
3. 將憑證的指紋複製到文字編輯器中，例如「記事本」。  
  
4. 移除十六進位字元之間的所有空格。 完成這項工作的方法之一是使用文字編輯器的尋找與取代功能，並使用 null 字元來取代各個空格。  
  
## <a name="bind-an-ssl-certificate-to-a-port-number"></a>將 SSL 憑證系結至埠號碼  
  
1. 在 Windows Server 2003 或 Windows XP 中，請使用安全通訊端層 (SSL) 存放區上「設定」模式中的 HttpCfg.exe 工具，將憑證系結至埠號碼。 此工具是使用指紋來識別憑證，如下列範例所示。  
  
    ```console  
    httpcfg set ssl -i 0.0.0.0:8012 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6  
    ```  
  
    - **-I**參數的語法為 `IP` ： `port` ，並指示工具將憑證設定為電腦的埠8012。 或者，號碼前面的四個零也可以使用電腦的實際 IP 位址來取代。  
  
    - **-H**參數會指定憑證的指紋。  
  
2. 在 Windows Vista 中，請使用 Netsh.exe 工具，如下列範例所示。  
  
    ```console  
    netsh http add sslcert ipport=0.0.0.0:8000 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}
    ```  
  
    - **Certhash**參數會指定憑證的指紋。  
  
    - **Ipport**參數會指定 IP 位址和埠，以及與所述 Httpcfg.exe 工具的 **-i**參數一樣的函式。  
  
    - **Appid**參數是一種 GUID，可用來識別擁有應用程式。  
  
## <a name="bind-an-ssl-certificate-to-a-port-number-and-support-client-certificates"></a>將 SSL 憑證系結至埠號碼，並支援用戶端憑證  
  
1. 在 Windows Server 2003 或 Windows XP 中，為了支援在傳輸層以 x.509 憑證進行驗證的用戶端，請遵循上述程式，但是將額外的命令列參數傳遞至 HttpCfg.exe，如下列範例所示。  
  
    ```console  
    httpcfg set ssl -i 0.0.0.0:8012 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6 -f 2  
    ```  
  
     **-F**參數具有的語法， `n` 其中 n 是介於1和7之間的數位。 值為 2 (如上一個範例所示) 會在傳輸層啟用用戶端憑證。 值為 3 會啟用用戶端憑證，並將這些憑證對應至 Windows 帳戶。 如需其他值的行為，請參閱 HttpCfg.exe 說明。  
  
2. 在 Windows Vista 中，為了支援在傳輸層以 x.509 憑證進行驗證的用戶端，請遵循上述程式，但使用額外的參數，如下列範例所示。  
  
    ```console  
    netsh http add sslcert ipport=0.0.0.0:8000 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF} clientcertnegotiation=enable  
    ```  
  
## <a name="delete-an-ssl-certificate-from-a-port-number"></a>從埠號碼刪除 SSL 憑證  
  
1. 使用 HttpCfg.exe 或 Netsh.exe 工具來查看電腦上所有繫結的連接埠和指紋。 若要將資訊列印到磁片，請使用重新導向字元 ">"，如下列範例所示。  
  
    ```console  
    httpcfg query ssl>myMachinePorts.txt  
    ```
  
2. 在 Windows Server 2003 或 Windows XP 中，請使用 HttpCfg.exe 工具搭配 **delete** 和 **ssl** 關鍵字。 使用 **-i** 參數來指定 `IP` ： `port` 號碼，並使用 **-h** 參數來指定指紋。  
  
    ```console  
    httpcfg delete ssl -i 0.0.0.0:8005 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6  
    ```  
  
3. 在 Windows Vista 中，請使用 Netsh.exe 工具，如下列範例所示。  
  
    ```console  
    Netsh http delete sslcert ipport=0.0.0.0:8005  
    ```  
  
## <a name="example"></a>範例  

 下列程式碼將示範如何使用設定為傳輸安全性的 <xref:System.ServiceModel.WSHttpBinding> 類別來建立自我裝載的服務。 當建立應用程式時，請在位址中指定連接埠號碼。  
  
 [!code-csharp[c_WsHttpService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wshttpservice/cs/source.cs#3)]
 [!code-vb[c_WsHttpService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wshttpservice/vb/source.vb#3)]  
  
## <a name="see-also"></a>另請參閱

- [HTTP 傳輸安全性](http-transport-security.md)
