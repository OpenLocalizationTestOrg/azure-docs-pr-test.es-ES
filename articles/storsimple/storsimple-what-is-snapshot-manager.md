---
title: "¿aaaWhat es el Administrador de instantáneas de StorSimple? | Microsoft Docs"
description: "Describe hello StorSimple Snapshot Manager, su arquitectura y sus características."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>Un administrador de instantáneas tooStorSimple de introducción

## <a name="overview"></a>Información general
Administrador de instantáneas StorSimple es un complemento de Microsoft Management Console (MMC) que simplifica la protección de datos y la administración de las copias de seguridad en un entorno de Microsoft Azure StorSimple. Con el Administrador de instantáneas de StorSimple, puede administrar datos de Microsoft Azure StorSimple en el centro de datos de Hola y en la nube de hello como una solución de almacenamiento de información integrada y, por tanto, lo que simplifica los procesos de copia de seguridad y reducen los costos.

Esta introducción presenta Hola Administrador de instantáneas de StorSimple, describe sus características y explica su función en Microsoft Azure StorSimple. 

Para obtener información general del sistema de Microsoft Azure StorSimple todo hello, incluidos los dispositivos de StorSimple de hello, el servicio StorSimple Manager, Administrador de instantáneas StorSimple y el adaptador de StorSimple para SharePoint, consulte [serie StorSimple 8000: una nube híbrida solución de almacenamiento](storsimple-overview.md). 

> [!NOTE]
> * No puede usar el Administrador de instantáneas StorSimple toomanage Microsoft Azure StorSimple Virtual matrices (también conocido como StorSimple virtuales dispositivos locales).
> * Si tiene previsto tooinstall StorSimple Update 2 en el dispositivo StorSimple, ser seguro toodownload Hola última versión del Administrador de instantáneas de StorSimple e instalarlo **antes de instalar StorSimple Update 2**. la versión más reciente de Hola de StorSimple Snapshot Manager es compatible con versiones anteriores y funciona con todas las versiones publicadas de Microsoft Azure StorSimple. Si está utilizando la versión anterior de Hola de administrador de instantáneas de StorSimple, necesitará tooupdate TI (no necesita toouninstall Hola anterior versión antes de instalar la nueva versión de hello).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>Arquitectura y propósito de Administrador de instantáneas StorSimple
Administrador de instantáneas StorSimple proporciona una consola de administración central que puede usar toocreate coherente, copias de seguridad en el momento de local y nube datos. Por ejemplo, puede usar la consola de Hola para:

* Configurar, crear copias de seguridad y eliminar volúmenes.
* Configurar el volumen tooensure de grupos que la copia de seguridad de datos es coherente con la aplicación.
* Administrar directivas de copia de seguridad, con el fin de que las copias de seguridad de los datos se realicen según una programación predeterminada.
* Crear local y en la nube, que se pueden almacenar en la nube de Hola y usado para la recuperación ante desastres.

Hola, Administrador de instantáneas StorSimple captura lista Hola de aplicaciones registradas con el proveedor VSS de hello en el host de Hola. A continuación, toocreate coherentes con la aplicación copias de seguridad, comprueba los volúmenes de hello utilizado por una aplicación y sugiere tooconfigure de grupos de volumen. Administrador de instantáneas StorSimple usa estas copias de seguridad de toogenerate grupos de volumen que son coherentes con la aplicación. (Coherencia de la aplicación existe cuando todos los archivos relacionados y las bases de datos están sincronizados y representan Hola estado real de la aplicación hello en un momento concreto en el tiempo). 

Las copias de seguridad de administrador de instantáneas StorSimple adoptan la forma de Hola de instantáneas incrementales que capturan únicamente los cambios de Hola desde la última copia de seguridad de Hola. Como consecuencia, las copias de seguridad requieren menos espacio de almacenamiento y se pueden crear y restaurar rápidamente. Administrador de instantáneas StorSimple usa tooensure de servicio de copia de instantáneas de volumen (VSS) de Windows hello que las instantáneas capturan datos coherentes con la aplicación. (Para obtener más información, vaya toohello integración con la sección Windows Volume Shadow Copy Service). Con Administrador de instantáneas StorSimple, puede crear programaciones de copia de seguridad o hacer copias inmediatas, según sea necesario. Si necesita datos toorestore desde una copia de seguridad, permite el Administrador de instantáneas StorSimple seleccione desde un catálogo de variable local o de instantáneas en la nube. StorSimple de Azure restaura solo Hola datos que son necesarios cuando es necesario, lo que impide que los retrasos en la disponibilidad de los datos durante las operaciones de restauración).

![Arquitectura de Administrador de instantáneas StorSimple](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**Arquitectura de Administrador de instantáneas StorSimple** 

## <a name="support-for-multiple-volume-types"></a>Compatibilidad con varios tipos de volumen
Puede usar hello tooconfigure de administrador de instantáneas StorSimple y respaldar Hola siguientes tipos de volúmenes: 

* **Volúmenes básicos** : un volumen básico es una sola partición en un disco básico. 
* **Volúmenes simples**: un volumen simple es un volumen dinámico que contiene el espacio en disco de un único disco dinámico. Un volumen simple se compone de una única región en un disco o varias regiones vinculadas entre sí en Hola mismo disco. (Los volúmenes simples solo se pueden crear en discos dinámicos.) Los volúmenes simples no son tolerantes a errores.
* **Volúmenes dinámicos** : un volumen dinámico es un volumen creado en un disco dinámico. Los discos dinámicos utilizan una base de datos tootrack información de los volúmenes que se encuentran en discos dinámicos en un equipo. 
* **Volúmenes dinámicos con reflejo** : volúmenes dinámicos con reflejo se crean en arquitecturas de hello RAID 1. Con RAID 1, se escriben datos idénticos en dos o más discos, lo que genera un conjunto reflejado. Una solicitud de lectura, a continuación, puede controlarse mediante cualquier disco que contiene Hola datos solicitados.
* **Volúmenes compartidos de clúster** – con volúmenes compartidos de clúster (CSV), varios nodos en un clúster de conmutación por error al mismo tiempo pueden leer o escribir toohello mismo disco. Conmutación por error de un nodo tooanother nodo puede producirse rápidamente, sin necesidad de un cambio en la propiedad de la unidad o montar, desmontar y eliminar un volumen. 

> [!IMPORTANT]
> No mezcle los csv y no csv en hello misma instantánea. No se admite la mezcla de CSV y no CSV en una instantánea. 
> 
> 

Puede usar grupos de volúmenes completos de administrador de instantáneas StorSimple toorestore o clonar volúmenes individuales y recuperar archivos individuales.

* [Volúmenes y grupos de volúmenes](#volumes-and-volume-groups) 
* [Tipos de copia de seguridad y directivas de copia de seguridad](#backup-types-and-backup-policies) 

Para obtener más información acerca de las características de administrador de instantáneas StorSimple y toouse, vea [interfaz de usuario de administrador de instantáneas StorSimple](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Volúmenes y grupos de volúmenes
Con Administrador de instantáneas StorSimple, es posible crear volúmenes y, a continuación, configurarlos en grupos de volúmenes. 

Administrador de instantáneas StorSimple usa volumen grupos toocreate copias de seguridad que son coherentes con la aplicación. Coherencia de la aplicación existe cuando todos los archivos relacionados y las bases de datos están sincronizados y representan Hola estado real de una aplicación en un momento concreto en el tiempo. Grupos de volúmenes (también conocido como que son *grupos de consistencia*) forman Hola base de una copia de seguridad o restaurar el trabajo.

Grupos de volúmenes no se Hola igual que los contenedores de volúmenes. Un contenedor de volúmenes contiene uno o varios volúmenes que comparten una cuenta de almacenamiento de nube y otros atributos, como el consumo de ancho de banda y el cifrado. Un único contenedor de volúmenes puede contener hasta los volúmenes de StorSimple too256 aprovisionado fino. Para obtener más información sobre contenedores de volúmenes, vaya demasiado[administrar los contenedores de volúmenes](storsimple-manage-volume-containers.md). Grupos de volúmenes son conjuntos de volúmenes que configure las operaciones de copia de seguridad de toofacilitate. Si selecciona dos volúmenes que pertenecen los contenedores de volúmenes toodifferent, colóquelos en un único grupo de volúmenes y, a continuación, crear una directiva de copia de seguridad para ese grupo de volúmenes, cada volumen se copiarán en el contenedor de volumen correspondiente de hello, con almacenamiento adecuado de Hola cuenta.

> [!NOTE]
> Todos los volúmenes de un grupo de volúmenes deben provenir de un solo proveedor de servicios en la nube.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Integración con el Servicio de instantáneas de volumen de Windows
Administrador de instantáneas StorSimple usa Hola datos coherentes con la aplicación de servicio de copia de instantáneas de volumen (VSS) de Windows toocapture. VSS facilita la coherencia con las aplicaciones comunicándose con la creación de hello de toocoordinate de las aplicaciones basadas en VSS de instantáneas incrementales. VSS garantiza que las aplicaciones de hello están temporalmente inactivas o inactiva, cuando se realizan las instantáneas. 

implementación de administrador de instantáneas StorSimple Hola de VSS funciona con SQL Server y volúmenes NTFS genéricos. proceso de Hello es el siguiente: 

1. Un solicitante, que normalmente es una administración de datos y solución de protección (por ejemplo, Administrador de instantáneas StorSimple) o una aplicación de copia de seguridad, invoca a VSS y le pide información de toogather de software de sistema de escritura de hello en la aplicación de destino de Hola.
2. Contactos VSS Hola tooretrieve de componente de sistema de escritura una descripción de los datos de Hola. escritor de Hello devuelve la descripción de Hola de hello datos toobe copia de seguridad. 
3. VSS envía una señal de aplicación de hello tooprepare Hola de escritura para copia de seguridad. escritor de Hello prepara los datos de Hola para copia de seguridad completando las transacciones completadas, actualizando los registros de transacciones y así sucesivamente y, a continuación, notifica a VSS.
4. VSS indica a escritor hello tootemporarily stop Hola datos de la aplicación almacenan y asegúrese de que no se escriben datos toohello volumen mientras se crea la instantánea de Hola. Este paso garantiza la coherencia de datos y no tarda más de 60 segundos en completarse.
5. VSS indica Hola proveedor toocreate Hola de instantáneas. Los proveedores, que pueden ser según de software o hardware, administración volúmenes de Hola que se están ejecutando actualmente y crear instantáneas de ellos a petición. proveedor de Hello crea instantáneas de Hola y notifica a VSS cuando se completan.
6. VSS contactos hello toonotify Hola aplicación escritura que puede reanudar la E/S y también tooconfirm que E/S se pausó correctamente durante la sombra copie creación. 
7. Si copia Hola se realizó correctamente, VSS devuelve Hola solicitante de toohello de ubicación de la copia. 
8. Si se escribieron datos mientras creaba la instantánea de hello, copia de seguridad de hello serán incoherente. VSS elimina la instantánea de Hola y notifica al solicitante Hola. Hello solicitante puede repetir el proceso de copia de seguridad de hello automáticamente o notificar Hola administrador tooretry en un momento posterior.

Vea Hola siguiente ilustración.

![Proceso VSS](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Proceso del Servicio de instantáneas de volumen de Windows** 

## <a name="backup-types-and-backup-policies"></a>Tipos de copia de seguridad y directivas de copia de seguridad
Con el Administrador de instantáneas de StorSimple, puede realizar copias de seguridad de los datos y almacenarlos localmente y en la nube de Hola. Puede usar el Administrador de instantáneas StorSimple tooback los datos inmediatamente o puede usar un toocreate una programación de directiva de copia de seguridad para realizar copias de seguridad automáticamente. Las directivas de copia de seguridad también permiten toospecify cuántas instantáneas se conservarán. 

### <a name="backup-types"></a>Tipos de copia de seguridad
Puede usar Hola de administrador de instantáneas StorSimple toocreate siguientes tipos de copias de seguridad:

* **Las instantáneas locales** : las instantáneas locales son copias instantáneas de datos del volumen que se almacenan en el dispositivo StorSimple Hola. Normalmente, este tipo de copia de seguridad se puede crear y restaurar rápidamente. Puede usar una instantánea local como lo haría con una copia de seguridad local.
* **Instantáneas en la nube** : instantáneas en la nube son copias instantáneas de datos del volumen que se almacenan en la nube de Hola. Una instantánea en la nube es equivalente instantánea de tooa replicada en un sistema de almacenamiento diferente, fuera del sitio. Las instantáneas en la nube son especialmente útiles en escenarios de recuperación ante desastres.

### <a name="on-demand-and-scheduled-backups"></a>Copias de seguridad a petición y programadas
Con el Administrador de instantáneas de StorSimple, puede iniciar una única toobe de copia de seguridad creado inmediatamente, o puede usar un tooschedule de directiva de copia de seguridad periódica de las operaciones de copia de seguridad.

Una directiva de copia de seguridad es un conjunto de reglas automatizadas que se pueden usar copias de seguridad periódicas de tooschedule. Una directiva de copia de seguridad permite toodefine Hola frecuencia y los parámetros para realizar instantáneas de un grupo de volúmenes específico. Puede usar fechas de inicio y caducidad de toospecify de directivas, horas, frecuencias y requisitos de retención para ambos local y en la nube. Las directivas se aplican inmediatamente después de que se definen. 

Puede usar el Administrador de instantáneas StorSimple tooconfigure o volver a configurar las directivas de copia de seguridad siempre que sea necesario. 

Configurar Hola siguiente información para cada directiva de copia de seguridad que cree:

* **Nombre** : nombre único de Hola de hello seleccionada Directiva de copia de seguridad.
* **Tipo de** : Hola tipo de directiva de copia de seguridad: instantánea local o instantánea en la nube.
* **Grupo de volúmenes** : directiva de copia de seguridad de hello volumen grupo toowhich Hola seleccionado se asigna.
* **Retención** : Hola número de copias de seguridad tooretain. Si selecciona hello **todos los** cuadro, todas las copias de seguridad se conservan hasta que se alcanza el número máximo de Hola de copias de seguridad por volumen, en qué punto Hola directiva provocarán errores y generar un mensaje de error. Como alternativa, puede especificar un número de copias de seguridad tooretain (entre 1 y 64).
* **Fecha** : fecha de hello cuando se creó la directiva de copia de seguridad de Hola.

Para obtener información acerca de cómo configurar las directivas de copia de seguridad, vaya demasiado[toocreate Use el Administrador de instantáneas de StorSimple y administrar las directivas de copia de seguridad](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Supervisión y administración de trabajos de copia de seguridad
Puede usar hello toomonitor de administrador de instantáneas StorSimple y administrar trabajos de copia de seguridad de las próximas, programados y completados. Además, el Administrador de instantáneas StorSimple proporciona un catálogo de copias de seguridad too64 completado. Puede usar Hola catálogo toofind y restaurar volúmenes o archivos individuales. 

Para obtener información acerca de la supervisión de trabajos de copia de seguridad, vaya demasiado[tooview Use el Administrador de instantáneas de StorSimple y administrar los trabajos de copia de seguridad](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre [mediante el Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).
* Descargue el [Administrador de instantáneas StorSimple](https://www.microsoft.com/download/details.aspx?id=44220).

