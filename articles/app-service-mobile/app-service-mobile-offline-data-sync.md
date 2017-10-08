---
title: "aaaOffline Data Sync en aplicaciones móviles de Azure | Documentos de Microsoft"
description: "Referencia conceptual e información general sobre la característica de sincronización de datos sin conexión de Hola para aplicaciones móviles de Azure"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Sincronización de datos sin conexión en Aplicaciones móviles de Azure
## <a name="what-is-offline-data-sync"></a>¿Qué es la sincronización de datos sin conexión?
Sincronización de datos sin conexión es un cliente y servidor característica SDK de aplicaciones móviles de Azure que facilita a los desarrolladores toocreate aplicaciones que funcionan siempre, sin una conexión de red.

Cuando la aplicación está en modo sin conexión, puede crear y modificar los datos, que se guardan el almacén local de tooa. Cuando la aplicación hello es nuevo en línea, puede sincronizar los cambios locales con el back-end de aplicación móvil de Azure. característica de Hello también incluye compatibilidad para detectar los conflictos cuando Hola se cambia el mismo registro en ambos Hola cliente y Hola back-end. Conflictos, a continuación, pueden controlarse en el servidor de Hola o cliente Hola.

La sincronización sin conexión tiene varias ventajas:

* Mejorar la capacidad de respuesta de la aplicación al almacenamiento en caché de datos del servidor local en el dispositivo de Hola
* Creación de aplicaciones sólidas que sigan siendo útiles cuando hay problemas de red
* Permitir toocreate de los usuarios finales y modificar datos, incluso cuando no hay ningún acceso a la red, es posible admitir escenarios con poca o ninguna conectividad
* Sincronizar datos entre varios dispositivos y detectar conflictos cuando hello misma se modifica el registro por dos dispositivos
* Limitar el uso de las redes medidas o de alta latencia

Hola tutoriales muestra cómo tooadd sin conexión sincronizar a clientes móviles tooyour con aplicaciones móviles de Azure:

* [Android: habilitar la sincronización sin conexión]
* [Apache Cordova: habilitación de la sincronización sin conexión](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS: habilitar la sincronización sin conexión]
* [Xamarin iOS: habilitar la sincronización sin conexión]
* [Xamarin Android: habilitar la sincronización sin conexión]
* [Xamarin.Forms: habilitar la sincronización sin conexión](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [Plataforma universal de Windows: habilitación de la sincronización sin conexión]

## <a name="what-is-a-sync-table"></a>¿Qué es una tabla de sincronización?
Hola tooaccess "/ tablas" punto de conexión, cliente de Azure Mobile Hola SDK proporcionan interfaces como `IMobileServiceTable` (cliente de .NET SDK) o `MSTable` (cliente de iOS). Estas API conectan directamente back-end de toohello aplicación móvil de Azure y se producirá un error si el dispositivo de cliente hello no tiene una conexión de red.

toosupport uso sin conexión, la aplicación en su lugar, debe usar hello *tabla sincronización* API, como `IMobileServiceSyncTable` (cliente de .NET SDK) o `MSSyncTable` (cliente de iOS). Hola todas las mismas operaciones CRUD (creación, lectura, actualización, eliminación) funcionan con la sincronización de las API de tabla, salvo que se lean de o escribir tooa *almacén local*. Para poder realizar cualquier operación de tabla de sincronización, se debe inicializar el almacén local de Hola.

## <a name="what-is-a-local-store"></a>¿Qué es un almacén local?
Un almacén local es la capa de persistencia de datos de hello en dispositivo de cliente de Hola. implementación de almacén de cliente de aplicaciones móviles de Azure Hola SDK proporcionan una configuración regional predeterminada. En Windows, Xamarin y Android, se basa en SQLite. En iOS, se basa en Core Data.

toouse Hola SQLite implementación basada en Windows Phone o la tienda Windows 8.1, deberá tooinstall una extensión de SQLite. Para más información, consulte [Plataforma universal de Windows: habilitación de la sincronización sin conexión]. IOS y Android se distribuye con una versión de código en el sistema operativo, por lo que no es necesario tooreference su propia versión de código de dispositivo de Hola.

Los desarrolladores también pueden implementar su propio almacén local. Por ejemplo, si desea que toostore datos en un formato cifrado en el cliente móvil hello, puede definir un almacén local que usa SQLCipher para el cifrado.

## <a name="what-is-a-sync-context"></a>¿Qué es un contexto de sincronización?
Un *contexto de sincronización* está asociado a un objeto de cliente móvil (como `IMobileServiceClient` o `MSClient`) y realiza el seguimiento de los cambios que se realizan con las tablas de sincronización. contexto de sincronización de Hello mantiene un *cola de operación*, que mantiene una lista ordenada de operaciones CUD (Create, Update, Delete) que es una versión posterior, se enviarán toohello server.

Un almacén local está asociado con el contexto de sincronización de hello mediante un método de inicialización como `IMobileServicesSyncContext.InitializeAsync(localstore)` en hello [cliente .NET SDK].

## <a name="how-sync-works"></a>Funcionamiento de la sincronización sin conexión
Al usar tablas de sincronización, el código de cliente determina el momento en que se sincronizan los cambios locales con un back-end de Azure Mobile App. No se envía nada toohello back-end hasta que haya una llamada*inserción* cambios locales. De forma similar, almacén local de Hola se rellena con datos nuevos solo cuando hay una llamada*extracción* datos.

* **Inserción**: inserción es una operación en el contexto de sincronización de Hola y envía todos los cambios CUD desde la última inserción de Hola. Tenga en cuenta que TI es toosend no es posible sólo los cambios de una tabla individual, ya que en caso contrario, las operaciones podrían enviarse fuera de servicio. Inserción ejecuta una serie de REST llamadas tooyour aplicación móvil de Azure back-end, lo que a su vez modifica la base de datos de servidor.
* **Extraer**: extracción se realiza en una base por cada tabla y se puede personalizar con una consulta tooretrieve solo un subconjunto de datos del servidor hello. Hola SDK de cliente de Azure Mobile, a continuación, insertar los datos resultantes de hello en almacén local de Hola.
* **Inserciones implícita**: si una extracción se ejecuta en una tabla que tiene las actualizaciones locales pendientes, extracción de hello en primer lugar se ejecuta un `push()` en el contexto de sincronización de Hola. Esta inserción le ayuda a minimizar los conflictos entre los cambios que ya se ponen en cola y los nuevos datos del servidor de Hola.
* **Sincronización incremental**: Hola primer parámetro toohello extracción operación es un *nombre de la consulta* que sólo se utiliza en el cliente de Hola. Si utiliza un nombre de consulta no null, Hola SDK de Azure Mobile realiza una *sincronización incremental*. Cada vez que una operación de extracción devuelve un conjunto de resultados, Hola más reciente `updatedAt` marca de tiempo de ese conjunto de resultados se almacena en tablas de sistema local del SDK de Hola. Las operaciones de extracción posteriores solo recuperarán registros después de esa marca de tiempo.

  toouse sincronización incremental, el servidor debe devolver significativo `updatedAt` valores y también debe admitir la ordenación por este campo. Sin embargo, puesto que Hola SDK agrega su propio ordenación en el campo de updatedAt hello, no puede usar una consulta de extracción que tiene su propio `orderBy` cláusula.

  nombre de la consulta de Hello puede ser cualquier cadena que elija, pero debe ser único para cada consulta lógica en la aplicación.
  De lo contrario, las operaciones de extracción diferentes pudieron sobrescribir Hola misma marca de tiempo de sincronización incremental y las consultas pueden devolver resultados incorrectos.

  Si consulta hello tiene un parámetro, toocreate una forma de un nombre de consulta única es el valor del parámetro hello tooincorporate.
  Por ejemplo, si está filtrando por userid, el nombre de consulta podría ser el siguiente (en C#):

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  Si desea tooopt dejen de estar sincronizados incremental, pase `null` como Hola Id. de consulta. En este caso, se recuperan todos los registros en cada llamada demasiado`PullAsync`, que es potencialmente ineficaz.
* **Purga**: puede borrar el contenido de hello del uso del almacén local de hello `IMobileServiceSyncTable.PurgeAsync`.
  Purga puede ser necesaria si tiene datos obsoletos en la base de datos de cliente de hello, o si desea toodiscard todos los cambios pendientes.

  Una purga borra una tabla desde el almacén local Hola. Si no hay operaciones de espera de sincronización con la base de datos de servidor de hello, Hola purga inicia una excepción a menos que Hola *forzar purga* parámetro está establecido.

  Como ejemplo de datos obsoletos en el cliente de hello, suponga que en el ejemplo de "lista de tareas" ¡hello, dispositivo1 extrae sólo los elementos que no se han completado. Todoitem "Comprar leche" está marcado como completado en el servidor de Hola por otro dispositivo. Sin embargo, dispositivo1 aún hello todoitem "Comprar leche" en el almacén local porque solo extrae elementos que no están marcado completa. Una purga borra este elemento obsoleto.

## <a name="next-steps"></a>Pasos siguientes
* [iOS: habilitar la sincronización sin conexión]
* [Xamarin iOS: habilitar la sincronización sin conexión]
* [Xamarin Android: habilitar la sincronización sin conexión]
* [Plataforma universal de Windows: habilitación de la sincronización sin conexión]

<!-- Links -->
[cliente .NET SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android: habilitar la sincronización sin conexión]: app-service-mobile-android-get-started-offline-data.md
[iOS: habilitar la sincronización sin conexión]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: habilitar la sincronización sin conexión]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android: habilitar la sincronización sin conexión]: app-service-mobile-xamarin-android-get-started-offline-data.md
[Plataforma universal de Windows: habilitación de la sincronización sin conexión]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
