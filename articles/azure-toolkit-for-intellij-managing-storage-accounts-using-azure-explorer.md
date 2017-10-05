---
title: "Administración de cuentas de almacenamiento mediante Azure Explorer para IntelliJ | Microsoft Docs"
description: "Obtenga información sobre cómo administrar las cuentas de Azure Storage mediante Azure Explorer para IntelliJ."
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
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="3ba68-103">Administración de cuentas de almacenamiento mediante Azure Explorer para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3ba68-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="3ba68-104">Azure Explorer, que forma parte del kit de herramientas de Azure para IntelliJ, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de cuentas de almacenamiento en su cuenta de Azure desde el entorno de desarrollo integrado de IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="3ba68-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="3ba68-105">Creación de una cuenta de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3ba68-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="3ba68-106">Para crear una cuenta de almacenamiento con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ba68-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3ba68-107">Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3ba68-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span> 

2. <span data-ttu-id="3ba68-108">En la vista de **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Cuentas de almacenamiento** y, después, haga clic en **Crear cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="3ba68-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Comando Crear cuenta de almacenamiento][CS01]

3. <span data-ttu-id="3ba68-110">En el cuadro de diálogo**Crear cuenta de almacenamiento**, especifique las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="3ba68-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Cuadro de diálogo Crear nueva cuenta de almacenamiento][CS02]

   * <span data-ttu-id="3ba68-112">**Nombre**: especifica el nombre para la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3ba68-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="3ba68-113">**Tipo de cuenta**: especifica el tipo de cuenta de almacenamiento que se va a crear, por ejemplo, "Blob Storage".</span><span class="sxs-lookup"><span data-stu-id="3ba68-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="3ba68-114">Para más información, consulte [Acerca de las cuentas de almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="3ba68-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="3ba68-115">**Rendimiento**: especifica la oferta de cuenta de almacenamiento que quiere usar del publicador seleccionado; por ejemplo, "Premium".</span><span class="sxs-lookup"><span data-stu-id="3ba68-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="3ba68-116">Para obtener más información, consulte [Objetivos de escalabilidad y rendimiento de Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="3ba68-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="3ba68-117">**Replicación**: especifica la replicación para la cuenta de almacenamiento; por ejemplo, en "Redundancia de zona".</span><span class="sxs-lookup"><span data-stu-id="3ba68-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="3ba68-118">Para obtener más información, vea el artículo de [replicación de Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="3ba68-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="3ba68-119">**Suscripción**: especifica la suscripción de Azure que quiere usar para la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3ba68-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="3ba68-120">**Ubicación**: especifica la ubicación donde se creará la cuenta de almacenamiento; por ejemplo, "oeste de EE. UU.".</span><span class="sxs-lookup"><span data-stu-id="3ba68-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="3ba68-121">**Grupo de recursos**: especifica el grupo de recursos para su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3ba68-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="3ba68-122">Seleccione una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="3ba68-122">Select one of the following options:</span></span>
      * <span data-ttu-id="3ba68-123">**Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3ba68-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="3ba68-124">**Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba68-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="3ba68-125">Cuando haya especificado todas las opciones anteriores, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3ba68-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="3ba68-126">Creación de un contenedor de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3ba68-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="3ba68-127">Para crear un contenedor de almacenamiento con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ba68-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3ba68-128">En la vista de Azure Explorer, haga clic con el botón derecho en la cuenta de almacenamiento donde quiera crear un contenedor y, después, haga clic en **Crear contenedor de blobs**.</span><span class="sxs-lookup"><span data-stu-id="3ba68-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Comando Crear contenedor de blobs][CC01]

2. <span data-ttu-id="3ba68-130">En el cuadro de diálogo **Crear contenedor de blobs**, especifique el nombre para el contenedor y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3ba68-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="3ba68-131">Para obtener más información sobre la nomenclatura de contenedores de almacenamiento, vea [Asignar nombres y hacer referencia a contenedores, blobs y metadatos].</span><span class="sxs-lookup"><span data-stu-id="3ba68-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Cuadro de diálogo Crear contenedor de almacenamiento][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="3ba68-133">Eliminación de un contenedor de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3ba68-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="3ba68-134">Para eliminar un contenedor de almacenamiento mediante Azure Explorer, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3ba68-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3ba68-135">En la vista de Azure Explorer, haga clic con el botón derecho en el contenedor de almacenamiento y, después, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="3ba68-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Comando Eliminar contenedor de almacenamiento][DC01]

2. <span data-ttu-id="3ba68-137">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="3ba68-137">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación Eliminar contenedor de almacenamiento][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="3ba68-139">Eliminación de una cuenta de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3ba68-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="3ba68-140">Para crear una cuenta de almacenamiento con Azure Explorer, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ba68-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="3ba68-141">En la vista de **Azure Explorer**, haga clic con el botón derecho en la cuenta de almacenamiento y seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="3ba68-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Menú Eliminar cuenta de almacenamiento][DS01]

2. <span data-ttu-id="3ba68-143">En la ventana confirmación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="3ba68-143">In the confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación Eliminar cuenta de almacenamiento][DS02]

## <a name="next-steps"></a><span data-ttu-id="3ba68-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ba68-145">Next steps</span></span>
<span data-ttu-id="3ba68-146">Para obtener más información sobre las cuentas de Azure Storage, tamaños y precios, vea los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="3ba68-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="3ba68-147">[Introducción a Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="3ba68-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="3ba68-148">[Acerca de las cuentas de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="3ba68-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="3ba68-149">Tamaños de cuentas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3ba68-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="3ba68-150">[Tamaños de las cuentas de almacenamiento de Windows en Azure]</span><span class="sxs-lookup"><span data-stu-id="3ba68-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="3ba68-151">[Tamaños de las cuentas de almacenamiento de Linux en Azure]</span><span class="sxs-lookup"><span data-stu-id="3ba68-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="3ba68-152">Precios de las cuentas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3ba68-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="3ba68-153">[Precios de cuentas de almacenamiento de Windows]</span><span class="sxs-lookup"><span data-stu-id="3ba68-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="3ba68-154">[Precios de cuentas de almacenamiento de Linux]</span><span class="sxs-lookup"><span data-stu-id="3ba68-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="3ba68-155">Para obtener más información sobre los kits de herramientas de Azure para los IDE de Java, consulte los siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="3ba68-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="3ba68-156">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3ba68-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3ba68-157">[Novedades del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3ba68-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3ba68-158">[Instalación del Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3ba68-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3ba68-159">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3ba68-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3ba68-160">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3ba68-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="3ba68-161">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3ba68-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3ba68-162">[Novedades del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3ba68-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3ba68-163">[Instalación del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3ba68-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3ba68-164">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3ba68-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3ba68-165">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3ba68-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="3ba68-166">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="3ba68-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="3ba68-167">[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="3ba68-168">[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="3ba68-169">[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="3ba68-170">[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="3ba68-171">[Instalación del Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="3ba68-172">[Instalación del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="3ba68-173">[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="3ba68-174">[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="3ba68-175">[Novedades del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="3ba68-176">[Novedades del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="3ba68-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="3ba68-177">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="3ba68-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="3ba68-178">[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="3ba68-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="3ba68-179">[Introducción a Microsoft Azure Storage]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="3ba68-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="3ba68-180">[Acerca de las cuentas de almacenamiento de Azure]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="3ba68-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="3ba68-181">[replicación de Azure Storage]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="3ba68-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="3ba68-182">[Objetivos de escalabilidad y rendimiento de Azure Storage]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="3ba68-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="3ba68-183">[Asignar nombres y hacer referencia a contenedores, blobs y metadatos]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="3ba68-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="3ba68-184">[Tamaños de las cuentas de almacenamiento de Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="3ba68-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="3ba68-185">[Tamaños de las cuentas de almacenamiento de Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="3ba68-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="3ba68-186">[Precios de cuentas de almacenamiento de Windows]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="3ba68-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="3ba68-187">[Precios de cuentas de almacenamiento de Linux]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="3ba68-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png