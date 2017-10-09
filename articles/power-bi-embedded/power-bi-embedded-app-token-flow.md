---
title: aaaAuthenticating y autorizar con Power BI Embedded
description: "Autenticación y autorización con Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="71c5c-103">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="71c5c-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="71c5c-104">Hola servicio Power BI Embedded usa **claves** y **aplicación Tokens** para la autenticación y autorización, en lugar de autenticación explícita del usuario final.</span><span class="sxs-lookup"><span data-stu-id="71c5c-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="71c5c-105">En este modelo, la aplicación, la aplicación administra la autenticación y la autorización de sus usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="71c5c-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="71c5c-106">Cuando sea necesario, la aplicación crea y envía los Tokens de aplicación Hola que indica a nuestro servicio toorender Hola informe solicitado.</span><span class="sxs-lookup"><span data-stu-id="71c5c-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="71c5c-107">Este diseño no requiere la toouse aplicación Azure Active Directory para la autenticación y autorización, aunque puede seguir.</span><span class="sxs-lookup"><span data-stu-id="71c5c-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="71c5c-108">Dos formas tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="71c5c-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="71c5c-109">**Clave**: puede usar claves para todas las llamadas de API de REST de Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="71c5c-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="71c5c-110">Hola claves pueden encontrarse en hello **portal de Azure** haciendo clic en **toda la configuración de** y, a continuación, **las claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="71c5c-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="71c5c-111">Debe tratar siempre la clave como si fuese una contraseña.</span><span class="sxs-lookup"><span data-stu-id="71c5c-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="71c5c-112">Estas claves tienen toomake permisos llamar cualquier API de REST en una colección de área de trabajo determinada.</span><span class="sxs-lookup"><span data-stu-id="71c5c-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="71c5c-113">toouse una clave en una llamada REST, agregue Hola siguiente encabezado de autorización:</span><span class="sxs-lookup"><span data-stu-id="71c5c-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="71c5c-114">**Token de aplicación** : los tokens de aplicación se utilizan para todas las solicitudes de inserción.</span><span class="sxs-lookup"><span data-stu-id="71c5c-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="71c5c-115">Están diseñadas toobe ejecutar de cliente, por lo que están restringidos tooa único informe y sus tooset prácticas recomendada un tiempo de expiración.</span><span class="sxs-lookup"><span data-stu-id="71c5c-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="71c5c-116">Los tokens de aplicación son un JWT (JSON Web Token) que está firmado por una de sus claves.</span><span class="sxs-lookup"><span data-stu-id="71c5c-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="71c5c-117">El token de aplicación puede contener Hola siguientes notificaciones:</span><span class="sxs-lookup"><span data-stu-id="71c5c-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="71c5c-118">Notificación</span><span class="sxs-lookup"><span data-stu-id="71c5c-118">Claim</span></span> | <span data-ttu-id="71c5c-119">Description</span><span class="sxs-lookup"><span data-stu-id="71c5c-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71c5c-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="71c5c-120">**ver**</span></span> |<span data-ttu-id="71c5c-121">versión de Hola de token de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="71c5c-121">hello version of hello app token.</span></span> <span data-ttu-id="71c5c-122">0.2.0 es la versión actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="71c5c-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="71c5c-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="71c5c-123">**aud**</span></span> |<span data-ttu-id="71c5c-124">Hola destinatario del token de Hola.</span><span class="sxs-lookup"><span data-stu-id="71c5c-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="71c5c-125">Para usar Power BI Embedded: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="71c5c-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="71c5c-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="71c5c-126">**iss**</span></span> |<span data-ttu-id="71c5c-127">Una cadena que indica la aplicación hello que Hola token emitido.</span><span class="sxs-lookup"><span data-stu-id="71c5c-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="71c5c-128">**type**</span><span class="sxs-lookup"><span data-stu-id="71c5c-128">**type**</span></span> |<span data-ttu-id="71c5c-129">tipo de Hello del token de aplicación que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="71c5c-129">hello type of app token which is being created.</span></span> <span data-ttu-id="71c5c-130">Tipo de hello solo admitido actual es **incrustar**.</span><span class="sxs-lookup"><span data-stu-id="71c5c-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="71c5c-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="71c5c-131">**wcn**</span></span> |<span data-ttu-id="71c5c-132">Se está emitiendo el token de Hola de nombre de colección de área de trabajo para.</span><span class="sxs-lookup"><span data-stu-id="71c5c-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="71c5c-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="71c5c-133">**wid**</span></span> |<span data-ttu-id="71c5c-134">Se está emitiendo el token de Hola de Id. de área de trabajo para.</span><span class="sxs-lookup"><span data-stu-id="71c5c-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="71c5c-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="71c5c-135">**rid**</span></span> |<span data-ttu-id="71c5c-136">Se está emitiendo el token de Hola de Id. de informe para.</span><span class="sxs-lookup"><span data-stu-id="71c5c-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="71c5c-137">**username** (opcional)</span><span class="sxs-lookup"><span data-stu-id="71c5c-137">**username** (optional)</span></span> |<span data-ttu-id="71c5c-138">Se utiliza con RLS, esto es una cadena que puede ayudar a identificar usuario Hola al aplicar reglas RLS.</span><span class="sxs-lookup"><span data-stu-id="71c5c-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="71c5c-139">**roles** (opcional)</span><span class="sxs-lookup"><span data-stu-id="71c5c-139">**roles** (optional)</span></span> |<span data-ttu-id="71c5c-140">Una cadena que contiene Hola roles tooselect al aplicar las reglas de seguridad de nivel de fila.</span><span class="sxs-lookup"><span data-stu-id="71c5c-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="71c5c-141">Si se pasa más de un rol, se deben pasar como una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="71c5c-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="71c5c-142">**scp** (opcional)</span><span class="sxs-lookup"><span data-stu-id="71c5c-142">**scp** (optional)</span></span> |<span data-ttu-id="71c5c-143">Una cadena que contiene ámbitos de permisos de Hola.</span><span class="sxs-lookup"><span data-stu-id="71c5c-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="71c5c-144">Si se pasa más de un rol, se deben pasar como una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="71c5c-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="71c5c-145">**exp** (opcional)</span><span class="sxs-lookup"><span data-stu-id="71c5c-145">**exp** (optional)</span></span> |<span data-ttu-id="71c5c-146">Indica el tiempo de hello en qué Hola token expirará.</span><span class="sxs-lookup"><span data-stu-id="71c5c-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="71c5c-147">Se deben pasar como marcas de tiempo de Unix.</span><span class="sxs-lookup"><span data-stu-id="71c5c-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="71c5c-148">**nbf** (opcional)</span><span class="sxs-lookup"><span data-stu-id="71c5c-148">**nbf** (optional)</span></span> |<span data-ttu-id="71c5c-149">Indica el tiempo de hello en qué Hola token inicia no es válida.</span><span class="sxs-lookup"><span data-stu-id="71c5c-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="71c5c-150">Se deben pasar como marcas de tiempo de Unix.</span><span class="sxs-lookup"><span data-stu-id="71c5c-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="71c5c-151">Un ejemplo de token de aplicación tendrá este aspecto:</span><span class="sxs-lookup"><span data-stu-id="71c5c-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="71c5c-152">Cuando se descodifica, tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="71c5c-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="71c5c-153">Hay métodos disponibles dentro de hello SDK que facilitan la creación de apptokens.</span><span class="sxs-lookup"><span data-stu-id="71c5c-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="71c5c-154">Por ejemplo, para .NET puede mirar hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) hello y clase [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) métodos.</span><span class="sxs-lookup"><span data-stu-id="71c5c-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="71c5c-155">Para hello .NET SDK, puede remitir demasiado[ámbitos](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="71c5c-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="71c5c-156">Ámbitos</span><span class="sxs-lookup"><span data-stu-id="71c5c-156">Scopes</span></span>

<span data-ttu-id="71c5c-157">Cuando se usa tokens de insertar, puede que desee toorestrict uso de recursos de hello a que ofrecen acceso.</span><span class="sxs-lookup"><span data-stu-id="71c5c-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="71c5c-158">Por este motivo, puede generar un token con permisos con ámbito.</span><span class="sxs-lookup"><span data-stu-id="71c5c-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="71c5c-159">siguiente Hola es Hola dos ámbitos disponibles para Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="71c5c-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="71c5c-160">Scope</span><span class="sxs-lookup"><span data-stu-id="71c5c-160">Scope</span></span>|<span data-ttu-id="71c5c-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="71c5c-161">Description</span></span>|
|---|---|
|<span data-ttu-id="71c5c-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="71c5c-162">Dataset.Read</span></span>|<span data-ttu-id="71c5c-163">Proporciona permiso tooread Hola especifica el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="71c5c-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="71c5c-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="71c5c-164">Dataset.Write</span></span>|<span data-ttu-id="71c5c-165">Proporciona permiso toowrite toohello especificado conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="71c5c-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="71c5c-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="71c5c-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="71c5c-167">Proporciona permiso tooread y escritura toohello especificado conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="71c5c-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="71c5c-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="71c5c-168">Report.Read</span></span>|<span data-ttu-id="71c5c-169">Proporciona permiso tooview Hola especifica el informe.</span><span class="sxs-lookup"><span data-stu-id="71c5c-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="71c5c-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="71c5c-170">Report.ReadWrite</span></span>|<span data-ttu-id="71c5c-171">Proporciona la edición y permiso tooview Hola informe especificado.</span><span class="sxs-lookup"><span data-stu-id="71c5c-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="71c5c-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="71c5c-172">Workspace.Report.Create</span></span>|<span data-ttu-id="71c5c-173">Proporciona permiso toocreate un nuevo informe en hello especificado área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="71c5c-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="71c5c-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="71c5c-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="71c5c-175">Proporciona un informe existente en hello especificado de permiso tooclone área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="71c5c-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="71c5c-176">Puede proporcionar varios ámbitos mediante el uso de un espacio entre los ámbitos de hello como Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="71c5c-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="71c5c-177">**Notificaciones necesarias: ámbitos**</span><span class="sxs-lookup"><span data-stu-id="71c5c-177">**Required claims - scopes**</span></span>

<span data-ttu-id="71c5c-178">SCP: {scopesClaim} scopesClaim puede ser una cadena o una matriz de cadenas, teniendo en cuenta permisos permitidos hello tooworkspace recursos (informe, conjunto de datos, etcetera.)</span><span class="sxs-lookup"><span data-stu-id="71c5c-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="71c5c-179">Un token descodificado, con ámbitos definidos, tendría un aspecto similar a continuación toohello.</span><span class="sxs-lookup"><span data-stu-id="71c5c-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="71c5c-180">Operaciones y ámbitos</span><span class="sxs-lookup"><span data-stu-id="71c5c-180">Operations and scopes</span></span>

|<span data-ttu-id="71c5c-181">Operación</span><span class="sxs-lookup"><span data-stu-id="71c5c-181">Operation</span></span>|<span data-ttu-id="71c5c-182">Recurso de destino</span><span class="sxs-lookup"><span data-stu-id="71c5c-182">Target resource</span></span>|<span data-ttu-id="71c5c-183">Permisos de token</span><span class="sxs-lookup"><span data-stu-id="71c5c-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="71c5c-184">Crea (en memoria) un informe nuevo basado en un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="71c5c-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="71c5c-185">Dataset</span><span class="sxs-lookup"><span data-stu-id="71c5c-185">Dataset</span></span>|<span data-ttu-id="71c5c-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="71c5c-186">Dataset.Read</span></span>|
|<span data-ttu-id="71c5c-187">Crear un nuevo informe basado en un conjunto de datos de (en memoria) y guardar el informe de Hola.</span><span class="sxs-lookup"><span data-stu-id="71c5c-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="71c5c-188">Dataset</span><span class="sxs-lookup"><span data-stu-id="71c5c-188">Dataset</span></span>|<span data-ttu-id="71c5c-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="71c5c-189">* Dataset.Read</span></span><br><span data-ttu-id="71c5c-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="71c5c-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="71c5c-191">Ve y explora o edite (en memoria) un informe existente.</span><span class="sxs-lookup"><span data-stu-id="71c5c-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="71c5c-192">Report.Read implica Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="71c5c-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="71c5c-193">Esto no le permitirá permisos toosave modificaciones.</span><span class="sxs-lookup"><span data-stu-id="71c5c-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="71c5c-194">Informe</span><span class="sxs-lookup"><span data-stu-id="71c5c-194">Report</span></span>|<span data-ttu-id="71c5c-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="71c5c-195">Report.Read</span></span>|
|<span data-ttu-id="71c5c-196">Edita y guarda un informe existente.</span><span class="sxs-lookup"><span data-stu-id="71c5c-196">Edit and save an existing report.</span></span>|<span data-ttu-id="71c5c-197">Informe</span><span class="sxs-lookup"><span data-stu-id="71c5c-197">Report</span></span>|<span data-ttu-id="71c5c-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="71c5c-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="71c5c-199">Guarda una copie de un informe (Guardar como).</span><span class="sxs-lookup"><span data-stu-id="71c5c-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="71c5c-200">Informe</span><span class="sxs-lookup"><span data-stu-id="71c5c-200">Report</span></span>|<span data-ttu-id="71c5c-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="71c5c-201">* Report.Read</span></span><br><span data-ttu-id="71c5c-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="71c5c-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="71c5c-203">Aquí es cómo funciona el flujo de Hola</span><span class="sxs-lookup"><span data-stu-id="71c5c-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="71c5c-204">Copie la aplicación de tooyour de claves de API de hello.</span><span class="sxs-lookup"><span data-stu-id="71c5c-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="71c5c-205">Puede obtener las claves de hello **Portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="71c5c-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="71c5c-206">El token impone una notificación y tiene un tiempo de expiración.</span><span class="sxs-lookup"><span data-stu-id="71c5c-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="71c5c-207">El token se firma con las claves de acceso de la API.</span><span class="sxs-lookup"><span data-stu-id="71c5c-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="71c5c-208">El usuario solicita tooview un informe.</span><span class="sxs-lookup"><span data-stu-id="71c5c-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="71c5c-209">El token se valida con claves de acceso de una API.</span><span class="sxs-lookup"><span data-stu-id="71c5c-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="71c5c-210">Power BI Embedded envía un informe toouser.</span><span class="sxs-lookup"><span data-stu-id="71c5c-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="71c5c-211">Después de **Power BI Embedded** envía un usuario de toohello informes, usuario Hola puede ver el informe de hello en la aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="71c5c-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="71c5c-212">Por ejemplo, si importó hello [ejemplo de análisis de ventas datos PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), aplicación web de ejemplo de Hola sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="71c5c-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="71c5c-213">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="71c5c-213">See Also</span></span>

[<span data-ttu-id="71c5c-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="71c5c-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="71c5c-215">Get started with Microsoft Power BI Embedded sample (Introducción al ejemplo de Microsoft Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="71c5c-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="71c5c-216">Common Microsoft Power BI Embedded scenarios (Escenarios comunes de Microsoft Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="71c5c-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="71c5c-217">Introducción a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="71c5c-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="71c5c-218">Repositorio GIT PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="71c5c-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="71c5c-219">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="71c5c-219">More questions?</span></span> [<span data-ttu-id="71c5c-220">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="71c5c-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

