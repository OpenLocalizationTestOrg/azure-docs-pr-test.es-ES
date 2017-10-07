---
title: aaaOverview de base de datos de Azure para el servicio de base de datos relacional de MySQL | Documentos de Microsoft
description: "Información general de hello base de datos de Azure para el servicio de base de datos relacional de MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>¿Qué es Azure Database for MySQL? Introducción al servicio
Base de datos de Azure para MySQL es un servicio de base de datos relacional en hello basado en la nube de Microsoft [MySQL Community Edition](https://www.mysql.com/products/community/) motor de base de datos.  Azure Database for MySQL ofrece lo siguiente:

- Rendimiento predecible en varios niveles de servicio
- Escalabilidad dinámica sin tiempo de inactividad de la aplicación
- Alta disponibilidad integrada
- Protección de datos

Estas funcionalidades no requieren casi ninguna tarea de administración y todas se proporcionan sin ningún costo adicional. Le permiten toofocus en desarrollo de aplicaciones rápida y acelerar su toomarket de tiempo, en lugar de asignar un tiempo muy valioso y máquinas virtuales de toomanaging de recursos y la infraestructura. Además, puede continuar toodevelop la aplicación con hello Abrir origen herramientas y plataforma de su elección y entregar con velocidad de Hola y eficacia que exige su negocio sin tener toolearn nuevas habilidades.

![Diagrama conceptual de Azure Database for MySQL](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Este artículo es una introducción tooAzure base de datos de conceptos básicos de MySQL y características relacionadas tooperformance, escalabilidad y facilidad de uso, con detalles de tooexplore de vínculos. Consulte que estos rápida inicia tooget inició:
- [Create an Azure Database for MySQL server using Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- [Create an Azure Database for MySQL server using Azure CLI](quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)

Para ver ejemplos de la CLI de Azure, consulte:
- [Ejemplos de la CLI de Azure para Azure Database for MySQL](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Ajuste del rendimiento y escalabilidad sin tiempo de inactividad
El servicio Azure Database for MySQL actualmente ofrece dos niveles de servicio: Básico y Estándar. Cada nivel ofrece rendimiento diferentes y las cargas de trabajo de base de datos de las capacidades toosupport tooheavyweight ligera. Puede compilar su primera aplicación en una base de datos pequeño para unos cuantos dólares de un mes, a continuación, cambiar su tooscale de nivel de servicio con necesidades de la solución sin tiempo de inactividad. Escalabilidad dinámica permite su toorapidly de base de datos tootransparently responden cambiantes requerimientos de recursos. Solo paga por recursos de Hola que necesita, cuando los necesite.

## <a name="monitoring-and-alerting"></a>Supervisión y alertas
¿Cómo sabrá Hola integral haga clic cuando marque arriba y abajo? Usar la supervisión de rendimiento integrado de Hola y características, combinadas con una clasificación de rendimiento Hola basada en unidad de proceso de alertas. Uso de estas características, puede evaluar rápidamente impacto Hola de escalar verticalmente en función de su suscripción actual o se proyecta necesidades de rendimiento. Consulte [Conceptos: niveles de servicio](concepts-service-tiers.md) para más información.

## <a name="keep-your-app-and-business-running"></a>Mantenimiento de la aplicación y el negocio en funcionamiento
El Acuerdo de Nivel de Servicio (SLA) de Azure, con una disponibilidad del 99,99 % líder del sector y con la tecnología de una red global de centros de datos administrados por Microsoft, ayuda a mantener las aplicaciones en funcionamiento de forma ininterrumpida. Con cada base de datos de MySQL server, aprovechar las ventajas de seguridad integrados, tolerancia a errores y protección de datos que, en caso contrario tendría toobuy o diseño, crear y administrar. Con la base de datos de Azure para MySQL, puede utilizar restauración a un punto en el momento toorecover tooan de un servidor de estado anteriormente, anteriores hasta 35 días.

## <a name="secure-your-data"></a>Protección de los datos
Los servicios de bases de datos de Azure tienen una tradición de seguridad de datos que conserva Azure Database for MySQL con características que limitan el acceso, protegen los datos en reposo y en movimiento, y le ayudan a supervisar la actividad. Visite hello [centro de confianza de Azure](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) para obtener información acerca de la seguridad de plataforma de Azure.

Hola base de datos de Azure para servicio de MySQL usa cifrado de almacenamiento de datos en reposo. Datos incluidos en las copias de seguridad, se cifran en el disco (con excepción de Hola de archivos temporales creados por el motor de Hola durante la ejecución de consultas). servicio Hello usa cifrado de AES de 256 bits que se incluye en el cifrado de almacenamiento de Azure y las claves de hello están administrado por el sistema. El cifrado de almacenamiento siempre está activado y no se puede deshabilitar.

De forma predeterminada, Hola base de datos de Azure para servicio de MySQL es configurado toorequire [seguridad de la conexión SSL](./concepts-ssl-connection-security.md) para datos en movimiento a través de red de Hola. Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.  Si lo desea, puede deshabilitar requerir SSL para la conexión de servicio de base de datos de tooyour si la aplicación cliente no es compatible con la conectividad SSL.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha leer una base de datos de tooAzure de introducción para MySQL y respondía a Hola pregunta "¿Cuál es la base de datos de Azure para MySQL?", está listo para:
- Vea Hola página para las comparaciones de costo y calculadoras de precios. [Precios](https://azure.microsoft.com/pricing/details/mysql/)
- Comience por crear su primer servidor. [Create an Azure Database for MySQL server using Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- Compilar la primera aplicación de Python, PHP, Ruby, C\#, Java, Node.js: [bibliotecas de conectividad usan tooconnect tooAzure base de datos de MySQL](concepts-connection-libraries.md)
