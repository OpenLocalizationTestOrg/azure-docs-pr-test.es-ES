---
title: "máquinas virtuales aaaManage con hello Azure explorador para IntelliJ | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage máquinas virtuales de Azure mediante el uso de Hola Explorer de Azure para IntelliJ."
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="b26f5-103">Administrar máquinas virtuales mediante el uso de hello Azure explorador para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b26f5-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="b26f5-104">Hola Explorador de Azure, que forma parte de hello Azure Toolkit for IntelliJ, proporciona a los desarrolladores de Java con una solución fácil de usar para administrar máquinas virtuales en su cuenta de Azure desde dentro del entorno de desarrollo integrado de hello IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="b26f5-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="b26f5-105">Creación de una máquina virtual en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b26f5-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b26f5-106">toocreate una máquina virtual mediante el uso de hello Azure explorador, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b26f5-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="b26f5-107">Inicie sesión en tooyour cuenta de Azure mediante los pasos de Hola Hola [instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ] artículo.</span><span class="sxs-lookup"><span data-stu-id="b26f5-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="b26f5-108">Hola **explorador Azure** , expanda hello **Azure** nodo, haga clic en **máquinas virtuales**y, a continuación, haga clic en **crear VM**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="b26f5-109">![Hola comando Crear VM][CR01]</span><span class="sxs-lookup"><span data-stu-id="b26f5-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="b26f5-110">Hola **crear nueva máquina Virtual** abre el asistente.</span><span class="sxs-lookup"><span data-stu-id="b26f5-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="b26f5-111">Hola **elegir una suscripción** ventana, seleccione su suscripción y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Hola elegir una ventana de suscripción][CR02]

4. <span data-ttu-id="b26f5-113">Hola **seleccionar una imagen de máquina Virtual** ventana, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b26f5-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="b26f5-114">**Ubicación**: especifica la ubicación donde se creará la máquina virtual (por ejemplo, *oeste de EE. UU.*).</span><span class="sxs-lookup"><span data-stu-id="b26f5-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="b26f5-115">**Imagen recomendada**: especifica que elegirá una imagen de una lista abreviada de imágenes usadas con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="b26f5-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="b26f5-116">**Imagen personalizada**: Especifica que elegirá una imagen personalizada proporcionando Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b26f5-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="b26f5-117">**Publisher**: especifica el publicador de Hola que creó la imagen de Hola que va a utilizar para la máquina virtual (por ejemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="b26f5-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="b26f5-118">**Ofrecer**: especifica la máquina virtual de hello toouse la oferta de publicador seleccionado hello (por ejemplo, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="b26f5-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="b26f5-119">**SKU**: especifica Hola toouse de almacén (SKU) de almacenamiento de oferta de hello seleccionado (por ejemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="b26f5-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="b26f5-120">**Versión #**: especifica qué versión de Hola seleccionado toouse SKU.</span><span class="sxs-lookup"><span data-stu-id="b26f5-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![Hola seleccionar una ventana de la imagen de máquina Virtual][CR03]

5. <span data-ttu-id="b26f5-122">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-122">Click **Next**.</span></span> 

6. <span data-ttu-id="b26f5-123">Hola **configuración básica de máquina Virtual** ventana, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b26f5-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="b26f5-124">**Nombre de máquina virtual**: especifica el nombre de hello para la nueva máquina virtual, que debe empezar por una letra y contener solo letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="b26f5-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="b26f5-125">**Tamaño**: especifica el número de Hola de núcleos y memoria tooallocate para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b26f5-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="b26f5-126">**Nombre de usuario**: especifica hello toocreate de cuenta de administrador para administrar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b26f5-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="b26f5-127">**Contraseña** y **confirmar**: especifica la contraseña de hello para la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="b26f5-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![ventana de configuración de máquina Virtual básica Hello][CR04]

7. <span data-ttu-id="b26f5-129">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-129">Click **Next**.</span></span> 

8. <span data-ttu-id="b26f5-130">Hola **recursos asociados** ventana, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b26f5-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="b26f5-131">**Grupo de recursos**: especifica el grupo de recursos de hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b26f5-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="b26f5-132">Seleccione una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="b26f5-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="b26f5-133">**Cree una nueva**: Especifica que desea toocreate un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b26f5-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="b26f5-134">**Usar existente**: Especifica que desea tooselect en una lista de grupos de recursos que están asociados a su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b26f5-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![ventana de Hello recursos asociados][CR07]

   * <span data-ttu-id="b26f5-136">**Cuenta de almacenamiento**: especifica hello toouse de cuenta de almacenamiento para almacenar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b26f5-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="b26f5-137">Puede usar una cuenta de almacenamiento o crear una.</span><span class="sxs-lookup"><span data-stu-id="b26f5-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="b26f5-138">Si elige **crear nuevo**, aparece hello después el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="b26f5-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![cuadro de diálogo Crear cuenta de almacenamiento de Hola][CR05]

   * <span data-ttu-id="b26f5-140">**Red virtual** y **subred**: especifica la red virtual de Hola y de las subredes que se conectará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b26f5-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="b26f5-141">Puede usar una red y subred existentes, o puede crear una nueva red y subred.</span><span class="sxs-lookup"><span data-stu-id="b26f5-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="b26f5-142">Si selecciona **crear nuevo**, aparece hello después el cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="b26f5-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![cuadro de diálogo de creación de red Virtual de Hola][CR06]

   * <span data-ttu-id="b26f5-144">**Dirección IP pública**: especifica una dirección IP externa para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b26f5-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="b26f5-145">Puede elegir una nueva dirección IP toocreate o, si la máquina virtual no tiene una dirección IP pública, puede seleccionar **(ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="b26f5-146">**Grupo de seguridad de red**: especifica un firewall de red opcional para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b26f5-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="b26f5-147">Puede seleccionar un firewall o, si la máquina virtual no utiliza un firewall, puede seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="b26f5-148">**Conjunto de disponibilidad**: especifica un conjunto de disponibilidad opcional al que puede pertenecer su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b26f5-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="b26f5-149">Puede seleccionar un conjunto de disponibilidad existente, cree un nuevo conjunto de disponibilidad o, si la máquina virtual no pertenecerá tooan conjunto de disponibilidad, seleccione **(ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="b26f5-150">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="b26f5-150">Click **Finish**.</span></span>  
    <span data-ttu-id="b26f5-151">La nueva máquina virtual aparece en la ventana de herramientas del explorador de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="b26f5-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Máquina virtual nueva en hello Azure del explorador][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="b26f5-153">Reinicio de una máquina virtual en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b26f5-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b26f5-154">una máquina virtual mediante el uso de hello Azure explorador en IntelliJ, toorestart Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b26f5-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="b26f5-155">Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![comando de reinicio de máquina virtual de Hola][RE01]

2. <span data-ttu-id="b26f5-157">En la ventana de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-157">In hello confirmation window, click **Yes**.</span></span> 

   ![Hola reiniciar la ventana de confirmación de la máquina virtual][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="b26f5-159">Apagado de una máquina virtual en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b26f5-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b26f5-160">tooshut hacia abajo una máquina virtual en ejecución mediante el uso de hello Azure explorador en IntelliJ, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b26f5-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="b26f5-161">Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **apagado**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![comando de apagado de máquina virtual de Hola][SH01]

2. <span data-ttu-id="b26f5-163">En la ventana de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-163">In hello confirmation window, click **Yes**.</span></span> 

   ![Hola cerrar la ventana de confirmación de la máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="b26f5-165">Eliminación de una máquina virtual en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b26f5-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b26f5-166">una máquina virtual mediante el uso de hello Azure explorador en IntelliJ, toodelete Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b26f5-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="b26f5-167">Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![comando de eliminación de máquina virtual de Hola][DE01]

2. <span data-ttu-id="b26f5-169">En la ventana de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b26f5-169">In hello confirmation window, click **Yes**.</span></span> 

   ![Hola eliminar la ventana de confirmación de la máquina virtual][DE02]

## <a name="next-steps"></a><span data-ttu-id="b26f5-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b26f5-171">Next steps</span></span>
<span data-ttu-id="b26f5-172">Para obtener más información acerca de los tamaños de máquina virtual de Azure y los precios, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b26f5-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="b26f5-173">Tamaños de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="b26f5-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="b26f5-174">[Tamaños de las máquinas virtuales Windows en Azure]</span><span class="sxs-lookup"><span data-stu-id="b26f5-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="b26f5-175">[Tamaños de las máquinas virtuales Linux en Azure]</span><span class="sxs-lookup"><span data-stu-id="b26f5-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="b26f5-176">Precios de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="b26f5-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="b26f5-177">[Precios de máquinas virtuales Windows]</span><span class="sxs-lookup"><span data-stu-id="b26f5-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="b26f5-178">[Precios de máquinas virtuales Linux]</span><span class="sxs-lookup"><span data-stu-id="b26f5-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="b26f5-179">Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b26f5-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="b26f5-180">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b26f5-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b26f5-181">[Novedades de hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b26f5-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b26f5-182">[Instalar hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b26f5-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b26f5-183">[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b26f5-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b26f5-184">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b26f5-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="b26f5-185">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b26f5-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b26f5-186">[Novedades de hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b26f5-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b26f5-187">[Instalación hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b26f5-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b26f5-188">[instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b26f5-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b26f5-189">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b26f5-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="b26f5-190">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b26f5-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novedades de hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novedades de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Tamaños de las máquinas virtuales Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamaños de las máquinas virtuales Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Precios de máquinas virtuales Windows]: /pricing/details/virtual-machines/windows/
[Precios de máquinas virtuales Linux]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
