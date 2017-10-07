---
title: 'Licensing: Azure AD SSPR (Licencias: SSPR de Azure AD) | Microsoft Docs'
description: "Requisitos de concesión de licencias del autoservicio de restablecimiento de contraseña de Azure AD"
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
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="1aa56-103">Licensing requirements for Azure AD self-service password reset (Requisitos de concesión de licencias del autoservicio de restablecimiento de contraseña de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="1aa56-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="1aa56-104">En orden de restablecimiento de contraseña de Azure AD toofunction, le **debe tener al menos una licencia asignada en su organización**.</span><span class="sxs-lookup"><span data-stu-id="1aa56-104">In order for Azure AD Password Reset toofunction, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="1aa56-105">No se aplican licencias en la experiencia de restablecimiento de contraseña de Hola por usuario.</span><span class="sxs-lookup"><span data-stu-id="1aa56-105">We do not enforce per-user licensing on hello password reset experience.</span></span> <span data-ttu-id="1aa56-106">toomaintain el cumplimiento con el contrato de licencia de Microsoft, necesita que tooassign licencias tooany usuarios que usen las características premium.</span><span class="sxs-lookup"><span data-stu-id="1aa56-106">toomaintain compliance with your Microsoft licensing agreement, you need tooassign licenses tooany users that use premium features.</span></span>

* <span data-ttu-id="1aa56-107">**Solo usuarios en la nube**: Office 365 (O365), cualquier SKU de pago o Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="1aa56-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="1aa56-108">**Usuarios en la nube** o **locales**: Azure AD Premium P1 o P2, Mobility + Security (EMS) o Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="1aa56-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="1aa56-109">Licencias necesarias para la escritura diferida de contraseñas</span><span class="sxs-lookup"><span data-stu-id="1aa56-109">Licenses required for password writeback</span></span>

<span data-ttu-id="1aa56-110">escritura diferida de contraseñas toouse, debe tener uno de hello después licencias asignadas en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="1aa56-110">toouse password writeback, you must have one of hello following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="1aa56-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="1aa56-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="1aa56-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="1aa56-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="1aa56-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="1aa56-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="1aa56-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="1aa56-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="1aa56-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="1aa56-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="1aa56-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="1aa56-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="1aa56-117">Planes de licencias por independiente Office 365 **no admiten la escritura diferida de contraseñas** y necesitan una de hello anterior planes para este toowork de funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="1aa56-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of hello preceding plans for this functionality toowork.</span></span>

<span data-ttu-id="1aa56-118">Información de licencia adicional incluidos los costos puede encontrarse en hello después de páginas</span><span class="sxs-lookup"><span data-stu-id="1aa56-118">Additional licensing info including costs can be found on hello following pages</span></span>

* [<span data-ttu-id="1aa56-119">Sitio sobre precios de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1aa56-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="1aa56-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="1aa56-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="1aa56-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="1aa56-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="1aa56-122">Habilitar licencias basadas en grupos o usuarios</span><span class="sxs-lookup"><span data-stu-id="1aa56-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="1aa56-123">Ahora, Azure AD admite basado en el grupo licencias permitiendo administradores tooassign licencias en grupo de tooa de forma masiva de usuarios en lugar de asignar uno a la vez.</span><span class="sxs-lookup"><span data-stu-id="1aa56-123">Azure AD now supports group-based licensing allowing administrators tooassign licenses in bulk tooa group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="1aa56-124">Asignar, comprobar y resolver los problemas con licencias</span><span class="sxs-lookup"><span data-stu-id="1aa56-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="1aa56-125">Algunos servicios de Microsoft no están disponibles en todas las ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="1aa56-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="1aa56-126">Antes de poder asignar una licencia de usuario de tooa, Administrador de hello debe especificar la propiedad de "Ubicación de uso" de hello en usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="1aa56-126">Before a license can be assigned tooa user, hello administrator must specify hello “Usage location” property on hello user.</span></span> <span data-ttu-id="1aa56-127">Es posible la asignación de licencias de usuario > perfil > sección de configuración en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1aa56-127">Assignment of licenses can be done under User > Profile > Settings section in hello Azure portal.</span></span> <span data-ttu-id="1aa56-128">**Cuando se utiliza la asignación de licencias del grupo, los usuarios sin especificar una ubicación de uso heredan ubicación hello del directorio de Hola.**</span><span class="sxs-lookup"><span data-stu-id="1aa56-128">**When using group license assignment, any users without a usage location specified inherit hello location of hello directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aa56-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1aa56-129">Next steps</span></span>

<span data-ttu-id="1aa56-130">Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="1aa56-130">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="1aa56-131">[**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa56-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="1aa56-132">[**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas</span><span class="sxs-lookup"><span data-stu-id="1aa56-132">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="1aa56-133">[**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí</span><span class="sxs-lookup"><span data-stu-id="1aa56-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="1aa56-134">[**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.</span><span class="sxs-lookup"><span data-stu-id="1aa56-134">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="1aa56-135">[**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.</span><span class="sxs-lookup"><span data-stu-id="1aa56-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="1aa56-136">[**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona</span><span class="sxs-lookup"><span data-stu-id="1aa56-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="1aa56-137">[**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo?</span><span class="sxs-lookup"><span data-stu-id="1aa56-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="1aa56-138">¿Por qué?</span><span class="sxs-lookup"><span data-stu-id="1aa56-138">Why?</span></span> <span data-ttu-id="1aa56-139">¿Qué?</span><span class="sxs-lookup"><span data-stu-id="1aa56-139">What?</span></span> <span data-ttu-id="1aa56-140">¿Dónde?</span><span class="sxs-lookup"><span data-stu-id="1aa56-140">Where?</span></span> <span data-ttu-id="1aa56-141">¿Quién?</span><span class="sxs-lookup"><span data-stu-id="1aa56-141">Who?</span></span> <span data-ttu-id="1aa56-142">¿Cuándo?</span><span class="sxs-lookup"><span data-stu-id="1aa56-142">When?</span></span> <span data-ttu-id="1aa56-143">-Responde tooquestions siempre deseara tooask</span><span class="sxs-lookup"><span data-stu-id="1aa56-143">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="1aa56-144">[**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR</span><span class="sxs-lookup"><span data-stu-id="1aa56-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

