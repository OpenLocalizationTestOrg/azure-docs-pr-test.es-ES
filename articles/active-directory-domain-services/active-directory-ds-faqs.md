---
title: "Preguntas más frecuentes - Azure Active Directory Domain Services | Microsoft Docs"
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
ms.openlocfilehash: 7f3212350b1158cd51a34ee1b20a456a73d41672
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services: Preguntas más frecuentes (P+F)
Esta página responde a las preguntas más frecuentes acerca de Azure Active Directory Domain Services. Siga comprobando si hay actualizaciones.

### <a name="troubleshooting-guide"></a>Guía de solución de problemas
Consulte nuestra [Guía de solución de problemas](active-directory-ds-troubleshooting.md) para obtener soluciones para los problemas habituales detectados al configurar o administrar los Servicios de dominio de Azure AD.

### <a name="configuration"></a>Configuración
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>¿Se pueden crear varios dominios para un único directorio de Azure AD?
No. Solo se puede crear un único dominio atendido por Servicios de dominio de Azure AD para un único directorio de Azure AD.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>¿Puedo habilitar Azure AD Domain Services en una red virtual de Azure Resource Manager?
No. Azure AD Domain Services solo se puede habilitar en una red virtual de Azure clásica. Puede conectar la red virtual clásica a una red virtual de Resource Manager mediante el emparejamiento de redes virtuales para usar su dominio administrado en una red virtual de Resource Manager.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-to-authenticate-users-for-access-to-office-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>¿Puedo habilitar Azure AD Domain Services en un directorio de Azure AD federado? Uso ADFS para autenticar a los usuarios para tener acceso a Office 365. ¿Puedo habilitar Azure AD Domain Services para este directorio?
Nº Azure AD Domain Services necesita acceso a los hashes de contraseña de las cuentas de usuario para autenticar a los usuarios a través de NTLM o Kerberos. En un directorio federado, los hashes de contraseña no se almacenan en el directorio de Azure AD. Por tanto, Azure AD Domain Services no funciona con estos directorios de Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>¿Puedo hacer que Azure AD Domain Services esté disponible en varias redes virtuales dentro de mi suscripción?
El propio servicio no admite directamente este escenario. Azure AD Domain Services está disponible solo en una red virtual en cada momento. Sin embargo, puede configurar la conectividad entre varias redes virtuales con el fin de exponer Azure AD Domain Services a otras redes virtuales. Este artículo describe cómo puede [conectar redes virtuales en Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>¿Puedo habilitar Servicios de dominio de Azure AD mediante PowerShell?
PowerShell y la implementación automatizada de Servicios de dominio de Azure AD no están disponible actualmente.

#### <a name="is-azure-ad-domain-services-available-in-the-new-azure-portal"></a>¿Está Servicios de dominio de Azure AD disponible en el nuevo portal de Azure?
No. Los Servicios de dominio de Azure AD solo se pueden configurar en el [Portal de Azure clásico](https://manage.windowsazure.com). Tenemos previsto ampliar la compatibilidad para el [Portal de Azure](https://portal.azure.com) en el futuro.

#### <a name="can-i-add-domain-controllers-to-an-azure-ad-domain-services-managed-domain"></a>¿Puedo agregar controladores de dominio a un dominio administrado de Servicios de dominio de Azure AD?
No. El dominio de Servicios de dominio de Azure AD es un dominio administrado. No es necesario aprovisionar, configurar o administrar controladores de dominio para este dominio, Microsoft proporciona estas actividades de administración como un servicio. Por lo tanto, no podrá agregar controladores de dominio adicionales (ni de lectura y escritura ni de solo lectura) para el dominio administrado.

### <a name="administration-and-operations"></a>Administración y operaciones
#### <a name="can-i-connect-to-the-domain-controller-for-my-managed-domain-using-remote-desktop"></a>¿Puedo conectarme al controlador de dominio para mi dominio administrado mediante Escritorio remoto?
No. Los administradores de inquilinos no tienen privilegios para conectarse a controladores de dominio en el dominio administrado mediante el Escritorio remoto. Los miembros del grupo "Administradores de controlador de dominio de AAD" pueden administrar el dominio administrado usando las herramientas de administración de AD, como el Centro de administración de Active Directory (ADAC) o AD PowerShell. Estas herramientas se instalan mediante la característica "Herramientas de administración de servidor remoto" en un servidor de Windows unido al dominio administrado.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-to-domain-join-machines-to-this-domain"></a>He habilitado Servicios de dominio de Azure AD ¿Qué cuenta de usuario utilizo para unir máquinas a este dominio?
Los miembros del grupo administrativo "Administradores de controlador de dominio de AAD" pueden unir máquinas mediante dominio. Además, los miembros de este grupo se les concede acceso mediante Escritorio remoto a las máquinas que se han unido al dominio.

#### <a name="do-i-have-domain-administrator-privileges-for-the-managed-domain-provided-by-azure-ad-domain-services"></a>¿Puedo tener privilegios de administrador de dominio para el dominio administrado proporcionado por Azure AD Domain Services?
No. No se le conceden privilegios administrativos en el dominio administrado. Los privilegios "Administrador de dominio" y "Administrador de organización" no estarán disponibles dentro del dominio. A los grupos de administradores de dominio o administradores de organización existentes dentro del directorio de Azure AD tampoco se les concederá privilegios de administrador de dominio o de organización en el dominio.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>¿Puedo modificar pertenencias a grupos mediante LDAP u otras herramientas administrativas de AD en dominios administrados?
No. Las pertenencias a grupos en dominios ofrecidos por Servicios de dominio de Azure AD no se pueden modificar. Lo mismo se aplica para los atributos de usuario. Sin embargo, puede cambiar las pertenencias a grupos o los atributos de usuario en Azure AD o en el dominio local. Dichos cambios se sincronizarán automáticamente con Azure AD Domain Services.

#### <a name="how-long-does-it-take-for-changes-i-make-to-my-azure-ad-directory-to-be-visible-in-my-managed-domain"></a>¿Cuánto tardan los cambios realizados en el directorio de Azure AD en estar visibles en mi dominio administrado?
Los cambios realizados en su directorio de Azure AD mediante la interfaz de usuario de Azure AD o PowerShell se sincronizan con el dominio administrado. Este proceso de sincronización se ejecuta en segundo plano. Una vez completada la sincronización inicial de su directorio, suelen transcurrir unos 20 minutos hasta que los cambios realizados en Azure AD se reflejan en el dominio administrado.

#### <a name="can-i-extend-the-schema-of-the-managed-domain-provided-by-azure-ad-domain-services"></a>¿Puedo extender el esquema del dominio administrado por Azure AD Domain Services?
No. Microsoft administra el esquema del dominio administrado. No se admiten extensiones de esquema en los Servicios de dominio de Azure AD.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>¿Puedo modificar o agregar registros DNS en mi dominio administrado?
Sí. Los miembros del grupo "Administradores de controlador de dominio de AAD" reciben privilegios de "Administrador de DNS" con el fin de modificar los registros DNS en el dominio administrado. Pueden utilizar la consola de administrador de DNS en un equipo que ejecuta Windows Server unido al dominio administrado para administrar DNS. A fin de utilizar la consola de administrador de DNS, instale "Herramientas del servidor DNS", que forma parte de la característica opcional "Herramientas de administración remota del servidor" en el servidor. Hay más información sobre [utilidades para administrar, supervisar y solucionar problemas de DNS](https://technet.microsoft.com/library/cc753579.aspx) disponible en TechNet.

### <a name="billing-and-availability"></a>Facturación y disponibilidad
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>¿Azure AD Domain Services es un servicio de pago?
Sí. Consulte la [página de precios](https://azure.microsoft.com/pricing/details/active-directory-ds/)para obtener más información.

#### <a name="is-there-a-free-trial-for-the-service"></a>¿Hay una versión de prueba gratuita para el servicio?
Este servicio se incluye en evaluación gratuita de Azure. Puede suscribirse a un [mes de evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-to-use-azure-ad-domain-services"></a>¿Puedo obtener Servicios de dominio de Azure AD como parte de Enterprise Mobility Suite (EMS)? ¿Necesito Azure AD Premium para usar Azure AD Domain Services?
No. No, Azure AD Domain Services es un servicio de pago por uso de Azure y no forma parte de EMS. Azure AD Domain Services puede utilizarse con todas las ediciones de Azure AD (Gratis, Básico y Premium). Se le facturará por cada hora en función del uso.

#### <a name="what-azure-regions-is-the-service-available-in"></a>¿En qué regiones de Azure está disponible el servicio?
Consulte la página de [servicios de Azure por región](https://azure.microsoft.com/regions/#services/) para saber en qué regiones de Azure está disponible Azure AD Domain Services.
