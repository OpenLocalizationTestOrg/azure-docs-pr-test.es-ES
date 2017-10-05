---
title: "Azure AD Connect: Autenticación de paso a través - Bloqueo inteligente | Microsoft Docs"
description: "En este artículo se describe cómo la autenticación de paso a través de Azure Active Directory (Azure AD) protege las cuentas locales de ataques por fuerza bruta de contraseñas en la nube."
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
ms.openlocfilehash: c84b2406e6373701c83c509342129bd6d7d4034b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="a39f6-104">Autenticación de paso a través de Azure Active Directory: Bloqueo inteligente</span><span class="sxs-lookup"><span data-stu-id="a39f6-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="a39f6-105">Información general</span><span class="sxs-lookup"><span data-stu-id="a39f6-105">Overview</span></span>

<span data-ttu-id="a39f6-106">Azure AD protege frente a los ataques de contraseña por fuerza bruta e impide que se bloquee a los usuarios originales de sus aplicaciones de Office 365 y SaaS.</span><span class="sxs-lookup"><span data-stu-id="a39f6-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="a39f6-107">Esta capacidad, denominada **Bloqueo inteligente**, se admite cuando se usa la autenticación de paso a través como método de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a39f6-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="a39f6-108">Bloqueo inteligente está habilitado de forma predeterminada para todos los inquilinos y las cuentas de usuario se protegen en todo momento; no es necesario activarlo.</span><span class="sxs-lookup"><span data-stu-id="a39f6-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all the time; there is no need to turn it on.</span></span>

<span data-ttu-id="a39f6-109">Bloqueo inteligente funciona mediante el seguimiento de los errores de inicio de sesión y después de un determinado **Umbral de bloqueo**, a partir de una **Duración del bloqueo**.</span><span class="sxs-lookup"><span data-stu-id="a39f6-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="a39f6-110">Durante la duración del bloqueo se rechazan los intentos de inicio de sesión del atacante.</span><span class="sxs-lookup"><span data-stu-id="a39f6-110">Any sign-in attempts from the attacker during the Lockout Duration are rejected.</span></span> <span data-ttu-id="a39f6-111">Si el ataque continúa, los errores de inicio de sesión siguientes después de que finalice la duración del bloqueo generan una duración del bloqueo más larga.</span><span class="sxs-lookup"><span data-stu-id="a39f6-111">If the attack continues, the subsequent failed sign-in attempts after the Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="a39f6-112">El valor predeterminado del umbral de bloqueo es de 10 intentos incorrectos y la duración del bloqueo predeterminada es de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="a39f6-112">The default Lockout Threshold is 10 failed attempts, and the default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="a39f6-113">Bloqueo inteligente también distingue entre inicios de sesión de usuarios originales y de los atacantes, y solo bloquea a los atacantes en la mayoría de los casos.</span><span class="sxs-lookup"><span data-stu-id="a39f6-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out the attackers in most cases.</span></span> <span data-ttu-id="a39f6-114">Esta funcionalidad impide que los atacantes bloqueen de forma malintencionada a los usuarios originales.</span><span class="sxs-lookup"><span data-stu-id="a39f6-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="a39f6-115">Se usa el comportamiento de inicio de sesión pasado, los exploradores y dispositivos de los usuarios, y otras señales para distinguir entre atacantes y usuarios originales.</span><span class="sxs-lookup"><span data-stu-id="a39f6-115">We use past sign-in behavior, users’ devices & browsers and other signals to distinguish between genuine users and attackers.</span></span> <span data-ttu-id="a39f6-116">Estamos mejorando constantemente nuestros algoritmos.</span><span class="sxs-lookup"><span data-stu-id="a39f6-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="a39f6-117">Como la autenticación de paso a través reenvía las solicitudes de validación de contraseñas a la instancia local de Active Directory (AD), tendrá que evitar que los atacantes bloqueen las cuentas de AD de sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="a39f6-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need to prevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="a39f6-118">Como tiene sus propias directivas de bloqueo de cuentas de AD (en concreto, [**Umbral de bloqueo de cuenta**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) y [**Restablecer contador de bloqueo de cuenta después de** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), debe configurar los valores de umbral de bloqueo y duración del bloqueo de Azure AD adecuadamente para filtrar ataques en la nube antes de que lleguen a la instancia local de AD.</span><span class="sxs-lookup"><span data-stu-id="a39f6-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need to configure Azure AD’s Lockout Threshold and Lockout Duration values appropriately to filter out attacks in the cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="a39f6-119">La característica de bloqueo inteligente es gratuita y está _activada_ de forma predeterminada para todos los clientes.</span><span class="sxs-lookup"><span data-stu-id="a39f6-119">The Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="a39f6-120">Sin embargo, la modificación de los valores de Umbral de bloqueo y Duración del bloqueo de Azure AD mediante la API Graph requiere que el inquilino disponga al menos de una licencia de Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="a39f6-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant to have at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="a39f6-121">No se necesita una licencia de Azure AD Premium P2 _por usuario_ para habilitar la característica de bloqueo inteligente con la autenticación de paso a través.</span><span class="sxs-lookup"><span data-stu-id="a39f6-121">You don't need an Azure AD Premium P2 license _per user_ to get the Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="a39f6-122">Para asegurarse de que las cuentas locales de AD de los usuarios están bien protegidas, debe asegurarse de que:</span><span class="sxs-lookup"><span data-stu-id="a39f6-122">To ensure that your users’ on-premises AD accounts are well protected, you need to ensure that:</span></span>

1.  <span data-ttu-id="a39f6-123">El umbral de bloqueo de Azure AD es _menos_ que el umbral de bloqueo de cuentas de AD.</span><span class="sxs-lookup"><span data-stu-id="a39f6-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="a39f6-124">Se recomienda establecer los valores de modo que el umbral de bloqueo de cuentas de AD sea al menos dos o tres veces el umbral de bloqueo de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a39f6-124">We recommend that you set the values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="a39f6-125">La duración del bloqueo de Azure AD (representada en segundos) es _mayor_ que el valor de Restablecer el bloqueo de cuenta después de AD de (representado en minutos).</span><span class="sxs-lookup"><span data-stu-id="a39f6-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="a39f6-126">Comprobar las directivas de bloqueo de cuentas de AD</span><span class="sxs-lookup"><span data-stu-id="a39f6-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="a39f6-127">Use las siguientes instrucciones para comprobar las directivas de bloqueo de cuentas de AD:</span><span class="sxs-lookup"><span data-stu-id="a39f6-127">Use the following instructions to verify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="a39f6-128">Abra las herramientas de administración de directivas de grupo.</span><span class="sxs-lookup"><span data-stu-id="a39f6-128">Open the Group Policy Management tool.</span></span>
2.  <span data-ttu-id="a39f6-129">Edite la directiva de grupo que se aplica a todos los usuarios, por ejemplo, la directiva de dominio predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a39f6-129">Edit the group policy that is applied to all users, for example, the Default Domain Policy.</span></span>
3.  <span data-ttu-id="a39f6-130">Vaya a Configuración del equipo\Directivas\Configuración de Windows\Configuración de seguridad\Directivas de cuenta\Directiva de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="a39f6-130">Navigate to Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="a39f6-131">Compruebe los valores de Umbral de bloqueo de cuenta y Restablecer contador de bloqueo de cuenta después de.</span><span class="sxs-lookup"><span data-stu-id="a39f6-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Directivas de bloqueo de cuentas de AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-the-graph-api-to-manage-your-tenants-smart-lockout-values"></a><span data-ttu-id="a39f6-133">Usar la API de Graph para administrar los valores de Bloqueo inteligente del inquilino</span><span class="sxs-lookup"><span data-stu-id="a39f6-133">Use the Graph API to manage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="a39f6-134">Modificar los valores de umbral de bloqueo y duración del bloqueo de Azure AD mediante la API de Graph es una característica de Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="a39f6-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="a39f6-135">También debe ser un administrador global en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="a39f6-135">It also needs you to be a Global Administrator on your tenant.</span></span>

<span data-ttu-id="a39f6-136">Puede usar [Explorador de gráficos](https://developer.microsoft.com/graph/graph-explorer) para leer, establecer y actualizar los valores de bloqueo inteligente de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a39f6-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="a39f6-137">Pero también puede realizar estas operaciones mediante programación.</span><span class="sxs-lookup"><span data-stu-id="a39f6-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="a39f6-138">Leer valores de bloqueo de inteligente</span><span class="sxs-lookup"><span data-stu-id="a39f6-138">Read Smart Lockout values</span></span>

<span data-ttu-id="a39f6-139">Siga estos pasos para leer los valores de bloqueo inteligente del inquilino:</span><span class="sxs-lookup"><span data-stu-id="a39f6-139">Follow these steps to read your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="a39f6-140">Inicie sesión en el Explorador de gráficos como un administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="a39f6-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a39f6-141">Si se le solicita, conceda acceso para los permisos solicitados.</span><span class="sxs-lookup"><span data-stu-id="a39f6-141">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="a39f6-142">Haga clic en "Modificar permisos" y seleccione el permiso "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="a39f6-142">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a39f6-143">Configure la solicitud de la API de Graph como sigue: establezca la versión en "BETA", el tipo de solicitud en "GET" y la dirección URL en `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="a39f6-143">Configure the Graph API request as follows: Set version to “BETA”, request type to “GET” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="a39f6-144">Haga clic en "Ejecutar consulta" para ver los valores de bloqueo inteligente del inquilino.</span><span class="sxs-lookup"><span data-stu-id="a39f6-144">Click "Run Query" to see your tenant's Smart Lockout values.</span></span> <span data-ttu-id="a39f6-145">Si no ha establecido los valores del inquilino antes, verá un conjunto vacío.</span><span class="sxs-lookup"><span data-stu-id="a39f6-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="a39f6-146">Establecer valores de bloqueo de inteligente</span><span class="sxs-lookup"><span data-stu-id="a39f6-146">Set Smart Lockout values</span></span>

<span data-ttu-id="a39f6-147">Siga estos pasos para establecer los valores de bloqueo inteligente del inquilino (solo para la primera vez):</span><span class="sxs-lookup"><span data-stu-id="a39f6-147">Follow these steps to set your tenant’s Smart Lockout values (for the first time only):</span></span>

1. <span data-ttu-id="a39f6-148">Inicie sesión en el Explorador de gráficos como un administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="a39f6-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a39f6-149">Si se le solicita, conceda acceso para los permisos solicitados.</span><span class="sxs-lookup"><span data-stu-id="a39f6-149">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="a39f6-150">Haga clic en "Modificar permisos" y seleccione el permiso "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="a39f6-150">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a39f6-151">Configure la solicitud de la API de Graph como sigue: establezca la versión en "BETA", el tipo de solicitud en "POST" y la dirección URL en `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="a39f6-151">Configure the Graph API request as follows: Set version to “BETA”, request type to “POST” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="a39f6-152">Copie y pegue la siguiente solicitud de JSON en el campo "Cuerpo de la solicitud".</span><span class="sxs-lookup"><span data-stu-id="a39f6-152">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="a39f6-153">Cambie los valores de bloqueo inteligente según corresponda y use un GUID aleatorio para `templateId`.</span><span class="sxs-lookup"><span data-stu-id="a39f6-153">Change the Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="a39f6-154">Haga clic en "Ejecutar consulta" para establecer los valores de bloqueo inteligente del inquilino.</span><span class="sxs-lookup"><span data-stu-id="a39f6-154">Click "Run Query" to set your tenant's Smart Lockout values.</span></span>

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
><span data-ttu-id="a39f6-155">Si no los está usando, puede dejar los valores **BannedPasswordList** y **EnableBannedPasswordCheck** como vacío ("") y "false" respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a39f6-155">If you are not using them, you can leave the **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="a39f6-156">Compruebe que ha establecido correctamente los valores de bloqueo inteligente del inquilino mediante [estos pasos](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="a39f6-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="a39f6-157">Actualizar los valores de bloqueo de inteligente</span><span class="sxs-lookup"><span data-stu-id="a39f6-157">Update Smart Lockout values</span></span>

<span data-ttu-id="a39f6-158">Siga estos pasos para actualizar los valores de bloqueo inteligente del inquilino (si ya los ha configurado antes):</span><span class="sxs-lookup"><span data-stu-id="a39f6-158">Follow these steps to update your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="a39f6-159">Inicie sesión en el Explorador de gráficos como un administrador global del inquilino.</span><span class="sxs-lookup"><span data-stu-id="a39f6-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a39f6-160">Si se le solicita, conceda acceso para los permisos solicitados.</span><span class="sxs-lookup"><span data-stu-id="a39f6-160">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="a39f6-161">Haga clic en "Modificar permisos" y seleccione el permiso "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="a39f6-161">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a39f6-162">[Siga estos pasos para leer los valores de bloqueo inteligente del inquilino](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="a39f6-162">[Follow these steps to read your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="a39f6-163">Copie el valor `id` (GUID) del elemento con "displayName" como "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="a39f6-163">Copy the `id` value (a GUID) of the item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="a39f6-164">Configure la solicitud de la API de Graph como sigue: establezca la versión en "BETA", el tipo de solicitud en "PATCH" y la dirección URL en `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` (use el GUID del Paso 3 para `<id>`).</span><span class="sxs-lookup"><span data-stu-id="a39f6-164">Configure the Graph API request as follows: Set version to “BETA”, request type to “PATCH” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use the GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="a39f6-165">Copie y pegue la siguiente solicitud de JSON en el campo "Cuerpo de la solicitud".</span><span class="sxs-lookup"><span data-stu-id="a39f6-165">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="a39f6-166">Cambie los valores de bloqueo inteligente según corresponda.</span><span class="sxs-lookup"><span data-stu-id="a39f6-166">Change the Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="a39f6-167">Haga clic en "Ejecutar consulta" para actualizar los valores de bloqueo inteligente del inquilino.</span><span class="sxs-lookup"><span data-stu-id="a39f6-167">Click "Run Query" to update your tenant's Smart Lockout values.</span></span>

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

<span data-ttu-id="a39f6-168">Compruebe que ha actualizado correctamente los valores de bloqueo inteligente del inquilino mediante [estos pasos](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="a39f6-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a39f6-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a39f6-169">Next steps</span></span>
- <span data-ttu-id="a39f6-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para rellenar solicitudes de características nuevas.</span><span class="sxs-lookup"><span data-stu-id="a39f6-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
