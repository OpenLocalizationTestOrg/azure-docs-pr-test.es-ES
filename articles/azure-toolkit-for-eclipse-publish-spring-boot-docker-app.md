---
title: "aaaPublish como un contenedor de Docker mediante el uso de una aplicación de arranque de primavera hello Azure Toolkit for Eclipse | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopublish una tooMicrosoft de aplicación web Azure como un contenedor de Docker mediante el uso de hello Azure Toolkit for Eclipse."
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
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publicar una aplicación de arranque de primavera como un contenedor de Docker mediante el uso de hello Kit de herramientas de Azure para Eclipse

Hola [Spring Framework] es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos de más populares de Hola que se compila sobre dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones de Java de independiente.

[Docker] es una solución de código abierto que ayuda a los desarrolladores automatizar la implementación de hello, ajuste de escala y administración de las aplicaciones que se ejecutan en contenedores.

Este tutorial le guiará por hello pasos toodeploy una aplicación Spring arranque como un tooMicrosoft de contenedor de Docker Azure mediante el uso de hello Kit de herramientas de Azure para Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Clonar el repositorio de Docker de arranque de primavera de hello predeterminado

### <a name="import-hello-public-repository"></a>Repositorio público de Hola de importación

Hello pasos siguientes le guían a través de clonación ordenador de hello Spring arranque Docker repositorio tooyour utilizando IntelliJ. Si desea toouse una línea de comandos, consulte [implementar una aplicación de arranque del muelle en Linux en el servicio de contenedor de Azure][Deploy Spring Boot on Linux in ACS].

1. Abra Eclipse.

1. Haga clic en **Archivo** > **Importar**.

   ![Menú de importación de archivo][CL01]

1. Cuando Hola **importación** abre el cuadro de diálogo:

   a. Expanda **GIT**.

   b. Seleccione **Proyectos de GIT**.
   
   c. Haga clic en **Siguiente**.

   ![Cuadro de diálogo de importación][CL02]

1. En hello **Seleccionar origen de repositorio** página:

   a. Seleccione **Clonar URI**.
   
   b. Haga clic en **Siguiente**.

   ![Página Seleccionar origen del repositorio][CL03]

1. En hello **repositorio de código fuente Git** página:

   a. Para **URI**, escriba `https://github.com/spring-guides/gs-spring-boot-docker.git`. Este paso debe rellenar de forma automática hello **Host** y **ruta del repositorio** campos con hello corregir valores.
   
   b. repositorio de arranque de primavera de Hello es pública, por lo que no debería ser necesario tooenter el nombre de usuario de Git y la contraseña.
   
   c. Haga clic en **Siguiente**.

   ![Página Repositorio de GIT de origen][CL04]

1. En hello **selección rama** página, haga clic en **siguiente**.

   ![Página Selección de rama][CL05]

1. En hello **destino Local** página:

   a. Especifique Hola carpeta local donde desea que el repositorio local.
   
   b. Haga clic en **Siguiente**.

   ![Página Destino local][CL06]

1. En hello **seleccionar un toouse del Asistente para importar proyectos** página:

   a. Seleccione **Import as a general project** (Importar como proyecto general).
   
   b. Haga clic en **Siguiente**.

   ![Página "Seleccionar una toouse del Asistente para importar proyectos"][CL07]

1. En hello **importar proyectos** página:

   a. Especifique el nombre del proyecto.
   
   b. Haga clic en **Finalizar**

   ![Página Importar proyectos][CL08]

1. Al repositorio de Hola se clona correctamente, verá todos los archivos de hello enumerados en Eclipse.

   ![Repositorio local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Crear un proyecto de Maven desde el repositorio local

repositorio de Docker de arranque de primavera de Hello contiene un proyecto de Maven completado, que va a utilizar para este tutorial. 

1. Haga clic en **Archivo** > **Importar**.

   ![Importar en el menú archivo de hello, comando][CL01]

1. Cuando Hola **importación** abre el cuadro de diálogo:

   a. Expanda **Maven**.
   
   b. Seleccione **Existing Maven Projects** (Proyectos existentes de Maven).
   
   c. Haga clic en **Siguiente**.

   ![Cuadro de diálogo de importación][MV01]

1. En hello **proyectos de Maven** página:

   a. Para **directorio raíz**, especifique hello **completa** carpeta en el repositorio local.
   
   b. Expanda hello **avanzadas** sección y escriba un nombre personalizado para **plantilla del nombre**.
   
   c. Cuadro Seleccione Hola Hola **pom.xml** archivo de proyecto de Hola.
   
   d. Haga clic en **Finalizar**

   ![Página de proyectos de Maven][MV02]

1. Cuando se abre el proyecto de Maven de hello correctamente, verá un segundo proyecto aparece en Eclipse.

   ![Proyecto local de Maven][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Crear una aplicación Spring Boot mediante Maven

1. En el Explorador de proyectos de Eclipse hello, seleccione el proyecto de Maven de Hola.

1. Haga clic en **Ejecutar** > **Ejecutar como** > **Compilación de Maven**.

   ![Toorun de comandos como la compilación de Maven][BU01]

1. Cuando la aplicación se compila correctamente, ventana de la consola de hello muestra el estado de saludo.

   ![Compilación correcta de Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar su tooAzure de aplicación web mediante el uso de un contenedor de Docker

1. En el Explorador de proyectos de Eclipse hello, seleccione el proyecto de Maven de Hola.

1. Haga clic en hello Azure **publicar** menú y, a continuación, haga clic en **publicar como contenedor de Docker**.

   ![Comando Publish as Docker Container (Publicar como contenedor de Docker)][PU01]

1. Cuando Hola **implementación de contenedor de Docker en Azure** aparece el cuadro de diálogo:

   a. Escriba un nombre de imagen de Docker personalizado.
   
   b. Para **artefacto toodeploy**, especifique toohello de ruta de acceso de hello **gs spring arranque docker 0.1.0** acaba de compilar el archivo.

   ![Especificar opciones de Docker][PU02]

   Se muestran todos los hosts de Docker existentes. 

1. Si elige toodeploy tooan de host existente, puede omitir toostep 5. En caso contrario, utilice Hola siguiendo los pasos toocreate un host:

   a. Haga clic en **Agregar**.

      ![Agregar un nuevo host de Docker][PU03]

   b. Cuando Hola **crear un Host Docker** aparece el cuadro de diálogo, puede elegir los valores predeterminados de tooaccept Hola o puede especificar cualquier configuración personalizada para el nuevo host Docker. (Para obtener descripciones detalladas de hello distintas configuraciones, vea [publicar una aplicación web como un contenedor de Docker mediante hello Azure Toolkit para IntelliJ][Publish Container with Azure Toolkit].) Haga clic en **siguiente** cuando se especifica qué toouse de configuración.

      ![Especificar las opciones de host de Docker][PU04]

   c. Puede elegir las credenciales de inicio de sesión existentes toouse desde un almacén de claves de Azure, o puede elegir tooenter nuevas credenciales de inicio de sesión de Docker. Haga clic en **Finalizar** cuando haya especificado las opciones.

      ![Especificar credenciales del host de Docker][PU05]

1. Seleccione el host de Docker y, después, haga clic en **Siguiente**.

   ![Seleccione toouse de host de Docker][PU06]

1. En la última página de Hola de hello **implementación de contenedor de Docker en Azure** cuadro de diálogo, especifique Hola siguientes opciones:

   a. Puede elegir un nombre personalizado para el contenedor de Hola que va a hospedar el contenedor de Docker toospecify, o puede aceptar predeterminado Hola.

   b. Escriba los puertos TCP hello para el host de docker mediante Hola según la sintaxis: *[puerto externo]*:*[puerto interno]*. Por ejemplo, **80:8080** especifica un puerto externo del 80 y el puerto Hola predeterminado de arranque Spring interno de 8080.
   
      Si ha personalizado el puerto interno (por ejemplo, editando el archivo de hello application.yml), necesitará toospecify número de puerto de Hola para hello toooccur de enrutamiento correcto en Azure.

   c. Después de configurar estas opciones, haga clic en **Finalizar**.

   ![Implementar un contenedor de Docker en Azure][PU07]

1. Cuando hello Azure Toolkit ha terminado de publicar, Hola muestra de registro de actividad de Azure **publicada** para el estado de saludo.

   ![Host de Docker correctamente implementado][PU08]

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[arranque primavera]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
