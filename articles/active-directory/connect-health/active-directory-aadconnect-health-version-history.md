---
title: aaaAzure AD conectarse el historial de versiones de mantenimiento
description: Este documento describe las versiones de Hola para Azure AD Connect Health y lo que se ha incluido en dichas versiones.
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: a583263e412f5da9af75947f3431de2494042388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-version-release-history"></a>Azure AD Connect Health: historial de versiones
equipo de Hello Azure Active Directory actualiza regularmente Azure AD Connect Health con nuevas características y funcionalidades. Este artículo enumeran las versiones de Hola y características que se han liberado.

## <a name="october-2016"></a>Octubre de 2016
**Actualización del agente:**

* Agente de Azure AD Connect Health para AD FS \(versión 2.6.408.0\)
  1. Mejoras en la detección de direcciones IP de cliente en las solicitudes de autenticación
  2. Correcciones de errores relacionados con tooAlerts
* Agente de Azure AD Connect Health para AD DS (versión 2.6.408.0)
  1. Correcciones de errores relacionados con tooAlerts.
* Agente de Azure AD Connect Health para sincronización (versión 2.6.353.0), publicado con Azure AD Connect versión 1.1.281.0
  1. Proporcionar datos de hello necesario para hello informes de errores de sincronización
  2. Correcciones de errores relacionados con tooAlerts

**Nuevas características de la versión preliminar:**

* Informes de errores de sincronización de Azure AD Connect

**Nuevas características:**

* Azure AD Connect Health para AD FS - campo de dirección IP está disponible en informes de hello sobre top 50 usuarios con nombre de usuario/contraseña incorrecta.

## <a name="july-2016"></a>Julio de 2016
**Nuevas características de la versión preliminar:**

* [Azure AD Connect Health para AD DS](active-directory-aadconnect-health-adds.md).

## <a name="january-2016"></a>Enero de 2016
**Actualización del agente:**

* Agente de Azure AD Connect Health para AD FS (versión 2.6.91.1512)

**Nuevas características:**

* [Herramienta de conexión de prueba para agentes de Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a>Noviembre de 2015
**Nuevas características:**

* Soporte para el [control de acceso basado en rol](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)

**Nuevas características de la versión preliminar:**

* [Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md)

**Problemas corregidos:**

* Correcciones de errores detectados durante los registros del agente.

## <a name="september-2015"></a>Septiembre de 2015
**Nuevas características:**

* Informe de contraseña de nombre de usuario incorrecto para AD FS
* Compatibilidad con tooconfigure sin autenticar HTTP Proxy
* Agente de tooconfigure de soporte técnico en Server core
* TooAlerts mejoras de AD FS
* Mejoras en el agente de Azure AD Connect Health para AD FS en la conectividad y carga de datos.

**Problemas corregidos:**

* Correcciones de errores en el uso de tipos de errores de AD FS.

## <a name="june-2015"></a>Junio de 2015
**Versión inicial de Azure AD Connect Health para AD FS y el proxy de AD FS.**

**Nuevas características:**

* Alertas de supervisión de AD FS y servidores proxy de AD FS con notificaciones de correo electrónico.
* Topología de tooAD FS de un acceso sencillo y patrones en los contadores de rendimiento de AD FS.
* Tendencia de las solicitudes correctas de token en servidores de AD FS agrupados por aplicaciones, métodos de autenticación, ubicación de la red de solicitud, etc.
* Tendencias en las solicitudes con error en los servidores de AD FS agrupados por aplicaciones, tipos de error, etc.
* Implementación más sencilla del agente mediante credenciales de administrador global de Azure AD.  

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre [supervisar los servicios de infraestructura y la sincronización de identidad local en la nube de hello](active-directory-aadconnect-health.md).

