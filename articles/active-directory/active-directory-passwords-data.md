---
title: Azure AD SSPR data requirements (Requisitos de datos de SSPR de Azure AD) | Microsoft Docs
description: "Requisitos de datos del autoservicio de restablecimiento de contraseña de Azure AD y cómo cumplirlos"
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
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="b857e-103">Implementación del restablecimiento de contraseña sin necesidad de registro del usuario final</span><span class="sxs-lookup"><span data-stu-id="b857e-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="b857e-104">La implementación del autoservicio de restablecimiento de contraseña (SSPR) requiere que los datos de autenticación estén presentes.</span><span class="sxs-lookup"><span data-stu-id="b857e-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="b857e-105">Algunas organizaciones piden a sus usuarios que escriban sus datos de autenticación por sí mismos, pero muchas organizaciones prefieren sincronizar los datos existentes en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b857e-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="b857e-106">Si ha dado formato correctamente a los datos del directorio local y configura [Azure AD Connect mediante la configuración rápida](./connect/active-directory-aadconnect-get-started-express.md), esos datos se ponen a disposición de Azure AD y SSPR sin necesidad de interacción por parte del usuario.</span><span class="sxs-lookup"><span data-stu-id="b857e-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="b857e-107">Todos los números de teléfono deben tener el formato +CountryCode PhoneNumber (ejemplo: +1 4255551234) para funcionar correctamente.</span><span class="sxs-lookup"><span data-stu-id="b857e-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="b857e-108">El restablecimiento de contraseña no admite extensiones telefónicas.</span><span class="sxs-lookup"><span data-stu-id="b857e-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="b857e-109">Incluso con el formato +1 4255551234X12345, las extensiones se quitan antes de realizarse la llamada.</span><span class="sxs-lookup"><span data-stu-id="b857e-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="b857e-110">Campos rellenos</span><span class="sxs-lookup"><span data-stu-id="b857e-110">Fields populated</span></span>

<span data-ttu-id="b857e-111">Si usa la configuración predeterminada en Azure AD Connect, se realizan las siguientes asignaciones.</span><span class="sxs-lookup"><span data-stu-id="b857e-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="b857e-112">AD local</span><span class="sxs-lookup"><span data-stu-id="b857e-112">On-premises AD</span></span> | <span data-ttu-id="b857e-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="b857e-113">Azure AD</span></span> | <span data-ttu-id="b857e-114">Información de contacto de Autenticación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b857e-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b857e-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="b857e-115">telephoneNumber</span></span> | <span data-ttu-id="b857e-116">Teléfono del trabajo</span><span class="sxs-lookup"><span data-stu-id="b857e-116">Office phone</span></span> | <span data-ttu-id="b857e-117">Teléfono alternativo</span><span class="sxs-lookup"><span data-stu-id="b857e-117">Alternate phone</span></span> |
| <span data-ttu-id="b857e-118">mobile</span><span class="sxs-lookup"><span data-stu-id="b857e-118">mobile</span></span> | <span data-ttu-id="b857e-119">Teléfono móvil</span><span class="sxs-lookup"><span data-stu-id="b857e-119">Mobile phone</span></span> | <span data-ttu-id="b857e-120">Teléfono</span><span class="sxs-lookup"><span data-stu-id="b857e-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="b857e-121">Preguntas y respuestas de seguridad</span><span class="sxs-lookup"><span data-stu-id="b857e-121">Security questions and answers</span></span>

<span data-ttu-id="b857e-122">Las preguntas y respuestas de seguridad se almacenan de forma segura en el inquilino de Azure AD y los usuarios pueden tener acceso a ellas solo a través del [portal de registro de SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="b857e-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="b857e-123">Los administradores no pueden ver ni modificar el contenido de las preguntas y respuestas de otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="b857e-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="b857e-124">Qué ocurre cuando se registra un usuario</span><span class="sxs-lookup"><span data-stu-id="b857e-124">What happens when a user registers</span></span>

<span data-ttu-id="b857e-125">Cuando se registre un usuario, la página de registro establecerá los campos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b857e-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="b857e-126">Teléfono de autenticación</span><span class="sxs-lookup"><span data-stu-id="b857e-126">Authentication Phone</span></span>
* <span data-ttu-id="b857e-127">Correo electrónico de autenticación</span><span class="sxs-lookup"><span data-stu-id="b857e-127">Authentication Email</span></span>
* <span data-ttu-id="b857e-128">Preguntas y respuestas de seguridad</span><span class="sxs-lookup"><span data-stu-id="b857e-128">Security Questions and Answers</span></span>

<span data-ttu-id="b857e-129">Si ha especificado un valor para **Teléfono móvil** o **Correo electrónico alternativo**, los usuarios podrán usarlos inmediatamente para restablecer sus contraseñas, aunque no se hayan registrado para el servicio.</span><span class="sxs-lookup"><span data-stu-id="b857e-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="b857e-130">Además, los usuarios ven esos valores cuando se registran por primera vez y pueden modificarlos si lo desean.</span><span class="sxs-lookup"><span data-stu-id="b857e-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="b857e-131">Una vez que se registren correctamente, dichos valores se conservarán en los campos **Teléfono de autenticación** y **Correo electrónico de autenticación**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b857e-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="b857e-132">Establecimiento y lectura de datos de autenticación mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b857e-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="b857e-133">Los siguientes campos pueden establecerse mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b857e-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="b857e-134">Correo electrónico alternativo</span><span class="sxs-lookup"><span data-stu-id="b857e-134">Alternate Email</span></span>
* <span data-ttu-id="b857e-135">Teléfono móvil</span><span class="sxs-lookup"><span data-stu-id="b857e-135">Mobile Phone</span></span>
* <span data-ttu-id="b857e-136">Teléfono del trabajo: solo puede establecerse si no se sincroniza un directorio local</span><span class="sxs-lookup"><span data-stu-id="b857e-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="b857e-137">Uso de PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="b857e-137">Using PowerShell V1</span></span>

<span data-ttu-id="b857e-138">Para empezar, debe [descargar e instalar el módulo de Azure AD PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="b857e-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="b857e-139">Una vez instalado, puede seguir los pasos mostrados a continuación para configurar cada campo.</span><span class="sxs-lookup"><span data-stu-id="b857e-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="b857e-140">Establecimiento de datos de autenticación con PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="b857e-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="b857e-141">Lectura de datos de autenticación con PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="b857e-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="b857e-142">Teléfono de autenticación y Correo electrónico de autenticación solo pueden leerse mediante Powershell V1 usando los comandos mostrados a continuación</span><span class="sxs-lookup"><span data-stu-id="b857e-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="b857e-143">Uso de PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="b857e-143">Using PowerShell V2</span></span>

<span data-ttu-id="b857e-144">Para empezar, debe [descargar e instalar el módulo de Azure AD V2 PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="b857e-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="b857e-145">Una vez instalado, puede seguir los pasos mostrados a continuación para configurar cada campo.</span><span class="sxs-lookup"><span data-stu-id="b857e-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="b857e-146">Para instalar rápidamente desde versiones recientes de PowerShell que admiten Install-Module, ejecute estos comandos (la primera línea simplemente comprueba si ya se ha instalado):</span><span class="sxs-lookup"><span data-stu-id="b857e-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="b857e-147">Establecimiento de datos de autenticación con PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="b857e-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="b857e-148">Lectura de datos de autenticación con PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="b857e-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="b857e-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b857e-149">Next steps</span></span>

<span data-ttu-id="b857e-150">Los vínculos siguientes proporcionan información adicional sobre el restablecimiento de contraseñas con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b857e-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="b857e-151">[**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b857e-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="b857e-152">[**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b857e-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="b857e-153">[**Implementación**](active-directory-passwords-best-practices.md): planificación e implementación de SSPR para los usuarios con las directrices que aquí se proporcionan</span><span class="sxs-lookup"><span data-stu-id="b857e-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="b857e-154">[**Personalización**](active-directory-passwords-customize.md): personalice el aspecto de la experiencia SSPR para su empresa.</span><span class="sxs-lookup"><span data-stu-id="b857e-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="b857e-155">[**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas</span><span class="sxs-lookup"><span data-stu-id="b857e-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="b857e-156">[**Informes**](active-directory-passwords-reporting.md): informes para detectar si los usuarios acceden a la funcionalidad de SSPR que especifican el momento y el lugar del acceso</span><span class="sxs-lookup"><span data-stu-id="b857e-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="b857e-157">[**Profundización técnica**](active-directory-passwords-how-it-works.md): conozca lo que hay detrás para comprender cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="b857e-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="b857e-158">[**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo?</span><span class="sxs-lookup"><span data-stu-id="b857e-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="b857e-159">¿Por qué?</span><span class="sxs-lookup"><span data-stu-id="b857e-159">Why?</span></span> <span data-ttu-id="b857e-160">¿Qué?</span><span class="sxs-lookup"><span data-stu-id="b857e-160">What?</span></span> <span data-ttu-id="b857e-161">¿Dónde?</span><span class="sxs-lookup"><span data-stu-id="b857e-161">Where?</span></span> <span data-ttu-id="b857e-162">¿Quién?</span><span class="sxs-lookup"><span data-stu-id="b857e-162">Who?</span></span> <span data-ttu-id="b857e-163">¿Cuándo?</span><span class="sxs-lookup"><span data-stu-id="b857e-163">When?</span></span> <span data-ttu-id="b857e-164">: respuestas a las preguntas que siempre se ha hecho.</span><span class="sxs-lookup"><span data-stu-id="b857e-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="b857e-165">[**Solución de problemas**](active-directory-passwords-troubleshoot.md): información para resolver problemas habituales de SSPR</span><span class="sxs-lookup"><span data-stu-id="b857e-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
