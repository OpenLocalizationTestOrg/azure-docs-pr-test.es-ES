---
title: "Problema al crear una aplicación de proxy de aplicación | Microsoft Docs"
description: "Cómo solucionar los problemas que surgen al crear aplicaciones de proxy de aplicación en el portal de administración de Azure AD"
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
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="be9b2-103">Problema al crear una aplicación de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="be9b2-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="be9b2-104">A continuación, se muestran algunos de los problemas habituales a los que se enfrentan los usuarios cuando crean una aplicación de proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="be9b2-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="be9b2-105">Documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="be9b2-105">Recommended documents</span></span> 

<span data-ttu-id="be9b2-106">Para más información sobre la creación de una aplicación de proxy de aplicación mediante el portal de administración, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="be9b2-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="be9b2-107">Si está siguiendo los pasos de ese documento y obtiene un error al crear la aplicación, consulte los detalles del error para obtener información y sugerencias para corregir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="be9b2-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="be9b2-108">La mayoría de los mensajes de error incluyen una sugerencia de corrección.</span><span class="sxs-lookup"><span data-stu-id="be9b2-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="be9b2-109">Aspectos específicos que comprobar</span><span class="sxs-lookup"><span data-stu-id="be9b2-109">Specific things to check</span></span>

<span data-ttu-id="be9b2-110">Para evitar errores habituales, compruebe que:</span><span class="sxs-lookup"><span data-stu-id="be9b2-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="be9b2-111">Sea un administrador con permiso para crear una aplicación de proxy de aplicación;</span><span class="sxs-lookup"><span data-stu-id="be9b2-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="be9b2-112">La dirección URL interna sea única;</span><span class="sxs-lookup"><span data-stu-id="be9b2-112">The internal URL is unique</span></span>

-   <span data-ttu-id="be9b2-113">La dirección URL externa sea única;</span><span class="sxs-lookup"><span data-stu-id="be9b2-113">The external URL is unique</span></span>

-   <span data-ttu-id="be9b2-114">Las direcciones URL empiecen por http o https y terminen en "/";</span><span class="sxs-lookup"><span data-stu-id="be9b2-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="be9b2-115">La dirección URL debe ser un nombre de dominio y no una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="be9b2-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="be9b2-116">El mensaje de error debería aparecer en la esquina superior derecha cuando cree la aplicación.</span><span class="sxs-lookup"><span data-stu-id="be9b2-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="be9b2-117">También puede seleccionar el icono de notificación para ver los mensajes de error.</span><span class="sxs-lookup"><span data-stu-id="be9b2-117">You can also select the notification icon to see the error messages.</span></span>

   ![Mensaje de notificación](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="be9b2-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be9b2-119">Next steps</span></span>
[<span data-ttu-id="be9b2-120">Habilitación del proxy de aplicación en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="be9b2-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
