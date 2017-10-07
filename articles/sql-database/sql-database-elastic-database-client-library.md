---
title: las bases de datos en la nube escalables de aaaBuilding | Documentos de Microsoft
description: "Compilar aplicaciones de base de datos escalables de .NET con la biblioteca de cliente de base de datos elástica Hola"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>Creación de bases de datos escalables en la nube
El escalado horizontal de bases de datos puede realizarse con facilidad mediante herramientas y características escalables de Base de datos SQL de Azure. En concreto, puede usar hello **biblioteca de cliente de base de datos elástica** toocreate y administrar las bases de datos de escala horizontal. Esta característica permite desarrollar fácilmente aplicaciones particionadas mediante cientos (o incluso miles) de bases de datos SQL de Azure. [Trabajos elásticos](sql-database-elastic-jobs-powershell.md) , a continuación, puede ser usado toohelp facilitar la administración de las bases de datos.

biblioteca de hello tooinstall, vaya demasiado[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Documentación
1. [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md)
2. [Características de Base de datos elástica](sql-database-elastic-scale-introduction.md)
3. [Administración de mapas de particiones.](sql-database-elastic-scale-shard-map-management.md)
4. [Migrar tooscale-fuera de las bases de datos existente](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [Enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md)
6. [Consultas en varias particiones](sql-database-elastic-scale-multishard-querying.md)
7. [Incorporación de una partición con herramientas de bases de datos elásticas](sql-database-elastic-scale-add-a-shard.md)
8. [Aplicaciones de múltiples inquilinos con herramientas de bases de datos elásticas y seguridad de nivel de fila](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [Actualización de aplicaciones de la biblioteca de cliente](sql-database-elastic-scale-upgrade-client-library.md) 
10. [Información general de consultas elásticas](sql-database-elastic-query-overview.md)
11. [Glosario de las herramientas de bases de datos elásticas](sql-database-elastic-scale-glossary.md)
12. [Biblioteca de cliente de base de datos elástica con Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [Biblioteca de cliente de Base de datos elástica con Dapper](sql-database-elastic-scale-working-with-dapper.md)
14. [Herramienta de división y combinación](sql-database-elastic-scale-overview-split-and-merge.md)
15. [Creación de bases de datos escalables en la nube](sql-database-elastic-database-client-library.md) 
16. [Preguntas frecuentes de herramientas de Base de datos elástica](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>Capacidades de cliente
Las aplicaciones que usan el escalado *particionamiento* presenta desafíos para desarrolladores de hello así como administrador de Hola. biblioteca de cliente de Hello simplifica las tareas de administración de hello proporcionándoles herramientas que permiten tanto a los desarrolladores y los administradores administrar las bases de datos de escala horizontal. En un ejemplo típico, hay muchas bases de datos, conocidos como "particiones", toomanage. Los clientes están colocados en Hola la misma base de datos, y no hay una base de datos por cliente (un esquema único inquilino). biblioteca de cliente de Hello incluye estas características:

- **Administración de mapa de particiones**: se crea una base de datos especial denominada Hola "shard map manager". Administración de mapa de particiones es la capacidad de Hola de metadatos de toomanage de una aplicación acerca de sus particiones. Los programadores pueden usar las bases de datos de este tooregister de funcionalidad como particiones, describen las asignaciones de las claves de particionamiento individuales o bases de datos de intervalos de clave toothose y mantener estos metadatos como número de Hola y composición de las bases de datos evoluciona tooreflect cambios en la capacidad. Sin la biblioteca de cliente de base de datos elástica hello, deberá toospend mucho tiempo escribir código de administración de hello al implementar el particionamiento. Para obtener más información, consulte [Administración de mapas de particiones](sql-database-elastic-scale-shard-map-management.md).

- **Enrutamiento dependiente de datos**: Imagine una solicitud que entran en la aplicación hello. Según el valor de clave de particionamiento de saludo de solicitud de hello, aplicación hello debe toodetermine Hola correcto de base de datos se basa en el valor de clave de Hola. A continuación, abre una solicitud de conexión toohello base de datos tooprocess Hola. Enrutamiento dependiente de datos permite hello tooopen conexiones con una sola llamada fácil en mapa de particiones de Hola de aplicación hello. Enrutamiento dependiente de datos era otra área del código de infraestructura que ahora está cubierto por las funciones de biblioteca de cliente de base de datos elástica Hola. Para obtener más información, consulte [Enrutamiento dependiente de los datos](sql-database-elastic-scale-data-dependent-routing.md).
- **Consultas a través de particiones múltiples (MSQ)**: las consultas a través de particiones múltiples cuando una solicitud implica varias particiones (o todas). Una consulta de varias particiones ejecuta Hola mismo código de T-SQL en todas las particiones o un conjunto de particiones. resultados de Hola de hello participa particiones se combinan en un conjunto utilizando la semántica de UNION ALL de resultados general. funcionalidad tal como se expone a través de la biblioteca de cliente de Hola Hola controla diversas tareas, incluidas: administración de conexiones, administración de subprocesos, control de errores y procesar los resultados intermedios. Puede consultar MSQ seguridad toohundreds de particiones. Para obtener más información, consulte [Consultas a través de particiones múltiples](sql-database-elastic-scale-multishard-querying.md).

En general, los clientes que usan herramientas de base de datos elástica pueden esperar tooget toda la funcionalidad de T-SQL al enviar las operaciones de partición local como operaciones de lugar toocross particiones que tienen su propia semántica.

## <a name="next-steps"></a>Pasos siguientes
Intente hello [aplicación de ejemplo](sql-database-elastic-scale-get-started.md) que muestra las funciones de cliente de Hola. 

biblioteca de hello tooinstall, vaya demasiado[biblioteca de cliente de base de datos elástica](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Para obtener instrucciones sobre cómo utilizar la herramienta de combinación de la división de hello, vea hello [Introducción a la herramienta Dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md).

[La biblioteca de cliente de bases de datos elásticas tiene ahora código abierto.](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Use [consultas elásticas](sql-database-elastic-query-overview.md).

Hello biblioteca está disponible como software de código abierto en [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

