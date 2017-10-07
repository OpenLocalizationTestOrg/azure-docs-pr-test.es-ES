---
title: "aaaProblem instalar extensión de explorador del panel de acceso de aplicación de hello | Documentos de Microsoft"
description: "¿Cómo toofix comunes errores al instalar la extensión de explorador del panel de acceso de Hola"
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
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Problema al instalar la extensión de explorador del panel de acceso de aplicación de Hola

Hola Panel de acceso es un portal basado en web que permite un usuario que tiene una empresa o centro educativo Administrador de la cuenta en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que hello Azure AD le haya concedido acceso a. Un usuario que tenga las ediciones de Azure AD también puede utilizar grupos de autoservicio y capacidades de administración de aplicaciones a través de hello Panel de acceso. Hola Panel de acceso es independiente de hello portal de Azure y no requiere que los usuarios toohave una suscripción de Azure.

toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola. Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Se cumplen los requisitos de explorador para hello Panel de acceso

Hola Panel de acceso requiere un explorador que admita JavaScript y se han habilitado de CSS. toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola. Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.

Para el SSO basado en contraseña, pueden ser Hola exploradores de los usuarios:

-   Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)

-   Edge en Windows 10 Anniversary Edition o posterior 

-   Chrome (en Windows 7 o posterior y en Mac OS X o posterior)

-   Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>¿Cómo tooinstall Hola extensión de explorador del Panel de acceso

Hola tooinstall extensión de explorador del Panel de acceso, siga Hola pasos:

1.  Abra hello [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores compatibles de Hola y de inicio de sesión como un **usuario** en Azure AD.

2.  Haga clic en un **aplicación SSO de contraseña** Hola Panel de acceso.

3.  En hello símbolo del sistema que se pregunta tooinstall Hola software, seleccione **instalar ahora**.

4.  Basado en el explorador es que el vínculo de descarga de toohello dirigida. **Agregar** tooyour Explorador de hello extensión.

5.  Si el explorador solicita, seleccione tooeither **habilitar** o **permitir** Hola extensión.

6.  Una vez instalada, **reinicie** la sesión del explorador.

7.  Inicie sesión en el Panel de acceso de Hola y vea si puede **iniciar** las aplicaciones de SSO de contraseña

También puede descargar extensión Hola para Chrome y borde de vínculos directos de Hola a continuación:

-   [Extensión del Panel de acceso para Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensión del Panel de acceso para Edge](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Configuración de una directiva de grupo para Internet Explorer

Puede configurar una directiva de grupo que le permiten tooremotely instalar extensión de Panel de acceso de Hola para Internet Explorer en equipos de los usuarios.

requisitos previos de Hello incluyen:

-   Ha configurado [los servicios de dominio de Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), y se han unido a dominio de tooyour de máquinas de los usuarios.

-   Debe tener Hola "Editar configuración de" permiso tooedit Hola objeto de directiva de grupo (GPO). De forma predeterminada, los miembros del programa Hola a los grupos de seguridad siguientes tienen este permiso: los administradores de dominio, los administradores de organización y propietarios del creador de directivas de grupo. [Más información](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Siga el tutorial de hello [cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo](active-directory-saas-ie-group-policy.md) para obtener instrucciones paso a paso acerca de cómo tooconfigure Hola de directiva de grupo e implementarla toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Solucionar problemas de hello Panel de acceso en Internet Explorer

Siga hello [solucionar Hola extensión del Panel de acceso de Internet Explorer](active-directory-saas-ie-troubleshooting.md) guía para el acceso a una herramienta de diagnóstico y obtener instrucciones paso a paso acerca de cómo configurar la extensión de Hola para Internet Explorer.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Si estos pasos no resuelven el problema de Hola

Abra una incidencia de soporte técnico con hello siguiente información si está disponible:

-   Id. de error de correlación

-   UPN (dirección de correo electrónico del usuario)

-   TenantID

-   Tipo de explorador

-   Zona horaria y hora/período de tiempo durante el que se produce el error

-   Seguimientos de Fiddler

## <a name="next-steps"></a>Pasos siguientes
[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
