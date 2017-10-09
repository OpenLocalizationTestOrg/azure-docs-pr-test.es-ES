---
title: "Guía de aaaBackup para SAP HANA en máquinas virtuales de Azure | Documentos de Microsoft"
description: "Guía de copia de seguridad para SAP HANA proporciona dos posibilidades de copia de seguridad principales para SAP HANA en Azure Virtual Machines"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Guía de copia de seguridad de SAP HANA en Azure Virtual Machines

## <a name="getting-started"></a>Introducción

manual de copia de seguridad de Hola para SAP HANA que se ejecutan en máquinas virtuales de Azure solo se describen los temas específicos de Azure. Para general SAP HANA copia de seguridad elementos relacionados, consulte la documentación de SAP HANA Hola (vea _documentación de copia de seguridad de SAP HANA_ más adelante en este artículo).

enfoque de Hola de este artículo se encuentra en dos principales copia de seguridad posibilidades de SAP HANA en máquinas virtuales de Azure:

- Sistema de archivos de copia de seguridad toohello HANA en una máquina Virtual de Linux de Azure (consulte [SAP HANA Azure copia de seguridad en el nivel de archivo](sap-hana-backup-file-level.md))
- Copia de seguridad HANA en función de las instantáneas de almacenamiento en función de instantánea de blob de almacenamiento de Azure de hello manualmente o servicio de copia de seguridad de Azure (consulte [copia de seguridad de SAP HANA basándose en instantáneas de almacenamiento](sap-hana-backup-storage-snapshots.md))

SAP HANA ofrece una API, lo que permite toointegrate de herramientas de copia de seguridad de terceros directamente con SAP HANA de copia de seguridad. (Que no está dentro del ámbito de Hola de esta guía.) No hay ninguna integración directa de SAP HANA con el servicio Azure Backup disponible actualmente basada en esta API.

SAP HANA se admite oficialmente en el tipo de máquina virtual de Azure GS5 como instancia única con cargas de trabajo de tooOLAP de una restricción adicional (consulte [buscar plataformas de IaaS certificadas](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) en el sitio Web SAP de hello). En este artículo se actualizará a medida que estén disponibles nuevas ofertas para SAP HANA en Azure.

También hay una solución híbrida de SAP HANA en Azure, donde SAP HANA ejecuta elementos no virtualizados en servidores físicos. Sin embargo, esta guía de Azure Backup para SAP HANA cubre un entorno puro de Azure donde se ejecuta SAP HANA en una máquina virtual de Azure, no SAP HANA en &quot;instancias de gran tamaño.&quot; Vea [Introducción y arquitectura de SAP HANA en Azure (instancias grandes)](hana-overview-architecture.md) para obtener más información sobre esta solución de copia de seguridad en &quot;instancias grandes&quot; basada en instantáneas de almacenamiento.

Puede obtener información general sobre productos SAP admitidos en Azure en la [nota 1928533 de SAP](https://launchpad.support.sap.com/#/notes/1928533).

Hello tres ilustraciones siguientes proporcionan una visión general del programa Hola a opciones de copia de seguridad de SAP HANA con las capacidades nativas de Azure actualmente y también muestran tres escenarios posibles de copia de seguridad futuras. artículos relacionados con Hello [SAP HANA Azure copia de seguridad en el nivel de archivo](sap-hana-backup-file-level.md) y [copia de seguridad de SAP HANA basándose en instantáneas de almacenamiento](sap-hana-backup-storage-snapshots.md) se describen estas opciones con más detalle, incluidas las consideraciones de tamaño y rendimiento para SAP Copias de seguridad HANA varios terabytes de tamaño.

![Esta ilustración muestra dos posibilidades para guardar el estado actual de VM de Hola](media/sap-hana-backup-guide/image001.png)

Esta ilustración muestra la posibilidad de Hola de guardar Hola VM estado actual, ya sea a través del servicio de copia de seguridad de Azure o instantánea manual de los discos de máquina virtual. Con este enfoque, una &#39; no tiene copias de seguridad de toomanage SAP HANA. desafío de Hola de escenario de instantánea de disco de hello es coherencia del sistema de archivos y el estado de disco coherentes con la aplicación. tema de coherencia de Hola se describe en la sección de hello _coherencia de datos de SAP HANA al tomar instantáneas de almacenamiento_ más adelante en este artículo. Capacidades y las restricciones de las copias de seguridad de tooSAP HANA también se describen más adelante en este artículo relacionados con el servicio de copia de seguridad de Azure.

![Esta ilustración muestra opciones para realizar un SAP HANA archivo de copia de seguridad dentro de hello VM](media/sap-hana-backup-guide/image002.png)

En esta ilustración se muestra opciones para realizar una copia de seguridad de archivos de SAP HANA dentro de hello VM y, a continuación, almacenarlos archivos de copia de seguridad de HANA en algún lugar else con herramientas diferentes. La realización de una copia de seguridad de HANA requiere más tiempo que una solución de copia de seguridad basada en instantáneas, pero tiene ventajas con respecto a la integridad y la coherencia. Se proporcionarán más detalles más tarde en este artículo.

![Esta ilustración muestra un posible escenario futuro de copia de seguridad de SAP HANA](media/sap-hana-backup-guide/image003.png)

Esta ilustración muestra un posible escenario futuro de copia de seguridad de SAP HANA. Si SAP HANA permitió realizar copias de seguridad desde una replicación secundaria, agregaría opciones adicionales para las estrategias de copia de seguridad. Actualmente no es posible según tooa post en hello SAP HANA Wiki:

_&quot;¿Es posible tootake copias de seguridad lado secundario Hola?_

_No, actualmente solo puede tomar datos y copias de seguridad en el lado principal de Hola de registro. Si está habilitada la copia de seguridad de inicio de sesión automático, después de la adquisición toohello lado secundario, las copias de seguridad del registro de hello automáticamente se escribirán no existe.&quot;_

## <a name="sap-resources-for-hana-backup"></a>Recursos SAP para copia de seguridad de HANA

### <a name="sap-hana-backup-documentation"></a>Documentación de copia de seguridad de SAP HANA

- [Introducción tooSAP HANA administración](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [Planeación de su estrategia de copia de seguridad y recuperación](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)
- [Programación de la copia de seguridad de HANA mediante ABAP DBACOCKPIT](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html)
- [Programación de copias de seguridad de datos (SAP HANA Cockpit)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm)
- Preguntas más frecuentes sobre la copia de seguridad de SAP HANA en la [nota 1642148 de SAP](https://launchpad.support.sap.com/#/notes/1642148)
- Preguntas más frecuentes sobre las instantáneas de base de datos y almacenamiento en la [nota 2039883 de SAP](https://launchpad.support.sap.com/#/notes/2039883)
- Sistemas de archivos de red no apropiados para la copia de seguridad y la recuperación en la [nota 1820529 de SAP](https://launchpad.support.sap.com/#/notes/1820529)

### <a name="why-sap-hana-backup"></a>¿Por qué la copia de seguridad de SAP HANA?

Almacenamiento de Azure ofrece disponibilidad y confiabilidad fuera del cuadro de hello (vea [Introducción tooMicrosoft almacenamiento de Azure](../../../storage/common/storage-introduction.md) para obtener más información sobre el almacenamiento de Azure).

Hola mínimo para &quot;copia de seguridad&quot; es toorely en hello SLA de Azure: Hola de mantener los archivos de registro y datos de SAP HANA en máquina virtual del servidor de SAP HANA discos duros virtuales de Azure toohello adjunto. Este enfoque trata sobre errores de la máquina virtual, pero no posibles datos de SAP HANA toohello de daños y archivos de registro o errores lógicos como eliminar archivos de datos o por accidente. Las copias de seguridad también son necesarias para el cumplimiento o por motivos legales. En resumen, las copias de seguridad de SAP HANA son siempre necesarias.

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>La corrección de tooverify de copia de seguridad de SAP HANA
Cuando se usan instantáneas de almacenamiento, se recomienda ejecutar una restauración de prueba en un sistema diferente. Este enfoque proporciona una tooensure de manera que una copia de seguridad es correcta e internos procesos de trabajo de copia de seguridad y restauración según lo previsto. Aunque esto es una importante obstáculo local, es mucho más fácil tooaccomplish en la nube de hello al proporcionar temporalmente los recursos necesarios para este propósito.

Tenga en cuenta que realizar una restauración simple y comprobar si HANA está listo para empezar no es suficiente. Idealmente, uno debe ejecutar un toobe de comprobación de coherencia de tabla seguro de que esa base de datos de hello restaurado es correcto. SAP HANA ofrece varios tipos de comprobaciones de coherencia que se describen en la [nota 1977584 de SAP](https://launchpad.support.sap.com/#/notes/1977584).

También encontrará información sobre la comprobación de coherencia de tabla de hello en el sitio Web SAP de hello en [tabla y comprobaciones de coherencia de catálogo](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b).

Para las copias de seguridad de archivos estándar no es necesaria una restauración de prueba. Existen dos herramientas de SAP HANA que le ayudan a toocheck qué copia de seguridad se puede utilizar para restore: hdbbackupdiag y hdbbackupcheck. Vea [Comprobación manual si una recuperación es posible](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm) para obtener más información sobre estas herramientas.

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>Ventajas y desventajas de la copia de seguridad de HANA frente a instantáneas de almacenamiento

SAP &#39; t dar preferencia tooeither HANA copia de seguridad frente a instantáneas de almacenamiento. Enumera sus ventajas y desventajas, por lo que uno puede determinar qué toouse según la situación de Hola y tecnología de almacenamiento disponible (vea [planear la copia de seguridad y la estrategia de recuperación](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)).

En Azure, tenga en cuenta el hecho de Hola Hola no de característica de instantánea de blob de Azure &#39; t garantizar la coherencia del sistema de archivos (vea [mediante instantáneas de blob con PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)). Hola la siguiente sección, _coherencia de datos de SAP HANA al tomar instantáneas de almacenamiento_, se describen algunas consideraciones relacionadas con esta característica.

Asimismo, uno tiene toounderstand Hola implicaciones de facturación cuando se trabaja con frecuencia con instantáneas de blob, como se describe en este artículo: [comprender cómo las instantáneas pueden incrementar los](/rest/api/storageservices/understanding-how-snapshots-accrue-charges): lo ejecutando &#39; t evidente como uso de Azure discos virtuales.

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>Coherencia de datos de SAP HANA al tomar instantáneas de almacenamiento

La coherencia del sistema de archivos y la aplicación es un problema complejo cuando se toman instantáneas de almacenamiento. problemas de tooavoid de manera más fáciles de Hello estaría tooshut hacia abajo de SAP HANA, o quizás incluso Hola todo el equipo virtual. El cierre puede ser factible con una demostración o prototipo, o incluso en un sistema de desarrollo, pero no es una opción para un sistema de producción.

En Azure, uno tiene tookeep en cuenta que Hola no de característica de instantánea de blob de Azure &#39; t garantizar la coherencia del sistema de archivos. Funciona correctamente sin embargo, mediante el uso de hello SAP HANA instantánea característica, siempre que hay un único disco virtual implicados. Pero incluso con un solo disco, elementos adicionales tienen toobe activada. La [nota 2039883 de SAP](https://launchpad.support.sap.com/#/notes/2039883) dispone de información importante sobre las copias de seguridad de SAP HANA a través de instantáneas de almacenamiento. Por ejemplo, menciona que, con el sistema de archivos de hello XFS, es necesario toorun **xfs\_inmovilizar** antes de iniciar un almacenamiento de instantáneas tooguarantee coherencia (vea [xfs\_freeze(8) - man de Linux página](https://linux.die.net/man/8/xfs_freeze) para obtener más información sobre **xfs\_inmovilizar**).

tema de Hola de coherencia pasa a ser incluso más complejo en un escenario donde un sistema de archivos de solo abarca varios discos o volúmenes. Por ejemplo, si utiliza mdadm o LVM, y fragmentación. Hola nota de SAP mencionadas anteriormente estados:

_&quot;Pero tenga en cuenta que el sistema de almacenamiento de hello tenga coherencia tooguarantee E/S al crear una instantánea de almacenamiento por volumen de datos de SAP HANA, es decir, la toma de instantáneas de un volumen de datos específicos del servicio de SAP HANA debe ser una operación atómica.&quot;_

Suponiendo que existe un sistema de archivos XFS expansión cuatro discos virtuales de Azure, hello pasos siguientes proporcionan una instantánea coherente que representa el área de datos HANA hello:

- Preparación de la instantánea de HANA
- Inmovilizar el sistema de archivos de hello (por ejemplo, utilice **xfs\_inmovilizar**)
- Creación de todas las instantáneas de blob necesarias en Azure
- Anular la inmovilización de sistema de archivos de Hola
- Confirmar la instantánea HANA Hola

La recomendación es toouse Hola procedimiento anteriormente toobe de todos los casos en lado de hello seguro, con independencia de qué sistema de archivos. O bien, si es un solo disco o una fragmentación, a través de mdadm o LVM en varios discos.

Es importante tooconfirm Hola HANA instantánea. Due toohello &quot;copia en escritura&quot; SAP HANA no pueden requerir espacio en disco adicional en este modo de preparación de instantánea. &#39; s también no es posible toostart nuevas copias de seguridad hasta que se confirma la instantánea de SAP HANA Hola.

Servicio de copia de seguridad de Azure usa tootake de extensiones de máquina virtual de Azure atención Hola coherencia del sistema de archivos. Estas extensiones de VM no están disponibles para el uso independiente. Aún una coherencia de SAP HANA toomanage. Consulte el artículo relacionado de hello [copia de seguridad de Azure de SAP HANA en el nivel de archivo](sap-hana-backup-file-level.md) para obtener más información.

### <a name="sap-hana-backup-scheduling-strategy"></a>Estrategia de programación de copia de seguridad de SAP HANA

artículo de SAP HANA Hello [planear la copia de seguridad y la estrategia de recuperación](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) Estados a basic plan las copias de seguridad de toodo:

- Instantánea del almacenamiento (diaria)
- Copia de seguridad de datos completa con formato de archivo o backint (una vez a la semana)
- Copias de seguridad de registro automáticas

Opcionalmente, puede realizar el proceso completo sin instantáneas de almacenamiento; se reemplazarán por copias de seguridad diferenciales de HANA, como copias de seguridad incrementales o diferenciales (vea [Copias de seguridad diferenciales](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm)).

Guía de administración de HANA Hola proporciona una lista de ejemplo. Sugiere que uno recuperar momento específico de SAP HANA tooa en el tiempo con hello sigue la secuencia de copias de seguridad:

1. Copia de seguridad de datos completa
2. Copia de seguridad diferencial
3. Copia de seguridad incremental 1
4. Copia de seguridad incremental 2
5. Copias de seguridad de registro

Con respecto a una programación exacta como toowhen y la frecuencia con la que debe ocurrir un tipo de copia de seguridad específico, no es posible toogive norma general, es muy específica del cliente y depende de cuántos cambios de datos se producen en el sistema de Hola. Una recomendación básica del lado SAP, que se puede ver como guía general, es toomake una HANA copia de seguridad completa una vez por semana.
Sobre copias de seguridad de registro, consulte la documentación de SAP HANA Hola [copias de seguridad del registro](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm).

SAP también recomienda realizar algunas tareas de mantenimiento de tookeep de catálogo de copia de seguridad de Hola que crezca de forma desmesurada (vea [de limpieza para el catálogo de copia de seguridad y el almacenamiento de copia de seguridad](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm)).

### <a name="sap-hana-configuration-files"></a>Archivos de configuración de SAP HANA

Como se indica en las P+F de hello en [1642148 de nota de SAP](https://launchpad.support.sap.com/#/notes/1642148), archivos de configuración de SAP HANA hello no forman parte de una copia de seguridad HANA estándar. No son esencial toorestore un sistema. configuración de HANA Hola podría cambiarse manualmente después de la restauración de Hola. En caso de que se desee tooget Hola misma configuración personalizada durante el proceso de restauración de hello, es necesario tooback seguridad de los archivos de configuración de HANA Hola por separado.

Si las copias de seguridad HANA estándar van tooa dedicado de sistema de archivos de copia de seguridad de HANA, uno podría copiar toohello de archivos de configuración de hello mismo sistema de archivos de copia de seguridad y, a continuación, copiarlo todo como destino de final de almacenamiento toohello juntos estupendo almacenamiento de blobs.

### <a name="sap-hana-cockpit"></a>SAP HANA Cockpit

SAP HANA cabina ofrece la posibilidad de Hola de supervisión y administración de SAP HANA a través de un explorador. También permite el tratamiento de las copias de seguridad de SAP HANA y, por lo tanto, puede utilizarse como una alternativa tooSAP Studio HANA y ABAP DBACOCKPIT (consulte [SAP HANA cabina](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm) para obtener más información).

![Esta ilustración muestra la pantalla de administración de base de datos de SAP HANA cabina Hola](media/sap-hana-backup-guide/image004.png)

Este Hola de ilustración se muestra en pantalla de administración de base de datos de SAP HANA cabina y el icono de copia de seguridad de hello en hello deja. Icono de copia de seguridad de hello realizar requiere permisos de usuario apropiados para la cuenta de inicio de sesión.

![Las copias de seguridad pueden supervisarse en SAP HANA Cockpit mientras están en curso](media/sap-hana-backup-guide/image005.png)

Las copias de seguridad pueden supervisarse en la cabina de SAP HANA mientras están en curso y, una vez que haya finalizado, todos los detalles de copia de seguridad de hello están disponibles.

![Un ejemplo de uso de Firefox en una VM de Azure SLES 12 con el escritorio de Gnome](media/sap-hana-backup-guide/image006.png)

Hola capturas de pantalla anteriores se han realizado desde una VM de Windows Azure. Este es un ejemplo de uso de Firefox en una VM de Azure SLES 12 con el escritorio de Gnome Programaciones de copia de seguridad de hello opción toodefine SAP HANA muestran en la cabina de SAP HANA. A medida que también puede ver uno, sugiere fecha y hora como prefijo para los archivos de copia de seguridad de Hola. En SAP HANA Studio, es el prefijo predeterminado de hello &quot;completar\_datos\_copia de seguridad&quot; al realizar una copia de seguridad completa. Se recomienda usar un prefijo único.

### <a name="sap-hana-backup-encryption"></a>Cifrado de copia de seguridad de SAP HANA

SAP HANA ofrece cifrado de datos y de registro. Si no se cifran los datos de SAP HANA y de registro, a continuación, las copias de seguridad de hello también no se cifran. Es una toohello cliente toouse alguna forma de copias de seguridad de soluciones de terceros tooencrypt Hola SAP HANA. Vea [datos y el cifrado del volumen de registro](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm) toofind más información sobre el cifrado de SAP HANA.

En Microsoft Azure, un cliente puede utilizar hello tooencrypt de característica de cifrado de VM IaaS. Por ejemplo, uno podría utilizar toohello adjunto de discos de datos dedicada VM, que son utilizado toostore copias de seguridad de SAP HANA, a continuación, realizar copias de estos discos.

Servicio de copia de seguridad de Azure puede controlar las máquinas virtuales/discos cifrados (vea [cómo tooback seguridad y restauración cifran las máquinas virtuales con copia de seguridad de Azure](../../../backup/backup-azure-vms-encryption.md)).

Otra opción sería toomaintain Hola SAP HANA VM y sus discos sin cifrar y almacenar los archivos de copia de seguridad de SAP HANA hello en una cuenta de almacenamiento para el que ha habilitado el cifrado (vea [cifrado del servicio de almacenamiento de Azure para datos en reposo](../../../storage/common/storage-service-encryption.md)) .

## <a name="test-setup"></a>Prueba de configuración

### <a name="test-virtual-machine-on-azure"></a>Prueba de la máquina virtual en Azure

Una instalación de SAP HANA en una máquina virtual GS5 de Azure se usó para hello después de las pruebas de copia de seguridad/restauración.

![Esta ilustración muestra parte de información general del portal Azure para la máquina virtual de prueba HANA Hola Hola](media/sap-hana-backup-guide/image007.png)

En esta ilustración se muestra parte de hello Azure información general del portal para la máquina virtual de prueba HANA Hola.

### <a name="test-backup-size"></a>Prueba de tamaño de copia de seguridad

![En esta ilustración se ha tomado de la consola de copia de seguridad de hello en Studio HANA y muestra el tamaño de archivo de copia de seguridad de Hola para servidor de indexación HANA Hola de 229 GB](media/sap-hana-backup-guide/image008.png)

Una tabla ficticia se llena con datos tooget un tamaño de la copia de seguridad total de los datos más de 200 GB tooderive realista de datos de rendimiento. Figura Hola se ha tomado de la consola de copia de seguridad de hello en Studio HANA y muestra el tamaño de archivo de copia de seguridad de Hola para servidor de indexación HANA Hola de 229 GB. Para las pruebas de hello, Hola predeterminado copia de seguridad "COMPLETE_DATA_BACKUP" en SAP HANA Studio se utilizaba. En los sistemas de producción real, debe definirse un prefijo más útil. SAP HANA Cockpit sugiere la fecha/hora.

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>Toocopy de la herramienta de prueba directamente archivos de almacenamiento de tooAzure

los archivos de copia de seguridad de SAP HANA de tootransfer directamente el almacenamiento de blobs de tooAzure o recursos compartidos de archivos de Azure hello blobxfer usó la herramienta porque admite destinos y pueden integrarse fácilmente en los scripts de automatización de vencimiento tooits interfaz de línea de comandos. Hola blobxfer herramienta está disponible en [GitHub](https://github.com/Azure/blobxfer).

### <a name="test-backup-size-estimation"></a>Prueba de estimación del tamaño de la copia de seguridad

Es importante tooestimate Hola copia de seguridad tamaño de SAP HANA. Esta estimación mejora el rendimiento de tooimprove mediante la definición de tamaño máximo de archivo de copia de seguridad de Hola durante un número de archivos de copia de seguridad, tooparallelism debido al hacer una copia de archivo. (Estos detalles se explican posteriormente en este artículo). También se debe decidir si toodo una completa de copia de seguridad o un delta de copia de seguridad (incremental o diferencial).

Afortunadamente, hay una instrucción SQL que calcula el tamaño de Hola de archivos de copia de seguridad de hello: **seleccione \* de M\_copia de seguridad\_tamaño\_estimaciones** (consulte [ Hola de estimación espacio necesario en hello sistema de archivos para una copia de seguridad de datos](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm)).

![salida de Hello de esta instrucción SQL coincide con casi exactamente Hola tamaño real de copia de seguridad de datos completa de hello en disco](media/sap-hana-backup-guide/image009.png)

Para el sistema de prueba de hello, salida de hello de esta instrucción SQL coincide con casi exactamente Hola tamaño real de copia de seguridad de datos completa de hello en el disco.

### <a name="test-hana-backup-file-size"></a>Prueba del tamaño del archivo de copia de seguridad de HANA

![consola de copia de seguridad de Hello HANA Studio permite un tamaño máximo de archivo de hello toorestrict de archivos de copia de seguridad de HANA](media/sap-hana-backup-guide/image010.png)

consola de copia de seguridad de Hello HANA Studio permite un tamaño máximo de archivo de hello toorestrict de archivos de copia de seguridad de HANA. En el entorno de ejemplo de Hola, esa característica hace posible tooget varias copias de seguridad más pequeños archivos en lugar de un archivo de copia de seguridad de 230 GB. Tamaño de archivo tiene un impacto significativo en el rendimiento (consulte el artículo relacionado de hello [copia de seguridad de Azure de SAP HANA en el nivel de archivo](sap-hana-backup-file-level.md)).

## <a name="summary"></a>Resumen

Se basa en los resultados de pruebas de Hola Hola las tablas siguientes muestra ventajas y desventajas de las soluciones tooback una base de datos de SAP HANA que se ejecutan en máquinas virtuales de Azure.

**Realizar copias de seguridad de copia y sistema de archivos de SAP HANA toohello copia de seguridad de archivos después toohello destino de copia de seguridad final**

|Solución                                           |Ventajas                                 |Desventajas                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Conservación de copias de seguridad de HANA en discos de VM                      |No hay esfuerzos de administración adicionales     |Consume espacio en disco de VM local           |
|Almacenamiento de tooblob de Blobxfer herramienta toocopy archivos de copia de seguridad |Paralelismo toocopy varios archivos, el almacenamiento de blobs de acceso esporádico de toouse de elección | Mantenimiento de la herramienta adicional y scripting personalizado | 
|Copia de blobs a través de Powershell o CLI                    |No es necesaria ninguna herramienta adicional, puede realizarse a través de Azure Powershell o CLI |proceso manual, el cliente tiene tootake atención scripting y administración de blobs copiados para la restauración|
|Recurso compartido de tooNFS                                  |Posterior al procesamiento de archivos de copia de seguridad en otra máquina virtual sin impacto en el servidor de archivos de HANA Hola|Proceso de copia lento|
|Blobxfer copia tooAzure servicio de archivos                |No consume espacio en discos de VM locales|Escritura directa no compatible con copia de seguridad de HANA, restricción del tamaño del recurso compartido de archivo actual de 5 TB|
|Azure Backup Agent                                 | Sería la mejor solución         | No disponible actualmente en Linux    |



**Copia de seguridad de SAP HANA basada en instantáneas de almacenamiento**

|Solución                                           |Ventajas                                 |Desventajas                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Servicio Azure Backup                               | Permite la copia de seguridad de VM basada en instantáneas de blobs | Si no usa restore a nivel de archivo, requiere la creación de hello de una nueva máquina virtual para el proceso de restauración de hello, lo que, a continuación, implica la necesidad de Hola de una nueva clave de licencia de SAP HANA|
|Instantáneas de blobs manuales                              | Flexibilidad toocreate y restore específicos discos de máquina virtual sin cambiar Hola Id. único de máquina virtual|Todo el trabajo manual, que tiene toobe realizarla cliente hello|

## <a name="next-steps"></a>Pasos siguientes
* [SAP HANA Azure copia de seguridad en el nivel de archivo](sap-hana-backup-file-level.md) describe la opción de copia de seguridad basados en archivos Hola.
* [Copia de seguridad de SAP HANA basándose en instantáneas de almacenamiento](sap-hana-backup-storage-snapshots.md) describe Hola almacenamiento basados en instantáneas copia de seguridad de las opciones.
* toolearn tooestablish alta disponibilidad y el plan de recuperación ante desastres de SAP HANA en Azure (instancias grandes), vea [SAP HANA (instancias de gran tamaño) alta disponibilidad y recuperación ante desastres en Azure](hana-overview-high-availability-disaster-recovery.md).
