---
title: "Realizar una copia de seguridad de la aplicación en Azure"
description: "Obtenga información sobre cómo crear copias de seguridad de sus aplicaciones en el Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 77e983afaaba8e944ab1f337e1c28ced83b63205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="edd20-103">Realizar una copia de seguridad de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="edd20-103">Back up your app in Azure</span></span>
<span data-ttu-id="edd20-104">La característica Copia de seguridad y restauración de [Azure App Service](../app-service/app-service-value-prop-what-is.md) le permite crear fácilmente las copias de seguridad de la aplicación manualmente o en base a una programación.</span><span class="sxs-lookup"><span data-stu-id="edd20-104">The Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="edd20-105">Puede restaurar la aplicación a una instantánea de un estado anterior sobrescribiendo la aplicación existente o restaurando en otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="edd20-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="edd20-106">Para obtener información sobre cómo restaurar una aplicación desde la copia de seguridad, vea [Restauración de una aplicación en el Servicio de aplicaciones de Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="edd20-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="edd20-107">¿Qué se incluye en la copia de seguridad?</span><span class="sxs-lookup"><span data-stu-id="edd20-107">What gets backed up</span></span>
<span data-ttu-id="edd20-108">App Service puede hacer una copia de seguridad de la siguiente información en una cuenta de almacenamiento de Azure y el contenedor que ha configurado para que lo utilice la aplicación.</span><span class="sxs-lookup"><span data-stu-id="edd20-108">App Service can backup the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="edd20-109">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="edd20-109">App configuration</span></span>
* <span data-ttu-id="edd20-110">Contenido del archivo</span><span class="sxs-lookup"><span data-stu-id="edd20-110">File content</span></span>
* <span data-ttu-id="edd20-111">Base de datos conectada a la aplicación</span><span class="sxs-lookup"><span data-stu-id="edd20-111">Database connected to your app</span></span>

<span data-ttu-id="edd20-112">Las siguientes soluciones de base de datos son compatibles con la característica de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="edd20-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="edd20-113">Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="edd20-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="edd20-114">Azure Database for MySQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="edd20-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="edd20-115">Azure Database for PostgreSQL (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="edd20-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="edd20-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="edd20-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="edd20-117">MySQL en aplicación</span><span class="sxs-lookup"><span data-stu-id="edd20-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="edd20-118">Cada copia de seguridad es una copia completa sin conexión de su aplicación, no una actualización incremental.</span><span class="sxs-lookup"><span data-stu-id="edd20-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="edd20-119">Requisitos y restricciones</span><span class="sxs-lookup"><span data-stu-id="edd20-119">Requirements and restrictions</span></span>
* <span data-ttu-id="edd20-120">La característica Copia de seguridad y restauración requiere que el plan de App Service tenga el nivel **estándar** o **premium**.</span><span class="sxs-lookup"><span data-stu-id="edd20-120">The Back up and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="edd20-121">Para obtener más información sobre cómo escalar el plan Servicio de aplicaciones para usar un nivel superior, vea [Escalación de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="edd20-121">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="edd20-122">El nivel **premium** permite realizar un mayor número de copias de seguridad diarias que el nivel **estándar**.</span><span class="sxs-lookup"><span data-stu-id="edd20-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="edd20-123">Necesita una cuenta de almacenamiento de Azure y un contenedor en la misma suscripción que la aplicación de la que quiere realizar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edd20-123">You need an Azure storage account and container in the same subscription as the app that you want to backup.</span></span> <span data-ttu-id="edd20-124">Para obtener más información acerca de las cuentas de almacenamiento de Azure, consulte los [vínculos](#moreaboutstorage) al final de este artículo.</span><span class="sxs-lookup"><span data-stu-id="edd20-124">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="edd20-125">Puede realizar copias de seguridad de hasta 10 GB de contenido de base de datos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="edd20-125">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="edd20-126">Si el tamaño de la copia de seguridad supera este límite, obtendrá un error.</span><span class="sxs-lookup"><span data-stu-id="edd20-126">If the backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="edd20-127">Crear una copia de seguridad manual</span><span class="sxs-lookup"><span data-stu-id="edd20-127">Create a manual backup</span></span>
1. <span data-ttu-id="edd20-128">En [Azure Portal](https://portal.azure.com), vaya a la hoja de la aplicación y seleccione **Copias de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="edd20-128">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Backups**.</span></span> <span data-ttu-id="edd20-129">Se mostrará la hoja **Copias de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="edd20-129">The **Backups** blade will be displayed.</span></span>
   
    ![Página Copias de seguridad][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="edd20-131">Si ve el mensaje siguiente, haga clic en él para actualizar su plan del Servicio de aplicaciones antes de continuar con las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edd20-131">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="edd20-132">Vea [Escalación de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="edd20-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="edd20-133">![Selección de la cuenta de almacenamiento](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="edd20-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="edd20-134">En la hoja **Copia de seguridad**, haga clic en **Configurar**
![Haga clic en Configurar](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="edd20-134">In the **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="edd20-135">En la hoja **Configuración de copia de seguridad**, haga clic en **Almacenamiento: no configurado** para configurar una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="edd20-135">In the **Backup Configuration** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Selección de la cuenta de almacenamiento][ChooseStorageAccount]
4. <span data-ttu-id="edd20-137">Elija el destino de copia de seguridad; para ello, seleccione una **Cuenta de almacenamiento** y un **Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="edd20-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="edd20-138">La cuenta de almacenamiento debe pertenecer a la misma suscripción que la aplicación de la que quiere realizar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edd20-138">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="edd20-139">Si lo desea, puede crear una nueva cuenta de almacenamiento o un nuevo contenedor en las hojas correspondientes.</span><span class="sxs-lookup"><span data-stu-id="edd20-139">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="edd20-140">Cuando haya terminado, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="edd20-140">When you're done, click **Select**.</span></span>
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="edd20-142">En la hoja **Configuración de copia de seguridad** que sigue abierta, puede configurar **Copia de seguridad de la base de datos**, seleccionar las bases de datos que desee incluir en las copias de seguridad (SQL Database o MySQL) y después haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="edd20-142">In the **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="edd20-144">Para que una base de datos aparezca en esta lista, su cadena de conexión debe existir en la sección **Cadenas de conexión** de la hoja **Configuración de la aplicación** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="edd20-144">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="edd20-145">En la hoja **Configuración de copia de seguridad**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="edd20-145">In the **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="edd20-146">En la hoja **Copias de seguridad**, haga clic en **Copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="edd20-146">In the  **Backups** blade, click **Backup**.</span></span>
   
    ![Botón Backup Now][BackUpNow]
   
    <span data-ttu-id="edd20-148">Verá un mensaje de progreso durante el proceso de realización de la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edd20-148">You see a progress message during the backup process.</span></span>

<span data-ttu-id="edd20-149">Una vez configurados tanto la cuenta de almacenamiento como el contenedor, puede iniciar una copia de seguridad manual en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="edd20-149">Once the storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="edd20-150">Configuración de copias de seguridad automatizadas</span><span class="sxs-lookup"><span data-stu-id="edd20-150">Configure automated backups</span></span>
1. <span data-ttu-id="edd20-151">En la hoja **Configuración de copia de seguridad**, establezca **Copia de seguridad programada** en **Activada**.</span><span class="sxs-lookup"><span data-stu-id="edd20-151">In the **Backup Configuration** blade, set **Scheduled backup** to **On**.</span></span> 
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="edd20-153">Se mostrarán las opciones de programación de copia de seguridad. Establezca **Copia de seguridad programada** en **Activada**, configure la programación de la copia de seguridad como desee y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="edd20-153">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Activación de las copias de seguridad automatizadas][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="edd20-155">Configuración de copias de seguridad parciales</span><span class="sxs-lookup"><span data-stu-id="edd20-155">Configure Partial Backups</span></span>
<span data-ttu-id="edd20-156">En ocasiones, no querrá realizar una copia de seguridad de todo el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="edd20-156">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="edd20-157">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="edd20-157">Here are a few examples:</span></span>

* <span data-ttu-id="edd20-158">[Configure copias de seguridad semanales](web-sites-backup.md#configure-automated-backups) de la aplicación que contiene contenido estático que nunca cambia, como entradas de blog antiguas o imágenes.</span><span class="sxs-lookup"><span data-stu-id="edd20-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="edd20-159">Su aplicación tiene más de 10 GB de contenido (que es la cantidad máxima de la que puede realizar una copia de seguridad a la vez).</span><span class="sxs-lookup"><span data-stu-id="edd20-159">Your app has over 10 GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="edd20-160">No desea realizar copias de seguridad de los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="edd20-160">You don't want to backup the log files.</span></span>

<span data-ttu-id="edd20-161">Las copias de seguridad parciales permiten elegir exactamente de qué archivos desea realizar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edd20-161">Partial backups allows you choose exactly which files you want to backup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="edd20-162">Exclusión de los archivos de la copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="edd20-162">Exclude files from your backup</span></span>
<span data-ttu-id="edd20-163">Suponga que tiene una aplicación que contiene archivos de registro e imágenes estáticas de los que se ha hecho una copia de seguridad una vez y nunca van a cambiar.</span><span class="sxs-lookup"><span data-stu-id="edd20-163">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="edd20-164">En tales casos puede excluir las carpetas y los archivos para que no se almacenen en las futuras copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edd20-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="edd20-165">Para excluir archivos y carpetas de las copias de seguridad, cree un archivo `_backup.filter` en la carpeta `D:\home\site\wwwroot` de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="edd20-165">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="edd20-166">Especifique la lista de archivos y carpetas que desea excluir en este archivo.</span><span class="sxs-lookup"><span data-stu-id="edd20-166">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="edd20-167">Una manera fácil de acceder a los archivos es usar Kudu.</span><span class="sxs-lookup"><span data-stu-id="edd20-167">An easy way to access your files is to use Kudu .</span></span> <span data-ttu-id="edd20-168">Haga clic en la configuración **Herramientas avanzadas-> Ir** correspondiente a la aplicación web para acceder a Kudu.</span><span class="sxs-lookup"><span data-stu-id="edd20-168">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![Portal de uso de Kudu][kudu-portal]

<span data-ttu-id="edd20-170">Identifique las carpetas que desee excluir de las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edd20-170">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="edd20-171">Por ejemplo, desea filtrar los archivos y la carpeta resaltados.</span><span class="sxs-lookup"><span data-stu-id="edd20-171">For example , you want to filter out the highlighted folder and files.</span></span>

![Carpeta de imágenes][ImagesFolder]

<span data-ttu-id="edd20-173">Cree un archivo llamado `_backup.filter` y ponga la lista anterior en el archivo, pero quite `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="edd20-173">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="edd20-174">Enumere un directorio o archivo por línea.</span><span class="sxs-lookup"><span data-stu-id="edd20-174">List one directory or file per line.</span></span> <span data-ttu-id="edd20-175">Por lo tanto, el contenido del archivo debe ser:</span><span class="sxs-lookup"><span data-stu-id="edd20-175">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="edd20-176">Cargue el archivo `_backup.filter` en el directorio `D:\home\site\wwwroot\` de su sitio mediante [ftp](web-sites-deploy.md#ftp) o cualquier otro método.</span><span class="sxs-lookup"><span data-stu-id="edd20-176">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="edd20-177">Si lo desea, puede crear el archivo directamente mediante `DebugConsole` de Kudu e insertar el contenido.</span><span class="sxs-lookup"><span data-stu-id="edd20-177">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="edd20-178">Ejecute copias de seguridad de la misma forma que lo haría normalmente, [manual](#create-a-manual-backup) o [automáticamente](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="edd20-178">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="edd20-179">Ahora, todos archivos y las carpetas que se especifican en `_backup.filter` se excluirán de las copias de seguridad futuras programadas o iniciadas manualmente.</span><span class="sxs-lookup"><span data-stu-id="edd20-179">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="edd20-180">La restauración de las copias de seguridad parciales del sitio se realizan de la misma manera que se hace para [restaurar una copia de seguridad regular](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="edd20-180">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="edd20-181">El proceso de restauración hace lo correcto.</span><span class="sxs-lookup"><span data-stu-id="edd20-181">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="edd20-182">Cuando se restaura una copia de seguridad completa, se reemplaza todo el contenido en el sitio por lo que haya en la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edd20-182">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="edd20-183">Si un archivo está en el sitio pero no en la copia de seguridad, se elimina.</span><span class="sxs-lookup"><span data-stu-id="edd20-183">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="edd20-184">Sin embargo, cuando se restaura una copia de seguridad parcial, cualquier contenido que se encuentre en uno de los directorios en la lista negra, o cualquier archivo en la lista negra, permanecerá tal y como está.</span><span class="sxs-lookup"><span data-stu-id="edd20-184">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="edd20-185">Cómo se almacenan las copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="edd20-185">How backups are stored</span></span>
<span data-ttu-id="edd20-186">Después de realizar una o varias copias de seguridad de la aplicación, dichas copias de seguridad estarán visibles en la hoja **Contenedores** de la cuenta de almacenamiento, así como en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="edd20-186">After you have made one or more backups for your app, the backups are visible on the **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="edd20-187">En la cuenta de almacenamiento, cada copia de seguridad consta de un archivo `.zip` que contiene los datos de copia de seguridad y un archivo `.xml` que contiene un manifiesto del contenido del archivo `.zip`.</span><span class="sxs-lookup"><span data-stu-id="edd20-187">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="edd20-188">Puede descomprimir y examinar estos archivos si quiere disponer de acceso a las copias de seguridad sin tener que realizar una restauración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="edd20-188">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="edd20-189">La copia de seguridad de la base de datos para la aplicación se almacena en la raíz del archivo .zip.</span><span class="sxs-lookup"><span data-stu-id="edd20-189">The database backup for the app is stored in the root of the.zip file.</span></span> <span data-ttu-id="edd20-190">En bases de datos de SQL, este es un archivo BACPAC (sin extensión de archivo) y se puede importar.</span><span class="sxs-lookup"><span data-stu-id="edd20-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="edd20-191">Para crear una base de datos SQL basándose en la exportación del BACPAC, vea [Importar un archivo de bacpac para crear una nueva base de datos de usuario](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="edd20-191">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="edd20-192">La modificación de los archivos del contenedor **websitebackups** puede ocasionar que la base de datos deje de ser válida y, por lo tanto, no se pueda restaurar.</span><span class="sxs-lookup"><span data-stu-id="edd20-192">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="edd20-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="edd20-193">Next Steps</span></span>
<span data-ttu-id="edd20-194">Para obtener información sobre cómo restaurar una aplicación desde una copia de seguridad, vea [Restauración de una aplicación en el Servicio de aplicaciones de Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="edd20-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="edd20-195">También puede crear una copia de seguridad y restaurar las aplicaciones de App Service mediante la API de REST (vea [Uso de REST para copia de seguridad y restauración de aplicaciones de App Service](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="edd20-195">You can also backup and restore App Service apps using REST API (see [Use REST to backup and restore App Service apps](websites-csm-backup.md)).</span></span>


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

