---
title: las cuentas de almacenamiento de aaaManage mediante el uso de hello Azure explorador para IntelliJ | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage cuentas de su almacenamiento de Azure mediante hello Azure explorador para IntelliJ."
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
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="b89b5-103">Administrar cuentas de almacenamiento mediante hello Azure explorador para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b89b5-103">Manage storage accounts by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="b89b5-104">Hola Explorador de Azure, que forma parte de hello Azure Toolkit for IntelliJ, proporciona a los desarrolladores de Java con una solución fácil de usar para administrar las cuentas de almacenamiento en su cuenta de Azure desde dentro del entorno de desarrollo integrado de hello IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="b89b5-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="b89b5-105">Creación de una cuenta de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b89b5-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="b89b5-106">toocreate una cuenta de almacenamiento mediante el uso de hello Azure explorador, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b89b5-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="b89b5-107">Inicie sesión en tooyour cuenta de Azure mediante hello [instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="b89b5-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span> 

2. <span data-ttu-id="b89b5-108">Hola **explorador Azure** , expanda hello **Azure** nodo, haga clic en **cuentas de almacenamiento**y, a continuación, haga clic en **crear cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="b89b5-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Comando Crear cuenta de almacenamiento][CS01]

3. <span data-ttu-id="b89b5-110">Hola **crear cuenta de almacenamiento** diálogo cuadro, especifique Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="b89b5-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![Cuadro de diálogo Crear nueva cuenta de almacenamiento][CS02]

   * <span data-ttu-id="b89b5-112">**Nombre**: especifica el nombre de Hola Hola nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b89b5-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="b89b5-113">**Tipo de cuenta**: especifica el tipo de saludo de toocreate de cuenta de almacenamiento (por ejemplo, "almacenamiento de blobs").</span><span class="sxs-lookup"><span data-stu-id="b89b5-113">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="b89b5-114">Para más información, consulte [Acerca de las cuentas de almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="b89b5-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="b89b5-115">**Rendimiento**: especifica la cuenta de almacenamiento toouse de la oferta de publicador seleccionado de hello (por ejemplo, "Premium").</span><span class="sxs-lookup"><span data-stu-id="b89b5-115">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="b89b5-116">Para obtener más información, consulte [Objetivos de escalabilidad y rendimiento de Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="b89b5-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="b89b5-117">**Replicación**: especifica la replicación Hola Hola cuenta de almacenamiento (por ejemplo, "con redundancia de zona").</span><span class="sxs-lookup"><span data-stu-id="b89b5-117">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="b89b5-118">Para más información, consulte el artículo sobre la [replicación de Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="b89b5-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="b89b5-119">**Suscripción**: especifica la suscripción de Azure que quiere toouse de nueva cuenta de almacenamiento Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="b89b5-119">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="b89b5-120">**Ubicación**: especifica la ubicación de Hola donde se creará la cuenta de almacenamiento (por ejemplo, "West US").</span><span class="sxs-lookup"><span data-stu-id="b89b5-120">**Location**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="b89b5-121">**Grupo de recursos**: especifica el grupo de recursos de hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b89b5-121">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="b89b5-122">Seleccione una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="b89b5-122">Select one of hello following options:</span></span>
      * <span data-ttu-id="b89b5-123">**Cree una nueva**: Especifica que desea toocreate un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b89b5-123">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="b89b5-124">**Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b89b5-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="b89b5-125">Cuando se ha especificado todas Hola anterior opciones, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b89b5-125">When you have specified all of hello preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="b89b5-126">Creación de un contenedor de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b89b5-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="b89b5-127">toocreate un contenedor de almacenamiento mediante el uso de hello Azure explorador, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b89b5-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="b89b5-128">En hello Azure del explorador, haga clic en cuenta de almacenamiento de Hola donde desee toocreate un contenedor y, a continuación, haga clic en **crear contenedor de blob**.</span><span class="sxs-lookup"><span data-stu-id="b89b5-128">In hello Azure Explorer view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![Comando Crear contenedor de blobs][CC01]

2. <span data-ttu-id="b89b5-130">Hola **crear contenedor de blob** cuadro de diálogo, especifique el nombre de hello para el contenedor y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b89b5-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="b89b5-131">Para más información sobre la nomenclatura de contenedores de almacenamiento, consulte [Asignar nombres y hacer referencia a contenedores, blobs y metadatos].</span><span class="sxs-lookup"><span data-stu-id="b89b5-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Cuadro de diálogo Crear contenedor de almacenamiento][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="b89b5-133">Eliminación de un contenedor de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b89b5-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="b89b5-134">toodelete un contenedor de almacenamiento mediante el uso de hello Azure explorador, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b89b5-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="b89b5-135">Hola Azure del explorador, haga clic en el contenedor de almacenamiento de hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b89b5-135">In hello Azure Explorer view, right-click hello storage container, and then click **Delete**.</span></span>

   ![Comando Eliminar contenedor de almacenamiento][DC01]

2. <span data-ttu-id="b89b5-137">En la ventana de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b89b5-137">In hello confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación Eliminar contenedor de almacenamiento][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="b89b5-139">Eliminación de una cuenta de almacenamiento en IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b89b5-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="b89b5-140">toodelete una cuenta de almacenamiento mediante el uso de hello Azure explorador, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b89b5-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="b89b5-141">Hola **explorador Azure** ver, haga clic en la cuenta de almacenamiento de hello y, a continuación, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b89b5-141">In hello **Azure Explorer** view, right-click hello storage account, and then select **Delete**.</span></span>

   ![Menú Eliminar cuenta de almacenamiento][DS01]

2. <span data-ttu-id="b89b5-143">En la ventana de confirmación de hello, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="b89b5-143">In hello confirmation window, click **Yes**.</span></span>

   ![Ventana de confirmación Eliminar cuenta de almacenamiento][DS02]

## <a name="next-steps"></a><span data-ttu-id="b89b5-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b89b5-145">Next steps</span></span>
<span data-ttu-id="b89b5-146">Para obtener más información acerca de las cuentas de almacenamiento de Azure, tamaños y precios, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b89b5-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="b89b5-147">[Introducción tooMicrosoft almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="b89b5-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="b89b5-148">[Acerca de las cuentas de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="b89b5-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="b89b5-149">Tamaños de cuentas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b89b5-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="b89b5-150">[Tamaños de las cuentas de almacenamiento de Windows en Azure]</span><span class="sxs-lookup"><span data-stu-id="b89b5-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="b89b5-151">[Tamaños de las cuentas de almacenamiento de Linux en Azure]</span><span class="sxs-lookup"><span data-stu-id="b89b5-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="b89b5-152">Precios de las cuentas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b89b5-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="b89b5-153">[Precios de cuentas de almacenamiento de Windows]</span><span class="sxs-lookup"><span data-stu-id="b89b5-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="b89b5-154">[Precios de cuentas de almacenamiento de Linux]</span><span class="sxs-lookup"><span data-stu-id="b89b5-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="b89b5-155">Para obtener más información acerca de los kits de herramientas de Azure para Java IDE, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b89b5-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="b89b5-156">[Kit de herramientas de Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b89b5-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b89b5-157">[Novedades de hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b89b5-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b89b5-158">[Instalar hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b89b5-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b89b5-159">[instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b89b5-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b89b5-160">[Creación de una aplicación web Hello World para Azure en Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b89b5-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="b89b5-161">[Kit de herramientas de Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b89b5-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b89b5-162">[Novedades de hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b89b5-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b89b5-163">[Instalación hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b89b5-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b89b5-164">[Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b89b5-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b89b5-165">[Creación de una aplicación web Hello World para Azure en IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b89b5-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="b89b5-166">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b89b5-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

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

[Introducción tooMicrosoft almacenamiento de Azure]: /azure/storage/storage-introduction
[Acerca de las cuentas de almacenamiento de Azure]: /azure/storage/storage-create-storage-account
[replicación de Azure Storage]: /azure/storage/storage-redundancy
[Objetivos de escalabilidad y rendimiento de Azure Storage]: /azure/storage/storage-scalability-targets
[Asignar nombres y hacer referencia a contenedores, blobs y metadatos]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tamaños de las cuentas de almacenamiento de Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamaños de las cuentas de almacenamiento de Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Precios de cuentas de almacenamiento de Windows]: /pricing/details/virtual-machines/windows/
[Precios de cuentas de almacenamiento de Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
