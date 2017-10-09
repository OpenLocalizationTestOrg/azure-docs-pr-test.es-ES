---
title: "aaaDeploy una tooLinux de aplicación Node.js máquinas virtuales en Azure"
description: "Obtenga información acerca de cómo toodeploy un Node.js máquinas de virtuales tooLinux de aplicación en Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="a11e4-103">Implementar un tooLinux de aplicación Node.js máquinas virtuales en Azure</span><span class="sxs-lookup"><span data-stu-id="a11e4-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="a11e4-104">Este tutorial se muestra cómo una aplicación Node.js tootake e implementar máquinas virtuales de tooLinux ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="a11e4-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="a11e4-105">instrucciones de Hello en este tutorial se pueden aplicar en cualquier sistema operativo que sea capaz de ejecutar Node.js.</span><span class="sxs-lookup"><span data-stu-id="a11e4-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="a11e4-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="a11e4-106">You'll learn how to:</span></span>

* <span data-ttu-id="a11e4-107">Bifurcar y clonar un repositorio de GitHub con una aplicación simple de tarea pendiente</span><span class="sxs-lookup"><span data-stu-id="a11e4-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="a11e4-108">Crear y configurar dos máquinas virtuales de Linux en la aplicación de Azure toorun hello;</span><span class="sxs-lookup"><span data-stu-id="a11e4-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="a11e4-109">Recorrer en iteración en la aplicación hello insertando la máquina virtual de las actualizaciones toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="a11e4-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="a11e4-110">toocomplete este tutorial, se necesita una cuenta de GitHub y una cuenta de Microsoft Azure y Hola capacidad toouse Git desde un equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="a11e4-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="a11e4-111">Si no tiene cuenta de GitHub, puede suscribirse para obtener una gratis [aquí](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="a11e4-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="a11e4-112">Si no tiene una cuenta de [Microsoft Azure](https://azure.microsoft.com/), puede registrarse para obtener una evaluación gratuita [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a11e4-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="a11e4-113">Esto le llevará también a través del proceso de registro de hello un [Account Microsoft](http://account.microsoft.com) si ya no dispone de uno.</span><span class="sxs-lookup"><span data-stu-id="a11e4-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="a11e4-114">Como alternativa, si tiene una suscripción de Visual Studio, puede [activar los beneficios de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a11e4-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="a11e4-115">Si no tiene Git en la máquina de desarrollo y está utilizando un equipo Macintosh o Windows, instale Git desde [aquí](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="a11e4-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="a11e4-116">Si usas Linux, instale git mediante el mecanismo de hello más adecuada para usted, como `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="a11e4-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="a11e4-117">Bifurcación y clonar Hola la aplicación de tareas</span><span class="sxs-lookup"><span data-stu-id="a11e4-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="a11e4-118">Hola aplicación de lista de tareas usada por este tutorial implementa un servidor front-end web simple sobre una instancia de MongoDB que realiza un seguimiento de una lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="a11e4-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="a11e4-119">Tras iniciar sesión en tooGitHub, vaya [aquí](https://github.com/stepro/node-todo) toofind Hola aplicación y bifurcar mediante el vínculo de hello en la parte superior de hello derecha.</span><span class="sxs-lookup"><span data-stu-id="a11e4-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="a11e4-120">Esto debería crear un repositorio en la cuenta con el nombre *accountname*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="a11e4-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="a11e4-121">Ahora en la máquina de desarrollo, clone este repositorio:</span><span class="sxs-lookup"><span data-stu-id="a11e4-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="a11e4-122">Usaremos este clon local del repositorio de hello un poco más adelante al realizar cambios de código fuente de toohello.</span><span class="sxs-lookup"><span data-stu-id="a11e4-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="a11e4-123">Crear y configurar Hola máquinas virtuales de Linux</span><span class="sxs-lookup"><span data-stu-id="a11e4-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="a11e4-124">Azure ofrece un buen soporte para los procesos sin formato con las máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="a11e4-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="a11e4-125">Esta parte de hello tutorial, se muestra cómo puede poner en marcha dos máquinas virtuales de Linux e implementar toothem de aplicación de lista de tareas de hello, ejecución Hola front-end web en uno y Hola instancia MongoDB en hello otro fácilmente.</span><span class="sxs-lookup"><span data-stu-id="a11e4-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="a11e4-126">Creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a11e4-126">Creating Virtual Machines</span></span>
<span data-ttu-id="a11e4-127">toocreate de manera más fácil de Hello una nueva máquina virtual en Azure es toouse Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a11e4-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="a11e4-128">Haga clic en [aquí](https://portal.azure.com) toosign en e inicie Hola Portal de Azure en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="a11e4-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="a11e4-129">Una vez que haya cargado Hola Portal de Azure, complete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a11e4-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="a11e4-130">Haga clic en Hola "+ nuevo" vincular;</span><span class="sxs-lookup"><span data-stu-id="a11e4-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="a11e4-131">Seleccione la categoría de "Proceso" hello y elija "Ubuntu Server 14.04 LTS";</span><span class="sxs-lookup"><span data-stu-id="a11e4-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="a11e4-132">Seleccione el modelo de implementación de "Administrador de recursos" hello y haga clic en "Crear";</span><span class="sxs-lookup"><span data-stu-id="a11e4-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="a11e4-133">Rellene los conceptos básicos de hello siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="a11e4-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="a11e4-134">Especifique un nombre que pueda identificar fácilmente más tarde.</span><span class="sxs-lookup"><span data-stu-id="a11e4-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="a11e4-135">Para este tutorial, elija la autenticación mediante contraseña.</span><span class="sxs-lookup"><span data-stu-id="a11e4-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="a11e4-136">Cree un nuevo grupo de recursos con un nombre identificable.</span><span class="sxs-lookup"><span data-stu-id="a11e4-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="a11e4-137">Para el tamaño de la máquina Virtual de hello, "A1" estándar"es una opción razonable para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a11e4-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="a11e4-138">Para ver otras opciones, asegúrese de que el tipo de disco de hello es "Estándar" y acepte que Hola a todos los valores predeterminados restantes.</span><span class="sxs-lookup"><span data-stu-id="a11e4-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="a11e4-139">Iniciar creación de hello en la página de resumen de Hola.</span><span class="sxs-lookup"><span data-stu-id="a11e4-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="a11e4-140">Realizar Hola anterior procesar dos veces toocreate dos las máquinas virtuales Linux, uno para front-end web de hello y otro para la instancia de MongoDB Hola.</span><span class="sxs-lookup"><span data-stu-id="a11e4-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="a11e4-141">Creación de máquinas virtuales de hello tardará unos 5-10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a11e4-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="a11e4-142">Asignación de una entrada DNS para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a11e4-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="a11e4-143">De manera predeterminada, a las máquinas virtuales creadas en Azure se puede acceder solo a través de una dirección IP pública, como 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="a11e4-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="a11e4-144">Vamos a hacer máquinas Hola identificar más fácilmente mediante la asignación de las entradas de DNS.</span><span class="sxs-lookup"><span data-stu-id="a11e4-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="a11e4-145">Una vez que el portal de hello indica que se han creado las máquinas virtuales hello, haga clic en vínculo de Hola "Máquinas virtuales" en la barra de navegación izquierdo de Hola y busque las máquinas.</span><span class="sxs-lookup"><span data-stu-id="a11e4-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="a11e4-146">Para cada máquina:</span><span class="sxs-lookup"><span data-stu-id="a11e4-146">For each machine:</span></span>

* <span data-ttu-id="a11e4-147">Busque la pestaña de Essentials hello y haga clic en hello la dirección IP pública;</span><span class="sxs-lookup"><span data-stu-id="a11e4-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="a11e4-148">En la configuración de dirección IP pública hello, asigne una etiqueta de nombre DNS y guardar.</span><span class="sxs-lookup"><span data-stu-id="a11e4-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="a11e4-149">portal de Hello garantizará ese nombre de Hola que especifique estará disponible.</span><span class="sxs-lookup"><span data-stu-id="a11e4-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="a11e4-150">Después de guardar la configuración de hello, las máquinas virtuales tendrán nombres de host similares demasiado`machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="a11e4-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="a11e4-151">Conexión toohello máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a11e4-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="a11e4-152">Cuando se aprovisionan las máquinas virtuales, eran tooallow preconfigurada de conexiones remotas a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="a11e4-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="a11e4-153">Se trata de mecanismo de hello usaremos máquinas virtuales de tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="a11e4-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="a11e4-154">Si está utilizando Windows para el desarrollo, deberá tooget un cliente de SSH si ya no dispone de uno.</span><span class="sxs-lookup"><span data-stu-id="a11e4-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="a11e4-155">Una opción común es PuTTY, que puede descargar desde [aquí](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="a11e4-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="a11e4-156">Los sistemas operativos Macintosh y Linux vienen con una versión de SSH preinstalada.</span><span class="sxs-lookup"><span data-stu-id="a11e4-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="a11e4-157">Configuración de máquina Virtual del servidor front-end Web de Hola</span><span class="sxs-lookup"><span data-stu-id="a11e4-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="a11e4-158">Máquina de front-end web SSH toohello creado mediante PuTTY, ssh línea de comandos o la herramienta SSH prefiera.</span><span class="sxs-lookup"><span data-stu-id="a11e4-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="a11e4-159">Debería ver un mensaje de bienvenida seguido de un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="a11e4-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="a11e4-160">En primer lugar, debe asegurarse de que Git y el nodo estén instalados:</span><span class="sxs-lookup"><span data-stu-id="a11e4-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="a11e4-161">Puesto que el front-end web de la aplicación hello depende de algunos módulos de Node.js nativo, necesitamos conjunto esencial de hello tooinstall de herramientas de compilación:</span><span class="sxs-lookup"><span data-stu-id="a11e4-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="a11e4-162">Por último, vamos a instalar una aplicación Node.js denominada *indefinidamente*, que permite a las aplicaciones de servidor de Node.js toorun:</span><span class="sxs-lookup"><span data-stu-id="a11e4-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="a11e4-163">Estas son todas las dependencias de hello necesarios en el front-end de máquina virtual toobe toorun capaz de Hola de esta aplicación web, así que vamos a hacer que ejecutan.</span><span class="sxs-lookup"><span data-stu-id="a11e4-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="a11e4-164">toodo, primero crearemos a un clon del repositorio de GitHub de Hola que bifurcado previamente para que pueda publicar fácilmente las actualizaciones toohello virtual machine (hablaremos sobre este escenario de actualización más adelante) y, a continuación, clonar Hola clon tooprovide una versión de Hola repositorio que realmente se pueden ejecutar.</span><span class="sxs-lookup"><span data-stu-id="a11e4-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="a11e4-165">A partir del directorio de inicio (~) hello, ejecutar Hola después de comandos (reemplazando *accountname* con su nombre de cuenta de usuario de GitHub):</span><span class="sxs-lookup"><span data-stu-id="a11e4-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="a11e4-166">Ahora escriba Hola todo en el nodo directorio y ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="a11e4-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="a11e4-167">Hello front-end de la aplicación web se está ejecutando ahora, sin embargo, es un paso más poder tener acceso aplicación hello desde un explorador web.</span><span class="sxs-lookup"><span data-stu-id="a11e4-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="a11e4-168">Hello máquina virtual que creó protegida por un recurso de Azure llama un *grupo de seguridad de red*, que se creó para que al aprovisionar Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a11e4-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="a11e4-169">Actualmente, este recurso sólo permite las solicitudes externas tooport toobe 22 enrutan toohello máquina virtual, que permite la comunicación de SSH con máquina Hola pero nada más.</span><span class="sxs-lookup"><span data-stu-id="a11e4-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="a11e4-170">Por tanto, Hola de orden tooview aplicación de lista de tareas, que es toorun configurado en el puerto 8080, este puerto también debe toobe añadido.</span><span class="sxs-lookup"><span data-stu-id="a11e4-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="a11e4-171">Devolver toohello Portal de Azure y complete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a11e4-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="a11e4-172">Haga clic en "Grupos de recursos" en la barra de navegación izquierdo de hello;</span><span class="sxs-lookup"><span data-stu-id="a11e4-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="a11e4-173">Seleccionar grupo de recursos de Hola que contiene la máquina virtual;</span><span class="sxs-lookup"><span data-stu-id="a11e4-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="a11e4-174">En la lista resultante de Hola de recursos, seleccione el grupo de seguridad de red de hello (Hola uno con un icono de escudo);</span><span class="sxs-lookup"><span data-stu-id="a11e4-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="a11e4-175">En Propiedades de hello, elija "las reglas de seguridad de entrada";</span><span class="sxs-lookup"><span data-stu-id="a11e4-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="a11e4-176">En la barra de herramientas de hello, haga clic en "Agregar";</span><span class="sxs-lookup"><span data-stu-id="a11e4-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="a11e4-177">Especifique un nombre como "default-allow-todo".</span><span class="sxs-lookup"><span data-stu-id="a11e4-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="a11e4-178">Establecer el protocolo de hello demasiado "TCP";</span><span class="sxs-lookup"><span data-stu-id="a11e4-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="a11e4-179">Establecer el intervalo de puertos de destino de hello demasiado "8080;"</span><span class="sxs-lookup"><span data-stu-id="a11e4-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="a11e4-180">Haga clic en Aceptar y espere toobe de regla de seguridad de hello creado.</span><span class="sxs-lookup"><span data-stu-id="a11e4-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="a11e4-181">Después de crear esta regla de seguridad, Hola la aplicación de tareas está visible públicamente en internet de Hola y puede examinar tooit, por ejemplo mediante una dirección URL como:</span><span class="sxs-lookup"><span data-stu-id="a11e4-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="a11e4-182">Observará que, aunque aún no hemos configurado máquina virtual de hello MongoDB, Hola la aplicación de tareas aparece toobe muy funcional.</span><span class="sxs-lookup"><span data-stu-id="a11e4-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="a11e4-183">Esto es porque repositorio de código fuente de hello está codificado de forma rígida toouse una instancia de MongoDB previamente implementada.</span><span class="sxs-lookup"><span data-stu-id="a11e4-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="a11e4-184">Una vez que hemos configurado Hola MongoDB virtual machine, se le volver atrás y cambiar tooutilize de código de origen de hello nuestra instancia privada de MongoDB en su lugar.</span><span class="sxs-lookup"><span data-stu-id="a11e4-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="a11e4-185">Configuración de máquina Virtual de MongoDB Hola</span><span class="sxs-lookup"><span data-stu-id="a11e4-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="a11e4-186">SSH toohello segundo equipo que creó mediante PuTTY, ssh línea de comandos o la herramienta SSH prefiera.</span><span class="sxs-lookup"><span data-stu-id="a11e4-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="a11e4-187">Después de ver el mensaje de bienvenida de Hola y el símbolo del sistema, instale MongoDB (estas instrucciones se realizaron desde [aquí](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="a11e4-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="a11e4-188">De forma predeterminada, MongoDB está configurado para que solo se pueda acceder localmente.</span><span class="sxs-lookup"><span data-stu-id="a11e4-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="a11e4-189">Para este tutorial, se configurará MongoDB por lo que puede obtenerse de la máquina virtual de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a11e4-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="a11e4-190">En un contexto de sudo, abra hello /etc/mongod.conf archivo y busque hello `# network interfaces` sección.</span><span class="sxs-lookup"><span data-stu-id="a11e4-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="a11e4-191">Hola de cambio `net.bindIp` configuración valor demasiado`0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="a11e4-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="a11e4-192">Esta configuración es para fines de Hola de este tutorial solo.</span><span class="sxs-lookup"><span data-stu-id="a11e4-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="a11e4-193">**NO** constituye una práctica de seguridad recomendada y no se debe usar en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="a11e4-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="a11e4-194">Ahora asegúrese Hola MongoDB se ha iniciado el servicio:</span><span class="sxs-lookup"><span data-stu-id="a11e4-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="a11e4-195">MongoDB funciona a través del puerto 27017 de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a11e4-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="a11e4-196">Por lo tanto, en hello igual que necesitábamos tooopen el puerto 8080 en máquina virtual de hello web front-end, es necesario que el puerto de tooopen 27017 en la máquina virtual de hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a11e4-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="a11e4-197">Devolver toohello Portal de Azure y complete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a11e4-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="a11e4-198">Haga clic en "Grupos de recursos" en la barra de navegación izquierdo de hello;</span><span class="sxs-lookup"><span data-stu-id="a11e4-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="a11e4-199">Seleccionar grupo de recursos de Hola que contiene la máquina virtual de hello MongoDB;</span><span class="sxs-lookup"><span data-stu-id="a11e4-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="a11e4-200">En la lista resultante de Hola de recursos, seleccione el grupo de seguridad de red de hello (Hola uno con un icono de escudo) con el mismo nombre que se le asignó la máquina virtual de toohello MongoDB; de Hola</span><span class="sxs-lookup"><span data-stu-id="a11e4-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="a11e4-201">En Propiedades de hello, elija "las reglas de seguridad de entrada";</span><span class="sxs-lookup"><span data-stu-id="a11e4-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="a11e4-202">En la barra de herramientas de hello, haga clic en "Agregar";</span><span class="sxs-lookup"><span data-stu-id="a11e4-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="a11e4-203">Especifique un nombre como "default-allow-mongo".</span><span class="sxs-lookup"><span data-stu-id="a11e4-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="a11e4-204">Establecer el protocolo de hello demasiado "TCP";</span><span class="sxs-lookup"><span data-stu-id="a11e4-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="a11e4-205">Establecer el intervalo de puertos de destino de hello demasiado "27017;"</span><span class="sxs-lookup"><span data-stu-id="a11e4-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="a11e4-206">Haga clic en Aceptar y espere toobe de regla de seguridad de hello creado.</span><span class="sxs-lookup"><span data-stu-id="a11e4-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="a11e4-207">Iterar en hello aplicación de lista de tareas</span><span class="sxs-lookup"><span data-stu-id="a11e4-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="a11e4-208">Hasta ahora, hemos proporcionamos dos máquinas virtuales de Linux: uno que ejecuta la aplicación hello front-end web y otra que esté ejecutando una instancia de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a11e4-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="a11e4-209">Pero hay un problema: front-end web de hello no es realmente Hola aprovisionado MongoDB instancia todavía utiliza.</span><span class="sxs-lookup"><span data-stu-id="a11e4-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="a11e4-210">Vamos a solucionar esto mediante la actualización de hello web front-end código toouse una variable de entorno en lugar de una instancia codificados de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="a11e4-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="a11e4-211">Cambio de la aplicación hello tareas</span><span class="sxs-lookup"><span data-stu-id="a11e4-211">Changing hello TODO application</span></span>
<span data-ttu-id="a11e4-212">En el equipo de desarrollo donde clonó repositorio todo en el nodo de Hola por primera vez, abra hello `node-todo/config/database.js` un archivo en su editor favorito y cambie el valor de dirección url de Hola de valor codificado de forma rígida de hello como `mongodb://...` demasiado`process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="a11e4-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="a11e4-213">Confirme los cambios e inserte a toohello GitHub master:</span><span class="sxs-lookup"><span data-stu-id="a11e4-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="a11e4-214">Lamentablemente, esto no publica máquina virtual del Hola cambio toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="a11e4-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="a11e4-215">Vamos a hacer un mecanismo simple pero eficaz para la publicación de actualizaciones para que pueda observar rápidamente efecto Hola de cambios de hello en el entorno activo de hello unos más cambios toothat máquina virtual tooenable.</span><span class="sxs-lookup"><span data-stu-id="a11e4-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="a11e4-216">Configuración de máquina Virtual del servidor front-end Web de Hola</span><span class="sxs-lookup"><span data-stu-id="a11e4-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="a11e4-217">Recuerde que creamos previamente un clon reconstrucción del repositorio de todo en el nodo de hello en la máquina virtual de hello web front-end.</span><span class="sxs-lookup"><span data-stu-id="a11e4-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="a11e4-218">Esto resulta que esta acción crea un nuevo Git remoto toowhich cambios se pueden insertar.</span><span class="sxs-lookup"><span data-stu-id="a11e4-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="a11e4-219">Sin embargo, simplemente insertar toothis remoto no proporciona bastante modelo del iteración rápida de Hola que están buscando los programadores al trabajar en su código.</span><span class="sxs-lookup"><span data-stu-id="a11e4-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="a11e4-220">Lo que nos gustaría toobe capaz de toodo es asegurarse de que cuando se produce un repositorio remoto de toohello de inserción en la máquina virtual de hello, ejecución de la aplicación tareas Hola se actualiza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a11e4-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="a11e4-221">Afortunadamente, esto es fácil tooachieve con git.</span><span class="sxs-lookup"><span data-stu-id="a11e4-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="a11e4-222">GIT expone una serie de enlaces que se denominan a veces determinado tooreact tooactions realizadas en el repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a11e4-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="a11e4-223">Se especifican mediante secuencias de comandos de shell en el repositorio de hello `hooks` carpeta.</span><span class="sxs-lookup"><span data-stu-id="a11e4-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="a11e4-224">enlace de Hola que es más apropiado para el escenario de actualización automática de hello es hello `post-update` eventos.</span><span class="sxs-lookup"><span data-stu-id="a11e4-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="a11e4-225">En una máquina de virtual SSH sesión toohello web front-end, cambie toohello `~/node-todo.git/hooks` directorio y agregue Hola siguiente con el nombre el archivo de contenido tooa `post-update` (reemplazando `machinename` y `region` con la información de la máquina virtual de MongoDB):</span><span class="sxs-lookup"><span data-stu-id="a11e4-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="a11e4-226">Asegúrese de que este archivo es ejecutable ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a11e4-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="a11e4-227">Este script se asegura de que se detiene la aplicación de servidor actual de hello, código de hello en el repositorio clonado hello es toohello actualizada más reciente, se cumplen todas las dependencias actualizadas y se reinicia el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="a11e4-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="a11e4-228">También se asegura de que ese entorno Hola se ha configurado en preparación para recibir la primera instancia de aplicación actualización tooget Hola MongoDB de una variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="a11e4-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="a11e4-229">Configuración de la máquina de desarrollo</span><span class="sxs-lookup"><span data-stu-id="a11e4-229">Configuring your Development Machine</span></span>
<span data-ttu-id="a11e4-230">Ahora vamos a su equipo de desarrollo enlazarse de máquina virtual de toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="a11e4-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="a11e4-231">Esto es tan simple como Agregar repositorio de reconstrucción de hello en la máquina virtual de Hola como un control remoto.</span><span class="sxs-lookup"><span data-stu-id="a11e4-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="a11e4-232">Ejecutar este ejemplo Hola siguiendo el comando toodo (reemplazando *usuario* con su nombre de inicio de sesión de máquina virtual de front-end web y *machinename* y *región* según corresponda):</span><span class="sxs-lookup"><span data-stu-id="a11e4-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="a11e4-233">Esto es todo lo que es necesario tooenable insertar o publicar en vigor, cambios de máquina virtual de toohello web front-end.</span><span class="sxs-lookup"><span data-stu-id="a11e4-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="a11e4-234">Publicación de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="a11e4-234">Publishing Updates</span></span>
<span data-ttu-id="a11e4-235">Vamos a publicar el cambio de uno de Hola que se ha realizado hasta ahora para que la aplicación hello usará nuestra propia instancia de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="a11e4-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="a11e4-236">Debería ver toothis similar de salida:</span><span class="sxs-lookup"><span data-stu-id="a11e4-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="a11e4-237">Una vez completado este comando, pruebe a actualizar la aplicación hello en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="a11e4-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="a11e4-238">Debe ser capaz de toosee que lista de tareas de hello proporcionada en esta guía está vacía y ya no está enlazada toohello compartido implementado MongoDB instancia.</span><span class="sxs-lookup"><span data-stu-id="a11e4-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="a11e4-239">tutorial de hello toocomplete, vamos a hacer más visible, otro cambio.</span><span class="sxs-lookup"><span data-stu-id="a11e4-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="a11e4-240">En el equipo de desarrollo, abra el archivo de node-todo/public/index.html de hello con su editor favorito.</span><span class="sxs-lookup"><span data-stu-id="a11e4-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="a11e4-241">Localizar hello jumbotron encabezado y cambie el título de Hola de "Soy una lista de tareas-aholic" demasiado "Soy un aholic Todo en Azure!".</span><span class="sxs-lookup"><span data-stu-id="a11e4-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="a11e4-242">Ahora vamos a confirmarlo:</span><span class="sxs-lookup"><span data-stu-id="a11e4-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="a11e4-243">Esta vez, vamos a publicar hello tooAzure de cambio antes de insertar repositorio de GitHub de tooback toohello:</span><span class="sxs-lookup"><span data-stu-id="a11e4-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="a11e4-244">Una vez completado este comando, página web de actualización de Hola y verá cambios Hola.</span><span class="sxs-lookup"><span data-stu-id="a11e4-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="a11e4-245">Puesto que se muestren correctamente, push Hola cambio toohello atrás origen remoto:</span><span class="sxs-lookup"><span data-stu-id="a11e4-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="a11e4-246">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a11e4-246">Next Steps</span></span>
<span data-ttu-id="a11e4-247">En este artículo ha explicado cómo tootake una aplicación Node.js e implementar máquinas virtuales de tooLinux ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="a11e4-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="a11e4-248">toolearn más información acerca de máquinas virtuales de Linux en Azure, consulte [tooLinux de introducción en Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="a11e4-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="a11e4-249">Para obtener más información acerca de cómo toodevelop las aplicaciones Node.js en Azure, vea hello [Centro para desarrolladores de Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="a11e4-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

