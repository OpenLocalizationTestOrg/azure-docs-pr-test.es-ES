---
title: "Diagnóstico de problemas de Analytics de Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 02df117908fc1790e8cfb9ec0a7218c1b8be856c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="1d96c-104">Solución de problemas de Analytics en Application Insights</span><span class="sxs-lookup"><span data-stu-id="1d96c-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="1d96c-105">¿Problemas con [Analytics de Application Insights](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="1d96c-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="1d96c-106">Comience aquí.</span><span class="sxs-lookup"><span data-stu-id="1d96c-106">Start here.</span></span> <span data-ttu-id="1d96c-107">Analytics es la herramienta eficaz de búsqueda de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1d96c-107">Analytics is the powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="1d96c-108">límites</span><span class="sxs-lookup"><span data-stu-id="1d96c-108">Limits</span></span>
* <span data-ttu-id="1d96c-109">En la actualidad, los resultados de consulta están limitados exclusivamente a solo una semana de datos antiguos.</span><span class="sxs-lookup"><span data-stu-id="1d96c-109">At present, query results are limited to just over a week of past data.</span></span>
* <span data-ttu-id="1d96c-110">Exploradores en los que la hemos probado: últimas ediciones de Chrome, Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="1d96c-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="1d96c-111">Extensiones de explorador incompatibles conocidas</span><span class="sxs-lookup"><span data-stu-id="1d96c-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="1d96c-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="1d96c-112">Ghostery</span></span>

<span data-ttu-id="1d96c-113">Deshabilite la extensión o use un explorador diferente.</span><span class="sxs-lookup"><span data-stu-id="1d96c-113">Disable the extension or use a different browser.</span></span>

## <span data-ttu-id="1d96c-114"><a name="e-a"></a> "Error inesperado"</span><span class="sxs-lookup"><span data-stu-id="1d96c-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Pantalla de error inesperado](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="1d96c-116">Error interno durante el tiempo de ejecución del portal: excepción no controlada.</span><span class="sxs-lookup"><span data-stu-id="1d96c-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="1d96c-117">Limpie la caché del explorador.</span><span class="sxs-lookup"><span data-stu-id="1d96c-117">Clean the browser's cache.</span></span> 

## <span data-ttu-id="1d96c-118"><a name="e-b"></a>403... intente volver a cargar</span><span class="sxs-lookup"><span data-stu-id="1d96c-118"><a name="e-b"></a>403 ... please try to reload</span></span>
![403... intente volver a cargar](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="1d96c-120">Se ha producido un error relacionado con la autenticación (durante la autenticación o durante la generación del token de acceso).</span><span class="sxs-lookup"><span data-stu-id="1d96c-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="1d96c-121">Puede que el portal no tenga forma de recuperarse sin cambiar la configuración del explorador.</span><span class="sxs-lookup"><span data-stu-id="1d96c-121">The portal may have no way to  recover without changing browser settings.</span></span>

* <span data-ttu-id="1d96c-122">Compruebe que las [cookies de terceros estén habilitadas](#cookies) en el explorador.</span><span class="sxs-lookup"><span data-stu-id="1d96c-122">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 

## <span data-ttu-id="1d96c-123"><a name="authentication"></a>403... compruebe la zona de seguridad</span><span class="sxs-lookup"><span data-stu-id="1d96c-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... compruebe la zona de seguridad](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="1d96c-125">Se ha producido un error relacionado con la autenticación (durante la autenticación o durante la generación del token de acceso).</span><span class="sxs-lookup"><span data-stu-id="1d96c-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="1d96c-126">Puede que el portal no tenga forma de recuperarse sin cambiar la configuración del explorador.</span><span class="sxs-lookup"><span data-stu-id="1d96c-126">The portal may have no way to  recover without changing browser settings.</span></span>

1. <span data-ttu-id="1d96c-127">Compruebe que las [cookies de terceros estén habilitadas](#cookies) en el explorador.</span><span class="sxs-lookup"><span data-stu-id="1d96c-127">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 
2. <span data-ttu-id="1d96c-128">¿Ha utilizado un favorito, un marcador o un vínculo guardado para abrir el portal de Analytics?</span><span class="sxs-lookup"><span data-stu-id="1d96c-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span></span> <span data-ttu-id="1d96c-129">¿Ha iniciado sesión con credenciales diferentes a las que utilizó cuando guardó el vínculo?</span><span class="sxs-lookup"><span data-stu-id="1d96c-129">Are you signed in with different credentials than you used when you saved the link?</span></span>
3. <span data-ttu-id="1d96c-130">Pruebe a usar una ventana de exploración privada o de incógnito (después de cerrar todas estas ventanas).</span><span class="sxs-lookup"><span data-stu-id="1d96c-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="1d96c-131">Tendrá que proporcionar sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="1d96c-131">You'll have to provide your credentials.</span></span> 
4. <span data-ttu-id="1d96c-132">Abra otra ventana de explorador (ordinaria) y vaya a [Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d96c-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span></span> <span data-ttu-id="1d96c-133">Cierre la sesión. A continuación, abra el vínculo e inicie sesión con las credenciales correctas.</span><span class="sxs-lookup"><span data-stu-id="1d96c-133">Sign out. Then open your link and sign in with the correct credentials.</span></span>
5. <span data-ttu-id="1d96c-134">Los usuarios de Edge y de Internet Explorer también pueden recibir este error cuando no se admite la configuración de zona Sitios de confianza.</span><span class="sxs-lookup"><span data-stu-id="1d96c-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="1d96c-135">Compruebe que tanto el [portal de Analytics](https://analytics.applicationinsights.io) como el [portal de Azure Active Directory](https://portal.azure.com) se encuentren en la misma zona de seguridad:</span><span class="sxs-lookup"><span data-stu-id="1d96c-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span></span>
   
   * <span data-ttu-id="1d96c-136">En Internet Explorer, abra **Opciones de Internet**, **Seguridad**, **Sitios de confianza**, **Sitios**:</span><span class="sxs-lookup"><span data-stu-id="1d96c-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Cuadro de diálogo Opciones de Internet, agregar un sitio a Sitios de confianza](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="1d96c-138">En la lista de sitios web, si se incluye alguna de las siguientes direcciones URL, asegúrese de que las otras se incluyan también:</span><span class="sxs-lookup"><span data-stu-id="1d96c-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span></span>
     
     <span data-ttu-id="1d96c-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="1d96c-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="1d96c-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1d96c-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="1d96c-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="1d96c-141">https://login.windows.net</span></span>

## <span data-ttu-id="1d96c-142"><a name="e-d"></a>404 ... Recurso no encontrado</span><span class="sxs-lookup"><span data-stu-id="1d96c-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404 ... recurso no encontrado](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="1d96c-144">Los recursos de la aplicación se eliminaron de Application Insights y ya no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="1d96c-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="1d96c-145">Esto puede suceder si guardó la dirección URL en la página de Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d96c-145">This can happen if you saved the URL to the Analytics page.</span></span>

## <span data-ttu-id="1d96c-146"><a name="e-e"></a>403 ... Sin autorización</span><span class="sxs-lookup"><span data-stu-id="1d96c-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... no autorizado](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="1d96c-148">No tiene permiso para abrir esta aplicación en Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d96c-148">You don't have permission to open this application in Analytics.</span></span>

* <span data-ttu-id="1d96c-149">¿Recibió el vínculo de otra persona?</span><span class="sxs-lookup"><span data-stu-id="1d96c-149">Did you get the link from someone else?</span></span> <span data-ttu-id="1d96c-150">Pregúnteles para asegurarse de que se encuentra en los roles de [lector o colaborador en este grupo de recursos](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="1d96c-150">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="1d96c-151">¿Guardó el vínculo mediante credenciales diferentes?</span><span class="sxs-lookup"><span data-stu-id="1d96c-151">Did you save the link using different credentials?</span></span> <span data-ttu-id="1d96c-152">Abra el [Portal de Azure](https://portal.azure.com), cierre sesión y vuelva a probar este vínculo con las credenciales correctas.</span><span class="sxs-lookup"><span data-stu-id="1d96c-152">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span></span>

## <span data-ttu-id="1d96c-153"><a name="html-storage"></a>403 ... Almacenamiento de HTML5</span><span class="sxs-lookup"><span data-stu-id="1d96c-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="1d96c-154">Nuestro portal utiliza localStorage y sessionStorage de HTML5.</span><span class="sxs-lookup"><span data-stu-id="1d96c-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="1d96c-155">Chrome: Configuración, Privacidad, Configuración de contenido.</span><span class="sxs-lookup"><span data-stu-id="1d96c-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="1d96c-156">Internet Explorer: Opciones de Internet, pestaña Opciones avanzadas, Seguridad, Habilitar el almacenamiento DOM</span><span class="sxs-lookup"><span data-stu-id="1d96c-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... pruebe a habilitar el almacenamiento de HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="1d96c-158"><a name="e-g"></a>404 ... Suscripción no encontrada</span><span class="sxs-lookup"><span data-stu-id="1d96c-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Suscripción no encontrada](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="1d96c-160">La dirección URL no es válida.</span><span class="sxs-lookup"><span data-stu-id="1d96c-160">The URL is invalid.</span></span> 

* <span data-ttu-id="1d96c-161">Abra el recurso de aplicación en el [portal de Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d96c-161">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="1d96c-162">A continuación, utilice el botón de Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d96c-162">Then use the Analytics button.</span></span>

## <span data-ttu-id="1d96c-163"><a name="e-h"></a>404... la página no existe</span><span class="sxs-lookup"><span data-stu-id="1d96c-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... La página no existe](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="1d96c-165">La dirección URL no es válida.</span><span class="sxs-lookup"><span data-stu-id="1d96c-165">The URL is invalid.</span></span>

* <span data-ttu-id="1d96c-166">Abra el recurso de aplicación en el [portal de Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d96c-166">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="1d96c-167">A continuación, utilice el botón de Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d96c-167">Then use the Analytics button.</span></span>

## <span data-ttu-id="1d96c-168"><a name="cookies"></a>Habilitar cookies de terceros</span><span class="sxs-lookup"><span data-stu-id="1d96c-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="1d96c-169">Vea [How to disable third-party cookies in all major web browsers](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers)(Cómo deshabilitar las cookies de terceros en todos los principales exploradores), pero tenga en cuenta que es necesario **habilitarlas** .</span><span class="sxs-lookup"><span data-stu-id="1d96c-169">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

