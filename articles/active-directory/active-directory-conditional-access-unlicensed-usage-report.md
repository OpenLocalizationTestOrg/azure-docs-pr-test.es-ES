---
title: Informe de uso sin licencia | Microsoft Docs
description: "El informe de uso sin licencia ayuda a identificar usuarios sin licencia que utilizan características de Azure AD de pago,"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="c4262-103">Informe de uso sin licencia</span><span class="sxs-lookup"><span data-stu-id="c4262-103">Unlicensed usage report</span></span>
<span data-ttu-id="c4262-104">El informe de uso sin licencia ayuda a identificar usuarios sin licencia que utilizan características de Azure AD de pago,</span><span class="sxs-lookup"><span data-stu-id="c4262-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="c4262-105">lo que permite hacer un mejor uso de las licencias que se han adquirido e identificar en qué momento se necesitan más licencias.</span><span class="sxs-lookup"><span data-stu-id="c4262-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="c4262-106">El informe muestra el uso activo de las características de pago en los últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="c4262-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="c4262-107">Estructura del informe</span><span class="sxs-lookup"><span data-stu-id="c4262-107">Report structure</span></span>
| <span data-ttu-id="c4262-108">Nombre de la columna</span><span class="sxs-lookup"><span data-stu-id="c4262-108">Column name</span></span> | <span data-ttu-id="c4262-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="c4262-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c4262-110">Usuario sin licencia</span><span class="sxs-lookup"><span data-stu-id="c4262-110">Unlicensed User</span></span> |<span data-ttu-id="c4262-111">Nombre del usuario</span><span class="sxs-lookup"><span data-stu-id="c4262-111">Name of the user</span></span> |
| <span data-ttu-id="c4262-112">Característica</span><span class="sxs-lookup"><span data-stu-id="c4262-112">Feature</span></span> |<span data-ttu-id="c4262-113">El nombre de la característica.</span><span class="sxs-lookup"><span data-stu-id="c4262-113">The feature name.</span></span> <span data-ttu-id="c4262-114">Por ejemplo: acceso condicional</span><span class="sxs-lookup"><span data-stu-id="c4262-114">For example: conditional access</span></span> |
| <span data-ttu-id="c4262-115">Aplicación a la que se accede</span><span class="sxs-lookup"><span data-stu-id="c4262-115">Application Accessed</span></span> |<span data-ttu-id="c4262-116">El nombre de la aplicación a la que se accede con la característica.</span><span class="sxs-lookup"><span data-stu-id="c4262-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="c4262-117">Por ejemplo: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="c4262-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="c4262-118">Si se ha eliminado una cuenta de usuario, la columna "Usuario sin licencia" se rellenará con un identificador, como 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="c4262-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="c4262-119">Características de acceso condicional</span><span class="sxs-lookup"><span data-stu-id="c4262-119">Conditional access feature</span></span>
<span data-ttu-id="c4262-120">A los usuarios sin licencia se les marcará cuando accedan a un servicio al que se haya aplicado la directiva de acceso condicional, siempre que no tengan una licencia de Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="c4262-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="c4262-121">Esto se aplica a las directivas de MFA/ubicación, así como a las directivas de dispositivos que usan Intune.</span><span class="sxs-lookup"><span data-stu-id="c4262-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="c4262-122">Consulte también</span><span class="sxs-lookup"><span data-stu-id="c4262-122">See also</span></span>
* [<span data-ttu-id="c4262-123">Protección del acceso a Office 365 y otras aplicaciones conectadas a Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4262-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="c4262-124">Introducción al acceso condicional a Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4262-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

