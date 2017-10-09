---
title: "aaaInstall MongoDB en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se crea tooinstall MongoDB en una VM de Azure que ejecuta Windows Server 2012 R2 con el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="5a7a2-103">Instalación y configuración de MongoDB en una máquina virtual Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="5a7a2-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="5a7a2-104">[MongoDB](http://www.mongodb.org) es una conocida base de datos NoSQL de código abierto y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="5a7a2-105">Este artículo le guía a través de la instalación y configuración de MongoDB en una máquina virtual (VM) con Windows Server 2012 R2 en Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="5a7a2-106">También es posible [instalar MongoDB en una máquina virtual Linux en Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="5a7a2-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a7a2-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5a7a2-107">Prerequisites</span></span>
<span data-ttu-id="5a7a2-108">Antes de instalar y configurar MongoDB, necesita toocreate una máquina virtual y, idealmente, agregue un tooit de disco de datos.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="5a7a2-109">Vea Hola siguiendo artículos toocreate una máquina virtual y agregue un disco de datos:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="5a7a2-110">Crear una VM de Windows Server mediante [Hola portal de Azure](quick-create-portal.md) o [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5a7a2-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="5a7a2-111">Adjuntar un uso de VM de Windows Server de datos disco tooa [Hola portal de Azure](attach-managed-disk-portal.md) o [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5a7a2-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="5a7a2-112">toobegin instalación y configuración de MongoDB, [tooyour VM de Windows Server de inicio de sesión](connect-logon.md) mediante Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="5a7a2-113">Instalación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="5a7a2-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5a7a2-114">Las características de seguridad de MongoDB, como la vinculación de direcciones IP y la autenticación, no se encuentran habilitadas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="5a7a2-115">Características de seguridad deben habilitarse antes de implementar el entorno de producción de MongoDB tooa.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="5a7a2-116">Para más información, consulte [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication) (Seguridad y autenticación de MongoDB).</span><span class="sxs-lookup"><span data-stu-id="5a7a2-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="5a7a2-117">Una vez haya conectado tooyour máquina virtual mediante Escritorio remoto, abra Internet Explorer de hello **iniciar** menú Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="5a7a2-118">Seleccione **Usar la configuración recomendada de compatibilidad, privacidad y seguridad** la primera vez que se abra Internet Explorer y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="5a7a2-119">De forma predeterminada está habilitada la configuración de seguridad mejorada de Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="5a7a2-120">Agregar Hola MongoDB sitio Web toohello lista de sitios permitidos:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="5a7a2-121">Seleccione hello **herramientas** icono en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="5a7a2-122">En **opciones de Internet**, seleccione hello **seguridad** ficha y, a continuación, seleccione hello **sitios de confianza** icono.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="5a7a2-123">Haga clic en hello **sitios** botón.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-123">Click hello **Sites** button.</span></span> <span data-ttu-id="5a7a2-124">Agregar *https://\*. mongodb.org* toohello lista de sitios de confianza y cuadro de diálogo de hello, a continuación, cierre.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Configurar las opciones de seguridad de Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="5a7a2-126">Examinar toohello [MongoDB - descargas](http://www.mongodb.org/downloads) página (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="5a7a2-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="5a7a2-127">Si es necesario, seleccione hello **Community Server** edition y, a continuación, seleccione hello más reciente actual versión estable para Windows Server 2008 R2 de 64 bits y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="5a7a2-128">toodownload Hola instalador, haga clic en **descarga (msi)**.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Descargue el instalador de MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="5a7a2-130">Ejecute el instalador de hello una vez completada la descarga de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="5a7a2-131">Lea y acepte el contrato de licencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="5a7a2-132">Cuando se le pida, seleccione **Complete** (Completar) instalación.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="5a7a2-133">En la pantalla final de bienvenida, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="5a7a2-134">Configurar Hola VM y MongoDB</span><span class="sxs-lookup"><span data-stu-id="5a7a2-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="5a7a2-135">no se actualizan las variables de ruta de acceso de Hello instalador de MongoDB Hola.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="5a7a2-136">Sin Hola MongoDB `bin` ubicación en la variable path, necesita ruta de acceso completa de toospecify Hola cada vez que use un archivo ejecutable de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="5a7a2-137">variable de ruta de acceso de tooadd Hola ubicación tooyour:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="5a7a2-138">Menú contextual hello **iniciar** menú y seleccione **System**.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="5a7a2-139">Haga clic en la pestaña **Configuración avanzada del sistema** y luego en **Variables de entorno**.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="5a7a2-140">En **Variables del sistema**, seleccione **Path**, y, luego, haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configurar variables PATH](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="5a7a2-142">Agregar ruta de acceso de hello tooyour MongoDB `bin` carpeta.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="5a7a2-143">MongoDB se suele instalar en *C:\Archivos de programa\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="5a7a2-144">Compruebe la ruta de instalación de hello en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="5a7a2-145">Hello en el ejemplo siguiente se agrega toohello de ubicación de instalación de hello predeterminado MongoDB `PATH` variable:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="5a7a2-146">Ser seguro tooadd Hola inicial punto y coma (`;`) tooindicate que va a agregar una ubicación tooyour `PATH` variable.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="5a7a2-147">Cree los directorios de registro y datos de MongoDB en el disco de datos.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="5a7a2-148">De hello **iniciar** menú, seleccione **símbolo**.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="5a7a2-149">Hello en los ejemplos siguientes crea directorios de hello en la unidad F:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="5a7a2-150">Iniciar una instancia de MongoDB con hello siguiente comando, ajustar los datos de tooyour de ruta de acceso de Hola y los directorios de registro según corresponda:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="5a7a2-151">Puede tardar varios minutos para MongoDB tooallocate archivos de diario de Hola y empiece a escuchar las conexiones.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="5a7a2-152">Todos los mensajes de registro son dirigido toohello *F:\MongoLogs\mongolog.log* archivo como `mongod.exe` server se inicia y asigna los archivos de diario.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a7a2-153">símbolo de Hello permanece centrado en esta tarea mientras se ejecuta la instancia de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="5a7a2-154">Deje Hola símbolo ventana abierta toocontinue ejecutando MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="5a7a2-155">O bien, instale MongoDB como servicio, tal como se detalla en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="5a7a2-156">Para una experiencia más sólida de MongoDB, instale hello `mongod.exe` como un servicio.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="5a7a2-157">Creación de un servicio significa que no es necesario tooleave una línea de comandos que se ejecuta cada vez que desee toouse MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="5a7a2-158">Crear servicio hello como se indica a continuación, ajustar Hola datos tooyour de ruta de acceso y los directorios de registro según corresponda:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="5a7a2-159">Hello comando anterior crea un servicio denominado MongoDB, con una descripción de "Base de datos de Mongo".</span><span class="sxs-lookup"><span data-stu-id="5a7a2-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="5a7a2-160">También se especifica Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="5a7a2-161">Hola `--dbpath` opción especifica la ubicación de Hola Hola del directorio de datos.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="5a7a2-162">Hola `--logpath` opción debe ser toospecify usa un archivo de registro, porque el servicio en ejecución hello no tiene una salida de toodisplay de la ventana de comandos.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="5a7a2-163">Hola `--logappend` opción especifica que un reinicio del servicio de hello hace el archivo de registro existente de salida tooappend toohello.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="5a7a2-164">servicio de MongoDB en hello toostart, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="5a7a2-165">Para obtener más información acerca de cómo crear el servicio de MongoDB hello, consulte [configurar un servicio de Windows para MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="5a7a2-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="5a7a2-166">Instancia de prueba Hola MongoDB</span><span class="sxs-lookup"><span data-stu-id="5a7a2-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="5a7a2-167">Con MongoDB ejecutándose como una instancia individual o instalado como un servicio, ya puede comenzar la creación y uso de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="5a7a2-168">Hola toostart MongoDB shell administrativo, abra otra ventana del símbolo del sistema de hello **iniciar** menú y escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="5a7a2-169">Puede enumerar las bases de datos de hello con hello `db` comando.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="5a7a2-170">Inserte algunos datos como sigue:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="5a7a2-171">Busque datos como sigue:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="5a7a2-172">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="5a7a2-173">Hola de salida `mongo` consola como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="5a7a2-174">Configuración de reglas del grupo de seguridad de red y del firewall</span><span class="sxs-lookup"><span data-stu-id="5a7a2-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="5a7a2-175">Ahora que MongoDB está instalado y en ejecución, abra un puerto en Firewall de Windows para que pueda conectarse de forma remota tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="5a7a2-176">toocreate un nueva regla de entrada tooallow el puerto TCP 27017, abra un símbolo del sistema administrativo de PowerShell y escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5a7a2-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="5a7a2-177">También puede crear reglas de hello mediante hello **Firewall de Windows con seguridad avanzada** herramienta de administración gráfica.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="5a7a2-178">Crear un nueva regla de entrada tooallow el puerto TCP 27017.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="5a7a2-179">Si es necesario, cree un grupo de seguridad de red regla tooallow acceso tooMongoDB desde fuera de la subred de red virtual de Azure existente Hola.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="5a7a2-180">Puede crear hello las reglas del grupo de seguridad de red mediante hello [portal de Azure](nsg-quickstart-portal.md) o [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5a7a2-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="5a7a2-181">Al igual que con las reglas de Firewall de Windows hello, permitir la interfaz de red virtual de TCP puerto 27017 toohello de la VM de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="5a7a2-182">Puerto TCP 27017 es Hola predeterminado utilizado por MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="5a7a2-183">Puede cambiar este puerto mediante hello `--port` parámetro al iniciar `mongod.exe` manualmente o desde un servicio.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="5a7a2-184">Si cambia el puerto de hello, realizar seguros reglas tooupdate de grupo de seguridad de red y Firewall de Windows hello en hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5a7a2-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a7a2-185">Next steps</span></span>
<span data-ttu-id="5a7a2-186">En este tutorial, se habrá aprendido cómo tooinstall y configurar MongoDB en la máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="5a7a2-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="5a7a2-187">Ahora puedes acceder MongoDB en su máquina virtual de Windows, por siguientes Hola temas avanzados de hello [la documentación de MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="5a7a2-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

