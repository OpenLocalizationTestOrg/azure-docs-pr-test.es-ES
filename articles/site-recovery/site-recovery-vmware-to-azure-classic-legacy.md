---
title: "aaaReplicate máquinas virtuales de VMware y servidores físicos tooAzure (heredado clásico) | Documentos de Microsoft"
description: "Describe cómo tooreplicate local las máquinas virtuales y tooAzure de servidores físicos de Windows/Linux con Azure Site Recovery en una implementación heredada en portal clásico de Hola."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>Replicar máquinas virtuales de VMware y servidores físicos tooAzure con Azure Site Recovery mediante el portal clásico de hello (heredado)
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmware-to-azure.md)
> * [Portal clásico](site-recovery-vmware-to-azure-classic.md)
> * [Portal clásico (heredado)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Bienvenido tooAzure Site Recovery. Este artículo describe una implementación heredada para la replicación de máquinas virtuales de VMware locales o tooAzure de servidores físicos de Windows/Linux con Azure Site Recovery en el portal clásico de Hola.

## <a name="overview"></a>Información general
Las organizaciones necesitan una estrategia BCDR que determina cómo aplicaciones, las cargas de trabajo y los datos permanecen disponibles y ejecutarse durante el tiempo de inactividad planeado y no planeado y recuperación las condiciones de trabajo de toonormal tan pronto como sea posible. Su estrategia de BCDR se centra en soluciones que mantengan los datos empresariales seguros y recuperables, y garanticen que las cargas de trabajo estarán disponibles continuamente en caso de desastre.

Recuperación del sitio es un servicio de Azure que contribuye estrategia BCDR tooyour por la organización de replicación de servidores físicos locales y máquinas virtuales en la nube toohello (Azure) o tooa centro de datos secundario. Cuando se producen interrupciones en la ubicación principal, conmutación por error toohello ubicación secundaria tookeep aplicaciones y cargas de trabajo disponibles. Producirá un error de ubicación principal tooyour atrás cuando devuelve las operaciones de toonormal. Más información en [¿Qué es Site Recovery?](site-recovery-overview.md)

> [!WARNING]
> Este artículo contiene **instrucciones heredadas**. No lo utilice para las nuevas implementaciones. En su lugar, [, siga estas instrucciones](site-recovery-vmware-to-azure.md) toodeploy Site Recovery en el portal de Azure, Hola o [siga estas instrucciones](site-recovery-vmware-to-azure-classic.md) tooconfigure Hola mejorado de implementación en el portal clásico de Hola. Si ya ha implementado utilizando el método hello descrito en este artículo, se recomienda que migre implementación toohello mejorada en el portal clásico de Hola.
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>Migrar la implementación de toohello mejorado
Esta sección solo es relevante si ya ha implementado la recuperación del sitio siguiendo las instrucciones de hello en este artículo.

toomigrate la implementación existente, necesitará:

1. Implementar nuevos componentes de Site Recovery en el sitio local.
2. Configure las credenciales para la detección automática de máquinas virtuales de VMware en el nuevo servidor de configuración de Hola.
3. Detecta servidores de VMware Hola con el nuevo servidor de configuración de Hola.
4. Crear un nuevo grupo de protección con el nuevo servidor de configuración de Hola.

Antes de comenzar:

* Se recomienda que configure una ventana de mantenimiento para la migración.
* Hola **migrar máquinas** opción sólo está disponible si tiene grupos de protección existentes que se crearon durante una implementación heredada.
* Después de haber completado los pasos de migración de hello puede tardar 15 minutos o más credenciales de hello toorefresh y toodiscover y la actualización de máquinas virtuales para que pueda agregar grupo de protección de tooa. Puede actualizar manualmente en lugar de esperar.

Realice la migración de la siguiente forma:

1. Obtenga información sobre [mejorado la implementación en el portal clásico de hello](site-recovery-vmware-to-azure-classic.md). Hola de revisión mejorada [arquitectura](site-recovery-vmware-to-azure-classic.md), y [requisitos previos](site-recovery-vmware-to-azure-classic.md).
2. Desinstale el servicio de movilidad de Hola de máquinas que está replicando actualmente. Se instalará una nueva versión del servicio de hello en máquinas de hello al agregarlas toohello nuevo grupo de protección.
3. Descargar un [clave de registro del almacén](site-recovery-vmware-to-azure-classic.md) y [ejecutar el Asistente para la instalación unificada de hello](site-recovery-vmware-to-azure-classic.md) servidor de configuración de tooinstall hello, servidor de procesos y maestro de componentes de servidor de destino. Más información sobre el [planeamiento de capacidad](site-recovery-vmware-to-azure-classic.md).
4. [Configurar credenciales](site-recovery-vmware-to-azure-classic.md) esa recuperación del sitio puede usar tooaccess VMware server tooautomatically detectar máquinas virtuales VMware. Más información acerca de los [permisos necesarios](site-recovery-vmware-to-azure-classic.md).
5. Agregue [servidores vCenter o hosts vSphere](site-recovery-vmware-to-azure-classic.md). Se pueden tardar 15 minutos para obtener más información para servidores tooappear Hola portal de Site Recovery.
6. Cree un [nuevo grupo de protección](site-recovery-vmware-to-azure-classic.md). Puede tardar minutos too15 toorefresh portal Hola para que las máquinas virtuales Hola se detectan y aparecen. Si no desea toowait puede resaltar el nombre del servidor de administración de hello (no haga clic en él) > **actualizar**.
7. Hola nuevo grupo de protección, haga clic en **migrar máquinas**.

    ![Agregar cuenta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. En **seleccionar máquinas** grupo de protección de hello seleccione desee toomigrate desde y Hola máquinas que desee toomigrate.

    ![Agregar cuenta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. En **configurar opciones de destino** especifique si desea que toouse Hola la misma configuración para todas las máquinas y servidor de procesos seleccione hello y cuenta de almacenamiento de Azure. Si no tiene un servidor de procesos independiente tratarse dirección IP de Hola Hola Hola server del servidor de configuración.

    ![Agregar cuenta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [Migración de cuentas de almacenamiento](../resource-group-move-resources.md) a través de recursos grupos dentro Hola misma suscripción o en las suscripciones no se admite para las cuentas de almacenamiento utilizadas para la implementación de Site Recovery.

1. En **especificar cuentas**, seleccione cuenta de hello que creó para tooaccess de servidor de proceso de Hola Hola versión nueva Hola la máquina toopush Hola del servicio de movilidad.

   ![Agregar cuenta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. Recuperación de sitio a migrar su cuenta de almacenamiento de Azure de toohello de los datos replicados que proporcionó. Opcionalmente, puede volver a usar cuenta de almacenamiento de hello utilizado en la implementación heredada de Hola.
3. Después del trabajo de hello finaliza las máquinas virtuales se sincronizará automáticamente. Una vez completada la sincronización puede eliminar máquinas virtuales de Hola Hola heredado de grupo de protección.
4. Después de han migrado todas las máquinas puede eliminar el grupo de protección heredada de Hola.
5. Recuerde toospecify propiedades de conmutación por error Hola máquinas y Hola configuración de red de Azure, una vez completada la sincronización.
6. Si dispone de los planes de recuperación existentes, puede migrarlas implementación toohello mejorado con hello **migrar el Plan de recuperación** opción. Solo debe hacerlo después de que se hayan migrado todas las máquinas protegidas.

   ![Agregar cuenta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> Una vez que haya terminado de migración continuar con hello [artículo mejorada](site-recovery-vmware-to-azure-classic.md). resto de Hola de este artículo heredado ya no será relevante y no es necesario toofollow cualquier más de los pasos de hello descritos en TI **.
>
>

## <a name="what-do-i-need"></a>¿Qué necesito?
Este diagrama muestra los componentes de implementación de Hola.

![Almacén nuevo](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

Esto es lo que necesita:

| **Componente** | **Implementación** | **Detalles** |
| --- | --- | --- |
| **Servidor de configuración** |Estándar A3 máquinas virtuales de Azure en hello misma suscripción que Site Recovery. |servidor de configuración de Hello coordina la comunicación entre máquinas protegidas, servidor de procesos de Hola y servidores de destino maestro en Azure. Configura la replicación y coordina la recuperación en Azure cuando se produce la conmutación por error. |
| **Servidor de destino principal** |Una máquina virtual de Azure, un servidor de Windows en función de una imagen de la Galería de Windows Server 2012 R2 (tooprotect máquinas de Windows) o en un servidor Linux basada en una imagen de la Galería de OpenLogic CentOS 6.6 (tooprotect máquinas de Linux).<br/><br/> Hay tres opciones de tamaño disponibles: A4 estándar, D14 estándar y DS4 estándar.<br/><br/> Hello servidor está conectado toohello misma red de Azure como servidor de configuración de Hola.<br/><br/> Configurar en el portal de Site Recovery Hola |Recibe y retiene los datos replicados de las máquinas protegidas usando discos duros virtuales asociados creados en Almacenamiento de blobs de su cuenta de almacenamiento de Azure.<br/><br/> Seleccione DS4 estándar específicamente para configurar la protección para las cargas de trabajo que requieren alto rendimiento y baja latencia coherentes mediante la cuenta de almacenamiento premium. |
| **Servidor de proceso** |Un servidor virtual o físico local que ejecute Windows Server 2012 R2<br/><br/> Se recomienda ha colocado en hello mismo tooit de visibilidad de red de red y el segmento de LAN como máquinas de Hola que desee tooprotect, pero se puede ejecutar en una red diferente como máquinas protegidas tienen L3.<br/><br/> Configurar y registrar el servidor de configuración de toohello Hola portal de Site Recovery. |Las máquinas protegidas envían servidor de procesos de replicación datos toohello local. Tiene una memoria caché de disco toocache replicación de datos que recibe. Realiza una serie de acciones en los datos.<br/><br/> Optimiza los datos por el almacenamiento en caché, comprimir y cifrar antes de enviar en el servidor de destino maestro toohello.<br/><br/> Controla la instalación por inserción del servicio de movilidad de Hola.<br/><br/> Realiza la detección automática de las máquinas virtuales de VMware. |
| **Máquinas locales** |Máquinas virtuales de VMware locales o servidores físicos ejecutándose en Windows o Linux. |Configurar los ajustes de replicación que se aplican uno o varias máquinas. Puede crear una conmutación por error en una máquina individual o, más generalmente, en varias máquinas virtuales que reúna en un plan de recuperación. |
| **Servicio de movilidad** |Instalado en cada máquina virtual o el servidor físico que desea tooprotect<br/><br/> Se pueden instalar manualmente o insertan e instalan automáticamente el servidor de procesos de hello cuando se habilita la replicación para una máquina. |Hola servicio de movilidad envía el servidor de procesos de toohello de datos durante la replicación inicial (resincronización). Después de máquina de hello esté en un estado protegido (después de que finalice la resincronización) Hola servicio de movilidad captura toodisk escrituras en memoria y los envía toohello servidor de procesos. La coherencia de las aplicaciones para servidores Windows se logra mediante VSS. |
| **Almacén de Azure Site Recovery** |Puede crear un almacén de Site Recovery con una suscripción de Azure y registra los servidores en el almacén de Hola. |almacén de Hello coordina y organiza la replicación de datos, la conmutación por error y la recuperación entre el sitio local y Azure. |
| **Mecanismo de replicación** |**A través de Internet de Hola**: Hola de comunicados y replica los datos desde tooAzure de servidores protegidos en local mediante el canal seguro SSL/TLS en internet. Se trata de una opción predeterminada de Hola.<br/><br/> **VPN/ExpressRoute**: se comunica y replica datos entre servidores locales y Azure a través de una conexión VPN. Necesitará tooset una VPN de sitio a sitio o una conexión de ExpressRoute entre el sitio local y la red de Azure.<br/><br/> Se seleccionará cómo desea tooreplicate durante la implementación de Site Recovery. No se puede cambiar el mecanismo de hello tras la configuración sin afectar a la replicación de las máquinas existentes. |Ninguna opción requiere tooopen los puertos de red entrantes en equipos protegidos. Todas las comunicaciones de red se inician desde el sitio local de Hola. |

## <a name="capacity-planning"></a>Planificación de capacidad
áreas principales de Hello, deberá tooconsider:

* **Entorno de origen**: Hola infraestructura de VMware, configuración de la máquina de origen y requisitos.
* **Servidores de componentes**: Hola servidor de procesos, el servidor de configuración y el servidor de destino maestro

### <a name="considerations-for-hello-source-environment"></a>Consideraciones para el entorno de origen Hola
* **Tamaño máximo del disco**: Hola de tamaño máximo actual del disco de Hola que puede ser la máquina virtual de tooa adjunto es 1 TB. Por lo tanto tamaño máximo de Hola de un disco de origen que se pueden replicar también es limitado too1 TB.
* **Tamaño máximo por origen**: tamaño máximo de Hola de una máquina de origen único es 31 TB (con 31 discos) y con una instancia de D14 aprovisionados para el servidor de destino maestro Hola.
* **Número de orígenes por servidor de destino principal**: se pueden proteger varias máquinas de origen con un único servidor de destino principal. Sin embargo, no se puede proteger un equipo de origen único en varios servidores de destino maestro, porque como replican los discos, un disco duro virtual que refleja el tamaño de hello del disco de Hola se crea en el almacenamiento de blobs de Azure y se adjunta como un servidor de destino maestro de toohello de disco de datos.  
* **Tasa de cambio diario máximo por origen**: hay tres factores que deben toobe considera al considerar Hola recomienda cambiar velocidad por origen. Para conocer las consideraciones de hello en función de destino se requieren dos e/s por segundo en el disco de destino de Hola para cada operación en el origen de Hola. Esto es porque una lectura de datos antiguos y una operación de escritura de datos nuevos de Hola se realizará en el disco de destino de Hola.
  * **Diariamente cambiar frecuencia compatible con el servidor de procesos de Hola**: una máquina de origen no puede abarcar varios servidores de procesos. Un servidor de proceso único puede admitir hasta too1 TB de tasa de cambio diaria. Por lo tanto, es 1 TB admitido para una máquina de origen de velocidad de cambio de datos diario máximo de Hola.
  * **Rendimiento máximo compatible con el disco de destino de Hola**: renovación máximo por disco de origen no puede ser más de 144 GB/día (con tamaño de escritura de 8 K). Vea la tabla de hello en la sección de destino maestro Hola de rendimiento de Hola y la e/s por segundo de destino de Hola para diversos tamaños de escritura. Este número debe dividirse en dos porque cada origen IOP genera 2 IOPS en el disco de destino de Hola. Obtenga información sobre [Azure destinos de escalabilidad y rendimiento](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) al configurar el destino de Hola para cuentas de almacenamiento premium.
  * **Rendimiento máximo compatible con la cuenta de almacenamiento de Hola**: un origen no puede abarcar varias cuentas de almacenamiento. Dado que una cuenta de almacenamiento tiene un máximo de 20.000 solicitudes por segundo y que cada origen IOP genera 2 IOPS en el servidor de destino maestro de hello, se recomienda que mantener Hola número de IOPS en hello origen too10, 000. Obtenga información sobre [Azure destinos de escalabilidad y rendimiento](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) al configurar el origen de Hola para cuentas de almacenamiento premium.

### <a name="considerations-for-component-servers"></a>Consideraciones para servidores de componentes
Tabla 1 se resumen los tamaños de máquina virtual de hello para la configuración de Hola y servidores de destino maestro.

| **Componente** | **Instancias de Azure implementadas** | **Núcleos** | **Memoria** | **Discos máx.** | **Tamaño del disco** |
| --- | --- | --- | --- | --- | --- |
| Servidor de configuración |A3 estándar |4 |7 GB |8 |1023 GB |
| Servidor de destino principal |A4 estándar |8 |14 GB |16 |1023 GB |
| D14 estándar |16 |112 GB |32 |1023 GB | |
| DS4 estándar |8 |28 GB |16 |1023 GB | |

**Tabla 1**

#### <a name="process-server-considerations"></a>Consideraciones acerca del servidor de procesos
Por lo general el tamaño del servidor de proceso depende de la tasa de cambio diaria de Hola a través de todas las cargas de trabajo protegidas.

* Necesita suficiente proceso tooperform tareas como la compresión en línea y el cifrado.
* servidor de procesos de Hello usa caché basada en disco. Asegúrese de hello seguro recomendado de espacio de la caché y el rendimiento del disco es cambios de datos de hello toofacilitate disponibles almacenados en caso de hello de cuello de botella de red o una interrupción.
* Asegúrese de ancho de banda suficiente para que hello servidor de proceso puede cargar la protección de datos continua del tooprovide de servidor de destino maestro de hello datos toohello.

Tabla 2 proporciona un resumen de las instrucciones de servidor de proceso de Hola.

| **Frecuencia de cambio de datos** | **CPU** | **Memoria** | **Tamaño del disco de caché** | **Rendimiento del disco de caché** | **Entrada/salida de ancho de banda** |
| --- | --- | --- | --- | --- | --- |
| < 300 GB |4 vCPU (2 sockets * 2 núcleos @ 2,5 GHz) |4 GB |600 GB |too10 7 MB por segundo |30 Mbps/21 Mbps |
| too600 300 GB |8 vCPU (2 sockets * 4 núcleos @ 2,5 GHz) |6 GB |600 GB |too15 11 MB por segundo |60 Mbps/42 Mbps |
| 600 GB too1 TB |12 vCPU (2 sockets * 6 núcleos @ 2,5 GHz) |8 GB |600 GB |too20 16 MB por segundo |100 Mbps/70 Mbps |
| > 1 TB |Implementar otro servidor de procesos | | | | |

**Tabla 2**

Donde:

* Entrada es el ancho de banda de descarga (intranet entre el servidor de origen y el proceso de hello).
* Salida es el ancho de banda de carga (internet entre el servidor de procesos de Hola y el servidor de destino maestro). Los números de salida suponen una compresión promedio de servidor de procesos del 30%.
* Para la caché de disco, se recomienda un disco de sistema operativo independiente de 128 GB mínimo para todos los servidores de procesos.
* Hola de rendimiento de disco de memoria caché después de almacenamiento se usan para pruebas comparativas: 8 unidades SAS de 10 K RPM con configuración de RAID 10.

#### <a name="configuration-server-considerations"></a>Consideraciones del servidor de configuración
Cada servidor de configuración puede admitir hasta too100 máquinas de origen con volúmenes de 3 y 4. Si la implementación es mayor se recomienda implementar otro servidor de configuración. Consulte la tabla 1 para las propiedades de máquina virtual predeterminadas de Hola Hola del servidor de configuración.

#### <a name="master-target-server-and-storage-account-considerations"></a>Consideraciones de la cuenta de almacenamiento y el servidor de destino principal
almacenamiento de Hola para cada servidor de destino maestro incluye un disco del sistema operativo, un volumen de retención y los discos de datos. unidad de retención de Hello mantiene diario Hola de cambios de disco durante Hola del período de retención de hello definido en el portal de Site Recovery Hola.  Consulte tooTable 1 para las propiedades de la máquina virtual de Hola Hola maestra del servidor de destino. Tabla 3 se muestra cómo se utilizan discos de hello a4.

| **Instancia** | **Disco del sistema operativo** | **Retención** | **Discos de datos** |
| --- | --- | --- | --- |
| **Retención** |**Discos de datos** | | |
| A4 estándar |1 disco (1 * 1023 GB) |1 disco (1 * 1023 GB) |15 discos (15 * 1023 GB) |
| D14 estándar |1 disco (1 * 1023 GB) |1 disco (1 * 1023 GB) |31 discos (15 * 1023 GB) |
| DS4 estándar |1 disco (1 * 1023 GB) |1 disco (1 * 1023 GB) |15 discos (15 * 1023 GB) |

**Tabla 3**

Planear la capacidad de servidor de destino maestro Hola depende de:

* Las limitaciones y el rendimiento de almacenamiento de Azure
  * número máximo de Hola de alta utilizan discos para una máquina virtual de nivel estándar, es de aproximadamente 40 (20.000/500 IOPS por disco) en una única cuenta de almacenamiento. Conozca los [objetivos de escalabilidad de las cuentas de almacenamiento estándar](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) y de las [cuentas de Premium Storage](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
* Frecuencia de cambio de datos
* Almacenamiento de volúmenes de retención.

Observe lo siguiente:

* Un origen no puede abarcar varias cuentas de almacenamiento. Esto aplica toohello disco de datos que tienen que ver cuentas de almacenamiento de toohello seleccionadas al configurar la protección. discos de retención de SO y Hola Hola suele ir toohello implementa automáticamente la cuenta de almacenamiento.
* volumen de almacenamiento de retención de Hello necesaria depende de la tasa de cambio diaria de Hola y número de Hola de días de retención. Hola almacenamiento de retención requerido por el servidor de destino maestro = renovación total de origen al día * número de días de retención.
* Cada servidor de destino principal tiene solo un volumen de retención. volumen de retención de Hola se comparte entre el servidor de destino maestro de hello discos toohello adjunto. Por ejemplo:
  * Si hay una máquina de origen con 5 discos y cada disco genera 120 IOPS (tamaño de 8 KB) en el origen de hello, esto traduce too240 de IOPS por disco (2 operaciones en disco de destino de Hola por cada origen de E/S). 240 IOPS está dentro de hello Azure por límite de IOPS de disco de 500.
  * En el volumen de retención de hello, esta se convierte en 120 * 5 = 600 IOPS y esto pueden convertirse en un cuello de botella. En este escenario, una buena estrategia podría ser tooadd volumen de retención de más discos toohello y extenderlo a través de, como una configuración de bandas RAID. Esto mejorará el rendimiento porque Hola IOPS se distribuyen en varias unidades. número de Hola de unidades toobe agregado toohello volumen de retención será la siguiente:
    * E/S por segundo total del entorno de origen / 500
    * Renovación total por día desde el entorno de origen (sin comprimir) / 287 GB. 287 GB es el rendimiento máximo de hello compatible con un disco de destino al día. Esta métrica variará en función de tamaño de la escritura de hello con un factor de 8K, porque en este caso 8K es tres supone que el tamaño de escritura. Por ejemplo, si el tamaño de escritura de hello es 4K, a continuación, el rendimiento será 287/2. Y si el tamaño de escritura de hello es 16K el rendimiento será 287 * 2.
* Hola número de cuentas de almacenamiento necesario = origen total de IOPs/10000.

## <a name="before-you-start"></a>Antes de comenzar
| **Componente** | **Requisitos** | **Detalles** |
| --- | --- | --- |
| **Cuenta de Azure** |Necesitará una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). | |
| **Almacenamiento de Azure** |Necesitará un toostore replicado de datos de la cuenta de almacenamiento de Azure<br/><br/> Cualquier cuenta de hello debe ser un [cuenta de almacenamiento con redundancia geográfica estándar](../storage/common/storage-redundancy.md#geo-redundant-storage) o [cuenta de almacenamiento Premium](../storage/common/storage-premium-storage.md).<br/><br/> Debe Hola misma región que Hola servicio Azure Site Recovery en y asociarse con hello misma suscripción. No se admite mover Hola de cuentas de almacenamiento creados mediante hello [nuevo portal de Azure](../storage/common/storage-create-storage-account.md) en grupos de recursos.<br/><br/> toolearn leer más [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md) | |
| **Red virtual de Azure** |Necesitará una red virtual de Azure en qué Hola se implementará el servidor de configuración y el servidor de destino maestro. Debería ser Hola misma suscripción y región como almacén de Azure Site Recovery Hola. Si desea tooreplicate datos a través de un saludo de conexión ExpressRoute o VPN Azure virtual red debe estar conectado tooyour red de local a través de una conexión ExpressRoute o una VPN de sitio a sitio. | |
| **Recursos de Azure** |Asegúrese de que tiene suficientes recursos de Azure toodeploy todos los componentes. Más información en [Límites de suscripción de Azure](../azure-subscription-service-limits.md). | |
| **Máquinas virtuales de Azure** |Deben cumplir con las máquinas virtuales que desea tooprotect [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).<br/><br/> **Recuento de disco**: se admite un máximo de 31 discos en un único servidor protegido<br/><br/> **Tamaños de disco**: la capacidad del disco individual no debe superar los 1023 GB<br/><br/> **Agrupación en clústeres**: no se admiten los servidores en clúster<br/><br/> **Arranque**: no se admite el arranque de Unified Extensible Firmware Interface (UEFI)/Extensible Firmware Interface (EFI)<br/><br/> **Volúmenes**: no se admiten los volúmenes cifrados de Bitlocker<br/><br/> **Nombres de servidor**: los nombres deben contener entre 1 y 63 caracteres (letras, números y guiones). nombre de Hello debe empezar con una letra o un número y terminar por una letra o un número. Después de proteger una máquina puede modificar Hola nombres de Azure. | |
| **Servidor de configuración** |Se creará la máquina de virtual A3 estándar, en función de una imagen de la Galería de recuperación de sitio de Azure Windows Server 2012 R2 en la suscripción para el servidor de configuración de Hola. Se crea como Hola primera instancia de un nuevo servicio de nube. Si selecciona red pública de Internet como tipo de conectividad de Hola para servicio de nube de hello configuración server Hola se creará con una dirección IP pública reservada.<br/><br/> ruta de instalación de Hello debe tener sólo caracteres del alfabeto inglés. | |
| **Servidor de destino principal** |Máquina virtual de Azure estándar A4, D14 o DS4.<br/><br/> ruta de instalación de Hello debe tener sólo caracteres del alfabeto inglés. Por ejemplo debe ser la ruta de acceso de hello **/usr/local/ASR** para un servidor de destino maestro que ejecutan Linux. | |
| **Servidor de proceso** |Puede implementar el servidor de procesos de hello en una máquina virtual que ejecuta Windows Server 2012 R2 con las últimas actualizaciones de Hola o física. Instálelo en la unidad C:/.<br/><br/> Se recomienda colocar el servidor de hello en hello misma red y subred como Hola máquinas que desee tooprotect.<br/><br/> Instalar VMware vSphere CLI 5.5.0 en el servidor de procesos de Hola. componente de Hello VMware vSphere CLI se requiere en el servidor de procesos de hello en máquinas virtuales orden toodiscover que administra un servidor vCenter o máquinas virtuales que se ejecutan en un host ESXi.<br/><br/> ruta de instalación de Hello debe tener sólo caracteres del alfabeto inglés.<br/><br/> No se admite el sistema de archivos ReFS. | |
| **VMware** |Un servidor VMWare vCenter que administra los hipervisores de VMware vSphere. Se debería estar ejecutando vCenter versión 5.1 ó 5.5 con las actualizaciones más recientes de Hola.<br/><br/> Uno o varios de los hipervisores de vSphere que contiene máquinas virtuales de VMware que desee tooprotect. Hola hipervisor debe disponer de ESX/ESXi versión 5.1 ó 5.5 con las actualizaciones más recientes de Hola.<br/><br/> Las máquinas virtuales de VMware deben tener herramientas de VMware instaladas y en ejecución. | |
| **Máquinas de Windows** |Los servidores físicos protegidos o las máquinas virtuales VMWare con Windows tienen una serie de requisitos.<br/><br/> Un sistema operativo de 64 bits compatible: **Windows Server 2012 R2**, **Windows Server 2012** o **Windows Server 2008 R2 con SP1 como mínimo**.<br/><br/> Hola, nombre de host, los puntos de montaje, nombres de dispositivo, ruta de acceso de sistema de Windows (p. ej.: C:\Windows) debe estar en inglés solamente.<br/><br/> sistema operativo de Hello debe instalarse en la unidad C:\.<br/><br/> Solo se admiten discos básicos. No se admiten discos dinámicos.<br/><br/> Las reglas de Firewall en equipos protegidos deben permitirles servidores de destino maestro y configuración Hola de tooreach en Azure.p ><p>Necesitará una cuenta de administrador de tooprovide (debe ser un administrador local en el equipo de Windows hello) toopush instalar servicio de movilidad de hello en los servidores de Windows. Si Hola proporcionada es una cuenta de dominio no necesitará toodisable control de acceso de usuarios remotos en el equipo local de Hola. toodo esta entrada del registro LocalAccountTokenFilterPolicy DWORD con un valor de 1 en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System Hola de agregar. entrada de registro de hello tooadd desde una CLI abra cmd o powershell y escriba  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** . [Más información](https://msdn.microsoft.com/library/aa826699.aspx) sobre el control de acceso.<br/><br/> Después de la conmutación por error, si desea conectar máquinas virtuales de tooWindows en Azure con Escritorio remoto Asegúrese de que Escritorio remoto está habilitado para la máquina local de Hola. Si no se está conectando a través de VPN, las reglas de firewall deben permitir conexiones de escritorio remoto a través de hello internet. | |
| **Equipos Linux** |Un sistema operativo de 64 bits admitidos: **Centos 6.4, 6.5, 6.6**; **Oracle Enterprise Linux 6.4, 6.5 ejecuta kernel compatible de Red Hat de Hola o separable Enterprise Kernel versión 3 (UEK3)**, **SUSE Linux Enterprise Server 11 SP3**.<br/><br/> Las reglas de Firewall en equipos protegidos deben permitirles tooreach configuración de Hola y servidores de destino maestro en Azure.<br/><br/> los archivos / etc/hosts en equipos protegidos deben contener las entradas que asignan las direcciones del nombre tooIP de hello host local asociadas a todas las NIC <br/><br/> Si desea que tooconnect tooan virtual de Azure máquina Linux ejecución después de conmutación por error mediante un Secure Shell cliente (ssh), asegúrese de ese servicio de Secure Shell en hello protegido Hola máquina configurada toostart automáticamente en el arranque del sistema, y que las reglas de firewall permiten un ssh tooit de conexión.<br/><br/> nombre de host de Hello, puntos de montaje, nombres de dispositivo y las rutas de acceso de sistema de Linux y nombres de archivo (por ejemplo, / etcetera /; / usr) deben estar en inglés solamente.<br/><br/> Se puede habilitar la protección para máquinas locales con hello después de almacenamiento:-<br>Sistema de archivos: EXT3, ETX4, ReiserFS, XFS<br>Software de múltiples rutas / asignador de dispositivos (múltiples rutas)<br>Administrador de volúmenes: LVM2<br>No se admiten servidores físicos con almacenamiento de controlador HP CCISS. | |
| **Terceros** |Algunos componentes de implementación en este escenario dependen toofunction de otros fabricantes de software correctamente. Para obtener una lista completa, consulte [Avisos e información de software de terceros](#third-party) | |

### <a name="network-connectivity"></a>Conectividad de red
Tiene dos opciones para configurar la conectividad de red entre el sitio local y Hola red virtual de Azure en qué Hola se implementan los componentes de la infraestructura (servidor de configuración, los servidores de destino maestro). Necesitará toodecide qué toouse de opción de conectividad de red antes de puede implementar el servidor de configuración. Necesitará toochoose esta configuración en el momento de saludo de la implementación. No puede cambiarse más adelante.

**Internet:** comunicación y la replicación de datos entre servidores locales de hello (servidor de procesos, equipos protegidos) y servidores de componentes de infraestructura de Azure hello (servidor de configuración, el servidor de destino maestro) se realiza a través de un seguro SSL / Conexión TLS de extremos públicos de toohello local en los servidores de destino de configuración y el maestro de Hola. (Hola única excepción es conexión Hola entre el servidor de procesos de Hola y el servidor de destino maestro de hello en el puerto TCP 9080 que no está cifrado. Solo control información relacionada con toohello protocolo de replicación para el programa de instalación de la replicación se intercambia en esta conexión.)

![Diagrama de implementación Internet](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**VPN**: comunicación y la replicación de datos entre servidores locales de hello (servidor de procesos, equipos protegidos) y servidores de componentes de infraestructura de Azure hello (servidor de configuración, el servidor de destino maestro) se realiza a través de una conexión VPN entre la red local y Azure hello en qué Hola se implementan servidores de destino maestro y servidor de configuración de red virtual. Asegúrese de que la red local está conectado toohello red virtual de Azure mediante una conexión ExpressRoute o una conexión VPN de sitio a sitio.

![Diagrama de implementación VPN](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>Paso 1: Creación de un almacén
1. Inicie sesión en toohello [Portal de administración](https://portal.azure.com).
2. Expanda **Data Services** > **Recovery Services** y haga clic en **Almacén de Site Recovery**.
3. Haga clic en **Crear nuevo	** > **Creación rápida**.
4. En **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.
5. En **región**, seleccione Hola región geográfica para el almacén de Hola. toocheck admite regiones, consulte disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
6. Haga clic en **Crear almacén**.

    ![Almacén nuevo](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

Compruebe tooconfirm de barra de estado de Hola que Hola almacén se creó correctamente. almacén de Hola se mostrarán como **Active** en hello principal **servicios de recuperación** página.

## <a name="step-2-deploy-a-configuration-server"></a>Paso 2: Implementación de un servidor de configuración
### <a name="configure-server-settings"></a>Configuración del servidor
1. Hola **servicios de recuperación** página, haga clic en página de inicio rápido de hello almacén tooopen Hola. Inicio rápido también se puede abrir en cualquier momento mediante el icono de Hola.

    ![Icono de inicio rápido](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. En la lista desplegable de hello, seleccione **entre un sitio local con servidores físicos/VMware y Azure**.
3. En **Preparar los recursos de destino (Azure)**, haga clic en **Implementar el servidor de configuración**.

    ![Implementar el servidor de configuración](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. En **Nuevos detalles del servidor de configuración** , especifique:

   * Un nombre para tooit de tooconnect de servidor y las credenciales para la configuración de Hola.
   * En el tipo de conectividad de red de Hola de lista desplegable seleccione **red pública de Internet** o **VPN**. Tenga en cuenta que una vez que se aplica esta configuración no se puede modificar.
   * Seleccione Hola red de Azure en qué Hola server debe estar ubicado. Si usa VPN, asegúrese seguro Hola red de Azure es red local de tooyour conectado según lo previsto.
   * Especifique la dirección IP interna de Hola y de las subredes que se va a asignar a toohello server. Tenga en cuenta que Hola cuatro primeras direcciones IP en una subred están reservados para uso interno de Azure. Utilice cualquier dirección IP disponible.

     ![Implementar el servidor de configuración](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. Al hacer clic en **Aceptar** se creará una máquina de virtual A3 estándar basada en una imagen de la Galería de recuperación de sitio de Azure Windows Server 2012 R2 en su suscripción de servidor de configuración de Hola. Se crea como Hola primera instancia de un nuevo servicio de nube. Si seleccionó tooconnect a través del servicio en la nube Hola Hola internet se crea con una dirección IP pública reservada. Puede supervisar el progreso en hello **trabajos** ficha.

    ![Supervisión de progreso](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. Si se está conectando a través de Hola a internet, una vez implementado Nota Hola pública IP dirección asignada tooit en hello servidor de configuración de hello **máquinas virtuales** página Hola portal de Azure. A continuación, en hello **extremos** puerto público de HTTPS de ficha Nota Hola asignado tooprivate puerto 443. Necesitará esta información más adelante al registrar servidores de procesos y de destino maestro Hola con servidor de configuración de Hola. servidor de configuración de Hola se implementa con estos puntos de conexión:

   * HTTPS: Un puerto público es toocoordinate usa la comunicación entre servidores de componentes y Hola de Azure a través de internet. Puerto privado 443 es toocoordinate usa la comunicación entre servidores de componentes y Azure a través de VPN.
   * Personalizado: Un puerto público se utiliza para la comunicación de la herramienta de conmutación por recuperación a través de hello internet. El puerto privado 9443 se usa para la herramienta de conmutación por recuperación a través de una VPN.
   * PowerShell: puerto privado 5986
   * Escritorio remoto: puerto 3389 privado

   ![Extremos de VM](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > No eliminar ni cambiar número de puerto público o privado de Hola de los puntos de conexión creados durante la implementación de servidor de configuración.
   >
   >

servidor de configuración de Hola se implementa en un servicio de nube de Azure creados de forma automática con una dirección IP reservada. Hello dirección reservada forma tooensure necesario que la dirección IP del servicio de nube de servidor de configuración de Hola Hola sigue siendo igual durante el reinicio de hello las máquinas virtuales (incluido el servidor de configuración de hello) de servicio en la nube Hola. Hello dirección IP pública reservada deberá toobe manualmente cuando se retira el servidor de configuración de Hola o deberá permanecer reservada. Hay un límite predeterminado de 20 direcciones IP públicas reservadas por suscripción. [Más información](../virtual-network/virtual-networks-reserved-private-ip.md) sobre las direcciones IP reservadas.

### <a name="register-hello-configuration-server-in-hello-vault"></a>Registrar el servidor de configuración de hello en el almacén de Hola
1. Hola **inicio rápido** página haga clic en **preparar recursos de destino** > **descargar una clave de registro**. archivo de clave de Hola se genera automáticamente. Es válido durante 5 días a partir del momento en que se genera. Cópielo toohello servidor de configuración.
2. En **máquinas virtuales** servidor de configuración de hello seleccione de la lista de máquinas virtuales de Hola. Abra hello **panel** ficha y haga clic en **conectar**. **Abra** Hola descargado toolog de archivo RDP en el servidor de configuración de hello mediante Escritorio remoto. Si usas VPN, usar dirección IP interna de hello (dirección de Hola que especificó cuando implementa el servidor de configuración de hello) para una conexión a Escritorio remoto desde el sitio local de Hola. Hola Asistente de instalación de servidor de configuración de Azure Site Recovery se ejecuta automáticamente al iniciar la sesión para hello primera vez.

    ![Registro](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. En **instalación de Software de terceros** haga clic en **acepto** toodownload e instalar MySQL.

    ![Instalación de MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. En **detalles del servidor MySQL** crear toolog de credenciales en la instancia del servidor MySQL Hola.

    ![Credenciales de MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. En **configuración de Internet** especificar cómo servidor de configuración de Hola se conectará toohello internet. Observe lo siguiente:

   * Si desea que toouse un proxy personalizado debe configurarla antes de instalar el proveedor de Hola.
   * Al hacer clic en **siguiente** una prueba ejecutará la conexión del proxy toocheck Hola.
   * Si usa a un proxy personalizado o el proxy predeterminado requiere autenticación necesitará detalles del proxy hello tooenter, incluidas las credenciales, puerto y dirección de Hola.
   * Hello las siguientes direcciones URL debe ser accesible a través de proxy de hello:
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Si tiene basado en la dirección IP reglas de firewall Asegúrese de que las reglas de Hola se establecen comunicación tooallow de hello configuración toohello direcciones IP del servidor se describe en [intervalos de IP del centro de datos de Azure](https://msdn.microsoft.com/library/azure/dn175718.aspx) y el protocolo HTTPS (443). ¿Tienen intervalos IP de toowhite-list de hello región de Azure que piensa toouse y del oeste de Estados Unidos.

     ![Registro de proxy](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. En **configuración de localización del mensaje de Error de proveedor** especificar en qué idioma desea tooappear de mensajes de error.

    ![Registro de mensajes de error](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. En **el registro de recuperación del sitio de Azure** examinar y archivo de clave de hello seleccione copió toohello server.

    ![Registro de archivo de clave](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. En la realización de hello página del Asistente para hello seleccione estas opciones:

   * Seleccione **iniciar el cuadro de diálogo de cuenta de administración** toospecify que Hola cuadro de diálogo Administrar cuentas debería abrir después de finalizar el Asistente de Hola.
   * Seleccione **crear un icono del escritorio para Cspsconfigtool** tooadd un acceso directo del escritorio en el servidor de configuración de Hola para que puedan abrir hello **administrar cuentas de** cuadro de diálogo en cualquier momento sin necesidad de hello toorerun Asistente.

     ![Registro completado](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. Haga clic en **finalizar** Asistente de hello toocomplete. Se genera una frase de contraseña. Cópielo tooa de ubicación segura. Podrá necesita tooauthenticate y registrar el proceso de Hola y los servidores de destino maestro con el servidor de configuración de Hola. También ha utilizado la integridad de canal de tooensure en las comunicaciones entre el servidor de configuración. Puede volver a generar frase de contraseña de hello pero, a continuación, necesitará destino maestro de hello toore el registro y los servidores de procesos con hello nueva frase de contraseña.

    ![Frase de contraseña](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

Después del registro el servidor de configuración de Hola se mostrarán en hello **servidores de configuración** página en el almacén de Hola.

### <a name="set-up-and-manage-accounts"></a>Configuración y administración de cuentas
Durante la implementación de Site Recovery solicita sus credenciales para hello siguientes acciones:

* Una cuenta de VMware para que Site Recovery pueda detectar automáticamente las máquinas virtuales en los servidores vCenter o los hosts de vSphere.
* Al agregar máquinas para la protección, para que la recuperación del sitio puede instalar el servicio de movilidad de hello en ellos.

Una vez que haya registrado el servidor de configuración de hello puede abrir hello **administrar cuentas de** tooadd de cuadro de diálogo y administrar las cuentas que deben utilizarse para estas acciones. Hay un par de maneras toodo esto:

* Abrir el acceso directo de hello ha elegido toocreated de cuadro de diálogo de hello en la última página de hello del programa de instalación para el servidor de configuración de hello (cspsconfigtool).
* Cuadro de diálogo Abrir Hola Finalizar del programa de instalación del servidor de configuración.

1. En **Administrar cuentas** click **Agregar cuenta**. También puede modificar y eliminar las cuentas existentes.

    ![Administrar cuentas](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. En **detalles de la cuenta** especificar un toouse de nombre de cuenta en Azure y las credenciales (nombre de dominio/usuario).

    ![Administrar cuentas](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Conectar el servidor de configuración de toohello
Hay dos maneras tooconnect toohello servidor de configuración:

* Mediante una conexión VPN de sitio a sitio o ExpressRoute
* Sobre Hola internet

Observe lo siguiente:

* Una conexión a internet usa los extremos de Hola de máquina virtual de hello junto con la dirección IP virtual pública del saludo del servidor de Hola.
* Una conexión VPN usa la dirección IP interna de Hola de servidor hello junto con puertos privados de punto de conexión de Hola.
* Si es una decisión de un solo uso toodecide tooconnect (control y replicación de datos) de su toohello de servidores locales distintos servidores de componente (servidor de configuración, el servidor de destino maestro) ejecuta en Azure mediante una conexión VPN u Hola internet. No puede cambiar esta configuración posteriormente. Si lo hace, deberá necesita tooredeploy Hola escenario y vuelva a proteger las máquinas.  

## <a name="step-3-deploy-hello-master-target-server"></a>Paso 3: Implementar el servidor de destino maestro Hola
1. Haga clic en **Preparar recursos de destino (Azure)** > **Implementar el servidor de destino maestro**.
2. Especifique las credenciales y detalles del servidor de destino maestro Hola. se implementará el servidor de Hola Hola misma red de Azure como servidor de configuración de Hola. Al hacer clic en toocomplete una máquina virtual se creará con una imagen de galería Windows o Linux.

    ![Configuración de servidor de destino](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

Tenga en cuenta que Hola cuatro primeras direcciones IP en una subred están reservados para uso interno de Azure. Especifique cualquier dirección IP disponible.

> [!NOTE]
> Seleccione estándar DS4 al configurar la protección para cargas de trabajo que requieren coherente alto rendimiento de E/S y la latencia baja de cargas de trabajo de orden toohost E/S intensiva con [cuenta de almacenamiento Premium](../storage/common/storage-premium-storage.md).
>
>

1. Se crea una máquina virtual de servidor de destino maestro de Windows con estos puntos de conexión. Tenga en cuenta que los extremos públicos se crean solo si su conectan a través de internet de Hola.

   * Personalizado: Puerto público utilizado por los datos de replicación de hello proceso servidor toosend sobre Hola internet. Puerto privado 9443 se usa por hello proceso servidor toosend datos toohello destino maestro servidor de replicación a través de VPN.
   * Custom1: Puerto público utilizado por los metadatos de toosend del servidor de proceso de Hola sobre Hola internet. Puerto privado 9080 se usa por servidor de destino maestro toohello de hello proceso servidor toosend metadatos a través de VPN.
   * PowerShell: puerto privado 5986
   * Escritorio remoto: puerto 3389 privado
2. Se crea una máquina virtual de servidor de destino maestro de Linux con estos puntos de conexión. Tenga en cuenta que los extremos públicos se crean solo si se está conectando a través de hello internet.

   * Personalizado: Puerto público utilizado por los datos de replicación de toosend de servidor de proceso a través de Hola internet. Puerto privado 9443 se usa por hello proceso servidor toosend datos toohello destino maestro servidor de replicación a través de VPN.
   * Custom1: Puerto público Hola proceso servidor toosend de metadatos utiliza sobre Hola internet. Se utiliza el puerto privado 9080 por servidor de destino maestro toohello de hello proceso servidor toosend metadatos a través de VPN
   * SSH: puerto privado 22

     > [!WARNING]
     > No eliminar ni cambiar número de puerto público o privado Hola de cualquiera de los puntos de conexión de hello creados durante la implementación de servidor de destino maestro de Hola.
     >
     >
3. En **máquinas virtuales** espere hello toostart de máquina virtual.

   * Si es un detalles del escritorio remoto hello anote server de Windows.
   * Si es un servidor Linux y que se está conectando a través de VPN Nota Hola dirección IP interna de la máquina virtual de Hola. Si se está conectando a través de la dirección IP pública de hello internet Nota Hola.
4. Inicie sesión en la instalación del servidor toocomplete de Hola y registrarlo con el servidor de configuración de Hola.
5. Si está ejecutando Windows:

   1. Iniciar una máquina virtual de toohello de conexión a Escritorio remoto. Hola se ejecutará primera vez que inicie sesión en una secuencia de comandos en una ventana de PowerShell. No la cierre. Cuando termine de herramienta de configuración de agente de Host de Hola abre automáticamente servidor de hello tooregister.
   2. En **configuración de agente de Host** especificar Hola de dirección IP interna del servidor de configuración de Hola y el puerto 443. Puede usar la dirección interna hello y puerto privado 443 incluso si no se está conectando a través de VPN porque es de máquina virtual de hello toohello adjunto misma red de Azure como servidor de configuración de Hola. Deje **Usar HTTPS** habilitado. Escriba la frase de contraseña de hello para el servidor de configuración de Hola que anotó anteriormente. Haga clic en **Aceptar** servidor de hello tooregister. Puede omitir opciones de NAT de Hola. No se usan.
   3. Si el requisito de unidad de retención estimado es de más de 1 TB puede configurar el volumen de retención de hello (R:) usa un disco virtual y [espacios de almacenamiento](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![Servidor de destino principal de Windows](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. Si ejecuta Linux:

   1. Asegúrese de que ha instalado Hola servicios de integración de Linux (LIS) más reciente instalado antes de instalar el servidor de destino maestro Hola. Encontrará la versión más reciente de Hola de LIS junto con instrucciones sobre cómo tooinstall [aquí](https://www.microsoft.com/download/details.aspx?id=46842). Reinicie la máquina de hello después de instalar Hola LIS.
   2. En **Preparar los recursos de destino (Azure)**, haga clic en **Descargar e instalar software adicional (solo para el servidor de destino Linux Master)**. Hola de copia descargado tar archivo toohello máquina virtual a través a un cliente de sftp. También puede iniciar sesión en el servidor de destino maestro de linux implementada toohello y usar *wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* archivo hello de toodownload Hola.
   3. Inicie sesión en el servidor toohello mediante un cliente de Shell seguro. Si está conectado toohello red de Azure a través de VPN usar dirección IP interna de Hola. En caso contrario, usar dirección IP externa de Hola y punto de conexión público de hello SSH.
   4. Extraiga los archivos de hello del instalador de hello comprimido con gzip ejecutando: **tar – xvzf Microsoft-ASR_UA_8.4.0.0_RHEL6-64***
      ![servidor de destino maestro de Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. Asegúrese de que ha iniciado sesión Hola directory toowhich extraer contenido de Hola de archivo tar de Hola.
   6. Copia Hola servidor frase de contraseña tooa local archivo de configuración mediante el comando hello **echo  *`<passphrase>`*  > passphrase.txt**
   7. Ejecute el comando de Hola "**sudo. /Install -t ambos - a host -R MasterTarget -d /usr/local/ASR -i  *`<Configuration server internal IP address>`*  -p 443 -s y - c https -P passphrase.txt**".

      ![Registrar servidor de destino](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. Espere unos minutos (10-15) y aparece en la comprobación de página de hello ese servidor de destino maestro hello como está registrado en **servidores** > **servidores de configuración** **Detallesdelservidor** ficha. Si está ejecutando Linux y no registrará ejecutar Hola host herramienta de configuración nuevo de /usr/local/ASR/Vx/bin/hostconfigcli. Necesitará permisos de acceso de tooset ejecutando chmod como raíz.

    ![Verificar servidor de destino](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> Puede tardar hasta too15 minutos después de que el registro está completado para toobe de servidor de destino maestro Hola aparece en el portal de Hola. inmediatamente, haga clic en la tooupdate **actualizar** en hello **servidores de configuración** página.
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>Paso 4: Implementar el servidor de procesos de hello local
Antes de empezar, se recomienda que configure una dirección IP estática en el servidor de procesos de Hola para que se garantiza a través reinicia toobe persistente.

1. Haga clic en Inicio rápido > **instalar servidor de proceso local** > **descargar e instalar el servidor de procesos de hello**.

    ![Instalar servidor de procesos](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. Hola de copia descargado de servidor de toohello de archivos zip en el que se vayan a servidor de procesos de hello tooinstall. archivo zip de Hello contiene dos archivos de instalación:

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. Descomprima Hola archivo y copia Hola archivos tooa ubicación de instalación en el servidor de Hola.
4. Ejecute hello **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** Hola a archivo de instalación y siga las instrucciones. Esto instala los componentes de terceros necesarios para la implementación de Hola.
5. A continuación, ejecute **Microsoft-ASR_CX_8.4.0.0_Windows***.
6. En hello **modo de servidor** página, seleccione **servidor de procesos**.
7. En hello **detalles del entorno** página Hola siguientes:

    - Si desea hacer clic de máquinas virtuales de VMware tooprotect **sí**
    - Si solo desea tooprotect de servidores físicos y, por tanto, no es necesario vCLI VMware instalado en el servidor de procesos de Hola. Haga clic en **No** y continúe.

1. Tenga en cuenta los siguiente de hello al instalar vCLI de VMware:

   * **Se admite solo VMware vSphere CLI 5.5.0**. servidor de procesos de Hello no funciona con otras versiones o actualizaciones de la interfaz vSphere CLI.
   * Descargue vSphere CLI 5.5.0 desde [aquí.](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * Si ha instalado la interfaz vSphere CLI justo antes de que se ha iniciado la instalación de servidor de procesos de Hola y el programa de instalación no lo detectará, esperar hasta toofive minutos antes de intentarlo de nuevo el programa de instalación. Esto garantiza que todas las variables de entorno de hello necesitan para la detección de interfaz vSphere CLI ha se ha inicializado correctamente.
2. En **selección de NIC en servidor de procesos** adaptador de red de hello seleccione debe usar ese servidor de procesos de Hola.

   ![Seleccionar adaptador](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. En **Detalles del servidor de configuración**:

   * Para dirección IP de Hola y el puerto, si se está conectando a través de VPN especificar dirección IP interna de Hola Hola del servidor de configuración y 443 para el puerto de Hola. En caso contrario, especifique dirección IP virtual pública Hola y punto de conexión HTTP pública asignada.
   * Escriba en la frase de contraseña de Hola Hola del servidor de configuración.
   * Desactive **firma de software de servicio de movilidad comprobar** si desea toodisable comprobación cuando se usa el servicio de inserción automática tooinstall Hola. Comprobación de la firma tiene conectividad a internet en el servidor de procesos de Hola.
   * Haga clic en **Siguiente**.

   ![Registrar servidor de configuración](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. En **Seleccionar unidad de instalación** , seleccione una unidad de caché. servidor de procesos de Hello necesita una unidad de memoria caché con un mínimo de 600 GB de espacio libre. Luego haga clic en **Instalar**.

   ![Registrar servidor de configuración](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. Tenga en cuenta que puede ser necesario instalación de toorestart Hola server toocomplete Hola. En **servidor de configuración** > **detalles del servidor** comprobar dicho servidor de proceso de hello aparece y se ha registrado correctamente en el almacén de Hola.

> [!NOTE]
> Esta operación puede tardar too15 minutos una vez completado para hello proceso servidor tooappear como se muestra en el servidor de configuración de hello registro. tooupdate actualizar inmediatamente, el servidor de configuración de hello haciendo clic en el botón de actualización de hello final Hola de página del servidor de configuración de Hola
>
>

![Validar servidor de procesos](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

Si no deshabilita la comprobación de firmas para el servicio de movilidad de hello al registrar el servidor de procesos de hello podrá hacerlo más adelante como se indica a continuación:

1. Inicie sesión en el servidor de procesos de hello como administrador y abra el archivo de hello C:\pushinstallsvc\pushinstaller.conf para su edición. En la sección de hello **[PushInstaller.transport]** agregar esta línea: **SignatureVerificationChecks = "0"**. Guarde y cierre el archivo hello.
2. Reiniciar servicio InMage PushInstall Hola.

## <a name="step-5-update-site-recovery-components"></a>Paso 5: Actualización de los componentes de Site Recovery
Componentes de recuperación de sitio se actualizan desde tootime de tiempo. Cuando estén disponibles nuevas actualizaciones se debe instalar en hello siguiendo el orden:

1. Servidor de configuración
2. Servidor de proceso
3. Servidor de destino principal
4. Herramienta de conmutación por recuperación (vContinuum)

### <a name="obtain-and-install-hello-updates"></a>Obtenga e instale las actualizaciones de Hola
1. Puede obtener las actualizaciones de configuración de hello, proceso y servidores de destino maestro de hello Site Recovery **panel**. Para la instalación de Linux, extraiga los archivos de hello del instalador de hello comprimido con gzip y ejecute el comando de Hola "sudo. / instalar" actualización de hello tooinstall.
2. [Descargar](http://go.microsoft.com/fwlink/?LinkID=533813) Hola última actualización de hello tool(vContinuum) de conmutación por recuperación.
3. Si se ejecutan las máquinas virtuales o servidores físicos que ya tienen instalado el servicio de movilidad de hello, puede obtener actualizaciones para el servicio de hello como se indica a continuación:

   * **Opción 1**: Descarga de actualizaciones
     * [Windows Server 64 (solo 64 bits)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4, 6.5, 6.6 (solo 64 bits)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle Enterprise Linux 6.4, 6.5 (solo 64 bits)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server SP3 (solo 64 bits)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Después de actualizar saludos del servidor de proceso de hello versión actualizada del servicio de movilidad de hello estará disponible en la carpeta C:\pushinstallsvc\repository de hello en el servidor de procesos de Hola.
   * **Opción 2**: si tiene una máquina con una versión anterior de hello instalado el servicio de movilidad, puede actualizar automáticamente el servicio de movilidad de hello en la máquina de Hola desde el portal de administración de Hola.

     1. Asegúrese de que ese servidor de procesos de Hola se actualiza.
     2. Asegúrese de que ese equipo protegido Hola cumple hello [requisitos previos](#install-the-mobility-service-automatically) para insertar automáticamente el servicio de movilidad de hello, para que la actualización de hello funciona según lo previsto.
     3. Grupo de protección de SELECT hello, resaltado Hola protegido máquina y haga clic en **servicio de movilidad de actualización**. Este botón solo está disponible si hay una versión más reciente del programa Hola a servicio de movilidad.

         ![Seleccionar servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

En cuentas seleccionadas especificar Hola administrador cuenta toobe utiliza tooupdate Hola mobility service en el servidor de hello protegido. Haga clic en Aceptar y espere Hola desencadenada trabajo toocomplete.

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>Paso 6: Incorporación de los servidores vCenter o los hosts vSphere
1. Haga clic en **servidores** > **servidores de configuración** > servidor de configuración >**Agregar servidor vCenter** tooadd un host de servidor o vSphere de vCenter.

    ![Seleccionar servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. Especificar los detalles de hello servidores o host y seleccione Hola procesos que será usado toodiscover lo.

   * Si no se está ejecutando el servidor de vCenter hello en el puerto 443 de hello predeterminado especificar el número de puerto de hello en qué Hola vCenter está en funcionamiento.
   * servidor de procesos de Hello debe estar en hello igual como Hola vCenter server o host de vSphere de red y no debe tener VMware vSphere CLI 5.5.0 instalado.

     ![Configuración de servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. Una vez finalizada la detección de servidor de vCenter Hola se enumerará en detalles del servidor de configuración de Hola.

    ![Configuración de servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. Si usa un servidor de cuenta sin privilegios de administrador tooadd Hola o host, asegúrese de que cuenta de hello tiene Hola siguientes privilegios:

   * Las cuentas de vCenter deben tener habilitados el centro de datos, el almacén de datos, la carpeta, el host, la red, recursos, vistas de almacenamiento, la máquina virtual y privilegios del conmutador distribuido de vSphere habilitados.
   * cuentas de host de vSphere deben tener Hola Datacenter, almacén de datos, carpeta, Host, red, recursos, Máquina Virtual y privilegios del conmutador de distribuidas vSphere habilitados

## <a name="step-7-create-a-protection-group"></a>Paso 7: Crear un grupo de protección
1. Abra **Elementos protegidos** > **Grupo de protección** > **Crear grupo de protección**.

    ![Crear un grupo de protección](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. En hello **especificar configuración de grupo de protección** página Especifique un nombre para el grupo de Hola y el servidor de configuración de hello seleccione en el que desea que el grupo de Hola de toocreate.

    ![Configuración del grupo de protección](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. En hello **especifique la configuración de replicación** página Configurar opciones de replicación de Hola que se usará para todas las máquinas Hola Hola grupo.

    ![Replicación del grupo de protección](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. Configuración:

   * **Coherencia de múltiples VM**: Si desactiva esta crea puntos de recuperación coherentes con la aplicación compartida en los equipos de Hola Hola grupo de protección. Esta configuración es muy importante cuando se están ejecutando las máquinas de hello en el grupo de protección de Hola Hola la misma carga de trabajo. Todas las máquinas será toohello recuperada mismo punto de datos. Solo disponible para servidores Windows Server.
   * **Umbral de RPO**: se generarán alertas cuando el RPO de replicación de protección de datos continuos de hello supera el valor de umbral RPO de hello configurado.
   * **Retención de punto de recuperación**: especifica un período de retención Hola. Equipos protegidos pueden ser recuperado tooany punto dentro de esta ventana.
   * **Frecuencia de la instantánea de coherencia de la aplicación**: especifica la frecuencia con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación.

Puede supervisar el grupo de protección de hello tal y como se crean en hello **elementos protegidos** página.

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>Paso 8: Configurar las máquinas que desee tooprotect
Necesitará tooinstall Hola servicio de movilidad de máquinas virtuales y servidores físicos que desee tooprotect. Puede hacerlo de dos maneras:

* Push e instalará servicio hello en cada equipo de servidor de procesos de hello automáticamente.
* Instalar servicio de Hola de forma manual.

### <a name="install-hello-mobility-service-automatically"></a>Instalar servicio de movilidad de hello automáticamente
Al agregar Hola de grupo de protección servicio de movilidad de máquinas tooa automáticamente se insertan e instalado en cada equipo por el servidor de procesos de Hola.

**Inserción instalar automáticamente servicio de movilidad de hello en servidores de Windows:**

1. Instalar las últimas actualizaciones de hello en servidor de procesos de hello tal y como se describe en [paso 5: instalar las últimas actualizaciones](#step-5-install-latest-updates)y asegúrese de que ese servidor de procesos de hello está disponible.
2. Asegúrese de no hay conectividad de red entre la máquina de origen de Hola y Hola servidor de procesos y esa máquina de origen hello es accesible desde el servidor de procesos de Hola.  
3. Configurar tooallow de firewall de Windows hello **compartir archivos e impresoras** y **Windows Management Instrumentation**. En configuración de Firewall de Windows, seleccione la opción de Hola "Permitir una aplicación o una característica a través del Firewall" y seleccione aplicaciones de hello tal como se muestra en figura Hola siguiente. Para las máquinas que pertenecen el dominio tooa puede configurar la directiva de firewall de hello con un GPO.

    ![Configuración de firewall](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. instalación de inserción de Hello cuenta usada tooperform Hola debe estar en grupo de administradores de hello en la máquina de hello que desea tooprotect. Estas credenciales solo se usan para la instalación por inserción del servicio de movilidad de Hola y deberá proporcionar al agregar un grupo de protección de máquina tooa.
5. Si Hola proporciona la cuenta no es una cuenta de dominio deberá toodisable control de acceso de usuarios remotos en el equipo local de Hola. toodo esta entrada del registro LocalAccountTokenFilterPolicy DWORD con un valor de 1 en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System Hola de agregar. entrada de registro de hello tooadd desde una CLI abra cmd o powershell y escriba  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .

**Inserción instalar automáticamente servicio de movilidad de hello en servidores Linux:**

1. Instalar las últimas actualizaciones de hello en servidor de procesos de hello tal y como se describe en [paso 5: instalar las últimas actualizaciones](#step-5-install-latest-updates)y asegúrese de que ese servidor de procesos de hello está disponible.
2. Asegúrese de no hay conectividad de red entre la máquina de origen de Hola y Hola servidor de procesos y esa máquina de origen hello es accesible desde el servidor de procesos de Hola.  
3. Asegúrese de que la cuenta de hello es un usuario raíz Hola servidor de origen Linux.
4. Asegúrese de archivo/etc/hosts hello en origen Hola server contiene las entradas que asignan las direcciones del nombre tooIP de hello host local asociadas a todas las NIC de Linux.
5. Instalar openssh más reciente de hello, servidor de openssh, paquetes de openssl en la máquina de hello desea tooprotect.
6. Asegúrese de que SSH está habilitado y ejecutándose en el puerto 22.
7. Habilitar la autenticación de subsistema y la contraseña SFTP en el archivo de hello sshd_config como sigue:

   * a) Inicie sesión como root.
   * b) en Hola archivo/etcetera/ssh/archivo sshd_config, buscar Hola de línea que comienza con **PasswordAuthentication**.
   * c) quite el comentario de línea de Hola y cambie el valor de Hola de "no" demasiado "Sí".

       ![Movilidad de Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * d) línea de hello buscar que comienza con el subsistema y quite el comentario de línea de saludo.

       ![Movilidad de inserción de Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. Asegúrese de que se admite la variante de Linux de máquina de origen Hola.

### <a name="install-hello-mobility-service-manually"></a>Instalar manualmente el servicio de movilidad de Hola
paquetes de software de Hello usan tooinstall Hola Mobility service se encuentran en el servidor de procesos de hello en C:\pushinstallsvc\repository. Inicie sesión en el servidor de procesos de Hola y copia Hola instalación correspondiente paquete toohello máquina de origen en función de tabla de hello siguiente:-

| Sistema operativo de origen | Paquete de Mobility Service en el servidor de procesos |
| --- | --- |
| Windows Server 64 (solo 64 bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4, 6.5, 6.6 (solo 64 bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3 (solo 64 bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4, 6.5 (solo 64 bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**Hola tooinstall servicio de movilidad manualmente en un servidor Windows**, Hola siguientes:

1. Hola copia **Microsoft ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe** paquete desde la ruta de acceso de directorio de servidor de proceso de Hola se muestran en tabla de Hola por encima de la máquina de origen toohello.
2. Instalar servicio de movilidad de hello ejecutando ejecutable hello en la máquina de origen Hola.
3. Siga las instrucciones del instalador de Hola.
4. Seleccione **servicio de movilidad** como rol de Hola y haga clic en **siguiente**.

    ![Instalar Mobility Service](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. Deje el directorio de instalación de hello como ruta de instalación predeterminada de Hola y haga clic en **instalar**.
6. En **configuración de agente de Host** especificar dirección IP de Hola y el puerto HTTPS Hola del servidor de configuración.

   * Si se está conectando a través de hello internet especificar Hola dirección IP virtual pública y el extremo HTTPS público como puerto de Hola.
   * Si se está conectando a través de VPN especifique la dirección IP interna de Hola y 443 para el puerto de Hola. Deje la opción **Usar HTTPS** marcada.

     ![Instalar Mobility Service](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. Especifique la frase de contraseña del servidor de configuración de Hola y haga clic en **Aceptar** tooregister Hola servicio de movilidad con servidor de configuración de Hola.

**toorun desde la línea de comandos de hello:**

1. Copiar Hola frase de contraseña de archivo "C:\connection.passphrase" CX toohello hello en el servidor de Hola y ejecute este comando. En nuestro ejemplo CX hello puerto HTTPS y i 104.40.75.37 es 62519:

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**Instalar manualmente el servicio de movilidad de hello en un servidor Linux**:

1. Copiar archivo de hello tar adecuado basado en la tabla de hello anteriormente, de la máquina de origen de hello proceso servidor toohello.
2. Abrir un programa de shell y extraer Hola tar comprimido archive tooa ruta de acceso local mediante la ejecución`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. Crear un archivo passphrase.txt Hola directorio local toowhich ha extraído contenido Hola de archivo tar de hello escribiendo  *`echo <passphrase> >passphrase.txt`*  de shell.
4. Instalar servicio de movilidad de hello escribiendo  *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* .
5. Especifique el puerto y la dirección IP de hello:

   * Si va a conectar el servidor de configuración de toohello sobre Hola internet especificar Hola Configuración servidor virtual dirección IP pública y pública extremo HTTPS en `<IP address>` y `<port>`.
   * Si se conecta mediante una conexión VPN especificar dirección IP interna de Hola y 443.

**toorun desde la línea de comandos de Hola**:

1. Copie frase de contraseña de Hola de archivo "passphrase.txt" CX toohello hello en el servidor de Hola y ejecute este comando. En nuestro ejemplo CX hello puerto HTTPS y i 104.40.75.37 es 62519:

tooinstall en un servidor de producción:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall en el servidor de destino de hello:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> Al agregar un grupo de protección de tooa de máquinas que se están ejecutando una versión adecuada de hello servicio de movilidad, a continuación, se omite la instalación de inserción de Hola.
>
>

## <a name="step-9-enable-protection"></a>Paso 9: Habilitar protección
protección de tooenable Agregar grupo de protección de tooa servidores físicos y máquinas virtuales. Antes de comenzar, tenga en cuenta que:

* Máquinas virtuales se detectan cada 15 minutos y pueden tardar minutos too15 para ellos tooappear en Azure Site Recovery después de la detección.
* Cambios en el entorno en la máquina virtual de hello (como la instalación de herramientas de VMware) también pueden tardar hasta too15 minutos toobe actualizado en Site Recovery.
* Puede comprobar Hola último detectado tiempo en hello **último contacto a** field para hello vCenter server o el host ESXi en hello **servidores de configuración** página.
* Si tiene un grupo de protección ya creado y agregar un host de servidor o ESXi vCenter después de eso, toma quince minutos para hello Azure Site Recovery portal toorefresh y toobe de máquinas virtuales que se muestran en hello **grupo de protección de agregar máquinas tooa**  cuadro de diálogo.
* Si desea que tooproceed inmediatamente con Agregar grupo de máquinas tooprotection sin tener que esperar para la detección programada de hello, resalte el servidor de configuración de hello (no haga clic en él) y haga clic en hello **actualizar** botón.
* Al agregar máquinas virtuales o grupo de protección de máquinas físicas tooa, servidor de procesos de Hola se inserta automáticamente e instala el servicio de movilidad de hello en el servidor de origen de hello si hello no está ya instalado.
* Mecanismo de inserción automática de hello toowork Asegúrese de que ha configurado los equipos protegidos tal y como se describe en el paso anterior de Hola.

Agregue las máquinas como sigue:

1. Haga clic en **Elementos protegidos** > **Grupos de protección** > **Máquinas** > **Agregar máquinas**. Como práctica recomendada, se recomienda que los grupos de protección deberían reflejar las cargas de trabajo para que agreguen equipos que ejecutan una aplicación específica toohello mismo grupo.
2. En **seleccionar máquinas virtuales** si va a proteger los servidores físicos, Hola **agregar máquinas físicas** proporciona el Asistente de dirección IP de Hola y un nombre descriptivo. A continuación, seleccione la familia de sistemas operativos de Hola.

    ![Agregar servidor V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. En **seleccionar máquinas virtuales** si va a proteger máquinas virtuales de VMware, seleccione un servidor vCenter que administra sus máquinas virtuales (o el host de EXSi hello en el que se está ejecutando) y, a continuación, seleccione las máquinas de Hola.

    ![Agregar servidor V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. En **especificar recursos de destino** seleccione servidores de destino maestro de Hola y toouse de almacenamiento para la replicación y seleccione si se debe utilizar la configuración de Hola para todas las cargas de trabajo. Seleccione [cuenta de almacenamiento Premium](../storage/common/storage-premium-storage.md) al configurar la protección para cargas de trabajo que requieren coherente alto rendimiento de E/S y la latencia baja de cargas de trabajo intensivas de orden toohost E/S. Si desea toouse una cuenta de almacenamiento Premium para los discos de cargas de trabajo, deberá toouse Hola destino maestro de la serie DS. No puede usar discos de almacenamiento premium con máquinas virtuales que no sean de serie DS.

   > [!NOTE]
   > No se admite mover Hola de cuentas de almacenamiento creados mediante hello [nuevo portal de Azure](../storage/common/storage-create-storage-account.md) en grupos de recursos.
   >
   >

    ![Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. En **especificar cuentas** Seleccionar cuenta de hello que desea toouse para instalar el servicio de movilidad de hello en equipos protegidos. se requieren credenciales de cuenta de Hello para la instalación automática del programa Hola a servicio de movilidad. Si no puede seleccionar una cuenta, asegúrese configurar una tal y como se describe en el paso 2. Tenga en cuenta que Azure no puede tener acceso a esta cuenta. Para Windows cuenta de hello de servidor debe tener privilegios de administrador en el servidor de origen de Hola. Para Linux cuenta de hello debe ser raíz.

    ![Credenciales de Linux](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. Haga clic en toofinish de marca de verificación de hello agregar máquinas toohello protección toostart y grupo de replicación inicial para cada máquina. Puede supervisar el estado en hello **trabajos** página.

    ![Agregar servidor V-Center](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. Además, puede supervisar el estado de protección; para ello, haga clic en **Elementos protegidos** > Nombre del grupo de protección > **Máquinas virtuales**. Una vez completada la replicación inicial y máquinas de hello están sincronizando datos mostrarán **Protected** estado.

    ![Trabajos de máquina virtual](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>Establecimiento de propiedades del equipo protegido
1. Cuando los equipos ya tienen el estado **Protegido** , puede configurar sus propiedades de conmutación por error. En detalles del grupo de protección de hello seleccione Hola Hola de equipos y abra **configurar** ficha.
2. Puede modificar el nombre hello que se asignará toohello máquina en Azure después de hello y conmutación por error de tamaño de máquina virtual de Azure. También puede seleccionar hello Azure red toowhich Hola máquina está conectada después de la conmutación por error.

   > [!NOTE]
   > [Migración de redes](../resource-group-move-resources.md) a través de recursos grupos dentro Hola misma suscripción o en las suscripciones no se admite para las redes usadas para la implementación de Site Recovery.
   >
   >

    ![Establecer propiedades de máquina virtual](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

Observe lo siguiente:

* nombre de Hola de hello máquina de Azure debe cumplir con requisitos de Azure.
* De forma predeterminada las máquinas virtuales replicadas en Azure no están conectado tooan red de Azure. Si desea que las máquinas virtuales replicadas toocommunicate Asegúrese de que tooset Hola la misma red de Azure para ellos.
* Si cambia el tamaño de un volumen en un servidor físico o máquina virtual de VMware, entrará en estado crítico. Si necesita toomodify tamaño de hello, Hola siguientes:

  * ) configuración de tamaño de Hola de cambio.
  * b) en hello **máquinas virtuales** , seleccione la máquina virtual de Hola y haga clic en **quitar**.
  * c) en **quitar Máquina Virtual** seleccione opción hello **deshabilite la protección (use para la recuperación de obtención de detalles y cambiar el tamaño del volumen)**. Esta opción deshabilita la protección, pero conserva los puntos de recuperación de hello en Azure.

      ![Establecer propiedades de máquina virtual](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d) vuelva a habilitar la protección de máquina virtual de Hola. Cuando vuelva a habilitar protección de datos de hello para el volumen de hello cambia de tamaño será tooAzure transferido.

## <a name="step-10-run-a-failover"></a>Paso 10: Ejecutar la conmutación por error
Actualmente solo se pueden ejecutar conmutaciones por error no previstas de servidores físicos y máquinas virtuales de VMware protegidos. Tenga en cuenta los siguiente hello:

* Antes de iniciar una conmutación por error, asegúrese de que los servidores de destino de configuración y el maestro de hello estén ejecutando y correcto. De lo contrario, se producirá un error de conmutación por error.
* Las máquinas de origen no se apagan como parte de una conmutación por error no planeada. Realizar una conmutación por error no planeada detiene la replicación de datos para los servidores de hello protegido. Podrá tener toodelete Hola máquinas del grupo de protección de Hola y agregarlos de nuevo en toostart orden proteger máquinas de nuevo una vez finalizada de Hola o no planeada.
* Si desea toofail sobre sin pérdida de datos, asegúrese de que están desactivadas máquinas virtuales de hello sitio primario antes de iniciar la conmutación por error de Hola.

1. En hello **planes de recuperación** página y agregue un plan de recuperación. Especifique los detalles para el plan de Hola y seleccione **Azure** como destino de Hola.

    ![Configurar plan de recuperación](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. En **seleccionar Máquina Virtual** seleccione un grupo de protección y, a continuación, seleccione las máquinas en el plan de recuperación de hello grupo tooadd toohello. [Obtenga más información](site-recovery-create-recovery-plans.md) sobre los planes de recuperación.

    ![Agregar máquinas virtuales](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. Si necesita puede personalizar toocreate grupos del plan de Hola y orden secuencial de hello en qué máquinas en recuperación de hello plan se conmutan por error. También puede agregar avisos para las acciones manuales y los scripts. Hola scripts al recuperar tooAzure puede agregarse mediante [Runbooks de automatización de Azure](site-recovery-runbook-automation.md).
4. Hola **planes de recuperación** plan Hola seleccione y haga clic en la página **conmutación por error imprevista**.
5. En **confirmar conmutación por error** Compruebe la dirección de conmutación por error de hello (tooAzure) y seleccione toofail de punto de recuperación de hello en a.
6. Espere toocomplete de trabajo de conmutación por error de hello y, a continuación, compruebe que Hola conmutación por error funcionó como se esperaba y que Hola replica inicio de máquinas virtuales correctamente en Azure.

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>Paso 11: Conmutación por recuperación a través de máquinas de Azure
[Obtener más información](site-recovery-failback-azure-to-vmware-classic-legacy.md) acerca de cómo toobring los errores a través de máquinas que se ejecutan en Azure nuevo entorno de tooyour local.

## <a name="manage-your-process-servers"></a>Administración de servidores de procesos
servidor de procesos de Hello envía el servidor de destino maestro de toohello de datos de replicación en Azure y detecta el nuevo servidor de vCenter de tooa agregada de máquinas virtuales de VMware. Hola siguientes circunstancias puede ser conveniente toochange servidor de procesos de hello en la implementación:

* Si el servidor de proceso actual de hello deja de funcionar
* Si el punto de recuperación (RPO) de objetivo crece tooan nivel aceptable para su organización.

Si es necesario que puede mover la replicación Hola de algunos o todos los virtual de VMware locales máquinas y tooa servidores físicos diferentes servidor de procesos. Por ejemplo:

* **Error**: si un servidor de procesos se produce un error o no está disponible puede mover el servidor de procesos de tooanother de replicación de máquina protegida. Metadatos de la máquina de origen de Hola y máquina de réplica se ha movido toohello nuevo servidor de procesos y se vuelve a sincronizar datos. nuevo servidor de procesos Hola conectará automáticamente toohello vCenter server tooperform la detección automática. Puede supervisar el estado Hola de servidores de procesos en el panel de Site Recovery Hola.
* **Tooadjust RPO de equilibrio de carga**: para mejorar el equilibrio carga puede seleccionar un servidor de proceso diferente en el portal de Site Recovery de Hola y mueva la replicación de uno o más tooit máquinas para el equilibrio de carga manual. En este caso, los metadatos de origen seleccionado hello y máquinas de réplica son toohello movida nuevo servidor de procesos. servidor de procesos de Hello original permanece conectado toohello vCenter server.

### <a name="monitor-hello-process-server"></a>Servidor de procesos de Hola de Monitor
Si un servidor de procesos está en un estado crítico se mostrará una advertencia de estado en hello panel de recuperación de sitios. Puede hacer clic en la ficha de eventos de hello estado tooopen Hola y explorarlo toospecific trabajos en la ficha trabajos de Hola.

### <a name="modify-hello-process-server-used-for-replication"></a>Modificar el servidor de procesos de hello usada para la replicación
1. Abra **Servidores** > **Servidores de configuración** > Servidor de configuración > **Detalles del servidor**.
2. Haga clic en **servidores de procesos** > **Cambiar servidor de proceso** siguiente servidor toohello desea toomodify.

    ![Cambiar servidor de proceso 1](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. En **Cambiar servidor de proceso** > **servidor de procesos de destino** seleccione Hola nuevo servidor que desee toouse y, a continuación, seleccione hello las máquinas virtuales que desea tooreplicate toohello nuevo servidor. Haga clic en hello información icono siguiente toohello nombre del servidor para obtener más información de espacio libre y memoria usada. espacio promedio Hola que será necesario tooreplicate toohello de máquina virtual seleccionada cada nuevo servidor de procesos es toohelp mostrado realizar decisiones de carga.

    ![Cambiar servidor de proceso 2](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. Haga clic en toobegin de marca de verificación de hello replicar toohello nuevo servidor de procesos. Tenga en cuenta que si quita todas las máquinas virtuales de un servidor de procesos que era crítico debería ya no se mostrarán una advertencia crítica en el panel de Hola.

## <a name="third-party-software-notices-and-information"></a>Avisos e información de software de terceros
Do Not Translate or Localize

software de Hola y firmware que se ejecuta Hola técnico de Microsoft o servicio se basa en o incorpora material de hello proyectos enumerados a continuación (colectivamente, "código de terceros").  Microsoft es hello autor no original del programa Hola a código de terceros.  Hola aviso de propiedad intelectual y licencia, en la que Microsoft ha recibido este código de terceros, se establecen estipulado más adelante.

información de Hello en la sección A se con respecto a otro código de terceros componentes de proyectos de Hola se enumeran a continuación. Such licenses and information are provided for informational purposes only.  Este código de terceros se está tooyou relicensed por Microsoft en términos de los productos de Microsoft de Hola y servicio de licencias de software de Microsoft.  

información de Hello en la sección B se con respecto a los componentes de código de terceros que se están realizando tooyou disponible por parte de Microsoft bajo los términos de licencia original Hola.

podrá encontrar más completa del archivo Hello en hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
