---
title: "migración entre regiones de almacén de Data Lake aaaAzure | Documentos de Microsoft"
description: "Más información sobre la migración entre regiones para Azure Data Lake Store."
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>Migración de Data Lake Store entre regiones

Como almacén de Azure Data Lake está disponible en las regiones de nuevo, puede elegir toodo una migración en un solo uso, tootake aprovechar la nueva región de Hola. Obtenga información acerca de qué tooconsider mientras planea y completar la migración de Hola.

## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción de Azure**. Para más información, consulte [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Data Lake Store en dos regiones diferentes**. Para más información, consulte [Introducción a Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Azure Data Factory**. Para obtener más información, consulte [tooAzure Introducción factoría de datos](../data-factory/data-factory-introduction.md).


## <a name="migration-considerations"></a>Consideraciones sobre la migración

En primer lugar, identifique la estrategia de migración de Hola que se adapte mejor a la aplicación que escribe, lee y procesa los datos en el almacén de Data Lake. Cuando se elige una estrategia, considere la posibilidad de requisitos de disponibilidad de su aplicación y el tiempo de inactividad de Hola que se produce durante una migración. Por ejemplo, el enfoque más sencillo podría ser el modelo de migración de toouse Hola "elevación y Mayús" en la nube. En este enfoque, pausar aplicación hello en su región existente mientras copian todos los datos son toohello nueva región. Cuando finaliza el proceso de copia de hello, reanude la aplicación en la nueva región de Hola y, a continuación, eliminar cuenta de almacén de Data Lake anterior Hola. Tiempo de inactividad durante la migración de hello es necesario.

tiempo de inactividad de tooreduce, inmediatamente puede empezar introducir nuevos datos en la nueva región de Hola. Cuando haya datos mínima Hola necesarios, ejecute la aplicación en la nueva región de Hola. En segundo plano de hello, continuar toocopy los datos más antiguos de hello almacén de Data Lake cuenta toohello nuevo almacén de Data Lake cuenta existente en la nueva región de Hola. Con este enfoque, puede realizar las nueva área de toohello del conmutador de hello con poco tiempo de inactividad. Cuando se ha copiado todos los datos más antiguos de hello, eliminar cuenta de almacén de Data Lake anterior Hola.

Otro tooconsider detalles importantes al planear la migración son:

* **Volumen de datos**. volumen Hola de datos (en gigabytes, número de Hola de archivos y carpetas y así sucesivamente) afecta al tiempo de Hola y recursos que necesita para la migración de Hola.

* **Nombre de la cuenta de Data Lake Store**. nuevo nombre de cuenta Hello en la nueva región de hello debe ser único globalmente. Por ejemplo, nombre de hello de la antigua cuenta de almacén de Data Lake zona horaria del Pacífico oriental 2 podría ser contosoeastus2.azuredatalakestore.net. Podría denominar a la nueva cuenta de Data Lake Store en Norte UE contosonortheu.azuredatalakestore.net.

* **Herramientas**. Le recomendamos que use hello [actividad de copia de factoría de datos de Azure](../data-factory/data-factory-azure-datalake-connector.md) toocopy archivos de almacén de Data Lake. Data Factory admite el movimiento de datos con alto rendimiento y confiabilidad. Tenga en cuenta que la factoría de datos copia solo jerarquía de carpetas de Hola y el contenido de archivos de Hola. Necesita toomanually aplicar las listas de control de acceso (ACL) que se utilizan en hello antiguo toohello nueva cuenta. Para obtener más información, incluidos los objetivos de rendimiento de escenarios mejores, vea hello [actividad de copia Guía de rendimiento y optimización](../data-factory/data-factory-copy-activity-performance.md). Si desea que los datos copiados más rápidamente, puede que tenga toouse unidades adicionales de movimiento de datos de nube. Otras herramientas, como AdlCopy, no admiten la copia de datos entre regiones.  

* **Cobros por ancho de banda**. [Los cobros por ancho de banda](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) se aplican porque los datos se transfieren fuera de una región de Azure.

* **ACL de los datos**. Proteger los datos en la nueva región de hello aplicando las carpetas y toofiles de ACL. Para más información, consulte [Protección de los datos almacenados en Azure Data Lake Store](data-lake-store-secure-data.md). Se recomienda que utilice tooupdate de migración de Hola y ajustar la ACL. Puede ser conveniente toouse configuración tooyour actual una configuración similar. Puede ver las ACL de Hola que están aplicados tooany archivo mediante Hola portal de Azure, [cmdlets de PowerShell](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission), o SDK.  

* **Ubicación de los servicios de análisis**. Para obtener el mejor rendimiento, los servicios de análisis, como análisis de Azure Data Lake o HDInsight de Azure, deben estar en hello misma región que los datos.  

## <a name="next-steps"></a>Pasos siguientes
* [Información general del Almacén de Azure Data Lake](data-lake-store-overview.md)
