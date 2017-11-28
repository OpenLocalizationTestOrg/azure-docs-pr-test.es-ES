---
title: "aaaHow toofind una API específica necesaria para que una aplicación desarrollados de forma personalizada | Documentos de Microsoft"
description: "Cómo permisos de hello tooconfigure necesita tooaccess una API determinada en su personalizado desarrollan aplicación de Azure AD"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="bef44-103">¿Cómo toofind una API específica necesaria para una aplicación desarrollados de forma personalizada</span><span class="sxs-lookup"><span data-stu-id="bef44-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="bef44-104">Acceso tooAPIs requieren la configuración de roles y ámbitos de acceso.</span><span class="sxs-lookup"><span data-stu-id="bef44-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="bef44-105">Si desea tooexpose las aplicaciones de tooclient de las API de recursos aplicación web, necesitará roles y ámbitos de acceso de tooconfigure para hello API.</span><span class="sxs-lookup"><span data-stu-id="bef44-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="bef44-106">Si desea que un tooaccess de aplicación cliente una API web, deberá tooconfigure permisos tooaccess Hola API en el registro de una aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="bef44-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="bef44-107">Configuración de una aplicación de recursos tooexpose web API</span><span class="sxs-lookup"><span data-stu-id="bef44-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="bef44-108">Al exponer su API, web Hola API se muestran en hello **seleccionar una API** lista al agregar el registro de la aplicación de permisos tooan.</span><span class="sxs-lookup"><span data-stu-id="bef44-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="bef44-109">ámbitos de acceso tooadd, siga los pasos de hello descritos en [agregar acceso establece el ámbito de aplicación de recursos de tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="bef44-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="bef44-110">Configurar una aplicación de cliente tooaccess web API</span><span class="sxs-lookup"><span data-stu-id="bef44-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="bef44-111">Cuando se agrega el registro de la aplicación de permisos tooyour, puede **agregar acceso de API** tooexposed web API.</span><span class="sxs-lookup"><span data-stu-id="bef44-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="bef44-112">tooaccess las API web, siga los pasos de hello descritos en [agregar las API web de las credenciales o permisos tooaccess](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="bef44-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bef44-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bef44-113">Next steps</span></span>

-   [<span data-ttu-id="bef44-114">Integración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bef44-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="bef44-115">Descripción de manifiesto de aplicación de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="bef44-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


