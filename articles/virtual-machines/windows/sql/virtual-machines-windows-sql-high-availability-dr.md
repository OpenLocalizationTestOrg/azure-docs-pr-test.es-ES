---
title: "aaaHigh disponibilidad y recuperación ante desastres para SQL Server | Documentos de Microsoft"
description: "Obtener una explicación de Hola diversos tipos de estrategias HADR de SQL Server en máquinas virtuales de Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Alta disponibilidad y recuperación ante desastres para SQL Server en máquinas virtuales de Azure

Máquinas virtuales de Microsoft Azure (VM) con SQL Server puede ayudar a reducir el costo de Hola de una solución de base de datos alta disponibilidad y ante desastres (HADR) de recuperación. La mayoría de las soluciones HADR de SQL Server son compatibles con las máquinas virtuales de Azure, bien como soluciones exclusivas de Azure o híbridas. En una solución solo de Azure, Hola todo el sistema HADR se ejecuta en Azure. En una configuración híbrida, parte de la solución de Hola se ejecuta en Azure y Hola otra parte se ejecuta de forma local en su organización. Hello flexibilidad de hello entorno Azure le permite toomove total o parcialmente presupuesto de tooAzure toosatisfy hello y requisitos de HADR de SQL Server de base de datos sistemas.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>Necesidad de Hola de descripción de una solución HADR
Es una tooyou tooensure que el sistema de base de datos posee capacidades HADR de Hola Hola contrato de nivel de servicio (SLA) requiere. hecho de Hola que Azure proporcione mecanismos de alta disponibilidad, como la recuperación del servicio para los servicios de nube y detección de errores para las máquinas virtuales, no garantiza por sí solo que puede cumplir el SLA de hello deseado. Estos mecanismos protegen la alta disponibilidad de Hola de hello las máquinas virtuales, pero no Hola alta disponibilidad de SQL Server que se ejecuta dentro de hello las máquinas virtuales. Es posible que toofail de instancia de SQL Server de hello mientras Hola VM está en línea y en buen estado. Además, los mecanismos de alta disponibilidad incluso Hola proporcionados por Azure permiten tiempos de inactividad de las máquinas virtuales de hello due tooevents como la recuperación de errores de software o hardware y actualizaciones del sistema operativo.

Además, el almacenamiento con redundancia geográfica (GRS) de Azure, que se implementa con una característica llamada replicación geográfica, podría no ser una solución para recuperación ante desastres adecuada para sus bases de datos. Dado que la replicación geográfica envía datos de forma asincrónica, se pueden perder actualizaciones recientes en caso de hello de un desastre. Para obtener más información sobre las limitaciones de replicación geográfica se tratan en hello [no se admite para los archivos de datos y de registro en discos independientes de replicación geográfica](#geo-replication-support) sección.

## <a name="hadr-deployment-architectures"></a>Arquitecturas de implementación HADR
Entre las tecnologías HADR de SQL Server compatibles con Azure se incluyen:

* [Grupos de disponibilidad AlwaysOn (SQL Server)](https://technet.microsoft.com/library/hh510230.aspx)
* [Instancias de clúster de conmutación por error de AlwaysOn (SQL Server)](https://technet.microsoft.com/library/ms189134.aspx)
* [Trasvase de registros](https://technet.microsoft.com/library/ms187103.aspx)
* [Copia de seguridad y restauración de SQL Server con el servicio Azure Blob Storage](https://msdn.microsoft.com/library/jj919148.aspx)
* [Creación de reflejo de la base de datos](https://technet.microsoft.com/library/ms189852.aspx): en desuso en SQL Server 2016

Es posible toocombine Hola tecnologías conjuntamente tooimplement una solución de SQL Server que tenga alta disponibilidad y capacidades de recuperación ante desastres. Dependiendo de la tecnología de Hola que se utilice, una implementación híbrida puede requerir un túnel VPN con hello red virtual de Azure. Hello las siguientes secciones muestran algunas de las arquitecturas de implementación de ejemplo de Hola.

## <a name="azure-only-high-availability-solutions"></a>Exclusiva de Azure: soluciones de alta disponibilidad

Puede tener una solución de alta disponibilidad para SQL Server en un nivel de base de datos con grupos de disponibilidad Always On (denominados grupos de disponibilidad). También puede crear una solución de alta disponibilidad en un nivel de instancia con instancias de clúster de conmutación por error Always On (instancias del clúster de conmutación por error). Si desea obtener redundancia adicional, puede crear redundancia en ambos niveles creando de grupos de disponibilidad en instancias de clúster de conmutación por error. 

| Technology | Arquitecturas de ejemplo |
| --- | --- |
| **Grupos de disponibilidad** |Réplicas de disponibilidad que se ejecutan en máquinas virtuales de Azure Hola misma región proporcionar una alta disponibilidad. Necesita tooconfigure un controlador de dominio de máquina virtual, porque de agrupación en clústeres de conmutación por error de Windows requiere un dominio de Active Directory.<br/> ![Grupos de disponibilidad](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>Para más información, vea [Configuración de grupos de disponibilidad en Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). |
| **Instancias de clúster de conmutación por error** |Las instancias de clúster de conmutación por error (FCI), que requieren almacenamiento compartido, se pueden crear de tres maneras distintas.<br/><br/>1. Un clúster de conmutación por error de dos nodos que se ejecuta en máquinas virtuales de Azure con el uso de almacenamiento conectado [espacios de almacenamiento de Windows Server 2016 directo \(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide una SAN virtual basada en software.<br/><br/>2. Un clúster de conmutación por error de dos nodos que se ejecuta en Azure Virtual Machines con almacenamiento posibilitado por una solución de clústeres de terceros. Si desea obtener un ejemplo específico con SIOS DataKeeper, vea [High availability for a file share using failover clustering and 3rd party software SIOS Datakeeper](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/) (Alta disponibilidad de un recurso compartido de archivos con clúster de conmutación por error y el software de terceros SIOS DataKeeper).<br/><br/>3. Un clúster de conmutación por error de dos nodos que se ejecuta en Azure Virtual Machines con almacenamiento en bloque compartido de destino iSCSI remoto a través de ExpressRoute. Por ejemplo, almacenamiento de información privada de NetApp (NPS) expone un destino iSCSI a través de ExpressRoute con Equinix tooAzure máquinas virtuales.<br/><br/>Para el almacenamiento compartido de terceros y soluciones de replicación de datos, debe ponerse en contacto con el proveedor de Hola de los datos de tooaccessing relacionados con problemas de conmutación por error.<br/><br/>Tenga en cuenta que todavía no se admite el uso de FCI basado en el [Almacenamiento de archivos de Azure](https://azure.microsoft.com/services/storage/files/) , porque esta solución no utiliza Almacenamiento premium. Estamos trabajando toosupport este pronto. |

## <a name="azure-only-disaster-recovery-solutions"></a>Exclusiva de Azure: soluciones de recuperación ante desastres
Puede tener una solución de recuperación ante desastres para las bases de datos de SQL Server en Azure con grupos de disponibilidad, creación de reflejo de bases de datos o copias de seguridad y restauración con blobs de almacenamiento.

| Technology | Arquitecturas de ejemplo |
| --- | --- |
| **Grupos de disponibilidad** |Réplicas de disponibilidad que se ejecutan en varios centros de datos en máquinas virtuales de Azure para la recuperación ante desastres. Esta solución entre regiones protege frente a interrupciones en todo el sitio. <br/> ![Grupos de disponibilidad](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>Dentro de una región, todas las réplicas deben ser dentro de hello mismo servicio en la nube y Hola misma red virtual. Dado que cada región tendrá una red virtual distinta, estas soluciones requieren conectividad de red virtual tooVNet. Para obtener más información, consulte [configurar una red virtual a red de virtual de conexión mediante Hola portal de Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md). Para obtener instrucciones detalladas, vea [Configuración de un grupo de disponibilidad en máquinas virtuales de Azure en distintas regiones](virtual-machines-windows-portal-sql-availability-group-dr.md).|
| **Creación de reflejo de la base de datos** |Los servidores principal y de reflejo se ejecutan en distintos centros de datos para la recuperación ante desastres. Debe realizar la implementación con certificados de servidor porque un dominio de Active Directory no puede abarcar varios centros de datos.<br/>![Creación de reflejo de la base de datos](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Copia de seguridad y restauración con el servicio Almacenamiento de blobs de Azure** |Las bases de datos de producción copian directamente tooblob almacenamiento en otro centro de datos para la recuperación ante desastres.<br/>![Copia de seguridad y restauración](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>Para más información, consulte [Copias de seguridad y restauración para SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="hybrid-it-disaster-recovery-solutions"></a>TI híbrida: soluciones de recuperación ante desastres
Puede tener una solución de recuperación ante desastres para las bases de datos de SQL Server en un entorno de TI híbrida con grupos de disponibilidad, creación de reflejo de la base de datos, trasvase de registros y copias de seguridad y restauración con Azure Blob Storage.

| Technology | Arquitecturas de ejemplo |
| --- | --- |
| **Grupos de disponibilidad** |Algunas réplicas de disponibilidad se ejecutan en máquinas virtuales de Azure y réplicas se ejecutan localmente para la recuperación ante desastres a través de sitios. Hello sitio de producción puede ser local o en un centro de datos de Azure.<br/>![Grupos de disponibilidad](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>Dado que todas las réplicas de disponibilidad deben estar en Hola mismo clúster de conmutación por error, hello debe abarcar ambas redes (un clúster de conmutación por error de múltiples subredes). Esta configuración requiere una conexión VPN entre Azure y Hola red local.<br/><br/>Para la recuperación ante desastres correcta de las bases de datos, también debe instalar un controlador de dominio de réplica en el sitio de recuperación ante desastres de Hola.<br/><br/>Es posible toouse Hola Asistente para agregar réplicas en SSMS tooadd un tooan de réplica de Azure siempre en el grupo de disponibilidad existente. Para obtener más información, consulte Tutorial: ampliar su tooAzure siempre en el grupo de disponibilidad. |
| **Creación de reflejo de la base de datos** |Un asociado ejecutándose en una máquina virtual de Azure y Hola otro ejecutando de forma local para la recuperación ante desastres a través de sitios con certificados de servidor. Los asociados no necesitan toobe en Hola mismo dominio de Active Directory y no se requiere ninguna conexión de VPN.<br/>![Creación de reflejo de la base de datos](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>Otra situación de creación de reflejo de base de datos implica un asociado se ejecuta en una máquina virtual de Azure y hello otra que se ejecuta de forma local en hello mismo dominio de Active Directory para la recuperación ante desastres entre sitios. A [conexión VPN entre la red de hello Azure virtual hello y red local](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) es necesario.<br/><br/>Para la recuperación ante desastres correcta de las bases de datos, también debe instalar un controlador de dominio de réplica en el sitio de recuperación ante desastres de Hola. |
| **Trasvase de registros** |Un servidor que ejecuta en una máquina virtual de Azure y Hola otro ejecutando de forma local para la recuperación ante desastres entre sitios. Trasvase de registros depende de Windows uso compartido de archivos, por lo que se requiere la red en local de una conexión VPN entre la red virtual de Azure de Hola y Hola.<br/>![Trasvase de registros](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>Para la recuperación ante desastres correcta de las bases de datos, también debe instalar un controlador de dominio de réplica en el sitio de recuperación ante desastres de Hola. |
| **Copia de seguridad y restauración con el servicio Almacenamiento de blobs de Azure** |Copia de seguridad directamente tooAzure almacenamiento de blobs para recuperación ante desastres de bases de datos de producción en local.<br/>![Copia de seguridad y restauración](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>Para más información, consulte [Copias de seguridad y restauración para SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Consideraciones importantes para HADR de SQL Server en Azure
Las máquinas virtuales de Azure, el almacenamiento y la conexión de red tienen características operativas diferentes de las de una infraestructura TI local y no virtualizada. Una implementación correcta de una solución de SQL Server HADR en Azure requiere que entender estas diferencias y diseñar su solución tooaccommodate ellos.

### <a name="high-availability-nodes-in-an-availability-set"></a>Nodos de alta disponibilidad en un conjunto de disponibilidad
Conjuntos de disponibilidad de Azure permiten nodos de alta disponibilidad de hello tooplace en diferentes dominios de error (FD) y dominios de actualización (ud). Para las máquinas virtuales de Azure toobe realizó Hola mismo conjunto de disponibilidad, debe implementarlas en hello mismo servicio en la nube. Sólo los nodos en hello mismo servicio en la nube puede participar en Hola el mismo conjunto de disponibilidad. Para obtener más información, consulte [administrar Hola disponibilidad de las máquinas virtuales](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="failover-cluster-behavior-in-azure-networking"></a>Comportamiento de clúster de conmutación por error en redes de Azure
servicio DHCP no compatible con RFC de Hello en Azure puede hacer la creación de hello de determinados toofail de configuraciones de clúster de conmutación por error, debido a toohello nombre de red de clúster que se asigna una dirección IP duplicada, como hello las direcciones IP mismo como uno de los nodos de clúster de Hola. Se trata de un problema al implementar grupos de disponibilidad, que depende la característica de clúster de conmutación por error de Windows hello.

Considere el escenario de hello cuando se crea un clúster de dos nodos y se pone en línea:

1. Hola clúster estará en línea y, a continuación, NODE1 solicita una dirección IP asignada dinámicamente para el nombre de red del clúster de Hola.
2. Ninguna dirección IP que no sea la dirección IP de NODE1 viene dado por hello servicio DHCP, puesto que Hola servicio DHCP reconoce dicha solicitud Hola procede Nodo1 propio.
3. Windows detecta que se asigna una dirección duplicada tooNODE1 y toohello nombre de red del clúster de conmutación por error, y se produce un error en grupo de clúster predeterminado de hello toocome en línea.
4. grupo de clústeres predeterminado Hola mueve tooNODE2, que trata la dirección IP de NODE1 como dirección IP del clúster hello y pone Hola grupo predeterminado del clúster en línea.
5. Cuando NODE2 intenta tooestablish conectividad con NODE1, los paquetes dirigidos a NODE1 nunca abandonan NODE2 porque resuelve tooitself de dirección IP de NODE1. Nodo2 no se puede establecer conectividad con NODE1, pierde el quórum y cierra el clúster de Hola.
6. Hola mientras tanto, NODE1 puede enviar paquetes tooNODE2 pero NODE2 no puede responder. Node1 pierde el quórum y cierra el clúster de Hola.

Este escenario puede evitarse mediante la asignación de una dirección IP sin usar estática, como una dirección IP de vínculo local como 169.254.1.1, nombre de red del clúster de toohello en orden toobring Hola clúster nombre de red en línea. toosimplify este proceso, consulte [clúster de conmutación por error de configuración de Windows en Azure para grupos de disponibilidad](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx).

Para más información, vea [Configuración de grupos de disponibilidad en Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md).

### <a name="availability-group-listener-support"></a>Compatibilidad del agente de escucha del grupo de disponibilidad
Los agentes de escucha del grupo de disponibilidad son compatibles con máquinas virtuales de Azure que ejecutan Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 y Windows Server 2016. Esta compatibilidad se realiza mediante el uso de Hola de extremos con equilibrio de carga habilitado Hola máquinas virtuales de Azure que sean nodos de grupo de disponibilidad. Debe seguir los pasos de configuración especiales para toowork de agentes de escucha de Hola para ambas aplicaciones de cliente que se ejecutan en Azure, así como los que se ejecutan en local.

Existen dos opciones principales para configurar el agente de escucha: externa (público) o interna. Hola agente de escucha externo (público) se utiliza una conexión a internet el equilibrador de carga y está asociado con una IP Virtual pública (VIP) que sea accesible a través de Hola a internet. Un agente de escucha interno utiliza un equilibrador de carga interno y solo es compatible con clientes en Hola misma red Virtual. Para cada tipo de equilibrador de carga, debe habilitar Direct Server Return. 

Si Hola grupo de disponibilidad abarca varias subredes de Azure (por ejemplo, una implementación que se cruza con regiones de Azure), debe incluir la cadena de conexión de cliente de Hola "**MultisubnetFailover = True**". Esto da como resultado toohello réplicas de intentos de conexión paralela en subredes diferentes de Hola. Para obtener instrucciones sobre cómo configurar un agente de escucha, consulte

* [Configuración de un agente de escucha con ILB para grupos de disponibilidad en Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md).
* [Configuración de un agente de escucha externo para grupos de disponibilidad en Azure](../classic/ps-sql-ext-listener.md).

Pueden seguir conectándose tooeach réplica de disponibilidad por separado conectándose directamente toohello instancia del servicio. Además, puesto que los grupos de disponibilidad son compatibles con versiones anteriores con clientes de creación de reflejo de la base de datos, puede conectarse toohello réplicas de disponibilidad como asociados de creación de reflejo como Hola réplicas están configuradas de la base de datos similar de creación de reflejo toodatabase:

* Una réplica principal y una réplica secundaria
* Hello réplica secundaria está configurada como no legible (**secundaria legible** opción establecida demasiado**n**)

Es una cadena de conexión de cliente de ejemplo que corresponde la configuración de tipo de creación de reflejo de base de datos de toothis usa ADO.NET o SQL Server Native Client a continuación:

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

Para obtener más información sobre la conectividad del cliente, consulte:

* [Usar palabras clave de cadena de conexión con SQL Server Native Client](https://msdn.microsoft.com/library/ms130822.aspx)
* [Conectar clientes tooa sesión de creación de reflejo de base de datos (SQL Server)](https://technet.microsoft.com/library/ms175484.aspx)
* [Conexión tooAvailability agente de escucha de grupo de TI híbrida](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [Agentes de escucha del grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [Uso de cadenas de conexión de creación de reflejo de la base de datos con grupos de disponibilidad](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>Latencia de red en TI híbrida
Debe implementar la solución HADR con la suposición de Hola que puede haber períodos de tiempo con alta latencia de red entre la red local y Azure. Al implementar réplicas tooAzure, debe utilizar la confirmación asincrónica en lugar de confirmación sincrónica para el modo de sincronización de Hola. Al implementar servidores de creación de reflejo de la base de datos tanto local como en Azure, use el modo de alto rendimiento de hello en lugar de modo de alta seguridad Hola.

### <a name="geo-replication-support"></a>Compatibilidad de la replicación geográfica
Replicación geográfica en discos de Azure no admite archivos de datos de Hola y archivo de registro de hello mismo toobe de base de datos almacenado en discos independientes. La GRS replica los cambios en cada disco independiente y asincrónicamente. Este mecanismo garantiza el orden de escritura de hello en un único disco en la copia de replicación geográfica de hello, pero no a través de las copias replicadas geográficamente de varios discos. Si configura una base de datos toostore su archivo de datos y su archivo de registro en discos independientes, Hola recupera discos después de un desastre pueden contener una copia más actualizada del archivo de datos de Hola que archivo de registro de hello, que se introduce Hola registro de escritura anticipada en SQL Server y Hola ACID propiedades de las transacciones. Si no tiene Hola opción toodisable de replicación geográfica en la cuenta de almacenamiento de hello, debe mantener todos los datos y archivos de registro para una base de datos en hello mismo disco. Si tiene que utilizar más de un disco debido toohello tamaño de base de datos de hello, deberá toodeploy una de las soluciones de recuperación ante desastres de hello mencionada anteriormente tooensure redundancia de datos.

## <a name="next-steps"></a>Pasos siguientes
Si necesita toocreate una máquina virtual de Azure con SQL Server, vea [aprovisionamiento de una máquina Virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).

tooget Hola un rendimiento óptimo de SQL Server que se ejecuta en una máquina virtual de Azure, consulte las instrucciones de hello en [prácticas recomendadas de rendimiento para SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-performance.md).

Para ver otros temas relacionados con toorunning SQL Server en máquinas virtuales de Azure, consulte [SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-server-iaas-overview.md).

### <a name="other-resources"></a>Otros recursos:
* [Instalación de un nuevo bosque de Active Directory en Azure](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Creación del clúster de conmutación por error para grupos de disponibilidad en la VM de Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)

