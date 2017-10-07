---
title: 'Cifrado de bases de datos en reposo: Azure Cosmos DB | Microsoft Docs'
description: "Obtenga información sobre cómo Azure Cosmos DB proporciona cifrado predeterminado de todos los datos."
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>Cifrado de base de datos en reposo en Azure Cosmos DB

El cifrado en reposo es una frase que se refiere normalmente a toohello cifrado de datos en los dispositivos de almacenamiento no volátil como unidades de estado sólido (SSD) y unidades de disco duro (HDD). Cosmos DB almacena sus bases de datos principales en unidades SSD. Sus elementos multimedia adjuntos y las copias de seguridad se almacenan en Azure Blob Storage, cuyos archivos de copia de seguridad suelen encontrarse en unidades HDD. Con la versión de Hola de cifrado en reposo para Cosmos DB, se cifran todas las bases de datos, datos adjuntos de multimedia y las copias de seguridad. Ahora se cifran los datos en tránsito (a través de la red Hola) y en reposo (almacenamiento no volátil), lo que le ofrece cifrado de extremo a extremo.

Como un servicio de PaaS, Cosmos DB es muy fácil toouse. Dado que todos los datos de usuario almacenados en la base de datos de Cosmos se cifran en reposo y en transporte, no es necesario tootake ninguna acción. Tooput de otra manera es que el cifrado en rest es "on" de forma predeterminada. No hay ningún tooturn controles, o desactivar. Proporcionamos esta característica mientras continuamos toomeet nuestro [SLA de disponibilidad y rendimiento](https://azure.microsoft.com/support/legal/sla/cosmos-db).

## <a name="implement-encryption-at-rest"></a>Implementación de cifrado en reposo

El cifrado en reposo se implementa mediante una serie de tecnologías de seguridad, como sistemas seguros de almacenamiento de claves, redes cifradas y API criptográficas. Los sistemas que descifrar y procesan los datos tienen toocommunicate con sistemas que administrar las claves. diagrama de Hello muestra cómo se separa el almacenamiento de administración de hello y los datos cifrados de claves. 

![Diagrama de diseño](./media/database-encryption-at-rest/design-diagram.png)

Hola flujo básico de una solicitud de usuario es como sigue:
- cuenta de base de datos de usuario de Hello estará listo y recuperaron las claves de almacenamiento a través de un proveedor de recursos del servicio de administración de toohello de solicitud.
- Un usuario crea una base de datos de tooCosmos de conexión a través de transporte HTTPS/secure. (detalles de hello abstracta de hello SDK).
- usuario de Hello envía una toobe de documento JSON almacenado a lo largo Hola conexión segura creada anteriormente.
- documento JSON de Hola se indiza a menos que el usuario de hello ha desactivado la indización.
- Hola documento JSON y datos del índice se escriben toosecure almacenamiento.
- Periódicamente, datos lee desde un almacenamiento seguro hello y copia de seguridad toohello el almacén de blobs de Azure cifrada.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>P: ¿Cuánto aumenta el costo de Azure Storage si se habilita el cifrado del servicio Storage?
R: No hay costo adicional.

### <a name="q-who-manages-hello-encryption-keys"></a>P: ¿a quién administra las claves de cifrado de hello?
R: Microsoft administra las claves de Hola.

### <a name="q-how-often-are-encryption-keys-rotated"></a>P: ¿Con qué frecuencia se alternan las claves de cifrado?
R: Microsoft cuenta con un conjunto de directrices internas para la rotación de claves de cifrado y Cosmos DB las sigue. no se publican instrucciones específicas de Hola. Microsoft publica hello [del ciclo de vida de desarrollo de seguridad (SDL)](https://www.microsoft.com/sdl/default.aspx), que se ve como un subconjunto de instrucciones internas y tiene útiles prácticas recomendadas para los desarrolladores.

### <a name="q-can-i-use-my-own-encryption-keys"></a>P: ¿Puedo usar mis propias claves de cifrado?
R: cosmos DB es un servicio de PaaS y trabajamos duro tookeep Hola servicio fácil toouse. Se ha observado que esta pregunta suele plantearse en relación con proxys y con la satisfacción de algún requisito de conformidad, como PCI DSS. Como parte de la creación de esta característica, hemos trabajado con cumplimiento auditores tooensure que los clientes que utilizan DB Cosmos cumplan sus requisitos sin Hola necesidad toomanage propias claves.
Como resultado, que actualmente no ofrecemos usuarios Hola opción tooburden por sí mismos con administración de claves.

### <a name="q-what-regions-have-encryption-turned-on"></a>P: ¿Qué regiones tienen activado el cifrado?
R: Todas las regiones de Azure Cosmos DB tienen activado el cifrado de todos los datos de usuario.

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>P: ¿cifrado afectan a la latencia de rendimiento de Hola y el rendimiento SLA?
R: no hay ningún impacto o cambios toohello de rendimiento SLA ahora que está habilitado el cifrado en reposo para todas las cuentas nuevas y existentes. Puede leer más en hello [SLA de Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db) página garantías más recientes de toosee Hola.

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>P: ¿emulador local de hello admite el cifrado en reposo?
R: emulador de hello es una herramienta de desarrollo/pruebas independiente y no utiliza servicios de administración de claves de Hola que Hola administrado Cosmos DB servicio utiliza. Nuestra recomendación es tooenable BitLocker en unidades de disco donde se almacenan los datos de prueba de emulador confidenciales. Hola [emulador admite cambiar directorio de datos predeterminado de hello](local-emulator.md) equivalente a una ubicación conocida.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información general de seguridad de base de datos de Cosmos y mejoras más recientes de hello, consulte [seguridad de base de datos de la base de datos de Azure Cosmos](database-security.md).
Para obtener más información acerca de las certificaciones de Microsoft, vea hello [centro de confianza de Azure](https://azure.microsoft.com/en-us/support/trust-center/).
