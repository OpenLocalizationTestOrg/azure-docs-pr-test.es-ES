---
title: "Autenticación y autorización con Power BI Embedded"
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
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="cec7a-103">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="cec7a-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="cec7a-104">El servicio Power BI Embedded usa **claves** y **tokens de aplicación** para la autenticación y la autorización en lugar de la autenticación explícita de usuario final.</span><span class="sxs-lookup"><span data-stu-id="cec7a-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="cec7a-105">En este modelo, la aplicación, la aplicación administra la autenticación y la autorización de sus usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="cec7a-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="cec7a-106">Si es necesario, la aplicación crea y envía los tokens de aplicación que indican a nuestro servicio que presente el informe solicitado.</span><span class="sxs-lookup"><span data-stu-id="cec7a-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span></span> <span data-ttu-id="cec7a-107">En este diseño no es necesario que la aplicación use Azure Active Directory para la autenticación y la autorización de usuarios, aunque puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="cec7a-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-to-authenticate"></a><span data-ttu-id="cec7a-108">Dos modos de autenticación</span><span class="sxs-lookup"><span data-stu-id="cec7a-108">Two ways to authenticate</span></span>

<span data-ttu-id="cec7a-109">**Clave**: puede usar claves para todas las llamadas de API de REST de Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="cec7a-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="cec7a-110">Las claves pueden encontrarse en **Azure portal** haciendo clic en **Toda la configuración** y, luego, en **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="cec7a-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="cec7a-111">Debe tratar siempre la clave como si fuese una contraseña.</span><span class="sxs-lookup"><span data-stu-id="cec7a-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="cec7a-112">Estas claves tienen permisos para llamar a cualquier API de REST en una colección de área de trabajo determinada.</span><span class="sxs-lookup"><span data-stu-id="cec7a-112">These keys have permissions to make any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="cec7a-113">Para utilizar una clave en una llamada de REST, agregue el siguiente encabezado de autorización:</span><span class="sxs-lookup"><span data-stu-id="cec7a-113">To use a key on a REST call, add the following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="cec7a-114">**Token de aplicación** : los tokens de aplicación se utilizan para todas las solicitudes de inserción.</span><span class="sxs-lookup"><span data-stu-id="cec7a-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="cec7a-115">Están diseñados para ejecutarse en el lado del cliente, por lo que están restringidas a un único informe y se recomienda establecer un tiempo de expiración.</span><span class="sxs-lookup"><span data-stu-id="cec7a-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span></span>

<span data-ttu-id="cec7a-116">Los tokens de aplicación son un JWT (JSON Web Token) que está firmado por una de sus claves.</span><span class="sxs-lookup"><span data-stu-id="cec7a-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="cec7a-117">El token de la aplicación puede contener las siguientes notificaciones:</span><span class="sxs-lookup"><span data-stu-id="cec7a-117">Your app token can contain the following claims:</span></span>

| <span data-ttu-id="cec7a-118">Notificación</span><span class="sxs-lookup"><span data-stu-id="cec7a-118">Claim</span></span> | <span data-ttu-id="cec7a-119">Description</span><span class="sxs-lookup"><span data-stu-id="cec7a-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cec7a-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="cec7a-120">**ver**</span></span> |<span data-ttu-id="cec7a-121">La versión del token de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cec7a-121">The version of the app token.</span></span> <span data-ttu-id="cec7a-122">La versión actual es 0.2.0.</span><span class="sxs-lookup"><span data-stu-id="cec7a-122">0.2.0 is the current version.</span></span> |
| <span data-ttu-id="cec7a-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="cec7a-123">**aud**</span></span> |<span data-ttu-id="cec7a-124">El destinatario previsto del token.</span><span class="sxs-lookup"><span data-stu-id="cec7a-124">The intended recipient of the token.</span></span> <span data-ttu-id="cec7a-125">Para usar Power BI Embedded: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="cec7a-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="cec7a-126">**iss**</span><span class="sxs-lookup"><span data-stu-id="cec7a-126">**iss**</span></span> |<span data-ttu-id="cec7a-127">Una cadena que indica la aplicación que emitió el token.</span><span class="sxs-lookup"><span data-stu-id="cec7a-127">A string indicating the application which issued the token.</span></span> |
| <span data-ttu-id="cec7a-128">**type**</span><span class="sxs-lookup"><span data-stu-id="cec7a-128">**type**</span></span> |<span data-ttu-id="cec7a-129">El tipo de token de aplicación que se está creando.</span><span class="sxs-lookup"><span data-stu-id="cec7a-129">The type of app token which is being created.</span></span> <span data-ttu-id="cec7a-130">El único tipo admitido actualmente es **insertar**.</span><span class="sxs-lookup"><span data-stu-id="cec7a-130">Current the only supported type is **embed**.</span></span> |
| <span data-ttu-id="cec7a-131">**wcn**</span><span class="sxs-lookup"><span data-stu-id="cec7a-131">**wcn**</span></span> |<span data-ttu-id="cec7a-132">El nombre de la colección de área de trabajo para el que se emite el token.</span><span class="sxs-lookup"><span data-stu-id="cec7a-132">Workspace collection name the token is being issued for.</span></span> |
| <span data-ttu-id="cec7a-133">**wid**</span><span class="sxs-lookup"><span data-stu-id="cec7a-133">**wid**</span></span> |<span data-ttu-id="cec7a-134">El id. del área de trabajo para el que se emite el token.</span><span class="sxs-lookup"><span data-stu-id="cec7a-134">Workspace ID the token is being issued for.</span></span> |
| <span data-ttu-id="cec7a-135">**rid**</span><span class="sxs-lookup"><span data-stu-id="cec7a-135">**rid**</span></span> |<span data-ttu-id="cec7a-136">El id. del informe para el que se emite el token.</span><span class="sxs-lookup"><span data-stu-id="cec7a-136">Report ID the token is being issued for.</span></span> |
| <span data-ttu-id="cec7a-137">**username** (opcional)</span><span class="sxs-lookup"><span data-stu-id="cec7a-137">**username** (optional)</span></span> |<span data-ttu-id="cec7a-138">Se utiliza con RLS y es una cadena que ayuda a identificar el usuario cuando se aplican las reglas RLS.</span><span class="sxs-lookup"><span data-stu-id="cec7a-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span></span> |
| <span data-ttu-id="cec7a-139">**roles** (opcional)</span><span class="sxs-lookup"><span data-stu-id="cec7a-139">**roles** (optional)</span></span> |<span data-ttu-id="cec7a-140">Una cadena que contiene los roles que seleccione al aplicar las reglas de seguridad de nivel de fila.</span><span class="sxs-lookup"><span data-stu-id="cec7a-140">A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="cec7a-141">Si se pasa más de un rol, se deben pasar como una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="cec7a-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="cec7a-142">**scp** (opcional)</span><span class="sxs-lookup"><span data-stu-id="cec7a-142">**scp** (optional)</span></span> |<span data-ttu-id="cec7a-143">Cadena que contiene los ámbitos de los permisos.</span><span class="sxs-lookup"><span data-stu-id="cec7a-143">A string containing the permissions scopes.</span></span> <span data-ttu-id="cec7a-144">Si se pasa más de un rol, se deben pasar como una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="cec7a-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="cec7a-145">**exp** (opcional)</span><span class="sxs-lookup"><span data-stu-id="cec7a-145">**exp** (optional)</span></span> |<span data-ttu-id="cec7a-146">Indica la hora a la que caducará el token.</span><span class="sxs-lookup"><span data-stu-id="cec7a-146">Indicates the time in which the token will expire.</span></span> <span data-ttu-id="cec7a-147">Se deben pasar como marcas de tiempo de Unix.</span><span class="sxs-lookup"><span data-stu-id="cec7a-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="cec7a-148">**nbf** (opcional)</span><span class="sxs-lookup"><span data-stu-id="cec7a-148">**nbf** (optional)</span></span> |<span data-ttu-id="cec7a-149">Indica la hora a la que comienza a ser válido el token.</span><span class="sxs-lookup"><span data-stu-id="cec7a-149">Indicates the time in which the token starts being valid.</span></span> <span data-ttu-id="cec7a-150">Se deben pasar como marcas de tiempo de Unix.</span><span class="sxs-lookup"><span data-stu-id="cec7a-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="cec7a-151">Un ejemplo de token de aplicación tendrá este aspecto:</span><span class="sxs-lookup"><span data-stu-id="cec7a-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="cec7a-152">Cuando se descodifica, tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="cec7a-152">When decoded, it will look something like this:</span></span>

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

<span data-ttu-id="cec7a-153">Hay métodos disponibles dentro de los SDK que facilitan la creación de apptokens.</span><span class="sxs-lookup"><span data-stu-id="cec7a-153">There are methods available within the SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="cec7a-154">Por ejemplo, para .NET puede observar la clase [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) y los métodos [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="cec7a-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="cec7a-155">Para el SDK de .NET, puede consultar [Ámbitos](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="cec7a-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="cec7a-156">Ámbitos</span><span class="sxs-lookup"><span data-stu-id="cec7a-156">Scopes</span></span>

<span data-ttu-id="cec7a-157">Si usa tokens de inserción, puede restringir el uso de los recursos a los que proporciona acceso.</span><span class="sxs-lookup"><span data-stu-id="cec7a-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="cec7a-158">Por este motivo, puede generar un token con permisos con ámbito.</span><span class="sxs-lookup"><span data-stu-id="cec7a-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="cec7a-159">Los siguientes son los ámbitos disponibles para Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="cec7a-159">The following are the available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="cec7a-160">Scope</span><span class="sxs-lookup"><span data-stu-id="cec7a-160">Scope</span></span>|<span data-ttu-id="cec7a-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="cec7a-161">Description</span></span>|
|---|---|
|<span data-ttu-id="cec7a-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="cec7a-162">Dataset.Read</span></span>|<span data-ttu-id="cec7a-163">Proporciona permiso para leer el conjunto de datos especificado.</span><span class="sxs-lookup"><span data-stu-id="cec7a-163">Provides permission to read the specified dataset.</span></span>|
|<span data-ttu-id="cec7a-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="cec7a-164">Dataset.Write</span></span>|<span data-ttu-id="cec7a-165">Proporciona permiso para escribir en el conjunto de datos especificado.</span><span class="sxs-lookup"><span data-stu-id="cec7a-165">Provides permission to write to the specified dataset.</span></span>|
|<span data-ttu-id="cec7a-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="cec7a-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="cec7a-167">Proporciona permiso para leer el conjunto de datos especificado y escribir en él.</span><span class="sxs-lookup"><span data-stu-id="cec7a-167">Provides permission to read and write to the specificed dataset.</span></span>|
|<span data-ttu-id="cec7a-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="cec7a-168">Report.Read</span></span>|<span data-ttu-id="cec7a-169">Proporciona permiso para ver el informe especificado.</span><span class="sxs-lookup"><span data-stu-id="cec7a-169">Provides permission to view the specified report.</span></span>|
|<span data-ttu-id="cec7a-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="cec7a-170">Report.ReadWrite</span></span>|<span data-ttu-id="cec7a-171">Proporciona permiso para ver y editar el informe especificado.</span><span class="sxs-lookup"><span data-stu-id="cec7a-171">Provides permission to view and edit the specified report.</span></span>|
|<span data-ttu-id="cec7a-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="cec7a-172">Workspace.Report.Create</span></span>|<span data-ttu-id="cec7a-173">Proporciona permiso para crear un informe nuevo dentro del área de trabajo especificada.</span><span class="sxs-lookup"><span data-stu-id="cec7a-173">Provides permission to create a new report within the specified workspace.</span></span>|
|<span data-ttu-id="cec7a-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="cec7a-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="cec7a-175">Proporciona permiso para clonar un informe existente dentro del área de trabajo especificada.</span><span class="sxs-lookup"><span data-stu-id="cec7a-175">Provides permission to clone an existing report within the specified workspace.</span></span>|

<span data-ttu-id="cec7a-176">Puede suministrar varios ámbitos; para ello, use un espacio entre los ámbitos de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="cec7a-176">You can supply multiple scopes by using a space between the scopes like the following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="cec7a-177">**Notificaciones necesarias: ámbitos**</span><span class="sxs-lookup"><span data-stu-id="cec7a-177">**Required claims - scopes**</span></span>

<span data-ttu-id="cec7a-178">scp: {scopesClaim} scopesClaim puede ser una cadena o una matriz de cadenas, teniendo en cuenta los permisos asociados a los recursos del área de trabajo (Report, Dataset, etc.)</span><span class="sxs-lookup"><span data-stu-id="cec7a-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="cec7a-179">Un token descodificado, como ámbitos definidos, tendría un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="cec7a-179">A decoded token, with scopes defined, would look similar to the following.</span></span>

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

### <a name="operations-and-scopes"></a><span data-ttu-id="cec7a-180">Operaciones y ámbitos</span><span class="sxs-lookup"><span data-stu-id="cec7a-180">Operations and scopes</span></span>

|<span data-ttu-id="cec7a-181">Operación</span><span class="sxs-lookup"><span data-stu-id="cec7a-181">Operation</span></span>|<span data-ttu-id="cec7a-182">Recurso de destino</span><span class="sxs-lookup"><span data-stu-id="cec7a-182">Target resource</span></span>|<span data-ttu-id="cec7a-183">Permisos de token</span><span class="sxs-lookup"><span data-stu-id="cec7a-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="cec7a-184">Crea (en memoria) un informe nuevo basado en un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="cec7a-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="cec7a-185">Dataset</span><span class="sxs-lookup"><span data-stu-id="cec7a-185">Dataset</span></span>|<span data-ttu-id="cec7a-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="cec7a-186">Dataset.Read</span></span>|
|<span data-ttu-id="cec7a-187">Crea (en memoria) un informe nuevo basado en un conjunto de datos y guarda el informe.</span><span class="sxs-lookup"><span data-stu-id="cec7a-187">Create (in-memory) a new report based on a dataset and save the report.</span></span>|<span data-ttu-id="cec7a-188">Dataset</span><span class="sxs-lookup"><span data-stu-id="cec7a-188">Dataset</span></span>|<span data-ttu-id="cec7a-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="cec7a-189">* Dataset.Read</span></span><br><span data-ttu-id="cec7a-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="cec7a-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="cec7a-191">Ve y explora o edite (en memoria) un informe existente.</span><span class="sxs-lookup"><span data-stu-id="cec7a-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="cec7a-192">Report.Read implica Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="cec7a-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="cec7a-193">Con esto no se permitirá que los permisos guarden las modificaciones.</span><span class="sxs-lookup"><span data-stu-id="cec7a-193">This will not allow permissions to save edits.</span></span>|<span data-ttu-id="cec7a-194">Informe</span><span class="sxs-lookup"><span data-stu-id="cec7a-194">Report</span></span>|<span data-ttu-id="cec7a-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="cec7a-195">Report.Read</span></span>|
|<span data-ttu-id="cec7a-196">Edita y guarda un informe existente.</span><span class="sxs-lookup"><span data-stu-id="cec7a-196">Edit and save an existing report.</span></span>|<span data-ttu-id="cec7a-197">Informe</span><span class="sxs-lookup"><span data-stu-id="cec7a-197">Report</span></span>|<span data-ttu-id="cec7a-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="cec7a-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="cec7a-199">Guarda una copie de un informe (Guardar como).</span><span class="sxs-lookup"><span data-stu-id="cec7a-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="cec7a-200">Informe</span><span class="sxs-lookup"><span data-stu-id="cec7a-200">Report</span></span>|<span data-ttu-id="cec7a-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="cec7a-201">* Report.Read</span></span><br><span data-ttu-id="cec7a-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="cec7a-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-the-flow-works"></a><span data-ttu-id="cec7a-203">Funcionamiento del flujo</span><span class="sxs-lookup"><span data-stu-id="cec7a-203">Here's how the flow works</span></span>
1. <span data-ttu-id="cec7a-204">Copie las claves de API a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cec7a-204">Copy the API keys to your application.</span></span> <span data-ttu-id="cec7a-205">Puede obtener las claves en el **Portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="cec7a-205">You can get the keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="cec7a-206">El token impone una notificación y tiene un tiempo de expiración.</span><span class="sxs-lookup"><span data-stu-id="cec7a-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="cec7a-207">El token se firma con las claves de acceso de la API.</span><span class="sxs-lookup"><span data-stu-id="cec7a-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="cec7a-208">El usuario solicita ver un informe.</span><span class="sxs-lookup"><span data-stu-id="cec7a-208">User requests to view a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="cec7a-209">El token se valida con claves de acceso de una API.</span><span class="sxs-lookup"><span data-stu-id="cec7a-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="cec7a-210">Power BI Embedded envía un informe al usuario.</span><span class="sxs-lookup"><span data-stu-id="cec7a-210">Power BI Embedded sends a report to user.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="cec7a-211">Después de que **Power BI Embedded** envíe un informe al usuario, este puede ver el informe en su aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="cec7a-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span></span> <span data-ttu-id="cec7a-212">Por ejemplo, si ha importado el [ejemplo .pbix de análisis de datos de venta](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), la aplicación web de ejemplo tendría el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="cec7a-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="cec7a-213">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="cec7a-213">See Also</span></span>

[<span data-ttu-id="cec7a-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="cec7a-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="cec7a-215">Get started with Microsoft Power BI Embedded sample (Introducción al ejemplo de Microsoft Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="cec7a-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="cec7a-216">Common Microsoft Power BI Embedded scenarios (Escenarios comunes de Microsoft Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="cec7a-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="cec7a-217">Introducción a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="cec7a-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="cec7a-218">Repositorio GIT PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="cec7a-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="cec7a-219">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="cec7a-219">More questions?</span></span> [<span data-ttu-id="cec7a-220">Pruebe la comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="cec7a-220">Try the Power BI Community</span></span>](http://community.powerbi.com/)

