---
title: "Creación de un servidor de Jenkins en Azure"
description: "Instale Jenkins en una máquina virtual Linux de Azure a partir de la plantilla de solución de Jenkins y genere una aplicación Java de ejemplo."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 7bb74f297d52fb25171817175cce64187b397c38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-the-azure-portal"></a><span data-ttu-id="3b5f0-103">Creación de un servidor de Jenkins en una máquina virtual Linux de Azure desde Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3b5f0-103">Create a Jenkins server on an Azure Linux VM from the Azure portal</span></span>

<span data-ttu-id="3b5f0-104">Este tutorial rápido muestra cómo instalar [Jenkins](https://jenkins.io) en una máquina virtual Linux de Ubuntu con las herramientas y complementos configurados para que funcionen con Azure.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-104">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span></span> <span data-ttu-id="3b5f0-105">Cuando haya terminado, dispondrá de un servidor de Jenkins en ejecución en Azure que permitirá compilar una aplicación Java de ejemplo desde [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="3b5f0-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b5f0-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3b5f0-106">Prerequisites</span></span>

* <span data-ttu-id="3b5f0-107">Una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="3b5f0-107">An Azure subscription</span></span>
* <span data-ttu-id="3b5f0-108">Acceso a SSH en la línea de comandos del equipo (por ejemplo, el shell de Bash o [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="3b5f0-108">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-jenkins-vm-from-the-solution-template"></a><span data-ttu-id="3b5f0-109">Creación de la máquina virtual de Jenkins a partir de la plantilla de solución</span><span class="sxs-lookup"><span data-stu-id="3b5f0-109">Create the Jenkins VM from the solution template</span></span>

<span data-ttu-id="3b5f0-110">Abra la [imagen de Marketplace para Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) en su explorador web y seleccione **OBTENERLA AHORA** en el lado izquierdo de la página.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-110">Open the [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from the left-hand side of the page.</span></span> <span data-ttu-id="3b5f0-111">Revise los detalles de precios y seleccione **Continuar** y, después, seleccione **Crear** para configurar el servidor de Jenkins en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-111">Review the pricing details and select **Continue**, then select **Create** to configure the Jenkins server in the Azure portal.</span></span> 
   
![Cuadro de diálogo de Azure Portal](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="3b5f0-113">En la pestaña **Configurar opciones básicas**, rellene los campos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b5f0-113">In the **Configure basic settings** tab, fill in the following fields:</span></span>

![Configuración básica](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="3b5f0-115">Use **Jenkins** en **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="3b5f0-116">Escriba un **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-116">Enter a **User name**.</span></span> <span data-ttu-id="3b5f0-117">El nombre de usuario debe cumplir [requisitos específicos](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="3b5f0-117">The user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="3b5f0-118">Seleccione **Contraseña** como **tipo de autenticación** y escriba una contraseña.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-118">Select **Password** as the **Authentication type** and enter a password.</span></span> <span data-ttu-id="3b5f0-119">La contraseña debe contener un carácter en mayúscula, un número y un carácter especial.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-119">The password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="3b5f0-120">Use **myJenkinsResourceGroup** en **Grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-120">Use **myJenkinsResourceGroup** for the **Resource Group**.</span></span>
* <span data-ttu-id="3b5f0-121">Elija **Este de EE. UU.** como [región de Azure](https://azure.microsoft.com/regions/) en la lista desplegable **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-121">Choose the **East US** [Azure region](https://azure.microsoft.com/regions/) from the **Location** drop-down.</span></span>

<span data-ttu-id="3b5f0-122">Seleccione **Aceptar** para pasar a la pestaña **Configurar opciones adicionales**. Escriba un nombre de dominio único para identificar el servidor Jenkins y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-122">Select **OK** to proceed to the **Configure additional options** tab. Enter a unique domain name to identify the Jenkins server and select **OK**.</span></span>

![Configurar opciones adicionales](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="3b5f0-124">Una vez aprobada la validación, seleccione **Aceptar** de nuevo desde la pestaña **Resumen**. Por último, seleccione **Adquirir** para crear la máquina virtual de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-124">Once validation passes, select **OK** again from the **Summary** tab. Finally, select **Purchase** to create the Jenkins VM.</span></span> <span data-ttu-id="3b5f0-125">Cuando el servidor esté listo, recibirá una notificación en Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="3b5f0-125">When your server is ready, you get a notification in the Azure portal:</span></span>   

![Notificación de que Jenkins está listo](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-to-jenkins"></a><span data-ttu-id="3b5f0-127">Conexión a Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b5f0-127">Connect to Jenkins</span></span>

<span data-ttu-id="3b5f0-128">Vaya a la máquina virtual (por ejemplo, http://jenkins2517454.eastus.cloudapp.azure.com/) en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-128">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="3b5f0-129">No se puede acceder a la consola de Jenkins a través de una HTTP no segura. Por ello, se proporcionan instrucciones en la página para acceder a la consola de forma segura desde su equipo mediante un túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-129">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Desbloquear jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="3b5f0-131">Configure el túnel mediante el comando `ssh` en la página de la línea de comandos, reemplazando `username` por el nombre del usuario administrador de la máquina virtual elegido anteriormente al configurar la máquina virtual desde la plantilla de solución.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-131">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="3b5f0-132">Después de haber iniciado el túnel, vaya a http://localhost:8080/ en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-132">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="3b5f0-133">Obtenga la contraseña inicial mediante la ejecución del comando siguiente en la línea de comandos mientras está conectado a través de SSH a la máquina virtual de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-133">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="3b5f0-134">Desbloquee el panel de Jenkins por primera vez con la contraseña inicial.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-134">Unlock the Jenkins dashboard for the first time using this initial password.</span></span>

![Desbloquear jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="3b5f0-136">Seleccione **Instalar los complementos sugeridos** en la siguiente página y, a continuación, cree un usuario administrador de Jenkins que se pueda utilizar para acceder al panel de este.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-136">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span></span>

![Jenkins ya está listo.](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="3b5f0-138">El servidor Jenkins ya está preparado para compilar código.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-138">The Jenkins server is now ready to build code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="3b5f0-139">Creación del primer trabajo</span><span class="sxs-lookup"><span data-stu-id="3b5f0-139">Create your first job</span></span>

<span data-ttu-id="3b5f0-140">Seleccione **Create new jobs** (Crear nuevos trabajos) en la consola de Jenkins, a continuación, asígnele el nombre **mySampleApp** y seleccione **Freestyle project** (Proyecto de estilo libre) y, finalmente, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-140">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Crear un nuevo trabajo](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="3b5f0-142">Seleccione la pestaña **Source Code Management** (Administración del código fuente), habilite **Git** y escriba la siguiente dirección URL en el campo **Repository URL** (URL del repositorio): `https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="3b5f0-142">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Definir el repositorio Git](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="3b5f0-144">Seleccione la pestaña **Build** (Compilación), después, seleccione **Add build step** (Agregar el paso de compilación) y seleccione la opción **Invoke Gradle script** (Invocar script de Gradle).</span><span class="sxs-lookup"><span data-stu-id="3b5f0-144">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="3b5f0-145">Seleccione **Use Gradle Wrapper** (Usar contenedor de Gradle). A continuación, escriba `complete` en **Wrapper location** (Ubicación del contenedor) y `build` en **Tasks** (Tareas).</span><span class="sxs-lookup"><span data-stu-id="3b5f0-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Usar el contenedor de Gradle para compilar](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="3b5f0-147">Seleccione **Advanced** (Avanzadas)</span><span class="sxs-lookup"><span data-stu-id="3b5f0-147">Select **Advanced..**</span></span> <span data-ttu-id="3b5f0-148">y, a continuación, escriba `complete` en el campo **Root Build script** (Script de compilación raíz).</span><span class="sxs-lookup"><span data-stu-id="3b5f0-148">and then enter `complete` in the **Root Build script** field.</span></span> <span data-ttu-id="3b5f0-149">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-149">Select **Save**.</span></span>

![Establecer configuraciones avanzadas en el paso de compilación del contenedor de Gradle](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-the-code"></a><span data-ttu-id="3b5f0-151">Compilación del código</span><span class="sxs-lookup"><span data-stu-id="3b5f0-151">Build the code</span></span>

<span data-ttu-id="3b5f0-152">Seleccione **Build Now** (Compilar ahora) para compilar el código y empaquetar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-152">Select **Build Now** to compile the code and package the sample app.</span></span> <span data-ttu-id="3b5f0-153">Cuando se complete la compilación, seleccione el vínculo del **área de trabajo** del proyecto.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-153">When your build completes, select the **Workspace** link for the project.</span></span>

![Vaya al área de trabajo para obtener el archivo JAR de la compilación](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="3b5f0-155">Vaya a `complete/build/libs` y asegúrese de que `gs-spring-boot-0.1.0.jar` está allí para comprobar que la compilación se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-155">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span></span> <span data-ttu-id="3b5f0-156">El servidor de Jenkins ya está listo para compilar sus propios proyectos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b5f0-156">Your Jenkins server is now ready to build your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b5f0-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b5f0-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b5f0-158">Agregar máquinas virtuales de Azure como agentes de Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b5f0-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
