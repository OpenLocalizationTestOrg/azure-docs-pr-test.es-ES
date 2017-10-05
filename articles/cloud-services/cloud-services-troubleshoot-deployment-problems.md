---
title: "Solución de problemas de implementación de servicios en la nube | Microsoft Docs"
description: "Hay varios problemas comunes que pueden surgir al implementar servicios en la nube en Azure. Este artículo proporciona soluciones a algunos de ellos."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 60e06ba292ff1e43d00cd69c1a422f9237d5e5a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a><span data-ttu-id="2c49a-104">Solución de problemas de implementación de servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="2c49a-104">Troubleshoot cloud service deployment problems</span></span>
<span data-ttu-id="2c49a-105">Al implementar un paquete de aplicación del servicio en la nube en Azure, puede obtener información sobre la implementación en el panel **Propiedades** del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2c49a-105">When you deploy a cloud service application package to Azure, you can obtain information about the deployment from the **Properties** pane in the Azure portal.</span></span> <span data-ttu-id="2c49a-106">Puede usar los detalles de este panel para ayudarle a solucionar problemas con el servicio en la nube y proporcionar esta información al soporte técnico de Azure al abrir una nueva solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="2c49a-106">You can use the details in this pane to help you troubleshoot problems with the cloud service, and you can provide this information to Azure Support when opening a new support request.</span></span>

<span data-ttu-id="2c49a-107">Puede encontrar el panel **Propiedades** panel de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="2c49a-107">You can find the **Properties** pane as follows:</span></span>

* <span data-ttu-id="2c49a-108">En Azure Portal, haga clic en la implementación del servicio en la nube, haga clic en **Toda la configuración** y después en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2c49a-108">In the Azure portal, click the deployment of your cloud service, click **All settings**, and then click **Properties**.</span></span>
* <span data-ttu-id="2c49a-109">En el Portal de Azure clásico, haga clic en la implementación del servicio en la nube y después en **PANEL**, que se encuentra en la esquina inferior derecha de la página (debajo de **vista rápida**).</span><span class="sxs-lookup"><span data-stu-id="2c49a-109">In the Azure classic portal, click the deployment of your cloud service, click **DASHBOARD**, located at the lower-right corner of the page (under **quick glance**).</span></span> <span data-ttu-id="2c49a-110">Tenga en cuenta que en este panel no hay ninguna etiqueta "Propiedades".</span><span class="sxs-lookup"><span data-stu-id="2c49a-110">Be aware that there's no "Properties" label on this pane.</span></span>

> [!NOTE]
> <span data-ttu-id="2c49a-111">El contenido del panel **Propiedades** se puede copiar en el Portapapeles. Para ello, es preciso hacer clic en el icono de la esquina superior derecha del panel.</span><span class="sxs-lookup"><span data-stu-id="2c49a-111">You can copy the contents of the **Properties** pane to the clipboard by clicking the icon in the upper-right corner of the pane.</span></span>
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a><span data-ttu-id="2c49a-112">Problema: no puedo acceder a mi sitio web, pero la implementación se ha iniciado y todas las instancias de rol están listas</span><span class="sxs-lookup"><span data-stu-id="2c49a-112">Problem: I cannot access my website, but my deployment is started and all role instances are ready</span></span>
<span data-ttu-id="2c49a-113">El vínculo de la dirección URL del sitio web que se muestra en el portal no incluye el puerto.</span><span class="sxs-lookup"><span data-stu-id="2c49a-113">The website URL link shown in the portal does not include the port.</span></span> <span data-ttu-id="2c49a-114">El puerto predeterminado para los sitios web es 80.</span><span class="sxs-lookup"><span data-stu-id="2c49a-114">The default port for websites is 80.</span></span> <span data-ttu-id="2c49a-115">Si la aplicación está configurada para ejecutarse en otro puerto, debe agregar el puerto correcto a la dirección URL al acceder al sitio web.</span><span class="sxs-lookup"><span data-stu-id="2c49a-115">If your application is configured to run in a different port, you must add the correct port number to the URL when accessing the website.</span></span>

1. <span data-ttu-id="2c49a-116">En el Portal de Azure, haga clic en la implementación del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="2c49a-116">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="2c49a-117">En el panel **Propiedades** de Azure Portal, compruebe los puertos de las instancias de rol (en **Puntos de conexión de entrada**).</span><span class="sxs-lookup"><span data-stu-id="2c49a-117">In the **Properties** pane of the Azure portal, check the ports for the role instances (under **Input Endpoints**).</span></span>
3. <span data-ttu-id="2c49a-118">Si el puerto no es el 80, agregue el valor de puerto correcto para la dirección URL al acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2c49a-118">If the port is not 80, add the correct port value to the URL when you access the application.</span></span> <span data-ttu-id="2c49a-119">Para especificar un puerto no predeterminado, escriba la dirección URL, seguida de dos puntos (:) y del número de puerto, sin espacios.</span><span class="sxs-lookup"><span data-stu-id="2c49a-119">To specify a non-default port, type the URL, followed by a colon (:), followed by the port number, with no spaces.</span></span>

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a><span data-ttu-id="2c49a-120">Problema: mis instancias de rol se reciclan automáticamente</span><span class="sxs-lookup"><span data-stu-id="2c49a-120">Problem: My role instances recycled without me doing anything</span></span>
<span data-ttu-id="2c49a-121">Se produce automáticamente una recuperación del servicio cuando Azure detecta nodos con problemas y, por consiguiente, mueve instancias de rol a nodos nuevos.</span><span class="sxs-lookup"><span data-stu-id="2c49a-121">Service healing occurs automatically when Azure detects problem nodes and therefore moves role instances to new nodes.</span></span> <span data-ttu-id="2c49a-122">Cuando esto ocurre, puede que vea que las instancias de rol se reciclan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2c49a-122">When this occurs, you might see your role instances recycling automatically.</span></span> <span data-ttu-id="2c49a-123">Para averiguar si se produjo la recuperación del servicio:</span><span class="sxs-lookup"><span data-stu-id="2c49a-123">To find out if service healing occurred:</span></span>

1. <span data-ttu-id="2c49a-124">En el Portal de Azure, haga clic en la implementación del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="2c49a-124">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="2c49a-125">En el panel **Propiedades** del Portal de Azure, revise la información y determine si la recuperación del servicio se produjo mientras observaba el reciclaje de roles.</span><span class="sxs-lookup"><span data-stu-id="2c49a-125">In the **Properties** pane of the Azure portal, review the information and determine whether service healing occurred during the time that you observed the roles recycling.</span></span>

<span data-ttu-id="2c49a-126">Los roles también se reciclarán aproximadamente una vez al mes durante las actualizaciones del sistema operativo del host y del sistema operativo invitado.</span><span class="sxs-lookup"><span data-stu-id="2c49a-126">Roles will also recycle roughly once per month during host-OS and guest-OS updates.</span></span>  
<span data-ttu-id="2c49a-127">Para obtener más información, consulte la entrada del blog [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span><span class="sxs-lookup"><span data-stu-id="2c49a-127">For more information, see the blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)</span></span>

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a><span data-ttu-id="2c49a-128">Problema: No puedo realizar un intercambio de VIP y recibo un error</span><span class="sxs-lookup"><span data-stu-id="2c49a-128">Problem: I cannot do a VIP swap and receive an error</span></span>
<span data-ttu-id="2c49a-129">No se permite un intercambio de VIP si una actualización de implementación está en curso.</span><span class="sxs-lookup"><span data-stu-id="2c49a-129">A VIP swap is not allowed if a deployment update is in progress.</span></span> <span data-ttu-id="2c49a-130">Las actualizaciones de implementación pueden ocurrir automáticamente cuando:</span><span class="sxs-lookup"><span data-stu-id="2c49a-130">Deployment updates can occur automatically when:</span></span>

* <span data-ttu-id="2c49a-131">Hay un nuevo sistema operativo invitado y ha configurado actualizaciones automáticas</span><span class="sxs-lookup"><span data-stu-id="2c49a-131">A new guest operating system is available and you are configured for automatic updates.</span></span>
* <span data-ttu-id="2c49a-132">Se produce una recuperación de servicio.</span><span class="sxs-lookup"><span data-stu-id="2c49a-132">Service healing occurs.</span></span>

<span data-ttu-id="2c49a-133">Para averiguar si alguna actualización automática impide la realización de un intercambio de VIP:</span><span class="sxs-lookup"><span data-stu-id="2c49a-133">To find out if an automatic update is preventing you from doing a VIP swap:</span></span>

1. <span data-ttu-id="2c49a-134">En el Portal de Azure, haga clic en la implementación del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="2c49a-134">In the Azure portal, click the deployment of your cloud service.</span></span>
2. <span data-ttu-id="2c49a-135">En el panel **Propiedades** de Azure Portal, examine el valor de **Estado**.</span><span class="sxs-lookup"><span data-stu-id="2c49a-135">In the **Properties** pane of the Azure portal, look at the value of **Status**.</span></span> <span data-ttu-id="2c49a-136">Si es **Listo**, compruebe **Última operación** para ver si hubo recientemente alguna que pudo impedir el intercambio de VIP.</span><span class="sxs-lookup"><span data-stu-id="2c49a-136">If it is **Ready**, then check **Last operation** to see if one recently happened that might prevent the VIP swap.</span></span>
3. <span data-ttu-id="2c49a-137">Repita los pasos 1 y 2 para la implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="2c49a-137">Repeat steps 1 and 2 for the production deployment.</span></span>
4. <span data-ttu-id="2c49a-138">Si una actualización automática está en curso, espere a que finalice antes de intentar realizar el intercambio de VIP.</span><span class="sxs-lookup"><span data-stu-id="2c49a-138">If an automatic update is in process, wait for it to finish before trying to do the VIP swap.</span></span>

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a><span data-ttu-id="2c49a-139">Problema: Una instancia de rol entra en un bucle entre Iniciado, Inicializando, Ocupado y Detenido</span><span class="sxs-lookup"><span data-stu-id="2c49a-139">Problem: A role instance is looping between Started, Initializing, Busy, and Stopped</span></span>
<span data-ttu-id="2c49a-140">Esta condición puede indicar un problema con el código de la aplicación, el paquete o el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="2c49a-140">This condition could indicate a problem with your application code, package, or configuration file.</span></span> <span data-ttu-id="2c49a-141">En ese caso, podría ver que el estado cambia cada pocos minutos y en Azure Portal puede aparecer algo como **Reciclando**, **Ocupado** o **Inicializando**.</span><span class="sxs-lookup"><span data-stu-id="2c49a-141">In that case, you should be able to see the status changing every few minutes and the Azure portal may say something like **Recycling**, **Busy**, or **Initializing**.</span></span> <span data-ttu-id="2c49a-142">Esto indica que hay algún problema con la aplicación que impide que la instancia de rol se ejecute.</span><span class="sxs-lookup"><span data-stu-id="2c49a-142">This indicates that there is something wrong with the application that is keeping the role instance from running.</span></span>

<span data-ttu-id="2c49a-143">Para más información acerca de cómo solucionar este problema, consulte la entrada de blog [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) (Datos de diagnóstico de proceso de PaaS de Azure) y [Problemas comunes que causan el reciclaje de los roles](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span><span class="sxs-lookup"><span data-stu-id="2c49a-143">For more information on how to troubleshoot for this problem, see the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) and [Common issues that cause roles to recycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

## <a name="problem-my-application-stopped-working"></a><span data-ttu-id="2c49a-144">Problema: Mi aplicación dejó de funcionar</span><span class="sxs-lookup"><span data-stu-id="2c49a-144">Problem: My application stopped working</span></span>
1. <span data-ttu-id="2c49a-145">En el Portal de Azure, haga clic en la instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="2c49a-145">In the Azure portal, click the role instance.</span></span>
2. <span data-ttu-id="2c49a-146">En el panel **Propiedades** del Portal de Azure, tenga en cuenta las condiciones siguientes para resolver el problema:</span><span class="sxs-lookup"><span data-stu-id="2c49a-146">In the **Properties** pane of the Azure portal, consider the following conditions to resolve your problem:</span></span>
   * <span data-ttu-id="2c49a-147">Si la instancia de rol se detuvo recientemente (puede comprobar el valor de **Recuento de anulados**), la implementación puede estar actualizándose.</span><span class="sxs-lookup"><span data-stu-id="2c49a-147">If the role instance has recently stopped (you can check the value of **Abort count**), the deployment could be updating.</span></span> <span data-ttu-id="2c49a-148">Espere para ver si la instancia de rol reanuda el funcionamiento por sí misma.</span><span class="sxs-lookup"><span data-stu-id="2c49a-148">Wait to see if the role instance resumes functioning on its own.</span></span>
   * <span data-ttu-id="2c49a-149">Si la instancia de rol está en estado **Ocupado**, compruebe el código de aplicación para ver si se controla el evento [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) .</span><span class="sxs-lookup"><span data-stu-id="2c49a-149">If the role instance is **Busy**, check your application code to see if the [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) event is handled.</span></span> <span data-ttu-id="2c49a-150">Debe agregar o corregir el código que controla este evento.</span><span class="sxs-lookup"><span data-stu-id="2c49a-150">You might need to add or fix some code that handles this event.</span></span>
   * <span data-ttu-id="2c49a-151">Revise los datos de diagnóstico y los escenarios de solución de problemas en la entrada del blog [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)(Datos de diagnóstico de proceso de PaaS de Azure).</span><span class="sxs-lookup"><span data-stu-id="2c49a-151">Go through the diagnostic data and troubleshooting scenarios in the blog post [Azure PaaS Compute Diagnostics Data](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="2c49a-152">Si recicla el servicio en la nube, se restablecen las propiedades de la implementación, con lo que se elimina eficazmente la información del problema original.</span><span class="sxs-lookup"><span data-stu-id="2c49a-152">If you recycle your cloud service, you reset the properties for the deployment, effectively erasing the information for the original problem.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2c49a-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2c49a-153">Next steps</span></span>
<span data-ttu-id="2c49a-154">Vea más [artículos de solución de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="2c49a-154">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="2c49a-155">Para más información acerca de cómo solucionar los problemas de los roles de los servicios en la nube mediante el uso de datos de diagnóstico de equipos de PaaS de Azure, consulte la [serie de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c49a-155">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>