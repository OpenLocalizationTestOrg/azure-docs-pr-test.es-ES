---
title: aaaHow tooconfigure un servicio de nube (portal) | Documentos de Microsoft
description: "Obtenga información acerca de cómo servicios en la nube tooconfigure en Azure. Obtenga información acerca de la configuración del servicio de nube de tooupdate hello y configurar instancias de toorole de acceso remoto. Estos ejemplos utilizan Hola portal de Azure."
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
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="ad404-105">Cómo tooConfigure los servicios de nube</span><span class="sxs-lookup"><span data-stu-id="ad404-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad404-106">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ad404-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="ad404-107">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="ad404-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="ad404-108">Puede configurar valores de hello suelen usada para un servicio de nube en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad404-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="ad404-109">O bien, si le gusta tooupdate los archivos de configuración directamente, descargar una tooupdate de archivo de configuración de servicio y, a continuación, cargar Hola Actualizar archivo y actualización Hola servicio en la nube con los cambios de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad404-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="ad404-110">En cualquier caso, se insertan las actualizaciones de configuración de hello tooall instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="ad404-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="ad404-111">También puede administrar instancias de Hola de los roles de servicio de nube o el escritorio remoto en ellos.</span><span class="sxs-lookup"><span data-stu-id="ad404-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="ad404-112">Azure solo puede asegurar de disponibilidad de servicio del 99,95 por ciento durante hello las actualizaciones de configuración si tiene al menos dos instancias de rol para cada rol.</span><span class="sxs-lookup"><span data-stu-id="ad404-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="ad404-113">Que permite las solicitudes de cliente de tooprocess de máquina virtual mientras se está actualizando Hola otro.</span><span class="sxs-lookup"><span data-stu-id="ad404-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="ad404-114">Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="ad404-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="ad404-115">Cambiar un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="ad404-115">Change a cloud service</span></span>
<span data-ttu-id="ad404-116">Después de abrir hello [portal de Azure](https://portal.azure.com/), navegar por el servicio en la nube tooyour.</span><span class="sxs-lookup"><span data-stu-id="ad404-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="ad404-117">Desde aquí puede administrar muchos aspectos de este.</span><span class="sxs-lookup"><span data-stu-id="ad404-117">From here, you manage many aspects of it.</span></span>

![Página de configuración](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="ad404-119">Hola **configuración** o **toda la configuración de** vínculos se abrirán hello **configuración** hoja donde puedes cambiar hello **propiedades**, cambiar Hola **Configuración**, administrar hello **certificados**, el programa de instalación **reglas de alerta**y administrar hello **usuarios** que tienen acceso toothis servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="ad404-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Hoja de configuración del servicio en la nube de Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="ad404-121">Administración de la versión del SO invitado</span><span class="sxs-lookup"><span data-stu-id="ad404-121">Manage Guest OS version</span></span>

<span data-ttu-id="ad404-122">De forma predeterminada, Azure actualiza periódicamente la toohello más reciente compatible imagen del SO invitado en hello familia del SO que haya especificado en la configuración del servicio (.cscfg), como Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ad404-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="ad404-123">Si necesita tootarget una versión específica del sistema operativo, puede establecerlo en hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="ad404-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Establecimiento de la versión del sistema operativo](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="ad404-125">Si elige una versión específica del sistema operativo deshabilitará las actualizaciones automáticas y hará que la aplicación de revisiones sea responsabilidad suya.</span><span class="sxs-lookup"><span data-stu-id="ad404-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="ad404-126">Debe asegurarse de que las instancias de rol están recibiendo actualizaciones o puede exponer sus vulnerabilidades de toosecurity de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad404-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="ad404-127">Supervisión</span><span class="sxs-lookup"><span data-stu-id="ad404-127">Monitoring</span></span>
<span data-ttu-id="ad404-128">Puede agregar el servicio de alertas tooyour en la nube.</span><span class="sxs-lookup"><span data-stu-id="ad404-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="ad404-129">Haga clic en **Configuración** > **Reglas de alerta** > **Agregar alerta**.</span><span class="sxs-lookup"><span data-stu-id="ad404-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="ad404-130">Desde aquí puede configurar una alerta.</span><span class="sxs-lookup"><span data-stu-id="ad404-130">From here, you can setup an alert.</span></span> <span data-ttu-id="ad404-131">Con hello **métrica** cuadro de lista desplegable, puede configurar una alerta para hello siguientes tipos de datos.</span><span class="sxs-lookup"><span data-stu-id="ad404-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="ad404-132">Lectura de disco</span><span class="sxs-lookup"><span data-stu-id="ad404-132">Disk read</span></span>
* <span data-ttu-id="ad404-133">Escritura de disco</span><span class="sxs-lookup"><span data-stu-id="ad404-133">Disk write</span></span>
* <span data-ttu-id="ad404-134">Red interna</span><span class="sxs-lookup"><span data-stu-id="ad404-134">Network in</span></span>
* <span data-ttu-id="ad404-135">Red externa</span><span class="sxs-lookup"><span data-stu-id="ad404-135">Network out</span></span>
* <span data-ttu-id="ad404-136">Porcentaje de CPU</span><span class="sxs-lookup"><span data-stu-id="ad404-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="ad404-137">Configuración de la supervisión desde un icono de métrica</span><span class="sxs-lookup"><span data-stu-id="ad404-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="ad404-138">En lugar de usar **configuración** > **reglas de alerta**, puede hacer clic en uno de los mosaicos de métrica de Hola Hola **supervisión** sección de hello **en la nube servicio** hoja.</span><span class="sxs-lookup"><span data-stu-id="ad404-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Supervisión de servicios en la nube](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="ad404-140">Desde aquí puede personalizar el gráfico de Hola que se usa con icono de hello, o agregar una regla de alerta.</span><span class="sxs-lookup"><span data-stu-id="ad404-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="ad404-141">Reinicio, restablecimiento de imagen inicial o conexión mediante Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="ad404-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="ad404-142">En este momento no se puede configurar Escritorio remoto con hello **portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="ad404-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="ad404-143">Sin embargo, puede configurarlo a través de hello [portal de Azure clásico](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), o a través [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ad404-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="ad404-144">En primer lugar, haga clic en la instancia de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad404-144">First, click on hello cloud service instance.</span></span>

![Instancia del servicio en la nube](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="ad404-146">De hello hoja que se abrirá, puede iniciar una conexión a escritorio remota, reiniciar la instancia de Hola o de forma remota instancia Hola de restablecimiento de imagen inicial (comenzar con una nueva imagen) de forma remota.</span><span class="sxs-lookup"><span data-stu-id="ad404-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Botones de instancia del servicio en la nube](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="ad404-148">Reconfiguración del archivo .cscfg</span><span class="sxs-lookup"><span data-stu-id="ad404-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="ad404-149">Puede que necesite tooreconfigure su servicio de nube a través de hello [la configuración de servicio (cscfg)](cloud-services-model-and-package.md#cscfg) archivo.</span><span class="sxs-lookup"><span data-stu-id="ad404-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="ad404-150">En primer lugar debe toodownload su .cscfg de archivo, modificarlo y cargarlo.</span><span class="sxs-lookup"><span data-stu-id="ad404-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="ad404-151">Haga clic en hello **configuración** icono o hello **toda la configuración de** vincular tooopen seguridad hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="ad404-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Página de configuración](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="ad404-153">Haga clic en hello **configuración** elemento.</span><span class="sxs-lookup"><span data-stu-id="ad404-153">Click on hello **Configuration** item.</span></span>

    ![Hoja de configuración](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="ad404-155">Haga clic en hello **descargar** botón.</span><span class="sxs-lookup"><span data-stu-id="ad404-155">Click on hello **Download** button.</span></span>

    ![Descargar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="ad404-157">Después de actualizar el archivo de configuración de servicio de hello, cargar y aplicar las actualizaciones de configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="ad404-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Cargar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="ad404-159">Seleccione el archivo de .cscfg de hello y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ad404-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad404-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad404-160">Next steps</span></span>
* <span data-ttu-id="ad404-161">Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ad404-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="ad404-162">Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ad404-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="ad404-163">[Administración de su servicio en la nube](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ad404-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="ad404-164">Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ad404-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
