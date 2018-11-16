---
title: 推送符号包，NuGet API |Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 发布服务允许客户端发布新的符号包。
keywords: NuGet API 推送符号包
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580410"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="80211-104">推送符号包</span><span class="sxs-lookup"><span data-stu-id="80211-104">Push Symbol Packages</span></span>

<span data-ttu-id="80211-105">可以将包推送符号 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 使用 NuGet V3 API。</span><span class="sxs-lookup"><span data-stu-id="80211-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="80211-106">这些操作所基于的中断`SymbolPackagePublish`资源中找到[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="80211-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="80211-107">版本管理</span><span class="sxs-lookup"><span data-stu-id="80211-107">Versioning</span></span>

<span data-ttu-id="80211-108">以下`@type`使用值：</span><span class="sxs-lookup"><span data-stu-id="80211-108">The following `@type` value is used:</span></span>

<span data-ttu-id="80211-109">@type 值</span><span class="sxs-lookup"><span data-stu-id="80211-109">@type value</span></span>                 | <span data-ttu-id="80211-110">说明</span><span class="sxs-lookup"><span data-stu-id="80211-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="80211-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="80211-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="80211-112">初始版本</span><span class="sxs-lookup"><span data-stu-id="80211-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="80211-113">基 URL</span><span class="sxs-lookup"><span data-stu-id="80211-113">Base URL</span></span>

<span data-ttu-id="80211-114">以下 Api 的基 URL 是的值`@id`的属性`SymbolPackagePublish/4.9.0`包源中的资源[服务索引](service-index.md)。</span><span class="sxs-lookup"><span data-stu-id="80211-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="80211-115">以下文档中，使用 nuget.org 的 URL。</span><span class="sxs-lookup"><span data-stu-id="80211-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="80211-116">请考虑`https://www.nuget.org/api/v2/symbolpackage`作为占位符`@id`服务索引中找到的值。</span><span class="sxs-lookup"><span data-stu-id="80211-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="80211-117">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="80211-117">HTTP methods</span></span>

<span data-ttu-id="80211-118">`PUT`此资源是否支持 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="80211-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="80211-119">推送符号包</span><span class="sxs-lookup"><span data-stu-id="80211-119">Push a symbol package</span></span>

<span data-ttu-id="80211-120">nuget.org 支持推送新的符号包格式 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 使用以下 API。</span><span class="sxs-lookup"><span data-stu-id="80211-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="80211-121">可以多次提交具有同一 ID 和版本的符号包。</span><span class="sxs-lookup"><span data-stu-id="80211-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="80211-122">在以下情况下，符号包将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="80211-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="80211-123">具有相同的 ID 和版本的包不存在。</span><span class="sxs-lookup"><span data-stu-id="80211-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="80211-124">具有相同的 ID 和版本的符号包已推送，但尚未发布。</span><span class="sxs-lookup"><span data-stu-id="80211-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="80211-125">符号包 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 是无效的 (请参阅[符号包约束](../create-packages/Symbol-Packages-snupkg.md))。</span><span class="sxs-lookup"><span data-stu-id="80211-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="80211-126">请求参数</span><span class="sxs-lookup"><span data-stu-id="80211-126">Request parameters</span></span>

<span data-ttu-id="80211-127">name</span><span class="sxs-lookup"><span data-stu-id="80211-127">Name</span></span>           | <span data-ttu-id="80211-128">内</span><span class="sxs-lookup"><span data-stu-id="80211-128">In</span></span>     | <span data-ttu-id="80211-129">类型</span><span class="sxs-lookup"><span data-stu-id="80211-129">Type</span></span>   | <span data-ttu-id="80211-130">必需</span><span class="sxs-lookup"><span data-stu-id="80211-130">Required</span></span> | <span data-ttu-id="80211-131">说明</span><span class="sxs-lookup"><span data-stu-id="80211-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="80211-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="80211-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="80211-133">Header</span><span class="sxs-lookup"><span data-stu-id="80211-133">Header</span></span> | <span data-ttu-id="80211-134">字符串</span><span class="sxs-lookup"><span data-stu-id="80211-134">string</span></span> | <span data-ttu-id="80211-135">是</span><span class="sxs-lookup"><span data-stu-id="80211-135">yes</span></span>      | <span data-ttu-id="80211-136">例如，`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="80211-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="80211-137">API 密钥是从包源获得由用户和配置到客户端不透明的字符串。</span><span class="sxs-lookup"><span data-stu-id="80211-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="80211-138">强制要求任何特定字符串格式，但 API 密钥的长度不应超过合理的大小，为 HTTP 标头值。</span><span class="sxs-lookup"><span data-stu-id="80211-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="80211-139">请求正文</span><span class="sxs-lookup"><span data-stu-id="80211-139">Request body</span></span>

<span data-ttu-id="80211-140">符号推送的请求正文是与包推送请求的请求正文 (请参阅[打包推送和删除](package-publish-resource.md))。</span><span class="sxs-lookup"><span data-stu-id="80211-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="80211-141">响应</span><span class="sxs-lookup"><span data-stu-id="80211-141">Response</span></span>

<span data-ttu-id="80211-142">状态代码</span><span class="sxs-lookup"><span data-stu-id="80211-142">Status Code</span></span> | <span data-ttu-id="80211-143">含义</span><span class="sxs-lookup"><span data-stu-id="80211-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="80211-144">201</span><span class="sxs-lookup"><span data-stu-id="80211-144">201</span></span>         | <span data-ttu-id="80211-145">已成功推送符号包。</span><span class="sxs-lookup"><span data-stu-id="80211-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="80211-146">400</span><span class="sxs-lookup"><span data-stu-id="80211-146">400</span></span>         | <span data-ttu-id="80211-147">提供的符号包无效。</span><span class="sxs-lookup"><span data-stu-id="80211-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="80211-148">401</span><span class="sxs-lookup"><span data-stu-id="80211-148">401</span></span>         | <span data-ttu-id="80211-149">用户无权执行此操作。</span><span class="sxs-lookup"><span data-stu-id="80211-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="80211-150">404</span><span class="sxs-lookup"><span data-stu-id="80211-150">404</span></span>         | <span data-ttu-id="80211-151">具有提供的 ID 和版本的相应包不存在。</span><span class="sxs-lookup"><span data-stu-id="80211-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="80211-152">409</span><span class="sxs-lookup"><span data-stu-id="80211-152">409</span></span>         | <span data-ttu-id="80211-153">已推送符号包具有提供的 ID 和版本，但尚不可用。</span><span class="sxs-lookup"><span data-stu-id="80211-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="80211-154">413</span><span class="sxs-lookup"><span data-stu-id="80211-154">413</span></span>         | <span data-ttu-id="80211-155">包是太大。</span><span class="sxs-lookup"><span data-stu-id="80211-155">The package is too large.</span></span>
