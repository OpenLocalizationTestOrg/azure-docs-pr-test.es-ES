---
title: "una solución de IoT mediante el uso de análisis de transmisiones de aaaBuild | Documentos de Microsoft"
description: "Tutorial: Introducción para solución de IoT de análisis de secuencia de un escenario de cabinas de hello"
keywords: "solución de IOT, funciones de ventana"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Compilación de una solución de IoT con Stream Analytics
## <a name="introduction"></a>Introducción
En este tutorial, aprenderá cómo información en tiempo real tooget de toouse análisis de transmisiones de Azure de los datos. Los programadores pueden combinar fácilmente flujos de datos, por ejemplo, haga clic en secuencias, los registros y los eventos generados por el dispositivo, con información de referencia datos tooderive empresarial o de registros históricos. Como un servicio de cálculo de secuencia completamente administrado y en tiempo real que se hospeda en Microsoft Azure, análisis de transmisiones de Azure proporciona resistencia integrada, baja latencia y escalabilidad tooget pueda ponerse a trabajar en minutos.

Después de completar este tutorial, estará capacitado para lo siguiente:

* Familiarícese con el portal de análisis de transmisiones de Azure Hola.
* Configurar e implementar un trabajo de streaming.
* Articular los problemas reales y solucionarlos mediante el lenguaje de consulta de análisis de transmisiones de Hola.
* Desarrollar soluciones de streaming para los clientes usando el lenguaje de consulta de Stream Analytics.
* Usar hello supervisión y el registro experiencia tootroubleshoot problemas.

## <a name="prerequisites"></a>Requisitos previos
Se necesita Hola siguiendo los requisitos previos toocomplete este tutorial:

* versión más reciente de Hola de [PowerShell de Azure](/powershell/azure/overview)
* Visual Studio de 2017 2015, o hello libre [Comunidad de Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* [Una suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/)
* Privilegios administrativos en el equipo de Hola
* La descarga de [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) de hello Microsoft Download Center
* Opcional: El código para el generador de eventos de hello TollApp en fuente [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>Introducción al escenario: peajes
Una estación de peaje es un fenómeno común. Se encuentra en muchas autopistas, puentes y túneles a través de Hola a todos. Cada estación de peaje tiene varias cabinas. En cabinas manuales, detener el operador de tooan de toopay Hola peaje. En cabinas automatizadas, un sensor sobre cada cabina escanea una tarjeta RFID que está colocado toohello parabrisas del vehículo cuando se pasa por cabina de peaje Hola. Es el paso de hello toovisualize fácil de los vehículos a través de estas estaciones de peaje como una secuencia de eventos sobre el que se pueden realizar operaciones interesantes.

![Imagen de automóviles en cabinas de peaje](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>Datos de entrada
Este tutorial funciona con dos secuencias de datos. Sensores instalados en la entrada de Hola y salir de estaciones de peaje Hola generan primer flujo de Hola. segundo flujo de Hello es un conjunto de datos de búsqueda estática que tenga datos de registro del vehículo.

### <a name="entry-data-stream"></a>Flujo de datos de entrada
flujo de datos de entrada de Hello contiene información sobre automóviles según va entrando en estaciones de peaje.

| TollId | EntryTime | LicensePlate | Estado | Asegúrese | Modelo | VehicleType | VehicleWeight | Toll | Etiqueta |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |10-09-2014 12:01:00.000 |JNB 7001 |NY |Honda |CRV |1 |0 |7 | |
| 1 |10-09-2014 12:02:00.000 |YXZ 1001 |NY |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |10-09-2014 12:02:00.000 |ABC 1004 |CT |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |10-09-2014 12:03:00.000 |XYZ 1003 |CT |Toyota |Corolla |1 |0 |4 | |
| 1 |10-09-2014 12:03:00.000 |BNJ 1007 |NY |Honda |CRV |1 |0 |5 |789123456 |
| 2 |10-09-2014 12:05:00.000 |CDE 1007 |NJ |Toyota |4 x 4 |1 |0 |6 |321987654 |

Esta es una breve descripción de las columnas de hello:

| Columna | Description |
| --- | --- |
| TollId |Id. de cabina de peaje Hola que identifica de forma única una cabina de peaje |
| EntryTime |Hola fecha y hora de entrada de cabina de peaje Hola vehículo toohello en UTC |
| LicensePlate |número de matrícula Hola de vehículo Hola |
| Estado |Estado de los Estados Unidos. |
| Asegúrese |fabricante de Hello del automóvil Hola |
| Modelo |número de modelo de Hola de automóvil Hola |
| VehicleType |1 para los vehículos de pasajeros o 2 para vehículos comerciales. |
| WeightType |Peso del vehículo en toneladas; es 0 para vehículos de pasajeros. |
| Toll |valor de peaje Hello en USD |
| Etiqueta |Hola e-Tag en automobile Hola que automatiza el pago; espacio en blanco donde se realizó el pago de hello manualmente |

### <a name="exit-data-stream"></a>Flujo de datos de salida
flujo de datos de salida de Hello contiene información acerca de automóviles dejando estación de peaje Hola.

| **TollId** | **ExitTime** | **LicensePlate** |
| --- | --- | --- |
| 1 |10-09-2014 T12:03:00.0000000Z |JNB 7001 |
| 1 |10-09-2014 T12:03:00.0000000Z |YXZ 1001 |
| 3 |10-09-2014 T12:04:00.0000000Z |ABC 1004 |
| 2 |10-09-2014 T12:07:00.0000000Z |XYZ 1003 |
| 1 |10-09-2014 T12:08:00.0000000Z |BNJ 1007 |
| 2 |10-09-2014 T12:07:00.0000000Z |CDE 1007 |

Esta es una breve descripción de las columnas de hello:

| Columna | Description |
| --- | --- |
| TollId |Id. de cabina de peaje Hola que identifica de forma única una cabina de peaje |
| ExitTime |Hola fecha y hora de salida del vehículo Hola de cabina de peaje en UTC |
| LicensePlate |número de matrícula Hola de vehículo Hola |

### <a name="commercial-vehicle-registration-data"></a>Datos de registro de vehículos comerciales
tutorial de Hello usa una instantánea estática de una base de datos de registro de vehículos comerciales.

| LicensePlate | RegistrationId | Expirada |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| BAC 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Esta es una breve descripción de las columnas de hello:

| Columna | Description |
| --- | --- |
| LicensePlate |número de matrícula Hola de vehículo Hola |
| RegistrationId |Id. del registro del vehículo Hola |
| Expirada |Hola estado de registro del vehículo hello: 0 si el registro de vehículo está activo, 1 si el registro ha expirado |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Configurar el entorno de Hola para análisis de transmisiones de Azure
toocomplete este tutorial, necesita una suscripción a Microsoft Azure. Microsoft ofrece una evaluación gratuita de los servicios de Microsoft Azure.

Si no tiene una cuenta de Azure, puede [solicitar una versión de evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> toosign hacia arriba para una prueba gratuita, necesita un dispositivo móvil que pueda recibir mensajes de texto y una tarjeta de crédito válida.
> 
> 

Asegúrese de hello toofollow pasos de sección de "Limpiar su cuenta de Azure" de hello final Hola de este artículo para que puede realizar un mejor uso de Hola de su crédito de Azure.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Aprovisionar recursos de Azure necesarios para el tutorial de Hola
Este tutorial requiere dos eventos concentradores tooreceive *entrada* y *salir* flujos de datos. La base de datos de SQL Azure genera resultados de Hola de los trabajos de análisis de transmisiones de Hola. Azure Storage almacena los datos de referencia sobre los registros de vehículos.

Puede usar hello Setup.ps1 script en la carpeta de hello TollApp en GitHub toocreate todos los recursos necesarios. En interés de Hola de tiempo, se recomienda que se ejecuta. Si desea más información acerca de cómo tooconfigure estos recursos en hello portal de Azure, consulte toolearn toohello "Configuración de recursos de tutorial en el portal de Azure" Apéndice.

Descargar y guardar los auxiliares hello [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) carpetas y archivos.

Abra una ventana de **Microsoft Azure PowerShell***como administrador*. Si aún no dispone de PowerShell de Azure, siga las instrucciones de hello en [instalar y configurar Azure PowerShell](/powershell/azure/overview) tooinstall lo.

Puesto que Windows bloquea automáticamente archivos .exe, .dll y. ps1, necesita directiva de ejecución de hello tooset antes de ejecutar script de Hola. Asegúrese de que está ejecutando la ventana de PowerShell de Azure de hello *como administrador*. Ejecute **Set-ExecutionPolicy unrestricted**. Cuando se le solicite, escriba **Y**.

![Captura de pantalla de "Set-ExecutionPolicy unrestricted" ejecutándose en la ventana de Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

Ejecutar **Get-ExecutionPolicy** toomake seguro de que el comando hello funcionaron.

![Captura de pantalla de "Get-ExecutionPolicy" ejecutándose en la ventana de Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Vaya a directorio toohello que tiene scripts de Hola y aplicación del generador.

![Captura de pantalla de "cd .\TollApp\TollApp" ejecutar en la ventana de PowerShell de Azure de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

Tipo de **.\\ Setup.ps1** tooset una cuenta de Azure, cree y configure todos los recursos necesarios e inicie toogenerate eventos. script de Hola aleatoriamente recoge un toocreate región sus recursos. tooexplicitly especificar una región, puede pasar hello **-ubicación** parámetro como en el siguiente ejemplo de Hola:

**.\\Setup.ps1 -ubicación “centro de EE. UU.”**

![Captura de pantalla de página Hola de inicio de sesión Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

Abre el script de Hola Hola **inicio de sesión** página de Microsoft Azure. Escriba los credenciales de la cuenta.

> [!NOTE]
> Si la cuenta tiene acceso toomultiple suscripciones, es posible que nombre de la suscripción de hello tooenter frecuentes que quiere toouse de tutorial Hola.
> 
> 

script de Hola puede adoptar varios toorun minutos. Una vez finalizada, la salida de hello debe ser similar Hola siguiente captura de pantalla.

![Captura de pantalla de salida del script de Hola en la ventana de PowerShell de Azure de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

También verá otra ventana que sea similar toohello siguiente captura de pantalla. Esta aplicación está enviando eventos tooAzure centros de eventos, que es el tutorial de hello toorun necesarios. Por lo tanto, no detenga la aplicación hello ni cierre esta ventana hasta que finaliza el tutorial Hola.

![Captura de pantalla "Enviando datos de centro de eventos"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

También debe ser capaz de toosee los recursos en el portal de Azure ahora. Vaya demasiado<https://portal.azure.com>e inicie sesión con sus credenciales de cuenta. Tenga en cuenta que, actualmente, algunas funciones utiliza portal clásico de Hola. Estos pasos se indicarán con claridad.

### <a name="azure-event-hubs"></a>Azure Event Hubs
Hola portal de Azure, haga clic en **más servicios** en parte inferior de hello del panel de administración izquierdo de Hola. Tipo de **centros de eventos** en Hola campo proporcionado y haga clic en **centros de eventos**. Esto inicia una nueva Hola de toodisplay de ventana de explorador **SERVICE BUS** área Hola **portal clásico**. Aquí puede ver Hola concentrador de eventos creado por hello Setup.ps1 script.

![Bus de servicio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Haga clic en hello uno que se inicia con *tolldata*. Haga clic en hello **centros de eventos** ficha. Verá dos Centros de eventos denominados *entry* y *exit* creados en este espacio de nombres.

![Pestaña de concentradores de eventos en el portal clásico de Hola](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Contenedor de Almacenamiento de Azure
1. Volver atrás toohello ficha en el portal de tooAzure abierta del explorador. Haga clic en **almacenamiento** en hello lado hello toosee portal Azure hello Azure del contenedor de almacenamiento que se utiliza en el tutorial Hola izquierdo.
   
    ![Elemento de menú de almacenamiento](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Haga clic en hello uno que empiezan por *tolldata*. Haga clic en hello **contenedores** contenedor de ficha toosee Hola creado.
   
    ![Pestaña de contenedores en hello portal de Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Haga clic en hello **tolldata** Hola de contenedor toosee carga archivo JSON que tiene datos de registro del vehículo.
   
    ![Captura de pantalla de archivo de registration.json hello en el contenedor de Hola](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Azure SQL Database
1. Volver atrás toohello portal de Azure en ficha primera Hola que abrió en el Explorador de Hola. Haga clic en **bases de datos SQL** en hello parte izquierda de hello toosee portal Azure Hola base de datos SQL que se utilizarán en el tutorial de Hola y haga clic en **tolldatadb**.
   
    ![Captura de pantalla de hello crea la base de datos SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Nombre del servidor de hello copia sin número de puerto de hello (*servername*. database.windows.net, por ejemplo).
    ![Captura de pantalla de hello crea la base de datos de base de datos SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>Conectar la base de datos de toohello desde Visual Studio
Use Visual Studio tooaccess resultados de la consulta de base de datos de salida de hello.

Conectar la base de datos SQL de toohello (destino de hello) de Visual Studio:

1. Abra Visual Studio y, a continuación, haga clic en **herramientas** > **conectar tooDatabase**.
2. Si se le solicita, haga clic en **Microsoft SQL Server** como origen de datos.
   
    ![Cuadro de diálogo Cambiar origen de datos](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. Hola **nombre del servidor** , a continuación, pegue el nombre de Hola que ha copiado en la sección anterior de Hola de hello portal de Azure (es decir, *servername*. database.windows.net).
4. Haga clic en **Usar autenticación de SQL Server**.
5. Escriba **tolladmin** en hello **nombre de usuario** campo y **123toll!** Hola **contraseña** campo.
6. Haga clic en **seleccione o escriba un nombre de base de datos**y seleccione **TollDataDB** como base de datos de Hola.
   
    ![Cuadro de diálogo Agregar conexión](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. Haga clic en **Aceptar**.
8. Abra el Explorador de servidores.
   
    ![Explorador de servidores](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. Vea cuatro tablas de base de datos de hello TollDataDB.
   
    ![Tablas de base de datos de hello TollDataDB](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>Generador de eventos: proyecto de ejemplo TollApp
Hola script de PowerShell inicia automáticamente toosend eventos mediante el uso de programa de aplicación de ejemplo de Hola TollApp. No es necesario tooperform todos los pasos adicionales.

Sin embargo, si está interesado en los detalles de implementación, puede encontrar código de hello de hello aplicación TollApp en GitHub [ejemplos/TollApp](https://aka.ms/azure-stream-analytics-toll-source).

![Captura de pantalla del código de ejemplo que se muestra en Visual Studio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Creación de un trabajo de Análisis de transmisiones
1. Hola portal de Azure, haga clic en Hola signo de color verde en la esquina superior izquierda de Hola de hello página toocreate un nuevo trabajo de análisis de transmisiones. Seleccione **Inteligencia y análisis** y, a continuación, haga clic en **Trabajo de Stream Analytics**.
   
    ![New button](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. Proporcione un nombre de trabajo, validar suscripción hello es correcta y, a continuación, cree un nuevo grupo de recursos en hello misma región que Hola almacenamiento de concentrador de eventos (valor predeterminado es Ee.uu. Central sur para script de Hola).
3. Haga clic en **Pin toodashboard** y, a continuación, **crear** final Hola de página Hola.
   
    ![Opción Crear el trabajo de Análisis de transmisiones](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>Definición de orígenes de entrada
1. trabajo de Hola creará y abrirá la página de trabajo de Hola. O bien, puede hacer clic Hola creado trabajo de análisis en el panel del portal Hola.

2. Haga clic en hello **entradas** ficha toodefine Hola origen de datos.
   
    ![pestaña de entradas de Hola](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. Haga clic en **AGREGAR ENTRADA**.
   
    ![Hola agregar una opción de entrada](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. Escriba **EntryStream** como **ALIAS DE ENTRADA**.
5. El tipo de origen es **Flujo de datos**
6. El origen es **Centro de eventos**.
7. **Espacio de nombres de bus de servicio** debe ser hello TollData Hola de lista desplegable.
8. **Nombre del concentrador de eventos** debe establecerse demasiado**entrada**.
9. **Nombre de directiva de centro de eventos*es **RootManageSharedAccessKey** (Hola el valor predeterminado).
10. Seleccione **JSON** para **FORMATO DE SERIALIZACIÓN DE EVENTOS** y **UTF8** para **CODIFICACIÓN**.
   
    La configuración se verá así:
   
    ![Configuración del centro de eventos](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. Haga clic en **crear** final Hola de Asistente de hello página toofinish Hola.
    
    Ahora que ha creado la secuencia de entrada de hello, seguirá Hola mismo flujo de salida de hello de toocreate pasos. Ser seguro de valores de tooenter como en la siguiente captura de pantalla de Hola.
    
    ![Configuración de flujo de salida de hello](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    Ha definido dos flujos de entrada:
    
    ![Flujos de entrada definidos en hello portal de Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    A continuación, va a agregar la entrada de datos de referencia para el archivo de blob de Hola que contiene datos de registro del automóvil.
11. Haga clic en **agregar**y, a continuación, siga Hola mismo proceso para las entradas de la secuencia de Hola, pero selecciona **datos de referencia** en lugar de **flujo de datos** hello y **Alias de entrada**  es **registro**.

12. cuenta de almacenamiento que comienza por **tolldata**. debe ser el nombre del contenedor de Hello **tolldata**, hello y **patrón de ruta de acceso** debe ser **registration.json**. Este nombre de archivo distingue mayúsculas de minúsculas, por lo que asegúrese de escribirlo en **minúsculas**.
    
    ![Configuración de almacenamiento de blobs](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. Haga clic en **crear** Asistente de hello toofinish.

Ahora todas las entradas están definidas.

## <a name="define-output"></a>Defininición de salida
1. En el panel de información general de trabajo de análisis de transmisiones de hello, seleccione **salidas**.
   
    ![ficha salida de Hello y la opción "Agregar una salida"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. Haga clic en **Agregar**.
3. Conjunto hello **alias de salida** too'output' y, a continuación, **receptor** demasiado**base de datos SQL**.
3. Seleccione el nombre del servidor de Hola que se usó en hello sección "Conectar tooDatabase desde Visual Studio" del artículo de Hola. es el nombre de la base de datos de Hello **TollDataDB**.
4. Escriba **tolladmin** en hello **nombre de usuario** campo, **123toll!** Hola **contraseña** campo, y **TollDataRefJoin** en hello **tabla** campo.
   
    ![Configuración de SQL Database](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. Haga clic en **Crear**.

## <a name="azure-stream-analytics-query"></a>Consulta de Análisis de transmisiones de Azure
Hola **consulta** pestaña contiene una consulta SQL que transformaciones Hola los datos entrantes.

![Una consulta de agregado toohello pestaña de consulta](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

Este tutorial trata tooanswer varias cuestiones empresariales que están relacionados con datos tootoll y construcciones de análisis de transmisiones de consultas que pueden usarse en análisis de transmisiones de Azure tooprovide una respuesta adecuada.

Antes de empezar su primer trabajo de análisis de transmisiones, vamos a examinar algunos escenarios y sintaxis de consultas de Hola.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>Introducción tooAzure lenguaje de consulta de análisis de transmisiones
- - -
Supongamos que necesita el número de hello toocount de vehículos que entran en una cabina de peaje. Se trata de una secuencia continua de eventos, que tiene toodefine un "período de tiempo." Vamos a modificar hello toobe de pregunta "¿cuántos vehículos escriba una cabina de peaje cada tres minutos?". Se trata de hello tooas comúnmente denominado recuento de saltos de tamaño constante.

Echemos un vistazo a la consulta de análisis de transmisiones de Azure de Hola que responda a esta pregunta:

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

Como puede ver, análisis de transmisiones de Azure usa un lenguaje de consulta que es similar a SQL y agrega algunas extensiones toospecify relacionados con el tiempo aspectos de hello consulta.

Para obtener más información, lea acerca de [administración del tiempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) y [ventana](https://msdn.microsoft.com/library/azure/dn835019.aspx) construcciones que se usan en consultas de Hola de MSDN.

## <a name="testing-azure-stream-analytics-queries"></a>Pruebas de consultas de Análisis de transmisiones de Azure
Ahora que ha escrito la primera consulta de análisis de transmisiones de Azure, es tootest de tiempo mediante los archivos de datos de ejemplo se encuentra en la carpeta de TollApp Hola siguiendo la ruta de acceso:

<seg>
  **..\\TollApp\\TollApp\\Datos**</seg>

Esta carpeta contiene Hola siguientes archivos:

* Entry.json
* Exit.json
* registration.json

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>Pregunta 1: Número de vehículos que entran en una cabina de peaje
1. Abra Hola portal de Azure y vaya tooyour crear trabajo de análisis de transmisiones de Azure. Haga clic en hello **consulta** pestaña y pegue la consulta desde la sección anterior de Hola.

2. toovalidate esta consulta con datos de ejemplo, cargar datos de hello en hello EntryStream entrada haciendo clic en... Hola símbolos y seleccionando **cargar datos de ejemplo de archivo**.

    ![Captura de pantalla de archivo de hello Entry.json](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. En panel de Hola que aparece el archivo de hello seleccione (Entry.json) en el equipo local y haga clic en **Aceptar**. Hola **prueba** icono podrá ahora iluminar y seleccionables.
   
    ![Captura de pantalla de archivo de hello Entry.json](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Validar que el resultado de hello de consulta de hello es como se esperaba:
   
    ![Resultados de prueba de Hola](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>Pregunta 2: Tiempo total para cada toopass automóvil a través de la cabina de peaje Hola de informes de
Hola promedio de tiempo que se necesita para una toopass automóvil a través de peaje Hola ayuda a eficacia de hello tooassess del proceso de Hola y experiencia de usuario de Hola.

tiempo total de toofind hello, necesita toojoin Hola EntryTime flujo con flujo de ExitTime Hola. Se unirá secuencias de hello en las columnas TollId y LicencePlate. Hola **UNIR** operador requiere toospecify libertad temporal que describe la diferencia entre Hola unido eventos de tiempo aceptable Hola. Va a usar **DATEDIFF** función toospecify que eventos deberían estar ya no más de 15 minutos entre sí. También se aplicarán hello **DATEDIFF** tooexit de función y entrada de horas de tiempo real de toocompute Hola que emplea un automóvil Hola estación de pago. Tenga en cuenta Hola diferencia del uso de Hola de **DATEDIFF** cuando se utiliza en una **seleccione** instrucción en lugar de un **UNIR** condición.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest esta consulta, consultas de actualización hello en hello **consulta** de trabajo de Hola. Agregar el archivo de prueba de hello para **ExitStream** igual que **EntryStream** se ha especificado anteriormente.
   
2. Haga clic en **Probar**.

3. Seleccione Hola casilla tootest Hola consultas y vistas Hola salida:
   
    ![Resultado de prueba de Hola](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>Pregunta 3: Notificar todos los vehículos comerciales con registro caducado
Análisis de transmisiones de Azure puede usar instantáneas estáticas de datos toojoin con flujos de datos temporales. toodemonstrate esta capacidad, Hola de uso siguiente pregunta de ejemplo.

Si un vehículo comercial está registrado con la empresa de peaje hello, puede pasar a través de la cabina de peaje Hola sin detenerse para inspección. Todos los vehículos comerciales que han expirado registros utilizará tooidentify de tabla de búsqueda de registro de vehículos comerciales.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

tootest una consulta mediante el uso de datos de referencia, debe toodefine un origen de entrada para los datos de referencia de hello, que se ha hecho todavía.

tootest esta consulta, consultas de hello pegar en hello **consulta** , haga clic en **prueba**y especificar los datos de ejemplo y haga clic en orígenes de entrada de hello dos y registro de hello **prueba**.  
   
![Resultado de prueba de Hola](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Iniciar el trabajo de análisis de transmisiones de Hola
Ahora es toofinish Hola configuración e iniciar Hola trabajo de temporizador. Guardar consulta Hola de pregunta 3, que generará un resultado que coincidencias Hola esquema de hello **TollDataRefJoin** tabla de salida.

Trabajo vaya toohello **panel**y haga clic en **iniciar**.

![Captura de pantalla del botón de inicio de hello en el panel de trabajo de Hola](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

En el cuadro de diálogo de Hola que se abre, cambiar hello **iniciar salida** demasiado tiempo**tiempo personalizada**. Cambio hello tooone horas antes de hello hora actual. Este cambio garantiza que se procesen todos los eventos de concentrador de eventos de Hola desde que comenzó a eventos de hello toogenerate al principio de hello del tutorial Hola. Ahora haga clic en hello **iniciar** trabajo de botón toostart Hola.

![Selección de tiempo personalizado](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Iniciando la tarea hello puede tardar unos minutos. Puede ver estado de hello en la página de nivel superior de hello para el análisis de transmisiones.

![Captura de pantalla de estado de Hola de trabajo de Hola](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Comprobación de resultados en Visual Studio
1. Abra el Explorador de servidores de Visual Studio y haga clic en hello **TollDataRefJoin** tabla.
2. Haga clic en **mostrar datos de tabla** toosee salida de hello de su trabajo.
   
    ![Selección de "Mostrar datos de tabla" en el Explorador de servidores](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Escalado horizontal de trabajos de Azure Stream Analytics
Análisis de transmisiones de Azure está diseñado tooelastically escalar por lo que puede controlar una gran cantidad de datos. pueden utilizar consultas de análisis de transmisiones de Azure Hola un **PARTITION BY** sistema Hola de cláusula tootell que este paso se escala horizontalmente. **PartitionId** es una columna especial que Hola sistema agrega Id. de partición de hello toomatch de entrada de hello (centro de eventos).

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. Parada Hola actual de trabajo, consultas de actualización Hola Hola **consulta** ficha y abra hello **configuración** engranaje en el panel de trabajo de Hola. Haga clic en **Escalar**.
   
    **UNIDADES de transmisión por secuencias** definir cantidad Hola de capacidad de proceso que Hola trabajo puede recibir.
2. Cambio Hola desplegable de 1 a 6.
   
    ![Captura de pantalla de selección de 6 unidades de streaming](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Vaya toohello **salidas** pestaña y cambie el nombre del saludo de la tabla SQL de Hola demasiado**TollDataTumblingCountPartitioned**.

Ahora, si inicia el trabajo de hello análisis de transmisiones de Azure puede distribuir el trabajo entre más recursos de proceso y lograr un mejor rendimiento. Tenga en cuenta que hello TollApp aplicación también enviaba eventos de particiones de forma TollId.

## <a name="monitor"></a>Supervisión
Hola **MONITOR** área contiene estadísticas sobre Hola ejecutando el trabajo. Primera vez que la configuración es necesario toouse cuenta de almacenamiento Hola Hola misma región (nombre de pago como Hola resto de este documento).   

![Captura de pantalla de Supervisión](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

Puede tener acceso a **registros de actividad** desde el panel de trabajo de hello **configuración** área así.


## <a name="conclusion"></a>Conclusión
Este tutorial introdujo toohello servicio de análisis de transmisiones de Azure. Muestra cómo tooconfigure entradas y salidas de Hola trabajo de análisis de transmisiones. Con un escenario de datos de peaje hello, tutorial Hola explica tipos comunes de problemas que surgen en el espacio de Hola de datos en movimiento y cómo pueden resolverse con consultas de tipo SQL simples en análisis de transmisiones de Azure. tutorial de Hello describe construcciones de extensión SQL para trabajar con datos temporales. Ha explicado cómo toojoin datos transmite, el archivo de secuencia de datos de hello tooenrich con datos de referencia estáticos y cómo tooscale espera un tooachieve mayor rendimiento de consulta.

Aunque este tutorial proporciona una buena introducción, no está completo de en modo alguno. Puede encontrar varios patrones de consulta mediante el lenguaje SAQL hello en [consultar ejemplos de patrones de uso comunes de análisis de transmisiones](stream-analytics-stream-analytics-query-patterns.md).
Consulte toohello [documentación en línea](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn más información sobre análisis de transmisiones de Azure.

## <a name="clean-up-your-azure-account"></a>Limpieza de la cuenta de Azure
1. Detener el trabajo de análisis de transmisiones de Hola Hola portal de Azure.
   
    Hola Setup.ps1 script crea una base de datos SQL y dos centros de eventos. Hola después de limpiar los recursos al final de hello del tutorial Hola de Ayuda de instrucciones.
2. En una ventana de PowerShell, escriba **.\\ Cleanup.ps1** toostart script de Hola que elimina los recursos utilizados en el tutorial de Hola.
   
   > [!NOTE]
   > Los recursos se identifican por su nombre de Hola. Asegúrese de revisar cuidadosamente cada elemento antes de confirmar la eliminación.
   > 
   > 


