---
title: "crear una aplicación de Proxy de aplicación de aaaProblem | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot problemas de creación de aplicaciones de Proxy de aplicación de portal de administración de AD de Azure de Hola"
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
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="c4118-103">Problema al crear una aplicación de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="c4118-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="c4118-104">A continuación son algunos de los problemas comunes de Hola se enfrentan los usuarios cuando se crea una nueva aplicación de proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4118-104">Below are some of hello common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="c4118-105">Documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="c4118-105">Recommended documents</span></span> 

<span data-ttu-id="c4118-106">toolearn más acerca de cómo crear una aplicación de Proxy de aplicación a través de hello Portal de administración, consulte [publicar aplicaciones mediante el Proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="c4118-106">toolearn more about creating an Application Proxy application through hello Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="c4118-107">Si está siguiendo los pasos de hello en ese documento y obtiene un error al crear la aplicación hello, vea los detalles del error Hola para obtener información y sugerencias sobre cómo toofix Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="c4118-107">If you are following hello steps in that document and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="c4118-108">La mayoría de los mensajes de error incluyen una sugerencia de corrección.</span><span class="sxs-lookup"><span data-stu-id="c4118-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-toocheck"></a><span data-ttu-id="c4118-109">Toocheck acciones específicas</span><span class="sxs-lookup"><span data-stu-id="c4118-109">Specific things toocheck</span></span>

<span data-ttu-id="c4118-110">tooavoid los errores comunes, compruebe que:</span><span class="sxs-lookup"><span data-stu-id="c4118-110">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="c4118-111">Es un administrador con permiso toocreate una aplicación de Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="c4118-111">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="c4118-112">dirección URL interna de Hello es único</span><span class="sxs-lookup"><span data-stu-id="c4118-112">hello internal URL is unique</span></span>

-   <span data-ttu-id="c4118-113">dirección URL externa de Hello es única</span><span class="sxs-lookup"><span data-stu-id="c4118-113">hello external URL is unique</span></span>

-   <span data-ttu-id="c4118-114">Hola direcciones URL de inicio con http o https y terminar con un "/"</span><span class="sxs-lookup"><span data-stu-id="c4118-114">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="c4118-115">dirección URL de Hello debe ser un nombre de dominio y no una dirección IP</span><span class="sxs-lookup"><span data-stu-id="c4118-115">hello URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="c4118-116">mensaje de error de Hello debe aparecer en la esquina superior derecha de hello cuando se crea la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c4118-116">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="c4118-117">También puede seleccionar los mensajes de error de hello notificación icono toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="c4118-117">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Mensaje de notificación](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="c4118-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4118-119">Next steps</span></span>
[<span data-ttu-id="c4118-120">Habilita el Proxy de aplicación en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c4118-120">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
