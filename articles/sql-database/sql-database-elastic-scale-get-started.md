---
title: "aaaGet a trabajar con herramientas de base de datos elástica | Documentos de Microsoft"
description: "Explicación básica de característica de herramientas de base de datos elástica Hola de base de datos de SQL Azure, incluida una aplicación de ejemplo y ejecutar."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>Introducción a las herramientas de Elastic Database
Este documento presenta la experiencia del desarrollador toohello, ya que la aplicación de ejemplo de Hola toorun. ejemplo de Hola crea una sencilla aplicación particionada y explora las principales funciones de herramientas de la base de datos elástica. ejemplo Hello muestra las funciones de hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md).

biblioteca de hello tooinstall, vaya demasiado[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). biblioteca de Hola se instala con la aplicación de ejemplo de Hola que se describe en los pasos de la sección de Hola.

## <a name="prerequisites"></a>Requisitos previos
* Visual Studio 2012 o posterior con C#. Descargue una versión gratuita desde [Descargas de Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* NuGet 2.7 o posterior. versión más reciente de tooget hello, consulte [instalación de NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).

## <a name="download-and-run-hello-sample-app"></a>Descargue y ejecute la aplicación de ejemplo de Hola
Hola **elástico herramientas de base de datos para SQL Azure - Getting Started** aplicación de ejemplo muestra los aspectos más importantes de Hola de experiencia de desarrollo de Hola para aplicaciones con particiones que utilizan herramientas de base de datos elástica. Se centra en casos de uso claves para la [administración de asignación de particiones](sql-database-elastic-scale-shard-map-management.md), el [enrutamiento dependiente de datos](sql-database-elastic-scale-data-dependent-routing.md) y las [consultas a través de particiones múltiples](sql-database-elastic-scale-multishard-querying.md). toodownload y ejemplo de Hola de ejecución, siga estos pasos: 

1. Descargar hello [elástico herramientas de base de datos de SQL Azure: ejemplo de introducción](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) de MSDN. Descomprima la ubicación de tooa de ejemplo de Hola que elija.

2. toocreate un proyecto, abra hello **ElasticScaleStarterKit.sln** solución de hello **C#** directory.

3. En soluciones de hello para el proyecto de ejemplo de Hola, abra hello **app.config** archivo. Siga las instrucciones de hello en hello archivo tooadd el nombre del servidor de base de datos de SQL Azure y la información de inicio de sesión (nombre de usuario y contraseña).

4. Compile y ejecute la aplicación hello. Cuando se le solicite, permiten que los paquetes de NuGet de Visual Studio toorestore Hola de solución de Hola. Esto descarga versión más reciente de Hola Hola elástico de base de datos de biblioteca de cliente de NuGet.

5. Experimentar con hello distintas opciones toolearn más información acerca de las funciones de biblioteca de cliente de Hola. Tenga en cuenta los pasos de Hola Hola toma de la aplicación en la salida de la consola de Hola y cree código de hello tooexplore libre entre bastidores de Hola.
   
    ![Progreso][4]

Enhorabuena, ha creado y ejecutado correctamente su primera aplicación con particiones mediante las herramientas de Elastic Database en SQL Database. Use Visual Studio o SQL Server Management Studio base de datos SQL de tooyour de tooconnect y echar un vistazo rápido a particiones de Hola que creó el ejemplo de Hola. Observará nuevas bases de datos de partición de ejemplo y una base de datos de administrador de asignación de particiones ese ejemplo Hola creada.

> [!IMPORTANT]
> Se recomienda usar siempre la versión más reciente de Hola de Management Studio para que están sincronizadas con las actualizaciones tooAzure y base de datos de SQL. [Actualice SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>Fragmentos de código de ejemplo de Hola clave
* **Administración de particiones y particiones asigna**: Hola observaremos cómo toowork con particiones, los intervalos y las asignaciones en el archivo hello **ShardManagementUtils.cs**. Para obtener más información, consulte [escalada de las bases de datos con el Administrador de mapa de particiones de hello](http://go.microsoft.com/?linkid=9862595).  

* **Enrutamiento dependiente de los datos**: enrutamiento de particiones de las transacciones toohello derecha se muestra en **DataDependentRoutingSample.cs**. Para más información, vea [Enrutamiento dependiente de los datos](http://go.microsoft.com/?linkid=9862596). 

* **Las consultas en varias particiones**: realizar consultas en varias particiones se muestra en el archivo hello **MultiShardQuerySample.cs**. Para más información, vea [Consultas a través de particiones múltiples](http://go.microsoft.com/?linkid=9862597).

* **Agregar particiones vacías**: Hola iterativo de adición de nuevas particiones vacías se realiza mediante el código de hello en el archivo hello **CreateShardSample.cs**. Para obtener más información, consulte [escalada de las bases de datos con el Administrador de mapa de particiones de hello](http://go.microsoft.com/?linkid=9862595).

### <a name="other-elastic-scale-operations"></a>Otras operaciones de escalado elástico
* **Dividir una partición existente**: Hola proporciona particiones de hello capacidad toosplit **herramienta Dividir-combinar**. Para más información, vea [Mover datos entre bases de datos en la nube escaladas horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md).

* **Combinar las particiones existentes**: combinaciones de particiones también se realizan mediante hello **herramienta Dividir-combinar**. Para más información, vea [Mover datos entre bases de datos en la nube escaladas horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md).   

## <a name="cost"></a>Coste
herramientas de base de datos elástica Hola son gratuitas. Al usar herramientas de base de datos elástica, no recibirá los cargos adicionales sobre el costo de Hola de su uso de Azure. 

Por ejemplo, la aplicación de ejemplo de Hola crea nuevas bases de datos. costo de Hola para esto depende de hello Azure, uso de la aplicación y la edición de base de datos SQL de Hola que elija.

Para obtener información sobre los precios, vea [SQL Database Precios](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de las herramientas de base de datos elástica, vea Hola siguientes páginas:

* Ejemplos de código: 
  * [Elastic DB Tools for Azure SQL - Getting Started](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [Elastic DB Tools for Azure SQL - Entity Framework Integration](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE)
  * [Shard Elasticity on Script Center (Elasticidad de particiones en el Centro de scripts)](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* Blog: [Elastic Scale announcement](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)
* Microsoft Virtual Academy: [implementar escalado horizontal usando particionamiento con hello elástico vídeo de biblioteca de cliente de base de datos](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* Canal 9: [vídeo de introducción al escalado elástico](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* Foro de discusión: [foro de Azure SQL Database](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* rendimiento de toomeasure: [contadores de rendimiento para el Administrador de mapa de particiones](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

