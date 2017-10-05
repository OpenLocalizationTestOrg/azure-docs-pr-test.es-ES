---
title: "Implementación en Azure App Service con el complemento de Jenkins | Microsoft Docs"
description: "Aprenda a usar el complemento de Jenkins de Azure App Service para implementar una aplicación web de Java para Azure en Jenkins"
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
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a><span data-ttu-id="bce3f-103">Implementación en Azure App Service con el complemento de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-103">Deploy to Azure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="bce3f-104">Para implementar una aplicación web de Java en Azure, puede utilizar la CLI de Azure en una [canalización de Jenkins](/azure/jenkins/execute-cli-jenkins-pipeline) o utilizar el [complemento de Jenkins de Azure App Service](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="bce3f-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="bce3f-105">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="bce3f-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bce3f-106">Configurar Jenkins para implementar en Azure App Service a través de FTP</span><span class="sxs-lookup"><span data-stu-id="bce3f-106">Configure Jenkins to deploy to Azure App Service through FTP</span></span> 
> * <span data-ttu-id="bce3f-107">Configurar Jenkins para implementar en Azure App Service en Linux con Docker</span><span class="sxs-lookup"><span data-stu-id="bce3f-107">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="bce3f-108">Creación y configuración de una instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="bce3f-109">Si aún no tiene un servidor maestro de Jenkins, comience con la [Solution Template](install-jenkins-solution-template.md) (Plantilla de la solución), que incluye JDK8 y los siguientes complementos necesarios:</span><span class="sxs-lookup"><span data-stu-id="bce3f-109">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and the following required plugins:</span></span>

* <span data-ttu-id="bce3f-110">[Complemento de cliente de Git de Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="bce3f-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="bce3f-111">[Complemento Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="bce3f-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="bce3f-112">[Credenciales de Azure](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="bce3f-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="bce3f-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="bce3f-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="bce3f-114">Puede usar el complemento de App Service para implementar aplicaciones web en todos los lenguajes (por ejemplo, C#, PHP, Java y node.js, etc.) admitidos por Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="bce3f-114">You can use the App Service plugin to deploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="bce3f-115">En este tutorial, estamos utilizando la aplicación de Java de ejemplo, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="bce3f-115">In this tutorial, we are using the sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="bce3f-116">Para bifurcar el repositorio en su propia cuenta de GitHub, haga clic en el botón **Fork** (Bifurcar) de la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="bce3f-116">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>  

<span data-ttu-id="bce3f-117">Son necesarios Java JDK y Maven para compilar el proyecto de Java.</span><span class="sxs-lookup"><span data-stu-id="bce3f-117">Java JDK and Maven are required for building the Java project.</span></span> <span data-ttu-id="bce3f-118">Asegúrese de instalar los componentes en el servidor maestro de Jenkins o en el agente de la máquina virtual si usa uno para la integración continua.</span><span class="sxs-lookup"><span data-stu-id="bce3f-118">Make sure you install the components in the Jenkins master or the VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="bce3f-119">Para la instalación, inicie sesión en la instancia de Jenkins con SSH y ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="bce3f-119">To install, log in to the Jenkins instance using SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="bce3f-120">Para la implementación en App Service en Linux, también debe instalar Docker en el servidor maestro de Jenkins o en el agente de la máquina virtual que se usa para la compilación.</span><span class="sxs-lookup"><span data-stu-id="bce3f-120">For deploying to App Service on Linux, you also need to install Docker on the Jenkins master or the VM agent used for build.</span></span> <span data-ttu-id="bce3f-121">Consulte este artículo para instalar Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="bce3f-121">Refer to this article to install Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="bce3f-122">Adición de un nombre de entidad de servicio de Azure a la credencial de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-122">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="bce3f-123">Se necesita una entidad de servicio de Azure para implementar en Azure.</span><span class="sxs-lookup"><span data-stu-id="bce3f-123">An Azure service principal is needed to deploy to Azure.</span></span> 

<ol>
<li><span data-ttu-id="bce3f-124">Use la [CLI de Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) o [Azure Portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) para crear una entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="bce3f-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) to create an Azure service principal</span></span></li>
<li><span data-ttu-id="bce3f-125">En el panel de Jenkins, haga clic en **Credenciales -> System ->**(Credenciales -> Sistema).</span><span class="sxs-lookup"><span data-stu-id="bce3f-125">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="bce3f-126">Haga clic en **Global credentials(unrestricted)**  [Credenciales (sin restricción) globales].</span><span class="sxs-lookup"><span data-stu-id="bce3f-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="bce3f-127">Haga clic en **Add Credentials** (Agregar credenciales) para agregar una entidad de servicio de Microsoft Azure rellenando los datos correspondientes a Subscription ID (Identificador de suscripción), Client ID (Identificador de cliente), Client Secret (Secreto de cliente) y OAuth 2.0 Token Endpoint (Punto de conexión de token OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="bce3f-127">Click **Add Credentials** to add a Microsoft Azure service principal by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="bce3f-128">Proporcione un identificador, **mySp**, para su uso en los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="bce3f-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="bce3f-129">Complemento de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bce3f-129">Azure App Service plugin</span></span>

<span data-ttu-id="bce3f-130">El complemento de Azure App Service v1.0 admite la implementación continua de una aplicación web en Azure a través de:</span><span class="sxs-lookup"><span data-stu-id="bce3f-130">Azure App Service plugin v1.0 supports continuous deployment to Azure Web App through:</span></span>

* <span data-ttu-id="bce3f-131">Git y FTP</span><span class="sxs-lookup"><span data-stu-id="bce3f-131">Git and FTP</span></span>
* <span data-ttu-id="bce3f-132">Docker para aplicaciones web en Linux</span><span class="sxs-lookup"><span data-stu-id="bce3f-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a><span data-ttu-id="bce3f-133">Configuración de Jenkins para implementar una aplicación web a través de FTP mediante el panel de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-133">Configure Jenkins to deploy Web App through FTP using the Jenkins dashboard</span></span>

<span data-ttu-id="bce3f-134">Para implementar el proyecto de aplicación web de Azure, puede cargar los artefactos de compilación (por ejemplo, el archivo .war en Java) usando Git o FTP.</span><span class="sxs-lookup"><span data-stu-id="bce3f-134">To deploy your project to Azure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="bce3f-135">Antes de configurar el trabajo en Jenkins, necesitará un plan de Azure App Service y una aplicación web para ejecutar la aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="bce3f-135">Before setting up the job in Jenkins, you need an Azure App Service plan and a Web App for running the Java app.</span></span>


1. <span data-ttu-id="bce3f-136">Cree un plan de Azure App Service con el plan de tarifa **GRATIS** mediante el comando [az appservice plan create](/cli/azure/appservice/plan#create) de la CLI.</span><span class="sxs-lookup"><span data-stu-id="bce3f-136">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="bce3f-137">Un plan de servicio de aplicaciones define los recursos físicos que se usan para hospedar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bce3f-137">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="bce3f-138">Todas las aplicaciones asignadas a un plan de servicio de aplicaciones comparten los recursos, lo que permite ahorrar costos al hospedar varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bce3f-138">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="bce3f-139">Creación de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bce3f-139">Create a Web App.</span></span> <span data-ttu-id="bce3f-140">Puede utilizar [Azure Portal](/azure/app-service-web/web-sites-configure) o bien el siguiente comando de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="bce3f-140">You can either use the [Azure portal](/azure/app-service-web/web-sites-configure) or use the following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="bce3f-141">Asegúrese de establecer la configuración en tiempo de ejecución de Java que necesita la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bce3f-141">Make sure you set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="bce3f-142">El siguiente comando de la CLI de Azure configura la aplicación web para que se ejecute en una versión reciente de Java 8 JDK y en [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="bce3f-142">The following Azure CLI command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="bce3f-143">Configuración del trabajo de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-143">Set up the Jenkins job</span></span>


1. <span data-ttu-id="bce3f-144">Creación de un nuevo proyecto **freestyle** (estilo libre) en el panel de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="bce3f-145">Configure **Source Code Management** (administración de código fuente) para usar la bifurcación local de [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) proporcionando la **dirección URL del repositorio**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-145">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="bce3f-146">Por ejemplo: http://github.com/&lt;su_ID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="bce3f-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="bce3f-147">Agregue un paso de compilación para compilar el proyecto con Maven.</span><span class="sxs-lookup"><span data-stu-id="bce3f-147">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="bce3f-148">Para ello, agregue un paso **Execute shell** (ejecutar shell).</span><span class="sxs-lookup"><span data-stu-id="bce3f-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="bce3f-149">En este ejemplo, es necesario un paso adicional para cambiar el nombre del archivo *.war en la carpeta de destino a ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="bce3f-149">For this example, we need an additional step to rename the *.war file in target folder to ROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="bce3f-150">Agregue una acción posterior a la compilación seleccionando **Publish an Azure Web App** (publicar una aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="bce3f-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="bce3f-151">Escriba "mySp", la entidad de servicio de Azure que se guardó en un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="bce3f-151">Supply, "mySp", the Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="bce3f-152">En la sección **App Configuration** (configuración de la aplicación), elija la aplicación web y el grupo de recursos de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="bce3f-152">In **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="bce3f-153">El complemento detecta automáticamente si la aplicación web está basada en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="bce3f-153">The plugin automatically detects whether the Web App is Windows or Linux-based.</span></span> <span data-ttu-id="bce3f-154">Para una aplicación web basada en Windows, se presenta la opción "Publish Files" (publicar archivos).</span><span class="sxs-lookup"><span data-stu-id="bce3f-154">For a Windows-based Web App, the option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="bce3f-155">Rellene los archivos que desea implementar (por ejemplo, un paquete war si usa Java.) Source Directory (directorio de origen) y Target Directory (directorio de destino) son opcionales.</span><span class="sxs-lookup"><span data-stu-id="bce3f-155">Fill in the files you want to deploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="bce3f-156">Los parámetros permiten especificar las carpetas de origen y destino al cargar archivos.</span><span class="sxs-lookup"><span data-stu-id="bce3f-156">The parameters allow you to specify source and target folders when uploading files.</span></span> <span data-ttu-id="bce3f-157">La aplicación web de Java en Azure se ejecuta en un servidor de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="bce3f-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="bce3f-158">Por lo tanto, cargue el paquete war a la carpeta webapps.</span><span class="sxs-lookup"><span data-stu-id="bce3f-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="bce3f-159">En este ejemplo, establezca **Source Directory** (directorio de origen) en "target" y **Target Directory** (directorio de destino) en "webapps".</span><span class="sxs-lookup"><span data-stu-id="bce3f-159">For this example, set **Source Directory** to "target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="bce3f-160">Si desea implementar en una ranura que no sea de producción, también puede establecer un nombre para **Slot** (ranura).</span><span class="sxs-lookup"><span data-stu-id="bce3f-160">If you want to deploy to a slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="bce3f-161">Guarde y compile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="bce3f-161">Save the project and build it.</span></span> <span data-ttu-id="bce3f-162">La aplicación web se implementa en Azure cuando finaliza la compilación.</span><span class="sxs-lookup"><span data-stu-id="bce3f-162">Your web app is deployed to Azure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="bce3f-163">Implementación de la aplicación web a través de FTP mediante la canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="bce3f-164">El complemento está preparado para la canalización.</span><span class="sxs-lookup"><span data-stu-id="bce3f-164">The plugin is pipeline-ready.</span></span> <span data-ttu-id="bce3f-165">Puede hacer referencia a un ejemplo en el repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="bce3f-165">You can refer to a sample in the GitHub repo.</span></span>

1. <span data-ttu-id="bce3f-166">En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="bce3f-167">Haga clic en el icono de lápiz para editar este archivo a fin de actualizar el grupo de recursos y el nombre de la aplicación web en las líneas 11 y 12, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bce3f-167">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="bce3f-168">Cambie la línea 14 para actualizar el identificador de la credencial en la instancia de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="bce3f-168">Change line 14 to update credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="bce3f-169">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="bce3f-170">Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento).</span><span class="sxs-lookup"><span data-stu-id="bce3f-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="bce3f-171">Proporcione un nombre para el trabajo y seleccione **Pipeline** (Canalización).</span><span class="sxs-lookup"><span data-stu-id="bce3f-171">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="bce3f-172">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-172">Click **OK**.</span></span>
3. <span data-ttu-id="bce3f-173">Haga clic en la pestaña **Pipeline** (Canalización) a continuación.</span><span class="sxs-lookup"><span data-stu-id="bce3f-173">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="bce3f-174">En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).</span><span class="sxs-lookup"><span data-stu-id="bce3f-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="bce3f-175">En **SCM**, seleccione **Git**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="bce3f-176">Escriba la dirección URL de GitHub para el repositorio bifurcado: https:&lt;su repositorio bifurcado>.git</span><span class="sxs-lookup"><span data-stu-id="bce3f-176">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="bce3f-177">Actualice **Script Path** (ruta de acceso del script) con el valor "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="bce3f-177">Update **Script Path** to "Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="bce3f-178">Haga clic en **Save** (guardar) y ejecute el trabajo.</span><span class="sxs-lookup"><span data-stu-id="bce3f-178">Click **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a><span data-ttu-id="bce3f-179">Configuración de Jenkins para implementar una aplicación web en Linux con Docker</span><span class="sxs-lookup"><span data-stu-id="bce3f-179">Configure Jenkins to deploy Web App on Linux through Docker</span></span>

<span data-ttu-id="bce3f-180">Además de con Git y FTP, la aplicación web en Linux admite la implementación con Docker.</span><span class="sxs-lookup"><span data-stu-id="bce3f-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="bce3f-181">Para la implementación con Docker, debe proporcionar un archivo de Docker que empaquete la aplicación web con el servicio en tiempo de ejecución en una imagen de Docker.</span><span class="sxs-lookup"><span data-stu-id="bce3f-181">To deploy using Docker, you need to provide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="bce3f-182">Después, el complemento compila la imagen, la inserta en un registro de Docker y la implementa en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bce3f-182">Then the plugin builds the image, pushes it to a docker registry and deploys the image to your web app.</span></span>

<span data-ttu-id="bce3f-183">La aplicación web en Linux también admite los métodos tradicionales como Git y FTP, pero solo para los lenguajes integrados (.NET Core, Node.js, PHP y Ruby).</span><span class="sxs-lookup"><span data-stu-id="bce3f-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="bce3f-184">Para otros lenguajes, debe empaquetar el código de la aplicación y el servicio en tiempo de ejecución juntos en una imagen de Docker y utilizar Docker para la implementación.</span><span class="sxs-lookup"><span data-stu-id="bce3f-184">For other languages, you need to package your application code and service runtime together into a docker image and use docker to deploy.</span></span>

<span data-ttu-id="bce3f-185">Antes de configurar el trabajo en Jenkins, necesita una instancia de Azure App Service en Linux.</span><span class="sxs-lookup"><span data-stu-id="bce3f-185">Before setting up the job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="bce3f-186">También es necesario un registro de contenedor para almacenar y administrar las imágenes del contenedor de Docker privado.</span><span class="sxs-lookup"><span data-stu-id="bce3f-186">A container registry is also needed to store and manage your private Docker container images.</span></span> <span data-ttu-id="bce3f-187">Puede usar DockerHub; en este ejemplo, usamos Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="bce3f-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="bce3f-188">Siga los pasos descritos [aquí](/azure/app-service-web/app-service-linux-how-to-create-web-app) para crear una aplicación web en Linux</span><span class="sxs-lookup"><span data-stu-id="bce3f-188">You can follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create a Web App on Linux</span></span> 
* <span data-ttu-id="bce3f-189">Azure Container Registry es un servicio administrado de [Docker registry] (https://docs.docker.com/registry/) basado en Docker Registry 2.0 de código abierto.</span><span class="sxs-lookup"><span data-stu-id="bce3f-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="bce3f-190">Siga los pasos descritos [aquí] (/ azure/container-registry/container-registry-get-started-azure-cli) para obtener instrucciones sobre cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="bce3f-190">Follow the steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how to do so.</span></span> <span data-ttu-id="bce3f-191">También puede usar DockerHub.</span><span class="sxs-lookup"><span data-stu-id="bce3f-191">You can also use DockerHub.</span></span>

### <a name="to-deploy-using-docker"></a><span data-ttu-id="bce3f-192">Para implementar con Docker:</span><span class="sxs-lookup"><span data-stu-id="bce3f-192">To deploy using docker:</span></span>

1. <span data-ttu-id="bce3f-193">Cree un nuevo proyecto freestyle (estilo libre) en el panel de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="bce3f-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="bce3f-194">Configure **Source Code Management** (administración de código fuente) para usar la bifurcación local de [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) proporcionando la **dirección URL del repositorio**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-194">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="bce3f-195">Por ejemplo: http://github.com/&lt;su_ID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="bce3f-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="bce3f-196">Agregue un paso de compilación para compilar el proyecto con Maven.</span><span class="sxs-lookup"><span data-stu-id="bce3f-196">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="bce3f-197">Para hacerlo, agregue un paso **Execute shell** (ejecutar shell) y agregue la siguiente línea en **Command** (comando):</span><span class="sxs-lookup"><span data-stu-id="bce3f-197">Do so by adding an **Execute shell** and add the following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="bce3f-198">Agregue una acción posterior a la compilación seleccionando **Publish an Azure Web App** (publicar una aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="bce3f-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="bce3f-199">Escriba **mySp**, la entidad de servicio de Azure que guardó en un paso anterior como credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="bce3f-199">Supply, **mySp**, the Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="bce3f-200">En la sección **App Configuration** (configuración de la aplicación), elija la aplicación web en Linux y el grupo de recursos de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="bce3f-200">In **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="bce3f-201">Elija Publish via Docker (publicar a través de Docker).</span><span class="sxs-lookup"><span data-stu-id="bce3f-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="bce3f-202">Rellene la ruta de acceso de **Dockerfile** (archivo de Docker).</span><span class="sxs-lookup"><span data-stu-id="bce3f-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="bce3f-203">Puede mantener el valor predeterminado "/Dockerfile" En **Docker registry URL** (Dirección URL del registro de Docker), utilice el formato https://&lt;myRegistry>.azurecr.io si usa Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="bce3f-203">You can keep the default "/Dockerfile" For **Docker registry URL**, supply in the format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="bce3f-204">Déjelo en blanco si utiliza DockerHub.</span><span class="sxs-lookup"><span data-stu-id="bce3f-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="bce3f-205">En **Registry credentials** (credenciales del registro), agregue las credenciales de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="bce3f-205">For **Registry credentials**, add the credential for the Azure Container Registry.</span></span> <span data-ttu-id="bce3f-206">Puede obtener el identificador de usuario y la contraseña mediante la ejecución de los siguientes comandos de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="bce3f-206">You can get the userid and password by running the following commands in Azure CLI.</span></span> <span data-ttu-id="bce3f-207">El primer comando habilita la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="bce3f-207">The first command enables the administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="bce3f-208">El nombre de la imagen de Docker y la etiqueta en la pestaña **Advanced** (Avanzado) son opcionales.</span><span class="sxs-lookup"><span data-stu-id="bce3f-208">The docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="bce3f-209">De forma predeterminada, el nombre de la imagen se obtiene del nombre de imagen que configuró en Azure Portal (en la configuración del contenedor de Docker.) La etiqueta se genera a partir de $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="bce3f-209">By default, image name is obtained from the image name you configured in Azure portal (in Docker Container setting.) The tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="bce3f-210">Asegúrese de especificar el nombre de la imagen en Azure Portal o bien proporcione un valor para **Docker Image** (imagen de Docker) en la pestaña **Advanced** (Avanzado). En este ejemplo, escriba "&lt;su_registro>.azurecr.io/calculator" para **Docker image** (imagen de Docker) y deje **Docker Image Tag** (etiqueta de imagen de Docker) en blanco.</span><span class="sxs-lookup"><span data-stu-id="bce3f-210">Make sure you specify the image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="bce3f-211">Se produce un error en la implementación si utiliza la configuración de imagen de Docker integrada.</span><span class="sxs-lookup"><span data-stu-id="bce3f-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="bce3f-212">Asegúrese de que cambia la configuración de Docker para usar la imagen personalizada en la Configuración del contenedor de Docker en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="bce3f-212">Make sure you change docker config to use custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="bce3f-213">Para la imagen integrada, utilice el enfoque de carga de archivos para la implementación.</span><span class="sxs-lookup"><span data-stu-id="bce3f-213">For built-in image, use file upload approach to deploy.</span></span>
11. <span data-ttu-id="bce3f-214">De forma similar al enfoque de carga de archivos, puede elegir una ranura diferente que no sea de producción.</span><span class="sxs-lookup"><span data-stu-id="bce3f-214">Similar to file upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="bce3f-215">Guarde y compile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="bce3f-215">Save and build the project.</span></span> <span data-ttu-id="bce3f-216">Verá que la imagen del contenedor se inserta en el registro y se implementa la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bce3f-216">You see your container image is pushed to your registry and web app is deployed.</span></span>

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="bce3f-217">Implementación de la aplicación web en Linux a través de Docker mediante la canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-217">Deploy to Web App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="bce3f-218">En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="bce3f-219">Haga clic en el icono de lápiz para editar este archivo a fin de actualizar el grupo de recursos y el nombre de la aplicación web en las líneas 11 y 12, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bce3f-219">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="bce3f-220">Cambie en la línea 13 su servidor de registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="bce3f-220">Change line 13 to your container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="bce3f-221">Cambie la línea 16 para actualizar el identificador de la credencial en la instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-221">Change line 16 to update credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="bce3f-222">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="bce3f-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="bce3f-223">Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento).</span><span class="sxs-lookup"><span data-stu-id="bce3f-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="bce3f-224">Proporcione un nombre para el trabajo y seleccione **Pipeline** (Canalización).</span><span class="sxs-lookup"><span data-stu-id="bce3f-224">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="bce3f-225">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-225">Click **OK**.</span></span>
3. <span data-ttu-id="bce3f-226">Haga clic en la pestaña **Pipeline** (Canalización) a continuación.</span><span class="sxs-lookup"><span data-stu-id="bce3f-226">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="bce3f-227">En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).</span><span class="sxs-lookup"><span data-stu-id="bce3f-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="bce3f-228">En **SCM**, seleccione **Git**.</span><span class="sxs-lookup"><span data-stu-id="bce3f-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="bce3f-229">Escriba la dirección URL de GitHub para el repositorio bifurcado: https:&lt;su repositorio bifurcado>.git</span><span class="sxs-lookup"><span data-stu-id="bce3f-229">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="bce3f-230">7, Actualice **Script Path** (ruta de acceso del script) con el valor "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="bce3f-230">7, Update **Script Path** to "Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="bce3f-231">Haga clic en **Save** (guardar) y ejecute el trabajo.</span><span class="sxs-lookup"><span data-stu-id="bce3f-231">Click **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="bce3f-232">Comprobación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="bce3f-232">Verify your web app</span></span>

1. <span data-ttu-id="bce3f-233">Para comprobar que el archivo WAR se ha implementado correctamente en la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="bce3f-233">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="bce3f-234">Abra un explorador web.</span><span class="sxs-lookup"><span data-stu-id="bce3f-234">Open a web browser.</span></span>
2. <span data-ttu-id="bce3f-235">Cuando vaya a la dirección http://&lt;nombre_aplicación>.azurewebsites.net/api/calculator/ping podrá ver:</span><span class="sxs-lookup"><span data-stu-id="bce3f-235">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="bce3f-236">Welcome to Java Web App!!! (Bienvenido a la aplicación web de Java)</span><span class="sxs-lookup"><span data-stu-id="bce3f-236">Welcome to Java Web App!!!</span></span> <span data-ttu-id="bce3f-237">Se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="bce3f-237">This is updated!</span></span>
   <span data-ttu-id="bce3f-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="bce3f-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="bce3f-239">Vaya a http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (sustituya &lt;x> e &lt;y> con cualquier número) para obtener la suma de x e y</span><span class="sxs-lookup"><span data-stu-id="bce3f-239">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>        
    ![Calculadora: suma](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="bce3f-241">Para App Service en Linux</span><span class="sxs-lookup"><span data-stu-id="bce3f-241">For App service on Linux</span></span>

* <span data-ttu-id="bce3f-242">Para comprobarlo, en la CLI de Azure, ejecute:</span><span class="sxs-lookup"><span data-stu-id="bce3f-242">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="bce3f-243">Obtiene el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="bce3f-243">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="bce3f-244">Vaya a http://&lt;nombre_aplicación>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="bce3f-244">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="bce3f-245">Verá el mensaje:</span><span class="sxs-lookup"><span data-stu-id="bce3f-245">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="bce3f-246">Vaya a http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (sustituya &lt;x> e &lt;y> con cualquier número) para obtener la suma de x e y</span><span class="sxs-lookup"><span data-stu-id="bce3f-246">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="bce3f-247">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bce3f-247">Next steps</span></span>

<span data-ttu-id="bce3f-248">En este tutorial se utiliza el complemento de Azure App Service para implementar en Azure.</span><span class="sxs-lookup"><span data-stu-id="bce3f-248">In this tutorial, you use the Azure App Service plugin to deploy to Azure.</span></span>

<span data-ttu-id="bce3f-249">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="bce3f-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bce3f-250">Configurar Jenkins para implementar en Azure App Service a través de FTP</span><span class="sxs-lookup"><span data-stu-id="bce3f-250">Configure Jenkins to deploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="bce3f-251">Configurar Jenkins para implementar en Azure App Service en Linux con Docker</span><span class="sxs-lookup"><span data-stu-id="bce3f-251">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 