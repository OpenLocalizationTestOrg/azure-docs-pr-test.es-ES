---
title: aaaSign en instrucciones de hello Azure Toolkit for Eclipse | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosign en Microsoft Azure mediante el uso de hello Azure Toolkit for Eclipse."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Azure inicio de sesión en las instrucciones de hello Azure Toolkit for Eclipse

Hello Azure Toolkit for Eclipse proporciona dos métodos para iniciar sesión en su cuenta de Azure:

  * **Interactivo**: al usar este método, deberá especificar sus credenciales de Azure cada vez que inicie sesión en su cuenta de Azure.
  * **Automatizada** : cuando se usa este método, se creará un archivo de credenciales que contiene los datos de entidad de seguridad de servicio, después del cual puede usar el inicio de sesión de hello credenciales archivo tooautomatically en su cuenta de Azure.

Hello en hello las secciones siguientes se explica cómo toouse cada método.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Inicio de sesión en la cuenta de Azure de forma interactiva

Hello pasos siguientes se ilustran cómo toosign en Azure bien especificando sus credenciales de Azure.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][I01]

1. Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, seleccione **Interactive**y, a continuación, haga clic en **inicio de sesión**.

   ![Cuadro de diálogo Iniciar sesión][I02]

1. Cuando Hola **inicio de sesión Azure** aparece el cuadro de diálogo, escriba sus credenciales de Azure y, a continuación, haga clic en **inicio de sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][I03]

1. Cuando Hola **seleccione suscripciones** aparece en el cuadro de diálogo, las suscripciones que desee toouse y, a continuación, haga clic en hello seleccione **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Cierre de sesión de la cuenta de Azure al iniciar sesión de forma interactiva

Después de haber configurado los pasos de hello en la sección anterior de hello, aparecerá automáticamente la sesión de su cuenta de Azure cada vez que inicie Eclipse. Sin embargo, si desea toosign fuera de su cuenta de Azure sin necesidad de reiniciar Eclipse, utilice Hola pasos.

1. En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. Cuando Hola **Azure Sign Out** aparece el cuadro de diálogo, haga clic en **Sí**.

   ![Cuadro de diálogo Cerrar sesión][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Inicie sesión en su cuenta de Azure de forma automática y la creación de credenciales de un archivo toouse Hola futuras

Hello siguientes pasos le guiarán por la creación de un archivo de credenciales que contiene los datos de entidad de seguridad de servicio. Una vez haya completado estos pasos, will Eclipse automáticamente uso Hola credenciales archivo tooautomatically inicio de sesión que en Azure cada vez que abra el proyecto.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, seleccione **automatizada**y, a continuación, haga clic en **nuevo**.

   ![Cuadro de diálogo Iniciar sesión][A02]

1. Cuando Hola **inicio de sesión Azure** aparece el cuadro de diálogo, escriba sus credenciales de Azure y, a continuación, haga clic en **inicio de sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A03]

1. Cuando Hola **crear archivos de autenticación** aparece en el cuadro de diálogo, las suscripciones que desee toouse, elija el directorio de destino y, a continuación, haga clic en hello seleccione **iniciar**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A04]

1. Hola **estado de creación de entidad de servicio** se mostrará el cuadro de diálogo y después de que los archivos se han creado correctamente, haga clic en **Aceptar**.

   ![Cuadro de diálogo Service Principal Creation Status (Estado de creación de entidades de servicio)][A05]

1. Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, haga clic en **inicio de sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. Cuando Hola **seleccione suscripciones** aparece en el cuadro de diálogo, las suscripciones que desee toouse y, a continuación, haga clic en hello seleccione **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Cierre de sesión de la cuenta de Azure al iniciar sesión de forma automática

Después de haber configurado los pasos de hello en la sección anterior de hello, hello Azure Toolkit iniciará sesión automáticamente en su cuenta de Azure cada vez que inicie Eclipse. Sin embargo, toosign fuera de su cuenta de Azure e impiden que hello Azure Toolkit iniciar sesión automáticamente, un uso Hola pasos.

1. En Eclipse, haga clic en **Herramientas** y, luego, en **Azure** y en **Cerrar sesión**.

   ![Menú de Eclipse para cerrar sesión en Azure][L01]

1. Cuando Hola **Azure Sign Out** aparece el cuadro de diálogo, haga clic en **Sí**.

   ![Cuadro de diálogo Cerrar sesión][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Inicio de sesión en su cuenta de Azure de forma automática y uso de un archivo de credenciales existente

Si cierre la sesión de Azure en Eclipse, necesitará tooreconfigure Hola Kit de herramientas de Azure para Eclipse toouse un archivo de credenciales que ha creado antes de poder firmar automáticamente en su cuenta de Azure. Hello pasos siguientes le guiará por configurar hello Azure Toolkit toouse un archivo de credenciales existente.

1. Abra el proyecto con Eclipse.

1. Haga clic en **Herramientas** y, luego, en **Azure**y en **Iniciar sesión**.

   ![Menú de Eclipse para iniciar sesión en Azure][A01]

1. Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, seleccione **automatizada**y, a continuación, haga clic en **examinar**.

   ![Cuadro de diálogo Iniciar sesión][A02]

1. Cuando Hola **Seleccionar archivo autenticado** aparece el cuadro de diálogo, seleccione un archivo de credenciales que creó anteriormente y, a continuación, haga clic en **seleccione**.

   ![Cuadro de diálogo Iniciar sesión][A08]

1. Cuando Hola **inicio de sesión en Azure** aparece el cuadro de diálogo, haga clic en **inicio de sesión**.

   ![Cuadro de diálogo Inicio de sesión en Microsoft Azure][A06]

1. Cuando Hola **seleccione suscripciones** aparece en el cuadro de diálogo, las suscripciones que desee toouse y, a continuación, haga clic en hello seleccione **Aceptar**.

   ![Cuadro de diálogo Seleccionar suscripciones][A07]

## <a name="see-also"></a>Otras referencias
Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola siguientes vínculos:

* [Kit de herramientas de Azure para Eclipse]
  * [What's New en hello Azure Toolkit for Eclipse]
  * [Instalar hello Azure Toolkit for Eclipse]
  * *Inicio de sesión en las instrucciones de hello Azure Toolkit for Eclipse (de este artículo)*
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [What's New en hello Azure Toolkit for IntelliJ]
  * [Instalación hello Azure Toolkit for IntelliJ]
  * [Inicio de sesión en las instrucciones de hello Azure Toolkit for IntelliJ]
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Inicio de sesión en las instrucciones de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's New en hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New en hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

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
