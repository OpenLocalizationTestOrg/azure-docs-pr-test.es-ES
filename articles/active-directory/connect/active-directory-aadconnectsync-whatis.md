---
title: "Sincronización de Azure AD Connect: descripción y personalización de la sincronización | Microsoft Docs"
description: "Explica cómo funciona la sincronización de Azure AD Connect y cómo toocustomize."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Sincronización de Azure AD Connect: comprender y personalizar la sincronización
Servicios de sincronización de Active Directory Connect de Azure de Hello (Azure AD Connect sync) es un componente principal de Azure AD Connect. Se encarga de todas las operaciones de Hola que son datos de identidad relacionados toosynchronize entre el entorno local y Azure AD. Azure AD Connect sync es sucesor de Hola de sincronización de directorios, sincronización de Azure AD y Forefront Identity Manager con hello configurado el conector de Active Directory de Azure.

Este tema es hello particular para **sincronización de Azure AD Connect** (también denominada **motor de sincronización**) y listas de vínculos tooall otro tooit relacionados de temas. Para vínculos tooAzure AD Connect, consulte [integrar las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

servicio de sincronización de Hello consta de dos componentes, Hola local **sincronización de Azure AD Connect** hello y componente lado del servicio en Azure AD llama **servicio de sincronización de Azure AD Connect**. servicio de Hello es común para la sincronización de directorios, sincronización de Azure AD y Azure AD Connect.

## <a name="azure-ad-connect-sync-topics"></a>Temas de sincronización de Azure AD Connect
| Tema. | ¿Qué incluye y cuándo tooread |
| --- | --- |
| **Fundamentos de la sincronización de Azure AD Connect** | |
| [Descripción de la arquitectura de Hola](active-directory-aadconnectsync-understanding-architecture.md) |Para aquellos que son el nuevo motor de sincronización de toohello y desea toolearn sobre arquitectura de Hola y los términos de hello usa. |
| [Conceptos técnicos](active-directory-aadconnectsync-technical-concepts.md) |Una versión abreviada de tema de la arquitectura de Hola y brevemente explica Hola términos que se usan. |
| [Topologías de Azure AD Connect](active-directory-aadconnect-topologies.md) |Describe Hola diferentes escenarios y topologías Hola sincronización motor admite. |
| **Configuración personalizada** | |
| [Ejecución Hola instalación del Asistente para nuevo](active-directory-aadconnectsync-installation-wizard.md) |Explica las opciones tiene disponibles cuando vuelva a ejecutar Asistente de instalación de hello Azure AD Connect. |
| [Conocimiento del aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |Describe el modelo de configuración de hello denominado aprovisionamiento declarativo. |
| [Explicación de las expresiones declarativas de aprovisionamiento](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |Describe la sintaxis de hello para el lenguaje de expresiones de hello empleado en el aprovisionamiento declarativo. |
| [Configuración predeterminada de Hola de descripción](active-directory-aadconnectsync-understanding-default-configuration.md) |Describe las reglas de out-of-box de Hola y configuración predeterminada de Hola. También se describe cómo funcionan conjuntamente las reglas de Hola para hello escenarios de out-of-box toowork. |
| [Descripción de usuarios y contactos](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Continúa en el tema anterior de Hola y se describe cómo configuración Hola para usuarios y contactos funciona juntos, en particular en un entorno de varios bosques. |
| [¿Cómo toomake un toohello de cambio de configuración predeterminados](active-directory-aadconnectsync-change-the-configuration.md) |Le guiará por el flujo de toomake un tooattribute de cambio de configuración comunes. |
| [Procedimientos recomendados para cambiar la configuración predeterminada de Hola](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Limitaciones de compatibilidad y para realizar la configuración de out-of-box toohello de cambios. |
| [Configuración del filtrado](active-directory-aadconnectsync-configure-filtering.md) |Describe las distintas opciones de Hola para cómo toolimit que los objetos que sincroniza tooAzure AD y paso a paso cómo tooconfigure estas opciones. |
| **Características y escenarios** | |
| [Evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |Describe hello *evitar eliminaciones accidentales* característica y cómo tooconfigure lo. |
| [Scheduler](active-directory-aadconnectsync-feature-scheduler.md) |Describe al programador integrado de hello, que está importando, la sincronización y exportar datos. |
| [Implementación de la sincronización de contraseñas](active-directory-aadconnectsync-implement-password-synchronization.md) |Describe cómo funciona la sincronización de contraseña, cómo tooimplement y cómo toooperate y solucionar problemas. |
| [Escritura diferida de dispositivos](active-directory-aadconnect-feature-device-writeback.md) |Describe cómo funciona la reescritura de dispositivos en Azure AD Connect. |
| [Extensiones de directorio](active-directory-aadconnectsync-feature-directory-extensions.md) |Describe cómo tooextend Hola esquema de Azure AD con sus propios atributos personalizados. |
| **Servicio de sincronización** | |
| [Características del servicio de sincronización de Azure AD Connect](active-directory-aadconnectsyncservice-features.md) |Describe el lado del servicio de sincronización de Hola y cómo toochange sincronizar los ajustes de Azure AD. |
| [Resistencia de atributos duplicados](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Describe cómo tooenable y usar **userPrincipalName** y **proxyAddresses** resistencia de los valores de atributo duplicado. |
| **Operaciones e interfaz de usuario** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |Describe Hola UI Synchronization Service Manager, incluidos los [Operations](active-directory-aadconnectsync-service-manager-ui-operations.md), [conectores](active-directory-aadconnectsync-service-manager-ui-connectors.md), [Diseñador de metaverso](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), y [debúsquedademetaverso](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) pestañas. |
| [Tareas y consideraciones operativas](active-directory-aadconnectsync-operations.md) |Describe las preocupaciones operativas, como la recuperación ante desastres. |
| **Procedimiento para:** | |
| [Restablecimiento de cuentas de hello Azure AD](active-directory-aadconnectsync-howto-azureadaccount.md) |Cómo las credenciales de hello tooreset de cuenta de servicio de hello utilizan tooconnect de Azure AD Connect sync tooAzure AD. |
| **Más información y referencias** | |
| [Puertos](active-directory-aadconnect-ports.md) |Listas de qué puertos necesitan tooopen entre el motor de sincronización de Hola y sus directorios locales y Azure AD. |
| [Atributos sincronizados tooAzure Active Directory](active-directory-aadconnectsync-attributes-synchronized.md) |Enumera todos los atributos que se sincronizan entre los AD locales y Azure AD. |
| [Referencia de funciones](active-directory-aadconnectsync-functions-reference.md) |Enumera todas las funciones disponibles en el aprovisionamiento declarativo. |

## <a name="additional-resources"></a>Recursos adicionales
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)

