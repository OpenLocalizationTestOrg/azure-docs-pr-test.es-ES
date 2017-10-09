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
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>La página de aplicación no se muestra correctamente para una aplicación de proxy de aplicación

Este artículo le ayudará tootroubleshoot problemas con aplicaciones de Proxy de aplicación de Azure Active Directory cuando navegue toohello página, pero algo en la página de hello no parece correcto.

## <a name="overview"></a>Información general
Cuando se publica una aplicación de Proxy de aplicación, solo las páginas en la raíz son accesibles al obtener acceso a la aplicación hello. Si no mostrar correctamente los página hello, URL interna en la raíz de hello utilizada para aplicación hello puede que falten algunos recursos de la página. tooresolve, asegúrese de que ha publicado *todos los* Hola recursos para la página de hello como parte de la aplicación.

Puede comprobar trata de problema de hello, abra la herramienta de seguimiento de red (como Fiddler o F12 herramientas en Internet Explorer o Edge), carga de página de Hola y busca 404 errores. Que indica las páginas de Hola que actualmente no se puede encontrar y pueden seguir necesitando toobe publicado.

Como ejemplo de este caso, se supone que ha publicado una aplicación de los gastos mediante una dirección URL interna de <http://myapps/expenses>, pero la aplicación hello utiliza hojas de estilo de hello <http://myapps/style.css>. En este caso, hojas de estilo de hello no se publican en la aplicación, por lo que carga la aplicación de los gastos de hello produzca un error al tratar de style.css tooload 404. En este ejemplo, el problema de hello debería resolverse mediante la publicación de la aplicación hello con una dirección URL interna de <http://myapp/> en su lugar.

## <a name="problems-with-publishing-as-one-application"></a>Problemas con la publicación como aplicación

Si no es posible toopublish misma aplicación Hola a todos los recursos en, necesita toopublish varias aplicaciones y habilitar los vínculos entre ellos.

toodo por lo tanto, se recomienda usar hello [dominios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solución. Sin embargo, esta solución requiere que posee el certificado de hello para el dominio y las aplicaciones utilizan nombres de dominio completo (FQDN). Para ver otras opciones, vea hello [solucionar problemas de documentación de vínculos rotos](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Pasos siguientes
[Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](application-proxy-publish-azure-portal.md)
