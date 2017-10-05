---
title: "Opciones para realizar una migración desde Azure RemoteApp | Microsoft Docs"
description: "Obtenga más información sobre las opciones para realizar una migración desde Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9ab63124e2521ee1922d15c1e388c54d50eb8301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="fe5e4-103">Opciones para realizar una migración desde Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="fe5e4-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fe5e4-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fe5e4-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="fe5e4-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="fe5e4-106">Si ha dejado de utilizar Azure RemoteApp debido al [anuncio de retirada](https://go.microsoft.com/fwlink/?linkid=821148) o porque ha terminado la evaluación, tiene que migrar de Azure RemoteApp a otro servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-106">If you have stopped using Azure RemoteApp because of the [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need to migrate off of Azure RemoteApp to another app service.</span></span> <span data-ttu-id="fe5e4-107">Hay dos enfoques diferentes de migración: una implementación autoadministrada (también denominada "infraestructura como servicio" [IaaS]) o una oferta totalmente administrada (a menudo denominada "plataforma como servicio" o "software como servicio"·[PaaS y SaaS respectivamente]).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="fe5e4-108">El IaaS de autoservicio es una implementación donde el usuario es el responsable y quien se encarga de administrarla y realizarla en sistemas físicos o máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="fe5e4-109">Por otro lado, una oferta PaaS y SaaS totalmente administrada guarda una gran similitud con Azure RemoteApp: un asociado proporciona una capa de servicio basada en una solución de acceso remoto que controla las tareas operativas y de mantenimiento, mientras que el usuario, como cliente, se encarga de la administración de las imágenes y las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-109">At the other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as the customer, do some image and app management.</span></span>

<span data-ttu-id="fe5e4-110">[Vea los seminarios web de Azure RemoteApp en las opciones de migración](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp) o siga leyendo para más información (incluidos ejemplos sobre las distintas opciones de hospedaje).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-110">[View the Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of the different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="fe5e4-111">Soluciones autoadministradas (IaaS)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="fe5e4-112">**RDS en IaaS**</span><span class="sxs-lookup"><span data-stu-id="fe5e4-112">**RDS on IaaS**</span></span>
<span data-ttu-id="fe5e4-113">Puede implementar una implementación nativa basada en sesiones de Servicios de Escritorio remoto (en Windows Server) mediante RemoteApp o escritorios locales, o bien en un entorno hospedado (como en máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="fe5e4-114">La opción de RDS en implementaciones de IaaS es más adecuada para los clientes que ya están familiarizados con esta herramienta y que tienen experiencia técnica en implementaciones de RDS.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="fe5e4-115">Para utilizar esta opción de implementación, necesita el programa de Licencias por Volumen con Software Assurance (SA) correspondiente a las licencias de acceso al cliente de RDS.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses to use this deployment option.</span></span>

<span data-ttu-id="fe5e4-116">Implementar RDS en máquinas virtuales de Azure es más fácil que nunca cuando se utilizan plantillas de implementación y aplicación de revisiones (lea una [Introducción](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) y, luego, [descárguelas](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="fe5e4-117">Puede obtener las mismas funcionalidades de escala elástica con los recursos del modelo de implementación clásica de Azure (no los recursos del modelo de Azure Resource Manager) en Azure RemoteApp mediante el [script de escalado automático](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), aunque hay más personalizaciones y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-117">You can get the same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using the [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="fe5e4-118">Al implementar RDS en máquinas virtuales de Azure, el soporte técnico se proporciona a través del equipo de [soporte técnico de Azure](https://azure.microsoft.com/support/plans/), los mismos profesionales que le prestaron asistencia con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), the same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="fe5e4-119">Puede obtener estimaciones de costos en función del patrón de uso actual poniéndose en contacto el equipo de [soporte técnico de Azure](https://azure.microsoft.com/support/plans/), o bien puede realizar los cálculos con una calculadora de costos que se publicará próximamente.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon to be released Cost Calculator.</span></span>  <span data-ttu-id="fe5e4-120">Además, con las máquinas virtuales de serie N (actualmente en fase de versión preliminar), puede agregar vGPU (puede obtener más información sobre cómo agregar vGPU y [aprovechar las mejoras de RDS en Windows Server 2016](https://myignite.microsoft.com/videos/2794) en nuestra sesión Ignite).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how to [harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="fe5e4-121">Contamos con guías de implementación paso a paso de [Windows Server 2012 R2](http://aka.ms/rdsonazure) y [Windows Server 2016](http://aka.ms/rdsonazure2016) para ayudarlo con el proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) to assist with your deployment.</span></span> <span data-ttu-id="fe5e4-122">Visite el [blog de Escritorio remoto](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) para consultar las noticias más recientes.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-122">Check out the [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for the latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="fe5e4-123">**Citrix en IaaS**</span><span class="sxs-lookup"><span data-stu-id="fe5e4-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="fe5e4-124">Las implementaciones nativas de Citrix de las aplicaciones XenApp o XenDesktop basadas en sesiones pueden realizarse en entornos locales u hospedados (por ejemplo, en máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="fe5e4-125">Consulte la guía de implementación paso a paso, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx) (Citrix XA 7.6 en Azure), para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-125">Check out the step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="fe5e4-126">Consulte más detalles sobre [Citrix en Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), donde podrá utilizar también una calculadora de precios.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="fe5e4-127">También puede encontrar un [contacto de Citrix](http://citrix.com/English/contact/index.asp) con quien podrá debatir sus alternativas.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) to discuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="fe5e4-128">Ofertas completamente administradas (PaaS y SaaS)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="fe5e4-129">Citrix XenApp Essentials (publicado en abril de 2017)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="fe5e4-130">Citrix XenApp Essentials, que se encuentra ahora disponible en [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), es el nuevo servicio de virtualización de aplicaciones que combina la potencia y flexibilidad de la plataforma de Citrix Cloud con la visión sencilla, vinculante y fácil de usar de Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-130">Available now on the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is the new application virtualization service, combining the power and flexibility of the Citrix Cloud platform with the simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="fe5e4-131">Los clientes de Azure RemoteApp existentes pueden [registrarse para obtener una evaluación gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="fe5e4-132">Nota: Solo el gasto de servicio de usuario de Citrix es gratis. Se aplican costos de almacenamiento y proceso de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="fe5e4-133">Más información:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-133">Learn More:</span></span>
- [<span data-ttu-id="fe5e4-134">Migración de Azure RemoteApp a Citrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="fe5e4-134">Migrate from Azure RemoteApp to Citrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="fe5e4-135">Citrix y Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe5e4-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="fe5e4-136">[Presentación de Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="fe5e4-137">Servicios Citrix Cloud XenApp y XenDesktop</span><span class="sxs-lookup"><span data-stu-id="fe5e4-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="fe5e4-138">Los servicios [Citrix Cloud XenApp y XenDesktop](https://www.citrix.com/products/citrix-cloud/services.html) son la mejor solución para la entrega de aplicaciones y escritorios y ofrecen además funcionalidades de supervisión y administración avanzadas.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is the best solution for the delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="fe5e4-139">Conexlink (nombre de la plataforma: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="fe5e4-140">[MyCloudIT](https://mycloudit.com) es una plataforma de automatización que permite a las empresas de TI simplificar, optimizar, y escalar la migración y la entrega de aplicaciones y escritorios remotos, además de la infraestructura en la nube de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies to simplify, optimize, and scale the migration and delivery of remote desktops, remote applications, and infrastructure in the Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="fe5e4-141">La plataforma MyCloudIT reduce el tiempo de implementación al 95 %, los costos de Azure al 30 % y mueve toda la infraestructura de TI del cliente a la nube en muy poco tiempo.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-141">The MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into the cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="fe5e4-142">Ahora, los asociados pueden administrar, desde un panel global, clientes y usuarios finales de servicios de todo el mundo como nunca antes, además de aumentar los ingresos, sin tener que agregar más sobrecarga ni ampliar el aprendizaje de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-142">Partners can now manage customers from one global dashboard, service end users around the world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="fe5e4-143">Ubicación principal: Dallas, Texas (Estados Unidos)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="fe5e4-144">Región operativa: en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="fe5e4-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="fe5e4-145">Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="fe5e4-146">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="fe5e4-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fe5e4-147">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="fe5e4-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fe5e4-148">Soluciones de migración de Azure RemoteApp: sí [(más información)](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="fe5e4-149">Brian Garoutte, vicepresidente de Desarrollo Empresarial</span><span class="sxs-lookup"><span data-stu-id="fe5e4-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="fe5e4-150">Teléfono: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="fe5e4-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="fe5e4-151">Correo electrónico: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="fe5e4-152">Frame</span><span class="sxs-lookup"><span data-stu-id="fe5e4-152">Frame</span></span>

<span data-ttu-id="fe5e4-153">Las organizaciones de TI de empresas y equipos gubernamentales, los proveedores de servicios administrados y los proveedores de software líderes eligen Frame para crear y administrar en la nube sus áreas de trabajo seguras y definidas por software.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame to create and manage their secure, software-defined workspaces in the cloud.</span></span> <span data-ttu-id="fe5e4-154">Frame facilita el trabajo enormemente a todo tipo de organizaciones, desde pequeñas hasta grandes, ya que permite a los usuarios acceder a aplicaciones de Windows en cualquier explorador y desde cualquier dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-154">From small to large organizations, Frame makes it incredibly easy to let users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="fe5e4-155">La plataforma Frame incluye todo lo que necesita un administrador para implementar aplicaciones desde la nube, incluidos la infraestructura de Azure y las licencias de RDS (es opcional incluir licencias y cuentas de Azure personalizadas).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-155">The Frame platform includes everything an admin needs to deploy applications from the cloud including the Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="fe5e4-156">Obtenga más información sobre [Frame en Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="fe5e4-157">Ubicación principal: San Mateo, California (Estados Unidos)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="fe5e4-158">Región operativa: en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="fe5e4-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="fe5e4-159">Asociado de Microsoft: Sí</span><span class="sxs-lookup"><span data-stu-id="fe5e4-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="fe5e4-160">Teléfono: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="fe5e4-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="fe5e4-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="fe5e4-161">Awingu</span></span>
<span data-ttu-id="fe5e4-162">Awingu proporciona una solución de área de trabajo en línea simple ejecutando aplicaciones heredadas, SaaS y documentos desde un explorador de html5.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="fe5e4-163">Por lo tanto, realizando todas las aplicaciones disponibles de forma segura en cualquier tipo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="fe5e4-164">Para los servicios de SaaS, existe una amplia gama de opciones de inicio de sesión único de operaciones disponible.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="fe5e4-165">También los sistemas de archivos diferentes (nube) se pueden integrar totalmente en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="fe5e4-166">Junto a la movilidad completa, el área de trabajo en línea enriquecida de Awingu le proporcionará una seguridad óptima con controles granulares (por ejemplo, carga y descarga), un uso completo de auditoría, Multi-Factor Authentication (por ejemplo, Azure MFA), grabación de la sesión y mucho más.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-166">Next to full mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="fe5e4-167">La solución de Awingu, que se encuentra lista para usarse, permite el uso compartido de sesión de la aplicación y documento para la colaboración segura y optimizada.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="fe5e4-168">Dicha solución es una API abierta de varios AD y de varios inquilinos.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="fe5e4-169">La usan pequeñas y grandes empresas, proveedores de servicio en la nube e [ISV](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="fe5e4-170">Estos clientes aprecian especialmente el bajo TCO y la facilidad de uso e instalación.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-170">These customers especially appreciate the easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="fe5e4-171">Awingu All-in-One está [disponible en Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) con dos usuarios simultáneos incorporados.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-171">Awingu All-in-One is [available in the Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="fe5e4-172">Las licencias adicionales están disponibles a través de una [amplia gama de distribuidores y revendedores](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="fe5e4-173">Obtenga más información sobre [Awingu como alternativa a Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-173">Learn more about [Awingu on as alternative to Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="fe5e4-174">Ubicación principal: Bélgica</span><span class="sxs-lookup"><span data-stu-id="fe5e4-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="fe5e4-175">Regiones de funcionamiento: EMEA, Norteamérica y Brasil</span><span class="sxs-lookup"><span data-stu-id="fe5e4-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="fe5e4-176">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="fe5e4-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="fe5e4-177">**Global**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-177">**Global**:</span></span>
> 
> <span data-ttu-id="fe5e4-178">Arnaud Marlière, director de marketing</span><span class="sxs-lookup"><span data-stu-id="fe5e4-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="fe5e4-179">Correo electrónico: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="fe5e4-180">Teléfono: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="fe5e4-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="fe5e4-181">**Sede de Bélgica**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="fe5e4-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="fe5e4-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="fe5e4-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="fe5e4-183">9000 Gent</span></span>
> 
> <span data-ttu-id="fe5e4-184">Correo electrónico: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="fe5e4-185">Teléfono: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="fe5e4-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="fe5e4-186">**EE. UU.**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-186">**USA**:</span></span>
> 
> <span data-ttu-id="fe5e4-187">7th floor, 1177 Ave of the Americas,</span><span class="sxs-lookup"><span data-stu-id="fe5e4-187">7th floor, 1177 Ave of the Americas,</span></span>
> 
> <span data-ttu-id="fe5e4-188">Nueva York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="fe5e4-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="fe5e4-189">Correo electrónico: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="fe5e4-190">Proveedor de servicios hospedados de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe5e4-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="fe5e4-191">Los asociados de hospedaje suelen ofrecen un servicio hospedado de aplicaciones y escritorio de Windows totalmente administrado, que puede incluir la administración de recursos de Azure, sistemas operativos, aplicaciones y el departamento de soporte técnico a través de los contratos de licencias de contratos del asociado con Microsoft y otros proveedores de software, además de constituir un contrato de licencia de proveedor de servicios para permitir la reventa de licencias de acceso de suscriptor (SAL).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing the Azure resources, operating systems, applications, and helpdesk using the partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement to allow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="fe5e4-192">La siguiente información proporciona detalles e información de contacto de algunos de los proveedores de hospedaje que están especializados en ayudar a los clientes con su migración de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-192">The following information provides details and contact information for some of the hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="fe5e4-193">Consulte la [lista actual de proveedores de servicios hospedados](http://aka.ms/rdsonazurecertified) que finalizaron la evaluación y la ruta de aprendizaje de RDS en IaaS.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-193">Check out [the current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed the RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="fe5e4-194">Programa de proveedor de servicios de Citrix</span><span class="sxs-lookup"><span data-stu-id="fe5e4-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="fe5e4-195">Gracias al programa de proveedor de servicios de Citrix, los proveedores de servicios pueden brindar a las pymes informática en la nube virtual de forma fácil, de modo que pueden ofrecer los servicios que estos quieran con un modelo de pago por uso sencillo.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-195">The Citrix Service Provider Program makes it easy for service providers to deliver the simplicity of virtual cloud computing to SMBs, offering them the services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="fe5e4-196">Los proveedores de servicios de Citrix aumentan su volumen de negocios de SPLA de Microsoft y amplían sus inversiones en plataformas RDS con acceso desde cualquier dispositivo y ubicación, la compatibilidad con aplicaciones más extensa del mercado, una experiencia de usuario fructífera, mayor seguridad y más escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, the broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="fe5e4-197">A su vez, proveedores de servicios de Citrix atraen a más suscriptores, aumentan la satisfacción del cliente y reducen los costos operativos.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="fe5e4-198">[Obtenga más información](http://www.citrix.com/products/service-providers.html) o [busque un asociado](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="fe5e4-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="fe5e4-199">Acuutech</span></span>
<span data-ttu-id="fe5e4-200">[Acuutech](http://www.acuutech.com) se especializa en proporcionar soluciones de escritorio hospedadas, de modo que brinda completas experiencias de aplicaciones de ISV y escritorios basadas en la tecnología de Microsoft a una base de clientes internacional a partir de Azure y sus propios centros de datos.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology to a global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="fe5e4-201">Ubicación principal: Londres, Reino Unido; Singapur; Houston, Texas</span><span class="sxs-lookup"><span data-stu-id="fe5e4-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="fe5e4-202">Región operativa: en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="fe5e4-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="fe5e4-203">Estado de asociado: Gold</span><span class="sxs-lookup"><span data-stu-id="fe5e4-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="fe5e4-204">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="fe5e4-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fe5e4-205">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="fe5e4-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fe5e4-206">Soluciones de migración de Azure RemoteApp: sí [(más información)](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="fe5e4-207">**Reino Unido**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="fe5e4-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="fe5e4-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="fe5e4-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="fe5e4-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="fe5e4-210">Teléfono: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="fe5e4-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="fe5e4-211">**Singapur**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="fe5e4-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="fe5e4-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="fe5e4-213">The Globe, Singapur 069532</span><span class="sxs-lookup"><span data-stu-id="fe5e4-213">The Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="fe5e4-214">Teléfono: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="fe5e4-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="fe5e4-215">**Norteamérica**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-215">**North America**:</span></span>
>   
> <span data-ttu-id="fe5e4-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="fe5e4-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="fe5e4-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="fe5e4-218">Teléfono: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="fe5e4-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="fe5e4-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="fe5e4-219">ASPEX</span></span>
<span data-ttu-id="fe5e4-220">[ASPEX](http://www.aspex.be/en) se especializa en los ISV que realizan el proceso de transición a la nube y buscan optimizar sus configuraciones en la nube actuales.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning to the Cloud and ISV‘ looking to optimize their current cloud setups.</span></span> <span data-ttu-id="fe5e4-221">ASPEX ofrece una amplia gama de servicios administrados, DevOps y servicios de consultoría.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="fe5e4-222">Ubicación principal: Amberes, Bélgica</span><span class="sxs-lookup"><span data-stu-id="fe5e4-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="fe5e4-223">Región operativa: Europa Occidental</span><span class="sxs-lookup"><span data-stu-id="fe5e4-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="fe5e4-224">Estado de asociado: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="fe5e4-225">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="fe5e4-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fe5e4-226">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="fe5e4-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fe5e4-227">Soluciones de migración de Azure RemoteApp: sí [(más información)](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="fe5e4-228">Teléfono: +3232202198</span><span class="sxs-lookup"><span data-stu-id="fe5e4-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="fe5e4-229">Correo electrónico: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="fe5e4-230">Sitio web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="fe5e4-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="fe5e4-231">Caase.com</span></span>
<span data-ttu-id="fe5e4-232">[Caase.com](http://www.caase.com/) ayuda a las empresas, gobiernos locales, organismos no gubernamentales e instituciones sanitarias en su ruta a una forma más inteligente de trabajar en Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in the Microsoft Cloud.</span></span> <span data-ttu-id="fe5e4-233">Sea productivo y esté protegido en cualquier lugar, con cualquier dispositivo y a un bajo costo de TI.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="fe5e4-234">Caase.com es un verdadero especialista en Microsoft Office365, Azure, Enterprise Mobility and Security y Windows.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="fe5e4-235">Con nuestra asesoría, servicios de migración, programas de adopción, aprendizaje, administración y respaldo, Caase.com crea una plataforma optimizada y segura de colaboración entre los proveedores, asociados y empleados de los clientes.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="fe5e4-236">Caase.com es el cerebro del área de trabajo remota de Azure (área de trabajo móvil) y del área de trabajo digital (intranet social).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-236">Caase.com is the mastermind of the Azure Remote Workspace (mobile workplace) and the Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="fe5e4-237">Ambas soluciones, logradas gracias a la adopción, son la base que garantiza que los usuarios de estas soluciones tengan la experiencia más agradable, correcta y eficaz en su ruta a Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-237">Both solutions – accomplished with adoption – are the foundation which ensures that the users of these solutions have the most pleasant, successful and effective experience in their route to the Microsoft Cloud.</span></span>
<span data-ttu-id="fe5e4-238">Aquí puede encontrar una traducción al neerlandés y una película de respaldo: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="fe5e4-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="fe5e4-239">Región de la operación: empresa neerlandesa con alcance mundial</span><span class="sxs-lookup"><span data-stu-id="fe5e4-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="fe5e4-240">Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="fe5e4-241">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="fe5e4-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fe5e4-242">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="fe5e4-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fe5e4-243">Soluciones de migración de Azure RemoteApp: sí [(más información)](http://caase.com/diensten/microsoft-azure/)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="fe5e4-244">Países Bajos:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-244">Netherlands:</span></span>
> 
> <span data-ttu-id="fe5e4-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="fe5e4-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="fe5e4-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="fe5e4-247">Teléfono: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="fe5e4-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="fe5e4-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="fe5e4-248">Nerdio</span></span>
<span data-ttu-id="fe5e4-249">[Nerdio for Azure](http://getnerdio.com/nfa/) es una plataforma de automatización de TI que ofrece aprovisionamiento, administración y optimización muy simples de entornos de TI completos en Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in the Microsoft cloud.</span></span> <span data-ttu-id="fe5e4-250">Optimice escritorios virtuales, aplicaciones remotas y servidores en un par de horas.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="fe5e4-251">Administre el entorno en tres clics o menos con el portal de administración de Nerdio.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-251">Administer the environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="fe5e4-252">Use el escalado automático inteligente y ahorre entre un 40 % y un 60 % en recursos de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-252">Use intelligent auto-scaling and save 40 to 60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="fe5e4-253">Ubicación principal: Chicago, IL Región de la operación: en todo el mundo Estado de asociado: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Proveedor de servicios en Microsoft Cloud: sí</span><span class="sxs-lookup"><span data-stu-id="fe5e4-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fe5e4-254">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="fe5e4-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fe5e4-255">Soluciones de migración de Azure RemoteApp: sí</span><span class="sxs-lookup"><span data-stu-id="fe5e4-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="fe5e4-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="fe5e4-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="fe5e4-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="fe5e4-257">Suite 212</span></span>
> 
> <span data-ttu-id="fe5e4-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="fe5e4-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="fe5e4-259">EE. UU.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-259">USA</span></span>
> 
> <span data-ttu-id="fe5e4-260">(844) 4NERDIO ext.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-260">(844) 4NERDIO ext.</span></span> <span data-ttu-id="fe5e4-261">6</span><span class="sxs-lookup"><span data-stu-id="fe5e4-261">6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="fe5e4-262">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="fe5e4-262">**SaaSplaza**</span></span>
<span data-ttu-id="fe5e4-263">[SaaSplaza](http://www.saasplaza.com/) ofrece las soluciones en la nube públicas y privadas (Azure) de la cartera completa de Microsoft Dynamics (NAV, AX, GP, SL y CRM).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-263">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="fe5e4-264">Ubicación principal: Países bajos</span><span class="sxs-lookup"><span data-stu-id="fe5e4-264">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="fe5e4-265">Región operativa: en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="fe5e4-265">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="fe5e4-266">Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="fe5e4-266">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="fe5e4-267">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="fe5e4-267">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="fe5e4-268">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="fe5e4-268">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="fe5e4-269">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-269">**EMEA**:</span></span>
> 
> <span data-ttu-id="fe5e4-270">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="fe5e4-270">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="fe5e4-271">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="fe5e4-271">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="fe5e4-272">Países Bajos</span><span class="sxs-lookup"><span data-stu-id="fe5e4-272">The Netherlands</span></span>
> 
> <span data-ttu-id="fe5e4-273">Teléfono: + 31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="fe5e4-273">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="fe5e4-274">**América**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-274">**Americas**:</span></span>
> 
> <span data-ttu-id="fe5e4-275">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="fe5e4-275">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="fe5e4-276">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="fe5e4-276">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="fe5e4-277">San Diego</span><span class="sxs-lookup"><span data-stu-id="fe5e4-277">San Diego</span></span>
> 
> <span data-ttu-id="fe5e4-278">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="fe5e4-278">United States</span></span>
> 
> <span data-ttu-id="fe5e4-279">Teléfono: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="fe5e4-279">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="fe5e4-280">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="fe5e4-280">**APAC**:</span></span>
> 
> <span data-ttu-id="fe5e4-281">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="fe5e4-281">105 Cecil Street</span></span>
>    
> <span data-ttu-id="fe5e4-282">\#11-08, The Octagon</span><span class="sxs-lookup"><span data-stu-id="fe5e4-282">\#11-08, The Octagon</span></span>
> 
> <span data-ttu-id="fe5e4-283">Singapur 069534</span><span class="sxs-lookup"><span data-stu-id="fe5e4-283">Singapore 069534</span></span>
> 
> <span data-ttu-id="fe5e4-284">Singapur</span><span class="sxs-lookup"><span data-stu-id="fe5e4-284">Singapore</span></span>
>   
> <span data-ttu-id="fe5e4-285">Teléfono (Singapur): + 65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="fe5e4-285">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="fe5e4-286">Teléfono (Australia): + 61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="fe5e4-286">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="fe5e4-287">Teléfono (Nueva Zelanda): + 64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="fe5e4-287">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="fe5e4-288">¿Necesita más ayuda?</span><span class="sxs-lookup"><span data-stu-id="fe5e4-288">Need more help?</span></span>
<span data-ttu-id="fe5e4-289">¿Todavía necesita ayuda para decidirse o tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="fe5e4-289">Still need help choosing or have further questions?</span></span> <span data-ttu-id="fe5e4-290">Use cualquiera de los métodos siguientes para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-290">Use one of the following methods to get help.</span></span> 

1. <span data-ttu-id="fe5e4-291">Envíenos un correo electrónico a [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-291">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="fe5e4-292">Póngase en contacto con el equipo de [soporte técnico de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-292">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="fe5e4-293">Comience abriendo un [caso de soporte técnico de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-293">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="fe5e4-294">Llámenos.</span><span class="sxs-lookup"><span data-stu-id="fe5e4-294">Call us.</span></span> <span data-ttu-id="fe5e4-295">[Encuentre un número de ventas local](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="fe5e4-295">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

