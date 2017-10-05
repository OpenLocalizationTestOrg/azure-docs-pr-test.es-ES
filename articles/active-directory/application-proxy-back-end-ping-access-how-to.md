---
title: "Configuración de una aplicación de proxy de aplicación para usar PingAccess | Microsoft Docs"
description: "Aprenda a usar PingAccess para extender las ventajas del proxy de aplicación a aplicaciones que usen la autenticación basada en el encabezado"
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
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="38f13-103">Configuración de una aplicación de proxy de aplicación para usar PingAccess</span><span class="sxs-lookup"><span data-stu-id="38f13-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="38f13-104">Nuestra colaboración con PingAccess ahora nos permite extender las ventajas del proxy de aplicación a aquellas aplicaciones que usen la autenticación basada en el encabezado.</span><span class="sxs-lookup"><span data-stu-id="38f13-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="38f13-105">Si las aplicaciones no utilizan encabezados, consulte nuestra [documentación sobre el inicio de sesión único](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) para ver detalles sobre otras opciones.</span><span class="sxs-lookup"><span data-stu-id="38f13-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="38f13-106">Introducción a los pasos y documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="38f13-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="38f13-107">Para configurar una aplicación con PingAccess, hay cuatro pasos:</span><span class="sxs-lookup"><span data-stu-id="38f13-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="38f13-108">Configurar los conectores del proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="38f13-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="38f13-109">Crear una aplicación de proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="38f13-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="38f13-110">Descargar y configurar PingAccess</span><span class="sxs-lookup"><span data-stu-id="38f13-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="38f13-111">Configurar aplicaciones en PingAccess</span><span class="sxs-lookup"><span data-stu-id="38f13-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="38f13-112">Para ver información detallada sobre cada uno de estos pasos, consulte nuestra [documentación sobre el inicio de sesión único con encabezados](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="38f13-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
