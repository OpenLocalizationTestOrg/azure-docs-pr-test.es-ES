---
title: "aaaBack seguridad de la aplicación en Azure"
description: "Obtenga información acerca de cómo toocreate las copias de seguridad de las aplicaciones de servicio de aplicaciones de Azure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="99242-103">Realizar una copia de seguridad de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="99242-103">Back up your app in Azure</span></span>
<span data-ttu-id="99242-104">Hola realizar copias de seguridad y restaurar la característica de [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) le permite crear fácilmente las copias de seguridad de la aplicación manualmente o según una programación.</span><span class="sxs-lookup"><span data-stu-id="99242-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="99242-105">Puede restaurar la instantánea de tooa de aplicación Hola de un estado anterior por la aplicación existente de sobrescritura Hola o restauración tooanother.</span><span class="sxs-lookup"><span data-stu-id="99242-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="99242-106">Para obtener información sobre cómo restaurar una aplicación desde la copia de seguridad, vea [Restauración de una aplicación en el Servicio de aplicaciones de Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="99242-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="99242-107">¿Qué se incluye en la copia de seguridad?</span><span class="sxs-lookup"><span data-stu-id="99242-107">What gets backed up</span></span>
<span data-ttu-id="99242-108">Servicio de aplicaciones de una copia de seguridad siguiente Hola información tooan cuenta de almacenamiento Azure y contenedor que se haya configurado su toouse de aplicación.</span><span class="sxs-lookup"><span data-stu-id="99242-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="99242-109">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="99242-109">App configuration</span></span>
* <span data-ttu-id="99242-110">Contenido del archivo</span><span class="sxs-lookup"><span data-stu-id="99242-110">File content</span></span>
* <span data-ttu-id="99242-111">Aplicación de base de datos conectado tooyour</span><span class="sxs-lookup"><span data-stu-id="99242-111">Database connected tooyour app</span></span>

<span data-ttu-id="99242-112">Hola después de soluciones de base de datos es compatibles con la característica de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="99242-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="99242-113">Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="99242-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="99242-114">Azure Database for MySQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="99242-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="99242-115">Azure Database for PostgreSQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="99242-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="99242-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="99242-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="99242-117">MySQL en aplicación</span><span class="sxs-lookup"><span data-stu-id="99242-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="99242-118">Cada copia de seguridad es una copia completa sin conexión de su aplicación, no una actualización incremental.</span><span class="sxs-lookup"><span data-stu-id="99242-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="99242-119">Requisitos y restricciones</span><span class="sxs-lookup"><span data-stu-id="99242-119">Requirements and restrictions</span></span>
* <span data-ttu-id="99242-120">Hola realizar copias de seguridad y la característica de restauración requiere hello toobe del plan de servicio de aplicaciones en hello **estándar** nivel o **Premium** capa.</span><span class="sxs-lookup"><span data-stu-id="99242-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="99242-121">Para obtener más información acerca de cómo ampliar el toouse del plan de servicio de aplicaciones un nivel superior, consulte [escalar una aplicación en Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="99242-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="99242-122">El nivel **premium** permite realizar un mayor número de copias de seguridad diarias que el nivel **estándar**.</span><span class="sxs-lookup"><span data-stu-id="99242-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="99242-123">Necesita una cuenta de almacenamiento de Azure y un contenedor en hello misma suscripción que la aplicación hello que desea toobackup.</span><span class="sxs-lookup"><span data-stu-id="99242-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="99242-124">Para obtener más información sobre las cuentas de almacenamiento de Azure, vea hello [vínculos](#moreaboutstorage) final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="99242-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="99242-125">Las copias de seguridad pueden estar too10 GB de contenido de aplicación y base de datos.</span><span class="sxs-lookup"><span data-stu-id="99242-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="99242-126">Si el tamaño de copia de seguridad de hello supera este límite, recibirá un error.</span><span class="sxs-lookup"><span data-stu-id="99242-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="99242-127">Crear una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="99242-127">Create a manual backup</span></span>
1. <span data-ttu-id="99242-128">Hola [Portal de Azure](https://portal.azure.com), navegue hoja de la aplicación tooyour, seleccione **copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="99242-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="99242-129">Hola **copias de seguridad** hoja se mostrarán.</span><span class="sxs-lookup"><span data-stu-id="99242-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Página Copias de seguridad][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="99242-131">Si ve el mensaje de Hola a continuación, haga clic en él tooupgrade el plan de servicio de aplicaciones antes de poder continuar con las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="99242-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="99242-132">Vea [Escalación de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="99242-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="99242-133">![Selección de la cuenta de almacenamiento](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="99242-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="99242-134">Hola **copia de seguridad** hoja, haga clic en **configurar**
![haga clic en configurar](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="99242-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="99242-135">Hola **configuración de copia de seguridad** hoja, haga clic en **almacenamiento: no configurado** tooconfigure una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="99242-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Selección de la cuenta de almacenamiento][ChooseStorageAccount]
4. <span data-ttu-id="99242-137">Elija el destino de copia de seguridad; para ello, seleccione una **Cuenta de almacenamiento** y un **Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="99242-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="99242-138">cuenta de almacenamiento de Hello debe pertenecer toohello misma suscripción que la aplicación hello desea tooback.</span><span class="sxs-lookup"><span data-stu-id="99242-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="99242-139">Si lo desea, puede crear una nueva cuenta de almacenamiento o un nuevo contenedor en módulos respectivos Hola.</span><span class="sxs-lookup"><span data-stu-id="99242-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="99242-140">Cuando haya terminado, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="99242-140">When you're done, click **Select**.</span></span>
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="99242-142">Hola **configuración de copia de seguridad** hoja que todavía queda abierta, puede configurar **base de datos de copia de seguridad**, a continuación, seleccione las bases de datos de Hola que desee tooinclude en las copias de seguridad de hello (base de datos SQL o MySQL), y después haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="99242-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="99242-144">Para tooappear de base de datos en esta lista, debe existir su cadena de conexión en hello **las cadenas de conexión** sección de hello **configuración de la aplicación** hoja para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99242-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="99242-145">Hola **configuración de copia de seguridad** hoja, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="99242-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="99242-146">Hola **copias de seguridad** hoja, haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="99242-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![Botón Backup Now][BackUpNow]
   
    <span data-ttu-id="99242-148">Verá un mensaje de progreso durante el proceso de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="99242-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="99242-149">Una vez configurado el contenedor y la cuenta de almacenamiento de hello puede iniciar una copia de seguridad manual en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="99242-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="99242-150">Configuración de copias de seguridad automatizadas</span><span class="sxs-lookup"><span data-stu-id="99242-150">Configure automated backups</span></span>
1. <span data-ttu-id="99242-151">Hola **configuración de copia de seguridad** hoja, establezca **copia de seguridad programada** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="99242-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="99242-153">Programación de copia de seguridad se mostrarán opciones, establecer **programar copia de seguridad** demasiado**en**, a continuación, configure la programación de copia de seguridad de hello según sea necesario y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="99242-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Activación de las copias de seguridad automatizadas][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="99242-155">Configuración de copias de seguridad parciales</span><span class="sxs-lookup"><span data-stu-id="99242-155">Configure Partial Backups</span></span>
<span data-ttu-id="99242-156">A veces no desea toobackup todo el contenido en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99242-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="99242-157">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="99242-157">Here are a few examples:</span></span>

* <span data-ttu-id="99242-158">[Configure copias de seguridad semanales](web-sites-backup.md#configure-automated-backups) de la aplicación que contiene contenido estático que nunca cambia, como entradas de blog antiguas o imágenes.</span><span class="sxs-lookup"><span data-stu-id="99242-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="99242-159">La aplicación tiene más de 10 GB de contenido (es decir, cantidad máxima de hello que puede hacer una copia a la vez).</span><span class="sxs-lookup"><span data-stu-id="99242-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="99242-160">No desea que los archivos de registro de hello toobackup.</span><span class="sxs-lookup"><span data-stu-id="99242-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="99242-161">Copias de seguridad parciales le permite elegir exactamente qué archivos desea toobackup.</span><span class="sxs-lookup"><span data-stu-id="99242-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="99242-162">Exclusión de los archivos de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="99242-162">Exclude files from your backup</span></span>
<span data-ttu-id="99242-163">Suponga que tiene una aplicación que contiene los archivos de registro y las imágenes estáticas que han sido copia de seguridad una vez y no va toochange.</span><span class="sxs-lookup"><span data-stu-id="99242-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="99242-164">En tales casos puede excluir las carpetas y los archivos para que no se almacenen en las futuras copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="99242-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="99242-165">tooexclude archivos y carpetas desde las copias de seguridad, cree un `_backup.filter` archivo Hola `D:\home\site\wwwroot` carpeta de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99242-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="99242-166">Especificar lista de Hola de archivos y carpetas que desee tooexclude en este archivo.</span><span class="sxs-lookup"><span data-stu-id="99242-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="99242-167">Un tooaccess fácilmente los archivos es toouse Kudu.</span><span class="sxs-lookup"><span data-stu-id="99242-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="99242-168">Haga clic en **herramientas avanzadas -> Go** establecer para su tooaccess de aplicación web Kudu.</span><span class="sxs-lookup"><span data-stu-id="99242-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![Portal de uso de Kudu][kudu-portal]

<span data-ttu-id="99242-170">Identificar las carpetas de Hola que desee tooexclude desde las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="99242-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="99242-171">Por ejemplo, desea toofilter carpeta resaltada hello y archivos.</span><span class="sxs-lookup"><span data-stu-id="99242-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Carpeta de imágenes][ImagesFolder]

<span data-ttu-id="99242-173">Cree un archivo denominado `_backup.filter` y coloque la lista de hello anteriormente en el archivo hello, pero quite `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="99242-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="99242-174">Enumere un directorio o archivo por línea.</span><span class="sxs-lookup"><span data-stu-id="99242-174">List one directory or file per line.</span></span> <span data-ttu-id="99242-175">Por lo que debe poder contenido de hello del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="99242-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="99242-176">Cargar `_backup.filter` archivo toohello `D:\home\site\wwwroot\` directorio de su sitio usando [ftp](web-sites-deploy.md#ftp) o cualquier otro método.</span><span class="sxs-lookup"><span data-stu-id="99242-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="99242-177">Si lo desea, puede crear el archivo hello directamente mediante Kudu `DebugConsole` e insertar el contenido de hello no existe.</span><span class="sxs-lookup"><span data-stu-id="99242-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="99242-178">Ejecución de copias de seguridad Hola igual como normalmente haría, [manualmente](#create-a-manual-backup) o [automáticamente](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="99242-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="99242-179">Ahora, los archivos y carpetas que se especifican en `_backup.filter` está excluido de hello futuras copias de seguridad programadas o iniciadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="99242-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="99242-180">Restaurar copias de seguridad parciales del programa Hola a su sitio igual que lo haría [restaurar una copia de seguridad periódica](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="99242-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="99242-181">proceso de restauración de Hola Hola lo correcto.</span><span class="sxs-lookup"><span data-stu-id="99242-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="99242-182">Cuando se restaura una copia de seguridad completa, se reemplaza todo el contenido en el sitio de hello con lo que se encuentra en la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="99242-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="99242-183">Si un archivo está en el sitio de hello, pero no en la copia de seguridad de Hola se elimina.</span><span class="sxs-lookup"><span data-stu-id="99242-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="99242-184">Pero cuando se restaura una copia de seguridad parcial, cualquier contenido que se encuentra en uno de los directorios en la lista negra de hello, o cualquier archivo en la lista negra, se deja tal como está.</span><span class="sxs-lookup"><span data-stu-id="99242-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="99242-185">Cómo se almacenan las copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="99242-185">How backups are stored</span></span>
<span data-ttu-id="99242-186">Después de realizar una o más copias de seguridad de la aplicación, las copias de seguridad de hello están visibles en hello **contenedores** hoja de la cuenta de almacenamiento y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99242-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="99242-187">En la cuenta de almacenamiento de hello, cada copia de seguridad consta de un`.zip` archivo que contiene los datos de copia de seguridad de Hola y un `.xml` archivo que contiene un manifiesto de hello `.zip` el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="99242-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="99242-188">Puede descomprimir y examinar estos archivos si desea tooaccess las copias de seguridad sin realizar una restauración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="99242-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="99242-189">copia de seguridad de base de datos de Hello para la aplicación hello se almacena en la raíz de hello del archivo.zip.</span><span class="sxs-lookup"><span data-stu-id="99242-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="99242-190">En bases de datos de SQL, este es un archivo BACPAC (sin extensión de archivo) y se puede importar.</span><span class="sxs-lookup"><span data-stu-id="99242-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="99242-191">toocreate una base de datos SQL según Hola exportación del BACPAC, consulte [importar una nueva base de datos de usuario de archivo BACPAC tooCreate](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="99242-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="99242-192">Modificar cualquiera de los archivos de hello en su **websitebackups** contenedor puede provocar hello toobecome de copia de seguridad no válido y, por tanto, no restaurable.</span><span class="sxs-lookup"><span data-stu-id="99242-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="99242-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99242-193">Next Steps</span></span>
<span data-ttu-id="99242-194">Para obtener información sobre cómo restaurar una aplicación desde una copia de seguridad, vea [Restauración de una aplicación en el Servicio de aplicaciones de Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="99242-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="99242-195">También puede una copia de seguridad y restaurar aplicaciones de servicio de aplicaciones mediante API de REST (vea [aplicaciones de servicio de aplicaciones de toobackup y restauración de REST de uso](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="99242-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

