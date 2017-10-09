---
title: aaaOverview de base de datos de Azure para el servicio de base de datos relacional de PostgreSQL | Documentos de Microsoft
description: "Proporciona información general sobre el servicio de base de datos relacional de Azure Database for MySQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>¿Qué es Azure Database for PostgreSQL?

Base de datos de Azure para PostgreSQL es un servicio de base de datos relacional en hello integrada para los desarrolladores que se basa en la versión de la Comunidad de Hola de código abierto de nube de Microsoft [PostgreSQL](https://www.postgresql.org/) motor de base de datos. Este servicio está en versión preliminar pública. Azure Database for PostgreSQL ofrece:
- Rendimiento predecible en varios niveles de servicio
- Escalabilidad dinámica sin tiempo de inactividad de la aplicación
- Alta disponibilidad integrada
- Protección de datos

Todas estas funcionalidades apenas requieren tareas de administración y todas se proporcionan sin costo adicional. Estas capacidades permiten toofocus en desarrollo rápido de aplicaciones y acelerar la toomarket de tiempo, en lugar de asignar un tiempo muy valioso y máquinas virtuales de toomanaging de recursos y la infraestructura. Además, puede continuar toodevelop la aplicación con hello Abrir origen herramientas y plataforma de su elección y entregar con velocidad de Hola y eficacia que exige su negocio sin tener toolearn nuevas habilidades. 

Este artículo es una introducción tooAzure base de datos de PostgreSQL principales conceptos y características relacionadas tooperformance, escalabilidad y facilidad de uso. Consulte que estos rápida inicia tooget inició:

- [Create an Azure Database for PostgreSQL using Azure portal](quickstart-create-server-database-portal.md) (Creación de una base de datos Azure Database for PostgreSQL con Azure Portal)
- [Crear una base de datos de Azure para PostgreSQL mediante Hola CLI de Azure](quickstart-create-server-database-azure-cli.md)

Para obtener ejemplos de la CLI de Azure y de PowerShell, consulte:

- [Azure CLI samples for Azure Database for PostgreSQL](./sample-scripts-azure-cli.md) (Ejemplos de la CLI de Azure para Azure Database for PostgreSQL)

## <a name="adjust-performance-and-scale-without-downtime"></a>Ajuste del rendimiento y escalabilidad sin tiempo de inactividad

El servicio Azure Database for PostgreSQL actualmente ofrece dos niveles de servicio: Básico y Estándar. Cada nivel de servicio ofrece [distintos niveles de rendimiento, las garantías de e/s por segundo y funcionalidades](concepts-service-tiers.md) las cargas de trabajo de base de datos de toosupport tooheavyweight ligera. Puede crear su primera aplicación en un servidor pequeño para unos reembolsos de un mes y, a continuación, [Cambiar nivel de rendimiento de hello](scripts/sample-scale-server-up-or-down.md) dentro de servicio de nivel manualmente o mediante programación a cualquier necesidad de hello toomeet de tiempo de la solución. Puede hacerlo sin aplicación tooyour de tiempo de inactividad o a los clientes de tooyour. Habilita la escalabilidad dinámica su base de datos tootransparently responder toorapidly cambiar los requisitos de recursos y habilita tooonly se paga por los recursos de Hola que necesite cuando los necesite.

## <a name="monitoring-and-alerting"></a>Supervisión y alertas
¿Cómo se decide cuándo toodial arriba y abajo? Supervisión de rendimiento integrado de Hola y características, combinadas con una clasificación de rendimiento Hola basándose en las unidades de proceso de alertas se utilizan. Con estas herramientas, puede evaluar rápidamente el impacto de Hola de escalado de proceso unidades o hacia abajo según sus necesidades de rendimiento actual o se proyecta. Para más información, consulte [Opciones y rendimiento de Azure Database for PostgreSQL: información sobre lo que está disponible en cada nivel de servicio](./concepts-service-tiers.md).

## <a name="keep-your-app-and-business-running"></a>Mantenimiento de la aplicación y el negocio en funcionamiento
El Acuerdo de Nivel de Servicio (SLA) de Azure, con una disponibilidad del 99,99 % líder del sector (no disponible en la versión preliminar) y con la tecnología de una red global de centros de datos administrados por Microsoft, ayuda a mantener las aplicaciones en funcionamiento de forma ininterrumpida. Con cada base de datos de Azure para servidor PostgreSQL, aprovechar las ventajas de seguridad integrados, tolerancia a errores y protección de datos que, en caso contrario tendría toobuy o diseño, crear y administrar. Con la base de datos de Azure para PostgreSQL, cada nivel de servicio ofrece un conjunto completo de características de continuidad de negocio y opciones que se pueden emplear tooget y ejecución y permanezca de este modo. Puede usar [restauración a un punto en el momento](howto-restore-server-portal.md) tooreturn tooan de una base de datos de estado anteriormente, anteriores hasta 35 días. Además, si hospeda las bases de datos de centros de datos de hello experimenta una interrupción inesperada, puede restaurar las bases de datos desde copias con redundancia geográfica de copias de seguridad recientes.

## <a name="secure-your-data"></a>Protección de los datos
Los servicios de bases de datos de Azure tienen una tradición de seguridad de datos que conserva Azure Database for PostgreSQL con características que limitan el acceso, protegen los datos en reposo y en movimiento, y le ayudan a supervisar la actividad. Visite hello [centro de confianza de Azure](https://www.microsoft.com/TrustCenter/Security/default.aspx) para obtener información acerca de la seguridad de plataforma de Azure.

Hola base de datos de Azure para servicio PostgreSQL usa cifrado de almacenamiento de datos en reposo. Incluidas las copias de seguridad de datos se cifran en el disco (con excepción de Hola de archivos temporales creados por el motor de Hola durante la ejecución de consultas). servicio Hello usa cifrado de AES de 256 bits que se incluye en el cifrado de almacenamiento de Azure y las claves de hello están administrado por el sistema. El cifrado de almacenamiento siempre está activado y no se puede deshabilitar.

De forma predeterminada, Hola base de datos de Azure para servicio PostgreSQL es configurado toorequire [seguridad de la conexión SSL](./concepts-ssl-connection-security.md) para datos en movimiento a través de red de Hola. Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.  Si lo desea, puede deshabilitar requerir SSL para la conexión de servicio de base de datos de tooyour si la aplicación cliente no es compatible con la conectividad SSL.

## <a name="next-steps"></a>Pasos siguientes
- Vea hello [página de precios](https://azure.microsoft.com/pricing/details/postgresql/) para las comparaciones de costo y calculadoras.
- Comience por [crear su primera base de datos de Azure Database for PostgreSQL](./quickstart-create-server-database-portal.md).
- Compile la primera aplicación de Python, PHP, Ruby, C\#, Java, Node.js: [Bibliotecas de conexiones](./concepts-connection-libraries.md)
