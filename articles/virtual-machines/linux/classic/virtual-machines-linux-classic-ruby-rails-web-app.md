---
title: "aaaHost un Ruby en el sitio Web de raíles en una VM Linux | Documentos de Microsoft"
description: "Configure y hospede un sitio web basado en Ruby on Rails en Azure usando una máquina virtual de Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="a7ac0-103">Aplicación web de Ruby on Rails en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="a7ac0-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="a7ac0-104">Este tutorial se muestra cómo toohost un Ruby en el sitio Web de raíles en Azure con una máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="a7ac0-105">Este tutorial se validó con Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="a7ac0-106">Si utiliza una distribución de Linux diferente, tendrá que toomodify Hola pasos tooinstall raíles.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7ac0-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a7ac0-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a7ac0-108">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="a7ac0-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="a7ac0-110">Creación de una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="a7ac0-110">Create an Azure VM</span></span>
<span data-ttu-id="a7ac0-111">Empiece por crear una máquina virtual de Azure con una imagen de Linux.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="a7ac0-112">toocreate Hola VM, puede usar hello portal de Azure u Hola interfaz de línea de comandos (CLI) de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a7ac0-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a7ac0-113">Azure portal</span></span>
1. <span data-ttu-id="a7ac0-114">Inicio de sesión en hello [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a7ac0-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="a7ac0-115">Haga clic en **nuevo**, a continuación, escriba "Ubuntu Server 14.04" en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="a7ac0-116">Haga clic en la entrada Hola devuelto por la búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="a7ac0-117">Para el modelo de implementación de hello, seleccione **clásico**, a continuación, haga clic en "Crear".</span><span class="sxs-lookup"><span data-stu-id="a7ac0-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="a7ac0-118">En la hoja de conceptos básicos de hello, proporcionar valores para campos de hello necesaria: nombre (para Hola VM), nombre de usuario, tipo de autenticación y las credenciales correspondientes de hello, suscripción de Azure, grupo de recursos y ubicación.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Creación de una imagen Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="a7ac0-120">Después de aprovisiona Hola VM, haga clic en el nombre de la máquina virtual de Hola y haga clic en **extremos** en hello **configuración** categoría.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="a7ac0-121">Buscar el punto de conexión SSH de hello, aparecen en **independiente**.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Punto de conexión predeterminado](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="a7ac0-123">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a7ac0-123">Azure CLI</span></span>
<span data-ttu-id="a7ac0-124">Siga los pasos de hello en [crear una máquina Virtual ejecuta Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="a7ac0-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="a7ac0-125">Después de aprovisiona Hola VM, puede obtener el punto de conexión de hello SSH ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="a7ac0-126">Instalación de Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="a7ac0-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="a7ac0-127">Utilizar SSH tooconnect toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="a7ac0-128">Desde la sesión de SSH de hello, usar hello siga comandos tooinstall Ruby en hello VM:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="a7ac0-129">instalación de Hello puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="a7ac0-130">Cuando se complete, use Hola después tooverify de comando que está instalado Ruby:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="a7ac0-131">Siguiente Hola de uso de comandos de raíles de tooinstall:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="a7ac0-132">Usar hello--rdoc n y--tooskip marcas ri no instalar la documentación de hello, que es más rápido.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="a7ac0-133">Este comando es probable que tardará mucho tiempo tooexecute, por lo que agregar Hola -V mostrará información sobre el progreso de la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="a7ac0-134">Creación y ejecución de una aplicación</span><span class="sxs-lookup"><span data-stu-id="a7ac0-134">Create and run an app</span></span>
<span data-ttu-id="a7ac0-135">Sin cerrar la sesión a través de SSH, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="a7ac0-136">Hola [nueva](http://guides.rubyonrails.org/command_line.html#rails-new) comando crea una nueva aplicación de raíles.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="a7ac0-137">Hola [server](http://guides.rubyonrails.org/command_line.html#rails-server) comando inicia Hola WEBrick servidor de web que se incluye con los raíles.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="a7ac0-138">(Para su uso en producción, probablemente querría toouse un servidor diferente, como unicornio o pasajeros.)</span><span class="sxs-lookup"><span data-stu-id="a7ac0-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="a7ac0-139">Debería aparecer resultados similares toohello siguiente.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="a7ac0-140">Agregación de un extremo</span><span class="sxs-lookup"><span data-stu-id="a7ac0-140">Add an endpoint</span></span>
1. <span data-ttu-id="a7ac0-141">Vaya toohello [portal de Azure] [https://portal.azure.com] y seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="a7ac0-142">Seleccione **EXTREMOS** en hello **configuración** a lo largo de la página de Hola de hello borde izquierdo.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="a7ac0-143">Haga clic en **agregar** al principio de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="a7ac0-144">Hola **Agregar extremo** cuadro de diálogo página, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="a7ac0-145">**Nombre**: HTTP</span><span class="sxs-lookup"><span data-stu-id="a7ac0-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="a7ac0-146">**Protocolo**: TCP</span><span class="sxs-lookup"><span data-stu-id="a7ac0-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="a7ac0-147">**Puerto público**: 80</span><span class="sxs-lookup"><span data-stu-id="a7ac0-147">**Public port**: 80</span></span>
   * <span data-ttu-id="a7ac0-148">**Puerto privado**: 3000</span><span class="sxs-lookup"><span data-stu-id="a7ac0-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="a7ac0-149">**Dirección IP flotante**: deshabilitada</span><span class="sxs-lookup"><span data-stu-id="a7ac0-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="a7ac0-150">**Lista de control de acceso - orden**: 1001 u otro valor que establece la prioridad de Hola de esta regla de acceso.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="a7ac0-151">**Lista de control de acceso - Nombre**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="a7ac0-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="a7ac0-152">**Lista de control de acceso - Acción**: permit</span><span class="sxs-lookup"><span data-stu-id="a7ac0-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="a7ac0-153">**Lista de control de acceso - Subred remota**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a7ac0-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="a7ac0-154">Este punto de conexión tiene un puerto público 80 que se usará para enrutar el tráfico toohello puerto privado de 3000, donde está escuchando el servidor de raíles de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="a7ac0-155">regla de lista de control de acceso de Hello permite el tráfico público en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![nuevo-punto-de-conexión](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="a7ac0-157">Haga clic en el punto de conexión de Aceptar toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="a7ac0-158">Debería aparecer un mensaje que indique: **Guardando el punto de conexión de la máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="a7ac0-159">Una vez que este mensaje desaparece, el punto de conexión de hello está activo.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="a7ac0-160">Ahora puede probar la aplicación desplazándose toohello nombre DNS de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="a7ac0-161">sitio Web de Hello debe aparecer toohello similar a continuación:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-161">hello website should appear similar toohello following:</span></span>

    ![Página predeterminada de Rails][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="a7ac0-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a7ac0-163">Next steps</span></span>
<span data-ttu-id="a7ac0-164">En este tutorial, se hizo la mayoría de los pasos de hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="a7ac0-165">En un entorno de producción, también podría escribir la aplicación en un equipo de desarrollo e implementarlo toohello máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="a7ac0-166">Además, la mayoría de los entornos de producción hospedan la aplicación de raíles de hello junto con otro proceso de servidor, como Apache o NginX, que controla solicitudes enrutamiento de toomultiple de instancias de aplicación de raíles de hello y que sirve al recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="a7ac0-167">Para obtener más información, consulte http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="a7ac0-168">toolearn más información acerca de Ruby sobre raíles, visite hello [Ruby en guías de raíles][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="a7ac0-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="a7ac0-169">Servicios de Azure de toouse desde la aplicación Ruby, vea:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="a7ac0-170">[Almacenamiento de datos no estructurados con blobs][blobs]</span><span class="sxs-lookup"><span data-stu-id="a7ac0-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="a7ac0-171">[Almacenamiento de parejas de clave/valor con tablas][tables]</span><span class="sxs-lookup"><span data-stu-id="a7ac0-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="a7ac0-172">[Servir el contenido de gran ancho de banda con hello red de entrega de contenido][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="a7ac0-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
