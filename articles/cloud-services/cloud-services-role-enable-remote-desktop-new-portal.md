---
title: "aaaEnable conexión a Escritorio remoto para un rol de servicios de nube de Azure | Documentos de Microsoft"
description: "¿Cómo tooconfigure la nube de azure conexiones de escritorio remoto de tooallow de aplicación de servicio"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="06ffb-103">Habilitación de la conexión a Escritorio remoto para un rol de Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="06ffb-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06ffb-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="06ffb-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="06ffb-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="06ffb-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="06ffb-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06ffb-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="06ffb-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="06ffb-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="06ffb-108">Escritorio remoto permite escritorio de hello tooaccess de una función que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="06ffb-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="06ffb-109">Puede usar un tootroubleshoot de conexión de escritorio remoto y diagnosticar problemas con la aplicación mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="06ffb-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="06ffb-110">Puede habilitar una conexión a Escritorio remoto en el rol durante el desarrollo mediante la inclusión de módulos de escritorio remoto de hello en la definición de servicio o puede elegir tooenable escritorio remoto a través de hello extensión de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="06ffb-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="06ffb-111">Hello método preferido es extensión de escritorio remoto de hello toouse tal y como se puede habilitar Escritorio remoto incluso después de que se implementa la aplicación hello sin necesidad de tooredeploy la aplicación.</span><span class="sxs-lookup"><span data-stu-id="06ffb-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="06ffb-112">Configurar Escritorio remoto desde Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="06ffb-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="06ffb-113">Hola portal de Azure utiliza el método de extensión de escritorio remoto de Hola por lo que puede habilitar Escritorio remoto incluso después de que se implementa la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="06ffb-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="06ffb-114">Hola **escritorio remoto** hoja para el servicio de nube permite tooenable escritorio remoto, Hola cambiar cuenta de administrador local usa máquinas virtuales de tooconnect toohello, certificado Hola utilizada en la autenticación y establece Hola fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="06ffb-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="06ffb-115">Haga clic en **servicios en la nube**, haga clic en nombre de hello del servicio de nube de hello y, a continuación, haga clic en **escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="06ffb-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="06ffb-117">Elija si desea tooenable escritorio remoto para un rol individual o para todos los roles, a continuación, cambie el valor de Hola de modificador de hello demasiado**habilitado**.</span><span class="sxs-lookup"><span data-stu-id="06ffb-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="06ffb-118">Rellene los campos de hello necesario para el nombre de usuario, contraseña, expiración y el certificado.</span><span class="sxs-lookup"><span data-stu-id="06ffb-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="06ffb-120">se reiniciarán todas las instancias de rol la primera vez que habilite el Escritorio remoto y haga clic en Aceptar (marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="06ffb-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="06ffb-121">tooprevent un reinicio, contraseña de Hola de hello certificado tooencrypt usado debe estar instalado en el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="06ffb-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="06ffb-122">tooprevent un reinicio, [cargar un certificado de servicio en la nube hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) y, a continuación, devolver toothis cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="06ffb-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="06ffb-123">En **Roles**, seleccione el rol de Hola que desee tooupdate o seleccione **todos los** para todos los roles.</span><span class="sxs-lookup"><span data-stu-id="06ffb-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="06ffb-124">Después de terminar las actualizaciones de la configuración, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="06ffb-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="06ffb-125">Tardará unos minutos antes de que las instancias del rol son conexiones tooreceive listo.</span><span class="sxs-lookup"><span data-stu-id="06ffb-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="06ffb-126">Acceso remoto en instancias de rol</span><span class="sxs-lookup"><span data-stu-id="06ffb-126">Remote into role instances</span></span>
<span data-ttu-id="06ffb-127">Una vez que Escritorio remoto está habilitado en los roles de hello, puede iniciar una conexión directamente desde Hola Portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="06ffb-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="06ffb-128">Haga clic en **instancias** tooopen hello **instancias** hoja.</span><span class="sxs-lookup"><span data-stu-id="06ffb-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="06ffb-129">Seleccione una instancia de rol que tenga el Escritorio remoto configurado.</span><span class="sxs-lookup"><span data-stu-id="06ffb-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="06ffb-130">Haga clic en **conectar** toodownload un RDP de archivos para la instancia de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="06ffb-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="06ffb-132">Haga clic en **abiertos** y, a continuación, **conectar** toostart Hola conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="06ffb-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="06ffb-133">Si su servicio en la nube se encuentra detrás de un NSG, probablemente necesite toocreate reglas que permitan el tráfico en puertos **3389** y **20000**.</span><span class="sxs-lookup"><span data-stu-id="06ffb-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="06ffb-134">Escritorio remoto usa el puerto **3389**.</span><span class="sxs-lookup"><span data-stu-id="06ffb-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="06ffb-135">Instancias de servicio en la nube son carga equilibrada, por lo que directamente no se puede controlar qué tooconnect de instancia a.</span><span class="sxs-lookup"><span data-stu-id="06ffb-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="06ffb-136">Hola *RemoteForwarder* y *RemoteAccess* agentes administrar el tráfico RDP y permitir Hola cliente toosend una cookie RDP y especificar un tooconnect de una instancia individual a.</span><span class="sxs-lookup"><span data-stu-id="06ffb-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="06ffb-137">Hola *RemoteForwarder* y *RemoteAccess* agentes requieren ese puerto **20000*** abrirse, que pueden bloquearse si tienes un NSG.</span><span class="sxs-lookup"><span data-stu-id="06ffb-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="06ffb-138">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="06ffb-138">Additional resources</span></span>

<span data-ttu-id="06ffb-139">[¿Cómo tooConfigure servicios en la nube](cloud-services-how-to-configure.md)
[preguntas más frecuentes: los servicios de nube escritorio remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="06ffb-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
