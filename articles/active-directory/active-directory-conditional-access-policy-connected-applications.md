---
title: directivas de acceso condicional basado en dispositivos de Azure Active Directory de aaaConfigure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las directivas de acceso condicional basado en dispositivos de Azure Active Directory tooconfigure."
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
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="377c3-103">Configuración de directivas de acceso condicional basadas en dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="377c3-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="377c3-104">Con el [acceso condicional de Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), puede ajustar el modo en que los usuarios autorizados pueden tener acceso a sus recursos.</span><span class="sxs-lookup"><span data-stu-id="377c3-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="377c3-105">Por ejemplo, limitar los dispositivos tootrusted Hola access toocertain recursos.</span><span class="sxs-lookup"><span data-stu-id="377c3-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="377c3-106">Una directiva de acceso condicional que requiere un dispositivo de confianza se conoce también como directiva de acceso condicional basada en dispositivos.</span><span class="sxs-lookup"><span data-stu-id="377c3-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="377c3-107">Este tema proporciona información sobre cómo condicional basado en dispositivos de tooconfigure tener acceso a las directivas de aplicaciones Azure conectada a AD.</span><span class="sxs-lookup"><span data-stu-id="377c3-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="377c3-108">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="377c3-108">Before you begin</span></span>

<span data-ttu-id="377c3-109">El acceso condicional basado en dispositivos une el **acceso condicional de Azure AD** y la **administración de dispositivos de Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="377c3-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="377c3-110">Si no está familiarizado con una de estas áreas aún, debe leer Hola siguientes temas, en primer lugar:</span><span class="sxs-lookup"><span data-stu-id="377c3-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="377c3-111">**[Acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  -este tema proporciona información general y conceptual de instrucción condicional acceso y Hola terminología relacionada.</span><span class="sxs-lookup"><span data-stu-id="377c3-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="377c3-112">**[Administración de toodevice de introducción en Azure Active Directory](device-management-introduction.md)**  -en este tema se ofrece una visión general de hello diversas opciones que tooconnect dispositivos con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="377c3-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="377c3-113">Dispositivos de confianza</span><span class="sxs-lookup"><span data-stu-id="377c3-113">Trusted devices</span></span>

<span data-ttu-id="377c3-114">En un mundo móvil en primer lugar, basado en la nube, Azure Active Directory permite toodevices de inicio de sesión único, las aplicaciones y servicios desde cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="377c3-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="377c3-115">Para determinados recursos en su entorno, conceder acceso de usuarios deseados toohello podrían no ser suficientemente buenos.</span><span class="sxs-lookup"><span data-stu-id="377c3-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="377c3-116">Además toohello usuarios deseados, también podría necesitar que un dispositivo de confianza toobe utiliza tooaccess un recurso.</span><span class="sxs-lookup"><span data-stu-id="377c3-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="377c3-117">En su entorno, puede definir lo que un dispositivo de confianza se basa en Hola siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="377c3-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="377c3-118">Hola [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="377c3-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="377c3-119">Si un dispositivo es compatible</span><span class="sxs-lookup"><span data-stu-id="377c3-119">Whether a device is compliant</span></span>
- <span data-ttu-id="377c3-120">Si un dispositivo está unido a un dominio</span><span class="sxs-lookup"><span data-stu-id="377c3-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="377c3-121">Hola [plataformas de dispositivos](active-directory-conditional-access-azure-portal.md#device-platforms) se caracteriza por sistema operativo de Hola que se ejecuta en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="377c3-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="377c3-122">En la directiva de acceso condicional basado en el dispositivo, puede limitar el acceso toocertain recursos toospecific plataformas de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="377c3-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="377c3-123">En una directiva de acceso condicional basado en el dispositivo, puede requerir toobe de dispositivos de confianza marcado como compatible.</span><span class="sxs-lookup"><span data-stu-id="377c3-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="377c3-125">Los dispositivos se pueden marcar como cumplen los requisitos de directorio Hola por:</span><span class="sxs-lookup"><span data-stu-id="377c3-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="377c3-126">Intune</span><span class="sxs-lookup"><span data-stu-id="377c3-126">Intune</span></span> 
- <span data-ttu-id="377c3-127">Un sistema de administración de dispositivos móviles de terceros integrado con Azure AD</span><span class="sxs-lookup"><span data-stu-id="377c3-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="377c3-128">Solo los dispositivos que están conectado tooAzure AD se pueden marcar como conformes.</span><span class="sxs-lookup"><span data-stu-id="377c3-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="377c3-129">tooconnect un tooAzure dispositivo Active Directory, deberá Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="377c3-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="377c3-130">Registrado en Azure AD</span><span class="sxs-lookup"><span data-stu-id="377c3-130">Azure AD registered</span></span>
- <span data-ttu-id="377c3-131">Unido a Azure AD</span><span class="sxs-lookup"><span data-stu-id="377c3-131">Azure AD joined</span></span>
- <span data-ttu-id="377c3-132">Híbrido unido a Azure AD</span><span class="sxs-lookup"><span data-stu-id="377c3-132">Hybrid Azure AD joined</span></span>

    ![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="377c3-134">Si tiene una superficie de Active Directory (AD) local, podría considerar dispositivos que no están conectado tooAzure AD pero toobe tooyour combinadas AD de confianza.</span><span class="sxs-lookup"><span data-stu-id="377c3-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![Aplicaciones de nube](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="377c3-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="377c3-136">Next steps</span></span>

<span data-ttu-id="377c3-137">Antes de configurar una directiva de acceso condicional basado en el dispositivo en su entorno, debe Eche un vistazo a hello [las prácticas recomendadas para el acceso condicional en Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="377c3-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

