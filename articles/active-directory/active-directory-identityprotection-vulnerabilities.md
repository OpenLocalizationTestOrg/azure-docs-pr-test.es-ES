---
title: Vulnerabilidades detectadas por Azure Active Directory Identity Protection | Microsoft Docs
description: "Información general de las vulnerabilidades detectadas por Azure Active Directory Identity Protection."
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
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="57ff1-104">Vulnerabilidades detectadas por Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="57ff1-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="57ff1-105">Los puntos vulnerables son puntos débiles de su entorno que pueden ser aprovechados por un atacante.</span><span class="sxs-lookup"><span data-stu-id="57ff1-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="57ff1-106">Se recomienda solucionar estas vulnerabilidades para mejorar la posición de seguridad de su organización y evitar que los atacantes se aprovechen de ellas.</span><span class="sxs-lookup"><span data-stu-id="57ff1-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="57ff1-107">![vulnerabilidades](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilidades")</span><span class="sxs-lookup"><span data-stu-id="57ff1-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="57ff1-108">En las siguientes secciones se ofrece información general de las vulnerabilidades de las que informa Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="57ff1-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="57ff1-109">Registro de la autenticación multifactor no configurado</span><span class="sxs-lookup"><span data-stu-id="57ff1-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="57ff1-110">Este punto vulnerable ayuda a controlar la implementación de Azure Multi-Factor Authentication en su organización.</span><span class="sxs-lookup"><span data-stu-id="57ff1-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="57ff1-111">Azure Multi-Factor Authentication proporciona una segunda capa de seguridad a la autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="57ff1-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="57ff1-112">Azure Multi-Factor Authentication ayuda a proteger el acceso a los datos y las aplicaciones, al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple.</span><span class="sxs-lookup"><span data-stu-id="57ff1-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="57ff1-113">Ofrece una autenticación segura a través de una gran variedad de opciones sencillas, como llamadas telefónicas, mensajes de texto o notificaciones de aplicaciones móviles, lo que permite a los usuarios elegir el mecanismo que prefieran.</span><span class="sxs-lookup"><span data-stu-id="57ff1-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="57ff1-114">Se recomienda pedir Azure Multi-Factor Authentication para los inicios de sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="57ff1-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="57ff1-115">La autenticación multifactor desempeña un papel clave en las directivas de acceso condicional basadas en riesgos disponibles mediante Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="57ff1-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="57ff1-116">Para obtener más detalles, consulte [Qué es Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="57ff1-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="57ff1-117">Aplicaciones en la nube no administradas</span><span class="sxs-lookup"><span data-stu-id="57ff1-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="57ff1-118">Este punto vulnerable ayuda a identificar aplicaciones en la nube no administradas en su organización.</span><span class="sxs-lookup"><span data-stu-id="57ff1-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="57ff1-119">En las empresas modernas, los departamentos de TI a menudo no son conscientes de todas las aplicaciones en la nube que usan los miembros de su organización para realizar su trabajo.</span><span class="sxs-lookup"><span data-stu-id="57ff1-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="57ff1-120">Es fácil ver por qué a los administradores les podría preocupar el acceso no autorizado a datos corporativos, la posible pérdida de datos y otros riesgos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="57ff1-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="57ff1-121">Le recomendamos que su organización implemente Cloud App Discovery para detectar aplicaciones en la nube no administradas, así como administrar estas aplicaciones con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57ff1-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="57ff1-122">Para obtener más detalles, consulte [Búsqueda de aplicaciones de nube no administradas con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57ff1-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="57ff1-123">Alertas de seguridad de administración de identidades con privilegios</span><span class="sxs-lookup"><span data-stu-id="57ff1-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="57ff1-124">Este punto vulnerable ayuda a detectar y resolver alertas acerca de las identidades con privilegios en su organización.</span><span class="sxs-lookup"><span data-stu-id="57ff1-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="57ff1-125">Para que los usuarios puedan realizar operaciones con privilegios, las organizaciones tienen que proporcionar a sus usuarios acceso con privilegios temporal o permanente en Azure AD, recursos de Azure u Office 365, y otras aplicaciones de SaaS.</span><span class="sxs-lookup"><span data-stu-id="57ff1-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="57ff1-126">Cada uno de estos usuarios con privilegios aumenta la superficie de ataque de su organización.</span><span class="sxs-lookup"><span data-stu-id="57ff1-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="57ff1-127">Este punto vulnerable ayuda a identificar a los usuarios con acceso con privilegios innecesarios y realizar la acción apropiada para reducir o eliminar el riesgo que suponen.</span><span class="sxs-lookup"><span data-stu-id="57ff1-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="57ff1-128">Recomendamos que la organización utilice Privileged Identity Management de Azure AD para administrar, controlar y supervisar las identidades con privilegios y su acceso a recursos en Azure AD y en otros servicios en línea de Microsoft, como Office 365 o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="57ff1-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="57ff1-129">Para obtener más detalles, consulte [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="57ff1-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="57ff1-130">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="57ff1-130">See also</span></span>
* [<span data-ttu-id="57ff1-131">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="57ff1-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

