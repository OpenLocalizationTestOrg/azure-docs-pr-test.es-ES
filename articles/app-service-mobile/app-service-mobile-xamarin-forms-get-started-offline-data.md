---
title: "aaaEnable la sincronización sin conexión de la aplicación móvil de Azure (Xamarin.Forms) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse la toocache y sincronización de datos sin conexión de aplicación del servicio de aplicaciones móviles en la aplicación de Xamarin.Forms"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Habilitación de la sincronización sin conexión para la aplicación móvil Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Información general
Este tutorial presenta la característica de sincronización sin conexión de Hola de aplicaciones móviles de Azure para Xamarin.Forms. La sincronización sin conexión permite a los usuarios finales interactuar con una aplicación móvil (ver, agregar o modificar datos), incluso cuando no hay ninguna conexión de red. Los cambios se almacenan en una base de datos local. Una vez que el dispositivo de hello vuelve a estar conectado, estos cambios se sincronizan con el servicio remoto hello.

Este tutorial se basa en hello solución de inicio rápido de Xamarin.Forms para las aplicaciones móviles que crea al completar el tutorial [crear una aplicación de iOS de Xamarin]. solución de inicio rápido de Hola para Xamarin.Forms contiene Hola código toosupport sincronización sin conexión, que solo necesita toobe habilitado. En este tutorial, va a actualizar hello tooturn de solución de inicio rápido sobre características sin conexión de Hola de aplicaciones móviles de Azure. También se resalte código de sin conexión específicas de hello en la aplicación hello. Si no utiliza soluciones de inicio rápido de hello descargado, debe agregar el proyecto tooyour de paquetes de extensión de acceso de hello datos. Para obtener más información acerca de los paquetes de extensión de servidor, consulte [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure][1].

toolearn más información acerca de la característica de sincronización sin conexión de hello, vea el tema de hello [sincronización de datos sin conexión en aplicaciones móviles de Azure][2].

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Habilitar la funcionalidad de sincronización sin conexión en la solución de inicio rápido de Hola
código de sincronización sin conexión de Hola se incluye en el proyecto de hello mediante el uso de directivas de preprocesador de C#. Cuando Hola **sin conexión\_sincronización\_habilitado** símbolo está definido, estas rutas de acceso de código se incluyen en la compilación de Hola. Para las aplicaciones de Windows, también debe instalar platform de SQLite Hola.

1. En Visual Studio, haga clic en soluciones de hello > **administrar paquetes de NuGet para la solución...** , a continuación, buscar e instalar el **Microsoft.Azure.Mobile.Client.SQLiteStore** paquete NuGet para todos los proyectos de la solución de Hola.
2. Hola el Explorador de soluciones, abra el archivo TodoItemManager.cs de hello del proyecto de Hola con **Portable** en nombre de hello, que es el proyecto de biblioteca de clases Portable, a continuación, quite Hola después de la directiva de preprocesador:

        #define OFFLINE_SYNC_ENABLED
3. Dispositivos de Windows toosupport (opcional), instale uno de los siguientes paquetes en tiempo de ejecución de código de hello:

   * **Runtime de Windows 8.1:** instale [SQLite para Windows 8.1][3].
   * **Windows Phone 8.1:** instale [SQLite para Windows Phone 8.1][4].
   * **Plataforma universal de Windows** instalar [SQLite para hello universales de Windows Universal][5].

     Aunque el inicio rápido de hello no contiene un proyecto Universal de Windows, plataforma Universal de Windows de hello es compatible con Xamarin Forms.
4. (Opcional) En cada proyecto de aplicación de Windows, haga clic en **referencias** > **Agregar referencia...** , expanda hello **Windows** carpeta > **extensiones**.
    Habilitar Hola adecuado **SQLite para Windows** SDK junto con hello **2013 en tiempo de ejecución para Windows de Visual C++** SDK.
    Hello SQLite SDK nombres varían ligeramente con cada plataforma de Windows.

## <a name="review-hello-client-sync-code"></a>Revise el código de sincronización de cliente hello
Esta es una breve descripción de lo que ya está incluido en el código del tutorial Hola Hola `#if OFFLINE_SYNC_ENABLED` directivas. La funcionalidad de sincronización sin conexión está en archivo de proyecto TodoItemManager.cs de hello en el proyecto de biblioteca de clases Portable Hola. Para obtener información conceptual de característica de hello, consulte [sin conexión la sincronización de datos en aplicaciones de Azure Mobile][2].

* Para poder realizar cualquier operación de tabla, se debe inicializar el almacén local de Hola. base de datos del almacén local Hello se inicializa una Hola **TodoItemManager** constructor de clase mediante el uso de hello siguiente código:

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    Este código crea una nueva base de SQLite local mediante hello **MobileServiceSQLiteStore** clase.

    Hola **DefineTable** método crea una tabla de almacén local de Hola que coincida con los campos de hello en el tipo de hello proporcionado.  tipo de Hello no tiene tooinclude todas las columnas de Hola que se encuentran en la base de datos remota Hola. Es posible toostore un subconjunto de columnas.
* Hola **todoTable** campo **TodoItemManager** es un **IMobileServiceSyncTable** escriba en lugar de **IMobileServiceTable**. Esta clase usa Hola base de datos local para todos los crear, leer, actualizar y eliminar operaciones (CRUD) de la tabla. Decidir si esos cambios se insertan back-end de aplicación móvil de toohello mediante una llamada a **PushAsync** en hello **IMobileServiceSyncContext**. Hello contexto de sincronización le ayuda a mantener las relaciones entre tablas de seguimiento e insertar los cambios en todas las tablas de una aplicación cliente modifica cuando **PushAsync** se llama.

    siguiente Hello **SyncAsync** toosync con back-end de aplicación móvil de Hola se llama al método:

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    Este ejemplo usa con el controlador de sincronización predeterminado de Hola de control de errores simple. Una aplicación real controlaría Hola varios errores al igual que las condiciones de red y el servidor está en conflicto mediante el comparador **IMobileServiceSyncHandler** implementación.

## <a name="offline-sync-considerations"></a>Consideraciones sobre la sincronización sin conexión
En el ejemplo de Hola Hola **SyncAsync** solo es llamar al método de inicio y cuando se solicita una sincronización.  tooinitiate una sincronización en una aplicación de Android o iOS, extracción hacia abajo en la lista de elementos de hello; para Windows, utilice hello **sincronización** botón. En una aplicación del mundo real, que podría realizar desencadenador de sincronización de hello cuando cambia el estado de la red de Hola.

Cuando se ejecuta una extracción en una tabla que tiene pendiente actualizaciones locales realiza un seguimiento mediante el contexto de hello, que extraen operación automáticamente desencadenadores una inserción de contexto anterior. Al actualizar, agregar y completar los elementos en este ejemplo, puede omitir Hola explícita **PushAsync** llamar.

En el código de hello proporcionada, se consultan todos los registros de la tabla TodoItem remota de hello, pero también es posible toofilter registros pasando un identificador de la consulta y una consulta demasiado**PushAsync**. Para obtener más información, vea la sección de hello *sincronización Incremental* en [sin conexión la sincronización de datos en aplicaciones de Azure Mobile][2].

## <a name="run-hello-client-app"></a>Ejecutar la aplicación de cliente hello
Con ahora habilitada la sincronización sin conexión, ejecutar aplicación de cliente de hello al menos una vez en cada base de datos de almacén local de plataforma toopopulate Hola. Más adelante, simular un escenario sin conexión y modificar datos de hello en el almacén local de hello mientras está sin conexión la aplicación hello.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Comportamiento de sincronización de Hola de aplicación de cliente de hello de la actualización
En esta sección, modificar Hola cliente proyecto toosimulate un escenario sin conexión mediante una dirección URL de aplicación no válido para el back-end. Como alternativa, puede desactivar las conexiones de red, mueva el dispositivo demasiado "Modo de avión".  Al agregar o cambiar los elementos de datos, estos cambios se conservan en el almacén local de hello, pero no sincronizan datos de back-end de toohello almacenan hasta que se haya restablecido la conexión de Hola.

1. Hola el Explorador de soluciones, abra el archivo de proyecto de Constants.cs de Hola de hello **Portable** del proyecto y cambiar el valor de Hola de `ApplicationURL` toopoint dirección URL no válida de tooan:

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. Archivo de TodoItemManager.cs de hello abierto de hello **Portable** del proyecto, a continuación, agregue un **catch** para hello base **excepción** toohello de clase **try... catch** bloquear **SyncAsync**. Esto **catch** bloque escribe consola de toohello de mensaje de excepción de hello, como se indica a continuación:

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. Compile y ejecute la aplicación de cliente de hello.  Agregue nuevos elementos. Tenga en cuenta que una excepción se registra en la consola de Hola para cada toosync intento con hello back-end. Estos nuevos elementos de solo existen en el almacén local de Hola hasta que estos se pueden insertar back-end de toohello móvil. aplicación de cliente de Hello se comporta como si estuviera conectado toohello back-end admitir que todos crear, leer, actualizar, las operaciones de eliminación (CRUD).
4. Cierre la aplicación hello y reiníciela tooverify que elementos nuevos de Hola que creó están almacén local toohello persistente.
5. (Opcional) Use Visual Studio tooview su toosee de tabla de base de datos de SQL Azure Hola datos en la base de datos de back-end de hello no han cambiado.

    En Visual Studio, abra el **Explorador de servidores**. Navegar por la base de datos de tooyour en **Azure**->**bases de datos SQL**. Haga clic con el botón derecho en la base de datos y seleccione **Abrir en el Explorador de objetos de SQL Server**. Ahora puede examinar la tabla de base de datos SQL tooyour y su contenido.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>Actualizar tooreconnect de aplicación de cliente de hello en el back-end móvil
En esta sección, vuelva a conectar hello toohello móviles backend de la aplicación, que simula la aplicación hello viniendo tooan de estado en línea. Al realizar gestos de actualización de hello, datos están móvil tooyour sincronizados back-end.

1. Vuelva a abrir Constants.cs. Hola correcto `applicationURL` toopoint toohello corrija la dirección URL.
2. Volver a generar y ejecutar la aplicación de cliente de hello. aplicación Hello intenta toosync con back-end de aplicación móvil de hello después de iniciar. Compruebe que ninguna excepción se registra en la consola de depuración de Hola.
3. (Opcional) Hola vista actualiza datos mediante el Explorador de objetos de SQL Server o una herramienta REST como Fiddler o [Postman][6]. Se ha sincronizado aviso Hola datos entre la base de datos de back-end de Hola y el almacén local de Hola.

    Tenga en cuenta datos Hola se ha sincronizado entre la base de datos de Hola y el almacén local de Hola y contiene elementos de hello que agregó mientras la aplicación se desconectó.

## <a name="additional-resources"></a>Recursos adicionales
* [Sincronización de datos sin conexión en Azure Mobile Apps][2]
* [Procedimiento del SDK de .NET de Azure Mobile Apps][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
