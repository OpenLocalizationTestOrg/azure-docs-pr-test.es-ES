---
title: "Procedimientos de actualización del SDK de Windows Phone Silverlight"
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
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="6f718-103">Procedimientos de actualización del SDK de Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="6f718-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="6f718-104">Si ya integró una versión anterior de nuestro SDK en la aplicación, debería tener en cuenta los siguientes puntos a la hora de actualizar el SDK.</span><span class="sxs-lookup"><span data-stu-id="6f718-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="6f718-105">Es posible que tenga que seguir varios procedimientos si se perdió varias versiones del SDK.</span><span class="sxs-lookup"><span data-stu-id="6f718-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="6f718-106">Por ejemplo, si migra desde 0.10.1 a 0.11.0, primero debe seguir el procedimiento "de 0.9.0 a 0.10.1" y luego el procedimiento "de 0.10.1 a 0.11.0".</span><span class="sxs-lookup"><span data-stu-id="6f718-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="6f718-107">De 2.0.0 a 3.3.0</span><span class="sxs-lookup"><span data-stu-id="6f718-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="6f718-108">Registros de prueba</span><span class="sxs-lookup"><span data-stu-id="6f718-108">Test logs</span></span>
<span data-ttu-id="6f718-109">Los registros de consola generados por el SDK ahora se pueden habilitar, deshabilitar o filtrar.</span><span class="sxs-lookup"><span data-stu-id="6f718-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="6f718-110">Para personalizar esto, actualice la propiedad `EngagementAgent.Instance.TestLogEnabled` a uno de los valores disponibles en la enumeración `EngagementTestLogLevel`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6f718-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="6f718-111">De 1.1.1 a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="6f718-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="6f718-112">A continuación se describe cómo migrar una integración del SDK desde el servicio Capptain que ofrece Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6f718-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6f718-113">Capptain y Mobile Engagement no son los mismos servicios, y el procedimiento que se indica a continuación destaca únicamente cómo migrar la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="6f718-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="6f718-114">La migración del SDK en la aplicación NO migrará los datos desde los servidores Capptain a los servidores Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6f718-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="6f718-115">Si va a migrar desde una versión anterior, consulte el sitio web de Capptain para migrar a 1.1.1 en primer lugar luego aplique el siguiente procedimiento.</span><span class="sxs-lookup"><span data-stu-id="6f718-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="6f718-116">Paquete de NuGet</span><span class="sxs-lookup"><span data-stu-id="6f718-116">Nuget package</span></span>
<span data-ttu-id="6f718-117">Reemplace **Capptain.WindowsPhone** por el paquete Nuget **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="6f718-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="6f718-118">Aplicar Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6f718-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="6f718-119">El SDK usa el término `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="6f718-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="6f718-120">Debe actualizar el proyecto para que coincida con este cambio.</span><span class="sxs-lookup"><span data-stu-id="6f718-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="6f718-121">Debe desinstalar el paquete NuGet de Capptain actual.</span><span class="sxs-lookup"><span data-stu-id="6f718-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="6f718-122">Tenga en cuenta que se van a quitar todos los cambios de la carpeta recursos de Capptain.</span><span class="sxs-lookup"><span data-stu-id="6f718-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="6f718-123">Si desea conservar los archivos, haga una copia de ellos.</span><span class="sxs-lookup"><span data-stu-id="6f718-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="6f718-124">Después, instale el nuevo paquete NuGet de Microsoft Azure Mobile Engagement en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="6f718-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="6f718-125">Puede encontrarlo directamente en [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="6f718-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="6f718-126">Esta acción reemplaza todos los archivos de recursos que Engagement usa y agrega el nuevo archivo DLL de Engagement a las referencias del proyecto.</span><span class="sxs-lookup"><span data-stu-id="6f718-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="6f718-127">Tendrá que limpiar las referencias del proyecto al eliminar de referencias del archivo DLL de Capptain.</span><span class="sxs-lookup"><span data-stu-id="6f718-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="6f718-128">Si no lo hace, la versión de Capptain entrará en conflicto y se producirán errores.</span><span class="sxs-lookup"><span data-stu-id="6f718-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="6f718-129">Si tiene recursos Capptain personalizados, copie el contenido de los archivos antiguos y péguelos en los nuevos archivos de Engagement.</span><span class="sxs-lookup"><span data-stu-id="6f718-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="6f718-130">Tenga en cuenta que se deben actualizar tanto los archivos xaml como los archivos cs.</span><span class="sxs-lookup"><span data-stu-id="6f718-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="6f718-131">Una vez completados estos pasos, solo tendrá que reemplazar las referencias de Capptain antiguas por las nuevas referencias de Engagement.</span><span class="sxs-lookup"><span data-stu-id="6f718-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="6f718-132">Se deben actualizar todos los espacios de nombres de Capptain.</span><span class="sxs-lookup"><span data-stu-id="6f718-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="6f718-133">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="6f718-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="6f718-134">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="6f718-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="6f718-135">Todas las clases de Capptain que contengan "Capptain" deberían contener "Engagement".</span><span class="sxs-lookup"><span data-stu-id="6f718-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="6f718-136">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="6f718-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="6f718-137">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="6f718-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="6f718-138">En el caso de los archivos xaml, también cambian el espacio de nombres y los atributos de Capptain.</span><span class="sxs-lookup"><span data-stu-id="6f718-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="6f718-139">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="6f718-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="6f718-140">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="6f718-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="6f718-141">En el caso de otros recursos, como imágenes Capptain, tenga en cuenta que su nombre también habrá cambiado para usar "Engagement".</span><span class="sxs-lookup"><span data-stu-id="6f718-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="6f718-142">Identificador de aplicación o clave SDK</span><span class="sxs-lookup"><span data-stu-id="6f718-142">Application ID / SDK Key</span></span>
<span data-ttu-id="6f718-143">Engagement usa una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="6f718-143">Engagement uses a connection string.</span></span> <span data-ttu-id="6f718-144">No es necesario especificar un identificador de aplicación y una clave SDK con Mobile Engagement, solo tiene que especificar una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="6f718-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="6f718-145">Esta se puede configurar en el archivo EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="6f718-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="6f718-146">La configuración de Engagement se puede establecer en el archivo `Resources\EngagementConfiguration.xml` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="6f718-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="6f718-147">Edite este archivo para especificar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6f718-147">Edit this file to specify:</span></span>

* <span data-ttu-id="6f718-148">La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="6f718-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="6f718-149">Si desea especificarla en tiempo de ejecución, puede llamar al método siguiente antes de la inicialización del agente de Engagement:</span><span class="sxs-lookup"><span data-stu-id="6f718-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="6f718-150">La cadena de conexión de la aplicación se muestra en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="6f718-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="6f718-151">Cambio de nombre de elementos</span><span class="sxs-lookup"><span data-stu-id="6f718-151">Items name change</span></span>
<span data-ttu-id="6f718-152">Todos los elementos con el nombre *capptain* han cambiado a *engagement*.</span><span class="sxs-lookup"><span data-stu-id="6f718-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="6f718-153">De forma similar, *Capptain* cambió a *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="6f718-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="6f718-154">Ejemplos de elementos Capptain que se usan habitualmente:</span><span class="sxs-lookup"><span data-stu-id="6f718-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="6f718-155">CapptainConfiguration ahora se llama EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="6f718-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="6f718-156">CapptainAgent ahora se llama EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="6f718-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="6f718-157">CapptainReach ahora se llama EngagementReach</span><span class="sxs-lookup"><span data-stu-id="6f718-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="6f718-158">CapptainHttpConfig ahora se llama EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="6f718-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="6f718-159">GetCapptainPageName ahora se llama GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="6f718-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="6f718-160">Tenga en cuenta que el cambio de nombre también afecta a los métodos invalidados.</span><span class="sxs-lookup"><span data-stu-id="6f718-160">Note that rename also affects overridden methods.</span></span>

