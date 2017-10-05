---
title: Ejecute la CLI de Azure con Jenkins | Documentos de Microsoft
description: "Aprenda a usar la CLI de Azure para implementar una aplicación web de Java para Azure en Jenkins Pipeline"
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
ms.openlocfilehash: 5ca8338d4bf343f08fe70081cff755fa76a126a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-and-the-azure-cli"></a><span data-ttu-id="ebc1a-103">Implementación en Azure App Service con Jenkins y la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ebc1a-103">Deploy to Azure App Service with Jenkins and the Azure CLI</span></span>
<span data-ttu-id="ebc1a-104">Para implementar una aplicación web de Java en Azure, puede utilizar la CLI de Azure en [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="ebc1a-105">En este tutorial, creará una canalización de CI/CD en una máquina virtual de Azure, y aprenderá los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ebc1a-106">Crear una máquina virtual de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="ebc1a-107">Configuración de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-107">Configure Jenkins</span></span>
> * <span data-ttu-id="ebc1a-108">Creación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="ebc1a-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="ebc1a-109">Preparación de un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="ebc1a-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="ebc1a-110">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="ebc1a-111">Ejecución de la canalización y comprobación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="ebc1a-111">Run the pipeline and verify the web app</span></span>

<span data-ttu-id="ebc1a-112">Para realizar este tutorial es necesaria la versión 2.0.4 o superior de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ebc1a-113">Para encontrar la versión, ejecute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-113">To find the version, run `az --version`.</span></span> <span data-ttu-id="ebc1a-114">Si necesita actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="ebc1a-115">Creación y configuración de una instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="ebc1a-116">Si aún no tiene un servidor maestro de Jenkins, comience con la [Solution Template](install-jenkins-solution-template.md) (Plantilla de la solución), que incluye el complemento [Azure Credentials](https://plugins.jenkins.io/azure-credentials) (Credenciales de Azure) necesario de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-116">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="ebc1a-117">El complemento Azure Credential permite almacenar las credenciales de la entidad de servicio de Microsoft Azure en Jenkins.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-117">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="ebc1a-118">En la versión 1.2, hemos agregado la compatibilidad para que Jenkins Pipeline pueda obtener las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-118">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span></span> 

<span data-ttu-id="ebc1a-119">Compruebe que dispone de la versión 1.2 o posterior:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="ebc1a-120">En el panel de Jenkins, haga clic en **Manage Jenkins -> Plugin Manager ->** (Administrar Jenkins -> Administrador de complementos) y busque **Azure Credential** (Credencial de Azure).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-120">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="ebc1a-121">Actualice el complemento si la versión es anterior a la 1.2.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-121">Update the plugin if the version is earlier than 1.2.</span></span>

<span data-ttu-id="ebc1a-122">Java JDK y Maven también son necesarios en el servidor maestro Jenkins.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-122">Java JDK and Maven are also required in the Jenkins master.</span></span> <span data-ttu-id="ebc1a-123">Para la instalación, inicie sesión en el servidor maestro de Jenkins con SSH y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-123">To install, log in to Jenkins master using SSH and run the following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="ebc1a-124">Adición de un nombre de entidad de servicio de Azure a la credencial de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-124">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="ebc1a-125">Para ejecutar la CLI de Azure se necesita una credencial de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-125">An Azure credential is needed to execute Azure CLI.</span></span>

* <span data-ttu-id="ebc1a-126">En el panel de Jenkins, haga clic en **Credenciales -> System ->**(Credenciales -> Sistema).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-126">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="ebc1a-127">Haga clic en **Global credentials(unrestricted)**  [Credenciales (sin restricción) globales].</span><span class="sxs-lookup"><span data-stu-id="ebc1a-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="ebc1a-128">Haga clic en **Add Credentials** (Agregar credenciales) para agregar una nueva [entidad de servicio de Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) rellenando los datos correspondientes a Subscription ID (Identificador de suscripción), Client ID (Identificador de cliente), Client Secret (Secreto de cliente) y OAuth 2.0 Token Endpoint (Punto de conexión de token OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-128">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="ebc1a-129">Proporcione un identificador para usarlo en el paso posterior.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-129">Provide an ID for use in subsequent step.</span></span>

![Adición de credenciales](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-the-java-web-app"></a><span data-ttu-id="ebc1a-131">Creación de una instancia de Azure App Service para implementar la aplicación web de Java</span><span class="sxs-lookup"><span data-stu-id="ebc1a-131">Create an Azure App Service for deploying the Java web app</span></span>

<span data-ttu-id="ebc1a-132">Cree un plan de Azure App Service con el plan de tarifa **GRATIS** mediante el comando [az appservice plan create](/cli/azure/appservice/plan#create) de la CLI.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-132">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="ebc1a-133">Un plan de servicio de aplicaciones define los recursos físicos que se usan para hospedar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-133">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="ebc1a-134">Todas las aplicaciones asignadas a un plan de servicio de aplicaciones comparten los recursos, lo que permite ahorrar costos al hospedar varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-134">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="ebc1a-135">Una vez preparado el plan, la CLI de Azure muestra un resultado similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-135">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="ebc1a-136">Creación de una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="ebc1a-136">Create an Azure Web app</span></span>

 <span data-ttu-id="ebc1a-137">Use el comando de la CLI [az webapp create ](/cli/azure/appservice/web#create) para crear una definición de aplicación web en el plan de App Service `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-137">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="ebc1a-138">La definición de la aplicación web proporciona una dirección URL para acceder a la aplicación y configura varias opciones para implementar el código en Azure.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-138">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="ebc1a-139">Sustituya el marcador de posición `<app_name>` por su propio nombre de aplicación único.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-139">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="ebc1a-140">Este nombre único forma parte del nombre de dominio predeterminado para la aplicación web, por lo que debe ser único en todas las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-140">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="ebc1a-141">Puede asignar una entrada de nombre de dominio personalizada a la aplicación web antes de exponerla a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-141">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="ebc1a-142">Cuando está preparada la definición de la aplicación web, la CLI de Azure muestra información similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-142">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="ebc1a-143">Configuración de Java</span><span class="sxs-lookup"><span data-stu-id="ebc1a-143">Configure Java</span></span> 

<span data-ttu-id="ebc1a-144">Establezca la configuración del sistema en tiempo de ejecución de Java que necesita la aplicación con el comando [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-144">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="ebc1a-145">El siguiente comando configura la aplicación web para que se ejecute en una versión reciente de Java 8 JDK y en [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-145">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="ebc1a-146">Preparación de un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="ebc1a-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="ebc1a-147">Abra el repositorio de [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) (Aplicación web de Simple Java para Azure).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-147">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="ebc1a-148">Para bifurcar el repositorio en su propia cuenta de GitHub, haga clic en el botón **Fork** (Bifurcar) de la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-148">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

* <span data-ttu-id="ebc1a-149">En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="ebc1a-150">Haga clic en el icono de lápiz para editar este archivo a fin de actualizar el grupo de recursos y el nombre de la aplicación web en las líneas 20 y 21, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-150">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="ebc1a-151">Cambie la línea 23 para actualizar el identificador de la credencial en la instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-151">Change line 23 to update credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="ebc1a-152">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="ebc1a-153">Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="ebc1a-154">Proporcione un nombre para el trabajo y seleccione **Pipeline** (Canalización).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-154">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="ebc1a-155">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-155">Click **OK**.</span></span>
* <span data-ttu-id="ebc1a-156">Haga clic en la pestaña **Pipeline** (Canalización) a continuación.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-156">Click the **Pipeline** tab next.</span></span> 
* <span data-ttu-id="ebc1a-157">En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="ebc1a-158">En **SCM**, seleccione **Git**.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="ebc1a-159">Escriba la dirección URL de GitHub para el repositorio bifurcado: https:\<su repositorio bifurcado\>.git</span><span class="sxs-lookup"><span data-stu-id="ebc1a-159">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="ebc1a-160">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="ebc1a-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="ebc1a-161">Prueba de la canalización</span><span class="sxs-lookup"><span data-stu-id="ebc1a-161">Test your pipeline</span></span>
* <span data-ttu-id="ebc1a-162">Vaya a la canalización que creó, haga clic en **Build Now** (Compilar ahora).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-162">Go to the pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="ebc1a-163">En algunos segundos, debería crearse correctamente una compilación y puede ir a ella y hacer clic en **Console Output** (Salida de la consola) para ver los detalles</span><span class="sxs-lookup"><span data-stu-id="ebc1a-163">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="ebc1a-164">Comprobación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="ebc1a-164">Verify your web app</span></span>
<span data-ttu-id="ebc1a-165">Para comprobar que el archivo WAR se ha implementado correctamente en la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-165">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="ebc1a-166">Abra un explorador web.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-166">Open a web browser:</span></span>

* <span data-ttu-id="ebc1a-167">Vaya a http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="ebc1a-167">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="ebc1a-168">Se ve lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-168">You see:</span></span>

        Welcome to Java Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="ebc1a-169">Vaya a http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (sustituya &lt;x> e &lt;y> con cualquier número) para obtener la suma de x e y</span><span class="sxs-lookup"><span data-stu-id="ebc1a-169">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>

![Calculadora: suma](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-to-azure-web-app-on-linux"></a><span data-ttu-id="ebc1a-171">Implementar en una aplicación web de Azure en Linux</span><span class="sxs-lookup"><span data-stu-id="ebc1a-171">Deploy to Azure Web App on Linux</span></span>
<span data-ttu-id="ebc1a-172">Ahora que sabe cómo se usa la CLI de Azure en la canalización de Jenkins, puede modificar el script para implementar en una aplicación web de Azure en Linux.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-172">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span></span>

<span data-ttu-id="ebc1a-173">La aplicación web en Linux es compatible con otra forma de realizar la implementación, que consiste en usar Docker.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-173">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span></span> <span data-ttu-id="ebc1a-174">Para la implementación, debe proporcionar un archivo de Docker que empaquete la aplicación web con el tiempo de ejecución de servicio en una imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-174">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="ebc1a-175">Después, el complemento compilará la imagen, la insertará en un registro de Docker y la implementará en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-175">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span></span>

* <span data-ttu-id="ebc1a-176">Siga los pasos descritos [aquí](/azure/app-service-web/app-service-linux-how-to-create-web-app) para crear una aplicación web de Azure que se ejecute en Linux.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-176">Follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="ebc1a-177">Instale Docker en la instancia de Jenkins siguiendo las instrucciones de este [artículo](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-177">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="ebc1a-178">Cree un registro de contenedor mediante Azure Portal siguiendo los pasos descritos [aquí](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ebc1a-178">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="ebc1a-179">En el mismo repositorio [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) (Aplicación web de Java simple para Azure), edite el archivo **Jenkinsfile2**:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-179">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="ebc1a-180">En las líneas 18-21, actualice los nombres del grupo de recursos, la aplicación web y el ACR respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-180">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="ebc1a-181">En la línea 24, actualice \<azsrvprincipal\> al identificador de la credencial.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-181">Line 24, update \<azsrvprincipal\> to your credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="ebc1a-182">Cree una nueva canalización Jenkins como hizo cuando implementó en la aplicación web de Azure en Windows, pero esta vez use **Jenkinsfile2** en su lugar.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-182">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="ebc1a-183">Ejecute el nuevo trabajo.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-183">Run your new job.</span></span>
* <span data-ttu-id="ebc1a-184">Para comprobarlo, en la CLI de Azure, ejecute:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-184">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="ebc1a-185">Obtiene el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-185">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="ebc1a-186">Vaya a http://&lt;nombre_aplicación>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-186">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="ebc1a-187">Verá el mensaje:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-187">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="ebc1a-188">Vaya a http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (sustituya &lt;x> e &lt;y> con cualquier número) para obtener la suma de x e y</span><span class="sxs-lookup"><span data-stu-id="ebc1a-188">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="ebc1a-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebc1a-189">Next steps</span></span>
<span data-ttu-id="ebc1a-190">En este tutorial, ha configurado una canalización de Jenkins que extrae del repositorio GitHub el código fuente.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-190">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span></span> <span data-ttu-id="ebc1a-191">Se ejecuta Maven para generar un archivo war y, a continuación, se utiliza la CLI de Azure para implementarlo en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ebc1a-191">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span></span> <span data-ttu-id="ebc1a-192">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="ebc1a-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ebc1a-193">Crear una máquina virtual de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="ebc1a-194">Configuración de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-194">Configure Jenkins</span></span>
> * <span data-ttu-id="ebc1a-195">Creación de una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="ebc1a-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="ebc1a-196">Preparación de un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="ebc1a-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="ebc1a-197">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="ebc1a-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="ebc1a-198">Ejecución de la canalización y comprobación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="ebc1a-198">Run the pipeline and verify the web app</span></span>
