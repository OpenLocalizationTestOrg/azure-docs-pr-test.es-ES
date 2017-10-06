---
title: Azure AD SSPR data requirements (Requisitos de datos de SSPR de Azure AD) | Microsoft Docs
description: "Restablecer requisitos de datos para la contraseña de autoservicio de Azure AD y cómo toosatisfy ellos"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="3d09c-103">Implementación del restablecimiento de contraseña sin necesidad de registro del usuario final</span><span class="sxs-lookup"><span data-stu-id="3d09c-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="3d09c-104">La implementación de restablecimiento de contraseña de autoservicio (SSPR) requiere autenticación datos toobe presente.</span><span class="sxs-lookup"><span data-stu-id="3d09c-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="3d09c-105">Algunas organizaciones tienen sus usuarios escribir sus datos de autenticación por sí mismos, pero muchas organizaciones prefieren toosynchronize con los datos existentes en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d09c-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="3d09c-106">Si con el formato correcto datos en el directorio local y configura [Azure AD Connect con configuración rápida](./connect/active-directory-aadconnect-get-started-express.md), que los datos se hacen disponible tooAzure AD y SSPR con requiere ninguna interacción del usuario.</span><span class="sxs-lookup"><span data-stu-id="3d09c-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="3d09c-107">Cualquier número de teléfono debe estar en formato de hello + CountryCode PhoneNumber ejemplo: + 1 4255551234 toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="3d09c-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="3d09c-108">El restablecimiento de contraseña no admite extensiones telefónicas.</span><span class="sxs-lookup"><span data-stu-id="3d09c-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="3d09c-109">Incluso en formato de hello 4255551234 + 1 X 12345, las extensiones se quitan antes de que se realiza la llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d09c-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="3d09c-110">Campos rellenos</span><span class="sxs-lookup"><span data-stu-id="3d09c-110">Fields populated</span></span>

<span data-ttu-id="3d09c-111">Si usa la configuración de predeterminada Hola Hola de Azure AD Connect después de cada asignación se realiza.</span><span class="sxs-lookup"><span data-stu-id="3d09c-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="3d09c-112">AD local</span><span class="sxs-lookup"><span data-stu-id="3d09c-112">On-premises AD</span></span> | <span data-ttu-id="3d09c-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d09c-113">Azure AD</span></span> | <span data-ttu-id="3d09c-114">Información de contacto de Autenticación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d09c-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3d09c-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="3d09c-115">telephoneNumber</span></span> | <span data-ttu-id="3d09c-116">Teléfono del trabajo</span><span class="sxs-lookup"><span data-stu-id="3d09c-116">Office phone</span></span> | <span data-ttu-id="3d09c-117">Teléfono alternativo</span><span class="sxs-lookup"><span data-stu-id="3d09c-117">Alternate phone</span></span> |
| <span data-ttu-id="3d09c-118">mobile</span><span class="sxs-lookup"><span data-stu-id="3d09c-118">mobile</span></span> | <span data-ttu-id="3d09c-119">Teléfono móvil</span><span class="sxs-lookup"><span data-stu-id="3d09c-119">Mobile phone</span></span> | <span data-ttu-id="3d09c-120">Teléfono</span><span class="sxs-lookup"><span data-stu-id="3d09c-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="3d09c-121">Preguntas y respuestas de seguridad</span><span class="sxs-lookup"><span data-stu-id="3d09c-121">Security questions and answers</span></span>

<span data-ttu-id="3d09c-122">Preguntas de seguridad y respuestas se almacenan de forma segura en su inquilino de Azure AD y son solo toousers accesible a través de hello [portal de registro](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="3d09c-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="3d09c-123">Los administradores no se vea o modifique contenido Hola de otro preguntas de los usuarios y respuestas.</span><span class="sxs-lookup"><span data-stu-id="3d09c-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="3d09c-124">Qué ocurre cuando se registra un usuario</span><span class="sxs-lookup"><span data-stu-id="3d09c-124">What happens when a user registers</span></span>

<span data-ttu-id="3d09c-125">Cuando un usuario se registra, página de registro de hello establece Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="3d09c-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="3d09c-126">Teléfono de autenticación</span><span class="sxs-lookup"><span data-stu-id="3d09c-126">Authentication Phone</span></span>
* <span data-ttu-id="3d09c-127">Correo electrónico de autenticación</span><span class="sxs-lookup"><span data-stu-id="3d09c-127">Authentication Email</span></span>
* <span data-ttu-id="3d09c-128">Preguntas y respuestas de seguridad</span><span class="sxs-lookup"><span data-stu-id="3d09c-128">Security Questions and Answers</span></span>

<span data-ttu-id="3d09c-129">Si ha proporcionado un valor para **teléfono móvil** o **correo electrónico alternativa**, los usuarios pueden usar inmediatamente los valores tooreset sus contraseñas, aunque no se haya registrado para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d09c-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="3d09c-130">Además, los usuarios ver esos valores al registrarse para hello primera vez y modificarlos si lo desean.</span><span class="sxs-lookup"><span data-stu-id="3d09c-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="3d09c-131">Después de que se registren correctamente, estos valores se conservarán en hello **teléfono de autenticación** y **correo electrónico de autenticación** campos, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="3d09c-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="3d09c-132">Establecimiento y lectura de datos de autenticación mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d09c-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="3d09c-133">Hola después campos puede establecerse utilizando PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d09c-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="3d09c-134">Correo electrónico alternativo</span><span class="sxs-lookup"><span data-stu-id="3d09c-134">Alternate Email</span></span>
* <span data-ttu-id="3d09c-135">Teléfono móvil</span><span class="sxs-lookup"><span data-stu-id="3d09c-135">Mobile Phone</span></span>
* <span data-ttu-id="3d09c-136">Teléfono del trabajo: solo puede establecerse si no se sincroniza un directorio local</span><span class="sxs-lookup"><span data-stu-id="3d09c-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="3d09c-137">Uso de PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="3d09c-137">Using PowerShell V1</span></span>

<span data-ttu-id="3d09c-138">tooget iniciado, necesita demasiado[descargar e instalar el módulo de PowerShell de Azure AD de hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="3d09c-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="3d09c-139">Una vez que se ha instalado, puede seguir los pasos de Hola que siguen tooconfigure cada campo.</span><span class="sxs-lookup"><span data-stu-id="3d09c-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="3d09c-140">Establecimiento de datos de autenticación con PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="3d09c-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="3d09c-141">Lectura de datos de autenticación con PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="3d09c-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="3d09c-142">Teléfono de autenticación y correo electrónico de autenticación sólo se pueden leer utilizando Powershell V1 utilizando Hola comandos que siguen</span><span class="sxs-lookup"><span data-stu-id="3d09c-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="3d09c-143">Uso de PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="3d09c-143">Using PowerShell V2</span></span>

<span data-ttu-id="3d09c-144">tooget iniciado, necesita demasiado[descargar e instalar el módulo de PowerShell de Azure AD V2 hello](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="3d09c-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="3d09c-145">Una vez que se ha instalado, puede seguir los pasos de Hola que siguen tooconfigure cada campo.</span><span class="sxs-lookup"><span data-stu-id="3d09c-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="3d09c-146">tooinstall rápidamente desde las versiones recientes de PowerShell que admiten Install-Module, ejecute estos comandos (primera línea de hello simplemente comprueba toosee si se encuentra ya instalada):</span><span class="sxs-lookup"><span data-stu-id="3d09c-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="3d09c-147">Establecimiento de datos de autenticación con PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="3d09c-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="3d09c-148">Lectura de datos de autenticación con PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="3d09c-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="3d09c-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3d09c-149">Next steps</span></span>

<span data-ttu-id="3d09c-150">Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="3d09c-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="3d09c-151">[**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d09c-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="3d09c-152">[**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d09c-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="3d09c-153">[**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí</span><span class="sxs-lookup"><span data-stu-id="3d09c-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="3d09c-154">[**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.</span><span class="sxs-lookup"><span data-stu-id="3d09c-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="3d09c-155">[**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas</span><span class="sxs-lookup"><span data-stu-id="3d09c-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="3d09c-156">[**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.</span><span class="sxs-lookup"><span data-stu-id="3d09c-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="3d09c-157">[**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona</span><span class="sxs-lookup"><span data-stu-id="3d09c-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="3d09c-158">[**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo?</span><span class="sxs-lookup"><span data-stu-id="3d09c-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="3d09c-159">¿Por qué?</span><span class="sxs-lookup"><span data-stu-id="3d09c-159">Why?</span></span> <span data-ttu-id="3d09c-160">¿Qué?</span><span class="sxs-lookup"><span data-stu-id="3d09c-160">What?</span></span> <span data-ttu-id="3d09c-161">¿Dónde?</span><span class="sxs-lookup"><span data-stu-id="3d09c-161">Where?</span></span> <span data-ttu-id="3d09c-162">¿Quién?</span><span class="sxs-lookup"><span data-stu-id="3d09c-162">Who?</span></span> <span data-ttu-id="3d09c-163">¿Cuándo?</span><span class="sxs-lookup"><span data-stu-id="3d09c-163">When?</span></span> <span data-ttu-id="3d09c-164">-Responde tooquestions siempre deseara tooask</span><span class="sxs-lookup"><span data-stu-id="3d09c-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="3d09c-165">[**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR</span><span class="sxs-lookup"><span data-stu-id="3d09c-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
