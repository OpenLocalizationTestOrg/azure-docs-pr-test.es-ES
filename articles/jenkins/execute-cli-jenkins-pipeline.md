---
title: Hola aaaExecute CLI de Azure con Jenkins | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse CLI de Azure toodeploy un Java web tooAzure de aplicación en la canalización de Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>Implementar el servicio de aplicaciones con Jenkins tooAzure y Hola CLI de Azure
toodeploy una tooAzure de aplicación web de Java, puede utilizar la CLI de Azure en [Jenkins canalización](https://jenkins.io/doc/book/pipeline/). En este tutorial, creará una canalización de CI/CD en una máquina virtual de Azure, y aprenderá los siguientes temas:

> [!div class="checklist"]
> * Crear una máquina virtual de Jenkins
> * Configuración de Jenkins
> * Creación de una aplicación web en Azure
> * Preparación de un repositorio de GitHub
> * Creación de una canalización de Jenkins
> * Ejecutar la canalización de Hola y compruebe la aplicación web de hello

Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores. versión de hello toofind, ejecute `az --version`. Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Creación y configuración de una instancia de Jenkins
Si no tiene todavía un patrón Jenkins, comience con hello [plantilla de solución](install-jenkins-solution-template.md), que incluye Hola necesario [las credenciales de Azure](https://plugins.jenkins.io/azure-credentials) complemento de forma predeterminada. 

complemento de Azure credencial Hola permite toostore credenciales de entidad de seguridad de servicio de Microsoft Azure en Jenkins. En la versión 1.2, agregamos compatibilidad Hola para que esa canalización Jenkins puedas hello las credenciales de Azure. 

Compruebe que dispone de la versión 1.2 o posterior:
* En el panel de Jenkins hello, haga clic en **Jenkins administrar -> complemento Administrador ->** y busque **credencial Azure**. 
* Actualizar el complemento de hello si la versión de hello es anterior a 1.2.

Java JDK y Maven también son necesarios en master de hello Jenkins. tooinstall, inicie sesión en el maestro de tooJenkins mediante SSH y ejecute hello siguientes comandos:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Agregar credencial tooJenkins principal de servicio de Azure

Una credencial de Azure es necesario tooexecute CLI de Azure.

* En el panel de Jenkins hello, haga clic en **credenciales -> sistema ->**. Haga clic en **Global credentials(unrestricted)**  [Credenciales (sin restricción) globales].
* Haga clic en **agregar credenciales** tooadd una [entidad de servicio de Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) rellenando Hola Id. de suscripción, Id. de cliente, el secreto de cliente y extremo de Token de OAuth 2.0. Proporcione un identificador para usarlo en el paso posterior.

![Adición de credenciales](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Crear un servicio de aplicaciones de Azure para implementar la aplicación web de Java de Hola

Crear un plan de servicio de aplicaciones de Azure con hello **libre** tarifa con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando de CLI. plan de servicio de aplicaciones de Hello define Hola recursos físicos que usa toohost sus aplicaciones. Todas las aplicaciones asignadas plan de servicio de aplicaciones de tooan compartan estos recursos, permitiéndole toosave costo al hospedar varias aplicaciones. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Si plan de hello está listo, Hola que CLI de Azure muestra similar salida toohello siguiente ejemplo:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Creación de una aplicación web de Azure

 Hola de uso [crear webapp az](/cli/azure/appservice/web#create) toocreate de comando CLI una definición de aplicación web en hello `myAppServicePlan` plan de servicio de aplicaciones. definición de la aplicación Hello web proporciona una tooaccess de dirección URL a la aplicación con y configura varias toodeploy opciones tooAzure de su código. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Hola sustituto `<app_name>` marcador de posición con su propio nombre de aplicación único. Este nombre único forma parte del nombre de dominio predeterminado de hello para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de Azure. Puede asignar una aplicación web de dominio personalizado nombre entrada toohello antes de exponer tooyour a los usuarios.

Cuando la definición de la aplicación hello web está listo, Hola CLI de Azure muestra información toohello similar siguiente ejemplo: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Configuración de Java 

Establecer la configuración de tiempo de ejecución de Java de Hola que necesita la aplicación con hello [actualización de la configuración de az servicio de aplicaciones web](/cli/azure/appservice/web/config#update) comando.

Hello siguiente comando configura toorun de aplicación web de hello en una versión reciente de Java 8 JDK y [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a>Preparación de un repositorio de GitHub
Abra hello [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample) repositorio. toofork Hola repositorio tooyour posee la cuenta de GitHub, haga clic en hello **bifurcar** botón en la esquina superior derecha de Hola.

* En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile**. Haga clic en tooedit de icono de lápiz Hola este grupo de recursos de archivo tooupdate Hola y el nombre de la aplicación web en línea 20 y 21 respectivamente.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Cambie la línea tooupdate 23 el identificador de la credencial en la instancia de Jenkins

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Creación de una canalización de Jenkins
Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento). 

* Proporcione un nombre para el trabajo de Hola y seleccione **canalización**. Haga clic en **Aceptar**.
* Haga clic en hello **canalización** pestaña a continuación. 
* En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).
* En **SCM**, seleccione **Git**.
* Escriba hello GitHub URL para el repositorio bifurcada: https:\<repositorio bifurcada\>.git
* Haga clic en **Guardar**

## <a name="test-your-pipeline"></a>Prueba de la canalización
* Vaya canalización toohello que creó, haga clic en **compilar ahora**
* Debe ejecutarse correctamente una compilación en unos segundos, y puede ir toohello compilación y haga clic en **salida de la consola** detalles de hello toosee

## <a name="verify-your-web-app"></a>Comprobación de la aplicación web
archivo WAR de tooverify Hola se ha implementado correctamente tooyour web app. Abra un explorador web.

* Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping  
Se ve lo siguiente:

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sustituya &lt;x > y &lt;y > con los números) suma de hello tooget de x e y

![Calculadora: suma](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>Implementar tooAzure Web App en Linux
Ahora que sabe cómo toouse CLI de Azure en su Jenkins canalización, puede modificar Hola script toodeploy tooan aplicación Web de Azure en Linux.

Web App en Linux es compatible con una implementación de hello toodo de manera diferente, que es toouse Docker. toodeploy, deberá tooprovide un Dockerfile que empaqueta la aplicación web con el runtime del servicio en una imagen de Docker. complemento de Hello, a continuación, compilará imagen hello, inserción del registro de Docker de tooa e implementará Hola imagen tooyour web app.

* Siga los pasos de hello [aquí](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate una aplicación Web de Azure ejecutando en Linux.
* Instale Docker en su instancia Jenkins siguiendo las instrucciones de hello en este [artículo](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Crear un registro de contenedor en hello portal de Azure mediante los pasos de hello [aquí](/azure/container-registry/container-registry-get-started-azure-cli).
* En Hola mismo [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample) repositorio bifurcado, editar hello **Jenkinsfile2** archivo:
    * Línea 18-21, actualizar los nombres de toohello de su grupo de recursos, la aplicación web y el ACR respectivamente. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Línea 24, actualización \<azsrvprincipal\> tooyour identificador de la credencial
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Crear una nueva canalización Jenkins como lo hizo al implementar la aplicación web de tooAzure en Windows, pero esta vez utilice **Jenkinsfile2** en su lugar.
* Ejecute el nuevo trabajo.
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
En este tutorial, ha configurado una canalización Jenkins que comprueba el código de origen de hello en el repositorio de GitHub. Ejecuta un archivo war de Maven toobuild y, a continuación, usa la CLI de Azure toodeploy tooAzure servicio de aplicaciones. Ha aprendido a:

> [!div class="checklist"]
> * Crear una máquina virtual de Jenkins
> * Configuración de Jenkins
> * Creación de una aplicación web en Azure
> * Preparación de un repositorio de GitHub
> * Creación de una canalización de Jenkins
> * Ejecutar la canalización de Hola y compruebe la aplicación web de hello
