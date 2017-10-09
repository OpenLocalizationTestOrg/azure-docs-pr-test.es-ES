---
title: "Hola a aaaManage máquinas virtuales con el Explorador de Azure para Eclipse | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage máquinas virtuales de Azure mediante el uso de Hola Explorer de Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="9107d-103">Administrar máquinas virtuales mediante el uso de hello Azure Explorer para Eclipse</span><span class="sxs-lookup"><span data-stu-id="9107d-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="9107d-104">Hola Explorador de Azure, que forma parte de hello Azure Toolkit for Eclipse, proporciona a los desarrolladores de Java con una solución fácil de usar para administrar máquinas virtuales en su cuenta de Azure desde dentro del entorno de desarrollo integrado Eclipse hello (IDE).</span><span class="sxs-lookup"><span data-stu-id="9107d-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="9107d-105">Creación de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="9107d-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="9107d-106">toocreate una máquina virtual mediante el uso de hello Azure explorador, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9107d-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="9107d-107">Inicie sesión en tooyour cuenta de Azure mediante hello [instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="9107d-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="9107d-108">Hola **explorador Azure** , expanda hello **Azure** nodo, haga clic en **máquinas virtuales**y, a continuación, haga clic en **crear VM**.</span><span class="sxs-lookup"><span data-stu-id="9107d-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="9107d-109">![Hola comando Crear VM][CR01]</span><span class="sxs-lookup"><span data-stu-id="9107d-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="9107d-110">Hola **crear nueva máquina Virtual** abre el asistente.</span><span class="sxs-lookup"><span data-stu-id="9107d-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="9107d-111">Hola **elegir una suscripción** ventana, seleccione su suscripción y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9107d-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Hola elegir una ventana de suscripción][CR02]

4. <span data-ttu-id="9107d-113">Hola **seleccionar una imagen de máquina Virtual** ventana, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="9107d-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="9107d-114">**Ubicación**: especifica la ubicación donde se creará la máquina virtual (por ejemplo, *oeste de EE. UU.*).</span><span class="sxs-lookup"><span data-stu-id="9107d-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="9107d-115">**Publisher**: especifica el publicador de Hola que creó la imagen de hello usará toocreate la máquina virtual (por ejemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="9107d-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="9107d-116">**Ofrecer**: especifica la máquina virtual de hello toouse la oferta de publicador seleccionado hello (por ejemplo, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="9107d-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="9107d-117">**SKU**: especifica Hola toouse de almacén (SKU) de almacenamiento de oferta de hello seleccionado (por ejemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="9107d-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="9107d-118">**Versión #**: especifica qué versión de Hola seleccionado toouse SKU.</span><span class="sxs-lookup"><span data-stu-id="9107d-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Hola seleccionar una ventana de la imagen de máquina Virtual][CR03]

5. <span data-ttu-id="9107d-120">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9107d-120">Click **Next**.</span></span>

6. <span data-ttu-id="9107d-121">Hola **configuración básica de máquina Virtual** ventana, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="9107d-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="9107d-122">**Nombre de máquina virtual**: especifica el nombre de hello para la nueva máquina virtual, que debe empezar por una letra y contener solo letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="9107d-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="9107d-123">**Tamaño**: especifica el número de Hola de núcleos y memoria tooallocate para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9107d-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="9107d-124">**Nombre de usuario**: especifica hello toocreate de cuenta de administrador para administrar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9107d-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="9107d-125">**Contraseña** y **confirmar**: especifica la contraseña de hello para la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="9107d-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![ventana de configuración de máquina Virtual básica Hello][CR04]

7. <span data-ttu-id="9107d-127">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9107d-127">Click **Next**.</span></span>

8. <span data-ttu-id="9107d-128">Hola **crear nueva cuenta de almacenamiento** ventana, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="9107d-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="9107d-129">**Grupo de recursos**: especifica el grupo de recursos de hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9107d-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="9107d-130">Seleccione una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="9107d-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="9107d-131">**Cree una nueva**: Especifica que desea toocreate un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9107d-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="9107d-132">**Usar existente**: Especifica que desea tooselect un grupo de recursos que ya está asociado a su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="9107d-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![cuadro de diálogo Crear nueva cuenta de almacenamiento de Hola][CR05]

   * <span data-ttu-id="9107d-134">**Cuenta de almacenamiento**: especifica hello toouse de cuenta de almacenamiento para almacenar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9107d-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="9107d-135">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="9107d-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="9107d-136">**Red virtual** y **subred**: especifica la red virtual de Hola y de las subredes que se conectará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9107d-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="9107d-137">Puede usar una red y subred existentes, o puede crear una nueva red y subred.</span><span class="sxs-lookup"><span data-stu-id="9107d-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="9107d-138">Si selecciona **crear nuevo**, Hola después el cuadro de diálogo se muestra:</span><span class="sxs-lookup"><span data-stu-id="9107d-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![cuadro de diálogo Crear nueva red Virtual de Hola][CR06]

9. <span data-ttu-id="9107d-140">Hola **recursos asociados** ventana, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="9107d-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="9107d-141">**Dirección IP pública**: especifica una dirección IP externa para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9107d-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="9107d-142">Puede elegir una nueva dirección IP toocreate o, si la máquina virtual no tiene una dirección IP pública, puede seleccionar **(ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="9107d-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="9107d-143">**Grupo de seguridad de red**: especifica un firewall de red opcional para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9107d-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="9107d-144">Puede seleccionar un firewall o, si la máquina virtual no utiliza un firewall, puede seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="9107d-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="9107d-145">**Conjunto de disponibilidad**: especifica un conjunto de disponibilidad opcional al que puede pertenecer su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9107d-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="9107d-146">Puede seleccionar un conjunto de disponibilidad existente o crear un nuevo conjunto de disponibilidad o, si la máquina virtual no pertenecerá tooan conjunto de disponibilidad, puede seleccionar **(ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="9107d-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![ventana de Hello recursos asociados][CR07]

9. <span data-ttu-id="9107d-148">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="9107d-148">Click **Finish**.</span></span>  
  <span data-ttu-id="9107d-149">La nueva máquina virtual se muestra en la ventana de herramientas del explorador de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="9107d-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Nueva máquina virtual][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="9107d-151">Reinicio de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="9107d-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="9107d-152">toorestart una máquina virtual mediante el uso de hello Explorador de Azure en Eclipse, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9107d-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="9107d-153">Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="9107d-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![comando de reinicio de máquina virtual de Hola][RE01]

2. <span data-ttu-id="9107d-155">En la ventana de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="9107d-155">In hello confirmation window, click **Yes**.</span></span>

   ![ventana de confirmación de reinicio de Hola][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="9107d-157">Apagado de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="9107d-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="9107d-158">tooshut hacia abajo una máquina virtual en ejecución mediante el uso de hello Explorador de Azure en Eclipse, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9107d-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="9107d-159">Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **apagado**.</span><span class="sxs-lookup"><span data-stu-id="9107d-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![comando de apagado de máquina virtual de Hola][SH01]

2. <span data-ttu-id="9107d-161">En la ventana de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="9107d-161">In hello confirmation window, click **Yes**.</span></span>

   ![ventana de confirmación de apagado de máquina virtual de Hola][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="9107d-163">Eliminación de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="9107d-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="9107d-164">toodelete una máquina virtual mediante el uso de hello Explorador de Azure en Eclipse, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="9107d-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="9107d-165">Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9107d-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![comando de eliminación de máquina virtual de Hola][DE01]

2. <span data-ttu-id="9107d-167">En la ventana de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="9107d-167">In hello confirmation window, click **Yes**.</span></span>

   ![ventana de confirmación de eliminación de la máquina virtual de Hola][DE02]

## <a name="next-steps"></a><span data-ttu-id="9107d-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9107d-169">Next steps</span></span>
<span data-ttu-id="9107d-170">Para obtener más información acerca de los tamaños de máquina virtual de Azure y los precios, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9107d-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="9107d-171">Tamaños de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="9107d-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="9107d-172">[Tamaños de las máquinas virtuales Windows en Azure]</span><span class="sxs-lookup"><span data-stu-id="9107d-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="9107d-173">[Tamaños de las máquinas virtuales Linux en Azure]</span><span class="sxs-lookup"><span data-stu-id="9107d-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="9107d-174">Precios de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="9107d-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="9107d-175">[Precios de máquinas virtuales Windows]</span><span class="sxs-lookup"><span data-stu-id="9107d-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="9107d-176">[Precios de máquinas virtuales Linux]</span><span class="sxs-lookup"><span data-stu-id="9107d-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="9107d-177">Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9107d-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="9107d-178">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9107d-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9107d-179">[Novedades de hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9107d-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9107d-180">[Instalar hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9107d-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9107d-181">[instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9107d-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9107d-182">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9107d-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="9107d-183">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9107d-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9107d-184">[Novedades de hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9107d-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9107d-185">[Instalación hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9107d-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9107d-186">[Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9107d-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9107d-187">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="9107d-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="9107d-188">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="9107d-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novedades de hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novedades de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Tamaños de las máquinas virtuales Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamaños de las máquinas virtuales Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Precios de máquinas virtuales Windows]: /pricing/details/virtual-machines/windows/
[Precios de máquinas virtuales Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
