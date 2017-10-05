---
title: Uso del SDK de Azure Mobile Apps para Android | Microsoft Docs
description: Uso del SDK de Azure Mobile Apps para Android
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
ms.openlocfilehash: 4b15d024ca6d5bbafe83d321a64021aecd78c4a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="113d7-103">Uso del SDK de Azure Mobile Apps para Android</span><span class="sxs-lookup"><span data-stu-id="113d7-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="113d7-104">En esta guía se muestra cómo utilizar el SDK cliente de Android para Mobile Apps con el objetivo de implementar escenarios comunes, como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="113d7-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="113d7-105">Consultas de datos (inserción, actualización y eliminación)</span><span class="sxs-lookup"><span data-stu-id="113d7-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="113d7-106">Autenticación</span><span class="sxs-lookup"><span data-stu-id="113d7-106">Authentication.</span></span>
* <span data-ttu-id="113d7-107">Control de errores</span><span class="sxs-lookup"><span data-stu-id="113d7-107">Handling errors.</span></span>
* <span data-ttu-id="113d7-108">Personalización del cliente</span><span class="sxs-lookup"><span data-stu-id="113d7-108">Customizing the client.</span></span>

<span data-ttu-id="113d7-109">Esta guía se centra en el SDK de Android del cliente.</span><span class="sxs-lookup"><span data-stu-id="113d7-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="113d7-110">Para más información sobre los SDK del lado servidor para Mobile Apps, consulte [Trabajar con el SDK del back-end de .NET][10] o [Cómo usar el SDK del back-end de Node.js][11].</span><span class="sxs-lookup"><span data-stu-id="113d7-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="113d7-111">Documentación de referencia</span><span class="sxs-lookup"><span data-stu-id="113d7-111">Reference Documentation</span></span>

<span data-ttu-id="113d7-112">Puede encontrar la [referencia de API de Javadocs][12] para la biblioteca de cliente Android en GitHub.</span><span class="sxs-lookup"><span data-stu-id="113d7-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="113d7-113">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="113d7-113">Supported Platforms</span></span>

<span data-ttu-id="113d7-114">El SDK de Azure Mobile Apps para Android admite los niveles de API del 19 al 24 (de KitKat a Nougat) para teléfonos y tabletas.</span><span class="sxs-lookup"><span data-stu-id="113d7-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="113d7-115">En concreto, la recopilación de credenciales para la autenticación se basa en un marco web común.</span><span class="sxs-lookup"><span data-stu-id="113d7-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="113d7-116">La autenticación de flujo de servidor no funciona con dispositivos pequeños, por ejemplo, relojes.</span><span class="sxs-lookup"><span data-stu-id="113d7-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="113d7-117">Configuración y requisitos previos</span><span class="sxs-lookup"><span data-stu-id="113d7-117">Setup and Prerequisites</span></span>

<span data-ttu-id="113d7-118">Complete el tutorial de [inicio rápido de Mobile Apps](app-service-mobile-android-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="113d7-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="113d7-119">Esta tarea garantiza que se cumplan todos los requisitos previos del desarrollo de aplicaciones de Mobile Apps de Azure.</span><span class="sxs-lookup"><span data-stu-id="113d7-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="113d7-120">El tutorial de inicio rápido ayuda a configurar la cuenta y a crear el primer back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="113d7-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="113d7-121">Si decide no completar el tutorial de inicio rápido, realice las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="113d7-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="113d7-122">[Cree un nuevo back-end de aplicación móvil][13] para usarlo con su aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="113d7-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="113d7-123">En Android Studio, [actualice los archivos de compilación de Gradle](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="113d7-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="113d7-124">[Habilite permisos de Internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="113d7-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="113d7-125"><a name="gradle-build"></a>Actualización del archivo de compilación de Gradle</span><span class="sxs-lookup"><span data-stu-id="113d7-125"><a name="gradle-build"></a>Update the Gradle build file</span></span>

<span data-ttu-id="113d7-126">Cambie ambos archivos **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="113d7-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="113d7-127">Agregue este código al archivo *build.gradle* del nivel **Project** dentro de la etiqueta *buildscript*:</span><span class="sxs-lookup"><span data-stu-id="113d7-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="113d7-128">Agregue este código al archivo *build.gradle* del nivel **Module app** dentro de la etiqueta *dependencies*:</span><span class="sxs-lookup"><span data-stu-id="113d7-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="113d7-129">Actualmente, la versión más reciente es la 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="113d7-129">Currently the latest version is 3.3.0.</span></span> <span data-ttu-id="113d7-130">Las versiones compatibles se indican [en Bintray][14].</span><span class="sxs-lookup"><span data-stu-id="113d7-130">The supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="113d7-131"><a name="enable-internet"></a>Habilitación de permisos de Internet</span><span class="sxs-lookup"><span data-stu-id="113d7-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="113d7-132">Para obtener acceso a Azure, la aplicación debe tener habilitado el permiso de INTERNET.</span><span class="sxs-lookup"><span data-stu-id="113d7-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="113d7-133">Si aún no está habilitado, agregue la siguiente línea de código a su archivo **AndroidManifest.xml** :</span><span class="sxs-lookup"><span data-stu-id="113d7-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="113d7-134">Creación de una conexión de cliente</span><span class="sxs-lookup"><span data-stu-id="113d7-134">Create a Client Connection</span></span>

<span data-ttu-id="113d7-135">Azure Mobile Apps proporciona cuatro funciones para sus aplicaciones móviles:</span><span class="sxs-lookup"><span data-stu-id="113d7-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="113d7-136">Acceso a datos y sincronización sin conexión con un servicio de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="113d7-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="113d7-137">Llamada a API personalizadas escritas con el SDK de servidor de Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="113d7-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="113d7-138">Autenticación con Autenticación y autorización de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="113d7-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="113d7-139">Registro de notificaciones push con Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="113d7-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="113d7-140">Cada una de estas funciones requiere en primer lugar que se cree un objeto `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="113d7-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="113d7-141">Solo se debe crear un objeto `MobileServiceClient` dentro de su cliente móvil (es decir, debe tener un patrón singleton).</span><span class="sxs-lookup"><span data-stu-id="113d7-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="113d7-142">Para crear un objeto `MobileServiceClient`:</span><span class="sxs-lookup"><span data-stu-id="113d7-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="113d7-143">`<MobileAppUrl>` es una cadena o un objeto de URL que apunta a su back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="113d7-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="113d7-144">Si va a usar Azure App Service para hospedar su back-end móvil, asegúrese de utilizar la versión `https://` segura de la URL.</span><span class="sxs-lookup"><span data-stu-id="113d7-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="113d7-145">El cliente también necesita acceso a la actividad o contexto; en este ejemplo, el parámetro `this`.</span><span class="sxs-lookup"><span data-stu-id="113d7-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="113d7-146">La construcción de MobileServiceClient debe tener lugar dentro del método `onCreate()` de la actividad a la que se hace referencia en el archivo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="113d7-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="113d7-147">Como procedimiento recomendado, debe abstraer la comunicación del servidor en su propia clase (patrón singleton).</span><span class="sxs-lookup"><span data-stu-id="113d7-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="113d7-148">En este caso, debe pasar la actividad dentro del constructor para configurar el servicio de manera adecuada.</span><span class="sxs-lookup"><span data-stu-id="113d7-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="113d7-149">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="113d7-149">For example:</span></span>

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

<span data-ttu-id="113d7-150">Ahora puede llamar a `AzureServiceAdapter.Initialize(this);` en el método `onCreate()` de su actividad principal.</span><span class="sxs-lookup"><span data-stu-id="113d7-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="113d7-151">Los otros métodos que necesitan acceso al cliente usan `AzureServiceAdapter.getInstance();` para obtener una referencia al adaptador de servicio.</span><span class="sxs-lookup"><span data-stu-id="113d7-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="113d7-152">Operaciones de datos</span><span class="sxs-lookup"><span data-stu-id="113d7-152">Data Operations</span></span>

<span data-ttu-id="113d7-153">La base del SDK de Azure Mobile Apps es proporcionar acceso a los datos almacenados dentro de SQL Azure en el back-end de Mobile App.</span><span class="sxs-lookup"><span data-stu-id="113d7-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="113d7-154">Se puede acceder a estos datos mediante clases fuertemente tipadas (preferidas) o consultas sin tipo (no se recomienda).</span><span class="sxs-lookup"><span data-stu-id="113d7-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="113d7-155">La mayor parte de esta sección trata del uso de clases fuertemente tipadas.</span><span class="sxs-lookup"><span data-stu-id="113d7-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="113d7-156">Definición de clases de datos de cliente</span><span class="sxs-lookup"><span data-stu-id="113d7-156">Define client data classes</span></span>

<span data-ttu-id="113d7-157">Para acceder a los datos de tablas de SQL Azure, defina las clases de datos cliente que corresponden a las tablas del back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="113d7-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="113d7-158">En los ejemplos de este tema se usa una tabla denominada **MyDataTable**, que tiene las siguientes columnas:</span><span class="sxs-lookup"><span data-stu-id="113d7-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="113d7-159">id</span><span class="sxs-lookup"><span data-stu-id="113d7-159">id</span></span>
* <span data-ttu-id="113d7-160">text</span><span class="sxs-lookup"><span data-stu-id="113d7-160">text</span></span>
* <span data-ttu-id="113d7-161">complete</span><span class="sxs-lookup"><span data-stu-id="113d7-161">complete</span></span>

<span data-ttu-id="113d7-162">El objeto de cliente con tipo correspondiente reside en un archivo denominado **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="113d7-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="113d7-163">Agregue los métodos captador y establecedor para cada campo que agregue.</span><span class="sxs-lookup"><span data-stu-id="113d7-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="113d7-164">Si la tabla de SQL Azure contuviera más columnas, agregaría los campos correspondientes a esta clase.</span><span class="sxs-lookup"><span data-stu-id="113d7-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="113d7-165">Por ejemplo, si el DTO (objeto de transferencia de datos) tuviera una columna Prioridad de tipo entero, podría agregar este campo junto con sus métodos de captador y establecedor:</span><span class="sxs-lookup"><span data-stu-id="113d7-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="113d7-166">Para más información sobre cómo crear tablas adicionales en el back-end de Mobile Apps, consulte [Cómo definir un controlador de tabla][15] (back-end de. NET) o [Definición de tablas con un esquema dinámico][16] (back-end de Node.js).</span><span class="sxs-lookup"><span data-stu-id="113d7-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="113d7-167">Una tabla de back-end de Azure Mobile Apps define cinco campos especiales, cuatro de los cuales están disponibles para los clientes:</span><span class="sxs-lookup"><span data-stu-id="113d7-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="113d7-168">`String id`: el identificador único global del registro.</span><span class="sxs-lookup"><span data-stu-id="113d7-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="113d7-169">Como procedimiento recomendado, convierta el identificador en la representación de cadena de un objeto [UUID][17].</span><span class="sxs-lookup"><span data-stu-id="113d7-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="113d7-170">`DateTimeOffset updatedAt`: la fecha y hora de la última actualización.</span><span class="sxs-lookup"><span data-stu-id="113d7-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="113d7-171">El campo updatedAt lo establece el servidor; nunca lo debe establecer el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="113d7-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="113d7-172">`DateTimeOffset createdAt`: la fecha y hora en que se creó el objeto.</span><span class="sxs-lookup"><span data-stu-id="113d7-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="113d7-173">El campo createdAt lo establece el servidor; nunca lo debe establecer el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="113d7-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="113d7-174">`byte[] version`: normalmente se representa como una cadena; la versión la establece también el servidor.</span><span class="sxs-lookup"><span data-stu-id="113d7-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="113d7-175">`boolean deleted`: indica que el registro se ha eliminado pero no se ha purgado aún.</span><span class="sxs-lookup"><span data-stu-id="113d7-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="113d7-176">No use `deleted` como propiedad en la clase.</span><span class="sxs-lookup"><span data-stu-id="113d7-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="113d7-177">El campo `id` es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="113d7-177">The `id` field is required.</span></span>  <span data-ttu-id="113d7-178">Los campos `updatedAt` y `version` se usan para la sincronización sin conexión (para la sincronización incremental y la resolución de conflictos, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="113d7-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="113d7-179">El campo `createdAt` es un campo de referencia y el cliente no lo utiliza.</span><span class="sxs-lookup"><span data-stu-id="113d7-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="113d7-180">Los nombres son nombres "a través de la red" de las propiedades y no son ajustables.</span><span class="sxs-lookup"><span data-stu-id="113d7-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="113d7-181">Sin embargo, puede crear una asignación entre el objeto y los nombres "a través de la red" con la biblioteca [gson][3].</span><span class="sxs-lookup"><span data-stu-id="113d7-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="113d7-182">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="113d7-182">For example:</span></span>

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

### <a name="create-a-table-reference"></a><span data-ttu-id="113d7-183">Creación de una referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="113d7-183">Create a Table Reference</span></span>

<span data-ttu-id="113d7-184">Para obtener acceso a una tabla, cree primero un objeto [MobileServiceTable][8] mediante una llamada al método **getTable** en [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="113d7-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="113d7-185">Este método tiene dos sobrecargas:</span><span class="sxs-lookup"><span data-stu-id="113d7-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="113d7-186">En el código siguiente, **mClient** es una referencia al objeto MobileServiceClient.</span><span class="sxs-lookup"><span data-stu-id="113d7-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="113d7-187">La primera sobrecarga se utiliza cuando coinciden el nombre de clase y el nombre de tabla, y es la que se emplea en el tutorial de inicio rápido:</span><span class="sxs-lookup"><span data-stu-id="113d7-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="113d7-188">La segunda sobrecarga se utiliza cuando el nombre de tabla es diferente del nombre de clase: el primer parámetro es el nombre de tabla.</span><span class="sxs-lookup"><span data-stu-id="113d7-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="113d7-189"><a name="query"></a>Consulta de una tabla de back-end</span><span class="sxs-lookup"><span data-stu-id="113d7-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="113d7-190">En primer lugar, obtenga una referencia de tabla.</span><span class="sxs-lookup"><span data-stu-id="113d7-190">First, obtain a table reference.</span></span>  <span data-ttu-id="113d7-191">A continuación, ejecute una consulta en la referencia de tabla.</span><span class="sxs-lookup"><span data-stu-id="113d7-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="113d7-192">Una consulta es cualquier combinación de:</span><span class="sxs-lookup"><span data-stu-id="113d7-192">A query is any combination of:</span></span>

* <span data-ttu-id="113d7-193">Una `.where()` [cláusula de filtro](#filtering).</span><span class="sxs-lookup"><span data-stu-id="113d7-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="113d7-194">Una `.orderBy()` [cláusula de ordenación](#sorting).</span><span class="sxs-lookup"><span data-stu-id="113d7-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="113d7-195">Una `.select()` [cláusula de selección de campos](#selection).</span><span class="sxs-lookup"><span data-stu-id="113d7-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="113d7-196">Una cláusula `.skip()` y `.top()` para [resultados paginados](#paging).</span><span class="sxs-lookup"><span data-stu-id="113d7-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="113d7-197">Las cláusulas deben presentarse en el orden anterior.</span><span class="sxs-lookup"><span data-stu-id="113d7-197">The clauses must be presented in the preceding order.</span></span>

### <span data-ttu-id="113d7-198"><a name="filter"></a>Filtrado de los resultados</span><span class="sxs-lookup"><span data-stu-id="113d7-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="113d7-199">La forma general de una consulta es:</span><span class="sxs-lookup"><span data-stu-id="113d7-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="113d7-200">En el ejemplo anterior se devuelven todos los resultados (hasta el tamaño máximo de página establecido por el servidor).</span><span class="sxs-lookup"><span data-stu-id="113d7-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="113d7-201">El método `.execute()` ejecuta la consulta en el back-end.</span><span class="sxs-lookup"><span data-stu-id="113d7-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="113d7-202">La consulta se convierte en una consulta [OData v3][19] antes de la transmisión al back.end de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="113d7-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="113d7-203">A la recepción, el back-end de Mobile Apps convierte la consulta en una instrucción SQL antes de ejecutarla en la instancia de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="113d7-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="113d7-204">Dado que la actividad de red tarda algún tiempo, el método `.execute()` devuelve [`ListenableFuture<E>`][18].</span><span class="sxs-lookup"><span data-stu-id="113d7-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="113d7-205"><a name="filtering"></a>Filtrado de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="113d7-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="113d7-206">La ejecución de la consulta siguiente devuelve todos los elementos de la tabla **ToDoItem** en los que **complete** es igual a **false**.</span><span class="sxs-lookup"><span data-stu-id="113d7-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="113d7-207">**mToDoTable** es la referencia a la tabla de servicio móvil que se ha creado previamente.</span><span class="sxs-lookup"><span data-stu-id="113d7-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="113d7-208">Se define un filtro mediante la llamada al método **where** en la referencia de tabla.</span><span class="sxs-lookup"><span data-stu-id="113d7-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="113d7-209">Al método **where** le sigue un método **field** y a este le sigue un método que especifica el predicado lógico.</span><span class="sxs-lookup"><span data-stu-id="113d7-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="113d7-210">Los posibles métodos de predicado incluyen **eq** (igual a), **ne** (no igual a), **gt** (mayor que), **ge** (mayor o igual que), **lt** (menor que) o **le** (menor o igual que).</span><span class="sxs-lookup"><span data-stu-id="113d7-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="113d7-211">Estos métodos permiten comparar campos de número y cadena con valores específicos.</span><span class="sxs-lookup"><span data-stu-id="113d7-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="113d7-212">Puede filtrar por fechas.</span><span class="sxs-lookup"><span data-stu-id="113d7-212">You can filter on dates.</span></span> <span data-ttu-id="113d7-213">Los métodos siguientes permiten comparar el campo de fecha entero o partes de la fecha: **year**, **month**, **day**, **hour**, **minute** y **second**.</span><span class="sxs-lookup"><span data-stu-id="113d7-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="113d7-214">El ejemplo siguiente agrega un filtro para los elementos cuyo valor *due date* sea igual a 2013.</span><span class="sxs-lookup"><span data-stu-id="113d7-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="113d7-215">Los métodos siguientes admiten filtros complejos en campos de cadena: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim** y **length**.</span><span class="sxs-lookup"><span data-stu-id="113d7-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="113d7-216">El ejemplo siguiente filtra las filas de tabla donde la columna *text* empieza por PRI0.</span><span class="sxs-lookup"><span data-stu-id="113d7-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="113d7-217">En los campos de número se admiten los siguientes métodos de operador: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling** y **round**.</span><span class="sxs-lookup"><span data-stu-id="113d7-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="113d7-218">El ejemplo siguiente filtra las filas de tabla en las que **duration** es un número par.</span><span class="sxs-lookup"><span data-stu-id="113d7-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="113d7-219">Puede combinar predicados con estos métodos lógicos: **and**, **or** y **not**.</span><span class="sxs-lookup"><span data-stu-id="113d7-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="113d7-220">En el ejemplo siguiente se combinan dos de los ejemplos anteriores.</span><span class="sxs-lookup"><span data-stu-id="113d7-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="113d7-221">Agrupe y anide los operadores lógicos:</span><span class="sxs-lookup"><span data-stu-id="113d7-221">Group and nest logical operators:</span></span>

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

<span data-ttu-id="113d7-222">Para obtener más información y ver ejemplos de filtrado, consulte [Exploring the richness of the Android client query model ][20] (Exploración de la riqueza del modelo de consulta del cliente Android).</span><span class="sxs-lookup"><span data-stu-id="113d7-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <span data-ttu-id="113d7-223"><a name="sorting"></a>Ordenación de datos devueltos</span><span class="sxs-lookup"><span data-stu-id="113d7-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="113d7-224">El código siguiente devuelve todos los elementos de una tabla de **ToDoItems** cuyo campo *text* sigue un orden ascendente.</span><span class="sxs-lookup"><span data-stu-id="113d7-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="113d7-225">*mToDoTable* es la referencia a la tabla del back-end que ha creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="113d7-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="113d7-226">El primer parámetro del método **orderBy** es una cadena igual al nombre del campo por el que realizar la ordenación.</span><span class="sxs-lookup"><span data-stu-id="113d7-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="113d7-227">El segundo parámetro usa la enumeración **QueryOrder** para especificar si la ordenación será ascendente o descendente.</span><span class="sxs-lookup"><span data-stu-id="113d7-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="113d7-228">Si filtra con el método ***where***, este debe invocarse ***antes*** del método ***orderBy***.</span><span class="sxs-lookup"><span data-stu-id="113d7-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <span data-ttu-id="113d7-229"><a name="selection"></a>Selección de columnas específicas</span><span class="sxs-lookup"><span data-stu-id="113d7-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="113d7-230">El código siguiente ilustra cómo devolver todos los elementos de una tabla de **ToDoItems**, pero solo muestra los campos **complete** y **text**.</span><span class="sxs-lookup"><span data-stu-id="113d7-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="113d7-231">**mToDoTable** es la referencia a la tabla de back-end que se ha creado previamente.</span><span class="sxs-lookup"><span data-stu-id="113d7-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="113d7-232">Los parámetros para la función de selección son los nombres de las cadenas de las columnas de la tabla que desea devolver.</span><span class="sxs-lookup"><span data-stu-id="113d7-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="113d7-233">El método **select** debe ir después de métodos como **where** y **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="113d7-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="113d7-234">Puede ir seguido de métodos de paginación como **skip** y **top**.</span><span class="sxs-lookup"><span data-stu-id="113d7-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="113d7-235"><a name="paging"></a>Devolución de datos en páginas</span><span class="sxs-lookup"><span data-stu-id="113d7-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="113d7-236">Los datos **SIEMPRE** se devuelven en páginas.</span><span class="sxs-lookup"><span data-stu-id="113d7-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="113d7-237">El servidor establece el número máximo de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="113d7-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="113d7-238">Si el cliente solicita más registros, el servidor devuelve entonces el número máximo de registros.</span><span class="sxs-lookup"><span data-stu-id="113d7-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="113d7-239">De forma predeterminada, el tamaño máximo de página en el servidor es de 50 registros.</span><span class="sxs-lookup"><span data-stu-id="113d7-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="113d7-240">El primer ejemplo muestra cómo seleccionar los cinco primeros elementos de una tabla.</span><span class="sxs-lookup"><span data-stu-id="113d7-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="113d7-241">La consulta devuelve los elementos de una tabla de **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="113d7-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="113d7-242">**mToDoTable** es la referencia a la tabla del back-end que ha creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="113d7-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="113d7-243">Aquí se muestra una consulta que omite los cinco primeros elementos y que, a continuación, devuelve los cinco siguientes:</span><span class="sxs-lookup"><span data-stu-id="113d7-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="113d7-244">Si desea obtener todos los registros en una tabla, implemente código para recorrer en iteración todas las páginas:</span><span class="sxs-lookup"><span data-stu-id="113d7-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

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

<span data-ttu-id="113d7-245">Una solicitud de todos los registros con este método crea dos solicitudes como mínimo al back-end de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="113d7-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="113d7-246">La elección del tamaño de página adecuado es un equilibrio entre el uso de memoria mientras tiene lugar la solicitud, el uso de ancho de banda y el retraso en la recepción completa de los datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="113d7-247">El valor predeterminado (50 registros) es adecuado para todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="113d7-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="113d7-248">Si usa exclusivamente dispositivos de memoria más grande, aumente hasta 500.</span><span class="sxs-lookup"><span data-stu-id="113d7-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="113d7-249">Hemos encontrado que si se aumenta el tamaño de página por encima de 500 registros da lugar a retrasos inaceptables y problemas de memoria graves.</span><span class="sxs-lookup"><span data-stu-id="113d7-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="113d7-250"><a name="chaining"></a>Concatenación de métodos de consulta</span><span class="sxs-lookup"><span data-stu-id="113d7-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="113d7-251">Se pueden concatenar los métodos usados en la consulta de tablas de back-end.</span><span class="sxs-lookup"><span data-stu-id="113d7-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="113d7-252">Gracias al encadenamiento de consultas, se pueden seleccionar columnas específicas de filas filtradas que se ordenan y paginan.</span><span class="sxs-lookup"><span data-stu-id="113d7-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="113d7-253">Puede crear filtros lógicos complejos.</span><span class="sxs-lookup"><span data-stu-id="113d7-253">You can create complex logical filters.</span></span>  <span data-ttu-id="113d7-254">Cada método de consulta devuelve un objeto Query.</span><span class="sxs-lookup"><span data-stu-id="113d7-254">Each query method returns a Query object.</span></span> <span data-ttu-id="113d7-255">Para finalizar las series de métodos y ejecutar la consulta, llame al método **execute** .</span><span class="sxs-lookup"><span data-stu-id="113d7-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="113d7-256">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="113d7-256">For example:</span></span>

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

<span data-ttu-id="113d7-257">Los métodos de consulta encadenadas se deben ordenar de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="113d7-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="113d7-258">Métodos de filtro (**where**)</span><span class="sxs-lookup"><span data-stu-id="113d7-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="113d7-259">Métodos de ordenación (**orderBy**)</span><span class="sxs-lookup"><span data-stu-id="113d7-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="113d7-260">Métodos de selección (**select**)</span><span class="sxs-lookup"><span data-stu-id="113d7-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="113d7-261">Métodos de paginación (**skip** y **top**)</span><span class="sxs-lookup"><span data-stu-id="113d7-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="113d7-262"><a name="binding"></a>Enlace de datos a la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="113d7-262"><a name="binding"></a>Bind data to the user interface</span></span>

<span data-ttu-id="113d7-263">El enlace de datos implica tres componentes:</span><span class="sxs-lookup"><span data-stu-id="113d7-263">Data binding involves three components:</span></span>

* <span data-ttu-id="113d7-264">El origen de datos</span><span class="sxs-lookup"><span data-stu-id="113d7-264">The data source</span></span>
* <span data-ttu-id="113d7-265">El diseño de la pantalla</span><span class="sxs-lookup"><span data-stu-id="113d7-265">The screen layout</span></span>
* <span data-ttu-id="113d7-266">El adaptador que une a ambos</span><span class="sxs-lookup"><span data-stu-id="113d7-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="113d7-267">En nuestro código de muestra, devolvemos los datos de la tabla SQL Azure de Aplicaciones móviles **ToDoItem** en una matriz.</span><span class="sxs-lookup"><span data-stu-id="113d7-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="113d7-268">Esta actividad es uno de los patrones más comunes para las aplicaciones de datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="113d7-269">Las consultas en bases de datos normalmente devuelven una serie de filas que el cliente recibe en una lista o una matriz.</span><span class="sxs-lookup"><span data-stu-id="113d7-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="113d7-270">En este ejemplo, la matriz es el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="113d7-271">El código especifica un diseño de pantalla que define la vista de los datos que aparecerán en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="113d7-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="113d7-272">Los dos están vinculados mediante un adaptador, que en este código es una extensión de la clase **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="113d7-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="113d7-273"><a name="layout"></a>Definición del diseño</span><span class="sxs-lookup"><span data-stu-id="113d7-273"><a name="layout"></a>Define the Layout</span></span>

<span data-ttu-id="113d7-274">El diseño lo definen varios fragmentos de código XML.</span><span class="sxs-lookup"><span data-stu-id="113d7-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="113d7-275">Dado el diseño existente, el código siguiente representa el elemento **ListView** que queremos rellenar con nuestros datos de servidor.</span><span class="sxs-lookup"><span data-stu-id="113d7-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="113d7-276">En el código anterior, el atributo *listitem* especifica el identificador del diseño de una fila concreta de la lista.</span><span class="sxs-lookup"><span data-stu-id="113d7-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="113d7-277">Este código especifica una casilla de verificación y su texto asociado, y crea una instancia de esta para cada elemento de la lista.</span><span class="sxs-lookup"><span data-stu-id="113d7-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="113d7-278">Este diseño no muestra el campo **id** y un diseño más complejo especificaría campos adicionales en la pantalla.</span><span class="sxs-lookup"><span data-stu-id="113d7-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="113d7-279">Este código está en el archivo **row_list_to_do.xml**.</span><span class="sxs-lookup"><span data-stu-id="113d7-279">This code is in the **row_list_to_do.xml** file.</span></span>

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

#### <span data-ttu-id="113d7-280"><a name="adapter"></a>Definición del adaptador</span><span class="sxs-lookup"><span data-stu-id="113d7-280"><a name="adapter"></a>Define the adapter</span></span>
<span data-ttu-id="113d7-281">Como el origen de datos de nuestra vista es una matriz de **ToDoItem**, se realiza una subclase en nuestro adaptador desde una clase **ArrayAdapter&lt;ToDoItem&gt;**.</span><span class="sxs-lookup"><span data-stu-id="113d7-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="113d7-282">Esta subclase producirá una vista para cada **ToDoItem** que use el diseño de **row_list_to_do**.</span><span class="sxs-lookup"><span data-stu-id="113d7-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="113d7-283">En el código, definimos la siguiente clase que es una extensión de la clase **ArrayAdapter&lt;E&gt;**:</span><span class="sxs-lookup"><span data-stu-id="113d7-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="113d7-284">Reemplace el método **getView** de los adaptadores.</span><span class="sxs-lookup"><span data-stu-id="113d7-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="113d7-285">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="113d7-285">For example:</span></span>

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

<span data-ttu-id="113d7-286">Creamos una instancia de esta clase en nuestra actividad de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="113d7-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="113d7-287">El segundo parámetro para el constructor ToDoItemAdapter es una referencia al diseño.</span><span class="sxs-lookup"><span data-stu-id="113d7-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="113d7-288">Ahora podemos crear una instancia del elemento **ListView** y asignar el adaptador a **ListView**.</span><span class="sxs-lookup"><span data-stu-id="113d7-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="113d7-289"><a name="use-adapter"></a>Uso del adaptador para enlazar con la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="113d7-289"><a name="use-adapter"></a>Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="113d7-290">Ahora ya puede usar el enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-290">You are now ready to use data binding.</span></span> <span data-ttu-id="113d7-291">El código siguiente muestra cómo obtener los elementos de la tabla y rellena el adaptador local con los elementos devueltos.</span><span class="sxs-lookup"><span data-stu-id="113d7-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

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

<span data-ttu-id="113d7-292">Llame al adaptador en cualquier momento para modificar la tabla **ToDoItem** .</span><span class="sxs-lookup"><span data-stu-id="113d7-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="113d7-293">Como las modificaciones se realizan de registro en registro, se ocupará de una sola fila en lugar de una serie de ellas.</span><span class="sxs-lookup"><span data-stu-id="113d7-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="113d7-294">Al insertar un elemento, se llama al método **add** del adaptador; al eliminarlo, al método **remove**.</span><span class="sxs-lookup"><span data-stu-id="113d7-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="113d7-295">Puede encontrar un ejemplo completo en el [proyecto de inicio rápido de Android][21].</span><span class="sxs-lookup"><span data-stu-id="113d7-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="113d7-296"><a name="inserting"></a>Inserción de datos en el back-end</span><span class="sxs-lookup"><span data-stu-id="113d7-296"><a name="inserting"></a>Insert data into the backend</span></span>

<span data-ttu-id="113d7-297">Cree instancias de la clase *ToDoItem* y configure sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="113d7-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="113d7-298">Después, utilice **insert()** insertar un objeto:</span><span class="sxs-lookup"><span data-stu-id="113d7-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="113d7-299">La entidad devuelta coincide con los datos insertados en la tabla de back-end, incluido el identificador y los otros valores establecidos en el back-end (como los campos `createdAt`, `updatedAt` y `version`).</span><span class="sxs-lookup"><span data-stu-id="113d7-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="113d7-300">Las tablas de Mobile Apps requieren una columna de clave principal denominada " **id**".</span><span class="sxs-lookup"><span data-stu-id="113d7-300">Mobile Apps tables require a primary key column named **id**.</span></span> <span data-ttu-id="113d7-301">Esta columna debe ser una cadena.</span><span class="sxs-lookup"><span data-stu-id="113d7-301">This column must be a string.</span></span> <span data-ttu-id="113d7-302">El valor predeterminado de la columna de identificador es un GUID.</span><span class="sxs-lookup"><span data-stu-id="113d7-302">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="113d7-303">Puede proporcionar otros valores únicos, como nombres de usuario o direcciones de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="113d7-303">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="113d7-304">Cuando no se proporciona un valor de identificador de cadena para un registro insertado, el back-end genera un nuevo GUID.</span><span class="sxs-lookup"><span data-stu-id="113d7-304">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="113d7-305">Los valores de identificador de cadena proporcionan las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="113d7-305">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="113d7-306">Los identificadores pueden generarse sin realizar un recorrido de ida y vuelta a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-306">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="113d7-307">Los registros son más fáciles de fusionar desde diferentes tablas o bases de datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-307">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="113d7-308">Los valores de los identificadores se integran mejor con una lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="113d7-308">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="113d7-309">Los valores de identificador de cadena son **OBLIGATORIOS** para poder utilizar la sincronización sin conexión.</span><span class="sxs-lookup"><span data-stu-id="113d7-309">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="113d7-310">No se puede cambiar un identificador una vez que se almacena en la base de datos de back-end.</span><span class="sxs-lookup"><span data-stu-id="113d7-310">You cannot change an Id once it is stored in the backend database.</span></span>

## <span data-ttu-id="113d7-311"><a name="updating"></a>Actualización de los datos en una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="113d7-311"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="113d7-312">Para actualizar los datos de una tabla, pase el nuevo objeto al método **update()** .</span><span class="sxs-lookup"><span data-stu-id="113d7-312">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="113d7-313">En este ejemplo, *item* es una referencia a una fila de la tabla *ToDoItem*, en la que se le han realizado algunos cambios.</span><span class="sxs-lookup"><span data-stu-id="113d7-313">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="113d7-314">Se actualiza la fila con el mismo campo **id** .</span><span class="sxs-lookup"><span data-stu-id="113d7-314">The row with the same **id** is updated.</span></span>

## <span data-ttu-id="113d7-315"><a name="deleting"></a>Eliminación de datos en una aplicación móvil</span><span class="sxs-lookup"><span data-stu-id="113d7-315"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="113d7-316">El código siguiente muestra cómo eliminar datos de una tabla especificando el objeto de datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-316">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="113d7-317">También puede eliminar un elemento especificando el campo **id** de la fila que se va a eliminar.</span><span class="sxs-lookup"><span data-stu-id="113d7-317">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="113d7-318"><a name="lookup"></a>Búsqueda de un elemento específico por el identificador</span><span class="sxs-lookup"><span data-stu-id="113d7-318"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="113d7-319">Busque un elemento con un campo **id** concreto con el método **lookUp()**:</span><span class="sxs-lookup"><span data-stu-id="113d7-319">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="113d7-320"><a name="untyped"></a>Trabajo con datos sin tipo</span><span class="sxs-lookup"><span data-stu-id="113d7-320"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="113d7-321">El modelo de programación sin tipo proporciona un control exacto de la serialización de JSON.</span><span class="sxs-lookup"><span data-stu-id="113d7-321">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="113d7-322">Existen algunos escenarios comunes donde recomendamos usar un modelo de programación sin tipo.</span><span class="sxs-lookup"><span data-stu-id="113d7-322">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="113d7-323">Por ejemplo, si la tabla de back-end contiene muchas columnas y solo necesita hacer referencia a un subconjunto de ellas.</span><span class="sxs-lookup"><span data-stu-id="113d7-323">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="113d7-324">El modelo con tipo precisa definir todas las columnas especificadas en el back-end de Mobile Apps de su clase de datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-324">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="113d7-325">La mayoría de las llamadas de API para obtener acceso a los datos son similares a las llamadas de programación con tipo.</span><span class="sxs-lookup"><span data-stu-id="113d7-325">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="113d7-326">La diferencia principal es que en el modelo sin tipo se invocan métodos en el objeto **MobileServiceJsonTable**, en lugar del objeto **MobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="113d7-326">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <span data-ttu-id="113d7-327"><a name="json_instance"></a>Creación de una instancia de tabla sin tipo</span><span class="sxs-lookup"><span data-stu-id="113d7-327"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="113d7-328">Como en el modelo con tipo, se empieza obteniendo una referencia de tabla, aunque en este caso se trate de un objeto **MobileServicesJsonTable** .</span><span class="sxs-lookup"><span data-stu-id="113d7-328">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="113d7-329">Obtenga la referencia llamando al método **getTable** en una instancia del cliente:</span><span class="sxs-lookup"><span data-stu-id="113d7-329">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="113d7-330">Cuando haya creado una instancia de **MobileServiceJsonTable**, tendrá disponible prácticamente la misma API que con el modelo de programación con tipo.</span><span class="sxs-lookup"><span data-stu-id="113d7-330">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="113d7-331">En algunos casos, los métodos toman un parámetro sin tipo en lugar de uno con tipo.</span><span class="sxs-lookup"><span data-stu-id="113d7-331">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="113d7-332"><a name="json_insert"></a>Inserción de una tabla sin tipo</span><span class="sxs-lookup"><span data-stu-id="113d7-332"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="113d7-333">El código siguiente muestra cómo realizar una inserción.</span><span class="sxs-lookup"><span data-stu-id="113d7-333">The following code shows how to do an insert.</span></span> <span data-ttu-id="113d7-334">El primer paso es crear un [JsonObject][1], que forma parte de la biblioteca de [gson][3].</span><span class="sxs-lookup"><span data-stu-id="113d7-334">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="113d7-335">Después, utilice **insert()** para insertar el objeto sin tipo en la tabla.</span><span class="sxs-lookup"><span data-stu-id="113d7-335">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="113d7-336">Si necesita obtener el identificador del objeto insertado, use el método **getAsJsonPrimitive()** .</span><span class="sxs-lookup"><span data-stu-id="113d7-336">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="113d7-337"><a name="json_delete"></a>Eliminación de una tabla sin tipo</span><span class="sxs-lookup"><span data-stu-id="113d7-337"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="113d7-338">El código siguiente muestra cómo eliminar una instancia, en este caso, la misma instancia de un **JsonObject** que se creó en el ejemplo de *insert* anterior.</span><span class="sxs-lookup"><span data-stu-id="113d7-338">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="113d7-339">El código es el mismo que con el caso con tipo, pero el método tiene una firma diferente, ya que hace referencia a un elemento **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="113d7-339">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="113d7-340">También puede eliminar una instancia directamente usando su identificador:</span><span class="sxs-lookup"><span data-stu-id="113d7-340">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="113d7-341"><a name="json_get"></a>Devolución de todas las filas de una tabla sin tipo</span><span class="sxs-lookup"><span data-stu-id="113d7-341"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="113d7-342">El código siguiente muestra cómo recuperar una tabla completa.</span><span class="sxs-lookup"><span data-stu-id="113d7-342">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="113d7-343">Puesto que está utilizando una tabla de JSON, solamente puede recuperar de manera selectiva algunas de las columnas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="113d7-343">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

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

<span data-ttu-id="113d7-344">En el modelo con tipo se encuentra disponible el mismo conjunto de métodos de filtrado y paginación que con el modelo sin tipo.</span><span class="sxs-lookup"><span data-stu-id="113d7-344">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <span data-ttu-id="113d7-345"><a name="offline-sync"></a>Implementación de la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="113d7-345"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="113d7-346">El SDK de cliente de Azure Mobile Apps también implementa la sincronización de datos sin conexión mediante una base de datos SQLite que almacena una copia de los datos de servidor de manera local.</span><span class="sxs-lookup"><span data-stu-id="113d7-346">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="113d7-347">Las operaciones realizadas en una tabla sin conexión no necesitan conectividad móvil para funcionar.</span><span class="sxs-lookup"><span data-stu-id="113d7-347">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="113d7-348">La sincronización sin conexión favorece la resistencia y el rendimiento; a cambio, la resolución de conflictos conlleva una lógica más compleja.</span><span class="sxs-lookup"><span data-stu-id="113d7-348">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="113d7-349">El SDK de cliente de Azure Mobile Apps implementa las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="113d7-349">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="113d7-350">Sincronización incremental: solo se descargan registros nuevos y actualizados, lo que ahorra ancho de banda y consumo de memoria.</span><span class="sxs-lookup"><span data-stu-id="113d7-350">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="113d7-351">Simultaneidad optimista: se supone que las operaciones se realizan correctamente.</span><span class="sxs-lookup"><span data-stu-id="113d7-351">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="113d7-352">La resolución de conflictos se aplaza hasta que se realizan actualizaciones en el servidor.</span><span class="sxs-lookup"><span data-stu-id="113d7-352">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="113d7-353">Resolución de conflictos: el SDK detecta cuándo se ha realizado un cambio conflictivo en el servidor y proporciona enlaces para avisar al usuario.</span><span class="sxs-lookup"><span data-stu-id="113d7-353">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="113d7-354">Eliminación temporal: los registros eliminados se marcan como eliminados, lo que permite que otros dispositivos actualicen su caché sin conexión.</span><span class="sxs-lookup"><span data-stu-id="113d7-354">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="113d7-355">Inicialización de la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="113d7-355">Initialize Offline Sync</span></span>

<span data-ttu-id="113d7-356">Cada tabla sin conexión se debe definir en la caché sin conexión antes de su uso.</span><span class="sxs-lookup"><span data-stu-id="113d7-356">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="113d7-357">Normalmente, la definición de la tabla se realiza inmediatamente después de la creación del cliente:</span><span class="sxs-lookup"><span data-stu-id="113d7-357">Normally, table definition is done immediately after the creation of the client:</span></span>

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

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
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

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="113d7-358">Obtención de una referencia a la tabla de caché sin conexión</span><span class="sxs-lookup"><span data-stu-id="113d7-358">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="113d7-359">Para una tabla en línea, use `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="113d7-359">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="113d7-360">Para una tabla sin conexión, use `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="113d7-360">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="113d7-361">Todos los métodos que están disponibles para tablas en línea (incluido el filtrado, la ordenación, la paginación, la inserción de datos, la actualización de datos y la eliminación de datos) funcionan igual de bien en tablas en línea que en tablas sin conexión.</span><span class="sxs-lookup"><span data-stu-id="113d7-361">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="113d7-362">Sincronización de la caché sin conexión local</span><span class="sxs-lookup"><span data-stu-id="113d7-362">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="113d7-363">La sincronización tiene lugar dentro del control de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="113d7-363">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="113d7-364">A continuación se muestra un método de sincronización de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="113d7-364">Here is an example synchronization method:</span></span>

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

<span data-ttu-id="113d7-365">Si se proporciona un nombre de consulta al método `.pull(query, queryname)`, se usa la sincronización incremental para devolver solo los registros que se han creado o cambiado desde la última extracción realizada correctamente.</span><span class="sxs-lookup"><span data-stu-id="113d7-365">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="113d7-366">Control de los conflictos durante la sincronización sin conexión</span><span class="sxs-lookup"><span data-stu-id="113d7-366">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="113d7-367">Si tiene lugar un conflicto durante una operación `.push()`, se produce una excepción `MobileServiceConflictException`.</span><span class="sxs-lookup"><span data-stu-id="113d7-367">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="113d7-368">El elemento emitido por el servidor se inserta en la excepción y se puede recuperar mediante `.getItem()` en la excepción.</span><span class="sxs-lookup"><span data-stu-id="113d7-368">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="113d7-369">Para ajustar la inserción, llame a los siguientes elementos del objeto MobileServiceSyncContext:</span><span class="sxs-lookup"><span data-stu-id="113d7-369">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="113d7-370">Cuando todos los conflictos estén marcados como desea, llame de nuevo a `.push()` para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="113d7-370">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <span data-ttu-id="113d7-371"><a name="custom-api"></a>Llamada a una API personalizada</span><span class="sxs-lookup"><span data-stu-id="113d7-371"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="113d7-372">Una API personalizada le permite definir extremos personalizados que exponen la funcionalidad del servidor que no se asigna a una operación de inserción, actualización, eliminación o lectura.</span><span class="sxs-lookup"><span data-stu-id="113d7-372">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="113d7-373">Al usar una API personalizada, puede tener más control sobre la mensajería, incluida la lectura y el establecimiento de encabezados de mensajes HTTP y la definición del formato del cuerpo de un mensaje diferente de JSON.</span><span class="sxs-lookup"><span data-stu-id="113d7-373">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="113d7-374">Desde un cliente Android, llame al método **invokeApi** para llamar al punto de conexión de API personalizado.</span><span class="sxs-lookup"><span data-stu-id="113d7-374">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="113d7-375">En el ejemplo siguiente se muestra cómo llamar a un punto de conexión de API denominado **completeAll**, que devuelve una clase de colección denominada **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="113d7-375">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

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

<span data-ttu-id="113d7-376">El método **invokeApi** se llama en el cliente, el cual envía una solicitud de POST a la nueva API personalizada.</span><span class="sxs-lookup"><span data-stu-id="113d7-376">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="113d7-377">El resultado devuelto por la API personalizada se muestra en un cuadro de diálogo de mensaje, al igual que todos los errores.</span><span class="sxs-lookup"><span data-stu-id="113d7-377">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="113d7-378">Otras versiones de **invokeApi** le permiten enviar opcionalmente un objeto en el cuerpo de solicitud, especificar el método HTTP y enviar parámetros de consulta con la solicitud.</span><span class="sxs-lookup"><span data-stu-id="113d7-378">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="113d7-379">También se proporcionan versiones sin tipo de **invokeApi** .</span><span class="sxs-lookup"><span data-stu-id="113d7-379">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="113d7-380"><a name="authentication"></a>Adición de autenticación a la aplicación</span><span class="sxs-lookup"><span data-stu-id="113d7-380"><a name="authentication"></a>Add authentication to your app</span></span>

<span data-ttu-id="113d7-381">Los tutoriales ya describen detalladamente cómo agregar estas características.</span><span class="sxs-lookup"><span data-stu-id="113d7-381">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="113d7-382">App Service admite la [autenticación de los usuarios de aplicaciones](app-service-mobile-android-get-started-users.md) mediante diversos proveedores de identidades externos: Facebook, Google, cuenta de Microsoft, Twitter y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="113d7-382">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="113d7-383">Puede establecer permisos en tablas para restringir el acceso a operaciones específicas solo a usuarios autenticados.</span><span class="sxs-lookup"><span data-stu-id="113d7-383">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="113d7-384">También puede usar la identidad de usuarios autenticados para implementar reglas de autorización en el back-end.</span><span class="sxs-lookup"><span data-stu-id="113d7-384">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="113d7-385">Se admiten dos flujos de autenticación: un flujo de **servidor** y un flujo de **cliente**.</span><span class="sxs-lookup"><span data-stu-id="113d7-385">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="113d7-386">El flujo de servidor ofrece la experiencia de autenticación más simple, ya que se basa en la interfaz de autenticación web de los proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="113d7-386">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="113d7-387">No se requieren más SDK para implementar la autenticación de flujo de servidor.</span><span class="sxs-lookup"><span data-stu-id="113d7-387">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="113d7-388">Este tipo de autenticación no proporciona una integración perfecta con el dispositivo móvil y solo se recomienda en escenarios de pruebas de concepto.</span><span class="sxs-lookup"><span data-stu-id="113d7-388">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="113d7-389">El flujo de cliente posibilita una mayor integración con funcionalidades específicas de dispositivos, como el inicio de sesión único, ya que se basa en SDK que proporciona el proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="113d7-389">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="113d7-390">Por ejemplo, puede integrar el SDK de Facebook en la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="113d7-390">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="113d7-391">El cliente móvil se coloca en la aplicación de Facebook y confirma el inicio de sesión antes de pasar a la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="113d7-391">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="113d7-392">Hay que realizar cuatro pasos para habilitar la autenticación en su aplicación:</span><span class="sxs-lookup"><span data-stu-id="113d7-392">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="113d7-393">Registre la aplicación para llevar a cabo la autenticación con un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="113d7-393">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="113d7-394">Configure el back-end de App Service.</span><span class="sxs-lookup"><span data-stu-id="113d7-394">Configure your App Service backend.</span></span>
* <span data-ttu-id="113d7-395">Restrinja los permisos de tabla a solo los usuarios autenticados en el back-end de App Service.</span><span class="sxs-lookup"><span data-stu-id="113d7-395">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="113d7-396">Agregar código de autenticación a su aplicación.</span><span class="sxs-lookup"><span data-stu-id="113d7-396">Add authentication code to your app.</span></span>

<span data-ttu-id="113d7-397">Puede establecer permisos en tablas para restringir el acceso a operaciones específicas solo a usuarios autenticados.</span><span class="sxs-lookup"><span data-stu-id="113d7-397">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="113d7-398">También puede usar el SID de un usuario autenticado para modificar las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="113d7-398">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="113d7-399">Para obtener más información, consulte [Introducción a la autenticación] y la documentación de los procedimientos del SDK de servidor.</span><span class="sxs-lookup"><span data-stu-id="113d7-399">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="113d7-400"><a name="caching"></a>Autenticación: flujo de servidor</span><span class="sxs-lookup"><span data-stu-id="113d7-400"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="113d7-401">El código siguiente inicia un proceso de inicio de sesión del flujo de servidor mediante el proveedor de Google:</span><span class="sxs-lookup"><span data-stu-id="113d7-401">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="113d7-402">Hace falta configuración adicional debido a los requisitos de seguridad del proveedor de Google:</span><span class="sxs-lookup"><span data-stu-id="113d7-402">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="113d7-403">Además, agregue el siguiente método a la clase principal Activity:</span><span class="sxs-lookup"><span data-stu-id="113d7-403">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="113d7-404">El valor de `GOOGLE_LOGIN_REQUEST_CODE` definido en la actividad principal se usa para el método `login()` y dentro del método `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="113d7-404">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="113d7-405">Puede elegir cualquier número único, siempre y cuando el mismo número se use dentro del método `login()` y del método `onActivityResult()`.</span><span class="sxs-lookup"><span data-stu-id="113d7-405">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="113d7-406">Si abstrae el código de cliente en un adaptador de servicio (como se mostró anteriormente), debe llamar a los métodos adecuados en el adaptador de servicio.</span><span class="sxs-lookup"><span data-stu-id="113d7-406">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="113d7-407">También debe configurar el proyecto para customtabs.</span><span class="sxs-lookup"><span data-stu-id="113d7-407">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="113d7-408">En primer lugar, especifique una dirección URL de redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="113d7-408">First specify a redirect-URL.</span></span>  <span data-ttu-id="113d7-409">Agregue el siguiente fragmento de código a `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="113d7-409">Add the following snippet to `AndroidManifest.xml`:</span></span>

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

<span data-ttu-id="113d7-410">Agregue **redirectUriScheme** al archivo `build.gradle` de su aplicación:</span><span class="sxs-lookup"><span data-stu-id="113d7-410">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

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

<span data-ttu-id="113d7-411">Por último, agregue `com.android.support:customtabs:23.0.1` a la lista de dependencias del archivo `build.gradle`:</span><span class="sxs-lookup"><span data-stu-id="113d7-411">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

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

<span data-ttu-id="113d7-412">Obtenga el identificador del usuario que ha iniciado sesión desde una clase **MobileServiceUser** utilizando el método **getUserId**.</span><span class="sxs-lookup"><span data-stu-id="113d7-412">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="113d7-413">Para obtener un ejemplo de cómo usar Futures para llamar a las API de inicio de sesión asincrónico, consulte [Introducción a la autenticación].</span><span class="sxs-lookup"><span data-stu-id="113d7-413">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="113d7-414">El esquema de dirección URL mencionado distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="113d7-414">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="113d7-415">Asegúrese de que todas las apariciones de `{url_scheme_of_you_app}` coincidan en las mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="113d7-415">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="113d7-416"><a name="caching"></a>Almacenamiento en caché de tokens de autenticación</span><span class="sxs-lookup"><span data-stu-id="113d7-416"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="113d7-417">El almacenamiento en caché de los tokens de autenticación requiere el almacenamiento del identificador de usuario y el token de autenticación localmente en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="113d7-417">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="113d7-418">La próxima vez que se inicie la aplicación, compruebe la caché y, si estos valores están presentes, puede omitir el procedimiento de inicio de sesión y rehidratar el cliente con estos datos.</span><span class="sxs-lookup"><span data-stu-id="113d7-418">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="113d7-419">No obstante, estos datos son confidenciales y deben almacenarse cifrados por seguridad en caso de que le roben el teléfono.</span><span class="sxs-lookup"><span data-stu-id="113d7-419">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="113d7-420">Puede ver un ejemplo completo de cómo almacenar tokens de autenticación en la memoria caché en la [sección Almacenamiento de tokens de autenticación en la caché][7].</span><span class="sxs-lookup"><span data-stu-id="113d7-420">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="113d7-421">Si trata de utilizar un token caducado, recibirá como respuesta *401 unauthorized* .</span><span class="sxs-lookup"><span data-stu-id="113d7-421">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="113d7-422">Puede controlar los errores de autenticación usando filtros.</span><span class="sxs-lookup"><span data-stu-id="113d7-422">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="113d7-423">Los filtros interceptan las solicitudes al back-end de App Service.</span><span class="sxs-lookup"><span data-stu-id="113d7-423">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="113d7-424">El código de filtro probará la respuesta a un error 401, desencadenará el proceso de inicio de sesión y, luego, reanudará la solicitud que generó el 401.</span><span class="sxs-lookup"><span data-stu-id="113d7-424">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <span data-ttu-id="113d7-425"><a name="refresh"></a>Uso de tokens de actualización</span><span class="sxs-lookup"><span data-stu-id="113d7-425"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="113d7-426">El token devuelto por la característica Autenticación y autorización de Azure App Service tiene una duración definida de una hora.</span><span class="sxs-lookup"><span data-stu-id="113d7-426">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="113d7-427">Después de este período, es necesario volver a autenticar al usuario.</span><span class="sxs-lookup"><span data-stu-id="113d7-427">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="113d7-428">Si usa un token de larga duración que haya recibido mediante la autenticación de flujo de cliente, entonces puede volver a autenticar con Autenticación y autorización de Azure App Service usando el mismo token.</span><span class="sxs-lookup"><span data-stu-id="113d7-428">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="113d7-429">Se genera otro token de Azure App Service con una nueva duración.</span><span class="sxs-lookup"><span data-stu-id="113d7-429">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="113d7-430">También puede registrar el proveedor para que use tokens de actualización.</span><span class="sxs-lookup"><span data-stu-id="113d7-430">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="113d7-431">Un token de actualización no está siempre disponible.</span><span class="sxs-lookup"><span data-stu-id="113d7-431">A Refresh Token is not always available.</span></span>  <span data-ttu-id="113d7-432">Se requiere configuración adicional:</span><span class="sxs-lookup"><span data-stu-id="113d7-432">Additional configuration is required:</span></span>

* <span data-ttu-id="113d7-433">Para **Azure Active Directory**, configure un secreto de cliente para la aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="113d7-433">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="113d7-434">Especifique el secreto del cliente en Azure App Service al configurar la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="113d7-434">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="113d7-435">Al llamar a `.login()`, pase `response_type=code id_token` como parámetro:</span><span class="sxs-lookup"><span data-stu-id="113d7-435">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="113d7-436">Para **Google**, pase `access_type=offline` como parámetro:</span><span class="sxs-lookup"><span data-stu-id="113d7-436">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="113d7-437">Para **Cuenta de Microsoft**, seleccione el ámbito `wl.offline_access`.</span><span class="sxs-lookup"><span data-stu-id="113d7-437">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="113d7-438">Para actualizar un token, llame a `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="113d7-438">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="113d7-439">Como procedimiento recomendado, cree un filtro que detecte una respuesta 401 del servidor y que intente actualizar el token de usuario.</span><span class="sxs-lookup"><span data-stu-id="113d7-439">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="113d7-440">Inicio de sesión con la autenticación de flujo de cliente</span><span class="sxs-lookup"><span data-stu-id="113d7-440">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="113d7-441">El proceso general para iniciar sesión con la autenticación de flujo de cliente es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="113d7-441">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="113d7-442">Configure Autenticación y autorización de Azure App Service como haría con la autenticación de flujo de servidor.</span><span class="sxs-lookup"><span data-stu-id="113d7-442">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="113d7-443">Integre el SDK del proveedor de autenticación para que la autenticación genere un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="113d7-443">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="113d7-444">Llame al método `.login()` de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="113d7-444">Call the `.login()` method as follows:</span></span>

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

<span data-ttu-id="113d7-445">Reemplace el método `onSuccess()` por cualquier código que desee usar en un inicio de sesión correcto.</span><span class="sxs-lookup"><span data-stu-id="113d7-445">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="113d7-446">La cadena `{provider}` es un proveedor válido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount** o **twitter**.</span><span class="sxs-lookup"><span data-stu-id="113d7-446">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="113d7-447">Si ha implementado autenticación personalizada, también puede usar la etiqueta de proveedor de autenticación personalizada.</span><span class="sxs-lookup"><span data-stu-id="113d7-447">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <span data-ttu-id="113d7-448"><a name="adal"></a>Autenticación de usuarios con la biblioteca de autenticación de Active Directory (ADAL)</span><span class="sxs-lookup"><span data-stu-id="113d7-448"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="113d7-449">Puede utilizar la biblioteca de autenticación de Active Directory (ADAL) para iniciar la sesión de los usuarios en su aplicación con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="113d7-449">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="113d7-450">La opción del inicio de sesión de flujo de cliente es, con frecuencia, preferible al uso de los métodos `loginAsync()` , ya que proporciona una experiencia UX más nativa y permite realizar más personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="113d7-450">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="113d7-451">Configure su back-end de aplicación móvil para el inicio de sesión en AAD siguiendo el tutorial [Configuración de la aplicación de App Service para usar el inicio de sesión de Azure Active Directory][22].</span><span class="sxs-lookup"><span data-stu-id="113d7-451">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="113d7-452">Asegúrese de completar el paso opcional de registrar una aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="113d7-452">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="113d7-453">Instale ADAL modificando el archivo build.gradle para incluir las siguientes definiciones:</span><span class="sxs-lookup"><span data-stu-id="113d7-453">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

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

1. <span data-ttu-id="113d7-454">Agregue el siguiente código a la aplicación y realice las siguientes sustituciones:</span><span class="sxs-lookup"><span data-stu-id="113d7-454">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="113d7-455">Reemplace **INSERT-AUTHORITY-HERE** por el nombre del inquilino en el que aprovisionó la aplicación.</span><span class="sxs-lookup"><span data-stu-id="113d7-455">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="113d7-456">El formato debería ser https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="113d7-456">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="113d7-457">Reemplace **INSERT-RESOURCE-ID-HERE** por el Id. de cliente del back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="113d7-457">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="113d7-458">El Id. de cliente en la pestaña **Opciones avanzadas** de **Configuración de Azure Active Directory** en el portal.</span><span class="sxs-lookup"><span data-stu-id="113d7-458">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="113d7-459">Reemplace **INSERT-CLIENT-ID-HERE** por el Id. de cliente que copió de la aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="113d7-459">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="113d7-460">Reemplace **INSERT-REDIRECT-URI-HERE** por el punto de conexión */.auth/login/done* del sitio, mediante el esquema HTTPS.</span><span class="sxs-lookup"><span data-stu-id="113d7-460">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="113d7-461">Este valor debe ser similar a *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="113d7-461">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

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

## <span data-ttu-id="113d7-462"><a name="filters"></a>Ajuste de la comunicación cliente-servidor</span><span class="sxs-lookup"><span data-stu-id="113d7-462"><a name="filters"></a>Adjust the Client-Server Communication</span></span>

<span data-ttu-id="113d7-463">La conexión de cliente es normalmente una conexión HTTP básica que usa la biblioteca HTTP subyacente que se suministra con el SDK de Android.</span><span class="sxs-lookup"><span data-stu-id="113d7-463">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="113d7-464">Hay varios motivos por los que desearía cambiar esta conexión:</span><span class="sxs-lookup"><span data-stu-id="113d7-464">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="113d7-465">Desea usar una biblioteca HTTP alternativa para ajustar los tiempos de espera.</span><span class="sxs-lookup"><span data-stu-id="113d7-465">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="113d7-466">Desea proporcionar una barra de progreso.</span><span class="sxs-lookup"><span data-stu-id="113d7-466">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="113d7-467">Desea agregar un encabezado personalizado para admitir la funcionalidad de administración de API.</span><span class="sxs-lookup"><span data-stu-id="113d7-467">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="113d7-468">Desea interceptar una respuesta errónea para que pueda implementar la reautenticación.</span><span class="sxs-lookup"><span data-stu-id="113d7-468">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="113d7-469">Desea registrar las solicitudes de back-end a un servicio de análisis.</span><span class="sxs-lookup"><span data-stu-id="113d7-469">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="113d7-470">Uso de una biblioteca HTTP alternativa</span><span class="sxs-lookup"><span data-stu-id="113d7-470">Using an alternate HTTP Library</span></span>

<span data-ttu-id="113d7-471">Llame al método `.setAndroidHttpClientFactory()` inmediatamente después de crear la referencia de cliente.</span><span class="sxs-lookup"><span data-stu-id="113d7-471">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="113d7-472">Por ejemplo, para establecer el tiempo de espera de conexión en 60 segundos (en lugar del valor predeterminado de 10 segundos):</span><span class="sxs-lookup"><span data-stu-id="113d7-472">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

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

### <a name="implement-a-progress-filter"></a><span data-ttu-id="113d7-473">Implementación de un filtro de progreso</span><span class="sxs-lookup"><span data-stu-id="113d7-473">Implement a Progress Filter</span></span>

<span data-ttu-id="113d7-474">Puede implementar una intersección de todas las solicitudes mediante la implementación de `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="113d7-474">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="113d7-475">Por ejemplo, a continuación se actualiza una barra de progreso creada previamente:</span><span class="sxs-lookup"><span data-stu-id="113d7-475">For example, the following updates a pre-created progress bar:</span></span>

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

<span data-ttu-id="113d7-476">Puede adjuntar este filtro al cliente de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="113d7-476">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="113d7-477">Personalización de los encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="113d7-477">Customize Request Headers</span></span>

<span data-ttu-id="113d7-478">Use el elemento siguiente `ServiceFilter` y adjunte el filtro de la misma manera que `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="113d7-478">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

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

### <span data-ttu-id="113d7-479"><a name="conversions"></a>Configuración de serialización automática</span><span class="sxs-lookup"><span data-stu-id="113d7-479"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="113d7-480">Puede especificar una estrategia de conversión que se aplique a todas las columnas utilizando la API de [gson][3].</span><span class="sxs-lookup"><span data-stu-id="113d7-480">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="113d7-481">La biblioteca de cliente Android utiliza la biblioteca [gson][3] en segundo plano para serializar los objetos de Java en datos JSON, que se envían a Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="113d7-481">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="113d7-482">El siguiente código utiliza el método **setFieldNamingStrategy()** para establecer la estrategia.</span><span class="sxs-lookup"><span data-stu-id="113d7-482">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="113d7-483">Este ejemplo eliminará el carácter inicial (una "m") y, después, pondrá el siguiente carácter en minúscula (en cada nombre de campo).</span><span class="sxs-lookup"><span data-stu-id="113d7-483">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="113d7-484">Por ejemplo, convertiría "mld" en "id".</span><span class="sxs-lookup"><span data-stu-id="113d7-484">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="113d7-485">Implemente una estrategia de conversión para reducir la necesidad de anotaciones `SerializedName()` en la mayoría de los campos.</span><span class="sxs-lookup"><span data-stu-id="113d7-485">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

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

<span data-ttu-id="113d7-486">Este código debe ejecutarse antes de crear una referencia de cliente móvil mediante **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="113d7-486">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
<span data-ttu-id="113d7-487">[Introducción a la autenticación]: app-service-mobile-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="113d7-487">[Get started with authentication]: app-service-mobile-android-get-started-users.md</span></span>
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
