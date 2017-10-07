---
title: "aaaAutomate los procesos de análisis de registros de Azure con Microsoft Flow"
description: "Obtenga información acerca de cómo puede utilizar Microsoft Flow tooquickly automatizar procesos repetibles mediante el conector de Azure Log Analytics Hola."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Automatizar los procesos de análisis de registros con el conector de Hola para Microsoft Flow
[Microsoft Flow](https://ms.flow.microsoft.com) permite los flujos de trabajo toocreate automatizada con cientos de acciones para una variedad de servicios. Salida de una acción puede utilizarse como entrada tooanother permitiéndole toocreate integración entre diferentes servicios.  Conector de Azure Log Analytics Hola para Microsoft Flow permitir que los flujos de trabajo de toobuild que incluyen datos recuperados por las búsquedas de registros de análisis de registros.

Por ejemplo, puede usar datos de análisis de registros de Microsoft Flow toouse en una notificación de correo electrónico de Office 365, crear un error en Visual Studio Team Services o publicar un mensaje demora.  Puede desencadenar un flujo de trabajo mediante una programación simple o a partir de alguna acción de un servicio conectado, como cuando se recibe un correo electrónico o un tweet.  


> [!NOTE]
> Conector de Azure Log Analytics Hola para Microsoft Flow requiere su área de trabajo toobe actualizado toohello nuevo análisis de registros lenguaje de consulta. Puede obtener más información sobre el nuevo lenguaje de Hola y obtener Hola procedimiento tooupgrade el área de trabajo en [actualizar la búsqueda de registros de toonew de área de trabajo de análisis de registros de Azure](log-analytics-log-search-upgrade.md).  

tutorial de Hello en este artículo muestra cómo Hola toocreate un flujo que envía automáticamente los resultados de una búsqueda de registros de análisis de registros por correo electrónico, solo un ejemplo de cómo puede usar análisis de registros en Microsoft Flow. 


## <a name="step-1-create-a-flow"></a>Paso 1: Creación de un almacén
1. Inicie sesión en demasiado[Microsoft Flow](http://flow.microsoft.com)y seleccione **fluye mi**.
2. Haga clic en **+ Crear desde cero**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>Paso 2: Creación de un desencadenador para el flujo
1. Haga clic en **Search hundreds of connectors and triggers** (Buscar cientos de conectores y desencadenadores).
2. Tipo de **programación** en el cuadro de búsqueda de Hola.
3. Elija **Programación** y, a continuación, **Programación: Periodicidad**.
4. Hola **frecuencia** cuadro Active **día** y Hola **intervalo** cuadro, escriba **1**.<br><br>![Cuadro de diálogo del desencadenador de Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>Paso 3: Adición de una acción de Log Analytics
1. Haga clic en **+ Nuevo paso** y, a continuación, en **Agregar una acción**.
2. Busque **Log Analytics**.
3. Haga clic en **Azure Log Analytics: ejecutar consulta y ver resultados**.<br><br>![Ventana Ejecutar consulta de Log Analytics](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Paso 4: Configurar la acción de análisis de registros de Hola

1. Especifique los detalles de hello para el área de trabajo incluidos Hola Id. de suscripción, grupo de recursos y el nombre de área de trabajo.
2. Agregar Hola después toohello de consultas de análisis de registros **consulta** ventana.  Esta es solo una consulta de ejemplo y puede reemplazarla por cualquier otra que devuelva datos.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Seleccione **tabla HTML** para hello **tipo de gráfico**.<br><br>![Acción de Log Analytics](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Paso 5: Configurar el correo electrónico de toosend de flujo de Hola

1. Haga clic en **Nuevo paso** y, a continuación, en **+ Agregar una acción**.
2. Busque **Office 365 Outlook**.
3. Haga clic en **Office 365 Outlook: Enviar un correo electrónico**.<br><br>![Ventana de selección de Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)

4. Especifique la dirección de un destinatario de correo electrónico de Hola Hola **a** ventana y el asunto de correo electrónico de hello en **asunto**.
5. Haga clic en cualquier lugar en hello **cuerpo** cuadro.  Se abre una ventana de **contenido dinámico** con los valores de las acciones anteriores.  
6. Seleccione **Cuerpo**.  Se trata de resultados de Hola de consulta Hola Hola acción de análisis de registros.
6. Haga clic en **Mostrar opciones avanzadas**.
7. Hola **es HTML** cuadro, seleccione **Sí**.<br><br>![Ventana de configuración de correo electrónico de Office 365](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>Paso 6: Guardado y prueba del flujo
1. Hola **nombre de flujo de** cuadro, agregue un nombre para el flujo y, a continuación, haga clic en **Crear flujo**.<br><br>![Guardar flujo](media/log-analytics-flow-tutorial/flow06.png)
2. flujo de Hello ahora se crea y se ejecutará después de un día que es la programación de Hola que especificó. 
3. tooimmediately prueba Hola flujo, haga clic en **ejecutar ahora** y, a continuación, **ejecutar flujo**.<br><br>![Ejecutar flujo](media/log-analytics-flow-tutorial/flow07.png)
3. Cuando se completa el flujo de hello, comprobar correo Hola del destinatario de Hola que especificó.  Debe haber recibido un correo electrónico con una continuación de toohello similar de cuerpo:<br><br>![Correo electrónico de ejemplo](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Pasos siguientes

- Más información sobre [búsquedas de registros en Log Analytics](log-analytics-log-search-new.md).
- Más información sobre [Microsoft Flow](https://ms.flow.microsoft.com).



