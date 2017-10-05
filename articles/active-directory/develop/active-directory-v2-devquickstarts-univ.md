---
title: "Aplicación universal de Windows de Azure AD v2.0 | Microsoft Docs"
description: "Cómo crear una aplicación universal de Windows con la que los usuarios pueden iniciar sesión utilizando tanto la cuenta personal de Microsoft como sus cuentas profesionales o educativas."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: d2c92b65-3c1d-46d1-81c8-88f32f6b2c4b
ms.service: active-directory
ms.workload: identity
ms.topic: article
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.date: 02/20/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 369802f1a42b8720aa730d5ac7e5576ed20eeddf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-universal-app-using-the-v20-endpoint"></a><span data-ttu-id="ede94-103">Agregar inicio de sesión a una aplicación universal de Windows mediante el punto de conexión de v2.0</span><span class="sxs-lookup"><span data-stu-id="ede94-103">Add sign-in to a Windows Universal app using the v2.0 endpoint</span></span>
  <span data-ttu-id="ede94-104">El tutorial de inicio rápido para aplicaciones universales de Windows aún no está listo... Vuelva pronto y busque actualizaciones de @AzureAD en Twitter.</span><span class="sxs-lookup"><span data-stu-id="ede94-104">The quick-start tutorial for Windows Universal apps isn't quite ready... Check back soon & look for updates from @AzureAD on Twitter.</span></span>

> [!NOTE]
> <span data-ttu-id="ede94-105">No todas las características y escenarios de Azure Active Directory son compatibles con el punto de conexión v2.0.</span><span class="sxs-lookup"><span data-stu-id="ede94-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="ede94-106">Para determinar si debe usar el punto de conexión v2.0, lea acerca de las [limitaciones de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="ede94-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

    ## Get security updates for our products

<span data-ttu-id="ede94-107">Le animamos a que obtenga notificaciones de los incidentes de seguridad que se produzcan; para ello, visite [esta página](https://technet.microsoft.com/security/dd252948) y suscríbase a las alertas de avisos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ede94-107">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

