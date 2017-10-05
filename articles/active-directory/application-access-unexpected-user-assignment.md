---
title: "Asignación de usuarios a las aplicaciones | Microsoft Docs"
description: "Descripción de cómo se asignan los usuarios a una aplicación del inquilino"
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="46466-103">Asignación de usuarios a las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="46466-103">How to assign users to applications</span></span>

<span data-ttu-id="46466-104">Este artículo le ayudará a comprender cómo se asignan los usuarios a una aplicación del inquilino.</span><span class="sxs-lookup"><span data-stu-id="46466-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="46466-105">¿Cómo se asignan los usuarios a una aplicación de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="46466-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="46466-106">Para que un usuario tenga acceso a una aplicación, se le debe primero asignar a ella de alguna forma.</span><span class="sxs-lookup"><span data-stu-id="46466-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="46466-107">Un administrador, un delegado de la empresa o, en ocasiones, el usuario mismo puede realizar esta asignación.</span><span class="sxs-lookup"><span data-stu-id="46466-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="46466-108">A continuación se describen las maneras en las que se pueden asignar los usuarios a las aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="46466-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="46466-109">Un administrador [asigna un usuario](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) a la aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="46466-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="46466-110">Un administrador [asigna un grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal), del que el usuario forma parte, a la aplicación, incluidos:</span><span class="sxs-lookup"><span data-stu-id="46466-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="46466-111">Un grupo que se ha sincronizado de forma local</span><span class="sxs-lookup"><span data-stu-id="46466-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="46466-112">Un grupo de seguridad estático creado en la nube</span><span class="sxs-lookup"><span data-stu-id="46466-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="46466-113">Un [grupo de seguridad dinámico](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) creado en la nube</span><span class="sxs-lookup"><span data-stu-id="46466-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="46466-114">Un grupo de Office 365 creado en la nube</span><span class="sxs-lookup"><span data-stu-id="46466-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="46466-115">El grupo [Todos los usuarios](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups)</span><span class="sxs-lookup"><span data-stu-id="46466-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="46466-116">Un administrador habilita [Acceso de autoservicio a las aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) para permitir que un usuario pueda agregar una aplicación mediante la característica **Agregar aplicación** del [panel de acceso a las aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **sin la aprobación de la empresa**</span><span class="sxs-lookup"><span data-stu-id="46466-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="46466-117">Un administrador habilita [Acceso de autoservicio a las aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) para permitir que un usuario pueda agregar una aplicación mediante la característica **Agregar aplicación** del [panel de acceso a las aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) pero solo **con la aprobación anterior de un conjunto seleccionado de aprobadores de la empresa**</span><span class="sxs-lookup"><span data-stu-id="46466-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="46466-118">Un administrador habilita [Administración de grupos de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) para permitir que un usuario se una a un grupo al que se ha asignado una aplicación **sin la aprobación de la empresa**</span><span class="sxs-lookup"><span data-stu-id="46466-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="46466-119">Un administrador habilita [Administración de grupos de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) para permitir que un usuario se una a un grupo al que se ha asignado una aplicación pero solo **con la aprobación anterior de un conjunto seleccionado de aprobadores de la empresa**</span><span class="sxs-lookup"><span data-stu-id="46466-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="46466-120">Un administrador asigna una licencia a un usuario directamente para una aplicación original de Microsoft, como [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="46466-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="46466-121">Un administrador asigna una licencia a un grupo del que el usuario forma parte para una aplicación original de Microsoft, como [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="46466-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="46466-122">Un [administrador da su consentimiento a una aplicación](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) para que la usen todos los usuarios y, a continuación, un usuario inicia sesión en ella</span><span class="sxs-lookup"><span data-stu-id="46466-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="46466-123">Un usuario [da su consentimiento a una aplicación](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) por sí mismo iniciando sesión en ella directamente</span><span class="sxs-lookup"><span data-stu-id="46466-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="46466-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46466-124">Next steps</span></span>
[<span data-ttu-id="46466-125">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46466-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
