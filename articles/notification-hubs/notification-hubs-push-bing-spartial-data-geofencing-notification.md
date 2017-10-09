---
title: "notificaciones de inserción delimitados aaaGeo con centros de notificaciones de Azure y los datos espaciales de Bing | Documentos de Microsoft"
description: "En este tutorial, aprenderá cómo toodeliver basada en la ubicación de inserción notificaciones con centros de notificaciones de Azure y los datos espaciales de Bing."
services: notification-hubs
documentationcenter: windows
keywords: "notificación push, notificación push"
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Notificaciones push geovalladas con los Centros de notificaciones de Azure y datos espaciales de Bing
> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).
> 
> 

En este tutorial, aprenderá cómo toodeliver basada en la ubicación de inserción notificaciones con centros de notificaciones de Azure y los datos espaciales de Bing, aprovecha desde dentro de una aplicación de plataforma Universal de Windows.

## <a name="prerequisites"></a>Requisitos previos
En primer lugar y ante todo, deberá toomake Asegúrese de que tiene todos los Hola software y servicio de requisitos previos:

* [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) o posterior ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) también servirá). 
* La versión más reciente de hello [Azure SDK](https://azure.microsoft.com/downloads/). 
* [Cuenta del Centro de desarrollo de Bing Maps](https://www.bingmapsportal.com/) (puede crear una gratis y asociarla a su cuenta de Microsoft). 

## <a name="getting-started"></a>Introducción
Empecemos creando proyecto Hola. En Visual Studio, inicie un nuevo proyecto de tipo **Aplicación vacía (Windows universal)**.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Una vez completada la creación del proyecto de hello, debe tener el instrumento de hello para la propia aplicación Hola. Ahora vamos a configurar todos los elementos de infraestructura de barrera geográfica Hola. Ya que estamos toouse continuo de servicios de Bing para que esto, hay un punto de conexión de API de REST público que nos permite tooquery marcos de ubicación específica:

    http://spatial.virtualearth.net/REST/v1/data/

Necesitará toospecify Hola siguientes tooget de parámetros que funcione:

* **Id. de origen de datos** y **Nombre de origen de datos**: en la API de Bing Maps, los orígenes de datos contienen distintos metadatos en depósitos, como las ubicaciones y el horario comercial de la operación. Puede leer más sobre ellos aquí. 
* **Nombre de la entidad** : Hola entidad que desee toouse como punto de referencia para la notificación de Hola. 
* **Clave de API de mapas de Bing** : se trata de clave de Hola que ha obtenido antes cuando se creó la cuenta del centro de desarrollo de Bing Hola.

Vamos a hacer un análisis más profundo en el programa de instalación de Hola para cada uno de los elementos de hello anteriores.

## <a name="setting-up-hello-data-source"></a>Configurar origen de datos de Hola
Puede hacerlo en hello centro de desarrollo de mapas de Bing. Haga clic en **orígenes de datos** en hello superior barra de navegación y seleccione **administrar orígenes de datos**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Si no ha trabajado con la API de Bing Maps antes, probablemente no haber ningún origen de datos está presente, por lo que solo puede crear uno nuevo, haga clic en el origen de datos de tooa de datos de carga. Asegúrese de que rellene todos los campos de hello necesario:

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

Tal vez se pregunte: ¿qué es el archivo de datos de hello y lo que debe puede cargar? Para fines de Hola de esta prueba, podemos utilizar ejemplo Hola basados en canalizaciones que rodea un área al mar de San Francisco hello:

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Hola anterior representa esta entidad:

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

Simplemente copie y pegue cadena Hola anterior en un nuevo archivo y guárdelo como **NotificationHubsGeofence.pipe**y cargarlo en hello centro de desarrollo de Bing.

> [!NOTE]
> Es posible que toospecify solicitada una nueva clave para hello **clave maestra** que es diferente de hello **clave de consulta**. Basta con crear una nueva clave a través de hello panel y la actualización de hello página origen de datos carga.
> 
> 

Una vez que cargue el archivo de datos de hello, necesitará toomake seguro de que publique el origen de datos de Hola. 

Vaya demasiado**administrar orígenes de datos**, igual que hicimos anteriormente, busque el origen de datos en la lista de Hola y haga clic en **publicar** en hello **acciones** columna. En un bit, debería ver el origen de datos en hello **orígenes de datos publicados** ficha:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

Si hace clic en **editar**, será capaz de toosee un vistazo qué ubicaciones se introdujo en ella:

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

En este momento, portal de hello no muestra Hola límites para geofence Hola que creamos: lo único que necesita es una confirmación que Hola especificado se encuentra en proximidad derecho Hola.

Ahora tiene todos los requisitos de Hola Hola origen de datos. Haga clic en detalles de hello tooget en dirección URL de solicitud de Hola para llamada de API hello, Hola centro de desarrollo de mapas de Bing, **orígenes de datos** y seleccione **información de origen de datos**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Hola **URL de consulta** que estamos después aquí. Se trata de punto de conexión de hello en el que podemos ejecutar consultas toocheck si Hola dispositivo actualmente dentro de una ubicación de los límites de Hola o no. tooperform esta comprobación, sólo será necesario tooexecute una operación GET llame a con la dirección URL de consulta de hello, con hello parámetros anexados siguientes:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

De este modo se está especificando un punto de destino que obtenemos desde dispositivo hello y mapas de Bing realizará automáticamente Hola cálculos toosee ya sea dentro de hello geofence. Una vez que se ejecuta la solicitud de Hola a través de un explorador (o cURL), obtendrá estándar una respuesta JSON:

![](./media/notification-hubs-geofence/bing-maps-json.png)

Esta respuesta solo se produce cuando punto de hello realmente está dentro de hello designado los límites. Si no es así, obtendrá un depósito de **resultados** vacío:

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Configuración de aplicación de UWP Hola
Ahora que tenemos el origen de datos de hello listo, se podemos empezar a trabajar en hello aplicación UWP que se iniciar anteriormente.

Ante todo, debemos habilitar los servicios de ubicación para nuestra aplicación. toodo, haga doble clic en `Package.appxmanifest` en el archivo **el Explorador de soluciones**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

En la ficha Propiedades de paquete Hola que acaba de abrir, haga clic en **capacidades** y asegúrese de que selecciona **ubicación**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Tal y como se declara la capacidad de ubicación de hello, cree una nueva carpeta de la solución denominada `Core`y agregar un archivo nuevo denominado `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Hola `LocationHelper` clase es bastante básica en este momento: todo lo que hace es nos permitirá tooobtain ubicación de usuario de Hola a través de la API del sistema hello:

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

Puede leer más sobre cómo obtener Hola ubicación del usuario en aplicaciones UWP en oficial de hello [el documento de MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

toocheck que la adquisición de ubicación de hello realmente funciona, abra parte de código de hello de la página principal (`MainPage.xaml.cs`). Crear un nuevo controlador de eventos para hello `Loaded` evento en hello `MainPage` constructor:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

implementación de Hola Hola del controlador de eventos es la siguiente:

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Tenga en cuenta que se declara controlador hello como asincrónicas porque `GetCurrentLocation` es que admite await y, por tanto, requiere toobe que se ejecuta en un contexto asincrónico. Además, dado que en determinadas circunstancias tengamos que terminar con una ubicación null (por ejemplo, se deshabilitan los servicios de ubicación de Hola o aplicación hello se denegó la ubicación de tooaccess de permisos), necesitamos toomake seguro de que se administran correctamente con una comprobación de valores null.

Ejecute la aplicación hello. Asegúrese de que se permite el acceso de ubicación:

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Una vez Hola lanzamientos de aplicación, debe ser capaz de toosee Hola coordenadas en hello **salida** ventana:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Ahora ya sabe que funciona de la adquisición de ubicación: sentirse controlador de eventos de prueba gratuita tooremove Hola para Loaded ya que no va a usar ya.

Hola siguiente paso es toocapture cambie la ubicación. Para ello, vamos atrás toohello `LocationHelper` clase y agregue un controlador de eventos de Hola para `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

implementación de Hello mostrará coordenadas de ubicación de Hola Hola **salida** ventana:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Cómo configurar Hola back-end
Descargar hello [ejemplo de back-end de .NET desde GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). Una vez completada la descarga de hello, abra hello `NotifyUsers` carpeta y posteriormente: Hola `NotifyUsers.sln` archivo.

Conjunto hello `AppBackend` proyecto como hello **proyecto de inicio** e iniciarlo.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Hello proyecto ya está configurado toosend inserción notificaciones tootarget dispositivos, por lo que necesitamos toodo solo dos cosas: intercambiar cadena de conexión correcta Hola Hola central de notificaciones y agregar límite identificación toosend Hola notificación solo cuando hello usuario está dentro de hello geofence.

cadena de conexión de hello tooconfigure, Hola `Models` carpeta abierta `Notifications.cs`. Hola `NotificationHubClient.CreateClientFromConnectionString` función debe contener información de hello sobre el centro de notificaciones que se puede obtener en hello [Portal de Azure](https://portal.azure.com) (Buscar dentro de hello **las directivas de acceso** hoja en  **Configuración de**). Guarde el archivo de configuración actualizada de hello.

Ahora necesitamos toocreate un modelo para hello resultado de la API de Bing Maps. Hola toodo de manera más fácil que es contextual en hello `Models` carpeta, **agregar** > **clase**. Asígnele el nombre `GeofenceBoundary.cs`. Una vez hecho, copie Hola JSON de respuesta Hola API que se describe en la primera sección de Hola y en el uso de Visual Studio **editar** > **Pegado especial** > **pegar JSON como las clases**. 

De este modo garantizamos que ese objeto Hola se deserializará exactamente tal y como estaba previsto. El conjunto de clases resultante debe ser similar a esto:

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

A continuación, abra `Controllers` > `NotificationsController.cs`. Necesitamos tootweak Hola Post llamada tooaccount de latitud y longitud de destino de Hola. Para ello, basta con agregar dos cadenas toohello firma de la función: `latitude` y `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Cree una nueva clase en proyecto de hello denominado `ApiHelper.cs` : vamos a usar las intersecciones de límite de tooconnect tooBing toocheck punto. Implemente una función `IsPointWithinBounds` , como esta:

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> Asegúrese de seguro de punto de conexión de hello API toosubstitute con dirección URL de consulta de Hola que ha obtenido antes de hello centro de desarrollo de Bing (mismo aplica clave toohello API). 
> 
> 

Si hay consultas toohello de resultados, eso significa que Hola punto especificado está dentro de los límites de Hola de hello geofence, por lo que se devuelven `true`. Si no hay ningún resultado, Bing nos indica que el punto de Hola se está fuera Hola marco de búsqueda, por lo que se devuelven `false`.

En `NotificationsController.cs`, cree una comprobación justo antes de la instrucción switch de hello:

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

De este modo, la notificación de hello sólo se envía al punto de hello está dentro de los límites de Hola.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Probar las notificaciones de inserción en la aplicación UWP hello
Si vuelve toohello aplicación de UWP, deberíamos estar ahora tootest capaz de notificaciones. Dentro de hello `LocationHelper` de clases, cree una nueva función – `SendLocationToBackend`:

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> Intercambiar hello `POST_URL` toohello ubicación de la aplicación web implementadas que hemos creado en la sección anterior de Hola. Por ahora, es aceptar toorun se localmente, sin embargo, cuando se trabaja sobre la implementación de una versión pública, debe toohost con un proveedor externo.
> 
> 

Ahora asegurémonos de que se registra la aplicación UWP hello las notificaciones de inserción. En Visual Studio, haga clic en **proyecto** > **almacenar** > **asociar aplicación con el almacén de hello**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Una vez que inicie sesión en la cuenta de desarrollador tooyour, asegúrese de seleccionar una aplicación existente o cree uno nuevo y asociar paquetes de saludo. 

Vaya toohello centro de desarrollo y aplicación de hello abierto que acaba de crear. Haga clic en **Servicios** > **Notificaciones push** > **Sitio de Servicios Live**.

![](./media/notification-hubs-geofence/ms-live-services.png)

En el sitio de hello, tome nota de hello **secreto de aplicación** hello y **SID del paquete**. Necesitará tanto en el Portal de Azure: Hola, abra el centro de notificaciones, haga clic en **configuración** > **Notification Services** > **de Windows (WNS)**y escriba la información de hello en campos de hello necesario.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

Haga clic en **Save**(Guardar).

Haga clic con el botón derecho en **Referencias** en el **Explorador de soluciones** y seleccione **Administrar paquetes NuGet**. Necesitamos tooadd un toohello referencia **biblioteca administrada de Microsoft Azure Service Bus** : simplemente buscar `WindowsAzure.Messaging.Managed` y agregue el proyecto de tooyour.

![](./media/notification-hubs-geofence/vs-nuget.png)

Para realizar pruebas, podemos crear hello `MainPage_Loaded` una vez más, el controlador de eventos y agregar este tooit de fragmento de código:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Hola anterior registra la aplicación hello con centro de notificaciones de Hola. Ya está listo toogo. 

En `LocationHelper`, dentro de hello `Geolocator_PositionChanged` controlador, puede agregar un fragmento de código de prueba que forzosamente incluirán la ubicación de Hola Hola geofence:

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Porque no se están superando coordenadas real hello (que no estén dentro de los límites de hello en el momento de hello) y usa los valores de prueba predefinidas, se muestra una notificación aparezca en la actualización:

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>Pasos siguientes
Hay un par de pasos que puede ser necesario toofollow en suma toohello anteriormente toomake seguro de que las soluciones de Hola para entornos de producción.

En primer lugar y ante todo, puede que tenga tooensure que geofences son dinámicos. Esto requerirá algún trabajo adicional con hello API de Bing en orden toobe tooupload capaz de nuevo los límites dentro de origen de datos existente de Hola. Consulte hello [documentación de API de servicios de datos espaciales de Bing](https://msdn.microsoft.com/library/ff701734.aspx) para obtener más detalles sobre el asunto de Hola.

En segundo lugar, tal y como están tooensure de trabajo que entrega Hola se realiza toohello derecho participantes, conviene tootarget ellas a través de [etiquetado](notification-hubs-tags-segment-push-message.md).

solución de Hello mostrado anteriormente describe un escenario en el que es posible que tenga una amplia variedad de plataformas de destino, por lo que no limitamos las capacidades de hello perímetro toosystem específica. Es decir, Hola plataforma Universal de Windows ofrece capacidades demasiado[detectar geofences derecha out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Para más información acerca de las funcionalidades de Centros de notificaciones, consulte nuestro [portal de documentación](https://azure.microsoft.com/documentation/services/notification-hubs/).

