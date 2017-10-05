---
title: "Aplicación de extensiones: Azure AD B2C | Microsoft Docs"
description: "Restauración de b2c-extensions-app"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: 17500b572a0e92c1c233c6967840a5b6d96e21cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="547f3-103">Azure AD B2C: aplicación de extensiones</span><span class="sxs-lookup"><span data-stu-id="547f3-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="547f3-104">Al crearse un directorio de Azure AD B2C, se crea automáticamente una aplicación denominada `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` dentro del nuevo directorio.</span><span class="sxs-lookup"><span data-stu-id="547f3-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside the new directory.</span></span> <span data-ttu-id="547f3-105">Esta aplicación, llamada **b2c-extensions-app**, se puede ver en *Registros de aplicaciones*.</span><span class="sxs-lookup"><span data-stu-id="547f3-105">This app, referred to as the **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="547f3-106">El servicio Azure AD B2C la usa para almacenar información sobre usuarios y atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="547f3-106">It is used by the Azure AD B2C service to store information about users and custom attributes.</span></span> <span data-ttu-id="547f3-107">Si se elimina la aplicación, Azure AD B2C no funcionará correctamente y su entorno de producción se verá afectado.</span><span class="sxs-lookup"><span data-stu-id="547f3-107">If the app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="547f3-108">No elimine b2c-extensions-app a menos que tenga previsto eliminar el inquilino inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="547f3-108">Do not delete the b2c-extensions-app unless you are planning to immediately delete your tenant.</span></span> <span data-ttu-id="547f3-109">Si la aplicación permanece eliminada durante más de 30 días, la información del usuario se perderá permanentemente.</span><span class="sxs-lookup"><span data-stu-id="547f3-109">If the app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-the-extensions-app-is-present"></a><span data-ttu-id="547f3-110">Comprobación de que la aplicación de extensiones está presente</span><span class="sxs-lookup"><span data-stu-id="547f3-110">Verifying that the extensions app is present</span></span>

<span data-ttu-id="547f3-111">Para comprobar que b2c-extensions-app está presente:</span><span class="sxs-lookup"><span data-stu-id="547f3-111">To verify that the b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="547f3-112">En el inquilino de Azure AD B2C, haga clic en **Más servicios** en el menú de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="547f3-112">Inside your Azure AD B2C tenant, click on **More services** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="547f3-113">Busque y abra **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="547f3-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="547f3-114">Busque una aplicación que empiece por **b2c-extensions-app**.</span><span class="sxs-lookup"><span data-stu-id="547f3-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-the-extensions-app"></a><span data-ttu-id="547f3-115">Recuperación de la aplicación de extensiones</span><span class="sxs-lookup"><span data-stu-id="547f3-115">Recover the extensions app</span></span>

<span data-ttu-id="547f3-116">Si ha eliminado b2c-extensions-app accidentalmente, tiene 30 días para recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="547f3-116">If you accidentally deleted the b2c-extensions-app, you have 30 days to recover it.</span></span> <span data-ttu-id="547f3-117">Puede restaurar la aplicación mediante la API Graph:</span><span class="sxs-lookup"><span data-stu-id="547f3-117">You can restore the app using the Graph API:</span></span>

1. <span data-ttu-id="547f3-118">Vaya a [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="547f3-118">Browse to [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="547f3-119">Inicie sesión en el sitio como administrador global para el directorio de Azure AD B2C para el que desea restaurar la aplicación eliminada.</span><span class="sxs-lookup"><span data-stu-id="547f3-119">Log in to the site as a global administrator for the Azure AD B2C directory that you want to restore the deleted app for.</span></span>
1. <span data-ttu-id="547f3-120">Emita HTTP GET en la dirección URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` con api-version=1.6.</span><span class="sxs-lookup"><span data-stu-id="547f3-120">Issue an HTTP GET against the URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="547f3-121">Asegúrese de reemplazar `{tenantName}` por el nombre del inquilino.</span><span class="sxs-lookup"><span data-stu-id="547f3-121">Make sure to replace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="547f3-122">Esta operación enumerará todas las aplicaciones que se han eliminado en los últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="547f3-122">This operation will list all of the applications that have been deleted within the past 30 days.</span></span>
1. <span data-ttu-id="547f3-123">Busque la aplicación en la lista cuyo nombre comienza por "b2c-extension-app" y copie su valor de propiedad `objectid`.</span><span class="sxs-lookup"><span data-stu-id="547f3-123">Find the application in the list where the name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="547f3-124">Emita HTTP POST en la dirección URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="547f3-124">Issue an HTTP POST against the URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="547f3-125">Reemplace la parte `{OBJECTID}` de la dirección URL por `objectid` del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="547f3-125">Replace the `{OBJECTID}` portion of the URL with the `objectid` from the previous step.</span></span> 

<span data-ttu-id="547f3-126">Ahora debería poder [ver la aplicación restaurada](#verifying-that-the-extensions-app-is-present) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="547f3-126">You should now be able to [see the restored app](#verifying-that-the-extensions-app-is-present) in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="547f3-127">Una aplicación solo se puede restaurar si se ha eliminado en los últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="547f3-127">An application can only be restored if it has been deleted within the last 30 days.</span></span> <span data-ttu-id="547f3-128">Si han pasado más de 30 días, los datos se perderán permanentemente.</span><span class="sxs-lookup"><span data-stu-id="547f3-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="547f3-129">Para obtener más ayuda, abra una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="547f3-129">For more assistance, file a support ticket.</span></span>