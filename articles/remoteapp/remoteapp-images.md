---
title: "¿aaaWhat contiene imágenes de plantilla de hello Azure RemoteApp? | Microsoft Docs"
description: "Obtenga información acerca de las imágenes de plantilla de hello incluidas con Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a><span data-ttu-id="e71ce-104">¿Qué es imágenes de plantilla de hello Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="e71ce-104">What is in hello Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e71ce-105">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="e71ce-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e71ce-106">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e71ce-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e71ce-107">La suscripción de Azure RemoteApp incluye tres imágenes de plantilla:</span><span class="sxs-lookup"><span data-stu-id="e71ce-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="e71ce-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e71ce-108">Windows Server 2012</span></span>
* <span data-ttu-id="e71ce-109">Microsoft Office 365 ProPlus (se requiere suscripción a Office 365)</span><span class="sxs-lookup"><span data-stu-id="e71ce-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="e71ce-110">Microsoft Office Professional Plus 2013 (solo versión de prueba)</span><span class="sxs-lookup"><span data-stu-id="e71ce-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e71ce-111">Su suscripción de Azure RemoteApp concede que acceso toohello software en imágenes de hello, con excepción de Hola de Office 365 ProPlus, lo que requiere una suscripción independiente, y Office 2013, que no se puede usar en producción.</span><span class="sxs-lookup"><span data-stu-id="e71ce-111">Your Azure RemoteApp subscription grants you access toohello software in hello images, with hello exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="e71ce-112">Esto significa que puede compartir programas Hola o aplicaciones en imágenes de plantilla de hello con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e71ce-112">This means that you can share hello programs or apps on hello template images with your users.</span></span> <span data-ttu-id="e71ce-113">Por ejemplo, si crea una recopilación que use la imagen de Windows Server 2012 R2 de hello, puede publicar System Center Endpoint Protection para tooaccess a los usuarios a través de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e71ce-113">For example, if you create a collection that uses hello Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users tooaccess through RemoteApp.</span></span>
> 
> <span data-ttu-id="e71ce-114">Extraer del repositorio hello [RemoteApp licencias detalles](remoteapp-licensing.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e71ce-114">Check out hello [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="e71ce-115">Y [usando Office con Azure RemoteApp](remoteapp-o365.md) para hello información de licencia de Office.</span><span class="sxs-lookup"><span data-stu-id="e71ce-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for hello Office licensing info.</span></span>
> 
> 

<span data-ttu-id="e71ce-116">Siga leyendo para obtener más información sobre lo que contiene cada imagen.</span><span class="sxs-lookup"><span data-stu-id="e71ce-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--hello-vanilla-image"></a><span data-ttu-id="e71ce-117">Windows Server 2012 R2 ("hello vainilla imagen")</span><span class="sxs-lookup"><span data-stu-id="e71ce-117">Windows Server 2012 R2  ("hello vanilla image")</span></span>
<span data-ttu-id="e71ce-118">Esta imagen se basa en el sistema operativo de Microsoft Windows Server 2012 R2 Datacenter y hello siguientes roles y características instaló toomeet requisitos de Hola para imágenes de plantilla de RemoteApp de Azure:</span><span class="sxs-lookup"><span data-stu-id="e71ce-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has hello following roles and features installed toomeet hello requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="e71ce-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="e71ce-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="e71ce-120">Experiencia de escritorio</span><span class="sxs-lookup"><span data-stu-id="e71ce-120">Desktop Experience</span></span>
* <span data-ttu-id="e71ce-121">Servicios de Escritura con lápiz y Escritura a mano</span><span class="sxs-lookup"><span data-stu-id="e71ce-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="e71ce-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="e71ce-122">Media Foundation</span></span>
* <span data-ttu-id="e71ce-123">Host de sesión de Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="e71ce-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="e71ce-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="e71ce-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="e71ce-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="e71ce-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="e71ce-126">Compatibilidad con WoW64</span><span class="sxs-lookup"><span data-stu-id="e71ce-126">WoW64 Support</span></span>

<span data-ttu-id="e71ce-127">Esta imagen también tiene Hola después de las aplicaciones instaladas:</span><span class="sxs-lookup"><span data-stu-id="e71ce-127">This image also has hello following applications installed:</span></span>

* <span data-ttu-id="e71ce-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="e71ce-128">Adobe Flash Player</span></span>
* <span data-ttu-id="e71ce-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="e71ce-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="e71ce-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="e71ce-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="e71ce-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="e71ce-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="e71ce-132">Microsoft Office 365 ProPlus (se requiere suscripción)</span><span class="sxs-lookup"><span data-stu-id="e71ce-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="e71ce-133">Office 365 es Hola más aplicación solicitada, por lo que se crea una imagen de "custom" toowork con.</span><span class="sxs-lookup"><span data-stu-id="e71ce-133">Office 365 is hello most requested application, so we created a "custom" image for you toowork with.</span></span>

<span data-ttu-id="e71ce-134">Esta imagen es una extensión de imagen de vainilla hello y tiene hello siguientes componentes de Microsoft Office 365 ProPlus además toohello componentes instalados que se describe en la imagen de Windows Server 2012 R2 de hello:</span><span class="sxs-lookup"><span data-stu-id="e71ce-134">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 365 ProPlus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="e71ce-135">Access</span><span class="sxs-lookup"><span data-stu-id="e71ce-135">Access</span></span>
* <span data-ttu-id="e71ce-136">Excel</span><span class="sxs-lookup"><span data-stu-id="e71ce-136">Excel</span></span>
* <span data-ttu-id="e71ce-137">Lync</span><span class="sxs-lookup"><span data-stu-id="e71ce-137">Lync</span></span>
* <span data-ttu-id="e71ce-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="e71ce-138">OneNote</span></span>
* <span data-ttu-id="e71ce-139">OneDrive para la empresa (tenga en cuenta ese agente de sincronización de hello no se admite para su uso con Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="e71ce-139">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="e71ce-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="e71ce-140">Outlook</span></span>
* <span data-ttu-id="e71ce-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="e71ce-141">PowerPoint</span></span>
* <span data-ttu-id="e71ce-142">Word</span><span class="sxs-lookup"><span data-stu-id="e71ce-142">Word</span></span>
* <span data-ttu-id="e71ce-143">Herramientas de corrección de Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="e71ce-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="e71ce-144">imagen de Hello también incluye Visio Pro y Project Pro.</span><span class="sxs-lookup"><span data-stu-id="e71ce-144">hello image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="e71ce-145">Y Hola derivados de la solicitud, así:</span><span class="sxs-lookup"><span data-stu-id="e71ce-145">And hello following applications, as well:</span></span>

* <span data-ttu-id="e71ce-146">SQL Native Client</span><span class="sxs-lookup"><span data-stu-id="e71ce-146">SQL Native client</span></span>
* <span data-ttu-id="e71ce-147">Controlador ODBC</span><span class="sxs-lookup"><span data-stu-id="e71ce-147">ODBC Driver</span></span>
* <span data-ttu-id="e71ce-148">Cliente de minería de datos para SQL Server</span><span class="sxs-lookup"><span data-stu-id="e71ce-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="e71ce-149">Cliente MasterDataServices</span><span class="sxs-lookup"><span data-stu-id="e71ce-149">MasterDataServices client</span></span>
* <span data-ttu-id="e71ce-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="e71ce-150">Microsoft Publisher</span></span>
* <span data-ttu-id="e71ce-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="e71ce-151">PowerQuery</span></span>
* <span data-ttu-id="e71ce-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="e71ce-152">PowerMap</span></span>

<span data-ttu-id="e71ce-153">La funcionalidad completa de las aplicaciones de Office 365 ProPlus está disponible solo para los usuarios que tienen un plan de Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="e71ce-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="e71ce-154">Para obtener más detalles sobre la suscripción de Office 365 Hola vea planes [planes de servicio de Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="e71ce-154">For more details on hello Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="e71ce-155">¿Todavía tiene preguntas?</span><span class="sxs-lookup"><span data-stu-id="e71ce-155">Still have questions?</span></span> <span data-ttu-id="e71ce-156">Extraer del repositorio hello [Office 365 + RemoteApp](remoteapp-o365.md) información.</span><span class="sxs-lookup"><span data-stu-id="e71ce-156">Check out hello [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="e71ce-157">Desproteger nuevo artículo de hello, [cómo toouse la suscripción a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="e71ce-157">Also check out hello new article, [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="e71ce-158">Tenga en cuenta que necesita toolicense Office 365 ProPlus, Visio Pro y proyecto Pro por separado, cada uno de ellos tiene su propia licencia.</span><span class="sxs-lookup"><span data-stu-id="e71ce-158">Note that you need toolicense Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="e71ce-159">Microsoft Office Professional Plus 2013 (solo versión de prueba)</span><span class="sxs-lookup"><span data-stu-id="e71ce-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="e71ce-160">Durante el período de evaluación gratuita de hello, puede probar servicio Hola con imagen Hola Office 2013.</span><span class="sxs-lookup"><span data-stu-id="e71ce-160">During hello free trial period, you can test hello service with hello Office 2013 image.</span></span>

<span data-ttu-id="e71ce-161">Esta imagen es una extensión de imagen de vainilla hello y tiene hello siguientes componentes de Microsoft Office 2013 Professional Plus además toohello componentes instalados que se describe en la imagen de Windows Server 2012 R2 de hello:</span><span class="sxs-lookup"><span data-stu-id="e71ce-161">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 2013 Professional Plus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="e71ce-162">Access</span><span class="sxs-lookup"><span data-stu-id="e71ce-162">Access</span></span>
* <span data-ttu-id="e71ce-163">Excel</span><span class="sxs-lookup"><span data-stu-id="e71ce-163">Excel</span></span>
* <span data-ttu-id="e71ce-164">Lync</span><span class="sxs-lookup"><span data-stu-id="e71ce-164">Lync</span></span>
* <span data-ttu-id="e71ce-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="e71ce-165">OneNote</span></span>
* <span data-ttu-id="e71ce-166">OneDrive para la empresa (tenga en cuenta ese agente de sincronización de hello no se admite para su uso con Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="e71ce-166">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="e71ce-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="e71ce-167">Outlook</span></span>
* <span data-ttu-id="e71ce-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="e71ce-168">PowerPoint</span></span>
* <span data-ttu-id="e71ce-169">proyecto</span><span class="sxs-lookup"><span data-stu-id="e71ce-169">Project</span></span>
* <span data-ttu-id="e71ce-170">Visio</span><span class="sxs-lookup"><span data-stu-id="e71ce-170">Visio</span></span>
* <span data-ttu-id="e71ce-171">Word</span><span class="sxs-lookup"><span data-stu-id="e71ce-171">Word</span></span>
* <span data-ttu-id="e71ce-172">Herramientas de corrección de Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="e71ce-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e71ce-173">**Información legal** : esta imagen no incluye una licencia de Microsoft Office y *no se puede usar en producción*.</span><span class="sxs-lookup"><span data-stu-id="e71ce-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="e71ce-174">imagen de Office 2013 Professional Plus Hola está pensado solo para fines de prueba.</span><span class="sxs-lookup"><span data-stu-id="e71ce-174">hello Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="e71ce-175">Si desea que las aplicaciones de Office toouse en Azure RemoteApp para la producción, debe imagen de Office 365 ProPlus toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="e71ce-175">If you want toouse Office apps in Azure RemoteApp for production, you need toouse hello Office 365 ProPlus image.</span></span> <span data-ttu-id="e71ce-176">Para obtener más detalles sobre las licencias de Office, consulte [Uso de Office 365 con Azure RemoteApp](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="e71ce-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

