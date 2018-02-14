---
title: "适用于 NuGet 的 .NET Compiler Platform 分析器格式 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: ".NET 分析器的约定，与实现 API 或库的 NuGet 包一起打包并分发。"
keywords: "NuGet 分析器约定, .NET 分析器, NuGet 和 .NET Compiler Platform, NuGet 和 Roslyn"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e44cfa609c14422d50769e512108844cbd2f96a4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="9e7e7-104">分析器 NuGet 格式</span><span class="sxs-lookup"><span data-stu-id="9e7e7-104">Analyzer NuGet formats</span></span>

<span data-ttu-id="9e7e7-105">借助 .NET Compiler Platform（也称为“Roslyn”），开发人员可创建 [分析器] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)，用于在写入代码时检查其语法树和语义。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-105">The .NET Compiler Platform (also known as "Roslyn") allow developers to create [analyzers] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="9e7e7-106">这为开发人员提供了创建方法和域特定的分析工具（如帮助指导如何使用特定 API 或库的工具）。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-106">This provides developers with a way to create and domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="9e7e7-107">可以在 [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki 上找到详细信息。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-107">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="9e7e7-108">另请参阅下文：MSDN 杂志中的[使用 Roslyn 编写 API 的实时代码分析器](https://msdn.microsoft.com/magazine/dn879356.aspx)</span><span class="sxs-lookup"><span data-stu-id="9e7e7-108">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="9e7e7-109">分析器本身通常作为实现 API 或相关库的 NuGet 包的一部分进行打包和分发。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-109">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="9e7e7-110">有关典型的示例，请参阅 [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) 包，其中包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="9e7e7-110">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="9e7e7-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9e7e7-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="9e7e7-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9e7e7-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="9e7e7-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="9e7e7-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="9e7e7-114">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="9e7e7-114">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="9e7e7-115">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9e7e7-115">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="9e7e7-116">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9e7e7-116">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="9e7e7-117">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="9e7e7-117">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="9e7e7-118">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="9e7e7-118">tools\install.ps1</span></span>
- <span data-ttu-id="9e7e7-119">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="9e7e7-119">tools\uninstall.ps1</span></span>

<span data-ttu-id="9e7e7-120">正如所见，分析器 DLL 放置于包中的 `analyzers` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-120">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="9e7e7-121">属性文件放置于 `build` 文件夹中，包括这些文件是为了禁用旧的 FxCop 规则以支持分析器实现。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-121">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="9e7e7-122">支持使用 `packages.config` 的项目的安装和卸载脚本放置于 `tools` 中。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-122">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="9e7e7-123">另请注意，因为此包没有平台特定的需求，因此 `platform` 文件夹已省略。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-123">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="9e7e7-124">分析器路径格式</span><span class="sxs-lookup"><span data-stu-id="9e7e7-124">Analyzers path format</span></span>

<span data-ttu-id="9e7e7-125">`analyzers` 文件夹的使用类似于用于 [框架目标](../create-packages/supporting-multiple-target-frameworks.md)，只是路径中的说明符描述开发主机依赖项而不是生成时。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-125">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="9e7e7-126">常规格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="9e7e7-126">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- <span data-ttu-id="9e7e7-127">**framework_name**：所包含 DLL 需要运行的 .NET framework 的可选 API 外围应用。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-127">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="9e7e7-128">`dotnet` 是目前唯一有效的值，因为 Roslyn 是唯一可运行分析器的主机。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-128">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="9e7e7-129">如果未指定目标，则假定 DLL 适用于所有目标。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-129">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="9e7e7-130">**supported_language**：DLL 适用的语言，`cs` (C#)、`vb` (Visual Basic) 和 `fs` 中的一种。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-130">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="9e7e7-131">语言表示应仅为使用该语言的项目加载分析器。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-131">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="9e7e7-132">如果未指定任何语言，则假定 DLL 适用于支持分析器的所有语言。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-132">If no language is specified then DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="9e7e7-133">**analyzer_name**：指定分析器的 DLL。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-133">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="9e7e7-134">如果需要 DLL 以外的其他文件，必须通过目标或属性文件包括它们。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-134">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="9e7e7-135">安装和卸载脚本</span><span class="sxs-lookup"><span data-stu-id="9e7e7-135">Install and uninstall scripts</span></span>

<span data-ttu-id="9e7e7-136">如果用户的项目使用的是 `packages.config`，则选取分析器的 MSBuild 脚本不起作用，因此应在 `tools` 文件夹中包含具有以下所述内容的 `install.ps1` 和 `uninstall.ps1` 文件。</span><span class="sxs-lookup"><span data-stu-id="9e7e7-136">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="9e7e7-137">**install.ps1 文件内容**</span><span class="sxs-lookup"><span data-stu-id="9e7e7-137">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="9e7e7-138">**uninstall.ps1 文件内容**</span><span class="sxs-lookup"><span data-stu-id="9e7e7-138">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```