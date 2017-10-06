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
# <a name="back-up-your-app-in-azure"></a>Realizar una copia de seguridad de la aplicación en Azure
Hola realizar copias de seguridad y restaurar la característica de [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) le permite crear fácilmente las copias de seguridad de la aplicación manualmente o según una programación. Puede restaurar la instantánea de tooa de aplicación Hola de un estado anterior por la aplicación existente de sobrescritura Hola o restauración tooanother. 

Para obtener información sobre cómo restaurar una aplicación desde la copia de seguridad, vea [Restauración de una aplicación en el Servicio de aplicaciones de Azure](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>¿Qué se incluye en la copia de seguridad?
Servicio de aplicaciones de una copia de seguridad siguiente Hola información tooan cuenta de almacenamiento Azure y contenedor que se haya configurado su toouse de aplicación. 

* Configuración de la aplicación
* Contenido del archivo
* Aplicación de base de datos conectado tooyour

Hola después de soluciones de base de datos es compatibles con la característica de copia de seguridad: 
   - [Base de datos SQL](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Azure Database for MySQL (versión preliminar)](https://azure.microsoft.com/en-us/services/mysql)
   - [Azure Database for PostgreSQL (versión preliminar)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [MySQL en aplicación](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  Cada copia de seguridad es una copia completa sin conexión de su aplicación, no una actualización incremental.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Requisitos y restricciones
* Hola realizar copias de seguridad y la característica de restauración requiere hello toobe del plan de servicio de aplicaciones en hello **estándar** nivel o **Premium** capa. Para obtener más información acerca de cómo ampliar el toouse del plan de servicio de aplicaciones un nivel superior, consulte [escalar una aplicación en Azure](web-sites-scale.md).  
  El nivel **premium** permite realizar un mayor número de copias de seguridad diarias que el nivel **estándar**.
* Necesita una cuenta de almacenamiento de Azure y un contenedor en hello misma suscripción que la aplicación hello que desea toobackup. Para obtener más información sobre las cuentas de almacenamiento de Azure, vea hello [vínculos](#moreaboutstorage) final Hola de este artículo.
* Las copias de seguridad pueden estar too10 GB de contenido de aplicación y base de datos. Si el tamaño de copia de seguridad de hello supera este límite, recibirá un error.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>Crear una copia de seguridad manual
1. Hola [Portal de Azure](https://portal.azure.com), navegue hoja de la aplicación tooyour, seleccione **copias de seguridad**. Hola **copias de seguridad** hoja se mostrarán.
   
    ![Página Copias de seguridad][ChooseBackupsPage]
   
   > [!NOTE]
   > Si ve el mensaje de Hola a continuación, haga clic en él tooupgrade el plan de servicio de aplicaciones antes de poder continuar con las copias de seguridad.
   > Vea [Escalación de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-scale.md) para obtener más información.  
   > ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. Hola **copia de seguridad** hoja, haga clic en **configurar**
![haga clic en configurar](./media/web-sites-backup/ClickConfigure1.png)
3. Hola **configuración de copia de seguridad** hoja, haga clic en **almacenamiento: no configurado** tooconfigure una cuenta de almacenamiento.
   
    ![Selección de la cuenta de almacenamiento][ChooseStorageAccount]
4. Elija el destino de copia de seguridad; para ello, seleccione una **Cuenta de almacenamiento** y un **Contenedor**. cuenta de almacenamiento de Hello debe pertenecer toohello misma suscripción que la aplicación hello desea tooback. Si lo desea, puede crear una nueva cuenta de almacenamiento o un nuevo contenedor en módulos respectivos Hola. Cuando haya terminado, haga clic en **Seleccionar**.
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. Hola **configuración de copia de seguridad** hoja que todavía queda abierta, puede configurar **base de datos de copia de seguridad**, a continuación, seleccione las bases de datos de Hola que desee tooinclude en las copias de seguridad de hello (base de datos SQL o MySQL), y después haga clic en **Aceptar**.  
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Para tooappear de base de datos en esta lista, debe existir su cadena de conexión en hello **las cadenas de conexión** sección de hello **configuración de la aplicación** hoja para la aplicación.
   > 
   > 
6. Hola **configuración de copia de seguridad** hoja, haga clic en **guardar**.    
7. Hola **copias de seguridad** hoja, haga clic en **copia de seguridad**.
   
    ![Botón Backup Now][BackUpNow]
   
    Verá un mensaje de progreso durante el proceso de copia de seguridad de Hola.

Una vez configurado el contenedor y la cuenta de almacenamiento de hello puede iniciar una copia de seguridad manual en cualquier momento.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Configuración de copias de seguridad automatizadas
1. Hola **configuración de copia de seguridad** hoja, establezca **copia de seguridad programada** demasiado**en**. 
   
    ![Selección de la cuenta de almacenamiento](./media/web-sites-backup/05ScheduleBackup1.png)
2. Programación de copia de seguridad se mostrarán opciones, establecer **programar copia de seguridad** demasiado**en**, a continuación, configure la programación de copia de seguridad de hello según sea necesario y haga clic en **Aceptar**.
   
    ![Activación de las copias de seguridad automatizadas][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Configuración de copias de seguridad parciales
A veces no desea toobackup todo el contenido en la aplicación. Estos son algunos ejemplos:

* [Configure copias de seguridad semanales](web-sites-backup.md#configure-automated-backups) de la aplicación que contiene contenido estático que nunca cambia, como entradas de blog antiguas o imágenes.
* La aplicación tiene más de 10 GB de contenido (es decir, cantidad máxima de hello que puede hacer una copia a la vez).
* No desea que los archivos de registro de hello toobackup.

Copias de seguridad parciales le permite elegir exactamente qué archivos desea toobackup.

### <a name="exclude-files-from-your-backup"></a>Exclusión de los archivos de la copia de seguridad
Suponga que tiene una aplicación que contiene los archivos de registro y las imágenes estáticas que han sido copia de seguridad una vez y no va toochange. En tales casos puede excluir las carpetas y los archivos para que no se almacenen en las futuras copias de seguridad. tooexclude archivos y carpetas desde las copias de seguridad, cree un `_backup.filter` archivo Hola `D:\home\site\wwwroot` carpeta de la aplicación. Especificar lista de Hola de archivos y carpetas que desee tooexclude en este archivo. 

Un tooaccess fácilmente los archivos es toouse Kudu. Haga clic en **herramientas avanzadas -> Go** establecer para su tooaccess de aplicación web Kudu.

![Portal de uso de Kudu][kudu-portal]

Identificar las carpetas de Hola que desee tooexclude desde las copias de seguridad.  Por ejemplo, desea toofilter carpeta resaltada hello y archivos.

![Carpeta de imágenes][ImagesFolder]

Cree un archivo denominado `_backup.filter` y coloque la lista de hello anteriormente en el archivo hello, pero quite `D:\home`. Enumere un directorio o archivo por línea. Por lo que debe poder contenido de hello del archivo hello:
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Cargar `_backup.filter` archivo toohello `D:\home\site\wwwroot\` directorio de su sitio usando [ftp](web-sites-deploy.md#ftp) o cualquier otro método. Si lo desea, puede crear el archivo hello directamente mediante Kudu `DebugConsole` e insertar el contenido de hello no existe.

Ejecución de copias de seguridad Hola igual como normalmente haría, [manualmente](#create-a-manual-backup) o [automáticamente](#configure-automated-backups). Ahora, los archivos y carpetas que se especifican en `_backup.filter` está excluido de hello futuras copias de seguridad programadas o iniciadas manualmente. 

> [!NOTE]
> Restaurar copias de seguridad parciales del programa Hola a su sitio igual que lo haría [restaurar una copia de seguridad periódica](web-sites-restore.md). proceso de restauración de Hola Hola lo correcto.
> 
> Cuando se restaura una copia de seguridad completa, se reemplaza todo el contenido en el sitio de hello con lo que se encuentra en la copia de seguridad de Hola. Si un archivo está en el sitio de hello, pero no en la copia de seguridad de Hola se elimina. Pero cuando se restaura una copia de seguridad parcial, cualquier contenido que se encuentra en uno de los directorios en la lista negra de hello, o cualquier archivo en la lista negra, se deja tal como está.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Cómo se almacenan las copias de seguridad
Después de realizar una o más copias de seguridad de la aplicación, las copias de seguridad de hello están visibles en hello **contenedores** hoja de la cuenta de almacenamiento y la aplicación. En la cuenta de almacenamiento de hello, cada copia de seguridad consta de un`.zip` archivo que contiene los datos de copia de seguridad de Hola y un `.xml` archivo que contiene un manifiesto de hello `.zip` el contenido del archivo. Puede descomprimir y examinar estos archivos si desea tooaccess las copias de seguridad sin realizar una restauración de la aplicación.

copia de seguridad de base de datos de Hello para la aplicación hello se almacena en la raíz de hello del archivo.zip. En bases de datos de SQL, este es un archivo BACPAC (sin extensión de archivo) y se puede importar. toocreate una base de datos SQL según Hola exportación del BACPAC, consulte [importar una nueva base de datos de usuario de archivo BACPAC tooCreate](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> Modificar cualquiera de los archivos de hello en su **websitebackups** contenedor puede provocar hello toobecome de copia de seguridad no válido y, por tanto, no restaurable.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>Pasos siguientes
Para obtener información sobre cómo restaurar una aplicación desde una copia de seguridad, vea [Restauración de una aplicación en el Servicio de aplicaciones de Azure](web-sites-restore.md). También puede una copia de seguridad y restaurar aplicaciones de servicio de aplicaciones mediante API de REST (vea [aplicaciones de servicio de aplicaciones de toobackup y restauración de REST de uso](websites-csm-backup.md)).


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

