---
title: aaaUse REST tooback seguridad y restaurar aplicaciones de servicio de aplicaciones
description: "Obtenga información acerca de cómo toouse API de REST llama tooback y restauración de una aplicación de servicio de aplicaciones de Azure"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="96a5d-103">Consumir tooback REST y restaurar aplicaciones de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="96a5d-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96a5d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96a5d-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="96a5d-105">API DE REST</span><span class="sxs-lookup"><span data-stu-id="96a5d-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="96a5d-106">[aplicaciones del Servicio de aplicaciones](https://azure.microsoft.com/services/app-service/web/) como blobs en Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="96a5d-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="96a5d-107">copia de seguridad de Hello también puede contener las bases de datos de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="96a5d-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="96a5d-108">Si alguna vez accidentalmente se elimina la aplicación hello, o si toobe de necesidades de aplicación Hola revertir la versión anterior de tooa, se puede restaurar desde cualquier copia de seguridad anterior.</span><span class="sxs-lookup"><span data-stu-id="96a5d-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="96a5d-109">Las copias de seguridad se pueden realizar en cualquier momento a petición o se pueden programar a intervalos adecuados.</span><span class="sxs-lookup"><span data-stu-id="96a5d-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="96a5d-110">Este artículo explica cómo toobackup y restauración solicita una aplicación con la API de REST.</span><span class="sxs-lookup"><span data-stu-id="96a5d-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="96a5d-111">Si lo desea toocreate y administrar copias de seguridad de aplicación gráficamente mediante Hola portal de Azure, consulte [copia de seguridad una aplicación web en el servicio de aplicación de Azure](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="96a5d-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="96a5d-112">Introducción</span><span class="sxs-lookup"><span data-stu-id="96a5d-112">Getting Started</span></span>
<span data-ttu-id="96a5d-113">solicita toosend REST, necesita la aplicación tooknow **nombre**, **grupo de recursos**, y **Id. de suscripción**. Esta información se puede encontrar haciendo clic en la aplicación en hello **servicio de aplicaciones** hoja de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96a5d-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="96a5d-114">Para obtener ejemplos de hello en este artículo, nos estamos configuración de sitio Web de hello **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="96a5d-115">Se almacena en el grupo de recursos de hello oesteee. UU. de Web predeterminado y se ejecuta en una suscripción con hello identificador 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="96a5d-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![Información del sitio web de ejemplo][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="96a5d-117">Copia de seguridad y restauración de API de REST</span><span class="sxs-lookup"><span data-stu-id="96a5d-117">Backup and restore REST API</span></span>
<span data-ttu-id="96a5d-118">Ahora se explicará varios ejemplos de cómo toouse Hola toobackup de API de REST y restauración de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="96a5d-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="96a5d-119">Cada ejemplo incluye una dirección URL y un cuerpo de solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="96a5d-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="96a5d-120">dirección URL de ejemplo de Hola contiene marcadores de posición que se ajustan entre llaves, como {Id. de suscripción}.</span><span class="sxs-lookup"><span data-stu-id="96a5d-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="96a5d-121">Reemplace los marcadores de posición de hello con la información correspondiente de hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="96a5d-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="96a5d-122">Como referencia, aquí es una explicación de cada marcador de posición que aparece en las direcciones URL de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="96a5d-123">identificador de suscripción: Id. de aplicación de Hola de hello suscripción de Azure que lo contiene</span><span class="sxs-lookup"><span data-stu-id="96a5d-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="96a5d-124">Resource-group-name: nombre de aplicación de hello contenedor de grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="96a5d-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="96a5d-125">nombre: nombre de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="96a5d-125">name – Name of hello app</span></span>
* <span data-ttu-id="96a5d-126">copia de seguridad-id: identificador de copia de seguridad de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="96a5d-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="96a5d-127">Para obtener documentación completa Hola de hello API, incluidos varios parámetros opcionales que pueden incluirse en la solicitud HTTP de hello, vea hello [Explorador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="96a5d-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="96a5d-128">Copia de seguridad de una aplicación a petición</span><span class="sxs-lookup"><span data-stu-id="96a5d-128">Backup an app on demand</span></span>
<span data-ttu-id="96a5d-129">tooback seguridad de una aplicación envíe inmediatamente, una **POST** solicitud demasiado**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ copia de seguridad /**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="96a5d-130">Este es el aspecto de dirección URL de hello como el uso de nuestro sitio Web de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="96a5d-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="96a5d-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="96a5d-132">Proporcione un objeto JSON en el cuerpo de Hola de su toospecify de solicitud que toostore toouse de cuenta de almacenamiento Hola copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="96a5d-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="96a5d-133">objeto JSON de Hello debe tener una propiedad denominada **storageAccountUrl**, que contiene un [URL de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) concesión de contenedor de almacenamiento de Azure de toohello de acceso de escritura que contiene el blob de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="96a5d-134">Si desea tooback las bases de datos, también debe proporcionar una lista que contiene nombres de hello, tipos y las cadenas de conexión de hello las bases de datos toobe copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="96a5d-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="96a5d-135">Una copia de seguridad de la aplicación hello comienza inmediatamente cuando se recibe una solicitud Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="96a5d-136">proceso de copia de seguridad de Hello puede tardar un toocomplete mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="96a5d-137">Hola respuesta HTTP contiene un identificador que puede usar en otro estado de hello toosee la solicitud de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="96a5d-138">Este es un ejemplo de cuerpo de Hola de solicitud de copia de seguridad de tooour de respuesta HTTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="96a5d-139">Mensajes de error pueden encontrarse en la propiedad de registro de hello de hello respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="96a5d-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="96a5d-140">Programación de copias de seguridad automáticas</span><span class="sxs-lookup"><span data-stu-id="96a5d-140">Schedule automatic backups</span></span>
<span data-ttu-id="96a5d-141">En toobacking de adición de una aplicación a petición, también puede programar una copia de seguridad toohappen automáticamente.</span><span class="sxs-lookup"><span data-stu-id="96a5d-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="96a5d-142">Configuración de una nueva programación de copias de seguridad automáticas</span><span class="sxs-lookup"><span data-stu-id="96a5d-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="96a5d-143">tooset de una programación de copia de seguridad, envíe un **colocar** solicitud demasiado**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="96a5d-144">Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="96a5d-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="96a5d-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="96a5d-146">cuerpo de la solicitud de Hello debe tener un objeto JSON que especifica la configuración de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="96a5d-147">Este es un ejemplo con todos los parámetros de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="96a5d-147">Here is an example with all hello required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="96a5d-148">Este ejemplo configura Hola aplicación toobe copia automáticamente cada siete días.</span><span class="sxs-lookup"><span data-stu-id="96a5d-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="96a5d-149">Hola parámetros **frequencyInterval** y **frequencyUnit** combinación determinan con qué frecuencia hello copias de seguridad realizan.</span><span class="sxs-lookup"><span data-stu-id="96a5d-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="96a5d-150">Los valores válidos para **frequencyUnit** son **hora** y **día**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="96a5d-151">Por ejemplo, tooback seguridad de una aplicación cada 12 horas, establezca frequencyInterval too12 y frequencyUnit toohour.</span><span class="sxs-lookup"><span data-stu-id="96a5d-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="96a5d-152">Copias de seguridad antiguas se quitan automáticamente de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="96a5d-153">Puede controlar la antigüedad Hola pueden ser copias de seguridad mediante la configuración hello **retentionPeriodInDays** parámetro.</span><span class="sxs-lookup"><span data-stu-id="96a5d-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="96a5d-154">Si desea que tooalways tiene al menos una copia de seguridad guardarlo, independientemente de su antigüedad, establecerla **keepAtLeastOneBackup** tootrue.</span><span class="sxs-lookup"><span data-stu-id="96a5d-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="96a5d-155">Obtener la programación de copia de seguridad automática de Hola</span><span class="sxs-lookup"><span data-stu-id="96a5d-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="96a5d-156">tooget una aplicación de copia de seguridad de configuración, enviar un **POST** toohello URL de solicitud **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sitios / {nombre} / config/copia de seguridad/lista**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="96a5d-157">dirección URL de Hola para nuestro sitio de ejemplo es **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="96a5d-158">Obtener estado de Hola de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="96a5d-158">Get hello status of a backup</span></span>
<span data-ttu-id="96a5d-159">Según el tamaño aplicación hello es, una copia de seguridad puede tardar un rato toocomplete.</span><span class="sxs-lookup"><span data-stu-id="96a5d-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="96a5d-160">Las copias de seguridad pueden también provocar errores, alargar el tiempo de espera o completarse solo parcialmente.</span><span class="sxs-lookup"><span data-stu-id="96a5d-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="96a5d-161">Enviar estado de hello toosee de copias de seguridad de todas las de una aplicación, un **obtener** toohello URL de solicitud **https://management.azure.com/subscriptions/ {Id. de suscripción} / ResourceGroups / {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="96a5d-162">estado de hello toosee de una copia de seguridad específica, enviar una dirección URL toohello GET **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { copia de seguridad-id}**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="96a5d-163">Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="96a5d-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="96a5d-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="96a5d-165">cuerpo de respuesta de Hello contiene un ejemplo de toothis similar del objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="96a5d-165">hello response body contains a JSON object similar toothis example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="96a5d-166">estado de Hola de una copia de seguridad es un tipo enumerado.</span><span class="sxs-lookup"><span data-stu-id="96a5d-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="96a5d-167">Mostramos, a continuación, todos los estados posibles.</span><span class="sxs-lookup"><span data-stu-id="96a5d-167">Here is every possible state.</span></span>

* <span data-ttu-id="96a5d-168">0 – InProgress: copia de seguridad de Hola se ha iniciado pero no se ha completado.</span><span class="sxs-lookup"><span data-stu-id="96a5d-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="96a5d-169">1: no se pudo: copia de seguridad de hello tuvo éxito.</span><span class="sxs-lookup"><span data-stu-id="96a5d-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="96a5d-170">2 – correcta: copia de seguridad de Hola se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="96a5d-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="96a5d-171">3 – TimedOut: copia de seguridad de hello no terminó en el tiempo y se ha cancelado.</span><span class="sxs-lookup"><span data-stu-id="96a5d-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="96a5d-172">4: crear: solicitud de copia de seguridad de Hola se pone en cola pero no se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="96a5d-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="96a5d-173">5: omitidos: copia de seguridad de hello no continuar debido programación tooa desencadenar demasiadas copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="96a5d-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="96a5d-174">6: PartiallySucceeded: copia de seguridad de hello correcta, pero algunos archivos no se incluyeron porque no se puede leer.</span><span class="sxs-lookup"><span data-stu-id="96a5d-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="96a5d-175">Esto suele suceder cuando se coloca un bloqueo exclusivo en archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="96a5d-176">7: DeleteInProgress: copia de seguridad de hello ha sido solicitado toobe eliminado, pero aún no se ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="96a5d-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="96a5d-177">8: DeleteFailed: no se pudo eliminar la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="96a5d-178">Esto podría deberse a que expiró Hola dirección URL de SAS copia de seguridad de hello toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="96a5d-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="96a5d-179">9: eliminar: copia de seguridad de Hola se eliminó correctamente.</span><span class="sxs-lookup"><span data-stu-id="96a5d-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="96a5d-180">Restauración de una aplicación desde una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="96a5d-180">Restore an app from a backup</span></span>
<span data-ttu-id="96a5d-181">Si la aplicación se ha eliminado, o si desea toorevert la versión anterior de tooa la aplicación, puede restaurar la aplicación hello desde una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="96a5d-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="96a5d-182">tooinvoke una restauración, envíe un **POST** toohello URL de solicitud **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ las copias de seguridad / {Id. de copia de seguridad} / restore**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="96a5d-183">Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="96a5d-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="96a5d-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="96a5d-185">En el cuerpo de la solicitud de hello, enviar un objeto JSON que contiene propiedades de hello para la operación de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="96a5d-186">Este es un ejemplo que contiene todas las propiedades necesarias:</span><span class="sxs-lookup"><span data-stu-id="96a5d-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="96a5d-187">Restaurar tooa nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="96a5d-187">Restore tooa new app</span></span>
<span data-ttu-id="96a5d-188">En ocasiones es preferible toocreate una nueva aplicación cuando se restaura una copia de seguridad, en lugar de sobrescribir una aplicación ya existente.</span><span class="sxs-lookup"><span data-stu-id="96a5d-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="96a5d-189">toodo, cambio Hola solicitud URL toopoint toohello nueva aplicación que desee toocreate y cambia hello **sobrescribir** propiedad Hola JSON demasiado**false**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="96a5d-190">Eliminación de una copia de seguridad de aplicación</span><span class="sxs-lookup"><span data-stu-id="96a5d-190">Delete an app backup</span></span>
<span data-ttu-id="96a5d-191">Si desea que toodelete una copia de seguridad, envíe un **eliminar** toohello URL de solicitud **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sitios / {nombre} /backups/ {Id. de copia de seguridad}**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="96a5d-192">Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="96a5d-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="96a5d-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="96a5d-194">Administración de la dirección URL de SAS de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="96a5d-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="96a5d-195">Servicio de aplicaciones de Azure intentará toodelete la copia de seguridad de almacenamiento de Azure con la dirección URL de SAS que se proporcionó cuando se creó la copia de seguridad de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="96a5d-196">Si esta dirección URL de SAS ya no es válida, no se puede eliminar la copia de seguridad de Hola a través de la API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="96a5d-197">Sin embargo, puede actualizar Hola URL de SAS asociada a una copia de seguridad mediante el envío de un **POST** toohello URL de solicitud **https://management.azure.com/subscriptions/ {Id. de suscripción} / ResourceGroups / {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="96a5d-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="96a5d-198">Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="96a5d-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="96a5d-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="96a5d-200">En el cuerpo de la solicitud de hello, enviar un objeto JSON que contiene la nueva dirección URL SAS Hola.</span><span class="sxs-lookup"><span data-stu-id="96a5d-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="96a5d-201">Aquí tiene un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="96a5d-202">Por motivos de seguridad, Hola que URL de SAS asociada a una copia de seguridad no se devuelve al enviar una solicitud GET para una copia de seguridad específica.</span><span class="sxs-lookup"><span data-stu-id="96a5d-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="96a5d-203">Si desea hello tooview URL de SAS asociada a una copia de seguridad, envíe un toohello de solicitud POST misma dirección URL anterior.</span><span class="sxs-lookup"><span data-stu-id="96a5d-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="96a5d-204">Incluir un objeto JSON vacío en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="96a5d-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="96a5d-205">respuesta de Hola desde servidor hello contiene toda información de copia de seguridad, incluida su dirección URL de SAS.</span><span class="sxs-lookup"><span data-stu-id="96a5d-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
