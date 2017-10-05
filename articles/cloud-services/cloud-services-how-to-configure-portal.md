---
title: "Configuración de un servicio en la nube (portal) | Microsoft Docs"
description: "Aprenda a configurar servicios en la nube en Azure. Aprenda a actualizar la configuración del servicio en la nube y configurar el acceso remoto en instancias de rol. Estos ejemplos usan el Portal de Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: a7e891d05ffe4cc2b4f68dce072a81499cc6de80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="db623-105">Configuración de servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="db623-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db623-106">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="db623-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="db623-107">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="db623-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="db623-108">Puede configurar la mayoría de los ajustes más usados para un servicio en la nube en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="db623-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="db623-109">O bien, si desea actualizar los archivos de configuración directamente, descargue un archivo de configuración de servicio para actualizar y, a continuación, cargue el archivo actualizado y actualice el servicio en la nube con los cambios en la configuración.</span><span class="sxs-lookup"><span data-stu-id="db623-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="db623-110">De cualquier manera, las actualizaciones de la configuración se realizan en todas las instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="db623-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="db623-111">También puede administrar las instancias de los roles de servicio en la nube o conectarse mediante Escritorio remoto a ellas.</span><span class="sxs-lookup"><span data-stu-id="db623-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="db623-112">Azure solo puede asegurar un 99,95 % de disponibilidad del servicio durante las actualizaciones de la configuración si tiene al menos dos instancias de rol para cada rol.</span><span class="sxs-lookup"><span data-stu-id="db623-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="db623-113">Esto permite que una máquina virtual procese las solicitudes del cliente mientras la otra se actualiza.</span><span class="sxs-lookup"><span data-stu-id="db623-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="db623-114">Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="db623-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="db623-115">Cambiar un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="db623-115">Change a cloud service</span></span>
<span data-ttu-id="db623-116">Después de abrir el [Portal de Azure](https://portal.azure.com/), vaya al servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="db623-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="db623-117">Desde aquí puede administrar muchos aspectos de este.</span><span class="sxs-lookup"><span data-stu-id="db623-117">From here, you manage many aspects of it.</span></span>

![Página de configuración](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="db623-119">Los vínculos de **Configuración** o **Toda la configuración** se abrirán en la hoja **Configuración** donde podrá cambiar las **propiedades**, cambiar la **configuración**, administrar los **certificados**, instalar las **reglas de alerta**, y administrar los **usuarios** que tienen acceso a este servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="db623-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Hoja de configuración del servicio en la nube de Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="db623-121">Administración de la versión del SO invitado</span><span class="sxs-lookup"><span data-stu-id="db623-121">Manage Guest OS version</span></span>

<span data-ttu-id="db623-122">De forma predeterminada, Azure actualiza periódicamente el sistema operativo invitado a la imagen compatible más reciente dentro de la familia del SO que ha especificado en la configuración del servicio (.cscfg), como Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="db623-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="db623-123">Si tiene como destino una versión de sistema operativo específica, puede establecerla en la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="db623-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![Establecimiento de la versión del sistema operativo](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="db623-125">Si elige una versión específica del sistema operativo deshabilitará las actualizaciones automáticas y hará que la aplicación de revisiones sea responsabilidad suya.</span><span class="sxs-lookup"><span data-stu-id="db623-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="db623-126">Debe asegurarse de que las instancias de rol están recibiendo actualizaciones o puede exponer su aplicación a las vulnerabilidades de seguridad.</span><span class="sxs-lookup"><span data-stu-id="db623-126">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="db623-127">Supervisión</span><span class="sxs-lookup"><span data-stu-id="db623-127">Monitoring</span></span>
<span data-ttu-id="db623-128">Puede agregar alertas a su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="db623-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="db623-129">Haga clic en **Configuración** > **Reglas de alerta** > **Agregar alerta**.</span><span class="sxs-lookup"><span data-stu-id="db623-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="db623-130">Desde aquí puede configurar una alerta.</span><span class="sxs-lookup"><span data-stu-id="db623-130">From here, you can setup an alert.</span></span> <span data-ttu-id="db623-131">Mediante el cuadro desplegable **Mertic** , puede configurar una alerta para los siguientes tipos de datos.</span><span class="sxs-lookup"><span data-stu-id="db623-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="db623-132">Lectura de disco</span><span class="sxs-lookup"><span data-stu-id="db623-132">Disk read</span></span>
* <span data-ttu-id="db623-133">Escritura de disco</span><span class="sxs-lookup"><span data-stu-id="db623-133">Disk write</span></span>
* <span data-ttu-id="db623-134">Red interna</span><span class="sxs-lookup"><span data-stu-id="db623-134">Network in</span></span>
* <span data-ttu-id="db623-135">Red externa</span><span class="sxs-lookup"><span data-stu-id="db623-135">Network out</span></span>
* <span data-ttu-id="db623-136">Porcentaje de CPU</span><span class="sxs-lookup"><span data-stu-id="db623-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="db623-137">Configuración de la supervisión desde un icono de métrica</span><span class="sxs-lookup"><span data-stu-id="db623-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="db623-138">En lugar de usar **Configuración** > **Reglas de alerta**, puede hacer clic en uno de los iconos de métrica en la sección **Supervisión** de la hoja **Servicio en la nube**.</span><span class="sxs-lookup"><span data-stu-id="db623-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![Supervisión de servicios en la nube](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="db623-140">Desde aquí puede personalizar el gráfico que se usa con el icono o agregar una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="db623-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="db623-141">Reinicio, restablecimiento de imagen inicial o conexión mediante Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="db623-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="db623-142">En este momento no se puede configurar el Escritorio remoto con el **Portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="db623-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="db623-143">Sin embargo, se puede configurar a través del [Portal de Azure clásico](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md) o mediante [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="db623-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="db623-144">Primero, haga clic en la instancia de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="db623-144">First, click on the cloud service instance.</span></span>

![Instancia del servicio en la nube](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="db623-146">En la hoja que se abre, puede iniciar una conexión de escritorio remoto, reiniciar la instancia de forma remota o restablecer la imagen inicial de forma remota (empieza con una imagen nueva) de la instancia.</span><span class="sxs-lookup"><span data-stu-id="db623-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![Botones de instancia del servicio en la nube](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="db623-148">Reconfiguración del archivo .cscfg</span><span class="sxs-lookup"><span data-stu-id="db623-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="db623-149">Puede que necesite volver a configurar el servicio en la nube a través del archivo de [configuración de servicio (cscfg)](cloud-services-model-and-package.md#cscfg) .</span><span class="sxs-lookup"><span data-stu-id="db623-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="db623-150">Primero debe descargar el archivo .cscfg, modificarlo y volverlo a cargar.</span><span class="sxs-lookup"><span data-stu-id="db623-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="db623-151">Haga clic en el icono **Configuración** o el vínculo **Toda la configuración** para abrir la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="db623-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![Página de configuración](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="db623-153">Haga clic en el elemento **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="db623-153">Click on the **Configuration** item.</span></span>

    ![Hoja de configuración](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="db623-155">Haga clic en el botón **Descargar** .</span><span class="sxs-lookup"><span data-stu-id="db623-155">Click on the **Download** button.</span></span>

    ![Descargar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="db623-157">Después de actualizar el archivo de configuración del servicio, cargue y aplique las actualizaciones de la configuración:</span><span class="sxs-lookup"><span data-stu-id="db623-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![Cargar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="db623-159">Seleccione el archivo .cscfg y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="db623-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db623-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db623-160">Next steps</span></span>
* <span data-ttu-id="db623-161">Obtenga información sobre cómo [implementar un servicio en la nube](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db623-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="db623-162">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db623-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="db623-163">[Administración de su servicio en la nube](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db623-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="db623-164">Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db623-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
