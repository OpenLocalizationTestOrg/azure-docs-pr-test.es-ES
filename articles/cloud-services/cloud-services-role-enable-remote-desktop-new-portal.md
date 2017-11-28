---
title: "Habilitación de la conexión a Escritorio remoto para un rol en Azure Cloud Services | Microsoft Docs"
description: "Configuración de la aplicación de servicios en la nube de Azure para permitir conexiones a Escritorio remoto"
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="e48e4-103">Habilitación de la conexión a Escritorio remoto para un rol de Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e48e4-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e48e4-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e48e4-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="e48e4-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="e48e4-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="e48e4-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e48e4-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="e48e4-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e48e4-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="e48e4-108">Escritorio remoto le permite tener acceso al escritorio de un rol que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="e48e4-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="e48e4-109">Puede usar la conexión de Escritorio remoto para solucionar y diagnosticar problemas con su aplicación mientras se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="e48e4-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="e48e4-110">Puede habilitar una conexión a Escritorio remoto en el rol durante el desarrollo mediante la inclusión de los módulos de Escritorio remoto en la definición de servicio, o puede habilitar Escritorio remoto a través de la extensión de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="e48e4-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="e48e4-111">El método preferido es usar la extensión de Escritorio remoto dado que puede habilitar Escritorio remoto incluso después de que se implementa la aplicación sin tener que volver a implementarla.</span><span class="sxs-lookup"><span data-stu-id="e48e4-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="e48e4-112">Configuración de Escritorio remoto desde Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e48e4-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="e48e4-113">Azure Portal usa el enfoque de extensión de Escritorio remoto, por lo que puede habilitar Escritorio remoto incluso después de que se implementa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e48e4-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="e48e4-114">En la hoja **Escritorio remoto** de su servicio en la nube, puede habilitar Escritorio remoto, cambiar la cuenta de Administrador local usada para conectarse a las máquinas virtuales o el certificado que se usa en la autenticación y definir la fecha de caducidad.</span><span class="sxs-lookup"><span data-stu-id="e48e4-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="e48e4-115">Haga clic en **Cloud Services**, en el nombre del servicio en la nube y luego en **Escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="e48e4-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="e48e4-117">Elija si desea habilitar Escritorio remoto para un rol individual o para todos los roles y luego cambie el valor del modificador para **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="e48e4-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="e48e4-118">Rellene los campos obligatorios correspondientes al nombre de usuario, la contraseña, la expiración y el certificado.</span><span class="sxs-lookup"><span data-stu-id="e48e4-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="e48e4-120">se reiniciarán todas las instancias de rol la primera vez que habilite el Escritorio remoto y haga clic en Aceptar (marca de verificación).</span><span class="sxs-lookup"><span data-stu-id="e48e4-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="e48e4-121">Para evitar un reinicio, el certificado que se usó para cifrar la contraseña debe instalarse en el rol.</span><span class="sxs-lookup"><span data-stu-id="e48e4-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="e48e4-122">Para evitar un reinicio, [cargue un certificado para el servicio en la nube](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) y, luego, vuelva a este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e48e4-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="e48e4-123">En **Roles**, seleccione el rol de servicio que desea actualizar o seleccione **Todos** para todos los roles.</span><span class="sxs-lookup"><span data-stu-id="e48e4-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="e48e4-124">Después de terminar las actualizaciones de la configuración, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e48e4-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="e48e4-125">Las instancias de rol tardarán unos minutos en estar listas para recibir conexiones.</span><span class="sxs-lookup"><span data-stu-id="e48e4-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="e48e4-126">Acceso remoto en instancias de rol</span><span class="sxs-lookup"><span data-stu-id="e48e4-126">Remote into role instances</span></span>
<span data-ttu-id="e48e4-127">Una vez que Escritorio remoto está habilitado en los roles, puede iniciar una conexión directamente desde Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="e48e4-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="e48e4-128">Haga clic en **Instancias** para abrir la hoja **Instancias**.</span><span class="sxs-lookup"><span data-stu-id="e48e4-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="e48e4-129">Seleccione una instancia de rol que tenga el Escritorio remoto configurado.</span><span class="sxs-lookup"><span data-stu-id="e48e4-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="e48e4-130">Haga clic en **Conectar** para descargar un archivo RDP para la instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="e48e4-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![Escritorio remoto de Cloud Services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="e48e4-132">Haga clic en **Abrir** y, a continuación, en **Conectar** para iniciar la conexión del Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="e48e4-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="e48e4-133">Si su servicio en la nube se encuentra detrás de un NSG, quizás deba crear reglas que permitan el tráfico en los puertos **3389** y **20000**.</span><span class="sxs-lookup"><span data-stu-id="e48e4-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="e48e4-134">Escritorio remoto usa el puerto **3389**.</span><span class="sxs-lookup"><span data-stu-id="e48e4-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="e48e4-135">Las instancias del servicio en la nube tienen la carga equilibrada, por lo que no se puede controlar directamente a qué instancia conectarse.</span><span class="sxs-lookup"><span data-stu-id="e48e4-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="e48e4-136">Los agentes *RemoteForwarder* y *RemoteAccess* administran el tráfico RDP y permiten al cliente enviar una cookie de RDP y especificar una instancia concreta a la que conectarse.</span><span class="sxs-lookup"><span data-stu-id="e48e4-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="e48e4-137">Los agentes *RemoteForwarder* y *RemoteAccess* requieren que ese puerto **20000*** esté abierto, que podría estar bloqueado si tiene un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="e48e4-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e48e4-138">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e48e4-138">Additional resources</span></span>

<span data-ttu-id="e48e4-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md) (Configuración de Cloud Services)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md) (Preguntas frecuentes sobre Cloud Services > Escritorio remoto)</span><span class="sxs-lookup"><span data-stu-id="e48e4-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
