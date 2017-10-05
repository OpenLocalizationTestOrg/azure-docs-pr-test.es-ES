---
title: "Seguridad de contraseñas por niveles de Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="43472-103">Un enfoque de varios niveles para la seguridad de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43472-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="43472-104">En este artículo se describen los procedimientos recomendados que puede seguir como usuario o administrador para proteger su cuenta de Azure Active Directory (Azure AD) o Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43472-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="43472-105">Los administradores de Azure AD pueden restablecer las contraseñas de usuario mediante las instrucciones del artículo [Restablecimiento de la contraseña de un usuario en Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="43472-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="43472-106">Los usuarios pueden restablecer su propia contraseña mediante las instrucciones del artículo [Ayuda, he olvidado mi contraseña de Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="43472-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="43472-107">Requisitos de contraseña</span><span class="sxs-lookup"><span data-stu-id="43472-107">Password requirements</span></span>

<span data-ttu-id="43472-108">Azure AD incorpora los siguientes enfoques comunes para proteger las contraseñas:</span><span class="sxs-lookup"><span data-stu-id="43472-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="43472-109">Requisitos de longitud de contraseña</span><span class="sxs-lookup"><span data-stu-id="43472-109">Password length requirements</span></span>
* <span data-ttu-id="43472-110">Requisitos de complejidad de contraseña</span><span class="sxs-lookup"><span data-stu-id="43472-110">Password complexity requirements</span></span>
* <span data-ttu-id="43472-111">Expiración de contraseña normal y periódica</span><span class="sxs-lookup"><span data-stu-id="43472-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="43472-112">Para más información sobre el restablecimiento de contraseña en Azure Active Directory, consulte el tema [Autoservicio de restablecimiento de contraseña de Azure AD para profesionales de TI](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="43472-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="43472-113">Protección de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43472-113">Azure AD password protections</span></span>

<span data-ttu-id="43472-114">Azure AD y el sistema de cuentas de Microsoft usan enfoques de demostrada eficacia en el sector para garantizar la protección segura de las contraseñas de usuario y administrador, entre los que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="43472-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="43472-115">Contraseñas prohibidas dinámicamente</span><span class="sxs-lookup"><span data-stu-id="43472-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="43472-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="43472-116">Smart Password Lockout</span></span>

<span data-ttu-id="43472-117">Para más información sobre la administración de contraseñas basada en la investigación actual, consulte el documento técnico [Password Guidance](http://aka.ms/passwordguidance) (Guía de contraseñas).</span><span class="sxs-lookup"><span data-stu-id="43472-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="43472-118">Contraseñas prohibidas dinámicamente</span><span class="sxs-lookup"><span data-stu-id="43472-118">Dynamically banned passwords</span></span>

<span data-ttu-id="43472-119">Azure AD y el sistema de cuentas de Microsoft salvaguardan la protección de contraseñas mediante la prohibición dinámica de las contraseñas de uso más común.</span><span class="sxs-lookup"><span data-stu-id="43472-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="43472-120">El equipo de Azure AD Identity Protection analiza de manera rutinaria las listas de contraseñas prohibidas, y así impide que los usuarios seleccionen contraseñas de uso más común.</span><span class="sxs-lookup"><span data-stu-id="43472-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="43472-121">Este servicio está disponible en Azure AD y los clientes del servicio de la cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43472-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="43472-122">Al crear contraseñas, es importante que los administradores promuevan en los usuarios la selección de frases de contraseña que incluyan una combinación de letras, números, caracteres o palabras.</span><span class="sxs-lookup"><span data-stu-id="43472-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="43472-123">Este enfoque ayuda a crear contraseñas de usuario que es prácticamente imposible poner en peligro pero que son más fáciles de recordar para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="43472-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="43472-124">Infracciones de contraseña</span><span class="sxs-lookup"><span data-stu-id="43472-124">Password breaches</span></span>

<span data-ttu-id="43472-125">Microsoft se esfuerza siempre por situarse un paso por delante de los delincuentes cibernéticos.</span><span class="sxs-lookup"><span data-stu-id="43472-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="43472-126">El equipo de Azure AD Identity Protection analiza continuamente las contraseñas que se usan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="43472-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="43472-127">Los delincuentes cibernéticos también usan estrategias parecidas para informar de sus ataques, como la creación de una [tabla arco iris](https://en.wikipedia.org/wiki/Rainbow_table) para descifrar hashes de contraseña.</span><span class="sxs-lookup"><span data-stu-id="43472-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="43472-128">Microsoft analiza continuamente las [infracciones en los datos](https://www.privacyrights.org/data-breaches) para mantener una lista de contraseñas prohibidas actualizada dinámicamente, que garantiza que las contraseñas vulnerables se prohíban antes de que se conviertan en una amenaza real para los clientes de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43472-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="43472-129">Para más información sobre nuestros esfuerzos de seguridad actuales, consulte [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx) (Informe de inteligencia de seguridad de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="43472-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="43472-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="43472-130">Smart Password Lockout</span></span>

<span data-ttu-id="43472-131">Cuando AD Azure detecta un posible delincuente cibernético que intenta realizar modificaciones en la contraseña de un usuario, bloqueamos la cuenta de usuario con Smart Password Lockout.</span><span class="sxs-lookup"><span data-stu-id="43472-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="43472-132">Azure AD está diseñado para determinar el riesgo asociado con sesiones de inicio de sesión específicas.</span><span class="sxs-lookup"><span data-stu-id="43472-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="43472-133">Con los datos de seguridad más actualizados, aplicamos semántica de bloqueo para detener las amenazas de Internet.</span><span class="sxs-lookup"><span data-stu-id="43472-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="43472-134">Si un usuario está bloqueado en Azure AD, su pantalla tiene un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="43472-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Bloqueado en Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="43472-136">Para otras cuentas de Microsoft, su pantalla tiene un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="43472-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Bloqueado en una cuenta de Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="43472-138">Para más información sobre el restablecimiento de contraseña en Azure Active Directory, consulte el tema [Autoservicio de restablecimiento de contraseña de Azure AD para profesionales de TI](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="43472-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="43472-139">Los administradores de Azure AD pueden usar [Windows Hello](https://www.microsoft.com/windows/windows-hello) para evitar que los usuarios creen contraseñas tradicionales.</span><span class="sxs-lookup"><span data-stu-id="43472-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="43472-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43472-140">Next steps</span></span>

* [<span data-ttu-id="43472-141">Actualización de la propia contraseña</span><span class="sxs-lookup"><span data-stu-id="43472-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="43472-142">Aspectos básicos de la administración de identidades de Azure</span><span class="sxs-lookup"><span data-stu-id="43472-142">The fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="43472-143">Informe sobre la actividad de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="43472-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


