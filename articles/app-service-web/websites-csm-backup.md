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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>Consumir tooback REST y restaurar aplicaciones de servicio de aplicaciones
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [API DE REST](websites-csm-backup.md)
> 
> 

[aplicaciones del Servicio de aplicaciones](https://azure.microsoft.com/services/app-service/web/) como blobs en Almacenamiento de Azure. copia de seguridad de Hello también puede contener las bases de datos de la aplicación hello. Si alguna vez accidentalmente se elimina la aplicación hello, o si toobe de necesidades de aplicación Hola revertir la versión anterior de tooa, se puede restaurar desde cualquier copia de seguridad anterior. Las copias de seguridad se pueden realizar en cualquier momento a petición o se pueden programar a intervalos adecuados.

Este artículo explica cómo toobackup y restauración solicita una aplicación con la API de REST. Si lo desea toocreate y administrar copias de seguridad de aplicación gráficamente mediante Hola portal de Azure, consulte [copia de seguridad una aplicación web en el servicio de aplicación de Azure](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Introducción
solicita toosend REST, necesita la aplicación tooknow **nombre**, **grupo de recursos**, y **Id. de suscripción**. Esta información se puede encontrar haciendo clic en la aplicación en hello **servicio de aplicaciones** hoja de hello [portal de Azure](https://portal.azure.com). Para obtener ejemplos de hello en este artículo, nos estamos configuración de sitio Web de hello **backuprestoreapiexamples.azurewebsites.net**. Se almacena en el grupo de recursos de hello oesteee. UU. de Web predeterminado y se ejecuta en una suscripción con hello identificador 00001111-2222-3333-4444-555566667777.

![Información del sitio web de ejemplo][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>Copia de seguridad y restauración de API de REST
Ahora se explicará varios ejemplos de cómo toouse Hola toobackup de API de REST y restauración de una aplicación. Cada ejemplo incluye una dirección URL y un cuerpo de solicitud HTTP. dirección URL de ejemplo de Hola contiene marcadores de posición que se ajustan entre llaves, como {Id. de suscripción}. Reemplace los marcadores de posición de hello con la información correspondiente de hello para la aplicación. Como referencia, aquí es una explicación de cada marcador de posición que aparece en las direcciones URL de ejemplo de Hola.

* identificador de suscripción: Id. de aplicación de Hola de hello suscripción de Azure que lo contiene
* Resource-group-name: nombre de aplicación de hello contenedor de grupo de recursos de Hola
* nombre: nombre de la aplicación hello
* copia de seguridad-id: identificador de copia de seguridad de aplicación Hola

Para obtener documentación completa Hola de hello API, incluidos varios parámetros opcionales que pueden incluirse en la solicitud HTTP de hello, vea hello [Explorador de recursos de Azure](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Copia de seguridad de una aplicación a petición
tooback seguridad de una aplicación envíe inmediatamente, una **POST** solicitud demasiado**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ copia de seguridad /**.

Este es el aspecto de dirección URL de hello como el uso de nuestro sitio Web de ejemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

Proporcione un objeto JSON en el cuerpo de Hola de su toospecify de solicitud que toostore toouse de cuenta de almacenamiento Hola copia de seguridad. objeto JSON de Hello debe tener una propiedad denominada **storageAccountUrl**, que contiene un [URL de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) concesión de contenedor de almacenamiento de Azure de toohello de acceso de escritura que contiene el blob de copia de seguridad de Hola. Si desea tooback las bases de datos, también debe proporcionar una lista que contiene nombres de hello, tipos y las cadenas de conexión de hello las bases de datos toobe copia de seguridad.

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

Una copia de seguridad de la aplicación hello comienza inmediatamente cuando se recibe una solicitud Hola. proceso de copia de seguridad de Hello puede tardar un toocomplete mucho tiempo. Hola respuesta HTTP contiene un identificador que puede usar en otro estado de hello toosee la solicitud de copia de seguridad de Hola. Este es un ejemplo de cuerpo de Hola de solicitud de copia de seguridad de tooour de respuesta HTTP de Hola.

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
> Mensajes de error pueden encontrarse en la propiedad de registro de hello de hello respuesta HTTP.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Programación de copias de seguridad automáticas
En toobacking de adición de una aplicación a petición, también puede programar una copia de seguridad toohappen automáticamente.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Configuración de una nueva programación de copias de seguridad automáticas
tooset de una programación de copia de seguridad, envíe un **colocar** solicitud demasiado**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / copia de seguridad**.

Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

cuerpo de la solicitud de Hello debe tener un objeto JSON que especifica la configuración de copia de seguridad de Hola. Este es un ejemplo con todos los parámetros de hello necesario.

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

Este ejemplo configura Hola aplicación toobe copia automáticamente cada siete días. Hola parámetros **frequencyInterval** y **frequencyUnit** combinación determinan con qué frecuencia hello copias de seguridad realizan. Los valores válidos para **frequencyUnit** son **hora** y **día**. Por ejemplo, tooback seguridad de una aplicación cada 12 horas, establezca frequencyInterval too12 y frequencyUnit toohour.

Copias de seguridad antiguas se quitan automáticamente de la cuenta de almacenamiento de Hola. Puede controlar la antigüedad Hola pueden ser copias de seguridad mediante la configuración hello **retentionPeriodInDays** parámetro. Si desea que tooalways tiene al menos una copia de seguridad guardarlo, independientemente de su antigüedad, establecerla **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Obtener la programación de copia de seguridad automática de Hola
tooget una aplicación de copia de seguridad de configuración, enviar un **POST** toohello URL de solicitud **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sitios / {nombre} / config/copia de seguridad/lista**.

dirección URL de Hola para nuestro sitio de ejemplo es **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Obtener estado de Hola de una copia de seguridad
Según el tamaño aplicación hello es, una copia de seguridad puede tardar un rato toocomplete. Las copias de seguridad pueden también provocar errores, alargar el tiempo de espera o completarse solo parcialmente. Enviar estado de hello toosee de copias de seguridad de todas las de una aplicación, un **obtener** toohello URL de solicitud **https://management.azure.com/subscriptions/ {Id. de suscripción} / ResourceGroups / {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.

estado de hello toosee de una copia de seguridad específica, enviar una dirección URL toohello GET **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { copia de seguridad-id}**.

Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

cuerpo de respuesta de Hello contiene un ejemplo de toothis similar del objeto JSON.

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

estado de Hola de una copia de seguridad es un tipo enumerado. Mostramos, a continuación, todos los estados posibles.

* 0 – InProgress: copia de seguridad de Hola se ha iniciado pero no se ha completado.
* 1: no se pudo: copia de seguridad de hello tuvo éxito.
* 2 – correcta: copia de seguridad de Hola se completó correctamente.
* 3 – TimedOut: copia de seguridad de hello no terminó en el tiempo y se ha cancelado.
* 4: crear: solicitud de copia de seguridad de Hola se pone en cola pero no se ha iniciado.
* 5: omitidos: copia de seguridad de hello no continuar debido programación tooa desencadenar demasiadas copias de seguridad.
* 6: PartiallySucceeded: copia de seguridad de hello correcta, pero algunos archivos no se incluyeron porque no se puede leer. Esto suele suceder cuando se coloca un bloqueo exclusivo en archivos de Hola.
* 7: DeleteInProgress: copia de seguridad de hello ha sido solicitado toobe eliminado, pero aún no se ha eliminado.
* 8: DeleteFailed: no se pudo eliminar la copia de seguridad de Hola. Esto podría deberse a que expiró Hola dirección URL de SAS copia de seguridad de hello toocreate usado.
* 9: eliminar: copia de seguridad de Hola se eliminó correctamente.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Restauración de una aplicación desde una copia de seguridad
Si la aplicación se ha eliminado, o si desea toorevert la versión anterior de tooa la aplicación, puede restaurar la aplicación hello desde una copia de seguridad. tooinvoke una restauración, envíe un **POST** toohello URL de solicitud **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ las copias de seguridad / {Id. de copia de seguridad} / restore**.

Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**

En el cuerpo de la solicitud de hello, enviar un objeto JSON que contiene propiedades de hello para la operación de restauración de Hola. Este es un ejemplo que contiene todas las propiedades necesarias:

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

### <a name="restore-tooa-new-app"></a>Restaurar tooa nueva aplicación
En ocasiones es preferible toocreate una nueva aplicación cuando se restaura una copia de seguridad, en lugar de sobrescribir una aplicación ya existente. toodo, cambio Hola solicitud URL toopoint toohello nueva aplicación que desee toocreate y cambia hello **sobrescribir** propiedad Hola JSON demasiado**false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Eliminación de una copia de seguridad de aplicación
Si desea que toodelete una copia de seguridad, envíe un **eliminar** toohello URL de solicitud **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sitios / {nombre} /backups/ {Id. de copia de seguridad}**.

Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Administración de la dirección URL de SAS de una copia de seguridad
Servicio de aplicaciones de Azure intentará toodelete la copia de seguridad de almacenamiento de Azure con la dirección URL de SAS que se proporcionó cuando se creó la copia de seguridad de Hola Hola. Si esta dirección URL de SAS ya no es válida, no se puede eliminar la copia de seguridad de Hola a través de la API de REST de Hola. Sin embargo, puede actualizar Hola URL de SAS asociada a una copia de seguridad mediante el envío de un **POST** toohello URL de solicitud **https://management.azure.com/subscriptions/ {Id. de suscripción} / ResourceGroups / {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Este es el aspecto de dirección URL de Hola para nuestro sitio Web de ejemplo. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**

En el cuerpo de la solicitud de hello, enviar un objeto JSON que contiene la nueva dirección URL SAS Hola. Aquí tiene un ejemplo.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Por motivos de seguridad, Hola que URL de SAS asociada a una copia de seguridad no se devuelve al enviar una solicitud GET para una copia de seguridad específica. Si desea hello tooview URL de SAS asociada a una copia de seguridad, envíe un toohello de solicitud POST misma dirección URL anterior. Incluir un objeto JSON vacío en el cuerpo de la solicitud de saludo. respuesta de Hola desde servidor hello contiene toda información de copia de seguridad, incluida su dirección URL de SAS.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
