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
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="3e7c1-103">Implementar tooAzure servicio de aplicaciones con Jenkins complemento</span><span class="sxs-lookup"><span data-stu-id="3e7c1-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="3e7c1-104">toodeploy una tooAzure de aplicación web de Java, puede utilizar la CLI de Azure en [Jenkins canalización](/azure/jenkins/execute-cli-jenkins-pipeline) o hacer que el uso de hello [Jenkins de servicio de aplicación de Azure complemento](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="3e7c1-105">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3e7c1-106">Configurar Jenkins toodeploy tooAzure servicio de aplicaciones a través de FTP</span><span class="sxs-lookup"><span data-stu-id="3e7c1-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="3e7c1-107">Configurar Jenkins toodeploy tooAzure servicio de aplicaciones en Linux a través de Docker</span><span class="sxs-lookup"><span data-stu-id="3e7c1-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="3e7c1-108">Creación y configuración de una instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e7c1-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="3e7c1-109">Si no tiene todavía un patrón Jenkins, comience con hello [plantilla de solución](install-jenkins-solution-template.md), que incluye hello siguiendo los complementos necesarios y JDK8:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="3e7c1-110">[Complemento de cliente de Git de Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="3e7c1-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="3e7c1-111">[Complemento Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="3e7c1-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="3e7c1-112">[Credenciales de Azure](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="3e7c1-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="3e7c1-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="3e7c1-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="3e7c1-114">Puede usar hello toodeploy de complemento de servicio de aplicaciones Web App en todos los idiomas (por ejemplo, C#, PHP, Java y node.js, etc.) admitidos por el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="3e7c1-115">En este tutorial, estamos utilizando aplicaciones de Java de ejemplo de Hola, [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="3e7c1-116">toofork Hola repositorio tooyour posee la cuenta de GitHub, haga clic en hello **bifurcar** botón en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="3e7c1-117">Java JDK y Maven son necesarios para compilar el proyecto de Java de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="3e7c1-118">Asegúrese de que instalar componentes de hello en master de hello Jenkins o agente de máquina virtual de hello si usa un para la integración continua.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="3e7c1-119">tooinstall, inicie sesión en toohello Jenkins instancia mediante SSH y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="3e7c1-120">Para implementar tooApp servicio en Linux, también deberá tooinstall Docker en patrón de Jenkins Hola o el agente de máquina virtual de hello utilizado para la compilación.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="3e7c1-121">Consulte el artículo de toothis tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="3e7c1-122">Agregar credencial tooJenkins principal de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="3e7c1-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="3e7c1-123">Una entidad de seguridad de servicio de Azure es necesario toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="3e7c1-124">Use [CLI de Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) o [portal de Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate una entidad de seguridad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="3e7c1-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="3e7c1-125">En el panel de Jenkins hello, haga clic en **credenciales -> sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="3e7c1-126">Haga clic en **Global credentials(unrestricted) ** [Credenciales (sin restricción) globales].</span><span class="sxs-lookup"><span data-stu-id="3e7c1-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="3e7c1-127">Haga clic en **agregar credenciales** tooadd una entidad de servicio de Microsoft Azure rellenando Hola Id. de suscripción, Id. de cliente, el secreto de cliente y extremo de Token de OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="3e7c1-128">Proporcione un identificador, **mySp**, para su uso en los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="3e7c1-129">Complemento de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3e7c1-129">Azure App Service plugin</span></span>

<span data-ttu-id="3e7c1-130">Azure v1.0 de complemento de servicio de aplicaciones admite la implementación continua tooAzure aplicación Web a través de:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="3e7c1-131">Git y FTP</span><span class="sxs-lookup"><span data-stu-id="3e7c1-131">Git and FTP</span></span>
* <span data-ttu-id="3e7c1-132">Docker para aplicaciones web en Linux</span><span class="sxs-lookup"><span data-stu-id="3e7c1-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="3e7c1-133">Configurar Jenkins toodeploy aplicación Web a través de FTP con hello Jenkins panel</span><span class="sxs-lookup"><span data-stu-id="3e7c1-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="3e7c1-134">toodeploy su tooAzure de project Web App, puede cargar los artefactos de compilación (por ejemplo, el archivo .war en Java) usando Git o FTP.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="3e7c1-135">Antes de configurar el trabajo de hello en Jenkins, necesita un plan de servicio de aplicaciones de Azure y una aplicación Web para la aplicación en ejecución Hola Java.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="3e7c1-136">Crear un plan de servicio de aplicaciones de Azure con hello **libre** tarifa con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="3e7c1-137">plan de servicio de aplicaciones de Hello define Hola recursos físicos que usa toohost sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="3e7c1-138">Todas las aplicaciones asignadas plan de servicio de aplicaciones de tooan compartan estos recursos, permitiéndole toosave costo al hospedar varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="3e7c1-139">Creación de una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-139">Create a Web App.</span></span> <span data-ttu-id="3e7c1-140">Puede cualquier Hola uso [portal de Azure](/azure/app-service-web/web-sites-configure) o use Hola siguiente comando de CLI Az:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="3e7c1-141">Asegúrese de que establecer la configuración de tiempo de ejecución de Java de Hola que necesita la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="3e7c1-142">Hola siguiente comando de CLI de Azure configura toorun de aplicación web de hello en una versión reciente de Java 8 JDK y [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="3e7c1-143">Configurar el trabajo de hello Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e7c1-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="3e7c1-144">Creación de un nuevo proyecto **freestyle** (estilo libre) en el panel de Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e7c1-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="3e7c1-145">Configurar **administración de código fuente** toouse la bifurcación local de [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample) proporcionando hello **dirección URL de repositorio**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="3e7c1-146">Por ejemplo: http://github.com/&lt;su_ID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="3e7c1-147">Agregar un proyecto de hello toobuild de paso de compilación mediante Maven.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="3e7c1-148">Para ello, agregue un paso **Execute shell** (ejecutar shell).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="3e7c1-149">En este ejemplo, se necesita un archivo de *.war paso adicional toorename hello en tooROOT.war de la carpeta de destino.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="3e7c1-150">Agregue una acción posterior a la compilación seleccionando **Publish an Azure Web App** (publicar una aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="3e7c1-151">Fuente de alimentación, "mySp", entidad de seguridad de servicio de Azure de hello almacenados en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="3e7c1-152">En **configuración de la aplicación** sección, elija la aplicación de web y el grupo de recursos de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="3e7c1-153">complemento de Hello detecta automáticamente si Hola aplicación Web es Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="3e7c1-154">Para una aplicación Web basada en Windows, se presenta la opción de Hola "Publicar archivos".</span><span class="sxs-lookup"><span data-stu-id="3e7c1-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="3e7c1-155">Rellenar en archivos de hello desea toodeploy (por ejemplo, un war paquete si utiliza Java.) Source Directory (directorio de origen) y Target Directory (directorio de destino) son opcionales.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="3e7c1-156">parámetros de Hello permiten toospecify carpetas de origen y de destino al cargar archivos.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="3e7c1-157">La aplicación web de Java en Azure se ejecuta en un servidor de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="3e7c1-158">Por lo tanto, cargue el paquete war a la carpeta webapps.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="3e7c1-159">En este ejemplo, establezca **el directorio de origen** demasiado "destino" y proporcionan "móviles" de **directorio de destino**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="3e7c1-160">Si desea toodeploy tooa ranura que no sea de producción, también puede establecer **ranura** nombre.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="3e7c1-161">Guarde el proyecto de Hola y genérelo.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-161">Save hello project and build it.</span></span> <span data-ttu-id="3e7c1-162">La aplicación web está implementada tooAzure cuando se completa la compilación.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="3e7c1-163">Implementación de la aplicación web a través de FTP mediante la canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e7c1-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="3e7c1-164">complemento de Hello está preparada para la canalización.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="3e7c1-165">Puede hacer referencia en el ejemplo tooa en el repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="3e7c1-166">En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="3e7c1-167">Haga clic en tooedit de icono de lápiz Hola este grupo de recursos de archivo tooupdate Hola y el nombre de la aplicación web en línea 11 y 12 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="3e7c1-168">Cambie la línea 14 tooupdate el identificador de la credencial en la instancia de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="3e7c1-169">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e7c1-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="3e7c1-170">Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="3e7c1-171">Proporcione un nombre para el trabajo de Hola y seleccione **canalización**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="3e7c1-172">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-172">Click **OK**.</span></span>
3. <span data-ttu-id="3e7c1-173">Haga clic en hello **canalización** pestaña a continuación.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="3e7c1-174">En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="3e7c1-175">En **SCM**, seleccione **Git**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="3e7c1-176">Escriba hello GitHub URL para el repositorio bifurcada: https:&lt;repositorio bifurcada > .git</span><span class="sxs-lookup"><span data-stu-id="3e7c1-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="3e7c1-177">Actualización **ruta del Script** demasiado "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="3e7c1-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="3e7c1-178">Haga clic en **guardar** y trabajo de ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="3e7c1-179">Configurar Jenkins toodeploy aplicación Web en Linux a través de Docker</span><span class="sxs-lookup"><span data-stu-id="3e7c1-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="3e7c1-180">Además de con Git y FTP, la aplicación web en Linux admite la implementación con Docker.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="3e7c1-181">toodeploy con Docker, deberá tooprovide un Dockerfile que empaqueta la aplicación web con el runtime del servicio en una imagen de docker.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="3e7c1-182">A continuación, Hola complemento genera imágenes de hello, inserta del registro de docker de tooa e implementa Hola imagen tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="3e7c1-183">La aplicación web en Linux también admite los métodos tradicionales como Git y FTP, pero solo para los lenguajes integrados (.NET Core, Node.js, PHP y Ruby).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="3e7c1-184">Para otros idiomas, es necesario toopackage el tiempo de ejecución de código y el servicio de aplicación juntos en una imagen de docker y usar toodeploy de docker.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="3e7c1-185">Antes de configurar el trabajo de hello en Jenkins, necesita un servicio de aplicación de Azure en Linux.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="3e7c1-186">Un registro de contenedor también es necesario toostore y administrar las imágenes de contenedor de Docker privadas.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="3e7c1-187">Puede usar DockerHub; en este ejemplo, usamos Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="3e7c1-188">Puede seguir los pasos de hello [aquí](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate una aplicación Web en Linux</span><span class="sxs-lookup"><span data-stu-id="3e7c1-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="3e7c1-189">Registro de contenedor de Azure es un administrado [Docker registro] servicio (https://docs.docker.com/registry/) basado en Hola 2.0 de registro de Docker de código abierto.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="3e7c1-190">Siga los pasos de hello [aquí] (/ azure/container-registry/container-registry-get-started-azure-cli) para obtener instrucciones sobre cómo toodo para.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="3e7c1-191">También puede usar DockerHub.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="3e7c1-192">toodeploy con docker:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="3e7c1-193">Cree un nuevo proyecto freestyle (estilo libre) en el panel de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="3e7c1-194">Configurar **administración de código fuente** toouse la bifurcación local de [Simple aplicación Web de Java de Azure](https://github.com/azure-devops/javawebappsample) proporcionando hello **dirección URL de repositorio**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="3e7c1-195">Por ejemplo: http://github.com/&lt;su_ID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="3e7c1-196">Agregar un proyecto de hello toobuild de paso de compilación mediante Maven.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="3e7c1-197">Hacerlo agregando una **ejecutar shell** y agregue Hola después de línea en **comando**:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="3e7c1-198">Agregue una acción posterior a la compilación seleccionando **Publish an Azure Web App** (publicar una aplicación web de Azure).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="3e7c1-199">Proporcionar, **mySp**, entidad de seguridad de servicio de Azure de hello almacenado en el paso anterior como credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="3e7c1-200">En **configuración de la aplicación** sección, elija el grupo de recursos de hello y una aplicación web de Linux en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="3e7c1-201">Elija Publish via Docker (publicar a través de Docker).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="3e7c1-202">Rellene la ruta de acceso de **Dockerfile** (archivo de Docker).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="3e7c1-203">Puede conservar Hola predeterminada "/ Dockerfile" para **dirección URL de registro de Docker**, proporcione en formato de hello https://&lt;myRegistry >. azurecr.io si usas registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="3e7c1-204">Déjelo en blanco si utiliza DockerHub.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="3e7c1-205">Para **las credenciales del registro**, agregar credenciales de Hola para saludo del registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="3e7c1-206">Puede obtener userid hello y una contraseña mediante la ejecución de hello siga los comandos de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="3e7c1-207">Hola primer comando habilita la cuenta de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="3e7c1-208">Hola nombre de la imagen de docker y la etiqueta en **avanzadas** ficha son opcionales.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="3e7c1-209">De forma predeterminada, se obtiene el nombre de la imagen de la imagen de Hola nombre configurado en la etiqueta de Azure Hola portal (en la configuración de contenedor de Docker.) se genera desde $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="3e7c1-210">Asegúrese de especificar el nombre de la imagen de Hola en cualquier portal de Azure o proporcionar un valor para **imagen de Docker** en **avanzadas** ficha. En este ejemplo, escriba "&lt;su_registro>.azurecr.io/calculator" para **Docker image** (imagen de Docker) y deje **Docker Image Tag** (etiqueta de imagen de Docker) en blanco.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="3e7c1-211">Se produce un error en la implementación si utiliza la configuración de imagen de Docker integrada.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="3e7c1-212">Asegúrese de que cambiar imagen personalizada toouse de docker config en configuración del contenedor de Docker en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="3e7c1-213">Para la imagen integrada, utilice toodeploy de enfoque de carga de archivo.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="3e7c1-214">Enfoque de carga toofile similar, puede elegir una ranura diferente que no sea de producción.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="3e7c1-215">Guarde y compile el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-215">Save and build hello project.</span></span> <span data-ttu-id="3e7c1-216">Vea la imagen de contenedor se inserta el registro de tooyour y se implementa la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="3e7c1-217">Implementar la aplicación en Linux a través de Docker mediante canalización Jenkins tooWeb</span><span class="sxs-lookup"><span data-stu-id="3e7c1-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="3e7c1-218">En la interfaz de usuario web de GitHub, abra el archivo **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="3e7c1-219">Haga clic en tooedit de icono de lápiz Hola este grupo de recursos de archivo tooupdate Hola y el nombre de la aplicación web en línea 11 y 12 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="3e7c1-220">Cambiar servidor de línea 13 tooyour contenedor del registro</span><span class="sxs-lookup"><span data-stu-id="3e7c1-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="3e7c1-221">Cambie la línea tooupdate 16 el identificador de la credencial en la instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e7c1-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="3e7c1-222">Creación de una canalización de Jenkins</span><span class="sxs-lookup"><span data-stu-id="3e7c1-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="3e7c1-223">Abra Jenkins en un explorador web, haga clic en **New Item** (Nuevo elemento).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="3e7c1-224">Proporcione un nombre para el trabajo de Hola y seleccione **canalización**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="3e7c1-225">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-225">Click **OK**.</span></span>
3. <span data-ttu-id="3e7c1-226">Haga clic en hello **canalización** pestaña a continuación.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="3e7c1-227">En **Definition** (Definición), seleccione **Pipeline script from SCM** (Script de canalización del SCM).</span><span class="sxs-lookup"><span data-stu-id="3e7c1-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="3e7c1-228">En **SCM**, seleccione **Git**.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="3e7c1-229">Escriba hello GitHub URL para el repositorio bifurcada: https:&lt;repositorio bifurcada > .git</span><span class="sxs-lookup"><span data-stu-id="3e7c1-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="3e7c1-230">Actualizar 7, **ruta del Script** demasiado "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="3e7c1-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="3e7c1-231">Haga clic en **guardar** y trabajo de ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="3e7c1-232">Comprobación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="3e7c1-232">Verify your web app</span></span>

1. <span data-ttu-id="3e7c1-233">archivo WAR de tooverify Hola se ha implementado correctamente tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="3e7c1-234">Abra un explorador web.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-234">Open a web browser.</span></span>
2. <span data-ttu-id="3e7c1-235">Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping verá:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="3e7c1-236">Página principal tooJava aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="3e7c1-237">Se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-237">This is updated!</span></span>
   <span data-ttu-id="3e7c1-238">Sun Jun 17 16:39:10 UTC 2017</span><span class="sxs-lookup"><span data-stu-id="3e7c1-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="3e7c1-239">Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sustituya &lt;x > y &lt;y > con los números) suma de hello tooget de x e y</span><span class="sxs-lookup"><span data-stu-id="3e7c1-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![Calculadora: suma](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="3e7c1-241">Para App Service en Linux</span><span class="sxs-lookup"><span data-stu-id="3e7c1-241">For App service on Linux</span></span>

* <span data-ttu-id="3e7c1-242">tooverify, en CLI de Azure, ejecute:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="3e7c1-243">Obtener Hola siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="3e7c1-244">Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="3e7c1-245">Consulte el mensaje de bienvenida:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="3e7c1-246">Vaya toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (sustituya &lt;x > y &lt;y > con los números) suma de hello tooget de x e y</span><span class="sxs-lookup"><span data-stu-id="3e7c1-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="3e7c1-247">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e7c1-247">Next steps</span></span>

<span data-ttu-id="3e7c1-248">En este tutorial, utilizará Hola servicio de aplicaciones de Azure complemento toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3e7c1-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="3e7c1-249">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="3e7c1-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3e7c1-250">Configurar Jenkins toodeploy servicio de aplicaciones de Azure a través de FTP</span><span class="sxs-lookup"><span data-stu-id="3e7c1-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="3e7c1-251">Configurar Jenkins toodeploy tooAzure servicio de aplicaciones en Linux a través de Docker</span><span class="sxs-lookup"><span data-stu-id="3e7c1-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
