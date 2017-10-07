---
title: aaaCreate un servidor Jenkins en Azure
description: "Instalar Jenkins en una máquina virtual de Linux de Azure desde la plantilla de solución de hello Jenkins y generar una aplicación de Java de ejemplo."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="52760-103">Crear un servidor Jenkins en una máquina virtual Linux de Azure de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="52760-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="52760-104">Este tutorial rápido muestra cómo tooinstall [Jenkins](https://jenkins.io) en una VM de Linux Ubuntu con las herramientas de Hola y toowork complementos configurados con Azure.</span><span class="sxs-lookup"><span data-stu-id="52760-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="52760-105">Cuando haya terminado, dispondrá de un servidor de Jenkins en ejecución en Azure que permitirá compilar una aplicación Java de ejemplo desde [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="52760-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52760-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="52760-106">Prerequisites</span></span>

* <span data-ttu-id="52760-107">Una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="52760-107">An Azure subscription</span></span>
* <span data-ttu-id="52760-108">TooSSH de acceso en línea de comandos del equipo (como Hola shell de Bash o [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="52760-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="52760-109">Crear Hola Jenkins VM desde plantilla de solución de Hola</span><span class="sxs-lookup"><span data-stu-id="52760-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="52760-110">Abra hello [una imagen de marketplace para Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) en su explorador web y seleccione **obtener TI ahora** del lado izquierdo de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="52760-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="52760-111">Hola de revisión de precios detalles y seleccione **continuar**, a continuación, seleccione **crear** servidor tooconfigure Hola Jenkins Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="52760-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Cuadro de diálogo de Azure Portal](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="52760-113">Hola **configurar valores básicos** ficha, rellene Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="52760-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![Configuración básica](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="52760-115">Use **Jenkins** en **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="52760-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="52760-116">Escriba un **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="52760-116">Enter a **User name**.</span></span> <span data-ttu-id="52760-117">nombre de usuario de Hello debe cumplir [requisitos específicos](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="52760-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="52760-118">Seleccione **contraseña** como hello **tipo de autenticación** y escriba una contraseña.</span><span class="sxs-lookup"><span data-stu-id="52760-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="52760-119">Hola contraseña debe contener un carácter en mayúscula, un número y un carácter especial.</span><span class="sxs-lookup"><span data-stu-id="52760-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="52760-120">Use **myJenkinsResourceGroup** para hello **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="52760-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="52760-121">Elija hello **UU** [región de Azure](https://azure.microsoft.com/regions/) de hello **ubicación** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="52760-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="52760-122">Seleccione **Aceptar** tooproceed toohello **configurar opciones adicionales** ficha. Escriba un único tooidentify Hola Jenkins servidor DNS y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="52760-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![Configurar opciones adicionales](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="52760-124">Una vez que la validación es correcta, seleccione **Aceptar** nuevo desde hello **resumen** ficha. Por último, seleccione **compra** toocreate Hola Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="52760-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="52760-125">Cuando el servidor está listo, recibirá una notificación en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="52760-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Notificación de que Jenkins está listo](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="52760-127">Conectar tooJenkins</span><span class="sxs-lookup"><span data-stu-id="52760-127">Connect tooJenkins</span></span>

<span data-ttu-id="52760-128">Navegar por máquina virtual de tooyour (por ejemplo, http://jenkins2517454.eastus.cloudapp.azure.com/) en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="52760-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="52760-129">consola de Hello Jenkins es accesible a través de HTTP no segura, por lo que se proporcionan instrucciones en consola Hola página tooaccess Hola Jenkins forma segura desde su equipo usando un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="52760-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Desbloquear jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="52760-131">Configurar el túnel de hello con hello `ssh` comando página Hola desde la línea de comandos de hello, reemplazando `username` con el nombre de Hola de usuario de administrador de máquina virtual de hello elegido anteriormente al configurar la máquina virtual de Hola de plantilla de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="52760-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="52760-132">Después de haber iniciado túnel hello, navegue toohttp://localhost:8080 / en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="52760-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="52760-133">Obtener la contraseña inicial de hello ejecutando el siguiente comando en línea de comandos de hello mientras está conectado a través de SSH toohello Jenkins VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="52760-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="52760-134">Desbloquear el panel de Jenkins Hola para hello primera vez que usa esta contraseña inicial.</span><span class="sxs-lookup"><span data-stu-id="52760-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Desbloquear jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="52760-136">Seleccione **instalar complementos sugerido** en hello, página siguiente y, a continuación, crear un panel Jenkins admin usuario utiliza tooaccess Hola Jenkins.</span><span class="sxs-lookup"><span data-stu-id="52760-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Jenkins ya está listo.](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="52760-138">Hola Jenkins servidor está listo toobuild código.</span><span class="sxs-lookup"><span data-stu-id="52760-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="52760-139">Creación del primer trabajo</span><span class="sxs-lookup"><span data-stu-id="52760-139">Create your first job</span></span>

<span data-ttu-id="52760-140">Seleccione **crear trabajos nuevos** desde la consola de Jenkins hello, a continuación, asígnele el nombre **mySampleApp** y seleccione **proyecto estilo libre**, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="52760-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Crear un nuevo trabajo](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="52760-142">Seleccione hello **administración de código fuente** ficha, habilite **Git**y escriba Hola después de la dirección URL en **dirección URL de repositorio** campo:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="52760-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Definir el repositorio de Git Hola](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="52760-144">Seleccione hello **generar** y, después, seleccione **agregar el paso de compilación**, **Gradle invocar script**.</span><span class="sxs-lookup"><span data-stu-id="52760-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="52760-145">Seleccione **Use Gradle Wrapper** (Usar contenedor de Gradle). A continuación, escriba `complete` en **Wrapper location** (Ubicación del contenedor) y `build` en **Tasks** (Tareas).</span><span class="sxs-lookup"><span data-stu-id="52760-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Usar hello Gradle contenedor toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="52760-147">Seleccione **Advanced** (Avanzadas)</span><span class="sxs-lookup"><span data-stu-id="52760-147">Select **Advanced..**</span></span> <span data-ttu-id="52760-148">y, a continuación, escriba `complete` en hello **raíz Generar script** campo.</span><span class="sxs-lookup"><span data-stu-id="52760-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="52760-149">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="52760-149">Select **Save**.</span></span>

![Establecer la configuración avanzada en el paso de compilación de contenedor de hello Gradle](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="52760-151">Compilar código de hello</span><span class="sxs-lookup"><span data-stu-id="52760-151">Build hello code</span></span>

<span data-ttu-id="52760-152">Seleccione **generar ahora** toocompile Hola código y el paquete Hola aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="52760-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="52760-153">Cuando se complete la compilación, seleccione hello **área de trabajo** vínculo de proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="52760-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Examinar toohello el archivo JAR de área de trabajo tooget Hola de compilación de Hola](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="52760-155">Navegue demasiado`complete/build/libs` y asegúrese de hello `gs-spring-boot-0.1.0.jar` hay tooverify que la compilación fue correcta.</span><span class="sxs-lookup"><span data-stu-id="52760-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="52760-156">Sus Jenkins servidor ahora está listo toobuild sus propios proyectos de Azure.</span><span class="sxs-lookup"><span data-stu-id="52760-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52760-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52760-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52760-158">Agregar máquinas virtuales de Azure como agentes de Jenkins</span><span class="sxs-lookup"><span data-stu-id="52760-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
