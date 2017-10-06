---
title: "aaaFrequently almacén de Azure Data Lake preguntas más frecuentes | Documentos de Microsoft"
description: "Instrucciones sobre la solución de problemas o sobre como mitigarlos con Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Preguntas más frecuentes sobre Azure Data Lake Store
En este artículo aprenderá acerca de preguntas más frecuentes relacionada tooAzure almacén de Data Lake.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>¿Cómo puedo proteger mejor mis datos contra los desastres de toda la región o eliminaciones accidentales?
datos de Hello en su cuenta de almacén de Azure Data Lake están resistente tootransient los errores de hardware dentro de una región a través de las réplicas automatizadas. Esto garantiza la durabilidad y alta disponibilidad, Hola reunión SLA de almacén de datos Lake de Azure. Aquí tiene algunas instrucciones sobre cómo toofurther proteger los datos de eliminaciones accidentales o poco frecuentes interrupciones de toda la región.

### <a name="disaster-recovery-guidance"></a>Guía de recuperación ante desastres
Es fundamental para cada cliente tooprepare su propio plan de recuperación ante desastres. Consulte toohello documentación de Azure a continuación toobuild el plan de recuperación ante desastres. Aquí tiene algunos recursos que pueden ayudarle a crear su propio plan.

* [Recuperación ante desastres y alta disponibilidad para aplicaciones de Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Guía técnica sobre resistencia en Azure](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>Prácticas recomendadas
Se recomienda que copie su cuenta de almacén de Data Lake tooanother de los datos críticos en otra región con una frecuencia alineado toohello las necesidades de su plan de recuperación ante desastres. Hay una variedad de métodos toocopy datos incluidos [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) o [Data Factory de Azure](../data-factory/data-factory-azure-datalake-connector.md). Azure Data Factory es un servicio útil para crear e implementar las canalizaciones de movimiento de datos de forma periódica.

Si se produce una interrupción regional, a continuación, puede tener acceso a los datos en la región de Hola donde se ha copiado los datos de Hola. Puede supervisar hello [panel de estado del servicio de Azure](https://azure.microsoft.com/status/) toodetermine Hola estado del servicio de Azure en todo el mundo de Hola.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>Guía para la recuperación ante un problema de datos dañados o eliminación accidental
Tenga en cuenta que aunque Azure Data Lake Store ofrece resistencia de datos mediante réplicas automatizadas, esto no evita que su aplicación (o los desarrolladores o usuarios) puedan dañar o eliminar de forma no intencionada los datos.

#### <a name="best-practices"></a>Prácticas recomendadas
tooprevent la eliminación accidental, se recomienda que primero establecer directivas de acceso correcta de Hola para su cuenta de almacén de Data Lake.  Esto incluye la aplicación de [bloqueos de recursos de Azure](../azure-resource-manager/resource-group-lock-resources.md) toolock hacia abajo recursos importantes, así como aplicar control de acceso de nivel de cuenta y el archivo mediante Hola disponible [características de seguridad del almacén de Data Lake](data-lake-store-security-overview.md). También se recomienda que establezca una rutina de creación de copias de los datos críticos mediante [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) o [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) en otra cuenta de Data Lake Store, otra carpeta o suscripción de Azure.  Esto puede ser usado toorecover desde un incidente de daños o eliminación de datos. Azure Data Factory es un servicio útil para crear e implementar las canalizaciones de movimiento de datos de forma periódica.

También pueden habilitar las organizaciones [registro de diagnóstico](data-lake-store-diagnostic-logs.md) para su almacén de Azure Data Lake cuenta toocollect los seguimientos de auditoría de acceso a datos que proporciona información sobre quién podría eliminar o actualizar un archivo.

## <a name="next-steps"></a>Pasos siguientes
* [Introducción Azure Data Lake Store](data-lake-store-get-started-portal.md)
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)

