---
title: "Active Directory Domain Services: escenarios de implementación | Microsoft Docs"
description: "Escenarios de implementación de Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>Escenarios y casos de uso de implementación
En esta sección, echamos un vistazo a algunos escenarios y casos de uso que se benefician de Azure Active Directory (AD) Domain Services.

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Administración sencilla y segura de máquinas virtuales de Azure
Puede usar servicios de dominio de Active Directory de Azure toomanage máquinas virtuales de Azure de forma optimizada. Máquinas virtuales de Azure puede ser toohello Unidos a un dominio administrado, lo que permite toouse toolog en las credenciales de la instancia de AD corporativo. Este enfoque ayuda a evitar problemas de administración de credenciales, como el mantenimiento de cuentas de administrador local en cada una de sus máquinas virtuales de Azure.

Máquinas virtuales de servidor que están combinadas toohello administrado dominio también pueden administrar y proteger mediante Directiva de grupo. Puede aplicar las líneas de base de seguridad necesarios tooyour virtual de Azure máquinas y bloquear con arreglo a las directrices de seguridad de la empresa. Por ejemplo, puede usar el grupo Directiva administración capacidades toorestrict Hola tipos de aplicaciones que se pueden iniciar en estas máquinas virtuales.

![Administración simplificada de máquinas virtuales de Azure](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

Como los servidores y otras infraestructuras alcanza el final del ciclo de vida, Contoso refiere a muchas aplicaciones hospedadas actualmente en la nube de toohello local. Su norma actual de TI dictamina que los servidores que hospedan aplicaciones corporativas se deben unir a un dominio y administrarse mediante la directiva de grupo. Del Contoso Administrador de TI preferir toodomain unir implementados en Azure, toomake administración más fácil de los equipos virtuales. Como resultado, los administradores y usuarios pueden iniciar sesión con sus credenciales corporativas. En hello mismo tiempo, las máquinas pueden estar toocomply configurado con líneas de base de seguridad necesarios mediante la directiva de grupo. Contoso preferiría no toohave toodeploy, supervisar y administrar controladores de dominio en Azure toosecure máquinas virtuales de Azure. Por lo tanto, Azure AD Domain Services es un elemento idóneo para este caso de uso.

**Notas de implementación**

Considere la posibilidad de hello siguientes puntos son importantes para este escenario de implementación:

* Los dominios administrados que proporcionan Azure AD Domain Services solo admiten una única estructura de unidad organizativa plana. Todas las máquinas unidas a un dominio residen en una única unidad organizativa plana. Sin embargo puede elegir toocreate unidades organizativas personalizadas.
* Servicios de dominio de Azure AD es compatible con la directiva de grupo simple en forma de Hola de un GPO integrado cada para hello usuarios y equipos de contenedores. Puede crear GPO personalizados y dirigirlas toocustom las unidades organizativas.
* Servicios de dominio de Azure AD admite el esquema de objeto de equipo de base AD de Hola. No se puede extender el esquema del objeto de equipo de Hola.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>Elevación y MAYÚS una aplicación local que usa LDAP bind autenticación tooAzure servicios de infraestructura
![Enlace LDAP](./media/active-directory-domain-services-scenarios/ldap-bind.png)

Contoso cuenta con una aplicación local que se compró a un ISV hace muchos años. aplicación Hello está actualmente en modo de mantenimiento Hola ISV y aplicación de toohello cambios solicitante es muy caro para Contoso. Esta aplicación tiene un cliente basado en web que recopila credenciales de usuario mediante un formulario web Forms y, a continuación, se autentica a los usuarios mediante la realización de una toohello de enlace LDAP Active Directory corporativo. Contoso desea que toomigrate esta tooAzure servicios de infraestructura de aplicación. Es conveniente que la aplicación hello funciona tal cual, sin necesidad de realizar cambios. Además, los usuarios deben ser capaz de tooauthenticate con sus credenciales corporativas existentes y sin tener cosas toodo de tooretrain a los usuarios de forma diferente. En otras palabras, los usuarios finales deben ajena de donde se ejecuta la aplicación hello y migración de hello debe ser transparente toothem.

**Notas de implementación**

Considere la posibilidad de hello siguientes puntos son importantes para este escenario de implementación:

* Asegúrese de que la aplicación hello no es necesario toohello toomodify/escribir datos de directorio. No se admite dominios de toomanaged de acceso de escritura LDAP proporcionadas por servicios de dominio de Active Directory de Azure.
* No se puede cambiar las contraseñas directamente en el dominio administrado Hola. Los usuarios finales pueden cambiar su contraseña o mediante el mecanismo de cambio de contraseña de autoservicio de Azure AD o con respecto al directorio local de Hola. Estos cambios son sincronizados automáticamente y estén disponibles en el dominio administrado Hola.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>Elevación y MAYÚS una aplicación local que usa LDAP lee tooaccess Hola directory tooAzure servicios de infraestructura
Contoso tiene una aplicación de línea de negocio (LOB) local que se desarrolló hace casi una década. Esta aplicación es consciente del directorio y fue diseñado toowork con Windows Server AD. aplicación Hello usa LDAP (Protocolo ligero de acceso a directorios) tooread/atributos de la información acerca de los usuarios de Active Directory. aplicación Hello no modificar atributos o en caso contrario, escribir toohello directory. Contoso desea que toomigrate esta tooAzure aplicación Servicios de infraestructura y retirar hardware local Hola antigüedad que hospeda actualmente esta aplicación. aplicación Hello no puede ser toouse ha vuelto a escribir moderna directorio API como Hola basado en REST API de Azure AD Graph. Por lo tanto, una opción de elevación y MAYÚS se desea que la aplicación hello puede ser toorun migrado en la nube de hello, sin modificar el código o volver a escribir aplicación Hola.

**Notas de implementación**

Considere la posibilidad de hello siguientes puntos son importantes para este escenario de implementación:

* Asegúrese de que la aplicación hello no es necesario toohello toomodify/escribir datos de directorio. No se admite dominios de toomanaged de acceso de escritura LDAP proporcionadas por servicios de dominio de Active Directory de Azure.
* Asegúrese de que la aplicación hello no es necesario un esquema de Active Directory/ampliado personalizado. No se admiten extensiones de esquema en los Servicios de dominio de Azure AD.

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>Migrar una tooAzure de aplicación local demonio o del servicio servicios de infraestructura
Algunas aplicaciones constan de varios niveles, donde uno de los niveles de hello necesita capa de tooperform llamadas autenticadas tooa back-end como un nivel de base de datos. Las cuentas de servicio de Active Directory se utilizan normalmente para estos casos de uso. Es posible elevación y MAYÚS tales aplicaciones tooAzure servicios de infraestructura y usar servicios de dominio de Azure AD para necesidades de identidad de Hola de estas aplicaciones. Puede elegir toouse Hola la misma cuenta de servicio que se sincroniza desde su tooAzure de directorio local AD. Como alternativa, puede crear una OU personalizada y, a continuación, cree una cuenta de servicio independiente en esa unidad organizativa, toodeploy dichas aplicaciones.

![Cuenta de servicio mediante WIA](./media/active-directory-domain-services-scenarios/wia-service-account.png)

Contoso tiene una aplicación de almacén de software personalizada que incluye un front-end web, un servidor SQL y un servidor FTP de back-end. Autenticación integrada de Windows de las cuentas de servicio es servidor toohello FTP de tooauthenticate usado hello web front-end. toorun front-end de Hello web se configura como una cuenta de servicio. Hello servidor back-end está configurado tooauthorize acceso de cuenta de servicio de Hola para front-end de hello web. Contoso prefiere no toohave toodeploy una máquina virtual de controlador de dominio en hello en la nube toomove esta tooAzure servicios de infraestructura de aplicación. Del Contoso Administrador de TI puede implementar servidores de hello hospedaje front-end de hello web, SQL server y máquinas virtuales de hello FTP server tooAzure. Estos equipos son tooan unido a servicios de dominio de Azure AD administra el dominio. A continuación, puede usar Hola la misma cuenta de servicio en su directorio local para la autenticación de la aplicación hello. Esta cuenta de servicio es dominio administrado de los servicios de dominio de AD de Azure toohello sincronizados y está disponible para su uso.

**Notas de implementación**

Considere la posibilidad de hello siguientes puntos son importantes para este escenario de implementación:

* Asegúrese de que la aplicación hello usa nombre de usuario/contraseña para la autenticación. Los Servicios de dominio de Azure AD no admiten la autenticación basada en certificado o tarjeta inteligente.
* No se puede cambiar las contraseñas directamente en el dominio administrado Hola. Los usuarios finales pueden cambiar su contraseña o mediante el mecanismo de cambio de contraseña de autoservicio de Azure AD o con respecto al directorio local de Hola. Estos cambios son sincronizados automáticamente y estén disponibles en el dominio administrado Hola.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Implementaciones de Servicios de Escritorio Remoto de Windows Server en Azure
Puede usar los servicios de dominio de Azure AD tooprovide administrado AD tooyour implementados en Azure los servidores de escritorio remoto de servicios de dominio.

Para obtener más información acerca de este escenario de implementación, vea cómo demasiado[integrar servicios de dominio de AD de Azure con su implementación de RDS](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).
