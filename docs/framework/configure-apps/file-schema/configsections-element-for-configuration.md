---
title: <configuration> 的 <configSections> 項目
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections
helpviewer_keywords:
- configSections Element
- <configSections> Element
ms.assetid: 9f963c1b-dc3f-4220-a8b6-2dd7a5a8e039
ms.openlocfilehash: 55116f1fe6fdffffea8f26d8a4de783c7305ada3
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155345"
---
# <a name="configsections-element-for-configuration"></a><span data-ttu-id="7ee2d-102">\<configuration> 的 \<configSections> 項目</span><span class="sxs-lookup"><span data-stu-id="7ee2d-102">\<configSections> element for \<configuration></span></span>

<span data-ttu-id="7ee2d-103">包含設定區段和命名空間宣告。</span><span class="sxs-lookup"><span data-stu-id="7ee2d-103">Contains configuration section and namespace declarations.</span></span>

<span data-ttu-id="7ee2d-104">[**\<configuration>**](configuration-element.md) &nbsp;&nbsp;**\<configSections>**</span><span class="sxs-lookup"><span data-stu-id="7ee2d-104">[**\<configuration>**](configuration-element.md) &nbsp;&nbsp;**\<configSections>**</span></span>

## <a name="attributes"></a><span data-ttu-id="7ee2d-105">屬性</span><span class="sxs-lookup"><span data-stu-id="7ee2d-105">Attributes</span></span>

<span data-ttu-id="7ee2d-106">無</span><span class="sxs-lookup"><span data-stu-id="7ee2d-106">None</span></span>

## <a name="parent-element"></a><span data-ttu-id="7ee2d-107">父元素</span><span class="sxs-lookup"><span data-stu-id="7ee2d-107">Parent element</span></span>

|     | <span data-ttu-id="7ee2d-108">描述</span><span class="sxs-lookup"><span data-stu-id="7ee2d-108">Description</span></span> |
| --- | ----------- |
| [**\<configuration>**](configuration-element.md) | <span data-ttu-id="7ee2d-109">通用語言執行平台和 .NET Framework 應用程式所使用之每個組態檔中的根項目。</span><span class="sxs-lookup"><span data-stu-id="7ee2d-109">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span> |

## <a name="child-elements"></a><span data-ttu-id="7ee2d-110">子元素</span><span class="sxs-lookup"><span data-stu-id="7ee2d-110">Child elements</span></span>

|     | <span data-ttu-id="7ee2d-111">描述</span><span class="sxs-lookup"><span data-stu-id="7ee2d-111">Description</span></span> |
| --- | ----------- |
| [**\<section>**](section-element.md) | <span data-ttu-id="7ee2d-112">包含設定區段宣告。</span><span class="sxs-lookup"><span data-stu-id="7ee2d-112">Contains a configuration section declaration.</span></span> |
| [**\<sectionGroup>**](sectiongroup-element-for-configsections.md) | <span data-ttu-id="7ee2d-113">定義設定區段的命名空間。</span><span class="sxs-lookup"><span data-stu-id="7ee2d-113">Defines a namespace for configuration sections.</span></span> |
| [**\<remove>**](remove-element-for-configsections.md) | <span data-ttu-id="7ee2d-114">移除預先定義的區段或區段群組。</span><span class="sxs-lookup"><span data-stu-id="7ee2d-114">Removes a predefined section or section group.</span></span> |
| [**\<clear>**](clear-element-for-configsections.md) | <span data-ttu-id="7ee2d-115">清除所有先前定義的區段和區段群組。</span><span class="sxs-lookup"><span data-stu-id="7ee2d-115">Clears all previously defined sections and section groups.</span></span> |

## <a name="remarks"></a><span data-ttu-id="7ee2d-116">備註</span><span class="sxs-lookup"><span data-stu-id="7ee2d-116">Remarks</span></span>

<span data-ttu-id="7ee2d-117">如果這個元素是在設定檔中，它必須是元素的第一個子專案 **\<configuration>** 。</span><span class="sxs-lookup"><span data-stu-id="7ee2d-117">If this element is in a configuration file, it must be the first child element of the **\<configuration>** element.</span></span>

## <a name="example"></a><span data-ttu-id="7ee2d-118">範例</span><span class="sxs-lookup"><span data-stu-id="7ee2d-118">Example</span></span>

<span data-ttu-id="7ee2d-119">下列範例顯示如何定義設定區段，並定義該區段的設定：</span><span class="sxs-lookup"><span data-stu-id="7ee2d-119">The following example shows how to define a configuration section and define settings for that section:</span></span>

```xml
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" />
  </configSections>
  <sampleSection setting1="Value1"
                 setting2="value two"
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a><span data-ttu-id="7ee2d-120">組態檔</span><span class="sxs-lookup"><span data-stu-id="7ee2d-120">Configuration file</span></span>

<span data-ttu-id="7ee2d-121">此元素可用於應用程式佈建檔案 *、電腦設定檔案（machine.config*），以及不在應用程式目錄層級*的 web.config 檔案*。</span><span class="sxs-lookup"><span data-stu-id="7ee2d-121">This element can be used in the application configuration file, machine configuration file (*Machine.config*), and *Web.config* files that are not at the application directory level.</span></span>

## <a name="see-also"></a><span data-ttu-id="7ee2d-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7ee2d-122">See also</span></span>

- [<span data-ttu-id="7ee2d-123">.NET Framework 的設定檔架構</span><span class="sxs-lookup"><span data-stu-id="7ee2d-123">Configuration file schema for the .NET Framework</span></span>](index.md)
