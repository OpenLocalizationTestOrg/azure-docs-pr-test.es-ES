---
title: instrucciones de aaaSign para hello Azure Toolkit para IntelliJ | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosign en tooMicrosoft Azure mediante el uso de Hola Kit de herramientas de Azure para IntelliJ."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ

Hello Azure Toolkit for IntelliJ proporciona dos métodos para iniciar sesión en tooyour cuenta de Azure:

  * **Interactivo**: escriba sus credenciales de Azure cada vez que inicie sesión en tooyour cuenta de Azure.
  * **Automatizada**: crear un archivo de credenciales que puede usar el inicio de sesión de tooautomatically en tooyour cuenta de Azure.

Hello siguientes secciones se describen cómo toouse cada método.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Iniciar sesión en tooyour cuenta de Azure de forma interactiva

toosign en tooAzure bien especificando sus credenciales de Azure, Hola siguientes:

1. Abra el proyecto con IntelliJ IDEA.

2. Haga clic en **herramientas**, seleccione demasiado**Azure**y, a continuación, haga clic en **inicio de sesión de Azure en**.

   ![comando de inicio de sesión en Azure IntelliJ Hola][I01]

3. Hola **inicio de sesión en Azure** ventana, seleccione **Interactive**y, a continuación, haga clic en **iniciar sesión en**.

   ![inicio de sesión de Azure en ventana Hello con interactivo seleccionado][I02]

4. Hola **inicio de sesión Azure** aparece el cuadro de diálogo, escriba sus credenciales de Azure y, a continuación, haga clic en **iniciar sesión en**.

   ![cuadro de diálogo de inicio de sesión de Azure de Hola][I03]

5. Hola **seleccione suscripciones** cuadro de diálogo, las suscripciones de hello select que desee toouse y, a continuación, haga clic en **Aceptar**.

   ![cuadro de diálogo Seleccionar suscripciones Hola][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva

Después de haber configurado la cuenta mediante el uso de hello pasos anteriores, se cerrará sesión automáticamente en su cuenta de Azure cada vez que inicie IntelliJ IDEA. Sin embargo, si desea que toosign fuera de su cuenta de Azure *sin* reiniciar IntelliJ IDEA, Hola después.

1. En la IDEA de IntelliJ, en hello **herramientas** menú, seleccione demasiado**Azure**y, a continuación, haga clic en **Azure Sign Out**.

   ![Hola comando IntelliJ el inicio de sesión de Azure Out][L01]

2. Hola **Azure Sign Out** ventana de confirmación, haga clic en **Sí**.

   ![ventana Hello Azure Sign Out confirmación][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Iniciar sesión en tooyour cuenta de Azure automáticamente

Los siguientes pasos lo guiarán por el proceso de creación de un archivo de credenciales que contiene los datos de entidades de servicio. Después de completar este proceso, Eclipse usa Hola credenciales archivo tooautomatically inicio de sesión que de tooAzure cada vez que abra el proyecto.

1. Abra el proyecto con IntelliJ IDEA.

2. En hello **herramientas** menú, seleccione demasiado**Azure**y, a continuación, haga clic en **inicio de sesión de Azure en**.

   ![comando de inicio de sesión en Azure IntelliJ Hola][A01]

3. Hola **inicio de sesión en Azure** ventana, seleccione **automatizada**y, a continuación, haga clic en **nuevo**.

   ![inicio de sesión de Azure en ventana Hello con automática seleccionada][A02]

4. Hola **cuadro de diálogo de inicio de sesión de Azure** ventana, escriba sus credenciales de Azure y, a continuación, haga clic en **iniciar sesión en**.

   ![cuadro de diálogo de inicio de sesión de Azure de Hola][A03]

5. Hola **crear archivos de autenticación** (ventana), las suscripciones de hello select que desee toouse, elija el directorio de destino y, a continuación, haga clic en **iniciar**.

   ![ventana de Hello crear archivos de autenticación][A04]

6. Hola **estado de creación de entidad de servicio** cuadro de diálogo, después de que los archivos se han creado correctamente, haga clic en **Aceptar**.

   ![Hola, cuadro de diálogo de estado de creación de entidad de servicio][A05]

7. Hola **inicio de sesión en Azure** ventana, haga clic en **iniciar sesión en**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

8. Hola **seleccione suscripciones** cuadro de diálogo, las suscripciones de hello select que desee toouse y, a continuación, haga clic en **Aceptar**.

   ![cuadro de diálogo Seleccionar suscripciones Hola][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Cierre de sesión de la cuenta de Azure después de haber iniciado sesión de forma automática

Después de haber configurado la cuenta mediante el uso de hello pasos anteriores, hello Azure Toolkit inicia automáticamente la sesión en tooyour cuenta de Azure cada vez que inicie IntelliJ IDEA. Sin embargo, toosign fuera de su cuenta de Azure y evitar hello Azure Toolkit de iniciar sesión automáticamente, Hola siguientes:

1. En la IDEA de IntelliJ, en hello **herramientas** menú, seleccione demasiado**Azure**y, a continuación, haga clic en **Azure Sign Out**.

   ![Hola comando IntelliJ el inicio de sesión de Azure Out][L01]

2. Hola **Azure Sign Out** ventana de confirmación, haga clic en **Sí**.

   ![ventana Hello Azure Sign Out confirmación][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Inicie sesión en tooyour cuenta de Azure automáticamente mediante un archivo de credenciales existente

Si cierre la sesión de su cuenta de Azure cuando se utiliza la IDEA de IntelliJ, debe utilizar un inicio de sesión de tooautomatically de archivo de credenciales existente en toohello cuenta. Hola tooconfigure Kit de herramientas de Azure para Eclipse toouse un archivo de credenciales existente, Hola siguientes:

1. Abra el proyecto con IntelliJ IDEA.

2. En hello **herramientas** menú, seleccione demasiado**Azure**y, a continuación, haga clic en **inicio de sesión de Azure en**.

   ![comando de inicio de sesión en Azure IntelliJ Hola][A01]

3. Hola **inicio de sesión en Azure** ventana, seleccione **automatizada**y, a continuación, haga clic en **examinar**.

   ![inicio de sesión de Azure en ventana Hello con automática seleccionada][A02]

4. Hola **Seleccionar archivo de autenticación** cuadro de diálogo, seleccione un archivo de credenciales creado anteriormente y, a continuación, haga clic en **seleccione**.

   ![cuadro de diálogo Seleccionar archivo de autenticación de Hola][A08]

5. Hola **inicio de sesión en Azure** ventana, haga clic en **iniciar sesión en**.

   ![inicio de sesión de Azure en ventana Hello con automática seleccionada][A06]

6. Hola **seleccione suscripciones** cuadro de diálogo, las suscripciones de hello select que desee toouse y, a continuación, haga clic en **Aceptar**.

   ![cuadro de diálogo Seleccionar suscripciones Hola][A07]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola siguientes vínculos:

* [Kit de herramientas de Azure para Eclipse]
  * [Novedades de hello Azure Toolkit for Eclipse]
  * [Instalar hello Azure Toolkit for Eclipse]
  * [Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [Novedades de hello Azure Toolkit for IntelliJ]
  * [Instalación hello Azure Toolkit for IntelliJ]
  * *Instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ* (en este artículo)
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrucciones de inicio de sesión para hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novedades de hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novedades de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
