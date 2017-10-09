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
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a>Administrar máquinas virtuales mediante el uso de hello Azure explorador para IntelliJ

Hola Explorador de Azure, que forma parte de hello Azure Toolkit for IntelliJ, proporciona a los desarrolladores de Java con una solución fácil de usar para administrar máquinas virtuales en su cuenta de Azure desde dentro del entorno de desarrollo integrado de hello IntelliJ (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Creación de una máquina virtual en IntelliJ

toocreate una máquina virtual mediante el uso de hello Azure explorador, Hola siguientes: 

1. Inicie sesión en tooyour cuenta de Azure mediante los pasos de Hola Hola [instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ] artículo.

2. Hola **explorador Azure** , expanda hello **Azure** nodo, haga clic en **máquinas virtuales**y, a continuación, haga clic en **crear VM**. 

   ![Hola comando Crear VM][CR01]  
    Hola **crear nueva máquina Virtual** abre el asistente.

3. Hola **elegir una suscripción** ventana, seleccione su suscripción y, a continuación, haga clic en **siguiente**. 

   ![Hola elegir una ventana de suscripción][CR02]

4. Hola **seleccionar una imagen de máquina Virtual** ventana, escriba Hola siguiente información:

   * **Ubicación**: especifica la ubicación donde se creará la máquina virtual (por ejemplo, *oeste de EE. UU.*). 

   * **Imagen recomendada**: especifica que elegirá una imagen de una lista abreviada de imágenes usadas con frecuencia.

   * **Imagen personalizada**: Especifica que elegirá una imagen personalizada proporcionando Hola siguiente información:

      * **Publisher**: especifica el publicador de Hola que creó la imagen de Hola que va a utilizar para la máquina virtual (por ejemplo, *Microsoft*).

      * **Ofrecer**: especifica la máquina virtual de hello toouse la oferta de publicador seleccionado hello (por ejemplo, *JDK*).

      * **SKU**: especifica Hola toouse de almacén (SKU) de almacenamiento de oferta de hello seleccionado (por ejemplo, *JDK_8*).

      * **Versión #**: especifica qué versión de Hola seleccionado toouse SKU.

   ![Hola seleccionar una ventana de la imagen de máquina Virtual][CR03]

5. Haga clic en **Siguiente**. 

6. Hola **configuración básica de máquina Virtual** ventana, escriba Hola siguiente información:

   * **Nombre de máquina virtual**: especifica el nombre de hello para la nueva máquina virtual, que debe empezar por una letra y contener solo letras, números y guiones.

   * **Tamaño**: especifica el número de Hola de núcleos y memoria tooallocate para la máquina virtual.

   * **Nombre de usuario**: especifica hello toocreate de cuenta de administrador para administrar la máquina virtual.

   * **Contraseña** y **confirmar**: especifica la contraseña de hello para la cuenta de administrador.

   ![ventana de configuración de máquina Virtual básica Hello][CR04]

7. Haga clic en **Siguiente**. 

8. Hola **recursos asociados** ventana, escriba Hola siguiente información:

   * **Grupo de recursos**: especifica el grupo de recursos de hello para la máquina virtual. Seleccione una de las siguientes opciones de hello:
      * **Cree una nueva**: Especifica que desea toocreate un nuevo grupo de recursos.
      * **Usar existente**: Especifica que desea tooselect en una lista de grupos de recursos que están asociados a su cuenta de Azure.

       ![ventana de Hello recursos asociados][CR07]

   * **Cuenta de almacenamiento**: especifica hello toouse de cuenta de almacenamiento para almacenar la máquina virtual. Puede usar una cuenta de almacenamiento o crear una. Si elige **crear nuevo**, aparece hello después el cuadro de diálogo:

      ![cuadro de diálogo Crear cuenta de almacenamiento de Hola][CR05]

   * **Red virtual** y **subred**: especifica la red virtual de Hola y de las subredes que se conectará la máquina virtual. Puede usar una red y subred existentes, o puede crear una nueva red y subred. Si selecciona **crear nuevo**, aparece hello después el cuadro de diálogo:

      ![cuadro de diálogo de creación de red Virtual de Hola][CR06]

   * **Dirección IP pública**: especifica una dirección IP externa para la máquina virtual. Puede elegir una nueva dirección IP toocreate o, si la máquina virtual no tiene una dirección IP pública, puede seleccionar **(ninguno)**. 

   * **Grupo de seguridad de red**: especifica un firewall de red opcional para la máquina virtual. Puede seleccionar un firewall o, si la máquina virtual no utiliza un firewall, puede seleccionar **(Ninguno)**. 

   * **Conjunto de disponibilidad**: especifica un conjunto de disponibilidad opcional al que puede pertenecer su máquina virtual. Puede seleccionar un conjunto de disponibilidad existente, cree un nuevo conjunto de disponibilidad o, si la máquina virtual no pertenecerá tooan conjunto de disponibilidad, seleccione **(ninguno)**.

9. Haga clic en **Finalizar**  
    La nueva máquina virtual aparece en la ventana de herramientas del explorador de Azure de Hola. 

   ![Máquina virtual nueva en hello Azure del explorador][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Reinicio de una máquina virtual en IntelliJ

una máquina virtual mediante el uso de hello Azure explorador en IntelliJ, toorestart Hola siguientes:

1. Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **reiniciar**.

   ![comando de reinicio de máquina virtual de Hola][RE01]

2. En la ventana de confirmación de hello, haga clic en **Sí**. 

   ![Hola reiniciar la ventana de confirmación de la máquina virtual][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Apagado de una máquina virtual en IntelliJ

tooshut hacia abajo una máquina virtual en ejecución mediante el uso de hello Azure explorador en IntelliJ, Hola siguientes:

1. Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **apagado**.

   ![comando de apagado de máquina virtual de Hola][SH01]

2. En la ventana de confirmación de hello, haga clic en **Sí**. 

   ![Hola cerrar la ventana de confirmación de la máquina virtual][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Eliminación de una máquina virtual en IntelliJ

una máquina virtual mediante el uso de hello Azure explorador en IntelliJ, toodelete Hola siguientes:

1. Hola **explorador Azure** ver, haga clic en la máquina virtual de hello y, a continuación, seleccione **eliminar**.

   ![comando de eliminación de máquina virtual de Hola][DE01]

2. En la ventana de confirmación de hello, haga clic en **Sí**. 

   ![Hola eliminar la ventana de confirmación de la máquina virtual][DE02]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los tamaños de máquina virtual de Azure y los precios, vea Hola recursos siguientes:

* Tamaños de máquinas virtuales de Azure
  * [Tamaños de las máquinas virtuales Windows en Azure]
  * [Tamaños de las máquinas virtuales Linux en Azure]
* Precios de máquinas virtuales de Azure
  * [Precios de máquinas virtuales Windows]
  * [Precios de máquinas virtuales Linux]

Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola recursos siguientes:

* [Kit de herramientas de Azure para Eclipse]
  * [Novedades de hello Azure Toolkit for Eclipse]
  * [Instalar hello Azure Toolkit for Eclipse]
  * [Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [Novedades de hello Azure Toolkit for IntelliJ]
  * [Instalación hello Azure Toolkit for IntelliJ]
  * [instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ]
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]

Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y la página de [herramientas de Java para Visual Studio Team Services].

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
