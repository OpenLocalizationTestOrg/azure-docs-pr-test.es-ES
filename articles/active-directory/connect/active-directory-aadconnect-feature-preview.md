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
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="ea114-103">Más detalles sobre las características de vista previa</span><span class="sxs-lookup"><span data-stu-id="ea114-103">More details about features in preview</span></span>
<span data-ttu-id="ea114-104">En este tema se describe cómo usar las características que actualmente forman parte de la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="ea114-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="ea114-105">Escritura diferida de grupos</span><span class="sxs-lookup"><span data-stu-id="ea114-105">Group writeback</span></span>
<span data-ttu-id="ea114-106">La opción para la escritura diferida de grupos en las características opcionales le permitirá escribir en diferido **Grupos de Office 365** en un bosque con Exchange instalado.</span><span class="sxs-lookup"><span data-stu-id="ea114-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="ea114-107">Se trata de un tipo de grupo que siempre se controla en la nube.</span><span class="sxs-lookup"><span data-stu-id="ea114-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="ea114-108">Si dispone de Exchange local, puede reescribir estos grupos en el entono local, por lo que los usuarios con un buzón de Exchange local pueden enviar y recibir correos electrónicos de ellos.</span><span class="sxs-lookup"><span data-stu-id="ea114-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="ea114-109">Puede encontrar más información sobre los grupos de Office 365 y cómo utilizarlos [aquí](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="ea114-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="ea114-110">Este grupo de Office 365 se representará como un grupo de distribución en AD DS local.</span><span class="sxs-lookup"><span data-stu-id="ea114-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="ea114-111">El servidor de Exchange local debe tener la actualización acumulativa 8 de Exchange 2013 (publicada en marzo de 2015) o Exchange 2016 para reconocer este nuevo tipo de grupo.</span><span class="sxs-lookup"><span data-stu-id="ea114-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="ea114-112">**Notas durante la vista previa**</span><span class="sxs-lookup"><span data-stu-id="ea114-112">**Notes during the preview**</span></span>

* <span data-ttu-id="ea114-113">En la vista previa no se rellena actualmente el atributo de libreta de direcciones.</span><span class="sxs-lookup"><span data-stu-id="ea114-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="ea114-114">Sin este atributo, el grupo no estará visible en la GAL.</span><span class="sxs-lookup"><span data-stu-id="ea114-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="ea114-115">La manera más fácil de rellenar este atributo es usar el cmdlet de Exchange PowerShell `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="ea114-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="ea114-116">Solo los bosques con el esquema de Exchange son destinos válidos para los grupos.</span><span class="sxs-lookup"><span data-stu-id="ea114-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="ea114-117">Si no se ha detectado ningún Exchange, no se podrá habilitar la reescritura de grupos.</span><span class="sxs-lookup"><span data-stu-id="ea114-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="ea114-118">Actualmente solo se admiten las implementaciones de organizaciones de Exchange de un solo bosque.</span><span class="sxs-lookup"><span data-stu-id="ea114-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="ea114-119">Si tiene más de una organización de Exchange local, necesitará una solución de GALSync local para que estos grupos aparezcan en los demás bosques.</span><span class="sxs-lookup"><span data-stu-id="ea114-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="ea114-120">La característica Reescritura de grupos no controla actualmente los grupos de seguridad ni los grupos de distribución.</span><span class="sxs-lookup"><span data-stu-id="ea114-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="ea114-121">Se necesita una suscripción a Azure AD Premium para la escritura diferida de grupos.</span><span class="sxs-lookup"><span data-stu-id="ea114-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="ea114-122">Reescritura de usuarios</span><span class="sxs-lookup"><span data-stu-id="ea114-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ea114-123">La característica en vista previa de escritura diferida de usuario, se quitó en la actualización de agosto de 2015 a Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ea114-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="ea114-124">Si la ha habilitado, debería deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="ea114-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ea114-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea114-125">Next steps</span></span>
<span data-ttu-id="ea114-126">Continúe su [Instalación personalizada de Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ea114-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="ea114-127">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ea114-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
