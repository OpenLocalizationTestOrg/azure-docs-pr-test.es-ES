---
title: "prácticas recomendadas de aaaBest para StorSimple Virtual Array | Documentos de Microsoft"
description: Describe los procedimientos recomendados de Hola para implementar y administrar hello StorSimple Virtual Array.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>Procedimientos recomendados de la matriz virtual de StorSimple
## <a name="overview"></a>Información general
La matriz virtual de Microsoft Azure StorSimple es una solución de almacenamiento integrada que administra las tareas de almacenamiento de información entre un dispositivo virtual local que se ejecuta en un hipervisor y el almacenamiento de nube de Microsoft Azure. StorSimple Virtual Array es eficaz y rentable toohello alternativo 8000 series físico matriz. matriz virtual Hola puede ejecutar en la infraestructura existente de hipervisor, es compatible con iSCSI de Hola y protocolos SMB de Hola y es ideal para escenarios de oficinas remotas o sucursales. Para obtener más información sobre soluciones de StorSimple de hello, vaya demasiado[información general de Microsoft Azure StorSimple](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx).

Este artículo describen prácticas recomendadas de hello implementadas durante la instalación inicial de hello, implementación y administración de hello StorSimple Virtual Array. Estas prácticas recomendadas proporcionan directrices validadas para el programa de instalación de Hola y la administración de la matriz virtual. Este artículo va dirigido hacia Hola TI, los administradores que implementan y administran Hola arreglos de discos virtuales en sus centros de datos.

Se recomienda una revisión periódica del toohelp de prácticas recomendada de Hola garantizar el dispositivo sigue en cumplimiento de normas cuando se realizan cambios de instalación de toohello u operaciones de flujo. Si surgieran problemas al implementar estos procedimientos recomendados un disco virtual, [póngase en contacto con Microsoft Support](storsimple-virtual-array-log-support-ticket.md) para obtener ayuda.

## <a name="configuration-best-practices"></a>Procedimientos recomendados de configuración
Estas prácticas recomendadas tratan instrucciones de Hola que necesitan toobe seguido durante la instalación inicial de Hola y la implementación de arreglos de discos virtuales de Hola. Estas prácticas recomendadas incluyan esos toohello relacionados configurar aprovisionamiento de máquina virtual de hello, configuración de directiva de grupo, ajustar el tamaño, Hola a redes, configurar cuentas de almacenamiento y crear recursos compartidos y volúmenes de Hola matriz virtual. 

### <a name="provisioning"></a>Aprovisionamiento
StorSimple Virtual Array es una máquina virtual (VM) aprovisionada en hipervisor de hello (Hyper-V o VMware) del servidor host. Al aprovisionar la máquina virtual de hello, asegúrese de que el host es capaz de toodedicate suficientes recursos. Para obtener más información, consulte demasiado[requisitos mínimos recursos](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements) tooprovision una matriz.

Implementar Hola seguir las prácticas recomendadas al aprovisionar la matriz virtual hello:

|  | Hyper-V | VMware |
| --- | --- | --- |
| **Tipo de máquina virtual** |**segunda generación** para su uso con Windows Server 2012, o versiones posteriores, y una imagen *.vhdx* . <br></br> **primera generación** para su uso con Windows Server 2008, o versiones posteriores, y una imagen *.vhd* . |Su utiliza una imagen *.vmdk* , use la versión 8-11 de la máquina virtual. |
| **Tipo de memoria** |Configurar como **memoria estática**. <br></br> No utilice hello **memoria dinámica** opción. | |
| **Tipo de disco de datos** |Aprovisiónelo como **expansión dinámica**.<br></br> **Tamaño fijo** requiere mucho tiempo. <br></br> No utilice hello **diferenciación** opción. |Hola de uso **fino aprovisionar** opción. |
| **Modificación del disco de datos** |No se permiten la expansión ni la reducción. Un intento toodo por lo que produce pérdida de Hola de todos los datos locales de hello en dispositivo. |No se permiten la expansión ni la reducción. Un intento toodo por lo que produce pérdida de Hola de todos los datos locales de hello en dispositivo. |

### <a name="sizing"></a>Ajuste de tamaño
Al asignar el tamaño de la matriz Virtual de StorSimple, considere la posibilidad de hello siguientes factores:

* La reserva local para volúmenes o recursos compartidos. Aproximadamente 12% del espacio de Hola se reserva en el nivel local de Hola para cada volumen en capas aprovisionado o un recurso compartido. Aproximadamente 10% de espacio de hello también está reservado para un volumen anclado localmente para el sistema de archivos.
* Sobrecarga de instantáneas. Aproximadamente 15% de espacio en nivel local Hola está reservado para las instantáneas.
* Necesidad de restauraciones. Si Restaurar como una nueva operación, ajuste de tamaño debe contar con espacio Hola necesita para la restauración. Se realiza la restauración tooa compartido o volumen de hello mismo tamaño.
* Debe asignarse una parte del búfer para cualquier crecimiento inesperado.

En función de hello anterior factores, Hola requisitos de tamaño puede representarse por hello siguiente ecuación:

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

Hello en los ejemplos siguientes ilustran cómo puede ajustar el tamaño de una matriz virtual según sus requisitos.

#### <a name="example-1"></a>Ejemplo 1:
En la matriz virtual, desea toobe puede

* Aprovisionar un volumen en capas o recurso compartido de 2 TB.
* Aprovisionar un volumen en capas o recurso compartido de 1 TB.
* Aprovisionar volumen anclado localmente o recurso compartido de 300 GB.

Para saludo anterior volúmenes o recursos compartidos, hacernos calcular los requisitos de espacio de hello en nivel local Hola.

En primer lugar, para cada volumen/recurso compartido en capas, reserva local sería igual too12% del tamaño de volumen/recurso compartido de Hola. Hola anclado localmente volumen/recurso compartido, de reserva local es 10% de hello localmente anclado (además toohello aprovisionado tamaño) de tamaño de volumen/recurso compartido. En este ejemplo, necesita

* Una reserva local de 240 GB (para un volumen en capas o recurso compartido de 2 TB).
* Una reserva local de 120 GB (para un volumen en capas o recurso compartido de 1 TB).
* 330 GB por volumen anclado localmente o un recurso compartido (agregando el 10% del tamaño de reserva local toohello aprovisionado de 300 GB)

Hello espacio total necesario en el nivel local Hola hasta ahora es: 240 GB + 120 GB + 330 GB = 690 GB.

En segundo lugar, es necesario al menos espacio en el nivel local hello como reserva única de hello más grande. Se utiliza esta cantidad adicional por si tuviera que toorestore desde una instantánea en la nube. En este ejemplo, reserva local más grande de hello es 330 GB (incluida la reserva para el sistema de archivos), por lo que debe agregar ese toohello GB: 690 690 GB + 330 GB = 1020 GB.
Si se realizan las restauraciones posteriores adicionales, siempre se podemos obtener espacio de Hola de operación de restauración anterior de Hola.

En tercer lugar, se necesita el 15% del total local hasta ahora espacio toostore instantáneas locales, por lo que solo el 85% de la está disponible. En este ejemplo, sería alrededor de 1020 GB = 0,85&ast;TB del disco de datos aprovisionado. Por lo tanto, sería disco de datos de aprovisionamiento de hello (1020&ast;(1/0.85)) = 1200 GB = 1,20 TB ~ 1,25 TB (redondeo cuartil toonearest)

Si tiene en cuenta un crecimiento inesperado y nuevas restauraciones, debe aprovisionar un disco local de alrededor de 1,25 - 1,5 TB.

> [!NOTE]
> También se recomienda que ese disco local Hola con aprovisionamiento fino. Esta recomendación es porque solo se necesita espacio para restaurar hello cuando desee toorestore datos que es más de cinco días. Recuperación de nivel de elemento permite datos toorestore para hello cinco últimos días sin necesidad de Hola espacio adicional para la restauración.


#### <a name="example-2"></a>Ejemplo 2:
En la matriz virtual, desea toobe puede

* Aprovisionar un volumen en capas de 2 TB.
* Aprovisionar volumen anclado localmente de 300 GB.

En función del 12 % de reserva de espacio local para volúmenes o recursos compartidos en capas y el 10 % para volúmenes o recursos compartidos anclados localmente, necesitamos

* Una reserva local de 240 GB (para un volumen en capas o recurso compartido de 2 TB).
* 330 GB por volumen anclado localmente o un recurso compartido (agregando el 10% de espacio de 300 GB aprovisionado toohello de reserva local)

Espacio total necesario en el nivel local hello es: 240 GB + 330 GB = 570 GB

Hola local espacio mínimo necesario para la restauración es 330 GB.

15% del disco total es toostore usado instantáneas para que 0.85 solo está disponible. Por lo tanto, es el tamaño del disco hello (900&ast;(1/0.85)) = TB 1,06 ~ 1,25 TB (redondeo cuartil toonearest)

Si tiene en cuenta un crecimiento inesperado, puede aprovisionar un disco local de 1,25-1,5 TB.

### <a name="group-policy"></a>Directiva de grupo
Directiva de grupo es una infraestructura que permite tooimplement configuraciones específicas para usuarios y equipos. Configuración de directiva de grupo se encuentra en objetos de directiva de grupo (GPO), que son toohello vinculado después de contenedores de servicios de dominio de Active Directory (AD DS): sitios, dominios o unidades organizativas (OU). 

Si la matriz virtual que está unido a un dominio, los GPO pueden ser tooit aplicada. Estos GPO pueden instalar aplicaciones como un software antivirus que puede afectar negativamente al funcionamiento de Hola de hello StorSimple Virtual Array.

Por consiguiente, es recomendable que:

* Se asegure de que su matriz virtual está en su propia unidad organizativa (UO) de Active Directory.
* Asegúrese de que ningún objeto de directiva de grupo (GPO) está matriz virtual tooyour aplicada. Puede bloquear la herencia tooensure que Hola matriz virtual (nodo secundario) no heredan automáticamente todos los GPO del primario Hola. Para obtener más información, consulte demasiado[bloquear la herencia de](https://technet.microsoft.com/library/cc731076.aspx).

### <a name="networking"></a>Redes
configuración de red de Hello de la matriz virtual se realiza a través de la interfaz de usuario de web local Hola. Una interfaz de red virtual se habilita a través de hipervisor de hello en el que se aprovisiona la matriz virtual Hola. Hola de uso [configuración de red](storsimple-virtual-array-deploy3-fs-setup.md) página dirección IP de la interfaz de red virtual Hola de tooconfigure, subred y puerta de enlace.  También puede configurar el servidor DNS principal y secundario de hello, la configuración de tiempo y la configuración del proxy opcional para el dispositivo. La mayor parte de la configuración de red de hello es una configuración única. Hola de revisión [StorSimple requisitos de red](storsimple-ova-system-requirements.md#networking-requirements) matriz virtual de hello toodeploying anterior.

Al implementar la matriz virtual, es aconsejable seguir estos procedimientos recomendados:

* Asegúrese de que esa red hello en qué Hola matriz virtual se implementa siempre tenga Hola capacidad toodedicate 5 ancho de banda de Mbps Internet (o más).
  
  * Necesidad de ancho de banda de Internet varía dependiendo de sus características de carga de trabajo y la tasa de Hola de cambio de datos.
  * cambio de datos de Hola que puede controlarse es directamente proporcional tooyour ancho de banda de Internet. Por ejemplo, cuando se realiza una copia de seguridad, un ancho de banda de 5 Mbps puede acomodar un cambio de datos de alrededor de 18 GB en 8 horas. Con cuatro veces más ancho de banda (20 Mbps) puede controlar el cambio de cuatro veces más datos (72 GB).
* Asegúrese de conectividad toohello Internet siempre está disponible. Dispositivos de toohello de conexiones de Internet esporádicos o poco confiables pueden ocasionar una pérdida de acceso toodata en la nube de Hola y dar lugar a una configuración no admitida.
* Si tiene previsto toodeploy el dispositivo como un servidor de iSCSI:
  
  * Le recomendamos que deshabilite hello **obtener dirección IP automáticamente** opción (de host DHCP).
  * Configure las direcciones IP estáticas. Debe configurar un servidor DNS principal y uno secundario.
  * Si define varias interfaces de red en la matriz virtual, solo Hola la primera interfaz de red (de forma predeterminada, esta interfaz es **Ethernet**) puede llegar a la nube de Hola. tipo de hello toocontrol de tráfico, puede crear varias interfaces de red virtual en la matriz virtual (configurada como un servidor de iSCSI) y conectar esas subredes toodifferent de interfaces.
* toothrottle Hola nube ancho de banda sólo (usa matriz virtual hello), configurar la limitación en enrutador de Hola o firewall Hola. Si se define en el hipervisor de limitación, limitará todos los protocolos de hello incluidos SMB e iSCSI en lugar de simplemente Hola nube ancho de banda.
* Asegúrese de que está habilitada la sincronización de hora de los hipervisores. Si mediante Hyper-V, seleccione la matriz virtual Hola Administrador de Hyper-V, vaya demasiado**configuración &gt; Integration Services**y asegúrese de que hello **sincronización de hora** está activada.

### <a name="storage-accounts"></a>Cuentas de almacenamiento
La matriz virtual de StorSimple puede asociarse con una cuenta de almacenamiento individual. Esta cuenta de almacenamiento podría ser una cuenta de almacenamiento generada automáticamente, una cuenta de hello tooanother suscripción relacionados con la misma suscripción que el servicio de Hola o una cuenta de almacenamiento. Para obtener más información, vea cómo demasiado[administrar cuentas de almacenamiento para la matriz virtual](storsimple-virtual-array-manage-storage-accounts.md).

Hola de uso se siguen las recomendaciones para las cuentas de almacenamiento asociadas a la matriz virtual.

* Al vincular varios arreglos de discos virtuales con una única cuenta de almacenamiento, factor en capacidad máxima de hello (64 TB) de una matriz virtual y el tamaño máximo de hello (500 TB) de una cuenta de almacenamiento. Esto limita el número de Hola de tamaño completo arreglos de discos virtuales que se pueden asociar con ese tooabout de cuenta de almacenamiento 7.
* Al crear una nueva cuenta de almacenamiento:
  
  * Se recomienda que cree en hello región más cercana toohello oficinas remotas/sucursales donde la matriz Virtual de StorSimple es toominimize implementado latencias.
  * Tenga en cuenta que las cuentas de almacenamiento no se pueden mover entre diferentes regiones. Tampoco es posible mover servicios entre suscripciones.
  * Usar una cuenta de almacenamiento que implementa redundancia entre centros de datos de Hola. El almacenamiento con redundancia geográfica (GRS), el almacenamiento con redundancia de zona (ZRS) y el almacenamiento con redundancia local (LRS) se admiten para su uso con cualquier matriz virtual. Para obtener más información sobre los diferentes tipos de cuentas de almacenamiento de hello, vaya demasiado[replicación de almacenamiento de Azure](../storage/common/storage-redundancy.md).

### <a name="shares-and-volumes"></a>Recursos compartidos y volúmenes
En una matriz virtual de StorSimple se pueden aprovisionar recursos compartidos cuando está configurada como un servidor de archivos y volúmenes cuando está configurada como un servidor de iSCSI. prácticas recomendadas de Hello para la creación de volúmenes y recursos compartidos están relacionados con tipo hello y tamaño de toohello configurado.

#### <a name="volumeshare-size"></a>Tamaño de volumen o recurso compartido
En una matriz virtual se pueden aprovisionar recursos compartidos cuando está configurada como un servidor de archivos y volúmenes cuando está configurada como un servidor de iSCSI. prácticas recomendadas de Hello para la creación de volúmenes y recursos compartidos relacionadas con el tamaño de toohello y Hola tipo configurado. 

Tenga en hello cuenta seguir las prácticas recomendadas para el aprovisionamiento de recursos compartidos o volúmenes en el dispositivo virtual.

* tamaño de toohello relativa aprovisionado de tamaños de archivo de Hola de un recurso compartido en capas puede afectar el rendimiento niveles de Hola. Si trabaja con archivos de gran tamaño, la salida en niveles se realizará más lentamente. Cuando se trabaja con archivos grandes, se recomienda que ese archivo más grande de hello es menor que 3% del tamaño del recurso compartido de Hola.
* Un máximo de 16 volúmenes o recursos compartidos se puede crear en la matriz virtual Hola. Para los límites de tamaño de Hola de hello localmente anclado y niveles volúmenes o recursos compartidos, siempre hacen referencia toohello [StorSimple Virtual Array limita](storsimple-ova-limits.md).
* Al crear un volumen, factor en hello esperada el consumo de datos, así como el crecimiento futuro. volumen de Hello no se puede expandir más adelante.
* Una vez que se ha creado el volumen de hello, no se puede reducir tamaño de Hola de volumen de hello en StorSimple.
* Al escribir tooa en niveles de volumen de StorSimple, cuando datos del volumen Hola alcanza un cierto umbral (toohello relativa local espacio reservado para el volumen de hello), Hola E/S está limitada. Continuar toowrite toothis volumen ralentiza Hola E/S notablemente. Aunque puede escribir tooa en niveles de volumen más allá de su capacidad aprovisionada (no activamente detenido usuario Hola escribir más allá de la capacidad de hello aprovisionado), verá un efecto de toohello de notificación de alerta se sobrescribe. Una vez que vea alertas de hello, es imperativo tomar medidas correctivas, como eliminar datos de volumen de hello (expansión del volumen actualmente no se admite).
* Para casos de uso de recuperación ante desastres, como número de Hola de recursos compartidos o volúmenes permitidos es 16 y Hola máximo número de recursos compartidos o volúmenes que se pueden procesar en paralelo también es 16, Hola el número de recursos compartidos o volúmenes no tiene una incidencia en el RPO y el RTO.

#### <a name="volumeshare-type"></a>Tipo de volumen o recurso compartido
StorSimple admite dos tipos de volumen/recurso compartido según el uso de hello: anclado localmente y en niveles. Anclado localmente volúmenes o recursos compartidos tienen aprovisionamiento denso mientras que hello en capas volúmenes o recursos compartidos se aprovisionamiento fino. No se puede convertir un tootiered volumen anclado localmente, compartir o *viceversa* una vez creado.

Se recomienda que implemente Hola siguiendo los procedimientos recomendados al configurar StorSimple volúmenes o recursos compartidos:

* Identificar el tipo de volumen de hello en función de las cargas de trabajo de Hola que piensa toodeploy antes de crear un volumen. Use volúmenes anclados localmente para cargas de trabajo que requieren tanto garantías locales de datos (incluso durante una interrupción de la nube) como latencias de nube bajas. Una vez que cree un volumen en la matriz virtual, no se puede cambiar el tipo de volumen Hola de tootiered anclado localmente o *viceversa*. Como ejemplo, cree volúmenes anclados localmente al implementar cargas de trabajo SQL o cargas de trabajo que hospeden máquinas virtuales (VM); use volúmenes en capas para cargas de trabajo del recurso compartido de archivos.
* Active la opción de Hola para datos de archivo menos usados con frecuencia cuando se trabaja con tamaños de archivo grande. Se utiliza un tamaño de fragmento de desduplicación de 512 KB cuando esta opción está habilitada en la nube toohello de transferencia de datos de hello tooexpedite.

#### <a name="volume-format"></a>Formato de volumen
Después de crear volúmenes de StorSimple en el servidor de iSCSI, necesita tooinitialize, montaje, formato hello y volúmenes. Esta operación se realiza en el dispositivo de StorSimple de tooyour de hello host conectado. Prácticas recomendadas siguientes se recomiendan cuando montar y dar formato a los volúmenes de host de StorSimple Hola.

* Dé un formato rápido a todos los volúmenes de StorSimple.
* Al dar formato a un volumen de StorSimple, utilice un tamaño de unidad de asignación (AUS) de 64 KB (el valor predeterminado es 4 KB). Hola se basa 64 KB AUS en pruebas realizadas internamente para cargas de trabajo comunes de StorSimple y otras cargas de trabajo.
* Al usar hello StorSimple Virtual Array configurado como un servidor de iSCSI, no utilice volúmenes distribuidos o discos dinámicos como estos volúmenes o discos no son compatibles con StorSimple.

#### <a name="share-access"></a>Acceso de recurso compartido
Al crear recursos compartidos en un servidor de archivos de la matriz virtual, siga estas directrices:

* Al crear un recurso compartido, asigne un grupo de usuarios como administrador de recursos compartidos, en lugar de usuario individual.
* Puede administrar los permisos de NTFS de hello después de crea el recurso compartido de hello mediante la edición de recursos compartidos de hello mediante el Explorador de Windows.

#### <a name="volume-access"></a>Acceso de volumen
Al configurar los volúmenes iSCSI de hello en la matriz Virtual de StorSimple, es importante toocontrol acceso siempre que sea necesario. toodetermine que hospeda los servidores puede tener acceso a volúmenes, crear y asociar los registros de control de acceso (ACR) con volúmenes de StorSimple.

Usar hello siguiendo los procedimientos recomendados al configurar ACRs para volúmenes de StorSimple:

* Asocie siempre al menos un ACR a un volumen.

* Al asignar más de un volumen ACR tooa, asegúrese de que el volumen de Hola no se expone de forma que puede obtenerse simultáneamente más de un host no agrupado. Si ha asignado varias ACR tooa volumen, un mensaje de advertencia aparece para tooreview la configuración.

### <a name="data-security-and-encryption"></a>Seguridad y cifrado de datos
La matriz Virtual de StorSimple tiene características de seguridad y cifrado de datos que se aseguran de hello confidencialidad e integridad de los datos. Al usar estas características, se recomienda seguir estos procedimientos recomendados: 

* Definir un cifrado de toogenerate clave AES-256 de cifrado de almacenamiento en la nube antes de enviar datos de saludo de la nube de toohello matriz virtual. Esta clave no es necesaria si los datos están cifrado toobegin con. Hello clave se pueden generar y mantener segura con un sistema de administración de claves como [almacén de claves de Azure](../key-vault/key-vault-whatis.md).
* Cuando configurando cuenta de almacenamiento de Hola a través del servicio de StorSimple Manager hello, asegúrese de que habilita Hola SSL modo toocreate un canal seguro para la comunicación de red entre el dispositivo de StorSimple y hello en la nube.
* Claves Hola regenerar para las cuentas de almacenamiento (mediante el acceso a servicio de almacenamiento de Azure de hello) periódicamente tooaccount para cualquier cambia tooaccess basadas en lista de hello cambiado de administradores.
* Datos en la matriz virtual se comprimen y se desduplican antes de enviarlo tooAzure. No se recomienda usar el servicio de rol de desduplicación de datos de hello en el host de Windows Server.

## <a name="operational-best-practices"></a>Procedimientos recomendados operativos
prácticas recomendadas de Hello son instrucciones que se deben seguir durante la administración cotidiana de hello ni el funcionamiento de la matriz virtual Hola. Estas prácticas tratan las tareas de administración específicas como realizar copias de seguridad, restaurar a partir de un conjunto de copia de seguridad, realizar una conmutación por error, desactivar y eliminar matriz hello, supervisión sistema uso y estado, y virus al ejecutar análisis en la matriz virtual.

### <a name="backups"></a>Copias de seguridad
Hola datos en la matriz virtual se copian en la nube toohello de dos maneras, valor predeterminado es automatizar la copia de seguridad diaria de hello todo dispositivo inicio a las 22:30 o a través de una copia de seguridad manual a petición. De forma predeterminada, el dispositivo de hello automáticamente crea instantáneas diarias en la nube de todos los datos de Hola que residen en él. Para obtener más información, consulte demasiado[copia de seguridad la matriz Virtual de StorSimple](storsimple-virtual-array-backup.md).

Hello frecuencia y retención asociado con las copias de seguridad predeterminada de hello no se puede cambiar pero se puede configurar el tiempo de hello en qué Hola copias de seguridad diarias se inician cada día. Para configurar la hora de inicio de Hola de hello automatizado las copias de seguridad, se recomienda que:

* Programar las copias de seguridad para que se realicen en horas de poca actividad. La hora de inicio de la copia de seguridad no debe coincidir con un momento de numerosas E/S del host.
* Iniciar una copia de seguridad manual a petición al planear tooperform una conmutación por error de dispositivo o la ventana de mantenimiento de toohello anteriores, datos de hello tooprotect en la matriz virtual.

### <a name="restore"></a>Restauración
Puede restaurar desde una copia de seguridad de dos maneras: restaurar tooanother volumen o recurso compartido o realizar una recuperación de nivel de elemento (disponible solo en una matriz virtual configurada como un servidor de archivos). Recuperación de nivel de elemento permite toodo una recuperación granular de archivos y carpetas desde una copia de seguridad de la nube de todos los recursos compartidos de hello en dispositivo de StorSimple Hola. Para obtener más información, consulte demasiado[restaurar a partir de una copia de seguridad](storsimple-virtual-array-clone.md).

Al realizar una restauración, tenga Hola siguiendo las directrices descritas en la cuenta:

* La matriz virtual de StorSimple no admite la restauración en contexto. Sin embargo puede ser fácilmente logra mediante un proceso de dos pasos: libere espacio en hello virtual de matriz y, a continuación, restaurar tooanother volumen/recurso compartido.
* Al restaurar desde un volumen local, tenga en la restauración de hello cuenta será una operación larga. Aunque el volumen de hello rápidamente puede ponerse en línea, los datos de hello continúan toobe hidratado en segundo plano de Hola.
* Hola volumen tipo permanece igual Hola durante el proceso de restauración de Hola. Se restaura un volumen en capas tooanother en niveles de volumen y un volumen de tooanother anclado localmente volumen anclado localmente.
* Al intentar toorestore un volumen o un recurso compartido de un conjunto de copia de seguridad, si se produce un error en el trabajo de restauración de hello, un volumen de destino o recurso compartido puede seguirá creando en el portal de Hola. Es importante que elimine este volumen de destino sin usar o compartir en toominimize portal Hola los futuros problemas derivados de este elemento.

### <a name="failover-and-disaster-recovery"></a>Conmutación por error y recuperación ante desastres
Un dispositivo de conmutación por error permite toomigrate los datos de un *origen* dispositivo en hello datacenter tooanother *destino* dispositivo ubicado en hello misma o a una ubicación geográfica diferente. conmutación por error de dispositivo de Hello es para todo dispositivo de Hola. Durante la conmutación por error, cambian los datos de nube hello para el dispositivo de origen de hello toothat propiedad hello de dispositivo de destino.

Para la matriz Virtual de StorSimple, solo puede conmutar por error matriz virtual tooanother administrados por hello mismo servicio StorSimple Manager. No se permite un dispositivo de la serie de conmutación por error tooan 8000 o una matriz que se administra mediante un servicio de StorSimple Manager diferentes (que Hola uno para el dispositivo de origen Hola). toolearn más información acerca de consideraciones de la conmutación por error de hello, vaya demasiado[requisitos previos para la conmutación por error de dispositivo de hello](storsimple-virtual-array-failover-dr.md).

Cuando se realiza por error a través de la matriz virtual, tenga en cuenta los siguiente de hello:

* Para una conmutación por error planeada, es un recomendada de procedimientos recomendados para tootake todos Hola volúmenes o recursos compartidos sin conexión tooinitiating anterior Hola conmutación por error. Siga instrucciones específicas del sistema operativo de hello tootake Hola volúmenes o recursos compartidos sin conexión en hello hospedar en primer lugar y, a continuación, dejarlos sin conexión en el dispositivo virtual.
* Una archivo server recuperación ante desastres (DR), se recomienda que se une toohello de dispositivo de destino de hello mismo dominio como origen de hello, por lo que Hola permisos de recurso compartido se resuelven automáticamente. Hola solo dispositivo de destino de conmutación por error tooa en el mismo dominio que se admite en esta versión de Hola.
* Una vez hello DR se ha completado correctamente, se elimina automáticamente el dispositivo de origen de Hola. Si bien dispositivo Hola ya no está disponible, máquina virtual de Hola que ha aprovisionado en el sistema de host de Hola se siguen consumiendo recursos. Se recomienda que elimine esta máquina virtual desde su tooprevent de sistema host cualquier cargo de acumulación.
* Tenga en cuenta que aunque es incorrecta, la conmutación por error de hello **Hola de datos está siempre en la nube de hello**. Considere la posibilidad de hello en qué Hola conmutación por error no se completó correctamente los tres escenarios siguientes:
  
  * Se produjo un error en fases iniciales de Hola de conmutación por error de hello, como cuando se realizan comprobaciones previas de hello recuperación ante desastres. En esta situación, aún puede usarse el dispositivo de destino. Puede volver a intentar la conmutación por error de hello en hello mismo dispositivo de destino.
  * Se produjo un error durante el proceso de conmutación por error real de Hola. En este caso, el dispositivo de destino de Hola se marca inutilizable. Debe aprovisionar y configurar otra matriz virtual de destino y usarla para la conmutación por error.
  * Hola conmutación por error se completa después de qué dispositivo de origen Hola se eliminó pero dispositivo de destino de hello tiene problemas y no se puede obtener acceso a los datos. datos de Hello están todavía seguros en la nube de Hola y se pueden recuperar fácilmente mediante la creación de otra matriz virtual y, a continuación, lo usa como un dispositivo de destino para la recuperación ante desastres de Hola.

### <a name="deactivate"></a>Desactivación
Cuando desactiva una matriz Virtual de StorSimple, servidor de conexión de hello entre el dispositivo de Hola y el servicio StorSimple Manager correspondiente Hola. La desactivación es una operación **permanente** y no se puede deshacer. Un dispositivo desactivado no se puede registrar con el servicio StorSimple Manager hello nuevo. Para obtener más información, consulte demasiado[desactivar y eliminar la matriz Virtual de StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

Mantener hello las siguientes prácticas recomendadas en cuenta cuando la desactivación de la matriz virtual:

* Crear una instantánea de nube de toodeactivating anteriores de datos un dispositivo virtual de todas las de Hola. Cuando desactiva una matriz virtual, se perderán todos los datos de dispositivo local de Hola. Tomar una instantánea de nube le permitirá toorecover datos en una fase posterior.
* Antes de desactivar una matriz Virtual de StorSimple, realizar toostop seguro o eliminar los clientes y hosts que dependen de dicho dispositivo.
* Elimine los dispositivos desactivados que no vaya a usar, con el fin de que no se acumulen cargos.

### <a name="monitoring"></a>Supervisión
tooensure que la matriz Virtual de StorSimple está en un estado correcto continuado, necesita toomonitor Hola matriz y asegurarse de que recibe información del sistema de hello incluidas las alertas. toomonitor Hola estado general de la matriz virtual de hello, Hola implemente seguir las prácticas recomendadas:

* Configurar el uso de disco de Hola de supervisión tootrack de su disco de datos de matriz virtual, así como el disco del sistema operativo de Hola. Si ejecuta Hyper-V, puede usar una combinación de System Center Virtual Machine Manager (SCVMM) y System Center Operations Manager (SCOM) toomonitor los hosts de virtualización.
* Configurar notificaciones por correo electrónico en las alertas de toosend matriz virtual unos niveles de uso.                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>Aplicaciones de detección de virus y búsqueda en índices
Una matriz Virtual de StorSimple puede interconectar automáticamente datos de hello nivel local toohello nube de Microsoft Azure. Cuando una aplicación como una búsqueda de índice o una detección de virus es datos de hello tooscan usado almacenados en StorSimple, necesita atención de tootake que hello en la nube datos no obtener acceso y extrae nuevo nivel local toohello.

Se recomienda que implemente Hola siguiendo los procedimientos recomendados al configurar el examen de virus o búsqueda de índice de hello en la matriz virtual:

* Deshabilite todas las operaciones de detección configuradas automáticamente.
* Para volúmenes en capas, configure Hola índice búsqueda o virus examen aplicación tooperform un recorrido incremental. Esto podría examinar sólo Hola nuevos datos probable que reside en el nivel local Hola. no se tiene acceso a datos Hello toohello en capas en la nube durante una operación incremental.
* Asegúrese de Hola filtros de búsqueda correcto y se configura para que solo los tipos de hello diseñada de archivos se exploran. Por ejemplo, la imagen archivos (JPEG, GIF y TIFF) y dibujos de ingeniería no deben analizarse durante la regeneración de índice completo o incremental de Hola.

Si utiliza el proceso de indexación de Windows, siga estas directrices:

* No utilice Hola indizador de Windows para volúmenes en capas, ya que recupera grandes cantidades de datos (TBs) de la nube de hello si índice Hola necesita toobe vuelve a generar con frecuencia. Volver a generar índice Hola recuperaría todos los tooindex de tipos de archivo su contenido.
* Usar Windows hello indización de proceso para volúmenes anclados localmente como esto solo podría tener acceso a datos en el índice de hello toobuild de hello niveles local (en la nube hello no tener acceso a datos).

### <a name="byte-range-locking"></a>Bloqueo de intervalo de bytes
Las aplicaciones pueden bloquear un intervalo de bytes especificado dentro de los archivos de Hola. Si está habilitado el bloqueo de intervalo de bytes en las aplicaciones de Hola que están escribiendo tooyour StorSimple, a continuación, niveles no funcionan en la matriz virtual. Para hello toowork niveles, se deben desbloqueadas todas las áreas de archivos de hello ha tenido acceso. El bloqueo del intervalo de bytes no admite los volúmenes en capas de una matriz virtual.

Recomienda medidas bloqueo de intervalo de bytes de tooalleviate incluyen:

* Desactive el bloqueo del intervalo de bytes en la lógica de la aplicación.
* Uso localmente anclado volúmenes (en lugar de en capas) para los datos de hello asociados con esta aplicación. Los volúmenes anclados localmente no nivel en la nube de Hola.
* Al usar anclado localmente volúmenes con bloqueo de intervalo de bytes habilitada, volumen de hello puede ponerse en línea antes de que finalice la restauración de Hola. En estos casos, se debe esperar a hello toobe de restauración completa.

## <a name="multiple-arrays"></a>Varias matrices
Varias matrices virtuales pueden necesitar tooaccount toobe implementado para un espacio de trabajo creciente de datos que pueden retrasar en nube de hello, por tanto, afectan negativamente al rendimiento de hello de dispositivo de Hola. En estos casos, es mejor dispositivos tooscale a medida que aumenta el espacio de trabajo de Hola. Para ello, uno o más toobe dispositivos que agregó en el centro de datos de hello en local. Al agregar dispositivos de hello, puede:

* Hola de división actual conjunto de datos.
* Implementar nuevos dispositivos de toonew de las cargas de trabajo.
* Si implementa varios arreglos de discos virtuales, se recomienda que Equilibrio de carga de perspectiva, distribuir matriz hello en hosts de hipervisor diferentes.
* Se pueden implementar varias matrices virtuales (cuando se configuran un servidor de archivos o un servidor de iSCSI) en un espacio de nombres de un sistema de archivos distribuido. Para obtener instrucciones detalladas, vaya demasiado[archivo sistema Namespace solución distribuida con la Guía de implementación de almacenamiento de nube híbrida](https://www.microsoft.com/download/details.aspx?id=45507). Replicación de sistema de archivos distribuido actualmente no se recomienda para su uso con la matriz virtual Hola. 

## <a name="see-also"></a>Otras referencias
Obtenga información acerca de cómo demasiado[administrar la matriz Virtual de StorSimple](storsimple-virtual-array-manager-service-administration.md) a través de hello el servicio StorSimple Manager.

