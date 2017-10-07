---
title: "Hola proceso de ciencia de datos de equipo en acción: con almacenamiento de datos SQL | Documentos de Microsoft"
description: "Tecnología y procesos de análisis avanzado en acción"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>Hola proceso de ciencia de datos de equipo en acción: con almacenamiento de datos SQL
En este tutorial, se le guían en la creación e implementación de un modelo de aprendizaje automático con almacenamiento de datos de SQL (SQL DW) para un conjunto de datos disponible públicamente--hello [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos. modelo de clasificación binaria de Hello construido predice si no se le paga una sugerencia para un recorrido, y los modelos de regresión y de clasificación multiclase también se tratan que predicen distribución Hola para hello cantidades de sugerencia de pago.

procedimiento de Hello sigue hello [proceso de ciencia de datos de equipo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) flujo de trabajo. Le mostramos cómo toosetup un entorno de ciencia de datos, cómo tooload Hola datos en almacenamiento de datos de SQL y cómo usar el almacenamiento de datos de SQL o un bloc de notas de IPython tooexplore Hola datos e ingeniero características toomodel. A continuación, mostramos cómo toobuild e implementar un modelo de aprendizaje automático de Azure.

## <a name="dataset"></a>el conjunto de datos de Hello NYC Taxi viajes
Hola datos NYC Taxi recorridos consta de unos 20GB de archivos comprimidos de CSV (sin comprimir de ~ 48GB), más de 173 millones de grabación hello y viajes individuales puntuación de pago para cada recorrido. Cada registro de ida y vuelta incluye ubicaciones de recogida y entrega de Hola y tiempos, anónimos hack número de licencia (del controlador) y Hola número medallion (identificador único del taxi). datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:

1. Hola **trip_data.csv** archivo contiene los detalles de ida y vuelta, como el número de los pasajeros, puntos de recogida y caída, duración de ida y vuelta y duración del viaje. Estos son algunos registros de ejemplo:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hola **trip_fare.csv** archivo contiene detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago. Estos son algunos registros de ejemplo:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hola **clave única** utilizan recorridos toojoin\_datos y recorridos\_tarifa se compone de hello después de tres campos:

* medallion,
* hack\_license y
* pickup\_datetime.

## <a name="mltasks"></a>Realicemos tres tipos de tareas de predicción
Se formular tres problemas de predicción basándose en hello *sugerencia\_cantidad* tooillustrate tres tipos de tareas de modelado:

1. **Clasificación binaria**: toopredict o no se pagó una sugerencia para un recorrido, es decir, un *sugerencia\_cantidad* que es mayor que $0 es un ejemplo positivo, mientras un *sugerencia\_cantidad* $ 0 es un ejemplo negativo.
2. **Clasificación multiclase**: intervalo de hello toopredict de sugerencia de pago para recorridos de Hola. Se divide hello *sugerencia\_cantidad* en cinco bandejas o clases:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Tarea de regresión**: cantidad de hello toopredict de sugerencia de pago para un recorrido.  

## <a name="setup"></a>Configurar el entorno de ciencia de datos de Azure de Hola para análisis avanzado
tooset del entorno de ciencia de datos de Azure, siga estos pasos.

**Cree su propia cuenta de Almacenamiento de blobs de Azure.**

* Al proporcionar su propio almacenamiento de blobs de Azure, elija una ubicación geográfica del almacenamiento de blobs de Azure en o tan cerca como sea posible demasiado**Ee.uu. Central sur**, que es donde se almacena los datos de Nueva York Taxi Hola. datos de Hola se copiarán con AzCopy de contenedor de tooa de contenedor de almacenamiento de blobs públicos de hello en su propia cuenta de almacenamiento. Hello cuando se acerque el almacenamiento de blobs de Azure es tooSouth Central US, hello más rápido (paso 4) se puede realizar esta tarea.
* cuenta de su propio almacenamiento de Azure toocreate, Hola seguir pasos que se describen en [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md). Estar seguro de notas de toomake valores de hello para las siguientes credenciales de cuenta de almacenamiento que se necesitarán más adelante en este tutorial.
  
  * **Nombre de cuenta de almacenamiento**
  * **Clave de cuenta de almacenamiento**
  * **Nombre del contenedor** (que quiere hello toobe de datos almacenado en hello almacenamiento de blobs de Azure)

**Aprovisione la instancia de Almacenamiento de datos SQL de Azure.**
Seguir la documentación de hello en [crear un almacén de datos de SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision una instancia de almacenamiento de datos SQL. Asegúrese de que realiza las notaciones en hello siguiendo las credenciales de almacén de datos de SQL que se utilizarán en pasos posteriores.

* **Nombre del servidor**: <server Name>.database.windows.net
* **Nombre de SQLDW (base de datos)**
* **Nombre de usuario**
* **Password**

**Instale Visual Studio y SQL Server Data Tools.** Para ver instrucciones, consulte [Instalación de Visual Studio 2015 y SSDT para Almacenamiento de datos SQL](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).

**Conectar tooyour almacenamiento de datos de SQL Azure con Visual Studio.** Para obtener instrucciones, consulte los pasos 1 y 2 en [conectar tooAzure almacenamiento de datos de SQL con Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).

> [!NOTE]
> Ejecución hello consulta SQL en la base de datos de Hola que creó en el almacenamiento de datos de SQL siguiente (en lugar de consulta de hello proporcionada en el paso 3 de hello conectar tema) demasiado**crear una clave maestra de**.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Cree un área de trabajo de Azure Machine Learning en su suscripción de Azure.** Para ver instrucciones, consulte [Creación de un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md).

## <a name="getdata"></a>Cargar datos de hello en almacenamiento de datos SQL
Abra una consola de comandos de Windows PowerShell. Ejecute hello siguiente comandos de PowerShell toodownload Hola ejemplo archivos de script SQL que se comparten con usted en GitHub tooa directorio local que se especifica con el parámetro hello *- DestDir*. Puede cambiar Hola valor del parámetro *- DestDir* tooany de directorio local. Si *- DestDir* no existe, se creará Hola script de PowerShell.

> [!NOTE]
> Es posible que tenga demasiado**ejecutar como administrador** al ejecutar Hola siguiente script de PowerShell si su *DestDir* directorio debe tooit de toocreate o toowrite de privilegios de administrador.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

Tras la ejecución correcta, el directorio de trabajo actual cambia demasiado*- DestDir*. Debería poder toosee pantalla como a continuación:

![][19]

En su *- DestDir*, ejecute hello siguiente script de PowerShell en modo de administrador:

    ./SQLDW_Data_Import.ps1

Cuando Hola script de PowerShell se ejecuta para hello primera vez, se le pedirá información de hello tooinput desde el almacenamiento de datos de SQL Azure y la cuenta de almacenamiento de blobs de Azure. Cuando se completa este script de PowerShell ejecuta para hello primera vez, las credenciales de hello proporcionados por el habrá se han escrito archivo de configuración de tooa SQLDW.conf en el directorio de trabajo presente Hola. Hello ejecución futuras de este archivo de script de PowerShell tiene Hola opción tooread necesarios todos los parámetros de este archivo de configuración. Si necesita toochange algunos parámetros, puede elegir parámetros hello en pantalla de bienvenida al símbolo del sistema si elimina este archivo de configuración y especificar valores de parámetros de hello cuando se le solicite o con valores de parámetro de hello toochange tooinput editando el archivo de hello SQLDW.conf en su *- DestDir* directory.

> [!NOTE]
> En orden tooavoid esquema nombre entra en conflicto con los que ya existen en el almacenamiento de datos de SQL Azure, al leer parámetros directamente desde el archivo de SQLDW.conf hello, un número aleatorio de 3 dígitos se agrega toohello nombre del esquema de archivo de hello SQLDW.conf como nombre de esquema predeterminado de Hola para cada ejecución. Hola script de PowerShell puede pedirle un nombre de esquema: se puede especificar el nombre de Hola a discreción del usuario.
> 
> 

Esto **script de PowerShell** archivo completa Hola siguiente las tareas:

* **Descarga e instala AzCopy**, si AzCopy no se ha instalado aún
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **Copia de la cuenta de almacenamiento de blobs privado de datos tooyour** de blob públicos de hello con AzCopy
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Carga datos mediante Polybase (mediante la ejecución de LoadDataToSQLDW.sql) tooyour Azure SQL DW** de la cuenta de almacenamiento de blobs privado con hello siga los comandos.
  
  * Creación de un esquema
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * Creación de una credencial con ámbito de base de datos
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Creación de un origen de datos externo para un blob de Almacenamiento de Azure
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * Cree un formato de archivo externo para un archivo .csv. Datos sin comprimir y los campos están separados con carácter de canalización de Hola.
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * Cree tablas externas de tarifas y propinas para el conjunto de datos de NYC Taxi en el Almacenamiento de blobs de Azure.
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - Cargar datos de tablas externas de almacenamiento de blobs de Azure tooSQL almacenamiento de datos

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - Crear una tabla de datos de ejemplo (NYCTaxi_Sample) e insertar tooit de datos de la selección de consultas SQL en tablas de tarifas y recorridos de Hola. (Algunos pasos de este tutorial debe toouse esta tabla de ejemplo.)

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

ubicación geográfica de Hola de sus cuentas de almacenamiento afecta a los tiempos de carga.

> [!NOTE]
> Según la ubicación geográfica de saludo de la cuenta de almacenamiento de blobs privado, proceso Hola de copiar datos de una cuenta de almacenamiento privado tooyour blob público puede tardar unos 15 minutos o incluso ya y hello del proceso de carga de datos de la cuenta de almacenamiento tooyour almacenamiento de datos de SQL Azure puede tardar 20 minutos o más.  
> 
> 

Deberá toodecide ¿qué hacer si tiene un origen duplicado y archivos de destino.

> [!NOTE]
> Si toobe de archivos .csv Hola copiado de cuenta de almacenamiento de blobs privado de hello blob público almacenamiento tooyour ya existe en la cuenta de almacenamiento de blobs privado, AzCopy le preguntará si desea toooverwrite ellos. Si no desea toooverwrite éstos, entrada  **n**  cuando se le solicite. Si desea que toooverwrite **todos los** de ellos, de entrada **un** cuando se le solicite. También puede introducir **y** toooverwrite .csv archivos individualmente.
> 
> 

![Diagrama 21][21]

Puede usar sus propios datos. Si los datos están en el equipo local en su aplicación en la vida real, todavía puede usar el almacenamiento de blobs de Azure privada de tooyour de datos de AzCopy tooupload local. Solo necesita hello toochange **origen** ubicación, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, Hola comandos de AzCopy de hello PowerShell script archivo toohello directorio local que contiene los datos.

> [!TIP]
> Si los datos ya están en el almacenamiento de blobs de Azure privada en la aplicación de la vida real, puede omitir hello AzCopy paso Hola script de PowerShell y cargar directamente hello tooAzure de datos SQL DW. Esto requerirá adicionales edita de hello script tootailor toohello formato de los datos.
> 
> 

Este script de Powershell también se conecta en hello información de almacenamiento de datos de SQL Azure en archivos ejemplo de Hola datos exploración SQLDW_Explorations.sql, SQLDW_Explorations.ipynb y SQLDW_Explorations_Scripts.py para que estos tres archivos sean toobe listo probado al instante una vez completada la Hola script de PowerShell.

Después de una ejecución correcta, verá una pantalla similar a la siguiente:

![][20]

## <a name="dbexplore"></a>Exploración de datos y diseño de características en Almacenamiento de datos SQL de Azure
En esta sección, realizamos la generación de características y la exploración de datos mediante la ejecución de consultas SQL en Almacenamiento de datos SQL de Azure directamente mediante **Visual Studio Data Tools**. Todas las consultas SQL que se utilizan en esta sección pueden encontrarse en el script de ejemplo de Hola denominado *SQLDW_Explorations.sql*. Este archivo ya ha sido descargado tooyour directorio local por script de PowerShell de Hola. También puede recuperarlo desde [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql). Pero el archivo hello en GitHub no tiene información de almacenamiento de datos de SQL Azure Hola enchufado.

Conectar tooyour almacenamiento de datos de SQL de Azure con Visual Studio con el nombre de inicio de sesión de SQL DW hello y una contraseña y se abrirán hello **Explorador de objetos SQL** base de datos de tooconfirm hello y las tablas se han importado. Recuperar hello *SQLDW_Explorations.sql* archivo.

> [!NOTE]
> tooopen un editor de consultas de almacenamiento de datos paralelo (PDW), usar hello **nueva consulta** comando mientras está seleccionado el PDW en hello **Explorador de objetos SQL**. editor de consultas SQL estándar de Hello no es compatible con PDW.
> 
> 

Estos son tipo hello de datos realizan tareas de generación de exploración y la característica de esta sección:

* Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.
* Investigue la calidad de los datos de los campos de longitud y latitud de Hola.
* Generar etiquetas de clasificación multiclase y binaria basándose en hello **sugerencia\_cantidad**.
* Generar características y calcular o comparar distancias de carreras.
* Combinar Hola dos tablas y extraer una muestra aleatoria que será usado toobuild modelos.

### <a name="data-import-verification"></a>Comprobación de la importación de datos
Estas consultas proporcionan una comprobación rápida del número de Hola de filas y columnas de hello importan tablas rellenadas anteriormente con masiva paralela de Polybase,

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**Salida:** debe obtener 173 179 759 filas y 14 columnas.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploración: distribución de carreras por licencia
Esta consulta de ejemplo identifica medallions Hola (taxi números) que completar más de 100 viajes dentro de un período de tiempo especificado. consulta de Hola se beneficiaría de acceso a la tabla con particiones de hello porque está condicionado por esquema de partición de Hola de **recogida\_datetime**. Consultar el conjunto de datos completo de hello también hará que el uso de la tabla con particiones de Hola o examen de índice.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**Salida:** deben devolver una tabla con filas especificando medallions hello 13,369 (taxis) de consultas de Hola y Hola número de recorridos realizarla en 2013. Hola última columna contiene recuento de hello del número de Hola de viajes y completado.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploración: distribución de carreras por medallion y hack_license
Este ejemplo identifica medallions Hola (taxi números) y hack_license números (controladores) que completar más de 100 viajes dentro de un período de tiempo especificado.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**Salida:** consulta Hola debe devolver una tabla con 13,369 filas especificar hello 13,369 automóvil/controlador identificadores que se han completado más que 100 viajes en 2013. Hola última columna contiene recuento de hello del número de Hola de viajes y completado.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Evaluación de la calidad de los datos: comprobar los registros con longitud o latitud incorrectas
En este ejemplo se investiga si alguno de los campos de longitud o latitud de Hola o contiene un valor no válido (grados Radián deben estar entre -90 y 90), o tener (0, 0) coordenadas.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**Salida:** consulta Hola devuelve 837,467 viajes y que tiene campos no válidos de longitud o latitud.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploración: distribución de carreras con propinas frente a sin propinas
Este ejemplo busca el número de Hola de viajes que se han superpuesto frente a número de Hola y que no se han superpuesto en un período de tiempo especificado (o conjunto de datos completa de hello si cubriendo año completo Hola tal y como se configura aquí). Esta distribución refleja Hola etiqueta binario distribución toobe que más adelante se usa para el modelo de clasificación binaria.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**Salida:** Hola consulta debe siguiente Hola devuelto sugerencia frecuencias de hello año 2013: 90,447,622 superpuesto y 82,264,709 superpuesto no.

### <a name="exploration-tip-classrange-distribution"></a>Exploración: distribución por intervalos y clases de propinas
Este ejemplo calcula distribución Hola de intervalos de sugerencia en un momento determinado período (o en el conjunto de datos completo de hello si relativo Hola completa año). Se trata de distribución de Hola de clases de etiqueta de Hola que usará más adelante para el modelado de clasificación multiclase.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**Salida:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82 230 915 |
| 2 |6 198 803 |
| 3 |1 932 223 |
| 0 |82 264 625 |
| 4 |85 765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>Exploración: proceso y comparación de la distancia de la carrera
Este ejemplo convierte la longitud de recogida y entrega de Hola y geografía de latitud tooSQL señala, calcula la distancia de viaje hello mediante diferencia de puntos de geography SQL y devuelve una muestra aleatoria de resultados de hello para la comparación. ejemplo de Hola limita los resultados de hello toovalid coordina únicamente con la consulta de evaluación de calidad Hola datos cubierto anteriormente.

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>Diseño de características con las funciones de SQL
A veces, las funciones de SQL pueden ser una opción eficiente de diseño de características. En este tutorial, definimos una SQL función toocalculate Hola distancia directa entre las ubicaciones de recogida y caída de Hola. Puede ejecutar Hola siguientes secuencias de comandos SQL en **herramientas de datos de Visual Studio**.

Esta es la secuencia de comandos SQL de Hola que define la función de distancia de hello.

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

Este es un toocall de ejemplo esta característica de toogenerate de función en la consulta SQL:

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**Salida:** esta consulta genera una tabla (con 2,803,538 filas) con recogida y caída latitudes y longitudes y Hola correspondiente dirigen distancias en millas. Estos son los resultados de Hola para primero 3 filas:

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40,731804 |-74,001083 |40,736622 |-73,988953 |0,7169601222 |
| 2 |40,715794 |-74,010635 |40,725338 |-74,00399 |0,7448343721 |
| 3 |40,761456 |-73,999886 |40,766544 |-73,988228 |0,7037227967 |

### <a name="prepare-data-for-model-building"></a>Preparar datos para la generación de modelos
Hola de combinaciones de consulta siguiente Hello **nyctaxi\_recorridos** y **nyctaxi\_tarifa** tablas, genera una etiqueta de clasificación binaria **superpuesto**, etiqueta de clasificación multiclase **sugerencia\_clase**y extrae un ejemplo de Hola completa Unidos a un conjunto de datos. muestreo de Hola se realiza mediante la recuperación de un subconjunto de viajes de hello en función del tiempo de recogida.  Esta consulta se puede copiar y pegar directamente en hello [estudio de aprendizaje automático de Azure](https://studio.azureml.net) [importar datos] [ import-data] módulo de recopilación de datos directa de instancia de base de datos SQL de Hola en Azure. consulta de Hello excluye los registros con incorrecto (0, 0) coordenadas.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

Cuando esté listo tooproceed tooAzure aprendizaje automático, puede:  

1. Guardar Hola final SQL consulta tooextract y ejemplo Hola datos y copiar y pegar Hola consulta directamente en un [importar datos] [ import-data] módulo aprendizaje automático de Azure, o
2. Hola muestreada se conservan e ingeniería datos que tiene previsto toouse para el modelo de creación de un nuevo almacenamiento de datos de SQL de la tabla y usar nueva tabla de hello en hello [importar datos] [ import-data] módulo aprendizaje automático de Azure. Hola script de PowerShell en el paso anterior hace esto automáticamente. Puede leer directamente en esta tabla en el módulo de importación de datos de Hola.

## <a name="ipnb"></a>Exploración de datos e ingeniería de características en IPython Notebook
En esta sección, se llevará a cabo una exploración de datos y la generación de característica con ambas Python y consultas SQL en hello SQL DW crean anteriormente. Un bloc de notas de IPython de ejemplo denominado **SQLDW_Explorations.ipynb** y un archivo de script de Python **SQLDW_Explorations_Scripts.py** se han descargado tooyour directorio local. También están disponibles en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW). Estos dos archivos son idénticos en los scripts de Python. archivo de script de Python Hola se proporciona tooyou en caso de que no tiene un servidor de Bloc de notas de IPython. Estos dos archivos de Python de muestra están diseñados en **Python 2.7**.

Hola información necesaria de almacenamiento de datos de SQL Azure en el Bloc de notas de IPython de ejemplo de Hola y Hola Python máquina local de tooyour descargado de archivos de script se ha conectado por script de PowerShell de hello previamente. Son ejecutables sin ninguna modificación.

Si ya ha configurado un área de trabajo de aprendizaje automático de Azure, puede cargar muestra de Hola a servicio de Bloc de notas de IPython toohello Bloc de notas de IPython de aprendizaje automático de Azure y comenzar a ejecutarla directamente. A continuación, incluimos Hola pasos tooupload tooAzureML servicio Bloc de notas de IPython:

1. Inicie sesión en el área de trabajo de tooyour aprendizaje automático de Azure, haga clic en "Studio" en la parte superior de Hola y haga clic en "Blocs de notas" en el lado izquierdo de Hola de página web de Hola.
   
    ![Diagrama 22][22]
2. Haga clic en "Nuevo" en la esquina inferior izquierda de Hola de página web de Hola y seleccione "Python 2". A continuación, proporcionar un bloc de notas de toohello de nombre y haga clic en hello marca de verificación toocreate Hola nuevo en blanco Bloc de notas de IPython.
   
    ![Diagrama 23][23]
3. Haga clic en el símbolo de "Jupyter" hello en la esquina superior izquierda de Hola de hello nuevo bloc de notas de IPython.
   
    ![Diagrama 24][24]
4. Arrastre y coloque Hola ejemplo Bloc de notas de IPython toohello **árbol** página del servicio de Bloc de notas de IPython de aprendizaje automático de Azure y haga clic en **cargar**. A continuación, muestra de Hola Bloc de notas de IPython será cargado toohello servicio Bloc de notas de IPython de aprendizaje automático de Azure.
   
    ![Diagrama 25][25]

Hola toorun de pedido de ejemplo Bloc de notas de IPython u Hola archivo de script de Python, hello siguientes Python paquetes son necesarios. Si usas el servicio de hello Bloc de notas de IPython de aprendizaje automático de Azure, estos paquetes se hayan instalado previamente.

    - Pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

Hola recomendada secuencia al compilar las soluciones analíticas avanzadas en aprendizaje automático de Azure con datos de gran tamaño es siguiente de hello:

* Leer en una pequeña muestra de datos de hello en un marco de datos en memoria.
* Realizar algunas visualizaciones y exploraciones con los datos de ejemplo de Hola.
* Experimente con ingeniería de característica con hello los datos de ejemplo.
* Exploración de datos mayor, manipulación de datos y la ingeniería de característica, utilizar consultas de SQL de tooissue de Python directamente en hello SQL DW.
* Decidir toobe de tamaño de ejemplo de Hola adecuado para la compilación del modelo de aprendizaje automático de Azure.

siguiente Hola es unos exploración de datos, visualización de datos y ejemplos de ingeniería de característica. Más exploraciones de datos pueden encontrarse en el ejemplo hello Bloc de notas de IPython y archivo de script de Python de ejemplo de Hola.

### <a name="initialize-database-credentials"></a>Inicialización de las credenciales de la base de datos
Inicializar la configuración de conexión de base de datos en hello siguientes variables:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>Creación de conexiones de base de datos
Aquí es cadena de conexión de Hola que crea la base de datos de hello conexión toohello.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Informe con el número de filas y columnas de la tabla <nyctaxi_trip>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de filas = 173179759  
* Número total de columnas = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>Informe con el número de filas y columnas de la tabla <nyctaxi_fare>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de filas = 173179759  
* Número total de columnas = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>Lectura de un pequeño datos de ejemplo de Hola base de datos de almacenamiento de datos de SQL
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tabla de ejemplo de Hola de tiempo tooread es 14.096495 segundos.  
Número de filas y columnas recuperadas = (1000, 21)

### <a name="descriptive-statistics"></a>Estadísticas descriptivas
Ahora está listo tooexplore Hola muestreada datos. Empezaremos con mirando algunas estadísticas descriptivas para hello **recorridos\_distancia** (o cualquier otro campo elija toospecify).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>Visualización: ejemplo de diagrama de caja
A continuación, veremos caja Hola para Hola de ida y vuelta distancia toovisualize hello cuantiles.

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagrama 1][1]

### <a name="visualization-distribution-plot-example"></a>Visualización: ejemplo de diagrama de distribución
Los trazados que visualización la distribución de Hola y un histograma para hello muestrearon las distancias de ida y vuelta.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagrama 2][2]

### <a name="visualization-bar-and-line-plots"></a>Visualización: diagramas de barras y líneas
En este ejemplo, hemos discretizar distancia de viaje hello en cinco cubos y visualizar Hola discretizar los resultados.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Podemos trazar Hola por encima de la distribución de la Papelera de una barra o línea trazado con:

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagrama 3][3]

y

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagrama 4][4]

### <a name="visualization-scatterplot-examples"></a>Visualización: ejemplos de gráfico de dispersión
Se muestra el gráfico de dispersión entre **recorridos\_tiempo\_en\_s** y **recorridos\_distancia** toosee si hay alguna correlación

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagrama 6][6]

De igual forma podemos comprobar relación Hola entre **velocidad\_código** y **recorridos\_distancia**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagrama 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>Exploración de datos en datos de muestreo mediante consultas SQL en IPython Notebook
En esta sección, exploramos distribuciones de datos utilizando los datos de hello muestreada que se guardan en la nueva tabla de hello que hemos creado anteriormente. Tenga en cuenta que se pueden realizar exploraciones similar mediante tablas originales de Hola.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>Exploración: Número de informes de filas y columnas de hello muestreadas tabla
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>Exploración: distribución con propinas y sin propinas
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>Exploración: distribución de clases de propinas
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>Exploración: Trazar la distribución de la sugerencia de Hola por clase
    tip_class_dist['tip_freq'].plot(kind='bar')

![Diagrama 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a>Exploración: distribución diaria de carreras
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploración: distribución de carreras por licencia
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>Exploración: distribución de carreras por placa y número de licencia
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>Exploración: distribución del tiempo de la carrera
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>Exploración: distribución de la distancia de la carrera
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>Exploración: distribución del tipo de pago
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Comprobar el formulario final de Hola de tabla de caracterizará Hola
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure
Ahora estamos listos tooproceed toomodel creación e implementación de modelo en [aprendizaje automático de Azure](https://studio.azureml.net). datos Hello están listo toobe usado en cualquiera de los problemas de predicción de hello identificados anteriormente, a saber:

1. **Clasificación binaria**: toopredict o no se pagó una sugerencia para un recorrido.
2. **Clasificación multiclase**: intervalo de hello toopredict de sugerencia de pago, según toohello clases definidas previamente.
3. **Tarea de regresión**: cantidad de hello toopredict de sugerencia de pago para un recorrido.  

toobegin Hola modelado ejercicio, inicie sesión en tooyour **aprendizaje automático de Azure** área de trabajo. Si aún no ha creado un área de trabajo de aprendizaje automático, consulte [Creación de un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md).

1. tooget a trabajar con aprendizaje automático de Azure, consulte [¿qué es el estudio de aprendizaje automático de Azure?](machine-learning-what-is-ml-studio.md)
2. Inicie sesión demasiado[estudio de aprendizaje automático de Azure](https://studio.azureml.net).
3. página de inicio de Studio Hola proporciona una gran cantidad de información, vídeos, tutoriales, vínculos toohello referencia de módulos y otros recursos. Para obtener más información acerca de aprendizaje automático de Azure, consulte hello [centro de documentación de aprendizaje automático](https://azure.microsoft.com/documentation/services/machine-learning/).

Un experimento de entrenamiento típico consta de hello pasos:

1. Crear un experimento **+NUEVO** .
2. Obtener datos de hello en aprendizaje automático de Azure.
3. Preprocesar, transformar y manipular datos Hola según sea necesario.
4. Generar características según sea necesario.
5. Dividir los datos de hello en conjuntos de datos de entrenamiento / / pruebas de validación (o tiene conjuntos de datos independiente para cada uno).
6. Seleccionar algoritmos función hello toosolve problema de aprendizaje de aprendizaje automático de uno o más. Por ejemplo: clasificación binaria, clasificación multiclase, regresión.
7. Entrenar uno o varios modelos utilizando el conjunto de datos de entrenamiento de Hola.
8. Puntuación Hola de conjunto de datos de validación utilizando modelos entrenados Hola.
9. Evaluar Hola modelos toocompute Hola métricas pertinente para hello problema de aprendizaje.
10. Ajustar los modelos de Hola y Hola seleccione mejor modelo toodeploy.

En este ejercicio, hemos ya explorar e ingeniería datos hello en el almacén de datos de SQL y decidido tooingest de tamaño de ejemplo de Hola en aprendizaje automático de Azure. Aquí es Hola procedimiento toobuild uno o varios de los modelos de predicción de hello:

1. Obtener datos de hello en aprendizaje automático de Azure con hello [importar datos] [ import-data] módulo, disponibles en hello **datos de entrada y salida** sección. Para obtener más información, vea hello [importar datos] [ import-data] página de referencia de módulo.
   
    ![Datos de importación de Aprendizaje automático de Azure][17]
2. Seleccione **base de datos de SQL Azure** como hello **origen de datos** en hello **propiedades** panel.
3. Escriba el nombre DNS de base de datos de Hola Hola **el nombre del servidor de base de datos** campo. Formato: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Escriba hello **nombre de base de datos** en el campo correspondiente Hola.
5. Escriba hello *nombre de usuario SQL* en hello **nombre de cuenta de usuario de servidor**, hello y *contraseña* en hello **contraseña de cuenta de usuario de servidor**.
6. Comprobar hello **Aceptar cualquier certificado de servidor** opción.
7. Hola **consulta de base de datos** editar el área de texto, pegue la consulta de Hola que extrae Hola necesarios campos (incluidos los campos calculados, como las etiquetas de hello) de la base de datos y el detalle de ejemplos de tamaño de la muestra de Hola datos toohello deseado.

Es un ejemplo de un experimento de clasificación binaria leer los datos directamente desde la base de datos de almacenamiento de datos SQL de hello en figura Hola siguiente (recuerde tooreplace Hola nombres de tabla nyctaxi_trip y nyctaxi_fare por esquema Hola hello y nombre de los nombres de tabla que usó en el tutorial). Se pueden construir experimentos similares para problemas de clasificación multiclase y de regresión.

![Entrenamiento de Aprendizaje automático de Azure][10]

> [!IMPORTANT]
> Hola, extracción de datos de modelado y realizando un muestreo ejemplos de consultas que se proporcionan en las secciones anteriores, **todas las etiquetas de ejercicios de modelado de hello tres se incluyen en la consulta de hello**. Un paso importante (obligatorio) en cada uno de los ejercicios de modelado de hello es demasiado**excluir** Hola etiquetas innecesarias para hello otros problemas de dos y cualquier otro **destino pérdidas**. Por ejemplo, cuando se usa la clasificación binaria, usar etiqueta hello **superpuesto** y excluir los campos de hello **sugerencia\_clase**, **sugerencia\_cantidad**, y **total\_cantidad**. Hola este último se pagan de pérdidas de destino ya que implican sugerencia Hola.
> 
> tooexclude las columnas innecesarias o pérdidas de destino, puede usar hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo o hello [editar metadatos] [ edit-metadata]. Para obtener más información, consulte las páginas de referencia de [Seleccionar columnas de conjunto de datos][select-columns] y [Editar metadatos][edit-metadata].
> 
> 

## <a name="mldeploy"></a>Implementación de modelos en Aprendizaje automático de Azure
Cuando el modelo está listo, puede implementar fácilmente como un servicio web directamente desde el experimento de Hola. Para obtener más información sobre la implementación de servicios web de Aprendizaje automático de Azure, vea [Implementación de un servicio web de Aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy un nuevo servicio web, debe:

1. Crear un experimento de puntuación.
2. Implementar el servicio web de Hola.

toocreate una puntuación experimentar de un **finalizado** experimento de entrenamiento, haga clic en **crear EXPERIMENTO de puntuación** en la barra de acción inferior de Hola.

![Puntuación de Azure][18]

Aprendizaje automático de Azure intentará toocreate un experimento de puntuación en función de los componentes de hello del experimento de entrenamiento de Hola. En concreto, hará lo siguiente:

1. Guardar modelo entrenado hello y quite los módulos de entrenamiento del modelo de Hola.
2. Identificar un valor lógico **puerto de entrada** toorepresent Hola esperaba el esquema de datos de entrada.
3. Identificar un valor lógico **puerto de salida** esquema de salida del servicio de toorepresent hello web esperado.

Cuando se crea el experimento de puntuación de hello, revisarlo y asegúrese de ajustar según sea necesario. Un ajuste típico es el conjunto de datos de entrada de hello tooreplace o consulta con uno que excluye los campos de etiqueta, ya estos no estarán disponibles cuando se llama servicio de Hola. También es que un tamaño de hello tooreduce buenas prácticas de hello entrada tooa de conjunto de datos o de consultas pocos registros, suficiente esquema de entrada tooindicate Hola. Para el puerto de salida de hello, es común tooexclude entrados todos los campos y solo se incluyen hello **puntuación de etiquetas** y **probabilidades con puntuación** Hola Hola de salida [seleccionar columnas de conjunto de datos ] [ select-columns] módulo.

Se proporciona un ejemplo experimento de puntuación en hello siguiente ilustración. Cuando esté listo toodeploy, haga clic en hello **publicar servicio WEB** botón de barra de acción de hello inferior.

![Publicación de Aprendizaje automático de Azure][11]

## <a name="summary"></a>Resumen
toorecap lo que hemos realizado en este tutorial del tutorial, ha creado un entorno de ciencia de datos de Azure, ha trabajado con un gran conjunto de datos público, si vamos a través del proceso de ciencia de datos de equipo, todas las forma de Hola de entrenamiento de toomodel de adquisición de datos, de hello y, a continuación, toohello la implementación de un servicio web de aprendizaje automático de Azure.

### <a name="license-information"></a>Información de licencia
En este tutorial de ejemplo y sus elementos notebook(s) IPython y secuencias de comandos que se comparten por Microsoft bajo licencia MIT de Hola. Compruebe archivo LICENSE.txt de hello directorio de hello del código de ejemplo de Hola en GitHub para obtener más detalles.

## <a name="references"></a>Referencias
•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)  
•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
