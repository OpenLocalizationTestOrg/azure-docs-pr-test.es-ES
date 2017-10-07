---
title: "Procedimientos de actualización de Phone Silverlight SDK aaaWindows"
description: "Procedimientos de actualización de SDK de Windows Phone Silverlight para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="12576-103">Procedimientos de actualización del SDK de Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="12576-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="12576-104">Si ya ha integrado una versión anterior de nuestro SDK en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="12576-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="12576-105">Puede tener toofollow varios procedimientos si ejecutado varias versiones de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="12576-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="12576-106">Por ejemplo, si migra desde 0.10.1 too0.11.0 tiene toofirst siga Hola "de 0.9.0 too0.10.1" procedimiento, a continuación, Hola "de 0.10.1 too0.11.0" procedimiento.</span><span class="sxs-lookup"><span data-stu-id="12576-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="12576-107">Desde 2.0.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="12576-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="12576-108">Registros de prueba</span><span class="sxs-lookup"><span data-stu-id="12576-108">Test logs</span></span>
<span data-ttu-id="12576-109">Registros de la consola producidos por hello SDK ahora pueden habilitada, deshabilitada o filtrado.</span><span class="sxs-lookup"><span data-stu-id="12576-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="12576-110">toocustomize, propiedad de hello actualización `EngagementAgent.Instance.TestLogEnabled` tooone del valor de hello disponible de hello `EngagementTestLogLevel` enumeración, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12576-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="12576-111">Desde 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="12576-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="12576-112">Hello siguiente describe cómo toomigrate una integración con el SDK de hello Capptain servicio ofrecido por Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="12576-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="12576-113">Capptain e interacción móvil no se Hola los mismos servicios y procedimiento Hola indicado a continuación sólo resalta cómo toomigrate Hola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="12576-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="12576-114">Migrar Hola SDK en la aplicación hello no migrará los datos de hello Capptain toohello Mobile Engagement servidores</span><span class="sxs-lookup"><span data-stu-id="12576-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="12576-115">Si va a migrar desde una versión anterior, por favor, consulte hello Capptain sitio web toomigrate too1.1.1 en primer lugar, aplique Hola procedimiento</span><span class="sxs-lookup"><span data-stu-id="12576-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="12576-116">Paquete de NuGet</span><span class="sxs-lookup"><span data-stu-id="12576-116">Nuget package</span></span>
<span data-ttu-id="12576-117">Reemplace **Capptain.WindowsPhone** por el paquete Nuget **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="12576-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="12576-118">Aplicar Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="12576-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="12576-119">Hola SDK utiliza el término de hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="12576-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="12576-120">Necesita tooupdate su toomatch proyecto este cambio.</span><span class="sxs-lookup"><span data-stu-id="12576-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="12576-121">Debe toouninstall el paquete de nuget Capptain actual.</span><span class="sxs-lookup"><span data-stu-id="12576-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="12576-122">Tenga en cuenta que se van a quitar todos los cambios de la carpeta recursos de Capptain.</span><span class="sxs-lookup"><span data-stu-id="12576-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="12576-123">Si desea que tookeep esos archivos, a continuación, haga una copia de ellos.</span><span class="sxs-lookup"><span data-stu-id="12576-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="12576-124">Después de eso, instale el nuevo paquete de nuget de Microsoft Azure Engagement hello en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="12576-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="12576-125">Puede encontrarlo directamente en [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="12576-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="12576-126">Este reemplaza acción todos los archivos de recursos utilizados por la interacción y agrega Hola nueva contratación DLL tooyour referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="12576-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="12576-127">Eliminando las referencias de Capptain DLL tienen tooclean las referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="12576-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="12576-128">Si no hace esto, versión de Hola de Capptain entrarán en conflicto y se producirán errores.</span><span class="sxs-lookup"><span data-stu-id="12576-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="12576-129">Si ha personalizado los recursos de Capptain, copie el contenido de los archivos antiguos y péguelos en los nuevos archivos de contratación Hola.</span><span class="sxs-lookup"><span data-stu-id="12576-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="12576-130">Tenga en cuenta que los archivos xaml y cs tienen toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="12576-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="12576-131">Una vez completados estos pasos solo tiene tooreplace Capptain las referencias anteriores a por nuevas referencias de contratación Hola.</span><span class="sxs-lookup"><span data-stu-id="12576-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="12576-132">Todos los espacios de nombres de Capptain tienen toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="12576-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="12576-133">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="12576-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="12576-134">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="12576-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="12576-135">Todas las clases de Capptain que contengan "Capptain" deberían contener "Engagement".</span><span class="sxs-lookup"><span data-stu-id="12576-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="12576-136">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="12576-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="12576-137">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="12576-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="12576-138">En el caso de los archivos xaml, también cambian el espacio de nombres y los atributos de Capptain.</span><span class="sxs-lookup"><span data-stu-id="12576-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="12576-139">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="12576-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="12576-140">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="12576-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="12576-141">Para hello otros recursos como imágenes de Capptain, tenga en cuenta que también han tenido toouse cuyo nombre ha cambiado "Interacción".</span><span class="sxs-lookup"><span data-stu-id="12576-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="12576-142">Identificador de aplicación o clave SDK</span><span class="sxs-lookup"><span data-stu-id="12576-142">Application ID / SDK Key</span></span>
<span data-ttu-id="12576-143">Engagement usa una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="12576-143">Engagement uses a connection string.</span></span> <span data-ttu-id="12576-144">Toospecify no tiene un identificador de la aplicación y una clave SDK con Mobile Engagement, solo tendrá toospecify una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="12576-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="12576-145">Esta se puede configurar en el archivo EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="12576-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="12576-146">configuración de la interacción de Hola se puede establecer el `Resources\EngagementConfiguration.xml` archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="12576-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="12576-147">Editar este archivo toospecify:</span><span class="sxs-lookup"><span data-stu-id="12576-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="12576-148">La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="12576-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="12576-149">Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="12576-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="12576-150">cadena de conexión de Hello para la aplicación se muestra en hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="12576-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="12576-151">Cambio de nombre de elementos</span><span class="sxs-lookup"><span data-stu-id="12576-151">Items name change</span></span>
<span data-ttu-id="12576-152">Todos los elementos con el nombre *capptain* han cambiado a *engagement*.</span><span class="sxs-lookup"><span data-stu-id="12576-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="12576-153">De forma similar para *Capptain* demasiado*interacción*.</span><span class="sxs-lookup"><span data-stu-id="12576-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="12576-154">Ejemplos de elementos Capptain que se usan habitualmente:</span><span class="sxs-lookup"><span data-stu-id="12576-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="12576-155">CapptainConfiguration ahora se llama EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="12576-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="12576-156">CapptainAgent ahora se llama EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="12576-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="12576-157">CapptainReach ahora se llama EngagementReach</span><span class="sxs-lookup"><span data-stu-id="12576-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="12576-158">CapptainHttpConfig ahora se llama EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="12576-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="12576-159">GetCapptainPageName ahora se llama GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="12576-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="12576-160">Tenga en cuenta que el cambio de nombre también afecta a los métodos invalidados.</span><span class="sxs-lookup"><span data-stu-id="12576-160">Note that rename also affects overridden methods.</span></span>

