---
title: aaaUse ScaleR y SparkR con HDInsight de Azure | Documentos de Microsoft
description: Uso de ScaleR y SparkR con R Server y HDInsight
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="ab2b2-103">Combinación de ScaleR y SparkR en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ab2b2-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="ab2b2-104">Este artículo muestra cómo toopredict flight retrasos de llegada con un **ScaleR** Unidos a un modelo de regresión logística de los datos de retrasos de vuelos y previsiones meteorológicas con **SparkR**.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-104">This article shows how toopredict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="ab2b2-105">Este escenario muestra las capacidades de Hola de ScaleR para la manipulación de datos en Spark usado con Microsoft R Server para el análisis.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-105">This scenario demonstrates hello capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="ab2b2-106">combinación de Hola de estas tecnologías habilita características más recientes de tooapply hello en el procesamiento distribuido.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-106">hello combination of these technologies enables you tooapply hello latest capabilities in distributed processing.</span></span>

<span data-ttu-id="ab2b2-107">Aunque ambos paquetes se procesan en el motor de ejecución de Spark de Hadoop, se les impide compartir datos en memoria, ya que cada uno de ellos requiere sus correspondientes sesiones de Spark.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="ab2b2-108">Hasta que este problema se trata en una próxima versión del servidor de R, solución de hello es toomaintain sesiones de Spark no superpuestos y tooexchange datos a través de los archivos intermedios.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-108">Until this issue is addressed in an upcoming version of R Server, hello workaround is toomaintain non-overlapping Spark sessions, and tooexchange data through intermediate files.</span></span> <span data-ttu-id="ab2b2-109">instrucciones de Hello aquí muestran que estos requisitos son tooachieve sencillo.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-109">hello instructions here show that these requirements are straightforward tooachieve.</span></span>

<span data-ttu-id="ab2b2-110">Utilizamos un ejemplo aquí compartido inicialmente en una charla en estratos 2016 Mario Inchiosa y Roni Burd que también está disponible a través de seminario Web hello [creación de una plataforma escalable de ciencia de datos con R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). ejemplo de Hola usa SparkR toojoin Hola airlines conocido el conjunto de datos de retraso de llegada con los datos del tiempo en aeropuertos de partida y de llegada.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through hello webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). hello example uses SparkR toojoin hello well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="ab2b2-111">datos Hola Unidos, a continuación, se usan como modelo de regresión logística de entrada tooa ScaleR para predecir los retrasos en vuelos llegada.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-111">hello data joined is then used as input tooa ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="ab2b2-112">Hola tutorial de código se escribió originalmente para servidor de R que se ejecuta en Spark en un clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-112">hello code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="ab2b2-113">Pero el concepto de Hola de combinación de uso de Hola de SparkR y ScaleR en un script, también es válido en el contexto de Hola de entornos locales.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-113">But hello concept of mixing hello use of SparkR and ScaleR in one script is also valid in hello context of on-premises environments.</span></span> <span data-ttu-id="ab2b2-114">En la siguiente hello, se suponen un nivel intermedio de conocimientos de R y R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) biblioteca del servidor de R.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-114">In hello following, we presume an intermediate level of knowledge of R and R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="ab2b2-115">También presentamos el uso de [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) al recorrer este escenario.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="hello-airline-and-weather-datasets"></a><span data-ttu-id="ab2b2-116">Hola airline y previsiones meteorológicas conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="ab2b2-116">hello airline and weather datasets</span></span>

<span data-ttu-id="ab2b2-117">Hola **AirOnTime08to12CSV** airlines pública conjunto de datos contiene información acerca de llegada de vuelo y los detalles de partida para todos los vuelos comerciales en Estados Unidos, Hola de octubre de 1987 tooDecember 2012.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-117">hello **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within hello USA, from October 1987 tooDecember 2012.</span></span> <span data-ttu-id="ab2b2-118">Se trata de un conjunto de datos grande: hay casi 150 millones de registros en total.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="ab2b2-119">Es algo inferior a 4 GB desempaquetado.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="ab2b2-120">Está disponible de hello [archivos del gobierno de EE. UU.](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span><span class="sxs-lookup"><span data-stu-id="ab2b2-120">It is available from hello [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="ab2b2-121">Una forma más conveniente, está disponible como un archivo zip (AirOnTimeCSV.zip) que contiene un conjunto de 303 archivos CSV mensuales independientes de hello [repositorio de conjunto de datos de Revolution Analytics](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span><span class="sxs-lookup"><span data-stu-id="ab2b2-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from hello [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="ab2b2-122">efectos de hello toosee de tiempo de los retrasos de vuelos, también es necesario meteorológica hello en cada uno de los aeropuertos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-122">toosee hello effects of weather on flight delays, we also need hello weather data at each of hello airports.</span></span> <span data-ttu-id="ab2b2-123">Estos datos se pueden descargar como archivos zip en formato sin procesar, por mes, de hello [repositorio nacional oceánica y atmosférica administración](http://www.ncdc.noaa.gov/orders/qclcd/).</span><span class="sxs-lookup"><span data-stu-id="ab2b2-123">This data can be downloaded as zip files in raw form, by month, from hello [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="ab2b2-124">Para fines de Hola de este ejemplo, se extraen datos de tiempo de mayo de 2007: diciembre de 2012 y usan los archivos de datos por hora de hello en cada una de 68 cremalleras mensual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-124">For hello purposes of this example, we pull weather data from May 2007 – December 2012 and used hello hourly data files within each of hello 68 monthly zips.</span></span> <span data-ttu-id="ab2b2-125">archivos zip mensual de Hello también contienen una asignación (YYYYMMstation.txt) entre la estación meteorológica de hello ID (WBAN), que está asociado a (CallSign), de aeropuerto de Hola y Hola ajuste de zona horaria del aeropuerto a la hora UTC (zona horaria).</span><span class="sxs-lookup"><span data-stu-id="ab2b2-125">hello monthly zip files also contain a mapping (YYYYMMstation.txt) between hello weather station ID (WBAN), hello airport that it is associated with (CallSign), and hello airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="ab2b2-126">Toda esta información es necesaria al unirse con datos de retraso y previsiones meteorológicas airline Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-126">All of this information is needed when joining with hello airline delay and weather data.</span></span>

## <a name="setting-up-hello-spark-environment"></a><span data-ttu-id="ab2b2-127">Configuración de entorno de Spark Hola</span><span class="sxs-lookup"><span data-stu-id="ab2b2-127">Setting up hello Spark environment</span></span>

<span data-ttu-id="ab2b2-128">Hola primer paso es tooset el entorno de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-128">hello first step is tooset up hello Spark environment.</span></span> <span data-ttu-id="ab2b2-129">Empezaremos que señala el directorio toohello que contiene nuestro directorios de datos de entrada, creando un contexto de proceso Spark y crear una función de registro para la consola de toohello de registro informativo:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-129">We begin by pointing toohello directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging toohello console:</span></span>

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

<span data-ttu-id="ab2b2-130">A continuación se agregue "Spark_Home" ruta de acceso de búsqueda de toohello paquetes de R para que podemos usar SparkR e inicializar una sesión de SparkR:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-130">Next we add “Spark_Home” toohello search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a><span data-ttu-id="ab2b2-131">Preparación de los datos de tiempo de Hola</span><span class="sxs-lookup"><span data-stu-id="ab2b2-131">Preparing hello weather data</span></span>

<span data-ttu-id="ab2b2-132">los datos del tiempo tooprepare hello, se subconjunto columnas de toohello necesarias para el modelado:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-132">tooprepare hello weather data, we subset it toohello columns needed for modeling:</span></span> 

- <span data-ttu-id="ab2b2-133">"Visibility"</span><span class="sxs-lookup"><span data-stu-id="ab2b2-133">"Visibility"</span></span>
- <span data-ttu-id="ab2b2-134">"DryBulbCelsius"</span><span class="sxs-lookup"><span data-stu-id="ab2b2-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="ab2b2-135">"DewPointCelsius"</span><span class="sxs-lookup"><span data-stu-id="ab2b2-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="ab2b2-136">"RelativeHumidity"</span><span class="sxs-lookup"><span data-stu-id="ab2b2-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="ab2b2-137">"WindSpeed"</span><span class="sxs-lookup"><span data-stu-id="ab2b2-137">"WindSpeed"</span></span>
- <span data-ttu-id="ab2b2-138">"Altimeter"</span><span class="sxs-lookup"><span data-stu-id="ab2b2-138">"Altimeter"</span></span>

<span data-ttu-id="ab2b2-139">A continuación, se agregue un código de aeropuerto asociado estación meteorológica de Hola y convertir las medidas de Hola de tooUTC de hora local.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-139">Then we add an airport code associated with hello weather station and convert hello measurements from local time tooUTC.</span></span>

<span data-ttu-id="ab2b2-140">Comenzamos creando un código de aeropuerto archivo toomap Hola estación meteorológica (WBAN) información tooan.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-140">We begin by creating a file toomap hello weather station (WBAN) info tooan airport code.</span></span> <span data-ttu-id="ab2b2-141">Esta correlación se pudo obtener del archivo de asignación de hello incluido con los datos de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-141">We could get this correlation from hello mapping file included with hello weather data.</span></span> <span data-ttu-id="ab2b2-142">Por Hola de asignación *CallSign* (por ejemplo, LAX) en el archivo de datos de tiempo de hello campo demasiado*origen* en datos de hello airline.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-142">By mapping hello *CallSign* (for example, LAX) field in hello weather data file too*Origin* in hello airline data.</span></span> <span data-ttu-id="ab2b2-143">Sin embargo, se pasó toohave otra asignación de mano que se asigna *WBAN* demasiado*AirportID* (por ejemplo, 12892 para LAX) e incluye *zona horaria* que se ha guardado tooa Archivo CSV denominado "wban-a-aeropuerto-id-tz. CSV"que podemos usar.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-143">However, we just happened toohave another mapping on hand that maps *WBAN* too*AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved tooa CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="ab2b2-144">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-144">For example:</span></span>

| <span data-ttu-id="ab2b2-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="ab2b2-145">AirportID</span></span> | <span data-ttu-id="ab2b2-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="ab2b2-146">WBAN</span></span> | <span data-ttu-id="ab2b2-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="ab2b2-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="ab2b2-148">10685</span><span class="sxs-lookup"><span data-stu-id="ab2b2-148">10685</span></span> | <span data-ttu-id="ab2b2-149">54831</span><span class="sxs-lookup"><span data-stu-id="ab2b2-149">54831</span></span> | <span data-ttu-id="ab2b2-150">-6</span><span class="sxs-lookup"><span data-stu-id="ab2b2-150">-6</span></span>
| <span data-ttu-id="ab2b2-151">14871</span><span class="sxs-lookup"><span data-stu-id="ab2b2-151">14871</span></span> | <span data-ttu-id="ab2b2-152">24232</span><span class="sxs-lookup"><span data-stu-id="ab2b2-152">24232</span></span> | <span data-ttu-id="ab2b2-153">-8</span><span class="sxs-lookup"><span data-stu-id="ab2b2-153">-8</span></span>
| <span data-ttu-id="ab2b2-154">..</span><span class="sxs-lookup"><span data-stu-id="ab2b2-154">..</span></span> | <span data-ttu-id="ab2b2-155">..</span><span class="sxs-lookup"><span data-stu-id="ab2b2-155">..</span></span> | <span data-ttu-id="ab2b2-156">..</span><span class="sxs-lookup"><span data-stu-id="ab2b2-156">..</span></span>

<span data-ttu-id="ab2b2-157">archivos de Hello siguiente código lee cada de los datos del tiempo sin procesar por hora hello, subconjuntos toohello columnas requeridas, combina el archivo de asignación de estación meteorológica hello, ajusta hello las fechas de tooUTC de medidas y, a continuación, escribe una nueva versión de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-157">hello following code reads each of hello hourly raw weather data files, subsets toohello columns we need, merges hello weather station mapping file, adjusts hello date times of measurements tooUTC, and then writes out a new version of hello file:</span></span>

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a><span data-ttu-id="ab2b2-158">Hola airline y previsiones meteorológicas datos tooSpark tramas de datos de importación</span><span class="sxs-lookup"><span data-stu-id="ab2b2-158">Importing hello airline and weather data tooSpark DataFrames</span></span>

<span data-ttu-id="ab2b2-159">Ahora usamos hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) función hello de tooimport tiempo y airline tooSpark de datos tramas de datos.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-159">Now we use hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function tooimport hello weather and airline data tooSpark DataFrames.</span></span> <span data-ttu-id="ab2b2-160">Esta función, al igual que muchos otros métodos de Spark, se ejecuta de forma diferida, lo que significa que se pone en la cola para la ejecución pero no se ejecuta hasta que es necesario.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="ab2b2-161">Limpieza y transformación de datos</span><span class="sxs-lookup"><span data-stu-id="ab2b2-161">Data cleansing and transformation</span></span>

<span data-ttu-id="ab2b2-162">Después, realizamos algunas Liberador de espacio en los datos de hello airline que hemos importado toorename columnas.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-162">Next we do some cleanup on hello airline data we’ve imported toorename columns.</span></span> <span data-ttu-id="ab2b2-163">Solo mantener las variables de hello necesitadas y tiempos de salida programada hacia abajo toohello más cercano de combinación con datos de tiempo más recientes de Hola a la partida de tooenable de hora de ida y vuelta:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-163">We only keep hello variables needed, and round scheduled departure times down toohello nearest hour tooenable merging with hello latest weather data at departure:</span></span>

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

<span data-ttu-id="ab2b2-164">Ahora se realizan operaciones similares en los datos del tiempo hello:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-164">Now we perform similar operations on hello weather data:</span></span>

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a><span data-ttu-id="ab2b2-165">Combinar datos de tiempo y airline Hola</span><span class="sxs-lookup"><span data-stu-id="ab2b2-165">Joining hello weather and airline data</span></span>

<span data-ttu-id="ab2b2-166">Ahora use hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) función toodo una combinación externa izquierda de los datos de airline y previsiones meteorológicas de Hola por partida AirportID y datetime.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-166">We now use hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function toodo a left outer join of hello airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="ab2b2-167">combinación externa Hola nos permite tooretain todos los datos de airline Hola registra incluso si no hay ningún dato de tiempo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-167">hello outer join allows us tooretain all hello airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="ab2b2-168">Después de la combinación de hello, se quitará algunas columnas redundantes y cambie el nombre hello mantiene columnas tooremove Hola entrantes trama de datos prefijo introducido por la combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-168">Following hello join, we remove some redundant columns, and rename hello kept columns tooremove hello incoming DataFrame prefix introduced by hello join.</span></span>

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

<span data-ttu-id="ab2b2-169">De forma similar, se unir los datos de tiempo y airline de hello en función de llegada AirportID y la fecha y hora:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-169">In a similar fashion, we join hello weather and airline data based on arrival AirportID and datetime:</span></span>

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a><span data-ttu-id="ab2b2-170">Guardar resultados tooCSV para exchange con ScaleR</span><span class="sxs-lookup"><span data-stu-id="ab2b2-170">Save results tooCSV for exchange with ScaleR</span></span>

<span data-ttu-id="ab2b2-171">Esto completa las combinaciones de hello necesitamos toodo con SparkR.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-171">That completes hello joins we need toodo with SparkR.</span></span> <span data-ttu-id="ab2b2-172">Se guardar datos de Hola de hello final trama de datos de Spark "joinedDF5" tooa CSV para tooScaleR de entrada y, a continuación, cerrar sesión de SparkR Hola.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-172">We save hello data from hello final Spark DataFrame “joinedDF5” tooa CSV for input tooScaleR and then close out hello SparkR session.</span></span> <span data-ttu-id="ab2b2-173">Le indicamos explícitamente SparkR toosave Hola CSV resultante en paralelismo suficiente de tooenable 80 particiones independientes en el procesamiento de ScaleR:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-173">We explicitly tell SparkR toosave hello resultant CSV in 80 separate partitions tooenable sufficient parallelism in ScaleR processing:</span></span>

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a><span data-ttu-id="ab2b2-174">Importar tooXDF para su uso por ScaleR</span><span class="sxs-lookup"><span data-stu-id="ab2b2-174">Import tooXDF for use by ScaleR</span></span>

<span data-ttu-id="ab2b2-175">Podríamos usar archivo CSV de hello de airline combinada y los datos del tiempo como-es para el modelado a través de un origen de datos de texto ScaleR.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-175">We could use hello CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="ab2b2-176">Pero se importarlo tooXDF en primer lugar, ya que es más eficaz cuando se ejecutan varias operaciones en el conjunto de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-176">But we import it tooXDF first, since it is more efficient when running multiple operations on hello dataset:</span></span>

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="ab2b2-177">División de los datos para entrenamiento y pruebas</span><span class="sxs-lookup"><span data-stu-id="ab2b2-177">Splitting data for training and test</span></span>

<span data-ttu-id="ab2b2-178">Utilizamos rxDataStep toosplit datos de 2012 de Hola para probar y mantener el resto de hello para el entrenamiento:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-178">We use rxDataStep toosplit out hello 2012 data for testing and keep hello rest for training:</span></span>

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="ab2b2-179">Entrenamiento y prueba de un modelo de regresión logístico</span><span class="sxs-lookup"><span data-stu-id="ab2b2-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="ab2b2-180">Ahora estamos listo toobuild un modelo.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-180">Now we are ready toobuild a model.</span></span> <span data-ttu-id="ab2b2-181">influencia de hello toosee de los datos del tiempo de retraso en la hora de llegada de hello, usamos rutina de regresión logística de ScaleR.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-181">toosee hello influence of weather data on delay in hello arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="ab2b2-182">Usamos esto toomodel si un retardo de llegada de más de 15 minutos se ve influenciado por tiempo de hello en aeropuertos de partida y de llegada de hello:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-182">We use it toomodel whether an arrival delay of greater than 15 minutes is influenced by hello weather at hello departure and arrival airports:</span></span>

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

<span data-ttu-id="ab2b2-183">Ahora veamos cómo en hello probar datos realizar algunas predicciones y examinando ROC y AUC.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-183">Now let’s see how it does on hello test data by making some predictions and looking at ROC and AUC.</span></span>

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a><span data-ttu-id="ab2b2-184">Puntuación en otros lugares</span><span class="sxs-lookup"><span data-stu-id="ab2b2-184">Scoring elsewhere</span></span>

<span data-ttu-id="ab2b2-185">Modelo de hello también se puede usar para los datos de puntuación en otra plataforma.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-185">We can also use hello model for scoring data on another platform.</span></span> <span data-ttu-id="ab2b2-186">Guarde este archivo RDS tooan y, a continuación, transferir e importándolos que RDS en un destino de la puntuación del entorno, como SQL Server R Services.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-186">By saving it tooan RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="ab2b2-187">Es importante tooensure que niveles de factor de Hola de hello toobe de datos con puntuación que coinciden con los que Hola modelo creó.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-187">It is important tooensure that hello factor levels of hello data toobe scored match those on which hello model was built.</span></span> <span data-ttu-id="ab2b2-188">Que coincidencia se puede lograr mediante la extracción y guardar la información de columna de hello asociado a Hola modelado de datos a través del ScaleR `rxCreateColInfo()` función y, a continuación, aplicar ese origen de datos de entrada de toohello de información de columna para la predicción.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-188">That match can be achieved by extracting and saving hello column infomation associated with hello modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information toohello input data source for prediction.</span></span> <span data-ttu-id="ab2b2-189">Siguiente Hola se guarden algunas filas del conjunto de datos de prueba de Hola y extraer y use información de columna de Hola de este ejemplo de script de Hola predicción:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-189">In hello following we save a few rows of hello test dataset and extract and use hello column information from this sample in hello prediction script:</span></span>

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a><span data-ttu-id="ab2b2-190">Resumen</span><span class="sxs-lookup"><span data-stu-id="ab2b2-190">Summary</span></span>

<span data-ttu-id="ab2b2-191">En este artículo, le mostramos cómo es posible toocombine uso de SparkR para la manipulación de datos con ScaleR para el desarrollo de modelos de Hadoop Spark.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-191">In this article, we’ve shown how it’s possible toocombine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="ab2b2-192">Este escenario requiere que se mantengan sesiones de Spark independientes, ejecutando solamente una sesión a la vez, y se intercambien datos a través de archivos CSV.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="ab2b2-193">Aunque sencillo, este proceso debe ser mucho más fácil en una próxima versión de R Server, cuando SparkR y ScaleR puedan compartir una sesión de Spark y, por tanto, compartir Spark DataFrames.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="ab2b2-194">Pasos siguientes y más información</span><span class="sxs-lookup"><span data-stu-id="ab2b2-194">Next steps and more information</span></span>

- <span data-ttu-id="ab2b2-195">Para obtener más información sobre el uso del servidor de R en Spark, vea hello [Guía de introducción en MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span><span class="sxs-lookup"><span data-stu-id="ab2b2-195">For more information on use of R Server on Spark, see hello [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="ab2b2-196">Para obtener información general sobre servidor de R, vea hello [empezar a trabajar con R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) artículo.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-196">For general information on R Server, see hello [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="ab2b2-197">Para obtener información sobre R Server en HDInsight, consulte [Introducción a las funcionalidades de R de código abierto de R Server en HDInsight](hdinsight-hadoop-r-server-overview.md) e [Introducción al uso de R Server en HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ab2b2-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="ab2b2-198">Para más información sobre el uso de SparkR, consulte:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-198">For more information on use of SparkR, see:</span></span>

- [<span data-ttu-id="ab2b2-199">Documento de Apache SparkR</span><span class="sxs-lookup"><span data-stu-id="ab2b2-199">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="ab2b2-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) (Información general de SparkR) de Databricks</span><span class="sxs-lookup"><span data-stu-id="ab2b2-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
