---
title: "Azure Active Directory B2C: intercambios de notificaciones de API de REST como paso de orquestación | Microsoft Docs"
description: Tema sobre las directivas personalizadas de Azure Active Directory B2C que se integran con una API
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
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="d8719-103">Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación</span><span class="sxs-lookup"><span data-stu-id="d8719-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="d8719-104">Hola Framework de experiencia de identidad (IEF) que subyace a Azure Active Directory B2C (Azure AD B2C) permite Hola identidad developer toointegrate una interacción con la API de REST en un viaje de usuario.</span><span class="sxs-lookup"><span data-stu-id="d8719-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="d8719-105">Al final de Hola de este tutorial, será capaz de toocreate un viaje de usuario de Azure AD B2C que interactúa con los servicios RESTful.</span><span class="sxs-lookup"><span data-stu-id="d8719-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="d8719-106">Hola IEF envía datos en las notificaciones y recibe los datos en las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d8719-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="d8719-107">Hola exchange de notificaciones de API de REST:</span><span class="sxs-lookup"><span data-stu-id="d8719-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="d8719-108">Puede diseñarse como un paso de orquestación.</span><span class="sxs-lookup"><span data-stu-id="d8719-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="d8719-109">Puede desencadenar una acción externa.</span><span class="sxs-lookup"><span data-stu-id="d8719-109">Can trigger an external action.</span></span> <span data-ttu-id="d8719-110">Por ejemplo, puede registrar un evento en una base de datos externa.</span><span class="sxs-lookup"><span data-stu-id="d8719-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="d8719-111">Puede ser toofetch usa un valor y, a continuación, almacenarla en la base de datos de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="d8719-112">Puede usar notificaciones de hello recibido posterior toochange Hola flujo de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="d8719-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="d8719-113">También puede diseñar interacción Hola como un perfil de validación.</span><span class="sxs-lookup"><span data-stu-id="d8719-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="d8719-114">Para obtener más información, vea [Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como validación en entradas de usuario](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d8719-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="d8719-115">escenario de Hello es que cuando un usuario realiza una operación de edición perfil, deseamos:</span><span class="sxs-lookup"><span data-stu-id="d8719-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="d8719-116">Buscar usuario hello en un sistema externo.</span><span class="sxs-lookup"><span data-stu-id="d8719-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="d8719-117">Obtener ciudad Hola donde se registra que el usuario.</span><span class="sxs-lookup"><span data-stu-id="d8719-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="d8719-118">Devolver esa aplicación toohello de atributo como una notificación.</span><span class="sxs-lookup"><span data-stu-id="d8719-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8719-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d8719-119">Prerequisites</span></span>

- <span data-ttu-id="d8719-120">Un toocomplete de Azure AD B2C inquilino configura una cuenta local de sesión-up/inicio de sesión de, como se describe en [Introducción](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d8719-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="d8719-121">Un punto de conexión de API de REST toointeract con.</span><span class="sxs-lookup"><span data-stu-id="d8719-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="d8719-122">Este tutorial usa como ejemplo un webhook simple de la aplicación de función de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8719-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="d8719-123">*Se recomienda*: Hola completa [tutorial de exchange como un paso de validación de notificaciones de la API de REST](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d8719-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="d8719-124">Paso 1: Preparar la función de la API de REST de Hola</span><span class="sxs-lookup"><span data-stu-id="d8719-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="d8719-125">El programa de instalación de funciones de la API de REST está fuera de ámbito de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="d8719-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="d8719-126">[Las funciones de Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) proporciona un Kit de herramientas de excelente toocreate servicios RESTful en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="d8719-127">Hemos configurado con una función de Azure que recibe una notificación que se llama `email`, y, a continuación, devuelve Hola notificación `city` con valor de hello asignado de `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="d8719-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="d8719-128">ejemplo de Hola función Azure está en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="d8719-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="d8719-129">Hola `userMessage` notificación que Hola devueltos de funciones de Azure es opcional en este contexto y hello IEF pasará por alto.</span><span class="sxs-lookup"><span data-stu-id="d8719-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="d8719-130">Potencialmente puede usarlo como un mensaje pasa la aplicación toohello y presenta toohello usuario más adelante.</span><span class="sxs-lookup"><span data-stu-id="d8719-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

<span data-ttu-id="d8719-131">Una aplicación de Azure función hace fácil tooget Hola función URL, que incluye el identificador hello de función específicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="d8719-132">En este caso, es la dirección URL de hello: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="d8719-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="d8719-133">Puede usarla para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="d8719-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="d8719-134">Paso 2: Configurar exchange de notificaciones de API de REST de Hola como un perfil técnico en el archivo TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="d8719-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="d8719-135">Un perfil técnico es la configuración completa de Hola de exchange Hola deseado con hello servicio RESTful.</span><span class="sxs-lookup"><span data-stu-id="d8719-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="d8719-136">Abra el archivo de TrustFrameworkExtensions.xml hello y agregue Hola siguiente fragmento XML dentro de hello `<ClaimsProvider>` elemento.</span><span class="sxs-lookup"><span data-stu-id="d8719-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="d8719-137">Hola continuación de XML, proveedor RESTful `Version=1.0.0.0` se describe como protocolo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="d8719-138">Considérelo como función hello que interactúa con el servicio externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="d8719-139">Hola `<InputClaims>` elemento define notificaciones de Hola que se enviarán desde Hola servicio REST de IEF toohello.</span><span class="sxs-lookup"><span data-stu-id="d8719-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="d8719-140">En este ejemplo, Hola contenido de notificación de hello `givenName` enviarán servicio REST de toohello como notificación de hello `email`.</span><span class="sxs-lookup"><span data-stu-id="d8719-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="d8719-141">Hola `<OutputClaims>` elemento define Hola notificaciones que hello IEF esperará de servicio REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="d8719-142">Independientemente del número de Hola de notificaciones que se reciben, hello IEF utilizará sólo aquellas identificado aquí.</span><span class="sxs-lookup"><span data-stu-id="d8719-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="d8719-143">En este ejemplo, se recibe una notificación como `city` tooan asignada IEF notificación llamará `city`.</span><span class="sxs-lookup"><span data-stu-id="d8719-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="d8719-144">Paso 3: Agregar nueva notificación de hello `city` toohello esquema del archivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="d8719-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="d8719-145">notificación de Hello `city` todavía no está definido en cualquier lugar en el esquema.</span><span class="sxs-lookup"><span data-stu-id="d8719-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="d8719-146">Por lo tanto, agregar una definición de elemento de hello `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="d8719-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="d8719-147">Puede encontrar este elemento al principio de hello del archivo de hello TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="d8719-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="d8719-148">Paso 4: Incluir el intercambio de notificaciones del servicio de REST de Hola como un paso de orquestación en su viaje de usuario de edición de perfil en TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="d8719-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="d8719-149">Agregar un paso de viaje de usuario de edición de perfil toohello, después de haber usuario Hola autenticado (pasos 1 a 4 de orquestación en hello continuación de XML) y usuario de hello ha proporcionado información de perfil de hello actualizado (paso 5).</span><span class="sxs-lookup"><span data-stu-id="d8719-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="d8719-150">Hay muchos casos donde hello llamada API de REST puede usarse como un paso de la orquestación.</span><span class="sxs-lookup"><span data-stu-id="d8719-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="d8719-151">Como un paso de la orquestación, que puede usarse como un sistema externo de tooan de actualización después de que un usuario se haya completado correctamente una tarea como registro por primera vez, o como un perfil de actualización sincronizada la información de tookeep.</span><span class="sxs-lookup"><span data-stu-id="d8719-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="d8719-152">En este caso, es la información de hello tooaugment usado proporcionada toohello aplicación después de editar el perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="d8719-153">Copiar Hola perfil editar código de usuario viaje XML de hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml archivo dentro de hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="d8719-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="d8719-154">A continuación, asegúrese de modificación de hello en el paso 6.</span><span class="sxs-lookup"><span data-stu-id="d8719-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="d8719-155">Si el orden de hello no coincide con su versión, asegúrese de que inserte código de hello como paso Hola antes de Hola `ClaimsExchange` tipo `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="d8719-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="d8719-156">Hello debe ser XML final para viaje de usuario de hello similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d8719-156">hello final XML for hello user journey should look like this:</span></span>

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="d8719-157">Paso 5: Agregar notificación de hello `city` para notificación de Hola se envía la aplicación tooyour de los archivos de directiva de entidad de confianza de tooyour</span><span class="sxs-lookup"><span data-stu-id="d8719-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="d8719-158">Edite el archivo de entidad (RP) de confianza de ProfileEdit.xml y modificar hello `<TechnicalProfile Id="PolicyProfile">` siguiente de elemento tooadd Hola: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="d8719-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="d8719-159">Después de agregar la nueva notificación de hello, perfil técnico hello tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="d8719-159">After you add hello new claim, hello technical profile looks like this:</span></span>

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="d8719-160">Paso 6: Carga de los cambios y prueba</span><span class="sxs-lookup"><span data-stu-id="d8719-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="d8719-161">Sobrescribir las versiones existentes de directiva de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="d8719-162">(Opcional:) Guardar la versión existente de hello (mediante la descarga) del archivo extensiones antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="d8719-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="d8719-163">tookeep Hola inicial complejidad baja, se recomienda que no cargar varias versiones de archivo de las extensiones de hello.</span><span class="sxs-lookup"><span data-stu-id="d8719-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="d8719-164">(Opcional:) Cambiar el nombre de nueva versión de hello de Id. de directiva de Hola para editar archivo de directiva de hello cambiando `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="d8719-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="d8719-165">Cargar archivo de extensiones de hello.</span><span class="sxs-lookup"><span data-stu-id="d8719-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="d8719-166">Cargar archivo de RP de edición de directivas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="d8719-167">Use **ejecutar ahora** tootest directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8719-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="d8719-168">Token de Hola de revisión que Hola IEF devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8719-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="d8719-169">Si todo está configurado correctamente, el token de hello incluirá nueva notificación de hello `city`, con el valor de hello `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="d8719-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="d8719-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8719-170">Next steps</span></span>

[<span data-ttu-id="d8719-171">Uso de una API de REST como paso de validación</span><span class="sxs-lookup"><span data-stu-id="d8719-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="d8719-172">Modificar Hola perfil editar toogather información adicional de los usuarios</span><span class="sxs-lookup"><span data-stu-id="d8719-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
