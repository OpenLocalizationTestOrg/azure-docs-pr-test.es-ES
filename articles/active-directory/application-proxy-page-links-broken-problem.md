---
title: "para una aplicación de Proxy de aplicación no admiten aaaLinks en la página de hello | Documentos de Microsoft"
description: "¿Cómo tootroubleshoot problemas con vínculos rotos en aplicaciones de Proxy de aplicación que se ha integrado con Azure AD"
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
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>Vínculos en la página de hello no funcionan para una aplicación de Proxy de aplicación

Este artículo le ayudará tootroubleshoot ¿por qué no funcionan los vínculos en la aplicación de Proxy de aplicación de Azure Active Directory correctamente.

## <a name="overview"></a>Información general 
Después de publicar una aplicación de Proxy de aplicación, vínculos de hello solamente que el trabajo de forma predeterminada en la aplicación hello son toodestinations vínculos dentro de hello publican dirección URL raíz. Hola vínculos dentro de las aplicaciones de hello no estén utilizando, Hola URL interna para la aplicación hello probablemente no incluye todos los destinos de Hola de vínculos dentro de la aplicación hello.

**¿Por qué ocurre esto?** Al hacer clic en un vínculo en una aplicación, dirección URL de tooresolve Hola intentos de Proxy de aplicación como ya sea una dirección URL interna en Hola misma aplicación, o como una dirección URL disponible externamente. Si tooan dirección URL interna que no está dentro que apunta el vínculo de Hola Hola misma aplicación no pertenecen tooeither de estos depósitos y obtendrá un error no se encuentra.

## <a name="ways-you-can-resolve-broken-links"></a>Maneras de resolver vínculos rotos

Hay tres tooresolve de formas de este problema. Opciones de Hello siguiente son enumerado en complejidad creciente.

1.  Asegúrese de que la URL interna de hello es una carpeta raíz que contiene todos los vínculos relevantes de hello para la aplicación hello. Esto permite que todos los toobe vínculos resuelve según el contenido publica en hello igual aplicación.

    Si cambiar la dirección URL interna de hello pero no desea hello toochange página para que los usuarios de destino, toohello de dirección URL de la página principal de cambio Hola publicados anteriormente URL interna. Puede hacerlo yendo demasiado "Azure Active Directory" -&gt; registros de aplicación -&gt; Seleccionar aplicación hello -&gt; propiedades. En esta pestaña Propiedades, vea Hola campo "URL de página principal", que se puede ajustar toobe Hola deseado página de aterrizaje.

2.  Si las aplicaciones usan nombres de dominio completo (FQDN), use [dominios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish sus aplicaciones. Esta característica permite Hola mismo toobe de dirección URL se usa tanto internamente y externamente.

    Esta opción asegura que los vínculos de hello en la aplicación están accesibles desde el exterior a través de Proxy de aplicación puesto que también se reconocen los vínculos de hello dentro de las direcciones URL de hello aplicación toointernal externamente. Tenga en cuenta que todos los vínculos sigue necesitan toobelong tooa publicó la aplicación. Sin embargo, con este Hola opción vínculos no es necesario toobelong toohello misma aplicación y puede pertenecer toomultiple aplicaciones.

3.  Si ninguna de estas opciones son viable, se une a la vista previa de Hola para una característica nueva que realizan la traducción de dirección URL/reescritura. Con esta opción, interno direcciones URL o vínculos que existen en el cuerpo de hello HTML de las aplicaciones pueden convertir, o "asignan", toohello publicado direcciones URL externas Proxy de aplicación. Esto solo funciona para los vínculos en hello HTML o CSS, y esto no ayudará a si el vínculo se genera a través de JS. 

Como resultado, se recomienda encarecidamente usar hello [dominios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solución si es posible. Si desea vista previa de hello toojoin, enviar por correo electrónico < aadapfeedback@microsoft.com > con applicationId(s) Hola.

## <a name="next-steps"></a>Pasos siguientes
[Trabajo con servidores proxy locales existentes](application-proxy-working-with-proxy-servers.md)

