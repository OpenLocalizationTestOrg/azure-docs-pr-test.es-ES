---
title: "Cómo quitar el acceso de un usuario a una aplicación | Microsoft Docs"
description: "Cómo quitar el acceso de un usuario a una aplicación"
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
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="bde10-103">Cómo quitar el acceso de un usuario a una aplicación</span><span class="sxs-lookup"><span data-stu-id="bde10-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="bde10-104">Este artículo le ayudará a entender cómo quitar el acceso de un usuario a una aplicación.</span><span class="sxs-lookup"><span data-stu-id="bde10-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="bde10-105">Deseo quitar la asignación de un usuario o grupo específicos a una aplicación</span><span class="sxs-lookup"><span data-stu-id="bde10-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="bde10-106">Para quitar la asignación de un usuario o grupo a una aplicación, siga los pasos indicados en el artículo [Eliminación de asignaciones de usuario o grupo de una aplicación empresarial en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="bde10-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="bde10-107">. ## Quiero deshabilitar el acceso a una aplicación para todos los usuarios</span><span class="sxs-lookup"><span data-stu-id="bde10-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="bde10-108">Para deshabilitar todos los inicios de sesión de usuarios a una aplicación, siga los pasos indicados en el artículo [Deshabilitación de los inicios de sesión de usuario de una aplicación empresarial en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="bde10-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="bde10-109">Quiero eliminar una aplicación por completo</span><span class="sxs-lookup"><span data-stu-id="bde10-109">I want to delete an application entirely</span></span>

<span data-ttu-id="bde10-110">Para **eliminar una aplicación**, siga las instrucciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="bde10-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="bde10-111">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="bde10-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bde10-112">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="bde10-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bde10-113">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bde10-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bde10-114">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bde10-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bde10-115">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bde10-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="bde10-116">Si no ve que la aplicación que desea aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="bde10-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="bde10-117">Seleccione la aplicación que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="bde10-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="bde10-118">Una vez que se carga la aplicación, haga clic en el icono **Eliminar** de la hoja **Introducción** de la aplicación situada en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="bde10-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="bde10-119">Quiero deshabilitar todas las operaciones de consentimiento de usuario futuras para todas las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bde10-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="bde10-120">Deshabilitar el consentimiento del usuario para todo el directorio impide que los usuarios finales den consentimiento a cualquier aplicación.</span><span class="sxs-lookup"><span data-stu-id="bde10-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="bde10-121">A pesar de ello, los administradores podrán seguir dando el consentimiento en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="bde10-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="bde10-122">Para más información sobre el consentimiento de aplicación y los motivos por los que es posible que quiera o no quiera hacer esto, lea el artículo [Descripción del consentimiento de usuario y administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="bde10-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="bde10-123">Para **deshabilitar todas las operaciones de consentimiento de usuario futuras en todo el directorio**, siga las instrucciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="bde10-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="bde10-124">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="bde10-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bde10-125">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="bde10-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bde10-126">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bde10-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bde10-127">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="bde10-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="bde10-128">Haga clic en **Configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="bde10-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="bde10-129">Deshabilite todas las operaciones de consentimiento de usuario futuras estableciendo la opción **Los usuarios pueden permitir que las aplicaciones accedan a sus datos** en **No**. Después, haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bde10-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="bde10-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bde10-130">Next steps</span></span>
[<span data-ttu-id="bde10-131">Administración del acceso a las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bde10-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
