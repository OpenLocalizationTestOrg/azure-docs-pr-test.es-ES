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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="8f6ee-103">Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación</span><span class="sxs-lookup"><span data-stu-id="8f6ee-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="8f6ee-104">El marco de experiencia de identidad (IEF) subyacente a Azure Active Directory B2C (Azure AD B2C) permite al desarrollador de identidades integrar una interacción con una API de RESTful en un recorrido del usuario.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="8f6ee-105">Al final de este tutorial podrá crear un recorrido del usuario de Azure AD B2C que interactúe con servicios RESTful.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="8f6ee-106">El IEF envía datos en notificaciones y recibe los datos en notificaciones.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="8f6ee-107">El intercambio de notificaciones de la API de REST:</span><span class="sxs-lookup"><span data-stu-id="8f6ee-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="8f6ee-108">Puede diseñarse como un paso de orquestación.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="8f6ee-109">Puede desencadenar una acción externa.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-109">Can trigger an external action.</span></span> <span data-ttu-id="8f6ee-110">Por ejemplo, puede registrar un evento en una base de datos externa.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="8f6ee-111">Puede usarse para capturar un valor y almacenarlo en la base de datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="8f6ee-112">Puede usar las notificaciones recibidas posteriormente para cambiar el flujo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="8f6ee-113">También puede diseñar la interacción como un perfil de validación.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="8f6ee-114">Para obtener más información, vea [Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como validación en entradas de usuario](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8f6ee-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="8f6ee-115">La situación es que cuando un usuario realiza una edición de perfil, nos gustaría:</span><span class="sxs-lookup"><span data-stu-id="8f6ee-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="8f6ee-116">Buscar al usuario en un sistema externo.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="8f6ee-117">Obtener la ciudad donde está registrado.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="8f6ee-118">Devolver ese atributo como una notificación a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f6ee-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8f6ee-119">Prerequisites</span></span>

- <span data-ttu-id="8f6ee-120">Configuración de un inquilino de Azure AD B2C para completar el registro o inicio de sesión de una cuenta local como se describe en [Introducción](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8f6ee-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="8f6ee-121">Un punto de conexión de API de REST con el que interactuar.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="8f6ee-122">Este tutorial usa como ejemplo un webhook simple de la aplicación de función de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="8f6ee-123">*Recomendado*: realice el [tutorial sobre el intercambio de notificaciones de API de REST como paso de validación](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8f6ee-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="8f6ee-124">Paso 1: Preparación de la función de API de REST</span><span class="sxs-lookup"><span data-stu-id="8f6ee-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="8f6ee-125">La configuración de funciones de la API de REST está fuera del ámbito de este artículo.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="8f6ee-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) proporciona un excelente conjunto de herramientas para crear servicios de RESTful en la nube.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="8f6ee-127">Hemos configurado una función de Azure que recibe una notificación denominada `email` y devuelve la notificación `city` con el valor asignado de `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="8f6ee-128">La función de Azure de ejemplo está en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="8f6ee-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="8f6ee-129">La notificación `userMessage` que devuelve la función de Azure es opcional en este contexto y el IEF la ignorará.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="8f6ee-130">Se podría usar posiblemente como un mensaje transmitido a la aplicación y presentado al usuario posteriormente.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="8f6ee-131">Una aplicación de función de Azure facilita la obtención de la dirección URL de la función, lo que incluye el identificador de la función específica.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="8f6ee-132">En este caso, la dirección URL es: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="8f6ee-133">Puede usarla para realizar pruebas.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="8f6ee-134">Paso 2: Configuración del intercambio de notificaciones de API de RESTful como perfil técnico en el archivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="8f6ee-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="8f6ee-135">Un perfil técnico es la configuración completa del intercambio deseado con el servicio RESTful.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="8f6ee-136">Abra el archivo TrustFrameworkExtensions.xml y agregue el siguiente fragmento de código XML dentro del elemento `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6ee-137">En el siguiente código XML, el proveedor de RESTful `Version=1.0.0.0` se describe como el protocolo.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="8f6ee-138">Considérelo como la función que interactuará con el servicio externo.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="8f6ee-139">El elemento `<InputClaims>` define las notificaciones que se enviarán desde el IEF al servicio REST.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="8f6ee-140">En este ejemplo, el contenido de la notificación `givenName` se enviará al servicio REST como la notificación `email`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="8f6ee-141">El elemento `<OutputClaims>` define las notificaciones que esperará el IEF del servicio REST.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="8f6ee-142">Independientemente del número de notificaciones que se reciban, el IEF solo usa las identificadas aquí.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="8f6ee-143">En este ejemplo, una notificación recibida como `city` se asignará a una notificación del IEF denominada `city`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="8f6ee-144">Paso 3: Adición de la nueva notificación `city` al esquema de su archivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="8f6ee-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="8f6ee-145">La notificación `city` todavía no se ha definido en ninguna parte de nuestro esquema.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="8f6ee-146">Por lo tanto, debe agregar una definición dentro del elemento `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="8f6ee-147">Encontrará dicho elemento al principio del archivo TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="8f6ee-148">Paso 4: Inclusión del intercambio de notificaciones del servicio REST como paso de orquestación en el recorrido del usuario de edición de perfil del archivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="8f6ee-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="8f6ee-149">Agregue un paso al recorrido del usuario de edición de perfil después de que el usuario se haya autenticado (pasos de orquestación del 1 al 4 en el siguiente código XML) y haya proporcionado la información de perfil actualizada (paso 5).</span><span class="sxs-lookup"><span data-stu-id="8f6ee-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="8f6ee-150">Hay muchos casos donde la llamada de API de REST puede usarse como paso de orquestación.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="8f6ee-151">Como tal, se puede usar como actualización a un sistema externo una vez que un usuario haya realizado correctamente una tarea, por ejemplo, el registro por primera vez, o como actualización de perfil para mantener la información sincronizada.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="8f6ee-152">En este caso, se usa para aumentar la información proporcionada a la aplicación después de la edición del perfil.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="8f6ee-153">Copie el código XML del recorrido del usuario de edición de perfil del archivo TrustFrameworkBase.xml en el archivo TrustFrameworkExtensions.xml dentro del elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="8f6ee-154">Después, realice la modificación en el paso 6.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="8f6ee-155">Si el orden no coincide con su versión, asegúrese de insertar el código como paso antes del tipo `SendClaims` de `ClaimsExchange`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="8f6ee-156">El código XML final del recorrido del usuario debe tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="8f6ee-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="8f6ee-157">Paso 5: Adición de la notificación `city` al archivo de directiva de usuario de confianza para que la notificación se envíe a la aplicación</span><span class="sxs-lookup"><span data-stu-id="8f6ee-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="8f6ee-158">Edite el archivo de usuario de confianza (RP) ProfileEdit.xml y modifique el elemento `<TechnicalProfile Id="PolicyProfile">` para agregar lo siguiente: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="8f6ee-159">Después de agregar la nueva notificación, el perfil técnico tendrá el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="8f6ee-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="8f6ee-160">Paso 6: Carga de los cambios y prueba</span><span class="sxs-lookup"><span data-stu-id="8f6ee-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="8f6ee-161">Sobrescriba las versiones existentes de la directiva.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="8f6ee-162">(Opcional) Guarde la versión existente (mediante descarga) del archivo de extensiones antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="8f6ee-163">Para mantener baja la complejidad inicial, se recomienda no cargar varias versiones del archivo de extensiones.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="8f6ee-164">(Opcional) Cambie el nombre de la nueva versión del identificador de directiva del archivo de edición de directiva. Para ello, cambie `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="8f6ee-165">Cargue el archivo de extensiones.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="8f6ee-166">Cargue el archivo de RP de edición de directiva.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="8f6ee-167">Use **Ejecutar ahora** para probar la directiva.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="8f6ee-168">Revise el token devuelto por el IEF a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="8f6ee-169">Si todo está configurado correctamente, el token incluirá la nueva notificación `city`, con el valor `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="8f6ee-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8f6ee-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f6ee-170">Next steps</span></span>

[<span data-ttu-id="8f6ee-171">Uso de una API de REST como paso de validación</span><span class="sxs-lookup"><span data-stu-id="8f6ee-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="8f6ee-172">Modificación de la edición de perfil para recopilar información adicional de sus usuarios</span><span class="sxs-lookup"><span data-stu-id="8f6ee-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
