# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Introducción al uso de Análisis de transmisiones de Azure: detección de fraudes en tiempo real

Este tutorial proporciona una ilustración to-end de cómo toouse análisis de transmisiones de Azure. Aprenderá a: 

* Incorporar eventos de streaming a una instancia de Azure Event Hubs. En este tutorial, usará una aplicación que le ofrecemos que simula un flujo de registros de metadatos de teléfono móvil.

* Escribir datos de tootransform análisis de transmisiones similar a SQL las consultas, agregar información o buscar patrones. Verá cómo toouse una tooexamine consulta hello secuencia entrante y busque las llamadas que podrían ser fraudulentas.

* Enviar Hola el receptor de salida de tooan de resultados (almacenamiento) que pueda analizar información adicional. En este caso, enviaremos el almacenamiento de blobs de hello llamada sospechosa datos tooAzure.

En este tutorial, usamos el ejemplo hello de detección de fraudes en tiempo real en función de los datos de llamada de teléfono. Pero técnica Hola que se muestran también es ideal para otros tipos de detección de fraudes, por ejemplo, tarjeta de crédito fraude o robo de identidad. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Escenario: telecomunicaciones y detección de fraudes de SIM en tiempo real

Una empresa de telecomunicaciones tiene un gran volumen de datos en llamadas entrantes. compañía de Hello desea toodetect fraudulenta llama en tiempo real para que puedan notificar a los clientes o apagar el servicio durante un número específico. Un tipo de fraude SIM implica varias llamadas de hello misma identidad alrededor de hello mismo tiempo pero en ubicaciones geográficamente diferentes. toodetect este tipo de fraude, Hola registros entrantes de teléfono de la compañía necesidades tooexamine y buscar patrones específicos, en este caso, para las llamadas realizadas alrededor de hello mismo tiempo en distintos países. Las entradas de teléfono que entran en esta categoría se escriben toostorage para su análisis posterior.

## <a name="prerequisites"></a>Requisitos previos

En este tutorial, simulará datos de llamadas telefónicas mediante una aplicación cliente que genera metadatos de llamada telefónica de muestra. Algunos de los registros de Hola que Hola aplicación genera aspecto llamadas fraudulentos. 

Antes de empezar, asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure.
* aplicación del generador de evento de llamada de Hello. Puede obtener mediante la descarga de hello [TelcoGenerator.zip archivo](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) de hello Microsoft Download Center. Descomprima este paquete un una carpeta en el equipo. Si desea código fuente de toosee hello y aplicación de hello de ejecución en un depurador, puede obtener el código fuente de aplicación Hola de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >Windows pueden bloquear el archivo .zip de hello descargado. Si no se descomprímalo, haga clic en el archivo de Hola y seleccione **propiedades**. Si ve Hola mensaje "este archivo procede de otro equipo y podría ser bloqueado toohelp proteger este equipo", seleccione hello **Unblock** opción y, a continuación, haga clic en **aplicar**.

Si desea que los resultados de hello tooexamine de trabajo de análisis de transmisión por secuencias de hello, también necesita una herramienta de visualización del contenido de Hola de un contenedor de almacenamiento de blobs de Azure. Si utiliza Visual Studio, puede usar [Azure Tools para Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) o [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). También puede instalar herramientas independientes, tales como [Explorador de Azure Storage](http://storageexplorer.com/) y [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Crear un evento Azure tooingest de los concentradores de eventos

tooanalyze un flujo de datos, se *Introducción* en Azure. Una forma habitual de datos de tooingest es toouse [centros de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md), que le permite introducir millones de eventos por segundo y, a continuación, procesar y almacenar información sobre eventos de Hola. Para este tutorial, crea un centro de eventos y, a continuación, tiene Hola evento de llamada generador aplicación envío llamada datos toothat concentrador de eventos. Para obtener más información acerca de los centros de eventos, vea hello [documentación de Service Bus de Azure](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Para obtener una versión más detallada de este procedimiento, consulte [crear un espacio de nombres de los centros de eventos y un concentrador de eventos mediante Hola portal de Azure](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Creación de un espacio de nombres y un centro de eventos
En este procedimiento, primero cree un espacio de nombres del centro de eventos y, a continuación, agregue un namepsace de toothat de concentrador de eventos. Los espacios de nombres del concentrador de eventos se utilizan instancias de bus de eventos relacionados con el grupo de toologically. 

1. Inicie sesión en el portal de Azure de Hola y haga clic en **New** > **Internet de las cosas** > **concentrador de eventos**. 

2. Hola **crear espacio de nombres** hoja, escriba un nombre de espacio de nombres como `<yourname>-eh-ns-demo`. Puede utilizar cualquier nombre de espacio de nombres de hello, pero Hola nombre debe ser válido para una dirección URL y debe ser único en Azure. 
    
3. Seleccione una suscripción y cree o elija un grupo de recursos. Luego haga clic en **Crear**. 

    ![Creación de un espacio de nombres del centro de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Cuando el espacio de nombres de hello ha terminado de implementar, buscar espacio de nombres del concentrador de eventos de hello en la lista de recursos de Azure. 

5. Haga clic en nuevo espacio de nombres Hola y en la hoja de espacio de nombres de hello, haga clic en  **+ &nbsp;concentrador de eventos**. 

    ![botón de agregar el concentrador de eventos de Hola para crear un nuevo centro de eventos ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Nuevo centro de eventos de nombre hello `sa-eh-frauddetection-demo`. Puede usar otro nombre. Si lo hace, tome nota del mismo, porque necesita Hola nombre más adelante. No es necesario tooset cualquier otra opción de concentrador de eventos de hello ahora mismo.

    ![Hoja para la creación de un centro de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. Haga clic en **Crear**.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Conceda el concentrador de eventos de acceso toohello y obtener una cadena de conexión

Antes de que un proceso puede enviar el concentrador de eventos de datos tooan, centro de eventos de hello debe tener una directiva que permita el acceso adecuado. Directiva de acceso de Hello genera una cadena de conexión que incluya la información de autorización.

1.  En la hoja de espacio de nombres de evento de hello, haga clic en **centros de eventos** y, a continuación, haga clic en nombre de Hola de su nuevo concentrador de eventos.

2.  En la hoja de concentrador de eventos de hello, haga clic en **directivas de acceso compartido** y, a continuación, haga clic en  **+ &nbsp;agregar**.

    >[!NOTE]
    >Asegúrese de que está trabajando con el concentrador de eventos de hello, no Hola eventos concentrador espacio de nombres.

3.  Agregue una directiva denominada `sa-policy-manage-demo` y, en **Notificación**, seleccione **Administrar**.

    ![Hoja para la creación de una directiva de acceso al centro de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  Haga clic en **Crear**.

5.  Después de que se ha implementado la directiva de hello, haga clic en la lista de Hola de directivas de acceso compartido.

6.  Cuadro de búsqueda Hola etiquetado **clave principal de la cadena de conexión** y haga clic en la cadena de conexión de hello copia botón siguiente toohello. 
    
    ![Copiar la clave de cadena de conexión principal de Hola Hola directiva de acceso](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Pegue la cadena de conexión de hello en un editor de texto. Necesita esta cadena de conexión para la sección siguiente de hello, después de realizar algunos tooit pequeñas modificaciones.

    cadena de conexión de Hello tiene el siguiente aspecto:

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Tenga en cuenta que la cadena de conexión de hello contiene varios pares de clave y valor, separados por punto y coma: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, y `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Configurar e iniciar la aplicación de generador de eventos de hello

Antes de iniciar la aplicación de hello TelcoGenerator, configúrelo para que enviará el concentrador de eventos de llamada registros toohello que acaba de crear.

### <a name="configure-hello-telcogeneratorapp"></a>Configurar hello TelcoGeneratorapp

1.  En el editor de Hola donde copió la cadena de conexión de hello, tome nota de hello `EntityPath` valor y, a continuación, quite hello `EntityPath` par (no olvide tooremove Hola por punto y coma que lo precede). 

2.  En carpeta de Hola donde descomprimió el archivo de TelcoGenerator.zip hello, abra el archivo de telcodatagen.exe.config de hello en un editor. (Hay más de un archivo .config, por tanto, asegúrese de que abra derecha hello).

3.  Hola `<appSettings>` elemento, hacer esto:

    * Establecer valor de Hola de hello `EventHubName` nombre centro de eventos clave toohello (es decir, el valor de toohello de ruta de acceso de hello entidad).
    * Establecer valor de Hola de hello `Microsoft.ServiceBus.ConnectionString` clave de cadena de conexión toohello. 

    Hola `<appSettings>` sección tendrá un aspecto como el siguiente ejemplo de Hola. (Para mayor claridad, se ajustan las líneas de Hola y quitan algunos caracteres de token de autorización de Hola.)

    ![Archivo de configuración de aplicación de TelcoGenerator que muestra la cadena de conexión y nombre de la base de datos central del evento Hola](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Guarde el archivo hello. 

### <a name="start-hello-app"></a>Iniciar aplicación hello
1.  Abra una ventana de comandos y cambie la carpeta toohello donde se descomprime hello TelcoGenerator aplicación.
2.  Escriba el siguiente comando de hello:

        telcodatagen.exe 1000 .2 2

    Hola parámetros son: 

    * Número de registros CDR por hora. 
    * Probabilidad de fraude de tarjeta SIM: La frecuencia, como un porcentaje de todas las llamadas, esa aplicación hello debe simular una llamada fraudulenta. valor de Hello.2 significa que aproximadamente el 20% de los registros de llamada de hello tendrá un aspecto fraudulento.
    * Duración en horas. número de Hola de horas que Hola aplicación debe ejecutar. También puede detener aplicación hello cualquier momento presionando Ctrl + C en línea de comandos de Hola.

    Después de unos segundos, aplicación hello comienza a mostrar los registros de llamada de teléfono en la pantalla de bienvenida tal y como lo envía toohello concentrador de eventos.

Algunos de los campos de clave de Hola que va a usar en esta aplicación de detección de fraudes en tiempo real son siguientes de hello:

|**Registro**|**Definición**|
|----------|--------------|
|`CallrecTime`|hora de inicio de la marca de tiempo de Hola de llamada de Hola. |
|`SwitchNum`|modificador de teléfono de Hello usa llamadas de hello tooconnect. En este ejemplo, conmutadores de hello son cadenas que representan el país de Hola de origen (Estados Unidos, China, del Reino Unido, Alemania o Australia). |
|`CallingNum`|número de teléfono de Hello del autor de llamada de Hola. |
|`CallingIMSI`|Hola identidad del suscriptor móvil internacional (IMSI). Se trata de un identificador único de hello del autor de llamada de Hola. |
|`CalledNum`|número de teléfono de Hello del destinatario de la llamada de Hola. |
|`CalledIMSI`|Identidad del suscriptor móvil internacional (IMSI). Se trata de un identificador único de hello del destinatario de la llamada de Hola. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Crear un toomanage de trabajo de análisis de transmisiones transmisión de datos

Ahora que tiene un flujo de eventos de llamada, puede configurar un trabajo de Stream Analytics. trabajo de Hello leerá los datos desde el concentrador de eventos de Hola que configuró. 

### <a name="create-hello-job"></a>Crear trabajo de Hola 

1. Hola portal de Azure, haga clic en **New** > **Internet de las cosas** > **trabajo de análisis de transmisiones**.

2. Nombre de trabajo de hello `sa_frauddetection_job_demo`, especifique una suscripción, el grupo de recursos y la ubicación.

    Es una buena idea tooplace Hola hello y trabajo Centro de eventos en hello misma región para optimizar el rendimiento y lo que no hay tootransfer datos entre regiones.

    ![Creación de un trabajo de Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. Haga clic en **Crear**.

    se crea el trabajo de Hola y portal de hello muestra detalles del trabajo. Nada está ejecutando todavía, sin embargo, tiene tooconfigure Hola trabajo antes de que se puede iniciar.

### <a name="configure-job-input"></a>Configuración de la entrada del trabajo

1. En el panel de Hola o hello **todos los recursos** hoja, busque y seleccione hello `sa_frauddetection_job_demo` trabajo de análisis de transmisiones. 
2. Hola **trabajo topología** sección de hello hoja de trabajo de análisis de transmisiones, haga clic en hello **entrada** cuadro.

    ![Cuadro de entrada en la topología en la hoja de trabajo de análisis de transmisión por secuencias de Hola](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Haga clic en  **+ &nbsp;agregar** y, a continuación, rellene hoja Hola con estos valores:

    * **Alias de entrada**: usar el nombre de hello `CallStream`. Si usa otro nombre, anótelo porque lo necesitará más adelante.
    * **Tipo de origen**: seleccione **Flujo de datos**. (**Hacen referencia a datos** hace referencia a datos de búsqueda de toostatic, que no usan en este tutorial.)
    * **Origen**: seleccione **Centro de eventos**.
    * **Opción de importación**: seleccione **Usar centro de eventos de la suscripción actual**. 
    * **Espacio de nombres de bus de servicio**: seleccione el espacio de nombres de la base de datos central de eventos de Hola que creó anteriormente (`<yourname>-eh-ns-demo`).
    * **Centro de eventos**: Centro de eventos de hello Select que creó anteriormente (`sa-eh-frauddetection-demo`).
    * **Nombre de directiva de centro de eventos**: seleccione la directiva de acceso de Hola que creó anteriormente (`sa-policy-manage-demo`).

    ![Creación de una entrada del trabajo de Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. Haga clic en **Crear**.

## <a name="create-queries-tootransform-real-time-data"></a>Crear consultas de datos en tiempo real de tootransform

En este punto, tiene un trabajo de análisis de transmisiones configurar tooread un flujo de datos entrante. Hola siguiente paso es toocreate una transformación que analiza los datos de hello en tiempo real. Para ello, cree una consulta. Stream Analytics admite un modelo de consulta declarativo sencillo que describe las transformaciones para el procesamiento en tiempo real. las consultas de Hello utilizan un lenguaje parecido a SQL que tiene algunos análisis toostream específico de extensiones. 

Una consulta muy simple simplemente podría leer todos los datos entrantes de saludo. Sin embargo, a menudo se crean consultas que buscan para datos específicos o para las relaciones en datos Hola. En esta sección del tutorial de hello, creará y probará varias consultas toolearn varias maneras en que puede transformar una secuencia de entrada para el análisis. 

las consultas de Hola que se crean aquí solo mostrará pantalla de bienvenida datos transformados toohello. En una sección posterior, configurará un receptor de salida y una consulta que escribe Hola datos transformados toothat receptor.

toolearn más información acerca del lenguaje de hello, vea hello [referencia de lenguaje de consulta de análisis de transmisiones de Azure](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Obtención de datos de muestra para probar las consultas

Hola TelcoGenerator aplicación está enviando concentrador de eventos de llamada registros toohello, y el trabajo de análisis de transmisiones está tooread configurado de concentrador de eventos de Hola. Puede usar una consulta tootest Hola trabajo toomake seguro de que está leyendo correctamente. demasiado probar una consulta en hello consola de Azure, necesita los datos de ejemplo. En este tutorial, podrá extraer datos de ejemplo de secuencia de Hola que procede a centro de eventos de Hola.

1. Asegúrese de que hello TelcoGenerator aplicación se esté ejecutando y generar registros de llamada.
2. En el portal de hello, devolver la hoja de trabajo de análisis de transmisión por secuencias de toohello. (Si lo ha cerrado hoja hello, busque `sa_frauddetection_job_demo` en hello **todos los recursos** hoja.)
3. Haga clic en hello **consulta** cuadro. Azure muestra entradas de Hola y salidas que se configuran para el trabajo de Hola y le permite crear una consulta que permite transforman flujo de entrada de hello mientras envía toohello salida.
4. Hola **consulta** hoja, haga clic en hello puntos siguiente toohello `CallStream` de entrada y, a continuación, seleccione **datos a partir de datos de ejemplo**.

    ![Menú Opciones toouse datos de ejemplo de Hola entrada de trabajo de análisis de transmisión por secuencias, con "Datos de ejemplo de entrada" seleccionados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Se abrirá una hoja que le permite especificar la cantidad tooget de datos de ejemplo, definido en términos de cuánto tiempo tooread hello secuencia de entrada.

5. Establecer **minutos** too3 y, a continuación, haga clic en **Aceptar**. 
    
    ![Opciones de muestreo de flujo de entrada de hello, con "3 minutos" seleccionados.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure muestrea los datos del flujo de entrada de hello correspondientes a tres minutos y le avisa cuando los datos de ejemplo de Hola están listos. (Tardará unos minutos). 

datos de ejemplo de Hola se almacenan temporalmente y están disponibles mientras tiene la ventana de consulta de hello abierto. Si cierra la ventana de consulta de hello, se descartan los datos de ejemplo de Hola y tendrá toocreate un nuevo conjunto de datos de ejemplo. 

Como alternativa, puede obtener un archivo .json que contiene los datos de ejemplo [desde GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)y, a continuación, cargar ese toouse de archivo .json como datos de ejemplo de Hola `CallStream` entrada. 

### <a name="test-using-a-pass-through-query"></a>Prueba con una consulta de paso a través

Si desea tooarchive todos los eventos, puede usar una consulta de paso a través de tooread todos los campos de hello en carga Hola de evento de Hola.

1. En la ventana de consulta de hello, escriba esta consulta:

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >Al igual que con SQL, las palabras clave no distinguen entre mayúsculas y minúsculas y un espacio en blanco no es significativo.

    En esta consulta, `CallStream` es Hola alias que especificó cuando creó la entrada de Hola. Si ha usado otro alias, use ese nombre en su lugar.

2. Haga clic en **Probar**.

    trabajo de análisis de transmisiones de Hola ejecuta la consulta de hello con datos de ejemplo de Hola y muestra el resultado de hello en parte inferior de Hola de ventana hello. Esto indica que concentrador de eventos de Hola y de trabajo de análisis de transmisión por secuencias de hello están configuradas correctamente. (Como se indicó, más adelante podrá crear un receptor de salida que Hola consulta puede escribir datos en.)

    ![Salida del trabajo de Stream Analytics que muestra 73 registros generados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    número exacto de Hola de registros que aparecen depende de cuántos registros se han capturado en el ejemplo de 3 minutos.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Reducir el número de Hola de campos utilizando una proyección de columna

En muchos casos, el análisis no necesita todas las columnas de Hola Hola flujo de entrada. Puede usar un tooproject consulta un conjunto más pequeño de devuelve campos que en la consulta de paso a través de Hola.

1. Cambie la consulta de hello en hello código editor toohello que sigue:

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Haga clic de nuevo en **Probar**. 

    ![Salida del trabajo de Stream Analytics correspondiente a la proyección que muestra 25 registros generados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Recuento de llamadas entrantes por región: ventana de saltos de tamaño constante con agregación

Suponga que desea toocount Hola número de llamadas entrantes por región. En la transmisión de datos, cuando desee que las funciones de agregado de tooperform como el recuento, necesita toosegment Hola flujo en unidades temporales (puesto que propio flujo de datos hello es eficazmente sin fin). Para ello, use una [función de ventana](stream-analytics-window-functions.md) de Stream Analytics. A continuación, puede trabajar con datos de saludo dentro de esa ventana como una unidad.

Para esta transformación, se busca una secuencia de ventanas temporales que no se superpongan; cada ventana tendrá un conjunto discreto de datos que se pueden agrupar y agregar. Este tipo de ventana es tooas que se hace referencia una *ventana de saltos de tamaño constante* . En la ventana de saltos de tamaño constante de hello, puede obtener un recuento de llamadas entrantes de hello agrupados por `SwitchNum`, que representa el país de Hola donde se originó la llamada de Hola. 

1. Cambie la consulta de hello en hello código editor toohello que sigue:

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    Esta consulta utiliza hello `Timestamp By` palabra clave en hello `FROM` toospecify cláusula qué campo de marca de tiempo en hello ventana de saltos de tamaño constante de hello de toodefine de toouse de flujo de entrada. En este caso, ventana hello divide los datos de hello en segmentos por hello `CallRecTime` campo en cada registro. (Si no se especifica ningún campo, la operación de ventana hello utiliza tiempo Hola que cada evento llega al centro de eventos de Hola. Vea "Tiempo de llegada frente a tiempo de aplicación" en [Referencia de lenguaje de consulta de Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    proyección de Hello incluye `System.Timestamp`, que devuelve una marca de tiempo para el fin de Hola de cada ventana. 

    toospecify que desea toouse una ventana de saltos de tamaño constante, usas hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) función Hola `GROUP BY `cláusula. En función de hello, especifique una unidad de tiempo (en cualquier parte de un día de tooa microsegundos) y un tamaño de ventana (el número de unidades). En este ejemplo, ventana de saltos de tamaño constante de hello consta de intervalos de 5 segundos, por lo que se obtendrá un recuento por país para llamadas correspondientes a cada 5 segundos.

2. Haga clic de nuevo en **Probar**. En los resultados de hello, tenga en cuenta que las marcas de tiempo de hello en **WindowEnd** en incrementos de 5 segundos.

    ![Salida del trabajo de Stream Analytics correspondiente a la agregación que muestra 13 registros generados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Detección de fraudes de SIM mediante una autocombinación

En este ejemplo, podemos consideramos uso fraudulento toobe llamadas que se originan en hello mismo usuario, pero en diferentes ubicaciones en 5 segundos entre sí. Por ejemplo, hello mismo usuario no puede legítimamente realizar una llamada de hello Estados Unidos y Australia en hello mismo tiempo. 

toocheck para estos casos, puede utilizar una autocombinación de transmisión por secuencias datos toojoin hello secuencia tooitself en función de Hola de hello `CallRecTime` valor. A continuación, puede buscar de llamada registra donde hello `CallingIMSI` valor (Hola número original) es Hola mismo pero Hola `SwitchNum` valor (país de origen) no es Hola igual.

Cuando se usa una combinación con la transmisión de datos, debe proporcionar combinación Hola algunas limitaciones en la diferencia entre Hola hacer coincidir las filas se pueden separar en el tiempo. (Tal y como se indicó anteriormente, Hola transmisión de datos es eficaz sin fin). se especifican los límites de tiempo de Hello para la relación de Hola de hello `ON` cláusula de combinación de hello, con hello `DATEDIFF` función. En este caso, la combinación de Hola se basa en un intervalo de 5 segundos de datos de la llamada.

1. Cambie la consulta de hello en hello código editor toohello que sigue: 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    Esta consulta es similar a cualquier combinación SQL excepto hello `DATEDIFF` función de combinación de Hola. Se trata de una versión de `DATEDIFF` tooStreaming específico de análisis, y debe aparecer en hello `ON...BETWEEN` cláusula. parámetros de Hello son alias de Hola de dos orígenes de Hola para una combinación de hello y una unidad de tiempo (en segundos en este ejemplo). (Esto es diferente de Hola SQL estándar `DATEDIFF` función.) 

    Hola `WHERE` cláusula incluye condición Hola que marca llamada fraudulentas hello: conmutadores origen hello no son Hola igual. 

2. Haga clic de nuevo en **Probar**. 

    ![Salida del trabajo de Stream Analytics correspondiente a la autocombinación que muestra seis registros generados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. Haga clic en **Guardar**. Esto ahorra la consulta de autocombinación de hello como parte del trabajo de análisis de transmisión por secuencias de Hola. (No guardar los datos de ejemplo de Hola.)

    ![Almacenamiento del trabajo de Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Crear un receptor de salida toostore transformar datos

Se ha definido un flujo de eventos, una entrada tooingest de concentrador de eventos y un tooperform consulta una transformación en secuencia Hola. Hola último paso es toodefine un receptor de salida para el trabajo de hello, es decir, un Hola de toowrite lugar transforma flujo a. 

Puede usar muchos recursos como receptores de salida: una base de datos de SQL Server, Table Storage, Data Lake Store, Power BI e incluso otro centro de eventos. Para este tutorial, escribirá hello secuencia tooAzure almacenamiento de blobs, que es una opción típica para recopilar información de eventos para su análisis posterior, ya que se adapta a los datos no estructurados.

Si ya tiene una cuenta de Blob Storage, puede utilizarla. Para este tutorial, le mostraremos cómo toocreate un nueva cuenta de almacenamiento, solo para este tutorial.

### <a name="create-an-azure-blob-storage-account"></a>Creación de una cuenta de Azure Blob Storage

1. Hola portal de Azure, devolver la hoja de trabajo de análisis de transmisión por secuencias de toohello. (Si lo ha cerrado hoja hello, busque `sa_frauddetection_job_demo` en hello **todos los recursos** hoja.)
2. Hola **trabajo topología** sección, haga clic en hello **salida** cuadro. 
3. Hola **salidas** hoja, haga clic en  **+ &nbsp;agregar** y, a continuación, rellene hoja Hola con estos valores:

    * **Alias de salida**: usar el nombre de hello `CallStream-FraudulentCalls`. 
    * **Receptor**: seleccione **Blob Storage**.
    * **Opciones de importación**: seleccione **Usar almacenamiento de blobs de la suscripción actual**.
    * **Cuenta de Storage**. Seleccione **Crear nueva cuenta de almacenamiento**.
    * **Cuenta de Storage** (segundo cuadro). Escriba `YOURNAMEsademo`, donde `YOURNAME` sea su nombre u otra cadena única. nombre de Hello puede usar solo letras minúsculas y números, y debe ser único en Azure. 
    * **Contenedor**. Escriba `sa-fraudulentcalls-demo`.
    nombre de cuenta de almacenamiento de Hola y el nombre del contenedor son tooprovide junto usa un URI para el almacenamiento de blobs de hello, similar al siguiente: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Hoja "Nueva salida" del trabajo de Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. Haga clic en **Crear**. 

    Azure crea la cuenta de almacenamiento de Hola y genera una clave automáticamente. 

5. Hola cerrar **salidas** hoja. 

## <a name="start-hello-streaming-analytics-job"></a>Iniciar trabajo de análisis de transmisión por secuencias de Hola

trabajo de Hello ya está configurada. Ha especificado una entrada (centro de eventos de hello), una transformación (hello toolook de consulta para las llamadas fraudulentas) y una salida (almacenamiento de blobs). Ahora puede iniciar el trabajo de Hola. 

1. Asegúrese de que está ejecutando la aplicación de hello TelcoGenerator.

2. En la hoja de trabajo de hello, haga clic en **iniciar**.

    ![Iniciar el trabajo de análisis de transmisiones de Hola](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. Hola **Start job** hoja, de hora de inicio de salida trabajo, seleccione **ahora**. 

4. Haga clic en **Iniciar**. 

    !["Iniciar el trabajo" hoja de trabajo de análisis de transmisiones de Hola](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure le avisa cuando ha iniciado el trabajo de Hola y de hoja de trabajo de hello, estado de Hola se muestra como **ejecutando**.

    ![Estado del trabajo de Stream Analytics que muestra "En ejecución"](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Examinar los datos de hello transformado

Ya dispone de un trabajo de Stream Analytics completo. trabajo de Hello es examinar un flujo de metadatos de la llamada de teléfono, buscando fraudulentas llamadas telefónicas en tiempo real y escribir la información sobre esos toostorage llamadas fraudulentos. 

toocomplete este tutorial, puede querer toolook datos Hola captura si el trabajo de análisis de transmisión por secuencias de Hola. Hola los datos se escriben tooAzure almacenamiento de blobs en fragmentos (archivos). Puede usar cualquier herramienta que lea Azure Blob Storage. Como se indicó en la sección Requisitos previos de hello, puede usar las extensiones de Azure en Visual Studio, o puede usar una herramienta como [Azure Storage Explorer](http://storageexplorer.com/) o [explorador Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

Cuando examine el contenido de Hola de un archivo de almacenamiento de blobs, verá algo parecido a Hola siguiente:

![Azure Blob Storage con salida de Streaming Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Limpieza de recursos

Tenemos otros artículos que continúe con el escenario de detección de fraudes de Hola y que usan recursos de Hola que ha creado en este tutorial. Si desea toocontinue, consulte sugerencias de hello en **pasos siguientes** más tarde.

Sin embargo, si ha terminado y no necesita recursos Hola que ha creado, puede eliminarlos para que no se incurre en cobros innecesarios a Azure. En ese caso, se recomienda que Hola siguientes:

1. Detener el trabajo de análisis de transmisión por secuencias de Hola. Hola **trabajos** hoja, haga clic en **detener** en la parte superior de Hola.
2. Detener la aplicación del generador de telecomunicaciones hello. En la ventana de comandos de Hola donde se inició la aplicación hello, presione CTRL+c.
3. Si ha creado una cuenta de Blob Storage exclusivamente para este tutorial, elimínela. 
4. Eliminar trabajo de análisis de transmisión por secuencias de Hola.
5. Eliminar el concentrador de eventos de Hola.
6. Eliminar espacio de nombres del concentrador de eventos de Hola.

## <a name="get-support"></a>Obtención de soporte técnico

Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes

Puede seguir este tutorial con hello siguientes artículos:

* [Stream Analytics y Power BI: panel de análisis en tiempo real de flujo de datos](stream-analytics-power-bi-dashboard.md). Este artículo muestra cómo toosend Hola salida de telecomunicaciones de análisis de transmisiones de hello trabajo tooPower BI para su visualización en tiempo real y análisis.
* [¿Cómo toostore datos de análisis de transmisiones de Azure en una caché en Redis de Azure mediante las funciones de Azure](stream-analytics-functions-redis.md). Este artículo muestra cómo toouse funciones de Azure toowrite fraudulenta llama tooan caché de Redis de Azure a través de una cola de Bus de servicio.

Para más información sobre Stream Analytics en general, examine los siguientes artículos:

* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
