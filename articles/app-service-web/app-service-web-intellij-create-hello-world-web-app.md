---
title: "una aplicación web de Azure básico en IntelliJ aaaCreate | Documentos de Microsoft"
description: "Este tutorial muestra cómo toouse hello Azure Toolkit para IntelliJ toocreate una aplicación de Hello World Web de Azure."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Creación de una aplicación web básica de Azure en IntelliJ
Este tutorial se muestra cómo toocreate e implementar un tooAzure de aplicación Hello World básico como una aplicación Web mediante hello [Azure Toolkit for IntelliJ]. Para que sea más sencillo, se muestra un ejemplo básico de JSP, pero los pasos similares se aplicarían en el caso de un servlet Java en lo que respecta a la implementación de Azure.

Cuando se haya completado este tutorial, la aplicación tendrá un aspecto similar toohello siguientes ilustración al verlo en un explorador web:

![Página web de ejemplo][01]

## <a name="prerequisites"></a>Requisitos previos
* Un kit para desarrolladores de Java (JDK) de la versión 1.8 o superior.
* IntelliJ IDEA Ultimate Edition. Se puede descargar desde <https://www.jetbrains.com/idea/download/index.html>.
* Una distribución de un servidor web basado en Java o un servidor de aplicaciones, como [Apache Tomcat] o [Jetty].
* Una suscripción a Azure, que se puede adquirir en <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.
* Hola [Azure Toolkit for IntelliJ]. Para obtener información acerca de cómo instalar hello Azure Toolkit, vea [instalar hello Azure Toolkit for IntelliJ].

## <a name="toocreate-a-hello-world-application"></a>toocreate una aplicación Hello World
En primer lugar, empezaremos con la creación de un proyecto Java.

1. Iniciar IntelliJ y haga clic en hello **archivo** menú, a continuación, haga clic en **New**y, a continuación, haga clic en **proyecto**.
   
    ![Archivo Nuevo Proyecto][02]
2. En el cuadro de diálogo nuevo proyecto de hello, seleccione **Java**, a continuación, **aplicación Web**y, a continuación, haga clic en **New** tooadd un SDK de Project.
   
    ![Cuadro de diálogo Nuevo proyecto][03a]
   
3. Hola seleccionar el directorio particular de cuadro de diálogo JDK, seleccione Hola carpeta donde está instalado el JDK y, a continuación, haga clic en **Aceptar**. Haga clic en **siguiente** en toocontinue del cuadro de diálogo de hello nuevo proyecto.
   
    ![Especificación del directorio de inicio de JDK][03b]
4. Para fines de este tutorial, denomine el proyecto de hello **Java aplicación Web en Azure**y, a continuación, haga clic en **finalizar**.
   
    ![Cuadro de diálogo Nuevo proyecto][04]
5. En la vista del explorador de proyectos de IntelliJ, expanda **Java-Web-App-On-Azure**, después expanda **web** y, luego, haga doble clic en **index.jsp**.
   
    ![Abrir página de índice][05c]
6. Cuando se abre el archivo index.jsp en IntelliJ, agregar en la presentación del texto toodynamically **Hello World!** dentro de hello existente `<body>` elemento. Su actualizada `<body>` contenido debe parecerse al siguiente ejemplo de Hola:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Guarde el archivo index.jsp.

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a>toodeploy su tooan aplicación contenedor de aplicación Web de Azure
Hay varias maneras, por lo que puede implementar un tooAzure de aplicación web de Java. Este tutorial describe uno de hello más sencilla: la aplicación será implementado tooan contenedor de aplicación Web de Azure: no se necesitan ningún tipo de proyecto especiales ni herramientas adicionales. software de contenedor de web JDK y Hola Hola se proporcionarán automáticamente con Azure, así que no hay ninguna necesidad de tooupload su propio; todo lo que necesita es la aplicación Web de Java. Como resultado, el proceso de publicación de hello para la aplicación tardará a segundos, minutos no.

Antes de publicar la aplicación, primero debe tooconfigure su configuración para el módulo. toodo por lo tanto, use Hola pasos:

1. En el Explorador de proyectos del IntelliJ, haga clic en hello **Java aplicación Web en Azure** proyecto. Cuando aparezca el menú contextual de hello, haga clic en **configuración para abrir el módulo**.

    ![Abrir configuración del módulo][05a]
2. Cuando aparezca el cuadro de diálogo de estructura del proyecto de hello:

   a. Haga clic en **artefactos** en la lista de Hola de **configuración del proyecto**.
   b. Cambiar el nombre del artefacto de Hola Hola **nombre** cuadro para que no contenga espacios en blanco o caracteres especiales; esto es necesario ya que se utilizará el nombre de Hola Hola identificador uniforme de recursos (URI).
   c. Hola de cambio **tipo** demasiado**aplicación Web: archivo**.
   d. Haga clic en **Aceptar** cuadro de diálogo de tooclose Hola estructura del proyecto.

    ![Abrir configuración del módulo][05b]

Cuando se ha configurado el módulo, puede publicar su aplicación tooAzure mediante Hola pasos:

1. En el Explorador de proyectos del IntelliJ, haga clic en hello **Java aplicación Web en Azure** proyecto. Cuando aparezca el menú contextual de hello, seleccione **Azure**y, a continuación, haga clic en **publicar como aplicación Web de Azure...**
   
    ![Menú contextual de publicación de Azure][06]
2. Si todavía no está suscrito a Azure desde IntelliJ, es posible que toosign solicitada en su cuenta de Azure. (Si tiene varias cuentas de Azure, algunos de los mensajes de Hola durante el inicio de sesión de hello en proceso pueden ser se muestra más de una vez, incluso si aparecen toobe Hola igual. Cuando esto sucede, continúe con el inicio de sesión de toofollow hello en instrucciones).
   
    ![Cuadro de diálogo de inicio de sesión de Azure][07]
3. Después de iniciar sesión en su cuenta de Azure, Hola **administrar suscripciones** cuadro de diálogo mostrará una lista de suscripciones que están asociados con sus credenciales. (Si hay varias suscripciones aparece y desea toowork con sólo un subconjunto específico de ellos, si lo desea puede desactivar suscripciones de Hola que no desea toouse). Cuando haya seleccionado las suscripciones, haga clic en **Cerrar**.
   
    ![Administrar suscripciones][08]
4. Cuando Hola **implementar tooAzure contenedor de la aplicación Web** aparece el cuadro de diálogo, se mostrará a los contenedores de la aplicación Web que creó anteriormente; si no ha creado los contenedores, lista de hello estará vacío.
   
    ![Contenedores de aplicaciones][09]
5. Si no ha creado un contenedor de aplicación Web de Azure antes o si desea que toopublish su tooa nuevo contenedor de aplicación, use Hola pasos. En caso contrario, seleccione un contenedor de la aplicación Web existente y omitir toostep 6 a continuación.
   
   1. Haga clic en **+**
      
       ![Agregar contenedor de aplicaciones][10]
   2. Hola **nuevo contenedor de la aplicación Web** se mostrará el cuadro de diálogo, que será utilizado para hello junto varios pasos.
      
       ![Nuevo contenedor de aplicaciones][11a]
   3. Escriba un **etiqueta DNS** para el contenedor de la aplicación Web; esto formará etiqueta DNS de hoja de Hola de dirección URL del host de hello para la aplicación web en Azure. Tenga en cuenta ese nombre hello debe estar disponibles y cumplir los requisitos de nombres de aplicación Web de tooAzure.
   4. Hola **contenedor Web** menú desplegable, el software adecuado de Hola seleccione para la aplicación.
      
       Actualmente, puede elegir entre Tomcat 8, Tomcat 7 o Jetty 9. Una distribución recientes de software de hello seleccionado se proporcionarán con Azure y se ejecutará en una distribución reciente de JDK 8 creada por Oracle y proporcionado por Azure.
   5. Hola **suscripción** menú desplegable, suscripción Hola seleccione desea toouse para esta implementación.
   6. Hola **grupo de recursos** menú desplegable, seleccione Hola grupo de recursos con el que desea tooassociate la aplicación Web. (Grupos de recursos de azure permiten toogroup recursos relacionados juntos para que, por ejemplo, pueden eliminarse juntos).
      
       Puede seleccionar un grupo de recursos existente (si tiene alguno) y omitir toostep g a continuación, o si uso Hola sigue los pasos toocreate un nuevo grupo de recursos:
      
      * Seleccione  **&lt; &lt; crear nuevo grupo de recursos &gt; &gt;**  en hello **grupo de recursos** menú desplegable.
      * Hola **nuevo grupo de recursos** se mostrará el cuadro de diálogo:
        
          ![Nuevo grupo de recursos][12]
      * Hola Hola **nombre** cuadro de texto, especifique un nombre para el nuevo grupo de recursos.
      * Hola Hola **región** menú desplegable, ubicación para el grupo de recursos del centro de datos de Azure adecuada Hola select.
      * Haga clic en **Aceptar**.
   7. Hola **Plan de servicio de aplicaciones** menú desplegable muestra planes de servicio de aplicación Hola que están asociados con hello grupo de recursos que ha seleccionado. (Un Plan de servicio de aplicaciones especifica información como ubicación de saludo de la aplicación Web, Hola plan de tarifa y tamaño de instancia de proceso de Hola. Un único plan de App Service se puede usar para varias aplicaciones web, motivo por el cual se mantiene independiente de una implementación específica de aplicaciones web.
      
       Puede seleccionar un Plan de servicio de aplicación existente (si tiene alguno) y omitir toostep h siguiente o usar hello después toocreate pasos un nuevo Plan de servicio de aplicación:
      
      * Seleccione  **&lt; &lt; crear nuevo Plan de servicio de aplicación &gt; &gt;**  en hello **Plan de servicio de aplicaciones** menú desplegable.
      * Hola **nuevo Plan de servicio de aplicación** se mostrará el cuadro de diálogo:
        
          ![Nuevo plan de App Service][13]
      * Hola Hola **nombre** cuadro de texto, especifique un nombre para el nuevo Plan de servicio de aplicación.
      * Hola Hola **ubicación** menú desplegable, ubicación para el plan de hello del centro de datos de Azure adecuada Hola select.
      * Hola Hola **tarifa** menú desplegable, seleccione Hola adecuado de precios para el plan de Hola. Con fines de prueba, puede elegir **Gratis**.
      * Hola Hola **tamaño de la instancia** menú desplegable, el tamaño de la instancia adecuada de hello seleccione plan Hola. Con fines de prueba, puede elegir **Pequeño**.
      * Haga clic en **Aceptar**.
   8. (Opcional) De forma predeterminada, una distribución reciente de Java 8 se implementarán automáticamente como la JVM por contenedor de aplicaciones web de Azure tooyour. Sin embargo, puede seleccionar una versión diferente y la distribución de hello JVM. toodo por lo tanto, use Hola pasos:
      
      * Haga clic en hello **JDK** ficha hello **nuevo contenedor de la aplicación Web** cuadro de diálogo.
      * Puede elegir una de las siguientes opciones de hello:
        
        * Implementación predeterminada de hello JDK que se ofrece a través de Azure
        * Implementar un JDK de terceros de lista desplegable de JDK adicionales que están disponibles en Azure
        * Implementar un JDK personalizado, que debe estar empaquetado en un archivo ZIP y bien estar disponible públicamente o en su cuenta de Azure Storage
        
        ![Pestaña JDK de nuevo contenedor de aplicaciones][11b]
   9. Una vez que haya completado todas de hello por encima de los pasos, cuadro de diálogo nuevo contenedor de la aplicación Web de hello debe ser similar a Hola siguiente ilustración:
      
       ![Nuevo contenedor de aplicaciones][14]
   10. Haga clic en **Aceptar** creación de hello toocomplete de su nuevo contenedor de aplicación Web.
       
        Actualiza espera unos segundos para obtener lista de Hola de toobe de contenedores de aplicación Web de Hola y el contenedor de la aplicación web recién creado debería estar ahora seleccionado en la lista de Hola.
6. Ya estás implementación inicial de hello listo toocomplete de tooAzure de su aplicación Web; Haga clic en **Aceptar** toodeploy su toohello de aplicación Java seleccionado contenedor de la aplicación Web. De forma predeterminada, la aplicación se implementará como un subdirectorio del servidor de aplicaciones de Hola. Si desea toobe implementado como aplicación de la raíz de hello, compruebe hello **implementar tooroot** casilla antes de hacer clic **Aceptar**.
   
    ![Implementar tooAzure][15]
7. A continuación, debería ver Hola **Azure Activity Log** vista, que indicará el estado de implementación de saludo de la aplicación Web.
   
    ![Indicador de progreso][16]
   
    proceso de Hello de la implementación de la aplicación Web tooAzure tardará unos pocos segundos toocomplete. Cuando esté listo aplicación, verá un vínculo denominado **publicada** en hello **estado** columna. Al hacer clic en el vínculo de hello, le permitirán página principal de la aplicación Web tooyour implementado, o puede usar pasos Hola Hola después de la aplicación web de sección toobrowse tooyour.

## <a name="browsing-tooyour-web-app-on-azure"></a>Exploración tooyour aplicación Web en Azure
toobrowse tooyour aplicación Web en Azure, puede usar hello **Azure explorador** vista.

Si hello **explorador Azure** vista ya no está abierta, puede abrirlo haciendo clic, a continuación, en **vista** IntelliJ, a continuación, haga clic en **las ventanas de herramientas**y, a continuación, haga clic en  **Servicio explorador**. Si anteriormente no han iniciado sesión, se le pedirá que toodo así.

Cuando Hola **explorador Azure** se muestra la vista, use siga estas tooyour de toobrowse pasos aplicación Web: 

1. Expanda hello **Azure** nodo.
2. Expanda hello **aplicaciones Web** nodo. 
3. Menú contextual Hola había deseado aplicación Web.
4. Cuando aparezca el menú contextual de hello, haga clic en **abrir en el explorador**.
   
    ![Examinar una aplicación web][17]

## <a name="updating-your-web-app"></a>Actualización de la aplicación web
Actualizar una aplicación web de Azure existente es un proceso rápido y sencillo, y tiene dos opciones para ello:

* Puede actualizar la implementación de Hola de una aplicación Web de Java existente.
* Puede publicar un toohello adicional de aplicación de Java mismo contenedor de la aplicación Web.

En cualquier caso, el proceso de hello es idéntico y tarda solo unos segundos:

1. En el Explorador de proyectos de hello IntelliJ, haga clic en aplicación de Java de hello desee tooupdate o agregar tooan existente contenedor de la aplicación Web.
2. Cuando aparezca el menú contextual de hello, seleccione **Azure** y, a continuación, **publicar como aplicación Web de Azure...**
3. Puesto que ya ha iniciado sesión anteriormente, verá una lista de contenedores de aplicaciones web existentes. Seleccione Hola uno desea toopublish o volver a publicar el Java aplicación tooand, haga clic **Aceptar**.

Hola unos segundos más tarde, **Azure Activity Log** vista mostrará la implementación actualizada como **publicada** y será capaz de tooverify la aplicación actualizada en un explorador web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Inicio, detención o reinicio de una aplicación web existente
toostart o detener un contenedor de aplicación Web de Azure existente, (incluido todas las aplicaciones de Java de hello implementado en él), puede usar hello **Azure explorador** vista.

Si hello **explorador Azure** vista ya no está abierta, puede abrirlo haciendo clic, a continuación, en **vista** IntelliJ, a continuación, haga clic en **las ventanas de herramientas**y, a continuación, haga clic en  **Servicio explorador**. Si anteriormente no han iniciado sesión, se le pedirá que toodo así.

Cuando Hola **explorador Azure** se muestra la vista, use, siga estos pasos toostart o detener la aplicación Web: 

1. Expanda hello **Azure** nodo.
2. Expanda hello **aplicaciones Web** nodo. 
3. Menú contextual Hola había deseado aplicación Web.
4. Cuando aparezca el menú contextual de hello, haga clic en **iniciar**, **detener**, o **reiniciar**. Tenga en cuenta que las opciones de menú de hello en contexto, por lo que solo puede detener una aplicación web en ejecución o iniciar una aplicación web que no se está ejecutando actualmente.
   
    ![Detener aplicación web][18]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de hello kits de herramientas de Azure para Java IDE, vea Hola siguientes vínculos:

* [Kit de herramientas de Azure para Eclipse]
  * [Instalar hello Azure Toolkit for Eclipse]
  * [Creación de una aplicación web Hello World para Azure en Eclipse]
  * [What's New en hello Azure Toolkit for Eclipse]
* [Azure Toolkit for IntelliJ]
  * [instalar hello Azure Toolkit for IntelliJ]
  * *Creación de una aplicación web Hello World para Azure en IntelliJ (este artículo)*
  * [What's New en hello Azure Toolkit for IntelliJ]

<a name="see-also"></a>

## <a name="see-also"></a>Otras referencias
Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure].

Para obtener información adicional acerca de cómo crear aplicaciones Web de Azure, vea hello [información general de aplicaciones Web].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Kit de herramientas de Azure para Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Creación de una aplicación web Hello World para Azure en Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Instalar hello Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[instalar hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[What's New en hello Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[What's New en hello Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[información general de aplicaciones Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
