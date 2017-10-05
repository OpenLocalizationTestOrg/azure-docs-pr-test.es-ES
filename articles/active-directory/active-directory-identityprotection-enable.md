---
title: "Habilitación de Azure Active Directory Identity Protection | Microsoft Docs"
description: "Sepa cómo habilitar Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e0683e837086ca08f4b4b3f49695bdd2b4063ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="de771-104">Habilitación de Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="de771-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="de771-105">Azure Active Directory Identity Protection es una nueva funcionalidad que proporciona una vista consolidada de las actividades de inicio de sesión sospechosas y las posibles vulnerabilidades, además de notificaciones, recomendaciones de solución y directivas basadas en riesgos que lo ayudarán a proteger su negocio.</span><span class="sxs-lookup"><span data-stu-id="de771-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="de771-106">El servicio detecta las actividades sospechosas de usuarios finales e identidades con privilegios (administrador) según determinadas señales, como ataques por fuerza bruta, pérdida de credenciales, inicios de sesión de ubicaciones desconocidas y dispositivos infectados. El objetivo es ofrecer una protección en tiempo real frente a estas actividades.</span><span class="sxs-lookup"><span data-stu-id="de771-106">The service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, to protect against these activities in real-time.</span></span> <span data-ttu-id="de771-107">Y lo que es más importante, se calcula la gravedad del riesgo para el usuario según estas actividades sospechosas y pueden configurarse directivas basadas en riesgos para proteger automáticamente las identidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="de771-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect the identities of your organization.</span></span> <span data-ttu-id="de771-108">Para más información, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="de771-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="de771-109">En este tema se muestra cómo habilitar Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="de771-109">This topics shows how to enable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-to-enable-azure-active-directory-identity-protection"></a><span data-ttu-id="de771-110">Pasos para habilitar Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="de771-110">Steps to enable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="de771-111">[Inicie sesión](https://ms.portal.azure.com/) en Azure Portal como administrador.</span><span class="sxs-lookup"><span data-stu-id="de771-111">[Sign-on](https://ms.portal.azure.com/) to your Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="de771-112">En Azure Portal, haga clic en **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="de771-112">In the Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="de771-113">![Crear](./media/active-directory-identityprotection-enable/01.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="de771-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="de771-114">En la lista de aplicaciones, haga clic en **Seguridad e identidad**.</span><span class="sxs-lookup"><span data-stu-id="de771-114">In the applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="de771-115">![Crear](./media/active-directory-identityprotection-enable/02.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="de771-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="de771-116">Haga clic en **Azure AD Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="de771-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="de771-117">![Crear](./media/active-directory-identityprotection-enable/03.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="de771-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="de771-118">En la hoja **Azure AD Identity Protection**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="de771-118">On the **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="de771-119">![Crear](./media/active-directory-identityprotection-enable/04.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="de771-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="de771-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de771-120">Next Steps</span></span>
* [<span data-ttu-id="de771-121">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="de771-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

