---
title: "información general acerca de aaaStorSimple 8000 series soluciones | Documentos de Microsoft"
description: "Describe los niveles de StorSimple, dispositivo hello, dispositivo virtual, servicios y administración de almacenamiento y presenta los términos claves usados en StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>Serie StorSimple 8000: una solución de almacenamiento en la nube híbrida
## <a name="overview"></a>Información general
Página principal de tooMicrosoft StorSimple de Azure, una solución de almacenamiento integrada que administra las tareas de almacenamiento de información entre dispositivos locales y el almacenamiento de nube de Microsoft Azure. StorSimple es una solución de red (SAN) de área de almacenamiento eficaz, rentable y fácil de administrar que elimina muchos problemas de Hola y los gastos asociados con la protección de datos y el almacenamiento de la empresa. Usa el dispositivo de hello propietario StorSimple 8000 series, se integra con servicios en la nube y proporciona un conjunto de herramientas de administración para una vista integrada de todo el almacenamiento empresarial, incluido el almacenamiento en la nube. (información sobre la implementación de hello StorSimple publicada en el sitio Web de Microsoft Azure Hola aplica tooStorSimple 8000 series solo a los dispositivos. Si está utilizando un dispositivo de la serie StorSimple 5000 o 7000, vaya demasiado[StorSimple ayuda](http://onlinehelp.storsimple.com/).)

Usa StorSimple [niveles de almacenamiento](#automatic-storage-tiering) toomanage los datos almacenados en varios medios de almacenamiento. espacio de trabajo actual de Hello está almacenada localmente en unidades de estado sólido (SSD), datos que se utilizan con menor frecuencia se almacenan en unidades de disco duro (HDD) y los datos de archivo se insertan en la nube toohello. Además, StorSimple usa la desduplicación y consume la cantidad de compresión tooreduce Hola de almacenamiento que Hola datos. Para obtener más información, consulte demasiado[desduplicación y la compresión](#deduplication-and-compression). Para obtener definiciones de otros términos y conceptos clave utilizados en la documentación de la serie de hello StorSimple 8000, vaya demasiado[StorSimple terminología](#storsimple-terminology) final Hola de este artículo.

Además de administración toostorage, características de protección de datos de StorSimple habilitan toocreate a petición y copias de seguridad programadas y almacenarlo ellos localmente o en hello en la nube. Las copias de seguridad se realizan en forma de Hola de instantáneas incrementales, lo que significa que se pueden crear y restaurar rápidamente. Instantáneas en la nube pueden ser muy importantes en escenarios de recuperación ante desastres, ya que reemplazan a los sistemas de almacenamiento secundaria (por ejemplo, copia de seguridad de cinta) y le permiten toorestore tooyour centro de datos o tooalternate los sitios de datos si es necesario.

![icono de vídeo](./media/storsimple-overview/video_icon.png) Vea el vídeo de Hola para un tooMicrosoft introducción rápida StorSimple de Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>¿Por qué usar StorSimple?
Hello tabla siguiente describen algunas de las ventajas principales de Hola que proporciona Microsoft Azure StorSimple.

| Característica | Ventaja |
| --- | --- |
| Integración transparente |Usa las instalaciones de almacenamiento de datos de vínculo de hello iSCSI protocolo tooinvisibly. Esto garantiza que los datos almacenados en la nube de hello, en el centro de datos de hello, o en servidores remotos aparece toobe almacenado en una única ubicación. |
| Costos de almacenamiento reducidos |Asigna suficiente local o exigencias de almacenamiento toomeet actual en la nube y amplía la capacidad solo cuando sea necesario. Además, reduce los requisitos de almacenamiento y los gastos eliminando versiones redundantes de hello mismos datos (desduplicación) y mediante la compresión. |
| Administración simplificada del almacenamiento |Proporciona tooconfigure de herramientas de administración de sistema y administrar los datos almacenados en local, en un servidor remoto y en la nube de Hola. Además, puede administrar copias de seguridad y restaurar funciones desde un complemento de Microsoft Management Console (MMC).|
| Mejor recuperación ante desastres y cumplimiento normativo |No requiere tiempo de recuperación extendido. En lugar de eso, restaura los datos según sea necesario. Esto significa que las operaciones normales pueden seguir con un mínimo de interrupción. Además, puede configurar programaciones de copia de seguridad de las directivas toospecify y retención de datos. |
| Movilidad de datos |Datos cargan tooMicrosoft pueden tener acceso a los servicios de otros sitios con fines de recuperación y migración de nube de Azure. Además, puede usar aparatos de StorSimple tooconfigure StorSimple en la nube en máquinas virtuales (VM) que se ejecutan en Microsoft Azure. Hola máquinas virtuales puede utilizar dispositivos virtuales tooaccess almacena datos para fines de prueba o de recuperación. |
| Continuidad del negocio |Permite que su dispositivo de la serie de datos tooa StorSimple 8000 toomigrate de los usuarios de serie StorSimple 5000-7000. |
| Disponibilidad de hello Portal de administración pública de Azure |StorSimple está disponible en hello Portal de administración pública de Azure. Para obtener más información, consulte [implementar el dispositivo de StorSimple local en hello Portal gobierno](storsimple-8000-deployment-walkthrough-gov-u2.md). |
| Disponibilidad y protección de datos |Hola serie StorSimple 8000 admite zona redundantes almacenamiento (ZRS), de adición tooLocally almacenamiento redundante (LRS) y almacenamiento con redundancia geográfica (GRS). Consulte demasiado[este artículo sobre las opciones de redundancia de almacenamiento de Azure](https://azure.microsoft.com/documentation/articles/storage-redundancy/) para obtener detalles ZRS. |
| Compatibilidad para las aplicaciones críticas |Permite StorSimple que identifique los volúmenes apropiados, como anclado localmente a su vez, lo que garantiza que los datos requeridos por las aplicaciones críticas no están toohello en capas en la nube. Los volúmenes anclados localmente no son las latencias de toocloud de asunto o problemas de conectividad. Para obtener más información acerca de los volúmenes anclados localmente, consulte [usar volúmenes de toomanage de servicio de administrador de dispositivos de StorSimple de hello](storsimple-8000-manage-volumes-u2.md). |
| Baja latencia y alto rendimiento |Puede crear aplicaciones de nube que aprovechan las características de latencia baja de almacenamiento premium de Azure de alto rendimiento hello. Para más información sobre aplicaciones en la nube premium StorSimple, consulte [Implementar y administrar un dispositivo virtual StorSimple en Azure](storsimple-8000-cloud-appliance-u2.md). |


## <a name="storsimple-components"></a>Componentes StorSimple
Hola soluciones de Microsoft Azure StorSimple incluye Hola de los componentes siguientes:

* **Dispositivo de Microsoft Azure StorSimple** : una matriz de almacenamiento híbrida local que contiene SSD y HDD, en conjunto con controladores redundantes y funcionalidades de conmutación automática por error. controladores de Hello administran el almacenamiento niveles, al colocar actualmente usados (o activos) los datos en el almacenamiento local (en hello dispositivo o forma local servidores), mientras se mueve en la nube toohello datos utilizados con menos frecuencia.
* **Dispositivo de nube de StorSimple** : también conocida como Hola dispositivo Virtual StorSimple, se trata de una versión de software de dispositivo de StorSimple de Hola que replica la arquitectura de Hola y mayoría de las funciones hello híbrida físico del dispositivo de almacenamiento. Hola dispositivo de StorSimple en la nube se ejecuta en un único nodo en una máquina virtual de Azure. Los dispositivos virtuales premium, que sacan partido del almacenamiento premium de Azure, están disponibles en Update 2 y posterior.
* **Servicio de administrador de dispositivos de StorSimple** : una extensión de hello portal de Azure que le permite administrar un dispositivo de StorSimple o un dispositivo de StorSimple en la nube de una única interfaz web. Puede usar toocreate de servicio del Administrador de dispositivos de StorSimple de Hola y administrar servicios, ver y administrar dispositivos, ver las alertas, administrar volúmenes y ver y administrar las directivas de copia de seguridad y el catálogo de copia de seguridad de Hola.
* **Windows PowerShell para StorSimple** : una interfaz de línea de comandos que se puede usar toomanage Hola dispositivo StorSimple. Windows PowerShell para StorSimple tiene características que le permiten tooregister dispositivo StorSimple, configure la interfaz de red de hello en el dispositivo, instalar a ciertos tipos de actualizaciones, solucionar problemas en el dispositivo mediante el acceso a la sesión de soporte técnico de Hola y cambiar Hola estado del dispositivo. Puede tener acceso a Windows PowerShell para StorSimple conexión toohello la consola serie o usando la comunicación remota de Windows PowerShell.
* **Cmdlets de Azure PowerShell StorSimple** : una colección de cmdlets de Windows PowerShell que permitir que las tareas de nivel de servicio y la migración de tooautomate desde la línea de comandos de Hola. Para obtener más información acerca de hello cmdlets de PowerShell de Azure para StorSimple, vaya toohello [referencia de cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0#azure).
* **Administrador de instantáneas StorSimple** : un complemento de MMC que usa grupos de volúmenes y copias de seguridad coherentes con la aplicación de hello Windows Volume Shadow Copy Service toogenerate. Además, puede usar la clonación y programaciones de copia de seguridad de administrador de instantáneas StorSimple toocreate o restaurar volúmenes.
* **El adaptador de StorSimple para SharePoint** : una herramienta que amplía de forma transparente protección de datos y el almacenamiento de Microsoft Azure StorSimple tooSharePoint granjas de servidores, mientras que el almacenamiento de StorSimple sea visible y administrable desde Hola Central de SharePoint Portal de administración.

diagrama de Hello siguiente proporciona una visión general de arquitectura de Microsoft Azure StorSimple hello y componentes.

![Arquitectura de StorSimple](./media/storsimple-overview/overview-big-picture.png)

Hello las secciones siguientes describen cada uno de estos componentes con más detalle y explican cómo solución Hola organiza los datos, asigna espacio de almacenamiento y facilita la administración de almacenamiento y protección de datos. última sección de Hello proporciona definiciones de algunos de los términos importantes hello y conceptos relacionados tooStorSimple componentes y su administración.

## <a name="storsimple-device"></a>Dispositivo de StorSimple
dispositivo de Microsoft Azure StorSimple Hello es una matriz de almacenamiento de híbrido local que proporciona almacenamiento principal y toodata de acceso de iSCSI almacenados en él. Administra la comunicación con el almacenamiento en nube y le ayuda a seguridad de hello tooensure y confidencialidad de todos los datos que se almacena en hello solución de StorSimple de Microsoft Azure.

dispositivo de StorSimple de Hello incluye SSD y HDD de unidades de disco duro, así como compatibilidad con conmutación por error automática y agrupación en clústeres. Contiene un procesador compartido, almacenamiento compartido y dos controladores reflejados. Cada controlador proporciona siguiente hello:

* Equipo host de conexión tooa
* Seguridad toosix red puertos tooconnect toohello red de área local (LAN)
* Supervisión de hardware
* Memoria de acceso aleatorio no volátil (NVRAM), que conserva la información incluso cuando se interrumpe la energía
* Compatible con clústeres actualizar toomanage las actualizaciones de software en los servidores de un clúster de conmutación por error para que las actualizaciones de hello cuentan con una mínima o ningún efecto en la disponibilidad del servicio
* Servicio de clúster, que funciona como un clúster back-end, proporciona alta disponibilidad y minimiza todos los efectos adversos que podrían producirse si un HDD o una SSD presentan errores o quedan sin conexión

En cualquier punto del tiempo solo hay un controlador activo. Si se produce un error en el controlador activo hello, segundo controlador de hello activará automáticamente.

Para obtener más información, consulte demasiado[StorSimple componentes de hardware y el estado](storsimple-8000-monitor-hardware-status.md).

## <a name="storsimple-cloud-appliance"></a>StorSimple Cloud Appliance
Puede usar StorSimple toocreate un dispositivo de nube que se replica la arquitectura de Hola y capacidades de dispositivo de almacenamiento físico híbrida Hola. Hola aparato de nube de StorSimple (también conocido como dispositivo Virtual StorSimple Hola) se ejecuta en un único nodo en una máquina virtual de Azure. (Una aplicación virtual solo se puede crear en una máquina virtual de Azure. No puede crear uno en un dispositivo de StorSimple o en un servidor local).

dispositivo de nube de Hello tiene Hola siguientes características:

* Se comporta como un dispositivo físico y puede ofrecer un iSCSI máquinas toovirtual de interfaz en la nube de Hola.
* Puede crear un número ilimitado de dispositivos en la nube en la nube de Hola y activarlas activar y desactivar según sea necesario.
* Puede ayudar a simular entornos locales en escenarios de recuperación ante desastres, desarrollo y pruebas, además de facilitar la recuperación de nivel de elemento a partir de copias de seguridad.

Hola dispositivo StorSimple de nube está disponible en dos modelos: dispositivo Hola 8010 (anteriormente conocido como modelo de hello 1100) y el dispositivo de hello 8020. dispositivo 8010 Hello tiene una capacidad máxima de 30 TB. dispositivo 8020 Hello, que aprovecha las ventajas de almacenamiento premium de Azure, tiene una capacidad máxima de 64 TB. (En niveles locales, el almacenamiento premium de Azure almacena datos en SSD, mientras que el estándar los almacena en HDD). Tenga en cuenta que debe tener un almacenamiento de Azure premium almacenamiento cuenta toouse premium. Para obtener más información sobre el almacenamiento premium, vaya demasiado[almacenamiento Premium: almacenamiento de alto rendimiento para cargas de trabajo de máquina Virtual de Azure](../storage/common/storage-premium-storage.md).

Para obtener más información acerca de hello de dispositivo de StorSimple en la nube, vaya demasiado[implementar y administrar un dispositivo StorSimple de nube en Azure](storsimple-8000-cloud-appliance-u2.md).

## <a name="storsimple-device-manager-service"></a>Servicio de administrador de dispositivos de StorSimple
StorSimple de Microsoft Azure proporciona una interfaz de usuario basada en web (servicio de administrador de dispositivos de StorSimple de Hola) que le permite toocentrally administrar centros de datos y almacenamiento en nube. Puede usar Hola Hola del tooperform del servicio de administrador de dispositivos de StorSimple siguiente las tareas:

* Ajustar la configuración del sistema para dispositivos de StorSimple.
* Configurar y administrar ajustes de seguridad para dispositivos de StorSimple.
* Configurar credenciales y propiedades de la nube.
* Configurar y administrar volúmenes en un servidor.
* Configurar grupos de volúmenes.
* Crear copias de seguridad y restaurar datos.
* Supervisar el rendimiento.
* Revisar la configuración del sistema e identificar posibles problemas.

Puede usar tooperform de servicio del Administrador de dispositivos de StorSimple de hello todas las tareas de administración, excepto aquellos que requieren parada, como la instalación de actualizaciones y la instalación inicial del sistema.

Para obtener más información, consulte demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

## <a name="windows-powershell-for-storsimple"></a>Windows PowerShell para StorSimple
Windows PowerShell para StorSimple proporciona una interfaz de línea de comandos que puede usar toocreate y administrar el servicio de Microsoft Azure StorSimple hello y configurar y supervisar dispositivos de StorSimple. Se trata de una interfaz de la línea de comandos basada en Windows PowerShell que incluye cmdlets dedicados para administrar su dispositivo de StorSimple. Windows PowerShell para StorSimple tiene características que le permiten:

* Registrar un dispositivo.
* Configurar la interfaz de red de hello en un dispositivo.
* Instalar ciertos tipos de actualizaciones.
* Solucionar problemas en el dispositivo mediante el acceso a la sesión de soporte técnico de Hola.
* Cambiar el estado del dispositivo de Hola.

Puede tener acceso a Windows PowerShell para StorSimple desde una consola en serie (en un host de equipo conectado directamente toohello dispositivo) o de forma remota mediante la comunicación remota de Windows PowerShell. Tenga en cuenta que algunos Windows PowerShell para tareas de StorSimple, como el registro de dispositivos inicial, sólo se puede realizar en la consola serie Hola.

Para obtener más información, consulte demasiado[usar Windows PowerShell para StorSimple tooadminister dispositivo](storsimple-8000-windows-powershell-administration.md).

## <a name="azure-powershell-storsimple-cmdlets"></a>Cmdlets de Azure PowerShell StorSimple
cmdlets de PowerShell de Azure StorSimple Hola son un conjunto de cmdlets de Windows PowerShell que permite tooautomate nivel de servicio y las tareas de migración de línea de comandos de Hola. Para obtener más información acerca de hello cmdlets de PowerShell de Azure para StorSimple, vaya toohello [referencia de cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0).

## <a name="storsimple-snapshot-manager"></a>StorSimple Snapshot Manager
Administrador de instantáneas de StorSimple es un complemento Microsoft Management Console (MMC) que se pueden usar toocreate coherente, momento en copias de seguridad de local y datos en la nube. Hola complemento se ejecuta en un host basado en Windows Server. Puede utilizar StorSimple Snapshot Manager para:

* Configurar, crear copias de seguridad y eliminar volúmenes.
* Configurar el volumen tooensure de grupos que la copia de seguridad de datos es coherente con la aplicación.
* Administrar directivas de copia de seguridad para que los datos se realiza según una programación predeterminada y se almacena en una ubicación designada (local o en la nube de hello).
* Restaurar volúmenes y archivos individuales.

Las copias de seguridad se capturan como instantáneas, que registran solo los cambios de Hola desde que se tomó la última instantánea de Hola y requieren mucho menos espacio de almacenamiento de copias de seguridad completas. Puede crear programaciones de copia de seguridad o crear copias de seguridad inmediatas, según sea necesario. Además, puede usar las directivas de retención de administrador de instantáneas StorSimple tooestablish que controlan el número de instantáneas se guardará. Si posteriormente necesita toorestore datos desde una copia de seguridad, permite StorSimple Snapshot Manager podrá seleccionar del catálogo Hola de variable local o instantáneas en la nube. 

Si se produce un desastre o si necesita datos toorestore por algún otro motivo, el Administrador de instantáneas StorSimple restaura de forma incremental según sea necesario. La restauración de datos no requiere que apague todo el sistema Hola mientras restaura un archivo, reemplaza un equipo o bien mover operaciones tooanother sitio.

Para obtener más información, consulte demasiado[¿qué es el Administrador de instantáneas StorSimple?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>Adaptador de StorSimple para SharePoint
Microsoft Azure StorSimple incluye Hola el adaptador de StorSimple para SharePoint, un componente opcional que amplía de forma transparente la protección de datos y el almacenamiento de StorSimple granjas de servidores de tooSharePoint de características. el adaptador de Hello funciona con un proveedor de almacenamiento remoto de blobs (RBS) y la característica de SQL Server RBS hello, lo que permite toomove BLOBs tooa servidor respaldado por el sistema de Microsoft Azure StorSimple Hola. Microsoft Azure StorSimple, a continuación, almacena datos BLOB de hello localmente o en la nube hello, según el uso.

Hola adaptador de StorSimple para SharePoint se administra desde portal de Administración Central de SharePoint de Hola. Por lo tanto, administración de SharePoint sigue estando centralizada y todo el almacenamiento parece toobe en la granja de servidores de SharePoint de Hola.

Para obtener más información, consulte demasiado[adaptador de StorSimple para SharePoint](storsimple-adapter-for-sharepoint.md). 

## <a name="storage-management-technologies"></a>Tecnologías de administración de almacenamiento
Además toohello había dedicado dispositivo StorSimple, dispositivo virtual y otros componentes, Microsoft Azure StorSimple usa Hola después software tecnologías tooprovide acceso rápido toodata y tooreduce consumo de almacenamiento:

* [Organización automática del almacenamiento en niveles](#automatic-storage-tiering) 
* [Aprovisionamiento fino](#thin-provisioning) 
* [Desduplicación y compresión](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>Organización automática del almacenamiento en niveles
Microsoft Azure StorSimple organiza automáticamente los datos en niveles lógicos según el uso actual, edad y datos de tooother la relación. Datos que se active la mayoría se almacena localmente, mientras que menos activo y los datos inactivos están automáticamente migran toohello en la nube. Hola siguiente diagrama muestra este enfoque de almacenamiento.

![Niveles de almacenamiento de StorSimple](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

tooenable un acceso rápido, StorSimple almacena datos muy activos (datos activos) en las SSD en el dispositivo StorSimple Hola. Almacena los datos que se usan ocasionalmente (estado de datos) en las unidades de disco duro en el dispositivo de Hola o en servidores en centros de datos de Hola. Mueve los datos inactivos, los datos de copia de seguridad, y los datos se conservan para archivo o cumplimiento con fines toohello en la nube. 

> [!NOTE]
> En Update 2 o posterior, puede especificar un volumen anclado localmente, en cuyo caso Hola datos permanecen en el dispositivo local hello y no en niveles toohello en la nube. 


StorSimple ajusta y reordena las asignaciones de datos y almacenamiento a medida que cambian los patrones de uso. Por ejemplo, cierta información puede volverse menos activo con el tiempo. Cuando se encuentre progresivamente menos activo, se migra desde SSD tooHDDs y, a continuación, en la nube toohello. Si esos mismos datos vuelva a están activas, es migrados toohello back-dispositivo de almacenamiento.

proceso niveles de almacenamiento de información de Hola se produce como sigue:

1. Un administrador del sistema configura una cuenta de almacenamiento en la nube de Microsoft Azure.
2. Administrador de Hello usa Hola serie hello y la consola de administrador de dispositivos de StorSimple (ejecutándose en hello portal de Azure) tooconfigure Hola dispositivo y archivo de servidor del servicio, la creación de directivas de protección de volúmenes y los datos. Máquinas locales (por ejemplo, servidores de archivos) usan el dispositivo de StorSimple de hello interfaz estándar de equipos pequeños de Internet (iSCSI) tooaccess Hola.
3. Inicialmente, StorSimple almacena los datos en la capa de SSD rápida de hello de dispositivo de Hola.
4. Como Hola capacidad de enfoques de capa de SSD, StorSimple deduplica comprime los bloques de datos más antiguos de Hola y mueve toohello capa HDD.
5. Como Hola capacidad de enfoques de capa de HDD, StorSimple cifra los bloques de datos más antiguos de Hola y los envía segura toohello cuenta de almacenamiento de Microsoft Azure a través de HTTPS.
6. Microsoft Azure crea varias réplicas de datos de hello en su centro de datos y en un centro de datos remoto, asegurándose de que se pueden recuperar datos de hello si se produce un desastre.
7. Cuando el servidor de archivos de hello solicita datos almacenados en la nube de hello, StorSimple devuelve de forma transparente y almacena una copia en la capa de SSD de hello de dispositivo de StorSimple Hola.

#### <a name="how-storsimple-manages-cloud-data"></a>Cómo administra StorSimple los datos en la nube

StorSimple deduplica los datos del cliente en todas las instantáneas de Hola y Hola principal datos (escritos por los hosts). Cuando la desduplicación es excelente para la eficacia de almacenamiento, se hace pregunta Hola de "Novedades en la nube de Hola" complicada. Hello en capas de datos principal y los datos de instantánea de Hola se superponen entre sí. Un único fragmento de datos en la nube de hello podría usarse como datos principales en capas y también hacer referencia a varias instantáneas. Cada instantánea en la nube garantiza que una copia de todos los datos de punto en el tiempo de hello está bloqueada en la nube de hello hasta que se elimine esa instantánea.

Datos solo se eliminan de nube de hello cuando no hay ningún dato de toothat de referencias. Por ejemplo, si se toma una instantánea de nube de todos los datos de Hola que está en el dispositivo de StorSimple de hello y, a continuación, elimina algunos datos principales, se vería hello _datos principal_ quitar inmediatamente. Hola _datos en la nube_ que incluye datos en niveles de Hola y Hola las copias de seguridad, Hola permanece igual. Esto es porque no hay una instantánea sigue haciendo referencia a datos en la nube Hola. Después de la nube de Hola se elimina la instantánea (y cualquier otra instantánea que hace referencia Hola los mismos datos), quita el consumo en la nube. Antes de eliminar datos en la nube, comprobamos que ninguna instantánea hace referencia a esos datos. Este proceso se denomina _recolección_ y un servicio en segundo plano se está ejecutando en el dispositivo de Hola. Eliminación de datos en la nube no es inmediato como servicio de recopilación de elementos no utilizados de hello las comprobaciones para otras referencias de datos toothat antes de la eliminación de Hola. velocidad de Hola de recolección depende de número total de Hola de instantáneas y datos total de saludo. Normalmente, los datos en la nube Hola se limpian en menos de una semana.


### <a name="thin-provisioning"></a>Aprovisionamiento fino
El aprovisionamiento fino es una tecnología de virtualización en el que el almacenamiento disponible parece tooexceed los recursos físicos. En lugar de reservar almacenamiento suficiente de antemano, StorSimple usa tooallocate de aprovisionamiento fino suficiente requisitos de espacio en toomeet actual. naturaleza elástica de Hola de almacenamiento en nube facilita este enfoque porque StorSimple puede aumentar o disminuir toomeet cambiantes exigencias de almacenamiento de nube.

> [!NOTE]
> El aprovisionamiento de los volúmenes anclados localmente no puede ser fino. Almacenamiento asignado tooa solo local volumen se aprovisiona en su totalidad cuando se crea el volumen de Hola.


### <a name="deduplication-and-compression"></a>Desduplicación y compresión
Microsoft Azure StorSimple usa la desduplicación y toofurther de compresión de datos reducen los requisitos de almacenamiento.

Desduplicación Hola reduce la cantidad total de los datos almacenados mediante la eliminación de redundancia en el conjunto de datos de hello almacenado. A medida que cambia la información, StorSimple omite los datos de hello sin cambios y captura solo Hola cambios. Además, StorSimple reduce Hola de los datos almacenados mediante la identificación y quita la información innecesaria. 

> [!NOTE]
> Los datos de los volúmenes anclados localmente no se desduplican ni comprimen. Sin embargo, las copias de seguridad de volúmenes localmente anclados sí se desduplican y comprimen.


## <a name="storsimple-workload-summary"></a>Resumen de la carga de trabajo de StorSimple
Un resumen de las cargas de trabajo de hello admitida StorSimple se tabulan a continuación.

| Escenario | Carga de trabajo | Compatible | Restricciones | Versión |
| --- | --- | --- | --- | --- |
| Colaboración |Uso compartido de archivos |Sí | |Todas las versiones |
| Colaboración |Uso compartido de archivos distribuidos |Sí | |Todas las versiones |
| Colaboración |SharePoint |Sí* |Solo compatible con volúmenes localmente anclados |Actualización 2 y posterior |
| Archivado |Archivado de archivos sencillo |Sí | |Todas las versiones |
| Virtualización |Máquinas virtuales |Sí* |Solo compatible con volúmenes localmente anclados |Actualización 2 y posterior |
| Base de datos |SQL |Sí* |Solo compatible con volúmenes localmente anclados |Actualización 2 y posterior |
| Vigilancia de vídeo |Vigilancia de vídeo |Sí* |Se admite cuando el dispositivo StorSimple está dedicado solo carga de trabajo de toothis |Actualización 2 y posterior |
| Copia de seguridad |Copia de seguridad de destino principal |Sí* |Se admite cuando el dispositivo StorSimple está dedicado solo carga de trabajo de toothis |Actualización 3 y posteriores |
| Copia de seguridad |Copia de seguridad de destino secundario |Sí* |Se admite cuando el dispositivo StorSimple está dedicado solo carga de trabajo de toothis |Actualización 3 y posteriores |

*Sí&amp;#42;. Se deben aplicar las restricciones y directrices de la solución.*

Hola siguiendo las cargas de trabajo no se admite los dispositivos serie 8000 de StorSimple. Si se implementa en StorSimple, estas cargas de trabajo generarán una configuración no admitida.

* Imágenes médicas
* Exchange
* VDI
* Oracle
* SAP
* Big Data
* Distribución de contenido
* Arranque desde SCSI

Aquí te mostramos una lista de componentes de la infraestructura de hello StorSimple compatible.

| Escenario | Carga de trabajo | Compatible | Restricciones | Versión |
| --- | --- | --- | --- | --- |
| General |ExpressRoute |Sí | |Todas las versiones |
| General |DataCore FC |Sí* |Compatible con DataCore SANsymphony |Todas las versiones |
| General |DFSR |Sí* |Solo compatible con volúmenes localmente anclados |Todas las versiones |
| General |Indización |Sí* |Para volúmenes en capas, solo se admite la indización de metadatos (sin datos).<br>Para volúmenes anclados localmente, se admite la indización completa. |Todas las versiones |
| General |Antivirus |Sí* |Para volúmenes en capas, se admite solo el examen al abrir y cerrar.<br> Para volúmenes anclados localmente, se admite el examen completo. |Todas las versiones |

*Sí&amp;#42;. Se deben aplicar las restricciones y directrices de la solución.*

Aquí te mostramos una lista de otro software que se usan con soluciones de toobuild de StorSimple.

| Tipo de carga de trabajo | Software usado con StorSimple | Versiones compatibles|Guía de toosolution de vínculo| 
| --- | --- | --- | --- |
| Destino de copia de seguridad |Veeam |Veeam versión 9 y versiones posterior |[StorSimple como destino de copia de seguridad con Veeam](storsimple-configure-backup-target-veeam.md)|
| Destino de copia de seguridad |Veritas Backup Exec |Backup Exec 16 y versiones posteriores |[StorSimple como destino de copia de seguridad con Backup Exec](storsimple-configure-backup-target-using-backup-exec.md)|
| Destino de copia de seguridad |Veritas NetBackup |NetBackup 7.7.x y versiones posteriores  |[StorSimple como destino de copia de seguridad con NetBackup](storsimple-configure-backuptarget-netbackup.md)|
| Uso compartido de archivos global <br></br> Colaboración |Talon  |[StorSimple con Talon](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>Terminología de StorSimple
Antes de implementar la solución de StorSimple de Microsoft Azure, se recomienda que revise los siguientes Hola términos y definiciones.

### <a name="key-terms-and-definitions"></a>Términos clave y definiciones
| Término (acrónimo o abreviatura) | Description |
| --- | --- |
| registros de control de acceso (ACR) |Un registro asociado a un volumen en el dispositivo de StorSimple de Microsoft Azure que determina qué hosts pueden conectarse tooit. determinación de Hola se basa en iSCSI Hola nombre completo (IQN) de hosts de hello (contenidos en hello ACR) que se conectan el dispositivo de StorSimple tooyour. |
| AES-256 |Un algoritmo de estándar de cifrado avanzado (AES) de 256 bits para cifrar los datos a medida que mueve tooand de nube de Hola. |
| tamaño de unidad de asignación (AUS) |Hola cantidad más pequeña de espacio en disco que se puede asigna toohold un archivo en los sistemas de archivos de Windows. Si un tamaño de archivo no es un múltiplo par del tamaño de clúster de hello, espacio adicional debe ser archivo de hello toohold usado (seguridad toohello siguiente múltiplo del tamaño de clúster de hello) lo que da lugar a espacio perdido y fragmentación de disco duro de Hola. <br>Hola recomienda que aus para volúmenes de StorSimple de Azure es 64 KB porque funciona bien con los algoritmos de desduplicación Hola. |
| organización automática del almacenamiento en niveles |Mover automáticamente los datos menos activos de SSD tooHDDs y, a continuación, tooa nivel en la nube de hello y, a continuación, habilitar la administración de todo el almacenamiento de una interfaz de usuario central. |
| catálogo de copias de seguridad |Una colección de copias de seguridad, normalmente relacionadas con el tipo de aplicación Hola que se utilizó. Esta colección se muestra en la hoja de catálogo de copia de seguridad de Hola de hello UI del servicio de administrador de dispositivos de StorSimple. |
| archivo del catálogo de copias de seguridad |Un archivo que contiene una lista de instantáneas disponibles almacenadas actualmente en la base de datos de hello copia de seguridad de administrador de instantáneas de StorSimple. |
| directiva de copia de seguridad |Una selección de volúmenes, tipos de copia de seguridad y horarios que le permite toocreate copias de seguridad en una programación predefinida. |
| objetos grandes binarios (BLOB) |Una colección de datos binarios almacenados como una sola entidad en un sistema de administración de base de datos. Los BLOB suelen ser imágenes, audio u otros objetos multimedia, aunque a veces el código binario ejecutable se almacena como un BLOB. |
| Protocolo de autenticación por desafío mutuo (CHAP) |Un protocolo utilizado tooauthenticate Hola del mismo nivel que una conexión, en función del mismo nivel de hello comparten una contraseña o secreto. CHAP puede ser unidireccional o mutuo. Con el CHAP unidireccional, destino Hola autentica como iniciador. El CHAP mutuo requiere que destino Hola autentique el iniciador de Hola y ese iniciador Hola autentica destino Hola. |
| clon |Una copia duplicada de un volumen. |
| Nube como nivel (CaaT) |Almacenamiento integrado como una capa en la arquitectura de almacenamiento de Hola de modo que todo el almacenamiento parece toobe parte de la red de almacenamiento de una de las empresas en la nube. |
| proveedor de servicios de nube (CSP) |Un proveedor de servicios de informática en la nube. |
| instantánea de la nube |Una copia en el momento de datos del volumen que se almacenan en la nube de Hola. Una instantánea en la nube es equivalente instantánea de tooa replicada en un sistema de almacenamiento diferente, fuera del sitio. Las instantáneas en la nube son especialmente útiles en escenarios de recuperación ante desastres. |
| clave de cifrado de almacenamiento en la nube |Una contraseña o clave usada por los datos de hello cifrado tooaccess de dispositivo de StorSimple enviados por el dispositivo de la nube de toohello. |
| actualización de clústeres |Administración de actualizaciones de software en los servidores de un clúster de conmutación por error para que las actualizaciones de hello cuentan con una mínima o ningún efecto en la disponibilidad del servicio. |
| ruta de datos |Una colección de unidades funcionales que realizan operaciones interconectadas de procesamiento de datos. |
| desactivar |Una acción permanente que saltos Hola conexión entre el dispositivo de StorSimple de Hola y Hola asociar el servicio de nube. Instantáneas en la nube del dispositivo de hello permanecen después de este proceso y se pueden clonar o utilizar para la recuperación ante desastres. |
| creación de reflejo de disco |Las unidades de replicación de volúmenes de disco lógico en disco duro diferente en tiempo real tooensure una disponibilidad continua. |
| creación de reflejo de disco dinámico |Replicación de volúmenes de discos lógicos en discos dinámicos. |
| discos dinámicos |Un formato de volumen de disco que usa Hola toostore de administrador de discos lógicos (LDM) y administrar datos en varios discos físicos. Los discos dinámicos puede ser tooprovide ampliada más espacio libre. |
| Gabinete Extended Bunch of Disks (EBOD) |Un gabinete secundario del dispositivo StorSimple de Microsoft Azure que contiene discos duros adicionales para almacenamiento adicional. |
| aprovisionamiento grueso |Un aprovisionamiento de almacenamiento convencional en qué almacenamiento se asigna espacio en función de prever las necesidades (y suele ser más allá necesidades actuales de hello). Consulte también *Aprovisionamiento fino*. |
| unidad de disco duro (HDD) |Una unidad que usa datos de toostore la rotación de discos. |
| almacenamiento de nube híbrida |Una arquitectura de almacenamiento que usa los recursos locales y remotos, incluidos el almacenamiento en la nube. |
| Internet Small Computer System Interface (iSCSI) |Un estándar de red de almacenamiento basado en el Protocolo de Internet (IP) para vincular el equipo de almacenamiento de datos o funciones. |
| iniciador iSCSI |Un componente de software que permite a un equipo host que ejecuta Windows tooconnect tooan almacenamiento externo basado en iSCSI red. |
| Nombre calificado iSCSI (IQN) |Un nombre único que identifica un destino o iniciador iSCSI. |
| destino iSCSI |Un componente de software que proporciona subsistemas de disco iSCCSI centralizados en redes de área de almacenamiento. |
| archivo de datos |Un enfoque de almacenamiento en el que los datos archivados son accesibles en todos los Hola momento (no se almacena fuera de las instalaciones en cinta, por ejemplo). Microsoft Azure StorSimple usa el archivo vivo. |
| Volumen anclado localmente |un volumen que reside en el dispositivo de Hola y nunca es niveles toohello en la nube. |
| instantánea local |Una copia en el momento de datos del volumen que se almacenan en el dispositivo de Microsoft Azure StorSimple Hola. |
| Microsoft Azure StorSimple |Una potente solución que consta de un dispositivo de almacenamiento del centro de datos y el software que permite tooleverage de las organizaciones de TI almacenamiento en nube como si se tratase de almacenamiento del centro de datos. StorSimple simplifica la administración y protección de datos al mismo tiempo que reduce los costos. solución de Hello consolida principal almacenamiento, archivo, copia de seguridad y recuperación de desastres (DR) mediante la integración sin problemas con la nube de Hola. Mediante la combinación de administración de datos de almacenamiento SAN y de nube en una plataforma empresarial, los dispositivos StorSimple habilitan la velocidad, la sencillez y confiabilidad para todas las necesidades relacionadas con el almacenamiento. |
| Módulo de alimentación y refrigeración (PCM) |Los componentes de hardware del dispositivo de StorSimple que se compone de hello, de ventilador de refrigeración y fuentes de alimentación de Hola Hola, por tanto, módulo de alimentación y refrigeración de nombre. alojamiento principal de Hello de dispositivo de hello tiene dos PCM de 764 w, mientras que hello alojamiento de EBOD tiene dos PCM de 580 w. |
| gabinete principal |Alojamiento principal del dispositivo StorSimple que contiene los controladores de plataforma de aplicación Hola. |
| objetivo de tiempo de recuperación (RTO) |Hola cantidad de tiempo máxima que debe emplearse antes de que un proceso o sistema empresarial esté completamente restaurado tras un desastre. |
| SCSI conectado en serie (SAS) |Un tipo de unidad de disco duro (HDD). |
| clave de cifrado de datos de servicio |Una clave realizados nuevo dispositivo de StorSimple de tooany disponibles que se registra con el servicio de administrador de dispositivos de StorSimple de hello. datos de configuración de Hello transferidos entre el servicio de administrador de dispositivos de StorSimple de Hola y dispositivo Hola se cifran con una clave pública y, a continuación, se pueden descifrar únicamente en dispositivos de hello mediante una clave privada. Clave de cifrado de datos de servicio permite Hola servicio tooobtain esta clave privada para el descifrado. |
| clave de registro del servicio |Una clave que le ayuda a registrar el dispositivo de StorSimple de hello con hello servicio Administrador de dispositivos de StorSimple para que aparezca en hello portal de Azure para diversas tareas administrativas. |
| Small Computer System Interface (SCSI) |Un conjunto de estándares para conectar físicamente equipos y pasar datos entre ellos. |
| unidad de estado sólido (SSD) |Un disco que no contiene piezas móviles; por ejemplo, una unidad flash. |
| Cuenta de almacenamiento |Un conjunto de credenciales de acceso vinculado tooyour cuenta de almacenamiento para un proveedor de servicios de nube especificada. |
| Adaptador de StorSimple para SharePoint |Un componente de Microsoft Azure StorSimple que amplía de forma transparente la protección de datos y el almacenamiento de StorSimple tooSharePoint granjas de servidores. |
| Servicio de administrador de dispositivos de StorSimple |Una extensión de Hola portal de Azure que le permite toomanage su local de StorSimple de Azure y los dispositivos virtuales. |
| StorSimple Snapshot Manager |Un complemento de Microsoft Management Console (MMC) para administrar las operaciones de copia de seguridad y restauración en Microsoft Azure StorSimple. |
| realizar copia de seguridad |Una característica que permite Hola usuario tootake una copia de seguridad interactiva de un volumen. Es una forma alternativa de realizar una copia de seguridad manual de un volumen como tootaking lugar una copia de seguridad automatizada a través de una directiva definida. |
| Aprovisionamiento fino |Método para optimizar la eficacia de hello con qué hello se utiliza espacio de almacenamiento disponible en sistemas de almacenamiento. En el aprovisionamiento fino, almacenamiento de Hola se asigna entre varios usuarios según Hola espacio mínimo requerido por cada usuario en un momento dado. Consulte también *Aprovisionamiento grueso*. |
| organización en niveles |Organizar datos en agrupaciones lógicas basadas en el uso actual, edad y datos de tooother la relación. StorSimple organiza automáticamente los datos en niveles. |
| volumen |Áreas de almacenamiento lógico presentadas en forma de Hola de unidades. Volúmenes de StorSimple corresponden toohello montadas por host hello, incluidos aquellos detectados a través del uso de Hola de iSCSI y un dispositivo de StorSimple. |
| contenedor de volúmenes |Un grupo de volúmenes y opciones de Hola que se aplican toothem. Todos los volúmenes en el dispositivo StorSimple se agrupan en contenedores de volúmenes. Configuración de contenedor de volumen incluye cuentas de almacenamiento, configuración de cifrado para los datos enviados toocloud con las claves de cifrado asociado y el ancho de banda consumido en operaciones relacionadas con la nube de Hola. |
| grupo de volúmenes |En el Administrador de instantáneas de StorSimple, un grupo de volúmenes es una colección de procesamiento de copia de seguridad de volúmenes se han configurado toofacilitate. |
| Volume Shadow Copy Service (VSS) |Un servicio de sistema operativo Windows Server que facilita la coherencia con las aplicaciones comunicándose con la creación de hello de toocoordinate de las aplicaciones basadas en VSS de instantáneas incrementales. VSS garantiza que las aplicaciones de hello están temporalmente inactivas cuando se realizan las instantáneas. |
| Windows PowerShell para StorSimple |Una interfaz de línea de comandos basada en Windows PowerShell usa toooperate y administrar el dispositivo de StorSimple. Además de conservar algunas capacidades básicas de Hola de Windows PowerShell, esta interfaz tiene cmdlets adicionales específicamente orientados a la administración de un dispositivo de StorSimple. |

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información acerca de la [Seguridad de StorSimple](storsimple-8000-security.md).

