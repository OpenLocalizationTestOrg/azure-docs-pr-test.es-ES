---
title: "aaaUsage escenarios y consideraciones de implementación de Azure AD Join | Documentos de Microsoft"
description: "Se explica cómo los administradores pueden configurar Azure AD Join para sus usuarios finales (empleados, estudiantes, otros usuarios). También se tratan las diferentes situaciones del mundo real hello para el uso de Azure AD Join."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Escenarios de uso y consideraciones de implementación de Azure AD Join
## <a name="usage-scenarios-for-azure-ad-join"></a>Escenarios de uso de Azure AD Join
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Escenario 1: Empresas en gran medida en la nube de Hola
Azure unión de Active Directory (Azure AD Join) puede obtener beneficios si actualmente operar y administrar identidades para su negocio en la nube de Hola o que se van a mover en la nube toohello pronto. Puede usar una cuenta que ha creado en Azure AD toosign en tooWindows 10. A través de [Hola primero ejecute el proceso de configuración rápida (FRX)](active-directory-azureadjoin-user-frx.md), o mediante la combinación de Azure AD desde [menú de configuración de hello](active-directory-azureadjoin-user-upgrade.md), los usuarios pueden unir su tooAzure máquinas AD.  Los usuarios también pueden disfrutar de inicio de sesión único (SSO) acceso demasiado recursos de la nube como Office 365, en sus exploradores o aplicaciones de Office.

### <a name="scenario-2-educational-institutions"></a>Escenario 2: Instituciones educativas
Las instituciones educativas normalmente tienen dos tipos de usuarios: profesores y estudiantes. Los miembros de profesores se consideran a miembros a largo plazo de organización de Hola. Es conveniente crear cuentas locales para ellos. Pero los estudiantes que son miembros de shorter-term de organización de Hola y se pueden administrar sus cuentas de Azure AD. Esto significa que se puede insertar escala directorio toohello en la nube en lugar de ser almacenada localmente. También significa que los alumnos se pueda toosign en tooWindows con sus cuentas de Azure AD y obtener acceso tooOffice 365 recursos en aplicaciones de Office.

### <a name="scenario-3-retail-businesses"></a>Escenario 3: Los negocios minoristas
El sector minorista tiene trabajadores de temporada y empleados a largo plazo. Lo habitual es crear cuentas locales y utilizar equipos unidos a dominio para los empleados a jornada completa cuyos contratos tienen una larga duración. Pero los trabajadores de la temporada son shorter-term miembros de la organización de hello, y es deseable toomanage sus cuentas en licencias de usuario se pueden mover más fácilmente alrededor. Al crear sus cuentas de usuario en la nube de hello con licencias de Office 365, estos usuarios aprovechen las ventajas de hello del inicio de sesión tooWindows y las aplicaciones de Office con una cuenta de Azure AD, mientras se mantiene más flexibilidad con sus licencias después de que atraviesan.

### <a name="scenario-4-additional-scenarios"></a>Escenario 4: Otros escenarios
Junto con los beneficios de Hola que se indicó anteriormente, las ventajas de tener los usuarios unir su tooAzure dispositivos AD debido a una experiencia simplificada de unión, la administración de dispositivos eficaz, inscripción en la administración automática de dispositivos móviles y tooAzure de inicio de sesión único AD y recursos locales.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Consideraciones de implementación de Azure AD Join
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>Habilitar la toojoin a los usuarios un dispositivo propiedad de la empresa directamente tooAzure AD
Las empresas pueden proporcionar las organizaciones y compañías de toopartner de cuentas solo en la nube. Estos asociados pueden acceder así fácilmente a aplicaciones y recursos de la empresa mediante el inicio de sesión único. Este escenario es toousers aplicables que tienen acceso a recursos principalmente en la nube de hello, como Office 365 o SaaS aplicaciones que se basan en Azure AD para la autenticación.

### <a name="prerequisites"></a>Requisitos previos
**Nivel de empresa de hello (Administrador)**

* Suscripción de Azure con Azure Active Directory  

**En el nivel de usuario de Hola**

* Windows 10 (ediciones Professional y Enterprise)

### <a name="administrator-tasks"></a>Tareas de administrador
* [Configuración del registro de dispositivos](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Tareas de usuario
* [Configuración de un nuevo dispositivo de Windows 10 con Azure AD durante la instalación](active-directory-azureadjoin-user-frx.md)
* [Configurar un dispositivo Windows 10 con Azure AD desde el menú de configuración de Hola](active-directory-azureadjoin-user-upgrade.md)
* [Unirse a una organización de tooyour de dispositivo de Windows 10 personal](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>Habilitación de BYOD en su organización para Windows 10
Puede configurar su toouse a los usuarios y los empleados de sus aplicaciones de empresa de tooaccess de dispositivos (BYOD) de Windows y recursos de personal. Los usuarios pueden agregar sus cuentas (profesional o educativa) tooa personal Windows dispositivo tooaccess recursos de Azure AD de forma segura y ser conforme.

### <a name="prerequisites"></a>Requisitos previos
**Nivel de empresa de hello (Administrador)**

* Suscripción de Azure AD

**En el nivel de usuario de Hola**

* Windows 10 (ediciones Professional y Enterprise)

### <a name="administrator-tasks"></a>Tareas de administrador
* [Configuración del registro de dispositivos](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Tareas de usuario
* [Unirse a una organización de tooyour de dispositivo de Windows 10 personal](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>Información adicional
* [Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Autenticación de identidades sin contraseñas a través de Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)

