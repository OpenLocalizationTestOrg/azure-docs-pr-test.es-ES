---
title: "Azure AD Connect: selección del tipo de instalación | Microsoft Docs"
description: "Este tema le guía a través de la instalación de hello tooselect escriba toouse para Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Seleccione qué toouse del tipo de instalación de Azure AD Connect
Azure AD Connect tiene dos tipos de instalación para la nueva instalación: rápida y personalizada. Este tema le ayudará a toodecide qué opción toouse durante la instalación.

## <a name="express"></a>Express
Express es la opción más común de Hola y se utiliza al 90% de todas las instalaciones nuevas. Fue diseñado tooprovide una configuración que le sirva para escenarios de clientes más comunes de Hola.

Se da por supuesto que:

- Tiene un único bosque de Active Directory local.
- Tener una cuenta de administrador de empresa que puede usar para la instalación de Hola.
- Tiene menos de 100 000 objetos en Active Directory local.

Obtendrá:

- [Sincronización de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) desde local tooAzure AD para inicio de sesión único.
- Una configuración que sincroniza a los [usuarios, grupos, contactos y equipos de Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).
- Sincronización de todos los objetos válidos en todos los dominios y todas las unidades organizativas.
- [La actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) está habilitado toomake Asegúrese de que siempre utilice Hola última versión disponible.

Opciones en las que puede continuar utilizando la instalación rápida:

- Si no desea toosynchronize todas las unidades organizativas, puede usar Express y en la última página de hello, anule la selección de **iniciar el proceso de sincronización de Hola...** *. A continuación, vuelva a ejecutar el Asistente para la instalación de Hola y cambie las unidades organizativas de hello en [opciones de configuración](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) y habilitar la sincronización programada.
- Desea tooenable una de las características de hello en Azure AD Premium, como la escritura diferida de contraseñas. En primer lugar, vaya a través de la instalación inicial de tooget express Hola completada. A continuación, vuelva a ejecutar el Asistente para la instalación de Hola y cambiar hello [opciones de configuración](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Personalizado
ruta de acceso personalizada Hello permite muchas más opciones que la versión express. Se debe usar en todos los casos donde la configuración de hello descrito en la sección anterior para express no es representativo de su organización.

Se debe utilizar si:

- No tiene cuenta de administrador de empresa de tooan de acceso en Active Directory.
- Tiene más de un bosque o piensa toosynchronize más de un bosque en hello futuras.
- Tiene dominios en el bosque no es accesible desde el servidor de Connect de Hola.
- Planear la federación toouse o la autenticación de paso a través para el inicio de sesión de usuario.
- Tiene más de 100.000 objetos y necesita toouse una versión completa de SQL Server.
- Planee toouse basado en el grupo filtrado y no solo dominio o filtrado basado en la unidad organizativa.

## <a name="upgrade-from-dirsync"></a>Actualización desde DirSync
Si actualmente utilizas DirSync, a continuación, siga los pasos de hello en [actualizar desde DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade la configuración existente. Hay dos opciones de actualización distintas:

- Conectar tooinstall de actualización en contexto en hello mismo servidor.
- Paralelo implementación tooinstall Connect en un nuevo servidor mientras servidor de sincronización de directorios existente de hello es sigue funcionando.

## <a name="upgrade-from-azure-ad-sync"></a>Actualización desde Sincronización de Azure AD
Si actualmente utilizas Azure AD Sync, puede seguir hello [mismos pasos](active-directory-aadconnect-upgrade-previous-version.md) como al actualizar desde una versión tooa de conectar más reciente. Hay dos opciones de actualización distintas:

- Conectar tooinstall de actualización en contexto en hello mismo servidor.
- Migración swing tooinstall Connect en un servidor nuevo al servidor de sincronización de Azure AD existente hello es sigue funcionando.

## <a name="migrate-from-fim2010-or-mim2016"></a>Migración desde FIM2010 o MIM2016
Si actualmente utilizas Forefront Identity Manager 2010 o Microsoft Identity Manager 2016 con hello conector de Azure AD, la única opción es una migración. Siga los pasos de hello descritos en [swing migración](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). En los pasos de hello, reemplace cualquier mención de Azure AD Sync con FIM2010/MIM2016.

## <a name="next-steps"></a>Pasos siguientes
Dependiendo de la opción de Hola que ha seleccionado toouse, utilice Hola tabla de contenido toohello izquierdo toofind el artículo con hello pasos detallados.
