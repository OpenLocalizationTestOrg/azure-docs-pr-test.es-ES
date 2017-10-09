---
title: aaaDesign e implementar Oracle base de datos de Azure | Documentos de Microsoft
description: "Diseño e implementación de una base de datos de Oracle en el entorno de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a>Diseño e implementación de una base de datos de Oracle en Azure

## <a name="assumptions"></a>Supuestos

- Planear la toomigrate una base de datos de Oracle desde tooAzure local.
- En los informes de Oracle AWR tener conocimientos de hello varias métricas.
- Tiene conocimientos básicos sobre el rendimiento de la aplicación y el uso de la plataforma.

## <a name="goals"></a>Objetivos

- Comprender cómo toooptimize la implementación de Oracle en Azure.
- Explorar las opciones de optimización del rendimiento de la base de datos de Oracle en el entorno de Azure.

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a>Hola diferencias entre una implementación local y la implementación de Azure 

Los siguientes son importantes algunas cosas tookeep en cuenta cuando realiza la migración de aplicaciones tooAzure local. 

Una diferencia importante es que en una implementación en Azure, los recursos, como las máquinas virtuales, discos y redes virtuales, se comparten con otros clientes. Además, se pueden limitar los recursos en función de los requisitos de Hola. En lugar de centrarse en evitar errores (MTBF), Azure se centra más en supervivientes error hello (MTTR).

Hello tabla siguiente enumeran algunas de las diferencias de hello entre una implementación local y una implementación de Azure de una base de datos de Oracle.

> 
> |  | **Implementación local** | **Implementación en Azure** |
> | --- | --- | --- |
> | **Redes** |LAN/WAN  |SDN (Redes definidas por software)|
> | **Grupo de seguridad** |Herramientas de restricción de IP y puerto |[Grupo de seguridad de red (NSG)](https://azure.microsoft.com/blog/network-security-groups) |
> | **Resistencia** |MTBF (tiempo medio entre errores) |MTTR (toorecovery de Greenwich)|
> | **Mantenimiento planeado** |Aplicación de revisiones/actualizaciones|[Conjuntos de disponibilidad](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (aplicación de revisiones o actualizaciones administradas por Azure) |
> | **Recurso** |Dedicado  |Compartido con otros clientes|
> | **Regiones** |Centros de datos |[Pares de región](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | **Almacenamiento** |SAN/discos físicos |[Almacenamiento administrado por Azure](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | **Escala** |Escalado vertical |Escalado horizontal|


### <a name="requirements"></a>Requisitos

- Determinar la tasa de tamaño y el crecimiento de la base de datos de Hola.
- Determinar los requisitos de IOPS de hello, que se pueden calcular en función de los informes de Oracle AWR u otra herramientas de supervisión de red.

## <a name="configuration-options"></a>Opciones de configuración

Hay cuatro áreas posibles que puede ajustar el rendimiento de tooimprove en un entorno de Azure:

- Tamaño de la máquina virtual
- Capacidad de proceso de la red
- Tipos y configuraciones de disco
- Configuración de la caché de disco

### <a name="generate-an-awr-report"></a>Generar un informe de AWR

Si tiene un servicio de una base de datos de Oracle y está planeando toomigrate tooAzure, tienes varias opciones. Puede ejecutar Hola Oracle AWR informe tooget Hola métricas (e/s por segundo, Mbps, GiBs y así sucesivamente). A continuación, elija Hola que VM en función de las métricas de Hola que haya recopilado. O bien, puede ponerse en contacto con su información de infraestructura equipo tooget similar.

Puede considerar la posibilidad de ejecutar el informe de AWR durante la carga de trabajo normal y máxima, para poder comparar ambas. En función de estos informes, puede cambiar el tamaño Hola máquinas virtuales en función de la carga de trabajo promedio de Hola o carga de trabajo máxima Hola.

Aquí te mostramos un ejemplo de cómo toogenerate un informe AWR:

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a>Métricas clave

Siguiente es métricas de Hola que puede obtener de hello informe AWR:

- Número total de núcleos
- Velocidad del reloj de la CPU
- Memoria total en GB
- Uso de CPU
- Velocidad de transferencia de datos máxima
- Frecuencia de cambios de E/S (lectura/escritura)
- Velocidad de los registros de rehacer (Mbps)
- Capacidad de proceso de la red
- Tasa de latencia de red (baja/alta)
- Tamaño de la base de datos en GB
- Bytes recibidos a través de SQL * Net de / tooclient

### <a name="virtual-machine-size"></a>Tamaño de la máquina virtual

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a>1. Estimar el tamaño de máquina virtual según el uso de CPU, memoria y E/S de hello informe AWR

Único lo que puede mirar es Hola superior cinco temporizado de primer plano eventos que indican dónde están los cuellos de botella del sistema de Hola.

Por ejemplo, en hello siguiente diagrama, sincronización de archivos de registro de hello es en la parte superior de Hola. Que indica el número de Hola de esperas que sean necesarios para que hello LGWR escribe el archivo de registro de hello registro búfer toohello puesta al día. Estos resultados indican que son necesarios almacenamiento o discos de mejor rendimiento. Además, diagrama hello también muestra número Hola de CPU (núcleos) y la cantidad de Hola de memoria.

![Captura de pantalla de página del informe AWR Hola](./media/oracle-design/cpu_memory_info.png)

Hello siguiente diagrama muestra hello total E/S de lectura y escritura. Hubo 59 leer y 247.3 GB escritas durante el tiempo de presentación del informe de Hola.

![Captura de pantalla de página del informe AWR Hola](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a>2. Elegir una máquina virtual

Basándose en información de Hola que recopiló de hello informe AWR, Hola siguiente paso es toochoose una máquina virtual de un tamaño similar que cumpla sus requisitos. Puede encontrar una lista de máquinas virtuales disponibles en el artículo hello [con optimización para memoria](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a>3. Ajustar tamaño de VM de hello con una serie VM similar en función de hello ACU

Después de que ha elegido Hola VM, preste atención toohello ACU para hello máquina virtual. Puede elegir una máquina virtual diferente en función de hello valor ACU que mejor se adapte a sus requisitos. Para más información, consulte [Unidad de proceso de Azure (ACU)](https://docs.microsoft.com/azure/virtual-machines/windows/acu).

![Captura de pantalla de página de hello ACU unidades](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a>Capacidad de proceso de la red

Hola siguiente diagrama muestra la relación de hello entre rendimiento y la e/s por segundo:

![Captura de pantalla del rendimiento](./media/oracle-design/throughput.png)

rendimiento de la red total de Hola se calcula en función de hello siguiente información:
- Tráfico de SQL*Net
- MBps multiplicado por el número de servidores (secuencia de salida, como Oracle Data Guard)
- Otros factores, como la replicación de aplicaciones

![Captura de pantalla de hello SQL * Net rendimiento](./media/oracle-design/sqlnet_info.png)

En función de los requisitos de ancho de banda de red, hay varios tipos de puerta de enlace para toochoose de. Entre los tipos se incluyen Básica, VpnGw y Azure ExpressRoute. Para obtener más información, vea hello [página de precios de puerta de enlace VPN](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).

**Recomendaciones**

- Latencia de red es mayor implementación de local tooan comparados. El rendimiento puede mejorar considerablemente si se reducen los recorridos de ida y vuelta de red.
- ida y vuelta tooreduce, consolidar las aplicaciones que tengan transacciones elevadas o aplicaciones "locuaces" en hello misma máquina virtual.

### <a name="disk-types-and-configurations"></a>Tipos y configuraciones de disco

- *Discos de sistema operativo predeterminados*: estos tipos de disco ofrecen datos persistentes y almacenamiento en caché. Estos discos están optimizados para el acceso del sistema operativo en tiempo de inicio y no están diseñados para cargas de trabajo transaccionales o de almacenamiento de datos (analíticas).

- *Sin administrar discos*: con estos tipos de disco, administrar cuentas de almacenamiento de Hola que almacenan los archivos de disco duro virtual (VHD) de hello corresponden tooyour discos de máquina virtual. Los archivos VHD se almacenan como blobs de páginas en las cuentas de Azure Storage.

- *Discos administrados por*: Azure administra las cuentas de almacenamiento de Hola que usas para los discos de máquina virtual. Especifique el tipo de disco de hello (premium o estándar) y el tamaño de hello del disco de Hola que necesita. Azure crea y administra el disco de hello en su nombre.

- *Discos de Premium Storage*: estos tipos de disco son más adecuados para las cargas de trabajo de producción. Premium almacenamiento es compatible con discos de máquina virtual pueden ser adjunta toospecific tamaño-series de máquinas virtuales, como las máquinas virtuales de serie DS, DSv2, GS y F. disco de Hello premium incluye tamaños diferentes, y puede elegir entre los discos que van desde too4 de 32 GB, de 096 GB. Cada tamaño de disco tiene sus propias especificaciones de rendimiento. Dependiendo de los requisitos de la aplicación, puede asociar uno o más discos tooyour máquina virtual.

Cuando se crea un nuevo disco administrado desde el portal de hello, puede elegir hello **tipo de cuenta** para el tipo de saludo del disco que desee toouse. Tenga en cuenta que no todos los discos disponibles se muestran en el menú desplegable de Hola. Después de elegir un tamaño de máquina virtual determinado, menú hello muestra el solo Hola premium disponibles almacenamiento SKU que se basan en ese tamaño de máquina virtual.

![Captura de pantalla de página de disco administrado Hola](./media/oracle-design/premium_disk01.png)

Para más información, consulte [Premium Storage de alto rendimiento y Managed Disks para máquinas virtuales](https://docs.microsoft.com/azure/storage/storage-premium-storage).

Después de configurar el almacenamiento en una máquina virtual, podría interesarle discos de tooload prueba Hola antes de crear una base de datos. Conocer la velocidad de E/S de hello en términos de latencia y rendimiento puede ayudarle a determinar si las máquinas virtuales de hello admiten Hola espera que el rendimiento con destinos de latencia.

Existen diversas herramientas para realizar pruebas de carga de aplicaciones, como Oracle Orion, Sysbench y Fio.

Ejecutar prueba de carga de Hola de nuevo después de implementar una base de datos de Oracle. Iniciar las cargas de trabajo normales y pico y Hola resultados muestran Hola línea de base de su entorno.

Puede que sea más importante toosize Hola el almacenamiento basado en tasa de IOPS de hello en lugar de tamaño de almacenamiento de Hola. Por ejemplo, si fuera necesario Hola IOPS es 5000, pero solo tiene 200 GB, todavía puede obtener hello P30 clase premium disco aunque se trata con más de 200 GB de almacenamiento.

tasa de IOPS de Hello puede obtenerse de hello informe AWR. Viene determinado por el registro de recuperación de hello, lecturas físicas y velocidad de escritura.

![Captura de pantalla de página del informe AWR Hola](./media/oracle-design/awr_report.png)

Por ejemplo, el tamaño de puesta al día de hello es 12,200,000 bytes por segundo, lo que es igual de too11.63 MBPs.
Hola IOPS es 12,200,000 / 2,358 = 5,174.

Después de tener una idea clara de los requisitos de E/S de hello, puede elegir una combinación de las unidades que sean más adecuado toomeet esos requisitos.

**Recomendaciones**

- Para el espacio de tablas de datos, distribuir cargas de trabajo de E/S de hello en un número de discos mediante el uso de almacenamiento administrado u Oracle ASM.
- A medida que aumenta el tamaño del bloque de hello E/S para operaciones de lectura intensiva y con muchas escrituras, agregue más discos de datos.
- Aumentar el tamaño de bloque de Hola para procesos secuenciales grandes.
- Utilizar E/S de tooreduce de compresión de datos (para datos e índices).
- Separe los registros de rehacer, sistema, temporales y de deshacer TS en discos de datos independientes.
- No colocar ningún archivo de aplicación en el disco predeterminado del sistema operativo (/dev/sda). Estos discos están optimizados para un tiempo de arranque rápido de la máquina virtual y podría no proporcionar un buen rendimiento para la aplicación.

### <a name="disk-cache-settings"></a>Configuración de la caché de disco

Existen tres opciones para el almacenamiento en caché de host:

- *Solo lectura*: todas las solicitudes se almacenan en caché para lecturas futuras. Se conservan todas las escrituras directamente tooAzure almacenamiento de blobs.

- *Lectura y escritura*: se trata de un algoritmo de "lectura anticipada". Hola lee y escribe se almacenan en caché para las lecturas futuras. Escrituras de no escritura continua conservan la memoria caché local de toohello en primer lugar. Para SQL Server, las escrituras son persistente tooAzure almacenamiento porque usa la escritura a través. También proporciona latencia de disco de hello más baja para cargas de trabajo claros.

- *Ninguno* (deshabilitado): con esta opción, se puede omitir la memoria caché de Hola. Todos los datos de hello es toodisk transferido y tooAzure almacenamiento es persistente. Esto deja de método Hola mayor velocidad de E/S para cargas de trabajo intensivas de E/S. También debe tootake "costo de transacción" en consideración.

**Recomendaciones**

rendimiento de hello toomaximize, es recomendable que comience con **ninguno** para el almacenamiento en caché de host. Almacenamiento Premium, tenga en cuenta que debe deshabilitar barreras"hello" al montar el sistema de archivos de hello con hello **ReadOnly** o **ninguno** opciones. Actualizar archivo/etc/fstab de hello con discos de hello UUID toohello.

Para obtener más información, vea [Premium Storage para VM Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).

![Captura de pantalla de página de disco administrado Hola](./media/oracle-design/premium_disk02.png)

- En los discos del sistema operativo, use el almacenamiento en caché predeterminado **Lectura y escritura**.
- En el caso de SYSTEM, TEMP y UNDO, use la opción **Ninguno** para el almacenamiento en caché.
- Para los datos, utilice **Ninguno** para el almacenamiento en caché. Pero si la base de datos es de solo lectura o de lectura intensiva, use el almacenamiento en caché de **Solo lectura**.

Después de guarda la configuración de disco de datos, no se puede cambiar la configuración de caché de host de Hola a menos que desmonta la unidad de hello en hello nivel del sistema operativo y, a continuación, se vuelva a montar, una vez que haya realizado Hola cambiar.


## <a name="security"></a>Seguridad

Después de que se instala y configura el entorno de Azure, Hola siguiente paso es toosecure la red. Estas son algunas recomendaciones:

- *Directiva NSG*: NSG puede definirse mediante una subred o NIC. Es más fácil acceso toocontrol en nivel de subred Hola tanto para la seguridad y forzar el enrutamiento para cosas como los servidores de seguridad de la aplicación.

- *Jumpbox*: para un acceso más seguro, los administradores deben no conectar directamente toohello servicio de aplicación o base de datos. Se utiliza un jumpbox como un medio entre la máquina de administrador de Hola y recursos de Azure.
![Captura de pantalla de página de topología de hello Jumpbox](./media/oracle-design/jumpbox.png)

    máquina de administrador de Hello debe ofrecer acceso restringido a IP toohello solo jumpbox. Hola jumpbox debe tener acceso toohello aplicación y base de datos.

- *Red privada* (subredes): se recomienda que tiene base de datos y servicio de la aplicación hello en subredes independientes, por lo que puede establecerse un mejor control de directiva de NSG.


## <a name="additional-reading"></a>Lecturas adicionales

- [Configuración de ASM de Oracle](configure-oracle-asm.md)
- [Configuración de la protección de datos de Oracle](configure-oracle-dataguard.md)
- [Configuración de Oracle Golden Gate](configure-oracle-golden-gate.md)
- [Copia de seguridad y recuperación de Oracle](oracle-backup-recovery.md)

## <a name="next-steps"></a>Pasos siguientes

- [Tutorial: Creación de máquinas virtuales de alta disponibilidad](../../linux/create-cli-complete.md)
- [Ejemplos de la CLI de Azure para implementación de máquinas virtuales](../../linux/cli-samples.md)
