---
title: aaaFAQs - servicios de dominio de Active Directory de Azure | Documentos de Microsoft
description: "Preguntas más frecuentes sobre Servicios de dominio de Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services: Preguntas más frecuentes (P+F)
Esta página responde a las preguntas más frecuentes sobre Hola servicios de dominio de Active Directory de Azure. Siga comprobando si hay actualizaciones.

### <a name="troubleshooting-guide"></a>Guía de solución de problemas
Consulte tooour [Guía de solución de problemas](active-directory-ds-troubleshooting.md) para problemas de toocommon de soluciones que producen cuando configuración o administración de servicios de dominio de Active Directory de Azure.

### <a name="configuration"></a>Configuración
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>¿Se pueden crear varios dominios para un único directorio de Azure AD?
No. Solo se puede crear un único dominio atendido por Servicios de dominio de Azure AD para un único directorio de Azure AD.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>¿Puedo habilitar Azure AD Domain Services en una red virtual de Azure Resource Manager?
No. Azure AD Domain Services solo se puede habilitar en una red virtual de Azure clásica. Puede conectar Hola clásico red virtual tooa el Administrador de recursos red virtual uso toouse de emparejamiento de red virtual de un dominio administrado en una red virtual del Administrador de recursos.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>¿Puedo habilitar Azure AD Domain Services en un directorio de Azure AD federado? Usar los usuarios de tooauthenticate ADFS para acceso tooOffice 365. ¿Puedo habilitar Azure AD Domain Services para este directorio?
No. Servicios de dominio de AD de Azure necesitan obtener acceso a toohello hashes de contraseña de cuentas de usuario, los usuarios de tooauthenticate a través de NTLM o Kerberos. En un directorio federado, hash de contraseña no se almacenan en el directorio de Azure AD de Hola. Por tanto, Azure AD Domain Services no funciona con estos directorios de Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>¿Puedo hacer que Azure AD Domain Services esté disponible en varias redes virtuales dentro de mi suscripción?
el propio servicio Hello no admite directamente en este escenario. Azure AD Domain Services está disponible solo en una red virtual en cada momento. Sin embargo, puede configurar la conectividad entre varias redes virtuales tooexpose servicios de dominio de AD de Azure tooother redes virtuales. Este artículo describe cómo puede [conectar redes virtuales en Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>¿Puedo habilitar Servicios de dominio de Azure AD mediante PowerShell?
PowerShell y la implementación automatizada de Servicios de dominio de Azure AD no están disponible actualmente.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>¿Está disponible en el nuevo portal de Azure Hola servicios de dominio de AD de Azure?
No. Se puede configurar los servicios de dominio de Azure AD solo en hello [portal de Azure clásico](https://manage.windowsazure.com). Se espera que la compatibilidad de tooextend para hello [portal de Azure](https://portal.azure.com) Hola futuras.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>¿Puedo agregar dominio administrado de dominio controladores tooan servicios de dominio de AD de Azure?
No. dominio de Hello proporcionado por servicios de dominio de Active Directory de Azure es un dominio administrado. No es necesario tooprovision, configurar o administrar controladores de dominio para este dominio: las actividades se proporcionan como un servicio de Microsoft de administración. Por lo tanto, no se puede agregar controladores de dominio adicionales (lectura y escritura o de sólo lectura) para el dominio administrado Hola.

### <a name="administration-and-operations"></a>Administración y operaciones
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>¿Se puede conectar el controlador de dominio de toohello para mi dominio administrado mediante Escritorio remoto?
No. No tiene permisos tooconnect toodomain controladores Hola administrados a través de escritorio remoto. Los miembros del grupo de 'Administradores de controlador de dominio de AAD' hello pueden administrar Hola dominio administrado mediante herramientas de administración de AD como Hola centro de administración de Active Directory (ADAC) o AD PowerShell. Estas herramientas se instalan con hello 'herramientas de administración remota' característica en un servidor de Windows Unidos a un dominio administrado toohello.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>He habilitado Servicios de dominio de Azure AD ¿Qué cuenta de usuario debe usarse la toodomain unirse al dominio de toothis de máquinas?
Los miembros del grupo administrativo de hello 'Administradores de controlador de dominio de AAD' pueden máquinas de unión a dominio. Además, los miembros de este grupo tienen toomachines de acceso al escritorio remoto que se han toohello Unidos a un dominio.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>¿Tengo privilegios de administrador de dominio para el dominio administrado Hola proporcionada por servicios de dominio de Azure AD?
No. No se le conceden privilegios de administrador en el dominio administrado Hola. Privilegios de administrador del dominio y ' Enterprise Administrator' no están disponibles para toouse dentro del dominio de Hola. Administrador de dominio existente o grupos de administradores de empresa dentro de su directorio Azure AD también no se conceden privilegios de administrador de dominio/enterprise en el dominio de Hola.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>¿Puedo modificar pertenencias a grupos mediante LDAP u otras herramientas administrativas de AD en dominios administrados?
No. Las pertenencias a grupos en dominios ofrecidos por Servicios de dominio de Azure AD no se pueden modificar. Hola que mismo se aplica a atributos de usuario. Sin embargo, puede cambiar las pertenencias a grupos o los atributos de usuario en Azure AD o en el dominio local. Estos cambios son servicios de dominio de tooAzure sincronizan automáticamente AD.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>¿Durante cuánto tiempo tardan los cambios se que toomy AD de Azure directory toobe visible en mi dominio administrado?
Los cambios realizados en su directorio de Azure AD con hello UI de Azure AD o PowerShell son dominio administrado tooyour sincronizados. Este proceso de sincronización se ejecuta en segundo plano de Hola. Una vez completada la sincronización inicial única Hola de su directorio, se tarda aproximadamente 20 minutos para que los cambios realizados en Azure AD toobe refleja normalmente en el dominio administrado.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>¿Puedo extender el esquema de Hola de dominio administrados Hola proporcionado por servicios de dominio de Active Directory de Azure?
No. esquema de Hola se administra por Microsoft para el dominio administrado Hola. No se admiten extensiones de esquema en los Servicios de dominio de Azure AD.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>¿Puedo modificar o agregar registros DNS en mi dominio administrado?
Sí. Los miembros del grupo de hello 'AAD DC administradores' se les conceden privilegios de administrador de DNS de '', toomodify registros DNS en el dominio administrado Hola. Puede usar la consola de administrador de DNS de hello en un equipo está ejecutando Windows Server toohello Unidos a un dominio administrado, toomanage DNS. Hola toouse consola de administrador de DNS, instale 'Herramientas del servidor DNS', que forma parte de la característica opcional de hello 'Herramientas de administración de servidor remoto' en el servidor de Hola. Hay más información sobre [utilidades para administrar, supervisar y solucionar problemas de DNS](https://technet.microsoft.com/library/cc753579.aspx) disponible en TechNet.

### <a name="billing-and-availability"></a>Facturación y disponibilidad
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>¿Azure AD Domain Services es un servicio de pago?
Sí. Para obtener más información, vea hello [página de precios](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>¿Hay una prueba gratuita para el servicio de hello?
Este servicio se incluye en la versión de prueba gratuita de Hola para Azure. Puede suscribirse a un [mes de evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>¿Puedo obtener Servicios de dominio de Azure AD como parte de Enterprise Mobility Suite (EMS)? ¿Necesito servicios de dominio de Azure AD Premium toouse Azure AD?
No. No, Azure AD Domain Services es un servicio de pago por uso de Azure y no forma parte de EMS. Azure AD Domain Services puede utilizarse con todas las ediciones de Azure AD (Gratis, Básico y Premium). Se le facturará por cada hora en función del uso.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>¿Qué regiones de Azure está disponible en la servicio Hola?
Consulte toohello [servicios de Azure por región](https://azure.microsoft.com/regions/#services/) Hola de página toosee una lista de regiones de Azure en servicios de dominio de Azure AD está disponible.
