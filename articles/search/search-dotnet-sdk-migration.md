---
title: "aaaUpgrading toohello versión 1.1 del SDK de .NET de búsqueda de Azure | Documentos de Microsoft"
description: "Actualizar toohello versión 1.1 del SDK de .NET de búsqueda de Azure"
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
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="899d1-103">Actualizar toohello .NET de búsqueda de Azure SDK versión 3</span><span class="sxs-lookup"><span data-stu-id="899d1-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="899d1-104">Si está utilizando la versión preview de 2.0 o anterior de hello [SDK de .NET de búsqueda de Azure](https://aka.ms/search-sdk), este artículo le ayudará a actualizar la versión de toouse aplicación 3.</span><span class="sxs-lookup"><span data-stu-id="899d1-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="899d1-105">Para ver un tutorial más general de hello SDK incluidos ejemplos, vea [cómo toouse Azure buscar desde una aplicación .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="899d1-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="899d1-106">Versión 3 de hello SDK de .NET de búsqueda de Azure contiene algunos cambios de versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="899d1-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="899d1-107">La mayoría son de menor importancia, por lo que cambiar el código solo precisará del mínimo esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="899d1-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="899d1-108">Vea [tooupgrade pasos](#UpgradeSteps) para obtener instrucciones sobre cómo toochange su código toouse Hola nueva versión del SDK.</span><span class="sxs-lookup"><span data-stu-id="899d1-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="899d1-109">Si está usando la versión 1.0.2-preview o anterior, debe actualizar tooversion 1.1 en primer lugar y, a continuación, actualizar tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="899d1-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="899d1-110">Vea [Apéndice: pasos tooupgrade tooversion 1.1](#UpgradeStepsV1) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="899d1-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="899d1-111">La instancia de servicio de búsqueda de Azure es compatible con varias versiones de API de REST, incluidas hello más reciente.</span><span class="sxs-lookup"><span data-stu-id="899d1-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="899d1-112">Puede continuar toouse una versión cuando ya no es Hola más reciente, pero se recomienda que migre la versión más reciente de código toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="899d1-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="899d1-113">Cuando se utiliza la API de REST de Hola, debe especificar versión de API de hello en cada solicitud realizada a través del parámetro de versión de la api de Hola.</span><span class="sxs-lookup"><span data-stu-id="899d1-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="899d1-114">Cuando se usa Hola .NET SDK, versión de Hola de hello SDK usa determina versión correspondiente de Hola de hello API de REST.</span><span class="sxs-lookup"><span data-stu-id="899d1-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="899d1-115">Si usas un SDK anterior, puede continuar toorun ese código sin cambios aunque servicio hello es la versión de toosupport actualizada una API más recientes.</span><span class="sxs-lookup"><span data-stu-id="899d1-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="899d1-116">Novedades de la versión 3</span><span class="sxs-lookup"><span data-stu-id="899d1-116">What's new in version 3</span></span>
<span data-ttu-id="899d1-117">Versión 3 de Hola de destinos de SDK de .NET de búsqueda de Azure de hello última versión disponible con carácter general de hello API de REST de búsqueda de Azure, específicamente 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="899d1-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="899d1-118">Esto hace posible toouse muchas características nuevas de búsqueda de Azure desde una aplicación. NET, incluidos Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="899d1-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="899d1-119">Analizadores personalizados</span><span class="sxs-lookup"><span data-stu-id="899d1-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="899d1-120">Compatibilidad del indexador de [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) y [Azure Table Storage](search-howto-indexing-azure-tables.md)</span><span class="sxs-lookup"><span data-stu-id="899d1-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="899d1-121">Personalización de indizador mediante [asignaciones de campos](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="899d1-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="899d1-122">ETags admite la actualización simultánea seguro tooenable de orígenes de datos, los indizadores y las definiciones de índice</span><span class="sxs-lookup"><span data-stu-id="899d1-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="899d1-123">Compatibilidad para generar definiciones de campo de índice mediante declaración al decorar la clase de modelo y con hello nuevo `FieldBuilder` clase.</span><span class="sxs-lookup"><span data-stu-id="899d1-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="899d1-124">Compatibilidad con .NET Core y .NET Portable Profile 111</span><span class="sxs-lookup"><span data-stu-id="899d1-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="899d1-125">Tooupgrade de pasos</span><span class="sxs-lookup"><span data-stu-id="899d1-125">Steps tooupgrade</span></span>
<span data-ttu-id="899d1-126">En primer lugar, actualice la referencia de NuGet para `Microsoft.Azure.Search` utilizando cualquier consola de administrador de paquetes de NuGet de Hola o por el botón secundario en las referencias del proyecto y seleccione "Administrar... de paquetes de NuGet" en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="899d1-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="899d1-127">Una vez que haya descargado NuGet Hola nuevos paquetes y sus dependencias, recompile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="899d1-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="899d1-128">Dependiendo de cómo se estructura el código, se podrá volver a compilar correctamente.</span><span class="sxs-lookup"><span data-stu-id="899d1-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="899d1-129">Si es así, está listo toogo.</span><span class="sxs-lookup"><span data-stu-id="899d1-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="899d1-130">Si se produce un error en la compilación, verá un error de compilación como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="899d1-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="899d1-131">paso siguiente Hello es toofix este error de compilación.</span><span class="sxs-lookup"><span data-stu-id="899d1-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="899d1-132">Vea [cambios importantes en la versión 3](#ListOfChanges) para obtener más información acerca de las causas de error de Hola y cómo toofix lo.</span><span class="sxs-lookup"><span data-stu-id="899d1-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="899d1-133">Es posible que vea compilación adicionales relacionados con advertencias tooobsolete métodos o propiedades.</span><span class="sxs-lookup"><span data-stu-id="899d1-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="899d1-134">advertencias de Hola incluyen instrucciones sobre qué toouse en su lugar de hello característica en desuso.</span><span class="sxs-lookup"><span data-stu-id="899d1-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="899d1-135">Por ejemplo, si la aplicación utiliza hello `IndexingParameters.Base64EncodeKeys` propiedad, recibirá una advertencia que indica que`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="899d1-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="899d1-136">Una vez que haya solucionado los errores de compilación, puede realizar cambios tooyour aplicación tootake aprovechar las nuevas funcionalidades si lo desea.</span><span class="sxs-lookup"><span data-stu-id="899d1-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="899d1-137">Nuevas características de hello SDK se detallan en [cuáles son las novedades en la versión 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="899d1-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="899d1-138">Cambios importantes en la versión 3</span><span class="sxs-lookup"><span data-stu-id="899d1-138">Breaking changes in version 3</span></span>
<span data-ttu-id="899d1-139">No existe un número reducido de cambios importantes en la versión 3 que requieran código cambia además toorebuilding la aplicación.</span><span class="sxs-lookup"><span data-stu-id="899d1-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="899d1-140">Tipo de valor devuelto de Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="899d1-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="899d1-141">Hola `Indexes.GetClient` método tiene un nuevo tipo de valor devuelto.</span><span class="sxs-lookup"><span data-stu-id="899d1-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="899d1-142">Anteriormente devolvía `SearchIndexClient`, pero esto se cambió demasiado`ISearchIndexClient` en vista previa versión 2.0 lo que conlleva cambios sobre tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="899d1-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="899d1-143">Se trata de los clientes de toosupport que desea toomock hello `GetClient` método para las pruebas unitarias mediante la devolución de una implementación ficticia del `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="899d1-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="899d1-144">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="899d1-144">Example</span></span>
<span data-ttu-id="899d1-145">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="899d1-146">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="899d1-147">AnalyzerName, tipo de datos u otros datos ya no son toostrings implícitamente convertibles</span><span class="sxs-lookup"><span data-stu-id="899d1-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="899d1-148">Hay muchos tipos de hello SDK de .NET de búsqueda de Azure que derivan de `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="899d1-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="899d1-149">Anteriormente, estos tipos eran tootype convertirse implícitamente todos los `string`.</span><span class="sxs-lookup"><span data-stu-id="899d1-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="899d1-150">Sin embargo, se ha detectado un error en hello `Object.Equals` implementación de estas clases y corregir errores de hello necesario deshabilitar esta conversión implícita.</span><span class="sxs-lookup"><span data-stu-id="899d1-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="899d1-151">Conversión explícita demasiado`string` todavía se permiten.</span><span class="sxs-lookup"><span data-stu-id="899d1-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="899d1-152">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="899d1-152">Example</span></span>
<span data-ttu-id="899d1-153">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-153">If your code looks like this:</span></span>

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

<span data-ttu-id="899d1-154">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-154">You can change it toothis toofix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="899d1-155">Miembros obsoletos quitados</span><span class="sxs-lookup"><span data-stu-id="899d1-155">Removed obsolete members</span></span>

<span data-ttu-id="899d1-156">Puede que vea toomethods relacionados de errores de compilación o propiedades que se han marcado como obsoleto en la versión 2.0-vista previa y posteriormente, se elimina con la versión 3.</span><span class="sxs-lookup"><span data-stu-id="899d1-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="899d1-157">Si se producen estos errores, mostramos cómo tooresolve ellos:</span><span class="sxs-lookup"><span data-stu-id="899d1-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="899d1-158">Si usaba este constructor: `ScoringParameter(string name, string value)`, utilice en su lugar este: `ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="899d1-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="899d1-159">Si usaba hello `ScoringParameter.Value` propiedad, utilice hello `ScoringParameter.Values` propiedad o hello `ToString` método en su lugar.</span><span class="sxs-lookup"><span data-stu-id="899d1-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="899d1-160">Si usaba hello `SearchRequestOptions.RequestId` propiedad, utilice hello `ClientRequestId` propiedad en su lugar.</span><span class="sxs-lookup"><span data-stu-id="899d1-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="899d1-161">Características quitadas de la versión preliminar</span><span class="sxs-lookup"><span data-stu-id="899d1-161">Removed preview features</span></span>

<span data-ttu-id="899d1-162">Si va a actualizar desde la versión 2.0-versión preliminar tooversion 3, tenga en cuenta que JSON y análisis de compatibilidad para los indizadores de Blob CSV se ha quitado ya que estas características están aún en la vista previa.</span><span class="sxs-lookup"><span data-stu-id="899d1-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="899d1-163">En concreto, Hola siguiendo métodos de hello `IndexingParametersExtensions` clase se han quitado:</span><span class="sxs-lookup"><span data-stu-id="899d1-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="899d1-164">Si la aplicación tiene una dependencia fuerte acerca de estas características, no será capaz de tooupgrade tooversion 3 de hello SDK de .NET de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="899d1-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="899d1-165">Puede continuar toouse versión 2.0-vista previa.</span><span class="sxs-lookup"><span data-stu-id="899d1-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="899d1-166">Sin embargo, tenga en cuenta que **no se recomienda usar SDK de versión preliminar en aplicaciones de producción**.</span><span class="sxs-lookup"><span data-stu-id="899d1-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="899d1-167">Las características de versión preliminar son solo para evaluación y pueden cambiar.</span><span class="sxs-lookup"><span data-stu-id="899d1-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="899d1-168">Conclusión</span><span class="sxs-lookup"><span data-stu-id="899d1-168">Conclusion</span></span>
<span data-ttu-id="899d1-169">Si necesita más detalles sobre el uso de hello SDK de .NET de búsqueda de Azure, consulte nuestro actualizados recientemente [procedimientos](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="899d1-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="899d1-170">Le agradecemos sus comentarios en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="899d1-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="899d1-171">Si tiene problemas, puede tooask libre nos para obtener ayuda sobre hello [foro de MSDN de búsqueda de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="899d1-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="899d1-172">Si encuentra un error, puede registrar un problema en hello [repositorio de GitHub de SDK de Azure .NET](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="899d1-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="899d1-173">Asegúrese de que tooprefix el título del problema con "SDK de búsqueda:".</span><span class="sxs-lookup"><span data-stu-id="899d1-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="899d1-174">Gracias por usar Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="899d1-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="899d1-175">Apéndice: Pasos tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="899d1-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="899d1-176">En esta sección se aplica solo toousers de hello .NET de búsqueda de Azure SDK versión 1.0.2-preview y anteriores.</span><span class="sxs-lookup"><span data-stu-id="899d1-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="899d1-177">En primer lugar, actualice la referencia de NuGet para `Microsoft.Azure.Search` utilizando cualquier consola de administrador de paquetes de NuGet de Hola o por el botón secundario en las referencias del proyecto y seleccione "Administrar... de paquetes de NuGet" en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="899d1-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="899d1-178">Una vez que haya descargado NuGet Hola nuevos paquetes y sus dependencias, recompile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="899d1-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="899d1-179">Si estuviera previamente mediante versión 1.0.0-preview, 1.0.1-preview o 1.0.2-preview, compilación Hola debe ejecutarse correctamente y está listo toogo!</span><span class="sxs-lookup"><span data-stu-id="899d1-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="899d1-180">Si antes usaba versión 0.13.0-preview o anterior, verá errores como Hola siguiente compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="899d1-181">Hola siguiente paso es errores de compilación de hello toofix uno por uno.</span><span class="sxs-lookup"><span data-stu-id="899d1-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="899d1-182">La mayor parte requerirán cambiar algunos nombres de clase y método cuyo nombre ha cambiado en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="899d1-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="899d1-183">[lista de cambios importantes de la versión 1.1](#ListOfChangesV1) contiene una lista de estos cambios de nombre.</span><span class="sxs-lookup"><span data-stu-id="899d1-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="899d1-184">Si usa las clases personalizadas toomodel los documentos y las clases tienen propiedades de tipos primitivos que no aceptan valores null (por ejemplo, `int` o `bool` en C#), hay una corrección de errores en la versión de Hola 1.1 del SDK de Hola de los cuales debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="899d1-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="899d1-185">Para obtener más información, consulte la sección [Correcciones de errores en la versión 1.1](#BugFixesV1) .</span><span class="sxs-lookup"><span data-stu-id="899d1-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="899d1-186">Por último, una vez que haya solucionado los errores de compilación, puede realizar cambios tooyour aplicación tootake aprovechar las nuevas funcionalidades si lo desea.</span><span class="sxs-lookup"><span data-stu-id="899d1-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="899d1-187">lista de cambios importantes de la versión 1.1</span><span class="sxs-lookup"><span data-stu-id="899d1-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="899d1-188">Hello siguiente lista se ordena por probabilidad de Hola que cambio de hello afectará el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="899d1-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="899d1-189">Cambios de IndexBatch e IndexAction</span><span class="sxs-lookup"><span data-stu-id="899d1-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="899d1-190">`IndexBatch.Create`se ha cambiado el nombre demasiado`IndexBatch.New` y ya no tiene un `params` argumento.</span><span class="sxs-lookup"><span data-stu-id="899d1-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="899d1-191">Puede usar `IndexBatch.New` para los lotes que mezclan distintos tipos de acciones (combinaciones, eliminaciones, etc.).</span><span class="sxs-lookup"><span data-stu-id="899d1-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="899d1-192">Además, existen nuevos métodos estáticos para crear lotes donde todas las acciones de Hola se Hola igual: `Delete`, `Merge`, `MergeOrUpload`, y `Upload`.</span><span class="sxs-lookup"><span data-stu-id="899d1-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="899d1-193">`IndexAction` ya no tiene constructores públicos y sus propiedades ahora son inmutables.</span><span class="sxs-lookup"><span data-stu-id="899d1-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="899d1-194">Debe usar métodos estáticos de hello nueva para la creación de acciones para propósitos diferentes: `Delete`, `Merge`, `MergeOrUpload`, y `Upload`.</span><span class="sxs-lookup"><span data-stu-id="899d1-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="899d1-195">`IndexAction.Create` se ha quitado.</span><span class="sxs-lookup"><span data-stu-id="899d1-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="899d1-196">Si utiliza la sobrecarga de Hola que toma solo un documento, asegúrese de toouse seguro `Upload` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="899d1-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="899d1-197">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="899d1-197">Example</span></span>
<span data-ttu-id="899d1-198">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="899d1-199">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="899d1-200">Si lo desea, se puede simplificar aún más lo toothis:</span><span class="sxs-lookup"><span data-stu-id="899d1-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="899d1-201">Cambios de IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="899d1-201">IndexBatchException changes</span></span>
<span data-ttu-id="899d1-202">Hola `IndexBatchException.IndexResponse` propiedad ha cambiado de nombre demasiado`IndexingResults`, y su tipo es ahora `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="899d1-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="899d1-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="899d1-203">Example</span></span>
<span data-ttu-id="899d1-204">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="899d1-205">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="899d1-206">Cambios del método de operación</span><span class="sxs-lookup"><span data-stu-id="899d1-206">Operation method changes</span></span>
<span data-ttu-id="899d1-207">Cada operación de hello SDK de .NET de búsqueda de Azure se expone como un conjunto de sobrecargas de método para los autores de llamadas sincrónicas y asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="899d1-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="899d1-208">Hello las firmas y la factorización de estas sobrecargas de método ha cambiado en la versión 1.1.</span><span class="sxs-lookup"><span data-stu-id="899d1-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="899d1-209">Por ejemplo, hello operación "Obtener estadísticas de índices" en versiones anteriores de hello SDK expone estas firmas:</span><span class="sxs-lookup"><span data-stu-id="899d1-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="899d1-210">En `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="899d1-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="899d1-211">En `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="899d1-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="899d1-212">firmas de métodos de Hola Hola misma operación en la versión 1.1 este aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="899d1-213">En `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="899d1-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="899d1-214">En `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="899d1-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="899d1-215">A partir de la versión 1.1, Hola SDK de .NET de búsqueda de Azure organiza métodos de operación de manera diferente:</span><span class="sxs-lookup"><span data-stu-id="899d1-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="899d1-216">Los parámetros opcionales ahora se modelan como predeterminados en lugar de como sobrecargas de método adicionales.</span><span class="sxs-lookup"><span data-stu-id="899d1-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="899d1-217">Esto reduce número Hola de sobrecargas del método, en ocasiones drásticamente.</span><span class="sxs-lookup"><span data-stu-id="899d1-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="899d1-218">métodos de extensión de Hello ocultan ahora muchos detalles extraños Hola de HTTP desde el llamador de Hola.</span><span class="sxs-lookup"><span data-stu-id="899d1-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="899d1-219">Por ejemplo, las versiones anteriores de hello SDK devuelve un objeto de respuesta con un código de estado HTTP, que a menudo no necesitan toocheck debido a que los métodos de operación producen `CloudException` para cualquier código de estado que indica un error.</span><span class="sxs-lookup"><span data-stu-id="899d1-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="899d1-220">Hola nuevos objetos del modelo de valor devuelto de métodos de extensión, ahorrar Hola problema de tener toounwrap ellas en el código.</span><span class="sxs-lookup"><span data-stu-id="899d1-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="899d1-221">Por el contrario, hello interfaces principales ahora exponen métodos que ofrecen un mayor control en el nivel de hello HTTP si lo necesita.</span><span class="sxs-lookup"><span data-stu-id="899d1-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="899d1-222">Ahora puede pasar en toobe de encabezados HTTP personalizado incluido en las solicitudes y Hola nueva `AzureOperationResponse<T>` devolver tipo da acceso directo toohello `HttpRequestMessage` y `HttpResponseMessage` para la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="899d1-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="899d1-223">`AzureOperationResponse`se define en hello `Microsoft.Rest.Azure` espacio de nombres y reemplaza `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="899d1-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="899d1-224">Cambios de ScoringParameters</span><span class="sxs-lookup"><span data-stu-id="899d1-224">ScoringParameters changes</span></span>
<span data-ttu-id="899d1-225">Una nueva clase denominada `ScoringParameter` ha sido agregado en hello toomake SDK más reciente sea más fácil tooprovide parámetros tooscoring los perfiles en una consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="899d1-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="899d1-226">Hola anteriormente `ScoringProfiles` propiedad de hello `SearchParameters` clase se ha escrito como `IList<string>`; Ahora se ha escrito como `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="899d1-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="899d1-227">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="899d1-227">Example</span></span>
<span data-ttu-id="899d1-228">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="899d1-229">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="899d1-230">Cambios de la clase de modelo</span><span class="sxs-lookup"><span data-stu-id="899d1-230">Model class changes</span></span>
<span data-ttu-id="899d1-231">Debido a cambios de firma de toohello descritos en [cambios de método de operación](#OperationMethodChanges), muchas clases de hello `Microsoft.Azure.Search.Models` espacio de nombres se han cambiado de nombre o eliminado.</span><span class="sxs-lookup"><span data-stu-id="899d1-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="899d1-232">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="899d1-232">For example:</span></span>

* <span data-ttu-id="899d1-233">`IndexDefinitionResponse` se ha reemplazado por `AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="899d1-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="899d1-234">`DocumentSearchResponse`se ha cambiado el nombre demasiado`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="899d1-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="899d1-235">`IndexResult`se ha cambiado el nombre demasiado`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="899d1-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="899d1-236">`Documents.Count()`ahora devuelve un `long` con recuento de documentos de hello en lugar de un`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="899d1-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="899d1-237">`IndexGetStatisticsResponse`se ha cambiado el nombre demasiado`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="899d1-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="899d1-238">`IndexListResponse`se ha cambiado el nombre demasiado`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="899d1-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="899d1-239">toosummarize, `OperationResponse`-las clases derivadas que existían solo toowrap un objeto de modelo se han quitado.</span><span class="sxs-lookup"><span data-stu-id="899d1-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="899d1-240">Hello clases restantes han tenido su sufijo cambió de `Response` demasiado`Result`.</span><span class="sxs-lookup"><span data-stu-id="899d1-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="899d1-241">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="899d1-241">Example</span></span>
<span data-ttu-id="899d1-242">Si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-242">If your code looks like this:</span></span>

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

<span data-ttu-id="899d1-243">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-243">You can change it toothis toofix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="899d1-244">Clases de respuesta e IEnumerable</span><span class="sxs-lookup"><span data-stu-id="899d1-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="899d1-245">Un cambio adicional que puede afectar a su código es que las clases de respuesta que contienen colecciones ya no implementan `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="899d1-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="899d1-246">En su lugar, puede tener acceso la propiedad de colección Hola directamente.</span><span class="sxs-lookup"><span data-stu-id="899d1-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="899d1-247">Por ejemplo, si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="899d1-248">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="899d1-249">Caso especial para aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="899d1-249">Special case for web applications</span></span>
<span data-ttu-id="899d1-250">Si tiene una aplicación web que serializa `DocumentSearchResponse` directamente los resultados de búsqueda de toosend toohello explorador, deberá toochange el código o los resultados de hello no serializará correctamente.</span><span class="sxs-lookup"><span data-stu-id="899d1-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="899d1-251">Por ejemplo, si el código tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="899d1-252">Puede cambiarlo obteniendo hello `.Results` propiedad de la representación de resultados de búsqueda de hello búsqueda respuesta toofix:</span><span class="sxs-lookup"><span data-stu-id="899d1-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="899d1-253">Habrá toolook para estos casos en el código por sí mismo; **compilador hello no le avisará** porque `JsonResult.Data` es de tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="899d1-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="899d1-254">Cambios de CloudException</span><span class="sxs-lookup"><span data-stu-id="899d1-254">CloudException changes</span></span>
<span data-ttu-id="899d1-255">Hola `CloudException` clase ha pasado de hello `Hyak.Common` toohello de espacio de nombres `Microsoft.Rest.Azure` espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="899d1-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="899d1-256">Además, su `Error` propiedad ha cambiado de nombre demasiado`Body`.</span><span class="sxs-lookup"><span data-stu-id="899d1-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="899d1-257">Cambios de SearchServiceClient y SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="899d1-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="899d1-258">Hola tipo de hello `Credentials` propiedad ha cambiado respecto de `SearchCredentials` tooits de la clase base `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="899d1-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="899d1-259">Si necesita hello tooaccess `SearchCredentials` de un `SearchIndexClient` o `SearchServiceClient`, use Hola nuevo `SearchCredentials` propiedad.</span><span class="sxs-lookup"><span data-stu-id="899d1-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="899d1-260">En versiones anteriores de hello SDK, `SearchServiceClient` y `SearchIndexClient` tenía constructores que tuvieron un `HttpClient` parámetro.</span><span class="sxs-lookup"><span data-stu-id="899d1-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="899d1-261">Estos se han reemplazado con constructores que obtienen `HttpClientHandler` y una matriz de objetos `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="899d1-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="899d1-262">Esto hace más fácil tooinstall controladores personalizados toopre proceso las solicitudes HTTP si es necesario.</span><span class="sxs-lookup"><span data-stu-id="899d1-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="899d1-263">Por último, Hola constructores que tardan una `Uri` y `SearchCredentials` han cambiado.</span><span class="sxs-lookup"><span data-stu-id="899d1-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="899d1-264">Por ejemplo, si tiene código con este aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="899d1-265">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="899d1-266">También tenga en cuenta que el tipo hello de hello credenciales parámetro ha cambiado demasiado`ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="899d1-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="899d1-267">Esto es improbable tooaffect su código desde `SearchCredentials` se deriva de `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="899d1-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="899d1-268">Transferir un identificador de solicitud</span><span class="sxs-lookup"><span data-stu-id="899d1-268">Passing a request ID</span></span>
<span data-ttu-id="899d1-269">En versiones anteriores de hello SDK, puede establecer un identificador de solicitud en hello `SearchServiceClient` o `SearchIndexClient` y se incluiría en cada toohello de solicitud API de REST.</span><span class="sxs-lookup"><span data-stu-id="899d1-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="899d1-270">Esto es útil para solucionar problemas con el servicio de búsqueda si necesita compatibilidad con toocontact.</span><span class="sxs-lookup"><span data-stu-id="899d1-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="899d1-271">Sin embargo, resulta más útil tooset un identificador único de la solicitud para cada operación en lugar de toouse Hola mismo identificador para todas las operaciones.</span><span class="sxs-lookup"><span data-stu-id="899d1-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="899d1-272">Por esta razón, Hola `SetClientRequestId` métodos de `SearchServiceClient` y `SearchIndexClient` se han quitado.</span><span class="sxs-lookup"><span data-stu-id="899d1-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="899d1-273">En su lugar, puede pasar un método de operación de tooeach de Id. de solicitud a través de hello opcional `SearchRequestOptions` parámetro.</span><span class="sxs-lookup"><span data-stu-id="899d1-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="899d1-274">En una futura versión de SDK de hello, agregaremos un nuevo mecanismo para establecer un identificador de solicitud global en el cliente de hello objetos que es coherente con el enfoque de hello utilizado por otros SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="899d1-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="899d1-275">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="899d1-275">Example</span></span>
<span data-ttu-id="899d1-276">Si tiene código con este aspecto:</span><span class="sxs-lookup"><span data-stu-id="899d1-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="899d1-277">Se puede cambiar toothis toofix cualquier error de compilación:</span><span class="sxs-lookup"><span data-stu-id="899d1-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="899d1-278">Cambios de nombre de interfaz</span><span class="sxs-lookup"><span data-stu-id="899d1-278">Interface name changes</span></span>
<span data-ttu-id="899d1-279">nombres de interfaz de Hello operación grupo tienen todos los toobe modificados coherente con sus nombres de propiedad correspondientes:</span><span class="sxs-lookup"><span data-stu-id="899d1-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="899d1-280">Hola tipo de `ISearchServiceClient.Indexes` se ha cambiado de `IIndexOperations` demasiado`IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="899d1-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="899d1-281">Hola tipo de `ISearchServiceClient.Indexers` se ha cambiado de `IIndexerOperations` demasiado`IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="899d1-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="899d1-282">Hola tipo de `ISearchServiceClient.DataSources` se ha cambiado de `IDataSourceOperations` demasiado`IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="899d1-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="899d1-283">Hola tipo de `ISearchIndexClient.Documents` se ha cambiado de `IDocumentOperations` demasiado`IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="899d1-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="899d1-284">Este cambio es poco probable que tooaffect su código a menos que cree las simulaciones de estas interfaces para fines de prueba.</span><span class="sxs-lookup"><span data-stu-id="899d1-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="899d1-285">Correcciones de errores en la versión 1.1</span><span class="sxs-lookup"><span data-stu-id="899d1-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="899d1-286">Se produjo un error en las versiones anteriores de hello SDK de .NET de búsqueda de Azure relacionado tooserialization de clases de modelos personalizados.</span><span class="sxs-lookup"><span data-stu-id="899d1-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="899d1-287">Error de Hello puede producirse si ha creado una clase de modelo personalizado con una propiedad de un tipo de valor no acepta valores NULL.</span><span class="sxs-lookup"><span data-stu-id="899d1-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="899d1-288">Tooreproduce de pasos</span><span class="sxs-lookup"><span data-stu-id="899d1-288">Steps tooreproduce</span></span>
<span data-ttu-id="899d1-289">Cree una clase de modelo personalizado con una propiedad de tipo de valor que no acepta valores NULL.</span><span class="sxs-lookup"><span data-stu-id="899d1-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="899d1-290">Por ejemplo, agregue una propiedad `UnitCount` pública de tipo `int` en lugar de `int?`.</span><span class="sxs-lookup"><span data-stu-id="899d1-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="899d1-291">Si se puede indizar un documento con el valor predeterminado de Hola de ese tipo (por ejemplo, 0 para `int`), campo Hola será null en la búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="899d1-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="899d1-292">Si posteriormente desea buscar ese documento, Hola `Search` llamada producirá `JsonSerializationException` quejan de que no se puede convertir `null` demasiado`int`.</span><span class="sxs-lookup"><span data-stu-id="899d1-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="899d1-293">Además, los filtros no funcionen según lo esperado desde que null se escribió toohello índice en lugar de valor de hello diseñado.</span><span class="sxs-lookup"><span data-stu-id="899d1-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="899d1-294">Detalles de corrección</span><span class="sxs-lookup"><span data-stu-id="899d1-294">Fix details</span></span>
<span data-ttu-id="899d1-295">Este problema se ha corregido en la versión 1.1 de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="899d1-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="899d1-296">Ahora, si tiene una clase de modelo similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="899d1-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="899d1-297">y establece `IntValue` too0, que valor es ahora correctamente serializado como 0 en el cable de Hola y almacenado como 0 en el índice de Hola.</span><span class="sxs-lookup"><span data-stu-id="899d1-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="899d1-298">El recorrido de ida y vuelta también funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="899d1-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="899d1-299">Hay un toobe problema potencial en cuenta con este enfoque: si usa un tipo de modelo con una propiedad que no acepta valores NULL, tienen también**garantizar** ningún documentos en el índice que contienen un valor nulo para el campo correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="899d1-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="899d1-300">Hola SDK ni Hola API de REST de búsqueda de Azure le ayudará a tooenforce esto.</span><span class="sxs-lookup"><span data-stu-id="899d1-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="899d1-301">Esto no es simplemente un problema hipotético: Imagine un escenario donde agrega un nuevo índice existente de campo tooan que es de tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="899d1-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="899d1-302">Después de actualizar la definición del índice hello, todos los documentos tendrá un valor null para ese campo nuevo (ya que todos los tipos admiten valores NULL en la búsqueda de Azure).</span><span class="sxs-lookup"><span data-stu-id="899d1-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="899d1-303">Si, a continuación, usa una clase de modelo con un acepta valores NULL `int` propiedad para ese campo, obtendrá un `JsonSerializationException` similar a éste al tratar de tooretrieve documentos:</span><span class="sxs-lookup"><span data-stu-id="899d1-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="899d1-304">Por este motivo, recomendamos utilizar tipos que aceptan valores null en las clases de modelo como procedimiento recomendado.</span><span class="sxs-lookup"><span data-stu-id="899d1-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="899d1-305">Para obtener más detalles sobre esta corrección hello y errores, vea [este problema en GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="899d1-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

