---
title: "aaaConfigure opciones de aplicación de función de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo funcionan las tooconfigure Azure configuración de la aplicación."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="81458-103">¿Cómo toomanage una aplicación de la función en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="81458-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="81458-104">En las funciones de Azure, una aplicación de la función proporciona el contexto de ejecución de Hola para las funciones individuales.</span><span class="sxs-lookup"><span data-stu-id="81458-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="81458-105">Comportamientos de la aplicación de función aplican funciones de tooall hospedadas por una aplicación de la función especificada.</span><span class="sxs-lookup"><span data-stu-id="81458-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="81458-106">Este tema se describe cómo tooconfigure y administrar las aplicaciones de la función en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="81458-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="81458-107">toobegin, vaya toohello [portal de Azure](http://portal.azure.com) e inicie sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="81458-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="81458-108">En la barra de búsqueda de hello en parte superior de hello del portal de hello, escriba Hola nombre de la aplicación de la función y selecciónelo en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="81458-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="81458-109">Después de seleccionar la aplicación de la función, vea Hola después de página:</span><span class="sxs-lookup"><span data-stu-id="81458-109">After selecting your function app, you see hello following page:</span></span>

![Información general de la aplicación de función en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="81458-111"><a name="manage-app-service-settings"></a>Pestaña Configuración de Function App</span><span class="sxs-lookup"><span data-stu-id="81458-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Información general de aplicaciones de función en hello portal de Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="81458-113">Hola **configuración** ficha es donde puede actualizar la versión de Hola funciones en tiempo de ejecución utilizado por la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="81458-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="81458-114">También es donde se administran hello las claves usadas toorestrict HTTP acceso tooall funciones de host hospedadas por la aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="81458-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="81458-115">Functions admite los planes de hospedaje de consumo y App Service.</span><span class="sxs-lookup"><span data-stu-id="81458-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="81458-116">Para obtener más información, consulte [elegir el plan del servicio correcta de Hola para las funciones de Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="81458-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="81458-117">Para poder predecir mejor en el plan de consumo de hello, funciones permite limitar el uso de plataforma estableciendo una cuota de uso diario, en segundos de gigabytes.</span><span class="sxs-lookup"><span data-stu-id="81458-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="81458-118">Una vez que se alcanza la cuota de uso diario de hello, aplicación de la función de hello se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="81458-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="81458-119">Una aplicación de función detenida como consecuencia de alcanzar Hola gastos cuota puede habilitarse de nuevo de hello mismo contexto que establecer Hola diariamente gastos cuota.</span><span class="sxs-lookup"><span data-stu-id="81458-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="81458-120">Vea hello [funciones de Azure página de precios](http://azure.microsoft.com/pricing/details/functions/) para obtener más información sobre la facturación.</span><span class="sxs-lookup"><span data-stu-id="81458-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="81458-121">Pestaña Características de la plataforma</span><span class="sxs-lookup"><span data-stu-id="81458-121">Platform features tab</span></span>

![Pestaña Características de la plataforma de Function App](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="81458-123">Aplicaciones de función se ejecutan y se mantienen por plataforma de servicio de aplicaciones de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="81458-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="81458-124">Por lo tanto, las aplicaciones de la función tienen acceso toomost de características de Hola de plataforma de hospedaje web de núcleo de Azure.</span><span class="sxs-lookup"><span data-stu-id="81458-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="81458-125">Hola **características de la plataforma** ficha es donde acceso Hola muchas características de hello plataforma de servicio de aplicaciones que puede usar en las aplicaciones de la función.</span><span class="sxs-lookup"><span data-stu-id="81458-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="81458-126">No todas las características de servicio de aplicaciones están disponibles cuando se ejecuta una aplicación de la función en el plan de hospedaje de consumo de Hola.</span><span class="sxs-lookup"><span data-stu-id="81458-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="81458-127">resto de Hola de este tema centra en hello siguientes características de servicio de aplicaciones en hello portal de Azure que son útiles para las funciones:</span><span class="sxs-lookup"><span data-stu-id="81458-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="81458-128">Editor de App Service</span><span class="sxs-lookup"><span data-stu-id="81458-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="81458-129">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="81458-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="81458-130">Console</span><span class="sxs-lookup"><span data-stu-id="81458-130">Console</span></span>](#console)
+ [<span data-ttu-id="81458-131">Herramientas avanzadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="81458-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="81458-132">Opciones de implementación</span><span class="sxs-lookup"><span data-stu-id="81458-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="81458-133">CORS</span><span class="sxs-lookup"><span data-stu-id="81458-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="81458-134">Autenticación</span><span class="sxs-lookup"><span data-stu-id="81458-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="81458-135">Definición de la API</span><span class="sxs-lookup"><span data-stu-id="81458-135">API definition</span></span>](#swagger)

<span data-ttu-id="81458-136">Para obtener más información acerca de cómo toowork con la configuración de servicio de aplicaciones, consulte [configurar opciones de servicio de aplicación de Azure](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="81458-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="81458-137"><a name="editor"></a>Editor de App Service</span><span class="sxs-lookup"><span data-stu-id="81458-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Editor de App Service de Function App](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="81458-139">Hola editor de servicio de aplicaciones es un editor en el portal avanzado que puede usar archivos de configuración de JSON de toomodify y archivos de código similares.</span><span class="sxs-lookup"><span data-stu-id="81458-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="81458-140">Al seleccionar esta opción se inicia una pestaña de explorador independiente con un editor básico.</span><span class="sxs-lookup"><span data-stu-id="81458-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="81458-141">Esto permite toointegrate con código de depuración, ejecución y repositorio de Git de Hola y modificar la configuración de aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="81458-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="81458-142">Este editor proporciona un entorno de desarrollo mejoradas para las funciones en comparación con la hoja de la aplicación de función de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="81458-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![Hola editor de servicio de aplicaciones](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="81458-144"><a name="settings"></a>Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="81458-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Configuración de la aplicación Function App](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="81458-146">Hola servicio de aplicaciones **configuración de la aplicación** hoja es donde configurar y administrar versiones de framework, depuración remota, configuración de la aplicación y las cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="81458-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="81458-147">Al integrar Function App con otros servicios de Azure y de terceros, puede modificar esta configuración aquí.</span><span class="sxs-lookup"><span data-stu-id="81458-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configuración de la aplicación](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="81458-149"><a name="console"></a>Consola</span><span class="sxs-lookup"><span data-stu-id="81458-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Consola de aplicación de función en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="81458-151">consola de Hello en el portal es una herramienta de desarrollador ideal cuando se prefiera toointeract con la aplicación de la función de la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="81458-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="81458-152">Los comandos comunes incluyen creación de archivos y directorios y navegación por los mismos, así como la ejecución de archivos y scripts por lotes.</span><span class="sxs-lookup"><span data-stu-id="81458-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Consola de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="81458-154"><a name="kudu"></a>Herramientas avanzadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="81458-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Función aplicación Kudu Hola portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="81458-156">Hello herramientas avanzadas para la aplicación de servicio (también conocido como Kudu) proporcionan acceso tooadvanced características administrativas de la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="81458-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="81458-157">Con Kudu, puede administrar la información del sistema, la configuración de las aplicaciones, las variables del entorno, las extensiones del sitio, los encabezados HTTP y las variables del servidor.</span><span class="sxs-lookup"><span data-stu-id="81458-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="81458-158">También puede iniciar **Kudu** examinando extremo SCM toohello para la aplicación de la función, al igual que`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="81458-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurar Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="81458-160"><a name="deployment">Opciones de implementación</span><span class="sxs-lookup"><span data-stu-id="81458-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opciones de implementación de aplicación de funciones en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="81458-162">Functions permite desarrollar código de funciones en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="81458-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="81458-163">A continuación, puede cargar su tooAzure de proyecto de aplicación de función local.</span><span class="sxs-lookup"><span data-stu-id="81458-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="81458-164">Además de carga FTP tootraditional, funciones le permite implementar la aplicación de función con soluciones de integración continua populares, como GitHub, VSTS, Dropbox, Bitbucket u otros datos.</span><span class="sxs-lookup"><span data-stu-id="81458-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="81458-165">Para más información, vea [Implementación continua para Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="81458-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="81458-166">tooupload manualmente mediante FTP o Git local, también debe [configurar las credenciales de implementación](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="81458-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="81458-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="81458-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Función aplicación CORS en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="81458-169">tooprevent la ejecución de código malintencionado en los servicios, bloques de servicio de aplicaciones llama a tooyour función aplicaciones desde orígenes externos.</span><span class="sxs-lookup"><span data-stu-id="81458-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="81458-170">Las funciones es compatible con toolet (CORS) que definen una "lista blanca" de permite orígenes desde el que las funciones pueden aceptar las solicitudes remotas de uso compartido de recursos entre orígenes.</span><span class="sxs-lookup"><span data-stu-id="81458-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configuración de CORS de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="81458-172"><a name="auth"></a>Autenticación</span><span class="sxs-lookup"><span data-stu-id="81458-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Autenticación de la aplicación de función en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="81458-174">Cuando las funciones usan un desencadenador HTTP, puede requerir llamadas toofirst autenticarse.</span><span class="sxs-lookup"><span data-stu-id="81458-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="81458-175">App Service admite la autenticación de Azure Active Directory y el inicio de sesión en proveedores locales, como Facebook, Microsoft y Twitter.</span><span class="sxs-lookup"><span data-stu-id="81458-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="81458-176">Para más información sobre cómo configurar los proveedores de autenticación específicos, consulte [Autenticación y autorización en Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81458-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configuración de la autenticación de una Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="81458-178"><a name="swagger"></a>Definición de la API</span><span class="sxs-lookup"><span data-stu-id="81458-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![API de aplicación de función swagger definición Hola portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="81458-180">Las funciones es compatible con Swagger tooallow clientes toomore utilizar fácilmente sus funciones desencadenados por HTTP.</span><span class="sxs-lookup"><span data-stu-id="81458-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="81458-181">Para más información sobre cómo crear definiciones de API con Swagger, visite la [introducción a API Apps, ASP.NET y Swagger en Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="81458-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="81458-182">También puede utilizar servidores proxy de funciones toodefine una sola superficie de API para varias funciones.</span><span class="sxs-lookup"><span data-stu-id="81458-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="81458-183">Para más información, vea [Trabajo con Azure Functions Proxies](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="81458-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configuración de la API de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="81458-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81458-185">Next steps</span></span>

+ [<span data-ttu-id="81458-186">Configuración de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="81458-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="81458-187">Implementación continua para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="81458-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



