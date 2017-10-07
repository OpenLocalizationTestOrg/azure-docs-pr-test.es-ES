---
title: "dispositivos de aaaUsing Windows 10 en el área de trabajo | Documentos de Microsoft"
description: "Proporciona una instantánea de capacidades para los usuarios y TI, contraste maneras diferentes de hello un dispositivo se pueden aprovisionar y usar en una empresa con Windows 10."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Uso de dispositivos de Windows 10 en el área de trabajo
Ámbito de aplicación: equipos con Windows 10

Windows 10 ofrece tres modelos para las organizaciones que permiten a los usuarios tooaccess los recursos de trabajo en un modo cómodo y seguro.

* **Azure Active Directory unirse a** (Azure AD Join), para los trabajadores que acceder a los recursos, como Office 365 principalmente en la nube de Hola. Azure AD Join es una experiencia de aprovisionamiento de trabajo de autoservicio nueva en Windows 10.
* **Unión a un dominio**: para las organizaciones que tienen inversiones en aplicaciones y recursos locales. Unión a un dominio ofrece una experiencia mejorada en Windows 10 cuando se conecta tooAzure AD.
* **Simplifica una nueva experiencia BYOD**, para los usuarios que quieran tooadd un trabajo de la cuenta o educativa tooWindows y obtener acceso fácilmente a los recursos en los dispositivos personales.

Hello tabla siguiente presenta una instantánea de capacidades para los usuarios y los administradores de TI, contraste maneras diferentes de hello un dispositivo se pueden aprovisionar y usar en una empresa con Windows 10:

|  | Unión a un dominio | Azure AD Join | Dispositivo personal |
| --- | --- | --- | --- |
| Inicio de sesión de dispositivos de Windows para cuentas profesionales o educativas. |Sí |Sí |No |
| Usuario de inicio de sesión único (SSO) tooOffice 365 y aplicaciones de Azure AD. SSO es toosign de capacidad de hello en una sola vez tooaccess recursos de la organización. |Sí |Sí |Sí |
| Aplicaciones de usuario SSO tooKerberos/NTLM. |Sí |Limitado |Sí, a través de VPN |
| Autorización segura y práctico inicio de sesión único para cuentas profesionales o educativas con Microsoft Passport y Windows Hello. |Sí |Sí |Sí |
| Obtener acceso a la tienda de Windows tooenterprise con una cuenta profesional o educativa (no una cuenta de Microsoft). |Sí |Sí |Sí |
| Movilidad de las configuraciones de usuario conforme a la empresa entre dispositivos que usan cuentas profesionales o educativas. |Sí |Sí |Sí |
| Hola capacidad toorestrict acceso tooorganizational aplicaciones toodevices que son compatibles con las directivas de dispositivo organizativa. |Sí |Sí |Sí |
| Autoservicio de usuarios para el aprovisionamiento de dispositivos para trabajar desde cualquier lugar. |No |Sí |Sí |
| Dispositivos de toomanage de capacidad. |Sí, a través de GP/SCCM |Sí |Sí |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Uso de dispositivos de trabajo con Azure AD Join y la unión a un dominio en Windows 10
10 de Windows ofrece dos formas para que los recursos de trabajo de tooaccess de dispositivos de trabajo:

* Azure AD Join
* Unión a un dominio
  
  Ambos pueden ser opciones válidas según las necesidades y los requisitos de una organización. En algunos casos, las organizaciones pueden beneficiarse de la habilitación de ambos métodos de implementación.

## <a name="when-toouse-azure-active-directory-join"></a>Cuando toouse Azure Active Directory Join
Azure AD Join es una nueva experiencia de aprovisionamiento de trabajo de autoservicio en Windows 10.  Está dirigido a los trabajadores que tienen acceso a los recursos de trabajo, como Office 365 principalmente en la nube de Hola. Es una forma sencilla tooconfigure equipos, tabletas y teléfonos para enterprise Hola. Los dispositivos se administran mediante la administración de dispositivos móviles, con controles coherentes entre plataformas de Windows.

**Use Azure AD Join por cualquiera de estos motivos**:

* Desea tooenable Hola autoservicio aprovisionamiento de dispositivos para los trabajadores de hello, visite.
* Desea proporcionar a los usuarios dispositivos móviles de trabajo como tabletas y teléfonos.
* Toomanage un conjunto de usuarios que desee en Azure AD en lugar de en Active Directory, como los trabajadores de la temporada, contratistas o a los alumnos.
* Desea tooprovide unión capacidades tooworkers en oficinas de sucursales remotas con la infraestructura local limitada.
* No tiene ningún entorno de Active Directory local.

Algunas organizaciones usará Azure AD Join como dispositivos de propiedad de trabajo de una toodeploy de modo principal hello, especial a medida que migran la mayoría o todos de su nube toohello de recursos. Las organizaciones de híbrida con Active Directory y Azure AD también pueden elegir toodeploy un método u otra función usuario de Hola o departamento.

Por ejemplo, los distritos escolares y las universidades pueden administrar al personal en Active Directory y a los estudiantes en Azure AD. Algunas compañías podrían necesitar toomanage de oficinas remotas o departamentos de ventas en Azure AD. Ambos métodos, Azure AD Join y la unión a un dominio, pueden usarse dentro de una organización híbrida. Azure AD combinación puede ser un buen complemento toodomain para la implementación de dispositivos en un entorno de trabajo.

**Si es hello más habitual acceder a tooenterprise los recursos a través de la nube de hello, su organización puede disfrutar de ventajas adicionales si**:

* Puede quitar las dependencias de infraestructura de identidad local.
* Puede simplificar el modelo de implementación de dispositivos dejando las soluciones de creación de imágenes y permitiendo la configuración de autoservicio.
* Puede usar todos los dispositivos de toomanage de administración de dispositivos móviles en diferentes plataformas.

Para obtener más información acerca de Azure AD Join, vea [extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="when-toouse-domain-join-or-keep-using-it"></a>Al unirse un dominio de toouse (o seguir usándola)
Durante hello en los últimos 15 años, muchas organizaciones han usado los dispositivos de trabajo de tooconnect de unión de dominio. Permite a los usuarios toosign cuentas en dispositivos tootheir con su Active Directory profesionales o educativas. Unión a un dominio también permite a TI toocentrally y administrar completamente estos dispositivos. Las organizaciones suelen basarse en métodos tooprovision dispositivos de imágenes a menudo usar toomanage de System Center Configuration Manager (SCCM) o directiva de grupo (GP) ellos.

**Su empresa debería usar la unión a un dominio (o continuar usándola) por cualquiera de los siguientes motivos**:

* Tiene dispositivos de implementada toothese de aplicaciones de Win32 que usan NTLM o Kerberos.
* Se requiere que los dispositivos toomanage GP o SCCM/DCM.
* Desea que los toocontinue toouse imágenes soluciones tooconfigure dispositivos para los empleados.

**Unión a un dominio de Windows 10, también podrá siguiente Hola ventajas cuando conectado tooAzure AD**:

* Autenticación sólida de dispositivo enlazado y práctico inicio de sesión único para cuentas profesionales o educativas con Microsoft Passport y Windows Hello.
* Obtener acceso a toohello enterprise tienda Windows para dispositivos que usan el trabajo o escuela cuentas (no requerida ninguna cuenta de Microsoft).
* Movilidad de las configuraciones de usuario conforme a la empresa entre dispositivos que usan cuentas profesionales o educativas (sin necesidad de una cuenta de Microsoft).
* Hola capacidad toorestrict acceso tooorganizational aplicaciones toodevices que son compatibles con las directivas de dispositivo organizativa.

Para obtener más información acerca de Azure AD Join, vea [extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Habilitación de la unión de dispositivos personales para el trabajo o la escuela
toosupport BYOD en las empresas de hello, Windows 10 ofrece Hola usuario Hola capacidad tooadd un trabajo o escuela cuenta tootheir equipo, Tablet PC o teléfono. Después de hello usuario agrega un trabajo o cuenta organizativa, dispositivo Hola está registrado con Azure AD y opcionalmente inscritos en el sistema de administración de dispositivos móviles de Hola Hola organización ha configurado. directorio de Hello mostrará estos dispositivos como 'Registrado' vs. "Unido a Azure AD". Los administradores de TI pueden aplicar diferentes directivas según esta información, proporcionando un enfoque más ligero en dispositivos personales que en dispositivos de trabajo, si así lo desea.

Los usuarios puedan agregar un trabajo o escuela dispositivo personal de cuenta tootheir una forma muy cómoda. Puede hacerlo al tener acceso a una aplicación de trabajo para hello primera vez o puede hacer manualmente a través del menú de configuración de Hola. Esta cuenta proporcionará recursos tooorganizational SSO.

Para obtener más información acerca de Azure AD Join, vea [conectar dispositivos Unidos a dominio tooAzure AD para Windows 10 experimenta](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Habilitación de la unión a un dominio o Azure AD Join
Todos los métodos descritos anteriormente (unión a un dominio, combinación de Azure AD y agregar cuenta profesional o educativa) tienen puntos de entrada en la experiencia del usuario Hola Windows 10. Sin embargo, todos requieren una funcionalidad de TI Administrador tooenable hello en la infraestructura de Hola para que funcione la experiencia de Hola.

## <a name="requirements-for-deploying-azure-ad-join"></a>Requisitos para implementar Azure AD Join
toodeploy Azure AD Join para cualquier conjunto de usuarios debe Hola siguientes:

* Una suscripción de Azure AD.
* Una suscripción de Azure AD Premium, como la inscripción automática a la administración de dispositivos móviles, en el caso de que requiera más funcionalidades.
* Administración de dispositivos móviles, por ejemplo, una suscripción a Microsoft Intune, administración de dispositivos móviles para Office 365 o cualquiera de los proveedores de administración de dispositivos móviles de socios comerciales de Hola que se integran con Azure AD. (Vea hello [sección de preguntas más frecuentes sobre](#frequently-asked-questions) cerca del final de Hola de este artículo para obtener más información).

Si sus instalaciones son híbridos, se recomienda encarecidamente que implemente local directory tooAzure AD de Azure AD Connect tooextend Hola.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Requisitos para usar la unión a un dominio con Azure AD
Unión a un dominio continúa toowork porque tiene siempre. Sin embargo, tooget ventajas de hello Azure AD, necesitará Hola siguientes:

* Una suscripción de Azure AD.
* Una implementación de Azure AD Connect tooextend Hola local directory tooAzure AD.
* Una directiva que permite a los dispositivos Unidos a un dominio toohave acceso condicional tooAzure AD.
* Una directiva que permita el acceso demasiado "dispositivos Unidos a dominio" Si desea toobe toorestrict capaz de acceso para algunos dispositivos.
* System Center Configuration Manager versión 1509 para Technical Preview, tooenable reglas para exigir a dispositivos compatibles. (Consulte la documentación de TechNet de Hola y de entrada de blog).

Para obtener más información acerca de la unión a un dominio de Windows 10, consulte [conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Requisitos para usar BYOD y "Agregar una cuenta profesional o educativa"
tooenable "bring your own device" (BYOD) con cuentas profesionales o educativas, necesita Hola siguiente:

* Una suscripción de Azure AD.
* Una suscripción de Azure AD Premium, como la inscripción automática a la administración de dispositivos móviles, en el caso de que requiera más funcionalidades.

## <a name="requirements-for-using-microsoft-passport"></a>Requisitos para usar Microsoft Passport
tooenable Microsoft Passport, necesitará la siguiente hello:

* Una infraestructura de clave pública (PKI) para compatibilidad de autenticación basada en certificados que usa Microsoft Passport.
* Una suscripción de Intune para la compatibilidad con la autenticación basada en certificados que usa Microsoft Passport para Azure AD Join y cuentas profesionales o educativas.
* System Center Configuration Manager versión 1509 para Technical Preview (vea la documentación de TechNet de Hola y de entrada de blog) para la compatibilidad con la autenticación basada en certificados que utiliza Microsoft Passport para unirse a un dominio.
* Una directiva para habilitar Microsoft Passport de organización de Hola.

Como una alternativa toousing una PKI, puede habilitar basada en claves Microsoft Passport haciendo Hola siguiente:

* Implemente controladores de dominio de 'Versión preliminar de producción 1' en Windows Server 2016 (no es necesario el nivel funcional del bosque o del dominio y bastarán varios controladores de dominio para la redundancia que da servicio a cada sitio de Active Directory).
* Establecer directiva tooenable Microsoft Passport de organización de Hola.

Para más información sobre Microsoft Passport y Windows Hello en Windows 10, consulte <link-to-MS-Passport-and-Windows-Hello-document>.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>¿Qué productos de administración de dispositivos móviles de asociados se integran con Azure AD?
Hello siguiente proveedor productos se integran con Azure AD para la inscripción unificada y acceso condicional en Windows 10:

* AirWatch de VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* Administración de dispositivos móviles locales SOTI
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>¿Qué ocurre con la unión al área de trabajo en Windows 10?
El área de trabajo se utilizó en Windows 8.1 tooenable BYOD. En Windows 10, BYOD se habilita mediante "Agregar una cuenta profesional o educativa", como se explicó anteriormente en este documento. Para las organizaciones que no integran su administración de dispositivos móviles con Azure AD, los usuarios pueden inscribir dispositivos hello en la administración de forma manual mediante **configuración** > **cuentas**  >  **Acceso al trabajo**.

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>¿Pueden a los usuarios conectarse a su cuenta de dominio de tootheir de cuenta de Microsoft en Windows 10?
No en Windows 10. En Windows 8.1, los usuarios de dispositivos Unidos a un dominio podrían "conectar" su tooenable de cuenta de dominio de Microsoft cuenta (por ejemplo, Hotmail, Live, Outlook, Xbox, etc.) tootheir ciertos experiencias como servicios tooLive SSO, uso de la tienda Windows hello y movilidad de configuración de usuario en todos los dispositivos. En Windows 10, Hola cuenta de Microsoft "conectar" funcionalidad se ha retirado. usuario de Hello puede agregar una o varias cuentas de Microsoft como servicios de cuentas adicionales tooenable SSO tooconsumer como Hola tienda Windows. Puede hacerlo en **Configuración** > **Cuentas** > **Su cuenta**.

Los usuarios que realicen la actualización de los dispositivos de Windows 8.1 Unidos a un dominio y que tenía su cuenta de Microsoft conectados, habrá su cuenta de Microsoft conectado agrega automáticamente toohello lista de cuentas adicionales que se usan.

## <a name="additional-information"></a>Información adicional
* [Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)

