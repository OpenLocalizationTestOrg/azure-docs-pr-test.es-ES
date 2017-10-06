---
title: aaaAzure Service Fabric complemento para Eclipse | Documentos de Microsoft
description: Empezar a trabajar con hello Service Fabric complemento para Eclipse.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Complemento de Service Fabric para el desarrollo de aplicaciones Java de Eclipse
Eclipse es uno de hello más usada en entornos de desarrollo (IDE) de integrados para los desarrolladores de Java. En este artículo se describe cómo tooset seguridad su toowork del entorno de desarrollo Eclipse con Azure Service Fabric. Obtenga información acerca de cómo tooinstall Hola Service Fabric complemento, crear una aplicación de Service Fabric e implementar su Service Fabric aplicación tooa local o remoto Service Fabric clúster en Eclipse Neon.

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>Instalar o actualizar Hola Service Fabric complemento de Eclipse Neon
En Eclipse se puede instalar un complemento Service Fabric. Hola complemento puede ayudar a simplificar el proceso de Hola de compilar e implementar servicios de Java.

1.  Asegúrese de que tiene la versión más reciente de Hola de Eclipse Neon y versión más reciente de Hola de Buildship (1.0.17 o una versión posterior) instalado:
    -   versiones de hello toocheck de componentes instalados, en Eclipse Neon, vaya demasiado**ayuda** > **detalles de instalación**.
    -   vea tooupdate Buildship, [Buildship Eclipse: complementos Eclipse para Gradle][buildship-update].
    -   toocheck para e instalar actualizaciones para Neon de Eclipse, vaya demasiado**ayuda** > **buscar actualizaciones**.

2.  Hola tooinstall Service Fabric complemento Neon de Eclipse, vaya demasiado**ayuda** > **instalar nuevo Software**.
  1.    Hola **trabajar con** cuadro, escriba **http://dl.microsoft.com/eclipse**.
  2.    Haga clic en **Agregar**.

         ![Complemento Service Fabric para Eclipse Neon][sf-eclipse-plugin-install]
  3.    Seleccione Hola Service Fabric complemento y, a continuación, haga clic en **siguiente**.
  4.    Complete los pasos de instalación de hello y, a continuación, acepte los términos de licencia del Software de Microsoft de Hola.

Si ya tiene Hola complemento Service Fabric instalado, asegúrese de que tiene la versión más reciente de Hola. toocheck si hay actualizaciones disponibles, vaya demasiado**ayuda** > **detalles de instalación**. En la lista Hola de complementos instalados, seleccione Service Fabric y, a continuación, haga clic en **actualización**. Se instalarán las actualizaciones disponibles.

> [!NOTE]
> Si instalar o actualizar Hola Service Fabric complemento es lenta, podría ser debido a la configuración de Eclipse tooan. Eclipse recopila metadatos en todos los sitios de tooupdate de cambios que están registrados con la instancia de Eclipse. toospeed proceso Hola de buscar e instalar una actualización de complemento de Service Fabric, vaya demasiado**sitios de Software disponibles**. Desactive las casillas de verificación de Hola para todos los sitios excepto Hola uno que señala la ubicación del complemento de Service Fabric toohello (http://dl.microsoft.com/eclipse/azure/servicefabric).

## <a name="create-a-service-fabric-application-in-eclipse"></a>Creación de una aplicación de Service Fabric en Eclipse

1.  En Eclipse Neon, vaya demasiado**archivo** > **New** > **otros**. Seleccione **Service Fabric Project** (Proyecto de Service Fabric) y haga clic en **Next** (Siguiente).

    ![Página 1 del nuevo proyecto de Service Fabric][create-application/p1]

2.  Escriba el nombre del proyecto y haga clic en **Next** (Siguiente).

    ![Página 2 del nuevo proyecto de Service Fabric][create-application/p2]

3.  En la lista Hola de plantillas, seleccione **plantilla de servicio**. Seleccione el tipo de plantilla de servicio (Actor, Stateless, Container o Guest Binary) y, después, haga clic en **Next** (Siguiente).

    ![Página 3 del nuevo proyecto de Service Fabric][create-application/p3]

4.  Escriba el nombre de servicio de Hola y detalles de servicio y, a continuación, haga clic en **finalizar**.

    ![Página 4 del nuevo proyecto de Service Fabric][create-application/p4]

5. Al crear su primer proyecto de Service Fabric en hello **abrir perspectiva asociados** cuadro de diálogo, haga clic en **Sí**.

    ![Página 5 del nuevo proyecto de Service Fabric][create-application/p5]

6.  Así es el nuevo proyecto:

    ![Página 6 del nuevo proyecto de Service Fabric][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Creación e implementación de una aplicación de Service Fabric en Eclipse

1.  Haga clic con el botón derecho en la nueva aplicación de Service Fabric y, después, seleccione **Service Fabric**.

    ![Menú contextual de Service Fabric][publish/RightClick]

2. En el submenú de hello, seleccione opción de Hola que desee:
    -   aplicación de hello toobuild sin limpiar, haga clic en **aplicación generar**.
    -   Haga clic en una compilación limpia de la aplicación hello, toodo **volver a generar aplicaciones**.
    -   aplicación de hello tooclean de artefactos integrados, haga clic en **aplicación limpia**.

3.  Desde este menú también se puede implementar, anular la implementación y publicar una aplicación:
    -   clúster local de toodeploy tooyour, haga clic en **implementar aplicación**.
    -   Hola **publicar aplicación de** cuadro de diálogo, seleccione un perfil de publicación:
        -  **Local.json**
        -  **Cloud.json**

     Estos archivos de JavaScript Object Notation (JSON) almacenan información (por ejemplo, los extremos de conexión e información de seguridad) que es necesario tooconnect tooyour local o un clúster en la nube (Azure).

  ![Menú Publish (Publicar) de Service Fabric][publish/Publish]

Una manera alternativa de toodeploy Service Fabric se ejecute la aplicación mediante el uso de Eclipse configuraciones.

  1.    Vaya demasiado**ejecutar** > **configuraciones de ejecución de**.
  2.    En **Gradle proyecto**, seleccione hello **ServiceFabricDeployer** configuración de ejecución.
  3.    En panel derecho de hello, en hello **argumentos** ficha, para **publishProfile**, seleccione **local** o **nube**.  valor predeterminado de Hello es **local**. toodeploy tooa remoto o un clúster en la nube, seleccione **nube**.
  4.    tooensure que se rellena la información adecuada de Hola Hola perfiles de publicación, edite **Local.json** o **Cloud.json** según sea necesario. Puede agregar o actualizar los detalles del punto de conexión y las credenciales de seguridad.
  5.    Asegúrese de que **Working Directory** señala aplicación toohello desea toodeploy. toochange Hola aplicación, haga clic en hello **área de trabajo** botón y, a continuación, seleccione aplicación Hola que desee.
  6.    Haga clic en **Apply** (Aplicar) y luego en **Run** (Ejecutar).

La aplicación se compila e implementa en un momento. Puede supervisar el estado de implementación de hello en el Explorador de Service Fabric.  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>Agregar un tooyour de servicio de Service Fabric aplicación Service Fabric

Hola tooadd una Service Fabric tooan existente Service Fabric aplicación de servicio, lo siguiente:

1.  Menú contextual proyecto de hello desea tooadd un servicio y, a continuación, haga clic en **Service Fabric**.

    ![Página 1 de Agregar servicio de Service Fabric][add-service/p1]

2.  Haga clic en **Agregar servicio de Fabric**, y Hola completo conjunto de pasos tooadd un proyecto de servicio toohello.
3.  Plantilla de servicio de hello SELECT que desee tooadd tooyour proyecto y, a continuación, haga clic en **siguiente**.

    ![Página 2 de Agregar servicio de Service Fabric][add-service/p2]

4.  Escriba el nombre del servicio de hello (y otros detalles, según sea necesario) y, a continuación, haga clic en hello **Agregar servicio** botón.  

    ![Página 3 de Agregar servicio de Service Fabric][add-service/p3]

5.  Después de agrega el servicio de hello, la estructura del proyecto global tiene un aspecto similar toohello después de proyecto:

    ![Página 4 de Agregar servicio de Service Fabric][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>Edición de las versiones de manifiesto de su aplicación Java de Service Fabric

versiones de manifiesto tooedit, haga clic con el botón secundario en el proyecto de hello, vaya demasiado**Service Fabric** y seleccione **editar versiones de manifiesto...**  de lista desplegable del menú Hola. En el Asistente de hello, puede actualizar versiones de manifiesto de hello para el manifiesto del servicio de aplicación manifiesto y versiones de hello para **código**, **Config** y **datos** paquetes.

Si activa la opción de hello **actualizar automáticamente la aplicación y las versiones de servicio** y, a continuación, actualizar una versión, las versiones de manifiesto de hello, a continuación, se actualizará automáticamente. toogive un ejemplo, primero selecciona casilla de verificación de hello, versión de Hola de actualización de **código** versión de 0.0.0 too0.0.1 y haga clic en **finalizar**, versión del manifiesto y el manifiesto de aplicación de servicio, a continuación, versión será too0.0.1 actualizan automáticamente.

## <a name="upgrade-your-service-fabric-java-application"></a>Actualización de la aplicación Java de Service Fabric

Para un escenario de actualización, diga creaste hello **App1** proyecto usando Hola Service Fabric complemento de Eclipse. Se implementó mediante Hola complemento toocreate una aplicación denominada **fabric: / App1Application**. tipo de aplicación Hello es **App1AppicationType**, y la versión de la aplicación hello es 1.0. Ahora, desea tooupgrade la aplicación sin interrumpir la disponibilidad.

En primer lugar, realice los cambios tooyour aplicación y, a continuación, volver a generar servicio Hola modificado. Hola de actualización modifica (ServiceManifest.xml) del archivo de manifiesto del servicio con las versiones de hello actualizado para servicio de hello (y código, configuración o datos, según corresponda). Además, modificar el manifiesto de la aplicación hello (ApplicationManifest.xml) con el número de versión de Hola actualizado para aplicación hello y Hola servicio modificado.  

tooupgrade la aplicación mediante el uso de neón de Eclipse, puede crear un perfil de configuración de ejecución duplicados. A continuación, utilice el tooupgrade la aplicación según sea necesario.

1.  Vaya demasiado**ejecutar** > **configuraciones de ejecución de**. En el panel izquierdo de hello, haga clic en hello pequeña flecha toohello a la izquierda de **Gradle proyecto**.
2.  Haga clic con el botón derecho en **ServiceFabricDeployer** y seleccione **Duplicate** (Duplicar). Escriba un nuevo nombre para esta configuración, por ejemplo, **ServiceFabricUpgrader**.
3.  En el panel derecho de hello, en hello **argumentos** , modifique **- ipconfig = 'implementar'** demasiado**- ipconfig = 'actualizar'**y, a continuación, haga clic en **aplicar**.

Este proceso crea y guarda un perfil de configuración de ejecución pueden usar en cualquier tooupgrade tiempo su aplicación. También obtiene versión del tipo de aplicación actualizada más reciente de Hola desde el archivo de manifiesto de aplicación Hola.

actualización de la aplicación Hello tarda unos minutos. Puede supervisar la actualización de la aplicación hello en el Explorador de Service Fabric.

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migrar toobe de aplicaciones de Java de tejido de servicio anterior utilizado con Maven
Recientemente se han transferido bibliotecas de Java de tejido de servicio desde el repositorio de tooMaven del SDK de Java del tejido de servicio. Mientras que las aplicaciones nuevas de hello generar usando Eclipse, generará más reciente de los proyectos actualizados (que serán capaz de toowork con Maven), puede actualizar su tejido de servicio existente sin estado o las aplicaciones de Java de actor, que usaba Hola SDK de Java del tejido de servicio versiones anteriores, toouse Hola Java de tejido de servicio las dependencias de Maven. Siga los pasos de hello mencionados [aquí](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure la aplicación anterior funcione con Maven.

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
