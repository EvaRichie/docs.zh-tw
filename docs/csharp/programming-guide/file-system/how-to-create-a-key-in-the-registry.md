---
title: '如何在登錄中建立機碼-c # 程式設計指南'
description: 瞭解如何在登錄中建立機碼。 請參閱程式碼範例、編譯指令和其他可用的資源。
ms.date: 07/20/2015
helpviewer_keywords:
- registry, adding keys and values [C#]
- registry keys, creating [C#]
- keys, creating in registry
ms.assetid: 8fa475b0-e01f-483a-9327-fd03488fdf5d
ms.openlocfilehash: c51fa61aa4c501921d5c7ace99a8c5aaf7b29f58
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203913"
---
# <a name="how-to-create-a-key-in-the-registry-c-programming-guide"></a><span data-ttu-id="4bdf5-104">如何在登錄中建立機碼 (c # 程式設計手冊) </span><span class="sxs-lookup"><span data-stu-id="4bdf5-104">How to create a key in the registry (C# Programming Guide)</span></span>

<span data-ttu-id="4bdf5-105">本範例會將 "Name" 和 "Isabella" 的值組新增至目前使用者之登錄的 "Names" 索引鍵下。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-105">This example adds the value pair, "Name" and "Isabella", to the current user's registry, under the key "Names".</span></span>  
  
## <a name="example"></a><span data-ttu-id="4bdf5-106">範例</span><span class="sxs-lookup"><span data-stu-id="4bdf5-106">Example</span></span>  
  
```csharp  
Microsoft.Win32.RegistryKey key;  
key = Microsoft.Win32.Registry.CurrentUser.CreateSubKey("Names");  
key.SetValue("Name", "Isabella");  
key.Close();  
```  
  
## <a name="compiling-the-code"></a><span data-ttu-id="4bdf5-107">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="4bdf5-107">Compiling the Code</span></span>  
  
- <span data-ttu-id="4bdf5-108">將程式碼複製並貼到主控台應用程式的 `Main` 方法中。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-108">Copy the code and paste it into the `Main` method of a console application.</span></span>  
  
- <span data-ttu-id="4bdf5-109">以直接位在登錄的 HKEY_CURRENT_USER 節點下的索引鍵名稱取代 `Names` 參數。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-109">Replace the `Names` parameter with the name of a key that exists directly under the HKEY_CURRENT_USER node of the registry.</span></span>  
  
- <span data-ttu-id="4bdf5-110">以直接位在 Names 節點下的值名稱取代 `Name` 參數。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-110">Replace the `Name` parameter with the name of a value that exists directly under the Names node.</span></span>  
  
## <a name="robust-programming"></a><span data-ttu-id="4bdf5-111">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="4bdf5-111">Robust Programming</span></span>  

 <span data-ttu-id="4bdf5-112">檢查登錄結構以找出適合索引鍵的位置。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-112">Examine the registry structure to find a suitable location for your key.</span></span> <span data-ttu-id="4bdf5-113">例如，您可能想要開啟目前使用者的軟體金鑰，並以貴公司的名稱建立金鑰。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-113">For example, you might want to open the Software key of the current user, and create a key with your company's name.</span></span> <span data-ttu-id="4bdf5-114">請將登錄值新增至貴公司的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-114">Then add the registry values to your company's key.</span></span>  
  
 <span data-ttu-id="4bdf5-115">以下條件可能會造成例外狀況：</span><span class="sxs-lookup"><span data-stu-id="4bdf5-115">The following conditions might cause an exception:</span></span>  
  
- <span data-ttu-id="4bdf5-116">索引鍵名稱是 Null。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-116">The name of the key is null.</span></span>  
  
- <span data-ttu-id="4bdf5-117">使用者沒有權限，無法建立登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-117">The user does not have permissions to create registry keys.</span></span>  
  
- <span data-ttu-id="4bdf5-118">索引鍵名稱超過 255 個字元的限制。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-118">The key name exceeds the 255-character limit.</span></span>  
  
- <span data-ttu-id="4bdf5-119">機碼已關閉。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-119">The key is closed.</span></span>  
  
- <span data-ttu-id="4bdf5-120">登錄機碼為唯讀。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-120">The registry key is read-only.</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="4bdf5-121">.NET 安全性</span><span class="sxs-lookup"><span data-stu-id="4bdf5-121">.NET Security</span></span>  

 <span data-ttu-id="4bdf5-122">將資料寫入使用者資料夾 `Microsoft.Win32.Registry.CurrentUser` 比寫入本機電腦 `Microsoft.Win32.Registry.LocalMachine` 更安全。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-122">It is more secure to write data to the user folder — `Microsoft.Win32.Registry.CurrentUser` — rather than to the local computer — `Microsoft.Win32.Registry.LocalMachine`.</span></span>  
  
 <span data-ttu-id="4bdf5-123">當您建立登錄值時，您需要決定如果該值已經存在該怎麼辦。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-123">When you create a registry value, you need to decide what to do if that value already exists.</span></span> <span data-ttu-id="4bdf5-124">另一個可能是惡意的處理序，可能已建立值並具有其存取權。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-124">Another process, perhaps a malicious one, may have already created the value and have access to it.</span></span> <span data-ttu-id="4bdf5-125">當您將資料放在登錄值中時，資料可供其他處理序使用。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-125">When you put data in the registry value, the data is available to the other process.</span></span> <span data-ttu-id="4bdf5-126">為避免此問題，請使用 `Overload:Microsoft.Win32.RegistryKey.GetValue`。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-126">To prevent this, use the.`Overload:Microsoft.Win32.RegistryKey.GetValue`</span></span> <span data-ttu-id="4bdf5-127">方法。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-127">method.</span></span> <span data-ttu-id="4bdf5-128">如果沒有索引鍵，則傳回 Null。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-128">It returns null if the key does not already exist.</span></span>  
  
 <span data-ttu-id="4bdf5-129">即使使用存取控制清單 (ACL) 來保護登錄機碼，將密碼等機密資料以純文字儲存在登錄中也不安全。</span><span class="sxs-lookup"><span data-stu-id="4bdf5-129">It is not secure to store secrets, such as passwords, in the registry as plain text, even if the registry key is protected by access control lists (ACL).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4bdf5-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4bdf5-130">See also</span></span>

- <xref:System.IO?displayProperty=nameWithType>
- [<span data-ttu-id="4bdf5-131">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="4bdf5-131">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="4bdf5-132">檔案系統和登錄 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="4bdf5-132">File System and the Registry (C# Programming Guide)</span></span>](./index.md)
- [<span data-ttu-id="4bdf5-133">使用 C# 從登錄進行讀取、寫入和刪除</span><span class="sxs-lookup"><span data-stu-id="4bdf5-133">Read, write and delete from the registry with C#</span></span>](https://www.codeproject.com/Articles/3389/Read-write-and-delete-from-registry-with-C)
