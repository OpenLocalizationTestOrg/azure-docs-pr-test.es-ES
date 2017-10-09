---
title: "Características de Azure AD Connect en la versión preliminar | Microsoft Docs"
description: "En este tema se describen más detenidamente las características que se encuentran en la versión preliminar en Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="37e3c-103">Más detalles sobre las características de vista previa</span><span class="sxs-lookup"><span data-stu-id="37e3c-103">More details about features in preview</span></span>
<span data-ttu-id="37e3c-104">Este tema describe cómo toouse características actualmente en vista previa.</span><span class="sxs-lookup"><span data-stu-id="37e3c-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="37e3c-105">Escritura diferida de grupos</span><span class="sxs-lookup"><span data-stu-id="37e3c-105">Group writeback</span></span>
<span data-ttu-id="37e3c-106">opción de Hola para reescritura de grupos de características opcionales permite toowriteback **grupos de Office 365** tooa bosque con Exchange instalado.</span><span class="sxs-lookup"><span data-stu-id="37e3c-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="37e3c-107">Se trata de un grupo que siempre se controla en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="37e3c-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="37e3c-108">Si tiene Exchange local, a continuación, puede escribir nuevo estos grupos tooon local para que los usuarios con un buzón de Exchange local pueden enviar y recibir mensajes de correo electrónico de estos grupos.</span><span class="sxs-lookup"><span data-stu-id="37e3c-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="37e3c-109">Para obtener más información acerca de los grupos de Office 365 y cómo toouse les pueden encontrarse [aquí](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="37e3c-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="37e3c-110">Este grupo de Office 365 se representará como un grupo de distribución en AD DS local.</span><span class="sxs-lookup"><span data-stu-id="37e3c-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="37e3c-111">El servidor de Exchange local debe estar en la actualización acumulativa de Exchange 2013 8 (publicada en marzo de 2015) o Exchange 2016 toorecognize este nuevo tipo de grupo.</span><span class="sxs-lookup"><span data-stu-id="37e3c-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="37e3c-112">**Notas durante la vista previa de Hola**</span><span class="sxs-lookup"><span data-stu-id="37e3c-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="37e3c-113">atributo de libreta de direcciones Hola actualmente no se rellena en la vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="37e3c-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="37e3c-114">Sin este atributo, grupo de hello no está visible en hello GAL.</span><span class="sxs-lookup"><span data-stu-id="37e3c-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="37e3c-115">Hola toopopulate de manera más fácil este atributo es el cmdlet de PowerShell de Exchange de hello toouse `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="37e3c-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="37e3c-116">Solo bosques con el esquema de Exchange Hola constituyen destinos válidos para los grupos.</span><span class="sxs-lookup"><span data-stu-id="37e3c-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="37e3c-117">Si se ha detectado ningún cambio, a continuación, reescritura de grupos no es posible tooenable.</span><span class="sxs-lookup"><span data-stu-id="37e3c-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="37e3c-118">Actualmente solo se admiten las implementaciones de organizaciones de Exchange de un solo bosque.</span><span class="sxs-lookup"><span data-stu-id="37e3c-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="37e3c-119">Si tiene más de una organización de Exchange en local, a continuación, necesita una local GALSync solución para estos tooappear grupos en los otros bosques.</span><span class="sxs-lookup"><span data-stu-id="37e3c-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="37e3c-120">característica de reescritura de grupos de Hello no controla los grupos de seguridad o grupos de distribución.</span><span class="sxs-lookup"><span data-stu-id="37e3c-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="37e3c-121">Un tooAzure de suscripción AD Premium es necesario para la reescritura de grupos.</span><span class="sxs-lookup"><span data-stu-id="37e3c-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="37e3c-122">Reescritura de usuarios</span><span class="sxs-lookup"><span data-stu-id="37e3c-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="37e3c-123">Hello característica de vista previa de reescritura de usuario se quitó en tooAzure de actualización de agosto de 2015 Hola AD Connect.</span><span class="sxs-lookup"><span data-stu-id="37e3c-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="37e3c-124">Si la ha habilitado, debería deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="37e3c-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="37e3c-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37e3c-125">Next steps</span></span>
<span data-ttu-id="37e3c-126">Continúe su [Instalación personalizada de Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="37e3c-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="37e3c-127">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="37e3c-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
