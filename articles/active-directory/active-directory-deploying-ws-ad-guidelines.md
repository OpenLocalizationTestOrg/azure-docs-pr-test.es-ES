---
title: "aaaGuidelines para implementar Windows Server Active Directory en máquinas virtuales de Azure | Documentos de Microsoft"
description: "Si ya sabe cómo los servicios de dominio de AD toodeploy y servicios de federación de AD local, obtenga información acerca de cómo funcionan en máquinas virtuales de Azure."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>Directrices para implementar Windows Server Active Directory en máquinas virtuales de Microsoft Azure
En este artículo se explica Hola diferencias importantes entre implementar Windows Server Active Directory servicios de dominio (AD DS) y los servicios de federación de Active Directory (AD FS) en forma local e implementarlos en máquinas virtuales de Microsoft Azure.

## <a name="scope-and-audience"></a>Ámbito y audiencia
artículo de Hello está destinado a los que ya tienen experiencia con la implementación de Active Directory local. Se ocupa de las diferencias de hello entre implementar Active Directory en redes virtuales de Microsoft Azure o SQL Azure máquinas virtuales y las implementaciones de Active Directory locales tradicionales. Máquinas virtuales de Azure y redes virtuales de Azure forman parte de un infraestructura como-servicio (IaaS) de la oferta para tooleverage de las organizaciones los recursos en nube Hola informáticos.

Para aquellos que no estén familiarizadas con la implementación de AD, vea hello [Guía de implementación de AD DS](https://technet.microsoft.com/library/cc753963) o [planear la implementación de AD FS](https://technet.microsoft.com/library/dn151324.aspx) según corresponda.

En este artículo se da por supuesto que Hola lector está familiarizado con hello siguientes conceptos:

* Implementación y administración de Windows Server AD DS
* Implementación y configuración de infraestructura de toosupport un Windows Server AD DS de DNS
* Implementación y administración de Windows Server AD FS
* Implementación, configuración y administración de aplicaciones de usuarios de confianza (sitios y servicios web) que pueden usar tokens de Windows Server AD FS
* Conceptos generales de máquina virtual, como cómo tooconfigure un virtual automático, virtual discos y las redes virtuales

Este artículo resalta los requisitos de Hola para un escenario de implementación híbrido en el que Windows Server AD DS o AD FS se implementa en parte en local y en parte en máquinas virtuales de Azure. Hola primero se explican las diferencias críticas de hello entre ejecutar Windows Server AD DS y AD FS en máquinas virtuales de Azure y local así como puntos de toma de decisiones importantes que afectan al diseño e implementación. resta de Hola de papel de hello contiene instrucciones para cada uno de los puntos de decisión de hello en más detalle, y cómo tooapply Hola escenarios de implementación de toovarious de instrucciones.

Este artículo describen la configuración de Hola de [Azure Active Directory](http://azure.microsoft.com/services/active-directory/), que es un servicio basado en REST que proporciona capacidades de control de acceso y la administración de identidades para aplicaciones en la nube. Azure Active Directory (Azure AD) y Windows Server AD DS, sin embargo, son toowork diseñada juntos tooprovide una solución de administración de identidades y accesos para híbridos de hoy en día TI entornos y las aplicaciones modernas. toohelp entender las diferencias de Hola y relaciones entre Windows Server AD DS y Azure AD, tenga en cuenta Hola siguiente:

1. Puede ejecutar Windows Server AD DS en la nube de hello en máquinas virtuales de Azure cuando se usa Azure tooextend su centro de datos local en la nube de Hola.
2. Puede usar Azure AD toogive las aplicaciones de single sign-on tooSoftware como-servicio (SaaS) de los usuarios. Por ejemplo, Microsoft Office 365 usa esta tecnología y las aplicaciones que se ejecutan en Azure u otras plataformas en la nube también pueden usarla.
3. Puede usar Azure AD (su servicio de Control de acceso) toolet a los usuarios de inicio de sesión mediante identidades de Facebook, Google, Microsoft y otros tooapplications de proveedores de identidad que se hospedan en la nube de Hola o de forma local.

Para más información sobre estas diferencias, consulte el artículo [Aspectos básicos de la administración de identidades de Azure](fundamentals-identity.md).

## <a name="related-resources"></a>Recursos relacionados
Puede descargar y ejecutar hello [evaluación de preparación de máquina Virtual de Azure](https://www.microsoft.com/download/details.aspx?id=40898). Hello evaluación automáticamente inspeccionará el entorno local y generar un informe personalizado basado en hello guía se encuentra en este tema toohelp migrar Hola entorno tooAzure.

Se recomienda que revise también primero Hola tutoriales, guías y vídeos que cubren Hola temas siguientes:

* [Configurar una red Virtual solo en hello Portal de Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [Configurar una VPN de sitio a sitio en hello Portal de Azure](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Instalación de un bosque nuevo de Active Directory en una red virtual de Azure](active-directory-new-forest-virtual-machine.md)
* [Instalación de un controlador de dominio de Active Directory de réplica en una red virtual de Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS para profesionales de TI: (01) Principios básicos sobre máquinas virtuales](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS para profesionales de TI: (05) Creación de redes virtuales y conectividad entre instalaciones](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>Introducción
Hello requisitos fundamentales para implementar Windows Server Active Directory en máquinas virtuales de Azure difieren muy poco de su implementación en máquinas virtuales en locales (y extensión toosome, máquinas físicas). Por ejemplo, en hello caso de Windows Server AD DS, si los controladores de dominio (DC) de Hola que puede implementar en máquinas virtuales de Azure son réplicas en una existente en local dominio o un bosque corporativo, a continuación, Hola implementación de Azure se puede tratar en gran medida de hello igual que puede tratar cualquier otro sitio adicional de Windows Server Active Directory. Es decir, se deben definir subredes en Windows Server AD DS, un sitio creado, Hola subredes vinculadas toothat sitio y conectado mediante vínculos de sitio adecuados de sitios de tooother. Sin embargo, hay algunas diferencias que son comunes tooall Azure implementaciones y otras que varían en escenario de implementación concreto toohello correspondiente. A continuación se presentan dos diferencias fundamentales:

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>Máquinas virtuales de Azure necesite red corporativa de conectividad toohello local.
Conectar máquinas virtuales de Azure red corporativa requiere la red virtual de Azure, que incluye un sitio a sitio o red privada virtual (VPN) de sitio a punto de local de atrás tooan tooseamlessly capaz de componente conectar máquinas virtuales de Azure y máquinas locales. También puede permitir que este componente de VPN local dominio miembro equipos tooaccess un dominio de Windows Server Active Directory cuyos controladores de dominio se hospedan exclusivamente en máquinas virtuales de Azure. Es importante toonote, sin embargo, que si hello VPN produce un error, la autenticación y otras operaciones que dependen de Active Directory de Windows Server se seguirán produciendo errores. Mientras los usuarios pueden ser capaz de toosign sesión con credenciales almacenadas en caché existentes, todos los peer-to-peer o los intentos de autenticación de cliente a servidor para los vales tienen todavía toobe emitido o estén obsoletos producirán un error.

Vea [red Virtual](http://azure.microsoft.com/documentation/services/virtual-network/) para una demostración en vídeo y una lista de tutoriales paso a paso, incluido [configurar una VPN de sitio a sitio en el portal de Azure hello](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> También puede implementar Windows Server Active Directory en una red virtual de Azure que no tenga conectividad con una red local. instrucciones de Hello en este tema, sin embargo, da por supuesto que se usa una red virtual de Azure porque proporciona capacidades que son esenciales tooWindows servidor de direccionamiento IP.
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>Las direcciones IP estáticas se deben configurar con Azure PowerShell.
Las direcciones dinámicas se asignan de forma predeterminada, pero utilice Hola Set-AzureStaticVNetIP cmdlet tooassign una dirección IP estática en su lugar. Eso permitirá establecer una dirección IP estática que se mantendrá durante la recuperación del servicio y el cierre y reinicio de la máquina virtual. Para más información, consulte [Static internal IP address for virtual machines (Dirección IP estática interna para máquinas virtuales)](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/).

## <a name="BKMK_Glossary"></a>Términos y definiciones
Hola aquí te mostramos una lista no exhaustiva de términos para diversas tecnologías de Azure que se hará referencia en este artículo.

* **Máquinas virtuales de Azure**: Hola oferta de IaaS de Azure que permite a los clientes toodeploy máquinas virtuales que ejecutan casi cualquier tradicionalmente cargas de trabajo de servidor local.
* **Red virtual de Azure**: Hola tootheir propio servicio de Azure que permite a los clientes crear y administrar redes virtuales en Azure y vincularlas de forma segura a redes de infraestructura local de red mediante el uso de una red privada virtual (VPN).
* **Dirección IP virtual**: dirección de una dirección IP a través de internet que se tooa no está enlazado específico equipo o red tarjeta de interfaz. Servicios de nube se les asigna una dirección IP virtual para recibir el tráfico de red que es redireccionado tooan máquina virtual de Azure. Una dirección IP virtual es una propiedad de un servicio en la nube que puede contener una o más máquinas virtuales de Azure. Tenga en cuenta que una red virtual de Azure puede contener uno o más servicios en la nube. Las direcciones IP virtuales proporcionan funcionalidades nativas de equilibrio de carga.
* **Dirección IP dinámica**: es la dirección IP de Hola que es solo interna. Debe configurarse como una dirección IP estática (mediante el uso de hello Set-AzureStaticVNetIP cmdlet) para máquinas virtuales que hospedan los roles de servidor DC/DNS Hola.
* **Recuperación del servicio**: error del proceso de Hola que Azure devuelve automáticamente un tooa de servicio móvil estado nuevo después de detectar que el servicio de Hola. La recuperación del servicio es uno de los aspectos de Hola de Azure que admite disponibilidad y resistencia. Si bien es improbable, resultado de hello después de un incidente de recuperación para un controlador de dominio que se ejecuta en una máquina virtual del servicio es similar reinicio no planeado de tooan, pero tiene algunos efectos secundarios:
  
  * adaptador de red virtual de Hola Hola máquina virtual cambiará
  * dirección MAC del adaptador de red virtual de Hola Hola cambiará
  * Hola Id. de procesador/CPU de hello máquina virtual cambiará
  * Hello configuración IP del adaptador de red virtual de hello no cambiará mientras Hola VM es red virtual tooa adjunto y hello dirección IP de la máquina virtual es estático.
  
  Ninguno de estos comportamientos afecta a Windows Server Active Directory ya no tiene ninguna dependencia de dirección MAC de Hola o identificador de procesador/CPU, y todas las implementaciones de Active Directory de Windows Server en Azure se recomienda toobe ejecutar en una red virtual de Azure, tal y como se ha descrito anteriormente .

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>¿Es seguro toovirtualize controladores de dominio de Active Directory de Windows Server?
Implementación de controladores de dominio de Windows Server Active Directory en máquinas virtuales de Azure está sujeto toohello mismas instrucciones que ejecutan controladores de dominio locales en una máquina virtual. Ejecutar controladores de dominio virtualizados es una práctica segura siempre y cuando se sigan las instrucciones para realizar copias de seguridad y restaurar dichos controladores de dominio. Para más información sobre las restricciones e instrucciones para ejecutar los controladores de dominio virtualizados, consulte [Controladores de dominio en ejecución en Hyper-V](https://technet.microsoft.com/library/dd363553).

Los hipervisores proporcionan o trivializan tecnologías que pueden causar problemas en muchos sistemas distribuidos, incluido Windows Server Active Directory. Por ejemplo, en un servidor físico, puede clonar un disco o usar métodos no admitidos tooroll Hola back-estado de un servidor, incluido el uso de SAN, y así sucesivamente, pero lo hace en un servidor físico es mucho más difícil que restaurar una instantánea de máquina virtual en un hipervisor. Azure ofrece funcionalidad que puede dar lugar a Hola misma condición no deseable. Por ejemplo, no debe copiar archivos VHD de controladores de dominio en lugar de realizar copias de seguridad periódicas porque su restauración puede producir un características de restauración de instantáneas de toousing situación similar.

Esas reversiones presentan burbujas de USN que pueden causar toopermanently divergentes estados entre controladores de dominio. Esto puede provocar problemas como:

* Objetos persistentes
* Contraseñas incoherentes
* Valores de atributo incoherentes
* Si se revierte maestro de esquema de hello discrepancias de esquema

Para más información acerca de cómo afecta esto a los controladores de dominio, consulte [USN y reversión de USN](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback).

A partir de Windows Server 2012, [medidas de seguridad adicionales se generan en tooAD DS](https://technet.microsoft.com/library/hh831734.aspx). Estas medidas de seguridad ayudan a proteger los controladores de dominio virtualizado frente a problemas de hello mencionado anteriormente, como plataforma de hipervisor de hello subyacente admita VM-GenerationID. Azure admite VM-GenerationID, lo que significa que los controladores de dominio que ejecutan Windows Server 2012 o posterior en Azure máquinas virtuales tienen medidas de seguridad adicionales de Hola.

> [!NOTE]
> Debe apagar y reiniciar una máquina virtual que se ejecuta función de controlador de dominio de hello en Azure en hello sistema operativo en lugar de usar hello **apagar** opción Hola PuertoA Azure. Hoy en día, utilizando hello tooshut portal hacia abajo una máquina virtual hace Hola VM toobe desasignado. Una máquina virtual desasignada tiene la ventaja de Hola de no incurre en cargos, pero también restablece Hola VM-GenerationID, lo que resulta deseable para un controlador de dominio. Cuando se restablece el VM-GenerationID hello, también se restablece el invocationID Hola de base de datos de hello AD DS, se descarta Hola grupo RID y SYSVOL se marca como no autoritativo. Para obtener más información, consulte [Introducción tooActive Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx) y [virtualización segura de DFSR](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx).
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>¿Por qué implementar Windows Server AD DS en Máquinas virtuales de Azure?
Muchos escenarios de implementación de Windows Server AD DS son adecuados para la implementación como máquinas virtuales en Azure. Por ejemplo, suponga que tiene una compañía en Europa que necesita tooauthenticate a los usuarios en una ubicación remota de Asia. Hello empresa no ha implementado anteriormente Windows Server Active Directory controladores de dominio en Asia debido toohello costo toodeploy posimplementación de y a su poca experiencia toomanage Hola servidores. Como resultado, los controladores de dominio en Europa atienden las solicitudes de autenticación de Asia con resultados poco óptimos. En este caso, puede implementar un controlador de dominio en una máquina virtual que ha especificado se debe ejecutar dentro de hello centro de datos de Azure de Asia. Asociar esa red virtual de Azure que está conectado directamente toohello de ubicación remota mejorará el rendimiento de la autenticación de controlador de dominio tooan.

Azure también resulta muy indicado como un sustituto toootherwise ante desastres costosa recovery (recuperación ante desastres) los sitios. Hola relativamente bajo coste de hospedar una pequeña cantidad de controladores de dominio y una única red virtual en Azure representa una alternativa atractiva.

Por último, puede que desee toodeploy una aplicación de red en Azure, como SharePoint, que requiere Windows Server Active Directory, pero no tiene ninguna dependencia en hello local de red o bienvenida de Windows Server Active Directory corporativo. En este caso, la implementación de un bosque aislado en Azure toomeet Hola SharePoint requisitos del servidor es óptimo. Una vez más, también se admite la implementación de aplicaciones de red que requieren conectividad toohello local de red y Hola Active Directory corporativo.

> [!NOTE]
> Puesto que ofrece una conexión layer-3, Hola componente de VPN que proporciona conectividad entre una red virtual de Azure y una red local también puede habilitar a los servidores miembro que se ejecutan los controladores de dominio local tooleverage que se ejecutan como máquinas virtuales de Azure en Azure red virtual. Pero si Hola VPN no está disponible, la comunicación entre equipos locales y los controladores de dominio basados en Azure no funcionará, lo que da lugar a la autenticación y varios otros errores.  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>Diferencias entre implementar controladores de dominio de Windows Server Active Directory en máquinas virtuales de Azure o hacerlo de forma local
* En cualquier escenario de implementación de Windows Server Active Directory que incluya más de una sola máquina virtual, es necesario toouse una red virtual de Azure para la coherencia de las direcciones IP. Tenga en cuenta que en esta guía se supone que los controladores de dominio se ejecutan en una red virtual.
* Al igual que con los controladores de dominio locales, se recomiendan direcciones IP estáticas. Una dirección IP estática solo se puede configurar mediante Azure PowerShell. Para más detalles, consulte [Static internal IP address for VMs (Dirección IP estática interna para máquinas virtuales)](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) . Si tienes sistemas de supervisión u otras soluciones que busque la dirección IP estática dentro de hello sistema operativo, puede asignar Hola mismo IP dirección toohello red adaptador propiedades estáticas de hello máquina virtual. Pero tenga en cuenta que adaptador de red de Hola se descartará si experimenta una recuperación del servicio hello VM o se apaga en el portal de Hola y se cancela su dirección. En ese caso, la dirección IP estática de hello en invitado Hola será necesario toobe restablecer.
* Implementar máquinas virtuales en una red virtual no implica (o requerir) red local de conectividad tooan atrás; red virtual de Hello habilita simplemente esa posibilidad. Debe crear una red virtual para la comunicación privada entre Azure y la red local. Es necesario un punto de conexión VPN en la red local de hello toodeploy. Hola VPN está abierta desde la red de Azure toohello local. Para obtener más información, consulte [información general de red Virtual](../virtual-network/virtual-networks-overview.md) y [configurar una VPN de sitio a sitio en hello Azure Portal](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Una opción demasiado[crear una VPN de punto a sitio](../vpn-gateway/vpn-gateway-point-to-site-create.md) es tooconnect disponible en equipos individuales basados en Windows directamente tooan red virtual de Azure.
> 
> 

* Independientemente de si crea una red virtual o no, Azure cobrará por el tráfico de salida, pero no por el de entrada. Varias opciones de diseño de Windows Server Active Directory pueden influir en cuánto tráfico de salida genera una implementación. Por ejemplo, la implementación de un controlador de dominio de solo lectura (RODC) limita el tráfico de salida ya que no replica datos de salida. Pero la decisión de hello toobe ponderarse con hello necesidad tooperform toodeploy un RODC es necesario escribir operaciones contra Hola DC y Hola [compatibilidad](https://technet.microsoft.com/library/cc755190) que tienen aplicaciones y servicios en el sitio de hello tiene los RODC. Para más información acerca de los gastos por tráfico, consulte [Precios de Azure](http://azure.microsoft.com/pricing/).
* Mientras se tiene un control total sobre qué toouse de recursos de servidor para las máquinas virtuales de forma local, como la RAM, tamaño del disco y así sucesivamente, en Azure debe seleccionar de una lista de tamaños de servidor preconfigurados. Para un controlador de dominio, se necesita un disco de datos en disco de sistema operativo toohello de adición de base de datos de pedido toostore Hola Windows Server Active Directory.

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>¿Se puede implementar Windows Server AD FS en Máquinas virtuales de Azure?
Sí, puede implementar Windows Server AD FS en máquinas virtuales de Azure y Hola [las prácticas recomendadas para la implementación de AD FS](https://technet.microsoft.com/library/dn151324.aspx) local aplica por igual tooAD FS implementación en Azure. Pero algunas prácticas recomendadas de hello como el equilibrio de carga y alta disponibilidad, requieren tecnologías más allá de lo que ofrece AD FS. Debe proporcionar la infraestructura subyacente de Hola. Vamos a revisar algunos de los procedimientos recomendados y a ver cómo pueden lograrse mediante el uso de Máquinas virtuales de Azure y una red virtual de Azure.

1. **Servidores de seguridad (STS) de servicio de token no exponga nunca directamente toohello Internet.**
   
    Esto es importante porque Hola STS emite tokens de seguridad. Como resultado, los servidores de STS como servidores de AD FS deben tratarse con Hola mismo nivel de protección que un controlador de dominio. Si un STS se ve comprometida, los usuarios malintencionados tienen tokens de acceso de tooissue Hola capacidad potencialmente que contiene notificaciones de sus aplicaciones de terceros eligiendo la opción de toorelying y otros servidores STS en las organizaciones de confianza.
2. **Implementar controladores de dominio de Active Directory para todos los dominios de usuario de hello misma red que los servidores de hello AD FS.**
   
    Servidores de AD FS utilizan usuarios tooauthenticate de servicios de dominio de Active Directory. Se recomienda toodeploy controladores de dominio en hello misma red que los servidores de hello AD FS. Esto proporciona continuidad del negocio en caso de hello vínculo entre Hola red de Azure y la red local se interrumpe y permite un mayor rendimiento para los inicios de sesión y una menor latencia.
3. **Implemente varios nodos de AD FS para alta disponibilidad y equilibrio de carga de Hola.**
   
    En la mayoría de los casos, el error de Hola de una aplicación que permite que AD FS es aceptable porque las aplicaciones de Hola que requieren suelen ser tokens de seguridad de misión crítica. Como resultado, y como AD FS ahora reside en hello ruta crítica tooaccessing aplicaciones críticas, servicio de hello AD FS debe tener alta disponibilidad a través de varios servidores proxy de AD FS y servidores de AD FS. distribución de tooachieve de solicitudes, equilibradores de carga se implementan normalmente delante tanto Hola AD FS y servidores proxy de hello AD FS.
4. **Implemente uno o más nodos de proxy de aplicación web para acceder a Internet.**
   
    Cuando los usuarios necesitan aplicaciones tooaccess protegidas por el servicio de hello AD FS, Hola AD FS servicio necesidades toobe disponibles de Hola a internet. Esto se logra mediante la implementación de servicio de Proxy de aplicación Web de Hola. Se recomienda encarecidamente toodeploy más de un nodo para los fines de Hola de alta disponibilidad y equilibrio de carga.
5. **Restringir el acceso de recursos de red de toointernal de nodos de Proxy de aplicación Web de Hola.**
   
    Hola a tooallow usuarios externos tooaccess AD FS desde internet, deberá toodeploy nodos de Proxy de aplicación Web (o Proxy de AD FS en versiones anteriores de Windows Server). Hola proxy de aplicación Web nodos están directamente expuestos toohello Internet. No son necesario toobe Unidos a un dominio y solo necesitan tener acceso a servidores de toohello AD FS a través de los puertos TCP 80 y 443. Se recomienda encarecidamente que tooall de comunicación está bloqueado a otros equipos (especialmente los controladores de dominio).
   
    Este se consigue normalmente de forma local mediante una red perimetral. Los firewalls usan un modo de lista blanca de tráfico de toorestrict de operación de red de hello DMZ toohello local (es decir, solo el tráfico de hello direcciones IP especificadas y over especificado se admite puertos y se bloquea el resto de tráfico).

Hello siguiente diagrama muestra un tradicional implementación de AD FS local.

![Diagrama de una implementación tradicional de servicios de federación de Active Directory de forma local](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

Sin embargo, dado que Azure no proporciona funcionalidad de firewall nativo y completa, toobe utiliza toorestrict tráfico necesario otras opciones. Hello tabla siguiente muestran las opciones y sus ventajas e inconvenientes.

| Opción | Ventaja | Desventaja |
| --- | --- | --- |
| [ACL de red de Azure](../virtual-network/virtual-networks-acl.md) |Configuración inicial menos costosa y más sencilla |Configuración de ACL de red adicional necesario si las nuevas máquinas virtuales se agregan toohello implementación |
| [Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) |Modo de funcionamiento mediante lista blanca y no requiere ninguna configuración de ACL de red |Aumento del costo y la complejidad de la instalación inicial |

Hola pasos de alto nivel toodeploy AD FS en este caso son como sigue:

1. Crear una red virtual con conectividad entre locales, mediante una VPN o mediante [ExpressRoute](http://azure.microsoft.com/services/expressroute/).
2. Implementar controladores de dominio de red virtual de Hola. Este paso es opcional pero recomendable.
3. Implementar servidores de AD FS Unidos a un dominio de red virtual de Hola.
4. Crear un [conjunto con equilibrio de carga interno](http://azure.microsoft.com/blog/internal-load-balancing/) que incluye servidores de AD FS de Hola y utiliza una nueva dirección IP privada dentro de la red virtual de hello (una dirección IP dinámica).
   
   1. Actualizar DNS toocreate Hola FQDN toopoint toohello (dinámica) dirección IP privada del conjunto de carga equilibrada interno Hola.
5. Crear un servicio de nube (o una red virtual independiente) para hello nodos de Proxy de aplicación Web.
6. Implementar nodos de Proxy de aplicación Web de hello en servicio de nube de Hola o red virtual
   
   1. Crear un conjunto de carga equilibrada externo que incluye nodos de Proxy de aplicación Web de Hola.
   2. Actualizar Hola externo DNS (FQDN) del nombre toopoint toohello nube servicio dirección IP pública (dirección IP virtual de hello).
   3. Configurar AD FS proxies toouse Hola FQDN que corresponde el conjunto de carga equilibrada interno toohello para servidores de hello AD FS.
   4. Actualizar sitios web basados en notificaciones toouse Hola FQDN externo para su proveedor de notificaciones.
7. Restringir el acceso entre la máquina de tooany de Proxy de aplicación Web en la red virtual de hello AD FS.

necesidades del conjunto de equilibrio de carga de hello para el equilibrador de carga interno de Azure Hola de tráfico de toorestrict, toobe configurado para sólo tráfico tooTCP los puertos 80 y 443, y se quita todos los otro tráfico toohello dinámica dirección IP interna del conjunto de carga equilibrada de Hola.

![Diagrama de las ACL de red de ADFS con TCP 443 + 80 permitido.](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

Servidores de tráfico toohello AD FS que se le permitiría solo por hello siguientes orígenes:

* equilibrador de carga interno de Azure Hola.
* dirección IP de Hola de un administrador de red local de Hola.

> [!WARNING]
> diseño de Hello debe impedir que los nodos de Proxy de aplicación Web lleguen a todas las ubicaciones en la red local de Hola o cualquier otra VM Hola red virtual de Azure. Que puede realizarse mediante la configuración de reglas de firewall en dispositivo de hello local para las conexiones de Express Route o dispositivo VPN de Hola para las conexiones VPN de sitio a sitio.
> 
> 

Una opción de toothis desventaja es Hola necesidad tooconfigure Hola ACL de red para varios dispositivos, incluidos el equilibrador de carga interno, los servidores de hello AD FS y cualquier otro servidor que se agrega toohello de red virtual. Si cualquier dispositivo se agrega toohello implementación sin configurar tooit de tráfico de red ACL toorestrict, toda la implementación de hello puede estar en peligro. Si alguna vez cambian las direcciones IP de nodos de Proxy de aplicación Web de Hola Hola, deben restablecerse ACL de red de hello (lo que significa que los proxies de hello debe estar configurado toouse [dinámica direcciones IP estáticas](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)).

![ADFS en Azure con ACL de red.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

Otra opción es hello toouse [Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) dispositivo toocontrol el tráfico entre servidores de proxy de AD FS y servidores de hello AD FS. Esta opción cumple con los procedimientos recomendados para la seguridad y alta disponibilidad y requiere menos administración después de la instalación inicial de hello porque Hola Barracuda NG Firewall proporciona un modo de lista blanca de la administración de firewall y se puede instalar directamente en una red virtual de Azure. Así se elimina ACL de red de tooconfigure Hola necesario siempre que se agrega un nuevo servidor toohello implementación. Pero esta opción agrega complejidad y costo a la implementación inicial.

En este caso, se implementan dos redes virtuales en lugar de una. Las llamaremos VNet1 y VNet2. VNet1 contiene a servidores proxy de Hola y VNet2 contiene Hola STS y red corporativa de hello red conexión back-toohello. VNet1 es, por tanto, físicamente (aunque prácticamente) aislada de VNet2 y, a su vez, de la red corporativa de Hola. VNet1, a continuación, tooVNet2 conectado usa una tecnología túnel especial conocida como transporte independiente red arquitectura (TINA). Hola túnel TINA es tooeach adjunto de redes virtuales hello mediante un dispositivo Barracuda NG firewall: un Barracuda en cada una de las redes virtuales Hola.  Para alta disponibilidad, se recomienda que implemente dos Barracudas en cada red virtual; una lista activa, Hola otro pasivo. Ofrecen capacidades de Firewall extremadamente abundantes que nos permiten operación de hello toomimic de una red Perimetral local tradicional en Azure.

![ADFS en Azure con firewall.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

Para obtener más información, consulte [AD FS: Extender un toohello de aplicación front-end local para notificaciones Internet](#BKMK_CloudOnlyFed).

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>Una implementación alternativa tooAD FS si el objetivo de hello es solo Office 365 SSO
No hay otra alternativa toodeploying AD FS completamente si su objetivo es solo tooenable sesión para Office 365. En ese caso, simplemente puede implementar localmente DirSync con sincronización de contraseña en local y lograr Hola mismo resultado final con la complejidad de la implementación mínima, dado que este enfoque no requiere AD FS o Azure.

Hello tabla siguiente compara el funcionamiento de procesos de inicio de sesión de hello con y sin implementar AD FS.

| Inicio de sesión único de Office 365 mediante AD FS y DirSync | Mismo inicio de sesión único de Office 365 mediante DirSync + sincronización de contraseñas |
| --- | --- |
| 1. Hola usuario inicia sesión en la red corporativa de tooa y es autenticado tooWindows Server Active Directory. |1. Hola usuario inicia sesión en la red corporativa de tooa y es autenticado tooWindows Server Active Directory. |
| 2. usuario de hello intente tooaccess Office 365 (soy @contoso.com). |2. usuario de hello intente tooaccess Office 365 (soy @contoso.com). |
| 3. Office 365 redirige Hola usuario tooAzure AD. |3. Office 365 redirige Hola usuario tooAzure AD. |
| 4. Dado que Azure AD no puede autenticar el usuario de Hola y entiende que hay una relación de confianza con AD FS local, redirige Hola usuario tooAD FS. |4. Azure AD no puede aceptar vales Kerberos directamente y no existe ninguna relación de confianza por lo que solicita que el usuario Hola especifique sus credenciales. |
| 5. Hola usuario envía un Kerberos vales a toohello AD FS STS. |5. usuario de Hola escribe Hola misma contraseña local y Azure AD la valida con el nombre de usuario de Hola y la contraseña que DirSync sincronizó. |
| 6. AD FS transforma hello toohello de vale de Kerberos requiere formato o las notificaciones del token y redirige Hola usuario tooAzure AD. |6. Azure AD redirige Hola usuario tooOffice 365. |
| 7. Hola usuario autentica tooAzure AD (se produce otra transformación). |7. usuario de hello puede iniciar sesión en tooOffice 365 y OWA con el token de hello Azure AD. |
| 8. Azure AD redirige Hola usuario tooOffice 365. | |
| 9. usuario de Hola entra en modo silencioso en tooOffice 365. | |

Hola Office 365 con DirSync con el escenario de sincronización de contraseña (sin AD FS), el inicio de sesión único se reemplaza por el"mismo inicio de sesión" donde "mismo" significa que los usuarios deben volver a escribir las mismas credenciales locales al tener acceso a Office 365. Tenga en cuenta que estos datos se pueden guardar por toohelp de explorador del usuario de hello reducir el número de solicitudes posterior.

### <a name="additional-food-for-thought"></a>Ideas adicionales para reflexionar
* Si implementa un proxy de AD FS en una máquina virtual de Azure, servidores de conectividad toohello AD FS es necesario. Si son locales, se recomienda que aproveche la conectividad VPN de sitio a sitio Hola proporcionado por toocommunicate de nodos de Proxy de aplicación Web de hello red virtual tooallow Hola con sus servidores de AD FS.
* Si implementa un servidor de AD FS en una virtual de Azure del equipo, controladores de dominio de Active Directory Server de tooWindows de conectividad, almacenes de atributos, y las bases de datos de configuración es necesarios y puede requerir también una ExpressRoute o una conexión VPN de sitio a sitio entre la red de hello Azure virtual hello y red local.
* Se aplican cargos de tráfico de tooall desde máquinas virtuales de Azure (tráfico de salida). Si el costo es un factor determinante hello, es aconsejable toodeploy nodos de Proxy de aplicación Web de hello en Azure, dejando Hola AD FS servidores locales. Si se implementan servidores de hello AD FS en máquinas virtuales de Azure, así, costos adicionales será que se incurra tooauthenticate local usuarios. Tráfico de salida supone un costo independientemente de si está atravesando hello ExpressRoute o hello conexión VPN de sitio a sitio.
* Si decide que la carga del servidor nativas de Azure toouse las capacidades de alta disponibilidad de servidores de AD FS de equilibrio, tenga en cuenta que el equilibrio de carga proporciona sondeos que son utilizados toodetermine Hola mantenimiento de máquinas virtuales de Hola Hola del servicio en nube. En caso de hello máquinas virtuales de Azure (como roles de trabajo o tooweb lugar), debe utilizarse un sondeo personalizado ya que el agente de Hola que responde toohello sondeos de forma predeterminada no está presente en máquinas virtuales de Azure. Para simplificar, puede usar un sondeo TCP personalizado: solo requiere que una conexión TCP (un segmento TCP SYN enviado y respondido toowith un segmento TCP SYN ACK) sea mantenimiento de la máquina virtual de toodetermine correctamente establecidos. Puede configurar Hola sondeo personalizado toouse cualquier toowhich de puerto TCP, que las máquinas virtuales estén escuchando activamente.

> [!NOTE]
> Equipos que necesitan hello tooexpose que mismo conjunto de puertos directamente toohello Internet (como los puertos 80 y 443) no puede compartir Hola mismo servicio en la nube. Por lo tanto, conviene crear un servicio de nube dedicado para los servidores de Windows Server AD FS en orden tooavoid posible superposiciones entre los requisitos de puerto para una aplicación y Windows Server AD FS.
> 
> 

## <a name="deployment-scenarios"></a>Escenarios de implementación
Hola siguiente sección describe implementación comunes escenarios toodraw atención tooimportant las consideraciones que deben tenerse en cuenta. Cada escenario tiene vínculos toomore detalladamente las decisiones de Hola y tooconsider de factores.

1. [AD DS: Implementación de una aplicación compatible con AD DS sin necesidad de conectividad de red corporativa](#BKMK_CloudOnly)
   
    Por ejemplo, un servicio de SharePoint a través de Internet se implementa en una máquina virtual de Azure. aplicación Hello no tiene dependencias en recursos de la red corporativa. requiere Windows Server AD DS Hello aplicación pero no requieren Hola Windows Server AD DS corporativo.
2. [AD FS: Extender un toohello de aplicación front-end local para notificaciones Internet](#BKMK_CloudOnlyFed)
   
    Por ejemplo, una aplicación para notificaciones que se ha implementado correctamente de forma local y se usan usuarios corporativos debe toobecome accesible desde Internet Hola. aplicación Hello debe toobe acceder a él directamente a través de Internet de hello tanto de asociados empresariales mediante sus propias identidades corporativas y a los usuarios corporativos existentes.
3. [AD DS: Implementar una aplicación de AD DS-compatible con Windows Server que requiere conectividad toohello en la red corporativa](#BKMK_HybridExt)
   
    Por ejemplo, una aplicación compatible con LDAP que admite la autenticación integrada de Windows y usa Windows Server AD DS como repositorio de datos de configuración y de perfil de usuario se implementa en una máquina virtual de Azure. Es deseable que Hola Hola de tooleverage de aplicación existente de Windows Server AD DS corporativo y proporcionar un inicio de sesión único. aplicación Hello no es compatible con notificaciones.

### <a name="BKMK_CloudOnly"></a>1. AD DS: Implementación de una aplicación compatible con AD DS sin necesidad de conectividad de red corporativa
![Implementación de AD DS solo en la nube](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**Figura 1**

#### <a name="description"></a>Descripción
SharePoint se implementa en una máquina virtual de Azure y aplicación Hola no tiene ninguna dependencia de recursos de la red corporativa. Hello aplicación requieren Windows Server AD DS pero no *no* requieren Hola Windows Server AD DS corporativo. No hay confianzas Kerberos ni federadas son necesarias porque los usuarios se aprovisionan automáticamente en la aplicación hello en el dominio de Windows Server AD DS de Hola que también se hospeda en la nube de hello en máquinas virtuales de Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Consideraciones sobre el escenario y cómo aplican las áreas de tecnología toohello escenario
* [Topología de red](#BKMK_NetworkTopology): cree una red virtual de Azure sin conectividad entre locales (también conocida como "conectividad de sitio a sitio").
* [Configuración de la implementación del controlador de dominio](#BKMK_DeploymentConfig): implemente un nuevo controlador de dominio en un bosque nuevo de Windows Server Active Directory de dominio único. Se debe implementar junto con el servidor de DNS de Windows hello.
* [Topología de sitio de Active Directory de Windows Server](#BKMK_ADSiteTopology): sitio de Active Directory de Windows Server Use Hola predeterminado (todos los equipos estarán en Default-First-Site-Name).
* [Direccionamiento IP y DNS](#BKMK_IPAddressDNS):
  
  * Establecer una dirección IP estática para Hola DC mediante el cmdlet de PowerShell de Azure de Set-AzureStaticVNetIP Hola.
  * Instalar y configurar DNS de Windows Server en los controladores de dominio de hello en Azure.
  * Configurar las propiedades de red virtual de hello con nombre de Hola y dirección IP de la máquina virtual que hospeda los roles de servidor de controlador de dominio y DNS de Hola Hola.
* [Catálogo global](#BKMK_GC): hello primer controlador de dominio en el bosque de hello debe ser un servidor de catálogo global. También se deberían configurar otros controladores de dominio como catálogos globales porque en un bosque de dominio único, catálogo global hello no requiere ningún trabajo adicional de Hola DC.
* [Selección de ubicación de la base de datos de Windows Server AD DS de Hola y SYSVOL](#BKMK_PlaceDB): agregar un tooDCs de disco de datos ejecutan como máquinas virtuales de Azure en la base de datos de pedido toostore Hola Windows Server Active Directory, los registros y SYSVOL.
* [Copia de seguridad y restauración](#BKMK_BUR): Determine dónde desea que las copias de seguridad del estado de sistema de toostore. Si es necesario, agregue otro disco toohello máquina virtual de controlador de dominio toostore copias de seguridad.

### <a name="BKMK_CloudOnlyFed"></a>2 AD FS: Extender un toohello de aplicación front-end local para notificaciones Internet
![Federación con conectividad entre locales](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**Figura 2**

#### <a name="description"></a>Descripción
Una aplicación para notificaciones que se ha implementado correctamente de forma local y utilizado por los usuarios corporativos necesidades toobecome accesible directamente desde Internet Hola. aplicación Hello actúa como web front-end tooa base de datos SQL en la que almacena los datos. servidores SQL Server Hola utilizado por la aplicación hello también se encuentra en la red corporativa de Hola. Dos STS de Windows Server AD FS y un equilibrador de carga han sido implementado de forma local tooprovide acceso toohello los usuarios corporativos. Ahora la aplicación Hello debe toobe accesible directamente a través de Internet de Hola por asociados empresariales mediante sus propias identidades corporativas y usuarios corporativos existentes.

En un esfuerzo toosimplify y las necesidades de implementación y configuración de hello cumple de este nuevo requisito, se decidió que aparecerán dos web front-ends y dos servidores de proxy de Windows Server AD FS instalarse en máquinas virtuales de Azure. Las cuatro máquinas virtuales estarán expuestos directamente toohello Internet y proporcionará la red de conectividad toohello local con capacidad VPN de sitio a sitio de la red Virtual de Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Consideraciones sobre el escenario y cómo aplican las áreas de tecnología toohello escenario
* [Topología de red](#BKMK_NetworkTopology): cree una red virtual de Azure y [configure la conectividad entre locales](../vpn-gateway/vpn-gateway-site-to-site-create.md).
  
  > [!NOTE]
  > Para cada uno de los certificados de Windows Server AD FS hello, asegúrese de que hello dirección URL definida dentro de la plantilla de certificado de Hola y certificados resultantes Hola pueden tener acceso mediante instancias de hello Windows Server AD FS que se ejecutan en Azure. Esto puede requerir tooparts de conectividad entre entornos de la infraestructura de PKI. Por ejemplo, si el punto de conexión de hello CRL es basados en LDAP y exclusivamente hospedado en local y, a continuación, la conectividad entre entornos será necesario. Si esto no es deseable, es posible certificados necesarios toouse emitidos por una entidad de certificación cuya CRL sea accesible a través de Internet de Hola.
  > 
  > 
* [Configuración de servicios en la nube](#BKMK_CloudSvcConfig): asegúrese de que tiene dos servicios en la nube para proporcionar dos direcciones IP virtuales de carga equilibrada. dirección IP virtual de Hello primer servicio en la nube será dirigido toohello dos Windows Server AD FS proxy máquinas virtuales en los puertos 80 y 443. Hello serán las máquinas virtuales de proxy de Windows Server AD FS configurado toopoint toohello dirección IP de hello local equilibrador de carga que atiende a Hola STS de Windows Server AD FS. dirección IP virtual de Hello segundo servicio en la nube será dirigido toohello dos las máquinas virtuales ejecutar front-end web de Hola de nuevo en los puertos 80 y 443. Configure un sondeo personalizado tooensure Hola equilibrador de carga solo dirige tráfico toofunctioning Windows Server AD FS proxy y web front-end máquinas virtuales.
* [Configuración del servidor de federación](#BKMK_FedSrvConfig): configurar Windows Server AD FS como un seguridad de federación (STS) de servidor toogenerate tokens para el bosque de Windows Server Active Directory Hola creado en la nube de Hola. Establecer relaciones de confianza de proveedor de notificaciones de federación asociados Hola diferentes que desea tooaccept las identidades y configurar relaciones de confianza para usuario autenticado con diferentes aplicaciones de hello que desea toogenerate símbolos (tokens).
  
    En la mayoría de los escenarios, los servidores proxy de Windows Server AD FS se implementan en una funcionalidad accesible desde Internet por motivos de seguridad mientras que sus homólogos de federación de Windows Server AD FS permanecen apartados de la conectividad directa a Internet. Independientemente de su escenario de implementación, debe configurar el servicio de nube con una dirección IP virtual que proporcionará una dirección IP expuesta públicamente y un puerto que sea capaz de equilibrar la tooload entre las dos instancias de STS de Windows Server AD FS o proxy.
* [Configuración de alta disponibilidad de Windows Server AD FS](#BKMK_ADFSHighAvail): es aconsejable toodeploy una granja de servidores de Windows Server AD FS con al menos dos servidores para la conmutación por error y equilibrio de carga. Podría desea tooconsider con hello Windows Internal Database (WID) para los datos de configuración de Windows Server AD FS y usar Hola interno equilibrio de carga capacidad de Azure toodistribute las solicitudes entrantes entre servidores de hello en la granja de servidores de Hola.

Para obtener más información, vea hello [Guía de implementación de AD DS](https://technet.microsoft.com/library/cc753963).

### <a name="BKMK_HybridExt"></a>3. AD DS: Implementar una aplicación de AD DS-compatible con Windows Server que requiere conectividad toohello en la red corporativa
![Implementación de AD DS entre locales](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**Figura 3**

#### <a name="description"></a>Descripción
Una aplicación compatible con LDAP se implementa en una máquina virtual de Azure. Admite la autenticación integrada de Windows y usa Windows Server AD DS como repositorio para los datos de configuración y de perfil de usuario. el objetivo de Hola Hola Hola de tooleverage de aplicación existente de Windows Server AD DS corporativo así como el inicio de sesión único. aplicación Hello no es compatible con notificaciones. Los usuarios también necesitan la aplicación de hello tooaccess directamente desde Internet Hola. toooptimize rendimiento y el costo, se decide implementar dos controladores de dominio adicionales que forman parte del dominio corporativo Hola junto con la aplicación hello en Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Consideraciones sobre el escenario y cómo aplican las áreas de tecnología toohello escenario
* [Topología de red](#BKMK_NetworkTopology): cree una red virtual de Azure con [conectividad entre locales](../vpn-gateway/vpn-gateway-site-to-site-create.md).
* [Método de instalación](#BKMK_InstallMethod): implementar controladores de dominio de réplica del dominio de Windows Server Active Directory corporativo Hola. Para un controlador de dominio de réplica, puede instalar Windows Server AD DS en hello VM y, opcionalmente, use Hola instalar desde medios (IFM) característica tooreduce Hola cantidad de datos que necesita toobe replica toohello nuevo controlador de dominio durante la instalación. Para ver un tutorial, consulte [Instalación de un controlador de dominio de Active Directory de réplica en una red virtual de Azure](active-directory-install-replica-active-directory-domain-controller.md). Incluso aunque utilice IFM, puede ser más eficaz Hola de toobuild controlador de dominio virtual local y mover Hola todo disco duro Virtual (VHD) toohello en la nube en lugar de replicar Windows Server AD DS durante la instalación. Por motivos de seguridad, se recomienda eliminar Hola VHD de red de hello local una vez se ha copiado tooAzure.
* [Topología del sitio de Windows Server Active Directory](#BKMK_ADSiteTopology): cree un nuevo sitio de Azure en Sitios y servicios de Active Directory. Cree un Hola de toorepresent objeto de subred de Windows Server Active Directory red virtual de Azure y agregar Hola subred toohello sitio. Crear un nuevo vínculo a sitios que incluye el nuevo sitio de Azure Hola y el sitio de hello en qué Hola red virtual de Azure extremo de VPN se encuentra en orden toocontrol y optimizan tooand de tráfico de Windows Server Active Directory de Azure.
* [Direccionamiento IP y DNS](#BKMK_IPAddressDNS):
  
  * Establecer una dirección IP estática para Hola DC mediante el cmdlet de PowerShell de Azure de Set-AzureStaticVNetIP Hola.
  * Instalar y configurar DNS de Windows Server en los controladores de dominio de hello en Azure.
  * Configurar las propiedades de red virtual de hello con nombre de Hola y dirección IP de la máquina virtual que hospeda los roles de servidor de controlador de dominio y DNS de Hola Hola.
* [Controladores de dominio distribuidos geográficamente](#BKMK_DistributedDCs): configure tantas redes virtuales adicionales como sea necesario. Si la topología de sitio de Active Directory necesita controladores de dominio en geografías que corresponden toodifferent Azure regiones, que desea toocreate sitios de Active Directory en consecuencia.
* [Controladores de dominio de solo lectura](#BKMK_RODC): puede implementar un RODC en hello sitio de Azure, dependiendo de sus requisitos para llevar a cabo las operaciones de escritura contra Hola compatibilidad hello y controlador de dominio de aplicaciones y servicios en el sitio de hello tiene los RODC. Para obtener más información acerca de la compatibilidad de aplicaciones, vea hello [Guía de compatibilidad de aplicaciones de controladores de dominio de solo lectura](https://technet.microsoft.com/library/cc755190).
* [Catálogo global](#BKMK_GC): catálogos globales son las solicitudes de inicio de sesión de tooservice necesarios en bosques con varios dominios. Si no implementa un catálogo global en hello sitio de Azure, incurrirá en costos de tráfico de salida porque las solicitudes de autenticación generan consultas de catálogos globales en otros sitios. toominimize que el tráfico, puede habilitar la pertenencia a grupos universales almacenamiento en caché para hello Azure sitio en servicios y sitios de Active Directory.
  
    Si implementa un catálogo global, configure los vínculos a sitios y los costos de vínculos de sitio para que GC Hola Hola sitio de Azure no es el preferido como un DC de origen otros catálogos globales que necesitan tooreplicate Hola mismas particiones parciales de dominio.
* [Selección de ubicación de la base de datos de Windows Server AD DS de Hola y SYSVOL](#BKMK_PlaceDB): agregar un tooDCs de disco de datos ejecuta en máquinas virtuales de Azure en la base de datos de pedido toostore Hola Windows Server Active Directory, los registros y SYSVOL.
* [Copia de seguridad y restauración](#BKMK_BUR): Determine dónde desea que las copias de seguridad del estado de sistema de toostore. Si es necesario, agregue otro disco toohello máquina virtual de controlador de dominio toostore copias de seguridad.

## <a name="deployment-decisions-and-factors"></a>Factores y decisiones de implementación
Esta tabla resumen las áreas de tecnología de Windows Server Active Directory Hola que se ven afectadas en hello anteriores escenarios y Hola tooconsider de decisiones correspondiente, con vínculos toomore nivel de detalle a continuación. Algunas áreas de tecnología pueden no ser aplicable tooevery escenario de implementación y algunas áreas de tecnología podrían ser más importante escenario de implementación de tooa a otras áreas de tecnología.

Por ejemplo, si implementa una controlador de dominio de réplica en una red virtual y el bosque tiene un solo dominio, a continuación, elija toodeploy un servidor de catálogo global en ese caso no será escenario de implementación de toohello crítico porque no creará ningún adicionales de replicación requisitos. En Hola otra parte, si Hola bosque tiene varios dominios, a continuación, podría afectar a la decisión de hello toodeploy un catálogo global en una red virtual de ancho de banda disponible, rendimiento, autenticación, las búsquedas de directorio y así sucesivamente.

| Área de tecnología en Windows Server Active Directory | Decisiones | Factores |
| --- | --- | --- |
| [Topología de red](#BKMK_NetworkTopology) |¿Crear una red virtual? |<li>Requisitos tooaccess recursos corporativos</li> <li>Autenticación</li> <li>Administración de cuentas</li> |
| [Configuración de la implementación del controlador de dominio](#BKMK_DeploymentConfig) |<li>¿Implementar un bosque independiente sin ninguna relación de confianza?</li> <li>¿Implementar un nuevo bosque con federación?</li> <li>¿Implementar un nuevo bosque con confianza de bosque de Windows Server Active Directory o Kerberos?</li> <li>¿Extender el bosque corporativo implementando un controlador de dominio de réplica?</li> <li>¿Extender el bosque corporativo implementando un nuevo dominio secundario o árbol de dominios?</li> |<li>Seguridad</li> <li>Cumplimiento normativo</li> <li>Coste</li> <li>Resistencia y tolerancia a errores</li> <li>Compatibilidad de aplicación</li> |
| [Topología del sitio en Windows Server Active Directory](#BKMK_ADSiteTopology) |¿Cómo configurar subredes, sitios y vínculos a sitios con el tráfico de red Virtual de Azure toooptimize y minimizar el costo? |<li>Definiciones de sitio y de subred</li> <li>Propiedades de vínculo de sitio y notificación de cambio</li> <li>Compresión de replicación</li> |
| [Direccionamiento IP y DNS](#BKMK_IPAddressDNS) |¿Cómo tooconfigure IP direcciones y la resolución de nombres? |<li>Usar Set-AzureStaticVNetIP cmdlet tooassign una dirección IP estática de hello uso Hola</li> <li>Instalar el servidor DNS de Windows Server y configurar las propiedades de red virtual de hello con nombre de Hola y dirección IP de la máquina virtual que hospeda los roles de servidor de controlador de dominio y DNS de Hola Hola</li> |
| [Controladores de dominio distribuidos geográficamente](#BKMK_DistributedDCs) |¿Cómo tooreplicate tooDCs en separar las redes virtuales? |Si la topología de sitio de Active Directory necesita controladores de dominio en geografías que corresponden toodifferent Azure regiones, que desea toocreate sitios de Active Directory en consecuencia. [Configurar la red de la red virtual toovirtual conectividad](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) tooreplicate entre controladores de dominio en redes virtuales diferentes. |
| [Controladores de dominio de solo lectura](#BKMK_RODC) |¿Usar controladores de dominio de solo lectura o de escritura? |<li>Filtrar atributos HBI/PII</li> <li>Filtrar secretos</li> <li>Limitar tráfico de salida</li> |
| [Catálogo global](#BKMK_GC) |¿Instalar un catálogo global? |<li>Para el bosque de dominio único, convertir todos los catálogos globales en controladores de dominio</li> <li>Para un bosque con varios dominios, se requieren catálogos globales para la autenticación.</li> |
| [Método de instalación](#BKMK_InstallMethod) |¿Cómo tooinstall DC en Azure? |Opciones:  <li>Instalar AD DS mediante Windows PowerShell o Dcpromo</li> <li>Trasladar VHD de un controlador de dominio virtual local a la nube</li> |
| [Selección de ubicación de la base de datos de Windows Server AD DS de Hola y SYSVOL](#BKMK_PlaceDB) |¿Cuando se inicia una base de datos de toostore Windows Server AD DS y SYSVOL? |Cambie los valores predeterminados de Dcpromo.exe. Estos archivos críticos de Active Directory *deben* colocarse en discos de datos de Azure en lugar de en discos del sistema operativo que implementan almacenamiento en caché de escritura. |
| [Copia de seguridad y restauración](#BKMK_BUR) |¿Cómo toosafeguard y recuperar los datos? |Creación de copias de seguridad del estado del sistema |
| [Configuración del servidor de federación](#BKMK_FedSrvConfig) |<li>¿Implementar un nuevo bosque con federación en la nube de hello?</li> <li>Implementar AD FS local y exponer a un proxy en la nube de hello?</li> |<li>Seguridad</li> <li>Cumplimiento normativo</li> <li>Coste</li> <li>Acceso tooapplications por los socios comerciales</li> |
| [Configuración de servicios en la nube](#BKMK_CloudSvcConfig) |Un servicio de nube se implementa implícitamente Hola la primera vez que cree una máquina virtual. ¿Necesita toodeploy servicios en la nube adicionales? |<li>¿Máquinas virtuales o una máquina virtual requiere exposición directa toohello Internet?</li> <li> ¿Servicio de hello requiere equilibrio de carga?</li> |
| [Requisitos del servidor de federación para el direccionamiento IP público y privado (IP dinámica frente a IP virtual)](#BKMK_FedReqVIPDIP) |<li>¿Necesita instancia Hola Windows Server AD FS toobe accesible directamente desde Internet Hola?</li> <li>¿Aplicación Hola se implementa en la nube de hello requiere su propia dirección IP de conexión a Internet y el puerto?</li> |Creación de un servicio en la nube para cada dirección IP virtual que necesite la implementación |
| [Configuración de alta disponibilidad de Windows Server AD FS](#BKMK_ADFSHighAvail) |<li>¿Cuántos nodos debe tener la granja de servidores de Windows Server AD FS?</li> <li>¿El número de nodos toodeploy en mi granja de servidores de proxy de Windows Server AD FS?</li> |Resistencia y tolerancia a errores |

### <a name="BKMK_NetworkTopology"></a>Topología de red
En orden toomeet Hola IP porque la dirección constante y los requisitos de DNS de Windows Server AD DS, es necesario crear toofirst una [red virtual de Azure](../virtual-network/virtual-networks-overview.md) y adjuntar su tooit de máquinas virtuales. Durante su creación, debe decidir si toooptionally extender conectividad tooyour local corporativa de red, lo que se conecta de forma transparente virtual de Azure máquinas máquinas locales tooon, esto se logra mediante tecnologías tradicionales de VPN y requiere que un extremo de VPN exponer en hello borde de la red corporativa de Hola. Es decir, Hola VPN se inicia desde la red corporativa de toohello de Azure, no al contrario.

Tenga en cuenta que se aplican cargos adicionales al extender una red de en entornos de red virtual tooyour más allá de hello cargos estándar según el que se aplican tooeach máquina virtual. En concreto, hay cargos por tiempo de CPU de puerta de enlace de red Virtual de Azure de Hola y para tráfico de salida de hello generado por cada máquina virtual que se comunica con equipos locales a través de hello VPN. Para obtener más información acerca de los gastos por tráfico de red, consulte [Precios de Azure](http://azure.microsoft.com/pricing/).

### <a name="BKMK_DeploymentConfig"></a>Configuración de la implementación del controlador de dominio
forma de Hello configurar Hola DC depende de los requisitos de Hola Hola de servicio que se desea toorun en Azure. Por ejemplo, podría implementar un nuevo bosque, aislado de su propio bosque corporativo, para probar una prueba de concepto, una nueva aplicación o algún otro proyecto a corto plazo requiere servicios de directorio pero los recursos corporativos de acceso no es específica de toointernal.

Como una de las ventajas, un bosque aislado de un con que controlador de dominio no se replica en controladores de dominio locales, resultante saliente menos tráfico de red generado por sistema hello, reduce directamente los costos. Para obtener más información acerca de los gastos por tráfico de red, consulte [Precios de Azure](http://azure.microsoft.com/pricing/).

Como otro ejemplo, supongamos que tiene requisitos de privacidad de un servicio, pero servicio Hola depende tooyour acceso interno Windows Server Active Directory. Si se permiten datos toohost para servicio de hello en nube de hello, podría implementar un nuevo dominio secundario para el bosque interno en Azure. En este caso, puede implementar un controlador de dominio para el nuevo dominio secundario hello (sin el catálogo global de hello en cuestiones de privacidad de dirección de orden toohelp). Este escenario, junto con una implementación de controlador de dominio de réplica, requiere una red virtual para la conectividad con los controladores de dominio locales.

Si crea un nuevo bosque, elija si toouse [confianzas de Active Directory](https://technet.microsoft.com/library/cc771397) o [confianzas de federación](https://technet.microsoft.com/library/dd807036). Equilibrar los requisitos de hello dictados por compatibilidad, seguridad, cumplimiento de normas, costo y resistencia. Por ejemplo, tootake aprovechar [autenticación selectiva](https://technet.microsoft.com/library/cc755844) podría elegir toodeploy un nuevo bosque en Azure y crear una confianza de Windows Server Active Directory entre bosques de local de Hola y Hola en la nube. Sin embargo, si la aplicación hello es compatible con notificaciones, puede implementar confianzas de federación en lugar de confianzas de bosque de Active Directory. Otro factor se Hola costo tooeither replicar más datos extendiendo sus instalaciones en nube de Windows Server Active Directory toohello o generar más tráfico de salida como resultado de la autenticación y la carga de la consulta.

Los requisitos de disponibilidad y tolerancia a errores también influyen en su elección. Por ejemplo, si se interrumpe el vínculo de hello, aplicaciones que aprovechan una confianza Kerberos o una confianza de federación están todos probablemente dejen de funcionar a menos que haya implementado una infraestructura suficiente en Azure. Las configuraciones de implementación alternativo, como controladores de dominio de réplica (escritura o RODC) aumentan Hola probabilidad de ser capaz de tootolerate interrupciones del vínculo.

### <a name="BKMK_ADSiteTopology"></a>Topología del sitio en Windows Server Active Directory
Se necesita toocorrectly definir sitios y vínculos a sitios en orden toooptimize tráfico y minimizar el costo. Sitios, vínculos a sitios y subredes afectan a la topología de replicación de hello entre controladores de dominio y el flujo de Hola de tráfico de autenticación. Considere la posibilidad de hello siguientes cargos de tráfico y, a continuación, implementar y configurar controladores de dominio según los requisitos de toohello de su escenario de implementación:

* Hay una cuota nominal por hora para hello puerta de enlace:
  
  * Se puede iniciar y detener como considere oportuno
  * Si se detiene, máquinas virtuales de Azure quedan aisladas de red corporativa de Hola
* El tráfico de entrada es gratis
* Se cobra el tráfico saliente, según demasiado[Azure precios de un vistazo](http://azure.microsoft.com/pricing/). Puede optimizar las propiedades de vínculo de sitio entre sitios locales y los sitios de la nube de hello como sigue:
  
  * Si usas varias redes virtuales, configurar vínculos de sitio de Hola y sus costos adecuadamente tooprevent Windows Server AD DS de Hola para establecer prioridades entre Azure sitio sobre uno que pueda proporcionar Hola mismos niveles de servicio sin cargo. También puede considerar deshabilitar puente Hola todo el sitio link (BASL) (opción) (que está habilitado de forma predeterminada). Esto garantiza que solo sitios con conexión directa se replican entre sí. Controladores de dominio en sitios conectados de forma transitiva ya no son tooreplicate pueda directamente entre ellos, pero deben replicar a través de una o varios sitios comunes. Si sitios intermedios Hola dejan de estar disponible por alguna razón, no se producirá la replicación entre controladores de dominio en sitios conectados de forma transitiva incluso si la conectividad entre sitios de hello está disponible. Por último, donde las secciones de comportamiento de la replicación transitiva permanecen deseables, crear sitio puentes de vínculos que contienen vínculos de sitio adecuados hello y sitios, por ejemplo, de forma local, sitios de la red corporativa.
  * [Configurar los costos del vínculo de sitio](https://technet.microsoft.com/library/cc794882) adecuadamente tooavoid tráfico no deseado. Por ejemplo, si **intentar siguiente sitio más cercano** está habilitada, asegúrese de red virtual de hello seguro sitios no se Hola junto más cercano si aumenta el costo de hello asociado del objeto de vínculo a sitios de Hola que conecta hello Azure sitio atrás toohello red corporativa.
  * Configurar el vínculo a sitios [intervalos](https://technet.microsoft.com/library/cc794878) y [programaciones](https://technet.microsoft.com/library/cc816906) según los requisitos de tooconsistency y la tasa de cambios de objeto. Alinee la programación de replicación con la tolerancia de latencia. Controladores de dominio replican sólo Hola último estado de un valor, por lo que el intervalo de replicación de hello decreciente puede ahorrar costos si hay una tasa de cambio de objeto suficiente.
* Si la reducción de costos es una prioridad, asegúrese de que se programa la replicación y que no está habilitada la notificación de cambios. Trata la configuración predeterminada de hello al replicar entre sitios. Esto no es importante si va a implementar un RODC en una red virtual porque Hola RODC no replicará ningún cambio de salida. Pero, si implementa un DC de escritura, debe asegurarse de que el vínculo a sitios hello no está configurado tooreplicate actualizaciones con una frecuencia innecesaria. Si implementa un servidor de catálogo global (GC), asegúrese de que todos los sitios que contiene un catálogo global replican las particiones de dominio desde un controlador de dominio en un sitio que está conectado a un vínculo de sitio de origen o vínculos de sitio que tienen un costo menor de Hola GC en Hola sitio de Azure.
* Es posible toofurther todavía reducir el tráfico de red generado por la replicación entre sitios si se cambia el algoritmo de compresión de replicación de Hola. algoritmo de compresión de Hola se controla mediante el algoritmo de compresión de HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Replicator de entrada de hello REG_DWORD del registro. valor predeterminado de Hello es 3, que correlaciona toohello algoritmo de compresión Xpress. Puede cambiar Hola valor too2, qué cambios Hola tooMSZip de algoritmo. En la mayoría de los casos, Esto aumentará la compresión hello, pero lo hace a expensas de hello del uso de CPU. Para obtener más información, consulte [How Active Directory replication topology works](https://technet.microsoft.com/library/cc755994)(Funcionamiento de la topología de replicación de Active Directory).

### <a name="BKMK_IPAddressDNS"></a>Direccionamiento IP y DNS
A las máquinas virtuales se les asignan "direcciones concedidas por DHCP" de forma predeterminada. Dado que direcciones dinámicas de red virtual de Azure se conservan con una máquina virtual para la duración de Hola de máquina virtual de hello, se cumplen los requisitos de Hola de Windows Server AD DS.

Como resultado, cuando se usa una dirección dinámica en Azure, están en vigor con una dirección IP estática porque es enrutable por período de Hola de concesión de Hola y período de Hola de concesión de hello es toohello igual duración del servicio de nube de Hola.

Sin embargo, una dirección dinámica Hola se desasigna si Hola VM se apaga. dirección IP de hello tooprevent desde que se va a cancelar la asignación, puede [usar Set-AzureStaticVNetIP tooassign una dirección IP estática](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx).

Resolución de nombres, implemente su propia (o aproveche sus) infraestructura de servidor DNS; DNS proporcionado por Azure no cumple Hola avanzadas necesidades de resolución de nombres de Windows Server AD DS. Por ejemplo, no admite registros SRV dinámicos, etc. La resolución de nombres es un elemento de configuración crítico para los controladores de dominio y los clientes unidos a un dominio. Los controladores de dominio deben ser capaces de registrar los registros de recursos y resolver los registros de recursos de otros controladores de dominio.
Por razones de rendimiento y tolerancia a errores, es óptimo tooinstall Hola DNS de Windows Server servicio en controladores de dominio de hello ejecuta en Azure. A continuación, configurar propiedades de red virtual de Azure de hello con nombre hello y dirección IP del servidor DNS de Hola. Cuando se inician otras máquinas virtuales en la red virtual de hello, su configuración de resolución de cliente DNS se configurarán con el servidor DNS como parte de la asignación de direcciones IP dinámicas de Hola.

> [!NOTE]
> No puede unirse a dominio de Active Directory de Windows Server AD DS de tooa de equipos de local que se hospeda en Azure directamente a través de Internet de Hola. Hola requisitos del puerto de Active Directory y la operación de unión a dominio Hola hacerla puertos necesarios de toodirectly poco práctico exponer Hola y de hecho, un toohello DC todo Internet.
> 
> 

Las máquinas virtuales registran su nombre DNS automáticamente al iniciarse o cuando hay un cambio de nombre.

Para obtener más información acerca de este ejemplo y otro ejemplo que muestra cómo tooprovision Hola primera máquina virtual e instalar AD DS en ella, vea [instalar un nuevo bosque de Active Directory en Microsoft Azure](active-directory-new-forest-virtual-machine.md). Si desea conocer más detalles sobre el uso de Windows PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) y [Azure Management Cmdlets](/powershell/module/azurerm.compute/#virtual_machines) (Cmdlets de administración de Azure).

### <a name="BKMK_DistributedDCs"></a>Controladores de dominio distribuidos geográficamente
Azure ofrece diversas ventajas cuando se hospedan varios controladores de dominio en redes virtuales diferentes:

* Tolerancia a errores de varios sitios
* Oficinas de proximidad física toobranch (menor latencia)

Para obtener información acerca de cómo configurar la comunicación directa entre redes virtuales, vea [configurar la conectividad de red de red virtual toovirtual](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

### <a name="BKMK_RODC"></a>Controladores de dominio de solo lectura
Necesita toochoose si toodeploy leyó-solo o puede escribir controladores de dominio. Es posible que toodeploy inclinada RODC porque no tendrá control físico sobre ellos, pero los RODC están diseñado toobe implementada en ubicaciones donde la seguridad física es un riesgo, como las sucursales.

Azure no presenta Hola de riesgo de seguridad física de una sucursal, pero los RODC siguen siendo toobe más rentables porque las características de Hola que proporcionan son adecuadas toothese entornos aunque por motivos muy diferentes. Por ejemplo, los RODC no tienen ninguna replicación de salida y se tooselectively pueda rellenar secretos (contraseñas). En desventaja de hello, falta de Hola de estos secretos puede requerir toovalidate el tráfico de salida a petición conforme se autentica un usuario o equipo. Pero los secretos se pueden rellenar previamente de forma selectiva y almacenarlos en caché.

Los RODC proporcionan una ventaja adicional en torno a las preocupaciones HBI y PII ya que puede agregar atributos que contienen datos confidenciales toohello RODC filtran el conjunto de atributos (FAS). Hola FAS es un conjunto personalizable de atributos que no están tooRODCs replicada. Puede usar hello FAS como medida de seguridad en caso de que no se permiten o no quiere toostore PII o HBI en Azure. Para más información, consulte [RODC filtered attribute set (Conjunto de atributos filtrados de RODC) en [(https://technet.microsoft.com/library/cc753459)]

Asegúrese de que las aplicaciones compatibles con los RODC tiene previsto toouse. Muchas aplicaciones basadas en Windows Server Active Directory funcionen bien con los RODC, pero algunas aplicaciones pueden realizar de forma ineficaz o se producirá un error si no tiene acceso tooa DC de escritura. Para obtener más información, consulte la [guía de compatibilidad de aplicaciones con controladores de dominio de solo lectura](https://technet.microsoft.com/library/cc755190).

### <a name="BKMK_GC"></a>Catálogo global
Si necesita toochoose tooinstall un catálogo global (GC). En un bosque de dominio único, debe configurar todos los controladores de dominio como servidores de catálogo global. Esto no aumentará los costos porque no habrá ningún tráfico de replicación adicional.

En un bosque con varios dominios, los catálogos globales son pertenencia al grupo Universal de tooexpand necesarios durante el proceso de autenticación de Hola. Si no implementa un catálogo global, cargas de trabajo en la red virtual de Hola que se autentican en un controlador de dominio en Azure generarán indirectamente tráfico de autenticación de salida tooquery catálogos globales locales durante cada intento de autenticación.

los costos de Hello asociados a catálogos globales son menos predecibles porque hospedan todos los dominios (en parte). Si la carga de trabajo de hello hospeda un servicio a través de Internet y autentica a los usuarios en Windows Server AD DS, los costos de hello podrían ser completamente imprevisibles. toohelp reducir las consultas de GC fuera de sitio en la nube de Hola durante la autenticación, puede [Habilitar caché de pertenencia al grupo Universal](https://technet.microsoft.com/library/cc816928).

### <a name="BKMK_InstallMethod"></a>Método de instalación
Necesita toochoose cómo tooinstall Hola controladores de dominio de red virtual de hello:

* Promoción de nuevos controladores de dominio. Para obtener más información, consulte [Instalación de un bosque nuevo de Active Directory en una red virtual de Azure](active-directory-new-forest-virtual-machine.md).
* Mover Hola VHD de una nube de toohello de controlador de dominio virtual local. En este caso, debe asegurarse de esa Hola de-local controlador de dominio virtual se "mueva", no "Copie" o "Clone".

Usar máquinas virtuales de Azure solo para controladores de dominio (como tooAzure lugar "web" o "trabajo" rol de VM). Son duraderas y la durabilidad de estado es un requisito para un controlador de dominio. Las máquinas virtuales de Azure están diseñadas para cargas de trabajo como controladores de dominio.

No utilice SYSPREP toodeploy o clonar controladores de dominio. Hola capacidad tooclone controladores de dominio está solo disponible a partir de Windows Server 2012. Hola característica clonación requiere compatibilidad con VMGenerationID en el hipervisor subyacente Hola. Tanto Hyper-V en Windows Server 2012 como Redes virtuales de Azure son compatibles con VMGenerationID, al igual que otros proveedores de software de virtualización de terceros.

### <a name="BKMK_PlaceDB"></a>Selección de ubicación de la base de datos de Windows Server AD DS de Hola y SYSVOL
Seleccione dónde toolocate Hola base de datos de Windows Server AD DS, los registros y SYSVOL. Se deben implementar en discos de datos de Azure.

> [!NOTE]
> Discos de datos de Azure son too1 restringida TB.
> 
> 

Las unidades de disco de datos no tienen cachés de escritura de forma predeterminada. Unidades de disco de datos que están conectado tooa VM usar escritura mediante el almacenamiento en caché. Facilita el almacenamiento en caché mediante escritura seguro Hola escritura es toodurable confirma el almacenamiento de Azure antes de hello completa desde la perspectiva de hello del sistema operativo de la máquina virtual de Hola. Proporciona durabilidad, a expensas de Hola de escrituras ligeramente más lentas.

Esto es importante para Windows Server AD DS porque la caché de disco de escritura en segundo plano invalida los supuestos realizados por Hola DC. Windows Server AD DS intenta toodisable la caché de escritura pero depende toohonor de sistema de E/S de disco toohello. Caché de escritura de error toodisable puede, en determinadas circunstancias, revertirse los USN resultante en persistentes objetos y otros problemas.

Como práctica recomendada para controladores de dominio virtuales, Hola siguientes:

* Establecer configuración de la preferencia de caché de Host de hello en el disco de datos de Azure de Hola para ninguno. Esto evita problemas con la caché de escritura para las operaciones de AD DS.
* Almacenar la base de datos de hello, los registros y SYSVOL en hello, ya sean los mismos datos en disco o discos de datos diferentes. Normalmente, se trata de un disco independiente de disco de hello usado para el propio sistema de operativo Hola. conclusión principal Hello es esa base de datos de Windows Server AD DS de Hola y SYSVOL no debe almacenarse en un tipo de disco de sistema operativo de Azure. De forma predeterminada, hello proceso de instalación de AD DS instala estos componentes en la carpeta de % systemroot %, que no se recomienda para Azure.

### <a name="BKMK_BUR"></a>Copia de seguridad y restauración
Tenga en cuenta lo que es compatible y lo que no a la hora de realizar una copia de seguridad y restauración de un controlador de dominio en general y, más concretamente, de aquellos que se ejecutan en una máquina virtual. Consulte la sección de [consideraciones relacionadas con la copia de seguridad y la restauración para controladores de dominio virtualizados](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers).

Cree copias de seguridad del estado del sistema solo mediante software que sea compatible específicamente con los requisitos de copia de seguridad para Windows Server AD DS como, por ejemplo, Copias de seguridad de Windows Server.

No copie ni clone archivos VHD de los controladores de dominio en lugar de realizar copias de seguridad periódicas. Si en alguna ocasión se necesita una restauración, hacerlo con VHD clonados o copiados sin Windows Server 2012 y un hipervisor compatible hará que se incluyan burbujas de USN.

### <a name="BKMK_FedSrvConfig"></a>Configuración del servidor de federación
configuración de Hola de servidores de federación (STS) de Windows Server AD FS depende en parte de si hello aplicaciones que desean toodeploy en Azure necesitan tooaccess recursos de la red local.

Si las aplicaciones de hello cumplen Hola siguiendo criterios, puede implementar aplicaciones de hello en aislamiento de la red local.

* Aceptan tokens de seguridad SAML
* Únicamente son toohello pueden exponer Internet
* No acceden a los recursos locales

En este caso, configure los STS de Windows Server AD FS como sigue:

1. Configure un bosque de dominio único aislado en Azure.
2. Proporcionar acceso federado toohello bosque configurando una granja de servidores de federación de Windows Server AD FS.
3. Configurar Windows Server AD FS (granja de servidores de federación y granja de servidores proxy de federación) en el bosque local de Hola.
4. Establecer una relación de confianza de federación entre hello en instancias locales y Azure de Windows Server AD FS.

En Hola otra parte, si las aplicaciones de hello requieren acceso a los recursos locales de tooon, podría configurar Windows Server AD FS con la aplicación hello en Azure como se indica a continuación:

1. Configure la conectividad entre redes locales y Azure.
2. Configurar una granja de servidores de federación de Windows Server AD FS en el bosque local de Hola.
3. Configure una granja proxy de servidores de federación de Windows Server AD FS en Azure.

Esta configuración tiene la ventaja de Hola de reducir la exposición de Hola de recursos locales, tooconfiguring similar Windows Server AD FS con aplicaciones en una red perimetral.

Tenga en cuenta que en ambos escenarios, puede establecer relaciones de confianza con varios proveedores de identidades, si es necesaria la colaboración de negocio a negocio.

### <a name="BKMK_CloudSvcConfig"></a>Configuración de servicios en la nube
Servicios en la nube son necesarios si desea tooexpose una máquina virtual directamente toohello Internet o tooexpose una conexión a Internet con equilibrio de carga aplicación. Esto es posible porque cada servicio en la nube ofrece una única dirección IP virtual configurable.

### <a name="BKMK_FedReqVIPDIP"></a>Requisitos del servidor de federación para el direccionamiento IP público y privado (IP dinámica frente a IP virtual)
Cada máquina virtual de Azure recibe una dirección IP dinámica. Una dirección IP dinámica es una dirección privada accesible únicamente desde dentro de Azure. Sin embargo, en la mayoría de los casos, será necesario tooconfigure una dirección IP virtual para las implementaciones de Windows Server AD FS. dirección IP virtual de Hello es necesario tooexpose toohello de puntos de conexión de Windows Server AD FS Internet y se utilizará por los asociados federados y los clientes para la autenticación y la administración continua. Una dirección IP virtual es una propiedad de un servicio en la nube que contiene una o más máquinas virtuales de Azure. Si la aplicación para notificaciones de hello implementada en Azure y Windows Server AD FS está orientado a Internet y el recurso compartido de puertos comunes, cada una requerirá una dirección IP virtual de su propio y por tanto será toocreate es necesario un servicio de aplicación hello y un en segundo lugar para Windows Server AD FS.

Para obtener definiciones de dirección IP dinámica y la dirección IP virtual de hello términos, vea [términos y definiciones](#BKMK_Glossary).

### <a name="BKMK_ADFSHighAvail"></a>Configuración de alta disponibilidad de Windows Server AD FS
Aunque es posible toodeploy los servicios de federación independiente de Windows Server AD FS, es recomendable toodeploy una granja de servidores con al menos dos nodos para STS de AD FS y servidores proxy para entornos de producción.

Vea [consideraciones de topología de AD FS 2.0 implementación](https://technet.microsoft.com/library/gg982489) en hello [AD FS 2.0 diseño guía](https://technet.microsoft.com/library/dd807036) toodecide opciones de configuración de implementación que mejor ajuste a sus necesidades concretas.

> [!NOTE]
> Orden tooget equilibrio de carga para los puntos de conexión de Windows Server AD FS en Azure, configure todos los miembros de la granja de servidores de Windows Server AD FS hello en hello mismo servicio en la nube y usar Hola equilibrio de carga capacidad de Azure para (el valor predeterminado es 80) puertos HTTP y HTTPS (el valor predeterminado es 443). Para obtener más información, consulte [Azure load-balancer probe](https://msdn.microsoft.com/library/azure/jj151530)(Sondeo de equilibrador de carga de Azure).
> No se admite el equilibrio de carga de red (NLB) de Windows Server en Azure.
> 
> 

