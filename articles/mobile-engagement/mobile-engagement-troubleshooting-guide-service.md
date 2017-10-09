---
title: aaaAzure Mobile Engagement Troubleshooting Guide - servicio
description: "Guías de solución de problemas de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="df835-103">Guía de solución de problemas de servicio</span><span class="sxs-lookup"><span data-stu-id="df835-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="df835-104">los siguientes Hola son posibles problemas que pueden producirse con cómo se ejecuta Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="df835-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="df835-105">Interrupciones del servicio</span><span class="sxs-lookup"><span data-stu-id="df835-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="df835-106">Problema</span><span class="sxs-lookup"><span data-stu-id="df835-106">Issue</span></span>
* <span data-ttu-id="df835-107">Problemas que aparecen toobe causado por interrupciones de servicio de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="df835-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="df835-108">Causas</span><span class="sxs-lookup"><span data-stu-id="df835-108">Causes</span></span>
* <span data-ttu-id="df835-109">Problemas que aparecen toobe causado por interrupciones de servicio de Azure Mobile Engagement pueden deberse a diversos problemas:</span><span class="sxs-lookup"><span data-stu-id="df835-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="df835-110">Problemas aislados que originalmente aparecen tooall sistémica de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="df835-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="df835-111">Problemas conocidos causados por interrupciones de los servidores (no siempre se muestran en el estado del servidor):</span><span class="sxs-lookup"><span data-stu-id="df835-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="df835-112">Programación retrasos, Targeting errores, problemas de actualización de distintivo, stop estadísticas recopilando, deja de inserción funcionar, dejan de funcionar, nuevas aplicaciones o los usuarios de la API no se puede crear, errores de DNS y los errores de tiempo de espera en hello IU, API o aplicaciones en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="df835-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="df835-113">Interrupciones de dependencia en la nube [Estado del servicio de Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="df835-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="df835-114">Interrupciones de dependencia de los servicios de notificación de inserción (PNS)</span><span class="sxs-lookup"><span data-stu-id="df835-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="df835-115">Interrupciones de la tienda de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="df835-115">App Store Outages</span></span>

1) <span data-ttu-id="df835-116">tootest toosee si el problema de hello es sistémico puede probar Hola la misma función de otra</span><span class="sxs-lookup"><span data-stu-id="df835-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="df835-117">Aplicación integrada de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="df835-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="df835-118">Dispositivo de prueba</span><span class="sxs-lookup"><span data-stu-id="df835-118">Test device</span></span>
* <span data-ttu-id="df835-119">Versión del sistema operativo del dispositivo de prueba</span><span class="sxs-lookup"><span data-stu-id="df835-119">Test device OS version</span></span>
* <span data-ttu-id="df835-120">Campaña</span><span class="sxs-lookup"><span data-stu-id="df835-120">Campaign</span></span>
* <span data-ttu-id="df835-121">Cuenta de usuario administrador</span><span class="sxs-lookup"><span data-stu-id="df835-121">Administrator user account</span></span>
* <span data-ttu-id="df835-122">Explorador (Internet Explorer, Firefox, Chrome, etc.)</span><span class="sxs-lookup"><span data-stu-id="df835-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="df835-123">Equipo</span><span class="sxs-lookup"><span data-stu-id="df835-123">Computer</span></span>

2) <span data-ttu-id="df835-124">tootest si Hola solo problema Hola Hola o interfaz de usuario de la API:</span><span class="sxs-lookup"><span data-stu-id="df835-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="df835-125">Probar Hola misma función de ambos Hola interfaz de usuario de Azure Mobile Engagement y Hola la API de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="df835-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="df835-126">tootest si el problema de hello está relacionado con la red de telefonía móvil:</span><span class="sxs-lookup"><span data-stu-id="df835-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="df835-127">Probar al toohello conectado a Internet a través de Wi-Fi y mientras se está conectado a través de la red de telefonía móvil 3G.</span><span class="sxs-lookup"><span data-stu-id="df835-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="df835-128">Confirme que el firewall no bloquee cualquiera de las direcciones IP hello Azure Mobile Engagement o puertos.</span><span class="sxs-lookup"><span data-stu-id="df835-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="df835-129">tootest si el problema de hello está relacionado con el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="df835-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="df835-130">Comprueba si el dispositivo es capaz de tooconnect tooAzure Mobile Engagement con otra aplicación de Azure Mobile Engagement integrado.</span><span class="sxs-lookup"><span data-stu-id="df835-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="df835-131">Compruebe que puede generar eventos, los trabajos y bloqueos desde el teléfono que se pueden ver en la interfaz de usuario de Azure Mobile Engagement Hola.</span><span class="sxs-lookup"><span data-stu-id="df835-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="df835-132">Probar si puede enviar notificaciones de inserción de dispositivo de tooyour de interfaz de usuario de Azure Mobile Engagement Hola basándose en su identificador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="df835-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="df835-133">tootest si el problema de hello está relacionado con la aplicación:</span><span class="sxs-lookup"><span data-stu-id="df835-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="df835-134">Instale y pruebe la aplicación desde un emulador en lugar de hacerlo desde un dispositivo físico:</span><span class="sxs-lookup"><span data-stu-id="df835-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="df835-135">tootest si el problema de hello es con un sistema operativo actualiza tooend usuario dispositivos, que requieren un tooresolve de actualización de SDK:</span><span class="sxs-lookup"><span data-stu-id="df835-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="df835-136">Probar la aplicación en distintos dispositivos con distintas versiones de SO Hola.</span><span class="sxs-lookup"><span data-stu-id="df835-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="df835-137">Confirme que está utilizando la versión más reciente de Hola de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="df835-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="df835-138">Problemas de conectividad e información incorrecta</span><span class="sxs-lookup"><span data-stu-id="df835-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="df835-139">Problema</span><span class="sxs-lookup"><span data-stu-id="df835-139">Issue</span></span>
* <span data-ttu-id="df835-140">Problemas para iniciar sesión en Hola interfaz de usuario de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="df835-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="df835-141">Errores de conexión con hello Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="df835-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="df835-142">Problemas al cargar las etiquetas de información de aplicación a través de hello API de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="df835-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="df835-143">Problemas de descarga de registros o datos exportados desde Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="df835-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="df835-144">Información incorrecta que se muestra en la interfaz de usuario de Azure Mobile Engagement Hola.</span><span class="sxs-lookup"><span data-stu-id="df835-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="df835-145">Información incorrecta que se muestra en los registros de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="df835-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="df835-146">Causas</span><span class="sxs-lookup"><span data-stu-id="df835-146">Causes</span></span>
* <span data-ttu-id="df835-147">Confirme que su cuenta de usuario tiene la tarea de hello de tooperform de permisos suficientes.</span><span class="sxs-lookup"><span data-stu-id="df835-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="df835-148">Confirme que error hello no está aislado tooone equipo o la red local.</span><span class="sxs-lookup"><span data-stu-id="df835-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="df835-149">Confirme que ese servicio de Azure Mobile Engagement hello no tiene ningún las interrupciones registradas.</span><span class="sxs-lookup"><span data-stu-id="df835-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="df835-150">Confirme que los archivos de la etiqueta de información de la aplicación siguen todas estas reglas:</span><span class="sxs-lookup"><span data-stu-id="df835-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="df835-151">Use solo Hola juego de caracteres UTF8 (no se admite el juego de caracteres ANSI de hello).</span><span class="sxs-lookup"><span data-stu-id="df835-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="df835-152">Use una coma "," como carácter de separador de hello (puede abrir un carácter de separador de servicio solicitud toorequest toochange Hola .csv desde una coma "," carácter tooanother como un punto y coma ";").</span><span class="sxs-lookup"><span data-stu-id="df835-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="df835-153">Use minúsculas para los valores booleanos "true" y "false".</span><span class="sxs-lookup"><span data-stu-id="df835-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="df835-154">Usar un archivo que es inferior al tamaño de archivo máximo de Hola de 35MB.</span><span class="sxs-lookup"><span data-stu-id="df835-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

