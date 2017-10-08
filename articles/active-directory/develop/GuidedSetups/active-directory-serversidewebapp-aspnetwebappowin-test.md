---
title: "aaaAzure AD v2 ASP.NET Web Server Introducción - prueba | Documentos de Microsoft"
description: "Implementación de inicio de sesión de Microsoft en una solución ASP.NET con una aplicación basada en un explorador web tradicional mediante el estándar OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="43a16-103">Prueba del código</span><span class="sxs-lookup"><span data-stu-id="43a16-103">Test your code</span></span>

<span data-ttu-id="43a16-104">Presione `F5` toorun el proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43a16-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="43a16-105">Hello explorador se abrirá y dirigirle demasiado*http://localhost: {port}* donde verá hello *iniciar sesión con Microsoft* botón.</span><span class="sxs-lookup"><span data-stu-id="43a16-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="43a16-106">Continúe y haga clic en él toosign en.</span><span class="sxs-lookup"><span data-stu-id="43a16-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="43a16-107">Cuando esté listo tootest, use un trabajo o educativa (Azure Active Directory) o un personal (live.com, outlook.com) toosign en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="43a16-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![Ventana Iniciar sesión en Microsoft del explorador](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Ventana Iniciar sesión en Microsoft del explorador](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="43a16-110">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="43a16-110">Expected results</span></span>
<span data-ttu-id="43a16-111">Después de iniciar sesión, usuario de hello es redirigido toohello portada del sitio web que es hello dirección URL HTTPS especificado en la información de registro de aplicación Hola Portal de registro de aplicación de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43a16-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="43a16-112">Esta página muestra ahora *Hola {User}* y una vínculo toosign horizontal y notificaciones de vínculo toosee Hola de un usuario: que es un controlador de autorización de vínculo toohello crean anteriormente.</span><span class="sxs-lookup"><span data-stu-id="43a16-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="43a16-113">Ver notificaciones del usuario</span><span class="sxs-lookup"><span data-stu-id="43a16-113">See user's claims</span></span>
<span data-ttu-id="43a16-114">Seleccione notificaciones del usuario de hello hipervínculo toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="43a16-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="43a16-115">Esto conduce toohello controlador y la vista que solo está disponible toousers que se autentican.</span><span class="sxs-lookup"><span data-stu-id="43a16-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="43a16-116">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="43a16-116">Expected results</span></span>
 <span data-ttu-id="43a16-117">Debería ver una tabla que contiene propiedades básicas de Hola de usuario de hello iniciado:</span><span class="sxs-lookup"><span data-stu-id="43a16-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="43a16-118">Propiedad</span><span class="sxs-lookup"><span data-stu-id="43a16-118">Property</span></span> | <span data-ttu-id="43a16-119">Valor</span><span class="sxs-lookup"><span data-stu-id="43a16-119">Value</span></span> | <span data-ttu-id="43a16-120">Descripción</span><span class="sxs-lookup"><span data-stu-id="43a16-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="43a16-121">Nombre</span><span class="sxs-lookup"><span data-stu-id="43a16-121">Name</span></span> | <span data-ttu-id="43a16-122">{Nombre completo del usuario}</span><span class="sxs-lookup"><span data-stu-id="43a16-122">{User Full Name}</span></span> | <span data-ttu-id="43a16-123">usuario de Hola y el apellido nombre</span><span class="sxs-lookup"><span data-stu-id="43a16-123">hello user’s first and last name</span></span>
|<span data-ttu-id="43a16-124">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="43a16-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="43a16-125">nombre de usuario de Hello usado usuario de hello registrado tooidentify</span><span class="sxs-lookup"><span data-stu-id="43a16-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="43a16-126">Asunto</span><span class="sxs-lookup"><span data-stu-id="43a16-126">Subject</span></span>| <span data-ttu-id="43a16-127">{Firmante}</span><span class="sxs-lookup"><span data-stu-id="43a16-127">{Subject}</span></span>|<span data-ttu-id="43a16-128">Una cadena toouniquely identificar inicio de sesión de usuario de hello en web Hola</span><span class="sxs-lookup"><span data-stu-id="43a16-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="43a16-129">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="43a16-129">Tenant ID</span></span>| <span data-ttu-id="43a16-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="43a16-130">{Guid}</span></span>| <span data-ttu-id="43a16-131">A *guid* toouniquely representan la organización de Azure Active Directory del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="43a16-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="43a16-132">Además, verá una tabla con todas las notificaciones de usuario incluidas en la solicitud de autenticación.</span><span class="sxs-lookup"><span data-stu-id="43a16-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="43a16-133">Para obtener una lista de todas las notificaciones de un token de identificador y una explicación, consulte este [artículo](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Lista de notificaciones en token de identificador").</span><span class="sxs-lookup"><span data-stu-id="43a16-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="43a16-134">Probar el acceso a un método que tiene un atributo *[Authorize]* (opcional)</span><span class="sxs-lookup"><span data-stu-id="43a16-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="43a16-135">En este paso, probará al tener acceso al controlador de autenticado hello como usuario anónimo:</span><span class="sxs-lookup"><span data-stu-id="43a16-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="43a16-136">Seleccione Hola vincular toosign horizontal Hola usuario y el proceso de cierre de sesión de hello completa.</span><span class="sxs-lookup"><span data-stu-id="43a16-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="43a16-137">Ahora en el explorador, escriba http://localhost: {port} / autenticado tooaccess el controlador que está protegido con hello `[Authorize]` atributo</span><span class="sxs-lookup"><span data-stu-id="43a16-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="43a16-138">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="43a16-138">Expected results</span></span>
<span data-ttu-id="43a16-139">Debería recibir el mensaje Hola necesidad de vista de tooauthenticate toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="43a16-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="43a16-140">Información adicional</span><span class="sxs-lookup"><span data-stu-id="43a16-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="43a16-141">Proteger todo el sitio web</span><span class="sxs-lookup"><span data-stu-id="43a16-141">Protect your entire web site</span></span>
<span data-ttu-id="43a16-142">tooprotect todo el sitio web, agregar hello `AuthorizeAttribute` demasiado`GlobalFilters` en `Global.asax` `Application_Start` método:</span><span class="sxs-lookup"><span data-stu-id="43a16-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="43a16-143">**Cómo los usuarios toorestrict toosign únicamente una organización en la aplicación de tooyour**</span><span class="sxs-lookup"><span data-stu-id="43a16-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="43a16-144">De forma predeterminada, las cuentas personales (incluidos outlook.com, live.com y otros), así como cuentas profesionales o educativas de cualquier empresa u organización que se integra con Azure Active Directory pueden iniciar sesión tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="43a16-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="43a16-145">Si desea que su aplicación tooaccept inicios de sesión de sólo una organización de Azure Active Directory, reemplace hello `Tenant` parámetro en *web.config* de `Common` toohello nombre del inquilino de organización de hello: ejemplo, *contoso.onmicrosoft.com*. A continuación, cambiar hello `ValidateIssuer` argumento en su *clase de inicio de OWIN* demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="43a16-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="43a16-146">los usuarios de tooallow de solo una lista de organizaciones específicas, establecer `ValidateIssuer` hello tootrue y uso `ValidIssuers` parámetro toospecify una lista de las organizaciones.</span><span class="sxs-lookup"><span data-stu-id="43a16-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="43a16-147">Otra opción es un método personalizado tooimplement emisores de hello toovalidate mediante el parámetro IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="43a16-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="43a16-148">Para más información acerca de `TokenValidationParameters`, consulte [este](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Artículo de MSDN acerca de TokenValidationParameters") artículo de MSDN.</span><span class="sxs-lookup"><span data-stu-id="43a16-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

