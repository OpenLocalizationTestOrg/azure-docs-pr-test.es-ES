---
title: grupos de aaaManage de bases de datos SQL de Azure | Documentos de Microsoft
description: "Tutorial sobre la creación y administración de un trabajo elástico."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>Creación y administración de Bases de datos SQL de Azure escaladas horizontalmente con trabajos elásticos (versión preliminar)


**trabajos de base de datos elástica** simplifican la administración de grupos de bases de datos al ejecutar operaciones administrativas, como cambios de esquemas, administración de credenciales, actualizaciones de datos de referencias, recopilación de datos de rendimiento o recopilación de telemetría del inquilino (cliente). Trabajos elásticos de base de datos está actualmente disponible a través de hello portal de Azure y cmdlets de PowerShell. Sin embargo, Hola funcionalidad reducida de superficies de portal de Azure limitadas tooexecution en todas las bases de datos en un [grupo elástico (versión preliminar)](sql-database-elastic-pool.md). establecen características adicionales de tooaccess y ejecución de secuencias de comandos en un grupo de bases de datos como un conjunto definido de forma personalizada o una partición (creado con [biblioteca de cliente de base de datos elástica](sql-database-elastic-scale-introduction.md)), consulte [crear y administrar trabajos usando PowerShell](sql-database-elastic-jobs-powershell.md). Para obtener más información, vea [Información general sobre Trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Requisitos previos
* Una suscripción de Azure. Para obtener una versión de evaluación gratuita, consulte [Versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Un grupo elástico. Consulte [Acerca de los grupos elásticos](sql-database-elastic-pool.md).
* Instalación de componentes del servicio de trabajo de bases de datos elásticas. Vea [instalar el servicio de trabajo de base de datos elástica hello](sql-database-elastic-jobs-service-installation.md).

## <a name="creating-jobs"></a>Creación de trabajos
1. Con hello [portal de Azure](https://portal.azure.com), en un grupo de trabajo elástico de base de datos existente, haga clic en **crear trabajo**.
2. Escriba en nombre de usuario de Hola y la contraseña de administrador de base de datos de hello (creado durante la instalación de trabajos) para la base de datos de control de trabajos de hello (almacenamiento de los metadatos para los trabajos).
   
    ![Trabajo de Hola de nombre, escriba o pegue en el código y haga clic en ejecutar][1]
3. Hola **crear trabajo** hoja, escriba un nombre para el trabajo de Hola.
4. Escriba Hola usuario nombre y la contraseña tooconnect toohello destino bases de datos con permisos suficientes para toosucceed de ejecución de secuencia de comandos.
5. Pegue o escriba en el script de Hola T-SQL.
6. Haga clic en **Guardar** y, a continuación, en **Ejecutar**.
   
    ![Creación y ejecución de trabajos][5]

## <a name="run-idempotent-jobs"></a>Ejecución de trabajos idempotentes
Cuando se ejecuta una secuencia de comandos en un conjunto de bases de datos, debe asegurarse de que el script de Hola es idempotente. Es decir, Hola script debe ser capaz de toorun varias veces, incluso si no ha superado antes en un estado incompleto. Por ejemplo, cuando se produce un error en una secuencia de comandos, el trabajo de Hola se reintentará de forma automática hasta que lo consiga (dentro de los límites, como Reintentar Hola lógica finalmente dejarán de hello Reintentar). Hola forma toodo toouse Hola se trata una cláusula "IF EXISTS" y eliminar cualquier instancia se encuentra antes de crear un nuevo objeto. A continuación se muestra un ejemplo:

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

De manera alternativa, puede usar una cláusula "IF NOT EXISTS" antes de crear una nueva instancia:

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

Esta secuencia de comandos, a continuación, actualiza la tabla Hola creado anteriormente.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>Comprobación del estado del trabajo
Tras iniciar un trabajo, puede comprobar su progreso.

1. En la página de grupo elástico de hello, haga clic en **administrar trabajos**.
   
    ![Haga clic en "Administrar trabajos".][2]
2. Haga clic en hello nombre (a) de un trabajo. Hola **estado** puede ser "Completed" o "Error". Detalles del trabajo de Hello aparecen (b) con su fecha y hora de creación y en ejecución. lista de Hello (c) por debajo de Hola que muestra el progreso de Hola de script de Hola en cada base de datos en el grupo de hello, que se facilite su información de fecha y hora.
   
    ![Comprobación de un trabajo finalizado][3]

## <a name="checking-failed-jobs"></a>Comprobación de trabajos con errores
Si se produce un error en un trabajo, puede encontrar un registro de su ejecución. Haga clic en Hola Hola error trabajo toosee sus detalles.

![Comprobación de un trabajo con error][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


