<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="10fb8-101">Cuando se realizan cambios toohello adaptador de StorSimple para la configuración de RBS de SharePoint, debe ser iniciado sesión con una cuenta de usuario que pertenece el grupo de administradores de dominio de toohello.</span><span class="sxs-lookup"><span data-stu-id="10fb8-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="10fb8-102">Además, debe tener acceso a la página de configuración de Hola desde un explorador que se ejecuta en hello mismo host como Administración Central.</span><span class="sxs-lookup"><span data-stu-id="10fb8-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="10fb8-103">tooconfigure RBS</span><span class="sxs-lookup"><span data-stu-id="10fb8-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="10fb8-104">Abra la página de Administración Central de SharePoint de Hola y examinar demasiado**configuración del sistema**.</span><span class="sxs-lookup"><span data-stu-id="10fb8-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="10fb8-105">Hola **StorSimple de Azure** sección, haga clic en **configurar el adaptador de StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="10fb8-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Configurar el adaptador de StorSimple Hola](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="10fb8-107">En hello **configurar el adaptador de StorSimple** página:</span><span class="sxs-lookup"><span data-stu-id="10fb8-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="10fb8-108">Asegúrese de que ese hello **habilitar la edición de la ruta de acceso** casilla está activada.</span><span class="sxs-lookup"><span data-stu-id="10fb8-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="10fb8-109">En el cuadro de texto hello, escriba la ruta de acceso de convención de nomenclatura universal (UNC, Universal Naming Convention) de Hola Hola de almacén de blobs.</span><span class="sxs-lookup"><span data-stu-id="10fb8-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="10fb8-110">volumen de almacén de blobs de Hello debe estar hospedado en un volumen de iSCSI configurado en el dispositivo StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="10fb8-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="10fb8-111">Haga clic en hello **habilitar** botón debajo de cada una de las bases de datos de contenido Hola que quiere tooconfigure de almacenamiento remoto.</span><span class="sxs-lookup"><span data-stu-id="10fb8-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="10fb8-112">almacén de blobs de Hello debe ser compartido y es accesible por todos los servidores web de front-end (WFE) y cuenta de usuario de Hola que está configurado para la granja de servidores de SharePoint de hello debe tener el recurso compartido de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="10fb8-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Habilitar a proveedor de RBS Hola](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="10fb8-114">Al habilitar o deshabilitar RBS, también podrá ver el siguiente mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="10fb8-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![Configuración del adaptador de StorSimple: habilitar y deshabilitar](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="10fb8-116">Haga clic en hello **actualización** configuración del botón tooapply Hola.</span><span class="sxs-lookup"><span data-stu-id="10fb8-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="10fb8-117">Al hacer clic en hello **actualización** botón, Hola estado de configuración de RBS se actualizará en todos los servidores WFE y conjunto de servidores completo Hola estará habilitado RBS.</span><span class="sxs-lookup"><span data-stu-id="10fb8-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="10fb8-118">aparece el siguiente mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="10fb8-118">hello following message appears.</span></span>
      
      ![Mensaje de configuración del adaptador](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="10fb8-120">Si va a configurar RBS para una granja de SharePoint con un gran número de bases de datos (más de 200), página web de Administración Central de SharePoint de hello, es posible que el tiempo de espera. Si sucede esto, actualice la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="10fb8-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="10fb8-121">Esto no afecta el proceso de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="10fb8-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="10fb8-122">Comprobar la configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="10fb8-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="10fb8-123">Inicie sesión en el sitio Web de Administración Central de SharePoint toohello y examinar toohello **configurar el adaptador de StorSimple** página.</span><span class="sxs-lookup"><span data-stu-id="10fb8-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="10fb8-124">Compruebe toomake de detalles de configuración de hello seguro de que coinciden con configuración de Hola que especificó.</span><span class="sxs-lookup"><span data-stu-id="10fb8-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="10fb8-125">Compruebe que RBS funciona correctamente:</span><span class="sxs-lookup"><span data-stu-id="10fb8-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="10fb8-126">Cargar un documento tooSharePoint.</span><span class="sxs-lookup"><span data-stu-id="10fb8-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="10fb8-127">Examinar ruta de acceso UNC toohello que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="10fb8-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="10fb8-128">Asegúrese de que se creó la estructura de directorios RBS de Hola y que contiene el objeto de hello cargado.</span><span class="sxs-lookup"><span data-stu-id="10fb8-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="10fb8-129">(Opcional) Puede usar Microsoft RBS hello `Migrate()` cmdlet de PowerShell incluido con SharePoint toomigrate existente BLOB toohello contenido el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="10fb8-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="10fb8-130">Para obtener más información, consulte [migrar contenido dentro o fuera de RBS en SharePoint 2013] [ 6] o [migrar contenido dentro o fuera de RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="10fb8-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="10fb8-131">(Opcional) En las instalaciones de prueba, puede comprobar que Hola BLOBs se han extraído de base de datos de contenido de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="10fb8-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="10fb8-132">Inicie SQL Management Studio</span><span class="sxs-lookup"><span data-stu-id="10fb8-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="10fb8-133">Ejecutar consulta ListBlobsInDB_2010.sql o ListBlobsInDB_2013.sql de hello, como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="10fb8-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="10fb8-134">Si RBS se ha configurado correctamente, debe aparecer un valor NULL en la columna de SizeOfContentInDB Hola para cualquier objeto que se ha cargado y correctamente externalizado con RBS.</span><span class="sxs-lookup"><span data-stu-id="10fb8-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="10fb8-135">(Opcional) Después de configurar RBS y mover toohello contenido de BLOB todos los dispositivos de StorSimple, puede mover el dispositivo de toohello de base de datos de contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="10fb8-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="10fb8-136">Si elige la base de datos de contenido de hello toomove, se recomienda que configurar el almacenamiento de contenido de la base de datos de hello en dispositivo hello como el volumen principal.</span><span class="sxs-lookup"><span data-stu-id="10fb8-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="10fb8-137">A continuación, use establece que el dispositivo de StorSimple de toohello toomigrate Hola contenido de la base de datos de prácticas recomendadas de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="10fb8-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="10fb8-138">Dispositivo de toohello de base de datos de contenido de hello móvil solo se admite para la serie de hello StorSimple 8000 (no se admite para la serie de hello 5000 o 7000).</span><span class="sxs-lookup"><span data-stu-id="10fb8-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="10fb8-139">Si almacena BLOBs y base de datos de contenido de hello en volúmenes separados en el dispositivo StorSimple hello, se recomienda configurarlos en hello mismo contenedor de volumen.</span><span class="sxs-lookup"><span data-stu-id="10fb8-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="10fb8-140">Esto garantiza que se hará la copia de seguridad de ellos juntos.</span><span class="sxs-lookup"><span data-stu-id="10fb8-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="10fb8-141">Si no ha habilitado RBS, no se recomienda mover el dispositivo de StorSimple de toohello de hello contenido de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="10fb8-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="10fb8-142">Se trata de una configuración no probada.</span><span class="sxs-lookup"><span data-stu-id="10fb8-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="10fb8-143">Vaya toohello siguiente paso: [configurar la recolección de elementos no utilizados](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="10fb8-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
