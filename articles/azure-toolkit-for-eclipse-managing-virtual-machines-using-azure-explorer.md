---
title: "Administración de máquinas virtuales con Azure Explorer para Eclipse | Microsoft Docs"
description: "Obtenga información sobre cómo administrar máquinas virtuales de Azure mediante Azure Explorer para Eclipse."
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
ms.openlocfilehash: 9784e8af9c530078afee06f08a23403a44b0762f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="d7230-103">Administración de máquinas virtuales con Azure Explorer para Eclipse</span><span class="sxs-lookup"><span data-stu-id="d7230-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="d7230-104">Azure Explorer, que forma parte del kit de herramientas de Azure para Eclipse, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de máquinas virtuales en su cuenta de Azure desde el entorno de desarrollo integrado de Eclipse (IDE).</span><span class="sxs-lookup"><span data-stu-id="d7230-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="d7230-105">Creación de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="d7230-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="d7230-106">Para crear una máquina virtual con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7230-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="d7230-107">Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="d7230-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="d7230-108">En la vista **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Virtual Machines** y, luego, en **Crear máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="d7230-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="d7230-109">![El comando Crear máquina virtual][CR01]</span><span class="sxs-lookup"><span data-stu-id="d7230-109">![The Create VM command][CR01]</span></span>  
   <span data-ttu-id="d7230-110">El Asistente **para crear nueva máquina virtual** se abrirá.</span><span class="sxs-lookup"><span data-stu-id="d7230-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="d7230-111">En la ventana **Elegir una suscripción**, seleccione su suscripción y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d7230-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Ventana Elegir una suscripción][CR02]

4. <span data-ttu-id="d7230-113">En la ventana **Seleccionar una imagen de máquina virtual**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d7230-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="d7230-114">**Ubicación**: especifica la ubicación donde se creará la máquina virtual (por ejemplo, *oeste de EE. UU.*).</span><span class="sxs-lookup"><span data-stu-id="d7230-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="d7230-115">**Publicador**: especifica el publicador que creó la imagen que se usará para crear la máquina virtual (por ejemplo, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="d7230-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="d7230-116">**Oferta**: especifica la oferta de máquina virtual que quiere usar del publicador seleccionado (por ejemplo, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="d7230-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="d7230-117">**SKU**: especifica la referencia de almacén (SKU) que quiere usar de la oferta seleccionada (por ejemplo, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="d7230-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="d7230-118">**N.º de versión**: especifica la versión que quiere usar de la SKU seleccionada.</span><span class="sxs-lookup"><span data-stu-id="d7230-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

    ![La ventana Seleccionar una imagen de máquina virtual][CR03]

5. <span data-ttu-id="d7230-120">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d7230-120">Click **Next**.</span></span>

6. <span data-ttu-id="d7230-121">En la pantalla **Configuración básica de máquina virtual**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d7230-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="d7230-122">**Nombre de máquina virtual**: especifica el nombre de la nueva máquina virtual, que debe comenzar con una letra y contener solo letras, números y guiones.</span><span class="sxs-lookup"><span data-stu-id="d7230-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="d7230-123">**Tamaño**: especifica el número de núcleos y la memoria que se asignará para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7230-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="d7230-124">**Nombre de usuario**: especifica la cuenta de administrador que se creará para administrar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7230-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="d7230-125">**Contraseña** y **Confirmar**: especifica la contraseña de la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="d7230-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

    ![La ventana Configuración básica de máquina virtual][CR04]

7. <span data-ttu-id="d7230-127">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d7230-127">Click **Next**.</span></span>

8. <span data-ttu-id="d7230-128">En la ventana **Crear una nueva cuenta de almacenamiento**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d7230-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="d7230-129">**Grupo de recursos**: especifica el grupo de recursos para su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7230-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="d7230-130">Seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="d7230-130">Select one of the following options:</span></span>
      * <span data-ttu-id="d7230-131">**Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d7230-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="d7230-132">**Usar existente**: especifica que desea seleccionar un grupo de recursos que ya está asociado a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7230-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

      ![Cuadro de diálogo Crear una nueva cuenta de almacenamiento][CR05]

   * <span data-ttu-id="d7230-134">**Cuenta de almacenamiento**: especifica la cuenta de almacenamiento que se usará para almacenar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7230-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="d7230-135">Puede usar una cuenta de almacenamiento existente o crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="d7230-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="d7230-136">**Red virtual** y **subred**: especifica la red virtual y subred que se conectará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7230-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="d7230-137">Puede usar una red y subred existentes, o puede crear una nueva red y subred.</span><span class="sxs-lookup"><span data-stu-id="d7230-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="d7230-138">Si selecciona **Crear nuevo**, se mostrará el cuadro de diálogo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7230-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![Cuadro de diálogo Crear una red virtual nueva][CR06]

9. <span data-ttu-id="d7230-140">En la ventana **Recursos asociados**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="d7230-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="d7230-141">**Dirección IP pública**: especifica una dirección IP externa para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7230-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="d7230-142">Puede crear una dirección IP o, si la máquina virtual no tiene una dirección IP pública, puede seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="d7230-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="d7230-143">**Grupo de seguridad de red**: especifica un firewall de red opcional para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7230-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="d7230-144">Puede seleccionar un firewall o, si la máquina virtual no utiliza un firewall, puede seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="d7230-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="d7230-145">**Conjunto de disponibilidad**: especifica un conjunto de disponibilidad opcional al que puede pertenecer su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d7230-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="d7230-146">Puede seleccionar un conjunto de disponibilidad, crear uno o, si la máquina virtual no pertenece a un conjunto de disponibilidad, seleccionar **(Ninguno)**.</span><span class="sxs-lookup"><span data-stu-id="d7230-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![La ventana Recursos asociados][CR07]

9. <span data-ttu-id="d7230-148">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="d7230-148">Click **Finish**.</span></span>  
  <span data-ttu-id="d7230-149">La nueva máquina virtual aparece en la ventana de la herramienta Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="d7230-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

   ![Nueva máquina virtual][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="d7230-151">Reinicio de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="d7230-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="d7230-152">Para reiniciar una máquina virtual mediante Azure Explorer en Eclipse, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d7230-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="d7230-153">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="d7230-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![El comando de reinicio de máquina virtual][RE01]

2. <span data-ttu-id="d7230-155">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d7230-155">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación de Reiniciar][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="d7230-157">Apagado de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="d7230-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="d7230-158">Para apagar una máquina virtual en funcionamiento con Azure Explorer en Eclipse, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d7230-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="d7230-159">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Apagar**.</span><span class="sxs-lookup"><span data-stu-id="d7230-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![El comando de apagado de máquina virtual][SH01]

2. <span data-ttu-id="d7230-161">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d7230-161">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación de apagado de máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="d7230-163">Eliminación de una máquina virtual en Eclipse</span><span class="sxs-lookup"><span data-stu-id="d7230-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="d7230-164">Para eliminar una máquina virtual mediante Azure Explorer en Eclipse, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d7230-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="d7230-165">En la vista **Azure Explorer**, haga clic con el botón derecho en la máquina virtual y elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="d7230-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![El comando de eliminación de máquina virtual][DE01]

2. <span data-ttu-id="d7230-167">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d7230-167">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación de eliminación de máquina virtual][DE02]

## <a name="next-steps"></a><span data-ttu-id="d7230-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7230-169">Next steps</span></span>
<span data-ttu-id="d7230-170">Para obtener más información sobre los tamaños y los precios de máquinas virtuales de Azure, consulte los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="d7230-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="d7230-171">Tamaños de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="d7230-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="d7230-172">[Tamaños de las máquinas virtuales Windows en Azure]</span><span class="sxs-lookup"><span data-stu-id="d7230-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="d7230-173">[Tamaños de las máquinas virtuales Linux en Azure]</span><span class="sxs-lookup"><span data-stu-id="d7230-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="d7230-174">Precios de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="d7230-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="d7230-175">[Precios de máquinas virtuales Windows]</span><span class="sxs-lookup"><span data-stu-id="d7230-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="d7230-176">[Precios de máquinas virtuales Linux]</span><span class="sxs-lookup"><span data-stu-id="d7230-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="d7230-177">Para obtener más información sobre los kits de herramientas de Azure para los IDE de Java, consulte los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="d7230-177">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="d7230-178">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d7230-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d7230-179">[Novedades del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d7230-179">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d7230-180">[Instalación del Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d7230-180">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d7230-181">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d7230-181">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d7230-182">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d7230-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="d7230-183">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d7230-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d7230-184">[Novedades del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d7230-184">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d7230-185">[Instalación del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d7230-185">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d7230-186">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d7230-186">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d7230-187">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d7230-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="d7230-188">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d7230-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="d7230-189">[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="d7230-189">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="d7230-190">[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="d7230-190">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="d7230-191">[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="d7230-191">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="d7230-192">[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="d7230-192">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="d7230-193">[Instalación del Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="d7230-193">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="d7230-194">[Instalación del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="d7230-194">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="d7230-195">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="d7230-195">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="d7230-196">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="d7230-196">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="d7230-197">[Novedades del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="d7230-197">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="d7230-198">[Novedades del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="d7230-198">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="d7230-199">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="d7230-199">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="d7230-200">[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="d7230-200">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="d7230-201">[Tamaños de las máquinas virtuales Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="d7230-201">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="d7230-202">[Tamaños de las máquinas virtuales Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="d7230-202">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="d7230-203">[Precios de máquinas virtuales Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="d7230-203">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="d7230-204">[Precios de máquinas virtuales Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="d7230-204">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>

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
