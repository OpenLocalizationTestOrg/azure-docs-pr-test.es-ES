---
title: aaaAzure SDK para .NET 2.9 notas
description: "Notas de la versión de SDK de Azure para .NET 2.9"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="9387f-103">Notas de la versión de SDK de Azure para .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="9387f-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="9387f-104">Este tema incluye notas de la versión para las versiones 2.9 y 2.9.6 del SDK de Azure para. NET.</span><span class="sxs-lookup"><span data-stu-id="9387f-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="9387f-105">Resumen de la versión de SDK de Azure para .NET 2.9.6.</span><span class="sxs-lookup"><span data-stu-id="9387f-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="9387f-106">Fecha de lanzamiento: 16/11/2016</span><span class="sxs-lookup"><span data-stu-id="9387f-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="9387f-107">No hay toohello de cambios de separación de Azure SDK 2.9 se han introducido en esta versión.</span><span class="sxs-lookup"><span data-stu-id="9387f-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="9387f-108">No hay también ninguna tooleverage del proceso de actualización necesitado este SDK con proyectos de servicio en la nube existentes.</span><span class="sxs-lookup"><span data-stu-id="9387f-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="9387f-109">Versión candidata para lanzamiento de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9387f-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="9387f-110">En Visual Studio de 2017 RC, esta versión de hello Azure SDK para .NET se basa Hola cargas de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="9387f-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="9387f-111">Todas las herramientas de hello necesita toodo desarrollo de Azure va a formar parte de Visual Studio de 2017 RC en el futuro.</span><span class="sxs-lookup"><span data-stu-id="9387f-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="9387f-112">Para Visual Studio 2015 y Visual Studio 2013, Hola SDK estará disponible a través de WebPI.</span><span class="sxs-lookup"><span data-stu-id="9387f-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="9387f-113">Cuando la versión de Visual Studio 2017 sea definitiva, se interrumpirán las versiones del SDK de Azure para .NET para Visual Studio 2013l.</span><span class="sxs-lookup"><span data-stu-id="9387f-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="9387f-114">Siga este toodownload vínculo Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="9387f-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="9387f-115">Diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="9387f-115">Azure Diagnostics</span></span>

- <span data-ttu-id="9387f-116">Hola modificada comportamiento tooonly almacenar una cadena de conexión parcial con clave de hello reemplazado por un token de cadena de conexión de almacenamiento de información de diagnóstico de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="9387f-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="9387f-117">clave de almacenamiento real de Hola ahora se almacena en la carpeta de perfil de usuario de hello, por lo que se puede controlar el acceso.</span><span class="sxs-lookup"><span data-stu-id="9387f-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="9387f-118">Visual Studio leerá clave de almacenamiento de Hola de carpeta de perfil de usuario para la depuración local y el proceso de publicación.</span><span class="sxs-lookup"><span data-stu-id="9387f-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="9387f-119">En cambio toohello de respuesta se ha descrito anteriormente, Visual Studio Online team Hola mejorada plantilla de tarea de implementación de servicios de nube de Azure para que los usuarios especificar clave de almacenamiento de Hola para establecer la extensión de diagnóstico al publicar tooAzure de integración continua y la implementación.</span><span class="sxs-lookup"><span data-stu-id="9387f-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="9387f-120">Que hemos hecho posible toostore cadena de conexión segura y tokenización para diagnósticos de Azure (WAD), toohelp solucionar problemas con la configuración entre entornos.</span><span class="sxs-lookup"><span data-stu-id="9387f-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="9387f-121">Máquinas virtuales Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9387f-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="9387f-122">Visual Studio ahora admite la implementación de servicios en la nube de tooOS máquinas virtuales de familia 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="9387f-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="9387f-123">Para los servicios de nube existente, puede cambiar su configuración tootarget Hola nueva familia del SO.</span><span class="sxs-lookup"><span data-stu-id="9387f-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="9387f-124">Al crear nuevos servicios de nube, si decide que el servicio de hello toocreate mediante .net 4.6 o posterior, serán Hola servicio toouse 5 de la familia de SO.</span><span class="sxs-lookup"><span data-stu-id="9387f-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="9387f-125">Para obtener más información, puede revisar hello [familia del SO invitado compatible con la tabla](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="9387f-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9387f-126">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="9387f-126">Known issues</span></span>

- <span data-ttu-id="9387f-127">Azure SDK para .NET 2.9.6 introdujo una restricción que bloquea la implementación de proyectos mediante tooany de marcos de trabajo (por ejemplo, .NET 4.6) .NET familia del SO no compatible < 5.</span><span class="sxs-lookup"><span data-stu-id="9387f-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="9387f-128">Se proporciona una solución alternativa [aquí](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="9387f-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="9387f-129">Caché en rol de Azure</span><span class="sxs-lookup"><span data-stu-id="9387f-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="9387f-130">La compatibilidad con Azure In-Role Cache finaliza el 30 de noviembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="9387f-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="9387f-131">Para más detalles, haga clic [aquí](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="9387f-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="9387f-132">Plantillas de Azure Resource Manager para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9387f-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="9387f-133">Hemos introducido Azure Stack como un destino de implementación para las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9387f-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="9387f-134">Resumen del SDK de Azure para .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="9387f-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="9387f-135">Información general</span><span class="sxs-lookup"><span data-stu-id="9387f-135">Overview</span></span>
<span data-ttu-id="9387f-136">Este documento contiene notas de la versión de Hola para hello Azure SDK para la versión 2.9. NET.</span><span class="sxs-lookup"><span data-stu-id="9387f-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="9387f-137">Para obtener información detallada acerca de las actualizaciones en esta versión, vea hello [post de anuncio de Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="9387f-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="9387f-138">SDK de Azure 2.9 para Visual Studio 2015 Update 2 y vista previa de Visual Studio "15"</span><span class="sxs-lookup"><span data-stu-id="9387f-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="9387f-139">Esta actualización incluye Hola después de correcciones de errores:</span><span class="sxs-lookup"><span data-stu-id="9387f-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="9387f-140">Emitir relacionado tooREST generación de API de cliente en la cadena de Hola "Tipo desconocido" aparecería como nombre de Hola de carpeta de generación de código de hello u Hola del espacio de nombres de hello colocado en el código de hello generado.</span><span class="sxs-lookup"><span data-stu-id="9387f-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="9387f-141">Emitir WebJobs tooScheduled relacionados en qué Hola información de autenticación producía un error toobe pasado el proceso de aprovisionamiento de toohello programador.</span><span class="sxs-lookup"><span data-stu-id="9387f-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="9387f-142">Esta actualización incluye Hola siguiendo la nueva característica:</span><span class="sxs-lookup"><span data-stu-id="9387f-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="9387f-143">Compatibilidad con los servicios de aplicación secundarios en la ficha de "Servicios" hello de hello diálogo de aprovisionamiento del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9387f-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="9387f-144">Azure Data Lake Tools para Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="9387f-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="9387f-145">Esta actualización incluye siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="9387f-145">This updates includes hello following:</span></span>

* <span data-ttu-id="9387f-146">**Azure Data Lake Tools** para Visual Studio ahora se combinan en hello Azure SDK para la versión de .NET.</span><span class="sxs-lookup"><span data-stu-id="9387f-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="9387f-147">herramienta de Hola se instala automáticamente al instalar el SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="9387f-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="9387f-148">herramienta de Hola se actualiza con frecuencia, vaya [aquí](http://aka.ms/datalaketool) tooget Hola actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="9387f-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="9387f-149">**Explorador de servidores** ahora permite tooview todos y crear algunas entidades de metadatos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="9387f-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="9387f-150">Para más información, consulte [este blog](https://azure.microsoft.com/documentation/services/data-lake-analytics/) .</span><span class="sxs-lookup"><span data-stu-id="9387f-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="9387f-151">Herramientas de HDInsight</span><span class="sxs-lookup"><span data-stu-id="9387f-151">HDInsight Tools</span></span>
<span data-ttu-id="9387f-152">**Herramientas de HDInsight** para Visual Studio ahora admite HDInsight versión 3.3, incluida la visualización de gráficos Tez y otras correcciones de lenguaje.</span><span class="sxs-lookup"><span data-stu-id="9387f-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="9387f-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9387f-153">Azure Resource Manager</span></span>
<span data-ttu-id="9387f-154">Esta versión agrega compatibilidad de [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) con plantillas de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9387f-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="9387f-155">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9387f-155">See also</span></span>
[<span data-ttu-id="9387f-156">Announcing the Visual Studio Azure Tools and SDK 2.9</span><span class="sxs-lookup"><span data-stu-id="9387f-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

