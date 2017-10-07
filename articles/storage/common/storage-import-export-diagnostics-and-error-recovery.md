---
title: "aaaDiagnostics y recuperación de errores para los trabajos de importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable el registro detallado para la importación/exportación de Microsoft Azure service trabajos."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Diagnóstico y recuperación de errores de los trabajos de Azure Import/Export
Para cada unidad de disco procesada, Hola servicio de importación y exportación de Azure crea un registro de errores en la cuenta de almacenamiento de hello asociado. También puede habilitar el registro detallado por establecer hello `LogLevel` propiedad demasiado`Verbose` al llamar a hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [actualizar propiedades del trabajo](/rest/api/storageimportexport/jobs#Jobs_Update) operaciones.

 De forma predeterminada, se escriben los registros con el nombre de contenedor de tooa `waimportexport`. Puede especificar un nombre diferente configuración hello `DiagnosticsPath` propiedad al llamar a hello `Put Job` o `Update Job Properties` las operaciones. Hello registros se almacenan como blobs en bloques con hello sigue la convención de nomenclatura: `waies/jobname_driveid_timestamp_logtype.xml`.

 Puede recuperar Hola URI de registros de Hola para un trabajo por llamada hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operación. Hola URI para el registro detallado de Hola se devuelve en hello `VerboseLogUri` propiedad para cada unidad, mientras hello URI para el registro de errores de Hola se devuelve en hello `ErrorLogUri` propiedad.

Puede usar Hola Hola tooidentify de datos después de problemas de registro.

## <a name="drive-errors"></a>Errores en la unidad

Hola siguientes elementos se clasifica como errores en la unidad:

-   Archivo de manifiesto de errores de acceso o lectura Hola

-   Claves de BitLocker incorrectas

-   Errores de escritura/lectura en la unidad

## <a name="blob-errors"></a>Errores de blobs

Hola siguientes elementos se clasifica como errores de blobs:

-   Nombres o blobs incorrectos o conflictivos

-   Archivos que faltan

-   Blob no encontrado

-   Archivos truncados (archivos de hello en el disco de hello son más pequeños que lo especificado en el manifiesto de hello)

-   Contenido de archivo dañado (para los trabajos de importación, se ha detectado una incoherencia de suma de comprobación MD5)

-   Archivos de metadatos y propiedades de blobs dañados (detectados con una incoherencia de suma de comprobación MD5)

-   Esquema incorrecto para propiedades del blob de Hola o archivos de metadatos

Puede haber casos donde algunas partes de un trabajo de importación o exportación no finaliza correctamente, mientras hello general trabajo finaliza. En este caso, puede cargar o descargar Hola falta partes de los datos de Hola a través de red, o puede crear una nueva trabajo tootransfer Hola de datos. Vea hello [referencia de herramienta de importación y exportación de Azure](storage-import-export-tool-how-to-v1.md) toolearn cómo toorepair Hola datos a través de la red.

## <a name="next-steps"></a>Pasos siguientes

* [Usar servicio de importación y exportación de hello API de REST](storage-import-export-using-the-rest-api.md)
