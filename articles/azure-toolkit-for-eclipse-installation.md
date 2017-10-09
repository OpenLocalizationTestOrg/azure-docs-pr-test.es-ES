---
title: Hola aaaInstalling Azure Toolkit for Eclipse | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall hello Azure Toolkit for Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6c195fab2b47fb5c42541a8cf52be4ec88d27b5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="installing-hello-azure-toolkit-for-eclipse"></a>Instalar hello Azure Toolkit for Eclipse
Hola Kit de herramientas de Azure para Eclipse ofrece plantillas y funciones que le permiten tooeasily crean, desarrollar, probar e implementar aplicaciones de Azure mediante el entorno de desarrollo Eclipse Hola. Hello Azure Toolkit for Eclipse es un proyecto de código abierto. código fuente de Hello está disponible bajo licencia MIT Hola de <https://github.com/microsoft/azure-tools-for-java>.

Hola siguientes pasos muestra cómo tooinstall hello Azure Toolkit for Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a>Hola tooinstall Kit de herramientas de Azure para Eclipse
1. Inicie Eclipse.
2. Haga clic en hello **ayuda** menú y, a continuación, haga clic en **instalar nuevo Software**, tal y como se muestra en hello siguiente ilustración.
   
    ![Instalar hello Azure Toolkit for Eclipse][01]
3. Hola **Software disponible** cuadro de diálogo, en hello **trabajar con** cuadro de texto, escriba `http://dl.microsoft.com/eclipse` seguido de hello **ENTRAR** clave.
4. Hola **nombre** panel, verificación **Azure Toolkit for Eclipse**y desactive la opción **póngase en contacto con todos los sitios de actualizaciones durante instalar software de toofind necesario**. La pantalla debe ser similar siguiente toohello:
   
    ![Instalar hello Azure Toolkit for Eclipse][02]
5. Si expande hello **Azure Toolkit for Eclipse**, verá Hola siguientes elementos:
   
   * **Complemento de información de aplicación de Java**: este componente permite los servicios de registro y análisis de telemetría de Azure toouse para las aplicaciones y las instancias de servidor.
   * **Filtro de servicios de Control de acceso a Azure**: este componente ofrece compatibilidad para autenticar a los usuarios de aplicación con ACS de Azure, lo que permite escenarios de inicio de sesión único y externalización de lógica de la identidad de aplicación hello.
   * **El complemento de Azure comunes**: este componente proporciona la funcionalidad común de hello necesaria para otros componentes del Kit de herramientas.
   * **Explorador de Azure para Eclipse**: este componente proporciona la funcionalidad común de hello necesaria para otros componentes del Kit de herramientas.
   * **El complemento de Azure para Eclipse con Java**: este componente proporciona soporte técnico para desarrollar proyectos que le ayudan a compilar, probar e implementar aplicaciones de Java para la nube de Microsoft Azure hello en Eclipse y a través de la línea de comandos.
   * **El complemento de aplicaciones Web Azure con Java**: este componente ofrece compatibilidad para la implementación de contenedores de Java web aplicaciones tooMicrosoft aplicación Web de Azure.
   * **Microsoft JDBC Driver 4.2 para SQL Server**: este componente proporciona la API de JDBC API para SQL Server y Microsoft Azure SQL Database para Java Platform Enterprise Edition 8.
   * **Paquete para bibliotecas de cliente de Apache Qpid para JMS**: este componente proporciona el componente de cliente JMS Hola de hello Apache Qpid proyecto tooenable su aplicación toouse AMQP de mensajería de Microsoft Azure.
   * **Paquete para bibliotecas de Microsoft Azure para Java**: este componente proporciona las API para acceder a los servicios de Microsoft Azure, como almacenamiento, service bus, runtime de servicio, etc.
6. Haga clic en **Siguiente**. (Si se producen retrasos inusuales al instalar el Kit de herramientas de hello, asegúrese de que **póngase en contacto con todos los sitios de actualizaciones durante instalar software de toofind necesario** está desactivada.)
7. Hola **Install Details** cuadro de diálogo, haga clic en **siguiente**.
   
    ![Revisión de los detalles de la instalación][03]
8. Hola **Review Licenses** cuadro de diálogo, revise los términos de Hola Hola de contratos de licencia. Si acepta los términos de Hola Hola de contratos de licencia, haga clic en **acepto los términos de Hola Hola de contratos de licencia** y, a continuación, haga clic en **finalizar**. (Hola restantes da por sentado que acepte los términos de Hola Hola de contratos de licencia. Si no acepta los términos de Hola Hola de contratos de licencia, salga del proceso de instalación de Hola.)
   
    ![Revisar licencias][04]
   
    Eclipse descargará e instalará los paquetes de requisitos de Hola.
   
    ![Progreso de la instalación][05]
9. Si se le solicita la instalación de toocomplete de toorestart Eclipse, haga clic en **Sí**.
   
    ![Reinicio del símbolo del sistema][06]

## <a name="see-also"></a>Otras referencias
Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola siguientes vínculos:

* [Kit de herramientas de Azure para Eclipse]
  * [What's New en hello Azure Toolkit for Eclipse]
  * *Instalar hello Azure Toolkit for Eclipse (de este artículo)*
  * [Inicio de sesión en las instrucciones de hello Azure Toolkit for Eclipse]
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [What's New en hello Azure Toolkit for IntelliJ]
  * [Instalación hello Azure Toolkit for IntelliJ]
  * [Inicio de sesión en las instrucciones de hello Azure Toolkit for IntelliJ]
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure].

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Inicio de sesión en las instrucciones de hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Inicio de sesión en las instrucciones de hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's New en hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New en hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
