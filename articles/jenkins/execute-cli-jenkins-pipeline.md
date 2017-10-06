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
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="b4804-103">Implementar el servicio de aplicaciones con Jenkins tooAzure y Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b4804-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="b4804-104">toodeploy una tooAzure de aplicación web de Java, puede utilizar la CLI de Azure en [Jenkins canalización](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="b4804-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="b4804-105">En este tutorial, creará una canalización de CI/CD en una máquina virtual de Azure, y aprenderá los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="b4804-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4804-106">Crear una máquina virtual de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="b4804-107">Configuración de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-107">Configure Jenkins</span></span>
> * <span data-ttu-id="b4804-108">Creación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="b4804-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="b4804-109">Preparación de un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="b4804-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="b4804-110">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="b4804-111">Ejecutar la canalización de Hola y compruebe la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="b4804-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="b4804-112">Este tutorial requiere hello Azure CLI versión 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="b4804-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b4804-113">versión de hello toofind, ejecute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="b4804-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="b4804-114">Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b4804-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="b4804-115">Creación y configuración de una instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="b4804-116">Si no tiene todavía un patrón Jenkins, comience con hello [plantilla de solución](install-jenkins-solution-template.md), que incluye Hola necesario [las credenciales de Azure](https://plugins.jenkins.io/azure-credentials) complemento de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b4804-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="b4804-117">complemento de Azure credencial Hola permite toostore credenciales de entidad de seguridad de servicio de Microsoft Azure en Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b4804-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="b4804-118">En la versión 1.2, agregamos compatibilidad Hola para que esa canalización Jenkins puedas hello las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4804-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="b4804-119">Compruebe que dispone de la versión 1.2 o posterior:</span><span class="sxs-lookup"><span data-stu-id="b4804-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="b4804-120">En el panel de Jenkins hello, haga clic en **Jenkins administrar -> complemento Administrador ->** y busque **credencial Azure**.</span><span class="sxs-lookup"><span data-stu-id="b4804-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="b4804-121">Actualizar el complemento de hello si la versión de hello es anterior a 1.2.</span><span class="sxs-lookup"><span data-stu-id="b4804-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="b4804-122">Java JDK y Maven también son necesarios en master de hello Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b4804-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="b4804-123">tooinstall, inicie sesión en el maestro de tooJenkins mediante SSH y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="b4804-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="b4804-124">Agregar credencial tooJenkins principal de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="b4804-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="b4804-125">Una credencial de Azure es necesario tooexecute CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4804-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="b4804-126">En el panel de Jenkins hello, haga clic en **credenciales -> sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="b4804-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="b4804-127">Haga clic en **Global credentials(unrestricted)**  [Credenciales (sin restricción) globales].</span><span class="sxs-lookup"><span data-stu-id="b4804-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="b4804-128">Haga clic en **agregar credenciales** tooadd una [entidad de servicio de Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) rellenando Hola Id. de suscripción, Id. de cliente, el secreto de cliente y extremo de Token de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="b4804-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="b4804-129">Proporcione un identificador para usarlo en el paso posterior.</span><span class="sxs-lookup"><span data-stu-id="b4804-129">Provide an ID for use in subsequent step.</span></span>

![Adición de credenciales](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="b4804-131">Crear un servicio de aplicaciones de Azure para implementar la aplicación web de Java de Hola</span><span class="sxs-lookup"><span data-stu-id="b4804-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="b4804-132">Crear un plan de servicio de aplicaciones de Azure con hello **libre** tarifa con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="b4804-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="b4804-133">plan de servicio de aplicaciones de Hello define Hola recursos físicos que usa toohost sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b4804-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="b4804-134">Todas las aplicaciones asignadas plan de servicio de aplicaciones de tooan compartan estos recursos, permitiéndole toosave costo al hospedar varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b4804-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="b4804-135">Si plan de hello está listo, Hola que CLI de Azure muestra similar salida toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b4804-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="b4804-136">Creación de una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="b4804-136">Create an Azure Web app</span></span>

 <span data-ttu-id="b4804-137">Hola de uso [crear webapp az](/cli/azure/appservice/web#create) toocreate de comando CLI una definición de aplicación web en hello `myAppServicePlan` plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b4804-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="b4804-138">definición de la aplicación Hello web proporciona una tooaccess de dirección URL a la aplicación con y configura varias toodeploy opciones tooAzure de su código.</span><span class="sxs-lookup"><span data-stu-id="b4804-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="b4804-139">Hola sustituto `<app_name>` marcador de posición con su propio nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="b4804-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="b4804-140">Este nombre único forma parte del nombre de dominio predeterminado de hello para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4804-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="b4804-141">Puede asignar una aplicación web de dominio personalizado nombre entrada toohello antes de exponer tooyour a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b4804-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="b4804-142">Cuando la definición de la aplicación hello web está listo, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b4804-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="b4804-143">Configuración de Java</span><span class="sxs-lookup"><span data-stu-id="b4804-143">Configure Java</span></span> 

<span data-ttu-id="b4804-144">Establecer la configuración de tiempo de ejecución de Java de Hola que necesita la aplicación con hello [actualización de la configuración de az servicio de aplicaciones web](/cli/azure/appservice/web/config#update) comando.</span><span class="sxs-lookup"><span data-stu-id="b4804-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="b4804-145">Hello siguiente comando configura toorun de aplicación web de hello en una versión reciente de Java 8 JDK y [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="b4804-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="b4804-146">Preparación de un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="b4804-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="b4804-147">Abra hello [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample) repositorio.</span><span class="sxs-lookup"><span data-stu-id="b4804-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="b4804-148">toofork Hola repositorio tooyour posee la cuenta de GitHub, haga clic en hello **bifurcar** botón en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4804-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="b4804-149">En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="b4804-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="b4804-150">Haga clic en tooedit de icono de lápiz Hola este grupo de recursos de archivo tooupdate Hola y el nombre de la aplicación web en línea 20 y 21 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b4804-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="b4804-151">Cambie la línea tooupdate 23 el identificador de la credencial en la instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="b4804-152">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="b4804-153">Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento).</span><span class="sxs-lookup"><span data-stu-id="b4804-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="b4804-154">Proporcione un nombre para el trabajo de Hola y seleccione **canalización**.</span><span class="sxs-lookup"><span data-stu-id="b4804-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="b4804-155">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b4804-155">Click **OK**.</span></span>
* <span data-ttu-id="b4804-156">Haga clic en hello **canalización** pestaña a continuación.</span><span class="sxs-lookup"><span data-stu-id="b4804-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="b4804-157">En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).</span><span class="sxs-lookup"><span data-stu-id="b4804-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="b4804-158">En **SCM**, seleccione **Git**.</span><span class="sxs-lookup"><span data-stu-id="b4804-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="b4804-159">Escriba hello GitHub URL para el repositorio bifurcada: https:\<repositorio bifurcada\>.git</span><span class="sxs-lookup"><span data-stu-id="b4804-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="b4804-160">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="b4804-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="b4804-161">Prueba de la canalización</span><span class="sxs-lookup"><span data-stu-id="b4804-161">Test your pipeline</span></span>
* <span data-ttu-id="b4804-162">Vaya canalización toohello que creó, haga clic en **compilar ahora**</span><span class="sxs-lookup"><span data-stu-id="b4804-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="b4804-163">Debe ejecutarse correctamente una compilación en unos segundos, y puede ir toohello compilación y haga clic en **salida de la consola** detalles de hello toosee</span><span class="sxs-lookup"><span data-stu-id="b4804-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="b4804-164">Comprobación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="b4804-164">Verify your web app</span></span>
<span data-ttu-id="b4804-165">archivo WAR de tooverify Hola se ha implementado correctamente tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="b4804-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="b4804-166">Abra un explorador web.</span><span class="sxs-lookup"><span data-stu-id="b4804-166">Open a web browser:</span></span>

* <span data-ttu-id="b4804-167">Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="b4804-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="b4804-168">Se ve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b4804-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="b4804-169">Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sustituya &lt;x > y &lt;y > con los números) suma de hello tooget de x e y</span><span class="sxs-lookup"><span data-stu-id="b4804-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Calculadora: suma](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="b4804-171">Implementar tooAzure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="b4804-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="b4804-172">Ahora que sabe cómo toouse CLI de Azure en su Jenkins canalización, puede modificar Hola script toodeploy tooan aplicación Web de Azure en Linux.</span><span class="sxs-lookup"><span data-stu-id="b4804-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="b4804-173">Web App en Linux es compatible con una implementación de hello toodo de manera diferente, que es toouse Docker.</span><span class="sxs-lookup"><span data-stu-id="b4804-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="b4804-174">toodeploy, deberá tooprovide un Dockerfile que empaqueta la aplicación web con el runtime del servicio en una imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="b4804-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="b4804-175">complemento de Hello, a continuación, compilará imagen hello, inserción del registro de Docker de tooa e implementará Hola imagen tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="b4804-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="b4804-176">Siga los pasos de hello [aquí](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate una aplicación Web de Azure ejecutando en Linux.</span><span class="sxs-lookup"><span data-stu-id="b4804-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="b4804-177">Instale Docker en su instancia Jenkins siguiendo las instrucciones de hello en este [artículo](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="b4804-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="b4804-178">Crear un registro de contenedor en hello portal de Azure mediante los pasos de hello [aquí](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b4804-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="b4804-179">En Hola mismo [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample) repositorio bifurcado, editar hello **Jenkinsfile2** archivo:</span><span class="sxs-lookup"><span data-stu-id="b4804-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="b4804-180">Línea 18-21, actualizar los nombres de toohello de su grupo de recursos, la aplicación web y el ACR respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b4804-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="b4804-181">Línea 24, actualización \<azsrvprincipal\> tooyour identificador de la credencial</span><span class="sxs-lookup"><span data-stu-id="b4804-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="b4804-182">Crear una nueva canalización Jenkins como lo hizo al implementar la aplicación web de tooAzure en Windows, pero esta vez utilice **Jenkinsfile2** en su lugar.</span><span class="sxs-lookup"><span data-stu-id="b4804-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="b4804-183">Ejecute el nuevo trabajo.</span><span class="sxs-lookup"><span data-stu-id="b4804-183">Run your new job.</span></span>
* <span data-ttu-id="b4804-184">tooverify, en CLI de Azure, ejecute:</span><span class="sxs-lookup"><span data-stu-id="b4804-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="b4804-185">Obtener Hola siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="b4804-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="b4804-186">Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="b4804-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="b4804-187">Consulte el mensaje de bienvenida:</span><span class="sxs-lookup"><span data-stu-id="b4804-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="b4804-188">Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sustituya &lt;x > y &lt;y > con los números) suma de hello tooget de x e y</span><span class="sxs-lookup"><span data-stu-id="b4804-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="b4804-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4804-189">Next steps</span></span>
<span data-ttu-id="b4804-190">En este tutorial, ha configurado una canalización Jenkins que comprueba el código de origen de hello en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="b4804-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="b4804-191">Ejecuta un archivo war de Maven toobuild y, a continuación, usa la CLI de Azure toodeploy tooAzure servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b4804-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="b4804-192">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="b4804-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4804-193">Crear una máquina virtual de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="b4804-194">Configuración de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-194">Configure Jenkins</span></span>
> * <span data-ttu-id="b4804-195">Creación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="b4804-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="b4804-196">Preparación de un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="b4804-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="b4804-197">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="b4804-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="b4804-198">Ejecutar la canalización de Hola y compruebe la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="b4804-198">Run hello pipeline and verify hello web app</span></span>
