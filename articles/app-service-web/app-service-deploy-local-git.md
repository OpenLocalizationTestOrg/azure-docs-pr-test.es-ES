---
title: "Implementación de Git local en el Servicio de aplicaciones de Azure"
description: "Aprenda a habilitar la implementación de Git local en el Servicio de aplicaciones de Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: f1c4911670d3aa32e74b3dfebd83cf3dc3830805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="d44dc-103">Implementación de Git local en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d44dc-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="d44dc-104">En este tutorial se muestra cómo implementar la aplicación en el [Servicio de aplicaciones de Azure] desde un repositorio de Git en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="d44dc-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="d44dc-105">El Servicio de aplicaciones admite este enfoque con la opción de implementación **Git local** en el [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="d44dc-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="d44dc-106">Muchos de los comandos de Git que se describen en este artículo se ejecutan automáticamente al crear una aplicación de App Service mediante la [interfaz de la línea de comandos de Azure], como se describe [aquí](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d44dc-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d44dc-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d44dc-107">Prerequisites</span></span>
<span data-ttu-id="d44dc-108">Para completar este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="d44dc-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="d44dc-109">Git.</span><span class="sxs-lookup"><span data-stu-id="d44dc-109">Git.</span></span> <span data-ttu-id="d44dc-110">Puede descargar el archivo binario de instalación [aquí](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="d44dc-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="d44dc-111">Conocimientos básicos de Git.</span><span class="sxs-lookup"><span data-stu-id="d44dc-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="d44dc-112">Una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d44dc-112">A Microsoft Azure account.</span></span> <span data-ttu-id="d44dc-113">Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="d44dc-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="d44dc-114">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Probar Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d44dc-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="d44dc-115">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="d44dc-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="d44dc-116"><a name="Step1"></a>Paso 1: Creación de un repositorio local</span><span class="sxs-lookup"><span data-stu-id="d44dc-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="d44dc-117">Realice las tareas siguientes al crear un nuevo repositorio Git.</span><span class="sxs-lookup"><span data-stu-id="d44dc-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="d44dc-118">Inicie una herramienta de línea de comandos, como **GitBash** (Windows) o **Bash** (shell de Unix).</span><span class="sxs-lookup"><span data-stu-id="d44dc-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="d44dc-119">En los sistemas OS X puede tener acceso a la línea de comandos mediante la aplicación **Terminal** .</span><span class="sxs-lookup"><span data-stu-id="d44dc-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="d44dc-120">Desplácese al directorio donde se ubicará el contenido que se va a implementar.</span><span class="sxs-lookup"><span data-stu-id="d44dc-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="d44dc-121">Utilice el comando siguiente para inicializar un nuevo repositorio Git:</span><span class="sxs-lookup"><span data-stu-id="d44dc-121">Use the following command to initialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="d44dc-122"><a name="Step2"></a>Paso 2: Confirmación del contenido</span><span class="sxs-lookup"><span data-stu-id="d44dc-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="d44dc-123">El Servicio de aplicaciones admite aplicaciones creadas en varios lenguajes de programación.</span><span class="sxs-lookup"><span data-stu-id="d44dc-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="d44dc-124">Si el repositorio ya incluye contenido, omita este punto y vaya al punto 2.</span><span class="sxs-lookup"><span data-stu-id="d44dc-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="d44dc-125">Si el repositorio todavía no incluye contenido, simplemente llénelo con un archivo .html estático, tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d44dc-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="d44dc-126">Con un editor de texto, cree un archivo nuevo denominado **index.html** en la raíz del repositorio Git.</span><span class="sxs-lookup"><span data-stu-id="d44dc-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="d44dc-127">Agregue el texto siguiente como contenido para el archivo index.htm y guárdelo: *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="d44dc-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="d44dc-128">Desde la línea de comandos, compruebe que está en la raíz de su repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="d44dc-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="d44dc-129">Use el comando siguiente para agregar archivos al repositorio:</span><span class="sxs-lookup"><span data-stu-id="d44dc-129">Then use the following command to add files to your repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="d44dc-130">A continuación, confirme los cambios en el repositorio mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d44dc-130">Next, commit the changes to the repository by using the following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="d44dc-131"><a name="Step3"></a>Paso 3: Habilitación del repositorio de aplicaciones de App Service</span><span class="sxs-lookup"><span data-stu-id="d44dc-131"><a name="Step3"></a>Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="d44dc-132">Lleve a cabo los pasos siguientes para habilitar un repositorio de Git para su aplicación del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d44dc-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="d44dc-133">Inicie sesión en el [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="d44dc-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="d44dc-134">En la hoja de su aplicación de App Service, haga clic en **Configuración > Origen de implementación**.</span><span class="sxs-lookup"><span data-stu-id="d44dc-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="d44dc-135">Haga clic en **Elegir recurso**, luego en **Repositorio de Git local** y, finalmente, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d44dc-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Repositorio de Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="d44dc-137">Si esta es la primera vez que configura un repositorio en Azure, tendrá que crear unas credenciales de inicio de sesión para él.</span><span class="sxs-lookup"><span data-stu-id="d44dc-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="d44dc-138">Las usará para iniciar sesión en el repositorio de Azure y aplicar cambios desde su repositorio Git local.</span><span class="sxs-lookup"><span data-stu-id="d44dc-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="d44dc-139">En la hoja de la aplicación, haga clic en **Configuración > Credenciales de implementación** y configure el nombre de usuario y la contraseña de la implementación.</span><span class="sxs-lookup"><span data-stu-id="d44dc-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="d44dc-140">Cuando haya terminado, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d44dc-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="d44dc-141"><a name="Step4"></a>Paso 4: Implementación del proyecto</span><span class="sxs-lookup"><span data-stu-id="d44dc-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="d44dc-142">Siga los pasos que se indican a continuación para publicar una aplicación en el Servicio de aplicaciones mediante un Git local.</span><span class="sxs-lookup"><span data-stu-id="d44dc-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="d44dc-143">En la hoja de la aplicación en Azure Portal, haga clic en **Configuración > Propiedades** para la **Dirección URL de Git**.</span><span class="sxs-lookup"><span data-stu-id="d44dc-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="d44dc-144">**Dirección URL de Git** es la referencia remota en la que se realizará la implementación desde el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="d44dc-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="d44dc-145">Usará esta dirección URL en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="d44dc-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="d44dc-146">Mediante la línea de comandos, compruebe que está en la raíz de su repositorio de Git local.</span><span class="sxs-lookup"><span data-stu-id="d44dc-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="d44dc-147">Use `git remote` para agregar la referencia remota que aparecía en **Dirección URL de Git** en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="d44dc-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="d44dc-148">El comando será similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d44dc-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="d44dc-149">El comando **remote** agrega una referencia con nombre a un repositorio remoto.</span><span class="sxs-lookup"><span data-stu-id="d44dc-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="d44dc-150">En este ejemplo, se crea una referencia llamada "azure" para el repositorio de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d44dc-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="d44dc-151">Inserte el contenido en el Servicio de aplicaciones con el nuevo comando remoto **azure** que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="d44dc-151">Push your content to App Service using the new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal. Enter the password (note that Gitbash does not echo asterisks to the console as you type your password). 
5. <span data-ttu-id="d44dc-152">Vuelva a la aplicación en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d44dc-152">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="d44dc-153">En la hoja **Implementaciones** debería aparecer una entrada de registro de la última inserción.</span><span class="sxs-lookup"><span data-stu-id="d44dc-153">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="d44dc-154">Haga clic en el botón **Examinar** situado en la parte superior de la hoja de la aplicación para comprobar que el contenido se haya implementado.</span><span class="sxs-lookup"><span data-stu-id="d44dc-154">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <span data-ttu-id="d44dc-155"><a name="Step5"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="d44dc-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="d44dc-156">Estos son los errores o problemas que suelen aparecer al usar Git para publicar en una aplicación del Servicio de aplicaciones en Azure:</span><span class="sxs-lookup"><span data-stu-id="d44dc-156">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="d44dc-157">**Síntoma**: no es posible tener acceso a ’[siteURL]’: error al conectarse a [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="d44dc-157">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="d44dc-158">**Causa**: este error puede producirse si la aplicación no está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="d44dc-158">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="d44dc-159">**Resolución**: inicie la aplicación en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d44dc-159">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="d44dc-160">La implementación de Git no funcionará a menos que se esté ejecutando la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d44dc-160">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="d44dc-161">**Síntoma**: no se pudo resolver el host "nombre de host".</span><span class="sxs-lookup"><span data-stu-id="d44dc-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="d44dc-162">**Causa**: este error puede ocurrir si la información de dirección introducida al crear el repositorio remoto "azure" no era correcta.</span><span class="sxs-lookup"><span data-stu-id="d44dc-162">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="d44dc-163">**Resolución**: use el comando `git remote -v` para obtener un listado de todos los remotos, junto con la dirección URL asociada.</span><span class="sxs-lookup"><span data-stu-id="d44dc-163">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="d44dc-164">Compruebe que la URL para el repositorio correcto "azure" es correcta.</span><span class="sxs-lookup"><span data-stu-id="d44dc-164">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="d44dc-165">Si lo necesita, suprima y vuelva a crear este repositorio remoto utilizando la URL correcta.</span><span class="sxs-lookup"><span data-stu-id="d44dc-165">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="d44dc-166">**Síntoma**: no hay referencias en común y no se ha especificado nada; sin hacer nada.</span><span class="sxs-lookup"><span data-stu-id="d44dc-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="d44dc-167">Quizá hay que especificar una rama como "principal".</span><span class="sxs-lookup"><span data-stu-id="d44dc-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="d44dc-168">**Causa**: este error puede ocurrir si no especifica una rama al realizar una operación de inserción en Git y no hay establecido el valor push.default utilizado por Git.</span><span class="sxs-lookup"><span data-stu-id="d44dc-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="d44dc-169">**Resolución**: vuelva a realizar la operación de inserción, especificando la rama principal.</span><span class="sxs-lookup"><span data-stu-id="d44dc-169">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="d44dc-170">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d44dc-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="d44dc-171">**Síntoma**: src refspec [branchname] no coincide con ninguna.</span><span class="sxs-lookup"><span data-stu-id="d44dc-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="d44dc-172">**Causa**: este error puede tener lugar si intenta insertar una rama que no es la principal en el repositorio remoto "azure".</span><span class="sxs-lookup"><span data-stu-id="d44dc-172">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="d44dc-173">**Resolución**: vuelva a realizar la operación de inserción, especificando la rama principal.</span><span class="sxs-lookup"><span data-stu-id="d44dc-173">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="d44dc-174">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d44dc-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="d44dc-175">**Síntoma**: error de RPC; resultado=22; código HTTP=502.</span><span class="sxs-lookup"><span data-stu-id="d44dc-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="d44dc-176">**Causa**: este error puede producirse si se trata de insertar un repositorio de git de gran tamaño a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d44dc-176">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="d44dc-177">**Resolución**: cambie la configuración de git en la máquina local para aumentar el tamaño de postBuffer.</span><span class="sxs-lookup"><span data-stu-id="d44dc-177">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="d44dc-178">**Síntoma**: Error: los cambios se han confirmado en el repositorio remoto, pero la aplicación web no se ha actualizado.</span><span class="sxs-lookup"><span data-stu-id="d44dc-178">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="d44dc-179">**Causa**: este error puede ocurrir si está implementando una aplicación Node.js que contiene un archivo package.json que especifica módulos requeridos adicionales.</span><span class="sxs-lookup"><span data-stu-id="d44dc-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="d44dc-180">**Resolución**: los mensajes adicionales que contienen 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="d44dc-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="d44dc-181">deben registrarse antes de este error y pueden proporcionar contexto adicional sobre el error.</span><span class="sxs-lookup"><span data-stu-id="d44dc-181">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="d44dc-182">A continuación se indican las causas conocidas de este error y el mensaje 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="d44dc-182">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="d44dc-183">correspondiente:</span><span class="sxs-lookup"><span data-stu-id="d44dc-183">message:</span></span>

* <span data-ttu-id="d44dc-184">**Archivo package.json con estructura incorrecta**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="d44dc-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="d44dc-185">No se pudieron leer las dependencias.</span><span class="sxs-lookup"><span data-stu-id="d44dc-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="d44dc-186">**Módulo nativo que no tiene una distribución binaria para Windows**:</span><span class="sxs-lookup"><span data-stu-id="d44dc-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="d44dc-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="d44dc-187">npm ERR!</span></span> <span data-ttu-id="d44dc-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="d44dc-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="d44dc-189">OR</span><span class="sxs-lookup"><span data-stu-id="d44dc-189">OR</span></span>
  * <span data-ttu-id="d44dc-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="d44dc-190">npm ERR!</span></span> <span data-ttu-id="d44dc-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="d44dc-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d44dc-192">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d44dc-192">Additional Resources</span></span>
* [<span data-ttu-id="d44dc-193">Documentación de Git</span><span class="sxs-lookup"><span data-stu-id="d44dc-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="d44dc-194">Documentación de Project Kudu</span><span class="sxs-lookup"><span data-stu-id="d44dc-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="d44dc-195">Implementación continua en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d44dc-195">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="d44dc-196">Uso de PowerShell para Azure</span><span class="sxs-lookup"><span data-stu-id="d44dc-196">How to use PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="d44dc-197">Cómo utilizar la interfaz de línea de comandos de Azure</span><span class="sxs-lookup"><span data-stu-id="d44dc-197">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="d44dc-198">[Servicio de aplicaciones de Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="d44dc-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span></span>
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
<span data-ttu-id="d44dc-199">[Portal de Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="d44dc-199">[Azure Portal]: https://portal.azure.com</span></span>
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="d44dc-200">[interfaz de la línea de comandos de Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span><span class="sxs-lookup"><span data-stu-id="d44dc-200">[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span></span>

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
