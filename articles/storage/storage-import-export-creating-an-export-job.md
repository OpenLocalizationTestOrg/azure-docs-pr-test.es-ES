---
title: "aaaCreate una exportación de trabajo para la importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una exportación de trabajo para hello servicio de importación y exportación de Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Crear un trabajo de exportación para hello servicio de importación y exportación de Azure
La creación de un trabajo de exportación para servicio de importación y exportación de Microsoft Azure de hello mediante API de REST de hello implica Hola pasos:

-   Seleccionar Hola blobs tooexport.

-   Obtener una ubicación de envío.

-   Crear trabajo de exportación de Hola.

-   Enviar su tooMicrosoft de unidades de disco vacías a través de un servicio de transporte admitido.

-   Actualizar el trabajo de exportación de hello con información del paquete Hola.

-   Recibir hello las unidades de Microsoft.

 Vea [con hello importación y exportación de Windows Azure service tooTransfer datos tooBlob almacenamiento](storage-import-export-service.md) para obtener información general del servicio de importación y exportación de Hola y un tutorial que demuestra cómo hello toouse [portal de Azure](https://portal.azure.com/) toocreate y administrar la importación y exportación de trabajos.

## <a name="selecting-blobs-tooexport"></a>Seleccionar tooexport de blobs
 toocreate un trabajo de exportación, deberá tooprovide una lista de blobs que desee tooexport desde su cuenta de almacenamiento. Hay varias maneras de tooselect toobe exportan los blobs:

-   Puede usar un tooselect de ruta de acceso relativa del blob un único blob y todas sus instantáneas.

-   Puede usar un tooselect de ruta de acceso relativa del blob en un solo blob, excepto sus instantáneas.

-   Puede usar una ruta de acceso relativa del blob y un tooselect de tiempo de la instantánea una sola instantánea.

-   Puede usar un tooselect de prefijo de blob todos los blobs e instantáneas con hello tiene prefijo.

-   Puede exportar todos los blobs e instantáneas en la cuenta de almacenamiento de Hola.

 Para obtener más información acerca de cómo especificar los blobs tooexport, vea hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación.

## <a name="obtaining-your-shipping-location"></a>Obtención de la ubicación de envío
Antes de crear un trabajo de exportación, deberá tooobtain un nombre de la ubicación de envío y la dirección por llamada hello [obtener ubicación](https://portal.azure.com) o [ubicaciones de la lista](/rest/api/storageimportexport/listlocations) operación. `List Locations` devolverá una lista de ubicaciones y sus direcciones de correo. Puede seleccionar una ubicación de hello devuelve la lista y enviar su dirección de toothat de unidades de disco duro. También puede usar hello `Get Location` Hola de tooobtain operación directamente de la dirección de una ubicación específica de envío.

Siga los pasos de Hola por debajo de la ubicación de envío de Hola tooobtain:

-   Identificar el nombre de Hola de ubicación de saludo de la cuenta de almacenamiento. Este valor puede encontrarse en hello **ubicación** campo de la cuenta de almacenamiento de hello **panel** en clásico de hello portal o puede consultarse mediante el uso de la operación de API de administración de servicio de hello [obtener Propiedades de la cuenta de almacenamiento](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Recuperar esta cuenta de almacenamiento de ubicación de Hola que están disponibles tooprocess por llamada hello `Get Location` operación.

-   Si hello `AlternateLocations` propiedad de ubicación de hello contiene la ubicación de hello propio, entonces es correcto toouse esta ubicación. De lo contrario, llame a hello `Get Location` operación de nuevo con una de las ubicaciones alternativas de Hola. ubicación original de Hello podría estar cerrado temporalmente para el mantenimiento.

## <a name="creating-hello-export-job"></a>Crear trabajo de exportación de Hola
 trabajo de exportación de hello toocreate, llamada hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación. Necesitará hello tooprovide siguiente información:

-   Un nombre para el trabajo de Hola.

-   nombre de cuenta de almacenamiento de Hola.

-   Hola nombre de ubicación, obtenido en el paso anterior de Hola de envío.

-   Un tipo de trabajo (exportar).

-   dirección de devolución de Hola que deben enviarse las unidades de hello después de que ha completado el trabajo de exportación de Hola.

-   Hola toobe de lista de blobs (o prefijos de blob) exportado.

## <a name="shipping-your-drives"></a>Envío de las unidades de disco
 A continuación, utilizar Hola herramienta de importación y exportación de Azure toodetermine Hola número de unidades que necesita toosend, en función de blobs de Hola que ha seleccionado toobe exportado y Hola tamaño de la unidad. Vea hello [referencia de herramienta de importación y exportación de Azure](storage-import-export-tool-how-to-v1.md) para obtener más información.

 Paquete Hola unidades en un único paquete y envíelas toohello dirección obtenida en hello el paso anterior. Tenga en cuenta Hola número del paquete para el paso siguiente Hola de seguimiento.

> [!NOTE]
>  Debe enviar las unidades de disco a través de un servicio de transporte admitido, que proporcionará un número de seguimiento del paquete.

## <a name="updating-hello-export-job-with-your-package-information"></a>Actualizar el trabajo de exportación de hello con la información del paquete
 Una vez que el número de seguimiento, llame a hello [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) nombre de transportista de operación tooupdated Hola y el número de trabajo de Hola de seguimiento. También puede especificar número Hola de unidades, dirección de devolución de Hola y fecha de envío de Hola.

## <a name="receiving-hello-package"></a>Recibir paquetes de saludo
 Una vez procesado el trabajo de exportación, se devolverán las unidades de disco tooyou con los datos cifrados. Puede recuperar la clave de BitLocker de Hola para cada una de las unidades de hello al Hola que realiza la llamada [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operación. A continuación, puede desbloquear unidad Hola con clave de Hola. archivo de manifiesto de unidad de Hello en cada unidad de disco contiene la lista de Hola de archivos en la unidad de hello, así como la dirección del blob original Hola para cada archivo.

## <a name="next-steps"></a>Pasos siguientes

* [Usar servicio de importación y exportación de hello API de REST](storage-import-export-using-the-rest-api.md)
