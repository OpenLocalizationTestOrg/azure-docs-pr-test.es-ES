---
title: "máquinas virtuales de VMware aaaReplicate y tooAzure de servidores físicos en Hola portal clásico | Documentos de Microsoft"
description: "Este artículo describe cómo la replicación de tooorchestrate de Azure Site Recovery toodeploy, conmutación por error y recuperación de local de máquinas virtuales de VMware y tooAzure de servidores físicos de Windows o Linux."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>Replicar máquinas virtuales de VMware y servidores físicos tooAzure con Azure Site Recovery
> [!div class="op_single_selector"]
> * [Hola portal de Azure](site-recovery-vmware-to-azure.md)
> * [portal clásico de Hola](site-recovery-vmware-to-azure-classic.md)
> * [portal clásico de Hello (heredado)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Hola servicio Azure Site Recovery contribuye tooyour la continuidad del negocio y estrategia de recuperación (BCDR) mediante la coordinación de replicación, la conmutación por error y la recuperación de máquinas virtuales y servidores físicos. Equipos pueden ser replicada tooAzure o centro de datos local secundario tooa. Para obtener una introducción rápida, lea [¿Qué es Azure Site Recovery?](site-recovery-overview.md).

## <a name="overview"></a>Información general
En este artículo se describe cómo:

* **Replicar tooAzure de máquinas virtuales de VMware**: replicación de toocoordinate de implementar recuperación del sitio, la conmutación por error y la recuperación de almacenamiento de tooAzure de máquinas virtuales de VMware en local.
* **Replicar servidores físicos tooAzure**: replicación de toocoordinate de implementar Azure Site Recovery, la conmutación por error y la recuperación de local físico Windows y Linux servidores tooAzure.

> [!NOTE]
> Este artículo se describe cómo tooreplicate tooAzure. Si desea tooreplicate máquinas virtuales de VMware o de Windows/Linux servidores físicos tooa centro de datos secundario, consulte [tooVMware de VMware de recuperación del sitio](site-recovery-vmware-to-vmware.md).
>
>

Enviar comentarios o preguntas en parte inferior de este artículo o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Implementación mejorada
Este artículo incluye instrucciones para una implementación mejorada en hello portal de Azure clásico. Se recomienda que utilice esta versión para todas las implementaciones nuevas. Si ya ha implementado por utilizando Hola anterior versión heredada, se recomienda que migre toohello nueva versión. Para obtener más información acerca de la migración, consulte [VMware de recuperación de sitio tooAzure clásico heredado](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

implementación de Hello mejorada es una actualización importante. Este es un resumen de las mejoras de Hola que hemos realizado:

* **Infraestructura de máquinas virtuales en Azure**: los datos replican directamente tooan cuenta de almacenamiento de Azure. Además, no hay ninguna tooset necesidad de configurar las máquinas virtuales de infraestructura (como servidor de configuración o el servidor de destino maestro) para la replicación y conmutación por error que se considere necesarias en la implementación heredada de Hola.  
* **Instalación unificada**: una instalación única proporciona configuración y escalabilidad únicas para los componentes locales.
* **Implementación segura**: se cifra todo el tráfico y las comunicaciones de administración se envían a través de HTTPS 443.
* **Puntos de recuperación**: compatibilidad con puntos de recuperación coherentes tras bloqueo y coherentes con la aplicación para entornos de Windows y Linux, además de compatibilidad con configuraciones coherentes con una sola máquina virtual y con varias máquinas virtuales.
* **Probar la conmutación por error**: compatibilidad con tooAzure de conmutación por error de prueba no provocan interrupciones sin afectar a la producción o interrumpir la replicación.
* **Conmutación por error imprevista**: compatibilidad con conmutación por error imprevista tooAzure con un tooautomatically mejorada opción apaga las máquinas virtuales antes de conmutación por error.
* **Conmutación por recuperación**: conmutación por recuperación integrada que se replica sólo los cambios delta realizar copia de toohello sitio local.
* **vSphere 6.0**: compatibilidad limitada para las implementaciones de VMware vSphere 6.0.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>¿De qué manera Site Recovery ayuda a proteger máquinas virtuales y servidores virtuales?
* Los administradores de VMware pueden configurar fuera de las medidas de seguridad tooprotect Azure de cargas de trabajo de negocio y aplicaciones que se ejecutan en máquinas virtuales de VMware. Los administradores de servidores pueden replicar tooAzure de servidores de Windows y Linux física local.
* consola de Azure Site Recovery Hola proporciona una única ubicación para el programa de instalación simple y la administración de replicación, conmutación por error y los procesos de recuperación.
* Si replica máquinas virtuales de VMware administradas por un servidor de vCenter, Site Recovery puede detectar automáticamente esas máquinas virtuales. Si los equipos están en un host ESXi, Site Recovery detecta las máquinas virtuales en host Hola.
* Si ejecuta las conmutaciones por error sencilla desde su tooAzure de infraestructura local, puede no hacer copia de (restore) de los servidores VM de Azure tooVMware de sitio local de Hola.
* Puede configurar planes de recuperación que agrupen las cargas de trabajo de aplicaciones organizadas en niveles en distintas máquinas. Si la conmutación por error esos planes, Site Recovery proporciona coherencia entre varias VM para que máquinas que se ejecutan Hola mismas cargas de trabajo se pueden recuperar juntos tooa punto de datos coherente.

## <a name="supported-operating-systems"></a>Sistemas operativos compatibles
### <a name="windows-64-bit-only"></a>Windows (solo 64 bits)
* Windows Server 2008 R2 SP1 y versiones posteriores
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (solo 64 bits)
* Red Hat Enterprise Linux 6.7, 7.1 y 7.2
* CentOS 6.5, 6.6, 6.7, 7.0, 7.1 y 7.2
* Kernel compatible de Oracle Enterprise Linux 6.4 y 6.5 ejecuta cualquier Red Hat de Hola o separable Enterprise Kernel versión 3 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>Arquitectura del escenario
Componentes del escenario:

* **Un servidor de administración local**: servidor de administración de hello ejecuta los componentes de Site Recovery:
  * **Servidor de configuración**: coordina la comunicación y administra los procesos de replicación y recuperación de datos.
  * **Servidor de procesos**: actúa como una puerta de enlace de replicación. Recibe datos de máquinas de origen protegido; optimiza con almacenamiento en caché, la compresión y cifrado; y el almacenamiento de tooAzure de datos de replicación de envíos. También controla la instalación de inserción de las máquinas de tooprotected de servicio de movilidad y realiza la detección automática de máquinas virtuales de VMware.
  * **Servidor de destino maestro**: controla los datos de replicación durante la conmutación por recuperación desde Azure.
    También puede implementar un servidor de administración que actúa como un tooscale de servidor de proceso su implementación.
* **servicio de movilidad de Hola**: este componente se implementa en cada máquina (VM de VMware o servidor físico) que desea tooreplicate tooAzure. Captura escrituras de datos en la máquina de Hola y reenvía el servidor de procesos de toohello.
* **Azure**: no es necesario toocreate las máquinas virtuales de Azure toohandle replicación y la conmutación por error. Hola servicio Site Recovery controla la administración de datos y los datos replican directamente tooAzure almacenamiento. Máquinas virtuales replicadas de Azure se active automáticamente cuando se produce la conmutación por error tooAzure. Sin embargo, si desea toofail de sitio de Azure toohello local, deberá tooset una tooact de una máquina virtual de Azure como un servidor de procesos.

Hola siguiente gráfico (creado por Henry Robalino) muestra cómo interactúan estos componentes:

![Arquitectura de componentes](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Planificación de capacidad
Al planear la capacidad, esto es lo necesita toothink sobre:

* **entorno de origen Hola**: planificación o hello VMware infraestructura y origen de máquina requisitos de capacidad.
* **servidor de administración de Hola**: planeación para hello local de servidores de administración que se ejecutan los componentes de Site Recovery.
* **Ancho de banda de red de origen tootarget**: planeación de ancho de banda de red necesario para la replicación entre el origen de Hola y Azure.

### <a name="source-environment-considerations"></a>Consideraciones sobre el entorno de origen
* **Frecuencia diaria de cambios máxima**: un equipo protegido solo puede utilizar un único servidor de procesos. Puede administrar un servidor de proceso único seguridad too2 TB de datos cambia al día. Por lo tanto, 2 TB es datos diario máximo Hola cambian tasa con la que se admite para un equipo protegido.
* **Rendimiento máximo**: un equipo replicado puede pertenecer tooone cuenta de almacenamiento de Azure. Una cuenta de almacenamiento estándar puede contener un máximo de 20.000 solicitudes por segundo, y se recomienda que mantenga el número de Hola de e/s por segundo a través de un too20 de la máquina de origen, 000. Por ejemplo, si tiene una máquina de origen con 5 discos y cada disco genera 120 IOPS (tamaño de 8 KB) en el origen de hello, resultará en hello Azure por límite de IOPS de disco de 500. Hola número de cuentas de almacenamiento necesario = origen total de IOPs/20 000.

### <a name="management-server-considerations"></a>Consideraciones sobre el servidor de administración
servidor de administración de Hello ejecuta los componentes de Site Recovery que administran la optimización de datos, replicación y administración. Debe ser capacidad de tasa de cambio diaria de toohandle capaz de hello en todas las cargas de trabajo que ejecutan en equipos protegidos y tiene toocontinuously de ancho de banda suficiente replicar tooAzure el almacenamiento de datos. Concretamente:

* servidor de procesos de Hello recibe datos de replicación de máquinas protegidas y optimiza con almacenamiento en caché, la compresión y cifrado antes de enviarlo tooAzure. servidor de administración de Hello debe tener suficientes tooperform de recursos de estas tareas.
* servidor de procesos de Hello usa caché basada en disco. Se recomienda un disco independiente de memoria caché de 600 GB o más cambios de datos de toohandle almacenados en caso de hello de cuello de botella de red o una interrupción. Durante la implementación, puede configurar caché hello en cualquier unidad que tenga al menos 5 GB de almacenamiento disponible, pero 600 GB es la recomendación mínimo de Hola.
* Como práctica recomendada, se recomienda que se encuentra dicho servidor de administración de hello en hello misma red y el segmento de LAN como Hola máquinas que desee tooprotect. Se puede encontrarse en una red diferente, pero las máquinas que desee tooprotect debe tener tooit de visibilidad de red L3.

En hello en la tabla siguiente se resumen las recomendaciones de tamaño para el servidor de administración de hello:

| **CPU del servidor de administración** | **Memoria** | **Tamaño del disco de caché** | **Frecuencia de cambio de datos** | **Máquinas protegidas** |
| --- | --- | --- | --- | --- |
| 8 vCPU (2 sockets * 4 núcleos @ 2,5 GHz) |16 GB |< 300 GB |500 GB o menos |Implementar un servidor de administración con estos tooreplicate configuración menos de 100 equipos. |
| 12 vCPUs (2 sockets * 6 núcleos @ 2,5 GHz) |18 GB |600 GB |500 GB too1 TB |Implementar un servidor de administración con estas máquinas de 100 a 150 tooreplicate de configuración. |
| 16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz) |32 GB |1 TB |1 TB too2 TB |Implementar un servidor de administración con estas máquinas de entre 150 y 200 tooreplicate de configuración. |
| Implementar otro servidor de procesos | | |2 TB |Implementar servidores de procesos adicionales si se están replicando más de 200 máquinas o si cambian los datos diario de hello tasa mayor que 2 TB. |

Donde:

* Cada máquina de origen está configurada con 3 discos de 100 GB cada una.
* Usamos almacenamiento de pruebas comparativas de 8 unidades SAS de 10 000 RPM con RAID 10 para las mediciones de disco de caché.

### <a name="network-bandwidth-from-source-tootarget"></a>Ancho de banda de red de origen tootarget
Asegúrese de que calcular el ancho de banda de Hola que sería necesario para la replicación inicial y replicación de datos mediante el uso de hello [herramienta de planificación de capacidad](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Limitación del ancho de banda usado para la replicación
VMware tráfico replican tooAzure pasa por un servidor de proceso específico. Puede limitar el ancho de banda de Hola que está disponible para la replicación de Site Recovery en el servidor como se indica a continuación:

1. Abra hello en el complemento MMC de copias de seguridad de Microsoft Azure en el servidor de administración principal de Hola o en un servidor de administración ejecuta adicionales aprovisiona servidores de procesos. De forma predeterminada, se crea un acceso directo para copia de seguridad de Microsoft Azure en el escritorio de Hola. También se encuentra en C:\Archivos de programa\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. En el complemento de hello, haga clic en **cambiar las propiedades de**.

    ![Cambio de propiedades para limitar ancho de banda](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. En hello **limitación** ficha, especifique el ancho de banda de Hola que puede usarse para la replicación de Site Recovery y Hola programación aplicable.

    ![Limitación de ancho de banda para replicación](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

También puede definir la limitación con PowerShell. Este es un ejemplo:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Maximización del uso del ancho de banda
tooincrease Hola ancho de banda utilizado para la replicación por Azure Site Recovery, deberá toochange una clave del registro.

Hello controles de tecla siguientes Hola número de subprocesos por replicar el disco que se utilizan cuando se replican:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 En una red sobreaprovisionada, esta clave del registro debe toobe cambiado sus valores predeterminados. Se admite un máximo de 32.  

Para más información acerca de la planeación de capacidad detallada, consulte [Site Recovery Capacity Planner](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Servidores de procesos adicionales
Si necesita tooprotect más de 200 máquinas o la tasa de cambio diaria es mayor que 2 TB, puede agregar servidores adicionales toohandle Hola carga. tooscale out, puede:

* Aumentar el número de Hola de servidores de administración. Por ejemplo, puede proteger las máquinas de too400 con dos servidores de administración.
* Agregar servidores de proceso adicionales y utilizar dichos servidores de administración de toohandle tráfico en lugar de (o además) Hola.

Esta tabla describe un escenario en el cual:

* Configurar toouse del servidor de administración original de hello porque sólo un servidor de configuración.
* Configura un servidor de procesos adicional.
* Configurar servidor de proceso adicional de máquinas virtuales protegidas toouse Hola.
* Cada máquina de origen protegida está configurada con tres discos de 100 GB cada uno.

| **Servidor de administración original**<br/><br/>(servidor de configuración) | **Servidores de procesos adicionales** | **Tamaño del disco de caché** | **Frecuencia de cambio de datos** | **Máquinas protegidas** |
| --- | --- | --- | --- | --- |
| 8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 16 GB de RAM |4 vCPU (2 sockets * 2 núcleos a 2,5 GHz), 8 GB de RAM |< 300 GB |250 GB o menos |Puede replicar 85 máquinas o menos. |
| 8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 16 GB de RAM |8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 12 GB de RAM |600 GB |250 GB too1 TB |Puede replicar entre 85 y 150 máquinas. |
| 12 vCPU (2 sockets * 6 núcleos a 2,5 GHz), 18 GB de RAM |12 vCPU (2 sockets * 6 núcleos a 2,5 GHz), 24 GB de RAM |1 TB |1 TB too2 TB |Puede replicar entre 150 y 225 máquinas. |

La forma de escalar los servidores depende de si prefiere un modelo de escalado vertical u horizontal. Para escalar verticalmente, implementa algunos servidores de procesos y administración de alto nivel, mientras que, para escalar horizontalmente, implementa más servidores con menos recursos. Por ejemplo: si necesita tooprotect 220 máquinas, puede hacer cualquiera de hello siguientes:

* Configurar el servidor de administración original de hello con 12 vCPU y 18 GB de RAM. Configure un servidor de procesos adicional con 12 vCPU y 24 GB de RAM. Configurar servidor de proceso adicional de máquinas protegidas toouse solo Hola.
* Configurar dos servidores de administración (vCPU, 16 GB de RAM de 2 x 8) y dos servidores de proceso adicionales (vCPU y 4vCPUs x 1 toohandle 135 + 85 a (220) máquinas 1 x 8). Configurar servidores de procesos adicionales de hello solo de las máquinas protegidas toouse.

Siga las instrucciones de hello en [implementar servidores de procesos adicionales](#deploy-additional-process-servers) tooset de un servidor de proceso adicionales.

## <a name="before-you-start-deployment"></a>Antes de comenzar la implementación
Hello en las tablas siguientes resumen los requisitos previos de Hola para implementar este escenario.

### <a name="azure-prerequisites"></a>Requisitos previos de Azure
| **Requisito previo** | **Detalles** |
| --- | --- |
| **Cuenta de Azure** |Necesita una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). Para más información sobre los precios de Site Recovery, consulte [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Almacenamiento de Azure** |Necesita un toostore replicado de datos de la cuenta de almacenamiento de Azure. Los datos replicados se almacenan en Azure Storage y las máquinas virtuales de Azure se ponen en marcha cuando se produce la conmutación por error. <br/><br/>Necesita una [cuenta de almacenamiento con redundancia geográfica de tipo estándar](../storage/storage-redundancy.md#geo-redundant-storage). cuenta de Hello debe estar en Hola misma región que Hola servicio Site Recovery y estar asociado con hello misma suscripción. Cuentas de almacenamiento de toopremium de replicación no se admite actualmente y no deben usarse.<br/><br/>No se admite mover las cuentas de almacenamiento creadas mediante hello [portal de Azure](../storage/storage-create-storage-account.md) en grupos de recursos. Para obtener más información, consulte [Introducción tooMicrosoft almacenamiento de Azure](../storage/storage-introduction.md).<br/><br/> |
| **Red de Azure** |Se necesita una red virtual de Azure que se conectarán las máquinas virtuales de Azure se produce la conmutación por error de toowhen. red virtual de Azure Hello debe ser una Hola misma región que el almacén de Site Recovery Hola.<br/><br/>toofail al tooAzure de conmutación por error, se necesita una VPN de conexión (o ExpressRoute de Azure) configurar desde el sitio local de hello Azure red toohello. |

### <a name="on-premises-prerequisites"></a>Requisitos previos locales
| **Requisito previo** | **Detalles** |
| --- | --- |
| **Servidor de administración** |Necesita un servidor local con Windows 2012 R2 que se ejecute en una máquina virtual o en un servidor físico. Todos los componentes de Site Recovery local Hola de están instalados en este servidor de administración.<br/><br/> Se recomienda que implementar servidor hello como una VM de VMware de alta disponibilidad. Sitio de conmutación por recuperación toohello local de Azure siempre es tooVMware las máquinas virtuales, independientemente de si ha conmutado por error las máquinas virtuales o servidores físicos. Si no configura el servidor de administración de hello como una VM de VMware, deberá tooset de un servidor de destino maestro independiente como un tráfico de conmutación por recuperación de tooreceive de VM de VMware.<br/><br/>servidor de Hello no debería ser un controlador de dominio.<br/><br/>servidor de Hello debe tener una dirección IP estática.<br/><br/>nombre de host de Hello del servidor de hello debe ser de 15 caracteres o menos.<br/><br/>configuración regional del sistema operativo de Hello debe estar en inglés solamente.<br/><br/>servidor de administración de Hello requiere acceso a Internet.<br/><br/>Necesita acceso de salida de servidor hello como sigue: acceso temporal en 80 HTTP durante la instalación de componentes de Site Recovery hello (toodownload MySQL); acceso de salida en curso en HTTPS 443 para la administración de replicación; en curso acceso de salida en 9443 HTTPS para el tráfico de replicación (se puede modificar este puerto).<br/><br/> Asegúrese de que estas direcciones URL son accesibles desde el servidor de administración de hello: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>- https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.MySQL.com/Get/Archives/MySQL-5.5/MySQL-5.5.37-Win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Si tiene reglas de firewall basado en la dirección IP en el servidor de hello, compruebe que las reglas de hello permiten tooAzure de comunicación. Necesita hello tooallow [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653) y Hola puerto HTTPS (443). También necesarios toowhitelist los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos. dirección URL de Hello [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") es para la descarga de MySQL. |
| **VMware vCenter/host ESXi** |Es necesario que uno o más VMware vSphere ESX/ESXi hipervisores administrar las máquinas virtuales de VMware, ejecutando ESX/ESXi versión 5.1, 5.5 o 6.0 con las últimas actualizaciones de Hola.<br/><br/> Se recomienda implementar un toomanage de servidor VMware vCenter los hosts de ESXi. Se debería estar ejecutando vCenter versión 6.0 o 5.5 con las actualizaciones más recientes de Hola.<br/><br/>Tenga en cuenta que Site Recovery no admite las nuevas características de vCenter y vSphere 6.0, como Cross vCenter vMotion, volúmenes virtuales y DRS de almacenamiento. Soporte de recuperación del sitio es toofeatures limitado que también estaban disponibles en la versión 5.5. |
| **Máquinas protegidas** |**Las tablas de Azure**<br/><br/>Equipos que desee tooprotect debe cumplir con los [requisitos previos de Azure](site-recovery-prereq.md) para crear máquinas virtuales de Azure.<br><br/>Si desea tooconnect toohello máquinas virtuales de Azure después de la conmutación por error, deberá tooenable conexiones a Escritorio remoto en el firewall local Hola.<br/><br/>La capacidad de disco individual en máquinas protegidas no debe ser superior a 1023 GB. Una máquina virtual puede tener los discos de too64 (lo que arriba too64 TB). Si tiene discos con una capacidad mayor que 1 TB, considere la posibilidad de usar una replicación de base de datos, como Oracle Data Guard o SQL Server AlwaysOn.<br/><br/>Mínimo 2 GB de espacio disponible en la unidad de instalación de Hola de instalación de componentes.<br/><br/>No se admiten clústeres de invitados de disco compartido. Si tiene una implementación en clúster, considere la posibilidad de usar una replicación de base de datos, como Oracle Data Guard o SQL Server AlwaysOn.<br/><br/>No se admite el arranque de Unified Extensible Firmware Interface (UEFI)/Extensible Firmware Interface (EFI).<br/><br/>Los nombres de las máquinas deben tener entre 1 y 63 caracteres (letras, números y guiones). nombre de Hello debe empezar con una letra o un número y terminar por una letra o un número. Después de proteger un equipo, puede modificar Hola nombres de Azure.<br/><br/>**Máquinas virtuales de VMware**<br/><br>Necesita tooinstall VMware vSphere PowerCLI 6.0. en el servidor de administración de hello (servidor de configuración).<br/><br/>Máquinas virtuales de VMware que desee tooprotect debe tener instalado y ejecutar las herramientas de VMware.<br/><br/>Si una VM de origen hello tiene la formación de equipos, se convierte tooa único NIC después tooAzure de conmutación por error.<br/><br/>Si las máquinas virtuales protegidas tienen un disco iSCSI, Site Recovery convierte Hola protegidos disco iSCSI de máquina virtual en un archivo de disco duro virtual cuando Hola máquina virtual conmuta por error tooAzure. Si el destino iSCSI puede tener acceso mediante hello Azure VM, se conectará tooiSCSI destino y básicamente ver dos discos: disco VHD de hello en disco de iSCSI de origen de máquina virtual de Azure y Hola Hola. En este caso, deberá toodisconnect destino de iSCSI de Hola que aparece en Hola conmutó por error máquinas virtuales de Azure.<br/><br/>Para obtener más información acerca de los permisos de usuario de VMware de hello ese sitio las necesidades de recuperación, consulte [permisos de VMware para el acceso de vCenter](#vmware-permissions-for-vcenter-access).<br/><br/> **Máquinas de Windows Server (en máquina virtual de VMware o servidor físico)**<br/><br/>servidor Hello debe disponer de un sistema operativo de 64 bits admitido: Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2 con al menos SP1.<br/><br/>sistema operativo de Hello debe instalarse en la unidad C y disco del sistema operativo Hola debe ser un disco básico de Windows. (Hola SO no debe estar instalado en un disco dinámico de Windows).<br/><br/>Para las máquinas de Windows Server 2008 R2, debe toohave .NET Framework 3.5.1 instalado.<br/><br/>Necesita una cuenta de administrador de tooprovide (debe ser un administrador local en el equipo de Windows hello) para Hola Hola de instalación de inserción servicio de movilidad en los servidores de Windows. Si Hola proporcionada es una cuenta no es de dominio, deberá toodisable control de acceso de usuarios remotos en el equipo local de Hola. Para obtener más información, consulte [instalar servicio de movilidad de hello con la instalación de inserción](#install-the-mobility-service-with-push-installation).<br/><br/>Site Recovery admite máquinas virtuales con un disco RDM. Durante la conmutación por recuperación, recuperación de sitio volverá a usar el disco RDM Hola si Hola original una VM de origen y el disco RDM están disponibles. Si no están disponibles, durante la conmutación por recuperación, Site Recovery creará un nuevo archivo VMDK para cada disco.<br/><br/>**Equipos Linux**<br/><br/>Necesita un sistema operativo de 64 bits compatible: Red Hat Enterprise Linux 6.7; CentOS 6.5, 6.6 ó 6.7; Oracle Enterprise Linux 6.4 o 6.5 ejecuta kernel compatible de Red Hat de Hola o separable Enterprise Kernel versión 3 (UEK3); SUSE Linux Enterprise Server 11 SP3.<br/><br/>los archivos / etc/hosts en equipos protegidos deben contener entradas que asignan nombre de host local de hello tooIP direcciones asociado con todos los adaptadores de red. <br/><br/>Si desea que tooconnect tooan máquina virtual de Azure ejecutan Linux después de la conmutación por error mediante el uso de un Shell seguro cliente (ssh), asegúrese de que el servicio de Secure Shell de hello en la máquina de hello protegido está establecido toostart automáticamente en el arranque del sistema y que las reglas de firewall permiten un ssh tooit de conexión.<br/><br/>Protección sólo puede habilitarse para las máquinas de Linux con hello después de almacenamiento: filesystem (EXT3, ETX4, ReiserFS, XFS); Dispositivo de software de múltiples rutas asignador (múltiples rutas); Administrador de volúmenes (LVM2). No se admiten servidores físicos con almacenamiento de controlador HP CCISS. sistema de archivos de Hello ReiserFS solo se admite en SUSE Linux Enterprise Server 11 SP3.<br/><br/>Site Recovery admite máquinas virtuales con un disco RDM. Durante la conmutación por recuperación de Linux, Site Recovery no volver a usar el disco RDM Hola. En lugar de eso, crea un nuevo archivo VMDK para cada disco RDM correspondiente. |

Solo para una VM de Linux: asegúrese de establecer configuración de disk.enableUUID=true Hola Hola parámetros de configuración del programa Hola a máquina virtual de VMware. Si la fila no existe, agréguela. Esto es necesario tooprovide una toohello UUID coherente VMDK para que monta correctamente. Sin esta configuración, conmutación por recuperación hará que una descarga completa aunque Hola VM sea de forma local. Si agrega esta opción, garantizará que solo se transfieran los cambios diferenciales durante la conmutación por recuperación.

## <a name="step-1-create-a-vault"></a>Paso 1: Creación de un almacén
1. Inicie sesión en toohello [portal de Azure](https://manage.windowsazure.com/).
2. Expanda **Data Services** > **Recovery Services** y haga clic en **Almacén de Site Recovery**.
3. Haga clic en **Crear nuevo	** > **Creación rápida**.
4. En **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.
5. En **región**, seleccione Hola región geográfica para el almacén de Hola. regiones de toocheck compatibles, consulte [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Haga clic en **Crear almacén**.
    ![Crear almacén](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Compruebe tooconfirm de barra de estado de Hola que Hola almacén se creó correctamente. almacén de Hola se mostrarán como **Active** en hello principal **servicios de recuperación** página.

## <a name="step-2-set-up-an-azure-network"></a>Paso 2: Configuración de una red de Azure
Configurar una red de Azure para que las máquinas virtuales de Azure será tooa conectado red después de la conmutación por error y, por lo que toohello de conmutación por recuperación local sitio puede funcionar según lo esperado.

1. Hola portal de Azure, seleccione **crear red virtual** y especifique el nombre de red de hello, intervalo de direcciones IP y nombre de subred.
2. Si necesita toodo conmutación por recuperación, agregar VPN/ExpressRoute toohello red. Incluso después de la conmutación por error, se pueden agregar toohello red VPN/ExpressRoute.

Para más información sobre redes de Azure, consulte [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Migración de redes](../azure-resource-manager/resource-group-move-resources.md) a través de recursos grupos dentro Hola misma suscripción o en las suscripciones no se admite para las redes usadas para la implementación de Site Recovery.
>
>

## <a name="step-3-install-hello-vmware-components"></a>Paso 3: Instalar componentes de VMware Hola
Si desea que las máquinas virtuales VMware tooreplicate, siga estos pasos en el servidor de administración de hello:

1. [Descargue](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) e instale VMware vSphere PowerCLI 6.0.
2. Reinicie el servidor de Hola.

## <a name="step-4-download-a-vault-registration-key"></a>Paso 4: Descarga de una clave de registro de almacén
1. Hola servidor de administración, abra la consola de recuperación del sitio de hello en Azure. En hello **servicios de recuperación** página, haga clic en Hola de hello almacén tooopen **inicio rápido** página. También puede abrir hello **inicio rápido** página en cualquier momento haciendo clic en el icono de Hola.

    ![Icono de Inicio rápido](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. En hello **inicio rápido** página, haga clic en **preparar recursos de destino** > **descargar una clave de registro**. archivo de registro de Hello se genera automáticamente. Es válido durante 5 días a partir del momento en que se genera.

## <a name="step-5-install-hello-management-server"></a>Paso 5: Instalar el servidor de administración de Hola
> [!TIP]
> Asegúrese de que estas direcciones URL son accesibles desde el servidor de administración de hello:
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. En hello **inicio rápido** página, descargue el servidor de toohello de archivos de instalación unificada de Hola.
2. Ejecute la instalación de toostart de archivo de instalación de Hola Hola **configuración unificado de Site Recovery** asistente.
3. En **antes de comenzar**, seleccione **instalar servidores de configuración de Hola y procesos**.

   ![Antes de empezar](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. En **licencia del Software de terceros**, haga clic en **acepto** toodownload e instalar MySQL.

    ![Software de terceros](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. En **registro**, busque y seleccione la clave de registro de hello que descargó desde el almacén de Hola.

    ![Registro](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. En **configuración de Internet**, especificar cómo conectará los proveedor de Hola que se ejecuta en el servidor de configuración de hello tooAzure Site Recovery a través de Internet de Hola.

   * Seleccione si desea tooconnect con proxy de Hola que actualmente está configurado en el equipo de hello, **conectar con la configuración de proxy existente**.
   * Si desea Hola proveedor tooconnect directamente, seleccione **conectar directamente sin proxy**.
   * Si Hola existente proxy requiere autenticación, o si desea toouse un proxy personalizado para la conexión del proveedor de hello, seleccione **conectar con la configuración de proxy personalizada**.
     * Si usa a un proxy personalizado, necesitará las credenciales, el puerto y dirección de hello toospecify.
     * Si usa a un proxy, debería haber permitido ya hello las siguientes direcciones URL:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Firewall](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. En **comprobación de requisitos previos**, el programa de instalación ejecuta un seguro de que puede ejecutar la instalación de hello toomake de comprobación.

    ![Requisitos previos](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Si aparece una advertencia acerca de hello **comprobación de la sincronización de hora Global**, comprobar esa hora Hola de reloj del sistema hello (**fecha y hora** configuración) Hola igual como zona de horaria Hola.

     ![Problema de sincronización de hora](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. En **configuración de MySQL**, crear credenciales para iniciar sesión en la instancia del servidor de MySQL de toohello que se instalará.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. En **detalles del entorno**, seleccione si se va a máquinas virtuales de VMware tooreplicate. En caso afirmativo, el programa de instalación comprueba si PowerCLI 6.0 está instalado.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. En **ubicación de instalación**, seleccione si desea que los archivos binarios de tooinstall hello y almacenar en memoria caché de Hola. Puede seleccionar una unidad que tenga al menos 5 GB de espacio disponible en disco, pero se recomienda usar una unidad de memoria caché con 600 GB o más de espacio disponible.

   ![Ubicación de instalación](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. En **selección de red**, especificar Hola agente de escucha (adaptador de red y el puerto SSL) en qué Hola servidor de configuración envíen y reciban datos de replicación. Puede modificar de forma predeterminada Hola puerto (9443). En el puerto de toothis de suma, se usará el puerto 443 por un servidor web que orquesta las operaciones de replicación. No use el puerto 443 para recibir tráfico de replicación.

    ![Selección de red](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. En **resumen**, revise la información de Hola y haga clic en **instalar**. Se genera una frase de contraseña cuando finaliza la instalación. La necesitará al habilitar la replicación, así que cópiela y manténgala en una ubicación segura.

   ![Resumen](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Hola proxy de agente del servicio de recuperación de Microsoft Azure debe estar configurado.
> Una vez finalizada la instalación de hello, inicie Hola Shell de servicios de recuperación de Microsoft Azure desde el menú de inicio de Windows hello. En la ventana de comandos de Hola que se abre, ejecute hello siguiendo el conjunto de comandos tooset la configuración de servidor proxy de Hola.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>Ejecute el programa de instalación de línea de comandos de Hola
También puede ejecutar a Asistente unificada de Hola desde la línea de comandos de hello, como se indica a continuación:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

Donde:

* /ServerMode: Obligatorio. Especifica si la instalación de hello debe instalar servidores de configuración y proceso de Hola o sólo servidor de hello proceso (servidores de procesos adicionales de tooinstall usado). Valores de entrada: CS, PS.
* InstallDrive: Obligatorio. Especifica la carpeta de Hola donde están instalados los componentes de Hola.
* /MySQLCredFilePath. Obligatorio. Especifica el archivo de tooa de ruta de acceso de Hola donde se almacenan las credenciales del servidor MySQL Hola. Obtener archivo de hello plantilla toocreate Hola.
* /VaultCredFilePath. Obligatorio. Ubicación del archivo de credenciales de almacén de Hola.
* /EnvType. Obligatorio. Tipo de instalación. Valores: VMware, NonVMware.
* /PSIP y /CSIP. Obligatorio. Dirección IP del servidor de procesos de Hola y el servidor de configuración.
* /PassphraseFilePath. Obligatorio. Ubicación del archivo de frase de contraseña de Hola.
* /ByPassProxy. Opcional. Especifica el servidor de administración de Hola que conecta tooAzure sin un servidor proxy.
* /ProxySettingsFilePath. Opcional. Especifica valores para un proxy personalizado (proxy predeterminado en servidor de Hola que requiere autenticación), o bien proxy personalizado.

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>Paso 6: Configurar las credenciales para el servidor de vCenter Hola
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

servidor de procesos de Hello podrán detectar automáticamente las máquinas virtuales de VMware que están administrados por un servidor vCenter. Para la detección automática, las necesidades de recuperación de sitio de una cuenta y las credenciales que pueden tener acceso a servidor de vCenter Hola. Esto no es relevante si solo va a replicar servidores físicos.

cuenta de hello tooset y las credenciales:

1. En el servidor de vCenter hello, crear un rol (**Azure_Site_Recovery**) en el nivel de vCenter de hello con hello [los permisos necesarios](#vmware-permissions-for-vcenter-access).
2. Asignar Hola **Azure_Site_Recovery** usuario de rol tooa vCenter.

   > [!NOTE]
   > Una cuenta de usuario de vCenter que tiene el rol de solo lectura de hello puede ejecutar la conmutación por error sin apagar las máquinas de origen protegido. Si desea que tooshut esas máquinas virtuales, necesitará Hola Azure_Site_Recovery rol. Si sólo se está migrando las máquinas virtuales de VMware tooAzure y no es necesario volver toofail, rol de solo lectura de hello es suficiente.
   >
   >
3. cuenta de hello tooadd, abra **cspsconfigtool**. Estará disponible como un acceso directo en el escritorio de Hola y ubicado en la carpeta de \home\svsystems\bin Hola [ubicación de instalación].
4. En hello **administrar cuentas de** , haga clic en **Agregar cuenta**.

    ![Agregar cuenta](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. En **detalles de la cuenta**, agregue las credenciales que pueden ser utilizados tooaccess Hola servidor vCenter. Puede tardar más de 15 minutos para tooappear de nombre de cuenta de hello en el portal de Hola. inmediatamente, haga clic en la tooupdate **actualizar** en hello **servidores de configuración** ficha.

    ![Detalles](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>Paso 7: Incorporación de servidores vCenter y hosts ESXi
Si replica máquinas virtuales VMware, necesitará un servidor vCenter tooadd (o host ESXi).

1. En hello **servidores** > **servidores de configuración** ficha, seleccione **Agregar servidor de vCenter**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. Agregar servidor de vCenter Hola o detalles del host ESXi, nombre de Hola de cuenta de hello que especificó tooaccess Hola servidor vCenter en el paso anterior de Hola y servidor de proceso de Hola que será usado toodiscover máquinas virtuales de VMware que están administrados por el servidor de vCenter Hola. servidor de vCenter Hola o host ESXi debe estar ubicado en la misma red que el servidor de hello en qué Hola está instalado el servidor de procesos de Hola.

   > [!NOTE]
   > Si va a agregar servidor de vCenter Hola o host ESXi con una cuenta que no tiene privilegios de administrador en el servidor de vCenter o host de hello, asegúrese de que vCenter Hola o ESXi cuentas tienen estos privilegios habilitados: Centro de datos, el almacén de datos, carpeta, Jost, red, Recurso, Máquina Virtual y vSphere conmutador distribuida. servidor de vCenter Hola necesita vistas de almacenamiento de hello habilitar privilegio.
   >
   >

    ![Agregar servidor vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Una vez finalizada la detección, el servidor de vCenter Hola se mostrarán en hello **servidores de configuración** ficha.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>Paso 8: Creación de un grupo de protección
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Grupos de protección son agrupaciones lógicas de máquinas virtuales o servidores físicos que desee tooprotect mediante Hola la misma configuración de protección. Aplicar el grupo de protección de tooa de configuración de protección, y esos valores tooall aplicado máquinas (virtuales o físicas) que agregar grupo toohello.

1. Vaya demasiado**elementos protegidos** > **grupo de protección** y haga clic en el icono de hello tooadd un grupo de protección.

    ![Crear un grupo de protección](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. En hello **especificar configuración de grupo de protección** página, especifique un nombre para el grupo de Hola. Hola **de** lista desplegable, el servidor de configuración de hello select en la que desea que el grupo de Hola de toocreate. El **destino** es Microsoft Azure.

    ![Configuración del grupo de protección](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. En hello **especifique la configuración de replicación** página, configurar las opciones de replicación de Hola que se usará para todas las máquinas Hola Hola grupo.

    ![Replicación del grupo de protección](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Coherencia de múltiples VM**: Si activa esta, crea puntos de recuperación coherentes con la aplicación compartida en los equipos de Hola Hola grupo de protección. Esta configuración es muy importante cuando se ejecutan todas las máquinas en el grupo de protección de Hola Hola la misma carga de trabajo. Todas las máquinas será toohello recuperada mismo punto de datos. Esta opción está disponible tanto si replica máquinas virtuales de VMware como servidores físicos (Windows o Linux).
   * **Umbral de RPO**: Hola de conjuntos de RPO. Se generan alertas cuando la replicación de protección de datos continua de hello supera el valor de umbral RPO de hello configurado.
   * **Retención de punto de recuperación**: especifica un período de retención Hola. Equipos protegidos pueden ser recuperado tooany punto dentro de esta ventana.
   * **Frecuencia de la instantánea de coherencia de la aplicación**: especifica la frecuencia con la que se crearán puntos de recuperación que contengan instantáneas coherentes con la aplicación.

Cuando se selecciona la marca de verificación de hello, se crea un grupo de protección con nombre hello especificado. Además, se crea un segundo grupo de protección con el nombre de hello *nombre del grupo de protección*- conmutación por recuperación. Este grupo de protección se utiliza si se produce un error al sitio local toohello atrás después tooAzure de conmutación por error. Puede supervisar los grupos de protección de hello tal y como se crean en hello **elementos protegidos** página.

## <a name="step-9-install-hello-mobility-service"></a>Paso 9: Instalar el servicio de movilidad de Hola
Hola primer paso para habilitar la protección de máquinas virtuales y servidores físicos es servicio de movilidad de tooinstall Hola. Puede hacerlo de dos maneras:

* Push e instalará servicio hello en cada equipo de servidor de procesos de hello automáticamente. Cuando se agrega el grupo de protección de máquinas tooa y ya está ejecutando una versión adecuada de servicio de movilidad de hello, no se produzca la instalación de inserción. Puede instalar también automáticamente el servicio hello mediante su método de inserción de la empresa, como WSUS o System Center Configuration Manager. Asegúrese de que ha configurado el servidor de administración de hello antes de hacerlo.
* Instalar manualmente el servicio de hello en cada equipo que desea tooprotect. Asegúrese de que ha configurado el servidor de administración de hello antes de hacerlo.

### <a name="install-hello-mobility-service-with-push-installation"></a>Instalar servicio de movilidad de hello con la instalación de inserción
Cuando se agrega el grupo de protección de máquinas tooa, se inserta e instalado en cada equipo por el servidor de procesos de Hola automáticamente Hola servicio de movilidad.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Preparación de la inserción automática en máquinas Windows
tooprepare máquinas con Windows para el servicio de movilidad de Hola pueden instalarse automáticamente por el servidor de procesos de hello:

1. Crear una cuenta de que ese servidor de procesos de hello puede usar la máquina de hello tooaccess. cuenta de Hello debe tener privilegios de administrador (local o dominio). Estas credenciales se utilizan únicamente para la instalación por inserción del servicio de movilidad de Hola.

   > [!NOTE]
   > Si no está utilizando una cuenta de dominio, deberá toodisable control de acceso de usuarios remotos en el equipo local de Hola. toodo, en el registro de hello en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, agregue Hola DWORD entrada LocalAccountTokenFilterPolicy con un valor de 1 en. entrada de registro de hello tooadd desde una CLI abrir (comando) o mediante el uso de PowerShell, escriba  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Firewall de Windows en la máquina de Hola que desea tooprotect, seleccione **permitir que una aplicación o una característica a través del Firewall**y habilitar **compartir archivos e impresoras** y **administración de Windows Instrumentación**. Para las máquinas que pertenecen tooa dominio, puede configurar la directiva de firewall de Hola con un GPO.

   ![Configuración de firewall](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Agregar cuenta de hello que creó:

   * Abra **cspsconfigtool**. Estará disponible como un acceso directo en el escritorio de Hola y ubicado en la carpeta de \home\svsystems\bin Hola [ubicación de instalación].
   * En hello **administrar cuentas de** , haga clic en **Agregar cuenta**.
   * Agregar cuenta de hello que creó. Después de agregar la cuenta de hello, necesitará credenciales de hello tooprovide cuando se agrega un grupo de protección de máquina tooa.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Preparación para la inserción automática en los servidores Linux
1. Asegúrese de que esa máquina Linux de Hola que desea se admite tooprotect tal y como se describe en [requisitos previos locales](#on-premises-prerequisites). Asegúrese de que hay conectividad de red entre la máquina de hello desea hello y tooprotect servidor de administración que ejecuta el servidor de procesos de Hola.
2. Crear una cuenta de que ese servidor de procesos de hello puede usar la máquina de hello tooaccess. cuenta de Hello debe ser un usuario raíz Hola servidor de origen Linux. Estas credenciales se utilizan únicamente para la instalación por inserción del servicio de movilidad de Hola.

   * Abra **cspsconfigtool**. Estará disponible como un acceso directo en el escritorio de Hola y ubicado en la carpeta de \home\svsystems\bin Hola [ubicación de instalación].
   * En hello **administrar cuentas de** , haga clic en **Agregar cuenta**.
   * Agregar cuenta de hello que creó. Después de agregar la cuenta de hello, necesitará credenciales de hello tooprovide cuando se agrega un grupo de protección de máquina tooa.
3. Compruebe el archivo/etc/hosts hello en origen Hola Linux server contiene las entradas que se asignan direcciones de tooIP de nombre de host local de hello asociadas con todos los adaptadores de red.
4. Instalar paquetes de openssh, el servidor de openssh y openssl de más recientes hello en la máquina de Hola que desea tooprotect.
5. Asegúrese de que SSH está habilitado y ejecutándose en el puerto 22.
6. Habilitar la autenticación de subsistema y la contraseña SFTP en el archivo de hello sshd_config como sigue:

   * Inicie sesión como root.
   * En el archivo de /etc/ssh/sshd_config hello, busque la línea de Hola que comienza con PasswordAuthentication.
   * Quite el comentario de línea de Hola y cambie el valor de Hola de **no** demasiado**Sí**.
   * Línea de Hola de búsqueda que comienza con **subsistema** y quite el comentario de línea de saludo.

     ![Valor predeterminado de invalidación de Linux de ningún subsistema](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>Instalar manualmente el servicio de movilidad de Hola
instaladores de Hello están disponibles en C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository.

| Sistema operativo de origen | Archivo de instalación del servicio de movilidad |
| --- | --- |
| Windows Server 64 (solo 64 bits) |Microsoft-ASR_UA_9.*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (solo 64 bits) |Microsoft-ASR_UA_9.*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (solo 64 bits) |Microsoft-ASR_UA_9.*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (solo 64 bits) |Microsoft-ASR_UA_9.*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Instalar manualmente el servicio de movilidad de hello en un servidor de Windows
1. Descargue y ejecute el instalador relevante Hola.
2. En **Antes de comenzar**, seleccione **Mobility Service**.

    ![Instalación de Mobility Service](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. En **detalles del servidor de configuración**, especifique la dirección IP de saludo del servidor de administración de Hola y Hola frase de contraseña que se generó cuando instala componentes de servidor de administración de Hola. Puede recuperar la frase de contraseña de hello ejecutando  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** en servidor de administración de Hola.

    ![Mobility Service](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. En **ubicación de instalación de**, conservar la ubicación predeterminada de Hola y haga clic en **siguiente** toobegin instalación.
5. En **progreso de la instalación**, compruebe la instalación y reiniciar la máquina de hello si se le solicita.

También puede instalar mediante la especificación de hello después de la línea de comandos de texto hello:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

Hola anterior comando:

* /Role: Obligatorio. Especifica si se debe instalar el servicio de movilidad de Hola.
* /InstallLocation: Obligatorio. Especifica dónde tooinstall Hola servicio.
* /PassphraseFilePath: Obligatorio. Especifica la frase de contraseña del servidor de configuración de Hola.
* /LogFilePath: Obligatorio. Especifica la ubicación del archivo de configuración de registro de hello.

#### <a name="uninstall-hello-mobility-service-manually"></a>Desinstalar el servicio de movilidad de hello manualmente
Puede desinstalar el servicio de movilidad de hello mediante **desinstalar o cambiar un programa** en el Panel de Control o mediante la línea de comandos de Hola.

Hola comando toouninstall servicio de movilidad mediante el uso de la línea de comandos de hello es:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>Cambiar la dirección IP de Hola Hola del servidor de administración
Después de ejecutar al Asistente de hello, puede cambiar la dirección IP de Hola Hola del servidor de administración como se indica a continuación:

1. Abra Hola archivo hostconfig.exe (que se encuentra en el escritorio de hello).
2. En hello **Global** , modifique la dirección IP de Hola Hola del servidor de administración.

   > [!NOTE]
   > Cambie sólo Hola dirección IP del servidor de administración de Hola. número de puerto de Hola para las comunicaciones entre el servidor de administración debe ser 443, y **Use HTTPS** debe habilitarse izquierda. No cambie la frase de contraseña de Hola.
   >
   >

    ![Dirección IP del servidor de administración](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>Instalar manualmente el servicio de movilidad de hello en un servidor Linux
1. Copie Hola tar adecuado archive toohello máquina Linux en la que desea que tooprotect. Vea la tabla de hello en [instalar manualmente el servicio de movilidad de hello](#install-the-mobility-service-manually) toodetermine qué tar archivar se debe usar.
2. Abrir un programa de shell y extraer Hola tar comprimido archive tooa ruta de acceso local mediante la ejecución:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Cree un archivo denominado passphrase.txt en toowhich de directorio local de Hola que extrajo el contenido de Hola Hola tar archivo. toodo, copia Hola frase de contraseña de C:\ProgramData\Microsoft Azure sitio Recovery\private\connection.passphrase en servidor de administración de hello y guarde el archivo en passphrase.txt ejecutando  *`echo <passphrase> >passphrase.txt`*  en el shell de Hola.
4. Instalar servicio de movilidad de hello escribiendo Hola siguiente comando:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Especificar Hola de dirección IP interna del servidor de administración de Hola y asegúrese de que está seleccionado el puerto 443.

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>Instalar servicio de movilidad de Hola desde línea de comandos de Hola

Copiar la frase de contraseña de Hola de C:\Program Files (x86) \InMage Systems\private\connection en servidor de administración de Hola y guárdelo como "passphrase.txt" en el servidor de administración de Hola. A continuación, ejecute hello siga los comandos. En nuestro ejemplo, dirección IP del servidor de administración de hello es 104.40.75.37 y Hola puerto HTTPS es 443:

tooinstall en un servidor de producción:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

tooinstall en el servidor de destino maestro hello:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>Paso 10: Habilitación de la protección de una máquina
protección de tooenable, agregue el grupo de protección de tooa servidores físicos y máquinas virtuales. Antes de comenzar, tenga en cuenta Hola siguiente si va a proteger máquinas virtuales de VMware:

* Máquinas virtuales de VMware se detectan cada 15 minutos, y puede tardar más de 15 minutos para ellos tooappear Hola portal de Site Recovery después de la detección.
* Cambios en el entorno en la máquina virtual de hello (como la instalación de herramientas de VMware) también pueden tardar más de toobe de 15 minutos actualizado en Site Recovery.
* Puede comprobar Hola último detectado tiempo para las máquinas virtuales de VMware en hello **último contacto a** field para hello vCenter server o el host ESXi en hello **servidores de configuración** ficha.
* Si agrega un servidor vCenter o host ESXi después de crear un grupo de protección, es posible que tarde más de 15 minutos para hello Azure Site Recovery portal toorefresh y toobe de máquinas virtuales que se muestran en hello **grupo de protección de agregar máquinas tooa**cuadro de diálogo.
* Si desea tooproceed inmediatamente y agregar el grupo de protección de máquinas tooa sin tener que esperar para la detección programada de hello, resalte el servidor de configuración de hello (no haga clic en él) y haga clic en **actualizar**.

Además:

* Se recomienda diseñar los grupos de protección para que reflejen las cargas de trabajo. Por ejemplo, agregar los equipos que ejecutan una aplicación específica toohello mismo grupo.
* Cuando se agrega el grupo de protección de máquinas tooa, servidor de procesos de Hola se inserta automáticamente e instala el servicio de movilidad de hello si no está ya instalado. Necesitará el mecanismo de inserción de hello toohave preparado tal y como se describe en el paso anterior de Hola.

### <a name="add-machines-tooa-protection-group"></a>Agregar grupo de protección de máquinas tooa

1. Vaya demasiado**elementos protegidos** > **grupo de protección** > **máquinas** > **agregar máquinas** .
2. Si va a proteger máquinas virtuales de VMware, en **seleccionar máquinas virtuales**, seleccione un servidor vCenter que administra sus máquinas virtuales (o el host de EXSi hello en el que se está ejecutando) y, a continuación, seleccione máquinas Hola.

    ![Habilitar protección para las máquinas virtuales](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. Si va a proteger los servidores físicos, en **seleccionar máquinas virtuales**, abra hello **agregar máquinas físicas** asistente y proporcione la dirección IP de Hola y un nombre descriptivo. A continuación, seleccione la familia de sistemas operativos de Hola.

   ![Habilitación de la protección de servidores físicos](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. En **especificar recursos de destino**, seleccione la cuenta de almacenamiento de Hola que esté usando para la replicación y seleccione si se debe utilizar la configuración de Hola para todas las cargas de trabajo. Por el momento, no se admiten cuentas de Premium Storage.

   > [!NOTE]
   > No se admite mover las cuentas de almacenamiento creadas mediante hello [portal de Azure](../storage/storage-create-storage-account.md) en grupos de recursos.                           
   > [Migración de cuentas de almacenamiento](../azure-resource-manager/resource-group-move-resources.md) a través de recursos grupos dentro Hola misma suscripción o en las suscripciones no se admite para las cuentas de almacenamiento utilizadas para la implementación de Site Recovery.
   >
   >

    ![Configuración de los ajustes de destino](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. En **especificar cuentas**, seleccione Hola cuenta que [configurar](#install-the-mobility-service-with-push-installation) toouse para la instalación automática del programa Hola a servicio de movilidad.

    ![Especificación de las cuentas](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Haga clic en toofinish de marca de verificación de hello agregar máquinas toohello protección toostart y grupo de replicación inicial para cada máquina.

   > [!NOTE]
   > Si se ha preparado la instalación de inserción, servicio de movilidad de Hola se instala automáticamente en equipos que no tengan como estas se agregan toohello grupo de protección. Después de instala el servicio de hello, un trabajo de protección se inicia y se produce un error. Después de un error de hello, deberá reiniciar toomanually Hola de cada máquina que se ha instalado el servicio de movilidad. Después del reinicio de hello, trabajo de protección de hello comienza de nuevo y se produce la replicación inicial.
   >
   >

Puede supervisar el estado en hello **trabajos** página.

![Supervisar el estado en la página de trabajos de Hola](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

El estado de protección también se puede supervisar en **Elementos protegidos** > *nombre del grupo de protección* > **Máquinas virtuales**. Después de que finalice la replicación inicial y se sincronizan los datos, la máquina cambios de estado demasiado**Protected**.

![Supervisión del estado en Elementos protegidos](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>Paso 11: Establecimiento de las propiedades de la máquina protegida
1. Cuando las máquinas ya tienen el estado **Protegido**, puede configurar sus propiedades de conmutación por error. En detalles del grupo de protección de hello, seleccione Hola Hola de equipos y abra **configurar** ficha.
2. Site Recovery automáticamente sugiere propiedades de hello Azure VM y detecta Hola configuración de red local.

    ![Establecer propiedades de máquina virtual](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. Puede cambiar las siguientes opciones:

   * **Nombre de máquina virtual de Azure**: este es el nombre de Hola que se asignará toohello máquina en Azure después de la conmutación por error. Hola nombre debe cumplir con requisitos de Azure.
   * **Tamaño de la máquina virtual de Azure**: número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de Hola. Para obtener más información sobre los tamaños y adaptadores, vea hello [cambiar el tamaño de tablas](../virtual-machines/linux/sizes.md). Observe lo siguiente:

     * Cuando modifique Hola tamaño de una máquina virtual y guardar la configuración de hello, cambiará el número de Hola de adaptadores de red al abrir hello **configurar** Hola pestaña próxima vez. número mínimo de Hola de adaptadores de red de máquinas virtuales de destino es igual toohello un mínimo de adaptadores de red en una máquina virtual de origen. número máximo de Hola de adaptadores de red se determina por tamaño de Hola de máquina virtual de Hola.
       * Si el número de Hola de adaptadores de red en la máquina de origen de hello es menor o igual toohello número de adaptadores permitido para el tamaño de la máquina de destino hello, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
       * Si número de Hola de adaptadores para la máquina virtual de origen de hello supera número de hello permitido para el tamaño de destino de hello, se utilizará el máximo de tamaño de destino de Hola.
        Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero tamaño de destino de hello admite admite solo una, el equipo de destino de hello tendrá solo un adaptador.
     * Si la máquina virtual de hello tiene varios adaptadores de red, todos los adaptadores deberían toohello conectado misma red de Azure.
   * **Red de Azure**: debe especificar una red de Azure que máquinas virtuales de Azure estará conectado tooafter conmutación por error. Si no se especifica uno, Hola máquinas virtuales de Azure no será red tooany conectado. Además, debe toospecify una red de Azure si desea toofailback de sitio de Azure toohello local. La conmutación por recuperación requiere una conexión VPN entre una red de Azure y una red local.
   * **Azure/subred de dirección IP**: para cada adaptador de red, seleccione Hola Hola de toowhich de subred debe conectar la máquina virtual de Azure. Tenga en cuenta que si el adaptador de red de Hola de máquina de origen de hello es toouse configurada una dirección IP estática, puede especificar una dirección IP estática para hello VM de Azure. Si no proporciona una dirección IP estática, se asignará cualquier dirección IP que se encuentre disponible. Si se especifica la dirección IP de destino de hello pero ya está en uso por otra máquina virtual en Azure, se producirá un error en la conmutación por error. Si el adaptador de red de Hola de máquina de origen de hello es toouse configurado DHCP, tendrá DHCP como opción de Hola para Azure.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>Paso 12: Creación de un plan de recuperación y ejecución de una conmutación por error
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

Puede ejecutar una conmutación por error para un único equipo, o puede conmutar por varias máquinas virtuales que realizan Hola igual de tareas o ejecute hello misma carga de trabajo. toofail a través de varios equipos en hello mismo tiempo, se agrega tooa plan de recuperación.

toocreate un plan de recuperación:

1. En hello **planes de recuperación** página, haga clic en **agregar Plan de recuperación** y agregar un plan de recuperación. Especifique los detalles para el plan de Hola y seleccione **Azure** como destino de Hola.

 ![Configurar plan de recuperación](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. En **seleccionar Máquina Virtual**, seleccione un grupo de protección y, a continuación, seleccione las máquinas en el plan de recuperación de hello grupo tooadd toohello.

 ![Agregar máquinas virtuales](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

Puede personalizar toocreate grupos del plan de Hola y orden de hello secuencia en la que las máquinas en el plan de recuperación de Hola se conmuten por error. También puede agregar scripts y avisos para las acciones manuales. Los scripts se pueden crear manualmente o mediante [runbooks de Azure Automation](site-recovery-runbook-automation.md). Para más información acerca de la personalización de los planes de recuperación, consulte [Creación de planes de recuperación](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Ejecución de la conmutación por error
Antes de ejecutar una conmutación por error:

* Asegúrese de que dicho servidor de administración de hello está ejecutándose y disponible. De lo contrario, la conmutación por error presentará errores.
* Si ejecuta una conmutación por error no planeada:

  * Si es posible, debe apagar las máquinas principales antes de ejecutar una conmutación por error no planeada. Esto garantiza que no tienen ambos equipos de origen y de réplica de hello ejecutando en hello mismo tiempo. Si replica máquinas virtuales de VMware al ejecutar una conmutación por error no planeada, puede especificar que Site Recovery debe intentar tooshut los equipos de origen Hola. Según el estado de saludo del sitio primario de hello, esto puede o no funcionen. Si replica servidores físicos, Site Recovery no ofrece esta opción.
  * Una conmutación por error no planeada detiene la replicación de datos desde las máquinas principales para que no se transfiera ningún diferencial de datos después de que comience una conmutación por error no planeada.
  * Si desea tooconnect toohello máquina virtual de Azure después de la conmutación por error, habilite la conexión a Escritorio remoto en la máquina de origen de hello antes de ejecutar Hola conmutación por error. A continuación, permitir la conexión RDP a través de firewall de Hola. También necesitará tooallow RDP en un punto de conexión público de Hola de hello máquina virtual de Azure después de la conmutación por error. Siga [prácticas recomendadas](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) tooensure que RDP funciona después de una conmutación por error.

> [!NOTE]
> tooget Hola obtener el mejor rendimiento cuando se realiza una conmutación por error tooAzure, asegúrese de que ha instalado Hola agente de Azure en la máquina de hello protegido. Esto facilita arranque de la máquina de hello más rápido y le ayuda a diagnosticar problemas. Hello Azure agente está disponible para [Linux](https://github.com/Azure/WALinuxAgent) y [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba
Ejecute un toosimulate de conmutación por error de prueba de la conmutación por error y procesos de recuperación en una red aislada que no afecta al entorno de producción y la replicación normal de permite continúan con normalidad. Conmutación por error de prueba es initiatd en origen de Hola y se puede ejecutar en un par de formas:

* **No se especifica una red de Azure**: si ejecuta una prueba de conmutación por error sin una red, prueba Hola comprobará que las máquinas virtuales se inicia y aparece correctamente en Azure. Máquinas virtuales no estará conectada tooan red de Azure después de la conmutación por error.
* **Especifique una red de Azure**: este tipo de conmutación por error comprueba que entorno de replicación total Hola aparece como se esperaba y que las máquinas virtuales de Azure son toohello conectado de red especificada.

toorun una conmutación por error de prueba:

1. En hello **planes de recuperación** , seleccione el plan de Hola y haga clic en **conmutación por error de prueba**.

 ![Seleccione el plan de Hola](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. En **confirmar probar conmutación por error**, seleccione **ninguno** tooindicate que no desea toouse una red de Azure para conmutación por error de prueba de Hola o prueba de Hola de hello seleccione red toowhich máquinas virtuales se conectarán tras la conmutación por error. Haga clic en hello marca de verificación toostart Hola conmutación por error.

 ![Realización de una selección](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Supervisar el progreso de la conmutación por error en hello **trabajos** ficha.

 ![Supervisión de progreso](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Una vez finalizada la conmutación por error de hello, también debe poder toosee Hola réplica Azure máquina aparecerá en **máquinas virtuales** Hola portal de Azure. Si desea tooinitiate una toohello de conexión RDP VM de Azure, necesitará tooopen puerto 3389 en el extremo de máquina virtual de Hola.
5. Cuando se haya terminado, cuando conmutación por error llegue hello **completar** pruebas fase, haga clic en **prueba completa** toofinish. En **notas**, registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola.
6. Haga clic en **conmutación por error de prueba de hello** tooautomatically limpiar el entorno de prueba de Hola. Una vez hecho esto, se le mostrará la conmutación por error de prueba de hello un **completar** estado. Se eliminan todos los elementos o las máquinas virtuales que se crean automáticamente durante la conmutación por error de prueba de Hola. Si una conmutación por error de prueba continúa durante más de dos semanas, se fuerza toofinish.

### <a name="run-an-unplanned-failover"></a>Ejecución de una conmutación por error no planeada
Conmutación por error imprevista se inicia desde Azure y puede llevar a cabo incluso si no está disponible el sitio primario de Hola.

1. En hello **planes de recuperación** , seleccione el plan de Hola y haga clic en **conmutación por error** > **conmutación por error imprevista**.

 ![Seleccione el plan de Hola](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. Si replica máquinas virtuales de VMware, puede intentar tooshut hacia abajo de máquinas virtuales locales. Se trata de una acción de mejor esfuerzo y conmutación por error sigue el esfuerzo de Hola para ver si se realiza correctamente o no. Si no tiene éxito, detalles del error aparecerá en hello **trabajos** en la ficha **trabajos de conmutación por error no planeada**.

 ![Opción para apagar máquinas virtuales locales](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Esta opción no está disponible si replica servidores físicos. Los necesitará tootry tooshut hacia abajo manualmente si es posible.
 >
 >

3. En **confirmar conmutación por error**, compruebe la dirección de conmutación por error de hello (tooAzure) y seleccione el punto de recuperación de Hola que quiere toouse de hello conmutación por error. Si habilita varias VM al configurar las propiedades de replicación, puede recuperar toohello punto de recuperación más reciente de aplicación o coherente para bloqueos. También puede seleccionar **punto de recuperación personalizada** toorecover tooan anterior al momento dado. Haga clic en hello marca de verificación toostart Hola conmutación por error.

 ![Confirmación de dirección de conmutación por error](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Espere hello toofinish de trabajo de conmutación por error no planeada. Puede supervisar el progreso de la conmutación por error en hello **trabajos** ficha. Incluso si se producen errores durante la conmutación por error imprevista, plan de recuperación de Hola se ejecuta hasta que se complete. También debe poder toosee Hola réplica Azure máquina aparecerá en **máquinas virtuales** Hola portal de Azure.

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>Conectar tooreplicated Azure máquinas virtuales después de la conmutación por error
tooconnect tooreplicated máquinas virtuales Azure después de la conmutación por error, debe:

- Una conexión a Escritorio remoto habilitada en el equipo principal Hola.
- Firewall de Windows en la máquina principal Hola establecer tooallow RDP.
- RDP agregado toohello extremo público para hello máquina virtual de Azure.

Para más información acerca de cómo configurar esto, consulte [Troubleshooting remote desktop connection after failover using ASR](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) (Solución de problemas de la conexión a Escritorio remoto tras conmutar por error con ASR).

## <a name="deploy-additional-process-servers"></a>Implementar servidores de procesos adicionales
Si debe escalar horizontalmente la implementación más allá de 200 máquinas de origen, o si la tasa de renovación de diario total superior a 2 TB, necesitará el volumen de tráfico de proceso adicionales servidores toohandle Hola. tooset de un servidor de proceso adicional, comprobación de requisitos de hello en [servidores de procesos adicionales](#additional-process-servers), y, a continuación, configurar el servidor de proceso de hello según toohello siguiendo las instrucciones. Después de configurar el servidor de hello, puede configurar toouse de máquinas de origen se.

### <a name="set-up-an-additional-process-server"></a>Configuración de un servidor de procesos adicional
Para configurar un servidor de procesos adicional, siga estos pasos:

* Ejecute hello unificado Asistente tooconfigure un servidor de administración como un servidor de procesos solo.
* Si desea que la replicación de datos toomanage utilizando solo Hola nuevo servidor de procesos, debe toomigrate los equipos protegidos.

### <a name="install-hello-process-server"></a>Instalar el servidor de procesos de Hola
1. En hello **inicio rápido** página, descargue el archivo de instalación unificada Hola Hola instalación de componentes de Site Recovery. Ejecute la configuración.
2. En **antes de comenzar**, seleccione **agregar tooscale de servidores de proceso adicionales horizontalmente la implementación**.

 ![Agregar servidores de procesos](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Complete el Asistente de hello como lo hizo cuando se [configurar](#step-5-install-the-management-server) primer servidor de administración de Hola.
4. En **detalles del servidor de configuración**, escriba la dirección IP de Hola Hola original del servidor de administración en el que instaló el servidor de configuración de hello y, a continuación, escriba la frase de contraseña de Hola. Si no tiene la frase de contraseña de hello, ejecute  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** en tooretrieve del servidor de administración original de Hola.

 ![Detalles del servidor de configuración](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Migrar máquinas toouse Hola nuevo servidor de procesos
1. Abra **servidores de configuración** > **Server** > *nombre del servidor de administración original hello*  >   **Detalles del servidor**.

 ![Detalles del servidor](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. Hola **servidores de procesos** lista, seleccione **Cambiar servidor de proceso** siguiente servidor toohello que desea toochange.

 ![Actualizar el servidor de procesos de Hola](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Seleccione **Cambiar servidor de proceso**, seleccione **servidor de procesos de destino**, y, a continuación, seleccione Hola nuevo servidor de administración. A continuación, va a controlar máquinas virtuales seleccione Hola Hola de nuevo servidor de procesos. Haga clic en hello icono tooget información acerca de servidor de Hola. Hola espacio medio requerido tooreplicate toohello de máquina virtual seleccionada cada nuevo servidor de procesos es toohelp mostrado realizar decisiones de carga. Haga clic en toostart de marca de verificación de hello replicar toohello nuevo servidor de procesos.

 ![Cambiar el servidor de proceso de Hola](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>Permisos de VMware para el acceso a vCenter
servidor de procesos de Hello podrán detectar automáticamente las máquinas virtuales en un servidor de vCenter. tooperform la detección automática, deberá toodefine un rol (Azure_Site_Recovery) en el servidor de hello vCenter tooallow nivel Site Recovery tooaccess Hola vCenter. Si solo necesita toomigrate VMware máquinas tooAzure y no es necesario toofailback de Azure, puede definir un rol de solo lectura que es suficiente. Configurar los permisos de hello, como se describe en [paso 6: configurar las credenciales para el servidor de vCenter hello](#step-6-set-up-credentials-for-the-vcenter-server). en hello en la tabla siguiente se resumen los permisos de la función de Hola:

| **Rol** | **Detalles** | **Permisos** |
| --- | --- | --- |
| Rol Azure_Site_Recovery |Detección de máquinas virtuales de VMware |Asignar estos privilegios para el servidor de v-Center de hello:<br/><br/>Almacén de datos: asignar espacio, examinar almacén de datos, operaciones de archivo de bajo nivel, quitar archivo, actualizar archivos de máquina virtual<br/><br/>Red: asignación de red<br/><br/>Recursos: Asignar grupo tooresource de máquina virtual, migrar apagado la máquina virtual, migrar con la tecnología de máquina virtual<br/><br/>Tareas: crear tarea, actualizar tarea<br/><br/>Máquina virtual > Configuración<br/><br/>Máquina virtual > Interactuar > Responder a pregunta, conexión de dispositivos, configurar soporte de CD, configurar soporte de disquete, apagar, encender, instalación de herramientas de VMware<br/><br/>Máquina virtual > Inventario > Crear, registrar, anular registro<br/><br/>Máquina virtual > Aprovisionamiento > Permitir descarga de máquina virtual, permitir carga de archivos de máquina virtual<br/><br/>Máquina virtual > Instantáneas > Quitar instantáneas |
| Rol de usuario de vCenter |Detección/conmutación por error de VMware sin apagar la máquina virtual de origen |Asignar estos privilegios para el servidor de v-Center de hello:<br/><br/>Objeto de centro de datos > propagar tooChild objeto, role = solo lectura <br/><br/>usuario de Hola se asigna en el nivel del centro de datos de hello y, por tanto, tiene acceso tooall Hola objetos en el centro de datos de Hola. Si desea tener acceso de hello toorestrict, asignar Hola **sin acceso** rol con hello **propagar toochild** toohello los objetos secundarios (hosts de ESX, almacenes de datos, las máquinas virtuales y redes) del objeto. |
| Rol de usuario de vCenter |Conmutación por error y conmutación por recuperación |Asignar estos privilegios para el servidor de v-Center de hello:<br/><br/>Objeto de centro de datos: objeto toochild de propagar, rol = Azure_Site_Recovery<br/><br/>usuario de Hola se asigna en el nivel del centro de datos y, por tanto, tiene acceso tooall Hola objetos en el centro de datos de Hola.  Si desea tener acceso de hello toorestrict, asignar Hola ** sin acceso ** rol con hello **propagar toochild objeto** objeto secundario de toohello (hosts de ESX, almacenes de datos, las máquinas virtuales y redes). |

## <a name="third-party-software-notices-and-information"></a>Avisos e información de software de terceros
<!--Do Not Translate or Localize-->

software de Hola y firmware que se ejecuta Hola técnico de Microsoft o servicio se basa en o incorpora material de hello proyectos enumerados a continuación (colectivamente, "código de terceros").  Microsoft es hello autor no original del programa Hola a código de terceros.  Hola aviso de propiedad intelectual y licencia, en la que Microsoft ha recibido este código de terceros, se establecen estipulado más adelante.

información de Hello en la sección A se con respecto a otro código de terceros componentes de proyectos de Hola se enumeran a continuación. Such licenses and information are provided for informational purposes only.  Este código de terceros se está tooyou relicensed por Microsoft en términos de los productos de Microsoft de Hola y servicio de licencias de software de Microsoft.  

información de Hello en la sección B se con respecto a los componentes de código de terceros que se están realizando tooyou disponible por parte de Microsoft bajo los términos de licencia original Hola.

podrá encontrar más completa del archivo Hello en hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información acerca de la conmutación por recuperación](site-recovery-failback-azure-to-vmware-classic.md) toobring entorno local de tooyour realizar copias de las máquinas se conmutó por error que se ejecuta en Azure.
