---
title: "aaaImport y exportar datos en caché en Redis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooimport y exportación tooand de datos de almacenamiento de blobs con las instancias de caché en Redis de Azure premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a>Importación y exportación de datos en la Caché en Redis de Azure
Importación y exportación es una operación de administración de datos de Azure Redis Cache, que permite tooimport datos en caché en Redis de Azure o exportar los datos de caché en Redis de Azure mediante la importación y exportación de una instantánea de base de datos de caché de Redis (RDB) de un blob de tooa de caché premium en un Azure Cuenta de almacenamiento. 

- **Exportar** -puede exportar su tooa de instantáneas de RDB caché Redis de Azure Blob en páginas.
- **Importar**: Puede importar las instantáneas de RDB de Redis Cache desde de un blob en páginas o un blob en bloques.

Importación y exportación permite toomigrate entre distintas instancias de caché en Redis de Azure o rellenar Hola caché con los datos antes de su uso.

Este artículo proporciona una guía para importar y exportar datos con caché en Redis de Azure y se proporcionan respuestas hello toocommonly preguntas más frecuentes.

> [!IMPORTANT]
> Importación/Exportación es una característica en versión preliminar y solo está disponible para las cachés de [nivel premium](cache-premium-tier-intro.md) .
>
>

## <a name="import"></a>Importación
Importación puede ser toobring usado Redis compatible RDB archivos desde cualquier servidor de Redis que se ejecute en cualquier nube o el entorno, incluidos Redis que se ejecutan en Linux, Windows o cualquier proveedor de nube, como Amazon Web Services y otros. Importación de datos es un toocreate fácilmente una memoria caché con datos rellenadas previamente. Durante el proceso de importación de hello, caché en Redis de Azure carga archivos RDB Hola del almacenamiento de Azure en la memoria y, a continuación, inserta las claves de hello en memoria caché de Hola.

> [!NOTE]
> Antes de comenzar la operación de importación de hello, asegúrese de que el archivo de base de datos Redis (RDB) o archivos se cargan en la página o blobs en bloques en almacenamiento de Azure, en hello misma región y suscripción que la instancia de caché de Redis de Azure. Para obtener información, vea [Introducción al Almacenamiento de blobs de Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Si ha exportado el archivo RDB con hello [exportar caché Redis de Azure](#export) característica, el archivo RDB ya está almacenado en un blob en páginas y está listo para la importación.
>
>

1. tooimport uno o más exportar blobs de caché, [examinar la caché de tooyour](cache-configure.md#configure-redis-cache-settings) en Hola portal de Azure y haga clic en **importar datos** de hello **menú recursos**.

    ![Importar datos][cache-import-data]
2. Haga clic en **Blob(s) elegir** y seleccione la cuenta de almacenamiento de Hola que contiene hello tooimport de datos.

    ![Selección de la cuenta de almacenamiento][cache-import-choose-storage-account]
3. Haga clic en el contenedor Hola Hola datos tooimport.

    ![Elegir contenedor][cache-import-choose-container]
4. Seleccione uno o más tooimport blobs haciendo clic en hello área toohello izquierda del nombre de blob de hello y, a continuación, haga clic en **seleccione**.

    ![Elegir blobs][cache-import-choose-blobs]
5. Haga clic en **importar** proceso de importación de toobegin Hola.

   > [!IMPORTANT]
   > memoria caché de Hello no está accesible para los clientes de caché durante el proceso de importación de Hola y se eliminan los datos existentes en la memoria caché de Hola.
   >
   >

    ![Importación][cache-import-blobs]

    Se puede supervisar el progreso de Hola de operación de importación de hello siguientes notificaciones Hola de hello portal de Azure, o consultando eventos Hola Hola [registro de auditoría](../azure-resource-manager/resource-group-audit.md).

    ![Progreso de la importación][cache-import-data-import-complete]

## <a name="export"></a>Exportación
Exportación permite datos de hello tooexport almacenados en caché en Redis de Azure tooRedis compatible RDB archivos. Puede usar estos datos de toomove característica de una caché en Redis de Azure instancia tooanother o un servidor de Redis tooanother. Durante el proceso de exportación de hello, se crea un archivo temporal en hello VM que hosts Hola instancia del servidor de caché en Redis de Azure y archivo hello toohello cargado designado de la cuenta de almacenamiento. Cuando se completa la operación de exportación de hello con estado de éxito o error, se elimina el archivo temporal de Hola.

1. contenido actual de hello tooexport de hello caché toostorage, [examinar la caché de tooyour](cache-configure.md#configure-redis-cache-settings) en Hola portal de Azure y haga clic en **exportar datos** de hello **menú recursos**.

    ![Elegir el contenedor de almacenamiento][cache-export-data-choose-storage-container]
2. Haga clic en **elegir contenedor de almacenamiento** y seleccione la cuenta de almacenamiento de hello deseado. cuenta de almacenamiento de Hello debe estar en hello misma suscripción y región que la memoria caché.

   > [!IMPORTANT]
   > La exportación funciona con blobs en páginas, que son compatibles con las cuentas de almacenamiento del modelo clásico y de Resource Manager, aunque en este momento no lo son con las [cuentas de Blob Storage](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).
   >
   >

    ![Cuenta de almacenamiento][cache-export-data-choose-account]
3. Elija Hola deseado contenedor de blobs y haga clic en **seleccione**. toouse nuevo contenedor, haga clic en **agregar contenedor** tooadd primero y, a continuación, seleccione de la lista de Hola.

    ![Elegir el contenedor de almacenamiento][cache-export-data-container]
4. Escriba un **el prefijo del nombre de Blob** y haga clic en **exportar** proceso de exportación de toostart Hola. prefijo del nombre de blob de Hello es tooprefix usado Hola nombres de los archivos generados por esta operación de exportación.

    ![Exportación][cache-export-data]

    Se puede supervisar el progreso de Hola de operación de exportación de hello siguientes notificaciones Hola de hello portal de Azure, o consultando eventos Hola Hola [registro de auditoría](../azure-resource-manager/resource-group-audit.md).

    ![Exportación de datos completa][cache-export-data-export-complete]

    Las memorias caché siguen estando disponibles para su uso durante el proceso de exportación de Hola.

## <a name="importexport-faq"></a>P+F de Importación/Exportación
Esta sección contiene las preguntas más frecuentes acerca de la característica de importación y exportación de Hola.

* [¿Con qué planes de tarifa se puede usar Importación/Exportación?](#what-pricing-tiers-can-use-importexport)
* [¿Puedo importar datos desde cualquier servidor de Redis?](#can-i-import-data-from-any-redis-server)
* [¿Qué versiones de RDB puedo importar?](#what-rdb-versions-can-i-import)
* [¿La memoria caché estará disponible durante una operación de Import/Export?](#is-my-cache-available-during-an-importexport-operation)
* [¿Puedo utilizar Importación/Exportación con un clúster de Redis?](#can-i-use-importexport-with-redis-cluster)
* [¿Cómo funciona la importación y exportación con una configuración de bases de datos personalizada?](#how-does-importexport-work-with-a-custom-databases-setting)
* [¿En qué se diferencia Importación/Exportación de la persistencia de Redis?](#how-is-importexport-different-from-redis-persistence)
* [¿Puedo automatizar Importación/Exportación mediante PowerShell, la CLI u otros clientes de administración?](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [He recibido un error de tiempo de espera durante la operación de Importación/Exportación. ¿Qué significa esto?](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [Recibe un error al exportar mi tooAzure datos del almacenamiento de blobs. ¿Qué ha ocurrido?](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>¿Con qué planes de tarifa se puede usar Importación/Exportación?
Importación/exportación solo está disponible en premium Hola nivel de precios.

### <a name="can-i-import-data-from-any-redis-server"></a>¿Puedo importar datos desde cualquier servidor de Redis?
Sí, además tooimporting datos exportados de instancias de caché en Redis de Azure, puede importar archivos RDB desde cualquier servidor de Redis que se ejecute en cualquier nube o el entorno, como proveedores de nube como Amazon Web Services, Windows o Linux. toodo esto, carga Hola RDB el archivo del servidor de Redis Hola deseado en un blob en bloques o en páginas en una cuenta de almacenamiento de Azure y, a continuación, importar, a la instancia de caché en Redis de Azure premium. Por ejemplo, puede desee datos de hello tooexport desde la memoria caché de producción e importarlo en una memoria caché que se usa como parte de un entorno de ensayo para pruebas o la migración.

> [!IMPORTANT]
> toosuccessfully importar datos exportados desde servidores de Redis distintos caché en Redis de Azure al uso de un blob en páginas, el tamaño del blob de página Hola debe estar alineado en un límite de 512 bytes. Para tooperform de código de ejemplo las necesarias relleno de bytes, vea [carga de blog de página de ejemplo](https://github.com/JimRoberts-MS/SamplePageBlobUpload).
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>¿Qué versiones de RDB puedo importar?

Azure Redis Cache admite la importación RDB hasta la versión 7 de RDB.

### <a name="is-my-cache-available-during-an-importexport-operation"></a>¿La memoria caché estará disponible durante una operación de Import/Export?
* **Exportar** : memorias caché siguen estando disponibles y puede continuar toouse la memoria caché durante una operación de exportación.
* **Importar** : memorias caché dejan de estar disponibles cuando se inicia una operación de importación y estén disponibles para su uso cuando se complete la operación de importación de Hola.

### <a name="can-i-use-importexport-with-redis-cluster"></a>¿Puedo utilizar Importación/Exportación con un clúster de Redis?
Sí, y puede importar/exportar entre una caché en clústeres y una caché que no esté en clústeres. Puesto que el clúster de Redis [solo admite la base de datos 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), solo se importarán los datos de la base de datos 0. Cuando se importan datos de caché en clúster, las claves de Hola se redistribuyen entre particiones Hola de clúster de Hola.

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>¿Cómo funciona la importación y exportación con una configuración de bases de datos personalizada?
Algunos niveles de precios tienen diferentes [límites de las bases de datos](cache-configure.md#databases), por lo que hay algunas consideraciones al importar si configura un valor personalizado para hello `databases` establecer durante la creación de la memoria caché.

* Al importar tooa tarifa con un menor `databases` límite de nivel de Hola desde el que exportó:
  * Si usas el número predeterminado de Hola de `databases`, que es 16 para todos los niveles de precios, se perderá ningún dato.
  * Si usas un número personalizado de `databases` que se encuentra dentro de los límites de Hola para hello interconectar toowhich va a importar, se perderá ningún dato.
  * Si los datos exportados incluían datos en una base de datos que supera los límites de Hola de nuevo nivel de hello, no se importan datos Hola de esas bases de datos mayor.

### <a name="how-is-importexport-different-from-redis-persistence"></a>¿En qué se diferencia Importación/Exportación de la persistencia de Redis?
Persistencia de caché en Redis de Azure permite toopersist los datos almacenados en Redis tooAzure almacenamiento. Cuando se configura la persistencia, caché en Redis de Azure mantiene una instantánea de memoria caché de Redis de hello en un toodisk de formato binario de Redis tomando como base una frecuencia de copia de seguridad configurable. Si se produce un evento grave que deshabilita la caché de réplica y de saludo principal, datos de la caché de Hola se restauran automáticamente con la instantánea más reciente de Hola. Para obtener más información, consulte [la persistencia de los datos de una caché en Redis de Azure Premium tooconfigure](cache-how-to-premium-persistence.md).

Importación / exportación permite toobring datos o la exportación de caché en Redis de Azure. No configura la copia de seguridad y restauración mediante la persistencia de Redis.

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>¿Puedo automatizar Importación/Exportación mediante PowerShell, la CLI u otros clientes de administración?
Sí, para PowerShell instrucciones consulte [tooimport una caché de Redis](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) y [tooexport una caché de Redis](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>He recibido un error de tiempo de espera durante la operación de Importación/Exportación. ¿Qué significa?
Si permanece en Hola **importar datos** o **exportar datos** hoja durante más de 15 minutos antes de iniciar la operación de hello, recibirá un error con un toohello similar de mensaje de error siguiente ejemplo:

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve, iniciar la importación de Hola o exportar operación antes de que haya transcurrido 15 minutos.

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>Recibe un error al exportar mi tooAzure datos del almacenamiento de blobs. ¿Qué ha ocurrido?
La exportación solo funciona con archivos RDB almacenados como blobs en páginas. No se admiten otros tipos de blob en este momento, incluidas las cuentas de Blob Storage con niveles de acceso frecuente y esporádico. Para más información, consulte [Cuentas de Blob Storage](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo toouse premium más características de caché.

* [Nivel de introducción toohello Premium de caché de Redis de Azure](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
