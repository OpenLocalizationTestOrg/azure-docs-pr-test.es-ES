---
title: "panel de BI de aaaPower en análisis de transmisiones de Azure | Documentos de Microsoft"
description: "Use un en tiempo real streaming Power BI panel toogather de business intelligence y análisis de datos de gran volumen de un trabajo de análisis de transmisiones."
keywords: "panel de análisis, panel en tiempo real"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Stream Analytics y Power BI: panel de análisis en tiempo real de flujo de datos
Análisis de transmisiones de Azure le permite tootake aprovechar uno de hello iniciales herramientas de business intelligence, [Microsoft Power BI](https://powerbi.com/). En este artículo, aprenderá a crear herramientas de inteligencia empresarial personalizadas utilizando Power BI como salida para los trabajos de Azure Stream Analytics. También aprenderá cómo toocreate y usar un panel en tiempo real.

Este artículo continúa a partir de análisis de transmisiones de hello [detección de fraudes en tiempo real](stream-analytics-real-time-fraud-detection.md) tutorial. Se basa en el flujo de trabajo de hello creado en este tutorial y agrega una Power BI, por lo que puede visualizar fraudulentas llamadas telefónicas que se detectó un trabajo de análisis de transmisión por secuencias de salida. 

Puede ver un [vídeo](https://www.youtube.com/watch?v=SGUpT-a99MA) que muestra este escenario.


## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure.
* Una cuenta de Power BI. Puede usar una cuenta profesional o una cuenta educativa.
* Una versión completada de hello [detección de fraudes en tiempo real](stream-analytics-real-time-fraud-detection.md) tutorial. tutorial de Hello incluye una aplicación que genera los metadatos de la llamada de teléfono ficticios. En el tutorial de hello, crear un centro de eventos y enviar Hola concentrador de eventos de llamada de teléfono datos toohello de transmisión por secuencias. Escribir una consulta que detecta llamadas fraudulentas (llamadas de hello mismo número en hello mismo tiempo en distintas ubicaciones). 


## <a name="add-power-bi-output"></a>Incorporación del resultado de Power BI
En el tutorial de detección de fraudes en tiempo real de hello, la salida de Hola se envía el almacenamiento de blobs de tooAzure. En esta sección, agregará una salida que envía información tooPower BI.

1. Hola portal de Azure, abra el trabajo de análisis de transmisión por secuencias de Hola que creó anteriormente. Si ha usado el nombre sugerido de hello, el trabajo de Hola se denomina `sa_frauddetection_job_demo`.

2. Seleccione hello **salidas** cuadro en medio de Hola de panel de trabajo de hello y, a continuación, seleccione **+ agregar**.

3. Como **Alias de salida**, escriba `CallStream-PowerBI`. Puede usar otro nombre. Si lo hace, tome nota del mismo, porque necesita Hola nombre más adelante. 

4. En **Receptor**, seleccione **Power BI**.

   ![Creación de una salida para Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Haga clic en **Autorizar**.

    Se abrirá una ventana donde puede especificar sus credenciales de Azure para una cuenta profesional o educativa. 

    ![Escriba las credenciales de acceso tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Escriba sus credenciales. Tenga en cuenta, a continuación, al escribir sus credenciales, está también da tooaccess de trabajo de análisis de transmisión por secuencias de permiso toohello su área de Power BI.

7. Cuando se le redirige toohello **nueva salida** hoja, escriba Hola siguiente información:

    * **Área de trabajo de grupo**: seleccione un área de trabajo en el inquilino de Power BI donde desea que el conjunto de datos de toocreate Hola.
    * **Nombre del conjunto de datos**: escriba `sa-dataset`. Puede usar otro nombre. Si lo hace, apúntelo para recordarlo más tarde.
    * **Nombre de la tabla**: escriba `fraudulent-calls`. Actualmente, la salida de Power BI de trabajos de Stream Analytics solo puede tener una tabla en un conjunto de datos.

    ![Área de trabajo de PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Si Power BI tiene un conjunto de datos y tabla cuyas Hola mismos nombres que Hola que especifique en el trabajo de análisis de transmisiones de hello, Hola existentes se sobrescribe.
    > Se recomienda no crear explícitamente este conjunto de datos y la tabla en la cuenta de Power BI. Se crean automáticamente al iniciar el trabajo de análisis de transmisiones y trabajo de Hola a partir del resultado bombeo Power BI. Si la consulta de trabajo no devuelve ningún resultado, no se crean la tabla y conjunto de datos de Hola.
    >

8. Haga clic en **Crear**.

se crea el conjunto de datos de Hello con hello después de configuración:

* **defaultRetentionPolicy: BasicFIFO**: los datos tienen un orden FIFO, con un máximo de 200 000 filas.
* **defaultMode: pushStreaming**: conjunto de datos de hello admite iconos de transmisión por secuencias y objetos visuales de informe basa tradicionales (conocido como) inserción).

Actualmente, no se pueden crear conjuntos de datos con otras marcas.

Para obtener más información acerca de los conjuntos de datos de Power BI, consulte hello [API de REST de Power BI](https://msdn.microsoft.com/library/mt203562.aspx) referencia.


## <a name="write-hello-query"></a>Escribir consulta Hola

1. Hola cerrar **salidas** hoja y hoja de trabajo de toohello devuelto.

2. Haga clic en hello **consulta** cuadro. 

3. Escriba Hola después de consulta. Esta consulta es similar toohello autocombinación que creó en el tutorial de detección de fraudes Hola. Hello diferencia es que esta consulta envía resultados toohello nueva salida que ha creado (`CallStream-PowerBI`). 

    >[!NOTE]
    >Si no asigna un nombre hello entrada `CallStream` en tutorial de detección de fraudes de hello, sustituya el nombre de `CallStream` en hello **FROM** y **UNIR** cláusulas de consulta de Hola.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. Haga clic en **Guardar**.


## <a name="test-hello-query"></a>Consulta de Hola de prueba
Esta sección es opcional pero conveniente. 

1. Si la aplicación de hello TelcoStreaming no se está ejecutando, inícielo siguiendo estos pasos:

    * Abra el símbolo del sistema.
    * Carpeta de toohello vaya donde se telcogenerator.exe hello y archivos telcodatagen.exe.config modificado.
    * Ejecute el siguiente comando de hello:

            telcodatagen.exe 1000 .2 2

2. Hola **consulta** hoja, haga clic en hello puntos siguiente toohello `CallStream` de entrada y, a continuación, seleccione **datos a partir de datos de ejemplo**.

3. Especifique que quiere datos correspondientes a tres minutos y haga clic en **OK**. Espere hasta que se le notifica que se han tomado como muestra datos de Hola.

4. Haga clic en **Probar** y asegúrese de que obtiene resultados.


## <a name="run-hello-job"></a>Ejecutar trabajo de Hola

1. Asegúrese de que está ejecutando la aplicación hello TelcoStreaming.

2. Hola cerrar **consulta** hoja.

3. En la hoja de trabajo de hello, haga clic en **iniciar**.

    ![Iniciar el trabajo de análisis de transmisiones de Hola](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

Su trabajo de análisis de transmisión por secuencias comienza buscando llamadas fraudulentas en secuencia de entrada de Hola. trabajo de Hello también crea el conjunto de datos de hello y una tabla en Power BI y comienza a enviar datos sobre Hola llamadas fraudulentas toothem.


## <a name="create-hello-dashboard-in-power-bi"></a>Crear panel hello en Power BI

1. Vaya demasiado[Powerbi.com](https://powerbi.com) e inicie sesión con su cuenta profesional o educativa. Si la consulta de trabajo de análisis de transmisiones de hello genera resultados, verá que ya se ha creado el conjunto de datos:

    ![Conjunto de datos de streaming en Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. En el área de trabajo, haga clic en **+&nbsp;Crear**.

    ![botón Crear de Hello en el área de trabajo de Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Cree otro panel y asígnele el nombre `Fraudulent Calls`.

    ![Creación de un panel y asignación de un nombre en el área de trabajo de Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. Hola parte superior de ventana hello, haga clic en **agregar icono**, seleccione **datos de transmisión personalizados**y, a continuación, haga clic en **siguiente**.

    ![Conjunto de datos de streaming personalizados](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. En **YOUR DATSETS** (SUS CONJUNTOS DE DATOS), seleccione el conjunto de datos y haga clic en **Siguiente**.

    ![Su conjunto de datos de streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. En **tipo de visualización**, seleccione **tarjeta**y, a continuación, en hello **campos** lista, seleccione **fraudulentcalls**.

    ![Detalles de visualización del nuevo icono](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. Haga clic en **Siguiente**.

8. Rellene detalles del icono, como el título y el subtítulo.

    ![Título y subtítulo del nuevo icono](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. Haga clic en **Apply**.

    Ahora tiene un contador de fraudes.

    ![Contador de fraudes](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. Hola siga los pasos del nuevo tooadd un icono (comenzando con el paso 4). En esta ocasión, Hola siguientes:

    * Al obtener demasiado**tipo de visualización**, seleccione **gráfico de líneas**. 
    * Agregue un eje y seleccione **windowend**. 
    * Agregue un valor y seleccione **fraudulentcalls**.
    * Para **toodisplay de la ventana de tiempo**, seleccione Hola últimos 10 minutos.

    ![Creación de un icono de gráfico de líneas](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Haga clic en **Siguiente**, agregue el título y el subtítulo y haga clic en **Aplicar**.

    panel de Power BI Hola le proporciona dos vistas de datos sobre las llamadas de fraudulentas según lo detecte en hello transmisión de datos.

    ![Panel de Power BI finalizado que muestra dos iconos de llamadas fraudulentas](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Más información sobre Power BI

Este tutorial se muestra cómo toocreate solo unos tipos de visualizaciones para un conjunto de datos. Power BI puede ayudarle a crear otras herramientas de inteligencia empresarial de cliente para su organización. Para obtener más ideas, vea Hola recursos siguientes:

* Para obtener otro ejemplo de un panel de Power BI, vea hello [Introducción a Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) vídeo.
* Para obtener más información acerca de cómo configurar el análisis de transmisión por secuencias de trabajo salida tooPower BI y uso de grupos de Power BI, revise hello [Power BI](stream-analytics-define-outputs.md#power-bi) sección de hello [análisis de transmisiones genera](stream-analytics-define-outputs.md) artículo. 
* Para información sobre el uso en general de Power BI, vea [Paneles de Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>Más información sobre limitaciones y prácticas recomendadas
Actualmente, se puede llamar a Power BI una vez por segundo aproximadamente. Los objetos visuales de streaming admiten paquetes de 15 KB. Más allá de eso, se producirá un error en la transmisión por secuencias de objetos visuales (pero inserción continúa toowork). Debido a estas limitaciones, Power BI se presta de forma más natural toocases que el análisis de transmisiones de Azure lleva a una reducción de la carga de gran volumen de datos. Se recomienda utilizar una ventana de saltos de tamaño constante o Hopping ventana tooensure que es de inserción de datos a lo sumo una inserción por segundo, y que llega a la consulta dentro de los requisitos de rendimiento de Hola.

Hola siguiente ecuación toocompute Hola valor toogive puede usar la ventana en segundos:

![Ecuación 1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Por ejemplo:

* Tiene 1000 dispositivos que envían datos a intervalos de un segundo.
* Utilizas Hola SKU Pro de Power BI que admita 1.000.000 de filas por hora.
* Desea toopublish Hola tamaño promedio de los datos por dispositivo tooPower BI.

Como resultado, se convierte en ecuación hello:

![Ecuación 2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

Dada esta configuración, puede cambiar Hola original consulta toohello a continuación:

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>Renovar la autorización
Si la contraseña de hello cambió desde que se creó o autenticado por última vez el trabajo, debe tooreauthenticate su cuenta de Power BI. Si la autenticación multifactor Azure está configurada en el inquilino de Azure Active Directory (Azure AD), también se necesita autorización de Power BI toorenew cada dos semanas. Si no lo renueva, podría ver síntomas como la falta de salida del trabajo o un `Authenticate user error` en registros de operaciones de Hola.

Del mismo modo, si se inicia un trabajo después de hello token ha expirado, se produce un error y se produce un error en el trabajo de Hola. tooresolve este problema, detenga trabajo Hola que se ejecuta y vaya tooyour Power BI de salida. tooavoid pérdida de datos, seleccione hello **renovar la autorización** vincular y, a continuación, reinicie el trabajo de hello **última hora de detención**.

Después de que se haya actualizado la autorización de hello con Power BI, aparecerá una alerta verde en hello autorización área tooreflect que se ha resuelto el problema de Hola.

## <a name="get-help"></a>Obtener ayuda
Para obtener ayuda adicional, pruebe nuestro [foro de Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
