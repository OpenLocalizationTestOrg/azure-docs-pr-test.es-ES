---
title: "configuración de directiva y MDM aaaGroup | Documentos de Microsoft"
description: "Proporciona información sobre la configuración de directiva de grupo y la administración de dispositivos móviles (MDM) que debe usarse en dispositivos de empresa. Estas directivas son dispositivo completo del usuario toohello aplicada."
services: active-directory
keywords: "¿cuál es la configuración de directiva de grupo y MDM para Enterprise State Roaming, Enterprise State Roaming, nube de windows"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>Configuración de MDM y directivas de grupo
Usar estas directivas de grupo y configuración de dispositivos móviles (MDM) de administración en los dispositivos corporativos como estas directivas son dispositivo completo del usuario toohello aplicada. Aplicar una sincronización de configuración de MDM directiva toodisable para un personal, dispositivo de usuario de la empresa afectará negativamente al uso de Hola de dicho dispositivo. Además, otras cuentas de usuario en el dispositivo de hello también se verá afectadas por la directiva de Hola.

Empresas que quieren toomanage móviles para sus dispositivos personales (no administrados) se puede usar hello Azure tooenable portal o deshabilitar la movilidad, en lugar de mediante la directiva de grupo o MDM.
Hello las tablas siguientes describe la configuración de directiva de hello disponible.

## <a name="mdm-settings"></a>Configuración de MDM
configuración de directivas MDM de Hello aplica tooboth Windows 10 y Windows 10 Mobile.  El soporte para Windows 10 Mobile existe solo para la itinerancia basada en cuentas de Microsoft a través de la cuenta OneDrive del usuario.  Consulte demasiado sección "Dispositivos y los puntos de conexión" para obtener detalles sobre qué dispositivos son compatibles con Azure AD según la sincronización.

| Nombre | Description |
| --- | --- |
| Permitir la conexión con una cuenta de Microsoft |Permite tooauthenticate a los usuarios con una cuenta de Microsoft en el dispositivo de Hola |
| Permitir la sincronización de mi configuración |Permite la configuración de Windows de los usuarios tooroam y datos de la aplicación; Si se deshabilita esta directiva, se deshabilitará sincronización, así como las copias de seguridad en dispositivos móviles |

## <a name="group-policy-settings"></a>Configuración de directiva de grupo
configuración de directiva de grupo de Hello aplica tooWindows 10 dispositivos que están tooan Unidos a un dominio de Active Directory. tabla de Hello también incluye la configuración heredada que aparecería toomanage la configuración de sincronización, pero que no funcionan para Enterprise estado de movilidad de Windows 10, que está anotadas con 'No utilice' en la descripción de Hola.

| Nombre | Description |
| --- | --- |
| Cuentas: bloquear cuentas Microsoft |Esta configuración de directiva impide a los usuarios agregar nuevas cuentas de Microsoft en este equipo. |
| No sincronizar |Impide que la configuración de Windows de los usuarios tooroam y datos de la aplicación |
| No sincronizar personalización |Deshabilita la sincronización del grupo de temas de Hola |
| No sincronizar la configuración del explorador |Deshabilita la sincronización del grupo de Internet Explorer Hola |
| No sincronizar contraseñas |Deshabilita la sincronización del grupo Contraseñas. |
| No sincronizar otra configuración de Windows |Deshabilita la sincronización del grupo Otra configuración de Windows. |
| No sincronizar la personalización del escritorio |No se usa; no tiene efecto. |
| No sincronizar con conexiones de uso medido |Deshabilita la movilidad en conexiones limitadas, como 3G móvil. |
| No sincronizar aplicaciones |No se usa; no tiene efecto. |
| No sincronizar la configuración de aplicaciones |Deshabilita la movilidad de datos de la aplicación. |
| No sincronizar la configuración de inicio |No se usa; no tiene efecto. |

## <a name="related-topics"></a>Temas relacionados
* [Información general de Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Habilitación de Enterprise State Roaming en Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Preguntas más frecuentes sobre itinerancia de datos y configuración](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Referencia de la configuración de movilidad de Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Solución de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

