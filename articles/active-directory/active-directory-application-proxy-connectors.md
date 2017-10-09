---
title: "conectores de Proxy de aplicación de Azure AD portales aaaClassic | Documentos de Microsoft"
description: "Cubre cómo toocreate y administrar grupos de conectores en el Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publicación de aplicaciones en redes independientes y ubicaciones mediante grupos de conectores
> [!div class="op_single_selector"]
> * [Portal de Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [Portal de Azure clásico](active-directory-application-proxy-connectors.md)
>
>

Los grupos de conectores son útiles para diversos escenarios, por ejemplo:

* Sitios con varios centros de datos interconectados. En este caso, desea tookeep como cantidad de tráfico en el centro de datos de hello como sea posible porque los vínculos entre centros de datos son costosos y lentos. Puede implementar los conectores en cada centro de datos tooserve solo hello las aplicaciones que residen en el centro de datos de Hola. Este enfoque minimiza los vínculos entre centros de datos y proporciona una experiencia totalmente transparente tooyour a los usuarios.
* Administrar las aplicaciones instaladas en redes aisladas que no forman parte de la red corporativa principal de Hola. Puede utilizar conectores de tooinstall dedicado de grupos de conector de red de toohello de redes aisladas tooalso aislar las aplicaciones.
* Para las aplicaciones instaladas en IaaS para el acceso a la nube, los grupos de conectores proporcionan una comunes del servicio toosecure Hola acceso tooall Hola de aplicaciones. Grupos de conectores no crear dependencia adicional en la red corporativa o fragmentar la experiencia de aplicación Hola. Los conectores se pueden instalarse en cada centro de datos en la nube y servir solo las aplicaciones que residen en esta red. Puede instalar varios disponibilidad alta tooachieve de conectores.
* Compatibilidad con entornos de varios bosques en la que pueden implementar por bosque conectores específicos y establecer tooserve determinadas aplicaciones.
* Grupos de conectores pueden utilizarse en sitios de recuperación ante desastres tooeither detectar conmutación por error o como copia de seguridad de Hola principal sitio.
* Grupos de conectores también pueden ser utilizado tooserve varias empresas de un solo inquilino.

## <a name="prerequisite-create-your-connectors"></a>Requisito previo: Crear conectores
toogroup sus conectores, [instalar varios conectores](active-directory-application-proxy-enable.md), a continuación, asigne un nombre y agruparlos. Por último tener tooassign les toospecific aplicaciones.

## <a name="step-1-create-connector-groups"></a>Paso 1: Crear grupos de conectores
Puede crear tantos grupos de conectores como desee. Creación de grupos de conector se realiza en hello portal de Azure clásico.

1. Seleccione el directorio y haga clic en **Configurar**.  
    ![Captura de pantalla de la configuración del proxy de la aplicación: clic en administrar grupos de conectores](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. En el Proxy de aplicación, haga clic en **administrar grupos de conectores** y crear un grupo de conectores proporcionando un nombre de grupo de Hola.  
    ![Captura de pantalla de grupos de conectores del proxy de la aplicación: asignar un nombre al grupo nuevo](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>Paso 2: Asignar conectores tooyour grupos
Una vez creados los grupos de conectores de hello, mover grupo adecuado de hello conectores toohello.

1. En **Proxy de la aplicación**, haga clic en **Administrar conectores**.
2. En **grupo**, seleccione grupo de Hola que desee para cada conector. Es posible que tarde conectores Hola seguridad too10 minutos toobecome activas en el nuevo grupo de Hola.  
    ![Captura de pantalla de conectores de proxy de la aplicación: seleccionar un grupo en el menú desplegable](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>Paso 3: Asignar aplicaciones de grupos de conectores de tooyour
último paso de Hello es tooset cada grupo de conectores de toohello de aplicación que atiende.

1. Hola portal de Azure clásico, en el directorio, seleccione Hola desea tooassign toohello grupo y haga clic en la aplicación **configurar**.
2. En **grupo de conectores**, seleccione grupo de Hola que desee Hola toouse de aplicación. Este cambio se aplica inmediatamente.  
    ![Captura de pantalla de grupo de conectores de proxy de la aplicación: seleccionar grupo en el menú desplegable](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Otras referencias
* [Habilitación del proxy de la aplicación](active-directory-application-proxy-enable.md)
* [Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md)
* [Habilitar el acceso condicional](active-directory-application-proxy-conditional-access.md)
* [Solucionar los problemas que tiene con el Proxy de aplicación](active-directory-application-proxy-troubleshoot.md)

Para obtener las actualizaciones y noticias más recientes de hello, visite hello [blog de Proxy de aplicación](http://blogs.technet.com/b/applicationproxyblog/)
