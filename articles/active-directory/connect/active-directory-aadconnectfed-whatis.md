---
title: "aaaAzure AD Connect y federación | Documentos de Microsoft"
description: "Esta página es la ubicación central de Hola para toda la documentación relacionada con las operaciones de AD FS que usan Azure AD Connect."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect y la federación
Connect de Azure Active Directory (Azure AD) le permite configurar la federación con Servicios de federación de Active Directory (AD FS) locales y Azure AD. Con inicio de sesión de federación, puede habilitar usuarios toosign en tooAzure basados en AD con sus contraseñas locales--y servicios, mientras que en la red corporativa de hello, sin tener tooenter sus contraseñas de nuevo. Con la opción de federación de hello con AD FS, puede implementar una nueva instalación de AD FS o puede especificar una instalación existente en una granja de servidores de Windows Server 2012 R2.

Este tema es hello doméstica para obtener información relacionada con la federación funcionalidades de Azure AD Connect. Enumera vínculos tooall temas relacionados. Para vínculos tooAzure AD Connect, consulte [integrar las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect: temas de federación
| Tema. | ¿Qué incluye y cuándo tooread, |
|:--- |:--- |
| **Opciones para el inicio de sesión de los usuarios en Azure AD Connect** | |
| [Descripción de las opciones de inicio de sesión de los usuarios](active-directory-aadconnect-user-signin.md) |Obtenga información sobre las distintas opciones de inicio de sesión de usuario y cómo afectan a la experiencia del usuario Hola de inicio de sesión Azure. |
| **Instalación de AD FS mediante Azure AD Connect** | |
| [Requisitos previos](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Consulte los requisitos previos de Hola para una correcta instalación de AD FS a través de Azure AD Connect. |
| [Configuración de una granja de servidores de AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Instale una nueva granja de servidores de AD FS mediante Azure AD Connect. |
| [Federación con Azure AD mediante un identificador de inicio de sesión alternativo](active-directory-aadconnect-federation-management.md#alternateid) | Configuración de la federación con un identificador de inicio de sesión alternativo  |
| **Modificar configuración de hello AD FS** | |
| [Confianza de Hola de reparación](active-directory-aadconnect-federation-management.md#repairthetrust) |Reparación Hola actual confianza entre local de AD FS y Office 365 o SQL Azure. |
| [Adición de un nuevo servidor de AD FS](active-directory-aadconnect-federation-management.md#addadfsserver) |Expansión de la granja de servidores de AD FS con un servidor de AD FS adicional después de la instalación inicial. |
| [Incorporación de un nuevo servidor WAP de AD FS](active-directory-aadconnect-federation-management.md#addwapserver) |Expanda una granja de servidores de AD FS con un servidor proxy de aplicación web (WAP) adicional después de la instalación inicial. |
| [Incorporación de un nuevo dominio federado](active-directory-aadconnect-federation-management.md#addfeddomain) |Agregue otro toobe dominio federado con Azure AD. |
| [Actualiza el certificado SSL de Hola](active-directory-aadconnectfed-ssl-update.md)| Actualiza el certificado SSL de Hola para una granja de servidores de AD FS. |
| **Otros parámetros de configuración de la federación** | |
| [Federación de varias instancias de Azure AD con una instancia única de AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Federación de varias instancias de Azure AD con una granja única de servidores de AD FS| 
| [Incorporación de una ilustración o un logotipo personalizado de la compañía](active-directory-aadconnect-federation-management.md#customlogo) |Modificar la experiencia de inicio de sesión de hello mediante la especificación logotipo personalizado de Hola que se muestra en el inicio de sesión página de hello AD FS. |
| [Adición de la descripción de inicio de sesión](active-directory-aadconnect-federation-management.md#addsignindescription) |Cambiar Hola inicio de sesión descripción en la página de inicio de sesión de hello AD FS. |
| [Modificación de las reglas de notificaciones de AD FS](active-directory-aadconnect-federation-management.md#modclaims) |Modificar o agregar reglas de notificaciones de AD FS que corresponden a configuración de sincronización de tooAzure AD Connect. |


## <a name="additional-resources"></a>Recursos adicionales
* [Federación de dos instancias de Azure AD con una instancia única de AD FS](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Implementación de AD FS en Azure](active-directory-aadconnect-azure-adfs.md)
* [Implementación de AD FS en Azure de alta disponibilidad entre regiones geográficas con Azure Traffic Manager](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
