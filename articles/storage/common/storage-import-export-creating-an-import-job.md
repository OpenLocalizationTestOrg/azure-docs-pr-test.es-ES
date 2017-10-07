---
title: "aaaCreate un trabajo de importación para la importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una importación para hello servicio de importación y exportación de Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Crear un trabajo de importación para hello servicio de importación y exportación de Azure

La creación de un trabajo de importación para servicio de importación y exportación de Microsoft Azure de hello mediante API de REST de hello implica Hola pasos:

-   Preparar las unidades con hello herramienta de importación y exportación de Azure.

-   Obtención Hola ubicación toowhich tooship Hola unidad.

-   Creando un trabajo de importación Hola.

-   Envío Hola unidades tooMicrosoft a través de un servicio de transporte admitido.

-   Actualizar el trabajo de importación de hello con hello detalles de envío.

 Vea [con hello importación y exportación de Microsoft Azure service tooTransfer datos tooBlob almacenamiento](storage-import-export-service.md) para obtener información general del servicio de importación y exportación de Hola y un tutorial que demuestra cómo hello toouse [portal de Azure](https://portal.azure.com/) toocreate y administrar la importación y exportación de trabajos.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Preparar las unidades con hello herramienta de importación y exportación de Azure

Hola pasos tooprepare unidades para un trabajo de importación se Hola mismo si crea Hola jobvia portal de Hola o a través de Hola API de REST.

A continuación se muestra una breve descripción general de cómo preparar la unidad. Consulte toohello [referencia ExportTool de importación de Azure](storage-import-export-tool-how-to-v1.md) para obtener instrucciones completas. Puede descargar la herramienta de importación y exportación de Azure de hello [aquí](http://go.microsoft.com/fwlink/?LinkID=301900).

La preparación de la unidad conlleva:

-   Identificación toobe Hola de datos importado.

-   Identificar blobs de destino de hello en almacenamiento de Windows Azure.

-   Uso de hello toocopy de herramienta de importación y exportación de Azure su tooone de datos o más unidades de disco duro.

 Hola, herramienta de importación y exportación de Azure también generará un archivo de manifiesto para cada una de las unidades de hello mientras las prepara. Un archivo de manifiesto contiene:

-   Una enumeración de todos los archivos de hello diseñada para la carga y las asignaciones de Hola de estos tooblobs de archivos.

-   Sumas de comprobación de los segmentos de Hola de cada archivo.

-   Información sobre tooassociate de metadatos y propiedades de Hola a cada blob.

-   Un listado de hello acción tootake si un blob que se está cargando tiene Hola mismo nombre como un blob existente en el contenedor de Hola. Las opciones posibles son: a) Hola blob se sobrescribe con el archivo hello, b) tenga blob existente de Hola y omite la carga de archivo hello, c) se anexa un nombre de sufijo toohello para que no esté en conflicto con otros archivos.

## <a name="obtaining-your-shipping-location"></a>Obtención de la ubicación de envío

Antes de crear un trabajo de importación, deberá tooobtain un nombre de la ubicación de envío y la dirección por llamada hello [ubicaciones de la lista](/rest/api/storageimportexport/listlocations) operación. `List Locations` devolverá una lista de ubicaciones y sus direcciones de correo. Puede seleccionar una ubicación de hello devuelve la lista y enviar su dirección de toothat de unidades de disco duro. También puede usar hello `Get Location` Hola de tooobtain operación directamente de la dirección de una ubicación específica de envío.

 Siga los pasos de Hola por debajo de la ubicación de envío de Hola tooobtain:

-   Identificar el nombre de Hola de ubicación de saludo de la cuenta de almacenamiento. Este valor puede encontrarse en hello **ubicación** campo de la cuenta de almacenamiento de hello **panel** en hello Azure portal o puede consultarse mediante el uso de la operación de API de administración de servicio de hello [obtener almacenamiento Propiedades de la cuenta](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Recuperar ubicación hello tooprocess disponible esta cuenta de almacenamiento que realiza la llamada hello `Get Location` operación.

-   Si hello `AlternateLocations` propiedad de ubicación de hello contiene la ubicación de hello propio, entonces es correcto toouse esta ubicación. De lo contrario, llame a hello `Get Location` operación de nuevo con una de las ubicaciones alternativas de Hola. ubicación original de Hello podría estar cerrado temporalmente para el mantenimiento.

## <a name="creating-hello-import-job"></a>Crear trabajo de importación de Hola
trabajo de importación de hello toocreate, llamada hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operación. Necesitará hello tooprovide siguiente información:

-   Un nombre para el trabajo de Hola.

-   nombre de cuenta de almacenamiento de Hola.

-   Hola nombre de ubicación, obtenida en el paso anterior de Hola de envío.

-   Un tipo de trabajo (importar).

-   dirección de devolución de Hola que deben enviarse las unidades de hello después de que ha completado el trabajo de importación de Hola.

-   lista de Hola de unidades de trabajo de Hola. Para cada unidad, debe incluir Hola siguiendo la información que se obtuvo durante el paso de preparación de unidad de hello:

    -   Id. de unidad de Hola

    -   clave de BitLocker de Hola

    -   Hola archivo de manifiesto ruta de acceso relativa en la unidad de disco duro de Hola

    -   archivo de manifiesto algoritmo hash MD5 codificado en Hello Base16

## <a name="shipping-your-drives"></a>Envío de las unidades de disco
Debes enviar su dirección de toohello de unidades que obtuvo en el paso anterior de Hola y debe proporcionar Hola servicio de importación y exportación con hello seguimiento número de paquetes de saludo.

> [!NOTE]
>  Debe enviar las unidades de disco a través de un servicio de transporte admitido, que proporcionará un número de seguimiento del paquete.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Actualizar el trabajo de importación de hello con la información de envío
Una vez que el número de seguimiento, llame a hello [actualizar propiedades del trabajo](/api/storageimportexport/jobs#Jobs_Update) hello tooupdate de operación de envío nombre del operador, número de seguimiento de hello para el trabajo de Hola y número de cuenta del transportista hello para el trasvase de valor devuelto. Opcionalmente, puede especificar número de Hola de hello también la fecha de envío y las unidades.

## <a name="next-steps"></a>Pasos siguientes

* [Usar servicio de importación y exportación de hello API de REST](storage-import-export-using-the-rest-api.md)
