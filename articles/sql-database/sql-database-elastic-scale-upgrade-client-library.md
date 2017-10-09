---
title: "biblioteca de cliente de base de datos elástica más reciente de aaaUpgrade toohello | Documentos de Microsoft"
description: "Actualización de aplicaciones y bibliotecas mediante NuGet"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>Actualizar una aplicación toouse hello más reciente bases de datos elásticas bibliotecas de cliente
Las nuevas versiones de hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md) están disponibles a través de la interfaz de NuGetPackage Manager NuGetand hello en Visual Studio. Las actualizaciones contienen correcciones de errores y compatibilidad con nuevas capacidades de la biblioteca de cliente de Hola.

**Para la versión más reciente de hello:** vaya demasiado[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Volver a generar la aplicación con la nueva biblioteca de hello, así como cambiar los metadatos de Shard Map Manager existentes almacenados en sus toosupport nuevas características de bases de datos de SQL Azure.

Llevar a cabo estos pasos en orden, se garantiza que las versiones anteriores de la biblioteca de cliente de hello ya no están presentes en un entorno cuando se actualizan los objetos de metadatos, lo que significa que no se creará objetos de metadatos de la antigua versión después de la actualización.   

## <a name="upgrade-steps"></a>Pasos de actualización
**1. Actualice sus aplicaciones.** En Visual Studio, la descarga y la versión de biblioteca cliente más reciente de referencia de Hola a todos los proyectos de desarrollo que usan la biblioteca de hello; a continuación, volver a generar e implementar. 

* En la solución de Visual Studio, seleccione **Herramientas** --> **Administrador de paquetes NuGet** -->  **Administrar paquetes NuGet para la solución**. 
* (Visual Studio 2013) En el panel izquierdo de hello, seleccione **actualizaciones**y, a continuación, seleccione hello **actualización** botón en el paquete de hello **base de datos de SQL Azure elástico biblioteca de cliente escala** que aparece en hello ventana.
* (Visual Studio 2015) Establezca el cuadro de filtro de hello demasiado**actualizar disponible**. Seleccione hello tooupdate de paquete y haga clic en hello **actualización** botón.
* (2017 de visual Studio) En hello parte superior del cuadro de diálogo de hello, seleccione **actualizaciones**. Seleccione hello tooupdate de paquete y haga clic en hello **actualización** botón.
* Genere e implemente. 

**2. Actualice los scripts.** Si utilizas **PowerShell** toomanage particiones, las secuencias de comandos [descargar la nueva versión de la biblioteca de hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) y cópielo al directorio de Hola desde el que ejecutar secuencias de comandos. 

**3. Actualice el servicio de división y combinación.** Si usas Hola bases de datos elásticas herramienta Dividir-combinar tooreorganize datos particionados, [descargar e implementar la versión más reciente de Hola de herramienta de hello](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/). Actualización pasos detallados para Hola se puede encontrar servicio [aquí](sql-database-elastic-scale-overview-split-and-merge.md). 

**4. Actualice las bases de datos de Shard Map Manager**. Actualizar los metadatos de hello admiten los mapas de particiones en la base de datos de SQL Azure.  Hay dos maneras de hacerlo, mediante PowerShell o C#. Ambas opciones se muestran a continuación.

***Opción 1: actualizar los metadatos mediante PowerShell***

1. Descargar hello más reciente de línea de comandos la utilidad de NuGet desde [aquí](http://nuget.org/nuget.exe) y guardar tooa carpeta. 
2. Abra un símbolo del sistema, vaya toohello misma carpeta y problema Hola comando:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Desplácese subcarpeta toohello que contiene Hola nueva DLL versión de cliente que se acaba de descargar, por ejemplo:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Descargar Hola elástico de base de datos cliente actualización scriptlet de hello [centro de scripts de](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), y guardarlo en hello la misma carpeta que contiene Hola DLL.
5. Desde esa carpeta, ejecute "PowerShell.\upgrade.ps1" Hola desde línea de comandos y siga las indicaciones de Hola.

***Opción 2: actualizar los metadatos mediante C#***

O bien, crear una aplicación de Visual Studio que abre su ShardMapManager, recorre en iteración todas las particiones y realiza una actualización de metadatos de hello llamando a métodos de hello [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) y [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) como en este ejemplo: 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

Estas técnicas para las actualizaciones de metadatos se pueden aplicar varias veces sin problema. Por ejemplo, si una versión anterior del cliente sin darse cuenta crea una partición después de haber actualizado ya, puede ejecutar actualización nuevo a través de tooensure de todas las particiones que hello versión más reciente de metadatos está presente en toda la infraestructura. 

**Nota:** a fecha de publicación de las nuevas versiones de la biblioteca de cliente de Hola continuar toowork con las versiones anteriores de hello Shard Map Manager metadatos en la base de datos de SQL Azure y viceversa.   Sin embargo tootake aprovechar algunas de las nuevas características de Hola de cliente más reciente de hello, metadatos necesita toobe actualizado.   Tenga en cuenta que las actualizaciones de metadatos no afecte a los datos de usuario o datos específicos de la aplicación, solo los objetos creados y utilizados por hello Shard Map Manager.  Y las aplicaciones siguen toooperate a través de la secuencia de actualización de Hola que se ha descrito anteriormente. 

## <a name="elastic-database-client-version-history"></a>Historial de versiones de cliente de base de datos elástica
Para el historial de versiones, vaya demasiado[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

