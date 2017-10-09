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
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a>Administrar cuentas de almacenamiento mediante hello Azure explorador para IntelliJ

Hola Explorador de Azure, que forma parte de hello Azure Toolkit for IntelliJ, proporciona a los desarrolladores de Java con una solución fácil de usar para administrar las cuentas de almacenamiento en su cuenta de Azure desde dentro del entorno de desarrollo integrado de hello IntelliJ (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Creación de una cuenta de almacenamiento en IntelliJ

toocreate una cuenta de almacenamiento mediante el uso de hello Azure explorador, Hola siguientes:

1. Inicie sesión en tooyour cuenta de Azure mediante hello [instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]. 

2. Hola **explorador Azure** , expanda hello **Azure** nodo, haga clic en **cuentas de almacenamiento**y, a continuación, haga clic en **crear cuenta de almacenamiento**.

   ![Comando Crear cuenta de almacenamiento][CS01]

3. Hola **crear cuenta de almacenamiento** diálogo cuadro, especifique Hola siguientes opciones:

   ![Cuadro de diálogo Crear nueva cuenta de almacenamiento][CS02]

   * **Nombre**: especifica el nombre de Hola Hola nueva cuenta de almacenamiento.

   * **Tipo de cuenta**: especifica el tipo de saludo de toocreate de cuenta de almacenamiento (por ejemplo, "almacenamiento de blobs"). Para más información, consulte [Acerca de las cuentas de almacenamiento de Azure]. 

   * **Rendimiento**: especifica la cuenta de almacenamiento toouse de la oferta de publicador seleccionado de hello (por ejemplo, "Premium"). Para obtener más información, consulte [Objetivos de escalabilidad y rendimiento de Azure Storage]. 

   * **Replicación**: especifica la replicación Hola Hola cuenta de almacenamiento (por ejemplo, "con redundancia de zona"). Para más información, consulte el artículo sobre la [replicación de Azure Storage]. 

   * **Suscripción**: especifica la suscripción de Azure que quiere toouse de nueva cuenta de almacenamiento Hola Hola.

   * **Ubicación**: especifica la ubicación de Hola donde se creará la cuenta de almacenamiento (por ejemplo, "West US").

   * **Grupo de recursos**: especifica el grupo de recursos de hello para la máquina virtual. Seleccione una de las siguientes opciones de hello:
      * **Cree una nueva**: Especifica que desea toocreate un nuevo grupo de recursos.
      * **Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure.

4. Cuando se ha especificado todas Hola anterior opciones, haga clic en **Aceptar**.

## <a name="create-a-storage-container-in-intellij"></a>Creación de un contenedor de almacenamiento en IntelliJ

toocreate un contenedor de almacenamiento mediante el uso de hello Azure explorador, Hola siguientes:

1. En hello Azure del explorador, haga clic en cuenta de almacenamiento de Hola donde desee toocreate un contenedor y, a continuación, haga clic en **crear contenedor de blob**.

   ![Comando Crear contenedor de blobs][CC01]

2. Hola **crear contenedor de blob** cuadro de diálogo, especifique el nombre de hello para el contenedor y, a continuación, haga clic en **Aceptar**. Para más información sobre la nomenclatura de contenedores de almacenamiento, consulte [Asignar nombres y hacer referencia a contenedores, blobs y metadatos].

   ![Cuadro de diálogo Crear contenedor de almacenamiento][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Eliminación de un contenedor de almacenamiento en IntelliJ

toodelete un contenedor de almacenamiento mediante el uso de hello Azure explorador, Hola siguientes:

1. Hola Azure del explorador, haga clic en el contenedor de almacenamiento de hello y, a continuación, haga clic en **eliminar**.

   ![Comando Eliminar contenedor de almacenamiento][DC01]

2. En la ventana de confirmación de hello, haga clic en **Sí**.

   ![Ventana de confirmación Eliminar contenedor de almacenamiento][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Eliminación de una cuenta de almacenamiento en IntelliJ

toodelete una cuenta de almacenamiento mediante el uso de hello Azure explorador, Hola siguientes:

1. Hola **explorador Azure** ver, haga clic en la cuenta de almacenamiento de hello y, a continuación, seleccione **eliminar**.

   ![Menú Eliminar cuenta de almacenamiento][DS01]

2. En la ventana de confirmación de hello, haga clic en **Sí**.

   ![Ventana de confirmación Eliminar cuenta de almacenamiento][DS02]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de las cuentas de almacenamiento de Azure, tamaños y precios, vea Hola recursos siguientes:

* [Introducción tooMicrosoft almacenamiento de Azure]
* [Acerca de las cuentas de almacenamiento de Azure]
* Tamaños de cuentas de Azure Storage
  * [Tamaños de las cuentas de almacenamiento de Windows en Azure]
  * [Tamaños de las cuentas de almacenamiento de Linux en Azure]
* Precios de las cuentas de Azure Storage
  * [Precios de cuentas de almacenamiento de Windows]
  * [Precios de cuentas de almacenamiento de Linux]

Para obtener más información acerca de los kits de herramientas de Azure para Java IDE, vea Hola recursos siguientes:

* [Kit de herramientas de Azure para Eclipse]
  * [Novedades de hello Azure Toolkit for Eclipse]
  * [Instalar hello Azure Toolkit for Eclipse]
  * [instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [Novedades de hello Azure Toolkit for IntelliJ]
  * [Instalación hello Azure Toolkit for IntelliJ]
  * [Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]

Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].

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
