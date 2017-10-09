---
title: "aaaContinuous compilación e integración de la aplicación Linux Java de Azure Service Fabric con Jenkins | Documentos de Microsoft"
description: "Compilación e integración continua de la aplicación de Java para Linux de Azure Service Fabric mediante Jenkins"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Usar Jenkins toobuild e implementar la aplicación Linux Java
Jenkins es una herramienta popular para la integración e implementación continuas de aplicaciones. Le mostramos cómo toobuild e implementar la aplicación de Azure Service Fabric mediante Jenkins.

## <a name="general-prerequisites"></a>Requisitos previos generales
- Git debe estar instalado localmente. Puede instalar versión de Hola adecuada Git desde [página de descargas de hello Git](https://git-scm.com/downloads), en función de su sistema operativo. Si es nuevo tooGit, obtener más información de hello [Git documentación](https://git-scm.com/docs).
- Tener Hola Service Fabric Jenkins complemento práctica. Puede descargarlo de las [descargas de Service Fabric](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Configuración de Jenkins en un clúster de Service Fabric

Jenkins se puede configurar dentro o fuera de un clúster de Service Fabric. siguiente Hola secciones mostrar tooset, configúrelo dentro de un clúster al usar un almacenamiento de Azure cuenta y cómo toosave estado de hello de la instancia del contenedor de Hola.

### <a name="prerequisites"></a>Requisitos previos
1. Tenga preparado un clúster Linux de Service Fabric. Un clúster de Service Fabric creado a partir de hello portal de Azure ya tiene Docker instalado. Si se ejecutan localmente clúster hello, compruebe si Docker se instala mediante el comando hello ``docker info``. Si no está instalado, instálelo en consecuencia usando Hola comandos siguientes:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Tiene la aplicación de contenedor de Service Fabric hello implementada en el clúster de hello, mediante el uso de hello siguiendo los pasos:

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. Necesita Hola conectarse detalles de las opciones del programa Hola a almacenamiento de Azure recurso compartido de archivos, donde desea que toopersist Hola de instancia del contenedor de hello Jenkins. Si usas el portal de Microsoft Azure Hola para hello iguales, por favor, siga los pasos de hello: crear una cuenta de almacenamiento de Azure, digamos ``sfjenkinsstorage1``. Cree un **recurso compartido de archivos** en esa cuenta de almacenamiento, por ejemplo ``sfjenkins``. Haga clic en **conectar** para Hola Hola de recurso compartido de archivos y observe los valores se muestra debajo de **conectarse desde Linux**, diga esto sería como sigue:
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Actualizar valores de marcador de posición de Hola Hola ```setupentrypoint.sh``` script con los detalles de almacenamiento de azure correspondientes.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
Reemplace ``[REMOTE_FILE_SHARE_LOCATION]`` con el valor de hello ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` de salida de hello de hello conectarse en el punto 3.
Reemplace ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` con el valor de hello ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` desde el punto 3 anteriores.

5. Conéctese toohello clúster e instale la aplicación de contenedor de hello.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
Esto instala un contenedor Jenkins en clúster de Hola y puede supervisarse utilizando Hola Service Fabric Explorer.

### <a name="steps"></a>Pasos
1. En el explorador, vaya demasiado``http://PublicIPorFQDN:8081``. Proporciona la ruta de acceso de Hola de toosign de requiere una contraseña de administrador inicial de hello en. Puede continuar toouse Jenkins como un usuario administrador. O bien, puede crear y cambiar usuario hello, una vez que inicie sesión con la cuenta de administrador inicial de Hola.

   > [!NOTE]
   > Asegúrese de especifica puerto 8081 de hello como puerto de extremo de aplicación Hola durante la creación de clúster de Hola.
   >

2. Obtener Id. de instancia de contenedor de hello mediante ``docker ps -a``.
3. Secure Shell (SSH) de inicio de sesión toohello contenedor y pegue la ruta de acceso de Hola que se mostraron en el portal de hello Jenkins. Por ejemplo, si en el portal de Hola muestra la ruta de acceso de hello `PATH_TO_INITIAL_ADMIN_PASSWORD`, ejecute hello siguiente:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Configurar el toowork de GitHub con Jenkins, mediante los pasos de hello mencionados en [generar una nueva clave SSH y agregar agente SSH de toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * Usar instrucciones de hello proporcionadas por clave SSH de GitHub toogenerate hello y tooadd Hola SSH clave toohello cuenta de GitHub que hospeda el repositorio.
    * Ejecute comandos de hello mencionados en hello anterior vínculo Hola shell Jenkins Docker (y no en el host).
    * toosign en toohello Jenkins shell del host, Hola de uso siguiente comando:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Configuración de Jenkins fuera de un clúster de Service Fabric

Jenkins se puede configurar dentro o fuera de un clúster de Service Fabric. Hola después cómo mostrar secciones tooset, configúrelo fuera de un clúster.

### <a name="prerequisites"></a>Requisitos previos
Necesita toohave Docker instalado. Hola después de comandos puede ser usado tooinstall Docker de hello terminal:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Ahora, cuando ejecute ``docker info`` Hola terminal, debería aparecer en la salida de hello ese hello Docker servicio se está ejecutando.

### <a name="steps"></a>Pasos
  1. Imagen de contenedor de servicio Fabric Jenkins Hola de extracción:``docker pull raunakpandya/jenkins:v1``
  2. Ejecutar la imagen de contenedor de hello:``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Obtener Id. de Hola de instancia de imagen de contenedor de Hola. Puede enumerar todos los contenedores de Docker de hello con comandos de Hola``docker ps –a``
  4. Inicie sesión en toohello Jenkins portal mediante Hola pasos:

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Si el identificador del contenedor es 2d24a73b5964, use 2d24.
    * Esta contraseña es necesaria para iniciar sesión en el panel de Jenkins toohello desde el portal, que es``http://<HOST-IP>:8080``
    * Después de iniciar sesión para hello primera vez, puede crear su propia cuenta de usuario y usarlo para propósitos futuros, o puede continuar la cuenta de administrador de toouse Hola. Después de crear un usuario, deberá toocontinue con el.
  5. Configurar el toowork de GitHub con Jenkins, mediante los pasos de hello mencionados en [generar una nueva clave SSH y agregar agente SSH de toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * Usar instrucciones de hello proporcionadas por clave SSH de GitHub toogenerate hello y tooadd Hola SSH clave toohello cuenta de GitHub que hospeda el repositorio de Hola.
        * Ejecute comandos de hello mencionados en hello anterior vínculo Hola shell Jenkins Docker (y no en el host).
      * toosign en toohello Jenkins shell del host, Hola de uso siguientes comandos:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Asegúrese de ese clúster de Hola o máquina donde Hola se hospeda la imagen del contenedor Jenkins tiene una dirección IP pública. Esto permite que las notificaciones de instancia tooreceive Jenkins de Hola desde GitHub.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>Instalar Hola Service Fabric Jenkins complemento desde el portal de Hola

1. Vaya demasiado``http://PublicIPorFQDN:8081``
2. En el panel de Jenkins hello, seleccione **administrar Jenkins** > **administrar complementos** > **avanzadas**.
Aquí puede cargar un complemento. Seleccione **Elegir archivo**y, a continuación, seleccione hello **serviceFabric.hpi** archivo que descargó en los requisitos previos. Cuando se selecciona **cargar**, Jenkins Hola complemento instala automáticamente. Permita un reinicio si se solicita.

## <a name="create-and-configure-a-jenkins-job"></a>Creación y configuración de trabajos de Jenkins

1. Cree un **nuevo elemento** desde el panel.
2. Escriba un nombre para dicho elemento (por ejemplo, **MyJob**). Seleccione **free-style project** (proyecto de estilo libre) y haga clic en **OK** (Aceptar).
3. Ir a página de trabajo de Hola y haga clic en **configurar**.

   a. En la sección general de hello, en **GitHub proyecto**, especifique la dirección URL de proyecto de GitHub. Flujo de implementación continua (CI/CD) de esta aplicación de Java de tejido de servicio Hola de direcciones URL de hosts se que desea toointegrate con hello integración continua Jenkins, (por ejemplo, ``https://github.com/sayantancs/SFJenkins``).

   b. En hello **administración de código fuente** sección, seleccione **Git**. Especifique la dirección URL de repositorio de Hola que hospeda la aplicación de Java de tejido de servicio de hello que desea toointegrate con hello flujo Jenkins CI/CD (por ejemplo, ``https://github.com/sayantancs/SFJenkins.git``). Además, puede especificar aquí qué toobuild rama (por ejemplo, **del patrón o**).
4. Configurar la *GitHub* (que hospeda el repositorio de hello) para que sea capaz de tootalk tooJenkins. Usar hello pasos:

   a. Ir a página de repositorio de GitHub de tooyour. Vaya demasiado**configuración** > **integraciones y servicios**.

   b. Seleccione **Agregar servicio**, tipo **Jenkins**, seleccione hello y **complemento de GitHub Jenkins**.

   c. Escriba la dirección URL del webhook de Jenkins (de forma predeterminada, será ``http://<PublicIPorFQDN>:8081/github-webhook/``). Haga clic en **Add/Update Service** (Agregar o actualizar servicio).

   d. Se enviará un evento de prueba tooyour Jenkins instancia. Debería ver una marca de verificación verde por hello webhook en GitHub y se compilará el proyecto.

   e. En hello **crear desencadenadores** sección, seleccione qué opción que desee de la compilación. En este ejemplo, desea tootrigger una compilación siempre que ocurre algunos repositorio toohello de inserción. Por tanto, selecciona **GitHub hook trigger for GITScm polling** (Desencadenador de enlace de GitHub para el sondeo de GITScm). (Anteriormente, esta opción se denomina **de compilación cuando un cambio se inserta tooGitHub**.)

   f. En hello **compilar sección**, desde la lista desplegable de Hola **agregar el paso de compilación**, seleccione opción hello **invocar el Gradle Script**. Widget de Hola que viene, especificar ruta de acceso de hello demasiado**raíz Generar script** para la aplicación. Recoge build.gradle de ruta de acceso de hello especificada y funciona en consecuencia. Si crea un proyecto denominado ``MyActor`` (mediante el generador de complemento o Yeoman Eclipse hello), debe contener el script de compilación de hello raíz ``${WORKSPACE}/MyActor``. Vea Hola siguiente captura de pantalla para obtener un ejemplo del aspecto:

    ![Acción de compilación de Jenkins en Service Fabric][build-step]

   g. De hello **acciones posteriores a la compilación** lista desplegable, seleccione **implementar proyecto de tejido de servicio**. Aquí deberá clúster tooprovide se implementaría detalles donde hello Jenkins compilan aplicaciones de Service Fabric. También puede proporcionar detalles adicionales de la aplicación utilizan la aplicación de hello toodeploy. Vea Hola siguiente captura de pantalla para obtener un ejemplo del aspecto:

    ![Acción de compilación de Jenkins en Service Fabric][post-build-step]

   > [!NOTE]
   > clúster de Hello aquí podría ser la misma que Hola Hola hospedaje una aplicación de contenedor de Jenkins, en caso de que usa la imagen de contenedor de Service Fabric toodeploy Hola Jenkins.
   >

## <a name="next-steps"></a>Pasos siguientes
GitHub y Jenkins ya están configurados. Considere la posibilidad de realizar algunos ejemplos de cambios en su ``MyActor`` proyecto de ejemplo de Hola a repositorio, https://github.com/sayantancs/SFJenkins. Insertar su tooa cambios remoto ``master`` bifurcación (o alguna de las bifurcaciones que ha configurado toowork con). Esto desencadena el trabajo de Jenkins hello, ``MyJob``, que ha configurado. Captura los cambios de Hola de GitHub, compilará e implementa Hola aplicación toohello clúster punto de conexión especificado en las acciones posteriores a la compilación.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
