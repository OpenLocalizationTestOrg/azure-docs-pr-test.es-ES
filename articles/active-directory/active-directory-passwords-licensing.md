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
ms.openlocfilehash: 936134bddad19964f809a17f200ebbeed5aa853c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="00a20-103">Licensing requirements for Azure AD self-service password reset (Requisitos de concesión de licencias del autoservicio de restablecimiento de contraseña de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="00a20-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="00a20-104">Para que el restablecimiento de contraseña de Azure AD funcione, **debe tener al menos una licencia asignada en su organización**.</span><span class="sxs-lookup"><span data-stu-id="00a20-104">In order for Azure AD Password Reset to function, you **must have at least one license assigned in your organization**.</span></span> <span data-ttu-id="00a20-105">No aplicamos la concesión de licencias por usuario en la experiencia de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="00a20-105">We do not enforce per-user licensing on the password reset experience.</span></span> <span data-ttu-id="00a20-106">A fin de que se siga cumpliendo el contrato de licencia de Microsoft, debe asignar licencias a los usuarios que usen características premium.</span><span class="sxs-lookup"><span data-stu-id="00a20-106">To maintain compliance with your Microsoft licensing agreement, you need to assign licenses to any users that use premium features.</span></span>

* <span data-ttu-id="00a20-107">**Solo usuarios en la nube**: Office 365 (O365), cualquier SKU de pago o Azure AD Basic</span><span class="sxs-lookup"><span data-stu-id="00a20-107">**Cloud only users** - Office 365 (O365) any paid SKU, or Azure AD Basic</span></span>
* <span data-ttu-id="00a20-108">**Usuarios en la nube** o **locales**: Azure AD Premium P1 o P2, Mobility + Security (EMS) o Secure Productive Enterprise (SPE)</span><span class="sxs-lookup"><span data-stu-id="00a20-108">**Cloud** and/or **on-premises users** - Azure AD Premium P1 or P2, Enterprise Mobility + Security (EMS), or Secure Productive Enterprise (SPE)</span></span>

## <a name="licenses-required-for-password-writeback"></a><span data-ttu-id="00a20-109">Licencias necesarias para la escritura diferida de contraseñas</span><span class="sxs-lookup"><span data-stu-id="00a20-109">Licenses required for password writeback</span></span>

<span data-ttu-id="00a20-110">Para poder usar la escritura diferida de contraseñas, debe tener una de las siguientes licencias asignadas en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="00a20-110">To use password writeback, you must have one of the following licenses assigned in your tenant.</span></span>

* <span data-ttu-id="00a20-111">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="00a20-111">Azure AD Premium P1</span></span>
* <span data-ttu-id="00a20-112">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="00a20-112">Azure AD Premium P2</span></span>
* <span data-ttu-id="00a20-113">Enterprise Mobility + Security E3</span><span class="sxs-lookup"><span data-stu-id="00a20-113">Enterprise Mobility + Security E3</span></span>
* <span data-ttu-id="00a20-114">Enterprise Mobility + Security E5</span><span class="sxs-lookup"><span data-stu-id="00a20-114">Enterprise Mobility + Security E5</span></span>
* <span data-ttu-id="00a20-115">Secure Productive Enterprise E3</span><span class="sxs-lookup"><span data-stu-id="00a20-115">Secure Productive Enterprise E3</span></span>
* <span data-ttu-id="00a20-116">Secure Productive Enterprise E5</span><span class="sxs-lookup"><span data-stu-id="00a20-116">Secure Productive Enterprise E5</span></span>

> [!NOTE]
> <span data-ttu-id="00a20-117">Los planes de licencias de Office 365 independientes **no admiten la escritura diferida de contraseñas** y requieren uno de los planes anteriores para que esta funcionalidad funcione.</span><span class="sxs-lookup"><span data-stu-id="00a20-117">Standalone Office 365 licensing plans **do not support password writeback** and require one of the preceding plans for this functionality to work.</span></span>

<span data-ttu-id="00a20-118">En las páginas siguientes encontrará información adicional sobre licencias, incluidos los costos</span><span class="sxs-lookup"><span data-stu-id="00a20-118">Additional licensing info including costs can be found on the following pages</span></span>

* [<span data-ttu-id="00a20-119">Sitio sobre precios de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00a20-119">Azure Active Directory Pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="00a20-120">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="00a20-120">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="00a20-121">Secure Productive Enterprise</span><span class="sxs-lookup"><span data-stu-id="00a20-121">Secure Productive Enterprise</span></span>](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="00a20-122">Habilitar licencias basadas en grupos o usuarios</span><span class="sxs-lookup"><span data-stu-id="00a20-122">Enable group or user-based licensing</span></span>

<span data-ttu-id="00a20-123">Azure AD admite ahora licencias basadas en grupos que permiten a los administradores asignar licencias en bloque a un grupo de usuarios en lugar de asignarlas una a una.</span><span class="sxs-lookup"><span data-stu-id="00a20-123">Azure AD now supports group-based licensing allowing administrators to assign licenses in bulk to a group of users, rather than assigning them one at a time.</span></span> [<span data-ttu-id="00a20-124">Asignar, comprobar y resolver los problemas con licencias</span><span class="sxs-lookup"><span data-stu-id="00a20-124">Assign, verify, and resolve problems with licenses</span></span>](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

<span data-ttu-id="00a20-125">Algunos servicios de Microsoft no están disponibles en todas las ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="00a20-125">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="00a20-126">Antes de poder asignar una licencia a un usuario, el administrador tiene que especificar la propiedad “Ubicación de uso” en el usuario.</span><span class="sxs-lookup"><span data-stu-id="00a20-126">Before a license can be assigned to a user, the administrator must specify the “Usage location” property on the user.</span></span> <span data-ttu-id="00a20-127">La asignación de licencias puede hacerse en la sección Usuario > Perfil > Configuración de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="00a20-127">Assignment of licenses can be done under User > Profile > Settings section in the Azure portal.</span></span> <span data-ttu-id="00a20-128">**Cuando se utiliza la asignación de licencias de grupo, los usuarios sin ubicación de uso especificada heredan la ubicación del directorio.**</span><span class="sxs-lookup"><span data-stu-id="00a20-128">**When using group license assignment, any users without a usage location specified inherit the location of the directory.**</span></span>

## <a name="next-steps"></a><span data-ttu-id="00a20-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="00a20-129">Next steps</span></span>

<span data-ttu-id="00a20-130">Los vínculos siguientes proporcionan información adicional sobre el restablecimiento de contraseñas con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="00a20-130">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="00a20-131">[**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="00a20-131">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="00a20-132">[**Datos**](active-directory-passwords-data.md): información sobre los datos necesarios y cómo se usan para administrar contraseñas</span><span class="sxs-lookup"><span data-stu-id="00a20-132">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="00a20-133">[**Implementación**](active-directory-passwords-best-practices.md): planee e implemente SSPR en sus usuarios mediante las instrucciones que se encuentran aquí.</span><span class="sxs-lookup"><span data-stu-id="00a20-133">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="00a20-134">[**Personalización**](active-directory-passwords-customize.md): personalización de la experiencia de SSPR para la empresa</span><span class="sxs-lookup"><span data-stu-id="00a20-134">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="00a20-135">[**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.</span><span class="sxs-lookup"><span data-stu-id="00a20-135">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="00a20-136">[**Profundización técnica**](active-directory-passwords-how-it-works.md): conozca lo que hay detrás para comprender cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="00a20-136">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="00a20-137">[**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo?</span><span class="sxs-lookup"><span data-stu-id="00a20-137">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="00a20-138">¿Por qué?</span><span class="sxs-lookup"><span data-stu-id="00a20-138">Why?</span></span> <span data-ttu-id="00a20-139">¿Qué?</span><span class="sxs-lookup"><span data-stu-id="00a20-139">What?</span></span> <span data-ttu-id="00a20-140">¿Dónde?</span><span class="sxs-lookup"><span data-stu-id="00a20-140">Where?</span></span> <span data-ttu-id="00a20-141">¿Quién?</span><span class="sxs-lookup"><span data-stu-id="00a20-141">Who?</span></span> <span data-ttu-id="00a20-142">¿Cuándo?</span><span class="sxs-lookup"><span data-stu-id="00a20-142">When?</span></span> <span data-ttu-id="00a20-143">: respuestas a las preguntas que siempre se ha hecho.</span><span class="sxs-lookup"><span data-stu-id="00a20-143">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="00a20-144">[**Solución de problemas**](active-directory-passwords-troubleshoot.md): información para resolver problemas habituales de SSPR</span><span class="sxs-lookup"><span data-stu-id="00a20-144">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

