---
title: "Azure Active Directory B2C: intercambios de notificaciones de API de REST como validación | Microsoft Docs"
description: Un tema acerca de las directivas personalizadas de Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="631cd-103">Tutorial: Integración de intercambios de notificaciones de API de REST en el recorrido del usuario de Azure AD B2C como validación en entradas de usuario</span><span class="sxs-lookup"><span data-stu-id="631cd-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="631cd-104">Hola Framework de experiencia de identidad (IEF) que subyace a Azure Active Directory B2C (Azure AD B2C) permite Hola identidad developer toointegrate una interacción con la API de REST en un viaje de usuario.</span><span class="sxs-lookup"><span data-stu-id="631cd-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="631cd-105">Al final de Hola de este tutorial, será capaz de toocreate un viaje de usuario de Azure AD B2C que interactúa con los servicios RESTful.</span><span class="sxs-lookup"><span data-stu-id="631cd-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="631cd-106">Hola IEF envía datos en las notificaciones y recibe los datos en las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="631cd-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="631cd-107">interacción de Hello con hello API:</span><span class="sxs-lookup"><span data-stu-id="631cd-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="631cd-108">Se puede diseñar como un intercambio de notificaciones de API de REST, a modo de un perfil de validación, que tiene lugar dentro de un paso de orquestación.</span><span class="sxs-lookup"><span data-stu-id="631cd-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="631cd-109">Normalmente valida la entrada de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="631cd-109">Typically validates input from hello user.</span></span> <span data-ttu-id="631cd-110">Si se rechaza el valor de Hola de usuario de hello, usuario Hola puede intentar volver a tooenter un valor válido con hello oportunidad tooreturn un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="631cd-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="631cd-111">También puede diseñar interacción Hola como un paso de la orquestación.</span><span class="sxs-lookup"><span data-stu-id="631cd-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="631cd-112">Para obtener más información, vea [Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="631cd-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="631cd-113">Por ejemplo de perfil de validación de hello, usaremos viaje de usuario de edición de perfil de hello en archivo de módulo de inicio de hello ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="631cd-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="631cd-114">Podemos comprobar ese nombre hello proporcionado por usuario de hello en el perfil de hello edición no forma parte de una lista de exclusión.</span><span class="sxs-lookup"><span data-stu-id="631cd-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="631cd-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="631cd-115">Prerequisites</span></span>

- <span data-ttu-id="631cd-116">Un toocomplete de Azure AD B2C inquilino configura una cuenta local de sesión-up/inicio de sesión de, como se describe en [Introducción](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="631cd-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="631cd-117">Un punto de conexión de API de REST toointeract con.</span><span class="sxs-lookup"><span data-stu-id="631cd-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="631cd-118">En este tutorial, hemos configurado un sitio de demostración denominado [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) con un servicio de API de REST.</span><span class="sxs-lookup"><span data-stu-id="631cd-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="631cd-119">Paso 1: Preparar la función de la API de REST de Hola</span><span class="sxs-lookup"><span data-stu-id="631cd-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="631cd-120">El programa de instalación de funciones de la API de REST está fuera de ámbito de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="631cd-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="631cd-121">[Las funciones de Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) proporciona un Kit de herramientas de excelente toocreate servicios RESTful en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="631cd-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="631cd-122">Hemos creado una función de Azure que recibe una notificación que espera como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="631cd-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="631cd-123">función Hello valida si existe esta notificación.</span><span class="sxs-lookup"><span data-stu-id="631cd-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="631cd-124">Puede tener acceso a código de la función de Azure completo de hello en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="631cd-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="631cd-125">Hola IEF espera hello `userMessage` devuelve esa función Azure Hola de notificación.</span><span class="sxs-lookup"><span data-stu-id="631cd-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="631cd-126">Esta notificación se presentará como un usuario de toohello cadena si falla la validación de hello, por ejemplo, cuando se devuelve un estado de 409 Conflicto en el anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="631cd-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="631cd-127">Paso 2: Configurar exchange de notificaciones de API de REST de Hola como un perfil técnico en el archivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="631cd-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="631cd-128">Un perfil técnico es la configuración completa de Hola de exchange Hola deseado con hello servicio RESTful.</span><span class="sxs-lookup"><span data-stu-id="631cd-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="631cd-129">Abra el archivo de TrustFrameworkExtensions.xml hello y agregue Hola siguiente fragmento XML dentro de hello `<ClaimsProviders>` elemento.</span><span class="sxs-lookup"><span data-stu-id="631cd-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="631cd-130">Hola continuación de XML, proveedor RESTful `Version=1.0.0.0` se describe como protocolo de Hola.</span><span class="sxs-lookup"><span data-stu-id="631cd-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="631cd-131">Considérelo como función hello que interactúa con el servicio externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="631cd-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="631cd-132">Hola `InputClaims` elemento define notificaciones de Hola que se enviarán desde Hola servicio REST de IEF toohello.</span><span class="sxs-lookup"><span data-stu-id="631cd-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="631cd-133">En este ejemplo, Hola contenido de notificación de hello `givenName` se enviará al servicio REST de toohello como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="631cd-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="631cd-134">En este ejemplo, hello que IEF no espera notificaciones de nuevo.</span><span class="sxs-lookup"><span data-stu-id="631cd-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="631cd-135">En su lugar, se espera una respuesta de servicio REST de Hola y actúa en función de los códigos de estado de Hola que recibe.</span><span class="sxs-lookup"><span data-stu-id="631cd-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="631cd-136">Paso 3: Incluir el intercambio de notificaciones del servicio RESTful de hello en autoafirmadas perfil técnica donde desea toovalidate Hola proporcionados por el usuario</span><span class="sxs-lookup"><span data-stu-id="631cd-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="631cd-137">Hola uso más común del paso de validación de Hola está en la interacción de Hola a un usuario.</span><span class="sxs-lookup"><span data-stu-id="631cd-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="631cd-138">Todas las interacciones donde usuario hello es tooprovide esperado de entrada están *impone automáticamente perfiles técnicos*.</span><span class="sxs-lookup"><span data-stu-id="631cd-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="631cd-139">En este ejemplo, agregaremos perfil de autoservicio Asserted ProfileUpdate de toohello de validación de hello técnica.</span><span class="sxs-lookup"><span data-stu-id="631cd-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="631cd-140">Hola perfil técnica que Hola archivo de directiva de confianza (RP) de la entidad `Profile Edit` usa.</span><span class="sxs-lookup"><span data-stu-id="631cd-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="631cd-141">tooadd Hola notificaciones exchange toohello impuesto automáticamente perfil técnico:</span><span class="sxs-lookup"><span data-stu-id="631cd-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="631cd-142">Abra el archivo TrustFrameworkBase.xml de Hola y busque `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="631cd-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="631cd-143">Revise la configuración de Hola de este perfil técnica.</span><span class="sxs-lookup"><span data-stu-id="631cd-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="631cd-144">Observe cómo exchange Hola con usuario Hola se define como las notificaciones que se le pide del usuario de hello (notificaciones de entrada) y que se espera de proveedor de hello autoafirmadas (notificaciones de salida).</span><span class="sxs-lookup"><span data-stu-id="631cd-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="631cd-145">Busque `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`; observe que este perfil se invoca como el paso de orquestación n.º 6 de `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="631cd-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="631cd-146">Paso 4: Cargar y probar el archivo de directiva de hello perfil editar RP</span><span class="sxs-lookup"><span data-stu-id="631cd-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="631cd-147">Cargue Hola nueva versión del archivo de TrustFrameworkExtensions.xml Hola.</span><span class="sxs-lookup"><span data-stu-id="631cd-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="631cd-148">Use **ejecutar ahora** perfil de hello tootest editar el archivo de directiva RP.</span><span class="sxs-lookup"><span data-stu-id="631cd-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="631cd-149">Probar la validación de hello proporcionando uno de los nombres existentes hello (por ejemplo, mcvinny) en hello **nombre dado** campo.</span><span class="sxs-lookup"><span data-stu-id="631cd-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="631cd-150">Si todo está configurado correctamente, debería recibir un mensaje que notifica al usuario de Hola que etiqueta de hello Reproductor ya está en uso.</span><span class="sxs-lookup"><span data-stu-id="631cd-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="631cd-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="631cd-151">Next steps</span></span>

[<span data-ttu-id="631cd-152">Modificar Hola perfil Editar usuario toogather adicional información de registro y de los usuarios</span><span class="sxs-lookup"><span data-stu-id="631cd-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="631cd-153">Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación</span><span class="sxs-lookup"><span data-stu-id="631cd-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
