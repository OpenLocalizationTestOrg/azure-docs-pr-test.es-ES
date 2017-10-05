---
title: "Notas de la versión de SDK de Azure para .NET 2.9"
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
ms.openlocfilehash: 199f0906f73d693d7cd4b73c928f23ae83b99596
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="3e702-103">Notas de la versión de SDK de Azure para .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="3e702-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="3e702-104">Este tema incluye notas de la versión para las versiones 2.9 y 2.9.6 del SDK de Azure para. NET.</span><span class="sxs-lookup"><span data-stu-id="3e702-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="3e702-105">Resumen de la versión de SDK de Azure para .NET 2.9.6.</span><span class="sxs-lookup"><span data-stu-id="3e702-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="3e702-106">Fecha de lanzamiento: 16/11/2016</span><span class="sxs-lookup"><span data-stu-id="3e702-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="3e702-107">En esta versión no se han hecho cambios importantes en el SDK de Azure 2.9.</span><span class="sxs-lookup"><span data-stu-id="3e702-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="3e702-108">Tampoco es necesario ningún proceso de actualización para aprovechar este SDK con proyectos de Cloud Services existentes.</span><span class="sxs-lookup"><span data-stu-id="3e702-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="3e702-109">Versión candidata para lanzamiento de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3e702-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="3e702-110">En Visual Studio de 2017 RC, esta versión del SDK de Azure para .NET se basa en la carga de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e702-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="3e702-111">Todas las herramientas que necesita para que el desarrollo de Azure forme parte de Visual Studio de 2017 RC y las versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="3e702-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="3e702-112">Para Visual Studio 2015 y Visual Studio 2013, el SDK estará disponible a través de WebPI.</span><span class="sxs-lookup"><span data-stu-id="3e702-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="3e702-113">Cuando la versión de Visual Studio 2017 sea definitiva, se interrumpirán las versiones del SDK de Azure para .NET para Visual Studio 2013l.</span><span class="sxs-lookup"><span data-stu-id="3e702-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="3e702-114">Siga este vínculo para descargar Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="3e702-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="3e702-115">Diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="3e702-115">Azure Diagnostics</span></span>

- <span data-ttu-id="3e702-116">Ha cambiado el comportamiento para almacenar solo una cadena de conexión parcial con la clave sustituida por un token de cadena de conexión de almacenamiento de diagnóstico de Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="3e702-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="3e702-117">La clave de almacenamiento real ahora se almacena en la carpeta del perfil de usuario para poder controlar el acceso.</span><span class="sxs-lookup"><span data-stu-id="3e702-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="3e702-118">Visual Studio leerá la clave de almacenamiento de la carpeta del perfil de usuario para los procesos de publicación y depuración local.</span><span class="sxs-lookup"><span data-stu-id="3e702-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="3e702-119">En respuesta al cambio descrito anteriormente, el equipo de Visual Studio Online ha mejorado la plantilla de tareas de implementación de Azure Cloud Services para que los usuarios puedan especificar la clave de almacenamiento para configurar la extensión de diagnósticos al publicar en Azure en la integración e implementación continuas.</span><span class="sxs-lookup"><span data-stu-id="3e702-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="3e702-120">Ahora es posible almacenar la cadena de conexión segura y la tokenización para diagnósticos de Azure (WAD), para ayudarle a solucionar problemas con la configuración entre entornos.</span><span class="sxs-lookup"><span data-stu-id="3e702-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="3e702-121">Máquinas virtuales Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3e702-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="3e702-122">Visual Studio ahora admite la implementación de Cloud Services en máquinas virtuales con la familia del SO 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="3e702-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="3e702-123">Para servicios en la nube existentes, puede cambiar la configuración para la nueva familia del SO.</span><span class="sxs-lookup"><span data-stu-id="3e702-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="3e702-124">Al crear servicios en la nube, si decide crear el servicio con .Net 4.6 o posterior, el servicio usará la familia del SO 5 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3e702-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="3e702-125">Para más información, puede consultar la tabla de [compatibilidad de la familia del SO invitado](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="3e702-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="3e702-126">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="3e702-126">Known issues</span></span>

- <span data-ttu-id="3e702-127">El SDK de Azure .NET 2.9.6 introdujo una restricción que bloquea la implementación de proyectos con componentes .NET Framework no compatibles (por ejemplo, .NET 4.6) en cualquier familia del SO inferior a la 5.</span><span class="sxs-lookup"><span data-stu-id="3e702-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="3e702-128">Se proporciona una solución alternativa [aquí](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="3e702-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="3e702-129">Caché en rol de Azure</span><span class="sxs-lookup"><span data-stu-id="3e702-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="3e702-130">La compatibilidad con Azure In-Role Cache finaliza el 30 de noviembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="3e702-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="3e702-131">Para más detalles, haga clic [aquí](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="3e702-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="3e702-132">Plantillas de Azure Resource Manager para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3e702-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="3e702-133">Hemos introducido Azure Stack como un destino de implementación para las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3e702-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="3e702-134">Resumen del SDK de Azure para .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="3e702-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="3e702-135">Información general</span><span class="sxs-lookup"><span data-stu-id="3e702-135">Overview</span></span>
<span data-ttu-id="3e702-136">Este documento contiene las notas de la versión de SDK de Azure para la versión .NET 2.9.</span><span class="sxs-lookup"><span data-stu-id="3e702-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="3e702-137">Para obtener información detallada sobre las actualizaciones de esta publicación, consulte [Announcing the Visual Studio Azure Tools and SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)(Presentación de Visual Studio Azure Tools y el SDK 2.9).</span><span class="sxs-lookup"><span data-stu-id="3e702-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="3e702-138">SDK de Azure 2.9 para Visual Studio 2015 Update 2 y vista previa de Visual Studio "15"</span><span class="sxs-lookup"><span data-stu-id="3e702-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="3e702-139">Esta actualización incluye las correcciones de errores siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e702-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="3e702-140">Problema relacionado con la generación de clientes de la API de REST, en el que la cadena "Tipo desconocido" aparecía como nombre de la carpeta de generación de código o como nombre del espacio de nombres que se coloca en el código generado.</span><span class="sxs-lookup"><span data-stu-id="3e702-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="3e702-141">Problema relacionado con WebJobs programados, en el que la información de autenticación no se transfería al proceso de aprovisionamiento del programador.</span><span class="sxs-lookup"><span data-stu-id="3e702-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="3e702-142">Esta actualización incluye la siguiente característica nueva:</span><span class="sxs-lookup"><span data-stu-id="3e702-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="3e702-143">Compatibilidad con Servicios de aplicaciones secundarios en la pestaña "Servicios" del cuadro de diálogo de aprovisionamiento de Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3e702-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="3e702-144">Azure Data Lake Tools para Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="3e702-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="3e702-145">Esta actualización incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e702-145">This updates includes the following:</span></span>

* <span data-ttu-id="3e702-146">**Azure Data Lake Tools** para Visual Studio se ha combinado en el SDK de Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="3e702-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="3e702-147">La herramienta se instala automáticamente cuando se instala el SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e702-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="3e702-148">La herramienta se actualiza con frecuencia. Vaya [aquí](http://aka.ms/datalaketool) para obtener las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="3e702-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="3e702-149">**Explorador de servidores** ahora le permite verlo todo y crear algunas entidades de metadatos U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3e702-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="3e702-150">Para más información, consulte [este blog](https://azure.microsoft.com/documentation/services/data-lake-analytics/) .</span><span class="sxs-lookup"><span data-stu-id="3e702-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="3e702-151">Herramientas de HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e702-151">HDInsight Tools</span></span>
<span data-ttu-id="3e702-152">**Herramientas de HDInsight** para Visual Studio ahora admite HDInsight versión 3.3, incluida la visualización de gráficos Tez y otras correcciones de lenguaje.</span><span class="sxs-lookup"><span data-stu-id="3e702-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="3e702-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3e702-153">Azure Resource Manager</span></span>
<span data-ttu-id="3e702-154">Esta versión agrega compatibilidad de [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) con plantillas de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3e702-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="3e702-155">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3e702-155">See also</span></span>
[<span data-ttu-id="3e702-156">Announcing the Visual Studio Azure Tools and SDK 2.9</span><span class="sxs-lookup"><span data-stu-id="3e702-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

