---
title: "Azure AD Connect: Autenticación de paso a través - Bloqueo inteligente | Microsoft Docs"
description: "Este artículo describe cómo la autenticación de paso a través de Azure Active Directory (Azure AD) protege las cuentas locales de ataques por fuerza bruta de contraseñas en nube de Hola."
services: active-directory
keywords: "Autenticación de paso a través de Azure AD Connect, instalación de Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="60896-104">Autenticación de paso a través de Azure Active Directory: Bloqueo inteligente</span><span class="sxs-lookup"><span data-stu-id="60896-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="60896-105">Información general</span><span class="sxs-lookup"><span data-stu-id="60896-105">Overview</span></span>

<span data-ttu-id="60896-106">Azure AD protege frente a los ataques de contraseña por fuerza bruta e impide que se bloquee a los usuarios originales de sus aplicaciones de Office 365 y SaaS.</span><span class="sxs-lookup"><span data-stu-id="60896-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="60896-107">Esta capacidad, denominada **Bloqueo inteligente**, se admite cuando se usa la autenticación de paso a través como método de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="60896-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="60896-108">Bloqueo inteligente está habilitada de forma predeterminada para todos los inquilinos y se protegen las cuentas de usuario todo el tiempo de hello; No hay ninguna necesidad de tooturn en.</span><span class="sxs-lookup"><span data-stu-id="60896-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="60896-109">Bloqueo inteligente funciona mediante el seguimiento de los errores de inicio de sesión y después de un determinado **Umbral de bloqueo**, a partir de una **Duración del bloqueo**.</span><span class="sxs-lookup"><span data-stu-id="60896-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="60896-110">Se rechazan los intentos de inicio de sesión del atacante Hola durante la duración del bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="60896-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="60896-111">Si continúa el ataque de hello, Hola posteriores Error inicio de sesión intentos de una vez finalizado el Hola duración del bloqueo de resultados de mayor duración de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="60896-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="60896-112">valor predeterminado de Hello umbral de bloqueo es 10 intentos fallidos y predeterminada de hello que duración del bloqueo es de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="60896-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="60896-113">Bloqueo inteligente también distingue entre inicios de sesión de usuarios originales y de los atacantes y sólo bloquea los atacantes hello en la mayoría de los casos.</span><span class="sxs-lookup"><span data-stu-id="60896-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="60896-114">Esta funcionalidad impide que los atacantes bloqueen de forma malintencionada a los usuarios originales.</span><span class="sxs-lookup"><span data-stu-id="60896-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="60896-115">Utilizamos más allá de inicio de sesión de comportamiento, los usuarios dispositivos y exploradores y otro toodistinguish señales entre usuarios originales y a los atacantes.</span><span class="sxs-lookup"><span data-stu-id="60896-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="60896-116">Estamos mejorando constantemente nuestros algoritmos.</span><span class="sxs-lookup"><span data-stu-id="60896-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="60896-117">Dado que este tipo de autenticación se reenvía las solicitudes de validación de contraseña en su Active Directory local (AD), necesita los atacantes tooprevent bloquear cuentas de AD de sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="60896-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="60896-118">Puesto que tiene sus propias directivas de bloqueo de cuentas de AD (específicamente, [ **umbral de bloqueo de cuenta** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) y [ **Restablecer contador de bloqueo de cuenta después de las directivas** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), necesita el umbral de bloqueo de tooconfigure de Azure AD y duración del bloqueo adecuadamente valores toofilter fuera de los ataques de nube de hello antes de alcanzar su local AD.</span><span class="sxs-lookup"><span data-stu-id="60896-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="60896-119">característica de bloqueo inteligente Hello es gratuito y está _en_ de forma predeterminada para todos los clientes.</span><span class="sxs-lookup"><span data-stu-id="60896-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="60896-120">Sin embargo, la modificación del umbral de bloqueo y los valores de duración del bloqueo mediante la API Graph de Azure AD necesita su licencia de inquilino toohave al menos un Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="60896-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="60896-121">No necesita una licencia de Azure AD Premium P2 _por usuario_ característica de bloqueo inteligente de hello tooget con la autenticación de paso a través.</span><span class="sxs-lookup"><span data-stu-id="60896-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="60896-122">tooensure que los usuarios en AD cuentas locales están bien protegidos, deberá tooensure que:</span><span class="sxs-lookup"><span data-stu-id="60896-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="60896-123">El umbral de bloqueo de Azure AD es _menos_ que el umbral de bloqueo de cuentas de AD.</span><span class="sxs-lookup"><span data-stu-id="60896-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="60896-124">Se recomienda establecer valores de hello tal que el umbral de bloqueo de cuentas de AD es al menos dos o tres veces el umbral de bloqueo de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60896-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="60896-125">La duración del bloqueo de Azure AD (representada en segundos) es _mayor_ que el valor de Restablecer el bloqueo de cuenta después de AD de (representado en minutos).</span><span class="sxs-lookup"><span data-stu-id="60896-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="60896-126">Comprobar las directivas de bloqueo de cuentas de AD</span><span class="sxs-lookup"><span data-stu-id="60896-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="60896-127">Usar hello siguiendo las instrucciones tooverify las directivas de bloqueo de cuentas de AD:</span><span class="sxs-lookup"><span data-stu-id="60896-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="60896-128">Abra la herramienta de administración de directivas de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="60896-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="60896-129">Editar Hola directiva de grupo que es usuarios de tooall aplicado, por ejemplo, hello directiva predeterminada de dominio.</span><span class="sxs-lookup"><span data-stu-id="60896-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="60896-130">Navegue tooComputer Configuration\Policies\Windows Windows\Configuración seguridad\Directivas cuenta\Directiva directiva de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="60896-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="60896-131">Compruebe los valores de Umbral de bloqueo de cuenta y Restablecer contador de bloqueo de cuenta después de.</span><span class="sxs-lookup"><span data-stu-id="60896-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Directivas de bloqueo de cuentas de AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="60896-133">Usar Hola API Graph toomanage valores de bloqueo inteligentes de su inquilino</span><span class="sxs-lookup"><span data-stu-id="60896-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="60896-134">Modificar los valores de umbral de bloqueo y duración del bloqueo de Azure AD mediante la API de Graph es una característica de Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="60896-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="60896-135">También debe toobe un administrador Global en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="60896-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="60896-136">Puede usar [Explorador de gráficos](https://developer.microsoft.com/graph/graph-explorer) tooread, configurar y actualizar valores de bloqueo inteligente de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60896-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="60896-137">Pero también puede realizar estas operaciones mediante programación.</span><span class="sxs-lookup"><span data-stu-id="60896-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="60896-138">Leer valores de bloqueo de inteligente</span><span class="sxs-lookup"><span data-stu-id="60896-138">Read Smart Lockout values</span></span>

<span data-ttu-id="60896-139">Siga estos pasos tooread valores de bloqueo inteligentes de su inquilino:</span><span class="sxs-lookup"><span data-stu-id="60896-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="60896-140">Inicie sesión en el Explorador de gráficos como un administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="60896-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="60896-141">Si se le solicita, conceder acceso para hello permisos solicitados.</span><span class="sxs-lookup"><span data-stu-id="60896-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="60896-142">Haga clic en "Modificar los permisos" y el permiso de "Directory.ReadWrite.All" hello select.</span><span class="sxs-lookup"><span data-stu-id="60896-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="60896-143">Configurar solicitud de API Graph hello como sigue: versión del juego demasiado "BETA", tipo de solicitud demasiado "GET" y la dirección URL demasiado`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="60896-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="60896-144">Haga clic en "Ejecutar consulta" toosee valores de bloqueo inteligentes de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="60896-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="60896-145">Si no ha establecido los valores del inquilino antes, verá un conjunto vacío.</span><span class="sxs-lookup"><span data-stu-id="60896-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="60896-146">Establecer valores de bloqueo de inteligente</span><span class="sxs-lookup"><span data-stu-id="60896-146">Set Smart Lockout values</span></span>

<span data-ttu-id="60896-147">Siga estos pasos tooset valores de bloqueo inteligentes de su inquilino (por Hola sólo la primera vez):</span><span class="sxs-lookup"><span data-stu-id="60896-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="60896-148">Inicie sesión en el Explorador de gráficos como un administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="60896-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="60896-149">Si se le solicita, conceder acceso para hello permisos solicitados.</span><span class="sxs-lookup"><span data-stu-id="60896-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="60896-150">Haga clic en "Modificar los permisos" y el permiso de "Directory.ReadWrite.All" hello select.</span><span class="sxs-lookup"><span data-stu-id="60896-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="60896-151">Configurar solicitud de API Graph hello como sigue: versión del juego demasiado "BETA", tipo de solicitud demasiado "POST" y la dirección URL demasiado`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="60896-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="60896-152">Copie y pegue Hola tras la solicitud JSON en el campo de "Cuerpo de la solicitud" Hola.</span><span class="sxs-lookup"><span data-stu-id="60896-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="60896-153">Cambiar valores de bloqueo inteligente Hola según corresponda y usar un GUID aleatorio para `templateId`.</span><span class="sxs-lookup"><span data-stu-id="60896-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="60896-154">Haga clic en "Ejecutar consulta" tooset valores de bloqueo inteligentes de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="60896-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="60896-155">Si no usas ellos, puede dejar hello **BannedPasswordList** y **EnableBannedPasswordCheck** valores como vacío ("") y "false" respectivamente.</span><span class="sxs-lookup"><span data-stu-id="60896-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="60896-156">Compruebe que ha establecido correctamente los valores de bloqueo inteligente del inquilino mediante [estos pasos](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="60896-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="60896-157">Actualizar los valores de bloqueo de inteligente</span><span class="sxs-lookup"><span data-stu-id="60896-157">Update Smart Lockout values</span></span>

<span data-ttu-id="60896-158">Siga estos pasos tooupdate valores de bloqueo inteligentes de su inquilino (si ya ha configurado antes):</span><span class="sxs-lookup"><span data-stu-id="60896-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="60896-159">Inicie sesión en el Explorador de gráficos como un administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="60896-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="60896-160">Si se le solicita, conceder acceso para hello permisos solicitados.</span><span class="sxs-lookup"><span data-stu-id="60896-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="60896-161">Haga clic en "Modificar los permisos" y el permiso de "Directory.ReadWrite.All" hello select.</span><span class="sxs-lookup"><span data-stu-id="60896-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="60896-162">[Siga estos pasos tooread valores de bloqueo inteligentes de su inquilino](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="60896-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="60896-163">Hola copia `id` valor (GUID) del elemento de hello con "displayName" como "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="60896-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="60896-164">Configurar solicitud de API Graph hello como sigue: establecer la versión "BETA", tipo de solicitud demasiado "Revisión" y la dirección URL demasiado`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -usar Hola GUID en el paso 3 para `<id>`.</span><span class="sxs-lookup"><span data-stu-id="60896-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="60896-165">Copie y pegue Hola tras la solicitud JSON en el campo de "Cuerpo de la solicitud" Hola.</span><span class="sxs-lookup"><span data-stu-id="60896-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="60896-166">Cambiar los valores de bloqueo inteligente Hola según corresponda.</span><span class="sxs-lookup"><span data-stu-id="60896-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="60896-167">Haga clic en "Ejecutar consulta" tooupdate valores de bloqueo inteligentes de su inquilino.</span><span class="sxs-lookup"><span data-stu-id="60896-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="60896-168">Compruebe que ha actualizado correctamente los valores de bloqueo inteligente del inquilino mediante [estos pasos](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="60896-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60896-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60896-169">Next steps</span></span>
- <span data-ttu-id="60896-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.</span><span class="sxs-lookup"><span data-stu-id="60896-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
