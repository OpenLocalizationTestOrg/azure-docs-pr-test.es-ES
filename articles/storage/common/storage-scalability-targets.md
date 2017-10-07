---
title: aaaAzure objetivos de rendimiento y escalabilidad de almacenamiento | Documentos de Microsoft
description: "Obtenga información acerca de los destinos de escalabilidad y rendimiento de hello para el almacenamiento de Azure, incluida la capacidad, la tasa de solicitud y ancho de banda entrante y saliente para ambas cuentas de almacenamiento estándar y premium. Comprender los objetivos de rendimiento de las particiones dentro de cada uno de los servicios de almacenamiento de Azure de Hola."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 7afe4366a02887b4e3d9781c26c8adda81adce95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Objetivos de escalabilidad y rendimiento del almacenamiento de Azure
## <a name="overview"></a>Información general
Este tema describe los temas de escalabilidad y rendimiento de hello para el almacenamiento de Azure de Microsoft. Para ver un resumen de otros límites de Azure, consulte [Suscripción de Azure y límites de servicio, cuotas y restricciones](../../azure-subscription-service-limits.md).

> [!NOTE]
> Todas las cuentas de almacenamiento ejecutan en hello nueva topología de red plana y admitan destinos de escalabilidad y rendimiento de hello, que se detallan a continuación, independientemente de cuándo se crearon. Para más información sobre la arquitectura de red plana de almacenamiento de Azure de Hola y acerca de la escalabilidad, vea [almacenamiento de Microsoft Azure: altamente disponible en la nube almacenamiento servicio con coherencia segura](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> destinos de escalabilidad y rendimiento de Hello enumerados aquí son destinos de tecnología avanzados, pero pueden llevarse a cabo. En todos los casos, la solicitud de hello velocidad y ancho de banda obtenido por su cuenta de almacenamiento depende de tamaño de Hola de los objetos almacenados, los patrones de acceso de hello utilizan y Hola tipo de carga de trabajo que se realiza de la aplicación. Ser seguro tootest su toodetermine de servicio si su rendimiento adecúa a sus requisitos. Si es posible, evite picos repentinos en la tasa de Hola de tráfico y asegúrese de que el tráfico se distribuye equitativamente entre las particiones.
> 
> Cuando la aplicación alcanza el límite de Hola de lo que puede administrar una partición para la carga de trabajo, el almacenamiento de Azure se iniciará tooreturn código de error 503 (servidor ocupado) o código de error 500 respuestas (tiempo de espera de operación). Cuando esto ocurre, aplicación hello debe usar una directiva de retroceso exponencial para reintentos. Hola retroceso exponencial permite carga Hola Hola partición toodecrease y tooease los picos en la partición de toothat de tráfico.
> 
> 

Si de la aplicación hello debe superar los objetivos de escalabilidad de Hola de una única cuenta de almacenamiento, puede compilar su aplicación toouse varias cuentas de almacenamiento y crear particiones de los objetos de datos a través de las cuentas de almacenamiento. Para obtener información sobre los precios por volumen, consulte [Precios de Almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/) .

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Objetivos de escalabilidad para blobs, colas, tablas y archivos
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Objetivos de escalabilidad para discos de máquinas virtuales
[!INCLUDE [azure-storage-limits-vm-disks](../../../includes/azure-storage-limits-vm-disks.md)]

Consulte el artículo sobre [tamaños de VM de Windows](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [tamaños de las VM Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener más información.

## <a name="managed-virtual-machine-disks"></a>Discos de máquinas virtuales administrados

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Discos de máquinas virtuales no administrados
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Objetivos de escalabilidad para el Administrador de recursos de Azure
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Particiones de Almacenamiento de Azure
Todos los objetos que contiene los datos que se almacenan en el almacenamiento de Azure (blobs, mensajes, entidades y archivos) pertenece tooa partición y se identifican mediante una clave de partición. partición de Hello determina cómo el almacenamiento de Azure equilibra la carga de blobs, mensajes, entidades y archivos a través de necesidades de tráfico de servidores toomeet Hola de dichos objetos. clave de partición de Hello es único y toolocate usado un blob, mensaje o entidad.

tabla de Hello mostrado anteriormente en [objetivos de escalabilidad de las cuentas de almacenamiento estándar](#standard-storage-accounts) listas Hola objetivos de rendimiento de una sola partición para cada servicio.

Las particiones son determinantes equilibrio de carga y escalabilidad para cada uno de los servicios de almacenamiento de Hola Hola siguientes maneras:

* **Blobs**: clave de partición de Hola para un blob es nombre de cuenta, nombre del contenedor + nombre de blob. Esto significa que cada blob puede tener su propia partición si se carga en el blob de hello lo requiera. Blobs se pueden distribuir en varios servidores en orden tooscale out toothem de acceso, pero solo se puede atender un único blob mediante un solo servidor. Aunque los blobs pueden agruparse lógicamente en contenedores de blob, esta agrupación no afecta a las particiones.
* **Archivos**: clave de partición de Hola para un archivo es nombre + archivo comparte el nombre de cuenta. Esto significa que todos los archivos de un recurso compartido de archivos también están en una sola partición.
* **Mensajes**: clave de partición de Hola para un mensaje es el nombre de cuenta de hello + nombre de la cola, por lo que todos los mensajes en una cola se agrupan en una sola partición y se sirven mediante un único servidor. Diferentes colas pueden ser procesadas por distintos servidores hello toobalance cargar para sin embargo, muchas de las colas que puede tener una cuenta de almacenamiento.
* **Entidades**: clave de partición de Hola para una entidad es el nombre de la cuenta + nombre de la tabla + clave de partición, donde clave de partición de hello es valor Hola de hello necesario definidos por el usuario **PartitionKey** propiedad de entidad de Hola. Todas las entidades con hello mismo valor de clave de partición se agrupan en hello misma partición y se atienden Hola con el mismo servidor de partición. Se trata de un toounderstand punto importante en el diseño de la aplicación. La aplicación debería equilibrar ventajas de escalabilidad de hello dispersión de entidades entre varias particiones con hello ventajas de acceso a datos de agrupación de entidades en una sola partición.  

Un toogrouping un conjunto de entidades en una tabla en una sola partición de ventaja clave es que resulta operaciones atómicas por lotes de tooperform posible a través de las entidades de hello misma partición, puesto que existe una partición en un único servidor. Por lo tanto, si desea tooperform operaciones por lotes en un grupo de entidades, considere la posibilidad de agruparlos con hello misma clave de partición. 

En Hola otra parte, las entidades que se encuentran en hello misma tabla pero tienen claves de partición diferente pueden ser la carga equilibrada en diferentes servidores, lo que sea posible toohave mayor escalabilidad.

Puede obtener recomendaciones detalladas sobre el diseño de la estrategia de partición para tablas [aquí](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Otras referencias
* [Detalles de precios de almacenamiento](https://azure.microsoft.com/pricing/details/storage/)
* [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../../azure-subscription-service-limits.md)
* [Almacenamiento premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../storage-premium-storage.md)
* [Replicación de almacenamiento de Azure](../storage-redundancy.md)
* [Lista de comprobación de rendimiento y escalabilidad de Almacenamiento de Microsoft Azure](../storage-performance-checklist.md)
* [Almacenamiento de Microsoft Azure: un servicio de almacenamiento en nube altamente disponible con gran coherencia](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

