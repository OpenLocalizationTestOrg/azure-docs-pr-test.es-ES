---
title: aaa "niveles de precios de base de datos de Azure para MySQL | Documentos de Microsoft"
description: Planes de tarifa de Azure Database for MySQL
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 2a05f00aff4f7166f04e035eb2a47e7662888ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Opciones y rendimiento de Azure Database for MySQL: información sobre el contenido disponible en cada plan de tarifa
Cuando se crea una base de datos de MySQL server, elija tres opciones principales recursos de hello tooconfigure asignados a dicho servidor. Estas opciones afectan al rendimiento de Hola y escala de servidor hello.
- Plan de tarifa 
- Unidades de proceso
- Almacenamiento (GB)

Cada nivel de precios tiene una duración de rendimiento toochoose de niveles (unidades de proceso), dependiendo de los requisitos de las cargas de trabajo. Niveles de rendimiento superiores proporcionan recursos adicionales para su servidor toodeliver diseñado un rendimiento mayor. Puede cambiar el nivel de rendimiento del servidor de hello dentro de un plan de tarifa prácticamente sin tiempo de inactividad de aplicación.

> [!IMPORTANT]
> Mientras está en vista previa pública del servicio de hello, no es un contrato de nivel de servicio (SLA) garantizada.

En un servidor de Azure Database for MySQL, puede tener una o varias bases de datos. Puede participar una base de datos por servidor tooutilize toocreate todos los recursos de Hola o crear tooshare de bases de datos de varios recursos de Hola. 

## <a name="choose-a-pricing-tier"></a>Elija un plan de tarifa.
Mientras se encuentre en versión preliminar, el servicio Azure Database for MySQL ofrece dos planes de tarifa: Básico y Estándar. El plan Premium no está disponible todavía, pero lo estará pronto. 

Hello tabla siguiente proporciona ejemplos de hello precios niveles recomendados adecuados para las cargas de trabajo de aplicación diferente.

| Plan de tarifa  | Carga de trabajo objetivo |
| :----------- | :----------------|
| Básica | Opción más conveniente para pequeñas cargas de trabajo que requieren almacenamiento y proceso escalables sin garantía de IOPS. Algunos ejemplos son los servidores utilizados para desarrollo o prueba, o las aplicaciones a pequeña escala que se emplean con poca frecuencia. |
| Estándar | Hola go-toooption para la nube garantizan las aplicaciones que necesitan e/s por segundo con un alto rendimiento. Como ejemplos destacan las aplicaciones web y analíticas. |
| Premium | La opción idónea para cargas de trabajo que necesiten de una baja latencia para transacciones y E/S. Proporciona mejor compatibilidad de Hola para muchos usuarios simultáneos. Toodatabases aplicable que admiten aplicaciones de misión crítica.<br />Hola Premium tarifa no está disponible en vista previa. |

toodecide sobre los precios de una capa, primer inicio mediante la determinación de si la carga de trabajo necesita una garantía de e/s por segundo. Si es así, seleccione el plan de tarifa Estándar.

| **Características del plan de tarifa** | **Básico** | **Standard** |
| :------------------------ | :-------- | :----------- |
| Unidades de proceso máximas | 100 | 800 | 
| Almacenamiento total máximo | 1 TB | 1 TB | 
| Garantía de IOPS de almacenamiento | N/D | Sí | 
| IOPS de almacenamiento máximas | N/D | 3000 | 
| Período de retención de copias de seguridad de base de datos | 7 días | 35 días | 

Durante el período de vista previa de hello, no se puede cambiar el nivel de precios una vez creado el servidor de Hola. Hola futuras, se tooupgrade posibles o degradar un servidor de una capa tooanother plan de tarifa.

## <a name="understand-hello-price"></a>Comprender el precio de Hola
Cuando se crea una nueva base de datos de Azure para MySQL dentro de hello [Portal de Azure](https://portal.azure.com/#create/Microsoft.MySQLServer), haga clic en hello **tarifa** hello costo mensual y hoja se mostrará según en Opciones de Hola que ha seleccionado. Si no tiene una suscripción de Azure, use hello tooget de calculadora de precios Azure un precio estimado. Visite hello [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) de sitio Web, a continuación, haga clic en **agregar elementos**, expanda hello **bases de datos** categoría y elija **base de datos de Azure para MySQL**  opciones de hello toocustomize.

## <a name="choose-a-performance-level-compute-units"></a>Selección de un nivel de rendimiento (unidades de proceso)
Una vez que haya determinado Hola tarifa para la base de datos de Azure para servidor MySQL, son nivel de rendimiento de hello toodetermine listo seleccionando Hola número de unidades de proceso sea necesario. Un buen punto de partida son 200 o 400 unidades de proceso para aplicaciones que necesiten más simultaneidad de usuarios para las cargas de trabajo web o analíticas. Esta cantidad se puede incrementar en función de las necesidades correspondientes. 

Proceso de unidades son una medida de rendimiento de procesamiento de CPU que se garantiza toobe disponible tooa única base de datos de MySQL server. Una unidad de proceso es una medida combinada de recursos de CPU y memoria.  Para más información, consulte [Explicación de las unidades de proceso](concepts-compute-unit-and-storage.md).

### <a name="basic-pricing-tier-performance-levels"></a>Niveles de rendimiento del plan de tarifa Básico:

| **Nivel de rendimiento** | **50** | **100** |
| :-------------------- | :----- | :------ |
| Unidades de proceso máximas | 50 | 100 |
| Tamaño de almacenamiento incluido | 50 GB | 50 GB |
| Tamaño máximo de almacenamiento en servidor\* | 1 TB | 1 TB |

### <a name="standard-pricing-tier-performance-levels"></a>Niveles de rendimiento del plan de tarifa Estándar:

| **Nivel de rendimiento** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| Unidades de proceso máximas | 100 | 200 | 400 | 800 |
| IOPS aprovisionadas y tamaño de almacenamiento incluidos | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS | 125 GB<br/> 375 IOPS |
| Tamaño máximo de almacenamiento en servidor\* | 1 TB | 1 TB | 1 TB | 1 TB |
| IOPS máximas aprovisionadas en servidor | 3000 IOPS | 3000 IOPS | 3000 IOPS | 3000 IOPS |
| IOPS máximas aprovisionadas en servidor por GB | 3 IOPS fijas por GB | 3 IOPS fijas por GB | 3 IOPS fijas por GB | 3 IOPS fijas por GB |

\*Tamaño máximo de almacenamiento de servidor hace referencia toohello tamaño de almacenamiento aprovisionado máximo para el servidor.

## <a name="storage"></a>Storage 
configuración de almacenamiento de Hello define la cantidad de Hola de almacenamiento capacidad disponible tooan base de datos de MySQL server. almacenamiento de Hello utilizado por el servicio de hello incluye archivos de base de datos de hello, registros de transacciones y registros de hello MySQL server. Considere la posibilidad de tamaño de Hola de almacenamiento necesario toohost las bases de datos y Hola requisitos de rendimiento (IOPS) al seleccionar la configuración de almacenamiento de Hola.

Cierta capacidad de almacenamiento se incluye como mínimo en cada nivel de precios, que se indica en hello anterior de la tabla como "Tamaño de almacenamiento incluidos". Capacidad de almacenamiento adicionales puede agregarse cuando se crea el servidor de hello, en incrementos de 125 GB, el almacenamiento máximo permitido de toohello. capacidad de almacenamiento adicional de Hello puede configurarse independientemente de la configuración de unidades de proceso de Hola. cambios de precio de Hello en función de la cantidad de Hola de almacenamiento seleccionada.

configuración de IOPS de Hello en cada nivel de rendimiento está relacionado con toohello plan de tarifa y tamaño de almacenamiento de hello elegido. El plan Básico no garantiza ningún valor de E/S por segundo. En el nivel de precios estándar de hello, Hola IOPS proporcionalmente toomaximum el tamaño de almacenamiento en una proporción de 3:1 fija. almacenamiento Hola incluido de garantías de 125 GB para 375 aprovisiona IOPS, cada uno con un tamaño de E/S de too256 KB. Puede elegir un almacenamiento de información adicional hasta too1 TB como máximo, tooguarantee 3.000 aprovisionado e/s por segundo.

Gráfico de métricas de monitor Hola Hola Azure portal o escritura CLI de Azure comandos toomeasure Hola consumo de almacenamiento e IOPS. Toomonitor de métricas pertinente son el límite de almacenamiento, el porcentaje de almacenamiento, almacenamiento utilizado y porcentaje de E/S.

>[!IMPORTANT]
> Mientras esté en la vista previa, elija cantidad Hola de almacenamiento en el momento de hello cuando se crea el servidor de Hola. Cambiar el tamaño de almacenamiento de hello en un servidor existente no se admite todavía. 

## <a name="scaling-a-server-up-or-down"></a>Escalado o reducción verticales de un servidor
Inicialmente, elegir Hola precios nivel y el rendimiento cuando se crea la base de datos de Azure para MySQL. Más adelante, puede escalar Hola unidades calcular una copia de seguridad o dinámicamente, abajo dentro del alcance de Hola de Hola mismo nivel de precios. Hola portal de Azure, deslice Hola proceso unidades en la hoja de nivel de precios del servidor de Hola o escribirlo siguiendo este ejemplo: [Monitor y escala de una base de datos de Azure para servidor de MySQL con CLI de Azure](scripts/sample-scale-server.md)

Ajuste de escala en unidades de Hola de proceso se realiza independientemente de tamaño de almacenamiento máximo de hello que ha elegido.

Entre bastidores de hello, cambiar el nivel de rendimiento de Hola de una base de datos crea una réplica de base de datos original de hello en el nuevo nivel de rendimiento de hello y, a continuación, cambia las conexiones toohello réplica. Durante este proceso no se pierde ningún dato. Durante Hola breve momento cuando se cambie a través de la réplica de toohello, base de datos de las conexiones toohello están deshabilitados, por lo que se pueden revertir algunas transacciones en tránsito. Este intervalo varía, pero de media dura menos de 4 segundos, y en más del 99 % de los casos es inferior a 30 segundos. Si hay grandes números de transacciones en tránsito en conexiones de momento Hola están deshabilitados, esta ventana puede ser superior.

duración de Hello del proceso de escala todo Hola depende de tamaño de Hola y nivel de precios de servidor hello antes y después de cambiar Hola. Por ejemplo, un servidor que está cambiando unidades de proceso en el nivel de precios estándar de hello, debe completar en pocos minutos. Hola nuevas propiedades de servidor hello no se aplican hasta que se completen los cambios de Hola.

## <a name="next-steps"></a>Pasos siguientes
- Para más información sobre las unidades de proceso, consulte [Explicación de las unidades de proceso](concepts-compute-unit-and-storage.md).
- Obtenga información acerca de cómo demasiado[Monitor y escala de una base de datos de Azure para servidor de MySQL con CLI de Azure](scripts/sample-scale-server.md)
