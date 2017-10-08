---
title: "dispositivos de aaaExtending en la nube capacidades tooWindows 10 a través de Azure Active Directory Join | Documentos de Microsoft"
description: "Ofrece una introducción detallada de cómo los dispositivos Windows 10 pueden utilizar Azure AD Join tooget registrado en Azure Active Directory."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join
## <a name="what-is-azure-active-directory-join"></a>¿Qué es Azure Active Directory Join?
Azure unión de Active Directory (Azure AD Join) es una funcionalidad de Hola que registra un dispositivo propiedad de la empresa en Azure Active Directory tooenable centralizada de administración del dispositivo de Hola. Permite que los usuarios, como los empleados y los estudiantes tooconnect toohello enterprise en la nube a través de Azure Active Directory. Esto permite simplificada implementaciones de Windows y acceso tooorganizational aplicaciones y recursos desde cualquier dispositivo de Windows, tanto corporativos y pertenecen (BYOD).

Azure AD Join está pensado para empresas que es la primera vez que operan en la nube o que solo funcionan en ella, así como pequeñas y medianas empresas que carecen de una infraestructura de Windows Server Active Directory local. Que Azure, dicha combinación AD puede también usarán y grandes organizaciones en los dispositivos que no pueden realizar una unión a un dominio tradicional (dispositivos móviles, por ejemplo), o para usuarios que necesitan principalmente tooaccess Office 365 u otras aplicaciones de SaaS integradas con Azure AD.

Aunque unión a un dominio tradicional Hola sigue ofreciendo Hola local mejor experiencia en los dispositivos que tienen la capacidad de unirse a dominio, Azure AD Join es adecuado para los dispositivos que no pueden unirse a un dominio. Combinación de Azure AD también es adecuado para la administración de usuarios en la nube de Hola. Lo hace mediante funcionalidades de administración de dispositivos móviles, en lugar de usar herramientas de administración de dominio tradicionales, como la directiva de grupo y System Center Configuration Manager (SCCM).

![Información general de los dispositivos de la empresa y personales con un entorno de Active Directory y Azure AD local](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>¿Por qué las empresas deberían adoptar Azure AD Join?
* **Las empresas que están en gran medida en Hola nube**: si se ha movido o se está moviendo tooa modelo en el que se reduce la superficie local y desea toooperate más en la nube de hello, Azure AD Join pueden beneficiarse también. Quizá ha creado cuentas de Azure AD manualmente o mediante la sincronización de su entorno de Active Directory local. En cualquier caso, tiene una cuenta de Azure AD y se puede usar toosign en tooWindows 10. Los usuarios pueden unir su equipos tooAzure AD a través de cualquier experiencia de out-of-box Hola (configuración rápida OOBE) o a través del menú de configuración de Hola. Después de unirse, los usuarios disfrutarán de inicio de sesión (SSO) acceso toocloud recursos individuales como Office 365, en sus exploradores o aplicaciones de Office.
* **Instituciones educativas**: uno de los escenarios de hello recibimos sobre a menudo es que las instituciones educativas tienen dos tipos de usuario: profesores y los estudiantes. Los miembros de profesores se consideran a miembros a largo plazo de organización de hello, por lo que crea cuentas locales para ellos es deseable. Pero los estudiantes que son miembros shorter-term de organización de hello y, por tanto, se pueden administrar en Azure AD. Esto significa que se puede insertar escala directorio toohello en la nube en lugar de almacenada localmente. También significa que los estudiantes pueden iniciar sesión en tooWindows con sus cuentas de Azure AD y obtener acceso a recursos de 365 de tooOffice, en sus exploradores o aplicaciones de Office.
* **Las empresas de Retail**: hemos sabido acerca de los clientes de otro escenario es sus trabajadores de temporada de toomanage desea más fácilmente.  De nuevo, las cuentas para los empleados a jornada completa y a más largo plazo se suelen crear como cuentas locales en equipos unidos a un dominio. Pero los trabajadores de la temporada pertenecen shorter-term org hello, por lo que es conveniente toomanage ellos donde licencias de usuario se pueden mover más fácilmente alrededor. La creación de estas cuentas de usuario en la nube de hello con Office 365 licencias permite Hola usuarios tooget Hola los beneficios del inicio de sesión tooWindows y las aplicaciones de Office con una cuenta de Azure AD. Además, se mantiene más flexibilidad con sus licencias una vez que abandonan su puesto de trabajo.
* **Otras empresas**: aunque mantenga a los usuarios en un entorno de Active Directory local, se puede beneficiar de tener a los usuarios unidos con Azure AD. Eso es porque Azure AD ofrece una experiencia de unión simplificada, la administración eficaz de dispositivos, la inscripción automática en la administración de dispositivos móviles y el inicio de sesión único a Azure AD y los recursos locales.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>¿Qué funcionalidades ofrece Azure AD Join?
Con Azure AD Join, obtendrá el siguiente hello:

* **Aprovisionamiento automático de dispositivos corporativos**: con Windows 10, los usuarios pueden configurar un dispositivo nuevo, reducido en experiencia de out-of-box hello, sin la participación de TI.
* **Compatibilidad con factores de forma moderna**: combinación de Azure AD funciona en dispositivos que no tienen dominio tradicional de hello combinar capacidades.  
* **Soporte técnico para cuentas organizativas existentes**: los usuarios ya no necesita toocreate y mantener un un tooget de cuenta Microsoft personal Hola mejor experiencia en dispositivos emitidos por la empresa, como lo hacían con Windows 8. Ahora, pueden usar sus cuentas profesionales existentes en Azure AD. Para muchas organizaciones, esto básicamente significa que los usuarios pueden configurar e iniciar sesión en tooWindows con hello mismo credenciales que usan tooaccess Office 365.
* **Inscripción en la administración automática de dispositivos móviles**: dispositivos pueden inscribirse automáticamente en administración de dispositivos móviles cuando se conecta tooAzure AD. Este proceso funciona con soluciones de administración de dispositivos móviles de asociados y Microsoft Intune. Cuando se realiza la administración de dispositivos con Intune, los administradores de TI pueden controlar/administrar Azure AD-dispositivos Unidos a un junto con dispositivos Unidos a un dominio en la consola de administración de SCCM Hola.
* **Solo los recursos de inicio de sesión toocompany**: los usuarios disfrutar de inicio de sesión único de tooapps de escritorio de Windows hello y recursos de nube de hello, como Office 365 y miles de aplicaciones empresariales que se basan en Azure AD para la autenticación a través de [De azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Dispositivos corporativos que están combinada tooAzure AD también gozan de recursos de tooon locales SSO cuando el dispositivo de hello está en una red corporativa y desde cualquier lugar cuando estos recursos se exponen a través de hello [el Proxy de aplicación de Azure AD](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **Movilidad de estado del SO**: la configuración de accesibilidad, los sitios web, las contraseñas Wi-Fi y otras opciones se sincronizarán en los dispositivos de la empresa sin necesidad de una cuenta de Microsoft personal.
* **Tienda de Windows preparada para la empresa**: Hola tienda Windows admite la adquisición de aplicaciones y licencias con cuentas de Azure AD. Las organizaciones pueden aplicaciones de la licencia de volumen y que estén disponibles toohello a los usuarios en su organización.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>¿Cómo funcionan diferentes dispositivos con Azure AD Join?
| Dispositivos corporativos (dominio local tooon combinadas) | Dispositivos corporativos (toohello unido a la nube) | Dispositivo personal |
| --- | --- | --- |
| Los usuarios pueden iniciar sesión en Windows con las credenciales de trabajo (como lo hacen hoy). |Los usuarios pueden iniciar sesión en tooWindows con credenciales de trabajo que se administran en Azure AD. Esto es importante para los dispositivos corporativos en tres casos: <ol><li>organización de Hello no tiene Active Directory local (por ejemplo, una pequeña empresa).</li><li>organización de Hello no crea todas las cuentas de usuario en Active Directory (por ejemplo, las cuentas de los trabajadores de la temporada, estudiantes o consultores no se crean en Active Directory).</li><li>organización de Hello tiene dispositivos corporativos que no pueden ser el dominio unido a tooan (local), como teléfonos o tabletas que ejecutan una SKU móviles (por ejemplo, un dispositivo secundaria realizada tooa generador/comercial piso).</li></ol> Azure AD Join permite unir dispositivos de la empresa para organizaciones administradas y federadas. |Los usuarios inician sesión en tooWindows con sus credenciales de cuenta de Microsoft personales (sin cambios). |
| Los usuarios tienen acceso tooroaming configuración y enterprise de hello tienda Windows. Estos servicios funcionan con cuentas profesionales y no requieren una cuenta de Microsoft personal. Para ello, las organizaciones tooconnect su tooAzure de Active Directory local AD. |Los usuarios pueden hacer la configuración de autoservicio. Pueden ir a través de la experiencia de primera ejecución hello (FRX) a través de su cuenta profesional como una alternativa toohaving TI aprovisione los dispositivos hello, aunque ambos métodos son compatibles. |Los usuarios pueden agregar fácilmente una cuenta profesional administrada en Active Directory o Azure AD. |
| Los usuarios tienen la posibilidad SSO desde aplicaciones de escritorio toowork hello, sitios Web y recursos, incluidos los recursos locales y las aplicaciones de nube que usan Azure AD para la autenticación. |Los dispositivos se registra automáticamente en el directorio empresarial de hello (Azure AD) y se inscribe automáticamente en administración de dispositivos móviles. (Característica de Azure AD Premium). |Los usuarios tienen la capacidad de SSO a través de las aplicaciones y toowebsites/recursos con esta cuenta profesional. |
| Los usuarios pueden agregar sus tooaccess de cuentas de Microsoft personal sus imágenes personales y archivos sin afectar a los datos de la empresa. (Configuración móvil continuar toowork con su cuenta profesional). Hola cuenta de Microsoft permite SSO y ya no unidades Hola itinerancia de configuración. |Los usuarios pueden usar el autoservicio de restablecimiento de contraseña (SSPR) en winlogon, lo que significa que pueden restablecer una contraseña olvidada. (Característica de Azure AD Premium). |Los usuarios tienen acceso toohello almacén de empresa de Windows para que puedan adquirir y usar aplicaciones de línea de negocio en sus dispositivos personales. |

## <a name="additional-information"></a>Información adicional
* [Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Autenticación de identidades sin contraseñas a través de Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)

