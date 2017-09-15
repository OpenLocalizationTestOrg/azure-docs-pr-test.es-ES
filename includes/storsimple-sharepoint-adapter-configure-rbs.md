<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="7b784-101">Al realizar cambios en la configuración de RBS del adaptador de StorSimple para SharePoint, es necesario haber iniciado sesión con una cuenta de usuario que pertenezca al grupo Admins. del dominio.</span><span class="sxs-lookup"><span data-stu-id="7b784-101">When making changes to the StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs to the Domain Admins group.</span></span> <span data-ttu-id="7b784-102">Además, debe tener acceso a la página de configuración desde un explorador que se ejecuta en el mismo host que la Administración central.</span><span class="sxs-lookup"><span data-stu-id="7b784-102">Additionally, you must access the configuration page from a browser running on the same host as Central Administration.</span></span>
> 
> 

#### <a name="to-configure-rbs"></a><span data-ttu-id="7b784-103">Para configurar RBS</span><span class="sxs-lookup"><span data-stu-id="7b784-103">To configure RBS</span></span>
1. <span data-ttu-id="7b784-104">Abra la página Administración central de SharePoint y vaya a **Configuración del sistema**.</span><span class="sxs-lookup"><span data-stu-id="7b784-104">Open the SharePoint Central Administration page, and browse to **System Settings**.</span></span> 
2. <span data-ttu-id="7b784-105">En la sección **Azure StorSimple**, haga clic en **Configure StorSimple Adapter** (Configurar adaptador de StorSimple).</span><span class="sxs-lookup"><span data-stu-id="7b784-105">In the **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Configuración del adaptador de StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="7b784-107">En la página **Configuración del adaptador de StorSimple** :</span><span class="sxs-lookup"><span data-stu-id="7b784-107">On the **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="7b784-108">Asegúrese de que la casilla **Habilitar ruta de edición** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="7b784-108">Make sure that the **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="7b784-109">En el cuadro de texto, escriba la ruta de acceso de convención de nomenclatura universal (UNC) del almacén de datos de blob.</span><span class="sxs-lookup"><span data-stu-id="7b784-109">In the text box, type the Universal Naming Convention (UNC) path of the BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="7b784-110">El volumen de almacenamiento de blobs debe alojarse en un volumen iSCSI configurado en el dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7b784-110">The BLOB store volume must be hosted on an iSCSI volume configured on the StorSimple device.</span></span>

   3. <span data-ttu-id="7b784-111">Haga clic en el botón **Habilitar** situado debajo de cada una de las bases de datos de contenido que desea configurar para el almacenamiento remoto.</span><span class="sxs-lookup"><span data-stu-id="7b784-111">Click the **Enable** button below each of the content databases that you want to configure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="7b784-112">El almacén de blobs debe ser compartido y accesible para todos los servidores web front-end (WFE) y la cuenta de usuario que está configurada para la granja de servidores de SharePoint debe tener acceso al recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="7b784-112">The BLOB store must be shared and reachable by all web front-end (WFE) servers, and the user account that is configured for the SharePoint server farm must have access to the share.</span></span>
      
      ![Habilitación del proveedor de RBS](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="7b784-114">Al habilitar o deshabilitar RBS, también verá el mensaje siguiente.</span><span class="sxs-lookup"><span data-stu-id="7b784-114">When you enable or disable RBS, you will also see the following message.</span></span>
      
      ![Configuración del adaptador de StorSimple: habilitar y deshabilitar](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="7b784-116">Haga clic en el botón **Actualizar** para aplicar la configuración.</span><span class="sxs-lookup"><span data-stu-id="7b784-116">Click the **Update** button to apply the configuration.</span></span> <span data-ttu-id="7b784-117">Al hacer clic en el botón **Actualizar** , se actualiza el estado de configuración de RBS en todos los servidores WFE y toda la granja de servidores estará habilitada para RBS.</span><span class="sxs-lookup"><span data-stu-id="7b784-117">When you click the **Update** button, the RBS configuration status will be updated on all WFE servers, and the entire farm will be RBS-enabled.</span></span> <span data-ttu-id="7b784-118">Aparece el mensaje siguiente.</span><span class="sxs-lookup"><span data-stu-id="7b784-118">The following message appears.</span></span>
      
      ![Mensaje de configuración del adaptador](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="7b784-120">Si va a configurar RBS para una granja de SharePoint que contiene un gran número de bases de datos (más de 200), podría agotarse el tiempo de espera de la página Administración central de SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7b784-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), the SharePoint Central Administration web page might time out.</span></span> <span data-ttu-id="7b784-121">Si esto sucede, actualice la página.</span><span class="sxs-lookup"><span data-stu-id="7b784-121">If that occurs, refresh the page.</span></span> <span data-ttu-id="7b784-122">Esto no afecta al proceso de configuración.</span><span class="sxs-lookup"><span data-stu-id="7b784-122">This does not affect the configuration process.</span></span>

4. <span data-ttu-id="7b784-123">Verifique la configuración:</span><span class="sxs-lookup"><span data-stu-id="7b784-123">Verify the configuration:</span></span>
   
   1. <span data-ttu-id="7b784-124">Inicie sesión en el sitio web Administración central de SharePoint y vaya a la página **Configuración del adaptador de StorSimple** .</span><span class="sxs-lookup"><span data-stu-id="7b784-124">Log on to the SharePoint Central Administration website, and browse to the **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="7b784-125">Compruebe los detalles de la configuración para asegurarse de que coinciden con la configuración que especificó.</span><span class="sxs-lookup"><span data-stu-id="7b784-125">Check the configuration details to make sure that they match the settings that you entered.</span></span> 
5. <span data-ttu-id="7b784-126">Compruebe que RBS funciona correctamente:</span><span class="sxs-lookup"><span data-stu-id="7b784-126">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="7b784-127">Cargue un documento en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7b784-127">Upload a document to SharePoint.</span></span> 
   2. <span data-ttu-id="7b784-128">Vaya a la ruta de acceso UNC que configuró.</span><span class="sxs-lookup"><span data-stu-id="7b784-128">Browse to the UNC path that you configured.</span></span> <span data-ttu-id="7b784-129">Asegúrese de que se ha creado la estructura de directorios de RBS y que contiene el objeto cargado.</span><span class="sxs-lookup"><span data-stu-id="7b784-129">Make sure that the RBS directory structure was created and that it contains the uploaded object.</span></span>
6. <span data-ttu-id="7b784-130">(Opcional) Puede usar el cmdlet de PowerShell `Migrate()` de Microsoft RBS incluido con SharePoint para migrar el contenido de BLOB existente para el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7b784-130">(Optional) You can use the Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint to migrate existing BLOB content to the StorSimple device.</span></span> <span data-ttu-id="7b784-131">Para obtener más información, consulte [migrar contenido dentro o fuera de RBS en SharePoint 2013] [ 6] o [migrar contenido dentro o fuera de RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="7b784-131">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="7b784-132">(Opcional) En instalaciones de prueba, puede comprobar que los blobs se han extraído de la base de datos de contenido como sigue:</span><span class="sxs-lookup"><span data-stu-id="7b784-132">(Optional) On test installations, you can verify that the BLOBs were moved out of the content database as follows:</span></span> 
   
   1. <span data-ttu-id="7b784-133">Inicie SQL Management Studio</span><span class="sxs-lookup"><span data-stu-id="7b784-133">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="7b784-134">Ejecute la consulta ListBlobsInDB_2010.sql o ListBlobsInDB_2013.sql, como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="7b784-134">Run the ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
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
      
      <span data-ttu-id="7b784-135">Si RBS se ha configurado correctamente, debe aparecer un valor NULL en la columna SizeOfContentInDB para cualquier objeto que se ha cargado y externalizado correctamente con RBS.</span><span class="sxs-lookup"><span data-stu-id="7b784-135">If RBS was configured correctly, a NULL value should appear in the SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="7b784-136">(Opcional) Después de configurar RBS y mover todo el contenido de BLOB al dispositivo de StorSimple, puede mover la base de datos de contenido al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7b784-136">(Optional) After you configure RBS and move all BLOB content to the StorSimple device, you can move the content database to the device.</span></span> <span data-ttu-id="7b784-137">Si elige mover la base de datos de contenido, recomendamos configurar el almacenamiento de la base de datos de contenido en el dispositivo como el volumen principal.</span><span class="sxs-lookup"><span data-stu-id="7b784-137">If you choose to move the content database, we recommend that you configure the content database storage on the device as a primary volume.</span></span> <span data-ttu-id="7b784-138">Use los procedimientos recomendados de migración de SQL Server para mover la base de datos de contenido al dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7b784-138">Then, use established SQL Server best practices to migrate the content database to the StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7b784-139">El traslado de la base de datos de contenido al dispositivo solo se admite para el dispositivo de la serie StorSimple 8000 (no admitido para las series 5000 o 7000).</span><span class="sxs-lookup"><span data-stu-id="7b784-139">Moving the content database to the device is only supported for the StorSimple 8000 series (it is not supported for the 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="7b784-140">Si almacena los blobs y la base de datos de contenido en volúmenes independientes en el dispositivo de StorSimple, se recomienda configurarlos en el mismo contenedor de volumen.</span><span class="sxs-lookup"><span data-stu-id="7b784-140">If you store BLOBs and the content database in separate volumes on the StorSimple device, we recommend that you configure them in the same volume container.</span></span> <span data-ttu-id="7b784-141">Esto garantiza que se hará la copia de seguridad de ellos juntos.</span><span class="sxs-lookup"><span data-stu-id="7b784-141">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="7b784-142">Si no tiene RBS habilitado, no es recomendable mover la base de datos de contenido al dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7b784-142">If you have not enabled RBS, we do not recommend moving the content database to the StorSimple device.</span></span> <span data-ttu-id="7b784-143">Se trata de una configuración no probada.</span><span class="sxs-lookup"><span data-stu-id="7b784-143">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="7b784-144">Vaya al paso siguiente: [Configuración de la recolección de elementos no utilizados](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="7b784-144">Go to the next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
