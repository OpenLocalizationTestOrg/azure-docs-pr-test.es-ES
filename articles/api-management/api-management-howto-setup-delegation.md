---
title: "Delegación de registros de usuario y suscripciones a producto"
description: "Obtenga información acerca de cómo delegar el registro de usuario y la suscripción de producto un tercero en la administración de la API de Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="f3160-103">Delegación de registros de usuario y suscripciones a producto</span><span class="sxs-lookup"><span data-stu-id="f3160-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="f3160-104">La delegación le permite usar su sitio web actual para controlar el inicio de sesión y la suscripción de los desarrolladores, así como sus suscripciones a productos, en contraposición al uso de la funcionalidad integrada en el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="f3160-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="f3160-105">Esto habilita su sitio web como propietario de los datos de usuario para poder realizar la validación de estos pasos de forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="f3160-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="f3160-106"><a name="delegate-signin-up"> </a>Delegación de inicios de sesión y suscripciones de desarrolladores</span><span class="sxs-lookup"><span data-stu-id="f3160-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="f3160-107">Para delegar el inicio de sesión y la suscripción de los desarrolladores a su sitio web actual, deberá crear un extremo especial de delegación en el sitio que funcione como punto de entrada de cualquier solicitud de este tipo que se inicie en el portal para desarrolladores de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="f3160-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="f3160-108">El flujo de trabajo final será el siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3160-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="f3160-109">El desarrollador hace clic en el enlace de inicio de sesión o de suscripción que se encuentra en el portal para desarrolladores de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="f3160-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="f3160-110">El explorador se redirige al extremo de delegación.</span><span class="sxs-lookup"><span data-stu-id="f3160-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="f3160-111">Como respuesta, el extremo de delegación se redirige a la interfaz de usuario o la presenta para pedir al usuario que inicie sesión o se suscriba.</span><span class="sxs-lookup"><span data-stu-id="f3160-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="f3160-112">Una vez conseguido, se redirige de nuevo al usuario a la página del portal para desarrolladores de Administración de API de la que partió.</span><span class="sxs-lookup"><span data-stu-id="f3160-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="f3160-113">Para empezar, configuremos primero Administración de API para que dirija las solicitudes a través del extremo de delegación.</span><span class="sxs-lookup"><span data-stu-id="f3160-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="f3160-114">En el portal para editores de API Management, haga clic en **Seguridad** y, a continuación, haga clic en la pestaña **Delegación**.</span><span class="sxs-lookup"><span data-stu-id="f3160-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="f3160-115">Haga clic en la casilla para activar "Delegar inicio de sesión y suscripción".</span><span class="sxs-lookup"><span data-stu-id="f3160-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Delegation page][api-management-delegation-signin-up]

* <span data-ttu-id="f3160-117">Determine cuál será la dirección URL del extremo especial de delegación y escríbala en el campo **Dirección URL del extremo de delegación** .</span><span class="sxs-lookup"><span data-stu-id="f3160-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="f3160-118">En el campo **Clave de autenticación de delegación** , escriba el secreto que se usará para procesar una firma suministrada para su comprobación con objeto de garantizar que la solicitud procede efectivamente de Administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3160-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="f3160-119">Puede hacer clic en el botón **generar** para que Administración de API genere de forma aleatoria una clave en su lugar.</span><span class="sxs-lookup"><span data-stu-id="f3160-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="f3160-120">Ahora debe crear el **extremo de delegación**.</span><span class="sxs-lookup"><span data-stu-id="f3160-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="f3160-121">Este tiene que realizar varias acciones:</span><span class="sxs-lookup"><span data-stu-id="f3160-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="f3160-122">Recibir una solicitud de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3160-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="f3160-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL de la página de origen}&salt={string}&sig={string}*</span><span class="sxs-lookup"><span data-stu-id="f3160-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="f3160-124">Parámetros de consulta en el caso de inicio de sesión o suscripción:</span><span class="sxs-lookup"><span data-stu-id="f3160-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="f3160-125">**operation**: identifica el tipo de solicitud de delegación del que se trata. Solo puede ser **SignIn** en este caso.</span><span class="sxs-lookup"><span data-stu-id="f3160-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="f3160-126">**returnUrl**: la dirección URL de la página en la que el usuario hizo clic en un vínculo de suscripción o de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f3160-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="f3160-127">**salt**: una cadena salt especial que se usa para procesar un hash de seguridad</span><span class="sxs-lookup"><span data-stu-id="f3160-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="f3160-128">**sig**: un hash de seguridad procesado que se comparará con su propio hash procesado</span><span class="sxs-lookup"><span data-stu-id="f3160-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="f3160-129">Compruebe que la solicitud procede de Administración de API de Azure (opcional, pero especialmente recomendado por motivos de seguridad).</span><span class="sxs-lookup"><span data-stu-id="f3160-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="f3160-130">Procese un hash HMAC-SHA512 de una cadena según los parámetros de consulta **returnUrl** y **salt** ([se proporciona código de ejemplo a continuación]):</span><span class="sxs-lookup"><span data-stu-id="f3160-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="f3160-131">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="f3160-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="f3160-132">Compare el hash procesado anteriormente con el valor del parámetro de consulta **sig** .</span><span class="sxs-lookup"><span data-stu-id="f3160-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="f3160-133">Si los dos hashes coinciden, vaya a paso siguiente; de lo contrario, deniegue la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f3160-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="f3160-134">Compruebe que ha recibido una solicitud para inicio de sesión/suscripción: el parámetro de consulta **operation** se establecerá en "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="f3160-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="f3160-135">Presente al usuario la interfaz de usuario para que inicie sesión o se suscriba.</span><span class="sxs-lookup"><span data-stu-id="f3160-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="f3160-136">Si el usuario se suscribe, hay que crear la cuenta correspondiente en Administración de API.</span><span class="sxs-lookup"><span data-stu-id="f3160-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="f3160-137">[Cree un usuario] con la API de REST de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="f3160-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="f3160-138">Al hacerlo, asegúrese de que el identificador de usuario se establece en el mismo que existe en su almacén de usuario o en un identificador al que pueda realizar el seguimiento.</span><span class="sxs-lookup"><span data-stu-id="f3160-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="f3160-139">Cuando el usuario se autentique correctamente:</span><span class="sxs-lookup"><span data-stu-id="f3160-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="f3160-140">[solicite un token de inicio de sesión único (SSO)] a través de la API de REST de Administración de API</span><span class="sxs-lookup"><span data-stu-id="f3160-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="f3160-141">anexe un parámetro de consulta returnUrl a la URL de SSO que se recibió de la llamada de API anterior:</span><span class="sxs-lookup"><span data-stu-id="f3160-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="f3160-142">por ejemplo, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="f3160-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="f3160-143">redirija al usuario a la URL producida anteriormente</span><span class="sxs-lookup"><span data-stu-id="f3160-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="f3160-144">Además de la operación **SignIn** , también puede realizar la administración de cuentas siguiendo los pasos anteriores y utilizando una de las siguientes operaciones.</span><span class="sxs-lookup"><span data-stu-id="f3160-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="f3160-145">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="f3160-145">**ChangePassword**</span></span>
* <span data-ttu-id="f3160-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="f3160-146">**ChangeProfile**</span></span>
* <span data-ttu-id="f3160-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="f3160-147">**CloseAccount**</span></span>

<span data-ttu-id="f3160-148">Debe pasar los siguientes parámetros de consulta para las operaciones de administración de cuenta.</span><span class="sxs-lookup"><span data-stu-id="f3160-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="f3160-149">**operation**: identifica qué tipo de solicitud de delegación es (ChangePassword, ChangeProfile o CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="f3160-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="f3160-150">**userId**: el identificador de usuario de la cuenta para administrar</span><span class="sxs-lookup"><span data-stu-id="f3160-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="f3160-151">**salt**: una cadena salt especial que se usa para procesar un hash de seguridad</span><span class="sxs-lookup"><span data-stu-id="f3160-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="f3160-152">**sig**: un hash de seguridad procesado que se comparará con su propio hash procesado</span><span class="sxs-lookup"><span data-stu-id="f3160-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="f3160-153"><a name="delegate-product-subscription"> </a>Delegación de suscripciones a productos</span><span class="sxs-lookup"><span data-stu-id="f3160-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="f3160-154">La delegación de una suscripción a productos funciona de forma similar a la delegación de inicio de sesión y suscripción de usuario.</span><span class="sxs-lookup"><span data-stu-id="f3160-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="f3160-155">El flujo de trabajo final sería el siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3160-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="f3160-156">El desarrollador selecciona un producto en el portal para desarrolladores de Administración de API y hace clic en el botón Suscribir.</span><span class="sxs-lookup"><span data-stu-id="f3160-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="f3160-157">El explorador se redirige al extremo de delegación.</span><span class="sxs-lookup"><span data-stu-id="f3160-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="f3160-158">El extremo de delegación realiza los pasos necesarios para la suscripción al producto: esto depende de usted, y puede que implique la redirección a otra página para solicitar información de facturación, la formulación de otras preguntas o simplemente el almacenamiento de la información sin que se requiera ninguna acción del usuario.</span><span class="sxs-lookup"><span data-stu-id="f3160-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="f3160-159">Para habilitar la funcionalidad, en la página **Delegación**, haga clic en **Delegar suscripción de productos**.</span><span class="sxs-lookup"><span data-stu-id="f3160-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="f3160-160">A continuación, asegúrese de que el extremo de delegación realiza las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f3160-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="f3160-161">Recibir una solicitud de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3160-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="f3160-162">*http://www.yourwebsite.com/apimdelegation?operation={operación}&productId={producto al que se suscribe}&userId={usuario que realiza la solicitud}&salt={cadena}&sig={cadena}*</span><span class="sxs-lookup"><span data-stu-id="f3160-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="f3160-163">Parámetros de consulta en el caso de suscripción a producto:</span><span class="sxs-lookup"><span data-stu-id="f3160-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="f3160-164">**operation**: identifica el tipo de solicitud de delegación del que se trata.</span><span class="sxs-lookup"><span data-stu-id="f3160-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="f3160-165">En las solicitudes de suscripción a producto las opciones válidas son:</span><span class="sxs-lookup"><span data-stu-id="f3160-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="f3160-166">"Subscribe": una solicitud para suscribir al usuario a un producto determinado con el id. especificado (consulte más información a continuación).</span><span class="sxs-lookup"><span data-stu-id="f3160-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="f3160-167">"Unsubscribe": una solicitud para cancelar la suscripción de un usuario a un producto.</span><span class="sxs-lookup"><span data-stu-id="f3160-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="f3160-168">"Renew": una solicitud para renovar una suscripción (p. ej., que esté a punto de expirar).</span><span class="sxs-lookup"><span data-stu-id="f3160-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="f3160-169">**productId**: el id. del producto al que el usuario solicitó suscribirse.</span><span class="sxs-lookup"><span data-stu-id="f3160-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="f3160-170">**userId**: el id. del usuario para el que se realiza la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f3160-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="f3160-171">**salt**: una cadena salt especial que se usa para procesar un hash de seguridad</span><span class="sxs-lookup"><span data-stu-id="f3160-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="f3160-172">**sig**: un hash de seguridad procesado que se comparará con su propio hash procesado</span><span class="sxs-lookup"><span data-stu-id="f3160-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="f3160-173">Compruebe que la solicitud procede de Administración de API de Azure (opcional, pero especialmente recomendado por motivos de seguridad).</span><span class="sxs-lookup"><span data-stu-id="f3160-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="f3160-174">Procesar un hash HMAC-SHA512 de una cadena en función de los parámetros de consulta **productId**, **userId** y **salt**:</span><span class="sxs-lookup"><span data-stu-id="f3160-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="f3160-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="f3160-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="f3160-176">Compare el hash procesado anteriormente con el valor del parámetro de consulta **sig** .</span><span class="sxs-lookup"><span data-stu-id="f3160-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="f3160-177">Si los dos hashes coinciden, vaya a paso siguiente; de lo contrario, deniegue la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f3160-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="f3160-178">Realice cualquier procesamiento de la suscripción a producto en función del tipo de operación solicitada en **operation** ; por ejemplo, facturación, preguntas adicionales, etc.</span><span class="sxs-lookup"><span data-stu-id="f3160-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="f3160-179">Tras la correcta suscripción del usuario al producto por su parte, suscriba al usuario al producto de Administración de API [llamando a la API de REST para la suscripción del producto].</span><span class="sxs-lookup"><span data-stu-id="f3160-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="f3160-180"><a name="delegate-example-code"> </a> Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="f3160-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="f3160-181">Estos ejemplos de código muestran cómo aprovechar la *clave de validación de delegación*, que se establece en la pantalla de delegación del portal del publicador para crear un HMAC que se utiliza para validar la firma, probando la validez del valor returnUrl que se ha pasado.</span><span class="sxs-lookup"><span data-stu-id="f3160-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="f3160-182">El mismo código funciona para productId y userId con pequeñas modificaciones.</span><span class="sxs-lookup"><span data-stu-id="f3160-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="f3160-183">**Código C# para generar el hash de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="f3160-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="f3160-184">**Código NodeJS para generar el hash de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="f3160-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="f3160-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3160-185">Next steps</span></span>
<span data-ttu-id="f3160-186">Para obtener más información acerca de la delegación, vea el siguiente vídeo.</span><span class="sxs-lookup"><span data-stu-id="f3160-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="f3160-187">[solicite un token de inicio de sesión único (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="f3160-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="f3160-188">[Cree un usuario]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="f3160-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="f3160-189">[llamando a la API de REST para la suscripción del producto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="f3160-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="f3160-190">[se proporciona código de ejemplo a continuación]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="f3160-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
