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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="1dd76-103">Tutorial: Integración de intercambios de notificaciones de API de REST en el recorrido del usuario de Azure AD B2C como validación en entradas de usuario</span><span class="sxs-lookup"><span data-stu-id="1dd76-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="1dd76-104">El marco de experiencia de identidad (IEF) subyacente a Azure Active Directory B2C (Azure AD B2C) permite al desarrollador de identidades integrar una interacción con una API de RESTful en un recorrido del usuario.</span><span class="sxs-lookup"><span data-stu-id="1dd76-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="1dd76-105">Al final de este tutorial podrá crear un recorrido del usuario de Azure AD B2C que interactúe con servicios RESTful.</span><span class="sxs-lookup"><span data-stu-id="1dd76-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="1dd76-106">El IEF envía datos en notificaciones y recibe los datos en notificaciones.</span><span class="sxs-lookup"><span data-stu-id="1dd76-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="1dd76-107">La interacción con la API:</span><span class="sxs-lookup"><span data-stu-id="1dd76-107">The interaction with the API:</span></span>

- <span data-ttu-id="1dd76-108">Se puede diseñar como un intercambio de notificaciones de API de REST, a modo de un perfil de validación, que tiene lugar dentro de un paso de orquestación.</span><span class="sxs-lookup"><span data-stu-id="1dd76-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="1dd76-109">Normalmente valida la entrada del usuario.</span><span class="sxs-lookup"><span data-stu-id="1dd76-109">Typically validates input from the user.</span></span> <span data-ttu-id="1dd76-110">Si se rechaza el valor del usuario, el usuario puede intentar escribir de nuevo un valor válido con la posibilidad de que reciba un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="1dd76-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="1dd76-111">La interacción también se puede diseñar como un paso de orquestación.</span><span class="sxs-lookup"><span data-stu-id="1dd76-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="1dd76-112">Para obtener más información, vea [Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="1dd76-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="1dd76-113">En el ejemplo de perfil de validación, usaremos el recorrido de usuario de edición de perfil del archivo del paquete de inicio ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="1dd76-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="1dd76-114">Podemos comprobar que el nombre proporcionado por el usuario en la edición del perfil no es parte de una lista de exclusión.</span><span class="sxs-lookup"><span data-stu-id="1dd76-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dd76-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1dd76-115">Prerequisites</span></span>

- <span data-ttu-id="1dd76-116">Configuración de un inquilino de Azure AD B2C para completar el registro o inicio de sesión de una cuenta local como se describe en [Introducción](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="1dd76-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="1dd76-117">Un punto de conexión de API de REST con el que interactuar.</span><span class="sxs-lookup"><span data-stu-id="1dd76-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="1dd76-118">En este tutorial, hemos configurado un sitio de demostración denominado [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) con un servicio de API de REST.</span><span class="sxs-lookup"><span data-stu-id="1dd76-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="1dd76-119">Paso 1: Preparación de la función de API de REST</span><span class="sxs-lookup"><span data-stu-id="1dd76-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="1dd76-120">La configuración de funciones de la API de REST está fuera del ámbito de este artículo.</span><span class="sxs-lookup"><span data-stu-id="1dd76-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="1dd76-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) proporciona un excelente conjunto de herramientas para crear servicios de RESTful en la nube.</span><span class="sxs-lookup"><span data-stu-id="1dd76-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="1dd76-122">Hemos creado una función de Azure que recibe una notificación que espera como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="1dd76-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="1dd76-123">La función valida si existe esta notificación.</span><span class="sxs-lookup"><span data-stu-id="1dd76-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="1dd76-124">Puede acceder al código completo de la función de Azure en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="1dd76-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="1dd76-125">El IEF espera la notificación `userMessage` que devuelve la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="1dd76-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="1dd76-126">Esta notificación se le presentará al usuario como una cadena si se produce un error en la validación, por ejemplo, si se devuelve un estado de conflicto 409 en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="1dd76-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="1dd76-127">Paso 2: Configuración del intercambio de notificaciones de API de RESTful como perfil técnico en el archivo TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="1dd76-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="1dd76-128">Un perfil técnico es la configuración completa del intercambio deseado con el servicio RESTful.</span><span class="sxs-lookup"><span data-stu-id="1dd76-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="1dd76-129">Abra el archivo TrustFrameworkExtensions.xml y agregue el siguiente fragmento de código XML dentro del elemento `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="1dd76-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="1dd76-130">En el siguiente código XML, el proveedor de RESTful `Version=1.0.0.0` se describe como el protocolo.</span><span class="sxs-lookup"><span data-stu-id="1dd76-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="1dd76-131">Considérelo como la función que interactuará con el servicio externo.</span><span class="sxs-lookup"><span data-stu-id="1dd76-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="1dd76-132">El elemento `InputClaims` define las notificaciones que se enviarán desde el IEF al servicio REST.</span><span class="sxs-lookup"><span data-stu-id="1dd76-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="1dd76-133">En este ejemplo, el contenido de la notificación `givenName` se enviará al servicio REST como `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="1dd76-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="1dd76-134">En este ejemplo, el IEF no espera que se devuelvan notificaciones.</span><span class="sxs-lookup"><span data-stu-id="1dd76-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="1dd76-135">En su lugar, espera una respuesta del servicio REST y actúa en función de los códigos de estado recibidos.</span><span class="sxs-lookup"><span data-stu-id="1dd76-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="1dd76-136">Paso 3: Inclusión del intercambio de notificaciones del servicio RESTful en un perfil técnico autoafirmado donde quiere validar la entrada del usuario</span><span class="sxs-lookup"><span data-stu-id="1dd76-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="1dd76-137">El uso más común del paso de validación es en la interacción con un usuario.</span><span class="sxs-lookup"><span data-stu-id="1dd76-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="1dd76-138">Todas las interacciones en las que se espera que el usuario proporcione una entrada son *perfiles técnicos autoafirmados*.</span><span class="sxs-lookup"><span data-stu-id="1dd76-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="1dd76-139">En este ejemplo, agregaremos esta validación al perfil técnico Self-Asserted-ProfileUpdate.</span><span class="sxs-lookup"><span data-stu-id="1dd76-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="1dd76-140">Se trata del perfil técnico que usa el archivo de directiva de usuario de confianza (RP) `Profile Edit`.</span><span class="sxs-lookup"><span data-stu-id="1dd76-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="1dd76-141">Para agregar el intercambio de notificaciones al perfil técnico autoafirmado:</span><span class="sxs-lookup"><span data-stu-id="1dd76-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="1dd76-142">Abra el archivo TrustFrameworkBase.xml y busque `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="1dd76-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="1dd76-143">Revise la configuración de este perfil técnico.</span><span class="sxs-lookup"><span data-stu-id="1dd76-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="1dd76-144">Observe cómo el intercambio con el usuario se define como notificaciones que se pedirán al usuario (notificaciones de entrada) y notificaciones que se espera que devuelva el proveedor autoafirmado (notificaciones de salida).</span><span class="sxs-lookup"><span data-stu-id="1dd76-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="1dd76-145">Busque `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`; observe que este perfil se invoca como el paso de orquestación n.º 6 de `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="1dd76-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="1dd76-146">Paso 4: Carga y prueba del archivo de directiva RP de edición de perfil</span><span class="sxs-lookup"><span data-stu-id="1dd76-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="1dd76-147">Cargue la nueva versión del archivo TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="1dd76-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="1dd76-148">Use **Ejecutar ahora** para probar el archivo de directiva RP de edición de perfil.</span><span class="sxs-lookup"><span data-stu-id="1dd76-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="1dd76-149">Para probar la validación, proporcione uno de los nombres existentes (por ejemplo: mcvinny) en el campo **Nombre propio**.</span><span class="sxs-lookup"><span data-stu-id="1dd76-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="1dd76-150">Si todo está configurado correctamente, debería recibir un mensaje que informa al usuario de que la etiqueta player ya está en uso.</span><span class="sxs-lookup"><span data-stu-id="1dd76-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dd76-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1dd76-151">Next steps</span></span>

[<span data-ttu-id="1dd76-152">Modificación de la edición de perfil y el registro de usuario para recopilar información adicional de sus usuarios</span><span class="sxs-lookup"><span data-stu-id="1dd76-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="1dd76-153">Tutorial: Integración de intercambios de notificaciones de API de REST en los recorridos de usuario de Azure AD B2C como un paso de orquestación</span><span class="sxs-lookup"><span data-stu-id="1dd76-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
