---
title: "La página de aplicación no se muestra correctamente para una aplicación de proxy de aplicación | Microsoft Docs"
description: "Instrucciones para cuando la página no se muestre correctamente en una aplicación de proxy de aplicación que se ha integrado con Azure AD"
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
ms.openlocfilehash: cac4c333e59ef9a0f28a2f93a7afee22eeafd54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="10f4c-103">La página de aplicación no se muestra correctamente para una aplicación de proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="10f4c-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="10f4c-104">Este artículo lo ayuda a solucionar problemas con aplicaciones de proxy de aplicación de Azure Active Directory cuando va a la página y hay algo en ella que no parece correcto.</span><span class="sxs-lookup"><span data-stu-id="10f4c-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="10f4c-105">Información general</span><span class="sxs-lookup"><span data-stu-id="10f4c-105">Overview</span></span>
<span data-ttu-id="10f4c-106">Cuando se publica una aplicación de proxy de aplicación, solo son accesibles las páginas en la raíz al acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="10f4c-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="10f4c-107">Si la página no se muestra correctamente, puede que falten algunos recursos de página en la dirección URL interna raíz utilizada para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="10f4c-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="10f4c-108">Para resolverlo, asegúrese de que ha publicado *todos* los recursos de la página como parte de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="10f4c-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="10f4c-109">Para comprobar si este es el problema, abra la herramienta de seguimiento de red (como Fiddler o las herramientas de F12 en Internet Explorer o Edge), cargue la página y busque errores 404.</span><span class="sxs-lookup"><span data-stu-id="10f4c-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="10f4c-110">Eso indica las páginas que actualmente no se encuentran y que es posible que todavía tengan que publicarse.</span><span class="sxs-lookup"><span data-stu-id="10f4c-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="10f4c-111">Como ejemplo de este caso, suponga que ha publicado una aplicación de gastos mediante la dirección URL interna <http://myapps/expenses>, pero la aplicación utiliza la hoja de estilos <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="10f4c-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="10f4c-112">En este caso, la hoja de estilos no está publicada en la aplicación, por lo que, cuando se carga, la aplicación de gastos genera un error 404 al intentar cargar style.css.</span><span class="sxs-lookup"><span data-stu-id="10f4c-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="10f4c-113">En este ejemplo, el problema se podría resolver publicando la aplicación con la dirección URL interna <http://myapp/> en su lugar.</span><span class="sxs-lookup"><span data-stu-id="10f4c-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="10f4c-114">Problemas con la publicación como aplicación</span><span class="sxs-lookup"><span data-stu-id="10f4c-114">Problems with publishing as one application</span></span>

<span data-ttu-id="10f4c-115">Si no es posible publicar todos los recursos en la misma aplicación, debe publicar varias aplicaciones y habilitar vínculos entre ellas.</span><span class="sxs-lookup"><span data-stu-id="10f4c-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="10f4c-116">Para ello, se recomienda utilizar la solución de [dominios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="10f4c-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="10f4c-117">Sin embargo, esta solución requiere que posea el certificado de su dominio y que las aplicaciones usen nombres de dominio completos (FQDN).</span><span class="sxs-lookup"><span data-stu-id="10f4c-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="10f4c-118">Para ver otras opciones, consulte la [documentación sobre la solución de problemas de vínculos rotos](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="10f4c-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10f4c-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10f4c-119">Next steps</span></span>
[<span data-ttu-id="10f4c-120">Publicación de aplicaciones mediante el proxy de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="10f4c-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
