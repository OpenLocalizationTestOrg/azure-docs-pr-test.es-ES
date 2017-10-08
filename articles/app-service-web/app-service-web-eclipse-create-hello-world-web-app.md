---
title: "Eclipse aaaCreate una aplicación web de Azure básico con | Documentos de Microsoft"
description: "Este tutorial muestra cómo toouse Hola Kit de herramientas de Azure para Eclipse toocreate una aplicación de Hello World Web de Azure."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a>Creación de una aplicación web básica de Azure con Eclipse
Este tutorial se muestra cómo toocreate e implementar un tooAzure de aplicación Hello World básico como una aplicación Web mediante hello [Azure Toolkit for Eclipse]. Para que sea más sencillo, se muestra un ejemplo básico de JSP, pero los pasos similares se aplicarían en el caso de un servlet Java en lo que respecta a la implementación de Azure.

Cuando se haya completado este tutorial, la aplicación tendrá un aspecto similar toohello siguientes ilustración al verlo en un explorador web:

![Versión preliminar de la aplicación Hello World][01]

## <a name="prerequisites"></a>Requisitos previos
* Un kit para desarrolladores de Java (JDK) de la versión 1.8 o superior.
* Eclipse IDE para Java EE Developers, Luna o superior. Se puede descargar en <http://www.eclipse.org/downloads/>.
* Una distribución de un servidor web basado en Java o un servidor de aplicaciones, como [Apache Tomcat] o [Jetty].
* Una suscripción a Azure, que se puede adquirir en <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.
* Hola [Azure Toolkit for Eclipse]. Para obtener información acerca de cómo instalar hello Azure Toolkit, vea [instalar hello Azure Toolkit for Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate una aplicación Hello World
En primer lugar, empezaremos con la creación de un proyecto Java.

1. Inicie Eclipse y, en el menú de hello en **archivo**, haga clic en **New**y, a continuación, haga clic en **Dynamic Web Project**. (Si no ve **Dynamic Web Project** aparece como proyecto disponible después de hacer clic **archivo** y **New**, a continuación, Hola después: haga clic en **archivo**, haga clic en **New**, haga clic en **proyecto...** , expanda **Web**, haga clic en **Dynamic Web Project**y haga clic en **siguiente**.)
2. Para fines de este tutorial, denomine el proyecto de hello **MyWebApp**. La pantalla aparecerá a continuación toohello similar:
   
    ![Creación de un nuevo proyecto web dinámico][02]
3. Haga clic en **Finalizar**
4. En la vista del explorador de proyectos de Eclipse, expanda **MyWebApp**. Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).
5. Hola **New JSP File** cuadro de diálogo, archivo de nombre hello **index.jsp**, mantenga la carpeta principal de hello como **MyWebApp/WebContent**y, a continuación, haga clic en **siguiente**.
6. Hola **Select JSP Template** cuadro de diálogo, para los fines de este tutorial, seleccione **New JSP File (html)**y, a continuación, haga clic en **finalizar**.
7. Cuando se abre el archivo index.jsp en Eclipse, agregar en la presentación del texto toodynamically **Hello World!** dentro de hello existente `<body>` elemento. Su actualizada `<body>` contenido debe parecerse al siguiente ejemplo de Hola:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. Guarde el archivo index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy su tooan aplicación contenedor de aplicación Web de Azure
Hay varias maneras, por lo que puede implementar un tooAzure de aplicación web de Java. Este tutorial describe uno de hello más sencilla: la aplicación será implementado tooan contenedor de aplicación Web de Azure: no se necesitan ningún tipo de proyecto especiales ni herramientas adicionales. software de contenedor de web JDK y Hola Hola se proporcionarán automáticamente con Azure, así que no hay ninguna necesidad de tooupload su propio; todo lo que necesita es la aplicación Web de Java. Como resultado, el proceso de publicación de hello para la aplicación tardará a segundos, minutos no.

1. En el Explorador de proyectos de Eclipse, haga clic con el botón derecho en **MyWebApp**.
2. En el menú contextual de hello, seleccione **Azure**, a continuación, haga clic en **publicar como aplicación Web de Azure...**
   
    ![Publish as Azure Web App][03]
   
    O bien, mientras está seleccionado el proyecto de aplicación web en el Explorador de proyectos de Hola, puede hacer clic en hello **publicar** botón de lista desplegable en la barra de herramientas de Hola y seleccione **publicar como aplicación Web de Azure** a partir de ahí:
   
    ![Publish as Azure Web App][14]
3. Si todavía no está suscrito a Azure desde Eclipse, es posible que toosign solicitada en su cuenta de Azure:
   
    ![Cuadro de diálogo de inicio de sesión en Azure][04]
   
    Si tiene varias cuentas de Azure, algunos de los mensajes de Hola durante Hola iniciar sesión en proceso se puede mostrar más de una vez, incluso si aparecen toobe Hola igual. Cuando esto sucede, continuar después de inicio de sesión de hello en instrucciones.
4. Después de iniciar sesión en su cuenta de Azure, Hola **administrar suscripciones** cuadro de diálogo mostrará una lista de suscripciones que están asociados con sus credenciales. Si hay varias suscripciones aparece y desea toowork con sólo un subconjunto específico de ellos, si lo desea puede desactivar Hola que desea toouse. Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.
   
    ![Cuadro de diálogo Administrar suscripciones][05]
5. Cuando Hola **implementar tooAzure contenedor de la aplicación Web** aparece el cuadro de diálogo, se mostrará a los contenedores de la aplicación Web que creó anteriormente; si no ha creado los contenedores, lista de hello estará vacío.
   
    ![Cuadro de diálogo de contenedor de la aplicación Web de tooAzure implementar][06]
6. Si no ha creado un contenedor de aplicación Web de Azure antes o si desea que toopublish su tooa nuevo contenedor de aplicación, use Hola pasos. En caso contrario, seleccione un contenedor de la aplicación Web existente y omitir toostep 7 siguiente.
   
   1. Haga clic en **Nuevo...**
      
       ![Cuadro de diálogo de contenedor de la aplicación Web de tooAzure implementar][15]
   2. Hola **nuevo contenedor de la aplicación Web** se mostrará el cuadro de diálogo:
      
       ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][07a]
   3. Escriba un **etiqueta DNS** para el contenedor de la aplicación Web; esto formará etiqueta DNS de hoja de Hola de dirección URL del host de hello para la aplicación web en Azure. (Tenga en cuenta ese nombre hello debe estar disponibles y cumplir los requisitos de nombres de aplicación Web de tooAzure).
   4. Hola **contenedor Web** menú desplegable, el software adecuado de Hola seleccione para la aplicación.
      
       Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9. Una distribución recientes de software de hello seleccionado se proporcionarán con Azure y se ejecutará en una distribución reciente de JDK 8 creada por Oracle y proporcionado por Azure.
   5. Hola **suscripción** menú desplegable, suscripción Hola seleccione desea toouse para esta implementación.
   6. Hola **grupo de recursos** menú desplegable, seleccione Hola grupo de recursos con el que desea tooassociate la aplicación Web. (Grupos de recursos de azure permiten toogroup recursos relacionados juntos para que, por ejemplo, pueden eliminarse juntos).
      
       Puede seleccionar un grupo de recursos existente (si tiene alguno) y omitir toostep g a continuación u Hola uso siguiendo estos pasos toocreate un nuevo grupo de recursos:
      
      * Haga clic en **Nuevo...**
      * Hola **nuevo grupo de recursos** se mostrará el cuadro de diálogo:
        
          ![Cuadro de diálogo Nuevo grupo de recursos][08]
      * Hola Hola **nombre** cuadro de texto, especifique un nombre para el nuevo grupo de recursos.
      * Hola Hola **región** menú desplegable, ubicación para el grupo de recursos del centro de datos de Azure adecuada Hola select.
      * OPCIONAL: De forma predeterminada, una distribución reciente de Java 8 se implementarán Azure automáticamente tooyour contenedor de la aplicación web como la JVM. Sin embargo, puede especificar una versión diferente y la distribución de hello JVM si así lo requiere la aplicación Web. Hola toospecify JDK para la aplicación Web, haga clic en hello **JDK** pestaña y seleccione una de las siguientes opciones de hello:
        
        * **Implementar de forma predeterminada Hola JDK que ofrece el servicio de aplicaciones Web de Azure**: esta opción implementará una distribución reciente de Java 8.
        * **Implementar una parte 3ª JDK disponible en Azure**: esta opción le permite toochoose de lista de Hola de JDK que se proporcionan con Microsoft Azure.
        * **Implementar mi propio JDK desde esta ubicación de descarga**: esta opción le permite toospecify su propia distribución JDK, que se debe empaquetar como un archivo ZIP y cargado tooeither una ubicación de descarga disponible públicamente o un almacenamiento de Azure de la cuenta para el que se tener acceso.
          
          ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][07b]
   7. Haga clic en **Aceptar**.
   8. Hola **Plan de servicio de aplicaciones** menú desplegable muestra planes de servicio de aplicación Hola que están asociados con hello grupo de recursos que ha seleccionado. (Los planes de servicio de aplicaciones especifican información como ubicación de saludo de la aplicación Web, Hola plan de tarifa y tamaño de instancia de proceso de Hola. Un único plan de App Service se puede usar para varias aplicaciones web, motivo por el cual se mantiene independiente de una implementación específica de aplicaciones web.
      
       Puede seleccionar un Plan de servicio de aplicación existente (si tiene alguno) y omitir toostep h siguiente o usar hello siguiendo estos toocreate pasos un nuevo Plan de servicio de aplicación:
      
      * Haga clic en **Nuevo...**
      * Hola **nuevo Plan de servicio de aplicación** se mostrará el cuadro de diálogo:
        
          ![Cuadro de diálogo de nuevo plan de App Service][09]
      * Hola Hola **nombre** cuadro de texto, especifique un nombre para el nuevo Plan de servicio de aplicación.
      * Hola Hola **ubicación** menú desplegable, ubicación para el plan de hello del centro de datos de Azure adecuada Hola select.
      * Hola Hola **tarifa** menú desplegable, seleccione Hola adecuado de precios para el plan de Hola. Con fines de prueba, puede elegir **Gratis**.
      * Hola Hola **tamaño de la instancia** menú desplegable, el tamaño de la instancia adecuada de hello seleccione plan Hola. Con fines de prueba, puede elegir **Pequeño**.
   9. Una vez que haya completado todas de hello por encima de los pasos, cuadro de diálogo nuevo contenedor de la aplicación Web de hello debe ser similar a Hola siguiente ilustración:
      
       ![Cuadro de diálogo de implementación en nuevo contenedor de aplicación web][10]
   10. Haga clic en **Aceptar** creación de hello toocomplete de su nuevo contenedor de aplicación Web.
       
        Actualiza espera unos segundos para obtener lista de Hola de toobe de contenedores de aplicación Web de Hola y el contenedor de la aplicación web recién creado debería estar ahora seleccionado en la lista de Hola.
7. Ya estás implementación inicial de hello toocomplete listo de su tooAzure de aplicación Web:
   
    ![Cuadro de diálogo de contenedor de la aplicación Web de tooAzure implementar][11]
   
    Haga clic en **Aceptar** toodeploy su toohello de aplicación Java seleccionado contenedor de la aplicación Web.
   
    De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones de Hola. Si desea toobe implementado como aplicación de la raíz de hello, compruebe hello **implementar tooroot** casilla antes de hacer clic **Aceptar**.
8. A continuación, debería ver Hola **Azure Activity Log** vista, que indicará el estado de implementación de saludo de la aplicación Web.
   
    ![Azure Activity Log][12]
   
    proceso de Hello de la implementación de la aplicación Web tooAzure tardará unos pocos segundos toocomplete. Cuando esté listo aplicación, verá un vínculo denominado **publicada** en hello **estado** columna. Al hacer clic en el vínculo de hello, le llevará página principal de la aplicación Web tooyour implementado.

## <a name="updating-your-web-app"></a>Actualización de la aplicación web
Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:

* Puede actualizar la implementación de Hola de una aplicación Web de Java existente.
* Puede publicar un toohello adicional de aplicación de Java mismo contenedor de la aplicación Web.

En cualquier caso, el proceso de hello es idéntico y tarda solo unos segundos:

1. En el Explorador de proyectos de Eclipse hello, haga clic en aplicación de Java de hello desee tooupdate o agregar tooan existente contenedor de la aplicación Web.
2. Cuando aparezca el menú contextual de hello, seleccione **Azure** y, a continuación, **publicar como aplicación Web de Azure...**
3. Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes. Seleccione Hola uno desea toopublish o volver a publicar el Java aplicación tooand, haga clic **Aceptar**.

Hola unos segundos más tarde, **Azure Activity Log** vista mostrará la implementación actualizada como **publicada** y será capaz de tooverify la aplicación actualizada en un explorador web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Inicio, detención o reinicio de una aplicación web existente
toostart o detener un contenedor de aplicación Web de Azure existente, (incluido todas las aplicaciones de Java de hello implementado en él), puede usar hello **Azure explorador** vista.

Si hello **explorador Azure** vista ya no está abierta, puede abrirlo haciendo clic, a continuación, en **ventana** , a continuación, haga clic en el menú de Eclipse, **Mostrar vista**, a continuación, **otros...** , a continuación, **Azure**y, a continuación, haga clic en **explorador Azure**. Si anteriormente no han iniciado sesión, se le pedirá que toodo así.

Cuando Hola **explorador Azure** se muestra la vista, use, siga estos pasos toostart o detener la aplicación Web: 

1. Expanda hello **Azure** nodo.
2. Expanda hello **aplicaciones Web** nodo. 
3. Menú contextual Hola había deseado aplicación Web.
4. Cuando aparezca el menú contextual de hello, haga clic en **iniciar**, **detener**, o **reiniciar**. Tenga en cuenta que las opciones de menú de hello en contexto, por lo que solo puede detener una aplicación web en ejecución o iniciar una aplicación web que no se está ejecutando actualmente.
   
    ![Detención de una aplicación web existente][13]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola siguientes vínculos:

* [Azure Toolkit for Eclipse]
  * [instalar hello Azure Toolkit for Eclipse]
  * *Creación de una aplicación web Hello World para Azure en Eclipse (este artículo)*
  * [What's New en hello Azure Toolkit for Eclipse]
* [Kit de herramientas de Azure para IntelliJ]
  * [Instalación hello Azure Toolkit for IntelliJ]
  * [Creación de una aplicación web Hello World para Azure en IntelliJ]
  * [What's New en hello Azure Toolkit for IntelliJ]

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure].

Para obtener información adicional acerca de cómo crear aplicaciones Web de Azure, vea hello [información general de aplicaciones Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Kit de herramientas de Azure para IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Creación de una aplicación web Hello World para Azure en IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[instalar hello Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Instalación hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[What's New en hello Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[What's New en hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[información general de aplicaciones Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
