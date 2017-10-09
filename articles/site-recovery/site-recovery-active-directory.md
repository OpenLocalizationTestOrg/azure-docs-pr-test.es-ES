---
title: aaaProtect Active Directory y DNS con Azure Site Recovery | Documentos de Microsoft
description: "Este artículo se describe cómo tooimplement una solución de recuperación ante desastres para Active Directory con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Protección de Active Directory y DNS con Azure Site Recovery
Las aplicaciones empresariales como SharePoint, Dynamics AX y SAP dependen de Active Directory y un toofunction de infraestructura DNS correctamente. Cuando se crea una solución de recuperación ante desastres para las aplicaciones, es importante tooremember que necesita tooprotect y recuperación de Active Directory y DNS antes de hello otros componentes de la aplicación, tooensure que cosas funcionan correctamente cuando se produce un desastre.

Site Recovery es un servicio de Azure que proporciona funcionalidades de recuperación ante desastres mediante la organización de la replicación, la conmutación por error y la recuperación de máquinas virtuales. Recuperación de sitio admite una serie de escenarios de replicación tooconsistently proteger y sin problemas en las nubes de tooprivate, pública o proveedor de hospedaje de máquinas virtuales y las aplicaciones de conmutación por error.

Con Site Recovery, puede crear un plan completo de recuperación ante desastres automatizada para Active Directory. En el momento en el que se produce una interrupción, puede iniciar la conmutación por error en segundos desde cualquier lugar y hacer que Active Directory vuelva a funcionar en unos minutos. Si ha implementado Active Directory para varias aplicaciones, como SharePoint y SAP en el sitio principal, y desea toofail sobre sitio completo hello, puede producir un error a través de Active Directory primero mediante Site Recovery y, a continuación, conmutar por error Hola otras aplicaciones uso de planes de recuperación específica de la aplicación.

Este artículo explica cómo toocreate una solución de recuperación ante desastres para Active Directory, cómo tooperform planeada, no planeada y las conmutaciones por error de prueba con un plan de recuperación de un solo clic, Hola configuraciones admitidas y requisitos previos.  Debe estar familiarizado con Active Directory y Azure Site Recovery antes de empezar.

## <a name="replicating-domain-controller"></a>Replicación de controlador de dominio

Necesita toosetup [replicación de Site Recovery](#enable-protection-using-site-recovery) en al menos una máquina virtual que hospeda el controlador de dominio y DNS. Si tiene [varios controladores de dominio](#environment-with-multiple-domain-controllers) en su entorno, además tooreplicating Hola máquina de virtual de controlador de dominio con la recuperación de sitio también podría tener tooset hasta un [delcontroladordedominioadicional](#protect-active-directory-with-active-directory-replication) en el sitio de destino de hello (Azure o un centro de datos local secundario). 

### <a name="single-domain-controller-environment"></a>Entorno con un solo controlador de dominio
Si tiene algunas aplicaciones y un controlador de dominio único y desea toofail sobre todo el sitio Hola juntos, le recomendamos con controladores de dominio de Site Recovery tooreplicate hello toohello de sitio secundario (si está conmuta tooAzure o sitio secundario de tooa). Hello mismo replicado puede utilizarse la máquina virtual de controlador/DNS para el dominio [probar conmutación por error](#test-failover-considerations) así.

### <a name="environment-with-multiple-domain-controllers"></a>Entorno con varios controladores de dominio
Si tiene muchas aplicaciones y hay más de un controlador de dominio en el entorno de Hola o si tiene previsto toofail sobre algunas aplicaciones a la vez, se recomienda que además tooreplicating controlador de dominio de hello virtual automático con Site Recovery se también configurar un [controlador de dominio adicional](#protect-active-directory-with-active-directory-replication) en el sitio de destino de hello (Azure o un centro de datos local secundario). Para [probar conmutación por error](#test-failover-considerations), utilice el controlador de dominio replicada Site Recovery y de conmutación por error, controlador de dominio adicional de hello en el sitio de destino de Hola. 


Hello siguientes secciones se explica cómo tooenable protección para un controlador de dominio en la recuperación del sitio y cómo tooset un controlador de dominio en Azure.

## <a name="prerequisites"></a>Requisitos previos
* Una implementación local del servidor DNS y Active Directory.
* Un almacén de los servicios de Azure Site Recovery en una suscripción de Microsoft Azure.
* Si replica tooAzure, ejecute la herramienta de evaluación de preparación de máquina Virtual de Azure de hello en tooensure de máquinas virtuales que son compatibles con máquinas virtuales de Azure y servicios de Azure Site Recovery.

## <a name="enable-protection-using-site-recovery"></a>Habilitación de la protección con Site Recovery
### <a name="protect-hello-virtual-machine"></a>Proteger la máquina virtual de Hola
Habilitar la protección de máquina virtual controlador/DNS del dominio hello en Site Recovery. Configurar opciones de recuperación del sitio en función de tipo de máquina virtual de hello (Hyper-V o VMware). controlador de dominio de Hello replicada con Site Recovery se utiliza para [probar conmutación por error](#test-failover-considerations). Asegúrese de que cumple Hola según los requisitos:

1. controlador de dominio de Hello es un servidor de catálogo global
2. controlador de dominio de Hello debe ser propietario de la función FSMO Hola para los roles que serán necesarias durante una conmutación por error de prueba (lo contrario, estas funciones necesitará toobe [confiscado](http://aka.ms/ad_seize_fsmo) después de la conmutación por error de hello)

### <a name="configure-virtual-machine-network-settings"></a>Configuración de los valores de red de la máquina virtual
Para DNS/controlador de dominio Hola máquina virtual, configurar opciones de red en Site Recovery para que Hola podrá máquina virtual toohello adjunto de red apropiado después de la conmutación por error. 

![Configuración de red de máquina virtual](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Protección de Active Directory con la replicación de Active Directory
### <a name="site-to-site-protection"></a>Protección de sitio a sitio
Crear un controlador de dominio en el sitio secundario de Hola. Cuando se promueve la función de controlador de dominio de hello server tooa, especifique el nombre de Hola de hello mismo dominio que se utiliza en el sitio principal de Hola. Puede usar hello **servicios y sitios de Active Directory** tooconfigure configuración de vínculo a sitios Hola se agregan sitios de hello toowhich del objeto de complemento. Al configurar los valores en un vínculo de sitio, puede controlar cuándo se produce la replicación entre dos o más sitios y con qué frecuencia se produce. Para más información, consulte [Programación de la replicación entre sitios](https://technet.microsoft.com/library/cc731862.aspx).

### <a name="site-to-azure-protection"></a>Protección del sitio en Azure
Siga las instrucciones de hello demasiado[crear un controlador de dominio en una red virtual de Azure](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). Cuando se promueve la función de controlador de dominio de hello server tooa, especifique Hola mismo nombre de dominio que se usa en el sitio primario de Hola.

A continuación, [volver a configurar el servidor DNS de hello para la red virtual de hello](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), servidor DNS de hello toouse en Azure.

![Red de Azure](./media/site-recovery-active-directory/azure-network.png)

**DNS en la red de producción de Azure**

## <a name="test-failover-considerations"></a>Consideraciones sobre la conmutación por error de prueba
La conmutación por error de prueba se produce en una red que está aislada de la red de producción para que no haya impacto alguno en la carga de trabajo de producción.

Mayoría de las aplicaciones también requiere la presencia de Hola de un controlador de dominio y un toofunction de servidor DNS. Por lo tanto, antes de que se conmuta la aplicación hello, un controlador de dominio debe toobe creado en hello aislamiento de red toobe utilizado para la conmutación por error. Hola toodo de manera más sencilla es tooreplicate una máquina virtual de controlador/DNS de dominio con Site Recovery. A continuación, ejecute una conmutación por error de prueba de la máquina virtual de controlador de hello dominio antes de ejecutar una conmutación por error de prueba del plan de recuperación de Hola para la aplicación hello. Así es cómo debe hacerlo:

1. [Replicar](site-recovery-replicate-vmware-to-azure.md) Hola máquina virtual controlador/DNS del dominio con Site Recovery.
1. Cree una red aislada. Cualquier red virtual que se cree en Azure de forma predeterminada está aislada de otras redes. Se recomienda que el intervalo de direcciones IP de Hola para esta red sea igual que el de la red de producción. No habilite la conectividad de sitio a sitio en esta red.
1. Proporcione una dirección IP de DNS de red Hola creado, como la dirección IP de Hola que espera tooget de máquina virtual de hello DNS. Si replica tooAzure, proporcione direcciones IP de Hola de hello máquina virtual que se utiliza en la conmutación por error en **IP de destino** en **proceso y red** configuración. 

    ![IP de destino](./media/site-recovery-active-directory/DNS-Target-IP.png)**IP de destino**

    ![Red de prueba de Azure](./media/site-recovery-active-directory/azure-test-network.png)

    **DNS en la red de prueba de Azure**

> [!TIP]
> Máquinas virtuales de prueba toocreate en una subred del mismo nombre de intentos de recuperación de sitio y usar Hola IP misma que la proporcionada en **proceso y red** configuración de máquina virtual de Hola. Si la subred del mismo nombre no está disponible en hello red virtual de Azure proporcionado para la conmutación por error de prueba, máquina virtual de prueba se crea en la primera subred de hello alfabéticamente. Si IP de destino de hello forma parte de hello elegido subred, Site Recovery intenta toocreate Hola prueba de conmutación por error máquina virtual a través Hola IP de destino. Si IP de destino de hello no forma parte de hello elegido subred, máquina virtual de conmutación por error de prueba se crea con cualquier dirección IP disponible en hello elegido subred. 
>
>


1. Si replica tooanother al sitio local y usa DHCP, siga las instrucciones de hello demasiado[la instalación de DNS y DHCP para conmutación por error de prueba](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Realice una conmutación por error de prueba de la máquina de virtual del controlador de dominio de hello ejecutar en la red aislada Hola. Usar más reciente disponible **coherentes con la aplicación** punto de recuperación de hello dominio controlador máquina virtual toodo Hola conmutación por error. 
1. Ejecute una conmutación por error de prueba para el plan de recuperación de Hola que contiene máquinas virtuales de la aplicación hello. 
1. Una vez finalizada, prueba **conmutación por error de prueba de limpieza** en hello máquina de virtual de controlador de dominio. Este paso elimina el controlador de dominio de Hola que se creó para la conmutación por error.


### <a name="removing-reference-tooother-domain-controllers"></a>Quitar controladores de dominio de referencia tooother
Cuando realiza una conmutación por error de prueba, no ponga todos los controladores de dominio de hello en red de prueba de Hola. referencia de hello tooremove de otros controladores de dominio que existen en el entorno de producción, es posible que tenga demasiado[asumir roles FSMO Active Directory](http://aka.ms/ad_seize_fsmo) y realice [la limpieza de metadatos](https://technet.microsoft.com/library/cc816907.aspx) para le falta el dominio controladores. 



> [!IMPORTANT]
> Algunas de las configuraciones de Hola que se describe en los pasos de la sección de hello no son configuraciones de controlador de dominio de hello estándar de forma predeterminada. Si no desea que toomake que estos controlador de dominio de producción de cambios tooa; a continuación, puede crear un toobe dedicado de controlador de dominio utilizado para la recuperación de sitio de conmutación por error de prueba y realice estos cambios toothat.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Problemas debidos a las medidas de seguridad de la virtualización 

A partir de Windows Server 2012, [se han integrado medidas de seguridad adicionales en Active Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Estas medidas de seguridad ayudan a proteger los controladores de dominio virtualizado frente reversiones de USN, como plataforma de hipervisor de hello subyacente admita VM-GenerationID. Azure admite VM-GenerationID, lo que significa que los controladores de dominio que ejecutan Windows Server 2012 o posterior en Azure máquinas virtuales tienen medidas de seguridad adicionales de Hola. 


Cuando se restablece el VM-GenerationID hello, también se restablece el invocationID Hola de base de datos de hello AD DS, se descarta Hola grupo RID y SYSVOL se marca como no autoritativo. Para obtener más información, consulte [Introducción tooActive virtualización de servicios de dominio de Directory](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) y [virtualización segura de DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

Conmutar por error tooAzure puede causar restablecer de VM-GenerationID y que se inicia en medidas de seguridad adicionales de hello cuando se inicia Hola máquina de virtual de controlador de dominio en Azure. Esto puede dar lugar a un **un retraso importante** de usuario que se va a la máquina de virtual del controlador de dominio de toologin puede toohello. Puesto que este controlador de dominio se utilizaría solo en una conmutación por error de prueba, las medidas de seguridad de virtualización no son necesarias. tooensure que VM-GenerationID de máquina de virtual del controlador de dominio de hello no cambia, a continuación, se puede cambiar el valor de Hola de too4 DWORD siguientes en el controlador de dominio local de Hola.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Síntomas de las medidas de seguridad de la virtualización
 
Si se han tomado medidas de seguridad de virtualización después de una conmutación por error de prueba, podría ver uno o varios de los síntomas siguientes:  

Cambio del Id. de generación

![Cambio del Id. de generación](./media/site-recovery-active-directory/Event2170.png)

Cambio del Id. de invocación

![Cambio del Id. de invocación](./media/site-recovery-active-directory/Event1109.png)

Recursos compartidos de Sysvol y Netlogon no disponibles

![Recurso compartido Sysvol](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

Bases de datos DFSR eliminadas

![Base de datos de DFSR eliminada](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Algunas de las configuraciones de Hola que se describe en los pasos de la sección de hello no son configuraciones de controlador de dominio de hello estándar de forma predeterminada. Si no desea que toomake que estos controlador de dominio de producción de cambios tooa; a continuación, puede crear un toobe dedicado de controlador de dominio utilizado para la recuperación de sitio de conmutación por error de prueba y realice estos cambios toothat.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Solución de los problemas de controlador de dominio durante la conmutación por error de prueba


En un símbolo del sistema, ejecute hello después toocheck comando si comparten carpetas SYSVOL y NETLOGON:

    NET SHARE

En el símbolo de hello, ejecute hello siguiente comando tooensure que Hola de controlador de dominio está funcionando correctamente.

    dcdiag /v > dcdiag.txt

En el registro de salida de hello, busque tooconfirm texto siguiente que Hola de controlador de dominio está funcionando bien. 

* "passed test Connectivity"
* "passed test Advertising"
* "passed test MachineAccount"

Si hello condiciones anteriores se cumplen, es probable que ese controlador de dominio de hello está funcionando bien. En caso contrario, realice estos pasos.


* Realizar una restauración autoritativa del controlador de dominio de Hola.
    * Aunque es [no recomienda la replicación FRS toouse](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), pero si todavía está utilizando, siga los pasos de hello proporciona [aquí](https://support.microsoft.com/kb/290762) toodo una restauración autoritativa. Puede obtener más información acerca de Burflags comentado en el vínculo anterior de hello [aquí](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * Si está utilizando la replicación DFSR, a continuación, siga pasos Hola disponibles [aquí](https://support.microsoft.com/kb/2218556) toodo una restauración autoritativa. También puede usar las funciones de Powershell disponibles [aquí](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/). 
    
* Omitir el requisito de sincronización inicial estableciendo después too0 de clave del registro en el controlador de dominio local de Hola. Si esta DWORD no existe, créela en el nodo "Parameters". Puede leer más sobre este tema [aquí](https://support.microsoft.com/kb/2001093).

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Deshabilitar el requisito de Hola que un servidor de catálogo global está disponible toovalidate inicio de sesión de usuario estableciendo después too1 de clave del registro en el controlador de dominio local de Hola. Si esta DWORD no existe, créela en el nodo "Lsa". Puede leer más sobre este tema [aquí](http://support.microsoft.com/kb/241789).

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>DNS y controlador de dominio en equipos diferentes
Si DNS no está en hello misma máquina virtual como controlador de dominio de hello, deberá toocreate una VM de DNS para la conmutación por error de prueba de Hola. Si encuentra en Hola misma máquina virtual, puede omitir esta sección.

Puede usar un nuevo servidor DNS y crear todas las zonas de hello necesario. Por ejemplo, si el dominio de Active Directory es contoso.com, puede crear una zona DNS con hello nombre contoso.com. las entradas de Hello correspondientes tooActive directorio deben actualizarse en DNS, como se indica a continuación:

1. Asegúrese de que estos valores están en vigor antes de cualquier otra máquina virtual en el plan de recuperación de hello aparece:
   
   * zona de Hello debe denominarse después el nombre de raíz del bosque de Hola.
   * zona de Hello debe estar basado en archivos.
   * Hola zona debe estar habilitada para actualizaciones seguras y no seguras.
   * resolución de Hola de máquina virtual de controlador de hello dominio debe apuntar toohello dirección IP de la máquina virtual de hello DNS.
2. Ejecute el siguiente comando en la máquina virtual de controlador de dominio de hello:
   
    `nltest /dsregdns`
3. Agregar una zona en el servidor DNS de hello, permitir actualizaciones no seguras y agregue una entrada para él tooDNS:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Pasos siguientes
Lectura [¿qué cargas de trabajo se debe proteger?](site-recovery-workload.md) toolearn más sobre la protección de cargas de trabajo empresariales con Azure Site Recovery.

