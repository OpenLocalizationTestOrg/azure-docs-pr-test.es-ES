---
title: "aaaPublish como un contenedor de Docker mediante el uso de una aplicación de arranque de primavera hello Azure Toolkit para IntelliJ | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopublish una tooMicrosoft de aplicación web Azure como un contenedor de Docker mediante el uso de Hola Kit de herramientas de Azure para IntelliJ."
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
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publicar una aplicación Spring arranque como un contenedor de Docker mediante hello Azure Toolkit para IntelliJ

Hola [Spring Framework] es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos de más populares de Hola que se compila sobre dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones de Java de independiente.

[Docker] es una solución de código abierto que ayuda a los desarrolladores automatizar la implementación de hello, ajuste de escala y administración de las aplicaciones que se ejecutan en contenedores.

Este tutorial le guiará por hello pasos toodeploy una aplicación Spring arranque como un tooMicrosoft de contenedor de Docker Azure mediante el uso de hello Azure Toolkit para IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a>Clonar Hola predeterminado Spring arranque Docker repositorio

Hello pasos siguientes le guían a través de clonación de repositorio de Docker de arranque de primavera de hello utilizando IntelliJ. Si desea toouse una línea de comandos, consulte [implementar una aplicación de arranque del muelle en Linux en el servicio de contenedor de Azure][Deploy Spring Boot on Linux in ACS].

1. Abra IntelliJ.

1. En la pantalla de bienvenida de bienvenida, seleccione hello **GitHub** opción Hola **desproteger del Control de versiones** lista.

   ![Opción de GitHub para el control de versiones][CL01]

1. Escriba sus credenciales si es toolog solicitada en.

   * Si está usando un nombre de usuario/contraseña toolog en tooGitHub:

      ![Cuadro de diálogo para escribir el nombre de usuario y la contraseña de GitHub][CL02a]

   * Si está utilizando un token toolog en tooGitHub:

      ![Cuadro de diálogo para especificar un token de GitHub][CL02b]

1. Escriba **https://github.com/spring-guides/gs-spring-boot-docker.git** para la dirección URL del repositorio de hello, especifique la ruta de acceso local y la información de la carpeta y, a continuación, haga clic en **clon**.

   ![Cuadro de diálogo Clonar repositorio][CL03]

1. Cuando se le pide un proyecto IntelliJ, seleccione toocreate **No**.

   ![Rechazar toocreate un proyecto IntelliJ][CL04]

1. En la página de bienvenida de hello, haga clic en **Importar proyecto**.

   ![Selección de Importar proyecto][CL05]

1. Buscar ruta de acceso de Hola donde clonó repositorio de arranque de primavera de hello, seleccione hello **completa** carpeta bajo la raíz de hello y, a continuación, haga clic en **Aceptar**.

   ![Seleccionar una carpeta para la importación][CL06]

1. Cuando se le pida, seleccione **Create project from existing sources** (Crear proyecto a partir de orígenes existentes).

   ![Opción toocreate un proyecto a partir de orígenes existentes][CL07]

1. Especifique el nombre del proyecto o acepte el predeterminado de hello, compruebe toohello de ruta de acceso correcta de hello **completa** carpeta y, a continuación, haga clic en **siguiente**.

   ![Especifique el nombre del proyecto de Hola][CL08]

1. Personalice los directorios para importar y haga clic en **Next** (Siguiente).

   ![Elegir directorios][CL09]

1. Revise Hola bibliotecas tooimport y, a continuación, haga clic en **siguiente**.

   ![Revisar bibliotecas de proyecto][CL10]

1. Revise la estructura del módulo de hello y, a continuación, haga clic en **siguiente**.

   ![Revisar la estructura del módulo][CL11]

1. Especifique el JDK y, después, haga clic en **Next** (Siguiente).

   ![Especificar un JDK][CL12]

1. Haga clic en **Finalizar**

   ![Botón Finalizar][CL13]

IntelliJ importa la aplicación de arranque de primavera de hello como un proyecto y muestra la estructura de hello cuando ha finalizado la importación de Hola.

![Aplicación Spring Boot en IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Crear una aplicación Spring Boot

### <a name="build-hello-app-by-using-hello-maven-pom"></a>Compilar la aplicación hello mediante hello Maven POM

1. Abrir ventana de herramientas de hello Maven si no está ya abierto. Haga clic en **Vista** > **Ventanas de herramientas** > **Proyectos de Maven**.

   ![Comandos Ventanas de herramientas y Proyectos de Maven][BU01]

1. En la ventana de herramientas de Maven hello, haga clic en **paquete** y seleccione **ejecutar la compilación de Maven**. (Si el proyecto de Maven no se muestran automáticamente, haga clic en hello **, vuelva a importar** icono en la barra de herramientas de hello Maven.)

   ![Comando Ejecutar la compilación de Maven][BU02]

1. IntelliJ debería mostrar un mensaje **COMPILACIÓN CORRECTA** cuando se cree correctamente la aplicación Spring Boot.

   ![Mensaje COMPILACIÓN CORRECTA][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Creación de un artefacto preparado para la implementación

toopublish la aplicación de arranque de primavera, deberá toocreate un artefacto preparada para la implementación. Usar hello pasos:

1. Abra el proyecto de aplicación web en IntelliJ.

1. Haga clic en **Archivo** y después en **Estructura del proyecto**.

   ![Comando Estructura del proyecto][ART01]

1. Haga clic en hello verde plus (**+**) tooadd un artefacto de símbolos, haga clic en **JAR**y, a continuación, haga clic en **vacía**.

   ![Agregar un artefacto][ART02]

1. Nombre el artefacto asegurándose de que no tooadd Hola ".jar" extensión y, a continuación, especifique la carpeta de destino de Hola para hello Maven de salida.

   ![Especificar las propiedades del artefacto][ART03]

1. Cree un manifiesto para el artefacto (opcional):

   a. Haga clic en **Create Manifest** (Crear manifiesto).

      ![Haga clic en botón crear manifiestos de Hola][ART04a]

   b. Elija ruta de acceso de hello predeterminada de artefacto de hello y, a continuación, haga clic en **Aceptar**.

      ![Especificar la ruta de acceso del artefacto][ART04b]

   c. Haga clic en el botón de puntos suspensivos hello (**...** ) clase principal de toolocate Hola.

      ![Buscar la clase principal][ART04c]

   d. Elija la clase principal y haga clic en **OK** (Aceptar).

      ![Especificar la clase principal][ART04d]

1. Haga clic en **Aceptar**.

   ![Cierre el cuadro de diálogo de estructura del proyecto de Hola][ART05]

> [!NOTE]
> Para obtener más información sobre cómo crear artefactos en IntelliJ, consulte [configurar artefactos] en el sitio Web de JetBrains Hola.
>

### <a name="build-hello-artifact-for-deployment"></a>Generar artefactos de hello para la implementación

1. Haga clic en **Build** (Compilar) y haga clic en **Artifacts** (Artefactos).

   ![Comando Compilar artefactos][BU04]

1. Cuando Hola **crear artefacto** aparece el menú contextual, haga clic en **generar**.

   ![Menú contextual Compilar artefacto][BU05]

IntelliJ debe aparecer artefacto Hola completado para la aplicación de arranque del muelle en ventana de herramientas de proyecto de Hola.

   ![Artefacto creado][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar su tooAzure de aplicación web mediante el uso de un contenedor de Docker

1. Si no se ha registrado en tooyour cuenta de Azure, siga los pasos de hello en [instrucciones de inicio de sesión para hello Azure Toolkit para IntelliJ][Azure Sign In for IntelliJ].

1. En la ventana de herramientas del explorador de proyectos de hello, haga clic en proyecto de hello y, a continuación, seleccione **Azure** > **publicar como contenedor de Docker**.

   ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PU01]

1. Cuando Hola **implementar contenedor de Docker en Azure** aparece el cuadro de diálogo, se muestran todos los hosts Docker existentes. Si elige toodeploy tooan de host existente, puede omitir toostep 4. En caso contrario, utilice Hola siguiendo los pasos toocreate un host:

   a. Haga clic en hello verde plus (**+**) símbolo.

      ![Agregar un nuevo host de Docker][PU02]

   b. Cuando Hola **crear un Host Docker** aparece el cuadro de diálogo, puede elegir los valores predeterminados de tooaccept Hola o puede especificar cualquier configuración personalizada para el nuevo host Docker. (Para obtener descripciones detalladas de hello distintas configuraciones, vea [publicar una aplicación web como un contenedor de Docker mediante hello Azure Toolkit para IntelliJ][Publish Container with Azure Toolkit].) Haga clic en **siguiente** cuando se especifica qué toouse de configuración.

      ![Especificar las opciones de host de Docker][PU03a]

   c. Puede elegir las credenciales de inicio de sesión existentes toouse desde un almacén de claves de Azure, o puede elegir tooenter nuevas credenciales de inicio de sesión de Docker. Haga clic en **Finalizar** cuando haya especificado las opciones.

      ![Especificar credenciales del host de Docker][PU03b]

1. Seleccione el host de Docker y, después, haga clic en **Siguiente**.

   ![Seleccione hello Docker host toouse][PU04]

1. En la última página de Hola de hello **implementar contenedor de Docker en Azure** cuadro de diálogo, especifique Hola siguientes opciones:

   a. Puede elegir un nombre personalizado para el contenedor de Hola que va a hospedar el contenedor de Docker toospecify, o puede aceptar predeterminado Hola.

   b. Escriba los puertos TCP hello para el host de docker mediante Hola según la sintaxis: *[puerto externo]*:*[puerto interno]*. Por ejemplo, **80:8080** especifica un puerto externo del 80 y el puerto Hola predeterminado de arranque Spring interno de 8080.
   
      Si ha personalizado el puerto interno (por ejemplo, editando el archivo de hello application.yml), necesitará toospecify número de puerto de Hola para hello toooccur de enrutamiento correcto en Azure.

   c. Después de configurar estas opciones, haga clic en **Finalizar**.

   ![Implementar un contenedor de Docker en Azure][PU05]

1. Cuando hello Azure Toolkit ha terminado de publicar, Hola muestra de registro de actividad de Azure **publicada** para el estado de saludo.

   ![Host de Docker correctamente implementado][PU06]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

toolearn sobre métodos adicionales para crear aplicaciones de arranque Spring mediante IntelliJ, consulte [crear proyectos de inicio de primavera](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) en el sitio Web de JetBrains Hola.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[configurar artefactos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuración de artefactos)
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[arranque primavera]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
