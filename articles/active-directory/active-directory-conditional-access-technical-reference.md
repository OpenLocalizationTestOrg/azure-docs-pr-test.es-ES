---
title: "referencia técnica de acceso condicional de Active Directory aaaAzure | Documentos de Microsoft"
description: "Con control de acceso condicional, Azure Active Directory comprueba las condiciones específicas de Hola que elegir al autenticar usuario hello y antes de permitir el acceso toohello aplicación. Una vez que se cumplen estas condiciones, usuario de hello es autenticado y acceso toohello aplicación permitida."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Referencia técnica del acceso condicional de Azure Active Directory

## <a name="services-enabled-with-conditional-access"></a>Servicios habilitados con acceso condicional

Las reglas de acceso condicional se admiten en varios tipos de aplicaciones de Azure AD. Esta lista incluye:


* Aplicaciones registradas con hello Proxy de aplicación de Azure
* Azure RemoteApp
* Aplicaciones desarrolladas de línea de negocio y multiinquilino registradas con Azure AD
* Dynamics CRM
* Aplicaciones federadas de galería de aplicaciones de Azure AD Hola
* Yammer de Microsoft Office 365
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online (incluye OneDrive para la Empresa)
* Microsoft Power BI 
* Aplicaciones de SSO de contraseña desde galería de aplicaciones de hello Azure AD
* Visual Studio Team Services
* Equipos de Microsoft









## <a name="enable-access-rules"></a>Habilitación de reglas de acceso
Cada regla puede habilitarse o deshabilitarse en función de la aplicación. Cuando las reglas son **ON** serán habilitados y se exige para los usuarios que acceden a la aplicación hello. Cuando se encuentran **OFF** no se utilizará y firmará no los usuarios de Hola de impacto en experiencia.

## <a name="applying-rules-toospecific-users"></a>Aplicar a los usuarios de las reglas toospecific
Las reglas pueden ser toospecific aplicado conjuntos de usuarios basados en el grupo de seguridad estableciendo **aplicar a**. **Aplicar a** puede establecerse demasiado**todos los usuarios** o **grupos**. Cuando se establece demasiado**todos los usuarios** aplicarán a las reglas de hello tooany usuario con la aplicación de access toohello. Hola **grupos** opción permite la seguridad específica y toobe de grupos de distribución seleccionado, solo se aplicarán las reglas para estos grupos.

Al implementar una regla, es común toofirst aplica un conjunto limitado de usuarios, que son miembros de un grupo piloto. Una vez que se pueden aplicar reglas de hello completa demasiado**todos los usuarios**. Esto hará que la regla de hello toobe obligatorio para todos los usuarios de la organización de Hola.

Seleccione grupos también pueden excluirse de la directiva mediante hello **excepto** opción. Aunque aparezcan en un grupo incluido, todos los miembros de estos grupos quedarán excluidos.

## <a name="at-work-networks"></a>Redes "en el trabajo"
Las reglas de acceso condicional que usan una red "en el trabajo", que se basan en confianza intervalos de direcciones IP que se han configurado en Azure AD, o el uso de Hola "dentro de la red corporativa" notificaciones de AD FS. Estas reglas incluyen:

* Requerir autenticación multifactor fuera del trabajo
* Bloquear el acceso fuera del trabajo

Opciones para especificar redes "en el trabajo"

1. Configurar intervalos de direcciones IP de confianza en hello [página de configuración de la autenticación multifactor](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Directiva de acceso condicional utilizará intervalos Hola configurado en cada solicitud y el token de emisión tooevaluate las reglas de autenticación. 
2. Configurar el uso de hello dentro de notificación de la red corporativa, esta opción puede utilizarse con directorios federados, mediante AD FS. toolearn más información acerca de hello dentro de notificaciones de la red corporativa, consulte [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Reglas basadas en la confidencialidad de las aplicaciones
Las reglas se configuran por aplicación lo que Hola valiosos servicios toobe protegida sin afectar a los servicios de acceso tooother. Se pueden configurar reglas de acceso condicional en hello **configurar** pestaña de aplicación hello. 

Reglas que se ofrecen actualmente:

* **Requerir autenticación multifactor**
  
  * Todos los usuarios que esta directiva se aplica toowill ser necesario tooauthenticate a través de la autenticación multifactor al menos una vez.
* **Requerir autenticación multifactor fuera del trabajo**
  
  * Si se aplica esta directiva, todos los usuarios será necesario toohave realiza la autenticación multifactor al menos una vez si tienen acceso a servicio de Hola desde una ubicación remota no laborables. Si mueve desde una ubicación de tooremote de trabajo, al obtener acceso a servicios de hello estará tooperform requiere la autenticación multifactor.
* **Bloquear el acceso fuera del trabajo** 
  
  * Cuando el usuario cambia de ubicación remota de tooa de trabajo, se bloqueará si directiva "Bloquear el acceso fuera del trabajo" hello es toothem aplicada.  Se les volverá a permitir el acceso cuando estén en una ubicación de trabajo.

## <a name="related-topics"></a>Temas relacionados
* [Proteger el acceso tooOffice 365 y otras aplicaciones conectadas tooAzure Active Directory](active-directory-conditional-access.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)

