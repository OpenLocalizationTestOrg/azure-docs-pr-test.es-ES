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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="ac9e1-104">Notificaciones push geovalladas con los Centros de notificaciones de Azure y datos espaciales de Bing</span><span class="sxs-lookup"><span data-stu-id="ac9e1-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="ac9e1-105">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ac9e1-106">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ac9e1-107">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="ac9e1-108">En este tutorial, aprenderá cómo toodeliver basada en la ubicación de inserción notificaciones con centros de notificaciones de Azure y los datos espaciales de Bing, aprovecha desde dentro de una aplicación de plataforma Universal de Windows.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac9e1-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ac9e1-109">Prerequisites</span></span>
<span data-ttu-id="ac9e1-110">En primer lugar y ante todo, deberá toomake Asegúrese de que tiene todos los Hola software y servicio de requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="ac9e1-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) o posterior ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) también servirá).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="ac9e1-112">La versión más reciente de hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="ac9e1-113">[Cuenta del Centro de desarrollo de Bing Maps](https://www.bingmapsportal.com/) (puede crear una gratis y asociarla a su cuenta de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="ac9e1-114">Introducción</span><span class="sxs-lookup"><span data-stu-id="ac9e1-114">Getting Started</span></span>
<span data-ttu-id="ac9e1-115">Empecemos creando proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="ac9e1-116">En Visual Studio, inicie un nuevo proyecto de tipo **Aplicación vacía (Windows universal)**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="ac9e1-117">Una vez completada la creación del proyecto de hello, debe tener el instrumento de hello para la propia aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="ac9e1-118">Ahora vamos a configurar todos los elementos de infraestructura de barrera geográfica Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="ac9e1-119">Ya que estamos toouse continuo de servicios de Bing para que esto, hay un punto de conexión de API de REST público que nos permite tooquery marcos de ubicación específica:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="ac9e1-120">Necesitará toospecify Hola siguientes tooget de parámetros que funcione:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="ac9e1-121">**Id. de origen de datos** y **Nombre de origen de datos**: en la API de Bing Maps, los orígenes de datos contienen distintos metadatos en depósitos, como las ubicaciones y el horario comercial de la operación.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="ac9e1-122">Puede leer más sobre ellos aquí.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-122">You can read more about those here.</span></span> 
* <span data-ttu-id="ac9e1-123">**Nombre de la entidad** : Hola entidad que desee toouse como punto de referencia para la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="ac9e1-124">**Clave de API de mapas de Bing** : se trata de clave de Hola que ha obtenido antes cuando se creó la cuenta del centro de desarrollo de Bing Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="ac9e1-125">Vamos a hacer un análisis más profundo en el programa de instalación de Hola para cada uno de los elementos de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="ac9e1-126">Configurar origen de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="ac9e1-126">Setting up hello data source</span></span>
<span data-ttu-id="ac9e1-127">Puede hacerlo en hello centro de desarrollo de mapas de Bing.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="ac9e1-128">Haga clic en **orígenes de datos** en hello superior barra de navegación y seleccione **administrar orígenes de datos**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="ac9e1-129">Si no ha trabajado con la API de Bing Maps antes, probablemente no haber ningún origen de datos está presente, por lo que solo puede crear uno nuevo, haga clic en el origen de datos de tooa de datos de carga.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="ac9e1-130">Asegúrese de que rellene todos los campos de hello necesario:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="ac9e1-131">Tal vez se pregunte: ¿qué es el archivo de datos de hello y lo que debe puede cargar?</span><span class="sxs-lookup"><span data-stu-id="ac9e1-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="ac9e1-132">Para fines de Hola de esta prueba, podemos utilizar ejemplo Hola basados en canalizaciones que rodea un área al mar de San Francisco hello:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="ac9e1-133">Hola anterior representa esta entidad:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="ac9e1-134">Simplemente copie y pegue cadena Hola anterior en un nuevo archivo y guárdelo como **NotificationHubsGeofence.pipe**y cargarlo en hello centro de desarrollo de Bing.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="ac9e1-135">Es posible que toospecify solicitada una nueva clave para hello **clave maestra** que es diferente de hello **clave de consulta**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="ac9e1-136">Basta con crear una nueva clave a través de hello panel y la actualización de hello página origen de datos carga.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="ac9e1-137">Una vez que cargue el archivo de datos de hello, necesitará toomake seguro de que publique el origen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="ac9e1-138">Vaya demasiado**administrar orígenes de datos**, igual que hicimos anteriormente, busque el origen de datos en la lista de Hola y haga clic en **publicar** en hello **acciones** columna.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="ac9e1-139">En un bit, debería ver el origen de datos en hello **orígenes de datos publicados** ficha:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="ac9e1-140">Si hace clic en **editar**, será capaz de toosee un vistazo qué ubicaciones se introdujo en ella:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="ac9e1-141">En este momento, portal de hello no muestra Hola límites para geofence Hola que creamos: lo único que necesita es una confirmación que Hola especificado se encuentra en proximidad derecho Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="ac9e1-142">Ahora tiene todos los requisitos de Hola Hola origen de datos.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="ac9e1-143">Haga clic en detalles de hello tooget en dirección URL de solicitud de Hola para llamada de API hello, Hola centro de desarrollo de mapas de Bing, **orígenes de datos** y seleccione **información de origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="ac9e1-144">Hola **URL de consulta** que estamos después aquí.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="ac9e1-145">Se trata de punto de conexión de hello en el que podemos ejecutar consultas toocheck si Hola dispositivo actualmente dentro de una ubicación de los límites de Hola o no.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="ac9e1-146">tooperform esta comprobación, sólo será necesario tooexecute una operación GET llame a con la dirección URL de consulta de hello, con hello parámetros anexados siguientes:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="ac9e1-147">De este modo se está especificando un punto de destino que obtenemos desde dispositivo hello y mapas de Bing realizará automáticamente Hola cálculos toosee ya sea dentro de hello geofence.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="ac9e1-148">Una vez que se ejecuta la solicitud de Hola a través de un explorador (o cURL), obtendrá estándar una respuesta JSON:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="ac9e1-149">Esta respuesta solo se produce cuando punto de hello realmente está dentro de hello designado los límites.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="ac9e1-150">Si no es así, obtendrá un depósito de **resultados** vacío:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="ac9e1-151">Configuración de aplicación de UWP Hola</span><span class="sxs-lookup"><span data-stu-id="ac9e1-151">Setting up hello UWP application</span></span>
<span data-ttu-id="ac9e1-152">Ahora que tenemos el origen de datos de hello listo, se podemos empezar a trabajar en hello aplicación UWP que se iniciar anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="ac9e1-153">Ante todo, debemos habilitar los servicios de ubicación para nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="ac9e1-154">toodo, haga doble clic en `Package.appxmanifest` en el archivo **el Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="ac9e1-155">En la ficha Propiedades de paquete Hola que acaba de abrir, haga clic en **capacidades** y asegúrese de que selecciona **ubicación**:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="ac9e1-156">Tal y como se declara la capacidad de ubicación de hello, cree una nueva carpeta de la solución denominada `Core`y agregar un archivo nuevo denominado `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="ac9e1-157">Hola `LocationHelper` clase es bastante básica en este momento: todo lo que hace es nos permitirá tooobtain ubicación de usuario de Hola a través de la API del sistema hello:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

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

<span data-ttu-id="ac9e1-158">Puede leer más sobre cómo obtener Hola ubicación del usuario en aplicaciones UWP en oficial de hello [el documento de MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="ac9e1-159">toocheck que la adquisición de ubicación de hello realmente funciona, abra parte de código de hello de la página principal (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="ac9e1-160">Crear un nuevo controlador de eventos para hello `Loaded` evento en hello `MainPage` constructor:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="ac9e1-161">implementación de Hola Hola del controlador de eventos es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="ac9e1-162">Tenga en cuenta que se declara controlador hello como asincrónicas porque `GetCurrentLocation` es que admite await y, por tanto, requiere toobe que se ejecuta en un contexto asincrónico.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="ac9e1-163">Además, dado que en determinadas circunstancias tengamos que terminar con una ubicación null (por ejemplo, se deshabilitan los servicios de ubicación de Hola o aplicación hello se denegó la ubicación de tooaccess de permisos), necesitamos toomake seguro de que se administran correctamente con una comprobación de valores null.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="ac9e1-164">Ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-164">Run hello application.</span></span> <span data-ttu-id="ac9e1-165">Asegúrese de que se permite el acceso de ubicación:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="ac9e1-166">Una vez Hola lanzamientos de aplicación, debe ser capaz de toosee Hola coordenadas en hello **salida** ventana:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="ac9e1-167">Ahora ya sabe que funciona de la adquisición de ubicación: sentirse controlador de eventos de prueba gratuita tooremove Hola para Loaded ya que no va a usar ya.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="ac9e1-168">Hola siguiente paso es toocapture cambie la ubicación.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="ac9e1-169">Para ello, vamos atrás toohello `LocationHelper` clase y agregue un controlador de eventos de Hola para `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="ac9e1-170">implementación de Hello mostrará coordenadas de ubicación de Hola Hola **salida** ventana:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="ac9e1-171">Cómo configurar Hola back-end</span><span class="sxs-lookup"><span data-stu-id="ac9e1-171">Setting up hello backend</span></span>
<span data-ttu-id="ac9e1-172">Descargar hello [ejemplo de back-end de .NET desde GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="ac9e1-173">Una vez completada la descarga de hello, abra hello `NotifyUsers` carpeta y posteriormente: Hola `NotifyUsers.sln` archivo.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="ac9e1-174">Conjunto hello `AppBackend` proyecto como hello **proyecto de inicio** e iniciarlo.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="ac9e1-175">Hello proyecto ya está configurado toosend inserción notificaciones tootarget dispositivos, por lo que necesitamos toodo solo dos cosas: intercambiar cadena de conexión correcta Hola Hola central de notificaciones y agregar límite identificación toosend Hola notificación solo cuando hello usuario está dentro de hello geofence.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="ac9e1-176">cadena de conexión de hello tooconfigure, Hola `Models` carpeta abierta `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="ac9e1-177">Hola `NotificationHubClient.CreateClientFromConnectionString` función debe contener información de hello sobre el centro de notificaciones que se puede obtener en hello [Portal de Azure](https://portal.azure.com) (Buscar dentro de hello **las directivas de acceso** hoja en  **Configuración de**).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="ac9e1-178">Guarde el archivo de configuración actualizada de hello.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="ac9e1-179">Ahora necesitamos toocreate un modelo para hello resultado de la API de Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="ac9e1-180">Hola toodo de manera más fácil que es contextual en hello `Models` carpeta, **agregar** > **clase**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="ac9e1-181">Asígnele el nombre `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="ac9e1-182">Una vez hecho, copie Hola JSON de respuesta Hola API que se describe en la primera sección de Hola y en el uso de Visual Studio **editar** > **Pegado especial** > **pegar JSON como las clases**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="ac9e1-183">De este modo garantizamos que ese objeto Hola se deserializará exactamente tal y como estaba previsto.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="ac9e1-184">El conjunto de clases resultante debe ser similar a esto:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="ac9e1-185">A continuación, abra `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="ac9e1-186">Necesitamos tootweak Hola Post llamada tooaccount de latitud y longitud de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="ac9e1-187">Para ello, basta con agregar dos cadenas toohello firma de la función: `latitude` y `longitude`.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="ac9e1-188">Cree una nueva clase en proyecto de hello denominado `ApiHelper.cs` : vamos a usar las intersecciones de límite de tooconnect tooBing toocheck punto.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="ac9e1-189">Implemente una función `IsPointWithinBounds` , como esta:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="ac9e1-190">Asegúrese de seguro de punto de conexión de hello API toosubstitute con dirección URL de consulta de Hola que ha obtenido antes de hello centro de desarrollo de Bing (mismo aplica clave toohello API).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="ac9e1-191">Si hay consultas toohello de resultados, eso significa que Hola punto especificado está dentro de los límites de Hola de hello geofence, por lo que se devuelven `true`.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="ac9e1-192">Si no hay ningún resultado, Bing nos indica que el punto de Hola se está fuera Hola marco de búsqueda, por lo que se devuelven `false`.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="ac9e1-193">En `NotificationsController.cs`, cree una comprobación justo antes de la instrucción switch de hello:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

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

<span data-ttu-id="ac9e1-194">De este modo, la notificación de hello sólo se envía al punto de hello está dentro de los límites de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="ac9e1-195">Probar las notificaciones de inserción en la aplicación UWP hello</span><span class="sxs-lookup"><span data-stu-id="ac9e1-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="ac9e1-196">Si vuelve toohello aplicación de UWP, deberíamos estar ahora tootest capaz de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="ac9e1-197">Dentro de hello `LocationHelper` de clases, cree una nueva función – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="ac9e1-198">Intercambiar hello `POST_URL` toohello ubicación de la aplicación web implementadas que hemos creado en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="ac9e1-199">Por ahora, es aceptar toorun se localmente, sin embargo, cuando se trabaja sobre la implementación de una versión pública, debe toohost con un proveedor externo.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="ac9e1-200">Ahora asegurémonos de que se registra la aplicación UWP hello las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="ac9e1-201">En Visual Studio, haga clic en **proyecto** > **almacenar** > **asociar aplicación con el almacén de hello**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="ac9e1-202">Una vez que inicie sesión en la cuenta de desarrollador tooyour, asegúrese de seleccionar una aplicación existente o cree uno nuevo y asociar paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="ac9e1-203">Vaya toohello centro de desarrollo y aplicación de hello abierto que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="ac9e1-204">Haga clic en **Servicios** > **Notificaciones push** > **Sitio de Servicios Live**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="ac9e1-205">En el sitio de hello, tome nota de hello **secreto de aplicación** hello y **SID del paquete**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="ac9e1-206">Necesitará tanto en el Portal de Azure: Hola, abra el centro de notificaciones, haga clic en **configuración** > **Notification Services** > **de Windows (WNS)**y escriba la información de hello en campos de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="ac9e1-207">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-207">Click on **Save**.</span></span>

<span data-ttu-id="ac9e1-208">Haga clic con el botón derecho en **Referencias** en el **Explorador de soluciones** y seleccione **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="ac9e1-209">Necesitamos tooadd un toohello referencia **biblioteca administrada de Microsoft Azure Service Bus** : simplemente buscar `WindowsAzure.Messaging.Managed` y agregue el proyecto de tooyour.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="ac9e1-210">Para realizar pruebas, podemos crear hello `MainPage_Loaded` una vez más, el controlador de eventos y agregar este tooit de fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="ac9e1-211">Hola anterior registra la aplicación hello con centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="ac9e1-212">Ya está listo toogo.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-212">You are ready toogo!</span></span> 

<span data-ttu-id="ac9e1-213">En `LocationHelper`, dentro de hello `Geolocator_PositionChanged` controlador, puede agregar un fragmento de código de prueba que forzosamente incluirán la ubicación de Hola Hola geofence:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="ac9e1-214">Porque no se están superando coordenadas real hello (que no estén dentro de los límites de hello en el momento de hello) y usa los valores de prueba predefinidas, se muestra una notificación aparezca en la actualización:</span><span class="sxs-lookup"><span data-stu-id="ac9e1-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="ac9e1-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac9e1-215">What’s next?</span></span>
<span data-ttu-id="ac9e1-216">Hay un par de pasos que puede ser necesario toofollow en suma toohello anteriormente toomake seguro de que las soluciones de Hola para entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="ac9e1-217">En primer lugar y ante todo, puede que tenga tooensure que geofences son dinámicos.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="ac9e1-218">Esto requerirá algún trabajo adicional con hello API de Bing en orden toobe tooupload capaz de nuevo los límites dentro de origen de datos existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="ac9e1-219">Consulte hello [documentación de API de servicios de datos espaciales de Bing](https://msdn.microsoft.com/library/ff701734.aspx) para obtener más detalles sobre el asunto de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="ac9e1-220">En segundo lugar, tal y como están tooensure de trabajo que entrega Hola se realiza toohello derecho participantes, conviene tootarget ellas a través de [etiquetado](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="ac9e1-221">solución de Hello mostrado anteriormente describe un escenario en el que es posible que tenga una amplia variedad de plataformas de destino, por lo que no limitamos las capacidades de hello perímetro toosystem específica.</span><span class="sxs-lookup"><span data-stu-id="ac9e1-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="ac9e1-222">Es decir, Hola plataforma Universal de Windows ofrece capacidades demasiado[detectar geofences derecha out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="ac9e1-223">Para más información acerca de las funcionalidades de Centros de notificaciones, consulte nuestro [portal de documentación](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="ac9e1-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

