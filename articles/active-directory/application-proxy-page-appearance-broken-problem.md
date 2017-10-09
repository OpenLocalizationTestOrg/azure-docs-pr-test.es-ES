---
title: "página de aaaApplication no se muestre correctamente para una aplicación de Proxy de aplicación | Documentos de Microsoft"
description: "Cuando la página de hello no muestra correctamente en una aplicación de Proxy de aplicación ha integrado con Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="3c498-103">La página de aplicación no se muestra correctamente para una aplicación de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="3c498-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="3c498-104">Este artículo le ayudará tootroubleshoot problemas con aplicaciones de Proxy de aplicación de Azure Active Directory cuando navegue toohello página, pero algo en la página de hello no parece correcto.</span><span class="sxs-lookup"><span data-stu-id="3c498-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="3c498-105">Información general</span><span class="sxs-lookup"><span data-stu-id="3c498-105">Overview</span></span>
<span data-ttu-id="3c498-106">Cuando se publica una aplicación de Proxy de aplicación, solo las páginas en la raíz son accesibles al obtener acceso a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3c498-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="3c498-107">Si no mostrar correctamente los página hello, URL interna en la raíz de hello utilizada para aplicación hello puede que falten algunos recursos de la página.</span><span class="sxs-lookup"><span data-stu-id="3c498-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="3c498-108">tooresolve, asegúrese de que ha publicado *todos los* Hola recursos para la página de hello como parte de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c498-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="3c498-109">Puede comprobar trata de problema de hello, abra la herramienta de seguimiento de red (como Fiddler o F12 herramientas en Internet Explorer o Edge), carga de página de Hola y busca 404 errores.</span><span class="sxs-lookup"><span data-stu-id="3c498-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="3c498-110">Que indica las páginas de Hola que actualmente no se puede encontrar y pueden seguir necesitando toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="3c498-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="3c498-111">Como ejemplo de este caso, se supone que ha publicado una aplicación de los gastos mediante una dirección URL interna de <http://myapps/expenses>, pero la aplicación hello utiliza hojas de estilo de hello <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="3c498-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="3c498-112">En este caso, hojas de estilo de hello no se publican en la aplicación, por lo que carga la aplicación de los gastos de hello produzca un error al tratar de style.css tooload 404.</span><span class="sxs-lookup"><span data-stu-id="3c498-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="3c498-113">En este ejemplo, el problema de hello debería resolverse mediante la publicación de la aplicación hello con una dirección URL interna de <http://myapp/> en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3c498-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="3c498-114">Problemas con la publicación como aplicación</span><span class="sxs-lookup"><span data-stu-id="3c498-114">Problems with publishing as one application</span></span>

<span data-ttu-id="3c498-115">Si no es posible toopublish misma aplicación Hola a todos los recursos en, necesita toopublish varias aplicaciones y habilitar los vínculos entre ellos.</span><span class="sxs-lookup"><span data-stu-id="3c498-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="3c498-116">toodo por lo tanto, se recomienda usar hello [dominios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solución.</span><span class="sxs-lookup"><span data-stu-id="3c498-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="3c498-117">Sin embargo, esta solución requiere que posee el certificado de hello para el dominio y las aplicaciones utilizan nombres de dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="3c498-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="3c498-118">Para ver otras opciones, vea hello [solucionar problemas de documentación de vínculos rotos](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="3c498-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c498-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c498-119">Next steps</span></span>
[<span data-ttu-id="3c498-120">Publicación de aplicaciones mediante el proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c498-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
