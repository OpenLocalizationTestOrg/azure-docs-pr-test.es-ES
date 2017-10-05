---
title: "Configuración de directivas de acceso condicional basadas en dispositivos de Azure Active Directory | Microsoft Docs"
description: "Obtenga información sobre cómo configurar directivas de acceso condicional basadas en dispositivos de Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a26c40351c6b982fd90acb4bf06220ef3f79f399
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="f3dec-103">Configuración de directivas de acceso condicional basadas en dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3dec-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="f3dec-104">Con el [acceso condicional de Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), puede ajustar el modo en que los usuarios autorizados pueden tener acceso a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="f3dec-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="f3dec-105">Por ejemplo, limita el acceso a determinados recursos a dispositivos de confianza.</span><span class="sxs-lookup"><span data-stu-id="f3dec-105">For example, you limit the access to certain resources to trusted devices.</span></span> <span data-ttu-id="f3dec-106">Una directiva de acceso condicional que requiere un dispositivo de confianza se conoce también como directiva de acceso condicional basada en dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f3dec-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="f3dec-107">En este tema se proporciona información sobre cómo configurar directivas de acceso condicional basadas en dispositivos para aplicaciones conectadas a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3dec-107">This topic provides you with information on how to configure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="f3dec-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f3dec-108">Before you begin</span></span>

<span data-ttu-id="f3dec-109">El acceso condicional basado en dispositivos une el **acceso condicional de Azure AD** y la **administración de dispositivos de Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="f3dec-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="f3dec-110">Si no está familiarizado con ninguna de estas áreas, debería leer los siguientes temas en primer lugar:</span><span class="sxs-lookup"><span data-stu-id="f3dec-110">If you are not familiar with one of these areas yet, you should read the following topics, first:</span></span>

- <span data-ttu-id="f3dec-111">**[Acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal.md)**: en este tema se proporcionan tanto información general conceptual de acceso condicional como la terminología relacionada.</span><span class="sxs-lookup"><span data-stu-id="f3dec-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and the related terminology.</span></span>

- <span data-ttu-id="f3dec-112">**[Introducción a la administración de dispositivos en Azure Active Directory](device-management-introduction.md)**: en este tema se proporciona información general de las diversas opciones que tiene para conectar dispositivos con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3dec-112">**[Introduction to device management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of the various options you have to connect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="f3dec-113">Dispositivos de confianza</span><span class="sxs-lookup"><span data-stu-id="f3dec-113">Trusted devices</span></span>

<span data-ttu-id="f3dec-114">En un mundo Mobile First, Cloud First, Azure Active Directory permite el inicio de sesión único en dispositivos, aplicaciones y servicios desde cualquier parte.</span><span class="sxs-lookup"><span data-stu-id="f3dec-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="f3dec-115">Para determinados recursos de su entorno, es posible que conceder acceso a los usuarios adecuados no sea una acción lo suficientemente buena.</span><span class="sxs-lookup"><span data-stu-id="f3dec-115">For certain resources in your environment, granting access to the right users might not be good enough.</span></span> <span data-ttu-id="f3dec-116">Además de los usuarios adecuados, puede que también requiera el uso de un dispositivo de confianza para tener acceso a un recurso.</span><span class="sxs-lookup"><span data-stu-id="f3dec-116">In addition to the right users, you might also require a trusted device to be used to access a resource.</span></span> <span data-ttu-id="f3dec-117">En su entorno, puede definir lo que es un dispositivo de confianza en función de los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="f3dec-117">In your environment, you can define what a trusted device is based on the following components:</span></span>

- <span data-ttu-id="f3dec-118">Las [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) de un dispositivo</span><span class="sxs-lookup"><span data-stu-id="f3dec-118">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="f3dec-119">Si un dispositivo es compatible</span><span class="sxs-lookup"><span data-stu-id="f3dec-119">Whether a device is compliant</span></span>
- <span data-ttu-id="f3dec-120">Si un dispositivo está unido a un dominio</span><span class="sxs-lookup"><span data-stu-id="f3dec-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="f3dec-121">La [plataforma de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) se caracteriza por el sistema operativo que se ejecuta en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f3dec-121">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by the operating system that is running on your device.</span></span> <span data-ttu-id="f3dec-122">En su directiva de acceso condicional basada en dispositivos, puede limitar el acceso a determinados recursos a plataformas de dispositivo específicas.</span><span class="sxs-lookup"><span data-stu-id="f3dec-122">In your device-based conditional access policy, you can limit access to certain resources to specific device platforms.</span></span>



<span data-ttu-id="f3dec-123">En una directiva de acceso condicional basada en dispositivos, puede requerir que se marquen dispositivos de confianza como compatibles.</span><span class="sxs-lookup"><span data-stu-id="f3dec-123">In a device-based conditional access policy, you can require trusted devices to be marked as compliant.</span></span>

![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="f3dec-125">Los dispositivos se pueden marcar como compatibles en el directorio por medio de:</span><span class="sxs-lookup"><span data-stu-id="f3dec-125">Devices can be marked as compliant in the directory by:</span></span>

- <span data-ttu-id="f3dec-126">Intune</span><span class="sxs-lookup"><span data-stu-id="f3dec-126">Intune</span></span> 
- <span data-ttu-id="f3dec-127">Un sistema de administración de dispositivos móviles de terceros integrado con Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3dec-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="f3dec-128">Solo los dispositivos conectados a Azure AD pueden marcarse como compatibles.</span><span class="sxs-lookup"><span data-stu-id="f3dec-128">Only devices that are connected to Azure AD can be marked as compliant.</span></span> <span data-ttu-id="f3dec-129">Para conectar un dispositivo a Azure Active Directory, tiene las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="f3dec-129">To connect a device to Azure Active Directory, you have the following options:</span></span> 

- <span data-ttu-id="f3dec-130">Registrado en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3dec-130">Azure AD registered</span></span>
- <span data-ttu-id="f3dec-131">Unido a Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3dec-131">Azure AD joined</span></span>
- <span data-ttu-id="f3dec-132">Híbrido unido a Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3dec-132">Hybrid Azure AD joined</span></span>

    ![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="f3dec-134">Si tiene una superficie de Active Directory (AD) local, podría considerar la posibilidad de hacer que los dispositivos no conectados a Azure AD, pero unidos a AD, sean de confianza.</span><span class="sxs-lookup"><span data-stu-id="f3dec-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected to Azure AD but joined to your AD to be trusted.</span></span>

![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="f3dec-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3dec-136">Next steps</span></span>

<span data-ttu-id="f3dec-137">Antes de configurar una directiva de acceso condicional basada en dispositivos en su entorno, debería echar un vistazo a [Procedimientos recomendados para el acceso condicional en Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="f3dec-137">Before configuring a device-based conditional access policy in your environment, you should take a look at the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

