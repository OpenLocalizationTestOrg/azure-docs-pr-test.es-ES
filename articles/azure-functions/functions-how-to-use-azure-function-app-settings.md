---
title: "Definición de la configuración de Azure Function App | Microsoft Docs"
description: "Obtenga información sobre cómo definir la configuración de Azure Function App."
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
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="c3fd8-103">Administración de una Function App en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c3fd8-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="c3fd8-104">En Azure Functions, una Function App ofrece el contexto de ejecución de funciones individuales.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="c3fd8-105">Los comportamientos de Function App se aplican a todas las funciones hospedadas en una Function App determinada.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="c3fd8-106">En este tema se describe cómo configurar y administrar Function App en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="c3fd8-107">Para comenzar, vaya a [Azure Portal](http://portal.azure.com) e inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="c3fd8-108">En la barra de búsqueda en la parte superior del portal, escriba el nombre de la Function App y selecciónela en la lista.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="c3fd8-109">Después de seleccionar la Function App, vea la siguiente página:</span><span class="sxs-lookup"><span data-stu-id="c3fd8-109">After selecting your function app, you see the following page:</span></span>

![Información general sobre Function App en Azure Portal](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="c3fd8-111"><a name="manage-app-service-settings"></a>Pestaña Configuración de Function App</span><span class="sxs-lookup"><span data-stu-id="c3fd8-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Información general sobre Function App en Azure Portal](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="c3fd8-113">En la pestaña **Configuración**, puede actualizar la versión de Functions en tiempo de ejecución que la Function App utiliza.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="c3fd8-114">Aquí también puede administrar las claves de host usadas para restringir el acceso HTTP a todas las funciones que Function App hospeda.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="c3fd8-115">Functions admite los planes de hospedaje de consumo y App Service.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="c3fd8-116">Para más información, vea [Elija el plan de servicio correcto para Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="c3fd8-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="c3fd8-117">Para poder predecir mejor en el plan de consumo, Functions le permite limitar el uso de la plataforma mediante la configuración de una cuota de uso diaria, en gigabytes por segundo.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="c3fd8-118">Cuando se alcanza la cuota de uso diaria, la Function App se detiene.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="c3fd8-119">Una Function App que se haya detenido como resultado de alcanzar la cuota de gasto se puede volver a habilitar desde el mismo contexto que con el que se estableciera la cuota de gasto diario.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="c3fd8-120">Vea la [página de precios de Azure Functions](http://azure.microsoft.com/pricing/details/functions/) para consultar los detalles de facturación.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="c3fd8-121">Pestaña Características de la plataforma</span><span class="sxs-lookup"><span data-stu-id="c3fd8-121">Platform features tab</span></span>

![Pestaña Características de la plataforma de Function App](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="c3fd8-123">Las Function App se ejecutan en la plataforma de Azure App Service, donde también se realiza su mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="c3fd8-124">Por tanto, Function App tiene acceso a la mayoría de las características de la plataforma de hospedaje web principal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="c3fd8-125">En la pestaña **Características de la plataforma** puede acceder a muchas características de la plataforma de App Service que puede usar en las Function App.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="c3fd8-126">No todas las características de App Service están disponibles cuando una Function App se ejecuta con el plan de hospedaje de consumo.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="c3fd8-127">El resto de este tema se centra en las siguientes características de App Service en Azure Portal que resultan útiles para Functions:</span><span class="sxs-lookup"><span data-stu-id="c3fd8-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="c3fd8-128">Editor de App Service</span><span class="sxs-lookup"><span data-stu-id="c3fd8-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="c3fd8-129">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c3fd8-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="c3fd8-130">Console</span><span class="sxs-lookup"><span data-stu-id="c3fd8-130">Console</span></span>](#console)
+ [<span data-ttu-id="c3fd8-131">Herramientas avanzadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="c3fd8-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="c3fd8-132">Opciones de implementación</span><span class="sxs-lookup"><span data-stu-id="c3fd8-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="c3fd8-133">CORS</span><span class="sxs-lookup"><span data-stu-id="c3fd8-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="c3fd8-134">Autenticación</span><span class="sxs-lookup"><span data-stu-id="c3fd8-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="c3fd8-135">Definición de la API</span><span class="sxs-lookup"><span data-stu-id="c3fd8-135">API definition</span></span>](#swagger)

<span data-ttu-id="c3fd8-136">Para más información sobre cómo trabajar con la configuración de App Service, vea [Configuración de Azure App Service](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c3fd8-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="c3fd8-137"><a name="editor"></a>Editor de App Service</span><span class="sxs-lookup"><span data-stu-id="c3fd8-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Editor de App Service de Function App](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="c3fd8-139">El Editor de App Service es un editor en portal avanzado que puede usar para modificar archivos de configuración JSON y archivos de código similares.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="c3fd8-140">Al seleccionar esta opción se inicia una pestaña de explorador independiente con un editor básico.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="c3fd8-141">Esto le permite realizar la integración con el repositorio Git, ejecutar y depurar código y modificar la configuración de Function App.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="c3fd8-142">Este editor proporciona un entorno de desarrollo mejorado para las funciones en comparación con la hoja de Function App predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![Editor de App Service](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="c3fd8-144"><a name="settings"></a>Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c3fd8-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Configuración de la aplicación Function App](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="c3fd8-146">En la hoja **Configuración de la aplicación** de App Service puede configurar y administrar las versiones de Framework, la depuración remota, la configuración de las aplicaciones y las cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="c3fd8-147">Al integrar Function App con otros servicios de Azure y de terceros, puede modificar esta configuración aquí.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configuración de la aplicación](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="c3fd8-149"><a name="console"></a>Consola</span><span class="sxs-lookup"><span data-stu-id="c3fd8-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Consola de Function App en Azure Portal](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="c3fd8-151">La consola del portal es una herramienta ideal para desarrolladores si prefiere interactuar con Function App desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="c3fd8-152">Los comandos comunes incluyen creación de archivos y directorios y navegación por los mismos, así como la ejecución de archivos y scripts por lotes.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Consola de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="c3fd8-154"><a name="kudu"></a>Herramientas avanzadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="c3fd8-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Kudu de Function App en Azure Portal](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="c3fd8-156">Las herramientas avanzadas para App Service (también conocidas como Kudu) proporcionan acceso a las características administrativas avanzadas de la Function App.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="c3fd8-157">Con Kudu, puede administrar la información del sistema, la configuración de las aplicaciones, las variables del entorno, las extensiones del sitio, los encabezados HTTP y las variables del servidor.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="c3fd8-158">También puede iniciar **Kudu** si examina el punto de conexión de SCM de la Function App, como `https://<myfunctionapp>.scm.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurar Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="c3fd8-160"><a name="deployment">Opciones de implementación</span><span class="sxs-lookup"><span data-stu-id="c3fd8-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opciones de implementación de Function App en Azure Portal](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="c3fd8-162">Functions permite desarrollar código de funciones en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="c3fd8-163">Después, puede cargar el proyecto de Function App local en Azure.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="c3fd8-164">Además de la carga por FTP tradicional, Functions permite implementar Function App con soluciones populares de integración continua, como GitHub, VSTS, Dropbox, Bitbucket y otras.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="c3fd8-165">Para más información, vea [Implementación continua para Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c3fd8-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="c3fd8-166">Para realizar cargas manuales con FTP o Git local, también debe [configurar las credenciales de implementación](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="c3fd8-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="c3fd8-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="c3fd8-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![CORS de Function App en Azure Portal](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="c3fd8-169">Para evitar la ejecución de código malintencionado en los servicios, App Service bloquea las llamadas a las Function App desde orígenes externos.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="c3fd8-170">Functions admite el uso compartido de recursos entre orígenes (CORS) para que pueda definir una "lista blanca" de orígenes permitidos desde los que las funciones puedan aceptar solicitudes remotas.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configuración de CORS de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="c3fd8-172"><a name="auth"></a>Autenticación</span><span class="sxs-lookup"><span data-stu-id="c3fd8-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Autenticación de Function App en Azure Portal](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="c3fd8-174">Si las funciones usan un desencadenador HTTP, puede requerir que las llamadas se autentiquen primero.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="c3fd8-175">App Service admite la autenticación de Azure Active Directory y el inicio de sesión en proveedores locales, como Facebook, Microsoft y Twitter.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="c3fd8-176">Para más información sobre cómo configurar los proveedores de autenticación específicos, consulte [Autenticación y autorización en Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3fd8-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configuración de la autenticación de una Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="c3fd8-178"><a name="swagger"></a>Definición de la API</span><span class="sxs-lookup"><span data-stu-id="c3fd8-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Definición de API de Function App mediante Swagger en Azure Portal](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="c3fd8-180">Functions admite Swagger para permitir que los clientes consuman las funciones desencadenadas por HTTP de forma más fácil.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="c3fd8-181">Para más información sobre cómo crear definiciones de API con Swagger, visite la [introducción a API Apps, ASP.NET y Swagger en Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3fd8-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="c3fd8-182">También puede usar Functions Proxies para definir una única superficie de API para varias funciones.</span><span class="sxs-lookup"><span data-stu-id="c3fd8-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="c3fd8-183">Para más información, vea [Trabajo con Azure Functions Proxies](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="c3fd8-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configuración de la API de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="c3fd8-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3fd8-185">Next steps</span></span>

+ [<span data-ttu-id="c3fd8-186">Configuración de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c3fd8-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="c3fd8-187">Implementación continua para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c3fd8-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



