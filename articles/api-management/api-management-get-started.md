---
title: "aaaManage la primera API de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agregar operaciones toocreate API y empezar a trabajar con administración de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="fea5c-103">Administración de su primera API en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="fea5c-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="fea5c-104"><a name="overview"></a>Información general</span><span class="sxs-lookup"><span data-stu-id="fea5c-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="fea5c-105">Esta guía muestra cómo tooquickly empezar a trabajar en el uso de administración de API de Azure y realizar la primera llamada de API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="fea5c-106"><a name="concepts"></a>¿Qué es la Administración de API de Azure?</span><span class="sxs-lookup"><span data-stu-id="fea5c-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="fea5c-107">Puede usar Administración de API de Azure tootake cualquier back-end e iniciar un programa completo de API basado en él.</span><span class="sxs-lookup"><span data-stu-id="fea5c-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="fea5c-108">Entre los escenarios habituales se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="fea5c-108">Common scenarios include:</span></span>

* <span data-ttu-id="fea5c-109">**Protección de la infraestructura móvil** mediante el control de acceso con claves de API, la prevención de ataques de denegación de servicio mediante la limitación o el uso de directivas de seguridad avanzadas como la validación de tokens JWT.</span><span class="sxs-lookup"><span data-stu-id="fea5c-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="fea5c-110">**Habilitación de ecosistemas de socio comercial de ISV** , ya que ofrece la incorporación de socios rápido por un desarrollador de hello portal y generar un toodecouple de fachada de API de las implementaciones internas que no son listo para consumo partner.</span><span class="sxs-lookup"><span data-stu-id="fea5c-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="fea5c-111">**Ejecutar un programa de API interno** , ya que ofrece una ubicación centralizada para hello organización toocommunicate sobre la disponibilidad de Hola y la versión más reciente de tooAPIs los cambios, el control de acceso en función de las cuentas organizativas, basadas en un canal seguro entre puerta de enlace de API de Hola y Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="fea5c-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="fea5c-112">sistema de Hola se compone de Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="fea5c-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="fea5c-113">Hola **puerta de enlace de API** es el punto de conexión de Hola que:</span><span class="sxs-lookup"><span data-stu-id="fea5c-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="fea5c-114">Acepta llamadas API y los enruta tooyour back-ends.</span><span class="sxs-lookup"><span data-stu-id="fea5c-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="fea5c-115">Comprueba las claves de API, los tokens JWT, los certificados y otras credenciales.</span><span class="sxs-lookup"><span data-stu-id="fea5c-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="fea5c-116">Aplica cuotas de uso y límites de frecuencia.</span><span class="sxs-lookup"><span data-stu-id="fea5c-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="fea5c-117">Transforma la API en marcha Hola sin modificaciones en el código.</span><span class="sxs-lookup"><span data-stu-id="fea5c-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="fea5c-118">Almacena en caché las respuestas de back-end donde se instalaron.</span><span class="sxs-lookup"><span data-stu-id="fea5c-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="fea5c-119">Registra los metadatos de llamada para fines de análisis.</span><span class="sxs-lookup"><span data-stu-id="fea5c-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="fea5c-120">Hola **portal para desarrolladores de** es la interfaz administrativa de Hola donde configuró el programa de API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="fea5c-121">Utilícelo para:</span><span class="sxs-lookup"><span data-stu-id="fea5c-121">Use it to:</span></span>
  
  * <span data-ttu-id="fea5c-122">definir o importar el esquema de API</span><span class="sxs-lookup"><span data-stu-id="fea5c-122">Define or import API schema.</span></span>
  * <span data-ttu-id="fea5c-123">empaquetar las API en productos</span><span class="sxs-lookup"><span data-stu-id="fea5c-123">Package APIs into products.</span></span>
  * <span data-ttu-id="fea5c-124">Configure directivas como las cuotas o transformaciones en hello API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="fea5c-125">obtener información del análisis</span><span class="sxs-lookup"><span data-stu-id="fea5c-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="fea5c-126">administrar usuarios</span><span class="sxs-lookup"><span data-stu-id="fea5c-126">Manage users.</span></span>
* <span data-ttu-id="fea5c-127">Hola **portal para desarrolladores de** actúa como la presencia de hello web principal para los desarrolladores, siempre sea posible:</span><span class="sxs-lookup"><span data-stu-id="fea5c-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="fea5c-128">leer documentación de la API</span><span class="sxs-lookup"><span data-stu-id="fea5c-128">Read API documentation.</span></span>
  * <span data-ttu-id="fea5c-129">Pruebe una API a través de la consola interactiva Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="fea5c-130">Crear una cuenta y suscribirse tooget API claves.</span><span class="sxs-lookup"><span data-stu-id="fea5c-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="fea5c-131">obtener acceso a análisis sobre su propio uso</span><span class="sxs-lookup"><span data-stu-id="fea5c-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="fea5c-132"><a name="create-service-instance"></a>Creación de una instancia de Administración de API</span><span class="sxs-lookup"><span data-stu-id="fea5c-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="fea5c-133">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fea5c-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="fea5c-134">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="fea5c-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="fea5c-135">Para más información, consulte la [evaluación gratuita de Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="fea5c-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="fea5c-136">primer paso para trabajar con la API de administración de Hello es toocreate una instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="fea5c-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="fea5c-137">Inicie sesión en toohello [Portal de Azure] [ Azure Portal] y haga clic en **New**, **Web y móvil**, **administración de API**.</span><span class="sxs-lookup"><span data-stu-id="fea5c-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![API Management new instance][api-management-create-instance-menu]

<span data-ttu-id="fea5c-139">Para **nombre**, especifique un toouse de nombre de subdominio único para la dirección URL del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="fea5c-140">Elija Hola deseado **suscripción**, **grupo de recursos** y **ubicación** para la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="fea5c-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="fea5c-141">Escriba **Contoso Ltd.** para hello **nombreDeOrganización**y escriba la dirección de correo electrónico en hello **correo electrónico del administrador** campo.</span><span class="sxs-lookup"><span data-stu-id="fea5c-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="fea5c-142">Esta dirección de correo electrónico se usa para recibir notificaciones del sistema de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="fea5c-143">Para obtener más información, consulte [cómo tooconfigure notificaciones y plantillas en la administración de API de Azure de correo electrónico][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="fea5c-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![New API Management service][api-management-create-instance-step1]

<span data-ttu-id="fea5c-145">Las instancias de servicio de Administración de API están disponibles en tres niveles: Desarrollador, Estándar y Premium.</span><span class="sxs-lookup"><span data-stu-id="fea5c-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="fea5c-146">Hola nivel desarrollador es para el desarrollo, prueba y pilotos programas de API que la alta disponibilidad no es un problema.</span><span class="sxs-lookup"><span data-stu-id="fea5c-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="fea5c-147">En hello estándar y niveles de Premium, puede escalar su toohandle de recuento de unidad reservada más tráfico.</span><span class="sxs-lookup"><span data-stu-id="fea5c-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="fea5c-148">niveles de Standard y Premium de Hello proporcionan el servicio de administración de API con hello mayoría potencia de procesamiento y el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="fea5c-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="fea5c-149">Puede completar este tutorial mediante cualquier nivel.</span><span class="sxs-lookup"><span data-stu-id="fea5c-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="fea5c-150">Para más información acerca de los niveles de API Management, consulte [Precios de API Management][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="fea5c-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="fea5c-151">Haga clic en **crear** toostart aprovisionamiento de la instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="fea5c-151">Click **Create** toostart provisioning your service instance.</span></span>

![New API Management service][api-management-instance-created]

<span data-ttu-id="fea5c-153">Una vez creada la instancia de servicio de hello, paso siguiente hello es toocreate o importar una API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="fea5c-154"><a name="create-api"></a>Importación de una API</span><span class="sxs-lookup"><span data-stu-id="fea5c-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="fea5c-155">Una API consta de un conjunto de operaciones que se pueden invocar desde una aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="fea5c-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="fea5c-156">Las operaciones de API son servicios de tooexisting procesadas por el proxy web.</span><span class="sxs-lookup"><span data-stu-id="fea5c-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="fea5c-157">Las API se pueden crear (y las operaciones se pueden agregar) manualmente o se pueden importar.</span><span class="sxs-lookup"><span data-stu-id="fea5c-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="fea5c-158">En este tutorial, se importará Hola API para un servicio de web de calculadora de ejemplo proporcionados por Microsoft y hospedadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="fea5c-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="fea5c-159">Para obtener instrucciones sobre cómo crear una API y agregar manualmente las operaciones, vea [cómo toocreate API](api-management-howto-create-apis.md) y [cómo tooadd operaciones tooan API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="fea5c-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="fea5c-160">Se configuran las API de portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="fea5c-161">tooreach, haga clic en **portal para desarrolladores de** de barra de herramientas de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="fea5c-163">Calculadora de hello tooimport API, haga clic en **API** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **API de importación**.</span><span class="sxs-lookup"><span data-stu-id="fea5c-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Botón Importar API][api-management-import-api]

<span data-ttu-id="fea5c-165">Lleve a cabo Hola siguiendo los pasos tooconfigure Hola calculadora API:</span><span class="sxs-lookup"><span data-stu-id="fea5c-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="fea5c-166">Haga clic en **From URL**, escriba **http://calcapi.cloudapp.net/calcapi.json** en hello **dirección URL del documento de especificación** texto cuadro y haga clic en hello **Swagger**  botón de radio.</span><span class="sxs-lookup"><span data-stu-id="fea5c-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="fea5c-167">Tipo de **calc** en hello **sufijo de URL de la API de Web** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="fea5c-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="fea5c-168">Haga clic en hello **productos (opcionales)** cuadro y elija **Starter**.</span><span class="sxs-lookup"><span data-stu-id="fea5c-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="fea5c-169">Haga clic en **guardar** tooimport Hola API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-169">Click **Save** tooimport hello API.</span></span>

![Add new API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="fea5c-171">**Administración de API** admite actualmente las versiones 1.2 y 2.0 del documento Swagger para la importación.</span><span class="sxs-lookup"><span data-stu-id="fea5c-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="fea5c-172">Aunque la [especificación Swagger 2.0](http://swagger.io/specification) declara que las propiedades `host`, `basePath` y `schemes` son opcionales, el documento Swagger 2.0 **DEBE** contener esas propiedades; en caso contrario, no se importará.</span><span class="sxs-lookup"><span data-stu-id="fea5c-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="fea5c-173">Una vez que se importa la API de hello, hello página de resumen de la API de Hola se muestra en portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![API summary][api-management-imported-api-summary]

<span data-ttu-id="fea5c-175">sección de la API de Hello tiene varias pestañas.</span><span class="sxs-lookup"><span data-stu-id="fea5c-175">hello API section has several tabs.</span></span> <span data-ttu-id="fea5c-176">Hola **resumen** ficha muestra métricas básicas e información sobre Hola API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="fea5c-177">Hola [configuración](api-management-howto-create-apis.md#configure-api-settings) ficha es configuración de hello tooview y editar utilizada para una API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="fea5c-178">Hola [Operations](api-management-howto-add-operations.md) ficha es operaciones hello toomanage usa la API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="fea5c-179">Hola **seguridad** ficha puede ser tooconfigure usa autenticación de puerta de enlace para el servidor back-end de hello mediante autenticación básica o [autenticación de certificado mutua](api-management-howto-mutual-certificates.md)y tooconfigure [ autorización del usuario mediante el uso de OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="fea5c-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="fea5c-180">Hola **problemas** ficha es tooview usado los problemas notificados por los desarrolladores de Hola que usan las API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="fea5c-181">Hola **productos** ficha es productos de hello tooconfigure utilizadas que contienen esta API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="fea5c-182">De forma predeterminada, cada instancia de Administración de API incluye dos productos de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fea5c-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="fea5c-183">**Starter**</span><span class="sxs-lookup"><span data-stu-id="fea5c-183">**Starter**</span></span>
* <span data-ttu-id="fea5c-184">**Sin límite**</span><span class="sxs-lookup"><span data-stu-id="fea5c-184">**Unlimited**</span></span>

<span data-ttu-id="fea5c-185">En este tutorial, Hola API calculadora básica se agregó toohello producto de inicio cuando se importó Hola API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="fea5c-186">En orden toomake llamadas tooan API, los desarrolladores en primer lugar deben suscribirse producto tooa que le da acceso tooit.</span><span class="sxs-lookup"><span data-stu-id="fea5c-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="fea5c-187">Los desarrolladores pueden suscribirse tooproducts en el portal para desarrolladores de Hola o los administradores pueden suscribirse a los desarrolladores tooproducts en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="fea5c-188">Es un administrador como se ha creado instancia de administración de API de Hola Hola pasos anteriores en el tutorial de hello, por lo que ya está suscrito tooevery producto de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fea5c-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="fea5c-189"><a name="call-operation"></a>Llamar a una operación de portal para desarrolladores de Hola</span><span class="sxs-lookup"><span data-stu-id="fea5c-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="fea5c-190">Las operaciones pueden llamarse directamente desde el portal para desarrolladores de hello, que proporciona una manera cómoda de tooview y pruebe las operaciones de Hola de una API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="fea5c-191">En este paso del tutorial, llamará hello básico calculadora API **agrega dos enteros** operación.</span><span class="sxs-lookup"><span data-stu-id="fea5c-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="fea5c-192">Haga clic en **portal para desarrolladores de** desde el menú de Hola Hola parte superior derecha del portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="fea5c-194">Haga clic en **API** desde el menú superior de hello y, a continuación, haga clic en **calculadora básica** toosee Hola operaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="fea5c-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![portal para desarrolladores][api-management-developer-portal-calc-api]

<span data-ttu-id="fea5c-196">Tenga en cuenta las descripciones de ejemplo de Hola y los parámetros que se importaron junto con hello API y operaciones, proporcionar documentación para desarrolladores de Hola que va a utilizar esta operación.</span><span class="sxs-lookup"><span data-stu-id="fea5c-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="fea5c-197">Estas descripciones también pueden agregarse cuando las operaciones se agregan manualmente.</span><span class="sxs-lookup"><span data-stu-id="fea5c-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="fea5c-198">Hola toocall **agrega dos enteros** operación, haga clic en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="fea5c-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Pruébelo][api-management-developer-portal-calc-api-console]

<span data-ttu-id="fea5c-200">Puede especifique algunos valores para parámetros de Hola o mantener los valores predeterminados de hello y, a continuación, haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="fea5c-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="fea5c-202">Después de invoca una operación, el portal para desarrolladores de hello muestra hello **estado de respuesta**, hello **encabezados de respuesta**y cualquier **contenido de la respuesta**.</span><span class="sxs-lookup"><span data-stu-id="fea5c-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Response][api-management-invoke-get-response]

## <span data-ttu-id="fea5c-204"><a name="view-analytics"></a>Visualización de análisis</span><span class="sxs-lookup"><span data-stu-id="fea5c-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="fea5c-205">análisis de tooview de calculadora básica, el portal para desarrolladores de conmutador toohello atrás seleccionando **administrar** desde el menú de Hola Hola parte superior derecha del portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Administrar][api-management-manage-menu]

<span data-ttu-id="fea5c-207">vista predeterminada para el portal para desarrolladores de hello Hello es hello **panel**, lo que proporciona una visión general de la instancia de la administración de API.</span><span class="sxs-lookup"><span data-stu-id="fea5c-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Panel][api-management-dashboard]

<span data-ttu-id="fea5c-209">Al mantener el mouse Hola mouse (ratón) sobre el gráfico de Hola para **calculadora básica** toosee hello las medidas específicas para el uso de Hola de hello API durante un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="fea5c-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="fea5c-210">Si no ve todas las líneas del gráfico, cambie el portal para desarrolladores de toohello back- y realizar algunas llamadas en hello API, espere unos minutos y, a continuación, vuelven a estar toohello panel.</span><span class="sxs-lookup"><span data-stu-id="fea5c-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="fea5c-211">Haga clic en **ver detalles** página de resumen de Hola de tooview de API, incluidas las versiones más grandes de las métricas de muestra de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="fea5c-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Análisis][api-management-mouse-over]

![Resumen][api-management-api-summary-metrics]

<span data-ttu-id="fea5c-214">Para métricas detalladas e informes, haga clic en **análisis** de hello **administración de API** menú de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="fea5c-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Información general][api-management-analytics-overview]

<span data-ttu-id="fea5c-216">Hola **análisis** sección tiene Hola después de cuatro pestañas:</span><span class="sxs-lookup"><span data-stu-id="fea5c-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="fea5c-217">**Un vistazo** proporciona el uso general y las métricas de mantenimiento, así como Hola superior a los desarrolladores, productos más vendidos, las API principales y las operaciones principales.</span><span class="sxs-lookup"><span data-stu-id="fea5c-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="fea5c-218">**Uso** proporciona información detallada de las llamadas de API y del ancho de banda, incluida una representación geográfica.</span><span class="sxs-lookup"><span data-stu-id="fea5c-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="fea5c-219">**Mantenimiento** se centra en los códigos de estado, las tasas de éxito de caché, los tiempos de respuesta y los tiempos de respuesta de la API y del servicio.</span><span class="sxs-lookup"><span data-stu-id="fea5c-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="fea5c-220">**Actividad** proporciona informes que explorar en profundidad de la actividad específica de Hola por el desarrollador, producto, API y operación.</span><span class="sxs-lookup"><span data-stu-id="fea5c-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="fea5c-221"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fea5c-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="fea5c-222">Obtenga información acerca de cómo demasiado[proteger su API con límites de frecuencia](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="fea5c-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
