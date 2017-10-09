---
title: "soluciones de aaaStorage para máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para implementar soluciones de almacenamiento en los servicios de infraestructura de Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57c27a7305964a56e6b2d1e73dee8e7da19fa8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a>Directrices de infraestructura de Azure Storage para máquinas virtuales Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Este artículo se centra en entender las necesidades de almacenamiento y las consideraciones de diseño para conseguir un rendimiento óptimo de la máquina virtual.

## <a name="implementation-guidelines-for-storage"></a>Directrices de implementación para el almacenamiento
Decisiones:

* ¿Vas toouse Azure administra discos o discos no administrados?
* ¿Necesita almacenamiento Standard o Premium de toouse para la carga de trabajo?
* ¿Necesita discos de toocreate de creación de bandas en disco más de 4TB?
* ¿Necesita rendimiento de E/S óptimo de tooachieve de creación de bandas de disco para la carga de trabajo?
* El conjunto de cuentas de almacenamiento ¿necesita toohost su infraestructura o la carga de trabajo de TI?

Tareas:

* Revise las demandas de E/S de las aplicaciones de hello va a implementar y planear el número adecuado de Hola y el tipo de cuentas de almacenamiento.
* Crear conjunto de Hola de cuentas de almacenamiento mediante la convención de nomenclatura. Puede usar Azure PowerShell o portal de Hola.

## <a name="storage"></a>Storage
Almacenamiento de Azure es una parte clave del proceso de implementación y administración de aplicaciones y máquinas virtuales. Almacenamiento de Azure proporciona servicios para almacenar los datos de archivo, los datos no estructurados y mensajes, y también es parte de la infraestructura de hello admitir máquinas virtuales.

[Azure discos administrados](../../storage/storage-managed-disks-overview.md) controla el almacenamiento de entre bastidores de Hola. Con los discos no administrados, crea cuentas de almacenamiento toohold Hola discos (archivos VHD) para las máquinas virtuales de Azure. Cuando el escalado, debe asegurarse de que crea cuentas de almacenamiento adicionales, por lo que no superan el límite IOPS de hello para el almacenamiento con cualquiera de los discos. Con discos administrados controlar el almacenamiento, ya no está limitado por hello límites de la cuenta de almacenamiento (por ejemplo, 20.000 IOPS / cuenta). También ya no tiene toocopy sus cuentas de almacenamiento de toomultiple imágenes personalizadas (archivos VHD). También puede administrarlos en una ubicación central: una cuenta de almacenamiento por cada región de Azure – y usarlos toocreate cientos de máquinas virtuales en una suscripción. Se recomienda utilizar Managed Disks para las nuevas implementaciones.

Existen dos tipos de cuentas de almacenamiento disponibles para la compatibilidad con máquinas virtuales.

* Conceda a las cuentas de almacenamiento estándar que tener acceso al almacenamiento de tooblob (que se usa para almacenar los discos de máquina virtual de Azure), la tabla de almacenamiento, almacenamiento de cola y almacenamiento de archivos.
* [Premium Storage](../../storage/storage-premium-storage.md) ofrecen compatibilidad con discos de alto rendimiento y baja latencia para cargas de trabajo de E/S intensivas, como los servidores SQL Server de un clúster de AlwaysOn. En estos momentos, Premium Storage solo admite discos de máquinas virtuales de Azure.

Azure crea máquinas virtuales con un disco del sistema operativo, un disco temporal y ninguno o varios discos de datos opcionales. el disco del sistema operativo de Hola y discos de datos son blobs en páginas de Azure, mientras que el disco temporal de Hola se almacena localmente en el nodo de Hola donde reside la máquina de Hola. Tenga cuidado al diseñar aplicaciones tooonly usen este disco temporal para los datos no persistentes como Hola máquina virtual se puede migrar entre hosts durante un evento de mantenimiento. Todos los datos almacenados en disco temporal de Hola se perderían.

Alta disponibilidad y durabilidad proporciona hello tooensure de entorno de almacenamiento de Azure subyacente que los datos permanecen protegidos frente a errores de hardware o de mantenimiento no planeados. Al diseñar su entorno de almacenamiento de Azure, puede elegir tooreplicate almacenamiento de máquina virtual:

* Localmente dentro de un determinado centro de datos de Azure
* En centros de datos de Azure dentro de una región determinada
* En centros de datos de Azure de diferentes regiones

Puede leer [más acerca de las opciones de replicación de Hola para lograr alta disponibilidad](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Los discos de datos y del sistema operativo tienen un tamaño máximo de 4 TB. Puede usar espacios de almacenamiento en Windows Server 2012 o posterior toosurpass este límite por la agrupación juntos datos discos toopresent lógico volúmenes mayores de 4TB tooyour máquina virtual.

Existen algunos límites de escalabilidad que se aplican a la hora de diseñar las implementaciones de Azure Storage. Consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../../azure-subscription-service-limits.md#storage-limits) para obtener más información. Consulte también [Objetivos de escalabilidad y rendimiento del almacenamiento en Azure](../../storage/storage-scalability-targets.md).

En cuanto al almacenamiento de aplicaciones, puede guardar datos de objetos no estructurados como documentos, imágenes, copias de seguridad, datos de configuración, registros, etc. mediante Blob Storage. En lugar de la aplicación escribir tooa disco virtual conectado toohello VM, aplicación hello puede escribir directamente el almacenamiento de blobs de tooAzure. Almacenamiento de blobs también proporciona la opción de Hola de [caliente y estupendo capas de almacenamiento](../../storage/storage-blob-storage-tiers.md) según sus necesidades de disponibilidad y las restricciones de costo.

## <a name="striped-disks"></a>Discos con bandas
Además de permitirle toocreate discos mayores de 4TB, en muchos casos, el uso de creación de bandas en discos de datos mejora el rendimiento al permitir que varios blobs de almacenamiento de hello tooback un único volumen. Con el seccionamiento, Hola E/S necesario toowrite y los datos leídos de un único disco lógico se realiza en paralelo.

Azure impone límites de número Hola de discos de datos y la cantidad de ancho de banda disponible, según el tamaño de la máquina virtual de Hola. Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md).

Si usas la creación de bandas en disco para los discos de datos de Azure, considere la posibilidad de hello siguientes instrucciones:

* Conectar discos de datos máximo de hello permitidos para hello tamaño de máquina virtual.
* Use Espacios de almacenamiento.
* Evite utilizar opciones de almacenamiento en caché de discos de datos de Azure (directiva de almacenamiento en caché = Ninguna).

Para obtener más información, consulte [Espacios de almacenamiento - Diseño para el rendimiento](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).

## <a name="multiple-storage-accounts"></a>Cuentas de almacenamiento múltiples
En esta sección no se aplica demasiado[discos de Azure administrados](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ya que usted no crea cuentas de almacenamiento independientes. 

Al diseñar su entorno de almacenamiento de Azure para los discos no administrados, puede usar varias cuentas de almacenamiento según el número de Hola de máquinas virtuales que implemente aumenta. Este enfoque ayuda a distribuir out Hola E/S a través de hello subyacente almacenamiento de Azure infraestructura toomaintain un rendimiento óptimo para las máquinas virtuales y las aplicaciones. Al diseñar aplicaciones de Hola que va a implementar, tenga en cuenta los requisitos de E/S de hello que tiene de cada máquina virtual y saldo de esas máquinas virtuales entre cuentas de almacenamiento de Azure. Intente tooavoid agrupar todas las E/S altas de hello exigentes máquinas virtuales en toojust uno o dos cuentas de almacenamiento.

Para obtener más información acerca de las capacidades de hello E/S de opciones de almacenamiento de Azure diferentes de Hola y algunos recomiendan valores máximos, consulte [destinos de escalabilidad y rendimiento de almacenamiento de Azure](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

