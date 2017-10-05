---
title: "Introducción a Azure AD en proyectos de WebApi de Visual Studio | Microsoft Docs"
description: "Cómo empezar a usar Azure Active Directory en los proyectos de WebApi después de crear un Azure AD usando los servicios conectados de Visual Studio o de conectarse a él"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="9671d-103">Introducción a Azure Active Directory y servicios conectados de Visual Studio (proyectos de WebApi)</span><span class="sxs-lookup"><span data-stu-id="9671d-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9671d-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="9671d-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="9671d-105">¿Qué ha ocurrido?</span><span class="sxs-lookup"><span data-stu-id="9671d-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="9671d-106">Requerimiento de autenticación para obtener acceso a los controladores</span><span class="sxs-lookup"><span data-stu-id="9671d-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="9671d-107">Todos los controladores de su proyecto cuentan ahora con el atributo **Authorize** .</span><span class="sxs-lookup"><span data-stu-id="9671d-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="9671d-108">Este atributo requiere que el usuario se autentique antes de tener acceso a las API definidas por estos controladores.</span><span class="sxs-lookup"><span data-stu-id="9671d-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="9671d-109">Para permitir el acceso anónimo al controlador, quite este atributo del controlador.</span><span class="sxs-lookup"><span data-stu-id="9671d-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="9671d-110">Si desea establecer los permisos a un nivel más detallado, aplique el atributo a cada método que requiere autorización en vez de aplicarlo a la clase del controlador.</span><span class="sxs-lookup"><span data-stu-id="9671d-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9671d-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9671d-111">Next steps</span></span>
[<span data-ttu-id="9671d-112">Más información acerca de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9671d-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

