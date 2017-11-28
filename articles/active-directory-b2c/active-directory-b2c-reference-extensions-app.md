---
title: "Aplicación de extensiones: Azure AD B2C | Microsoft Docs"
description: "Restaurar Hola b2c extensiones de aplicación"
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
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="6a743-103">Azure AD B2C: aplicación de extensiones</span><span class="sxs-lookup"><span data-stu-id="6a743-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="6a743-104">Cuando se crea un directorio de Azure AD B2C, llama a una aplicación `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` automáticamente se crea dentro de hello nuevo directorio.</span><span class="sxs-lookup"><span data-stu-id="6a743-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="6a743-105">Esta aplicación, que se hace referencia tooas Hola **b2c-extensiones-app**, está visible en *registros de aplicación*.</span><span class="sxs-lookup"><span data-stu-id="6a743-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="6a743-106">Se utiliza por hello Azure AD B2C toostore información sobre los usuarios y los atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="6a743-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="6a743-107">Si se elimina la aplicación hello, Azure AD B2C no funcionará correctamente y el entorno de producción se verán afectado.</span><span class="sxs-lookup"><span data-stu-id="6a743-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a743-108">No elimine Hola b2c extensiones de aplicación, a menos que piensa eliminar tooimmediately el inquilino.</span><span class="sxs-lookup"><span data-stu-id="6a743-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="6a743-109">Si la aplicación hello permanece eliminado durante más de 30 días, información de usuario se perderá permanentemente.</span><span class="sxs-lookup"><span data-stu-id="6a743-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="6a743-110">Comprobar que las extensiones de la aplicación hello está presente</span><span class="sxs-lookup"><span data-stu-id="6a743-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="6a743-111">tooverify que Hola b2c-extensiones-app está presente:</span><span class="sxs-lookup"><span data-stu-id="6a743-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="6a743-112">Dentro de su inquilino de Azure AD B2C, haga clic en **más servicios** en el menú de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a743-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="6a743-113">Busque y abra **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6a743-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="6a743-114">Busque una aplicación que empiece por **b2c-extensions-app**.</span><span class="sxs-lookup"><span data-stu-id="6a743-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="6a743-115">Recuperar la aplicación de las extensiones de hello</span><span class="sxs-lookup"><span data-stu-id="6a743-115">Recover hello extensions app</span></span>

<span data-ttu-id="6a743-116">Si elimina accidentalmente Hola b2c extensiones de aplicación, tendrá que toorecover de 30 días se.</span><span class="sxs-lookup"><span data-stu-id="6a743-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="6a743-117">Puede restaurar la aplicación hello mediante Hola API Graph:</span><span class="sxs-lookup"><span data-stu-id="6a743-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="6a743-118">Examinar demasiado[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="6a743-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="6a743-119">Inicie sesión en el sitio de toohello como administrador global para el directorio de Azure AD B2C Hola que desee toorestore Hola Eliminar aplicación para.</span><span class="sxs-lookup"><span data-stu-id="6a743-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="6a743-120">Emitir una solicitud HTTP GET en la dirección URL de hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` con api-version = 1.6.</span><span class="sxs-lookup"><span data-stu-id="6a743-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="6a743-121">Asegúrese de que tooreplace `{tenantName}` con el nombre del inquilino.</span><span class="sxs-lookup"><span data-stu-id="6a743-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="6a743-122">Esta operación enumera todas las aplicaciones de Hola que se han eliminado en hello últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="6a743-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="6a743-123">Busque aplicación hello en lista de Hola donde nombre de hello comienza con 'aplicación de extensión b2c' y copie su `objectid` valor de propiedad.</span><span class="sxs-lookup"><span data-stu-id="6a743-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="6a743-124">Emitir una solicitud HTTP POST con la dirección URL de hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="6a743-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="6a743-125">Reemplace hello `{OBJECTID}` parte de la dirección URL de hello con hello `objectid` del paso anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="6a743-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="6a743-126">Ahora debe poder demasiado[vea aplicación hello restaurar](#verifying-that-the-extensions-app-is-present) Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a743-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6a743-127">Una aplicación sólo puede restaurarse si se ha eliminado en hello últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="6a743-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="6a743-128">Si han pasado más de 30 días, los datos se perderán permanentemente.</span><span class="sxs-lookup"><span data-stu-id="6a743-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="6a743-129">Para obtener más ayuda, abra una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="6a743-129">For more assistance, file a support ticket.</span></span>
