---
title: "análisis de opinión de Twitter de tiempo aaaReal con análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse análisis de transmisiones para el análisis de opinión de Twitter en tiempo real. Guía paso a paso de toodata de generación de eventos en un panel en tiempo real."
keywords: "análisis de tendencias de twitter en tiempo real, análisis de opiniones, análisis de medios sociales, ejemplo de análisis de tendencias"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Análisis de sentimiento de Twitter en tiempo real en Azure Stream Analytics

Obtenga información acerca de cómo Twitter toobuild una solución de análisis de opiniones para el análisis de los medios sociales si se ponen en tiempo real de los eventos en los centros de eventos de Azure. A continuación, puede escribir un análisis de transmisiones de Azure consultar tooanalyze Hola datos y cualquier almacén Hola resultados para su uso posterior o usar un panel y [Power BI](https://powerbi.com/) tooprovide información en tiempo real.

Las herramientas de análisis de las redes sociales ayudan a las organizaciones a comprender los temas que son tendencias. Los temas que son tendencias son asuntos y actitudes con un gran volumen de entradas en las redes sociales. Análisis de opiniones, que también se denomina *minería de datos de opinión*, usa medios sociales análisis herramientas toodetermine actitudes de un producto, idea y así sucesivamente. 

Análisis de tendencias de Twitter en tiempo real es un buen ejemplo de una herramienta de análisis, porque el modelo de suscripción de hello hashtag permite palabras clave de toospecific de toolisten (hashtags) y desarrollar análisis de opiniones de hello fuente de distribución.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>Escenario: Análisis de opinión de redes sociales en tiempo real

Una empresa que tiene un sitio Web de noticias multimedia está interesada en obtener una ventaja con respecto a sus competidores ya que presenta el contenido del sitio que es importante de inmediato tooits lectores. empresa Hola utiliza el análisis de los medios sociales en temas que son relevantes tooreaders realizando análisis de opiniones en tiempo real de los datos de Twitter.

tooidentify temas tendencias en tiempo real en Twitter, Hola empresa necesidades de análisis en tiempo real acerca del volumen de tweet de Hola y opiniones de los temas claves. En otras palabras, la necesidad de hello es un motor de análisis de análisis de opiniones que se basa en esta fuente de distribución de los medios sociales.

## <a name="prerequisites"></a>Requisitos previos
En este tutorial, utilice una aplicación cliente que se conecta tooTwitter y busca tweets que tienen ciertas hashtags (lo que se puede establecer). En orden toorun Hola aplicación y analizar Hola tweets mediante el análisis de transmisión por secuencias de Azure, debe disponer de hello siguiente:

* Una suscripción de Azure
* Una cuenta de Twitter 
* Una aplicación de Twitter, hello y [token de acceso de OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) para esa aplicación. Se proporcionan instrucciones de alto nivel sobre cómo toocreate una aplicación de Twitter más tarde.
* fuente de aplicación de TwitterWPFClient Hello, que lee Hola Twitter. tooget esta aplicación, descarga hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) de GitHub de archivos y, a continuación, descomprima el paquete de hello en una carpeta en el equipo. Si desea que el código fuente de toosee hello y ejecutar aplicación hello en un depurador, puede obtener el código fuente de Hola de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Creación de un centro de eventos para la entrada de Stream Analytics

aplicación de ejemplo de Hola genera eventos y los envía tooan concentrador de eventos de Azure. Los concentradores de eventos de Azure son método hello preferido de recopilación de eventos para el análisis de transmisiones. Para obtener más información, vea hello [documentación de los centros de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md).


### <a name="create-an-event-hub-namespace-and-event-hub"></a>Creación de un espacio de nombres del centro de eventos y un centro de eventos
En este procedimiento, primero cree un espacio de nombres del centro de eventos y, a continuación, agregue un espacio de nombres de toothat de concentrador de eventos. Los espacios de nombres del concentrador de eventos se utilizan instancias de bus de eventos relacionados con el grupo de toologically. 

1. Inicie sesión en toohello portal de Azure y haga clic en **New** > **Internet de las cosas** > **concentrador de eventos**. 

2. Hola **crear espacio de nombres** hoja, escriba un nombre de espacio de nombres como `<yourname>-socialtwitter-eh-ns`. Puede utilizar cualquier nombre de espacio de nombres de hello, pero Hola nombre debe ser válido para una dirección URL y debe ser único en Azure. 
    
3. Seleccione una suscripción y cree o elija un grupo de recursos. Luego haga clic en **Crear**. 

    ![Creación de un espacio de nombres del centro de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. Cuando el espacio de nombres de hello ha terminado de implementar, buscar espacio de nombres del concentrador de eventos de hello en la lista de recursos de Azure. 

5. Haga clic en nuevo espacio de nombres Hola y en la hoja de espacio de nombres de hello, haga clic en  **+ &nbsp;concentrador de eventos**. 

    ![botón de agregar el concentrador de eventos de Hola para crear un nuevo centro de eventos ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. Nuevo centro de eventos de nombre hello `socialtwitter-eh`. Puede usar otro nombre. Si lo hace, tome nota del mismo, porque necesita Hola nombre más adelante. No es necesario tooset cualquier otra opción de concentrador de eventos de Hola.

    ![Hoja para la creación de un centro de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. Haga clic en **Crear**.


### <a name="grant-access-toohello-event-hub"></a>Centro de eventos de conceder acceso toohello

Antes de que un proceso puede enviar el concentrador de eventos de datos tooan, centro de eventos de hello debe tener una directiva que permita el acceso adecuado. Directiva de acceso de Hello genera una cadena de conexión que incluya la información de autorización.

1.  En la hoja de espacio de nombres de evento de hello, haga clic en **centros de eventos** y, a continuación, haga clic en nombre de Hola de su nuevo concentrador de eventos.

2.  En la hoja de concentrador de eventos de hello, haga clic en **directivas de acceso compartido** y, a continuación, haga clic en  **+ &nbsp;agregar**.

    >[!NOTE]
    >Asegúrese de que está trabajando con el concentrador de eventos de hello, no Hola eventos concentrador espacio de nombres.

3.  Agregue una directiva denominada `socialtwitter-access` y, en **Notificación**, seleccione **Administrar**.

    ![Hoja para la creación de una directiva de acceso al centro de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  Haga clic en **Crear**.

5.  Después de que se ha implementado la directiva de hello, haga clic en la lista de Hola de directivas de acceso compartido.

6.  Cuadro de búsqueda Hola etiquetado **clave principal de la cadena de conexión** y haga clic en la cadena de conexión de hello copia botón siguiente toohello. 
    
    ![Copiar la clave de cadena de conexión principal de Hola Hola directiva de acceso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  Pegue la cadena de conexión de hello en un editor de texto. Necesita esta cadena de conexión para la sección siguiente de hello, después de realizar algunos tooit pequeñas modificaciones.

    cadena de conexión de Hello tiene el siguiente aspecto:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    Tenga en cuenta que la cadena de conexión de hello contiene varios pares de clave y valor, separados por punto y coma: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, y `EntityPath`.  

    > [!NOTE]
    > Para la seguridad, se han quitado los elementos de cadena de conexión de hello en el ejemplo de Hola.

8.  En el editor de texto hello, quitar hello `EntityPath` par de cadena de conexión de hello (no olvide tooremove Hola por punto y coma que lo precede). Cuando haya terminado, cadena de conexión de hello tiene este aspecto:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>Configurar e iniciar la aplicación de cliente de Twitter de hello
aplicación de cliente de Hello obtiene eventos tweet directamente de Twitter. En orden toodo lo, necesita Hola de toocall de permiso de Twitter API de transmisión por secuencias. tooconfigure permiso, crear una aplicación en Twitter, lo que genera credenciales exclusivas (por ejemplo, un token de OAuth). A continuación, puede configurar toouse de aplicación de cliente de hello en estas credenciales cuando se realizan llamadas de API. 

### <a name="create-a-twitter-application"></a>Crear una aplicación de Twitter
Si no dispone de una aplicación de Twitter que pueda usar para este tutorial, puede crear una. Ya debe tener una cuenta de Twitter.

> [!NOTE]
> puede cambiar el proceso exacto de Hello en Twitter para crear una aplicación y obtener el token, secretos y las claves de Hola. Si estas instrucciones no coincide con lo que se ve en el sitio de Twitter de hello, consulte la documentación del desarrollador de Twitter de toohello.

1. Vaya toohello [página de administración de aplicaciones de Twitter](https://apps.twitter.com/). 

2. Cree una aplicación. 

    * Dirección URL del sitio Web de hello, especifique una dirección URL válida. No tiene toobe un sitio en vivo. (No puede especificar simplemente `localhost`).
    * Deje en blanco campo de devolución de llamada de Hola. aplicación de cliente de Hola que utiliza para este tutorial no requiere las devoluciones de llamada.

    ![Creación de una aplicación en Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. Opcionalmente, cambie los permisos de la aplicación hello solo tooread.

4. Cuando se crea la aplicación hello, vaya toohello **claves y Tokens de acceso** página.

5. Haga clic en el botón de hello toogenerate un token de acceso y el secreto del token de acceso.

Mantenga esta información útil, ya que necesitará en el procedimiento siguiente Hola.

>[!NOTE]
>Hola claves y secretos de aplicación de Twitter de hello proporcionan la cuenta de acceso de Twitter tooyour. Tratar esta información como confidencial, Hola igual a como lo hace la contraseña de Twitter. Por ejemplo, no inserte esta información en una aplicación que se asigne tooothers. 


### <a name="configure-hello-client-application"></a>Configurar la aplicación de cliente hello
Hemos creado una aplicación de cliente que se conecte mediante datos de tooTwitter [API de transmisión por secuencias de Twitter](https://dev.twitter.com/streaming/overview) eventos de tweet toocollect sobre un conjunto específico de temas. aplicación Hello usa hello [Sentiment140](http://help.sentiment140.com/) herramienta de código abierto, que asigna Hola después tweet de opiniones valor tooeach:

* 0 = negativo
* 2 = neutral
* 4 = positivo

Después de eventos de tweet Hola se han asignado un valor de opinión, se insertan concentrador de eventos de toohello que creó anteriormente.

Antes de que se ejecute la aplicación hello, requiere cierta información del usuario, como las claves de Twitter de Hola y cadena de conexión de concentrador de eventos de Hola. Puede proporcionar información de configuración de Hola de las siguientes maneras:

* Ejecutar la aplicación hello y, a continuación, utilice claves de hello tooenter interfaz de usuario de la aplicación hello, secretos y cadena de conexión. Si lo hace, se utiliza la información de configuración de hello en la sesión actual, pero no se guarda.
* Edite el archivo .config de la aplicación hello y establecer los valores hello no existe. Este enfoque conserva la información de configuración de hello, pero también significa que esta información potencialmente confidencial se almacena en texto sin formato en el equipo.

Hello siguiente procedimiento documenta ambos enfoques. 

1. Asegúrese de que ha descargado y descomprimido hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) aplicación, como se muestra en los requisitos previos de Hola.

2. valores de hello tooset en tiempo de ejecución (y solo para hello sesión actual), ejecute hello `TwitterWPFClient.exe` aplicación. Cuando solicite aplicación hello, escriba Hola siguientes valores:

    * Hola clave de consumidor de Twitter (clave de API).
    * Hola secreto de consumidor de Twitter (secreto de API).
    * Hola Token de acceso de Twitter.
    * Hola secreto del Token de acceso de Twitter.
    * información de la cadena de conexión Hola que guardó anteriormente. Asegúrese de que usar cadena de conexión de Hola que quitan hello `EntityPath` par clave-valor de.
    * Hola Twitter palabras clave que desea toodetermine opinión de.

   ![Aplicación de TwitterWpfClient en ejecución, mostrando los valores difuminados](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. valores de hello tooset de forma persistente, usan un archivo de texto del editor tooopen hello TwitterWpfClient.exe.config. A continuación, en hello `<appSettings>` elemento, hacer esto:

    * Establecer `oauth_consumer_key` toohello clave de consumidor de Twitter (clave de API). 
    * Establecer `oauth_consumer_secret` toohello secreto de consumidor de Twitter (secreto de API).
    * Establecer `oauth_token` toohello Token de acceso de Twitter.
    * Establecer `oauth_token_secret` toohello secreto del Token de acceso de Twitter.

    Más adelante en hello `<appSettings>` elemento, realice estos cambios:

    * Establecer `EventHubName` toohello nombre de centro de eventos (es decir, el valor de toohello de ruta de acceso de hello entidad).
    * Establecer `EventHubNameConnectionString` toohello cadena de conexión. Asegúrese de que usar cadena de conexión de Hola que quitan hello `EntityPath` par clave-valor de.

    Hola `<appSettings>` sección aspecto Hola siguiente ejemplo. (Para mayor claridad y seguridad, se han ajustado algunas líneas y se han quitado algunos caracteres).

    ![Archivo de configuración de aplicación TwitterWpfClient en un editor de texto, que muestra las claves de Twitter de Hola y secretos e información de cadena de conexión de concentrador de eventos de Hola](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Si ya no ha iniciado la aplicación hello, ejecute TwitterWpfClient.exe ahora. 

5. Haga clic en medios sociales del toocollect de botón Inicio verde Hola. Ver eventos de Tweet con hello **registroen**, **tema**, y **SentimentScore** valores que se va a enviar tooyour concentrador de eventos.

    ![Aplicación de TwitterWpfClient en ejecución, mostrando una lista de tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >Si ve errores y no ve una secuencia de tweets de muestra en la parte inferior de Hola de ventana hello, vuelva a comprobar los secretos y las claves de Hola. Compruebe también la cadena de conexión de hello (asegúrese de que no incluyen hello `EntityPath` clave y valor.)


## <a name="create-a-stream-analytics-job"></a>Creación de un trabajo de Análisis de transmisiones

Ahora que están transmitiendo por secuencias de eventos de tweet en tiempo real de Twitter, puede configurar una tooanalyze de trabajo de análisis de transmisiones estos eventos en tiempo real.

1. Hola portal de Azure, haga clic en **New** > **Internet de las cosas** > **trabajo de análisis de transmisiones**.

2. Nombre de trabajo de hello `socialtwitter-sa-job` y especifique una suscripción, el grupo de recursos y la ubicación.

    Es una buena idea tooplace Hola hello y trabajo Centro de eventos en hello misma región para optimizar el rendimiento y lo que no hay tootransfer datos entre regiones.

    ![Creación de un trabajo de Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. Haga clic en **Crear**.

    se crea el trabajo de Hola y portal de hello muestra detalles del trabajo.


## <a name="specify-hello-job-input"></a>Especificar la entrada de trabajo de Hola

1. En el trabajo de análisis de transmisiones, en **trabajo topología** en medio de Hola de hoja de trabajo de hello, haga clic en **entradas**. 

2. Hola **entradas** hoja, haga clic en  **+ &nbsp;agregar** y, a continuación, rellene hoja Hola con estos valores:

    * **Alias de entrada**: usar el nombre de hello `TwitterStream`. Si usa otro nombre, anótelo porque lo necesitará más adelante.
    * **Tipo de origen**: seleccione **Flujo de datos**.
    * **Origen**: seleccione **Centro de eventos**.
    * **Opción de importación**: seleccione **Usar centro de eventos de la suscripción actual**. 
    * **Espacio de nombres de bus de servicio**: seleccione el espacio de nombres de la base de datos central de eventos de Hola que creó anteriormente (`<yourname>-socialtwitter-eh-ns`).
    * **Centro de eventos**: Centro de eventos de hello Select que creó anteriormente (`socialtwitter-eh`).
    * **Nombre de directiva de centro de eventos**: seleccione la directiva de acceso de Hola que creó anteriormente (`socialtwitter-access`).

    ![Creación de una entrada del trabajo de Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. Haga clic en **Crear**.


## <a name="specify-hello-job-query"></a>Especifique la consulta de la tarea hello

Stream Analytics admite un modelo de consulta declarativa simple que describe las transformaciones. toolearn más información acerca del lenguaje de hello, vea hello [referencia de lenguaje de consulta de análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx).  Este tutorial le ayuda a crear y probar varias consultas sobre datos de Twitter.

número de hello toocompare de menciones entre los temas, puede usar un [ventana de saltos de tamaño constante](https://msdn.microsoft.com/library/azure/dn835055.aspx) recuento de hello tooget de menciones por tema cada cinco segundos.

1. Hola cerrar **entradas** hoja si no lo ha hecho ya.

2. En la hoja de trabajo de hello, haga clic en hello **consulta** cuadro. Azure muestra entradas de Hola y salidas que se configuran para el trabajo de Hola y le permite crear una consulta que permite transforman flujo de entrada de hello mientras envía toohello salida.

3. Asegúrese de que se ejecuta dicha aplicación TwitterWpfClient Hola. 

3. Hola **consulta** hoja, haga clic en hello puntos siguiente toohello `TwitterStream` de entrada y, a continuación, seleccione **datos a partir de datos de ejemplo**.

    ![Menú Opciones toouse datos de ejemplo de Hola entrada de trabajo de análisis de transmisión por secuencias, con "Datos de ejemplo de entrada" seleccionados](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Se abrirá una hoja que le permite especificar la cantidad tooget de datos de ejemplo, definido en términos de cuánto tiempo tooread hello secuencia de entrada.

4. Establecer **minutos** too3 y, a continuación, haga clic en **Aceptar**. 
    
    ![Opciones de muestreo de flujo de entrada de hello, con "3 minutos" seleccionados.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure muestrea los datos del flujo de entrada de hello correspondientes a tres minutos y le avisa cuando los datos de ejemplo de Hola están listos. (Tardará unos minutos). 

    datos de ejemplo de Hola se almacenan temporalmente y están disponibles mientras tiene la ventana de consulta de hello abierto. Si cierra la ventana de consulta de hello, se descartan los datos de ejemplo de Hola y tiene toocreate un nuevo conjunto de datos de ejemplo. 

5. Cambie la consulta de hello en hello código editor toohello que sigue:

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    Si no usó `TwitterStream` como Hola alias para la entrada de hello, sustituya su alias para `TwitterStream` en consulta Hola.  

    Esta consulta utiliza hello **TIMESTAMP BY** toospecify un campo de marca de tiempo en hello carga toobe utilizado en el cálculo temporal Hola de palabra clave. Si no se especifica este campo, operación basada en ventanas de Hola se realiza mediante el tiempo de Hola que cada evento llegaron al concentrador de eventos de Hola. Obtenga más información en la sección de Hola "hora de llegada frente a tiempo de aplicación" de [referencia de consulta de análisis de transmisiones](https://msdn.microsoft.com/library/azure/dn834998.aspx).

    Esta consulta también tiene acceso a una marca de tiempo para el fin de Hola de cada ventana mediante hello **System.Timestamp** propiedad.

5. Haga clic en **Probar**. Hola consulta se ejecuta con datos de Hola que realizó el muestreo.
    
6. Haga clic en **Guardar**. Esto ahorra consulta hello como parte del trabajo de análisis de transmisión por secuencias de Hola. (No guardar los datos de ejemplo de Hola.)


## <a name="experiment-using-different-fields-from-hello-stream"></a>Experimentar con distintos campos de secuencia de Hola 

Hello tabla siguiente enumeran los campos de Hola que forman parte del programa Hola a datos de transmisión por secuencias de JSON. Sentirse tooexperiment disponible en el editor de consultas Hola.

|Propiedad JSON | Definición|
|--- | ---|
|CreatedAt | tiempo de Hola se creó ese tweet Hola|
|Tema. | tema de Hola que coincide con hello especificados (palabra clave)|
|SentimentScore | puntuación de opinión de Hola de Sentiment140|
|Autor | identificador de Twitter de Hola que envían tweet Hola|
|Texto | cuerpo total de Hola de tweet Hola|


## <a name="create-an-output-sink"></a>Creación de un receptor de salida

Ahora ha definido un flujo de eventos, una entrada tooingest de concentrador de eventos y un tooperform consulta una transformación en secuencia Hola. Hola último paso es toodefine un receptor de salida para el trabajo de Hola.  

En este tutorial, escribe Hola agregado tweet eventos desde Hola trabajo consulta tooAzure almacenamiento de blobs.  También puede insertar su tooAzure de resultados de la base de datos de SQL, almacenamiento de tabla de Azure, los concentradores de eventos, o Power BI, dependiendo de la aplicación necesita.

## <a name="specify-hello-job-output"></a>Especificar la salida del trabajo Hola

1. Hola **trabajo topología** sección, haga clic en hello **salida** cuadro. 

2. Hola **salidas** hoja, haga clic en  **+ &nbsp;agregar** y, a continuación, rellene hoja Hola con estos valores:

    * **Alias de salida**: usar el nombre de hello `TwitterStream-Output`. 
    * **Receptor**: seleccione **Blob Storage**.
    * **Opciones de importación**: seleccione **Usar almacenamiento de blobs de la suscripción actual**.
    * **Cuenta de Storage**. Seleccione **Crear una nueva cuenta de almacenamiento**.
    * **Cuenta de Storage** (segundo cuadro). Escriba `YOURNAMEsa`, donde `YOURNAME` sea su nombre u otra cadena única. nombre de Hello puede usar solo letras minúsculas y números, y debe ser único en Azure. 
    * **Contenedor**. Escriba `socialtwitter`.
    nombre de cuenta de almacenamiento de Hola y el nombre del contenedor son tooprovide junto usa un URI para el almacenamiento de blobs de hello, similar al siguiente: 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Hoja "Nueva salida" del trabajo de Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. Haga clic en **Crear**. 

    Azure crea la cuenta de almacenamiento de Hola y genera una clave automáticamente. 

5. Hola cerrar **salidas** hoja. 


## <a name="start-hello-job"></a>Iniciar el trabajo de Hola

Se especifican una entrada de trabajo, la consulta y la salida. Son trabajo de análisis de transmisiones de hello toostart listo.

1. Asegúrese de que se ejecuta dicha aplicación TwitterWpfClient Hola. 

2. En la hoja de trabajo de hello, haga clic en **iniciar**.

    ![Iniciar el trabajo de análisis de transmisiones de Hola](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. Hola **Start job** hoja, para **hora de inicio de salida del trabajo**, seleccione **ahora** y, a continuación, haga clic en **iniciar**. 

    !["Iniciar el trabajo" hoja de trabajo de análisis de transmisiones de Hola](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure le avisa cuando ha iniciado el trabajo de Hola y de hoja de trabajo de hello, estado de Hola se muestra como **ejecutando**.

    ![Trabajo en ejecución](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>Consulta de la salida del análisis de opinión

Después de que el trabajo ha empezado a ejecutarse y está procesando transmisiones en tiempo real de Twitter de hello, puede ver la salida de hello para el análisis de opiniones.

Puede usar una herramienta como [Azure Storage Explorer](https://http://storageexplorer.com/) o [explorador Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview su trabajo de salida en tiempo real. Desde aquí, puede usar [Power BI](https://powerbi.com/) tooextend su tooinclude de aplicación un panel personalizado, como se muestra en la siguiente captura de pantalla de Hola Hola:

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>Cree otra consulta tooidentify tendencias temas

Puede usar la opinión de Twitter toounderstand de otra consulta se basa en un [ventana deslizante](https://msdn.microsoft.com/library/azure/dn835051.aspx). tooidentify temas tendencias, busca temas que cruzan un valor de umbral para menciones en un período de tiempo especificado.

Para fines de Hola de este tutorial, busque los temas que se mencionan más de 20 veces en hello últimos 5 segundos.

1. En la hoja de trabajo de hello, haga clic en **detener** trabajo de hello toostop. 

2. Hola **trabajo topología** sección, haga clic en hello **consulta** cuadro. 

3. Cambiar Hola consulta toohello a continuación:

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. Haga clic en **Guardar**.

5. Asegúrese de que se ejecuta dicha aplicación TwitterWpfClient Hola. 

6. Haga clic en **iniciar** trabajo de hello toorestart mediante Hola nueva consulta.


## <a name="get-support"></a>Obtención de soporte técnico
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
