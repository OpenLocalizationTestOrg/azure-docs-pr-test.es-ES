---
title: "Administración de cuentas de almacenamiento mediante Azure Explorer para Eclipse | Microsoft Docs"
description: "Obtenga información sobre cómo administrar las cuentas de almacenamiento de Azure mediante Azure Explorer para Eclipse."
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
ms.openlocfilehash: 5b3014b5aca368be8ea46863c83665abde10fed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a>Administración de cuentas de almacenamiento mediante Azure Explorer para Eclipse

Azure Explorer, que forma parte del kit de herramientas de Azure para Eclipse, proporciona a los desarrolladores de Java una solución fácil de usar para la administración de cuentas de almacenamiento en su cuenta de Azure desde el entorno de desarrollo integrado de Eclipse (IDE).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a>Creación de una cuenta de almacenamiento en Eclipse

Para crear una cuenta de almacenamiento con Azure Explorer, haga lo siguiente:

1. Inicie sesión en su cuenta de Azure siguiendo los pasos del artículo [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse].

2. En la vista de **Azure Explorer**, expanda el nodo **Azure**, haga clic con el botón derecho en **Cuentas de almacenamiento** y, después, haga clic en **Crear cuenta de almacenamiento**.

   ![Comando Crear cuenta de almacenamiento][CS01]

3. En el cuadro de diálogo**Crear cuenta de almacenamiento**, especifique las siguientes opciones:

   ![Cuadro de diálogo Crear nueva cuenta de almacenamiento][CS02]

   * **Nombre**: especifica el nombre para la nueva cuenta de almacenamiento.

   * **Suscripción**: especifica la suscripción de Azure que quiere usar para la nueva cuenta de almacenamiento.

   * **Grupo de recursos**: especifica el grupo de recursos para su máquina virtual. Seleccione una de las siguientes opciones:
      * **Crear nuevo**: especifica que quiere crear un nuevo grupo de recursos.
      * **Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure.

   * **Región**: especifica la ubicación donde se creará la cuenta de almacenamiento, por ejemplo, "Oeste de EE. UU.".

   * **Tipo de cuenta**: especifica el tipo de cuenta de almacenamiento que se va a crear, por ejemplo, "Blob Storage". Para más información, consulte [Acerca de las cuentas de almacenamiento de Azure].

   * **Rendimiento**: especifica la oferta de cuenta de almacenamiento que quiere usar del publicador seleccionado; por ejemplo, "Premium". Para obtener más información, consulte [Objetivos de escalabilidad y rendimiento de Azure Storage].

   * **Replicación**: especifica la replicación para la cuenta de almacenamiento; por ejemplo, en "Redundancia de zona". Para más información, consulte el artículo sobre la [replicación de Azure Storage].

4. Cuando haya especificado todas las opciones anteriores, haga clic en **Crear**.

## <a name="create-a-storage-container-in-eclipse"></a>Creación de un contenedor de almacenamiento en Eclipse

Para crear un contenedor de almacenamiento con Azure Explorer, haga lo siguiente:

1. En la vista de **Azure Explorer**, haga clic con el botón derecho en la cuenta de almacenamiento donde quiera crear un contenedor y, después, haga clic en **Crear contenedor de blobs**.

   ![Comando Crear contenedor de blobs][CC01]

2. En el cuadro de diálogo **Crear contenedor de blobs**, especifique el nombre para el contenedor y, después, haga clic en **Aceptar**. Para más información sobre la nomenclatura de contenedores de almacenamiento, consulte [Asignar nombres y hacer referencia a contenedores, blobs y metadatos].

   ![Cuadro de diálogo Crear contenedor de blobs][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a>Eliminación de un contenedor de almacenamiento en Eclipse

Para eliminar un contenedor de almacenamiento mediante Azure Explorer, siga estos pasos:

1. En la vista de **Azure Explorer**, haga clic con el botón derecho en el contenedor de almacenamiento y, después, haga clic en **Eliminar**.

   ![Comando Eliminar contenedor de almacenamiento][DC01]

2. En la ventana confirmación, haga clic en **Aceptar**.

   ![Ventana de confirmación Eliminar contenedor de almacenamiento][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a>Eliminación de una cuenta de almacenamiento en Eclipse

Para eliminar una cuenta de almacenamiento con Azure Explorer, haga lo siguiente:

1. En la vista de **Azure Explorer**, haga clic con el botón derecho en la cuenta de almacenamiento y haga clic en **Eliminar**.

   ![Comando Eliminar cuenta de almacenamiento][DS01]

2. En la ventana confirmación, haga clic en **Aceptar**.

   ![Ventana de confirmación Eliminar cuenta de almacenamiento][DS02]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre las cuentas de Azure Storage, tamaños y precios, vea los siguientes recursos:

* [Introducción a Microsoft Azure Storage]
* [Acerca de las cuentas de almacenamiento de Azure]
* Tamaños de cuentas de Azure Storage
  * [Tamaños de las cuentas de almacenamiento de Windows en Azure]
  * [Tamaños de las cuentas de almacenamiento de Linux en Azure]
* Precios de las cuentas de Azure Storage
  * [Precios de cuentas de almacenamiento de Windows]
  * [Precios de cuentas de almacenamiento de Linux]

Para obtener más información sobre los kits de herramientas de Azure para los IDE de Java, consulte los siguientes vínculos:

* [Kit de herramientas de Azure para Eclipse]
  * [Novedades del kit de herramientas de Azure para Eclipse]
  * [Instalación del Kit de herramientas de Azure para Eclipse]
  * [Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [Novedades del kit de herramientas de Azure para IntelliJ]
  * [Instalación del kit de herramientas de Azure para IntelliJ]
  * [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]

Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalación del Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novedades del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novedades del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Introducción a Microsoft Azure Storage]: /azure/storage/storage-introduction
[Acerca de las cuentas de almacenamiento de Azure]: /azure/storage/storage-create-storage-account
[replicación de Azure Storage]: /azure/storage/storage-redundancy
[Objetivos de escalabilidad y rendimiento de Azure Storage]: /azure/storage/storage-scalability-targets
[Asignar nombres y hacer referencia a contenedores, blobs y metadatos]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tamaños de las cuentas de almacenamiento de Windows en Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tamaños de las cuentas de almacenamiento de Linux en Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Precios de cuentas de almacenamiento de Windows]: /pricing/details/virtual-machines/windows/
[Precios de cuentas de almacenamiento de Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
