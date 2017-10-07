---
title: "aaaAdd tolerancia a errores en la actividad de copia de factoría de datos de Azure omitiendo filas incompatibles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd tolerancia a errores en la actividad de copia de factoría de datos de Azure omitiendo filas incompatibles durante la copia"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Incorporación de tolerancia a errores en la actividad de copia a través de la omisión de filas incompatibles

Factoría de datos de Azure [actividad de copia](data-factory-data-movement-activities.md) ofrece filas de dos maneras toohandle incompatible cuando se copian datos entre almacenes de datos de origen y el receptor:

- Puede anular y producirá un error de copia de hello actividad una vez datos incompatibles detectó (comportamiento predeterminado).
- Puede seguir toocopy todos los datos de hello agregando tolerancia a errores y omitir filas de datos incompatibles. Además, puede registrar filas incompatible hello en el almacenamiento de blobs de Azure. A continuación, puede examinar Hola registro toolearn Hola causa el error de hello, corregir datos hello en el origen de datos de hello y vuelva a intentar la actividad de copia de hello.

## <a name="supported-scenarios"></a>Escenarios admitidos
La actividad de copia admite tres escenarios para detectar, omitir y registrar datos incompatibles:

- **Incompatibilidad entre el tipo de datos de origen de Hola y el tipo nativo de hello receptor**

    Por ejemplo: copiar datos desde un archivo CSV en almacenamiento de Blob tooa SQL de base de datos con una definición de esquema que contiene tres **INT** columnas de tipo. Hola filas de los archivos CSV que contienen datos numéricos, como `123,456,789` se copian correctamente toohello almacén de receptor. Sin embargo, Hola filas que contienen valores no numéricos, como `123,456,abc` se detectan como incompatibles y se omiten.

- **El número de columnas entre el origen de Hola y el receptor de Hola Hola no coinciden**

    Por ejemplo: copiar datos desde un archivo CSV en almacenamiento de Blob tooa SQL de base de datos con una definición de esquema que contiene seis columnas. Hello archivo CSV que contiene seis columnas es copió correctamente toohello almacén de receptor. Hola CSV filas de los archivos que contengan más o menos de seis columnas se detectan como incompatible y se omiten.

- **Infracción de clave principal al escribir la base de datos relacional tooa**

    Por ejemplo: copiar los datos de una base de datos SQL de SQL server tooa. Una clave principal se define en la base de datos SQL de receptor de hello, pero dicha clave principal no se define en SQL server de origen de Hola. filas Hola duplicado que existen en el origen de hello no pueden ser copiado toohello receptor. Actividad de copia copia solo Hola primera fila de datos de origen de hello en receptor Hola. Hello fuente posterior las filas que contienen el valor de clave principal de hello duplicado se detectan como incompatible y se omiten.

## <a name="configuration"></a>Configuración
Hello en el ejemplo siguiente se proporciona un tooconfigure de definición de JSON omitir Hola filas incompatible en la actividad de copia:

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Propiedad | Descripción | Valores permitidos | Obligatorio |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Habilite si lo desea la omisión de filas incompatibles durante la copia. | True<br/>False (valor predeterminado) | No |
| **redirectIncompatibleRowSettings** | Un grupo de propiedades que se pueden especifica cuando desee filas incompatibles de toolog Hola. | &nbsp; | No |
| **linkedServiceName** | Hola vinculado servicio de registro de hello toostore de almacenamiento de Azure que contiene filas de hello omitido. | nombre de Hola de un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) servicio, que hace referencia la instancia de almacenamiento de toohello que desea que el archivo de registro de hello toouse toostore vinculado. | No |
| **path** | ruta de acceso de Hola Hola del archivo de registro que contiene Hola omite filas. | Especifique la ruta de almacenamiento de blobs de Hola que desea toouse toolog Hola incompatibles de los datos. Si no se proporciona una ruta de acceso, el servicio de Hola crea un contenedor para usted. | No |

## <a name="monitoring"></a>Supervisión
Una vez finalizada la ejecución de actividad de copia de hello, puede ver Hola número de filas omitidas en la sección supervisión de hello:

![Supervisión de filas incompatibles omitidas](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Si configura filas incompatibles de toolog hello, puede encontrar el archivo de registro de hello en esta ruta de acceso: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` en archivo de registro de hello, puede ver las filas de hello omitidos y Hola a causa de incompatibilidad de Hola.

Los datos originales de Hola y de error correspondiente Hola se registran en el archivo hello. Un ejemplo de contenido del archivo de registro de hello es como sigue:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la actividad de copia de factoría de datos de Azure, consulte [mover datos mediante la actividad de copia](data-factory-data-movement-activities.md).
