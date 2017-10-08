---
title: aaaVulnerabilities detectado por Azure Active Directory Identity Protection | Documentos de Microsoft
description: "Información general de vulnerabilidades de hello detectadas por Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="92ec4-104">Vulnerabilidades detectadas por Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="92ec4-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="92ec4-105">Los puntos vulnerables son puntos débiles de su entorno que pueden ser aprovechados por un atacante.</span><span class="sxs-lookup"><span data-stu-id="92ec4-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="92ec4-106">Se recomienda que solucionar estos postura de seguridad de las vulnerabilidades tooimprove Hola de su organización y evitar que los atacantes aprovecharse de ellos.</span><span class="sxs-lookup"><span data-stu-id="92ec4-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="92ec4-107">![vulnerabilidades](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilidades")</span><span class="sxs-lookup"><span data-stu-id="92ec4-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="92ec4-108">Hello las secciones siguientes proporcionan una visión general de las vulnerabilidades de hello notificados por protección de identidad.</span><span class="sxs-lookup"><span data-stu-id="92ec4-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="92ec4-109">Registro de la autenticación multifactor no configurado</span><span class="sxs-lookup"><span data-stu-id="92ec4-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="92ec4-110">Esta vulnerabilidad le ayuda a controlar la implementación de Hola de Azure la autenticación multifactor en su organización.</span><span class="sxs-lookup"><span data-stu-id="92ec4-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="92ec4-111">La autenticación multifactor Azure ofrece una segunda capa toouser de autenticación de seguridad.</span><span class="sxs-lookup"><span data-stu-id="92ec4-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="92ec4-112">Ayuda a proteger acceso toodata y aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple.</span><span class="sxs-lookup"><span data-stu-id="92ec4-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="92ec4-113">Ofrece una autenticación segura a través de una gran variedad de opciones sencillas, como llamadas telefónicas, mensajes de texto o notificaciones de aplicaciones móviles, lo que permite a los usuarios elegir el mecanismo que prefieran.</span><span class="sxs-lookup"><span data-stu-id="92ec4-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="92ec4-114">Se recomienda pedir Azure Multi-Factor Authentication para los inicios de sesión de usuario. La autenticación multifactor desempeña un papel clave en las directivas de acceso condicional basadas en riesgos disponibles mediante Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="92ec4-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="92ec4-115">Para obtener más detalles, consulte [Qué es Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="92ec4-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="92ec4-116">Aplicaciones en la nube no administradas</span><span class="sxs-lookup"><span data-stu-id="92ec4-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="92ec4-117">Este punto vulnerable ayuda a identificar aplicaciones en la nube no administradas en su organización.</span><span class="sxs-lookup"><span data-stu-id="92ec4-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="92ec4-118">En las empresas modernas, los departamentos de TI a menudo son conscientes de todas las aplicaciones de nube de Hola que los usuarios de su organización usa toodo su trabajo.</span><span class="sxs-lookup"><span data-stu-id="92ec4-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="92ec4-119">Es fácil toosee ¿por qué los administradores tendrían preocupado datos toocorporate de acceso no autorizado, posible pérdida de datos y otros riesgos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="92ec4-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="92ec4-120">Le recomendamos que su organización implemente aplicaciones de nube de Cloud App Discovery toodiscover no administrado y toomanage estas aplicaciones con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92ec4-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="92ec4-121">Para obtener más detalles, consulte [Búsqueda de aplicaciones de nube no administradas con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92ec4-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="92ec4-122">Alertas de seguridad de administración de identidades con privilegios</span><span class="sxs-lookup"><span data-stu-id="92ec4-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="92ec4-123">Este punto vulnerable ayuda a detectar y resolver alertas acerca de las identidades con privilegios en su organización.</span><span class="sxs-lookup"><span data-stu-id="92ec4-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="92ec4-124">tooenable toocarry de los usuarios con privilegios en operaciones de salida, las organizaciones necesitan los usuarios de toogrant temporales o permanentes privilegios de acceso en Azure AD, recursos de Azure u Office 365 u otras aplicaciones de SaaS.</span><span class="sxs-lookup"><span data-stu-id="92ec4-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="92ec4-125">Cada uno de estos usuarios privilegiados aumenta Hola superficie expuesta a ataques de su organización.</span><span class="sxs-lookup"><span data-stu-id="92ec4-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="92ec4-126">Esta vulnerabilidad le ayuda a identificar a los usuarios con acceso con privilegios innecesario y tomar las medidas adecuadas tooreduce o eliminar el riesgo de Hola que suponen.</span><span class="sxs-lookup"><span data-stu-id="92ec4-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="92ec4-127">Se recomienda que su organización utiliza Azure AD Privileged Identity Management toomanage, control y las identidades de monitor con privilegios y sus tooresources de acceso de Azure AD, así como otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="92ec4-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="92ec4-128">Para obtener más detalles, consulte [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="92ec4-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="92ec4-129">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="92ec4-129">See also</span></span>
* [<span data-ttu-id="92ec4-130">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="92ec4-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

