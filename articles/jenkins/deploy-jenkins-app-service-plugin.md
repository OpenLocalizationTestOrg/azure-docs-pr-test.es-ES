---
title: aaaDeploy tooAzure servicio de aplicaciones con Jenkins Plugin | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Jenkins de servicio de aplicación de Azure complemento toodeploy un Java web tooAzure de aplicación en Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>Implementar tooAzure servicio de aplicaciones con Jenkins complemento 
toodeploy una tooAzure de aplicación web de Java, puede utilizar la CLI de Azure en [Jenkins canalización](/azure/jenkins/execute-cli-jenkins-pipeline) o hacer que el uso de hello [Jenkins de servicio de aplicación de Azure complemento](https://plugins.jenkins.io/azure-app-service). En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Configurar Jenkins toodeploy tooAzure servicio de aplicaciones a través de FTP 
> * Configurar Jenkins toodeploy tooAzure servicio de aplicaciones en Linux a través de Docker 

## <a name="create-and-configure-jenkins-instance"></a>Creación y configuración de una instancia de Jenkins
Si no tiene todavía un patrón Jenkins, comience con hello [plantilla de solución](install-jenkins-solution-template.md), que incluye hello siguiendo los complementos necesarios y JDK8:

* [Complemento de cliente de Git de Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Complemento Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Credenciales de Azure](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1

Puede usar hello toodeploy de complemento de servicio de aplicaciones Web App en todos los idiomas (por ejemplo, C#, PHP, Java y node.js, etc.) admitidos por el servicio de aplicaciones de Azure. En este tutorial, estamos utilizando aplicaciones de Java de ejemplo de Hola, [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample). toofork Hola repositorio tooyour posee la cuenta de GitHub, haga clic en hello **bifurcar** botón en la esquina superior derecha de Hola.  

Java JDK y Maven son necesarios para compilar el proyecto de Java de Hola. Asegúrese de que instalar componentes de hello en master de hello Jenkins o agente de máquina virtual de hello si usa un para la integración continua. 

tooinstall, inicie sesión en toohello Jenkins instancia mediante SSH y ejecute hello siguientes comandos:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Para implementar tooApp servicio en Linux, también deberá tooinstall Docker en patrón de Jenkins Hola o el agente de máquina virtual de hello utilizado para la compilación. Consulte el artículo de toothis tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Agregar credencial tooJenkins principal de servicio de Azure

Una entidad de seguridad de servicio de Azure es necesario toodeploy tooAzure. 

<ol>
<li>Use [CLI de Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) o [portal de Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate una entidad de seguridad de servicio de Azure</li>
<li>En el panel de Jenkins hello, haga clic en **credenciales -> sistema ->**. Haga clic en **Global credentials(unrestricted) ** [Credenciales (sin restricción) globales].</li>
<li>Haga clic en **agregar credenciales** tooadd una entidad de servicio de Microsoft Azure rellenando Hola Id. de suscripción, Id. de cliente, el secreto de cliente y extremo de Token de OAuth 2.0. Proporcione un identificador, **mySp**, para su uso en los siguientes pasos.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Complemento de Azure App Service

Azure v1.0 de complemento de servicio de aplicaciones admite la implementación continua tooAzure aplicación Web a través de:

* Git y FTP
* Docker para aplicaciones web en Linux

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Configurar Jenkins toodeploy aplicación Web a través de FTP con hello Jenkins panel

toodeploy su tooAzure de project Web App, puede cargar los artefactos de compilación (por ejemplo, el archivo .war en Java) usando Git o FTP.

Antes de configurar el trabajo de hello en Jenkins, necesita un plan de servicio de aplicaciones de Azure y una aplicación Web para la aplicación en ejecución Hola Java.


1. Crear un plan de servicio de aplicaciones de Azure con hello **libre** tarifa con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando de CLI. plan de servicio de aplicaciones de Hello define Hola recursos físicos que usa toohost sus aplicaciones. Todas las aplicaciones asignadas plan de servicio de aplicaciones de tooan compartan estos recursos, permitiéndole toosave costo al hospedar varias aplicaciones.
2. Creación de una aplicación web. Puede cualquier Hola uso [portal de Azure](/azure/app-service-web/web-sites-configure) o use Hola siguiente comando de CLI Az:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Asegúrese de que establecer la configuración de tiempo de ejecución de Java de Hola que necesita la aplicación. Hola siguiente comando de CLI de Azure configura toorun de aplicación web de hello en una versión reciente de Java 8 JDK y [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Configurar el trabajo de hello Jenkins


1. Creación de un nuevo proyecto **freestyle** (estilo libre) en el panel de Jenkins
2. Configurar **administración de código fuente** toouse la bifurcación local de [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample) proporcionando hello **dirección URL de repositorio**. Por ejemplo: http://github.com/&lt;su_ID>/javawebappsample.
3. Agregar un proyecto de hello toobuild de paso de compilación mediante Maven. Para ello, agregue un paso **Execute shell** (ejecutar shell). En este ejemplo, se necesita un archivo de *.war paso adicional toorename hello en tooROOT.war de la carpeta de destino.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Agregue una acción posterior a la compilación seleccionando **Publish an Azure Web App** (publicar una aplicación web de Azure).
5. Fuente de alimentación, "mySp", entidad de seguridad de servicio de Azure de hello almacenados en el paso anterior.
6. En **configuración de la aplicación** sección, elija la aplicación de web y el grupo de recursos de hello en su suscripción. complemento de Hello detecta automáticamente si Hola aplicación Web es Windows o Linux. Para una aplicación Web basada en Windows, se presenta la opción de Hola "Publicar archivos".
7. Rellenar en archivos de hello desea toodeploy (por ejemplo, un war paquete si utiliza Java.) Source Directory (directorio de origen) y Target Directory (directorio de destino) son opcionales. parámetros de Hello permiten toospecify carpetas de origen y de destino al cargar archivos. La aplicación web de Java en Azure se ejecuta en un servidor de Tomcat. Por lo tanto, cargue el paquete war a la carpeta webapps. En este ejemplo, establezca **el directorio de origen** demasiado "destino" y proporcionan "móviles" de **directorio de destino**.
8. Si desea toodeploy tooa ranura que no sea de producción, también puede establecer **ranura** nombre.
9. Guarde el proyecto de Hola y genérelo. La aplicación web está implementada tooAzure cuando se completa la compilación.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Implementación de la aplicación web a través de FTP mediante la canalización de Jenkins

complemento de Hello está preparada para la canalización. Puede hacer referencia en el ejemplo tooa en el repositorio de GitHub de Hola.

1. En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile_ftp_plugin**. Haga clic en tooedit de icono de lápiz Hola este grupo de recursos de archivo tooupdate Hola y el nombre de la aplicación web en línea 11 y 12 respectivamente.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Cambie la línea 14 tooupdate el identificador de la credencial en la instancia de Jenkins.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Creación de una canalización de Jenkins

1. Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento).
2. Proporcione un nombre para el trabajo de Hola y seleccione **canalización**. Haga clic en **Aceptar**.
3. Haga clic en hello **canalización** pestaña a continuación.
4. En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).
5. En **SCM**, seleccione **Git**. Escriba hello GitHub URL para el repositorio bifurcada: https:&lt;repositorio bifurcada > .git
6. Actualización **ruta del Script** demasiado "Jenkinsfile_ftp_plugin"
7. Haga clic en **guardar** y trabajo de ejecución Hola.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Configurar Jenkins toodeploy aplicación Web en Linux a través de Docker

Además de con Git y FTP, la aplicación web en Linux admite la implementación con Docker. toodeploy con Docker, deberá tooprovide un Dockerfile que empaqueta la aplicación web con el runtime del servicio en una imagen de docker. A continuación, Hola complemento genera imágenes de hello, inserta del registro de docker de tooa e implementa Hola imagen tooyour web app.

La aplicación web en Linux también admite los métodos tradicionales como Git y FTP, pero solo para los lenguajes integrados (.NET Core, Node.js, PHP y Ruby). Para otros idiomas, es necesario toopackage el tiempo de ejecución de código y el servicio de aplicación juntos en una imagen de docker y usar toodeploy de docker.

Antes de configurar el trabajo de hello en Jenkins, necesita un servicio de aplicación de Azure en Linux. Un registro de contenedor también es necesario toostore y administrar las imágenes de contenedor de Docker privadas. Puede usar DockerHub; en este ejemplo, usamos Azure Container Registry.

* Puede seguir los pasos de hello [aquí](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate una aplicación Web en Linux 
* Registro de contenedor de Azure es un administrado [Docker registro] servicio (https://docs.docker.com/registry/) basado en Hola 2.0 de registro de Docker de código abierto. Siga los pasos de hello [aquí] (/ azure/container-registry/container-registry-get-started-azure-cli) para obtener instrucciones sobre cómo toodo para. También puede usar DockerHub.

### <a name="toodeploy-using-docker"></a>toodeploy con docker:

1. Cree un nuevo proyecto freestyle (estilo libre) en el panel de Jenkins.
2. Configurar **administración de código fuente** toouse la bifurcación local de [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample) proporcionando hello **dirección URL de repositorio**. Por ejemplo: http://github.com/&lt;su_ID>/javawebappsample.
Agregar un proyecto de hello toobuild de paso de compilación mediante Maven. Hacerlo agregando una **ejecutar shell** y agregue Hola después de línea en **comando**:    
```bash
mvn clean package
```

3. Agregue una acción posterior a la compilación seleccionando **Publish an Azure Web App** (publicar una aplicación web de Azure).
4. Proporcionar, **mySp**, entidad de seguridad de servicio de Azure de hello almacenado en el paso anterior como credenciales de Azure.
5. En **configuración de la aplicación** sección, elija el grupo de recursos de hello y una aplicación web de Linux en su suscripción.
6. Elija Publish via Docker (publicar a través de Docker).
7. Rellene la ruta de acceso de **Dockerfile** (archivo de Docker). Puede conservar Hola predeterminada "/ Dockerfile" para **dirección URL de registro de Docker**, proporcione en formato de hello https://&lt;myRegistry >. azurecr.io si usas registro de contenedor de Azure. Déjelo en blanco si utiliza DockerHub.
8. Para **las credenciales del registro**, agregar credenciales de Hola para saludo del registro de contenedor de Azure. Puede obtener userid hello y una contraseña mediante la ejecución de hello siga los comandos de CLI de Azure. Hola primer comando habilita la cuenta de administrador de Hola.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Hola nombre de la imagen de docker y la etiqueta en **avanzadas** ficha son opcionales. De forma predeterminada, se obtiene el nombre de la imagen de la imagen de Hola nombre configurado en la etiqueta de Azure Hola portal (en la configuración de contenedor de Docker.) se genera desde $BUILD_NUMBER. Asegúrese de especificar el nombre de la imagen de Hola en cualquier portal de Azure o proporcionar un valor para **imagen de Docker** en **avanzadas** ficha. En este ejemplo, escriba "&lt;su_registro>.azurecr.io/calculator" para **Docker image** (imagen de Docker) y deje **Docker Image Tag** (etiqueta de imagen de Docker) en blanco.
10. Se produce un error en la implementación si utiliza la configuración de imagen de Docker integrada. Asegúrese de que cambiar imagen personalizada toouse de docker config en configuración del contenedor de Docker en el portal de Azure. Para la imagen integrada, utilice toodeploy de enfoque de carga de archivo.
11. Enfoque de carga toofile similar, puede elegir una ranura diferente que no sea de producción.
12. Guarde y compile el proyecto de Hola. Vea la imagen de contenedor se inserta el registro de tooyour y se implementa la aplicación web.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>Implementar la aplicación en Linux a través de Docker mediante canalización Jenkins tooWeb

1. En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile_container_plugin**. Haga clic en tooedit de icono de lápiz Hola este grupo de recursos de archivo tooupdate Hola y el nombre de la aplicación web en línea 11 y 12 respectivamente.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Cambiar servidor de línea 13 tooyour contenedor del registro    
```java
def registryServer = '<registryURL>'
```    

3. Cambie la línea tooupdate 16 el identificador de la credencial en la instancia de Jenkins    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Creación de una canalización de Jenkins    

1. Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento).
2. Proporcione un nombre para el trabajo de Hola y seleccione **canalización**. Haga clic en **Aceptar**.
3. Haga clic en hello **canalización** pestaña a continuación.
4. En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).
5. En **SCM**, seleccione **Git**.
6. Escriba hello GitHub URL para el repositorio bifurcada: https:&lt;repositorio bifurcada > .git</li>
Actualizar 7, **ruta del Script** demasiado "Jenkinsfile_container_plugin"
8. Haga clic en **guardar** y trabajo de ejecución Hola.

## <a name="verify-your-web-app"></a>Comprobación de la aplicación web

1. archivo WAR de tooverify Hola se ha implementado correctamente tooyour web app. Abra un explorador web.
2. Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping verá:    
     Página principal tooJava aplicación Web. Se ha actualizado.
   Sun Jun 17 16:39:10 UTC 2017
3. Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sustituya &lt;x > y &lt;y > con los números) suma de hello tooget de x e y        
    ![Calculadora: suma](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Para App Service en Linux

* tooverify, en CLI de Azure, ejecute:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Obtener Hola siguiente resultado:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping. Consulte el mensaje de bienvenida: 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sustituya &lt;x > y &lt;y > con los números) suma de hello tooget de x e y
    
## <a name="next-steps"></a>Pasos siguientes

En este tutorial, utilizará Hola servicio de aplicaciones de Azure complemento toodeploy tooAzure.

Ha aprendido a:

> [!div class="checklist"]
> * Configurar Jenkins toodeploy servicio de aplicaciones de Azure a través de FTP 
> * Configurar Jenkins toodeploy tooAzure servicio de aplicaciones en Linux a través de Docker 
