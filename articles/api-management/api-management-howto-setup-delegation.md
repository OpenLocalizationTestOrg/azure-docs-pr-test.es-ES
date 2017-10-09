---
title: "aaaHow toodelegate producto y registro de suscripción del usuario"
description: "Obtenga información acerca de cómo tooa de suscripción de producto y de registro del usuario toodelegate de terceros en la administración de API de Azure."
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
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="cf331-103">La suscripción de producto y de registro de usuario toodelegate</span><span class="sxs-lookup"><span data-stu-id="cf331-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="cf331-104">La delegación permite toouse su sitio Web existente para controlar tooproducts de inicio de sesión-en/sesión-up y suscripción de desarrollador como opone funcionalidad integrada de toousing hello en el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf331-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="cf331-105">Esto permite que los datos de usuario de sitio Web tooown hello y realizar la validación de Hola de estos pasos de una manera personalizada.</span><span class="sxs-lookup"><span data-stu-id="cf331-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="cf331-106"><a name="delegate-signin-up"></a>Delegación de inicios de sesión y suscripciones de desarrolladores</span><span class="sxs-lookup"><span data-stu-id="cf331-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="cf331-107">toodelegate developer tooyour de inicio de sesión y suscripción a un sitio Web existente que deberá toocreate un punto de conexión de delegación especial en el sitio que actúa como Hola punto de entrada para cualquiera de esas solicitudes iniciada desde el portal para desarrolladores de administración de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf331-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="cf331-108">flujo de trabajo de Hello final será la siguiente:</span><span class="sxs-lookup"><span data-stu-id="cf331-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="cf331-109">Desarrollador hace clic en el vínculo de inicio de sesión o regístrese hello en hello portal de administración de API para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="cf331-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="cf331-110">Browser es el punto de conexión de toohello redirigida delegación</span><span class="sxs-lookup"><span data-stu-id="cf331-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="cf331-111">Punto de conexión de la delegación de vuelta redirige tooor presenta interfaz de usuario que se pregunta usuario toosign en o inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="cf331-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="cf331-112">Si se ejecuta correctamente, el usuario de hello es página de portal redirigida toohello back-administración de API para desarrolladores que inició desde</span><span class="sxs-lookup"><span data-stu-id="cf331-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="cf331-113">toobegin, vamos a primera tooroute de administración de API de instalación solicita a través de su punto de conexión de la delegación.</span><span class="sxs-lookup"><span data-stu-id="cf331-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="cf331-114">En el portal para desarrolladores de administración de API hello, haga clic en **seguridad** y, a continuación, haga clic en hello **delegación** ficha. Haga clic en tooenable de casilla de verificación de hello 'Delegate inicio de sesión & inicio de sesión'.</span><span class="sxs-lookup"><span data-stu-id="cf331-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Delegation page][api-management-delegation-signin-up]

* <span data-ttu-id="cf331-116">Decidir cómo se pueden y escríbala de nuevo en Hola Hola URL de su punto de conexión de delegación especial **dirección URL del extremo de delegación** campo.</span><span class="sxs-lookup"><span data-stu-id="cf331-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="cf331-117">Dentro de hello **clave de autenticación de delegación** campo Escriba un secreto que será usado toocompute un tooyou firma proporcionado para comprobación tooensure que Hola solicitud procede realmente de administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf331-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="cf331-118">Puede hacer clic en hello **generar** botón toohave API Managemnet generar de forma aleatoria una clave para usted.</span><span class="sxs-lookup"><span data-stu-id="cf331-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="cf331-119">Ahora deberá hello toocreate **punto de conexión de delegación**.</span><span class="sxs-lookup"><span data-stu-id="cf331-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="cf331-120">Tiene una serie de acciones tooperform:</span><span class="sxs-lookup"><span data-stu-id="cf331-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="cf331-121">Recibe una solicitud en hello siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="cf331-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="cf331-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&amp;returnUrl={URL de la página de origen}&amp;salt={string}&amp;sig={string}*</span><span class="sxs-lookup"><span data-stu-id="cf331-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="cf331-123">Parámetros de consulta para el caso de inicio de sesión / registro de hello:</span><span class="sxs-lookup"><span data-stu-id="cf331-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="cf331-124">**operation**: identifica el tipo de solicitud de delegación del que se trata. Solo puede ser **SignIn** en este caso.</span><span class="sxs-lookup"><span data-stu-id="cf331-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="cf331-125">**returnUrl**: Hola dirección URL de página de Hola donde ha hecho clic el usuario de hello en un vínculo de inicio de sesión o regístrese</span><span class="sxs-lookup"><span data-stu-id="cf331-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="cf331-126">**salt**: una cadena salt especial que se usa para procesar un hash de seguridad</span><span class="sxs-lookup"><span data-stu-id="cf331-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="cf331-127">**SIG**: un toobe de hash calculado de seguridad utilizado para la comparación tooyour propio algoritmo hash calculado</span><span class="sxs-lookup"><span data-stu-id="cf331-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="cf331-128">Compruebe que la solicitud Hola procede de administración de API de Azure (opcional, pero muy recomendado para la seguridad)</span><span class="sxs-lookup"><span data-stu-id="cf331-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="cf331-129">Calcular un hash HMAC-SHA512 de una cadena basándose en hello **returnUrl** y **"salt"** parámetros de consulta ([código de ejemplo se proporciona a continuación]):</span><span class="sxs-lookup"><span data-stu-id="cf331-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="cf331-130">HMAC(**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="cf331-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="cf331-131">Comparar Hola hash calculado anteriormente toohello valor de hello **sig** parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="cf331-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="cf331-132">Si dos valores de hello coinciden, mueve en toohello siguiente paso, en caso contrario denegar la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf331-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="cf331-133">Comprobar que se recibe una solicitud de inicio de sesión, en/Inicio de sesión y arriba: Hola **operación** demasiado se establecerá el parámetro de consulta "**SignIn**".</span><span class="sxs-lookup"><span data-stu-id="cf331-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="cf331-134">Usuario de hello presente con interfaz de usuario en toosign o regístrese</span><span class="sxs-lookup"><span data-stu-id="cf331-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="cf331-135">Si el usuario de hello es registrarse tiene toocreate una cuenta correspondiente para ellos en administración de API.</span><span class="sxs-lookup"><span data-stu-id="cf331-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="cf331-136">[Crear un usuario] con hello API de REST de administración.</span><span class="sxs-lookup"><span data-stu-id="cf331-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="cf331-137">Al hacerlo, asegúrese de establecer toohello de Id. de usuario de hello mismo está en el almacén de usuario o identificador tooan que puede realizar un seguimiento de.</span><span class="sxs-lookup"><span data-stu-id="cf331-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="cf331-138">Cuando el usuario de Hola se autentica correctamente:</span><span class="sxs-lookup"><span data-stu-id="cf331-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="cf331-139">[solicitar un token de inicio de sesión único (SSO)] a través de hello API de REST de administración</span><span class="sxs-lookup"><span data-stu-id="cf331-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="cf331-140">anexe un parámetro de consulta returnUrl toohello dirección URL de SSO que ha recibido de la llamada de API de hello anterior:</span><span class="sxs-lookup"><span data-stu-id="cf331-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="cf331-141">por ejemplo, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="cf331-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="cf331-142">redirigir hello toohello de usuario por encima de la dirección URL generado</span><span class="sxs-lookup"><span data-stu-id="cf331-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="cf331-143">En suma toohello **SignIn** operación, también puede realizar la administración de cuentas siguiendo los pasos anteriores de Hola y utilizando una de las siguientes operaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf331-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="cf331-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="cf331-144">**ChangePassword**</span></span>
* <span data-ttu-id="cf331-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="cf331-145">**ChangeProfile**</span></span>
* <span data-ttu-id="cf331-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="cf331-146">**CloseAccount**</span></span>

<span data-ttu-id="cf331-147">Debe pasar Hola después de parámetros de consulta para las operaciones de administración de cuenta.</span><span class="sxs-lookup"><span data-stu-id="cf331-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="cf331-148">**operation**: identifica qué tipo de solicitud de delegación es (ChangePassword, ChangeProfile o CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="cf331-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="cf331-149">**userId**: Id. de usuario de Hola de hello cuenta toomanage</span><span class="sxs-lookup"><span data-stu-id="cf331-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="cf331-150">**salt**: una cadena salt especial que se usa para procesar un hash de seguridad</span><span class="sxs-lookup"><span data-stu-id="cf331-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="cf331-151">**SIG**: un toobe de hash calculado de seguridad utilizado para la comparación tooyour propio algoritmo hash calculado</span><span class="sxs-lookup"><span data-stu-id="cf331-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="cf331-152"><a name="delegate-product-subscription"></a>Delegación de suscripciones a productos</span><span class="sxs-lookup"><span data-stu-id="cf331-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="cf331-153">Delegar la suscripción del producto funciona de forma similar toodelegating usuario inicio de sesión/vertical.</span><span class="sxs-lookup"><span data-stu-id="cf331-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="cf331-154">flujo de trabajo final Hola sería como sigue:</span><span class="sxs-lookup"><span data-stu-id="cf331-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="cf331-155">Desarrollador selecciona un producto en el portal para desarrolladores de administración de API de Hola y hace clic en el botón de suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="cf331-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="cf331-156">Browser es el punto de conexión de toohello redirigida delegación</span><span class="sxs-lookup"><span data-stu-id="cf331-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="cf331-157">Punto de conexión de delegación sigue los pasos de suscripción de producto requerido: se trata de una tooyou y puede implicar la redirección toorequest tooanother de página información de facturación, hacer preguntas adicionales, o simplemente almacenar información de hello y no requiere ninguna acción del usuario</span><span class="sxs-lookup"><span data-stu-id="cf331-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="cf331-158">funcionalidad de hello tooenable, en hello **delegación** página haga clic en **delegar la suscripción del producto**.</span><span class="sxs-lookup"><span data-stu-id="cf331-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="cf331-159">A continuación, asegúrese de punto de conexión de la delegación de hello realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="cf331-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="cf331-160">Recibe una solicitud en hello siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="cf331-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="cf331-161">*{operación} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {toosubscribe de producto a} & userId = {user realizar solicitud} & "salt" = {cadena} & sig = {cadena}*</span><span class="sxs-lookup"><span data-stu-id="cf331-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="cf331-162">Parámetros de consulta para el caso de suscripción de producto de hello:</span><span class="sxs-lookup"><span data-stu-id="cf331-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="cf331-163">**operation**: identifica el tipo de solicitud de delegación del que se trata.</span><span class="sxs-lookup"><span data-stu-id="cf331-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="cf331-164">Para la suscripción de producto solicitudes hello las opciones válidas son:</span><span class="sxs-lookup"><span data-stu-id="cf331-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="cf331-165">"Suscribirse": un tooa de usuario de solicitud toosubscribe Hola dada del producto con proporciona ID (ver abajo)</span><span class="sxs-lookup"><span data-stu-id="cf331-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="cf331-166">"Unsubscribe": un toounsubscribe un usuario de un producto de solicitud</span><span class="sxs-lookup"><span data-stu-id="cf331-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="cf331-167">"Renovar": un toorenew solicitud una suscripción (por ejemplo, que puede expirar)</span><span class="sxs-lookup"><span data-stu-id="cf331-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="cf331-168">**productId**: Id. de saludo del usuario de Hola de producto de hello solicitado toosubscribe a</span><span class="sxs-lookup"><span data-stu-id="cf331-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="cf331-169">**userId**: Hola Id. de usuario de hello para el que se realiza la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="cf331-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="cf331-170">**salt**: una cadena salt especial que se usa para procesar un hash de seguridad</span><span class="sxs-lookup"><span data-stu-id="cf331-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="cf331-171">**SIG**: un toobe de hash calculado de seguridad utilizado para la comparación tooyour propio algoritmo hash calculado</span><span class="sxs-lookup"><span data-stu-id="cf331-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="cf331-172">Compruebe que la solicitud Hola procede de administración de API de Azure (opcional, pero muy recomendado para la seguridad)</span><span class="sxs-lookup"><span data-stu-id="cf331-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="cf331-173">Calcular un HMAC-SHA512 de una cadena basándose en hello **productId**, **userId** y **"salt"** parámetros de consulta:</span><span class="sxs-lookup"><span data-stu-id="cf331-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="cf331-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="cf331-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="cf331-175">Comparar Hola hash calculado anteriormente toohello valor de hello **sig** parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="cf331-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="cf331-176">Si dos valores de hello coinciden, mueve en toohello siguiente paso, en caso contrario denegar la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf331-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="cf331-177">Realizar cualquier procesamiento de suscripción de producto según el tipo de saludo de la operación solicitada en **operación** -facturación p. ej., más preguntas, etcetera.</span><span class="sxs-lookup"><span data-stu-id="cf331-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="cf331-178">Acerca de la suscripción correctamente toohello producto de usuario de hello en su lado, suscribirse el producto de administración de API de hello usuario toohello por [Hola que realiza la llamada API de REST para la suscripción de producto].</span><span class="sxs-lookup"><span data-stu-id="cf331-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="cf331-179"><a name="delegate-example-code"></a> Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="cf331-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="cf331-180">Estos muestran ejemplos de código cómo hello tootake *clave de validación de delegación*, que se establece en pantalla de delegación de bienvenida del portal para desarrolladores de hello, toocreate un HMAC que es, a continuación, utiliza la firma de hello toovalidate, probar la validez de Hola de Hola returnUrl pasado.</span><span class="sxs-lookup"><span data-stu-id="cf331-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="cf331-181">Hola mismo código funciona para productId hello y userId con ligeras modificaciones.</span><span class="sxs-lookup"><span data-stu-id="cf331-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="cf331-182">**C# código toogenerate hash returnUrl**</span><span class="sxs-lookup"><span data-stu-id="cf331-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="cf331-183">**NodeJS código hash de toogenerate de returnUrl**</span><span class="sxs-lookup"><span data-stu-id="cf331-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="cf331-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf331-184">Next steps</span></span>
<span data-ttu-id="cf331-185">Para obtener más información sobre la delegación, vea Hola después de vídeo.</span><span class="sxs-lookup"><span data-stu-id="cf331-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[solicitar un token de inicio de sesión único (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[Cree un usuario]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[Hola que realiza la llamada API de REST para la suscripción de producto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[código de ejemplo se proporciona a continuación]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
