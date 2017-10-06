---
title: aaaUnlicensed informe de uso | Documentos de Microsoft
description: "Hola informes de uso sin licencia ayuda a que identificar a los usuarios sin licencia que usan características de Azure AD de pago."
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
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="a0d35-103">Informe de uso sin licencia</span><span class="sxs-lookup"><span data-stu-id="a0d35-103">Unlicensed usage report</span></span>
<span data-ttu-id="a0d35-104">Hola informes de uso sin licencia ayuda a que identificar a los usuarios sin licencia que usan características de Azure AD de pago.</span><span class="sxs-lookup"><span data-stu-id="a0d35-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="a0d35-105">Esto le permite toomake un mejor uso de licencias que ha adquirido y tooidentify sabrá cuando necesite obtener licencias adicionales.</span><span class="sxs-lookup"><span data-stu-id="a0d35-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="a0d35-106">informe de Hello muestra el uso de activo de hello características de pago en hello últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="a0d35-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="a0d35-107">Estructura del informe</span><span class="sxs-lookup"><span data-stu-id="a0d35-107">Report structure</span></span>
| <span data-ttu-id="a0d35-108">Nombre de la columna</span><span class="sxs-lookup"><span data-stu-id="a0d35-108">Column name</span></span> | <span data-ttu-id="a0d35-109">Descripción</span><span class="sxs-lookup"><span data-stu-id="a0d35-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a0d35-110">Usuario sin licencia</span><span class="sxs-lookup"><span data-stu-id="a0d35-110">Unlicensed User</span></span> |<span data-ttu-id="a0d35-111">Nombre de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="a0d35-111">Name of hello user</span></span> |
| <span data-ttu-id="a0d35-112">Característica</span><span class="sxs-lookup"><span data-stu-id="a0d35-112">Feature</span></span> |<span data-ttu-id="a0d35-113">nombre de la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0d35-113">hello feature name.</span></span> <span data-ttu-id="a0d35-114">Por ejemplo: acceso condicional</span><span class="sxs-lookup"><span data-stu-id="a0d35-114">For example: conditional access</span></span> |
| <span data-ttu-id="a0d35-115">Aplicación a la que se accede</span><span class="sxs-lookup"><span data-stu-id="a0d35-115">Application Accessed</span></span> |<span data-ttu-id="a0d35-116">nombre de Hola de aplicación Hola que se tiene acceso con la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0d35-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="a0d35-117">Por ejemplo: Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a0d35-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="a0d35-118">Si se ha eliminado una cuenta de usuario Hola 'Sin licencia User' columna se rellenará con el identificador, como 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="a0d35-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="a0d35-119">Características de acceso condicional</span><span class="sxs-lookup"><span data-stu-id="a0d35-119">Conditional access feature</span></span>
<span data-ttu-id="a0d35-120">A los usuarios sin licencia se les marcará cuando accedan a un servicio al que se haya aplicado la directiva de acceso condicional, siempre que no tengan una licencia de Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="a0d35-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="a0d35-121">Esto aplica tooMFA / directivas de ubicación, así como dispositivo directivas que usar Intune.</span><span class="sxs-lookup"><span data-stu-id="a0d35-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="a0d35-122">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a0d35-122">See also</span></span>
* [<span data-ttu-id="a0d35-123">Protección del acceso a Office 365 y otras aplicaciones conectadas a Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0d35-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="a0d35-124">Introducción a acceso condicional tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="a0d35-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

