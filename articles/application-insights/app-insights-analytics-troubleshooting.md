---
title: "aaaTroubleshoot análisis de visión de la aplicación de Azure | Documentos de Microsoft"
description: "¿Problemas con Analytics de Application Insights? Comience aquí. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="329c5-104">Solución de problemas de Analytics en Application Insights</span><span class="sxs-lookup"><span data-stu-id="329c5-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="329c5-105">¿Problemas con [Analytics de Application Insights](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="329c5-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="329c5-106">Comience aquí.</span><span class="sxs-lookup"><span data-stu-id="329c5-106">Start here.</span></span> <span data-ttu-id="329c5-107">Análisis de es Hola eficaz herramienta de búsqueda de Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="329c5-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="329c5-108">límites</span><span class="sxs-lookup"><span data-stu-id="329c5-108">Limits</span></span>
* <span data-ttu-id="329c5-109">En la actualidad, resultados de la consulta son toojust limitado durante una semana de datos pasados.</span><span class="sxs-lookup"><span data-stu-id="329c5-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="329c5-110">Exploradores en los que la hemos probado: últimas ediciones de Chrome, Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="329c5-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="329c5-111">Extensiones de explorador incompatibles conocidas</span><span class="sxs-lookup"><span data-stu-id="329c5-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="329c5-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="329c5-112">Ghostery</span></span>

<span data-ttu-id="329c5-113">Deshabilitar la extensión de Hola o use un explorador diferente.</span><span class="sxs-lookup"><span data-stu-id="329c5-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="329c5-114"><a name="e-a"></a> "Error inesperado"</span><span class="sxs-lookup"><span data-stu-id="329c5-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Pantalla de error inesperado](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="329c5-116">Error interno durante el tiempo de ejecución del portal: excepción no controlada.</span><span class="sxs-lookup"><span data-stu-id="329c5-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="329c5-117">Limpiar la memoria caché del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="329c5-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="329c5-118"><a name="e-b"></a>403... inténtelo tooreload</span><span class="sxs-lookup"><span data-stu-id="329c5-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403... inténtelo tooreload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="329c5-120">Se ha producido un error relacionado con la autenticación (durante la autenticación o durante la generación del token de acceso).</span><span class="sxs-lookup"><span data-stu-id="329c5-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="329c5-121">portal de Hello no puede tener ninguna manera de recuperar demasiado sin cambiar la configuración del explorador.</span><span class="sxs-lookup"><span data-stu-id="329c5-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="329c5-122">Comprobar [están habilitadas las cookies de terceros](#cookies) en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="329c5-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="329c5-123"><a name="authentication"></a>403... compruebe la zona de seguridad</span><span class="sxs-lookup"><span data-stu-id="329c5-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... compruebe la zona de seguridad](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="329c5-125">Se ha producido un error relacionado con la autenticación (durante la autenticación o durante la generación del token de acceso).</span><span class="sxs-lookup"><span data-stu-id="329c5-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="329c5-126">portal de Hello no puede tener ninguna manera de recuperar demasiado sin cambiar la configuración del explorador.</span><span class="sxs-lookup"><span data-stu-id="329c5-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="329c5-127">Comprobar [están habilitadas las cookies de terceros](#cookies) en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="329c5-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="329c5-128">¿Usó un favorito, marcador o portal de análisis de vínculo guardado tooopen Hola?</span><span class="sxs-lookup"><span data-stu-id="329c5-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="329c5-129">¿Se inició sesión con credenciales diferentes a las que utilizó cuando guarda vínculo Hola?</span><span class="sxs-lookup"><span data-stu-id="329c5-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="329c5-130">Pruebe a usar una ventana de exploración privada o de incógnito (después de cerrar todas estas ventanas).</span><span class="sxs-lookup"><span data-stu-id="329c5-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="329c5-131">Tendrá tooprovide sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="329c5-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="329c5-132">Abra otra ventana del explorador (normal) y vaya demasiado[Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="329c5-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="329c5-133">Cierre la sesión. A continuación, abra el vínculo e inicie sesión con las credenciales correctas de Hola.</span><span class="sxs-lookup"><span data-stu-id="329c5-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="329c5-134">Los usuarios de Edge y de Internet Explorer también pueden recibir este error cuando no se admite la configuración de zona Sitios de confianza.</span><span class="sxs-lookup"><span data-stu-id="329c5-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="329c5-135">Comprobar ambos [portal de análisis de](https://analytics.applicationinsights.io) y [portal de Azure Active Directory](https://portal.azure.com) están en hello misma zona de seguridad:</span><span class="sxs-lookup"><span data-stu-id="329c5-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="329c5-136">En Internet Explorer, abra **Opciones de Internet**, **Seguridad**, **Sitios de confianza**, **Sitios**:</span><span class="sxs-lookup"><span data-stu-id="329c5-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Cuadro de diálogo Opciones de Internet, si se agrega un sitio tooTrusted sitios](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="329c5-138">En la lista de sitios Web de hello, si cualquiera de las siguientes direcciones URL de Hola se incluyen, asegúrese de que ese Hola otros también se incluyen:</span><span class="sxs-lookup"><span data-stu-id="329c5-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="329c5-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="329c5-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="329c5-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="329c5-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="329c5-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="329c5-141">https://login.windows.net</span></span>

## <span data-ttu-id="329c5-142"><a name="e-d"></a>404 ... Recurso no encontrado</span><span class="sxs-lookup"><span data-stu-id="329c5-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404 ... recurso no encontrado](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="329c5-144">Los recursos de la aplicación se eliminaron de Application Insights y ya no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="329c5-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="329c5-145">Esto puede ocurrir si ha guardado la página de análisis de toohello de dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="329c5-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="329c5-146"><a name="e-e"></a>403 ... Sin autorización</span><span class="sxs-lookup"><span data-stu-id="329c5-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... no autorizado](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="329c5-148">No tienes permiso tooopen esta aplicación en el análisis.</span><span class="sxs-lookup"><span data-stu-id="329c5-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="329c5-149">¿Se obtuvo el vínculo de Hola de otra persona?</span><span class="sxs-lookup"><span data-stu-id="329c5-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="329c5-150">Pídales que estén en hello toomake [lectores o colaboradores para este grupo de recursos](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="329c5-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="329c5-151">¿Ha guardado vínculo Hola con credenciales diferentes?</span><span class="sxs-lookup"><span data-stu-id="329c5-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="329c5-152">Abra hello [portal de Azure](https://portal.azure.com), cierre la sesión y, a continuación, inténtelo de nuevo, este vínculo proporcionar las credenciales correctas de Hola.</span><span class="sxs-lookup"><span data-stu-id="329c5-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="329c5-153"><a name="html-storage"></a>403 ... Almacenamiento de HTML5</span><span class="sxs-lookup"><span data-stu-id="329c5-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="329c5-154">Nuestro portal utiliza localStorage y sessionStorage de HTML5.</span><span class="sxs-lookup"><span data-stu-id="329c5-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="329c5-155">Chrome: Configuración, Privacidad, Configuración de contenido.</span><span class="sxs-lookup"><span data-stu-id="329c5-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="329c5-156">Internet Explorer: Opciones de Internet, pestaña Opciones avanzadas, Seguridad, Habilitar el almacenamiento DOM</span><span class="sxs-lookup"><span data-stu-id="329c5-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... Intente almacenamiento tooenable HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="329c5-158"><a name="e-g"></a>404 ... Suscripción no encontrada</span><span class="sxs-lookup"><span data-stu-id="329c5-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Suscripción no encontrada](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="329c5-160">Hola URL no es válida.</span><span class="sxs-lookup"><span data-stu-id="329c5-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="329c5-161">Abra el recurso de aplicación hello en [portal de Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="329c5-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="329c5-162">A continuación, utilice botón de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="329c5-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="329c5-163"><a name="e-h"></a>404... la página no existe</span><span class="sxs-lookup"><span data-stu-id="329c5-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... La página no existe](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="329c5-165">Hola URL no es válida.</span><span class="sxs-lookup"><span data-stu-id="329c5-165">hello URL is invalid.</span></span>

* <span data-ttu-id="329c5-166">Abra el recurso de aplicación hello en [portal de Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="329c5-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="329c5-167">A continuación, utilice botón de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="329c5-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="329c5-168"><a name="cookies"></a>Habilitar cookies de terceros</span><span class="sxs-lookup"><span data-stu-id="329c5-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="329c5-169">Vea [cómo toodisable de terceros cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), pero tenga en cuenta que necesitamos demasiado**habilitar** ellos.</span><span class="sxs-lookup"><span data-stu-id="329c5-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

