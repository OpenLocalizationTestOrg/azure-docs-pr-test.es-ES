---
title: "información general de la movilidad de estado aaaEnterprise | Documentos de Microsoft"
description: "Proporciona información sobre la configuración de Enterprise State Roaming en dispositivos de Windows. Itinerancia de estado de Enterprise proporciona a los usuarios una experiencia unificada a través de sus dispositivos de Windows y reduce el tiempo de hello necesario para configurar un nuevo dispositivo."
services: active-directory
keywords: "qué es Enterprise State Roaming, sincronización empresarial, nube de windows"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 436076383b70b7cd65a612e3928f62f26ac5fa84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-state-roaming-overview"></a>Información general de Enterprise State Roaming
Con Windows 10, [Azure Active Directory (Azure AD)](active-directory-whatis.md) toosecurely de capacidad de los usuarios ganancia Hola sincronizar su configuración de usuario y la nube de toohello de datos de configuración de aplicación. Itinerancia de estado de Enterprise proporciona a los usuarios una experiencia unificada a través de sus dispositivos de Windows y reduce el tiempo de hello necesario para configurar un nuevo dispositivo. Itinerancia de estado de Enterprise funciona similar estándar toohello [sincronización de configuración de consumidor](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) que se introdujo en Windows 8. Además, Enterprise State Roaming ofrece:

* **Separación de datos del consumidor y de empresa** : las organizaciones controlan sus datos y no hay ninguna combinación de datos corporativos en una cuenta de nube de consumidor o datos de consumidores en una cuenta de nube de la empresa.
* **Seguridad mejorada** : datos se cifran automáticamente antes de salir del dispositivo de Windows 10 del usuario de hello mediante Azure Rights Management (Azure RMS) y datos se mantienen cifrados almacenados en la nube de Hola. Todo el contenido permanece cifrado en reposo en la nube de hello, excepto los espacios de nombres hello, como nombres de configuración y los nombres de aplicación de Windows.  
* **Una mejor administración y supervisión** – proporciona visibilidad y control con respecto a que sincroniza la configuración de su organización y en qué dispositivos mediante la integración de portal de hello Azure AD. 

Enterprise State Roaming está disponible en varias regiones de Azure. Puede encontrar Hola actualizar lista de regiones disponibles en hello [servicios de Azure por las regiones](https://azure.microsoft.com/regions/#services) página en Azure Active Directory.

| Artículo | Description |
| --- | --- |
| [Habilitación de Enterprise State Roaming en Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md) |Itinerancia de estado de empresa es la organización de tooany disponible con una suscripción Premium de Azure Active Directory (Azure AD). Para obtener más información acerca de cómo tooget una suscripción de Azure AD, vea hello [producto de Azure AD](https://azure.microsoft.com/services/active-directory) página. |
| [Preguntas más frecuentes sobre itinerancia de datos y configuración](active-directory-windows-enterprise-state-roaming-faqs.md) |Este tema responde a algunas preguntas que los administradores de TI podrían tener sobre la sincronización de datos de aplicación y la configuración. |
| [Configuración de MDM y directivas de grupo](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |Windows 10 le proporciona la directiva de grupo y sincronización de configuración de dispositivos móviles (MDM) de administración directiva configuración toolimit. |
| [Referencia de la configuración de movilidad de Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |Hola aquí te mostramos una lista completa de todas las configuraciones de Hola que se puede movido o copia de seguridad en Windows 10. |
| [Solución de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |En este tema se llevan a cabo algunos pasos básicos de solución de problemas y en él se incluye una lista de problemas conocidos. |

