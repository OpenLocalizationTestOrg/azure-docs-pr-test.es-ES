---
title: "aaaBuild e implementar un modelo de aprendizaje automático mediante SQL Server en una máquina virtual de Azure | Documentos de Microsoft"
description: "Tecnología y procesos de análisis avanzado en acción"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>Hola proceso de ciencia de datos de equipo en acción: uso de SQL Server
En este tutorial, guían en proceso de Hola de creación e implementación de un modelo de aprendizaje automático mediante SQL Server y un conjunto de datos disponible públicamente--hello [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos. procedimiento de Hello sigue un flujo de trabajo de ciencia de datos estándar: introducir y explorar los datos de hello, ingeniero de aprendizaje de toofacilitate de características, a continuación, generar e implementar un modelo.

## <a name="dataset"></a>Descripción del conjunto de datos NYC Taxi Trip
Hola datos NYC Taxi recorridos es aproximadamente 20GB de archivos comprimidos de CSV (sin comprimir de ~ 48GB), que incluye más de 173 millones hello y viajes individuales puntuación de pago para cada recorrido. Cada registro de ida y vuelta incluye ubicación de entrega y recogida de Hola y tiempo, hack anonimizado (controlador) número de licencia y número medallion (identificador único del taxi). datos de Hello cubre todos los viajes y en el año de hello 2013 y se proporcionan en hello siguiendo dos conjuntos de datos de cada mes:

1. Hola 'trip_data' CSV contiene los detalles de ida y vuelta, como el número de los pasajeros, recogida y puntos de caída, duración de ida y vuelta y duración del viaje. Estos son algunos registros de ejemplo:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hello 'trip_fare' CSV contiene detalles de tarifa de Hola de pago para cada recorrido, como tipo de pago, cantidad de tarifa, suplemento e impuestos, sugerencias y peajes y cantidad total de Hola de pago. Estos son algunos registros de ejemplo:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

recorridos de toojoin de clave única de Hello\_datos y recorridos\_tarifa se compone de campos de hello: medallion, prueba\_licencia y recogida\_fecha y hora.

## <a name="mltasks"></a>Ejemplos de tareas de predicción
Se formulará tres problemas de predicción basándose en hello *sugerencia\_cantidad*, a saber:

1. Clasificación binaria: permite predecir si se pagó una propina tras una carrera, o no; es decir, un valor de *tip\_amount* mayor que 0 $ es un ejemplo positivo, mientras que un valor de *tip\_amount* de 0 $ es un ejemplo negativo.
2. Clasificación multiclase: intervalo de hello toopredict de sugerencia de pago para recorridos de Hola. Se divide hello *sugerencia\_cantidad* en cinco bandejas o clases:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Tarea de regresión: cantidad de hello toopredict de sugerencia de pago para un recorrido.  

## <a name="setup"></a>Configurar el entorno de ciencia de análisis avanzado de hello datos de Azure
Como puede ver en hello [el entorno de su Plan](machine-learning-data-science-plan-your-environment.md) guía, hay varios toowork de opciones con conjunto de datos de Nueva York Taxi viajes de hello en Azure:

* Trabajar con datos de hello en blobs de Azure, a continuación, modelo de aprendizaje automático de Azure
* Cargar datos de hello en una base de datos de SQL Server, a continuación, modelo de aprendizaje automático de Azure

En este tutorial se indicará la importación masiva paralelas de hello tooa de datos SQL Server, exploración de datos, la característica de ingeniería y hacia abajo de muestreo utilizando SQL Server Management Studio, así como usar el Bloc de notas de IPython. Los [scripts de ejemplo](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) y [blocs de notas de IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) se comparten en GitHub. Un toowork de Bloc de notas de IPython de ejemplo con datos de hello en blobs de Azure también está disponible en hello misma ubicación.

tooset del entorno de ciencia de datos de Azure:

1. [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md)
2. [Creación de un área de trabajo de Aprendizaje automático de Azure](machine-learning-create-workspace.md)
3. [Aprovisione una máquina virtual de ciencia de datos](machine-learning-data-science-setup-sql-server-virtual-machine.md), que proporcionará un servidor de SQL Server y un servidor de Notebook de IPython.
   
   > [!NOTE]
   > las secuencias de comandos de ejemplo de Hola y notas de IPython será tooyour descargado ciencia de datos virtual machine durante el proceso de instalación de Hola. Cuando finalice el Hola script posterior a la instalación de VM, ejemplos de hello estarán en la biblioteca de documentos de la máquina virtual:  
   > 
   > * Scripts de ejemplo: `C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Blocs de notas de IPython de ejemplo: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   where `<user_name>` es el nombre de inicio de sesión de Windows de la máquina virtual. Nos referiremos a carpetas de ejemplo de toohello como **secuencias de comandos de ejemplo** y **ejemplo blocs de notas de IPython**.
   > 
   > 

En función de tamaño del conjunto de datos de hello, ubicación de origen de datos y entorno de destino de Azure seleccionado hello, este escenario es similar demasiado[escenario \#5: SQL Server en VM de Azure de destino de conjunto de datos grande en un archivos locales,](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Obtener Hola datos de origen pública
Hola tooget [NYC Taxi viajes](http://www.andresmh.com/nyctaxitrips/) conjunto de datos desde su ubicación pública, puede usar cualquiera de los métodos de hello descritos en [tooand de mover los datos desde el almacenamiento de blobs de Azure](machine-learning-data-science-move-azure-blob.md) toocopy Hola datos tooyour nueva máquina virtual.

datos de hello toocopy con AzCopy:

1. Inicie sesión en la máquina virtual (VM) de tooyour
2. Crear un nuevo directorio en el disco de datos de la máquina virtual de hello (Nota: no use Hola disco temporal que se incluye con hello máquina virtual como un disco de datos).
3. En una ventana del símbolo del sistema, ejecute hello después de la línea de comandos de Azcopy, reemplazando < path_to_data_folder > con la carpeta de datos creada en (2):
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    Cuando se completa el Hola AzCopy, un total de 24 zip archivos CSV (12 de ida y vuelta\_datos y 12 para recorridos\_tarifa) debe estar en la carpeta de datos de Hola.
4. Descomprimir archivos de hello descargado. Tenga en cuenta carpeta Hola donde residen los archivos de hello sin comprimir. Esta carpeta será la que se hace referencia tooas Hola < ruta de acceso\_a\_datos\_archivos\>.

## <a name="dbload"></a>Importación masiva de datos en una base de datos de SQL Server
Hello rendimiento de carga/transferir grandes cantidades de base de datos SQL de tooan de datos y las consultas posteriores se puede mejorar mediante el uso de *Partitioned Tables and vistas*. En esta sección, se sigue las instrucciones de hello descritas en [paralelo masiva datos utilizando SQL partición de tablas de importación](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate un nueva base de datos y cargar Hola datos en tablas con particiones en paralelo.

1. Iniciar una sesión en tooyour VM, **SQL Server Management Studio**.
2. Conéctese con la autenticación de Windows.
   
    ![Conexión SSMS][12]
3. Si todavía no ha cambiado el modo de autenticación de SQL Server de hello ni crea un nuevo usuario de inicio de sesión SQL, abra el archivo de script de Hola denominado **cambiar\_auth.sql** en hello **secuencias de comandos de ejemplo** carpeta. Cambiar el nombre de usuario predeterminado de Hola y la contraseña. Haga clic en **! Ejecutar** en secuencia de comandos de hello barra de herramientas toorun Hola.
   
    ![Ejecutar script][13]
4. Comprobar o cambiar Hola se almacenará la base de datos y registro tooensure carpetas predeterminado que recién creado bases de datos en un disco de datos de SQL Server. imagen de VM de SQL Server de Hola que está optimizado para cargas de almacén de datos está preconfigurado con discos de datos y de registro. Si la máquina virtual no incluía un disco de datos y agregar nuevos discos duros virtuales durante Hola proceso de configuración de máquina virtual, cambie las carpetas predeterminadas hello como sigue:
   
   * Nombre de SQL Server contextual Hola Hola dejado el panel y haga clic en **propiedades**.
     
       ![Propiedades de SQL Server][14]
   * Seleccione **configuración de base de datos** de hello **seleccionar una página** lista toohello izquierda.
   * Comprobar o cambiar hello **ubicaciones predeterminadas de la base de datos** toohello **disco de datos** ubicaciones de su elección. Esto es donde nuevas bases de datos residen si creado con la configuración de ubicación predeterminada de Hola.
     
       ![Valores predeterminados de Base de datos SQL][15]  
5. toocreate una nueva base de datos y un conjunto de grupos de archivos toohold Hola tablas con particiones, abra el script de ejemplo de Hola **crear\_db\_default.sql**. script de Hola creará una nueva base de datos denominada **TaxiNYC** y 12 grupos de archivos en la ubicación de datos predeterminada de Hola. Cada uno de los grupos de archivos contendrá un mes de datos de trip\_data y trip\_fare. Modifique el nombre de la base de datos de hello, si lo desea. Haga clic en **! Ejecutar** secuencia de comandos de toorun Hola.
6. A continuación, cree dos tablas de partición, uno para el recorrido de hello\_datos y otro para el recorrido de hello\_tarifa. Abra el script de ejemplo de Hola **crear\_con particiones\_table.sql**, que:
   
   * Crear una partición función toosplit Hola de datos por mes.
   * Crear un toomap de esquema de partición datos tooa otro grupo de archivos de cada mes.
   * Crear el esquema de partición de dos tablas con particiones toohello asignada: **nyctaxi\_recorridos** contendrá recorridos hello\_datos y **nyctaxi\_tarifa** contendrá recorridos Hola \_resultados son los datos.
     
     Haga clic en **! Ejecutar** toorun Hola script y crear tablas con particiones de Hola.
7. Hola **secuencias de comandos de ejemplo** carpeta, hay dos scripts de PowerShell de ejemplo proporcionan toodemonstrate importaciones por lotes paralela tooSQL servidor de tablas de datos.
   
   * **BCP\_paralelo\_generic.ps1** es una secuencia de comandos genérica tooparallel importación masiva de datos en una tabla. Modificar variables de entrada y de destino a esta Hola de tooset de secuencia de comandos como se indica en las líneas de comentario de hello en el script de Hola.
   * **BCP\_paralelo\_nyctaxi.ps1** es una versión preconfigurada de script genérico de Hola y puede ser tootooload usa ambas tablas para los datos de Nueva York Taxi viajes Hola.  
8. Menú contextual hello **bcp\_paralelo\_nyctaxi.ps1** nombre del script y haga clic en **editar** tooopen en PowerShell. Hola de revisión preestablecido variables y modificar el nombre de base de datos seleccionada tooyour correspondiente, carpeta de datos de entrada, carpeta de registro de destino y archivos de formato de ejemplo de las rutas de acceso toohello **nyctaxi_trip.xml** y **nyctaxi\_ Fare.XML** (proporcionadas en hello **secuencias de comandos de ejemplo** carpeta).
   
    ![Datos de importación en bloque][16]
   
    También puede seleccionar el modo de autenticación de hello, el valor predeterminado es autenticación de Windows. Haga clic en la flecha verde de Hola en hello toorun de barra de herramientas. script de Hola iniciará 24 operaciones de importación masiva en paralelo, 12 para cada tabla con particiones. Puede supervisar Hola progreso de la importación de datos, abra la carpeta de datos predeterminada de hello SQL Server como conjunto anterior.
9. informes de script de PowerShell de Hola Hola horas inicio y finalización. Cuando todas las importaciones que completar de forma masiva, se registrará Hola hora de finalización. Compruebe Hola destino registro carpeta tooverify importaciones masivas de hello tuvieron éxito, es decir, errores no notifican en la carpeta de registro de destino de Hola.
10. La base de datos ya está preparada para la exploración, diseño de características y otras operaciones que desee. Puesto que las tablas de hello tienen particiones según toohello **recogida\_datetime** campo, las consultas que incluyen **recogida\_datetime** condiciones en hello  **DONDE** cláusula se beneficiará de esquema de partición de Hola.
11. En **SQL Server Management Studio**, explorar el script de ejemplo de Hola proporciona **ejemplo\_queries.sql**. toorun cualquiera de las consultas de ejemplo de Hola, resaltado Hola líneas de consulta, a continuación, haga clic en **! Ejecutar** en la barra de herramientas de Hola.
12. Hola datos NYC Taxi viajes se carga en dos tablas independientes. operaciones de combinación de tooimprove, se recomienda encarecidamente tablas de hello tooindex. script de ejemplo de Hola **crear\_con particiones\_index.sql** crea índices con particiones en la clave de combinación compuesto de hello **medallion, prueba\_licencia y recogida\_datetime**.

## <a name="dbexplore"></a>Exploración de datos e ingeniería de características en SQL Server
En esta sección, se llevará a cabo generación de exploración y la característica de datos mediante la ejecución de consultas SQL directamente en hello **SQL Server Management Studio** usando la base de datos de SQL Server de hello creado anteriormente. Un script de ejemplo denominado **ejemplo\_queries.sql** se proporciona en hello **secuencias de comandos de ejemplo** carpeta. Modificar el nombre de base de datos de hello script toochange hello, si es diferente del valor predeterminado de hello: **TaxiNYC**.

En este ejercicio, se hará lo siguiente:

* Conectar demasiado**SQL Server Management Studio** mediante autenticación de Windows o con nombre de inicio de sesión SQL hello y autenticación de SQL y una contraseña.
* Explorar distribuciones de datos de algunos campos en diferentes ventanas de tiempo.
* Investigue la calidad de los datos de los campos de longitud y latitud de Hola.
* Generar etiquetas de clasificación multiclase y binaria basándose en hello **sugerencia\_cantidad**.
* Generar características y calcular o comparar distancias de carreras.
* Combinar Hola dos tablas y extraer una muestra aleatoria que será usado toobuild modelos.

Cuando esté listo tooproceed tooAzure aprendizaje automático, puede:  

1. Guardar Hola final SQL consulta tooextract y ejemplo Hola datos y copiar y pegar Hola consulta directamente en un [importar datos] [ import-data] módulo aprendizaje automático de Azure, o
2. Hola muestreada se conservan y datos de ingeniería que tiene previsto toouse para crear una nueva base de datos de modelo de tabla y usar nueva tabla de hello en hello [importar datos] [ import-data] módulo aprendizaje automático de Azure.

En esta sección se guardará Hola consulta final tooextract y Hola datos de ejemplo. segundo método de Hola se muestra en hello [exploración de datos y de ingeniería de características en el Bloc de notas de IPython](#ipnb) sección.

Para una comprobación rápida del número de Hola de filas y columnas de hello en tablas se rellenaron anteriormente con la importación masiva paralelas,

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Exploración: distribución de carreras por licencia
Este ejemplo identifica medallion Hola (números de taxi) con más de 100 viajes dentro de un período de tiempo determinado. consulta de Hola se beneficiaría de acceso a la tabla con particiones de hello porque está condicionado por esquema de partición de Hola de **recogida\_datetime**. Consultar el conjunto de datos completo de hello también hará que el uso de la tabla con particiones de Hola o examen de índice.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploración: distribución de carreras por medallion y hack_license
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Evaluación de la calidad de los datos: comprobar los registros con longitud o latitud incorrectas
En este ejemplo se investiga si alguno de los campos de longitud o latitud de Hola o contiene un valor no válido (grados Radián deben estar entre -90 y 90), o tener (0, 0) coordenadas.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploración: distribución de carreras con propinas frente a sin propinas
Este ejemplo busca el número de Hola de viajes que se han superpuesto frente a no superpuesto en un momento determinado período (o en el conjunto de datos completo de hello si cubriendo año completo hello) de. Esta distribución refleja Hola etiqueta binario distribución toobe que más adelante se usa para el modelo de clasificación binaria.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Exploración: distribución por intervalos y clases de propinas
Este ejemplo calcula distribución Hola de intervalos de sugerencia en un momento determinado período (o en el conjunto de datos completo de hello si relativo Hola completa año). Se trata de distribución de Hola de clases de etiqueta de Hola que usará más adelante para el modelado de clasificación multiclase.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Exploración: calcular y comparar la distancia de la carrera
Este ejemplo convierte la longitud de recogida y entrega de Hola y geografía de latitud tooSQL señala, calcula la distancia de viaje hello mediante diferencia de puntos de geography SQL y devuelve una muestra aleatoria de resultados de hello para la comparación. ejemplo de Hola limita los resultados de hello toovalid coordina únicamente con la consulta de evaluación de calidad Hola datos cubierto anteriormente.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Diseño de características en consultas SQL
Hola etiqueta geography y generación de conversión exploración también pueden ser consultas toogenerate usa etiquetas/características mediante la eliminación de hello contar parte. Se proporcionan ejemplos SQL de ingeniería de características adicionales en hello [exploración de datos y de ingeniería de características en el Bloc de notas de IPython](#ipnb) sección. Resulta más eficaz toorun Hola característica generación las consultas en el conjunto de datos completo de Hola o un gran subconjunto de dicho tipo mediante consultas SQL que se ejecutan directamente en la instancia de base de datos de SQL Server de Hola. se pueden ejecutar consultas de Hello en **SQL Server Management Studio**, Bloc de notas de IPython o cualquier herramienta o entorno de desarrollo que pueden tener acceso a Hola base de datos local o remotamente.

#### <a name="preparing-data-for-model-building"></a>Preparación de los datos para la creación del modelo
Hola de combinaciones de consulta siguiente Hello **nyctaxi\_recorridos** y **nyctaxi\_tarifa** tablas, genera una etiqueta de clasificación binaria **superpuesto**, etiqueta de clasificación multiclase **sugerencia\_clase**y extrae una muestra aleatoria de 1% del conjunto de datos combinado Hola completa. Esta consulta se puede copiar y pegar directamente en hello [estudio de aprendizaje automático de Azure](https://studio.azureml.net) [importar datos] [ import-data] módulo de recopilación de datos directas de base de datos de SQL Server de Hola instancia de Azure. consulta de Hello excluye los registros con incorrecto (0, 0) coordenadas.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Exploración de datos e ingeniería de características en el Bloc de notas de IPython
En esta sección, se llevará a cabo una exploración de datos y la generación de característica mediante consultas de Python y SQL contra Hola de base de datos de SQL Server creado anteriormente. Un bloc de notas de IPython de ejemplo denominado **machine-Learning-data-science-process-sql-story.ipynb** se proporciona en hello **ejemplo blocs de notas de IPython** carpeta. Este bloc de notas también está disponible en [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

Hola recomendada secuencia cuando se trabaja con grandes cantidades de datos es la siguiente de hello:

* Leer en una pequeña muestra de datos de hello en un marco de datos en memoria.
* Realizar algunas visualizaciones y exploraciones con los datos de ejemplo de Hola.
* Experimente con ingeniería de característica con hello los datos de ejemplo.
* Para la exploración de datos mayor, manipulación de datos y la ingeniería de característica, utilice Python tooissue SQL consultas directamente en la base de datos de SQL Server de Hola Hola VM de Azure.
* Decidir toouse de tamaño de ejemplo de Hola para una compilación de modelo de aprendizaje automático de Azure.

Cuando esté listo tooproceed tooAzure aprendizaje automático, es posible que ya sea:  

1. Guardar Hola final SQL consulta tooextract y ejemplo Hola datos y copiar y pegar Hola consulta directamente en un [importar datos] [ import-data] módulo aprendizaje automático de Azure. Este método se muestra en hello [generar modelos de aprendizaje automático de Azure](#mlmodel) sección.    
2. Conservar Hola muestreada y los datos de ingeniería piensa toouse para compilar en una nueva tabla de base de datos de modelo, utilice la nueva tabla de Hola Hola [importar datos] [ import-data] módulo.

siguiente Hola es unos exploración de datos, visualización de datos y ejemplos de ingeniería de característica. Para obtener más ejemplos, vea el Bloc de notas del IPython de SQL de ejemplo de Hola Hola **ejemplo blocs de notas de IPython** carpeta.

#### <a name="initialize-database-credentials"></a>Inicializar las credenciales de la base de datos
Inicializar la configuración de conexión de base de datos en hello siguientes variables:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Crear conexiones de base de datos
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Informe con el número de filas y columnas en la tabla nyctaxi_trip
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de filas = 173179759  
* Número total de columnas = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Lectura de un pequeño datos de ejemplo de Hola base de datos de SQL Server
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tabla de ejemplo de Hola de tiempo tooread es 6.492000 segundos  
Número de filas y columnas recuperadas = (84952, 21)

#### <a name="descriptive-statistics"></a>Estadísticas descriptivas
Ahora están datos de hello muestreada tooexplore listo. Empezaremos con examinando Estadísticas descriptivas para hello **recorridos\_distancia** (o cualquier otro) Field (s):

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Visualización: ejemplo de diagrama de caja
A continuación, veremos caja Hola para Hola de ida y vuelta distancia toovisualize hello cuantiles

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagrama 1][1]

#### <a name="visualization-distribution-plot-example"></a>Visualización: ejemplo de diagrama de distribución
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagrama 2][2]

#### <a name="visualization-bar-and-line-plots"></a>Visualización: diagramas de barras y líneas
En este ejemplo, hemos discretizar distancia de viaje hello en cinco cubos y visualizar Hola discretizar los resultados.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Podemos trazar Hola por encima de la distribución de la Papelera de una barra o trazado como a continuación de línea

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagrama 3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagrama 4][4]

#### <a name="visualization-scatterplot-example"></a>Visualización: ejemplo de gráfico de dispersión
Se muestra el gráfico de dispersión entre **recorridos\_tiempo\_en\_s** y **recorridos\_distancia** toosee si hay alguna correlación

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagrama 6][6]

De igual forma podemos comprobar relación Hola entre **velocidad\_código** y **recorridos\_distancia**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagrama 8][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Hola Submuestreo datos en SQL
Al preparar los datos de generación modelo [estudio de aprendizaje automático de Azure](https://studio.azureml.net), o bien puede decidir hello **toouse de consultas SQL directamente en el módulo de importación de datos de hello** o conservarlos Hola diseñados y muestrear datos de una tabla nueva, que puede usar en hello [importar datos] [ import-data] módulo con un sencillo **seleccione * FROM < su\_nueva\_tabla\_nombre >**.

En esta sección que se creará un nuevo hello toohold de tabla muestrea y datos de ingeniería. Se proporciona un ejemplo de una consulta SQL directo para la compilación del modelo en hello [exploración de datos y de ingeniería de características de SQL Server](#dbexplore) sección.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Crear una tabla de ejemplo y rellenar con % 1 de tablas unidas de Hola. Quite la tabla primero si existe.
En esta sección, se combinan tablas de hello **nyctaxi\_recorridos** y **nyctaxi\_tarifa**, extraer una muestra aleatoria de 1% y conservar los datos de hello muestreada en un nuevo nombre de tabla  **nyctaxi\_una\_por ciento**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Exploración de datos mediante consultas SQL en Blocs de notas de IPython
En esta sección, exploramos distribuciones de datos utilizando los datos de 1% muestreada Hola que se guardan en la nueva tabla de hello que hemos creado anteriormente. Tenga en cuenta que se pueden realizar exploraciones similar mediante tablas originales de hello, utilizando opcionalmente **TABLESAMPLE** toolimit de exploración de hello muestra o limitando Hola da como resultado tooa dado el período de tiempo mediante hello **recogida \_datetime** particiones, como se muestra en hello [exploración de datos y de ingeniería de características de SQL Server](#dbexplore) sección.

#### <a name="exploration-daily-distribution-of-trips"></a>Exploración: distribución diaria de carreras
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploración: distribución de carreras por licencia
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Generación de características mediante consultas SQL en Blocs de notas de IPython
En esta sección se generará nuevas etiquetas y en funcionamiento en la tabla de ejemplo de 1% de hello características directamente mediante consultas SQL, hemos creado en la sección anterior de Hola.

#### <a name="label-generation-generate-class-labels"></a>Generación de etiquetas: generar etiquetas de clase
En el siguiente ejemplo de Hola, se generan dos conjuntos de toouse de etiquetas para el modelado:

1. Etiquetas de clase binaria **tipped** (que predecirán si se dará propina)
2. Las etiquetas multiclase **sugerencia\_clase** (predecir bin de sugerencia de Hola o intervalo)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Ingeniería de características: características de recuento de columnas de categorías
En este ejemplo se transforma un campo de categoría en un campo numérico si se reemplaza cada categoría con el recuento de Hola de sus repeticiones en datos Hola.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Ingeniería de características: características de discretización de columnas numéricas
En este ejemplo se transforma un campo numérico continuo en intervalos de categoría preestablecidos; por ejemplo, la transformación de un campo numérico en un campo de categoría.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Ingeniería de características: extraer las características de ubicación a partir de una latitud o longitud decimal
Este ejemplo divide representación decimal de Hola de un campo o la latitud en varios campos de región de granularidad diferente, como por ejemplo, país, ciudad, ciudad, bloque, etcetera. Tenga en cuenta que Hola geográfica-campos nuevos no asignados tooactual ubicaciones. Para obtener información sobre la asignación de ubicaciones de códigos geográficos, consulte [Servicios REST de Mapas de Bing](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Comprobar el formulario final de Hola de tabla de caracterizará Hola
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Ahora estamos listos tooproceed toomodel creación e implementación de modelo en [aprendizaje automático de Azure](https://studio.azureml.net). datos de Hello están listos para cualquiera de los problemas de predicción de hello identificados anteriormente, a saber:

1. Clasificación binaria: toopredict o no se pagó una sugerencia para un recorrido.
2. Clasificación multiclase: intervalo de hello toopredict de sugerencia de pago, según toohello clases definidas previamente.
3. Tarea de regresión: cantidad de hello toopredict de sugerencia de pago para un recorrido.  

## <a name="mlmodel"></a>Creación de modelos en Aprendizaje automático de Azure
toobegin Hola modelado ejercicio, inicie sesión en el área de trabajo de tooyour aprendizaje automático de Azure. Si aún no ha creado un área de trabajo de aprendizaje automático, consulte [Creación y uso compartido de un área de trabajo de Azure Machine Learning](machine-learning-create-workspace.md).

1. tooget a trabajar con aprendizaje automático de Azure, consulte [¿qué es el estudio de aprendizaje automático de Azure?](machine-learning-what-is-ml-studio.md)
2. Inicie sesión demasiado[estudio de aprendizaje automático de Azure](https://studio.azureml.net).
3. página de inicio de Studio Hola proporciona una gran cantidad de información, vídeos, tutoriales, vínculos toohello referencia de módulos y otros recursos. Para obtener más información acerca de aprendizaje automático de Azure, consulte hello [centro de documentación de aprendizaje automático](https://azure.microsoft.com/documentation/services/machine-learning/).

Un experimento de entrenamiento típico consta de siguiente hello:

1. Crear un experimento **+NUEVO** .
2. Obtener datos de hello tooAzure aprendizaje automático.
3. Preprocesar, transformar y manipular datos Hola según sea necesario.
4. Generar características según sea necesario.
5. Dividir los datos de hello en conjuntos de datos de entrenamiento / / pruebas de validación (o tiene conjuntos de datos independiente para cada uno).
6. Seleccionar algoritmos función hello toosolve problema de aprendizaje de aprendizaje automático de uno o más. Por ejemplo: clasificación binaria, clasificación multiclase, regresión.
7. Entrenar uno o varios modelos utilizando el conjunto de datos de entrenamiento de Hola.
8. Puntuación Hola de conjunto de datos de validación utilizando modelos entrenados Hola.
9. Evaluar Hola modelos toocompute Hola métricas pertinente para hello problema de aprendizaje.
10. Ajustar los modelos de Hola y Hola seleccione mejor modelo toodeploy.

En este ejercicio, hemos ya explorar e ingeniería datos hello en SQL Server y decidido tooingest de tamaño de ejemplo de Hola en aprendizaje automático de Azure. toobuild uno o varios de los modelos de predicción de hello decidimos:

1. Obtener datos de hello tooAzure aprendizaje automático con hello [importar datos] [ import-data] módulo, disponibles en hello **datos de entrada y salida** sección. Para obtener más información, vea hello [importar datos] [ import-data] página de referencia de módulo.
   
    ![Importar datos de Azure Machine Learning][17]
2. Seleccione **base de datos de SQL Azure** como hello **origen de datos** en hello **propiedades** panel.
3. Escriba el nombre DNS de base de datos de Hola Hola **el nombre del servidor de base de datos** campo. Formato: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Escriba hello **nombre de base de datos** en el campo correspondiente Hola.
5. Escriba hello **nombre de usuario SQL** Hola ** aqccount nombre de usuario y la contraseña de Hola Hola **contraseña de cuenta de usuario de servidor**.
6. Activar la opción **Aceptar cualquier certificado de servidor** .
7. Hola **consulta de base de datos** editar el área de texto, pegue la consulta de Hola que extrae Hola necesarios campos (incluidos los campos calculados, como las etiquetas de hello) de la base de datos y el detalle de ejemplos de tamaño de la muestra de Hola datos toohello deseado.

Un ejemplo de un experimento de clasificación binaria leer los datos directamente desde la base de datos de SQL Server de hello es en hello siguiente ilustración. Se pueden construir experimentos similares para problemas de clasificación multiclase y de regresión.

![Entrenar Azure Machine Learning][10]

> [!IMPORTANT]
> Hola, extracción de datos de modelado y realizando un muestreo ejemplos de consultas que se proporcionan en las secciones anteriores, **todas las etiquetas de ejercicios de modelado de hello tres se incluyen en la consulta de hello**. Un paso importante (obligatorio) en cada uno de los ejercicios de modelado de hello es demasiado**excluir** Hola etiquetas innecesarias para hello otros problemas de dos y cualquier otro **destino pérdidas**. Para p. ej., cuando se usa la clasificación binaria, use etiqueta hello **superpuesto** y excluir los campos de hello **sugerencia\_clase**, **sugerencia\_cantidad**, y **total\_cantidad**. Hola este último se pagan de pérdidas de destino ya que implican sugerencia Hola.
> 
> las columnas innecesarias tooexclude o pérdidas de destino, puede usar hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo o hello [editar metadatos] [ edit-metadata]. Para obtener más información, consulte las páginas de referencia de [Seleccionar columnas de conjunto de datos][select-columns] y [Editar metadatos][edit-metadata].
> 
> 

## <a name="mldeploy"></a>Implementación de modelos en Aprendizaje automático de Azure
Cuando el modelo está listo, puede implementar fácilmente como un servicio web directamente desde el experimento de Hola. Para más información sobre la implementación de servicios web Azure Machine Learning, vea [Implementar un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy un nuevo servicio web, debe:

1. Crear un experimento de puntuación.
2. Implementar el servicio web de Hola.

toocreate una puntuación experimentar de un **finalizado** experimento de entrenamiento, haga clic en **crear EXPERIMENTO de puntuación** en la barra de acción inferior de Hola.

![Puntuación de Azure][18]

Aprendizaje automático de Azure intentará toocreate un experimento de puntuación en función de los componentes de hello del experimento de entrenamiento de Hola. En concreto, hará lo siguiente:

1. Guardar modelo entrenado hello y quite los módulos de entrenamiento del modelo de Hola.
2. Identificar un valor lógico **puerto de entrada** toorepresent Hola esperaba el esquema de datos de entrada.
3. Identificar un valor lógico **puerto de salida** esquema de salida del servicio de toorepresent hello web esperado.

Cuando se crea el experimento de puntuación de hello, revisarlo y ajustar según sea necesario. Un ajuste típico es el conjunto de datos de entrada de hello tooreplace o consulta con uno que excluye los campos de etiqueta, ya estos no estarán disponibles cuando se llama servicio de Hola. También es que un tamaño de hello tooreduce buenas prácticas de hello entrada tooa de conjunto de datos o de consultas pocos registros, suficiente esquema de entrada tooindicate Hola. Para el puerto de salida de hello, es común tooexclude entrados todos los campos y solo se incluyen hello **puntuación de etiquetas** y **probabilidades con puntuación** Hola Hola de salida [seleccionar columnas de conjunto de datos ] [ select-columns] módulo.

Un ejemplo de experimento de puntuación es en hello siguiente ilustración. Cuando esté listo toodeploy, haga clic en hello **publicar servicio WEB** botón de barra de acción de hello inferior.

![Publicar Azure Machine Learning][11]

toorecap, en este tutorial tutorial, ha creado un entorno de ciencia de datos de Azure, ha trabajado con un conjunto de datos público grande todas las forma de Hola de toomodel de adquisición de datos de entrenamiento y la implementación de un servicio web de aprendizaje automático de Azure.

### <a name="license-information"></a>Información de licencia
En este tutorial de ejemplo y sus elementos notebook(s) IPython y secuencias de comandos que se comparten por Microsoft bajo licencia MIT de Hola. Compruebe archivo LICENSE.txt de hello directorio de hello del código de ejemplo de Hola en GitHub para obtener más detalles.

### <a name="references"></a>Referencias
•   [Página de descarga de NYC Taxi Trips de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)  
•   [FOILing NYC’s Taxi Trip Data de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•   [Estadísticas e investigación de la Comisión de taxis y limusinas de la Ciudad de Nueva York](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
