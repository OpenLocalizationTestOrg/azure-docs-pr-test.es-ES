---
title: "Características de Azure Active Directory Domain Services | Microsoft Docs"
description: "Características de Servicios de dominio de Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="features"></a>Características
Hola siguientes características está disponible en dominios de servicios de dominio de Active Directory de Azure administrados.

* **Experiencia de implementación sencilla:** puede habilitar Servicios de dominio de Azure AD para el inquilino de Azure AD mediante unos cuantos clics. Independientemente de si el inquilino de Azure AD es un inquilino en la nube o sincronizado con el directorio local, el dominio administrado se puede aprovisionar rápidamente.
* **Compatibilidad para la unión a dominio:** le resultará muy fácil de equipos de unión a dominio de red virtual de Azure está disponible en el dominio administrado Hola. experiencia de unión a dominio de Hello en el cliente de Windows y funciona de sistemas operativos de servidor sin problemas con dominios atendidas por los servicios de dominio de AD de Azure. También puede utilizar herramientas automatizadas de unión a dominio en esos dominios.
* **Instancia de un dominio por directorio de Azure AD:** puede crear un único dominio de Active Directory para cada directorio de Azure AD.
* **Crear dominios con nombres personalizados:** puede crear dominios con nombres personalizados (por ejemplo, contoso100.local) mediante Azure AD Domain Services. Puede utilizar nombres de dominio comprobados o sin comprobar. Si lo desea, también puede crear un dominio con el sufijo de dominio predefinida de hello (es decir, ' *. onmicrosoft.com ") que ofrece su directorio Azure AD.
* **Integrar con Azure AD:** no necesita tooconfigure o administrar la replicación de servicios de dominio de AD tooAzure. Las cuentas de usuario, las pertenencias a grupos y las credenciales de usuario (contraseñas) del directorio de Azure AD están disponibles automáticamente con Azure AD Domain Services. Los nuevos usuarios, grupos o tooattributes de cambios de su inquilino de Azure AD o el directorio local son los servicios de dominio de tooAzure sincronizan automáticamente AD.
* **Autenticación Kerberos y NTLM:** con compatibilidad para la autenticación Kerberos y NTLM, puede implementar las aplicaciones que dependen de la autenticación integrada de Windows.
* **Utilizar las credenciales y contraseñas corporativas:** las contraseñas para usuarios del inquilino de Azure AD  funcionan con Servicios de dominio de Azure AD. Los usuarios pueden utilizar sus máquinas de combinación toodomain credenciales corporativas, inicie sesión forma interactiva o a través de escritorio remoto y autenticarse en el dominio administrado Hola.
* **Compatibilidad de lectura de un enlace LDAP & LDAP:** puede usar aplicaciones que confían en enlaces LDAP tooauthenticate a los usuarios en dominios atendidas por los servicios de dominio de AD de Azure. Además, las aplicaciones que usan LDAP leen las operaciones de atributos de usuario/equipo tooquery del directorio de hello también pueden trabajar con servicios de dominio de AD de Azure.
* **LDAP seguro (LDAPS):** pueda obtener acceso al directorio de toohello sobre LDAP seguro (LDAPS). El acceso LDAP seguro está disponible en la red virtual de Hola de forma predeterminada. Sin embargo, opcionalmente, también puede habilitar el acceso LDAP seguro a través de hello internet.
* **Directiva de grupo:** puede utilizar cada de un solo GPO integrado para hello usuarios y equipos de cumplimiento de normas de contenedores tooenforce con las directivas de seguridad necesarios para las cuentas de usuario y los equipos unidos a un dominio. También puede crear sus propios GPO personalizados y asignarlos unidades organizativas toocustom demasiado[administrar la directiva de grupo](active-directory-ds-admin-guide-administer-group-policy.md).
* **Administrar DNS:** DNS pueden administrar a los miembros del grupo de 'Administradores de controlador de dominio de AAD' hello para el dominio administrado mediante la administración de DNS conocida herramientas como Hola complemento MMC de administración de DNS.
* **Crear personalizados de unidades organizativas (OU):** miembros del grupo de 'Administradores de controlador de dominio de AAD' hello pueden crear unidades organizativas personalizadas en el dominio administrado Hola. A estos usuarios se les conceden privilegios administrativos completos sobre unidades organizativas personalizadas, por lo que pueden agregar o quitar cuentas de servicio, equipos, grupos, etc. dentro de estas unidades organizativas personalizadas.
* **Disponible en varias regiones de Azure:** vea hello [servicios de Azure por región](https://azure.microsoft.com/regions/#services/) página tooknow Hola regiones de Azure en que los servicios de dominio de Azure AD está disponible.
* **Alta disponibilidad** : Azure AD Domain Services proporciona alta disponibilidad para el dominio. Esta característica ofrece garantía Hola de mayor toofailures de tiempo de actividad y resistencia de servicio. Mantenimiento integrada supervisión ofertas de corrección automática de errores mediante la puesta en marcha nuevas instancias tooreplace no se pudo instancias y tooprovide continuar servicio para su dominio.
* **Usar herramientas de administración familiares:** puede usar herramientas de administración de Windows Server Active Directory conocidas como dominios de hello centro de administración de Active Directory o Active Directory PowerShell tooadminister administrado.
