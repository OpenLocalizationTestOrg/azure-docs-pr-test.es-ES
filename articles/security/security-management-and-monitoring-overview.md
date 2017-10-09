---
title: "aaaAzure Introducción a supervisión y administración de seguridad | Documentos de Microsoft"
description: " Azure proporciona tooaid de mecanismos de seguridad en administración de Hola y supervisión de servicios de nube de Azure y máquinas virtuales.  En este artículo se proporciona información general sobre estas características y servicios básicos de seguridad. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Información general sobre la administración y la supervisión de la seguridad en Azure
Azure proporciona tooaid de mecanismos de seguridad en administración de Hola y supervisión de servicios de nube de Azure y máquinas virtuales. En este artículo se proporciona información general sobre estas características y servicios básicos de seguridad. Se proporcionan vínculos tooarticles que proporcionan detalles de cada uno, por lo que puede obtener más información.

Hola la seguridad de los servicios de nube de Microsoft es una asociación y responsabilidad compartida entre usted y Microsoft. Responsabilidad compartida significa que Microsoft es responsable de hello Microsoft Azure y la seguridad física de sus centros de datos (mediante el uso de protecciones de seguridad como las puertas de entrada de badge bloqueados, barreras y restricciones). Además, Azure proporciona niveles seguros de seguridad de la nube en la capa de software de Hola que satisfaga las necesidades de cumplimiento de sus clientes exigentes, la privacidad y la seguridad de Hola.

Posee los datos y las identidades, Hola responsable de la protección, seguridad de Hola de los recursos locales y seguridad Hola de componentes de la nube en la que tendrá el control. Microsoft le proporciona con toohelp de controles y las capacidades de seguridad protege los datos y aplicaciones. El grado de responsabilidad de la seguridad se basa en tipo de Hola de servicio de nube.

Hola siguiente gráfico resume saldo Hola de responsabilidad de cliente hello y Microsoft.

![Responsabilidad compartida][1]

Para un análisis más profundo sobre la administración de la seguridad, consulte [Administración de la seguridad en Azure](azure-security-management.md).

A continuación, incluimos Hola core características toobe tratado en este artículo:

* Control de acceso basado en roles
* Antimalware
* Multi-Factor Authentication
* ExpressRoute
* Puertas de enlace de red virtual
* Privileged Identity Management
* Protección de identidad
* Centro de seguridad

## <a name="role-based-access-control"></a>Control de acceso basado en roles
El control de acceso basado en roles (RBAC) de Azure permite realizar una administración avanzada del acceso a los recursos de Azure. Usar RBAC, puede conceder a personas solo cantidad de Hola de acceso que necesitan tooperform sus trabajos.  RBAC también puede ayudar a asegurarse de que cuando los usuarios dejan la organización de hello pierde acceso tooresources en la nube de Hola.

Más información:

* [Blog del equipo de Active Directory sobre RBAC](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>Antimalware
Con Azure, puede usar el software antimalware de los proveedores de seguridad principales, como Microsoft, Symantec, Trend Micro, McAfee y Kaspersky toohelp proteger sus máquinas virtuales de archivos malintencionados, adware y otras amenazas.

Microsoft Antimalware ofrece que Hola capacidad tooinstall un agente antimalware para roles PaaS y máquinas virtuales. En función de System Center Endpoint Protection, esta característica proporciona local comprobadas nube de toohello de tecnología de seguridad.

También le ofrecemos la integración profunda para de Trend [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ y [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ productos Hola plataforma Windows Azure. DeepSecurity es una solución antivirus y SecureCloud es una solución de cifrado. DeepSecurity se implementará dentro de máquinas virtuales con un modelo de extensión. Mediante la interfaz de usuario del portal de Hola y PowerShell, puede elegir toouse DeepSecurity dentro de nuevas máquinas virtuales que se active, o las máquinas virtuales existentes que ya estén implementadas.

Symantec End Point Protection (SEP) también se admite en Azure. Mediante la integración de portal, los clientes pueden especificar que se propone toouse SEP dentro de una máquina virtual. SEP puede instalarse en una máquina virtual nueva a través del portal de Azure de Hola o se puede instalar en una máquina virtual existente mediante PowerShell.

Más información:

* [Implementación de soluciones antimalware en máquinas virtuales de Azure](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Microsoft Antimalware para Cloud Services y Virtual Machines de Azure](azure-security-antimalware.md)
* [¿Cómo tooinstall y configurar trendmicro Deep Security como un servicio en una VM de Windows](../virtual-machines/windows/classic/install-trend.md)
* [¿Cómo tooinstall y configurar Symantec Endpoint Protection en una VM de Windows](../virtual-machines/windows/classic/install-symantec.md)
* [New Antimalware Options for Protecting Azure Virtual Machines – McAfee Endpoint Protection](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure la autenticación multifactor (MFA) es un método de autenticación que requiere el uso de Hola de más de un método de comprobación y agrega una segunda capa crítica de inicios de sesión de seguridad toouser y las transacciones. MFA ayuda a proteger acceso toodata y las aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Proporciona autenticación sólida mediante una gran variedad de opciones de verificación, como llamadas telefónicas, mensajes de texto, notificaciones de aplicaciones móviles, códigos de verificación y tokens OATH de terceros.

Más información:

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [¿Qué es Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* [Cómo funciona Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>ExpressRoute
Microsoft Azure ExpressRoute le permite ampliar sus redes locales en hello nube de Microsoft a través de una conexión privada dedicada que se realiza mediante un proveedor de conectividad. Con ExpressRoute, puede establecer conexiones tooMicrosoft servicios en la nube, como Microsoft Azure, Office 365 y CRM Online. La conectividad puede ser desde una red de conectividad universal (IP VPN), una red Ethernet de punto a punto, o una conexión cruzada virtual a través de un proveedor de conectividad en una instalación de ubicación compartida. Las conexiones ExpressRoute no pasan por hello Internet pública. Esto permite toooffer las conexiones de ExpressRoute, más confiabilidad, velocidades más rápidas, latencias más bajas y mayor seguridad que las típicas conexiones a través de Internet de Hola.

Más información:

* [Información técnica de ExpressRoute](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>Puertas de enlace de red virtual
Se usan las puertas de enlace de VPN, también denominado portales de red Virtual de Azure, toosend el tráfico de red entre redes virtuales y las ubicaciones en local. También son toosend usado el tráfico entre varias redes virtuales dentro de Azure (VNet a VNet).  Las puertas de enlace de VPN proporcionan conectividad local segura entre Azure y su infraestructura.

Más información:

* [Información acerca de las puertas de enlace de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Azure Network Security Overview](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
En ocasiones, los usuarios necesitan toocarry operaciones con privilegios en recursos de Azure u otras aplicaciones de SaaS. Esto suele significar que las organizaciones tienen toogive tener acceso ellas con privilegios permanentes en Azure Active Directory (Azure AD). Este hecho representa un riesgo creciente para la seguridad de los recursos hospedados en la nube, ya que las organizaciones no pueden supervisar todo lo que deberían lo que hacen esos usuarios con su acceso con privilegios.
Además, si se pone en peligro la seguridad de una cuenta de usuario que tiene acceso con privilegios, esta situación podría afectar a la seguridad general en la nube. Identity Management de Azure AD privilegios ayuda tooresolve este riesgo reduciendo el tiempo de exposición de Hola de privilegios y aumentar la visibilidad en uso.  

Privileged Identity Management de presenta el concepto de Hola de un administrador temporal para un rol o "justo a tiempo" el acceso de administrador, que es un usuario que necesita toocomplete un proceso de activación para que asigna el rol de. cambios del proceso de activación de Hola Hola asignación de rol de tooa de usuario de hello en Azure AD desde tooactive inactiva, durante un período de tiempo especificado como ocho horas.

Más información:

* [Administración de identidades con privilegios de Azure AD](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Introducción a Privileged Identity Management de Azure AD](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>Protección de identidad
Protección de identidad de Azure Active Directory (AD) proporciona una vista consolidada de las actividades de inicio de sesión sospechosas y posibles toohelp vulnerabilidades proteger su empresa. Identity Protection detecta las actividades sospechosas de usuarios e identidades con privilegios (administrador) según determinadas señales, como ataques por fuerza bruta, pérdida de credenciales, inicios de sesión de ubicaciones desconocidas y dispositivos infectados.

Al proporcionar notificaciones y actualizaciones recomendadas, Identity Protection ayuda a los riesgos toomitigate en tiempo real. Calcula la gravedad del riesgo de usuario y puede configurar el acceso de aplicación de directivas basadas en riesgo tooautomatically ayuda protección frente a amenazas futuras.

Más información:

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD and Identity Show: Identity Protection Preview (Channel 9: Presentación de Azure AD e Identity: versión preliminar de Identity Protection)](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>Security Center
Centro de seguridad de Azure le ayuda a evitar, detectar y responder toothreats y proporciona que mayor visibilidad en y control sobre, seguridad de Hola de los recursos de Azure. Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.

Centro de seguridad le ayuda a optimizar y controlar la seguridad de Hola de los recursos de Azure por:

* Habilitar las directivas de toodefine para los recursos de suscripción de Azure según tooyour seguridad de la empresa necesita y Hola tipo de aplicaciones o importancia de los datos de hello en cada suscripción.
* Supervisión del estado de Hola de máquinas virtuales de Azure, redes y aplicaciones.
* Proporciona una lista de alertas de seguridad, incluidas las alertas del socio integrado investigar soluciones, junto con información de Hola que necesita tooquickly y recomendaciones sobre cómo un nivel de prioridad tooremediate un ataque.

Más información:

* [Introducción tooAzure centro de seguridad](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
