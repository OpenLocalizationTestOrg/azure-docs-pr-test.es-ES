---
title: "Actualización a la versión 1.1 del SDK de .NET para Azure Search | Microsoft Docs"
description: "Actualización a la versión 1.1 del SDK de .NET para Búsqueda de Azure"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 9782454e3bfc697b63cde8aa28a14be0c393c36b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a><span data-ttu-id="4f812-103">Actualización a la versión 3 del SDK de .NET para Azure Search</span><span class="sxs-lookup"><span data-stu-id="4f812-103">Upgrading to the Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="4f812-104">Si usa la versión preliminar 2.0 o posterior del [SDK de .NET para Azure Search](https://aka.ms/search-sdk), este artículo le ayudará a actualizar la aplicación para que use la versión 3.</span><span class="sxs-lookup"><span data-stu-id="4f812-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span></span>

<span data-ttu-id="4f812-105">Para obtener un tutorial más general del SDK que incluya ejemplos, vea [Cómo usar Búsqueda de Azure desde una aplicación .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4f812-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="4f812-106">La versión 3 del SDK de .NET para Azure Search contiene algunos cambios de versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="4f812-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="4f812-107">La mayoría son de menor importancia, por lo que cambiar el código solo precisará del mínimo esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="4f812-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="4f812-108">Vea [Pasos para actualizar](#UpgradeSteps) , a fin de obtener instrucciones sobre cómo cambiar el código para usar la nueva versión del SDK.</span><span class="sxs-lookup"><span data-stu-id="4f812-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="4f812-109">Si usa la versión 1.0.2-preview o anterior, debe actualizar primero a la versión 1.1 y luego a la versión 3.</span><span class="sxs-lookup"><span data-stu-id="4f812-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span></span> <span data-ttu-id="4f812-110">Consulte [Apéndice: pasos para actualizar a la versión 1.1](#UpgradeStepsV1) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="4f812-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="4f812-111">La instancia del servicio Azure Search es compatible con varias versiones de API de REST, incluida la más reciente.</span><span class="sxs-lookup"><span data-stu-id="4f812-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="4f812-112">Puede seguir usando una versión aunque no sea la más reciente, pero es recomendable que migre el código para usar la versión más actualizada.</span><span class="sxs-lookup"><span data-stu-id="4f812-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span> <span data-ttu-id="4f812-113">Cuando se usa la API de REST, debe especificar la versión de API en cada solicitud realizada a través del parámetro api-version.</span><span class="sxs-lookup"><span data-stu-id="4f812-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span></span> <span data-ttu-id="4f812-114">Al usar el SDK. NET, la versión del SDK que usa determina la versión correspondiente de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="4f812-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span></span> <span data-ttu-id="4f812-115">Si usa un SDK anterior, puede seguir ejecutando ese código sin realizar ningún cambio, incluso si el servicio se ha actualizado para admitir una versión más reciente de la API.</span><span class="sxs-lookup"><span data-stu-id="4f812-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="4f812-116">Novedades de la versión 3</span><span class="sxs-lookup"><span data-stu-id="4f812-116">What's new in version 3</span></span>
<span data-ttu-id="4f812-117">La versión 3 del SDK de .NET para Azure Search tiene como destino la versión más reciente con disponibilidad general de la API de REST de Azure Search, en concreto la del 01-09-2016.</span><span class="sxs-lookup"><span data-stu-id="4f812-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="4f812-118">Esto hace posible el uso de muchas características de Azure Search desde una aplicación. NET, incluidas las siguientes:</span><span class="sxs-lookup"><span data-stu-id="4f812-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span></span>

* [<span data-ttu-id="4f812-119">Analizadores personalizados</span><span class="sxs-lookup"><span data-stu-id="4f812-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="4f812-120">Compatibilidad del indexador de [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) y [Azure Table Storage](search-howto-indexing-azure-tables.md)</span><span class="sxs-lookup"><span data-stu-id="4f812-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="4f812-121">Personalización de indizador mediante [asignaciones de campos](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="4f812-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="4f812-122">Compatibilidad con ETags para permitir actualizaciones seguras simultáneas de definiciones de índice, indizadores y orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="4f812-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="4f812-123">Compatibilidad con la generación de definiciones de campos de índice de forma declarativa mediante la decoración de la clase model y el uso de la nueva clase `FieldBuilder`.</span><span class="sxs-lookup"><span data-stu-id="4f812-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span></span>
* <span data-ttu-id="4f812-124">Compatibilidad con .NET Core y .NET Portable Profile 111</span><span class="sxs-lookup"><span data-stu-id="4f812-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="4f812-125">Pasos para actualizar</span><span class="sxs-lookup"><span data-stu-id="4f812-125">Steps to upgrade</span></span>
<span data-ttu-id="4f812-126">En primer lugar, actualice la referencia de NuGet para `Microsoft.Azure.Search` mediante la Consola del Administrador de paquetes NuGet, o bien haga clic con el botón derecho en las referencias del proyecto y seleccione "Administrar paquetes NuGet" en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f812-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="4f812-127">Una vez que NuGet ha descargado los nuevos paquetes y sus dependencias, recompile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4f812-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="4f812-128">Dependiendo de cómo se estructura el código, se podrá volver a compilar correctamente.</span><span class="sxs-lookup"><span data-stu-id="4f812-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="4f812-129">Si lo consigue, ya estará listo para empezar.</span><span class="sxs-lookup"><span data-stu-id="4f812-129">If so, you're ready to go!</span></span>

<span data-ttu-id="4f812-130">Si se produce un error en la compilación, verá un mensaje similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4f812-130">If your build fails, you should see a build error like the following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="4f812-131">El paso siguiente consiste en corregir los errores de compilación.</span><span class="sxs-lookup"><span data-stu-id="4f812-131">The next step is to fix this build error.</span></span> <span data-ttu-id="4f812-132">Consulte [Cambios importantes en la versión 3](#ListOfChanges) para más información sobre las causas del error y cómo corregirlo.</span><span class="sxs-lookup"><span data-stu-id="4f812-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span></span>

<span data-ttu-id="4f812-133">Puede ver las advertencias de compilación adicionales relacionadas con propiedades o métodos obsoletos.</span><span class="sxs-lookup"><span data-stu-id="4f812-133">You may see additional build warnings related to obsolete methods or properties.</span></span> <span data-ttu-id="4f812-134">Las advertencias incluyen instrucciones sobre qué utilizar en lugar de la característica en desuso.</span><span class="sxs-lookup"><span data-stu-id="4f812-134">The warnings will include instructions on what to use instead of the deprecated feature.</span></span> <span data-ttu-id="4f812-135">Por ejemplo, si la aplicación utiliza la propiedad `IndexingParameters.Base64EncodeKeys`, recibirá una advertencia que indica lo siguiente: `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="4f812-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="4f812-136">Una vez que haya solucionado los errores de compilación, puede realizar cambios a la aplicación para aprovechar las ventajas de la nueva funcionalidad, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="4f812-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span> <span data-ttu-id="4f812-137">Las nuevas características en el SDK se detallan en [Novedades de la versión 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="4f812-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="4f812-138">Cambios importantes en la versión 3</span><span class="sxs-lookup"><span data-stu-id="4f812-138">Breaking changes in version 3</span></span>
<span data-ttu-id="4f812-139">Hay solo algunos cambios importantes en la versión 3 que pueden requerir cambios de código además de la recompilación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f812-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="4f812-140">Tipo de valor devuelto de Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="4f812-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="4f812-141">El método `Indexes.GetClient` tiene un nuevo tipo de valor devuelto.</span><span class="sxs-lookup"><span data-stu-id="4f812-141">The `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="4f812-142">Anteriormente devolvía `SearchIndexClient`, pero se ha cambiado a `ISearchIndexClient` en la versión 2.0-preview, y ese cambio se traslada a la versión 3.</span><span class="sxs-lookup"><span data-stu-id="4f812-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span></span> <span data-ttu-id="4f812-143">Sirve para admitir clientes que deseen simular el método `GetClient` para las pruebas unitarias devolviendo una implementación ficticia de `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="4f812-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="4f812-144">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f812-144">Example</span></span>
<span data-ttu-id="4f812-145">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="4f812-146">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-146">You can change it to this to fix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a><span data-ttu-id="4f812-147">AnalyzerName, DataType y otros ya no se pueden convertir de manera implícita en cadenas</span><span class="sxs-lookup"><span data-stu-id="4f812-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span></span>
<span data-ttu-id="4f812-148">Hay muchos tipos en el SDK de .NET para Azure Search que derivan de `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="4f812-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="4f812-149">Anteriormente, todos estos tipos eran convertibles de manera implícita en el tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="4f812-149">Previously these types were all implicitly convertible to type `string`.</span></span> <span data-ttu-id="4f812-150">Sin embargo, se detectó un error en la implementación de `Object.Equals` para estas clases y para corregir el error fue necesario deshabilitar esta conversión implícita.</span><span class="sxs-lookup"><span data-stu-id="4f812-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span></span> <span data-ttu-id="4f812-151">La conversión explícita a `string` todavía se permite.</span><span class="sxs-lookup"><span data-stu-id="4f812-151">Explicit conversion to `string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="4f812-152">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f812-152">Example</span></span>
<span data-ttu-id="4f812-153">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="4f812-154">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-154">You can change it to this to fix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="4f812-155">Miembros obsoletos quitados</span><span class="sxs-lookup"><span data-stu-id="4f812-155">Removed obsolete members</span></span>

<span data-ttu-id="4f812-156">Es posible que vea errores de compilación relacionados con métodos o propiedades que se marcaron como obsoletos en la versión 2.0-preview y que posteriormente se eliminaron en la versión 3.</span><span class="sxs-lookup"><span data-stu-id="4f812-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="4f812-157">Si se encuentra con tales errores, aquí le decimos cómo resolverlos:</span><span class="sxs-lookup"><span data-stu-id="4f812-157">If you encounter such errors, here is how to resolve them:</span></span>

- <span data-ttu-id="4f812-158">Si usaba este constructor: `ScoringParameter(string name, string value)`, utilice en su lugar este: `ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="4f812-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="4f812-159">Si usaba la propiedad `ScoringParameter.Value`, utilice en su lugar la propiedad `ScoringParameter.Values` o el método `ToString`.</span><span class="sxs-lookup"><span data-stu-id="4f812-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span></span>
- <span data-ttu-id="4f812-160">Si usaba la propiedad `SearchRequestOptions.RequestId`, utilice en su lugar la propiedad `ClientRequestId`.</span><span class="sxs-lookup"><span data-stu-id="4f812-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="4f812-161">Características quitadas de la versión preliminar</span><span class="sxs-lookup"><span data-stu-id="4f812-161">Removed preview features</span></span>

<span data-ttu-id="4f812-162">Si va a actualizar de la versión 2.0-preview a la versión 3, debe saber que se ha eliminado la compatibilidad con el análisis de JSON y CSV en los indexadores de blobs dado que estás características se encuentran aún en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="4f812-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="4f812-163">En concreto, se han quitado los siguientes métodos de la clase `IndexingParametersExtensions`:</span><span class="sxs-lookup"><span data-stu-id="4f812-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="4f812-164">Si la aplicación tiene una dependencia fuerte de estas características, no podrá actualizar a la versión 3 del SDK de Azure Search para .NET.</span><span class="sxs-lookup"><span data-stu-id="4f812-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span></span> <span data-ttu-id="4f812-165">Podrá seguir usando la versión 2.0-preview.</span><span class="sxs-lookup"><span data-stu-id="4f812-165">You can continue to use version 2.0-preview.</span></span> <span data-ttu-id="4f812-166">Sin embargo, tenga en cuenta que **no se recomienda usar SDK de versión preliminar en aplicaciones de producción**.</span><span class="sxs-lookup"><span data-stu-id="4f812-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="4f812-167">Las características de versión preliminar son solo para evaluación y pueden cambiar.</span><span class="sxs-lookup"><span data-stu-id="4f812-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4f812-168">Conclusión</span><span class="sxs-lookup"><span data-stu-id="4f812-168">Conclusion</span></span>
<span data-ttu-id="4f812-169">Si necesita más detalles sobre el uso del SDK de .NET para Búsqueda de Azure, vea nuestras instrucciones actualizadas recientemente y los artículos de [procedimientos](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4f812-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="4f812-170">Agradecemos sus comentarios sobre el SDK.</span><span class="sxs-lookup"><span data-stu-id="4f812-170">We welcome your feedback on the SDK.</span></span> <span data-ttu-id="4f812-171">Si tiene algún problema, no dude en pedirnos ayuda en el [foro de MSDN sobre Búsqueda de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="4f812-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="4f812-172">Si encuentra un error, puede enviarlo al [repositorio de GitHub del SDK de .NET para Azure](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="4f812-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="4f812-173">Asegúrese de que prefija el título del problema con "SDK de búsqueda: ".</span><span class="sxs-lookup"><span data-stu-id="4f812-173">Make sure to prefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="4f812-174">Gracias por usar Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f812-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a><span data-ttu-id="4f812-175">Apéndice: pasos para actualizar a la versión 1.1</span><span class="sxs-lookup"><span data-stu-id="4f812-175">Appendix: Steps to upgrade to version 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="4f812-176">Esta sección se aplica únicamente a los usuarios de la versión de SDK de Azure Search para .NET 1.0.2-preview y anteriores.</span><span class="sxs-lookup"><span data-stu-id="4f812-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="4f812-177">En primer lugar, actualice la referencia de NuGet para `Microsoft.Azure.Search` mediante la Consola del Administrador de paquetes NuGet, o bien haga clic con el botón derecho en las referencias del proyecto y seleccione "Administrar paquetes NuGet" en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4f812-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="4f812-178">Una vez que NuGet ha descargado los nuevos paquetes y sus dependencias, recompile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4f812-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="4f812-179">Si antes usaba las versiones preliminares 1.0.0, 1.0.1 o 1.0.2, la compilación debería ejecutarse correctamente y estará lista para comenzar a usarse.</span><span class="sxs-lookup"><span data-stu-id="4f812-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span></span>

<span data-ttu-id="4f812-180">De lo contrario, si usaba la versión preliminar 0.13.0 u otra anterior, verá errores de compilación como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="4f812-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="4f812-181">El paso siguiente consiste en corregir los errores de compilación uno a uno.</span><span class="sxs-lookup"><span data-stu-id="4f812-181">The next step is to fix the build errors one by one.</span></span> <span data-ttu-id="4f812-182">La mayoría requiere cambiar algunos nombres de clase y método cuyo nombre ha cambiado en el SDK.</span><span class="sxs-lookup"><span data-stu-id="4f812-182">Most will require changing some class and method names that have been renamed in the SDK.</span></span> <span data-ttu-id="4f812-183">[lista de cambios importantes de la versión 1.1](#ListOfChangesV1) contiene una lista de estos cambios de nombre.</span><span class="sxs-lookup"><span data-stu-id="4f812-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="4f812-184">Si usa clases personalizadas para modelar los documentos, y esas clases tienen propiedades de tipos primitivos que no aceptan valores nulos (por ejemplo, `int` o `bool` en C#), hay una corrección de errores en la versión 1.1 del SDK que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="4f812-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span></span> <span data-ttu-id="4f812-185">Para obtener más información, consulte la sección [Correcciones de errores en la versión 1.1](#BugFixesV1) .</span><span class="sxs-lookup"><span data-stu-id="4f812-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="4f812-186">Por último, una vez que haya solucionado los errores de compilación, puede realizar cambios a la aplicación para aprovechar las ventajas de la nueva funcionalidad, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="4f812-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="4f812-187">lista de cambios importantes de la versión 1.1</span><span class="sxs-lookup"><span data-stu-id="4f812-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="4f812-188">La siguiente lista se ordena por la probabilidad de que el cambio afecte al código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4f812-188">The following list is ordered by the likelihood that the change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="4f812-189">Cambios de IndexBatch e IndexAction</span><span class="sxs-lookup"><span data-stu-id="4f812-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="4f812-190">Se ha cambiado el nombre de `IndexBatch.Create` por `IndexBatch.New` y ya no tiene un argumento `params`.</span><span class="sxs-lookup"><span data-stu-id="4f812-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="4f812-191">Puede usar `IndexBatch.New` para los lotes que mezclan distintos tipos de acciones (combinaciones, eliminaciones, etc.).</span><span class="sxs-lookup"><span data-stu-id="4f812-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="4f812-192">Además, existen nuevos métodos estáticos para crear lotes donde todas las acciones son las mismas: `Delete`, `Merge`, `MergeOrUpload` y `Upload`.</span><span class="sxs-lookup"><span data-stu-id="4f812-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="4f812-193">`IndexAction` ya no tiene constructores públicos y sus propiedades ahora son inmutables.</span><span class="sxs-lookup"><span data-stu-id="4f812-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="4f812-194">Necesita usar los nuevos métodos estáticos para crear acciones para propósitos diferentes: `Delete`, `Merge`, `MergeOrUpload` y `Upload`.</span><span class="sxs-lookup"><span data-stu-id="4f812-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="4f812-195">`IndexAction.Create` se ha quitado.</span><span class="sxs-lookup"><span data-stu-id="4f812-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="4f812-196">Si utiliza la sobrecarga que solo usa un documento, asegúrese de usar `Upload` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="4f812-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="4f812-197">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f812-197">Example</span></span>
<span data-ttu-id="4f812-198">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="4f812-199">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-199">You can change it to this to fix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="4f812-200">Si lo desea, puede simplificarlo aún más y optar por este:</span><span class="sxs-lookup"><span data-stu-id="4f812-200">If you want, you can further simplify it to this:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="4f812-201">Cambios de IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="4f812-201">IndexBatchException changes</span></span>
<span data-ttu-id="4f812-202">La propiedad `IndexBatchException.IndexResponse` ha cambiado a `IndexingResults`, y su tipo ahora es `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="4f812-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="4f812-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f812-203">Example</span></span>
<span data-ttu-id="4f812-204">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="4f812-205">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-205">You can change it to this to fix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="4f812-206">Cambios del método de operación</span><span class="sxs-lookup"><span data-stu-id="4f812-206">Operation method changes</span></span>
<span data-ttu-id="4f812-207">Cada operación del SDK de .NET para Búsqueda de Azure se expone como un conjunto de sobrecargas de método para los autores de llamadas sincrónicas y asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="4f812-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="4f812-208">Las firmas y la factorización de estas sobrecargas de método han cambiado en la versión 1.1.</span><span class="sxs-lookup"><span data-stu-id="4f812-208">The signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="4f812-209">Por ejemplo, la operación de "Obtener estadísticas de índice" en versiones anteriores del SDK expone estas firmas:</span><span class="sxs-lookup"><span data-stu-id="4f812-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span></span>

<span data-ttu-id="4f812-210">En `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="4f812-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="4f812-211">En `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="4f812-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="4f812-212">Las firmas de método para la misma operación en la versión 1.1 tienen este aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-212">The method signatures for the same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="4f812-213">En `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="4f812-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="4f812-214">En `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="4f812-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="4f812-215">A partir de la versión 1.1, el SDK de .NET para Búsqueda de Azure organiza los métodos de operación de forma diferente:</span><span class="sxs-lookup"><span data-stu-id="4f812-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="4f812-216">Los parámetros opcionales ahora se modelan como predeterminados en lugar de como sobrecargas de método adicionales.</span><span class="sxs-lookup"><span data-stu-id="4f812-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="4f812-217">Esto reduce el número de sobrecargas de método, en ocasiones drásticamente.</span><span class="sxs-lookup"><span data-stu-id="4f812-217">This reduces the number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="4f812-218">Los métodos de extensión ahora ocultan muchos de los detalles superfluos de HTTP del autor de llamada.</span><span class="sxs-lookup"><span data-stu-id="4f812-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span></span> <span data-ttu-id="4f812-219">Por ejemplo, las versiones anteriores del SDK devuelven un objeto de respuesta con un código de estado HTTP, que a menudo no necesitará comprobar, ya que los métodos de operación lanzan `CloudException` para cualquier código de estado que indica un error.</span><span class="sxs-lookup"><span data-stu-id="4f812-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="4f812-220">Los nuevos métodos de extensión solo devuelven objetos de modelo, lo que le ahorra la molestia de tener que desencapsularlos en el código.</span><span class="sxs-lookup"><span data-stu-id="4f812-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span></span>
* <span data-ttu-id="4f812-221">Por el contrario, las interfaces principales ahora exponen métodos que permiten ejercer un mayor control a nivel de HTTP en caso de que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4f812-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span></span> <span data-ttu-id="4f812-222">Ahora puede pasar encabezados HTTP personalizados para incluirlos en solicitudes y el nuevo tipo de valor devuelto `AzureOperationResponse<T>` le ofrece acceso directo a `HttpRequestMessage` y `HttpResponseMessage` para la operación.</span><span class="sxs-lookup"><span data-stu-id="4f812-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span></span> <span data-ttu-id="4f812-223">`AzureOperationResponse` se define en el espacio de nombres `Microsoft.Rest.Azure` y reemplaza a `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="4f812-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="4f812-224">Cambios de ScoringParameters</span><span class="sxs-lookup"><span data-stu-id="4f812-224">ScoringParameters changes</span></span>
<span data-ttu-id="4f812-225">En el último SDK se agregó una nueva clase llamada `ScoringParameter` para que resulte más fácil proporcionar parámetros a los perfiles de puntuación en una consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4f812-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span></span> <span data-ttu-id="4f812-226">Antes, la propiedad `ScoringProfiles` de la clase `SearchParameters` tenía el tipo `IList<string>`. Ahora, el tipo es `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="4f812-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="4f812-227">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f812-227">Example</span></span>
<span data-ttu-id="4f812-228">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="4f812-229">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-229">You can change it to this to fix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="4f812-230">Cambios de la clase de modelo</span><span class="sxs-lookup"><span data-stu-id="4f812-230">Model class changes</span></span>
<span data-ttu-id="4f812-231">Debido a los cambios de firma descritos en [Cambios del método de operación](#OperationMethodChanges), muchas clases del espacio de nombres `Microsoft.Azure.Search.Models` han cambiado de nombre o se han eliminado.</span><span class="sxs-lookup"><span data-stu-id="4f812-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="4f812-232">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4f812-232">For example:</span></span>

* <span data-ttu-id="4f812-233">`IndexDefinitionResponse` se ha reemplazado por `AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="4f812-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="4f812-234">El nombre de `DocumentSearchResponse` ha cambiado a `DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="4f812-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span></span>
* <span data-ttu-id="4f812-235">El nombre de `IndexResult` ha cambiado a `IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="4f812-235">`IndexResult` has been renamed to `IndexingResult`</span></span>
* <span data-ttu-id="4f812-236">`Documents.Count()` ahora devuelve `long` con el número de documentos en lugar de `DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="4f812-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="4f812-237">El nombre de `IndexGetStatisticsResponse` ha cambiado a `IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="4f812-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="4f812-238">El nombre de `IndexListResponse` ha cambiado a `IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="4f812-238">`IndexListResponse` has been renamed to `IndexListResult`</span></span>

<span data-ttu-id="4f812-239">Para resumir, las clases derivadas de `OperationResponse`que existían solo para encapsular un objeto de modelo se han quitado.</span><span class="sxs-lookup"><span data-stu-id="4f812-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span></span> <span data-ttu-id="4f812-240">El sufijo de las demás clases ha cambiado de `Response` a `Result`.</span><span class="sxs-lookup"><span data-stu-id="4f812-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="4f812-241">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f812-241">Example</span></span>
<span data-ttu-id="4f812-242">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="4f812-243">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-243">You can change it to this to fix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="4f812-244">Clases de respuesta e IEnumerable</span><span class="sxs-lookup"><span data-stu-id="4f812-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="4f812-245">Un cambio adicional que puede afectar a su código es que las clases de respuesta que contienen colecciones ya no implementan `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="4f812-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="4f812-246">En su lugar, puede acceder a la propiedad de colección directamente.</span><span class="sxs-lookup"><span data-stu-id="4f812-246">Instead, you can access the collection property directly.</span></span> <span data-ttu-id="4f812-247">Por ejemplo, si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="4f812-248">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-248">You can change it to this to fix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="4f812-249">Caso especial para aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="4f812-249">Special case for web applications</span></span>
<span data-ttu-id="4f812-250">Si tiene una aplicación web que serializa `DocumentSearchResponse` directamente para enviar los resultados de la búsqueda al explorador, debe cambiar el código o los resultados no se serializarán correctamente.</span><span class="sxs-lookup"><span data-stu-id="4f812-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span></span> <span data-ttu-id="4f812-251">Por ejemplo, si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="4f812-252">Para cambiarlo, obtenga la propiedad `.Results` de la respuesta de búsqueda para corregir la representación de los resultados de la búsqueda:</span><span class="sxs-lookup"><span data-stu-id="4f812-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="4f812-253">Tendrá que buscar esos casos en el código por su cuenta. **El compilador no muestra advertencias** porque `JsonResult.Data` es del tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="4f812-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="4f812-254">Cambios de CloudException</span><span class="sxs-lookup"><span data-stu-id="4f812-254">CloudException changes</span></span>
<span data-ttu-id="4f812-255">La clase `CloudException` se ha desplazado desde el espacio de nombres `Hyak.Common` al espacio de nombres `Microsoft.Rest.Azure`.</span><span class="sxs-lookup"><span data-stu-id="4f812-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="4f812-256">Además, el nombre de su propiedad `Error` ha cambiado a `Body`.</span><span class="sxs-lookup"><span data-stu-id="4f812-256">Also, its `Error` property has been renamed to `Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="4f812-257">Cambios de SearchServiceClient y SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="4f812-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="4f812-258">El tipo de la propiedad `Credentials` ha cambiado de `SearchCredentials` a su clase base, `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4f812-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="4f812-259">Si necesita acceder al valor de `SearchCredentials` de `SearchIndexClient` o `SearchServiceClient`, use la nueva propiedad `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4f812-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span></span>

<span data-ttu-id="4f812-260">En versiones anteriores del SDK, `SearchServiceClient` y `SearchIndexClient` tenían constructores con un parámetro `HttpClient`.</span><span class="sxs-lookup"><span data-stu-id="4f812-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="4f812-261">Estos se han reemplazado con constructores que obtienen `HttpClientHandler` y una matriz de objetos `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="4f812-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="4f812-262">Esto facilita instalar controladores personalizados para procesar previamente las solicitudes HTTP si es necesario.</span><span class="sxs-lookup"><span data-stu-id="4f812-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="4f812-263">Por último, los constructores que requerían `Uri` y `SearchCredentials` han cambiado.</span><span class="sxs-lookup"><span data-stu-id="4f812-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="4f812-264">Por ejemplo, si tiene código con este aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="4f812-265">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-265">You can change it to this to fix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="4f812-266">Observe también que el tipo del parámetro de credenciales ha cambiado a `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4f812-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span></span> <span data-ttu-id="4f812-267">Es poco probable que esto afecte al código, ya que `SearchCredentials` deriva de `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4f812-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="4f812-268">Transferir un identificador de solicitud</span><span class="sxs-lookup"><span data-stu-id="4f812-268">Passing a request ID</span></span>
<span data-ttu-id="4f812-269">En versiones anteriores del SDK, se podía establecer un identificador de solicitud en `SearchServiceClient` o `SearchIndexClient`, que se incluiría en cada solicitud a la API de REST.</span><span class="sxs-lookup"><span data-stu-id="4f812-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span></span> <span data-ttu-id="4f812-270">Esto es útil para solucionar problemas con el servicio de búsqueda si necesita ponerse en contacto con soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="4f812-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span></span> <span data-ttu-id="4f812-271">Sin embargo, es más útil establecer un identificador único de solicitud para cada operación, en lugar de utilizar el mismo identificador para todas las operaciones.</span><span class="sxs-lookup"><span data-stu-id="4f812-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span></span> <span data-ttu-id="4f812-272">Por este motivo, los métodos `SetClientRequestId` de `SearchServiceClient` y `SearchIndexClient` se han quitado.</span><span class="sxs-lookup"><span data-stu-id="4f812-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="4f812-273">En su lugar, puede pasar un identificador de solicitud a cada método de operación mediante el parámetro opcional `SearchRequestOptions` .</span><span class="sxs-lookup"><span data-stu-id="4f812-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="4f812-274">En una futura versión del SDK, agregaremos un nuevo mecanismo para establecer un identificador de solicitud globalmente en los objetos cliente que sea coherente con el enfoque usado por otros SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f812-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="4f812-275">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4f812-275">Example</span></span>
<span data-ttu-id="4f812-276">Si tiene código con este aspecto:</span><span class="sxs-lookup"><span data-stu-id="4f812-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="4f812-277">Puede cambiarlo por este para corregir cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="4f812-277">You can change it to this to fix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="4f812-278">Cambios de nombre de interfaz</span><span class="sxs-lookup"><span data-stu-id="4f812-278">Interface name changes</span></span>
<span data-ttu-id="4f812-279">Los nombres de interfaz del grupo de operaciones han cambiado por coherencia con sus nombres de propiedad correspondientes:</span><span class="sxs-lookup"><span data-stu-id="4f812-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span></span>

* <span data-ttu-id="4f812-280">El nombre del tipo de `ISearchServiceClient.Indexes` ha cambiado de `IIndexOperations` a `IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="4f812-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span></span>
* <span data-ttu-id="4f812-281">El nombre del tipo de `ISearchServiceClient.Indexers` ha cambiado de `IIndexerOperations` a `IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="4f812-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span></span>
* <span data-ttu-id="4f812-282">El nombre del tipo de `ISearchServiceClient.DataSources` ha cambiado de `IDataSourceOperations` a `IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="4f812-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span></span>
* <span data-ttu-id="4f812-283">El nombre del tipo de `ISearchIndexClient.Documents` ha cambiado de `IDocumentOperations` a `IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="4f812-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span></span>

<span data-ttu-id="4f812-284">Es poco probable que este cambio afecte al código, a menos que cree simulacros de estas interfaces a efectos de pruebas.</span><span class="sxs-lookup"><span data-stu-id="4f812-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="4f812-285">Correcciones de errores en la versión 1.1</span><span class="sxs-lookup"><span data-stu-id="4f812-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="4f812-286">Se produjo un error en las versiones anteriores del SDK de .NET para Búsqueda de Azure en relación con la serialización de clases de modelos personalizados.</span><span class="sxs-lookup"><span data-stu-id="4f812-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span></span> <span data-ttu-id="4f812-287">El error puede producirse si ha creado una clase de modelo personalizado con una propiedad de un tipo de valor que no acepta valores NULL.</span><span class="sxs-lookup"><span data-stu-id="4f812-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-to-reproduce"></a><span data-ttu-id="4f812-288">Pasos para reproducir</span><span class="sxs-lookup"><span data-stu-id="4f812-288">Steps to reproduce</span></span>
<span data-ttu-id="4f812-289">Cree una clase de modelo personalizado con una propiedad de tipo de valor que no acepta valores NULL.</span><span class="sxs-lookup"><span data-stu-id="4f812-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="4f812-290">Por ejemplo, agregue una propiedad `UnitCount` pública de tipo `int` en lugar de `int?`.</span><span class="sxs-lookup"><span data-stu-id="4f812-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="4f812-291">Si indexa un documento con el valor predeterminado de ese tipo (por ejemplo, 0 para `int`), el campo será null en Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="4f812-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span></span> <span data-ttu-id="4f812-292">Si desea buscar posteriormente ese documento, la llamada `Search` producirá `JsonSerializationException` indicando que no se puede convertir `null` a `int`.</span><span class="sxs-lookup"><span data-stu-id="4f812-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span></span>

<span data-ttu-id="4f812-293">Además, los filtros pueden no funcionar según lo esperado, ya que se escribió null en el índice, en lugar del valor previsto.</span><span class="sxs-lookup"><span data-stu-id="4f812-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="4f812-294">Detalles de corrección</span><span class="sxs-lookup"><span data-stu-id="4f812-294">Fix details</span></span>
<span data-ttu-id="4f812-295">Corregimos este problema en la versión 1.1 del SDK.</span><span class="sxs-lookup"><span data-stu-id="4f812-295">We have fixed this issue in version 1.1 of the SDK.</span></span> <span data-ttu-id="4f812-296">Ahora, si tiene una clase de modelo similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="4f812-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="4f812-297">y establece `IntValue` en 0, ese valor ahora se serializa correctamente como 0 en la conexión y se almacena como 0 en el índice.</span><span class="sxs-lookup"><span data-stu-id="4f812-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span></span> <span data-ttu-id="4f812-298">El recorrido de ida y vuelta también funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="4f812-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="4f812-299">Hay un posible problema que hay que tener en cuenta con este enfoque: si usa un tipo de modelo con una propiedad que no acepta valores NULL, tendrá que **garantizar** que ningún documento del índice contiene un valor NULL para el campo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="4f812-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="4f812-300">Ni el SDK ni la API de REST para Búsqueda de Azure le permitirá aplicar esto.</span><span class="sxs-lookup"><span data-stu-id="4f812-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span></span>

<span data-ttu-id="4f812-301">Esto no es solo una inquietud hipotética: imagine un escenario donde se agrega un nuevo campo a un índice existente que es de tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="4f812-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="4f812-302">Después de actualizar la definición del índice, todos los documentos tendrán un valor null para ese campo nuevo (ya que todos los tipos aceptan valores NULL en Búsqueda de Azure).</span><span class="sxs-lookup"><span data-stu-id="4f812-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="4f812-303">Si después usa una clase de modelo con una propiedad `int` que no acepta valores NULL para ese campo, obtendrá `JsonSerializationException` así al intentar recuperar documentos:</span><span class="sxs-lookup"><span data-stu-id="4f812-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="4f812-304">Por este motivo, recomendamos utilizar tipos que aceptan valores null en las clases de modelo como procedimiento recomendado.</span><span class="sxs-lookup"><span data-stu-id="4f812-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="4f812-305">Para más detalles sobre este error y la corrección, vea [este problema en GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="4f812-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

