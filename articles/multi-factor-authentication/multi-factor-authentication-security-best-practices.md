---
title: "prácticas recomendadas de aaaSecurity para MFA | Documentos de Microsoft"
description: "Este documento proporciona las prácticas recomendadas de uso de Azure MFA con cuentas de Azure"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>Prácticas recomendadas de seguridad para usar Azure Multi-Factor Authentication con cuentas de Azure AD

Verificación en dos pasos es la opción de hello preferido para la mayoría de las organizaciones que desean a tooenhance su proceso de autenticación. Azure Multi-Factor Authentication (MFA) ayuda a las empresas a cumplir sus requisitos de seguridad y cumplimiento al tiempo que proporciona una experiencia de inicio de sesión sencilla para sus usuarios. Este artículo tratan algunas sugerencias que se deben considerar al planear la adopción de Hola de MFA de Azure.

## <a name="deploy-azure-mfa-in-hello-cloud"></a>Implementar Azure MFA en la nube de Hola

Hay dos maneras tooenable Azure MFA para todos los usuarios.

* Comprar licencias para cada usuario (Azure MFA, Azure AD Premium o Enterprise Mobility + Security)
* Crear un Proveedor de Multi-Factor Auth y pagar por usuario o por autenticación

### <a name="licenses"></a>Licencias
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

Si dispone de licencias de Azure AD Premium o Enterprise Mobility + Security, ya tiene Azure MFA. Su organización no tiene usuarios de tooextend nada adicional hello en dos pasos comprobación capacidad tooall. Solo debe tooassign un usuario de tooa de licencia y, a continuación, puede activar MFA.

Al configurar la autenticación multifactor, considere la posibilidad de hello sigue sugerencias:

* No cree un Proveedor de Multi-Factor Auth por autenticación. Si lo hace, puede acabar pagando por solicitudes de comprobación de usuarios que ya tienen licencias.
* Si no tiene suficientes licencias para todos los usuarios, puede crear un rest de Hola de toocover de proveedor de autenticación multifactor por usuario de su organización. 
* Azure AD Connect solo es un requisito si va a sincronizar su entorno de Active Directory local con un directorio de Azure AD. Si usa un directorio de Azure AD que no está sincronizado con una instancia local de Active Directory, no necesita Azure AD Connect.

### <a name="multi-factor-auth-provider"></a>Proveedor de Multi-Factor Authentication
![Proveedor de Multi-Factor Authentication](./media/multi-factor-authentication-security-best-practices/authprovider.png)

Si no tiene licencias que incluyan Azure MFA, puede crear un proveedor de autenticación MFA. 

Al crear el proveedor de autenticación de hello, que necesita tooselect un directorio y considere la posibilidad de hello detalles siguientes:

* No es necesario un toocreate del directorio de Azure AD un proveedor de autenticación multifactor, pero obtendrá más funcionalidad a uno. Hola siguientes características está habilitada al asociar Hola proveedor de autenticación a un directorio de Azure AD:  
  * Extender tooall de comprobación de dos pasos los usuarios  
  * Ofrecen características adicionales, como el portal de administración de hello, los saludos personalizados y los informes de los administradores globales.
* Se necesita DirSync o Sincronización de AAD si va sincroniza el entorno de Active Directory local con un directorio de Azure AD. Si utiliza un directorio de Azure AD que no está sincronizado con una instancia local de Active Directory, no necesita DirSync ni Sincronización de AAD.
* Elija el modelo de consumo de Hola que mejor se adapte a su negocio. Una vez que seleccione el modelo de uso de hello, no podrá cambiarlo. Hola dos modelos son:
  * Por autenticación: se le cobra por cada comprobación. Use este modelo si quiere verificación en dos pasos para cualquier persona que acceda a una aplicación determinada, pero no para usuarios específicos.
  * Por usuario habilitado: le cobra por cada usuario que se habilita para Azure MFA. Use este modelo si tiene algunos usuarios con licencias de Enterprise Mobility Suite o Azure AD Premium y otros sin ellas.

### <a name="supportability"></a>Compatibilidad
Puesto que la mayoría de los usuarios están acostumbrados toousing contraseñas solo tooauthenticate, es importante que su empresa informa de los usuarios de tooall con respecto a este proceso. Este conocimiento puede reducir probabilidad de Hola que los usuarios llamar a su departamento de soporte técnico para problemas poco importantes relacionados tooMFA. Sin embargo, hay algunos escenarios en los que es necesario deshabilitar temporalmente MFA. Hola uso siguiendo las directrices toounderstand cómo toohandle estos escenarios:

* Formar a los escenarios de toohandle de personal de soporte técnico donde hello usuario no puede iniciar sesión en porque la aplicación móvil de Hola o teléfono no recibe una llamada de teléfono o la notificación. Soporte técnico puede [habilitar una omisión por única vez](multi-factor-authentication-whats-next.md#one-time-bypass) tooallow un tooauthenticate de usuario una sola vez al "Omitir" la verificación en dos pasos. Hola omisión es temporal y expira después de un número especificado de segundos.
* Considere la posibilidad de hello [capacidad de IP de confianza](multi-factor-authentication-whats-next.md#trusted-ips) de MFA de Azure como una comprobación de manera toominimize en dos pasos. Con esta característica, los administradores de un inquilino administrado o federado pueden omitir la comprobación de dos pasos para los usuarios que inician sesión desde la intranet local de la compañía de Hola. Hola características están disponibles para los inquilinos de Azure AD que tienen licencias de Azure AD Premium, Enterprise Mobility Suite o Azure la autenticación multifactor.

## <a name="best-practices-for-an-on-premises-deployment"></a>Procedimientos recomendados para una implementación local
Si la empresa decidió tooleverage su propio tooenable infraestructura MFA, debe toodeploy un servidor Azure Multi-factor Authentication local. componentes de servidor MFA de Hola se muestran en hello siguiente diagrama:

![Componentes de servidor MFA predeterminados: consola, motor de sincronización, portal de administración, servicio en la nube](./media/multi-factor-authentication-security-best-practices/server.png)\*No se instalan de forma predeterminada \**Están instalados pero no habilitados de forma predeterminada

El servidor Azure Multi-Factor Authentication puede proteger los recursos en la nube y los recursos locales mediante la federación. Debe disponer de AD FS y federarlo con el inquilino de Azure AD.
Al configurar el servidor de autenticación multifactor, considere la posibilidad de hello detalles siguientes:

* Si la protección de recursos de Azure AD con los servicios de federación de Active Directory (AD FS), primer paso de verificación Hola se llevará a cabo de manera local mediante AD FS. Hola segundo paso es realiza localmente respondiendo a una notificación de Hola.
* No es necesario tooinstall Hola servidor Azure Multi-factor Authentication del servidor de federación de AD FS. Sin embargo, Hola adaptador de autenticación multifactor para AD FS debe instalarse en un Windows Server 2012 R2 que ejecuta AD FS. Puede instalar el servidor de hello en un equipo diferente, siempre y cuando sea una versión compatible e instalar a adaptador de hello AD FS por separado en el servidor de federación de AD FS. 
* Asistente para la instalación de Hola la autenticación multifactor AD FS adaptador crea un grupo de seguridad denominado PhoneFactor Admins en Active Directory y, a continuación, agrega el grupo de toothis de cuenta de servicio de AD FS. Compruebe que se creó Hola al grupo PhoneFactor Admins en el controlador de dominio, y esa cuenta de servicio de hello AD FS es un miembro de este grupo. Si es necesario, agregue manualmente toohello de cuenta de servicio de hello AD FS al grupo PhoneFactor Admins en el controlador de dominio.

### <a name="user-portal"></a>Portal de usuario
portal de usuarios de Hello permite capacidades de autoservicio y proporciona un conjunto completo de capacidades de administración de usuarios. Se ejecuta en un sitio web de Internet Information Server (IIS). Usar hello siguiendo las directrices tooconfigure este componente:

* Use IIS 6 o superior.
* Instale y registre ASP.NET v2.0.507207.
* Asegúrese de que este servidor se pueda implementar en una red perimetral.

### <a name="app-passwords"></a>Contraseñas de aplicación
Si su organización está federada para SSO con Azure AD y va toobe con Azure MFA, a continuación, tenga en cuenta de hello detalles siguientes:

* contraseña de aplicación Hola se comprueba mediante Azure AD y, por tanto, omite la federación. La federación solo se usa activamente al configurar contraseñas de aplicación.
* Para los usuarios federados de (SSO), las contraseñas se almacenan en Id. de organización de Hola. Si el usuario de hello deja la empresa de hello, esa información tiene Id. de tooorganizational tooflow mediante DirSync. La deshabilitación o eliminación de cuenta puede tardar horas de toothree toosync, lo que retrasa la deshabilitación o eliminación de contraseñas de aplicación en Azure AD.
* La configuración del control de acceso de cliente local no admite la contraseña de aplicación
* No hay ningún registro o funcionalidad de auditoría en la autenticación local que esté disponible para contraseñas de aplicación.
* Puede que algunos diseños de arquitectura avanzada requieran el uso de una combinación de nombre de usuario y contraseñas de la organización y de contraseñas de aplicación cuando se usa la verificación de dos pasos con clientes, en función de dónde se autentiquen. Para los clientes que se autentican en una infraestructura local, usaría un nombre de usuario y una contraseña de la organización. Para los clientes que se autentican en Azure AD, usaría la contraseña de aplicación Hola.
* De forma predeterminada, los usuarios no pueden crear contraseñas de aplicación. Si necesita contraseñas de aplicación de tooallow usuarios toocreate, seleccione hello **permitir toosign de las contraseñas de aplicación de los usuarios toocreate en aplicaciones sin explorador** opción.

## <a name="additional-considerations"></a>Consideraciones adicionales
Use esta lista para conocer algunas consideraciones adicionales y orientaciones para cada componente que se implementa de forma local:

- Instalación de Azure Multi-Factor Authentication con el [Servicio de federación de Active Directory](multi-factor-authentication-get-started-adfs.md).
- Instalar y configurar Hola servidor Azure MFA con [autenticación RADIUS](multi-factor-authentication-get-started-server-radius.md).
- Instalar y configurar Hola servidor Azure MFA con [autenticación IIS](multi-factor-authentication-get-started-server-iis.md).
- Instalar y configurar Hola servidor Azure MFA con [autenticación de Windows](multi-factor-authentication-get-started-server-windows.md).
- Instalar y configurar Hola servidor Azure MFA con [autenticación LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Instalar y configurar Hola servidor Azure MFA con [puerta de enlace de escritorio remoto y servidor de Azure Multi-factor Authentication con RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- Instalar y configurar la sincronización entre el servidor Azure MFA hello y [Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md).
- [Implementar el servicio Web de aplicación móvil de Azure Multi-factor Authentication Server hello](multi-factor-authentication-get-started-server-webservice.md).
- [Configuración avanzada de VPN con Azure Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) para aparatos VPN de Cisco ASA, Citrix Netscaler, y Juniper/Pulse Secure mediante LDAP o RADIUS.

## <a name="next-steps"></a>Pasos siguientes
Si bien este artículo resalta algunas prácticas recomendadas para Azure MFA, existen otros recursos que también puede usar al planear la implementación de MFA. lista de Hola a continuación tiene algunos artículos claves que pueden ayudarle durante este proceso:

* [Informes en Azure Multi-Factor Authentication](multi-factor-authentication-manage-reports.md)
* [experiencia de registro de comprobación de Hello en dos pasos](multi-factor-authentication-end-user-first-time.md)
* [P+F sobre Azure Multi-Factor Authentication](multi-factor-authentication-faq.md)

