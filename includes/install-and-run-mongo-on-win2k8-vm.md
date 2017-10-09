<span data-ttu-id="3c435-101">Siga estos pasos tooinstall y ejecute MongoDB en una máquina virtual que ejecuta Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3c435-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c435-102">Las características de seguridad de MongoDB, como la vinculación de direcciones IP y la autenticación, no se encuentran habilitadas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3c435-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="3c435-103">Características de seguridad deben habilitarse antes de implementar el entorno de producción de MongoDB tooa.</span><span class="sxs-lookup"><span data-stu-id="3c435-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="3c435-104">Para más información, consulte [Seguridad y autenticación](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="3c435-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="3c435-105">Una vez haya conectado la máquina virtual de toohello mediante Escritorio remoto, abra Internet Explorer de hello **iniciar** menú en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c435-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="3c435-106">Seleccione hello **herramientas** botón en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c435-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="3c435-107">En **opciones de Internet**, seleccione hello **seguridad** ficha y, a continuación, seleccione hello **sitios de confianza** icono y por último, haga clic en hello **sitios** botón.</span><span class="sxs-lookup"><span data-stu-id="3c435-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="3c435-108">Agregar *https://\*. mongodb.org* toohello lista de sitios de confianza.</span><span class="sxs-lookup"><span data-stu-id="3c435-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="3c435-109">Vaya demasiado[descargas - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="3c435-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="3c435-110">Buscar hello **versión estable actual** de **Community Server**, seleccione Hola más reciente **64-bit** versión en la columna de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="3c435-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="3c435-111">Descargue y ejecute el programa de instalación de hello MSI.</span><span class="sxs-lookup"><span data-stu-id="3c435-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="3c435-112">MongoDB se suele instalar en C:\Archivos de programa\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="3c435-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="3c435-113">Busque las Variables de entorno en el escritorio de Hola y agregue la variable de ruta de acceso de hello MongoDB binarios path toohello.</span><span class="sxs-lookup"><span data-stu-id="3c435-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="3c435-114">Por ejemplo, podría encontrar los archivos binarios de hello en C:\Program Files\MongoDB\Server\3.4\bin en su equipo.</span><span class="sxs-lookup"><span data-stu-id="3c435-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="3c435-115">Cree los directorios de datos y de registro de MongoDB en disco de datos de hello (como unidad **F:**) que creó en hello pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="3c435-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="3c435-116">De **iniciar**, seleccione **símbolo** tooopen una ventana del símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="3c435-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="3c435-117">Escriba:</span><span class="sxs-lookup"><span data-stu-id="3c435-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="3c435-118">toorun Hola base de datos, ejecute:</span><span class="sxs-lookup"><span data-stu-id="3c435-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="3c435-119">Todos los mensajes de registro son dirigido toohello *F:\MongoLogs\mongolog.log* archivo mongod.exe server se inicia y preasigna archivos de diario.</span><span class="sxs-lookup"><span data-stu-id="3c435-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="3c435-120">Puede tardar varios minutos para MongoDB toopreallocate archivos de diario de Hola y empiece a escuchar las conexiones.</span><span class="sxs-lookup"><span data-stu-id="3c435-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="3c435-121">símbolo de Hello permanece centrado en esta tarea mientras se ejecuta la instancia de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="3c435-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="3c435-122">Hola toostart MongoDB shell administrativo, abra otra ventana de comandos de **iniciar** y Hola de tipo siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="3c435-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="3c435-123">crea base de datos de Hello mediante insert Hola.</span><span class="sxs-lookup"><span data-stu-id="3c435-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="3c435-124">Como alternativa, puede instalar mongod.exe como servicio:</span><span class="sxs-lookup"><span data-stu-id="3c435-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="3c435-125">Se instala un servicio denominado MongoDB con la descripción "Mongo DB".</span><span class="sxs-lookup"><span data-stu-id="3c435-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="3c435-126">Hola `--logpath` opción debe ser toospecify usa un archivo de registro, desde Hola ejecutando el servicio no tiene una salida de toodisplay de la ventana de comandos.</span><span class="sxs-lookup"><span data-stu-id="3c435-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="3c435-127">Hola `--logappend` opción especifica que un reinicio del servicio de hello hace el archivo de registro existente de salida tooappend toohello.</span><span class="sxs-lookup"><span data-stu-id="3c435-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="3c435-128">Hola `--dbpath` opción especifica la ubicación de Hola Hola del directorio de datos.</span><span class="sxs-lookup"><span data-stu-id="3c435-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="3c435-129">Para ver más opciones de línea de comandos relacionadas con los servicios, consulte [Opciones de línea de comandos relacionadas con los servicios][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="3c435-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="3c435-130">servicio de hello toostart, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="3c435-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="3c435-131">Ahora que MongoDB está instalado y en ejecución, deberá tooopen un puerto en Firewall de Windows por lo que se puede conectarse de forma remota tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="3c435-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="3c435-132">De hello **iniciar** menú, seleccione **herramientas administrativas** y, a continuación, **Firewall de Windows con seguridad avanzada**.</span><span class="sxs-lookup"><span data-stu-id="3c435-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="3c435-133">a) en el panel izquierdo de hello, seleccione **reglas de entrada**.</span><span class="sxs-lookup"><span data-stu-id="3c435-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="3c435-134">Hola **acciones** panel en hello derecha, seleccione **nueva regla...** .</span><span class="sxs-lookup"><span data-stu-id="3c435-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Firewall de Windows][Image1]

    <span data-ttu-id="3c435-136">b) en hello **entrada Asistente para nueva regla**, seleccione **puerto** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3c435-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Firewall de Windows][Image2]

    <span data-ttu-id="3c435-138">c) Seleccione **TCP** y luego **Puertos locales específicos**.</span><span class="sxs-lookup"><span data-stu-id="3c435-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="3c435-139">Especifique un puerto de "27017" (MongoDB escucha en el puerto de forma predeterminada Hola) y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3c435-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Firewall de Windows][Image3]

    <span data-ttu-id="3c435-141">d) seleccione **Permitir conexión hello** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3c435-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Firewall de Windows][Image4]

    <span data-ttu-id="3c435-143">e) Haga clic en **Siguiente** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3c435-143">e) Click **Next** again.</span></span>

    ![Firewall de Windows][Image5]

    <span data-ttu-id="3c435-145">f) Especifique un nombre para la regla de hello, como "MongoPort" y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="3c435-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Firewall de Windows][Image6]

12. <span data-ttu-id="3c435-147">Si no ha configurado un punto de conexión para MongoDB cuando se creó la máquina virtual de hello, hágalo ahora.</span><span class="sxs-lookup"><span data-stu-id="3c435-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="3c435-148">Necesita regla de firewall de Hola y Hola extremo toobe tooconnect pueda tooMongoDB remotamente.</span><span class="sxs-lookup"><span data-stu-id="3c435-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="3c435-149">Hola portal de Azure, haga clic en **máquinas virtuales (clásicas)**, haga clic en nombre de saludo de la nueva máquina virtual y, a continuación, haga clic en **extremos**.</span><span class="sxs-lookup"><span data-stu-id="3c435-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Puntos de conexión][Image7]

13. <span data-ttu-id="3c435-151">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3c435-151">Click **Add**.</span></span>

14. <span data-ttu-id="3c435-152">Agregar un punto de conexión con el nombre "Mongo", protocolo **TCP**y ambos **público** y **privada** puertos conjunto demasiado "27017".</span><span class="sxs-lookup"><span data-stu-id="3c435-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="3c435-153">Apertura de este puerto permite toobe de MongoDB acceso remoto.</span><span class="sxs-lookup"><span data-stu-id="3c435-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Puntos de conexión][Image9]

> [!NOTE]
> <span data-ttu-id="3c435-155">Hola 27017 Hola puerto predeterminado es utilizado por MongoDB.</span><span class="sxs-lookup"><span data-stu-id="3c435-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="3c435-156">Puede cambiar este puerto predeterminado mediante la especificación de hello `--port` parámetro al iniciar hello mongod.exe servidor.</span><span class="sxs-lookup"><span data-stu-id="3c435-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="3c435-157">Asegúrese de toogive seguro Hola el mismo número de puerto en firewall de Hola y Hola extremo "Mongo" Hola anteriores instrucciones.</span><span class="sxs-lookup"><span data-stu-id="3c435-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
