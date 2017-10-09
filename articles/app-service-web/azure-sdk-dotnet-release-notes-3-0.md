---
title: SDK para .NET 3.0 notas aaaAzure | Documentos de Microsoft
description: "Notas de la versión de SDK de Azure para .NET 3.0"
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
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="17d44-103">Notas de la versión de SDK de Azure para .NET 3.0</span><span class="sxs-lookup"><span data-stu-id="17d44-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="17d44-104">Este tema incluye notas de la versión con la versión 3.0 de hello Azure SDK para. NET.</span><span class="sxs-lookup"><span data-stu-id="17d44-104">This topic includes release notes for version 3.0 of hello Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="17d44-105">Resumen de la versión de SDK de Azure para .NET 3.0</span><span class="sxs-lookup"><span data-stu-id="17d44-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="17d44-106">Fecha de lanzamiento: 07/03/2017</span><span class="sxs-lookup"><span data-stu-id="17d44-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="17d44-107">No toohello de cambios de separación de Azure SDK 3.0 se han introducido en esta versión.</span><span class="sxs-lookup"><span data-stu-id="17d44-107">No breaking changes toohello Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="17d44-108">No hay también ninguna tooleverage del proceso de actualización necesitado este SDK con proyectos de servicio en la nube existentes.</span><span class="sxs-lookup"><span data-stu-id="17d44-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="17d44-109">uso de tooallow de hello Azure SDK 3.0 sin necesidad de un proceso de actualización, Azure SDK 3.0 instala toohello mismos directorios que Azure SDK 2.9.</span><span class="sxs-lookup"><span data-stu-id="17d44-109">tooallow use of hello Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs toohello same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="17d44-110">Mayoría de los componentes de hello no ha cambiado la versión principal de Hola de 2.9 pero en su lugar acaba de actualizar número de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="17d44-110">Most hello components did not change hello major version from 2.9 but instead just updated hello build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="17d44-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="17d44-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="17d44-112">En Visual Studio de 2017, esta versión de hello Azure SDK para .NET se basa en toohello carga de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="17d44-112">In Visual Studio 2017, this release of hello Azure SDK for .NET is built in toohello Azure Workload.</span></span> <span data-ttu-id="17d44-113">Todas las herramientas de hello necesita toodo desarrollo de Azure va a formar parte de Visual Studio de 2017 en el futuro.</span><span class="sxs-lookup"><span data-stu-id="17d44-113">All hello tools you need toodo Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="17d44-114">Para Visual Studio 2015 Hola SDK estará disponible a través de WebPI.</span><span class="sxs-lookup"><span data-stu-id="17d44-114">For Visual Studio 2015 hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="17d44-115">Se ha suspendido el SDK de Azure para las versiones de .NET para Visual Studio 2013 ahora que se publicado Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="17d44-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="17d44-116">Diagnóstico de Azure</span><span class="sxs-lookup"><span data-stu-id="17d44-116">Azure Diagnostics</span></span>

- <span data-ttu-id="17d44-117">Hola modificada comportamiento tooonly almacenar una cadena de conexión parcial con clave de hello reemplazado por un token de cadena de conexión de almacenamiento de información de diagnóstico de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="17d44-117">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="17d44-118">clave de almacenamiento real de Hola ahora se almacena en la carpeta de perfil de usuario de hello, por lo que se puede controlar el acceso.</span><span class="sxs-lookup"><span data-stu-id="17d44-118">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="17d44-119">Visual Studio leerá clave de almacenamiento de Hola de carpeta de perfil de usuario para la depuración local y el proceso de publicación.</span><span class="sxs-lookup"><span data-stu-id="17d44-119">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="17d44-120">En cambio toohello de respuesta se ha descrito anteriormente, Visual Studio Online team Hola mejorada plantilla de tarea de implementación de servicios de nube de Azure para que los usuarios especificar clave de almacenamiento de Hola para establecer la extensión de diagnóstico al publicar tooAzure de integración continua y la implementación.</span><span class="sxs-lookup"><span data-stu-id="17d44-120">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="17d44-121">Que hemos hecho posible toostore cadena de conexión segura y tokenización para diagnósticos de Azure (WAD), toohelp solucionar problemas con la configuración entre entornos.</span><span class="sxs-lookup"><span data-stu-id="17d44-121">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="17d44-122">Máquinas virtuales Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="17d44-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="17d44-123">Visual Studio ahora admite la implementación de servicios en la nube de tooOS máquinas virtuales de familia 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="17d44-123">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="17d44-124">Para los servicios de nube existente, puede cambiar su configuración tootarget Hola nueva familia del SO.</span><span class="sxs-lookup"><span data-stu-id="17d44-124">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="17d44-125">Al crear nuevos servicios de nube, si decide que el servicio de hello toocreate mediante .net 4.6 o posterior, serán Hola servicio toouse 5 de la familia de SO.</span><span class="sxs-lookup"><span data-stu-id="17d44-125">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="17d44-126">Para obtener más información, puede revisar hello [familia del SO invitado compatible con la tabla](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="17d44-126">For more information, you can review hello [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="17d44-127">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="17d44-127">Known issues</span></span>

- <span data-ttu-id="17d44-128">El SDK de Azure para .NET 3.0 provoca un problema cuando se quita Visual Studio 2017 en una configuración en paralelo con Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="17d44-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="17d44-129">Si tienes hello Azure SDK instalado para Visual Studio 2015, Hola emulador de almacenamiento de Microsoft Azure y el emulador de proceso de Azure de Microsoft se quitarán si desinstala Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="17d44-129">If you have hello Azure SDK installed for Visual Studio 2015, hello Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="17d44-130">Esto generará un error al crear y depurar nuevos proyectos de servicios en la nube en Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="17d44-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="17d44-131">En Ordenar toofix este problema, vuelva a instalar hello Azure SDK de hello instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="17d44-131">In order toofix this issue,  reinstall hello Azure SDK from hello Web Platform Installer.</span></span>  <span data-ttu-id="17d44-132">Hello problema se solucionará en una futura actualización de Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="17d44-132">hello issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="17d44-133">.</span><span class="sxs-lookup"><span data-stu-id="17d44-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="17d44-134">Caché en rol de Azure</span><span class="sxs-lookup"><span data-stu-id="17d44-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="17d44-135">La compatibilidad con Azure In-Role Cache finalizó el 30 de noviembre de 2016.</span><span class="sxs-lookup"><span data-stu-id="17d44-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="17d44-136">Para más detalles, haga clic [aquí](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="17d44-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>



