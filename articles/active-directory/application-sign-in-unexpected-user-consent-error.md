---
title: "error inesperado de aaa al realizar la aplicación de consentimiento tooan | Documentos de Microsoft"
description: "Explica los errores que pueden producirse durante el proceso de Hola de consentimiento tooan aplicación y qué puede hacer con ellos"
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
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>Error inesperado al realizar la aplicación de tooan de consentimiento

En este artículo se describe los errores que pueden producirse durante el proceso de Hola de consentimiento tooan aplicación. Si está solucionando solicitudes de consentimiento inesperadas que no contienen ningún mensaje de error, consulte [Escenarios de autenticación para Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).

Muchas aplicaciones que se integran con Azure Active Directory requieren permisos tooaccess otros recursos en orden toofunction. Cuando estos recursos también están integrados con Azure Active Directory, tooaccess permisos ellos con frecuencia se solicita mediante Hola comunes consentimiento framework. 

Esto produce una solicitud de consentimiento que se muestra, que suele producirse Hola por primera vez que una aplicación se utiliza, pero también puede ocurrir en un uso posterior de la aplicación hello.

Determinadas condiciones deben cumplirse para tooconsent toohello permiso a un usuario requiere una aplicación. Si no se cumplen estas condiciones, pueden producirse varios errores. Entre ellos se incluyen los siguientes:

## <a name="requesting-not-authorized-permissions-error"></a>Error por solicitud de permisos no autorizados
* **AADSTS90093:** &lt;clientAppDisplayName&gt; solicita uno o varios de los permisos que no está autorización toogrant. Póngase en contacto con el administrador puede dar su consentimiento toothis aplicación en su nombre.

Este error se produce cuando un usuario que no sea un administrador de empresa intenta toouse una aplicación que está pidiendo permisos que sólo un administrador puede conceder. Este error se puede resolver por un administrador conceder acceso toohello aplicación en nombre de su organización.

## <a name="policy-prevents-granting-permissions-error"></a>Error porque la directiva impide conceder permisos
* **AADSTS90093:** administradora de &lt;tenantDisplayName&gt; ha establecido una directiva que le impide concederse &lt;nombre de aplicación&gt; Hola permisos está solicitando. Póngase en contacto con un administrador de &lt;tenantDisplayName&gt;, que puede conceder permisos toothis aplicación en su nombre.

Este error se produce cuando un administrador de la compañía desactiva la capacidad de Hola para usuarios tooconsent tooapplications, a continuación, un usuario sin privilegios de administrador intenta toouse una aplicación que requiere el consentimiento. Este error se puede resolver por un administrador conceder acceso toohello aplicación en nombre de su organización.

## <a name="intermittent-problem-error"></a>Error de un problema intermitente
* **AADSTS90090:** parece que hemos detectado un problema intermitente grabación permisos Hola ha intentado demasiado toogrant&lt;clientAppDisplayName&gt;. Inténtelo de nuevo más tarde.

Este error indica que se ha producido un problema de servicio intermitente. Se puede resolver mediante la aplicación de toohello tooconsent nuevo.

## <a name="resource-not-available-error"></a>Error de recurso no disponible
* **AADSTS65005:** aplicación hello &lt;clientAppDisplayName&gt; solicita permisos tooaccess un recurso &lt;resourceAppDisplayName&gt; que no está disponible. 

Póngase en contacto con el desarrollador de la aplicación hello.

##  <a name="resource-not-available-in-tenant-error"></a>Error de recurso no disponible en el inquilino
* **AADSTS65005:** &lt;clientAppDisplayName&gt; solicita acceso a recursos de tooa &lt;resourceAppDisplayName&gt; que no está disponible en su organización &lt; tenantDisplayName&gt;. 

Asegúrese de que este recurso esté disponible o póngase en contacto con un administrador de &lt;tenantDisplayName&gt;.

## <a name="permissions-mismatch-error"></a>Error de coincidencia de permisos
* **AADSTS65005:** aplicación hello solicita consentimiento tooaccess recursos &lt;resourceAppDisplayName&gt;. Error de esta solicitud porque no coincide con la aplicación hello se configuradas previamente durante el registro de aplicación. Póngase en contacto con vendor.* aplicación Hola *

Estos todos los errores se producen cuando la aplicación hello un usuario trate de toois tooconsent solicitar permisos tooaccess una aplicación de recursos que no se encuentra en el directorio de la organización de hello (inquilino). Esto puede ocurrir por varios motivos:

-   Programador de aplicaciones de cliente de Hello ha configurado su aplicación incorrectamente, haciendo que el recurso no válido de toorequest acceso tooan. En este caso, programador de la aplicación hello debe actualizar configuración de Hola de tooresolve de aplicación de cliente de Hola este problema.

-   Una entidad de servicio que representa la aplicación de recurso de destino de hello no existe en la organización de hello, o existía en los último Hola pero se ha quitado. tooresolve este problema, una entidad de servicio para la aplicación de recursos de hello debe haber aprovisionado en organización hello, por lo que la aplicación de cliente de hello puede solicitar permisos tooit. Esto puede ocurrir en un número de formas, según el tipo de saludo de aplicación, que incluye:

    -   Al adquirir una suscripción para la aplicación de recursos de hello (aplicaciones publicadas de Microsoft)

    -   Aplicación de recursos de toohello de consentimiento

    -   Conceder permisos de aplicación Hola a través de hello Portal de Azure

    -   Agregar aplicación hello de hello Galería de aplicaciones de Azure AD

## <a name="next-steps"></a>Pasos siguientes 

[Aplicaciones, permisos y consentimiento en Azure Active Directory (punto de conexión v1)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[Ámbitos, permisos y consentimiento de hello Azure Active Directory (extremo v2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


