---
title: "Guía de solución de problemas de Azure Mobile Engagement - Servicio"
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="3ad2f-103">Guía de solución de problemas de servicio</span><span class="sxs-lookup"><span data-stu-id="3ad2f-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="3ad2f-104">Los siguientes son posibles problemas que pueden producirse con cómo Azure Mobile Engagement se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="3ad2f-105">Interrupciones del servicio</span><span class="sxs-lookup"><span data-stu-id="3ad2f-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="3ad2f-106">Problema</span><span class="sxs-lookup"><span data-stu-id="3ad2f-106">Issue</span></span>
* <span data-ttu-id="3ad2f-107">Problemas que parecen deberse a interrupciones del servicio de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="3ad2f-108">Causas</span><span class="sxs-lookup"><span data-stu-id="3ad2f-108">Causes</span></span>
* <span data-ttu-id="3ad2f-109">Los problemas que parecen deberse a interrupciones del servicio de Azure Mobile Engagement pueden deberse a diversos problemas:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="3ad2f-110">Problemas aislados que originalmente parecen sistémicos de todo Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3ad2f-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="3ad2f-111">Problemas conocidos causados por interrupciones de los servidores (no siempre se muestran en el estado del servidor):</span><span class="sxs-lookup"><span data-stu-id="3ad2f-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="3ad2f-112">Retrasos de la programación, errores de orientación, problemas de actualización de distintivos, detención de la recopilación de estadísticas, detención del funcionamiento de las API, imposibilidad de crear nuevas aplicaciones o usuarios, errores de DNS y errores de tiempo de espera en la interfaz de usuario, en la API o en las aplicaciones de un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="3ad2f-113">Interrupciones de dependencia en la nube [Estado del servicio de Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="3ad2f-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="3ad2f-114">Interrupciones de dependencia de los servicios de notificación de inserción (PNS)</span><span class="sxs-lookup"><span data-stu-id="3ad2f-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="3ad2f-115">Interrupciones de la tienda de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="3ad2f-115">App Store Outages</span></span>

1) <span data-ttu-id="3ad2f-116">Para comprobar si el problema es sistémico, puede probar la misma función desde uno de estos elementos diferentes:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="3ad2f-117">Aplicación integrada de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3ad2f-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="3ad2f-118">Dispositivo de prueba</span><span class="sxs-lookup"><span data-stu-id="3ad2f-118">Test device</span></span>
* <span data-ttu-id="3ad2f-119">Versión del sistema operativo del dispositivo de prueba</span><span class="sxs-lookup"><span data-stu-id="3ad2f-119">Test device OS version</span></span>
* <span data-ttu-id="3ad2f-120">Campaña</span><span class="sxs-lookup"><span data-stu-id="3ad2f-120">Campaign</span></span>
* <span data-ttu-id="3ad2f-121">Cuenta de usuario administrador</span><span class="sxs-lookup"><span data-stu-id="3ad2f-121">Administrator user account</span></span>
* <span data-ttu-id="3ad2f-122">Explorador (Internet Explorer, Firefox, Chrome, etc.)</span><span class="sxs-lookup"><span data-stu-id="3ad2f-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="3ad2f-123">Equipo</span><span class="sxs-lookup"><span data-stu-id="3ad2f-123">Computer</span></span>

2) <span data-ttu-id="3ad2f-124">Para probar si el problema solo afecta a la interfaz de usuario o a la API:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="3ad2f-125">Pruebe la misma función en la interfaz de usuario de Azure Mobile Engagement y en la API de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="3ad2f-126">Para probar si el problema está relacionado con la red de telefonía móvil:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="3ad2f-127">Realice la prueba mientras está conectado a Internet a través de Wi-Fi y mientras está conectado a través de la red de teléfono móvil 3G.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="3ad2f-128">Confirme que el firewall no está bloqueando ninguna de las direcciones IP de Azure Mobile Engagement o ningún puerto.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="3ad2f-129">Para probar si el problema está relacionado con el dispositivo:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="3ad2f-130">Compruebe que el dispositivo puede conectarse a Azure Mobile Engagement con otra aplicación integrada en Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="3ad2f-131">Compruebe que puede generar eventos, trabajos y bloqueos desde el teléfono que se puede ver en la interfaz de usuario de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="3ad2f-132">Compruebe que puede enviar notificaciones push desde la interfaz de usuario de Azure Mobile Engagement al dispositivo según su identificador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="3ad2f-133">Para probar si el problema está relacionado con la aplicación:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="3ad2f-134">Instale y pruebe la aplicación desde un emulador en lugar de hacerlo desde un dispositivo físico:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="3ad2f-135">Para probar si el problema está relacionado con las actualizaciones del sistema operativo de los dispositivos del usuario final, que requieren una actualización SDK para resolver:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="3ad2f-136">Pruebe la aplicación en diferentes dispositivos con distintas versiones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="3ad2f-137">Confirme que está utilizando la versión más reciente del SDK.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="3ad2f-138">Problemas de conectividad e información incorrecta</span><span class="sxs-lookup"><span data-stu-id="3ad2f-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="3ad2f-139">Problema</span><span class="sxs-lookup"><span data-stu-id="3ad2f-139">Issue</span></span>
* <span data-ttu-id="3ad2f-140">Problemas para iniciar sesión en la interfaz de usuario de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="3ad2f-141">Errores de conexión con la API de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="3ad2f-142">Problemas al cargar etiquetas de información de aplicación a través de la API del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="3ad2f-143">Problemas de descarga de registros o datos exportados desde Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="3ad2f-144">Información incorrecta que se muestra en la interfaz de usuario de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="3ad2f-145">Información incorrecta que se muestra en los registros de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="3ad2f-146">Causas</span><span class="sxs-lookup"><span data-stu-id="3ad2f-146">Causes</span></span>
* <span data-ttu-id="3ad2f-147">Confirme que su cuenta de usuario tiene permisos suficientes para realizar la tarea.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="3ad2f-148">Confirme que el problema no se limita a un equipo o a la red local.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="3ad2f-149">Confirme que el servicio de Azure Mobile Engagement no tiene interrupciones registradas.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="3ad2f-150">Confirme que los archivos de la etiqueta de información de la aplicación siguen todas estas reglas:</span><span class="sxs-lookup"><span data-stu-id="3ad2f-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="3ad2f-151">Use únicamente el juego de caracteres UTF8 (no se admite el juego de caracteres ANSI).</span><span class="sxs-lookup"><span data-stu-id="3ad2f-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="3ad2f-152">Use una coma "," como carácter separador (puede abrir una solicitud de servicio para solicitar cambiar el carácter separador de .csv de una coma "," a otro carácter como un punto y coma ";").</span><span class="sxs-lookup"><span data-stu-id="3ad2f-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="3ad2f-153">Use minúsculas para los valores booleanos "true" y "false".</span><span class="sxs-lookup"><span data-stu-id="3ad2f-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="3ad2f-154">Use un archivo que de tamaño inferior al tamaño máximo de archivo de 35 MB.</span><span class="sxs-lookup"><span data-stu-id="3ad2f-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

