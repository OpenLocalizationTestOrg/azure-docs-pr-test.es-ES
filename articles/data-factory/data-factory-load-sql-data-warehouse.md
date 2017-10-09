---
title: aaaLoad terabytes de datos en almacenamiento de datos SQL | Documentos de Microsoft
description: "Muestra cómo se puede cargar 1 TB de datos en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a>Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Data Factory
[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) es una base de datos de escalado horizontal y basada en la nube que es capaz de procesar volúmenes masivos de datos (tanto relacionales como no relacionales).  Basado en nuestra arquitectura de procesamiento paralelo masivo (MPP), SQL Data Warehouse está mejorado para controlar las cargas de trabajo empresariales.  Ofrece elasticidad con almacenamiento de tooscale de hello flexibilidad en la nube y calcular de forma independiente.

La introducción a Azure SQL Data Warehouse es ahora más fácil que nunca usando **Azure Data Factory**.  Factoría de datos de Azure es un servicio de integración de datos en la nube totalmente administrado, que puede ser usado toopopulate un almacenamiento de datos de SQL con datos de saludo del sistema actual y ahorra tiempo valioso durante la evaluación de almacenamiento de datos SQL y creación de sus análisis soluciones. Estos son las principales ventajas de Hola de cargar datos en almacenamiento de datos de SQL Azure mediante Data Factory de Azure:

* **Fácil tooset seguridad**: paso 5 asistente intuitivo sin scripting necesarios.
* **Amplia compatibilidad para el almacenamiento de datos**: compatibilidad integrada para un amplio conjunto de almacenes de datos tanto locales como basados en la nube.
* **Seguros y conformes**: los datos se transfieren a través de HTTPS o ExpressRoute y presencia de servicio global garantiza que los datos nunca abandona los límites geográficos de Hola
* **Rendimiento sin parangón mediante PolyBase** : uso de Polybase es datos de toomove de manera más eficaces de hello en almacenamiento de datos de SQL Azure. Hola característica blobs de almacenamiento provisional se pueden conseguir velocidades de alta carga de todos los tipos de almacenes de datos además de almacenamiento de blobs de Azure, que Hola Polybase admite de forma predeterminada.

Este artículo muestra cómo toouse Asistente para copiar de factoría de datos tooload 1 TB de datos desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL Azure en menos de 15 minutos, a más de 1,2 rendimiento GBps.

Este artículo proporciona instrucciones paso a paso para mover datos a almacenamiento de datos de SQL Azure mediante el uso de hello Asistente para copiar.

> [!NOTE]
>  Para obtener información general acerca de las capacidades de la factoría de datos para mover datos hacia y desde el almacenamiento de datos de SQL Azure, consulte [mover tooand de datos de almacenamiento de datos de SQL Azure mediante Data Factory de Azure](data-factory-azure-sql-data-warehouse-connector.md) artículo.
>
> También puede crear canalizaciones utilizando Azure Portal, Visual Studio, PowerShell, etc. Vea [Tutorial: copiar los datos de Blob de Azure tooAzure base de datos SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para ver un tutorial rápido con instrucciones paso a paso para usar Hola actividad de copia de factoría de datos de Azure.  
>
>

## <a name="prerequisites"></a>Requisitos previos
* Azure Blob Storage: este experimento usa Azure Blob Storage (GRS) para almacenar un conjunto de datos de prueba TPC-H.  Si no tiene una cuenta de almacenamiento de Azure, descubra [cómo toocreate una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* [TPC-H](http://www.tpc.org/tpch/) datos: vamos toouse TPC-H como Hola prueba del conjunto de datos.  toodo esto, necesita toouse `dbgen` del Kit de herramientas de TPC-H, que le ayudará a generar el conjunto de datos de Hola.  Puede optar por descargar código fuente de `dbgen` de [TPC herramientas](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) y compílelo usted mismo o descarga Hola compila binarios de [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).  Ejecución dbgen.exe con siguiente Hola comandos de archivo sin formato de 1 TB de toogenerate para `lineitem` tabla propagación en 10 archivos:

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * …
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    Ahora Hola copia genera archivos tooAzure Blob.  Consulte demasiado[mover tooand de datos de un sistema de archivos local mediante el uso de Data Factory de Azure](data-factory-onprem-file-system-connector.md) para saber cómo toodo que mediante la copia de ADF.    
* Azure SQL Data Warehouse: este experimento carga datos en una instancia de Azure SQL Data Warehouse creada con 6.000 DWU

    Consulte demasiado[para crear un almacén de datos de SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) para obtener instrucciones detalladas sobre cómo toocreate un almacenamiento de datos SQL de base de datos.  tooget Hola carga posible un rendimiento óptimo en almacenamiento de datos de SQL con Polybase, elegimos número máximo de unidades de almacenamiento de datos (a Dwu) permitido en la configuración de rendimiento de hello, que es 6.000 a Dwu.

  > [!NOTE]
  > Al cargar desde el Blob de Azure, rendimiento de carga de datos de hello están el número de toohello directamente proporcional de a Dwu se configura en hello almacenamiento de datos SQL:
  >
  > Cargar 1 TB en SQL Data Warehouse de 1000 DWU tarda 87 minutos (con un rendimiento aproximado de 200 MB por segundo) Cargar 1 TB en SQL Data Warehouse de 2000 DWU tarda 46 minutos (con un rendimiento aproximado de 380 MB por segundo) Cargar 1 TB en SQL Data Warehouse de 6000 DWU tarda 14 minutos (con un rendimiento aproximado de 1,2 GB por segundo)
  >
  >

    toocreate un almacenamiento de datos de SQL con a 6.000 Dwu, mover la control deslizante de rendimiento de hello todos los toohello de manera Hola derecha:

    ![Control deslizante de rendimiento](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    Para una base de datos existente que no esté configurada con 6.000 DWU, puede escalarla verticalmente utilizando Azure Portal.  Navegar por la base de datos de toohello en el portal de Azure y no hay un **escala** botón en hello **información general sobre** panel se muestra en hello después de imagen:

    ![Botón de escala](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    Haga clic en hello **escala** siguiente de hello tooopen botón panel, mover el valor máximo de toohello de control deslizante de Hola y haga clic en **guardar** botón.

    ![Cuadro de diálogo Escala](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    Este experimento carga datos en Azure SQL Data Warehouse usando la clase de recursos `xlargerc`.

    necesidades de copia de tooachieve mejor rendimiento posible, toobe realiza con un usuario de almacenamiento de datos de SQL que pertenezca demasiado`xlargerc` clase de recursos.  Obtenga información acerca de cómo toodo que siguiendo [cambiar un ejemplo de clase del recurso de usuario](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).  
* Crear esquema de la tabla de destino en la base de datos de almacenamiento de datos de SQL Azure, mediante la ejecución de hello después de la instrucción DDL:

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
Con los pasos de requisitos previos de hello completados, ahora estamos actividad de copia de hello tooconfigure listo con hello Asistente para copiar.

## <a name="launch-copy-wizard"></a>Inicio del Asistente para copia
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **+ nuevo** desde la esquina superior izquierda de hello, haga clic en **Intelligence + análisis**y haga clic en **factoría de datos**.
3. Hola **factoría de datos** hoja:

   1. Escriba **LoadIntoSQLDWDataFactory** para hello **nombre**.
       nombre de Hola Hola Azure factoría de datos debe ser único globalmente. Si recibe el error hello: **nombre de generador de datos "LoadIntoSQLDWDataFactory" no está disponible**, cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameLoadIntoSQLDWDataFactory) y pruebe a crear de nuevo. Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.  
   2. Selección la **suscripción**de Azure.
   3. Para el grupo de recursos, realice una de hello pasos:
      1. Seleccione **utilizar existente** tooselect un grupo de recursos existente.
      2. Seleccione **crear nuevo** tooenter un nombre para un grupo de recursos.
   4. Seleccione un **ubicación** de factoría de datos de Hola.
   5. Seleccione **toodashboard Pin** casilla situada en la parte inferior de Hola de hoja de Hola.  
   6. Haga clic en **Crear**.
4. Una vez completada la creación de hello, vea hello **factoría de datos** hoja como se muestra en hello después de imagen:

   ![Página principal de Factoría de datos](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. En la página de inicio de la factoría de datos de hello, haga clic en hello **copiar datos** icono toolaunch **Asistente para copiar**.

   > [!NOTE]
   > Si ve ese explorador web de hello está atascado en "Autorizar …", deshabilite o desactive **bloquear las cookies de terceros y datos de sitio** configuración (o) manténgala habilitada y cree una excepción para **login.microsoftonline.com**y, a continuación, intente iniciar Asistente de Hola de nuevo.
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a>Paso 1: Configuración de la programación de carga de datos
Hola primer paso es programación al cargar los datos tooconfigure Hola.  

Hola **propiedades** página:

1. Escriba **CopyFromBlobToAzureSqlDataWarehouse** en **Nombre de tarea**
2. Seleccione la opción **Ejecutar una vez ahora**.   
3. Haga clic en **Siguiente**.  

    ![Asistente para copia: Página Propiedades](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a>Paso 2: Configuración del origen
En esta sección se muestra Hola pasos tooconfigure origen de hello: Blob de Azure que contiene Hola 1 TB TPC-archivos de elementos de línea de H.

1. Seleccione hello **almacenamiento de blobs de Azure** como datos de hello almacenar y haga clic en **siguiente**.

    ![Asistente para copia: Selección de página de origen](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. Rellene la información de conexión de Hola para hello cuenta de almacenamiento Blob de Azure y haga clic en **siguiente**.

    ![Asistente para copia: Información de conexión de origen](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. Elija hello **carpeta** que contiene la línea hello TPC-H elemento archivos y haga clic en **siguiente**.

    ![Asistente para copia: Selección de carpeta de entrada](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. Al hacer clic en **siguiente**, configuración de formato de archivo de Hola se detecta automáticamente.  Comprobar toomake seguro de que el delimitador de columnas es ' | 'en lugar de hello predeterminado por comas','.  Haga clic en **siguiente** después de que ha obtenido una vista previa de los datos de Hola.

    ![Herramienta de copia: Ajustes de formato de archivo](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a>Paso 3: Configuración del destino
Esta sección muestra cómo tooconfigure Hola destino: `lineitem` tabla de base de datos de almacenamiento de datos de SQL Azure Hola.

1. Elija **almacenamiento de datos de SQL Azure** como destino de hello almacenar y haga clic en **siguiente**.

    ![Asistente para copia: Selección del almacén de datos de destino](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. Rellene la información de conexión de hello para el almacenamiento de datos de SQL Azure.  Asegúrese de especificar usuario Hola que es un miembro del rol de hello `xlargerc` (vea hello **requisitos previos** sección para obtener instrucciones detalladas) y haga clic en **siguiente**.

    ![Asistente para copia: Información de conexión de destino](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. Elegir tabla de destino de Hola y haga clic en **siguiente**.

    ![Asistente para copia: Página de asignación de tabla](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. En la página de asignación de esquemas, deje desactivada la opción "Apply column mapping" (Aplicar asignación de columna) y haga clic en **Siguiente**.

## <a name="step-4-performance-settings"></a>Paso 4: Configuración de rendimiento

La opción **Allow polybase** (Permitir Polybase) está activada de forma predeterminada.  Haga clic en **Siguiente**.

![Asistente para copia: Página de asignación de esquema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a>Paso 5: Implementación y supervisión de los resultados de carga
1. Haga clic en **finalizar** toodeploy de botón.

    ![Asistente para copiar: Página de resumen](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. Una vez completada la implementación de hello, haga clic en `Click here toomonitor copy pipeline` copia de hello toomonitor progreso de la ejecución. Canalización de copia de hello SELECT que creó en hello **Windows actividad** lista.

    ![Asistente para copiar: Página de resumen](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    Puede ver detalles de la serie de Hola de copia de hello **Explorer de la ventana de actividad** en el panel derecho hello, incluidos el volumen de datos de hello leídos del origen y escribir en el destino, la duración y el rendimiento medio de Hola para hello ejecutar.

    Como puede ver en hello siguiente captura de pantalla, copiar 1 TB de almacenamiento de blobs de Azure en almacenamiento de datos de SQL tardó 14 minutos, eficazmente un rendimiento de GBps 1,22!

    ![Asistente para copia: Cuadro de diálogo de éxito en la operación](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a>Prácticas recomendadas
Estas son algunos de los procedimientos recomendados para la ejecución de la base de datos de Azure SQL Data Warehouse:

* Use una clase de recurso más grande al cargar en un ÍNDICE AGRUPADO DE ALMACÉN DE COLUMNAS.
* Para las combinaciones más eficaces, considere el uso de distribución hash con una columna seleccionada, en lugar de la distribución round robin predeterminada.
* Para conseguir una mayor velocidad de carga, considere la posibilidad de utilizar un montón para los datos transitorios.
* Cree estadísticas después de finalizar la carga de Azure SQL Data Warehouse.

Para información más detallada consulte [Procedimientos recomendados para Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

## <a name="next-steps"></a>Pasos siguientes
* [Asistente para copiar de factoría de datos](data-factory-copy-wizard.md) -este artículo proporciona detalles acerca de hello Asistente para copiar.
* [Copiar actividad Guía de rendimiento y optimización](data-factory-copy-activity-performance.md) -este artículo contiene las medidas de rendimiento de referencia de Hola y Guía de optimización.
