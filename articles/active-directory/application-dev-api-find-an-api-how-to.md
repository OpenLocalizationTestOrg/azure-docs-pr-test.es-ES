---
title: "Búsqueda de una API específica necesaria para una aplicación desarrollada internamente | Microsoft Docs"
description: "Configuración de los permisos necesarios para acceder a una API determinada en una aplicación desarrollada internamente con Azure AD"
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
ms.openlocfilehash: e0c07fd030339d025894520500d2cd948d31af45
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="4edff-103">Búsqueda de una API específica necesaria para una aplicación desarrollada internamente</span><span class="sxs-lookup"><span data-stu-id="4edff-103">How to find a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="4edff-104">El acceso a API requiere configurar los ámbitos y roles de acceso.</span><span class="sxs-lookup"><span data-stu-id="4edff-104">Access to APIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="4edff-105">Si desea exponer su API web de aplicaciones de recursos a aplicaciones cliente, debe configurar los roles y ámbitos de acceso de la API.</span><span class="sxs-lookup"><span data-stu-id="4edff-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span></span> <span data-ttu-id="4edff-106">Si desea que una aplicación cliente pueda acceder a una API web, debe configurar los permisos de acceso a la API en el registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4edff-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span></span>

## <a name="configuring-a-resource-application-to-expose-web-apis"></a><span data-ttu-id="4edff-107">Configuración de una aplicación de recursos para exponer las API web</span><span class="sxs-lookup"><span data-stu-id="4edff-107">Configuring a resource application to expose web APIs</span></span>

<span data-ttu-id="4edff-108">Al exponer la API web, la API se muestra en la lista **Seleccionar una API** al agregar permisos al registro de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="4edff-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span></span> <span data-ttu-id="4edff-109">Para agregar ámbitos de acceso, siga los pasos descritos en [Agregar ámbitos de acceso a la aplicación de recursos](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="4edff-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-to-access-web-apis"></a><span data-ttu-id="4edff-110">Configuración de una aplicación cliente para acceder a las API web</span><span class="sxs-lookup"><span data-stu-id="4edff-110">Configuring a client application to access web APIs</span></span>

<span data-ttu-id="4edff-111">Al agregar permisos al registro de la aplicación, también puede **agregar acceso a API** a las API web expuestas.</span><span class="sxs-lookup"><span data-stu-id="4edff-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span></span> <span data-ttu-id="4edff-112">Para acceder a API web, siga los pasos descritos en [Para agregar credenciales o permisos para acceder a las API web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="4edff-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4edff-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4edff-113">Next steps</span></span>

-   [<span data-ttu-id="4edff-114">Integración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4edff-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="4edff-115">Descripción del manifiesto de aplicación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4edff-115">Understanding the Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


