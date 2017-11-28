---
title: "Implementación de una aplicación Node.js para máquinas virtuales de Linux en Azure"
description: "Aprenda a implementar una aplicación Node.js en las máquinas virtuales Linux en Azure."
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
ms.openlocfilehash: d3d9fecfafb9ba422420230716b9c985481d1e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-nodejs-application-to-linux-virtual-machines-in-azure"></a><span data-ttu-id="fe462-103">Implementación de una aplicación Node.js para máquinas virtuales de Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="fe462-103">Deploy a Node.js application to Linux Virtual Machines in Azure</span></span>
<span data-ttu-id="fe462-104">Este tutorial muestra cómo implementar una aplicación Node.js en máquinas virtuales Linux que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="fe462-104">This tutorial shows how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="fe462-105">Las instrucciones de este tutorial se pueden seguir en cualquier sistema operativo que sea capaz de ejecutar Node.js.</span><span class="sxs-lookup"><span data-stu-id="fe462-105">The instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="fe462-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="fe462-106">You'll learn how to:</span></span>

* <span data-ttu-id="fe462-107">Bifurcar y clonar un repositorio de GitHub con una aplicación simple de tarea pendiente</span><span class="sxs-lookup"><span data-stu-id="fe462-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="fe462-108">Crear y configurar dos máquinas virtuales Linux en Azure para ejecutar la aplicación</span><span class="sxs-lookup"><span data-stu-id="fe462-108">Create and configure two Linux virtual machines in Azure to run the application;</span></span>
* <span data-ttu-id="fe462-109">Efectuar iteraciones en la aplicación enviando actualizaciones a la máquina virtual front-end web</span><span class="sxs-lookup"><span data-stu-id="fe462-109">Iterate on the application by pushing updates to the web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="fe462-110">Para realizar este tutorial, necesita una cuenta de GitHub y una de Microsoft Azure, además de la posibilidad de usar Git desde una máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="fe462-110">To complete this tutorial, you need a GitHub account and a Microsoft Azure account, and the ability to use Git from a development machine.</span></span>
> 
> <span data-ttu-id="fe462-111">Si no tiene cuenta de GitHub, puede suscribirse para obtener una gratis [aquí](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="fe462-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="fe462-112">Si no tiene una cuenta de [Microsoft Azure](https://azure.microsoft.com/), puede registrarse para obtener una evaluación gratuita [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe462-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="fe462-113">Esto le llevará también a través del proceso de inicio de sesión una [cuenta de Microsoft](http://account.microsoft.com) , en caso de que no disponga de una.</span><span class="sxs-lookup"><span data-stu-id="fe462-113">This will also lead you through the sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="fe462-114">Como alternativa, si tiene una suscripción de Visual Studio, puede [activar los beneficios de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fe462-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="fe462-115">Si no tiene Git en la máquina de desarrollo y está utilizando un equipo Macintosh o Windows, instale Git desde [aquí](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="fe462-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="fe462-116">Si usa Linux, instale Git mediante el mecanismo más adecuado para usted, como `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="fe462-116">If you are using Linux, install git using the mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-the-todo-application"></a><span data-ttu-id="fe462-117">Bifurcación y clonación de la aplicación de tareas pendientes</span><span class="sxs-lookup"><span data-stu-id="fe462-117">Forking and Cloning the TODO Application</span></span>
<span data-ttu-id="fe462-118">La aplicación de tareas pendientes que se usa en este tutorial permite implementar un front-end web sencillo en una instancia de MongoDB que realiza un seguimiento de una lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="fe462-118">The TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="fe462-119">Después de iniciar sesión en GitHub, vaya [aquí](https://github.com/stepro/node-todo) para buscar la aplicación y bifurcarla mediante el vínculo en la parte superior derecha.</span><span class="sxs-lookup"><span data-stu-id="fe462-119">After signing in to GitHub, go [here](https://github.com/stepro/node-todo) to find the application and fork it using the link in the top right.</span></span> <span data-ttu-id="fe462-120">Esto debería crear un repositorio en la cuenta con el nombre *accountname*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="fe462-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="fe462-121">Ahora en la máquina de desarrollo, clone este repositorio:</span><span class="sxs-lookup"><span data-stu-id="fe462-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="fe462-122">Usaremos este clon local del repositorio un poco más adelante al realizar cambios en el código fuente.</span><span class="sxs-lookup"><span data-stu-id="fe462-122">We'll use this local clone of the repository a little later when making changes to the source code.</span></span>

## <a name="creating-and-configuring-the-linux-virtual-machines"></a><span data-ttu-id="fe462-123">Creación y configuración de las máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="fe462-123">Creating and Configuring the Linux Virtual Machines</span></span>
<span data-ttu-id="fe462-124">Azure ofrece un buen soporte para los procesos sin formato con las máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="fe462-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="fe462-125">Esta parte del tutorial muestra la forma de establecer fácilmente dos máquinas virtuales de Linux e implementar la aplicación de tareas pendientes, ejecutando el front-end web en una de ellas y la instancia de MongoDB en la otra.</span><span class="sxs-lookup"><span data-stu-id="fe462-125">This part of the tutorial shows how you can easily spin up two Linux virtual machines and deploy the TODO application to them, running the web frontend on one and the MongoDB instance on the other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="fe462-126">Creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fe462-126">Creating Virtual Machines</span></span>
<span data-ttu-id="fe462-127">Para crear una nueva máquina virtual en Azure, lo más sencillo es usar el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe462-127">The easiest way to create a new virtual machine in Azure is to use the Azure Portal.</span></span> <span data-ttu-id="fe462-128">Haga clic en [aquí](https://portal.azure.com) para conectarse e iniciar el Portal de Azure en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="fe462-128">Click [here](https://portal.azure.com) to sign in and launch the Azure Portal in your web browser.</span></span> <span data-ttu-id="fe462-129">Cuando se haya cargado el Portal de Azure, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fe462-129">Once the Azure Portal has loaded, complete the following steps:</span></span>

* <span data-ttu-id="fe462-130">Haga clic en el vínculo "+ Nuevo".</span><span class="sxs-lookup"><span data-stu-id="fe462-130">Click the "+ New" link;</span></span>
* <span data-ttu-id="fe462-131">Elija la categoría "Proceso" y la opción "Ubuntu Server 14.04 LTS".</span><span class="sxs-lookup"><span data-stu-id="fe462-131">Pick the "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="fe462-132">Elija el modelo de implementación "Administrador de recursos" y haga clic en "Crear".</span><span class="sxs-lookup"><span data-stu-id="fe462-132">Select the "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="fe462-133">Para rellenar los aspectos básicos, siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="fe462-133">Fill in the basics following these guidelines:</span></span>
  * <span data-ttu-id="fe462-134">Especifique un nombre que pueda identificar fácilmente más tarde.</span><span class="sxs-lookup"><span data-stu-id="fe462-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="fe462-135">Para este tutorial, elija la autenticación mediante contraseña.</span><span class="sxs-lookup"><span data-stu-id="fe462-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="fe462-136">Cree un nuevo grupo de recursos con un nombre identificable.</span><span class="sxs-lookup"><span data-stu-id="fe462-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="fe462-137">Para el tamaño de la máquina virtual, "A1 estándar" es una buena opción para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fe462-137">For the Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="fe462-138">Para ver otras opciones, asegúrese de que el tipo de disco sea "Estándar" y acepte todos los valores predeterminados restantes.</span><span class="sxs-lookup"><span data-stu-id="fe462-138">For additional settings, ensure the disk type is "Standard" and accept all the remaining defaults.</span></span>
* <span data-ttu-id="fe462-139">Ponga en marcha la creación en la página de resumen.</span><span class="sxs-lookup"><span data-stu-id="fe462-139">Kick off the creation on the summary page.</span></span>

<span data-ttu-id="fe462-140">Realice el proceso anterior dos veces para crear dos máquinas virtuales Linux: una para el front-end web y otra para la instancia de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fe462-140">Perform the above process twice to create two Linux virtual machines, one for the web frontend and one for the MongoDB instance.</span></span> <span data-ttu-id="fe462-141">La creación de las máquinas virtuales tardará entre 5 y 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="fe462-141">Creation of the virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="fe462-142">Asignación de una entrada DNS para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fe462-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="fe462-143">De manera predeterminada, a las máquinas virtuales creadas en Azure se puede acceder solo a través de una dirección IP pública, como 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="fe462-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="fe462-144">Vamos a hacer que las máquinas se puedan identificar más fácilmente mediante la asignación de entradas de DNS.</span><span class="sxs-lookup"><span data-stu-id="fe462-144">Let's make the machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="fe462-145">Una vez que el portal indique que se han creado las máquinas virtuales, haga clic en el vínculo "Máquinas virtuales" en la barra de exploración izquierda y busque las máquinas.</span><span class="sxs-lookup"><span data-stu-id="fe462-145">Once the portal indicates that the virtual machines have been created, click on the "Virtual machines" link in the left navbar and locate your machines.</span></span> <span data-ttu-id="fe462-146">Para cada máquina:</span><span class="sxs-lookup"><span data-stu-id="fe462-146">For each machine:</span></span>

* <span data-ttu-id="fe462-147">Busque la pestaña Essentials y haga clic en la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="fe462-147">Locate the Essentials tab and click on the Public IP Address;</span></span>
* <span data-ttu-id="fe462-148">En la configuración de la dirección IP pública, asigne una etiqueta de nombre DNS y guárdela.</span><span class="sxs-lookup"><span data-stu-id="fe462-148">In the public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="fe462-149">El portal comprobará que el nombre especificado esté disponible.</span><span class="sxs-lookup"><span data-stu-id="fe462-149">The portal will ensure that the name you specify is available.</span></span> <span data-ttu-id="fe462-150">Después de guardar la configuración, las máquinas virtuales tendrán nombres de host similares a `machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="fe462-150">After saving the configuration, your virtual machines will have host names similar to `machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-to-the-virtual-machines"></a><span data-ttu-id="fe462-151">Conexión a las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fe462-151">Connecting to the Virtual Machines</span></span>
<span data-ttu-id="fe462-152">Al aprovisionar las máquinas virtuales, estas se configuraron para permitir las conexiones remotas a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="fe462-152">When your virtual machines were provisioned, they were pre-configured to allow remote connections over SSH.</span></span> <span data-ttu-id="fe462-153">Este es el mecanismo que se utilizará para configurar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fe462-153">This is the mechanism we will use to configure the virtual machines.</span></span> <span data-ttu-id="fe462-154">Si está utilizando Windows para el desarrollo, debe obtener un cliente SSH en caso de que no disponga de uno.</span><span class="sxs-lookup"><span data-stu-id="fe462-154">If you are using Windows for your development, you will need to get an SSH client if you do not already have one.</span></span> <span data-ttu-id="fe462-155">Una opción común es PuTTY, que puede descargar desde [aquí](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="fe462-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="fe462-156">Los sistemas operativos Macintosh y Linux vienen con una versión de SSH preinstalada.</span><span class="sxs-lookup"><span data-stu-id="fe462-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="fe462-157">Configuración de la máquina virtual front-end web</span><span class="sxs-lookup"><span data-stu-id="fe462-157">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="fe462-158">Inicie sesión con SSH en la máquina front-end web que creó mediante PuTTY, la línea de comandos ssh u otra herramienta SSH que desee.</span><span class="sxs-lookup"><span data-stu-id="fe462-158">SSH to the web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="fe462-159">Debería ver un mensaje de bienvenida seguido de un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="fe462-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="fe462-160">En primer lugar, debe asegurarse de que Git y el nodo estén instalados:</span><span class="sxs-lookup"><span data-stu-id="fe462-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="fe462-161">Puesto que el front-end web de la aplicación depende de algunos módulos Node.js nativos, también hay que instalar el conjunto esencial de herramientas de compilación:</span><span class="sxs-lookup"><span data-stu-id="fe462-161">Since the application's web frontend relies on some native Node.js modules, we also need to install the essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="fe462-162">Por último, vamos a instalar una aplicación Node.js denominada *forever*, que facilita la ejecución de aplicaciones del servidor Node.js:</span><span class="sxs-lookup"><span data-stu-id="fe462-162">Finally, let's install a Node.js application called *forever*, which helps to run Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="fe462-163">Estas son todas las dependencias que se necesitan en esta máquina virtual para poder ejecutar el front-end web de la aplicación, así que vamos a proceder con la ejecución.</span><span class="sxs-lookup"><span data-stu-id="fe462-163">These are all the dependencies needed on this virtual machine to be able to run the application's web frontend, so let's get that running.</span></span> <span data-ttu-id="fe462-164">Para ello, primero crearemos un clon básico del repositorio de GitHub que bifurcó previamente para que pueda publicar fácilmente las actualizaciones para la máquina virtual (explicaremos este escenario de actualización más adelante) y, a continuación, tendrá que clonar el clon básico para proporcionar una versión del repositorio que se pueda ejecutar realmente.</span><span class="sxs-lookup"><span data-stu-id="fe462-164">To do this, we will first create a bare clone of the GitHub repository you previously forked so that you can easily publish updates to the virtual machine (we'll cover this update scenario later), and then clone the bare clone to provide a version of the repository that can actually be executed.</span></span>

<span data-ttu-id="fe462-165">Desde el directorio particular (~), ejecute los siguientes comandos (reemplace *accountname* con su nombre de cuenta de usuario de GitHub):</span><span class="sxs-lookup"><span data-stu-id="fe462-165">Starting from the home (~) directory, run the following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="fe462-166">Ahora acceda al directorio node-todo y ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="fe462-166">Now enter the node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="fe462-167">El front-end web de la aplicación se está ejecutando ahora, sin embargo hay que realizar un paso más antes de que se pueda acceder a la aplicación desde un explorador web.</span><span class="sxs-lookup"><span data-stu-id="fe462-167">The application's web frontend is now running, however there is one more step before you can access the application from a web browser.</span></span> <span data-ttu-id="fe462-168">La máquina virtual que creó está protegida por un recurso de Azure denominado *grupo de seguridad de red*, que se creó al aprovisionar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe462-168">The virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned the virtual machine.</span></span> <span data-ttu-id="fe462-169">Actualmente, este recurso solo permite que las solicitudes externas al puerto 22 se enruten a la máquina virtual, lo que permite la comunicación SSH con la máquina, pero nada más.</span><span class="sxs-lookup"><span data-stu-id="fe462-169">Currently, this resource only allows external requests to port 22 to be routed to the virtual machine, which enables SSH communication with the machine but nothing else.</span></span> <span data-ttu-id="fe462-170">Por tanto, para poder ver la aplicación de tareas pendientes, que está configurada para ejecutarse en el puerto 8080, este puerto también debe estar abierto.</span><span class="sxs-lookup"><span data-stu-id="fe462-170">So in order to view the TODO application, which is configured to run on port 8080, this port also needs to be opened up.</span></span>

<span data-ttu-id="fe462-171">Vuelva al Portal de Azure y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fe462-171">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="fe462-172">Haga clic en "Grupos de recursos", en la barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="fe462-172">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="fe462-173">Elija el grupo de recursos que contiene la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe462-173">Select the resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="fe462-174">En la lista resultante de recursos, elija el grupo de seguridad de red (el que tiene un icono de escudo).</span><span class="sxs-lookup"><span data-stu-id="fe462-174">In the resulting list of resources, select the network security group (the one with a shield icon);</span></span>
* <span data-ttu-id="fe462-175">En las propiedades, elija "Reglas de seguridad de entrada".</span><span class="sxs-lookup"><span data-stu-id="fe462-175">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="fe462-176">En la barra de herramientas, haga clic en "Agregar".</span><span class="sxs-lookup"><span data-stu-id="fe462-176">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="fe462-177">Especifique un nombre como "default-allow-todo".</span><span class="sxs-lookup"><span data-stu-id="fe462-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="fe462-178">Configure el protocolo como "TCP".</span><span class="sxs-lookup"><span data-stu-id="fe462-178">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="fe462-179">Defina el intervalo de puertos de destino en "8080".</span><span class="sxs-lookup"><span data-stu-id="fe462-179">Set the destination port range to "8080";</span></span>
* <span data-ttu-id="fe462-180">Haga clic en Aceptar y espere a que se cree la regla de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fe462-180">Click OK and wait for the security rule to be created.</span></span>

<span data-ttu-id="fe462-181">Después de crear esta regla de seguridad, la aplicación de lista de tareas estará visible públicamente en Internet y podrá acceder a ella, por ejemplo, mediante una dirección URL como:</span><span class="sxs-lookup"><span data-stu-id="fe462-181">After creating this security rule, the TODO application is publically visible on the internet and you can browse to it, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="fe462-182">Observará que, aunque todavía no hemos configurado la máquina virtual de MongoDB, la aplicación de tarea pendiente parece ser bastante funcional.</span><span class="sxs-lookup"><span data-stu-id="fe462-182">You will notice that even though we have not yet configured the MongoDB virtual machine, the TODO application appears to be quite functional.</span></span> <span data-ttu-id="fe462-183">Esto es porque el repositorio de origen está codificado para usar una instancia de MongoDB implementada previamente.</span><span class="sxs-lookup"><span data-stu-id="fe462-183">This is because the source repository is hardcoded to use a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="fe462-184">Una vez que hemos configurado la máquina virtual de MongoDB, volvemos y cambiamos el código fuente para nuestra instancia de MongoDB privada en su lugar.</span><span class="sxs-lookup"><span data-stu-id="fe462-184">Once we have configured the MongoDB virtual machine, we will go back and change the source code to utilize our private MongoDB instance instead.</span></span>

### <a name="configuring-the-mongodb-virtual-machine"></a><span data-ttu-id="fe462-185">Configuración de la máquina virtual de MongoDB</span><span class="sxs-lookup"><span data-stu-id="fe462-185">Configuring the MongoDB Virtual Machine</span></span>
<span data-ttu-id="fe462-186">Inicie sesión con SSH en la segunda máquina que creó mediante PuTTY, la línea de comandos ssh u otra herramienta SSH que desee.</span><span class="sxs-lookup"><span data-stu-id="fe462-186">SSH to the second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="fe462-187">Después de ver el mensaje de bienvenida y el símbolo del sistema, instale MongoDB (estas instrucciones proceden de [aquí](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="fe462-187">After seeing the welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="fe462-188">De forma predeterminada, MongoDB está configurado para que solo se pueda acceder localmente.</span><span class="sxs-lookup"><span data-stu-id="fe462-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="fe462-189">Para este tutorial, configuraremos MongoDB para que se pueda acceder desde la máquina virtual de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fe462-189">For this tutorial, we will configure MongoDB so it can be accessed from the application's virtual machine.</span></span> <span data-ttu-id="fe462-190">En un contexto sudo, abra el archivo /etc/mongod.conf y busque la sección `# network interfaces` .</span><span class="sxs-lookup"><span data-stu-id="fe462-190">In a sudo context, open the /etc/mongod.conf file and locate the `# network interfaces` section.</span></span> <span data-ttu-id="fe462-191">Cambie el valor de la configuración `net.bindIp` por `0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="fe462-191">Change the `net.bindIp` configuration value to `0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="fe462-192">Esta configuración atiende solo a los fines de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fe462-192">This configuration is for the purposes of this tutorial only.</span></span> <span data-ttu-id="fe462-193">**NO** constituye una práctica de seguridad recomendada y no se debe usar en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="fe462-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="fe462-194">Ahora, asegúrese de que el servicio MongoDB se haya iniciado:</span><span class="sxs-lookup"><span data-stu-id="fe462-194">Now ensure the MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="fe462-195">MongoDB funciona a través del puerto 27017 de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fe462-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="fe462-196">Por lo tanto, de la misma manera que había que abrir el puerto 8080 en la máquina virtual front-end web, ahora hay que abrir el puerto 27017 en la máquina virtual de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fe462-196">So, in the same way that we needed to open port 8080 on the web frontend virtual machine, we need to open port 27017 on the MongoDB virtual machine.</span></span>

<span data-ttu-id="fe462-197">Vuelva al Portal de Azure y siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fe462-197">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="fe462-198">Haga clic en "Grupos de recursos", en la barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="fe462-198">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="fe462-199">Elija el grupo de recursos que contiene la máquina virtual MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fe462-199">Select the resource group that contains the MongoDB virtual machine;</span></span>
* <span data-ttu-id="fe462-200">En la lista resultante de recursos, elija el grupo de seguridad de red (el que tiene un icono de escudo) con el mismo nombre que asignó a la máquina virtual MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fe462-200">In the resulting list of resources, select the network security group (the one with a shield icon) with the same name that you gave to the MongoDB virtual machine;</span></span>
* <span data-ttu-id="fe462-201">En las propiedades, elija "Reglas de seguridad de entrada".</span><span class="sxs-lookup"><span data-stu-id="fe462-201">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="fe462-202">En la barra de herramientas, haga clic en "Agregar".</span><span class="sxs-lookup"><span data-stu-id="fe462-202">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="fe462-203">Especifique un nombre como "default-allow-mongo".</span><span class="sxs-lookup"><span data-stu-id="fe462-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="fe462-204">Configure el protocolo como "TCP".</span><span class="sxs-lookup"><span data-stu-id="fe462-204">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="fe462-205">Defina el intervalo de puertos de destino en "27017".</span><span class="sxs-lookup"><span data-stu-id="fe462-205">Set the destination port range to "27017";</span></span>
* <span data-ttu-id="fe462-206">Haga clic en Aceptar y espere a que se cree la regla de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fe462-206">Click OK and wait for the security rule to be created.</span></span>

## <a name="iterating-on-the-todo-application"></a><span data-ttu-id="fe462-207">Iteración en la aplicación de tareas pendientes</span><span class="sxs-lookup"><span data-stu-id="fe462-207">Iterating on the TODO application</span></span>
<span data-ttu-id="fe462-208">Hasta ahora, hemos aprovisionado dos máquinas virtuales Linux: una que ejecuta el front-end web de la aplicación y otra que ejecuta una instancia de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fe462-208">So far, we have provisioned two Linux virtual machines: one that is running the application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="fe462-209">Pero hay un problema: el front-end web no está utilizando realmente la instancia de MongoDB aprovisionada todavía.</span><span class="sxs-lookup"><span data-stu-id="fe462-209">But there is a problem - the web frontend isn't actually using the provisioned MongoDB instance yet.</span></span> <span data-ttu-id="fe462-210">Para solucionar esto, vamos a actualizar el código de front-end web para utilizar una variable de entorno en lugar de una instancia codificada de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="fe462-210">Let's fix that by updating the web frontend code to use an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-the-todo-application"></a><span data-ttu-id="fe462-211">Cambio de la aplicación de tareas pendientes</span><span class="sxs-lookup"><span data-stu-id="fe462-211">Changing the TODO application</span></span>
<span data-ttu-id="fe462-212">En la máquina de desarrollo donde clonó primero el repositorio node-todo, abra el archivo `node-todo/config/database.js` en el editor que desee y cambie el valor de la dirección URL del valor codificado de forma rígida como `mongodb://...` por `process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="fe462-212">On your development machine where you first cloned the node-todo repository, open the `node-todo/config/database.js` file in your favorite editor and change the url value from the hard-coded value like `mongodb://...` to `process.env.MONGODB`.</span></span>

<span data-ttu-id="fe462-213">Confirme los cambios y distribúyalos al patrón de GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe462-213">Commit your changes and push to the GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="fe462-214">Desafortunadamente, con esta acción no se publica el cambio en la máquina virtual front-end web.</span><span class="sxs-lookup"><span data-stu-id="fe462-214">Unfortunately, this doesn't publish the change to the web frontend virtual machine.</span></span> <span data-ttu-id="fe462-215">Vamos a hacer algunos cambios más en esa máquina virtual para habilitar un mecanismo sencillo pero eficaz con el que publicar las actualizaciones, de forma que pueda observar rápidamente el efecto de los cambios en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fe462-215">Let's make a few more changes to that virtual machine to enable a simple but effective mechanism for publishing updates so you can quickly observe the effect of the changes in the live environment.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="fe462-216">Configuración de la máquina virtual front-end web</span><span class="sxs-lookup"><span data-stu-id="fe462-216">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="fe462-217">Recuerde que hemos creado previamente un clon básico del repositorio node-todo en la máquina virtual front-end web.</span><span class="sxs-lookup"><span data-stu-id="fe462-217">Recall that we previously created a bare clone of the node-todo repository on the web frontend virtual machine.</span></span> <span data-ttu-id="fe462-218">Resulta que esta acción crea un nuevo Git remoto en el que se pueden insertar los cambios.</span><span class="sxs-lookup"><span data-stu-id="fe462-218">It turns out that this action created a new Git remote to which changes can be pushed.</span></span> <span data-ttu-id="fe462-219">Sin embargo, el hecho de realizar inserciones en este elemento remoto no ofrece el modelo de iteración rápido que necesitan los desarrolladores al trabajar con el código.</span><span class="sxs-lookup"><span data-stu-id="fe462-219">However, simply pushing to this remote doesn't quite give the rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="fe462-220">Lo que nos gustaría es que, al realizar una inserción en el repositorio remoto en la máquina virtual, la aplicación de tareas pendientes en ejecución se actualizara automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fe462-220">What we would like to be able to do is ensure that when a push to the remote repository on the virtual machine occurs, the running TODO application is automatically updated.</span></span> <span data-ttu-id="fe462-221">Por suerte, esto es fácil de conseguir con Git.</span><span class="sxs-lookup"><span data-stu-id="fe462-221">Fortunately, this is easy to achieve with git.</span></span>

<span data-ttu-id="fe462-222">Git ofrece una serie de enlaces que se ejecutan en momentos concretos para reaccionar ante las acciones realizadas en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="fe462-222">Git exposes a number of hooks that are called at particular times to react to actions taken on the repository.</span></span> <span data-ttu-id="fe462-223">Estas acciones se ejecutan mediante scripts de shell en la carpeta `hooks` del repositorio.</span><span class="sxs-lookup"><span data-stu-id="fe462-223">These are specified using shell scripts in the repository's `hooks` folder.</span></span> <span data-ttu-id="fe462-224">El enlace que es más aplicable para el escenario de actualización automática es el evento `post-update` .</span><span class="sxs-lookup"><span data-stu-id="fe462-224">The hook that is most applicable for the auto-update scenario is the `post-update` event.</span></span>

<span data-ttu-id="fe462-225">En una sesión SSH para la máquina virtual front-end web, cambie al directorio `~/node-todo.git/hooks` y agregue el siguiente contenido a un archivo denominado `post-update` (sustituya `machinename` y `region` por la información de la máquina virtual de MongoDB):</span><span class="sxs-lookup"><span data-stu-id="fe462-225">In a SSH session to the web frontend virtual machine, change to the `~/node-todo.git/hooks` directory and add the following content to a file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="fe462-226">Asegúrese de que este archivo sea ejecutable mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe462-226">Ensure this file is executable by running the following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="fe462-227">Este script garantiza que la aplicación de servidor actual se haya detenido, que el código del repositorio clonado se haya actualizado a la versión más reciente, que se cumplan las dependencias actualizadas y que se reinicie el servidor.</span><span class="sxs-lookup"><span data-stu-id="fe462-227">This script ensures that the current server application is stopped, the code in the cloned repository is updated to the latest, any updated dependencies are satisfied, and the server is restarted.</span></span> <span data-ttu-id="fe462-228">También garantiza que se haya configurado el entorno para recibir nuestra primera actualización de la aplicación para obtener la instancia de MongoDB desde una variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="fe462-228">It also ensures that the environment has been configured in preparation for receiving our first application update to get the MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="fe462-229">Configuración de la máquina de desarrollo</span><span class="sxs-lookup"><span data-stu-id="fe462-229">Configuring your Development Machine</span></span>
<span data-ttu-id="fe462-230">Ahora vamos a obtener el equipo de desarrollo con un enlace a la máquina virtual front-end web.</span><span class="sxs-lookup"><span data-stu-id="fe462-230">Now let's get your development machine hooked up to the web frontend virtual machine.</span></span> <span data-ttu-id="fe462-231">Esto es tan sencillo como agregar el repositorio básico a la máquina virtual como un equipo remoto.</span><span class="sxs-lookup"><span data-stu-id="fe462-231">This is as simple as adding the bare repository on the virtual machine as a remote.</span></span> <span data-ttu-id="fe462-232">Para ello, ejecute el siguiente comando (sustituya *user* por el nombre de inicio de sesión de la máquina virtual front-end web y especifique lo que proceda en *machinename* y *region*):</span><span class="sxs-lookup"><span data-stu-id="fe462-232">Run the following command to do this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="fe462-233">Esto es todo lo que se necesita para habilitar la inserción (o, en realidad, la publicación) de cambios en la máquina virtual front-end web.</span><span class="sxs-lookup"><span data-stu-id="fe462-233">This is all that is needed to enable pushing, or in effect publishing, changes to the web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="fe462-234">Publicación de actualizaciones</span><span class="sxs-lookup"><span data-stu-id="fe462-234">Publishing Updates</span></span>
<span data-ttu-id="fe462-235">Vamos a publicar el único cambio que se ha hecho hasta el momento, de forma que la aplicación usará nuestra instancia MongoDB:</span><span class="sxs-lookup"><span data-stu-id="fe462-235">Let's publish the one change that has been made so far so that the application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="fe462-236">Debería mostrarse una salida similar a esta:</span><span class="sxs-lookup"><span data-stu-id="fe462-236">You should see output similar to this:</span></span>

    Counting objects: 4, done.
    Delta compression using up to 4 threads.
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
    To username@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="fe462-237">Una vez finalizado este comando, actualice la aplicación en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="fe462-237">After this command completes, try refreshing the application in a web browser.</span></span> <span data-ttu-id="fe462-238">Podrá ver que la lista de tareas pendientes que se muestra aquí está vacía y ya no está enlazada a la instancia de MongoDB implementada compartida.</span><span class="sxs-lookup"><span data-stu-id="fe462-238">You should be able to see that the TODO list presented here is empty and no longer tied to the shared deployed MongoDB instance.</span></span>

<span data-ttu-id="fe462-239">Para completar el tutorial, vamos a hacer otro cambio más visible.</span><span class="sxs-lookup"><span data-stu-id="fe462-239">To complete the tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="fe462-240">En la máquina de desarrollo, abra el archivo node-todo/public/index.html con el editor que desee.</span><span class="sxs-lookup"><span data-stu-id="fe462-240">On your development machine, open the node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="fe462-241">Busque el encabezado jumbotron y cambie el título de "I'm a Todo-aholic" a "I'm a Todo-aholic on Azure!".</span><span class="sxs-lookup"><span data-stu-id="fe462-241">Locate the jumbotron header and change  the title from "I'm a Todo-aholic" to "I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="fe462-242">Ahora vamos a confirmarlo:</span><span class="sxs-lookup"><span data-stu-id="fe462-242">Now let's commit:</span></span>

    git commit -am "Azurify the title"

<span data-ttu-id="fe462-243">Esta vez, vamos a publicar el cambio en Azure antes de insertarlo en el repositorio de GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe462-243">This time, let's publish the change to Azure before pushing it to back to the GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="fe462-244">Una vez finalizado este comando, actualice la página web y verá los cambios.</span><span class="sxs-lookup"><span data-stu-id="fe462-244">Once this command completes, refresh the web page and you will see the changes.</span></span> <span data-ttu-id="fe462-245">Como el resultado es satisfactorio, inserte el cambio en el origen remoto:</span><span class="sxs-lookup"><span data-stu-id="fe462-245">Since they look good, push the change back to the origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="fe462-246">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe462-246">Next Steps</span></span>
<span data-ttu-id="fe462-247">En este artículo, hemos explicado cómo implementar una aplicación Node.js en máquinas virtuales Linux que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="fe462-247">This article showed how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="fe462-248">Para obtener más información acerca de las máquinas virtuales de Linux en Azure, consulte [Introducción a Linux en Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="fe462-248">To learn more about Linux virtual machines in Azure, see [Introduction to Linux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="fe462-249">Para más información sobre cómo desarrollar aplicaciones de Node.js en Azure, consulte el [Centro para desarrolladores de Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="fe462-249">For more information about how to develop Node.js applications on Azure, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

