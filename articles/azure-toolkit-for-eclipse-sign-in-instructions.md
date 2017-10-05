---
title: "Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse | Microsoft Docs"
description: "Obtenga información sobre cómo iniciar sesión en Microsoft Azure utilizando el Kit de herramientas de Azure para Eclipse."
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
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse

El kit de herramientas de Azure para Eclipse proporciona dos métodos para iniciar sesión en su cuenta de Azure:

  * **Interactivo**: al usar este método, deberá especificar sus credenciales de Azure cada vez que inicie sesión en su cuenta de Azure.
  * **Automatizado**: al utilizar este método, se creará un archivo de credenciales que contiene los datos de entidades de seguridad de servicio. Después, podrá utilizar el archivo de credenciales para iniciar sesión automáticamente en su cuenta de Azure.

Los pasos descritos en las secciones siguientes explican cómo utilizar cada método.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Inicio de sesión en la cuenta de Azure de forma interactiva

En los pasos siguientes se explica cómo iniciar sesión en Azure especificando manualmente las credenciales de Azure.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][I01]

1. Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Interactivo** y, luego, haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Iniciar sesión][I02]

1. Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva

Después de haber configurado los pasos en la sección anterior, se cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie Eclipse. Sin embargo, si desea cerrar sesión de su cuenta de Azure sin tener que reiniciar Eclipse, siga estos pasos.

1. En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.

   ![Cuadro de diálogo Cerrar sesión][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a>Inicio de sesión en su cuenta de Azure de forma automática y creación de un archivo de credenciales para utilizarlo en el futuro

Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de seguridad de servicio. Cuando finalice estos pasos, Eclipse usará automáticamente el archivo de credenciales para iniciar sesión automáticamente en Azure cada vez que abra el proyecto.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Nuevo**.

   ![Cuadro de diálogo Iniciar sesión][A02]

1. Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, escriba sus credenciales de Azure y, luego, haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A03]

1. Cuando se muestre el cuadro de diálogo **Create authentication files** (Crear archivos de autenticación), seleccione las suscripciones que desea utilizar, elija el directorio de destino y, luego, haga clic en **Iniciar**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A04]

1. Se mostrará el cuadro de diálogo **Service Principal Creation Status** (Estado de creación de entidades de servicio) y, una vez que se hayan creado correctamente los archivos, haga clic en **Aceptar**.

   ![Cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

1. Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure** , haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Cierre de sesión de la cuenta de Azure al iniciar sesión de forma automática

Después de haber configurado los pasos en la sección anterior, el kit de herramientas de Azure cerrará automáticamente la sesión de su cuenta de Azure cada vez que reinicie Eclipse. Sin embargo, para cerrar la sesión de su cuenta de Azure e impedir que el kit de herramientas de Azure inicie sesión automáticamente, siga estos pasos.

1. En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. Cuando se muestre el cuadro de diálogo **Cierre de sesión en Microsoft Azure** , haga clic en **Sí**.

   ![Cuadro de diálogo Cerrar sesión][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Inicio de sesión en su cuenta de Azure de forma automática y uso de un archivo de credenciales existente

Si cierra la sesión de Azure al utilizar Eclipse, debe volver a configurar el kit de herramientas de Azure para Eclipse con el fin de usar un archivo de credenciales ya creado antes de poder iniciar sesión automáticamente en su cuenta de Azure. Los siguientes pasos lo guiarán a través del proceso de configuración del kit de herramientas de Azure para usar un archivo de credenciales existente.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. Cuando se muestra el cuadro de diálogo **Inicio de sesión en Microsoft Azure**, seleccione **Automatizado** y, luego, haga clic en **Examinar**.

   ![Cuadro de diálogo Iniciar sesión][A02]

1. Cuando se muestra el cuadro de diálogo **Select Authentication File** (Seleccionar archivo de autenticación), elija un archivo de credenciales que creó anteriormente y, luego, haga clic en **Seleccionar**.

   ![Cuadro de diálogo Iniciar sesión][A08]

1. Cuando se muestre el cuadro de diálogo **Inicio de sesión en Microsoft Azure** , haga clic en **Iniciar sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. Cuando se muestre el cuadro de diálogo **Seleccionar suscripciones**, seleccione las suscripciones que desea usar y, luego, haga clic en **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="see-also"></a>Otras referencias
Para más información acerca de los kits de herramientas de Azure para los IDE de Java, vea los siguientes vínculos:

* [Kit de herramientas de Azure para Eclipse]
  * [Novedades del kit de herramientas de Azure para Eclipse]
  * [Instalación del Kit de herramientas de Azure para Eclipse]
  * *Instrucciones de inicio de sesión del kit de herramientas de Azure para Eclipse* (este artículo)
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [Novedades del kit de herramientas de Azure para IntelliJ]
  * [Instalación del kit de herramientas de Azure para IntelliJ]
  * [Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]

Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalación del Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instrucciones de inicio de sesión del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novedades del kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novedades del kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
