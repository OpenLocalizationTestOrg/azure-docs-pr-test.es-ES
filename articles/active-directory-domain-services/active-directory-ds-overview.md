---
title: aaaOverview de servicios de dominio de Active Directory de Azure | Documentos de Microsoft
description: "Información general de Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="overview"></a>Información general
Servicios de infraestructura de Azure permiten toodeploy una amplia gama de las soluciones de informática de una manera ágil. Con máquinas de virtuales de Azure, puede implementar casi al instante y deberá pagar solo por minuto de Hola. Con el soporte técnico para Windows, Linux, SQL Server, Oracle, IBM, SAP y BizTalk, puede implementar cualquier carga de trabajo y cualquier lenguaje en casi cualquier sistema operativo. Estas ventajas permiten toomigrate aplicaciones heredadas implementadas local tooAzure, toosave en gastos operativos.

Un aspecto clave de migración local tooAzure aplicaciones lleva a cabo las necesidades de identidad de Hola de estas aplicaciones. Aplicaciones basadas en el directorio pueden basadas en LDAP para acceso de lectura o escritura directory corporativo toohello o se basan en los usuarios finales de tooauthenticate de autenticación integrada de Windows (autenticación de Kerberos o NTLM). Las aplicaciones de línea de negocio (LOB) que se ejecutan en Windows Server se implementan normalmente en máquinas unidas a un dominio, de modo que se pueden administrar de forma segura mediante la directiva de grupo. desplazamiento de too'lift' en la nube local aplicaciones toohello, estas dependencias en la infraestructura de identidad corporativa Hola necesitan toobe resuelto.

Los administradores a menudo activar tooone de hello siguiendo las necesidades de identidad hello toosatisfy soluciones sus aplicaciones implementadas en Azure:

* Implementar una conexión de VPN de sitio a sitio entre las cargas de trabajo que se ejecuta en servicios de infraestructura de Azure y Hola directory corporativo local.
* Ampliar la infraestructura de dominio o un bosque de AD corporativo hello mediante la configuración de controladores de dominio de réplica mediante máquinas virtuales de Azure.
* Implemente un dominio independiente en Azure mediante controladores de dominio implementados como máquinas virtuales de Azure.

Todos estos enfoques presentan costo elevado y sobrecarga administrativa. Los administradores son toodeploy requiere controladores de dominio con máquinas virtuales en Azure. Además, necesitan toomanage, seguro, patch, monitor, copia de seguridad y solucionar problemas de estas máquinas virtuales. dependencia de Hola de toohello de las conexiones de VPN local directorio hace que las cargas de trabajo implementadas en problemas de red de Azure toobe tootransient vulnerable o las interrupciones. Estas interrupciones de red, a su vez, dan lugar a un bajo tiempo de actividad y a una menor confianza en estas aplicaciones.

Hemos diseñado tooprovide una alternativa más sencilla de servicios de dominio de AD de Azure.

## <a name="introducing-azure-ad-domain-services"></a>Presentación de los Servicios de dominio de Azure AD
Azure AD Domain Services proporciona servicios de dominio administrados como, por ejemplo, unión a un dominio, directiva de grupo, LDAP o autenticación Kerberos/NTLM, que son totalmente compatibles con Windows Server Active Directory. Puede utilizar estos servicios de dominio sin necesidad de Hola para toodeploy, administrar y revisión controladores de dominio en la nube de Hola. Servicios de dominio de AD de Azure se integra con el inquilino de Azure AD existente, haciendo posible que los usuarios toolog en con sus credenciales corporativas. Además, puede usar los grupos existentes y tooresources de acceso de toosecure de cuentas de usuario, lo que garantiza más suave 'elevación-y-trasladar' local recursos tooAzure servicios de infraestructura.

La funcionalidad de Azure AD Domain Services funciona perfectamente con independencia de si el inquilino de Azure AD es solo de nube o se sincroniza con su entorno de Active Directory local.

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>Servicios de dominio de Azure AD para las organizaciones solo de nube
Un anuncio de Azure solo en la nube de inquilinos (lo que se conoce a menudo tooas ' administrado inquilinos') no tiene ninguna superficie de identidad local. En otras palabras, las cuentas de usuario, sus contraseñas y las pertenencias a grupos son todos los toohello nativo en la nube: es decir, se crean y administran en Azure AD. Considere por un momento que Contoso es un inquilino de Azure AD solo de nube. Como se muestra en hello siguiente ilustración, el Administrador de Contoso ha configurado una red virtual en los servicios de infraestructura de Azure. Las aplicaciones y las cargas de trabajo de servidor se implementan en esta red virtual en máquinas virtuales de Azure. Puesto que Contoso es un inquilino solo de nube, todas las identidades de usuario, sus credenciales y pertenencias a grupos se crean y administran en Azure AD.

![Información general de los Servicios de dominio de Azure AD](./media/active-directory-domain-services-overview/aadds-overview.png)

Del Contoso Administrador de TI puede habilitar los servicios de dominio de Active Directory de Azure para su inquilino de Azure AD y elegir toomake disponibles en esta red virtual de servicios de dominio. Por lo tanto, los servicios de dominio de Azure AD aprovisiona un dominio administrado y hace que esté disponible en la red virtual de Hola. Todas las cuentas de usuario, pertenencias a grupos y credenciales de usuario disponibles en el inquilino de Azure AD de Contoso también están disponibles en este dominio recién creado. Esta característica permite a los usuarios en hello toosign de organización en el dominio toohello con sus credenciales corporativas - por ejemplo, al conectarse de forma remota toodomain-equipos unidos a un a través de escritorio remoto. Los administradores pueden aprovisionar tooresources de acceso de dominio de hello mediante la pertenencia a grupos existente. Las aplicaciones implementadas en máquinas virtuales de red virtual de hello pueden usar características como la unión a un dominio, lectura LDAP, enlace LDAP, la autenticación NTLM y Kerberos y directiva de grupo.

Algunos aspectos importantes de dominio administrados Hola aprovisionado por servicios de dominio de AD de Azure son los siguientes:

* Del Contoso Administrador de TI no es necesario toomanage, aplicar la revisión, o el monitor de este dominio o los controladores de dominio para este dominio administrado.
* No hay necesidad de toomanage AD replicación para este dominio. Las cuentas de usuario, las pertenencias a grupos y las credenciales del inquilino de Azure AD de Contoso están disponibles automáticamente dentro de este dominio administrado.
* Porque dominio hello es administrada por el dominio de servicios de Azure AD, Contoso Administrador de TI no tiene privilegios de administrador de dominio o administrador de empresa en este dominio.

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>Servicios de dominio de Azure AD para organizaciones híbridas
Las organizaciones con una infraestructura de TI híbrida consumen una combinación de recursos de nube y locales. Estas organizaciones sincronización información de identidad de su inquilino de Azure AD de tootheir de directorio local. Como de las organizaciones híbrida buscan toomigrate más de su local aplicaciones toohello en la nube, especialmente directorio compatible con las aplicaciones heredadas, servicios de dominio de AD de Azure pueden ser útil toothem.

Ha implementado Corporation Litware [Azure AD Connect](../active-directory/active-directory-aadconnect.md), información de identidad de toosynchronize de su inquilino de tootheir Azure AD del directorio local. información de identidad de Hola que se sincroniza incluye cuentas de usuario, los valores de hash de credenciales para la autenticación (sincronización de contraseñas) y las pertenencias a grupos.

> [!NOTE]
> **Sincronización de contraseña es obligatoria para híbrida organizaciones toouse servicios de dominio de Azure AD**. Este requisito es porque se necesitan credenciales de los usuarios en hello administrado dominio proporcionada por servicios de dominio de Active Directory de Azure, tooauthenticate estos usuarios a través de métodos de autenticación NTLM o Kerberos.
>
>

![Servicios de dominio de Azure AD para Litware Corporation](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

Hello en la ilustración anterior se muestra cómo las organizaciones con una infraestructura de TI, como Litware Corporation, híbrida pueden usar servicios de dominio de AD de Azure. Las aplicaciones y cargas de trabajo de servidor de Litware que requieren servicios de dominio, se implementan en una red virtual en los Servicios de infraestructura de Azure. Del Litware Administrador de TI puede habilitar los servicios de dominio de Active Directory de Azure para su inquilino de Azure AD y elegir toomake un dominio administrado disponible en esta red virtual. Puesto que Litware es una organización con una infraestructura de TI híbrida, credenciales, grupos y cuentas de usuario son inquilino sincronizada tootheir Azure AD desde su directorio local. Esta característica permite a los usuarios toosign en el dominio toohello con sus credenciales corporativas, por ejemplo, cuando se conecta de forma remota toomachines Unidos a un dominio de toohello a través de escritorio remoto. Los administradores pueden aprovisionar tooresources de acceso de dominio de hello mediante la pertenencia a grupos existente. Las aplicaciones implementadas en máquinas virtuales de red virtual de hello pueden usar características como la unión a un dominio, lectura LDAP, enlace LDAP, la autenticación NTLM y Kerberos y directiva de grupo.

Algunos aspectos importantes de dominio administrados Hola aprovisionado por servicios de dominio de AD de Azure son los siguientes:

* Hola administrado dominio es un dominio independiente. No es una extensión del dominio local de Litware.
* Del Litware Administrador de TI no necesita toomanage, patch o controladores de dominio de monitor para este dominio administrado.
* No hay ningún dominio de toothis de replicación de AD toomanage necesidad. Las cuentas de usuario, las pertenencias a grupos y las credenciales de directorio local de Litware están sincronizado tooAzure AD a través de Azure AD Connect. Estas cuentas de usuario, las pertenencias a grupos y las credenciales están automáticamente disponibles en dominio administrado Hola.
* Puesto que el dominio Hola está administrado por dominio servicios de Azure AD, Litware Administrador de TI no tiene privilegios de administrador de dominio o administrador de empresa en este dominio.

## <a name="benefits"></a>Ventajas
Con los servicios de dominio de Azure AD, pueda disfrutar Hola siguientes ventajas:

* **Simple** : puede satisfacer las necesidades de identidad de Hola de máquinas virtuales implementan tooAzure servicios de infraestructura con unos pocos pasos sencillos. No necesita toodeploy y administrar la infraestructura de identidad en Azure o el programa de instalación conectividad tooyour atrás identidad infraestructura local.
* **Integración** : los Servicios de dominio de Azure AD están profundamente integrados con su inquilino de Azure AD. Ahora puede usar Azure AD como un directorio de empresa integrada en la nube que se encarga de toohello las necesidades de sus aplicaciones modernas y las aplicaciones tradicionales basadas en el directorio.
* **Compatible** – servicios de dominio de Azure AD se basa en la infraestructura de grado empresarial comprobada de Hola de Active Directory de Windows Server. Por tanto, las aplicaciones pueden depender de un mayor grado de compatibilidad con características de Windows Server Active Directory. No todas las características disponibles en Windows Server AD están actualmente disponibles en Azure AD Domain Services. Sin embargo, las características disponibles son compatibles con características de Windows Server AD correspondientes Hola que dependen de su infraestructura local. Hello LDAP, Kerberos, NTLM, directiva de grupo y dominio capacidades de combinación constituyen una oferta consolidada que se ha probado y se perfeccionan a través de varias versiones de Windows Server.
* **Rentable** : con servicios de dominio de Azure AD, puede evitar la carga de infraestructura y administración de Hola que está asociado con la administración de identidad infraestructura toosupport directorio compatible con las aplicaciones tradicionales. Puede mover estos servicios de infraestructura de aplicaciones tooAzure y beneficiarse de un mayor ahorro en gastos operativos.
