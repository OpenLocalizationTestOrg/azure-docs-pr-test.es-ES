---
title: "aaaAzure AD en niveles de seguridad de contraseña | Documentos de Microsoft"
description: "Explica cómo Azure AD aplica contraseñas seguras y protege las contraseñas de los usuarios frente a los ciberdelincuentes."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="9a4d2-103">Un enfoque de varios niveles tooAzure AD contraseña de seguridad</span><span class="sxs-lookup"><span data-stu-id="9a4d2-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="9a4d2-104">En este artículo se describe algunos procedimientos recomendados que puede seguir como un usuario o un administrador tooprotect su Azure Active Directory (Azure AD) o Account de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="9a4d2-105">Administradores de Azure AD pueden restablecer las contraseñas de usuario usando la orientación de hello en el artículo hello [Hola restablecimiento de contraseñas para un usuario en Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9a4d2-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="9a4d2-106">Los usuarios pueden restablecer su contraseña usando la orientación de hello en el artículo hello [ayuda he olvidado mi contraseña de Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="9a4d2-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="9a4d2-107">Requisitos de contraseña</span><span class="sxs-lookup"><span data-stu-id="9a4d2-107">Password requirements</span></span>

<span data-ttu-id="9a4d2-108">Azure AD incorpora Hola después de contraseñas de toosecuring enfoques comunes:</span><span class="sxs-lookup"><span data-stu-id="9a4d2-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="9a4d2-109">Requisitos de longitud de contraseña</span><span class="sxs-lookup"><span data-stu-id="9a4d2-109">Password length requirements</span></span>
* <span data-ttu-id="9a4d2-110">Requisitos de complejidad de contraseña</span><span class="sxs-lookup"><span data-stu-id="9a4d2-110">Password complexity requirements</span></span>
* <span data-ttu-id="9a4d2-111">Expiración de contraseña normal y periódica</span><span class="sxs-lookup"><span data-stu-id="9a4d2-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="9a4d2-112">Para obtener información sobre el restablecimiento de contraseña en Azure Active Directory, vea el tema de hello [Azure AD restablecimiento de contraseña para profesionales de TI de hello](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="9a4d2-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="9a4d2-113">Protección de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a4d2-113">Azure AD password protections</span></span>

<span data-ttu-id="9a4d2-114">Azure AD y aproxime de hello sistema de cuentas Microsoft usar comprobadas de la industria tooensure protección segura de las contraseñas de usuario y al administrador incluidos:</span><span class="sxs-lookup"><span data-stu-id="9a4d2-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="9a4d2-115">Contraseñas prohibidas dinámicamente</span><span class="sxs-lookup"><span data-stu-id="9a4d2-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="9a4d2-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="9a4d2-116">Smart Password Lockout</span></span>

<span data-ttu-id="9a4d2-117">Para obtener información acerca de la administración de contraseñas basada en la investigación actual, vea notas del producto hello [contraseña instrucciones](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="9a4d2-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="9a4d2-118">Contraseñas prohibidas dinámicamente</span><span class="sxs-lookup"><span data-stu-id="9a4d2-118">Dynamically banned passwords</span></span>

<span data-ttu-id="9a4d2-119">Azure AD y el sistema de cuentas de Microsoft salvaguardan la protección de contraseñas mediante la prohibición dinámica de las contraseñas de uso más común.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="9a4d2-120">equipo de protección de la identidad de Azure identificador Hello habitualmente analiza las listas de contraseñas prohibido, evitar que los usuarios de la selección de contraseñas utilizadas comúnmente.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="9a4d2-121">Este servicio está disponible tooAzure AD y clientes del servicio de cuenta de Microsoft Hola.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="9a4d2-122">Al crear las contraseñas, es importante para los administradores tooencourage usuarios toochoose contraseña frases que contienen una combinación única de letras, números, caracteres o palabras.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="9a4d2-123">Este enfoque ayuda a las contraseñas de usuario de toomake toobe sea casi imposible en peligro pero más fácil para los usuarios tooremember.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="9a4d2-124">Infracciones de contraseña</span><span class="sxs-lookup"><span data-stu-id="9a4d2-124">Password breaches</span></span>

<span data-ttu-id="9a4d2-125">Microsoft está trabajando siempre toostay un paso por delante de delincuentes intrusos.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="9a4d2-126">equipo de Azure AD Identity Protection Hola analiza continuamente las contraseñas que se usan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="9a4d2-127">Delincuentes intrusos también utilizan similar tooinform estrategias sus ataques, como crear una [tabla de arco iris](https://en.wikipedia.org/wiki/Rainbow_table) para descifrar un hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="9a4d2-128">Microsoft lo analiza continuamente [las infracciones de datos](https://www.privacyrights.org/data-breaches) toomaintain una lista de contraseña prohibida actualizado dinámicamente, lo que garantiza que las contraseñas vulnerables están expulsadas antes de que se conviertan en un número real de amenaza tooAzure AD clientes.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="9a4d2-129">Para obtener más información sobre nuestros esfuerzos de seguridad actual, vea hello [informe de inteligencia de seguridad de Microsoft](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a4d2-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="9a4d2-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="9a4d2-130">Smart Password Lockout</span></span>

<span data-ttu-id="9a4d2-131">Cuando AD Azure detecta un toohack de tratar de intrusos penales potencial en una contraseña de usuario, se bloquear cuenta de usuario de hello inteligente el bloqueo de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="9a4d2-132">Azure AD está diseñado riesgo de hello toodetermine asociado a las sesiones de inicio de sesión específico.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="9a4d2-133">A continuación, utilizando los datos de seguridad más actualizadas de hello, aplicamos amenazas de ciberseguridad de toostop de semántica de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="9a4d2-134">Si un usuario está bloqueado fuera de Azure AD, su pantalla tiene un aspecto similar toohello que sigue:</span><span class="sxs-lookup"><span data-stu-id="9a4d2-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Bloqueado en Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="9a4d2-136">Para otras cuentas de Microsoft, su pantalla tiene un aspecto similar toohello que sigue:</span><span class="sxs-lookup"><span data-stu-id="9a4d2-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Bloqueado en una cuenta de Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="9a4d2-138">Para obtener información sobre el restablecimiento de contraseña en Azure Active Directory, vea el tema de hello [Azure AD restablecimiento de contraseña para profesionales de TI de hello](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="9a4d2-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="9a4d2-139">Si eres un administrador de Azure AD, puede que desee toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid que los usuarios crea contraseñas tradicionales por completo.</span><span class="sxs-lookup"><span data-stu-id="9a4d2-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="9a4d2-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a4d2-140">Next steps</span></span>

* [<span data-ttu-id="9a4d2-141">Cómo tooupdate su propia contraseña</span><span class="sxs-lookup"><span data-stu-id="9a4d2-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="9a4d2-142">aspectos básicos de Hola de administración de identidades de Azure</span><span class="sxs-lookup"><span data-stu-id="9a4d2-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="9a4d2-143">Informe sobre la actividad de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="9a4d2-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


