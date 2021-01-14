---
title: 建立具有外掛程式的 .NET Core 應用程式
description: 了解如何建立支援外掛程式的 .NET Core 應用程式。
author: jkoritzinsky
ms.author: jekoritz
ms.date: 10/16/2019
ms.openlocfilehash: d3b532ae72a80eef9603fc6f3ada8c11cae966dd
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98187895"
---
# <a name="create-a-net-core-application-with-plugins"></a>建立具有外掛程式的 .NET Core 應用程式

本教學課程會示範如何建立自訂的 <xref:System.Runtime.Loader.AssemblyLoadContext> 來載入外掛程式。 <xref:System.Runtime.Loader.AssemblyDependencyResolver>用來解析外掛程式的相依性。 本教學課程會正確地將外掛程式的相依性與主控應用程式隔離。 您將學習如何：

- 建構專案以支援外掛程式。
- 建立自訂 <xref:System.Runtime.Loader.AssemblyLoadContext> 以載入每個外掛程式。
- 使用 <xref:System.Runtime.Loader.AssemblyDependencyResolver?displayProperty=fullName> 類型以允許外掛程式具有相依性。
- 撰寫只要複製組建成品即可輕鬆部署的外掛程式。

## <a name="prerequisites"></a>先決條件

- 安裝 [.net 5 SDK](https://dotnet.microsoft.com/download) 或更新版本。

> [!NOTE]
> 此範例程式碼的目標是 .NET 5，但它使用的所有功能都是在 .NET Core 3.0 中引進，之後所有 .NET 版本都有提供。

## <a name="create-the-application"></a>建立應用程式

第一個步驟是建立應用程式：

1. 建立新的資料夾，然後在該資料夾中執行下列命令：

    ```dotnetcli
    dotnet new console -o AppWithPlugin
    ```

2. 若要更輕鬆地建立專案，請在相同的資料夾中建立 Visual Studio 方案檔。 執行以下命令：

    ```dotnetcli
    dotnet new sln
    ```

3. 執行下列命令，以將應用程式專案新增至方案：

    ```dotnetcli
    dotnet sln add AppWithPlugin/AppWithPlugin.csproj
    ```

現在，我們可以填入應用程式的基本架構。 以下列程式碼取代 *AppWithPlugin/Program.cs* 檔案中的程式碼：

```csharp
using PluginBase;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Reflection;

namespace AppWithPlugin
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                if (args.Length == 1 && args[0] == "/d")
                {
                    Console.WriteLine("Waiting for any key...");
                    Console.ReadLine();
                }

                // Load commands from plugins.

                if (args.Length == 0)
                {
                    Console.WriteLine("Commands: ");
                    // Output the loaded commands.
                }
                else
                {
                    foreach (string commandName in args)
                    {
                        Console.WriteLine($"-- {commandName} --");

                        // Execute the command with the name passed as an argument.

                        Console.WriteLine();
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex);
            }
        }
    }
}

```

## <a name="create-the-plugin-interfaces"></a>建立外掛程式介面

建置具有外掛程式之應用程式其下一步是定義外掛程式需要實作的介面。 建議您建立類別庫，其中包含您打算用來在應用程式與外掛程式之間通訊的任何類型。 這項劃分可讓您以套件形式發佈外掛程式介面，而不必提供完整的應用程式。

在專案的根資料夾中，執行 `dotnet new classlib -o PluginBase`。 另外執行 `dotnet sln add PluginBase/PluginBase.csproj` 以將專案新增至方案檔。 刪除 `PluginBase/Class1.cs` 檔案，並在 `PluginBase` 資料夾中，使用下列介面定義來建立名為 `ICommand.cs` 的新檔案：

[!code-csharp[the-plugin-interface](~/samples/snippets/core/tutorials/creating-app-with-plugin-support/csharp/PluginBase/ICommand.cs)]

此 `ICommand` 介面是所有外掛程式都會實作的介面。

現在已定義 `ICommand` 介面，可以為應用程式專案多填入一些資訊。 從根資料夾使用 `dotnet add AppWithPlugin/AppWithPlugin.csproj reference PluginBase/PluginBase.csproj` 命令，將 `AppWithPlugin` 專案的參考新增至 `PluginBase` 專案。

以下列程式碼片段取代 `// Load commands from plugins` 註解，讓它從指定的檔案路徑載入外掛程式：

```csharp
string[] pluginPaths = new string[]
{
    // Paths to plugins to load.
};

IEnumerable<ICommand> commands = pluginPaths.SelectMany(pluginPath =>
{
    Assembly pluginAssembly = LoadPlugin(pluginPath);
    return CreateCommands(pluginAssembly);
}).ToList();
```

然後以下列程式碼片段取代 `// Output the loaded commands` 註解：

```csharp
foreach (ICommand command in commands)
{
    Console.WriteLine($"{command.Name}\t - {command.Description}");
}
```

以下列程式碼片段取代 `// Execute the command with the name passed as an argument` 註解：

```csharp
ICommand command = commands.FirstOrDefault(c => c.Name == commandName);
if (command == null)
{
    Console.WriteLine("No such command is known.");
    return;
}

command.Execute();
```

最後，將靜態方法新增至名為 `LoadPlugin` 和 `CreateCommands` 的 `Program` 類別，如下所示：

```csharp
static Assembly LoadPlugin(string relativePath)
{
    throw new NotImplementedException();
}

static IEnumerable<ICommand> CreateCommands(Assembly assembly)
{
    int count = 0;

    foreach (Type type in assembly.GetTypes())
    {
        if (typeof(ICommand).IsAssignableFrom(type))
        {
            ICommand result = Activator.CreateInstance(type) as ICommand;
            if (result != null)
            {
                count++;
                yield return result;
            }
        }
    }

    if (count == 0)
    {
        string availableTypes = string.Join(",", assembly.GetTypes().Select(t => t.FullName));
        throw new ApplicationException(
            $"Can't find any type which implements ICommand in {assembly} from {assembly.Location}.\n" +
            $"Available types: {availableTypes}");
    }
}
```

## <a name="load-plugins"></a>載入外掛程式

現在，應用程式可以從載入的外掛程式元件正確地載入和具現化命令，但仍然無法載入外掛程式元件。 在 *AppWithPlugin* 資料夾中，使用下列內容來建立名為 *PluginLoadContext.cs* 的檔案：

[!code-csharp[loading-plugins](~/samples/snippets/core/tutorials/creating-app-with-plugin-support/csharp/AppWithPlugin/PluginLoadContext.cs)]

`PluginLoadContext` 類型衍生自 <xref:System.Runtime.Loader.AssemblyLoadContext>。 `AssemblyLoadContext`類型是執行時間中的特殊類型，可讓開發人員將載入的元件隔離到不同的群組，以確保元件版本不會衝突。 此外，自訂 `AssemblyLoadContext` 可以選擇要從中載入組件的不同路徑，並覆寫預設行為。 `PluginLoadContext` 使用 .NET Core 3.0 中引進的 `AssemblyDependencyResolver` 類型執行個體，將組件名稱解析為路徑。 `AssemblyDependencyResolver` 物件是以 .NET 類別庫路徑所建構。 它會根據類別庫（其路徑已傳遞至函式的檔案）的 *.deps.json* 檔案，將元件和原生程式庫解析為其相對路徑 `AssemblyDependencyResolver` 。 自訂 `AssemblyLoadContext` 可讓外掛程式具有自己的相依性，而 `AssemblyDependencyResolver` 可讓您輕鬆正確地載入相依性。

現在 `AppWithPlugin` 專案具有 `PluginLoadContext` 類型，請以下列主體更新 `Program.LoadPlugin` 方法：

```csharp
static Assembly LoadPlugin(string relativePath)
{
    // Navigate up to the solution root
    string root = Path.GetFullPath(Path.Combine(
        Path.GetDirectoryName(
            Path.GetDirectoryName(
                Path.GetDirectoryName(
                    Path.GetDirectoryName(
                        Path.GetDirectoryName(typeof(Program).Assembly.Location)))))));

    string pluginLocation = Path.GetFullPath(Path.Combine(root, relativePath.Replace('\\', Path.DirectorySeparatorChar)));
    Console.WriteLine($"Loading commands from: {pluginLocation}");
    PluginLoadContext loadContext = new PluginLoadContext(pluginLocation);
    return loadContext.LoadFromAssemblyName(new AssemblyName(Path.GetFileNameWithoutExtension(pluginLocation)));
}
```

藉由對每個外掛程式使用不同的 `PluginLoadContext` 執行個體，外掛程式就可以有不同或甚至衝突的相依性，而不會發生問題。

## <a name="simple-plugin-with-no-dependencies"></a>沒有相依性的簡單外掛程式

回到根資料夾，執行下列動作：

1. 執行下列命令，以建立名為的新類別庫專案 `HelloPlugin` ：

    ```dotnetcli
    dotnet new classlib -o HelloPlugin
    ```

2. 執行下列命令以將專案新增至 `AppWithPlugin` 方案：

    ```dotnetcli
    dotnet sln add HelloPlugin/HelloPlugin.csproj
    ```

3. 使用下列內容，以名為 *HelloCommand.cs* 的檔案取代名為 *HelloPlugin/Class1.cs* 的檔案：

[!code-csharp[the-hello-plugin](~/samples/snippets/core/tutorials/creating-app-with-plugin-support/csharp/HelloPlugin/HelloCommand.cs)]

現在，開啟 *HelloPlugin.csproj* 檔案。 看起來應類似下列範例：

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5</TargetFramework>
  </PropertyGroup>

</Project>

```

在 `<Project>` 標籤之間，新增下列項目：

```xml
<ItemGroup>
    <ProjectReference Include="..\PluginBase\PluginBase.csproj">
        <Private>false</Private>
        <ExcludeAssets>runtime</ExcludeAssets>
    </ProjectReference>
</ItemGroup>
```

`<Private>false</Private>`元素很重要。 這會指示 MSBuild 不要將 *PluginBase.dll* 複製到 HelloPlugin 的輸出目錄。 如果 *PluginBase.dll* 組件存在於輸出目錄中，`PluginLoadContext` 會在其中尋找組件，並在載入 *HelloPlugin.dll* 組件時將它載入。 此時，`HelloPlugin.HelloCommand` 類型會從 `HelloPlugin` 專案輸出目錄中的 *PluginBase.dll* 實作 `ICommand` 介面，而不是實作預設載入內容中所載入的 `ICommand` 介面。 由於執行時間會將這兩種類型視為不同元件的不同類型，因此 `AppWithPlugin.Program.CreateCommands` 方法找不到這些命令。 因此，需要 `<Private>false</Private>` 中繼資料才能參考含有外掛程式介面的組件。

同樣地， `<ExcludeAssets>runtime</ExcludeAssets>` 如果參考其他封裝，元素也很重要 `PluginBase` 。 這項設定與 `<Private>false</Private>` `PluginBase` 專案或其中一個相依性可能包含的封裝參考相同，也會有相同的效果。

現在 `HelloPlugin` 專案已完成，您應該更新 `AppWithPlugin` 專案，以瞭解 `HelloPlugin` 可以找到外掛程式的位置。 在 `// Paths to plugins to load` 批註之後，新增 `@"HelloPlugin\bin\Debug\netcoreapp3.0\HelloPlugin.dll"` (此路徑可能會根據您用來) 作為陣列元素的 .net Core 版本而不同 `pluginPaths` 。

## <a name="plugin-with-library-dependencies"></a>具有程式庫相依性的外掛程式

幾乎所有外掛程式都比簡單的 "Hello World" 還要複雜，且許多外掛程式都會相依於其他程式庫。 範例中的 `JsonPlugin` 和 `OldJson` 外掛程式專案示範兩個外掛程式，其中包含相依於 `Newtonsoft.Json` 的 NuGet 套件相依性。 專案檔本身不會有專案參考的任何特殊資訊，而且 (在將外掛程式路徑新增至 `pluginPaths` 陣列) 外掛程式會順利執行，即使在相同的 AppWithPlugin 應用程式執行中執行也一樣。 不過，這些專案不會將參考的元件複製到它們的輸出目錄中，因此元件必須存在於使用者的電腦上，才能讓外掛程式運作。 此問題有兩個解決方法。 第一個選項是使用 `dotnet publish` 命令來發佈類別庫。 或者，如果您想要能夠使用外掛程式的 `dotnet build` 輸出，您可以在外掛程式專案檔的 `<PropertyGroup>` 標籤之間新增 `<CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>` 屬性。 如需範例，請參閱 `XcopyablePlugin` 外掛程式專案。

## <a name="other-examples-in-the-sample"></a>範例中的其他範例

在 [the dotnet/samples 存放庫](https://github.com/dotnet/samples/tree/master/core/extensions/AppWithPlugin)中可以找到此教學課程的完整原始程式碼。 完整的範例包含 `AssemblyDependencyResolver` 行為的一些其他範例。 例如，`AssemblyDependencyResolver` 物件也可以解析 NuGet 套件隨附的原生程式庫，以及當地語系化附屬組件。 範例存放庫中的 `UVPlugin` 和 `FrenchPlugin` 示範了這些案例。

## <a name="reference-a-plugin-interface-from-a-nuget-package"></a>從 NuGet 套件參考外掛程式介面

假設應用程式 A 在 NuGet 套件中定義了名為 `A.PluginBase` 的外掛程式介面。 如何在您的外掛程式專案中正確地參考套件？ 針對專案參考，在專案檔中的 `ProjectReference` 項目上使用 `<Private>false</Private>` 中繼資料可防止將 DLL 複製到輸出。

若要正確地參考 `A.PluginBase` 套件，您需要將專案檔中的 `<PackageReference>` 項目變更如下：

```xml
<PackageReference Include="A.PluginBase" Version="1.0.0">
    <ExcludeAssets>runtime</ExcludeAssets>
</PackageReference>
```

這可防止將 `A.PluginBase` 組件複製到您外掛程式的輸出目錄，並確保外掛程式將會使用 A 的 `A.PluginBase` 版本。

## <a name="plugin-target-framework-recommendations"></a>外掛程式目標 Framework 建議

因為外掛程式相依性載入使用檔案 *上的.deps.js* ，所以會有與外掛程式的目標架構相關的陷阱。 具體而言，您的外掛程式應以執行時間（例如 .NET 5）為目標，而不是 .NET Standard 版本。 *.deps.json* 檔案是根據專案的目標 Framework 所產生；由於許多 .NET Standard 相容套件提供針對 .NET Standard 進行建置的參考組件，以及適用於特定執行階段的實作組件，因此 *.deps.json* 可能無法正確看到實作組件，或可能抓取 .NET Standard 版本的組件，而不是您預期的 .NET Core 版本。

## <a name="plugin-framework-references"></a>外掛程式架構參考

目前，外掛程式無法在程式中引入新的架構。 例如，您無法將使用架構的外掛程式載入 `Microsoft.AspNetCore.App` 只使用根架構的應用程式 `Microsoft.NETCore.App` 。 主機應用程式必須宣告外掛程式所需之所有架構的參考。
