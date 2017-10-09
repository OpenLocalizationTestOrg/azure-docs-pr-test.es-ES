---
title: "Implementación de Git de aaaLocal tooAzure servicio de aplicaciones"
description: "Obtenga información acerca de cómo tooenable local Git implementación tooAzure servicio de aplicaciones."
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
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="ed131-103">TooAzure de implementación de Git local servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ed131-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="ed131-104">Este tutorial muestra cómo toodeploy su aplicación demasiado[servicio de aplicaciones de Azure] desde un repositorio de Git en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="ed131-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="ed131-105">Servicio de aplicaciones es compatible con este enfoque con hello **Git Local** opción de implementación en hello [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="ed131-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="ed131-106">Muchos de los comandos de Git Hola se describe en este artículo se realizan automáticamente al crear una aplicación de servicio de aplicaciones con hello [interfaz de línea de comandos de Azure] tal como se describe [aquí](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed131-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed131-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ed131-107">Prerequisites</span></span>
<span data-ttu-id="ed131-108">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="ed131-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="ed131-109">Git.</span><span class="sxs-lookup"><span data-stu-id="ed131-109">Git.</span></span> <span data-ttu-id="ed131-110">Puede descargar los binarios de instalación de hello [aquí](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="ed131-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="ed131-111">Conocimientos básicos de Git.</span><span class="sxs-lookup"><span data-stu-id="ed131-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="ed131-112">Una cuenta de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ed131-112">A Microsoft Azure account.</span></span> <span data-ttu-id="ed131-113">Si aún no tiene ninguna, puede [registrarse para una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial) o [activar las ventajas de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="ed131-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="ed131-114">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ed131-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="ed131-115">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="ed131-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="ed131-116"><a name="Step1"></a>Paso 1: Creación de un repositorio local</span><span class="sxs-lookup"><span data-stu-id="ed131-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="ed131-117">Realizar Hola después tareas toocreate un nuevo repositorio Git.</span><span class="sxs-lookup"><span data-stu-id="ed131-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="ed131-118">Inicie una herramienta de línea de comandos, como **GitBash** (Windows) o **Bash** (shell de Unix).</span><span class="sxs-lookup"><span data-stu-id="ed131-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="ed131-119">En sistemas de OS X pueden acceder a los Hola de línea de comandos a través de hello **Terminal** aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed131-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="ed131-120">Navegue directorio toohello donde esté ubicado toodeploy contenido Hola.</span><span class="sxs-lookup"><span data-stu-id="ed131-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="ed131-121">Usar hello después de un nuevo repositorio Git del comando tooinitialize:</span><span class="sxs-lookup"><span data-stu-id="ed131-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="ed131-122"><a name="Step2"></a>Paso 2: Confirmación del contenido</span><span class="sxs-lookup"><span data-stu-id="ed131-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="ed131-123">El Servicio de aplicaciones admite aplicaciones creadas en varios lenguajes de programación.</span><span class="sxs-lookup"><span data-stu-id="ed131-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="ed131-124">Si el repositorio ya incluye contenido omitir este punto y mover toopoint 2 a continuación.</span><span class="sxs-lookup"><span data-stu-id="ed131-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="ed131-125">Si el repositorio todavía no incluye contenido, simplemente llénelo con un archivo .html estático, tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="ed131-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="ed131-126">Con un editor de texto, cree un nuevo archivo denominado **index.html** en raíz de hello del repositorio de Git Hola</span><span class="sxs-lookup"><span data-stu-id="ed131-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="ed131-127">Agregar Hola después de texto como contenido de Hola para index.html Hola de archivo y guárdelo: *Git Hola!*</span><span class="sxs-lookup"><span data-stu-id="ed131-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="ed131-128">Desde la línea de comandos de hello, compruebe que se encuentra bajo la raíz de Hola de su repositorio de Git.</span><span class="sxs-lookup"><span data-stu-id="ed131-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="ed131-129">A continuación, usar hello después de repositorio de comando tooadd archivos tooyour:</span><span class="sxs-lookup"><span data-stu-id="ed131-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="ed131-130">A continuación, confirmar toohello repositorio de hello cambios mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ed131-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="ed131-131"><a name="Step3"></a>Paso 3: Habilitar Hola repositorio de aplicación de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ed131-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="ed131-132">Realizar Hola siguiendo los pasos tooenable un repositorio Git para la aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ed131-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="ed131-133">Inicie sesión en toohello [Portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="ed131-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="ed131-134">En la hoja de su aplicación de App Service, haga clic en **Configuración > Origen de implementación**.</span><span class="sxs-lookup"><span data-stu-id="ed131-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="ed131-135">Haga clic en **Elegir recurso**, luego en **Repositorio de Git local** y, finalmente, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ed131-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Repositorio de Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="ed131-137">Si se trata de la primera configuración de tiempo de un repositorio de Azure, necesita credenciales de inicio de sesión de toocreate para él.</span><span class="sxs-lookup"><span data-stu-id="ed131-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="ed131-138">Se usará ellos toolog en hello Azure repositorio e insertar los cambios desde el repositorio Git local.</span><span class="sxs-lookup"><span data-stu-id="ed131-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="ed131-139">En la hoja de la aplicación, haga clic en **Configuración > Credenciales de implementación** y configure el nombre de usuario y la contraseña de la implementación.</span><span class="sxs-lookup"><span data-stu-id="ed131-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="ed131-140">Cuando haya terminado, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ed131-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="ed131-141"><a name="Step4"></a>Paso 4: Implementación del proyecto</span><span class="sxs-lookup"><span data-stu-id="ed131-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="ed131-142">Usar hello siguiendo los pasos toopublish su tooApp mediante Git Local del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed131-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="ed131-143">En la hoja de la aplicación Hola Portal de Azure, haga clic en **configuración > propiedades** para hello **dirección URL de Git**.</span><span class="sxs-lookup"><span data-stu-id="ed131-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="ed131-144">**Dirección URL de GIT** es Hola referencia remoto toodeploy toofrom el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="ed131-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="ed131-145">Usará esta dirección URL en hello pasos.</span><span class="sxs-lookup"><span data-stu-id="ed131-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="ed131-146">Use Hola de línea de comandos, para comprobar que está en la raíz de Hola de su repositorio de Git local.</span><span class="sxs-lookup"><span data-stu-id="ed131-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="ed131-147">Use `git remote` aparece en referencia tooadd Hola remoto **dirección URL de Git** del paso 1.</span><span class="sxs-lookup"><span data-stu-id="ed131-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="ed131-148">El comando tendrá un aspecto similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="ed131-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="ed131-149">Hola **remoto** comando agrega un repositorio remoto de tooa de referencia con nombre.</span><span class="sxs-lookup"><span data-stu-id="ed131-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="ed131-150">En este ejemplo, se crea una referencia llamada "azure" para el repositorio de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ed131-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="ed131-151">Insertar el contenido tooApp servicio usando Hola nueva **azure** remoto que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="ed131-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="ed131-152">Volver atrás tooyour aplicación Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed131-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="ed131-153">Una entrada del registro de la última inserción debe mostrarse en hello **implementaciones** hoja.</span><span class="sxs-lookup"><span data-stu-id="ed131-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="ed131-154">Haga clic en hello **examinar** situado en la parte superior de Hola de Hola de tooverify de hoja de la aplicación hello contenido se ha implementado.</span><span class="sxs-lookup"><span data-stu-id="ed131-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="ed131-155"><a name="Step5"></a>Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="ed131-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="ed131-156">siguiente Hola es errores o problemas más comunes al usar Git toopublish tooan aplicación de servicio de aplicaciones en Azure:</span><span class="sxs-lookup"><span data-stu-id="ed131-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="ed131-157">**Síntoma**: no se puede tooaccess '[siteURL]': no se pudo tooconnect demasiado [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="ed131-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="ed131-158">**Causa**: este error puede producirse si la aplicación hello no se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="ed131-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="ed131-159">**Resolución de**: inicio de aplicación de hello en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed131-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="ed131-160">Implementación de GIT no funcionará a menos que se ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ed131-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="ed131-161">**Síntoma**: no se pudo resolver el host "nombre de host".</span><span class="sxs-lookup"><span data-stu-id="ed131-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="ed131-162">**Causa**: este error puede producirse si escribe la información de dirección de hello al crear hello 'azure' remoto era incorrecto.</span><span class="sxs-lookup"><span data-stu-id="ed131-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="ed131-163">**Resolución**: Hola uso `git remote -v` comando toolist todos los controles remotos, junto con la dirección URL de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="ed131-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="ed131-164">Compruebe que la dirección URL de Hola para hello 'azure' remoto es correcto.</span><span class="sxs-lookup"><span data-stu-id="ed131-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="ed131-165">Si es necesario, quitar y volver a crear este remoto con la dirección URL correcta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed131-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="ed131-166">**Síntoma**: no hay referencias en común y no se ha especificado nada; sin hacer nada.</span><span class="sxs-lookup"><span data-stu-id="ed131-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="ed131-167">Quizá hay que especificar una rama como "principal".</span><span class="sxs-lookup"><span data-stu-id="ed131-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="ed131-168">**Causa**: este error puede producirse si no especifica una bifurcación al realizar una operación de inserción de git y tener no hello push.default valor establecido utilizando Git.</span><span class="sxs-lookup"><span data-stu-id="ed131-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="ed131-169">**Resolución**: realizar la operación de inserción de hello nuevo, especificando la bifurcación principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed131-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="ed131-170">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ed131-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="ed131-171">**Síntoma**: src refspec [branchname] no coincide con ninguna.</span><span class="sxs-lookup"><span data-stu-id="ed131-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="ed131-172">**Causa**: este error puede producirse si intenta toopush tooa rama distinta de la maestra en hello 'azure' remoto.</span><span class="sxs-lookup"><span data-stu-id="ed131-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="ed131-173">**Resolución**: realizar la operación de inserción de hello nuevo, especificando la bifurcación principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed131-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="ed131-174">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ed131-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="ed131-175">**Síntoma**: error de RPC; resultado=22; código HTTP=502.</span><span class="sxs-lookup"><span data-stu-id="ed131-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="ed131-176">**Causa**: este error puede producirse si intenta toopush un repositorio git grandes a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ed131-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="ed131-177">**Resolución**: cambiar la configuración de git hello en enviamos de Hola de hello máquina local toomake más grande</span><span class="sxs-lookup"><span data-stu-id="ed131-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="ed131-178">**Síntoma**: Error: repositorio de tooremote Confirmar cambios pero la aplicación web no actualizada.</span><span class="sxs-lookup"><span data-stu-id="ed131-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="ed131-179">**Causa**: este error puede ocurrir si está implementando una aplicación Node.js que contiene un archivo package.json que especifica módulos requeridos adicionales.</span><span class="sxs-lookup"><span data-stu-id="ed131-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="ed131-180">**Resolución**: los mensajes adicionales que contienen 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="ed131-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="ed131-181">debe ser error toothis anterior ha iniciado y puede proporcionar contexto adicional en caso de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed131-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="ed131-182">siguiente Hola se conocen las causas de este error y Hola correspondiente 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="ed131-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="ed131-183">correspondiente:</span><span class="sxs-lookup"><span data-stu-id="ed131-183">message:</span></span>

* <span data-ttu-id="ed131-184">**Archivo package.json con estructura incorrecta**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ed131-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="ed131-185">No se pudieron leer las dependencias.</span><span class="sxs-lookup"><span data-stu-id="ed131-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="ed131-186">**Módulo nativo que no tiene una distribución binaria para Windows**:</span><span class="sxs-lookup"><span data-stu-id="ed131-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="ed131-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ed131-187">npm ERR!</span></span> <span data-ttu-id="ed131-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="ed131-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="ed131-189">OR</span><span class="sxs-lookup"><span data-stu-id="ed131-189">OR</span></span>
  * <span data-ttu-id="ed131-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ed131-190">npm ERR!</span></span> <span data-ttu-id="ed131-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="ed131-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed131-192">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ed131-192">Additional Resources</span></span>
* [<span data-ttu-id="ed131-193">Documentación de Git</span><span class="sxs-lookup"><span data-stu-id="ed131-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="ed131-194">Documentación de Project Kudu</span><span class="sxs-lookup"><span data-stu-id="ed131-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="ed131-195">Implementación continua tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ed131-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="ed131-196">¿Cómo toouse PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="ed131-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="ed131-197">¿Cómo toouse Hola interfaz de línea de comandos de Azure</span><span class="sxs-lookup"><span data-stu-id="ed131-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[servicio de aplicaciones de Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Portal de Azure]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[interfaz de línea de comandos de Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
