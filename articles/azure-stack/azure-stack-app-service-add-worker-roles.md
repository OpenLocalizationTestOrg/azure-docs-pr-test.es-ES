---
title: 'aaaScale los roles de trabajo de servicios de aplicaciones: pila de Azure | Documentos de Microsoft'
description: Instrucciones detalladas de escalado de App Services en Azure Stack
services: azure-stack
documentationcenter: 
author: kathm
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: kathm
ms.openlocfilehash: 252b4a531655e38f3a3747f8a04b16fc6303f9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a><span data-ttu-id="95c2f-103">App Service en Azure Stack: incorporación de más roles de trabajo</span><span class="sxs-lookup"><span data-stu-id="95c2f-103">App Service on Azure Stack: Adding more worker roles</span></span> 

<span data-ttu-id="95c2f-104">Este documento proporciona instrucciones sobre cómo tooscale servicio de aplicaciones en roles de trabajador de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="95c2f-104">This document provides instructions about how tooscale App Service on Azure Stack worker roles.</span></span> <span data-ttu-id="95c2f-105">Contiene pasos para crear aplicaciones de toosupport de roles de trabajo adicional de cualquier tamaño.</span><span class="sxs-lookup"><span data-stu-id="95c2f-105">It contains steps for creating additional worker roles toosupport applications of any size.</span></span>

> [!NOTE]
> <span data-ttu-id="95c2f-106">Si su entorno de prueba de concepto de Azure Stack no tiene más de 96 GB de RAM, puede encontrar dificultades al agregar capacidad adicional.</span><span class="sxs-lookup"><span data-stu-id="95c2f-106">If your Azure Stack POC Environment does not have more than 96-GB RAM you may have difficulties adding additional capacity.</span></span>

<span data-ttu-id="95c2f-107">App Service en Azure Stack, de forma predeterminada, es compatible con los niveles de trabajo gratuito y compartido.</span><span class="sxs-lookup"><span data-stu-id="95c2f-107">App Service on Azure Stack, by default, supports free and shared worker tiers.</span></span> <span data-ttu-id="95c2f-108">tooadd otros niveles de trabajo, deberá tooadd más roles de trabajo.</span><span class="sxs-lookup"><span data-stu-id="95c2f-108">tooadd other worker tiers, you need tooadd more worker roles.</span></span>

<span data-ttu-id="95c2f-109">Si no estás seguro de lo que se implementó no tiene valor predeterminado de hello servicio de aplicaciones en la instalación de la pila de Azure, puede revisar la información adicional de hello [servicio de aplicaciones en información general de la pila de Azure](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95c2f-109">If you are not sure what was deployed with hello default App Service on Azure Stack installation, you can review additional information in hello [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>

<span data-ttu-id="95c2f-110">Hay dos maneras tooadd capacidad adicional tooApp servicio en la pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="95c2f-110">There are two ways tooadd additional capacity tooApp Service on Azure Stack:</span></span>
1.  <span data-ttu-id="95c2f-111">[Agregar trabajos adicionales directamente desde con dentro de hello App Admin de proveedor de recursos de servicio](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span><span class="sxs-lookup"><span data-stu-id="95c2f-111">[Add additional workers directly from with within hello App Service Resource Provider Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span></span>
2.  <span data-ttu-id="95c2f-112">[Crear máquinas virtuales adicionales manualmente y agregarlas toohello proveedor de recursos de servicio de aplicación](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span><span class="sxs-lookup"><span data-stu-id="95c2f-112">[Create additional VMs manually and add them toohello App Service Resource Provider](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span></span>

## <a name="add-additional-workers-directly-within-hello-app-service-resource-provider-admin"></a><span data-ttu-id="95c2f-113">Agregar trabajos adicionales directamente dentro de hello administrador. proveedor de recursos de servicio de aplicación</span><span class="sxs-lookup"><span data-stu-id="95c2f-113">Add additional workers directly within hello App Service Resource Provider Admin.</span></span>

1.  <span data-ttu-id="95c2f-114">Inicie sesión en toohello portal de la pila de Azure como administrador de servicios de hello;</span><span class="sxs-lookup"><span data-stu-id="95c2f-114">Log in toohello Azure Stack portal as hello service administrator;</span></span>
2.  <span data-ttu-id="95c2f-115">Examinar demasiado**proveedores de recursos** y seleccione hello **App Admin de proveedor de recursos de servicio**. ![Proveedores de recursos de Azure Stack][1]</span><span class="sxs-lookup"><span data-stu-id="95c2f-115">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**. ![Azure Stack Resource Providers][1]</span></span>
3.  <span data-ttu-id="95c2f-116">Haga clic en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-116">Click **Roles**.</span></span>  <span data-ttu-id="95c2f-117">Aquí verá desglose de Hola de todos los roles de servicio de aplicaciones implementadas.</span><span class="sxs-lookup"><span data-stu-id="95c2f-117">Here you see hello breakdown of all App Service roles deployed.</span></span>
4.  <span data-ttu-id="95c2f-118">Haga clic en la opción de hello **nueva instancia de rol** ![agregar una nueva instancia de rol][2]</span><span class="sxs-lookup"><span data-stu-id="95c2f-118">Click hello option **New Role Instance** ![Add new role instance][2]</span></span>
5.  <span data-ttu-id="95c2f-119">Hola **nueva instancia de rol** hoja:</span><span class="sxs-lookup"><span data-stu-id="95c2f-119">In hello **New Role Instance** blade:</span></span>
    1. <span data-ttu-id="95c2f-120">Elija cuántos adicionales **instancias de rol** le gustaría tooadd.</span><span class="sxs-lookup"><span data-stu-id="95c2f-120">Choose how many additional **role instances** you would like tooadd.</span></span>  <span data-ttu-id="95c2f-121">En la vista previa de hello, hay un máximo de 10.</span><span class="sxs-lookup"><span data-stu-id="95c2f-121">In hello preview, there is a maximum of 10.</span></span>
    2. <span data-ttu-id="95c2f-122">Seleccione hello **tipo de función**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-122">Select hello **role type**.</span></span>  <span data-ttu-id="95c2f-123">En esta versión preliminar, esta opción está limitada tooWeb trabajo.</span><span class="sxs-lookup"><span data-stu-id="95c2f-123">In this preview, this option is limited tooWeb Worker.</span></span>
    3. <span data-ttu-id="95c2f-124">Seleccione hello **nivel de trabajo** le gustaría toodeploy este trabajo en, las opciones predeterminadas son pequeño, mediano, grande o compartido.</span><span class="sxs-lookup"><span data-stu-id="95c2f-124">Select hello **worker tier** you would like toodeploy this worker into, default choices are Small, Medium, Large, or Shared.</span></span>  <span data-ttu-id="95c2f-125">Si ha creado sus propios niveles de trabajo, también estarán disponibles para la selección.</span><span class="sxs-lookup"><span data-stu-id="95c2f-125">If, you have created your own worker tiers, your worker tiers will also be available for selection.</span></span>
    4. <span data-ttu-id="95c2f-126">Haga clic en **Aceptar** toodeploy Hola los trabajadores adicionales</span><span class="sxs-lookup"><span data-stu-id="95c2f-126">Click **OK** toodeploy hello additional workers</span></span>
6.  <span data-ttu-id="95c2f-127">Servicio de aplicaciones de voluntad de pila de Azure ahora agregar Hola máquinas virtuales adicionales, configurarlos, instalar todo el software necesario de Hola y marcarlos como preparado para cuando se complete este proceso.</span><span class="sxs-lookup"><span data-stu-id="95c2f-127">App Service on Azure Stack will now add hello additional VMs, configure them, install all hello required software and mark them as ready when this process is complete.</span></span>  <span data-ttu-id="95c2f-128">que puede tardar unos 80 minutos.</span><span class="sxs-lookup"><span data-stu-id="95c2f-128">This process can take approximately 80 minutes.</span></span>
7.  <span data-ttu-id="95c2f-129">Puede supervisar el progreso de Hola de preparación de Hola de nuevos subprocesos de trabajo Hola viendo los trabajadores de hello en hello **roles** hoja.</span><span class="sxs-lookup"><span data-stu-id="95c2f-129">You can monitor hello progress of hello readiness of hello new workers by viewing hello workers in hello **roles** blade.</span></span>

>[!NOTE]
>  <span data-ttu-id="95c2f-130">En esta versión preliminar, hello integrado flujo de la nueva instancia de rol es limitado tooWorker Roles e implementar máquinas virtuales de tamaño A1.</span><span class="sxs-lookup"><span data-stu-id="95c2f-130">In this preview, hello integrated New Role Instance flow is limited tooWorker Roles and deploy VMs of size A1 only.</span></span>  <span data-ttu-id="95c2f-131">Esta funcionalidad se ampliará en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="95c2f-131">We will be expanding this capability in a future release.</span></span>

## <a name="manually-adding-additional-capacity-tooapp-service-on-azure-stack"></a><span data-ttu-id="95c2f-132">Cómo agregar manualmente una capacidad adicional tooApp servicio en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="95c2f-132">Manually adding additional capacity tooApp Service on Azure Stack.</span></span>

<span data-ttu-id="95c2f-133">Hello pasos siguientes son roles adicionales tooadd necesarios:</span><span class="sxs-lookup"><span data-stu-id="95c2f-133">hello following steps are required tooadd additional roles:</span></span>

1. [<span data-ttu-id="95c2f-134">Creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="95c2f-134">Create a new virtual machine</span></span>](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [<span data-ttu-id="95c2f-135">Configurar la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="95c2f-135">Configure hello virtual machine</span></span>](#step-2-configure-the-virtual-machine)
3. [<span data-ttu-id="95c2f-136">Configure el rol de trabajador de web de hello en el portal de Azure pila Hola</span><span class="sxs-lookup"><span data-stu-id="95c2f-136">Configure hello web worker role in hello Azure Stack portal</span></span>](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [<span data-ttu-id="95c2f-137">Configuración de los planes de App Service</span><span class="sxs-lookup"><span data-stu-id="95c2f-137">Configure app service plans</span></span>](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-toosupport-hello-new-instance-size"></a><span data-ttu-id="95c2f-138">Paso 1: Crear un nueva VM toosupport Hola nuevo tamaño de instancia</span><span class="sxs-lookup"><span data-stu-id="95c2f-138">Step 1: Create a new VM toosupport hello new instance size</span></span>
<span data-ttu-id="95c2f-139">Crear una máquina virtual como se describe en [este artículo](azure-stack-provision-vm.md), asegurándose de que siguiente Hola se realizan las selecciones:</span><span class="sxs-lookup"><span data-stu-id="95c2f-139">Create a virtual machine as described in [this article](azure-stack-provision-vm.md), ensuring that hello following selections are made:</span></span>

* <span data-ttu-id="95c2f-140">Nombre de usuario y contraseña: proporcionar Hola el mismo nombre de usuario y contraseña que especificó al instalar el servicio de aplicaciones en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="95c2f-140">User name and password: Provide hello same user name and password you provided when you installed App Service on Azure Stack.</span></span>
* <span data-ttu-id="95c2f-141">Suscripción: Suscripción de proveedor Use Hola predeterminada.</span><span class="sxs-lookup"><span data-stu-id="95c2f-141">Subscription: Use hello default provider subscription.</span></span>
* <span data-ttu-id="95c2f-142">Grupo de recursos: elija **AppService-LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-142">Resource group: Choose **AppService-LOCAL**.</span></span>

> [!NOTE]
> <span data-ttu-id="95c2f-143">Almacenar máquinas virtuales de Hola para roles de trabajo en hello al mismo grupo de recursos como servicio de aplicaciones en la pila de Azure se implementa en.</span><span class="sxs-lookup"><span data-stu-id="95c2f-143">Store hello virtual machines for worker roles in hello same resource group as App Service on Azure Stack is deployed to.</span></span> <span data-ttu-id="95c2f-144">(recomendación para esta versión).</span><span class="sxs-lookup"><span data-stu-id="95c2f-144">(This is recommended for this release.)</span></span>
> 
> 

## <a name="step-2-configure-hello-virtual-machine"></a><span data-ttu-id="95c2f-145">Paso 2: Configurar Hola Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="95c2f-145">Step 2: Configure hello Virtual Machine</span></span>
<span data-ttu-id="95c2f-146">Cuando haya completado la implementación de hello, Hola siguiente configuración es rol de trabajo de toosupport necesario hello web:</span><span class="sxs-lookup"><span data-stu-id="95c2f-146">Once hello deployment has completed, hello following configuration is required toosupport hello web worker role:</span></span>

1. <span data-ttu-id="95c2f-147">Examinar toohello **AppService LOCAL** grupo de recursos en el portal de Hola y máquina nueva Hola select que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="95c2f-147">Browse toohello **AppService-LOCAL** resource group in hello portal and select hello new machine you created in Step 1.</span></span>
2. <span data-ttu-id="95c2f-148">Haga clic en conectar en hello VM hoja toodownload Hola escritorio perfil remoto.</span><span class="sxs-lookup"><span data-stu-id="95c2f-148">Click connect in hello VM blade toodownload hello remote desktop profile.</span></span>  <span data-ttu-id="95c2f-149">Abra Hola perfil tooopen una VM de tooyour de sesión de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="95c2f-149">Open hello profile tooopen a remote desktop session tooyour VM.</span></span>
3. <span data-ttu-id="95c2f-150">Inicie sesión en toohello VM con hello de usuario y contraseña que especificó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="95c2f-150">Log in toohello VM using hello username and password you specified in Step 1.</span></span>
4. <span data-ttu-id="95c2f-151">Abra PowerShell haciendo clic en hello **iniciar** botón y escribiendo PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95c2f-151">Open PowerShell by clicking hello **Start** button and typing PowerShell.</span></span> <span data-ttu-id="95c2f-152">Haga clic en **PowerShell.exe**y seleccione **ejecutar como administrador** tooopen PowerShell en modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="95c2f-152">Right-click **PowerShell.exe**, and select **Run as administrator** tooopen PowerShell in administrator mode.</span></span>
5. <span data-ttu-id="95c2f-153">Copia y pegado de hello después de comandos (uno en uno) en la ventana de PowerShell de hello y presione ENTRAR:</span><span class="sxs-lookup"><span data-stu-id="95c2f-153">Copy and paste each of hello following commands (one at a time) into hello PowerShell window, and press enter:</span></span>
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. <span data-ttu-id="95c2f-154">Cierre la sesión de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="95c2f-154">Close your remote desktop session.</span></span>
7. <span data-ttu-id="95c2f-155">Reinicie Hola VM desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="95c2f-155">Restart hello VM from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="95c2f-156">Estos son los requisitos mínimos para App Service en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="95c2f-156">These are minimum requirements for App Service on Azure Stack.</span></span> <span data-ttu-id="95c2f-157">Son valores predeterminados de Hola de imagen de Windows 2012 R2 de hello incluida en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="95c2f-157">They are hello default settings of hello Windows 2012 R2 image included with Azure Stack.</span></span> <span data-ttu-id="95c2f-158">se han proporcionado instrucciones Hello en el futuro y para los usuarios que utilicen otra imagen.</span><span class="sxs-lookup"><span data-stu-id="95c2f-158">hello instructions have been provided for future reference, and for those using a different image.</span></span>
> 
> 

## <a name="step-3-configure-hello-worker-role-in-hello-azure-stack-portal"></a><span data-ttu-id="95c2f-159">Paso 3: Configurar el rol de trabajo de hello en el portal de Azure pila Hola</span><span class="sxs-lookup"><span data-stu-id="95c2f-159">Step 3: Configure hello worker role in hello Azure Stack portal</span></span>
1. <span data-ttu-id="95c2f-160">Portal de hello abra como administrador de servicios de hello en **ClientVM**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-160">Open hello portal as hello service administrator on **ClientVM**.</span></span>
2. <span data-ttu-id="95c2f-161">Navegue demasiado**proveedores de recursos** &gt; **App Admin de proveedor de recursos de servicio**.![ Administración de proveedor de recursos de servicio de aplicaciones][3]</span><span class="sxs-lookup"><span data-stu-id="95c2f-161">Navigate too**Resource Providers** &gt; **App Service Resource Provider Admin**.![App Service Resource Provider Admin][3]</span></span>
3. <span data-ttu-id="95c2f-162">En la hoja de configuración de hello, haga clic en **Roles**.![ Roles de proveedor de recursos de servicio de aplicaciones][4]</span><span class="sxs-lookup"><span data-stu-id="95c2f-162">In hello settings blade, click **Roles**.![App Service Resource Provider Roles][4]</span></span>
4. <span data-ttu-id="95c2f-163">Haga clic en **Agregar instancia de rol**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-163">Click **Add Role Instance**.</span></span>
5. <span data-ttu-id="95c2f-164">En el cuadro de texto de Hola para **nombre del servidor** escriba hello **dirección IP** de servidor de Hola que creó anteriormente (en la sección 1).</span><span class="sxs-lookup"><span data-stu-id="95c2f-164">In hello textbox for **Server Name** enter hello **IP Address** of hello server you created earlier (in Section 1).</span></span>
6. <span data-ttu-id="95c2f-165">Seleccione hello **tipo de rol** le gustaría tooadd - controlador, servidor de administración, Front-End, trabajo Web, publicador o servidor de archivos.</span><span class="sxs-lookup"><span data-stu-id="95c2f-165">Select hello **Role Type** you would like tooadd - Controller, Management Server, Front End, Web Worker, Publisher, or File Server.</span></span>  <span data-ttu-id="95c2f-166">En este caso, seleccione Trabajo web.</span><span class="sxs-lookup"><span data-stu-id="95c2f-166">In this instance, select Web Worker.</span></span>
7. <span data-ttu-id="95c2f-167">Haga clic en hello **capa** para sería como toodeploy Hola de nuevo la instancia de demasiado (pequeño, mediano, grande o compartido).</span><span class="sxs-lookup"><span data-stu-id="95c2f-167">Click hello **Tier** you would like toodeploy hello new instance too(small, medium, large, or shared).</span></span>  <span data-ttu-id="95c2f-168">Si ha creado sus propios niveles de trabajo, también estarán disponibles para la selección.</span><span class="sxs-lookup"><span data-stu-id="95c2f-168">If you have created your own worker tiers these will also be available for selection.</span></span>
8. <span data-ttu-id="95c2f-169">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-169">Click **OK.**</span></span>
9. <span data-ttu-id="95c2f-170">Volver atrás toohello **Roles** vista</span><span class="sxs-lookup"><span data-stu-id="95c2f-170">Go back toohello **Roles** view</span></span>
10. <span data-ttu-id="95c2f-171">Haga clic en hello fila correspondiente toohello combinación de tipo de función y nivel de trabajo que asignó la máquina virtual a.</span><span class="sxs-lookup"><span data-stu-id="95c2f-171">Click hello row corresponding toohello Role Type and Worker Tier combination you assigned your VM to.</span></span>
11. <span data-ttu-id="95c2f-172">Busque Hola nombre del servidor que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="95c2f-172">Look for hello Server Name you just added.</span></span> <span data-ttu-id="95c2f-173">Revise la columna de estado de Hola y espere toomove toohello siguiente paso hasta que el estado de hello es "Listo".</span><span class="sxs-lookup"><span data-stu-id="95c2f-173">Review hello status column, and wait toomove toohello next step until hello status is "Ready."</span></span> <span data-ttu-id="95c2f-174">esto puede tardar unos 80 minutos.</span><span class="sxs-lookup"><span data-stu-id="95c2f-174">This can take approximately 80 minutes.</span></span> <span data-ttu-id="95c2f-175">![Rol de proveedor de recursos de App Service listo][5]</span><span class="sxs-lookup"><span data-stu-id="95c2f-175">![App Service Resource Provider Role Ready][5]</span></span>

## <a name="step-4-configure-app-service-plans"></a><span data-ttu-id="95c2f-176">Paso 4: Configuración de los planes de App Service</span><span class="sxs-lookup"><span data-stu-id="95c2f-176">Step 4: Configure app service plans</span></span>

1. <span data-ttu-id="95c2f-177">Inicie sesión en el portal de toohello en hello ClientVM.</span><span class="sxs-lookup"><span data-stu-id="95c2f-177">Sign in toohello portal on hello ClientVM.</span></span>
2. <span data-ttu-id="95c2f-178">Navegue demasiado**New** &gt; **Web y móviles**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-178">Navigate too**New** &gt; **Web and Mobile**.</span></span>
3. <span data-ttu-id="95c2f-179">Seleccione el tipo de saludo de aplicación le gustaría toodeploy.</span><span class="sxs-lookup"><span data-stu-id="95c2f-179">Select hello type of application you would like toodeploy.</span></span>
4. <span data-ttu-id="95c2f-180">Proporcionar información de hello para la aplicación hello y, a continuación, seleccione **Plan de servicio de aplicaciones / ubicación**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-180">Provide hello information for hello application, and then select **AppService Plan / Location**.</span></span>
    1. <span data-ttu-id="95c2f-181">Haga clic en **Create New**.</span><span class="sxs-lookup"><span data-stu-id="95c2f-181">Click **Create New**.</span></span>
    2. <span data-ttu-id="95c2f-182">Crear un plan, seleccione tarifa correspondiente hello para el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="95c2f-182">Create your plan, selecting hello corresponding pricing tier for hello plan.</span></span>

> [!NOTE]
> <span data-ttu-id="95c2f-183">Puede crear varios planes en esta hoja.</span><span class="sxs-lookup"><span data-stu-id="95c2f-183">You can create multiple plans while on this blade.</span></span> <span data-ttu-id="95c2f-184">Antes de implementar, sin embargo, asegúrese de que seleccionó un plan adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="95c2f-184">Before you deploy, however, ensure you have selected hello appropriate plan.</span></span>
> 
> 

<span data-ttu-id="95c2f-185">Hola continuación muestra un ejemplo de Hola varios niveles de precios disponibles de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="95c2f-185">hello following shows an example of hello multiple pricing tiers available by default.</span></span>  <span data-ttu-id="95c2f-186">Observe que si no hay ningún trabajador disponibles para un nivel de trabajo concreto, Hola Hola de toochoose opción correspondiente nivel de precios no está disponible.</span><span class="sxs-lookup"><span data-stu-id="95c2f-186">You notice that if there are no available workers for a particular worker tier, hello option toochoose hello corresponding pricing tier is unavailable.</span></span>![Planes de tarifa predeterminados para App Service en Azure Stack][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: ./media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png
