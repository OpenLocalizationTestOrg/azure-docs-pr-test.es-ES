---
title: aaaIntroduction tooAzure almacenamiento de pila
description: "Más información acerca de Azure Stack Storage"
services: azure-stack
documentationcenter: 
author: xiaofmao
manager: 
editor: 
ms.assetid: 092aba28-04bc-44c0-90e1-e79d82f4ff42
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/19/2017
ms.author: xiaofmao
ms.openlocfilehash: 8e156584dafb8b084bfc69b9dbe7cbaa78717135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-stack-storage"></a>Introducción tooAzure almacenamiento de pila

## <a name="overview"></a>Información general
Azure Stack Storage es un conjunto de servicios de almacenamiento en la nube que incluyen blobs, tablas y colas que son coherentes con los servicios de Azure Storage.

## <a name="azure-stack-storage-services"></a>Servicios de Azure Stack Storage
Almacenamiento de Azure pila proporciona Hola siguiendo los tres servicios:

* **Blob Storage** 

    Blob Storage almacena datos de objetos no estructurados. Un blob puede ser un tipo cualquiera de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.
* **Table Storage** 

    El almacenamiento de tablas almacena conjuntos de datos estructurados. Almacenamiento de tabla es un almacén de datos del atributo de clave NoSQL, que permite el desarrollo rápido y las cantidades de toolarge de acceso rápido de datos.
* **Queue Storage** 

    El almacenamiento de colas ofrece una solución de mensajería confiable para el procesamiento de flujos de trabajo y para la comunicación entre los componentes de los servicios en la nube.

Una cuenta de almacenamiento de la pila de Azure es una cuenta segura que proporciona acceso a tooservices en la pila de almacenamiento de Azure. La cuenta de almacenamiento proporciona Hola espacio de nombres único para los recursos de almacenamiento. Hello diagrama siguiente muestra las relaciones de hello entre Hola recursos de almacenamiento de Azure pila en una cuenta de almacenamiento:

![Introducción a Azure Stack Storage](media/azure-stack-storage-overview/AzureStackStorageOverview.png)


### <a name="blob-storage"></a>Almacenamiento de blobs

Para los usuarios con una gran cantidad de toostore de datos de objeto no estructurados en la nube de hello, almacenamiento de blobs ofrece una solución escalable y eficaz. Puede usar el contenido de toostore de almacenamiento de blobs como:

* Documentos
* Datos de contenido social, como fotos, vídeos, música y blogs
* Copias de seguridad de archivos, equipos, bases de datos y dispositivos
* Imágenes y texto para las aplicaciones web
* Datos de configuración para las aplicaciones en la nube
* Datos de gran tamaño, como registros y otros conjuntos de datos grandes

Cada blob se organiza en un contenedor. Los contenedores también proporcionan un toogroups de directivas de seguridad de un modo útil tooassign de objetos. Una cuenta de almacenamiento puede contener cualquier número de contenedores y un contenedor puede contener cualquier número de blobs, la limitación de toohello de cuenta de almacenamiento.

Blob Storage ofrece tres tipos de blobs: 
* **Blobs en bloques** 

    Los blobs en bloques están optimizados para el streaming y para el almacenamiento de objetos en la nube, y constituyen una opción idónea para almacenar documentos, archivos multimedia y copias de seguridad, entre otros.
* **Blobs en anexos** 

    Anexar blobs de blobs de tooblock similares, pero están optimizados para las operaciones de anexión. Se puede actualizar un blob en anexos agregando un nuevo extremo toohello de bloque. Anexar blobs son una buena elección para escenarios como la del registro, donde nuevos datos necesitan toobe escribe solo toohello final del blob de Hola.
* **Blobs en páginas** 

    Blobs en páginas se optimización para representar los discos de IaaS y admitir aleatorio de escrituras que es hasta too1 TB de tamaño. Un disco IaaS asociado a una máquina virtual de Azure Stack es un VHD almacenado como blob en páginas.


### <a name="table-storage"></a>Almacenamiento de tablas
A menudo, las aplicaciones modernas demandan almacenes de datos con una flexibilidad y escalabilidad superiores a las que requerían las generaciones anteriores de software. Almacenamiento de tabla ofrece un almacenamiento altamente disponible y escalable de forma masiva, por lo que la aplicación puede escalar automáticamente toomeet demanda de los usuarios. Este tipo de almacenamiento se basa en un almacén de claves/atributos NoSQL de Microsoft con un diseño sin esquema que lo diferencia de las bases de datos relacionales tradicionales. Con un almacén de datos schemaless, resulta fácil tooadapt necesidades de los datos como Hola de evolucionar de la aplicación. Almacenamiento de tabla es fácil toouse, por lo que los desarrolladores pueden crear aplicaciones rápidamente.

Este tipo de almacenamiento se basa en un almacén de clave-atributo, lo que significa que cada valor de una tabla se almacena con un nombre de propiedad tipado. nombre de la propiedad de Hello puede usarse para filtrar y especificar criterios de selección. Una colección de propiedades y sus valores, componen una entidad. Puesto que el almacenamiento de tabla es schemaless, dos entidades en Hola misma tabla puede contener diferentes colecciones de propiedades y esas propiedades pueden ser de tipos diferentes.

Puede usar la tabla almacenamiento toostore flexible conjuntos de datos, como los datos de usuario para aplicaciones web, libretas de direcciones, información del dispositivo y cualquier otro tipo de metadatos que necesite el servicio. Para aplicaciones basadas en Internet de hoy en día, las bases de datos NoSQL como el almacenamiento de tabla ofrecen una popular tootraditional alternativo bases de datos relacionales.

Una cuenta de almacenamiento puede contener cualquier número de tablas y una tabla puede contener cualquier número de entidades, una toohello el límite de capacidad de la cuenta de almacenamiento de Hola.

### <a name="queue-storage"></a>Queue Storage
A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente. Almacenamiento de cola proporciona una solución de mensajería confiable para la comunicación asincrónica entre los componentes de aplicación, si se están ejecutando en la nube de hello, en el escritorio de hello, en un servidor local o en un dispositivo móvil. Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.

Una cuenta de almacenamiento puede contener cualquier número de colas y una cola puede contener cualquier número de mensajes, seguridad toohello el límite de capacidad de la cuenta de almacenamiento de Hola. Los mensajes individuales pueden ser up too64 KB de tamaño.

## <a name="next-steps"></a>Pasos siguientes
* [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md) (Azure Stack Storage: diferencias y consideraciones)

* toolearn más sobre el almacenamiento de Azure, consulte [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md)

