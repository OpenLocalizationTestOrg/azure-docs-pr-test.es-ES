---
title: aaaOptions para migrar de RemoteApp de Azure | Documentos de Microsoft
description: "Obtenga información acerca de las opciones de Hola para migrar de Azure RemoteApp."
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
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="7e348-103">Opciones para realizar una migración desde Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7e348-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7e348-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="7e348-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7e348-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7e348-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="7e348-106">Si se han dejado de usar Azure RemoteApp debido a hello [anuncio de retirada](https://go.microsoft.com/fwlink/?linkid=821148) o porque haya terminado la evaluación, necesitará toomigrate fuera de servicio de aplicaciones de Azure RemoteApp tooanother.</span><span class="sxs-lookup"><span data-stu-id="7e348-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="7e348-107">Hay dos enfoques diferentes de migración: una implementación autoadministrada (también denominada "infraestructura como servicio" [IaaS]) o una oferta totalmente administrada (a menudo denominada "plataforma como servicio" o "software como servicio"·[PaaS y SaaS respectivamente]).</span><span class="sxs-lookup"><span data-stu-id="7e348-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="7e348-108">El IaaS de autoservicio es una implementación donde el usuario es el responsable y quien se encarga de administrarla y realizarla en sistemas físicos o máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7e348-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="7e348-109">En hello otro finalizar una completamente administrado PaaS/oferta de SaaS es más, como Azure RemoteApp: un socio proporciona un nivel de servicio por encima de una solución de acceso remoto que controla operativa y de mantenimiento, mientras el equipo, como cliente de hello, realice algunas administración de aplicaciones y de imagen.</span><span class="sxs-lookup"><span data-stu-id="7e348-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="7e348-110">[Ver seminarios Web de Azure RemoteApp hello en Opciones de migración](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), o siga leyendo para obtener más información (con ejemplos de hello diferente opciones de hospedaje).</span><span class="sxs-lookup"><span data-stu-id="7e348-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="7e348-111">Soluciones autoadministradas (IaaS)</span><span class="sxs-lookup"><span data-stu-id="7e348-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="7e348-112">**RDS en IaaS**</span><span class="sxs-lookup"><span data-stu-id="7e348-112">**RDS on IaaS**</span></span>
<span data-ttu-id="7e348-113">Puede implementar una implementación nativa basada en sesiones de Servicios de Escritorio remoto (en Windows Server) mediante RemoteApp o escritorios locales, o bien en un entorno hospedado (como en máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="7e348-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="7e348-114">La opción de RDS en implementaciones de IaaS es más adecuada para los clientes que ya están familiarizados con esta herramienta y que tienen experiencia técnica en implementaciones de RDS.</span><span class="sxs-lookup"><span data-stu-id="7e348-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="7e348-115">Se necesita con Software Assurance (SA) de licencias por volumen para toouse de licencias de acceso de cliente RDS esta opción de implementación.</span><span class="sxs-lookup"><span data-stu-id="7e348-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="7e348-116">Implementar RDS en máquinas virtuales de Azure es más fácil que nunca cuando se utilizan plantillas de implementación y aplicación de revisiones (lea una [Introducción](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) y, luego, [descárguelas](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="7e348-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="7e348-117">Puede obtener Hola mismas capacidades de escala elásticas con recursos de modelo de implementación clásico de Azure (no los recursos de modelo de recursos de Azure) en Azure RemoteApp mediante hello [Autoescala script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), aunque haya más las personalizaciones y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="7e348-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="7e348-118">Al implementar RDS en máquinas virtuales de Azure, se admiten a través de [Azure admite](https://azure.microsoft.com/support/plans/), Hola mismo profesionales de soporte técnico que es compatible con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7e348-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="7e348-119">Se pueden obtener estimaciones de costos en función de su uso existente poniéndose en contacto [soporte técnico de Azure](https://azure.microsoft.com/support/plans/), o se pueden realizar cálculos mediante un poco toobe libera Calculadora de costo.</span><span class="sxs-lookup"><span data-stu-id="7e348-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="7e348-120">Además, con máquinas virtuales de serie N (actualmente en private preview), puede agregar vGPU - oír más acerca de cómo agregar vGPU y sobre cómo demasiado[aprovechar las mejoras de RDS en Windows Server 2016](https://myignite.microsoft.com/videos/2794) en nuestra sesión Ignite.</span><span class="sxs-lookup"><span data-stu-id="7e348-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="7e348-121">Contamos con guías de implementación paso a paso de [Windows Server 2012 R2](http://aka.ms/rdsonazure) y [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist con la implementación.</span><span class="sxs-lookup"><span data-stu-id="7e348-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="7e348-122">Extraer del repositorio hello [blog de escritorio remoto](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) para las últimas noticias de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e348-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="7e348-123">**Citrix en IaaS**</span><span class="sxs-lookup"><span data-stu-id="7e348-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="7e348-124">Las implementaciones nativas de Citrix de las aplicaciones XenApp o XenDesktop basadas en sesiones pueden realizarse en entornos locales u hospedados (por ejemplo, en máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="7e348-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="7e348-125">Visite la Guía de implementación paso a paso de hello, [Citrix XA 7.6 en Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7e348-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="7e348-126">Consulte más detalles sobre [Citrix en Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), donde podrá utilizar también una calculadora de precios.</span><span class="sxs-lookup"><span data-stu-id="7e348-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="7e348-127">También puede encontrar un [Citrix póngase en contacto con](http://citrix.com/English/contact/index.asp) toodiscuss las opciones con.</span><span class="sxs-lookup"><span data-stu-id="7e348-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="7e348-128">Ofertas completamente administradas (PaaS y SaaS)</span><span class="sxs-lookup"><span data-stu-id="7e348-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="7e348-129">Citrix XenApp Essentials (publicado en abril de 2017)</span><span class="sxs-lookup"><span data-stu-id="7e348-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="7e348-130">Está disponible ahora en hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials es servicio de virtualización de aplicaciones nueva hello, combinación de energía de Hola y Hola de flexibilidad de plataforma de nube de Citrix Hola simples, preceptivo, y fácil de consumir visión de Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7e348-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="7e348-131">Los clientes de Azure RemoteApp existentes pueden [registrarse para obtener una evaluación gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e348-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="7e348-132">Nota: Solo el gasto de servicio de usuario de Citrix es gratis. Se aplican costos de almacenamiento y proceso de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e348-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="7e348-133">Más información:</span><span class="sxs-lookup"><span data-stu-id="7e348-133">Learn More:</span></span>
- [<span data-ttu-id="7e348-134">Migrar de Azure RemoteApp tooCitrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="7e348-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="7e348-135">Citrix y Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e348-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="7e348-136">[Presentación de Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k)</span><span class="sxs-lookup"><span data-stu-id="7e348-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="7e348-137">Servicios Citrix Cloud XenApp y XenDesktop</span><span class="sxs-lookup"><span data-stu-id="7e348-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="7e348-138">[Citrix XenApp servicio nube y XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) es Hola mejor solución para la entrega de Hola de las aplicaciones y escritorios, más avanzadas de administración y capacidades de supervisión.</span><span class="sxs-lookup"><span data-stu-id="7e348-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="7e348-139">Conexlink (nombre de la plataforma: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="7e348-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="7e348-140">[MyCloudIT](https://mycloudit.com) es una plataforma de automatización para toosimplify de empresas de TI, optimizar y escalar la migración de Hola y Hola de entrega de escritorios remotos, las aplicaciones remotas y la infraestructura de nube de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7e348-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="7e348-141">plataforma de Hello MyCloudIT reduce el tiempo de implementación al 95%, Azure costos al 30% y mueve toda infraestructura de TI de su cliente en la nube de hello en cuestión de unas pocas pulsaciones de teclas.</span><span class="sxs-lookup"><span data-stu-id="7e348-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="7e348-142">Socios ahora pueden administrar los clientes de un panel global, los usuarios finales de servicio alrededor de Hola a todos como nunca antes y aumentar los ingresos sin tener que agregar una sobrecarga adicional o una amplia capacitación de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e348-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="7e348-143">Ubicación principal: Dallas, Texas (Estados Unidos)</span><span class="sxs-lookup"><span data-stu-id="7e348-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="7e348-144">Región operativa: en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="7e348-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="7e348-145">Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="7e348-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="7e348-146">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="7e348-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="7e348-147">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="7e348-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="7e348-148">Soluciones de migración de Azure RemoteApp: sí [(más información)](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="7e348-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="7e348-149">Brian Garoutte, vicepresidente de Desarrollo Empresarial</span><span class="sxs-lookup"><span data-stu-id="7e348-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="7e348-150">Teléfono: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="7e348-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="7e348-151">Correo electrónico: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="7e348-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="7e348-152">Frame</span><span class="sxs-lookup"><span data-stu-id="7e348-152">Frame</span></span>

<span data-ttu-id="7e348-153">Las organizaciones de TI en enterprise y gubernamentales, proveedores de servicios administrados y proveedores de software líderes elija marco toocreate y administración sus áreas de trabajo seguros y definidas por el software en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e348-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="7e348-154">De toolarge pequeñas organizaciones, marco hace toolet increíblemente fácil a los usuarios tener acceso a aplicaciones de Windows en cualquier explorador desde cualquier dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e348-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="7e348-155">Hello plataforma marco incluye todo lo que un administrador necesidades toodeploy aplicaciones de nube Hola incluidos Hola infraestructura de Azure y las licencias RDS (volver a poner su propia cuenta de Azure y las licencias es opcional).</span><span class="sxs-lookup"><span data-stu-id="7e348-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="7e348-156">Obtenga más información sobre [Frame en Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="7e348-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="7e348-157">Ubicación principal: San Mateo, California (Estados Unidos)</span><span class="sxs-lookup"><span data-stu-id="7e348-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="7e348-158">Región operativa: en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="7e348-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="7e348-159">Asociado de Microsoft: Sí</span><span class="sxs-lookup"><span data-stu-id="7e348-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="7e348-160">Teléfono: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="7e348-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="7e348-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="7e348-161">Awingu</span></span>
<span data-ttu-id="7e348-162">Awingu proporciona una solución de área de trabajo en línea simple ejecutando aplicaciones heredadas, SaaS y documentos desde un explorador de html5.</span><span class="sxs-lookup"><span data-stu-id="7e348-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="7e348-163">Por lo tanto, realizando todas las aplicaciones disponibles de forma segura en cualquier tipo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e348-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="7e348-164">Para los servicios de SaaS, existe una amplia gama de opciones de inicio de sesión único de operaciones disponible.</span><span class="sxs-lookup"><span data-stu-id="7e348-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="7e348-165">También los sistemas de archivos diferentes (nube) se pueden integrar totalmente en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7e348-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="7e348-166">Movilidad de toofull siguiente, área de trabajo en línea del Awingu enriquecido le dará una seguridad óptima con controles granulares (por ejemplo, carga y descarga), uso completo de auditoría, la autenticación multifactor (p. ej., Azure MFA), la grabación de sesión y mucho más.</span><span class="sxs-lookup"><span data-stu-id="7e348-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="7e348-167">La solución de Awingu, que se encuentra lista para usarse, permite el uso compartido de sesión de la aplicación y documento para la colaboración segura y optimizada.</span><span class="sxs-lookup"><span data-stu-id="7e348-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="7e348-168">Dicha solución es una API abierta de varios AD y de varios inquilinos.</span><span class="sxs-lookup"><span data-stu-id="7e348-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="7e348-169">La usan pequeñas y grandes empresas, proveedores de servicio en la nube e [ISV](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="7e348-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="7e348-170">Estos clientes especialmente aprecian Hola fácil de usar, TCO de facilidad de instalación y bajo.</span><span class="sxs-lookup"><span data-stu-id="7e348-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="7e348-171">Es Awingu All-in-One [disponibles en Azure Marketplace hello](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) con 2 usuarios simultáneos integrados.</span><span class="sxs-lookup"><span data-stu-id="7e348-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="7e348-172">Las licencias adicionales están disponibles a través de una [amplia gama de distribuidores y revendedores](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="7e348-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="7e348-173">Obtenga más información sobre [Awingu en como alternativo tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="7e348-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="7e348-174">Ubicación principal: Bélgica</span><span class="sxs-lookup"><span data-stu-id="7e348-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="7e348-175">Regiones de funcionamiento: EMEA, Norteamérica y Brasil</span><span class="sxs-lookup"><span data-stu-id="7e348-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="7e348-176">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="7e348-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="7e348-177">**Global**:</span><span class="sxs-lookup"><span data-stu-id="7e348-177">**Global**:</span></span>
> 
> <span data-ttu-id="7e348-178">Arnaud Marlière, director de marketing</span><span class="sxs-lookup"><span data-stu-id="7e348-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="7e348-179">Correo electrónico: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="7e348-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="7e348-180">Teléfono: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="7e348-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="7e348-181">**Sede de Bélgica**:</span><span class="sxs-lookup"><span data-stu-id="7e348-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="7e348-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="7e348-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="7e348-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="7e348-183">9000 Gent</span></span>
> 
> <span data-ttu-id="7e348-184">Correo electrónico: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="7e348-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="7e348-185">Teléfono: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="7e348-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="7e348-186">**EE. UU.**:</span><span class="sxs-lookup"><span data-stu-id="7e348-186">**USA**:</span></span>
> 
> <span data-ttu-id="7e348-187">7 floor, 1177 Ave de hello Americas,</span><span class="sxs-lookup"><span data-stu-id="7e348-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="7e348-188">Nueva York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="7e348-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="7e348-189">Correo electrónico: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="7e348-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="7e348-190">Proveedor de servicios hospedados de Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e348-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="7e348-191">Socios de hospedaje normalmente ofrecen un completamente administrado hospeda el escritorio de Windows y Hola de servicio de aplicaciones, que puede incluir la administración de recursos de Azure, sistemas operativos, aplicaciones y departamento de soporte técnico con los socios de Hola de licencias de contratos con Microsoft y otros proveedores de software junto con que se va a un contrato de licencia de proveedor de servicio tooallow revender licencias de acceso de suscriptor (SAL).</span><span class="sxs-lookup"><span data-stu-id="7e348-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="7e348-192">Hello siguiente información proporciona detalles e información de contacto para algunos de los proveedores de hospedaje de Hola que se especializan en ayudando a los clientes con su migración de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="7e348-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="7e348-193">Extraer del repositorio [lista actual de Hola de proveedores de servicios hospedados](http://aka.ms/rdsonazurecertified) que finalizaron Hola RDS en IaaS evaluación y la ruta de acceso de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="7e348-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="7e348-194">Programa de proveedor de servicios de Citrix</span><span class="sxs-lookup"><span data-stu-id="7e348-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="7e348-195">Hola Citrix el programa de proveedor de servicio facilita la sencillez de Hola de toodeliver de proveedores de servicio de virtual cloud computing tooSMBs, oferta de servicios de hello desean ver en un modelo de pago por uso, fácil.</span><span class="sxs-lookup"><span data-stu-id="7e348-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="7e348-196">Proveedores de servicios de Citrix crecer sus negocios de Microsoft SPLA y ampliar sus inversiones en plataformas RDS con cualquier dispositivo, acceso desde cualquier lugar, Hola más amplia compatibilidad de aplicación, una rica experiencia, lograr una mayor seguridad y una mayor escalabilidad.</span><span class="sxs-lookup"><span data-stu-id="7e348-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="7e348-197">A su vez, proveedores de servicios de Citrix atraen a más suscriptores, aumentan la satisfacción del cliente y reducen los costos operativos.</span><span class="sxs-lookup"><span data-stu-id="7e348-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="7e348-198">[Obtenga más información](http://www.citrix.com/products/service-providers.html) o [busque un asociado](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="7e348-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="7e348-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="7e348-199">Acuutech</span></span>
<span data-ttu-id="7e348-200">[Acuutech](http://www.acuutech.com) se especializa en proporcionar soluciones de escritorio hospedadas, entregar todo el escritorio y aplicaciones de ISV experiencias creadas en Microsoft tooa global cliente de la tecnología base de Azure y sus propios centros de datos.</span><span class="sxs-lookup"><span data-stu-id="7e348-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="7e348-201">Ubicación principal: Londres, Reino Unido; Singapur; Houston, Texas</span><span class="sxs-lookup"><span data-stu-id="7e348-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="7e348-202">Región operativa: en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="7e348-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="7e348-203">Estado de asociado: Gold</span><span class="sxs-lookup"><span data-stu-id="7e348-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="7e348-204">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="7e348-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="7e348-205">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="7e348-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="7e348-206">Soluciones de migración de Azure RemoteApp: sí [(más información)](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="7e348-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="7e348-207">**Reino Unido**:</span><span class="sxs-lookup"><span data-stu-id="7e348-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="7e348-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="7e348-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="7e348-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="7e348-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="7e348-210">Teléfono: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="7e348-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="7e348-211">**Singapur**:</span><span class="sxs-lookup"><span data-stu-id="7e348-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="7e348-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="7e348-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="7e348-213">Hola mundo, Singapur 069532</span><span class="sxs-lookup"><span data-stu-id="7e348-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="7e348-214">Teléfono: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="7e348-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="7e348-215">**Norteamérica**:</span><span class="sxs-lookup"><span data-stu-id="7e348-215">**North America**:</span></span>
>   
> <span data-ttu-id="7e348-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="7e348-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="7e348-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="7e348-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="7e348-218">Teléfono: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="7e348-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="7e348-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="7e348-219">ASPEX</span></span>
<span data-ttu-id="7e348-220">[ASPEX](http://www.aspex.be/en) se especializa en ISV transición toohello en la nube y ISV' busca toooptimize sus configuraciones de nube actuales.</span><span class="sxs-lookup"><span data-stu-id="7e348-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="7e348-221">ASPEX ofrece una amplia gama de servicios administrados, DevOps y servicios de consultoría.</span><span class="sxs-lookup"><span data-stu-id="7e348-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="7e348-222">Ubicación principal: Amberes, Bélgica</span><span class="sxs-lookup"><span data-stu-id="7e348-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="7e348-223">Región operativa: Europa Occidental</span><span class="sxs-lookup"><span data-stu-id="7e348-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="7e348-224">Estado de asociado: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="7e348-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="7e348-225">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="7e348-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="7e348-226">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="7e348-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="7e348-227">Soluciones de migración de Azure RemoteApp: sí [(más información)](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="7e348-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="7e348-228">Teléfono: +3232202198</span><span class="sxs-lookup"><span data-stu-id="7e348-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="7e348-229">Correo electrónico: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="7e348-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="7e348-230">Sitio web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="7e348-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="7e348-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="7e348-231">Caase.com</span></span>
<span data-ttu-id="7e348-232">[Caase.com](http://www.caase.com/) ayuda a las empresas, gobiernos locales, cuerpos no gubernamentales e instituciones sanitarios con su viaje hacia una manera más inteligente de trabajo en Microsoft Cloud Hola.</span><span class="sxs-lookup"><span data-stu-id="7e348-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="7e348-233">Sea productivo y esté protegido en cualquier lugar, con cualquier dispositivo y a un bajo costo de TI.</span><span class="sxs-lookup"><span data-stu-id="7e348-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="7e348-234">Caase.com es un verdadero especialista en Microsoft Office365, Azure, Enterprise Mobility and Security y Windows.</span><span class="sxs-lookup"><span data-stu-id="7e348-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="7e348-235">Con nuestra asesoría, servicios de migración, programas de adopción, aprendizaje, administración y respaldo, Caase.com crea una plataforma optimizada y segura de colaboración entre los proveedores, asociados y empleados de los clientes.</span><span class="sxs-lookup"><span data-stu-id="7e348-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="7e348-236">Caase.com es mastermind Hola de hello al área de trabajo Digital (sociales Intranet) y hello Azure remoto Workspace (área de trabajo móvil).</span><span class="sxs-lookup"><span data-stu-id="7e348-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="7e348-237">Ambas soluciones: llevar a cabo con la adopción: son foundation Hola que garantiza que los usuarios de Hola de estas soluciones tienen experiencia más agradable, correcta y eficaz de hello en su toohello ruta Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="7e348-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="7e348-238">Aquí puede encontrar una traducción al neerlandés y una película de respaldo: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="7e348-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="7e348-239">Región de la operación: empresa neerlandesa con alcance mundial</span><span class="sxs-lookup"><span data-stu-id="7e348-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="7e348-240">Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="7e348-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="7e348-241">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="7e348-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="7e348-242">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="7e348-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="7e348-243">Soluciones de migración de Azure RemoteApp: sí [(más información)](http://caase.com/diensten/microsoft-azure/)</span><span class="sxs-lookup"><span data-stu-id="7e348-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="7e348-244">Países Bajos:</span><span class="sxs-lookup"><span data-stu-id="7e348-244">Netherlands:</span></span>
> 
> <span data-ttu-id="7e348-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="7e348-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="7e348-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="7e348-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="7e348-247">Teléfono: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="7e348-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="7e348-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="7e348-248">Nerdio</span></span>
<span data-ttu-id="7e348-249">[Nerdio para Azure](http://getnerdio.com/nfa/) es una plataforma de automatización de TI que ofrece provisioning demasiado simple, administración y optimización de los entornos de TI completos en hello nube de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7e348-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="7e348-250">Optimice escritorios virtuales, aplicaciones remotas y servidores en un par de horas.</span><span class="sxs-lookup"><span data-stu-id="7e348-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="7e348-251">Administrar el entorno de hello en tres clics o menor con Nerdio del Portal de administración.</span><span class="sxs-lookup"><span data-stu-id="7e348-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="7e348-252">Usar inteligente la escala automática y guarde el 40% de too60 en recursos de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e348-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="7e348-253">Ubicación principal: Chicago, IL Región de la operación: en todo el mundo Estado de asociado: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Proveedor de servicios en Microsoft Cloud: sí</span><span class="sxs-lookup"><span data-stu-id="7e348-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="7e348-254">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="7e348-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="7e348-255">Soluciones de migración de Azure RemoteApp: sí</span><span class="sxs-lookup"><span data-stu-id="7e348-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="7e348-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="7e348-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="7e348-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="7e348-257">Suite 212</span></span>
> 
> <span data-ttu-id="7e348-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="7e348-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="7e348-259">EE. UU.</span><span class="sxs-lookup"><span data-stu-id="7e348-259">USA</span></span>
> 
> <span data-ttu-id="7e348-260">(844) 4NERDIO ext. 6</span><span class="sxs-lookup"><span data-stu-id="7e348-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="7e348-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="7e348-261">**SaaSplaza**</span></span>
<span data-ttu-id="7e348-262">[SaaSplaza](http://www.saasplaza.com/) ofrece las soluciones en la nube públicas y privadas (Azure) de la cartera completa de Microsoft Dynamics (NAV, AX, GP, SL y CRM).</span><span class="sxs-lookup"><span data-stu-id="7e348-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="7e348-263">Ubicación principal: Países bajos</span><span class="sxs-lookup"><span data-stu-id="7e348-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="7e348-264">Región operativa: en todo el mundo</span><span class="sxs-lookup"><span data-stu-id="7e348-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="7e348-265">Estado de asociado: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="7e348-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="7e348-266">Proveedor de servicios en la nube de Microsoft: sí</span><span class="sxs-lookup"><span data-stu-id="7e348-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="7e348-267">Oferta de soluciones de RemoteApp y escritorio basadas en sesiones: Sí, ambas</span><span class="sxs-lookup"><span data-stu-id="7e348-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="7e348-268">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="7e348-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="7e348-269">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="7e348-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="7e348-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="7e348-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="7e348-271">Hola países bajos</span><span class="sxs-lookup"><span data-stu-id="7e348-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="7e348-272">Teléfono: + 31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="7e348-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="7e348-273">**América**:</span><span class="sxs-lookup"><span data-stu-id="7e348-273">**Americas**:</span></span>
> 
> <span data-ttu-id="7e348-274">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="7e348-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="7e348-275">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="7e348-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="7e348-276">San Diego</span><span class="sxs-lookup"><span data-stu-id="7e348-276">San Diego</span></span>
> 
> <span data-ttu-id="7e348-277">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="7e348-277">United States</span></span>
> 
> <span data-ttu-id="7e348-278">Teléfono: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="7e348-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="7e348-279">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="7e348-279">**APAC**:</span></span>
> 
> <span data-ttu-id="7e348-280">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="7e348-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="7e348-281">\#11-08, Hola octágono</span><span class="sxs-lookup"><span data-stu-id="7e348-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="7e348-282">Singapur 069534</span><span class="sxs-lookup"><span data-stu-id="7e348-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="7e348-283">Singapur</span><span class="sxs-lookup"><span data-stu-id="7e348-283">Singapore</span></span>
>   
> <span data-ttu-id="7e348-284">Teléfono (Singapur): + 65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="7e348-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="7e348-285">Teléfono (Australia): + 61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="7e348-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="7e348-286">Teléfono (Nueva Zelanda): + 64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="7e348-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="7e348-287">¿Necesita más ayuda?</span><span class="sxs-lookup"><span data-stu-id="7e348-287">Need more help?</span></span>
<span data-ttu-id="7e348-288">¿Todavía necesita ayuda para decidirse o tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="7e348-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="7e348-289">Utilice uno de hello siguiendo métodos tooget ayuda.</span><span class="sxs-lookup"><span data-stu-id="7e348-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="7e348-290">Envíenos un correo electrónico a [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7e348-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="7e348-291">Póngase en contacto con el equipo de [soporte técnico de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="7e348-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="7e348-292">Comience abriendo un [caso de soporte técnico de Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="7e348-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="7e348-293">Llámenos.</span><span class="sxs-lookup"><span data-stu-id="7e348-293">Call us.</span></span> <span data-ttu-id="7e348-294">[Encuentre un número de ventas local](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="7e348-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

