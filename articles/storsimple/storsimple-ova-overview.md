---
title: "información general de Azure StorSimple Virtual Array aaaMicrosoft | Documentos de Microsoft"
description: "Describe hello StorSimple Virtual Array, una solución de almacenamiento integrada que administra las tareas de almacenamiento entre una matriz virtual local y el almacenamiento de nube de Microsoft Azure."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>Introducción toohello StorSimple Virtual Array
## <a name="overview"></a>Información general
Hola Microsoft Azure StorSimple Virtual Array es una solución de almacenamiento integrada que administra las tareas de almacenamiento entre una matriz virtual local ejecuta en un hipervisor y almacenamiento en nube de Microsoft Azure. matriz virtual Hello es un servidor de archivos eficaz, rentable y fácil de administrar o una solución de servidor de iSCSI que elimina muchos problemas de Hola y los gastos asociados con la protección de datos y el almacenamiento de la empresa. matriz virtual Hello es especialmente adecuada para escenarios de oficinas remotas o sucursales.

Este tema proporciona información general de la matriz virtual hello: aquí tiene algunos otros recursos:

* Para obtener prácticas recomendadas, consulte [Prácticas recomendadas de la matriz virtual de StorSimple](storsimple-ova-best-practices.md).
* Para obtener información general de los dispositivos de la serie de hello StorSimple 8000, vaya demasiado[serie StorSimple 8000: una solución de nube híbrida](storsimple-overview.md). 
* Para obtener información acerca de los dispositivos de la serie de hello StorSimple 5000 o 7000, vaya demasiado[ayuda en pantalla de StorSimple](http://onlinehelp.storsimple.com/).

matriz virtual de Hello es compatible con iSCSI de Hola o protocolo de bloque de mensajes del servidor (SMB). Se ejecuta en la infraestructura existente de hipervisor y proporcionan niveles toohello en la nube, copia de seguridad en la nube, restore rápido, recuperación de nivel de elemento y características de recuperación ante desastres.

Hello tabla siguiente resume Hola características importantes de hello StorSimple Virtual Array.

| Característica | StorSimple Virtual Array |
| --- | --- |
| Requisitos de instalación |Usa una infraestructura de virtualización (Hyper-V o VMware) |
| Disponibilidad |Nodo único |
| Capacidad total (incluida la nube) |Seguridad too64 TB de capacidad utilizable por matriz virtual |
| Capacidad local |GB 390 too6.4 TB de capacidad utilizable por matriz virtual (necesidad tooprovision 500 GB too8 TB de espacio en disco) |
| Protocolos nativos |iSCSI o SMB |
| Objetivo de tiempo de recuperación (RTO) |iSCSI: menos de 2 minutos, independientemente del tamaño |
| Objetivo de punto de recuperación (RPO) |Copias de seguridad diarias y a petición |
| Organización en niveles del almacenamiento |Usa calentar toodetermine asignación qué datos deben disponer en niveles o alejar |
| Soporte técnico |Infraestructura de virtualización compatible con el proveedor de Hola |
| Rendimiento |Varía en función de la infraestructura subyacente |
| Movilidad de datos |Puede restaurar toohello mismo dispositivo o el nivel de elemento de recuperación (servidor de archivos) |
| Niveles de almacenamiento |Almacenamiento de hipervisor local y de nube |
| Tamaño del recurso compartido |En capas: una too20 TB; anclado localmente: una copia de seguridad too2 TB |
| Tamaño del volumen |En niveles: 500 GB too5 TB; anclado localmente: 50 GB too500 GB |
| Tamaño del volumen |En capas: una too5 TB; anclado localmente: una copia de seguridad too500 GB |
| Instantáneas |Coherencia frente a bloqueos |
| Recuperación a nivel de elemento |Sí; los usuarios pueden realizar restauraciones desde recursos compartidos |

## <a name="why-use-storsimple"></a>¿Por qué usar StorSimple?
StorSimple conecta a los usuarios y servidores de almacenamiento de tooAzure en minutos, con ninguna modificación de la aplicación.

Hello tabla siguiente describen algunas de las ventajas principales de Hola que hello StorSimple Virtual Array proporciona soluciones.

| Característica | Ventaja |
| --- | --- |
| Integración transparente |matriz virtual de Hello es compatible con iSCSI de Hola o protocolo SMB Hola. movimiento de datos de Hello entre nivel local de Hola y Hola en la nube es usuario toohello transparente y sin problemas. |
| Costos de almacenamiento reducidos |Con StorSimple, proporcionar suficiente almacenamiento local toomeet las necesidades actuales de los datos activos de hello más usado. A medida que aumenten sus necesidades de almacenamiento, StorSimple puede organizar en niveles los datos inactivos en un almacenamiento en la nube que le resulte rentable. Hello datos desduplicados y comprimen antes de enviar en la nube toohello toofurther reducir los requisitos de almacenamiento y gastos. |
| Administración simplificada del almacenamiento |StorSimple permite una administración centralizada de la nube de hello mediante el Administrador de dispositivos de StorSimple toomanage varios dispositivos. |
| Mejor recuperación ante desastres y cumplimiento normativo |StorSimple facilita la recuperación ante desastres más rápida mediante la restauración Hola metadatos inmediatamente y restaurar los datos de hello según sea necesario. Esto significa que las operaciones normales pueden seguir con un mínimo de interrupción. |
| Movilidad de datos |En la nube toohello en capas puede tener acceso desde otros sitios con fines de recuperación y migración de datos. Tenga en cuenta que puede restaurar datos solo toohello virtual matriz original. Sin embargo, usar ante desastres recuperación características toorestore Hola toda la matriz virtual tooanother matriz virtual. |

## <a name="storsimple-workload-summary"></a>Resumen de la carga de trabajo de StorSimple

A continuación, presentamos un resumen de las cargas de trabajo de StorSimple.

|Escenario     |Carga de trabajo     |Compatible      |Restricciones               |
|-------------|-------------|---------------|---------------------------|
|Colaboración ROBO |Uso compartido de archivos     |Sí      |Consulte los [límites máximos del servidor de archivos](storsimple-ova-limits.md).<br></br>Consulte los [requisitos del sistema para versiones de SMB compatibles](storsimple-ova-system-requirements.md).| Todas las versiones     |

## <a name="workflows"></a>Flujos de trabajo
Hola StorSimple Virtual Array es especialmente adecuado para hello siguiendo los flujos de trabajo:

* [Administración del almacenamiento basado en la nube](#cloud-based-storage-management)
* [Copias de seguridad independientes de la ubicación](#location-independent-backup)
* [Recuperación ante desastres y protección de datos](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>Administración del almacenamiento basado en la nube
Puede usar el servicio de administrador de dispositivos de StorSimple de hello ejecutando en hello toomanage portal Azure los datos almacenados en varios dispositivos y en varias ubicaciones. Esto es especialmente útil en escenarios de sucursales distribuidas. Tenga en cuenta que debe crear instancias independientes de hello Administrador de dispositivos de StorSimple servicio toomanage arreglos de discos virtuales y los dispositivos de StorSimple físicos. Tenga en cuenta que esa matriz virtual Hola ahora usa el nuevo portal de Azure hello en lugar de hello portal de Azure clásico.

![Administración del almacenamiento basado en la nube](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>Copias de seguridad independientes de la ubicación
Con la matriz virtual de hello, instantáneas en la nube proporcionan una copia independiente de la ubicación en el momento de un volumen o recurso compartido. Las instantáneas de nube están habilitadas de forma predeterminada y no se pueden deshabilitar. Todos los volúmenes y recursos compartidos son copia de seguridad en hello en el mismo tiempo a través de una única directiva de copia de seguridad diaria, y puede realizar copias de seguridad de ad-hoc adicionales cuando sea necesario.

### <a name="data-protection-and-disaster-recovery"></a>Recuperación ante desastres y protección de datos
matriz virtual de Hello es compatible con hello siguiendo los escenarios de recuperación de desastres y la protección de datos:

* **Restauración de volumen o recurso compartido** : utilizar la restauración de hello como nuevo flujo de trabajo toorecover un volumen o recurso compartido. Utilice este enfoque toorecover Hola todo el volumen o recurso compartido.
* **Recuperación de nivel de elemento** : recursos compartidos de permiten el acceso simplificado toorecent copias de seguridad. Se puede recuperar fácilmente un archivo individual de una clase especial *copia de seguridad* carpeta disponible en la nube de Hola. Esta capacidad de restauración está controlada por el usuario y no es necesario que intervenga el administrador.
* **Recuperación ante desastres** : uso Hola a todos los volúmenes o recursos compartidos tooa nueva matriz virtual toorecover de capacidad de conmutación por error. Crear la nueva matriz virtual de Hola y registrarlo con el servicio de administrador de dispositivos de StorSimple de hello y luego conmutar por error matriz virtual original de Hola. la nueva matriz virtual de Hello, a continuación, presupone recursos Hola aprovisionado. 

## <a name="storsimple-virtual-array-components"></a>Componentes de la matriz virtual de StorSimple
matriz virtual Hola incluye Hola de los componentes siguientes:

* [Matriz virtual](#virtual-array): es un dispositivo de almacenamiento de nube híbrido basado en una máquina virtual aprovisionada en un entorno virtualizado o hipervisor.  
* [Servicio de administrador de dispositivos de StorSimple](#storsimple-device-manager-service) : una extensión de hello portal de Azure que permite administrar uno o varios dispositivos de StorSimple desde una única interfaz web que se puede acceder desde distintas ubicaciones geográficas. Puede usar toocreate de servicio del Administrador de dispositivos de StorSimple de Hola y administrar servicios, ver y administrar dispositivos y las alertas y administrar volúmenes, recursos compartidos y las instantáneas existentes.
* [Interfaz de usuario web local](#local-web-user-interface) : una interfaz de usuario basada en web que es el dispositivo de Hola de tooconfigure utilizado para que puede conectar la red local toohello y, a continuación, registrar el dispositivo de hello con el servicio de administrador de dispositivos de StorSimple de Hola. 
* [Interfaz de línea de comandos](#command-line-interface) : una interfaz de Windows PowerShell que puede usar toostart una sesión de soporte técnico en la matriz virtual Hola.
  Hello las secciones siguientes describen cada uno de estos componentes con más detalle y explican cómo solución Hola organiza los datos, asigna espacio de almacenamiento y facilita la administración de almacenamiento y protección de datos.

### <a name="virtual-array"></a>Matriz virtual
matriz virtual Hello es una solución de almacenamiento de nodo único que proporciona almacenamiento principal, administra la comunicación con el almacenamiento en nube y ayuda a seguridad de hello tooensure y confidencialidad de todos los datos que se almacena en el dispositivo de Hola.

matriz de Hello virtual está disponible en un modelo que está disponible para su descarga. matriz virtual Hello tiene una capacidad máxima de 6,4 TB en un dispositivo hello (con un requisito de almacenamiento subyacente de 8 TB) y 64 TB incluido almacenamiento en nube. 

matriz virtual Hello tiene Hola siguientes características:

* Es rentable Usa la infraestructura de virtualización y se puede implementar en el hipervisor de Hyper-V o VMware existente.
* Reside en el centro de datos de Hola y pueden configurarse como un servidor de iSCSI o un servidor de archivos. 
* Se integra con la nube de Hola.
* Las copias de seguridad se almacenan en la nube de hello, que puede facilitar la recuperación ante desastres y simplifican la recuperación de nivel de elemento (ILR). 
* Puede aplicar la matriz virtual de las actualizaciones toohello, tal y como se les aplicaría tooa de dispositivo físico.

> [!NOTE]
> Una matriz virtual no puede ampliarse. Por lo tanto, es importante tooprovision adecuado del almacenamiento al crear la matriz virtual Hola. 
> 
> 

### <a name="storsimple-device-manager-service"></a>Servicio de administrador de dispositivos de StorSimple
StorSimple de Microsoft Azure proporciona una interfaz de usuario basada en web, servicio de administrador de dispositivos de StorSimple, que permite toocentrally Hola administrar el almacenamiento de StorSimple. Puede usar Hola Hola del tooperform del servicio de administrador de dispositivos de StorSimple siguiente las tareas:

* Administrar varias matrices virtuales de StorSimple desde un único servicio. 
* Configurar y administrar ajustes de seguridad para matrices virtuales de StorSimple. (Cifrado en la nube de hello es dependiente de las API de Microsoft Azure.)
* Configurar las propiedades y las credenciales de la cuenta de almacenamiento.
* Configurar y administrar los volúmenes o recursos compartidos.
* Realizar copias de seguridad y restaurar datos en volúmenes o recursos compartidos.
* Supervisar el rendimiento.
* Revisar la configuración del sistema e identificar posibles problemas.

Utilice Hola Administrador de dispositivos de StorSimple servicio tooperform administración diaria de la matriz virtual.

Para obtener más información, consulte demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-virtual-array-manager-service-administration.md).

### <a name="local-web-user-interface"></a>Interfaz de usuario web local
matriz virtual Hola incluye una interfaz de usuario basada en web que se usa para la configuración de un solo uso y el registro del dispositivo de hello con hello servicio Administrador de dispositivos de StorSimple. Puede usar tooshut hacia abajo y reiniciar matriz virtual hello, ejecutar pruebas de diagnóstico, actualizar el software, cambiar contraseña del Administrador de dispositivos de hello, ver registros del sistema y póngase en contacto con Microsoft Support toofile una solicitud de servicio. 

Para obtener información acerca del uso de Hola interfaz de usuario basada en web, ir demasiado[uso Hola tooadminister de interfaz de usuario basada en web de la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md).

### <a name="command-line-interface"></a>Interfaz de la línea de comandos
Hola incluida Windows PowerShell le permite tooinitiate una sesión de soporte técnico con Microsoft Support para que pueden ayudarle a localizar y solucionar problemas que pueden surgir en la matriz virtual.

## <a name="storage-management-technologies"></a>Tecnologías de administración de almacenamiento
Además matriz virtual toohello y otros componentes, Hola StorSimple solución usa Hola software tecnologías tooprovide acceso rápido tooimportant datos siguientes, reduce el consumo de almacenamiento de información y proteger los datos almacenados en la matriz virtual:

* [Organización automática del almacenamiento en niveles](#automatic-storage-tiering) 
* [Volúmenes y recursos compartidos anclados localmente](#locally-pinned-shares-and-volumes)
* [La desduplicación y la compresión de datos en niveles o copias de seguridad en la nube toohello](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [Copias de seguridad a petición y programadas](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>Organización automática del almacenamiento en niveles
matriz virtual Hello usa un nuevos datos niveles mecanismo toomanage almacenado en hello virtual hello y matriz en la nube. Hay solo dos niveles: almacenamiento en nube matriz virtual local de Hola y Azure. Hola StorSimple Virtual Array organiza automáticamente los datos en niveles de hello en función de un mapa térmico, que realiza un seguimiento de los datos actuales de tooother de uso, edad y relaciones. Datos que se active mayoría (más reciente) se almacena localmente, sin datos menos activos e inactivos están automáticamente migran toohello en la nube. (Todas las copias de seguridad se almacenan en la nube de hello). StorSimple ajusta y reordena las asignaciones de datos y almacenamiento a medida que cambian los patrones de uso. Por ejemplo, cierta información puede volverse menos activo con el tiempo. Cuando se encuentre progresivamente menos activo, está interconectado out toohello en la nube. Si esos mismos datos vuelven a estar activos, está interconectado en la matriz de almacenamiento de toohello.

Los datos de un determinado recurso compartido o volumen en niveles tienen su propio espacio de nivel local. (aproximadamente 10% del espacio total de aprovisionamiento Hola para ese recurso compartido o volumen). Aunque esto reduce el almacenamiento disponible de hello en la matriz virtual de Hola para ese recurso compartido o volumen, se asegura de que la organización en niveles para un recurso compartido o volumen no afectarán necesidades de organización en niveles de Hola de otros recursos compartidos o volúmenes. Por lo tanto, una carga de trabajo muy ocupado en un recurso compartido o volumen no puede forzar todas las otra cargas de trabajo toohello en la nube. 

![Organización automática del almacenamiento en niveles](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> Puede especificar un volumen anclado localmente, en cuyo caso los datos de hello permanecen en la matriz virtual hello y nunca es en niveles toohello en la nube. Para obtener más información, consulte demasiado[anclado localmente volúmenes y recursos compartidos](#locally-pinned-shares-and-volumes).
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>Volúmenes y recursos compartidos anclados localmente
Puede crear útiles recursos compartidos y volúmenes que estén anclados localmente. Esta capacidad garantiza que los datos requeridos por las aplicaciones críticas permanecen en la matriz virtual hello y nunca está en niveles toohello en la nube. Volúmenes y recursos compartidos anclados localmente tienen Hola siguientes características: 

* No son las latencias de toocloud de asunto o problemas de conectividad.
* Siguen beneficiándose de las características de copia de seguridad en la nube y de la recuperación ante desastres de StorSimple.

Puede restaurar un recurso compartido o volumen anclado localmente para que esté organizado en niveles o viceversa. 

Para obtener más información acerca de los volúmenes anclados localmente, vaya demasiado[usar volúmenes de toomanage de servicio de administrador de dispositivos de StorSimple de hello](storsimple-virtual-array-manage-volumes.md).

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>La desduplicación y la compresión de datos en niveles o copias de seguridad en la nube toohello
StorSimple toofurther de usa la desduplicación y datos compresión reducirá los requisitos de almacenamiento en nube de Hola. Desduplicación Hola reduce la cantidad total de los datos almacenados mediante la eliminación de redundancia en el conjunto de datos de hello almacenado. A medida que cambia la información, StorSimple omite los datos de hello sin cambios y captura solo Hola cambios. Además, StorSimple reduce Hola de los datos almacenados mediante la identificación y quitar información duplicada. 

> [!NOTE]
> Datos almacenados en la matriz virtual hello no está desduplicados o comprimidos. Todas la desduplicación y compresión se produce justo antes de que se envían datos de hello toohello en la nube.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>Copias de seguridad a petición y programadas
Características de protección de datos de StorSimple permiten las copias de seguridad a petición de toocreate. Asimismo, si programa una copia de seguridad de forma predeterminada, se asegurará de que se copien los datos a diario. Las copias de seguridad se realizan en forma de Hola de instantáneas incrementales que se almacenan en la nube de Hola. Las instantáneas, que registran los cambios de hello solo desde la última copia de seguridad de hello, se pueden crear y restaurar rápidamente. Estas instantáneas pueden ser muy importantes en escenarios de recuperación ante desastres, ya que reemplazan a los sistemas de almacenamiento secundaria (por ejemplo, copia de seguridad de cinta) y le permiten toorestore tooyour centro de datos o tooalternate los sitios de datos si es necesario.

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo demasiado[prepare portal de la matriz virtual de hello](storsimple-virtual-array-deploy1-portal-prep.md).

