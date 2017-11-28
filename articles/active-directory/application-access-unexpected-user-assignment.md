---
title: aaaHow tooAssign usuarios tooapplications | Documentos de Microsoft
description: "Comprender cómo los usuarios se asignen tooan aplicación en su inquilino"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="a8b96-103">¿Cómo tooassign usuarios tooapplications</span><span class="sxs-lookup"><span data-stu-id="a8b96-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="a8b96-104">En este artículo le ayudarán a toounderstand cómo los usuarios se asignen tooan aplicación en su inquilino.</span><span class="sxs-lookup"><span data-stu-id="a8b96-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="a8b96-105">¿Cómo los usuarios se asignen tooan aplicación en Azure AD?</span><span class="sxs-lookup"><span data-stu-id="a8b96-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="a8b96-106">Para un usuario se tooaccess una aplicación, debe estar asignados tooit de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="a8b96-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="a8b96-107">Asignación puede realizarla un administrador, un delegado de negocio o a veces, Hola usuario por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="a8b96-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="a8b96-108">A continuación describe las formas de hello los usuarios pueden obtener asignar tooapplications:</span><span class="sxs-lookup"><span data-stu-id="a8b96-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="a8b96-109">Un administrador [asigna un usuario](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="a8b96-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="a8b96-110">Un administrador [asigna un grupo de](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) ese usuario hello es un miembro de la aplicación toohello, incluidos:</span><span class="sxs-lookup"><span data-stu-id="a8b96-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="a8b96-111">Un grupo que se ha sincronizado de forma local</span><span class="sxs-lookup"><span data-stu-id="a8b96-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="a8b96-112">Un grupo de seguridad estático creado en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="a8b96-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="a8b96-113">A [grupo de seguridad dinámica](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) creado en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="a8b96-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="a8b96-114">Un grupo de Office 365 creado en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="a8b96-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="a8b96-115">Hola [todos los usuarios](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grupo</span><span class="sxs-lookup"><span data-stu-id="a8b96-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="a8b96-116">Un administrador habilita [autoservicio acceso a la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow un tooadd de usuario una aplicación usando Hola [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Agregar aplicación** característica **sin la aprobación de negocios**</span><span class="sxs-lookup"><span data-stu-id="a8b96-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="a8b96-117">Un administrador habilita [autoservicio acceso a la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow un tooadd de usuario una aplicación usando Hola [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Agregar aplicación** característica, pero solo w **i-ésimo autorización previa de un conjunto seleccionado de aprobadores de negocios**</span><span class="sxs-lookup"><span data-stu-id="a8b96-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="a8b96-118">Un administrador habilita [administración de grupos de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow un toojoin un grupo que se asigna demasiado una aplicación de usuario**sin la aprobación de negocios**</span><span class="sxs-lookup"><span data-stu-id="a8b96-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="a8b96-119">Un administrador habilita [administración de grupos de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow un toojoin de usuario un grupo que se asigna una aplicación a, pero solo **con la aprobación previa de un conjunto seleccionado de aprobadores de negocios**</span><span class="sxs-lookup"><span data-stu-id="a8b96-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="a8b96-120">Un administrador asigna un usuario de tooa de licencia directamente para una primera aplicación de usuario, como [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="a8b96-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="a8b96-121">Un administrador asigna un grupo de tooa de licencias que Hola usuario es miembro de tooa primera aplicación de usuario, como [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="a8b96-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="a8b96-122">Un [administrador consiente aplicación tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe utilizado por todos los usuarios y, a continuación, un usuario inicia sesión en la aplicación de toohello</span><span class="sxs-lookup"><span data-stu-id="a8b96-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="a8b96-123">Un usuario [da su consentimiento tooan aplicación](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) por sí mismos, debe iniciar sesión en la aplicación de toohello</span><span class="sxs-lookup"><span data-stu-id="a8b96-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8b96-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8b96-124">Next steps</span></span>
[<span data-ttu-id="a8b96-125">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8b96-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
