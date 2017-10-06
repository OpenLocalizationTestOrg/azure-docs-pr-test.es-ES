---
title: "aaaHow toouse hello Azure SDK para aplicaciones móviles para Android | Documentos de Microsoft"
description: "¿Cómo toouse Hola SDK de aplicaciones móviles de Azure para Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="d2990-103">¿Cómo toouse Hola SDK de aplicaciones móviles de Azure para Android</span><span class="sxs-lookup"><span data-stu-id="d2990-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="d2990-104">Esta guía le mostrará cómo toouse Hola a cliente de Android SDK para aplicaciones móviles tooimplement los escenarios comunes, como:</span><span class="sxs-lookup"><span data-stu-id="d2990-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="d2990-105">Consultas de datos (inserción, actualización y eliminación)</span><span class="sxs-lookup"><span data-stu-id="d2990-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="d2990-106">Autenticación</span><span class="sxs-lookup"><span data-stu-id="d2990-106">Authentication.</span></span>
* <span data-ttu-id="d2990-107">Control de errores</span><span class="sxs-lookup"><span data-stu-id="d2990-107">Handling errors.</span></span>
* <span data-ttu-id="d2990-108">Personalización de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-108">Customizing hello client.</span></span>

<span data-ttu-id="d2990-109">Esta guía se centra en hello cliente SDK de Android.</span><span class="sxs-lookup"><span data-stu-id="d2990-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="d2990-110">toolearn Obtenga más información sobre hello servidor SDK para aplicaciones móviles, consulte [trabajar con back-end de .NET SDK] [ 10] o [cómo toouse Hola Node.js back-end SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="d2990-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="d2990-111">Documentación de referencia</span><span class="sxs-lookup"><span data-stu-id="d2990-111">Reference Documentation</span></span>

<span data-ttu-id="d2990-112">Puede encontrar Hola [referencia de la API de Javadocs] [ 12] de la biblioteca de cliente de Android hello en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d2990-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d2990-113">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="d2990-113">Supported Platforms</span></span>

<span data-ttu-id="d2990-114">Hello Azure SDK para aplicaciones móviles para Android admite niveles de API 19 y 24 (KitKat a través de nueces) para factores de forma de teléfono y Tablet PC.</span><span class="sxs-lookup"><span data-stu-id="d2990-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="d2990-115">La autenticación, en concreto, utiliza un credenciales de toogather del enfoque de framework web comunes.</span><span class="sxs-lookup"><span data-stu-id="d2990-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="d2990-116">La autenticación de flujo de servidor no funciona con dispositivos pequeños, por ejemplo, relojes.</span><span class="sxs-lookup"><span data-stu-id="d2990-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="d2990-117">Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d2990-117">Setup and Prerequisites</span></span>

<span data-ttu-id="d2990-118">Hola completa [inicio rápido de aplicaciones móviles](app-service-mobile-android-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d2990-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="d2990-119">Esta tarea garantiza que se cumplan todos los requisitos previos del desarrollo de aplicaciones de Mobile Apps de Azure.</span><span class="sxs-lookup"><span data-stu-id="d2990-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="d2990-120">Hola inicio rápido también ayuda a configurar su cuenta y crear su primer back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d2990-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="d2990-121">Si decide no toocomplete tutorial de inicio rápido de hello, complete Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="d2990-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="d2990-122">[crear un aplicación móvil de back-end] [ 13] toouse con la aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="d2990-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="d2990-123">En Android Studio [actualización hello Gradle compilar archivos](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="d2990-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="d2990-124">[Habilite permisos de Internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="d2990-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="d2990-125"><a name="gradle-build"></a>Actualizar hello Gradle crear archivo</span><span class="sxs-lookup"><span data-stu-id="d2990-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="d2990-126">Cambie ambos archivos **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="d2990-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="d2990-127">Agregue este código toohello *proyecto* nivel **build.gradle** archivo dentro de hello *buildscript* etiqueta:</span><span class="sxs-lookup"><span data-stu-id="d2990-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="d2990-128">Agregue este código toohello *módulo aplicación* nivel **build.gradle** archivo dentro de hello *dependencias* etiqueta:</span><span class="sxs-lookup"><span data-stu-id="d2990-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="d2990-129">Actualmente la versión más reciente de hello es 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="d2990-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="d2990-130">se enumeran las versiones compatibles de Hello [en bintray][14].</span><span class="sxs-lookup"><span data-stu-id="d2990-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="d2990-131"><a name="enable-internet"></a>Habilitación de permisos de Internet</span><span class="sxs-lookup"><span data-stu-id="d2990-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="d2990-132">tooaccess Azure, la aplicación debe tener permiso de INTERNET de hello habilitado.</span><span class="sxs-lookup"><span data-stu-id="d2990-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="d2990-133">Si aún no está habilitado, agregue Hola después de la línea de código tooyour **AndroidManifest.xml** archivo:</span><span class="sxs-lookup"><span data-stu-id="d2990-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="d2990-134">Creación de una conexión de cliente</span><span class="sxs-lookup"><span data-stu-id="d2990-134">Create a Client Connection</span></span>

<span data-ttu-id="d2990-135">Aplicaciones móviles de Azure proporciona cuatro funciones tooyour de aplicaciones móviles:</span><span class="sxs-lookup"><span data-stu-id="d2990-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="d2990-136">Acceso a datos y sincronización sin conexión con un servicio de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="d2990-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="d2990-137">Llamar a las API de personalizado que se escriben con hello SDK de servidor de aplicaciones móviles de Azure.</span><span class="sxs-lookup"><span data-stu-id="d2990-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="d2990-138">Autenticación con Autenticación y autorización de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="d2990-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="d2990-139">Registro de notificaciones push con Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="d2990-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="d2990-140">Cada una de estas funciones requiere en primer lugar que se cree un objeto `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="d2990-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="d2990-141">Solo se debe crear un objeto `MobileServiceClient` dentro de su cliente móvil (es decir, debe tener un patrón singleton).</span><span class="sxs-lookup"><span data-stu-id="d2990-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="d2990-142">toocreate un `MobileServiceClient` objeto:</span><span class="sxs-lookup"><span data-stu-id="d2990-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="d2990-143">Hola `<MobileAppUrl>` es una cadena o un objeto de dirección URL que señala el back-end de tooyour móvil.</span><span class="sxs-lookup"><span data-stu-id="d2990-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="d2990-144">Si usas toohost de servicio de aplicaciones de Azure el back-end móvil, a continuación, asegúrese de usar Hola segura `https://` versión de dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="d2990-145">Hola cliente también requiere acceso toohello actividad o contexto - hello `this` parámetro en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="d2990-146">Hola MobileServiceClient construcción debe realizarse en hello `onCreate()` método de hello al que hace referencia la actividad en hello `AndroidManifest.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="d2990-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="d2990-147">Como procedimiento recomendado, debe abstraer la comunicación del servidor en su propia clase (patrón singleton).</span><span class="sxs-lookup"><span data-stu-id="d2990-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="d2990-148">En este caso, debería pasar Hola actividad dentro de hello constructor tooappropriately Configurar servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="d2990-149">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2990-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="d2990-150">Ahora puede llamar a `AzureServiceAdapter.Initialize(this);` en hello `onCreate()` método de su actividad principal.</span><span class="sxs-lookup"><span data-stu-id="d2990-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="d2990-151">Usa ningún otro método necesidad de cliente de acceso toohello `AzureServiceAdapter.getInstance();` tooobtain un adaptador de servicio de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="d2990-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="d2990-152">Operaciones de datos</span><span class="sxs-lookup"><span data-stu-id="d2990-152">Data Operations</span></span>

<span data-ttu-id="d2990-153">núcleo de Hola de hello SDK de aplicaciones móviles de Azure es tooprovide acceso toodata almacenado en SQL Azure en el back-end de hello aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d2990-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="d2990-154">Se puede acceder a estos datos mediante clases fuertemente tipadas (preferidas) o consultas sin tipo (no se recomienda).</span><span class="sxs-lookup"><span data-stu-id="d2990-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="d2990-155">masiva Hola de esta sección se ocupa utilizando clases fuertemente tipadas.</span><span class="sxs-lookup"><span data-stu-id="d2990-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="d2990-156">Definición de clases de datos de cliente</span><span class="sxs-lookup"><span data-stu-id="d2990-156">Define client data classes</span></span>

<span data-ttu-id="d2990-157">tooaccess datos de tablas de SQL Azure, definir clases de datos de cliente que se corresponden toohello tablas en el back-end de hello aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d2990-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="d2990-158">Ejemplos de este tema supone que una tabla denominada **MyDataTable**, que tiene Hola siguientes columnas:</span><span class="sxs-lookup"><span data-stu-id="d2990-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="d2990-159">id</span><span class="sxs-lookup"><span data-stu-id="d2990-159">id</span></span>
* <span data-ttu-id="d2990-160">text</span><span class="sxs-lookup"><span data-stu-id="d2990-160">text</span></span>
* <span data-ttu-id="d2990-161">complete</span><span class="sxs-lookup"><span data-stu-id="d2990-161">complete</span></span>

<span data-ttu-id="d2990-162">Hello correspondiente objeto de cliente escrito reside en un archivo denominado **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="d2990-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="d2990-163">Agregue los métodos captador y establecedor para cada campo que agregue.</span><span class="sxs-lookup"><span data-stu-id="d2990-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="d2990-164">Si la tabla de SQL Azure contiene más columnas, podría agregar clase de hello correspondientes campos toothis.</span><span class="sxs-lookup"><span data-stu-id="d2990-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="d2990-165">Por ejemplo, si hello DTO (objeto de transferencia de datos) tenía una columna de prioridad de tipo entero, a continuación, puede agregar este campo, junto con sus métodos de captador y establecedor:</span><span class="sxs-lookup"><span data-stu-id="d2990-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="d2990-166">toolearn toocreate tablas adicionales en el back-end de aplicaciones móviles, vea [Cómo: definir un controlador de tabla] [ 15] (back-end de. NET) o [definir tablas mediante un esquema dinámico] [ 16] (Node.js back-end).</span><span class="sxs-lookup"><span data-stu-id="d2990-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="d2990-167">Una tabla de back-end de aplicaciones móviles de Azure define cinco campos especiales, cuatro de los cuales son tooclients disponibles:</span><span class="sxs-lookup"><span data-stu-id="d2990-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="d2990-168">`String id`: Hola identificador único global para el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="d2990-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="d2990-169">Como práctica recomendada, asegúrese de representación de cadena de Hola Hola Id. de un [UUID] [ 17] objeto.</span><span class="sxs-lookup"><span data-stu-id="d2990-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="d2990-170">`DateTimeOffset updatedAt`: Hola fecha/hora de la última actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="d2990-171">campo de Hello updatedAt se establece por servidor hello y nunca se debe establecer el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="d2990-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="d2990-172">`DateTimeOffset createdAt`: Hola fecha y hora se creó ese objeto Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="d2990-173">campo de registroen Hola se establece por servidor hello y nunca se debe establecer el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="d2990-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="d2990-174">`byte[] version`: Versión de hello normalmente se representa como una cadena, también se establece por servidor hello.</span><span class="sxs-lookup"><span data-stu-id="d2990-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="d2990-175">`boolean deleted`: Indica que el registro de hello se ha eliminado pero no se purgan todavía.</span><span class="sxs-lookup"><span data-stu-id="d2990-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="d2990-176">No use `deleted` como propiedad en la clase.</span><span class="sxs-lookup"><span data-stu-id="d2990-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="d2990-177">Hola `id` campo es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="d2990-177">hello `id` field is required.</span></span>  <span data-ttu-id="d2990-178">Hola `updatedAt` campo y `version` campo se usa para la sincronización sin conexión (para la resolución de conflictos y de sincronización incremental respectivamente).</span><span class="sxs-lookup"><span data-stu-id="d2990-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="d2990-179">Hola `createdAt` campo es un campo de referencia y no se usa en el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="d2990-180">nombres de Hello "en el cable" nombres de propiedades de hello y no son ajustables.</span><span class="sxs-lookup"><span data-stu-id="d2990-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="d2990-181">Sin embargo, puede crear una asignación entre el objeto y Hola nombres "en el cable" hello [gson] [ 3] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="d2990-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="d2990-182">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2990-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="d2990-183">Creación de una referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="d2990-183">Create a Table Reference</span></span>

<span data-ttu-id="d2990-184">tooaccess una tabla, cree primero un [MobileServiceTable] [ 8] objeto que realiza la llamada hello **getTable** método en hello [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="d2990-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="d2990-185">Este método tiene dos sobrecargas:</span><span class="sxs-lookup"><span data-stu-id="d2990-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="d2990-186">Hola siguiente código, **mClient** es un objeto de referencia tooyour MobileServiceClient.</span><span class="sxs-lookup"><span data-stu-id="d2990-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="d2990-187">Hola primera sobrecarga se utiliza donde son nombre de clase de Hola y el nombre de la tabla de Hola Hola mismo, y se hello uno usa Hola inicio rápido:</span><span class="sxs-lookup"><span data-stu-id="d2990-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="d2990-188">Hello segunda sobrecarga se utiliza al nombre de la tabla de hello es diferente del nombre de la clase hello: Hola primer parámetro es el nombre de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="d2990-189"><a name="query"></a>Consulta de una tabla de back-end</span><span class="sxs-lookup"><span data-stu-id="d2990-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="d2990-190">En primer lugar, obtenga una referencia de tabla.</span><span class="sxs-lookup"><span data-stu-id="d2990-190">First, obtain a table reference.</span></span>  <span data-ttu-id="d2990-191">A continuación, ejecutar una consulta en la referencia de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="d2990-192">Una consulta es cualquier combinación de:</span><span class="sxs-lookup"><span data-stu-id="d2990-192">A query is any combination of:</span></span>

* <span data-ttu-id="d2990-193">Una `.where()` [cláusula de filtro](#filtering).</span><span class="sxs-lookup"><span data-stu-id="d2990-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="d2990-194">Una `.orderBy()` [cláusula de ordenación](#sorting).</span><span class="sxs-lookup"><span data-stu-id="d2990-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="d2990-195">Una `.select()` [cláusula de selección de campos](#selection).</span><span class="sxs-lookup"><span data-stu-id="d2990-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="d2990-196">Una cláusula `.skip()` y `.top()` para [resultados paginados](#paging).</span><span class="sxs-lookup"><span data-stu-id="d2990-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="d2990-197">cláusulas de Hello deben presentarse en hello anterior orden.</span><span class="sxs-lookup"><span data-stu-id="d2990-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="d2990-198"><a name="filter"></a>Filtrado de los resultados</span><span class="sxs-lookup"><span data-stu-id="d2990-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="d2990-199">Hola forma general de una consulta es:</span><span class="sxs-lookup"><span data-stu-id="d2990-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="d2990-200">Hello en el ejemplo anterior se devuelve todos los resultados (arriba toohello tamaño de página máximo establecido por servidor hello).</span><span class="sxs-lookup"><span data-stu-id="d2990-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="d2990-201">Hola `.execute()` método ejecuta consultas de hello en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="d2990-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="d2990-202">consulta Hello es convertido tooan [OData v3] [ 19] consulta antes de back-end de transmisión toohello aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="d2990-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="d2990-203">Una vez recibido, back-end de aplicaciones móviles de hello convierte la consulta de hello en una instrucción SQL antes de ejecutarlo en la instancia de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="d2990-204">Puesto que la actividad de red tarda algún tiempo, Hola `.execute()` método devuelve un [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="d2990-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="d2990-205"><a name="filtering"></a>Filtrado de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="d2990-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="d2990-206">Hola después de la ejecución de la consulta devuelve todos los elementos de hello **ToDoItem** tabla where **completa** es igual a **false**.</span><span class="sxs-lookup"><span data-stu-id="d2990-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="d2990-207">**mToDoTable** es Hola referencia toohello servicio móvil tabla que hemos creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d2990-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="d2990-208">Definir un filtro mediante hello **donde** llamada al método en la referencia de tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="d2990-209">Hola **donde** método va seguido de un **campo** método seguido por un método que especifica el predicado lógico Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="d2990-210">Los posibles métodos de predicado incluyen **eq** (igual a), **ne** (no igual a), **gt** (mayor que), **ge** (mayor o igual que), **lt** (menor que) o **le** (menor o igual que).</span><span class="sxs-lookup"><span data-stu-id="d2990-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="d2990-211">Estos métodos permiten comparar el número y toospecific valores de campos de cadena.</span><span class="sxs-lookup"><span data-stu-id="d2990-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="d2990-212">Puede filtrar por fechas.</span><span class="sxs-lookup"><span data-stu-id="d2990-212">You can filter on dates.</span></span> <span data-ttu-id="d2990-213">Hello métodos siguientes permiten comparar el campo de fecha completa de Hola o partes de fecha de hello: **año**, **mes**, **día**, **hora**, **minuto**, y **segundo**.</span><span class="sxs-lookup"><span data-stu-id="d2990-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="d2990-214">Hello en el ejemplo siguiente se agrega un filtro para los elementos cuyos *fecha de vencimiento* es igual a 2013.</span><span class="sxs-lookup"><span data-stu-id="d2990-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="d2990-215">Hello métodos siguientes admiten filtros complejos en campos de cadena: **startsWith**, **endsWith**, **concat**, **subcadena**, **indexOf**, **reemplazar**, **toLower**, **toUpper**, **recortar**, y  **longitud**.</span><span class="sxs-lookup"><span data-stu-id="d2990-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="d2990-216">Hola siguiendo el ejemplo se filtra para filas de la tabla donde hello *texto* columna empieza por "PRI0".</span><span class="sxs-lookup"><span data-stu-id="d2990-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="d2990-217">Hola siguiendo métodos de operador se admite en los campos de número: **agregar**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, y **de ida y vuelta**.</span><span class="sxs-lookup"><span data-stu-id="d2990-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="d2990-218">Hola siguiendo el ejemplo se filtra para filas de la tabla donde hello **duración** es un número par.</span><span class="sxs-lookup"><span data-stu-id="d2990-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="d2990-219">Puede combinar predicados con estos métodos lógicos: **and**, **or** y **not**.</span><span class="sxs-lookup"><span data-stu-id="d2990-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="d2990-220">Hola siguiente ejemplo combina dos Hola anteriores ejemplos.</span><span class="sxs-lookup"><span data-stu-id="d2990-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="d2990-221">Agrupe y anide los operadores lógicos:</span><span class="sxs-lookup"><span data-stu-id="d2990-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="d2990-222">Para obtener más descripción y ejemplos de filtrado, consulte [explorar la riqueza de Hola de modelo de consultas de cliente de Android hello][20].</span><span class="sxs-lookup"><span data-stu-id="d2990-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="d2990-223"><a name="sorting"></a>Ordenación de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="d2990-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="d2990-224">Hello código siguiente devuelve todos los elementos de una tabla de **ToDoItems** ordena de forma ascendente por hello *texto* campo.</span><span class="sxs-lookup"><span data-stu-id="d2990-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="d2990-225">*mToDoTable* es hello toohello back-end tabla de referencia que creó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="d2990-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="d2990-226">Hola el primer parámetro de hello **orderBy** método es un nombre de toohello igual de cadena del campo de hello en qué toosort.</span><span class="sxs-lookup"><span data-stu-id="d2990-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="d2990-227">segundo parámetro de Hello usa hello **QueryOrder** toospecify de enumeración si toosort orden ascendente o descendente.</span><span class="sxs-lookup"><span data-stu-id="d2990-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="d2990-228">Si va a filtrar utilizando hello ***donde*** /método siguiente, hello ***donde*** se debe invocar el método antes de hello ***orderBy*** método.</span><span class="sxs-lookup"><span data-stu-id="d2990-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="d2990-229"><a name="selection"></a>Selección de columnas específicas</span><span class="sxs-lookup"><span data-stu-id="d2990-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="d2990-230">Hello código siguiente muestra cómo tooreturn todos los elementos de una tabla de **ToDoItems**, pero solo se muestra hello **completa** y **texto** campos.</span><span class="sxs-lookup"><span data-stu-id="d2990-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="d2990-231">**mToDoTable** es la tabla de back-end de toohello de referencia de Hola que hemos creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d2990-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="d2990-232">función select de Hello parámetros toohello son nombres de cadena de Hola Hola las columnas de tabla que desea tooreturn.</span><span class="sxs-lookup"><span data-stu-id="d2990-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="d2990-233">Hola **seleccione** método necesita toofollow métodos como **donde** y **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="d2990-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="d2990-234">Puede ir seguido de métodos de paginación como **skip** y **top**.</span><span class="sxs-lookup"><span data-stu-id="d2990-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="d2990-235"><a name="paging"></a>Devolución de datos en páginas</span><span class="sxs-lookup"><span data-stu-id="d2990-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="d2990-236">Los datos **SIEMPRE** se devuelven en páginas.</span><span class="sxs-lookup"><span data-stu-id="d2990-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="d2990-237">número máximo de Hola de registros devueltos se establece por servidor hello.</span><span class="sxs-lookup"><span data-stu-id="d2990-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="d2990-238">Si el cliente de hello solicita más registros, servidor hello devuelve número máximo de Hola de registros.</span><span class="sxs-lookup"><span data-stu-id="d2990-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="d2990-239">De forma predeterminada, el tamaño de página máximo de hello en el servidor hello es 50 registros.</span><span class="sxs-lookup"><span data-stu-id="d2990-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="d2990-240">Hola primer ejemplo muestra cómo tooselect Hola cinco elementos principales de una tabla.</span><span class="sxs-lookup"><span data-stu-id="d2990-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="d2990-241">consulta de Hello devuelve elementos de Hola de una tabla de **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="d2990-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="d2990-242">**mToDoTable** es hello toohello back-end tabla de referencia que creó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="d2990-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="d2990-243">Esta es una consulta que omite Hola cinco primeros elementos y, a continuación, devuelve Hola cinco siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2990-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="d2990-244">Si desea tooget todos los registros en una tabla, implementan código tooiterate sobre todas las páginas:</span><span class="sxs-lookup"><span data-stu-id="d2990-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="d2990-245">Una solicitud para todos los registros con este método crea un mínimo de dos solicitudes toohello aplicaciones móviles back-end.</span><span class="sxs-lookup"><span data-stu-id="d2990-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="d2990-246">Elige la opción tamaño de página derecha hello es un equilibrio entre el uso de memoria mientras está teniendo lugar solicitud hello, uso de ancho de banda y demora al recibir datos de hello completamente.</span><span class="sxs-lookup"><span data-stu-id="d2990-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="d2990-247">valor predeterminado de Hello (50 registros) es adecuado para todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d2990-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="d2990-248">Si exclusivamente opera en los dispositivos de memoria más grandes, aumentar hasta too500.</span><span class="sxs-lookup"><span data-stu-id="d2990-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="d2990-249">Hemos encontrado ese tamaño de página Hola aumenta más allá de 500 registra los resultados en inaceptables retrasos y problemas de memoria de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="d2990-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="d2990-250"><a name="chaining"></a>Concatenación de métodos de consulta</span><span class="sxs-lookup"><span data-stu-id="d2990-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="d2990-251">métodos de Hola que se utilizan al consultar tablas de back-end se pueden concatenar.</span><span class="sxs-lookup"><span data-stu-id="d2990-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="d2990-252">El encadenamiento de métodos permite tooselect columnas específicas de las filas filtradas que se ordenan y paginan de consulta.</span><span class="sxs-lookup"><span data-stu-id="d2990-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="d2990-253">Puede crear filtros lógicos complejos.</span><span class="sxs-lookup"><span data-stu-id="d2990-253">You can create complex logical filters.</span></span>  <span data-ttu-id="d2990-254">Cada método de consulta devuelve un objeto Query.</span><span class="sxs-lookup"><span data-stu-id="d2990-254">Each query method returns a Query object.</span></span> <span data-ttu-id="d2990-255">serie de hello tooend de métodos y consulta de ejecución realmente hello, llamada hello **ejecutar** método.</span><span class="sxs-lookup"><span data-stu-id="d2990-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="d2990-256">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2990-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="d2990-257">Hola encadenadas consulta métodos se deben ordenar como sigue:</span><span class="sxs-lookup"><span data-stu-id="d2990-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="d2990-258">Métodos de filtro (**where**)</span><span class="sxs-lookup"><span data-stu-id="d2990-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="d2990-259">Métodos de ordenación (**orderBy**)</span><span class="sxs-lookup"><span data-stu-id="d2990-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="d2990-260">Métodos de selección (**select**)</span><span class="sxs-lookup"><span data-stu-id="d2990-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="d2990-261">Métodos de paginación (**skip** y **top**)</span><span class="sxs-lookup"><span data-stu-id="d2990-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="d2990-262"><a name="binding"></a>Enlazar la interfaz de usuario de datos toohello</span><span class="sxs-lookup"><span data-stu-id="d2990-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="d2990-263">El enlace de datos implica tres componentes:</span><span class="sxs-lookup"><span data-stu-id="d2990-263">Data binding involves three components:</span></span>

* <span data-ttu-id="d2990-264">origen de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="d2990-264">hello data source</span></span>
* <span data-ttu-id="d2990-265">diseño de pantalla de Hola</span><span class="sxs-lookup"><span data-stu-id="d2990-265">hello screen layout</span></span>
* <span data-ttu-id="d2990-266">adaptador de Hola que vincula dos Hola juntos.</span><span class="sxs-lookup"><span data-stu-id="d2990-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="d2990-267">En el código de ejemplo se devuelven datos Hola de tabla de Mobile aplicaciones SQL Azure de hello **ToDoItem** en una matriz.</span><span class="sxs-lookup"><span data-stu-id="d2990-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="d2990-268">Esta actividad es uno de los patrones más comunes para las aplicaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="d2990-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="d2990-269">Las consultas de base de datos a menudo devuelven un conjunto de filas que Hola obtiene de cliente en una lista o matriz.</span><span class="sxs-lookup"><span data-stu-id="d2990-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="d2990-270">En este ejemplo, la matriz de hello es origen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="d2990-271">código de Hello especifica un diseño de pantalla que define la vista de Hola de datos de Hola que aparece en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="d2990-272">Hello dos se enlazan junto con un adaptador, que en este código es una extensión de hello **ArrayAdapter&lt;ToDoItem&gt;**  clase.</span><span class="sxs-lookup"><span data-stu-id="d2990-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="d2990-273"><a name="layout"></a>Definir el diseño de Hola</span><span class="sxs-lookup"><span data-stu-id="d2990-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="d2990-274">diseño de Hola se define mediante varios fragmentos de código XML.</span><span class="sxs-lookup"><span data-stu-id="d2990-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="d2990-275">Proporciona un diseño existente, Hola siguiente código representa hello **ListView** queremos toopopulate con nuestros datos del servidor.</span><span class="sxs-lookup"><span data-stu-id="d2990-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="d2990-276">En el anterior código de hello, Hola *listitem* atributo especifica el identificador de Hola de diseño de Hola para una fila individual en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="d2990-277">Este código especifica una casilla de verificación y su texto asociado y crea instancias una vez para cada elemento de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="d2990-278">Este diseño no muestra hello **identificador** campo y un diseño más complejo debería especificar campos adicionales de presentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="d2990-279">Este código está en hello **row_list_to_do.xml** archivo.</span><span class="sxs-lookup"><span data-stu-id="d2990-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="d2990-280"><a name="adapter"></a>Definir adaptador Hola</span><span class="sxs-lookup"><span data-stu-id="d2990-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="d2990-281">Puesto que el origen de datos de Hola de nuestro punto de vista es una matriz de **ToDoItem**, nos subclase nuestro adaptador desde una **ArrayAdapter&lt;ToDoItem&gt;**  clase.</span><span class="sxs-lookup"><span data-stu-id="d2990-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="d2990-282">Esta subclase genera una vista para cada **ToDoItem** con hello **row_list_to_do** diseño.</span><span class="sxs-lookup"><span data-stu-id="d2990-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="d2990-283">En el código, definimos Hola después de la clase que es una extensión de hello **ArrayAdapter&lt;E&gt;**  clase:</span><span class="sxs-lookup"><span data-stu-id="d2990-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="d2990-284">Invalidar adaptadores hello **getView** método.</span><span class="sxs-lookup"><span data-stu-id="d2990-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="d2990-285">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2990-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="d2990-286">Creamos una instancia de esta clase en nuestra actividad de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2990-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="d2990-287">Hola segundo parámetro toohello ToDoItemAdapter constructor es un diseño de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="d2990-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="d2990-288">Ahora se puede crear una instancia hello **ListView** y asignar Hola adaptador toohello **ListView**.</span><span class="sxs-lookup"><span data-stu-id="d2990-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="d2990-289"><a name="use-adapter"></a>Usar Hola adaptador tooBind toohello interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="d2990-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="d2990-290">Ya estás listo toouse enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="d2990-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="d2990-291">Hello código siguiente muestra cómo tooget elementos en la tabla de Hola y rellenos Hola adaptador local con hello productos devuelto.</span><span class="sxs-lookup"><span data-stu-id="d2990-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="d2990-292">Llame al adaptador de hello cualquier momento modificar hello **ToDoItem** tabla.</span><span class="sxs-lookup"><span data-stu-id="d2990-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="d2990-293">Como las modificaciones se realizan de registro en registro, se ocupará de una sola fila en lugar de una serie de ellas.</span><span class="sxs-lookup"><span data-stu-id="d2990-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="d2990-294">Cuando se inserta un elemento, llame a hello **agregar** método en Hola adaptador; cuando se elimina, llamar a hello **quitar** método.</span><span class="sxs-lookup"><span data-stu-id="d2990-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="d2990-295">Puede encontrar un ejemplo completo en hello [proyecto de inicio rápido Android][21].</span><span class="sxs-lookup"><span data-stu-id="d2990-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="d2990-296"><a name="inserting"></a>Insertar datos en hello back-end</span><span class="sxs-lookup"><span data-stu-id="d2990-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="d2990-297">Crear una instancia de hello *ToDoItem* clase y establecer sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="d2990-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="d2990-298">A continuación, utilice **insert()** tooinsert un objeto:</span><span class="sxs-lookup"><span data-stu-id="d2990-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="d2990-299">Hola devuelve coincidencias de entidad datos Hola insertados en la tabla de back-end de hello, Id. de hello incluye y cualquier otro valor (como hello `createdAt`, `updatedAt`, y `version` campos) establecido en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="d2990-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="d2990-300">Las tablas de Mobile Apps requieren una columna de clave principal denominada " **id**". Esta columna debe ser una cadena.</span><span class="sxs-lookup"><span data-stu-id="d2990-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="d2990-301">valor predeterminado de Hola de columna de Id. de hello es un GUID.</span><span class="sxs-lookup"><span data-stu-id="d2990-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="d2990-302">Puede proporcionar otros valores únicos, como nombres de usuario o direcciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="d2990-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="d2990-303">Cuando no se proporciona un valor de identificador de cadena para un registro insertado, Hola back-end genera un nuevo GUID.</span><span class="sxs-lookup"><span data-stu-id="d2990-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="d2990-304">Los valores de Id. de cadena proporcionan Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d2990-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="d2990-305">Se pueden generar identificadores sin crear una base de datos de toohello de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="d2990-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="d2990-306">Los registros son toomerge más fácil de diferentes tablas o bases de datos.</span><span class="sxs-lookup"><span data-stu-id="d2990-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="d2990-307">Los valores de los identificadores se integran mejor con una lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2990-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="d2990-308">Los valores de identificador de cadena son **OBLIGATORIOS** para poder utilizar la sincronización sin conexión.</span><span class="sxs-lookup"><span data-stu-id="d2990-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="d2990-309">No se puede cambiar un Id. una vez que se almacena en la base de datos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="d2990-310"><a name="updating"></a>Actualización de los datos en una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="d2990-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="d2990-311">tooupdate datos en una tabla, pasar Hola nuevo objeto toohello **update()** método.</span><span class="sxs-lookup"><span data-stu-id="d2990-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="d2990-312">En este ejemplo, *elemento* es una fila de tooa de referencia en hello *ToDoItem* tabla, lo que ha tenido algún tooit cambios realizados.</span><span class="sxs-lookup"><span data-stu-id="d2990-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="d2990-313">Hola de fila con hello mismo **identificador** se actualiza.</span><span class="sxs-lookup"><span data-stu-id="d2990-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="d2990-314"><a name="deleting"></a>Eliminación de datos en una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="d2990-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="d2990-315">Hola siguiente código muestra cómo toodelete datos de una tabla especificando Hola objeto de datos.</span><span class="sxs-lookup"><span data-stu-id="d2990-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="d2990-316">También puede eliminar un elemento mediante la especificación de hello **identificador** campo de hello toodelete de fila.</span><span class="sxs-lookup"><span data-stu-id="d2990-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="d2990-317"><a name="lookup"></a>Búsqueda de un elemento específico por el identificador</span><span class="sxs-lookup"><span data-stu-id="d2990-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="d2990-318">Buscar un elemento con un valor concreto **identificador** campo con hello **lookUp()** método:</span><span class="sxs-lookup"><span data-stu-id="d2990-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="d2990-319"><a name="untyped"></a>Trabajo con datos sin tipo</span><span class="sxs-lookup"><span data-stu-id="d2990-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="d2990-320">modelo de programación sin tipo Hello ofrece control exacto sobre la serialización de JSON.</span><span class="sxs-lookup"><span data-stu-id="d2990-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="d2990-321">Hay algunos escenarios comunes donde puede toouse un modelo de programación sin tipo.</span><span class="sxs-lookup"><span data-stu-id="d2990-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="d2990-322">Por ejemplo, si la tabla de back-end contiene muchas columnas y sólo necesita tooreference un subconjunto de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="d2990-323">modelo con tipo Hello requiere toodefine todas las columnas de hello definidas en el back-end de hello aplicaciones móviles en la clase de datos.</span><span class="sxs-lookup"><span data-stu-id="d2990-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="d2990-324">La mayoría de hello llamadas de API para tener acceso a datos es similar toohello escrito llamadas de programación.</span><span class="sxs-lookup"><span data-stu-id="d2990-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="d2990-325">Hello principal diferencia es que en el modelo sin tipo hello invoca métodos en hello **MobileServiceJsonTable** objeto, en lugar de hello **MobileServiceTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="d2990-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="d2990-326"><a name="json_instance"></a>Creación de una instancia de tabla sin tipo</span><span class="sxs-lookup"><span data-stu-id="d2990-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="d2990-327">Toohello similar con tipo modelo, primero debe obtener una referencia de tabla, pero en este caso es un **MobileServicesJsonTable** objeto.</span><span class="sxs-lookup"><span data-stu-id="d2990-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="d2990-328">Obtener referencia Hola Hola llamada **getTable** método en una instancia de cliente hello:</span><span class="sxs-lookup"><span data-stu-id="d2990-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="d2990-329">Una vez haya creado una instancia de hello **MobileServiceJsonTable**, prácticamente ha Hola misma API disponible como modelo de programación con tipo hello.</span><span class="sxs-lookup"><span data-stu-id="d2990-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="d2990-330">En algunos casos, los métodos de hello toman un parámetro sin tipo en lugar de un parámetro con tipo.</span><span class="sxs-lookup"><span data-stu-id="d2990-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="d2990-331"><a name="json_insert"></a>Inserción de una tabla sin tipo</span><span class="sxs-lookup"><span data-stu-id="d2990-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="d2990-332">Hola el siguiente código muestra cómo toodo una instrucción insert.</span><span class="sxs-lookup"><span data-stu-id="d2990-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="d2990-333">primer paso Hello es toocreate una [JsonObject][1], que forma parte del programa Hola a [gson] [ 3] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="d2990-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="d2990-334">A continuación, utilice **insert()** objeto sin tipo de hello tooinsert en tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="d2990-335">Si necesita tooget Hola ID de objeto de hello insertado, usar hello **getAsJsonPrimitive()** método.</span><span class="sxs-lookup"><span data-stu-id="d2990-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="d2990-336"><a name="json_delete"></a>Eliminación de una tabla sin tipo</span><span class="sxs-lookup"><span data-stu-id="d2990-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="d2990-337">Hello código siguiente muestra cómo toodelete una instancia, en este caso, Hola la misma instancia de un **JsonObject** que se creó en antes de hello *insertar* ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d2990-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="d2990-338">código de Hello es hello igual que con hello escribir caso, aunque método hello tiene una signatura diferente puesto que hace referencia a un **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="d2990-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="d2990-339">También puede eliminar una instancia directamente usando su identificador:</span><span class="sxs-lookup"><span data-stu-id="d2990-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="d2990-340"><a name="json_get"></a>Devolución de todas las filas de una tabla sin tipo</span><span class="sxs-lookup"><span data-stu-id="d2990-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="d2990-341">Hola el siguiente código muestra cómo tooretrieve una tabla completa.</span><span class="sxs-lookup"><span data-stu-id="d2990-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="d2990-342">Puesto que utiliza una tabla de JSON, puede recuperar selectivamente solo algunas de las columnas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="d2990-343">Hello mismo conjunto de filtrado, filtrado y paginación métodos que están disponibles para el modelo con tipo hello están disponibles para hello sin tipo modelo.</span><span class="sxs-lookup"><span data-stu-id="d2990-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="d2990-344"><a name="offline-sync"></a>Implementación de la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="d2990-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="d2990-345">Hola SDK de cliente de aplicaciones móviles de Azure también implementa sincronización sin conexión de datos con un toostore de base de datos de SQLite localmente una copia de datos del servidor de saludo.</span><span class="sxs-lookup"><span data-stu-id="d2990-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="d2990-346">Las operaciones realizadas en una tabla sin conexión no requieren conectividad móvil toowork.</span><span class="sxs-lookup"><span data-stu-id="d2990-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="d2990-347">Ayuda de sincronización sin conexión en la resistencia y el rendimiento a costa de Hola de una lógica más compleja para la resolución de conflictos.</span><span class="sxs-lookup"><span data-stu-id="d2990-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="d2990-348">Hola SDK de cliente de aplicaciones móviles de Azure implementa Hola siguientes características:</span><span class="sxs-lookup"><span data-stu-id="d2990-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="d2990-349">Sincronización incremental: solo se descargan registros nuevos y actualizados, lo que ahorra ancho de banda y consumo de memoria.</span><span class="sxs-lookup"><span data-stu-id="d2990-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="d2990-350">Simultaneidad optimista: Las operaciones se supone que toosucceed.</span><span class="sxs-lookup"><span data-stu-id="d2990-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="d2990-351">Resolución de conflictos se aplaza hasta que las actualizaciones se realizan en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="d2990-352">La resolución de conflictos: Hola que SDK detecta cuándo un cambio conflictivo se ha realizado en el servidor de Hola y proporciona enlaces de usuario de hello tooalert.</span><span class="sxs-lookup"><span data-stu-id="d2990-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="d2990-353">Eliminación temporal: Registros eliminados se marcan como eliminados, lo que permite a otro tooupdate de dispositivos en su caché sin conexión.</span><span class="sxs-lookup"><span data-stu-id="d2990-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="d2990-354">Inicialización de la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="d2990-354">Initialize Offline Sync</span></span>

<span data-ttu-id="d2990-355">Cada tabla sin conexión debe definirse en caché sin conexión de hello antes de su uso.</span><span class="sxs-lookup"><span data-stu-id="d2990-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="d2990-356">Normalmente, la definición de la tabla se realiza inmediatamente después de la creación de hello de cliente hello:</span><span class="sxs-lookup"><span data-stu-id="d2990-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="d2990-357">Obtener una tabla de la caché sin conexión de referencia toohello</span><span class="sxs-lookup"><span data-stu-id="d2990-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="d2990-358">Para una tabla en línea, use `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="d2990-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="d2990-359">Para una tabla sin conexión, use `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="d2990-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="d2990-360">Todos los Hola métodos que están disponibles para las tablas en línea (incluido el filtrado, ordenación, paginación, insertar datos, actualizar datos y eliminación de datos) también funcionan bien en tablas en línea y sin conexión.</span><span class="sxs-lookup"><span data-stu-id="d2990-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="d2990-361">Sincronizar Hola caché sin conexión Local</span><span class="sxs-lookup"><span data-stu-id="d2990-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="d2990-362">La sincronización está dentro del control de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2990-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="d2990-363">A continuación se muestra un método de sincronización de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2990-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="d2990-364">Si se proporciona un nombre de consulta toohello `.pull(query, queryname)` método, sincronización incremental es tooreturn utilizados solo los registros que se hayan creado o modificado desde la extracción de hello última se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="d2990-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="d2990-365">Control de los conflictos durante la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="d2990-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="d2990-366">Si tiene lugar un conflicto durante una operación `.push()`, se produce una excepción `MobileServiceConflictException`.</span><span class="sxs-lookup"><span data-stu-id="d2990-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="d2990-367">el elemento de servidor emitido Hola se incrusta en excepción hello y se puede recuperar `.getItem()` en la excepción de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="d2990-368">Ajustar la inserción de Hola por llamada Hola siguientes elementos en el objeto de Hola MobileServiceSyncContext:</span><span class="sxs-lookup"><span data-stu-id="d2990-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="d2990-369">Una vez que todos los conflictos se marcan como desee, llame a `.push()` nuevo tooresolve Hola a todos los conflictos.</span><span class="sxs-lookup"><span data-stu-id="d2990-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="d2990-370"><a name="custom-api"></a>Llamada a una API personalizada</span><span class="sxs-lookup"><span data-stu-id="d2990-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="d2990-371">Una API personalizada le permite toodefine extremos personalizados que exponen la funcionalidad de servidor que no asigne tooan Insertar, actualizar, eliminar o la operación de lectura.</span><span class="sxs-lookup"><span data-stu-id="d2990-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="d2990-372">Al usar una API personalizada, puede tener más control sobre la mensajería, incluida la lectura y el establecimiento de encabezados de mensajes HTTP y la definición del formato del cuerpo de un mensaje diferente de JSON.</span><span class="sxs-lookup"><span data-stu-id="d2990-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="d2990-373">Desde un cliente de Android, se llama a hello **invokeApi** método toocall Hola API punto de conexión personalizado.</span><span class="sxs-lookup"><span data-stu-id="d2990-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="d2990-374">Hello en el ejemplo siguiente se muestra cómo toocall un punto de conexión de API denominado **completeAll**, que devuelve una clase de colección denominada **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="d2990-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="d2990-375">Hola **invokeApi** método se llama en el cliente de hello, que envía una solicitud de una entrada de blog toohello nueva API personalizada.</span><span class="sxs-lookup"><span data-stu-id="d2990-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="d2990-376">resultado de Hello devuelto por la API personalizada hello se muestra en un cuadro de diálogo de mensaje, tal y como se han producido errores.</span><span class="sxs-lookup"><span data-stu-id="d2990-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="d2990-377">Otras versiones de **invokeApi** le permiten enviar un objeto en el cuerpo de la solicitud de hello, especificar método hello HTTP y enviar parámetros de consulta con la solicitud de hello si lo desea.</span><span class="sxs-lookup"><span data-stu-id="d2990-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="d2990-378">También se proporcionan versiones sin tipo de **invokeApi** .</span><span class="sxs-lookup"><span data-stu-id="d2990-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="d2990-379"><a name="authentication"></a>Agregar aplicación de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="d2990-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="d2990-380">Tutoriales ya se describen en detalle cómo tooadd estas características.</span><span class="sxs-lookup"><span data-stu-id="d2990-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="d2990-381">App Service admite la [autenticación de los usuarios de aplicaciones](app-service-mobile-android-get-started-users.md) mediante diversos proveedores de identidades externos: Facebook, Google, cuenta de Microsoft, Twitter y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2990-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="d2990-382">Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d2990-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="d2990-383">También puede utilizar la identidad de Hola a los usuarios autenticados tooimplement de reglas de autorización en el back-end.</span><span class="sxs-lookup"><span data-stu-id="d2990-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="d2990-384">Se admiten dos flujos de autenticación: un flujo de **servidor** y un flujo de **cliente**.</span><span class="sxs-lookup"><span data-stu-id="d2990-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="d2990-385">flujo de servidor Hello proporciona experiencia de autenticación más sencilla de hello, tal y como se basa en la interfaz de web de proveedores de identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="d2990-386">Ningún SDK adicionales es tooimplement requiere autenticación de flujo del servidor.</span><span class="sxs-lookup"><span data-stu-id="d2990-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="d2990-387">Autenticación de servidor flujo no proporciona una estrecha integración en dispositivos móviles de Hola y sólo se recomienda para la prueba de escenarios de concepto.</span><span class="sxs-lookup"><span data-stu-id="d2990-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="d2990-388">flujo de cliente Hello permite una integración más profunda con capacidades específicas del dispositivo, como el inicio de sesión único ya que se basa en SDK proporcionado por el proveedor de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="d2990-389">Por ejemplo, puede integrar Hola Facebook SDK en la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d2990-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="d2990-390">cliente móvil de Hello intercambia en aplicación de Facebook hello y confirma su inicio de sesión antes de intercambiar las aplicación móvil de back-tooyour.</span><span class="sxs-lookup"><span data-stu-id="d2990-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="d2990-391">Cuatro pasos son tooenable requiere la autenticación en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d2990-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="d2990-392">Registre la aplicación para llevar a cabo la autenticación con un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="d2990-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="d2990-393">Configure el back-end de App Service.</span><span class="sxs-lookup"><span data-stu-id="d2990-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="d2990-394">Restringir permisos de tabla tooauthenticated los usuarios solo en hello back-end del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d2990-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="d2990-395">Agregar aplicación de tooyour de código de autenticación.</span><span class="sxs-lookup"><span data-stu-id="d2990-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="d2990-396">Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d2990-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="d2990-397">También puede usar Hola SID de un usuario autenticado toomodify solicitudes.</span><span class="sxs-lookup"><span data-stu-id="d2990-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="d2990-398">Para obtener más información, consulte [empezar a trabajar con autenticación] y Hola documentación HOWTO de SDK de servidor.</span><span class="sxs-lookup"><span data-stu-id="d2990-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="d2990-399"><a name="caching"></a>Autenticación: flujo de servidor</span><span class="sxs-lookup"><span data-stu-id="d2990-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="d2990-400">Hello código siguiente inicia un proceso de inicio de sesión de flujo de servidor mediante el proveedor de Google Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="d2990-401">Se requiere configuración adicional debido a los requisitos de seguridad de hello para el proveedor de Hola de Google:</span><span class="sxs-lookup"><span data-stu-id="d2990-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="d2990-402">Además, agregue Hola después de la clase de actividad de método toohello principal:</span><span class="sxs-lookup"><span data-stu-id="d2990-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="d2990-403">Hola `GOOGLE_LOGIN_REQUEST_CODE` definido en la ventana principal de actividad se usa para hello `login()` método y dentro de hello `onActivityResult()` método.</span><span class="sxs-lookup"><span data-stu-id="d2990-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="d2990-404">Puede elegir cualquier número único, como hello tantos sirve de hello `login()` hello y método `onActivityResult()` método.</span><span class="sxs-lookup"><span data-stu-id="d2990-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="d2990-405">Si se abstraer el código de cliente de hello en un adaptador de servicio (como se muestra anteriormente), debe llamar a los métodos adecuados de hello en el adaptador del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="d2990-406">También necesita proyecto de hello tooconfigure para customtabs.</span><span class="sxs-lookup"><span data-stu-id="d2990-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="d2990-407">En primer lugar, especifique una dirección URL de redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="d2990-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="d2990-408">Agregar Hola siguiente fragmento de código demasiado`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="d2990-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="d2990-409">Agregar hello **redirectUriScheme** toohello `build.gradle` archivo de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="d2990-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="d2990-410">Por último, agregue `com.android.support:customtabs:23.0.1` toohello lista de dependencias en hello `build.gradle` archivo:</span><span class="sxs-lookup"><span data-stu-id="d2990-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="d2990-411">Obtener Id. de Hola Hola ha iniciado la sesión del usuario de desde una **MobileServiceUser** con hello **getUserId** método.</span><span class="sxs-lookup"><span data-stu-id="d2990-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="d2990-412">Para obtener un ejemplo de cómo toouse futuros toocall Hola API de inicio de sesión asincrónica, vea [empezar a trabajar con autenticación].</span><span class="sxs-lookup"><span data-stu-id="d2990-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="d2990-413">Hola menciona el esquema de dirección URL distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d2990-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="d2990-414">Asegúrese de que todas las apariciones de `{url_scheme_of_you_app}` coincidan en las mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d2990-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="d2990-415"><a name="caching"></a>Almacenamiento en caché de tokens de autenticación</span><span class="sxs-lookup"><span data-stu-id="d2990-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="d2990-416">Almacenamiento en caché de tokens de autenticación requiere toostore Hola Id. de usuario y el token de autenticación localmente en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="d2990-417">Hello próxima vez que se inicia la aplicación hello, compruebe caché hello, y si estos valores están presentes, puede omitir el registro de hello en procedimiento y rehidratar a cliente hello con estos datos.</span><span class="sxs-lookup"><span data-stu-id="d2990-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="d2990-418">Sin embargo, estos datos son importantes y deben almacenarse cifrarse por razones de seguridad en caso de que roben phone Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="d2990-419">Puede ver un ejemplo completo de cómo los tokens de autenticación de toocache en [sección de tokens de autenticación de caché][7].</span><span class="sxs-lookup"><span data-stu-id="d2990-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="d2990-420">Cuando intente toouse un token caducado, recibirá un *401 no autorizado* respuesta.</span><span class="sxs-lookup"><span data-stu-id="d2990-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="d2990-421">Puede controlar los errores de autenticación usando filtros.</span><span class="sxs-lookup"><span data-stu-id="d2990-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="d2990-422">Filtros de interceptan las solicitudes toohello back-end del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d2990-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="d2990-423">código de filtro de Hello comprueba la respuesta de Hola para 401, desencadena el proceso de inicio de sesión de hello y, a continuación, reanuda la solicitud de Hola que generan Hola 401.</span><span class="sxs-lookup"><span data-stu-id="d2990-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="d2990-424"><a name="refresh"></a>Uso de tokens de actualización</span><span class="sxs-lookup"><span data-stu-id="d2990-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="d2990-425">símbolo (token) de Hello devuelto por la autorización y autenticación del servicio de aplicación de Azure tiene un tiempo de vida definidos de una hora.</span><span class="sxs-lookup"><span data-stu-id="d2990-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="d2990-426">Después de este período, debe volver a autenticar usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="d2990-427">Si está utilizando un token de larga duración que han recibido a través de la autenticación de flujo de cliente, a continuación, puede volver a autenticar con la autenticación de servicio de aplicación de Azure y la autorización mediante Hola mismo símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="d2990-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="d2990-428">Se genera otro token de Azure App Service con una nueva duración.</span><span class="sxs-lookup"><span data-stu-id="d2990-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="d2990-429">También puede registrar Hola proveedor toouse Tokens de actualización.</span><span class="sxs-lookup"><span data-stu-id="d2990-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="d2990-430">Un token de actualización no está siempre disponible.</span><span class="sxs-lookup"><span data-stu-id="d2990-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="d2990-431">Se requiere configuración adicional:</span><span class="sxs-lookup"><span data-stu-id="d2990-431">Additional configuration is required:</span></span>

* <span data-ttu-id="d2990-432">Para **Azure Active Directory**, configurar un secreto de cliente para hello aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2990-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="d2990-433">Especifique el secreto del cliente de Hola en Hola servicio de aplicaciones de Azure al configurar la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2990-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="d2990-434">Al llamar a `.login()`, pase `response_type=code id_token` como parámetro:</span><span class="sxs-lookup"><span data-stu-id="d2990-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="d2990-435">Para **Google**, pasar hello `access_type=offline` como parámetro:</span><span class="sxs-lookup"><span data-stu-id="d2990-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="d2990-436">Para **Account Microsoft**, seleccione hello `wl.offline_access` ámbito.</span><span class="sxs-lookup"><span data-stu-id="d2990-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="d2990-437">toorefresh un token, llame a `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="d2990-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="d2990-438">Como práctica recomendada, cree un filtro que detecta una respuesta 401 desde servidor hello y trata de token de usuario de toorefresh Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="d2990-439">Inicio de sesión con la autenticación de flujo de cliente</span><span class="sxs-lookup"><span data-stu-id="d2990-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="d2990-440">proceso general de Hello para iniciar sesión con autenticación de cliente flujo es como sigue:</span><span class="sxs-lookup"><span data-stu-id="d2990-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="d2990-441">Configure Autenticación y autorización de Azure App Service como haría con la autenticación de flujo de servidor.</span><span class="sxs-lookup"><span data-stu-id="d2990-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="d2990-442">Integrar el proveedor de autenticación de hello SDK para autenticación tooproduce un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="d2990-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="d2990-443">Llamar a hello `.login()` método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d2990-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="d2990-444">Reemplace hello `onSuccess()` método con cualquier código que se desea toouse en un inicio de sesión correcto.</span><span class="sxs-lookup"><span data-stu-id="d2990-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="d2990-445">Hola `{provider}` cadena es un proveedor válido: **aad** (Azure Active Directory), **facebook**, **google**, **cuenta de Microsoft**, o **twitter**.</span><span class="sxs-lookup"><span data-stu-id="d2990-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="d2990-446">Si ha implementado la autenticación personalizada, también puede utilizar etiquetas de proveedor de autenticación personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="d2990-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="d2990-447"><a name="adal"></a>Autenticar a los usuarios con hello biblioteca de autenticación de Active Directory (ADAL)</span><span class="sxs-lookup"><span data-stu-id="d2990-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="d2990-448">Puede usar los usuarios de toosign de hello biblioteca de autenticación de Active Directory (ADAL) en la aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d2990-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="d2990-449">Mediante un inicio de sesión de flujo de cliente suele ser preferible toousing hello `loginAsync()` métodos tal como se proporciona una idea UX más nativa y permite la personalización adicional.</span><span class="sxs-lookup"><span data-stu-id="d2990-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d2990-450">Configurar el aplicación móvil de back-end para el inicio de sesión AAD Hola siguiente [cómo tooconfigure aplicación de servicio de inicio de sesión de Active Directory] [ 22] tutorial.</span><span class="sxs-lookup"><span data-stu-id="d2990-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="d2990-451">Asegúrese de que paso opcional de Hola de toocomplete de registrar una aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="d2990-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="d2990-452">Instalar AAL modificando su Hola de tooinclude de archivo build.gradle siguientes definiciones:</span><span class="sxs-lookup"><span data-stu-id="d2990-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="d2990-453">Agregue Hola tras la aplicación de código tooyour, por lo que Hola después reemplazos:</span><span class="sxs-lookup"><span data-stu-id="d2990-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="d2990-454">Reemplace **aquí de autoridad de INSERCIÓN** por nombre de Hola de inquilino de hello en el que se aprovisiona la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2990-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="d2990-455">formato de Hello debe ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d2990-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="d2990-456">Reemplace **Insertar recurso identificador aquí** con el identificador de cliente de Hola para su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="d2990-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="d2990-457">Puede obtener Id. de cliente de Hola de hello **avanzadas** en la ficha **configuración de Azure Active Directory** en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="d2990-458">Reemplace **INSERT-CLIENT-ID-aquí** con el Id. de cliente de Hola que copió de la aplicación de cliente nativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="d2990-459">Reemplace **INSERT-REDIRECT-URI-aquí** con su sitio */.auth/login/done* punto de conexión, mediante el esquema de hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d2990-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="d2990-460">Este valor debe ser similar demasiado*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="d2990-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="d2990-461"><a name="filters"></a>Ajustar Hola comunicación entre cliente y servidor</span><span class="sxs-lookup"><span data-stu-id="d2990-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="d2990-462">Hola conexión de cliente es normalmente una conexión HTTP básica con hello subyacente de la biblioteca HTTP que se suministra con hello SDK de Android.</span><span class="sxs-lookup"><span data-stu-id="d2990-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="d2990-463">Hay varios motivos por los que desearía toochange que:</span><span class="sxs-lookup"><span data-stu-id="d2990-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="d2990-464">Que se van a toouse una alternativa HTTP biblioteca tooadjust los tiempos de espera.</span><span class="sxs-lookup"><span data-stu-id="d2990-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="d2990-465">Que se va a tooprovide una barra de progreso.</span><span class="sxs-lookup"><span data-stu-id="d2990-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="d2990-466">Que se va a tooadd una funcionalidad de administración de toosupport API de encabezado personalizado.</span><span class="sxs-lookup"><span data-stu-id="d2990-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="d2990-467">Que se va a toointercept una respuesta error para que puedan implementar la reautenticación.</span><span class="sxs-lookup"><span data-stu-id="d2990-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="d2990-468">Desea que el servicio de análisis de tooan las solicitudes de toolog back-end.</span><span class="sxs-lookup"><span data-stu-id="d2990-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="d2990-469">Uso de una biblioteca HTTP alternativa</span><span class="sxs-lookup"><span data-stu-id="d2990-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="d2990-470">Llamar a hello `.setAndroidHttpClientFactory()` método inmediatamente después de crear la referencia de cliente.</span><span class="sxs-lookup"><span data-stu-id="d2990-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="d2990-471">Por ejemplo, tooset Hola conexión too60 segundos de espera (en lugar de valor predeterminado de hello 10 segundos):</span><span class="sxs-lookup"><span data-stu-id="d2990-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="d2990-472">Implementación de un filtro de progreso</span><span class="sxs-lookup"><span data-stu-id="d2990-472">Implement a Progress Filter</span></span>

<span data-ttu-id="d2990-473">Puede implementar una intersección de todas las solicitudes mediante la implementación de `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="d2990-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="d2990-474">Por ejemplo, la siguiente Hola actualiza una barra de progreso creada previamente:</span><span class="sxs-lookup"><span data-stu-id="d2990-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="d2990-475">Puede adjuntar a este cliente de toohello de filtro como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d2990-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="d2990-476">Personalización de los encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="d2990-476">Customize Request Headers</span></span>

<span data-ttu-id="d2990-477">Utilice Hola siguiente `ServiceFilter` y adjuntar filtro Hola Hola igual que Hola `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="d2990-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="d2990-478"><a name="conversions"></a>Configuración de serialización automática</span><span class="sxs-lookup"><span data-stu-id="d2990-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="d2990-479">Puede especificar una estrategia de conversión que se aplica tooevery columna mediante el uso de hello [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="d2990-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="d2990-480">biblioteca de cliente de Android Hello usa [gson] [ 3] entre bastidores de hello tooserialize Java objetos tooJSON datos antes de enviar datos de hello tooAzure servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d2990-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="d2990-481">Hello código siguiente usa hello **setFieldNamingStrategy()** estrategia del método tooset Hola.</span><span class="sxs-lookup"><span data-stu-id="d2990-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="d2990-482">En este ejemplo se eliminará Hola inicial (una "m"), minúsculas, a continuación, Hola siguiente caracteres y, por cada nombre de campo.</span><span class="sxs-lookup"><span data-stu-id="d2990-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="d2990-483">Por ejemplo, convertiría "mld" en "id".</span><span class="sxs-lookup"><span data-stu-id="d2990-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="d2990-484">Implemente un hello tooreduce de estrategia de conversión necesita para `SerializedName()` las anotaciones en la mayoría de los campos.</span><span class="sxs-lookup"><span data-stu-id="d2990-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="d2990-485">Este código debe ejecutarse antes de crear una referencia de cliente móvil mediante hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="d2990-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[empezar a trabajar con autenticación]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
