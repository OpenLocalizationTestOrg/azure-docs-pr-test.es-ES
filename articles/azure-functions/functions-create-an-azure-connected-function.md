---
title: "una función que se conecta a servicios de tooAzure aaaCreate | Documentos de Microsoft"
description: "Usar funciones de Azure toocreate una aplicación sin servidor que se conecta tooother Azure servicios."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Usar funciones de Azure toocreate una función que se conecta tooother Azure Servicios

Este tema muestra cómo una función en funciones de Azure que escucha toomessages en un Hola de cola y las copias de almacenamiento de Azure toocreate mensajes toorows en una tabla de almacenamiento de Azure. Una función de temporizador desencadenada es tooload usa mensajes en cola de Hola. Una segunda función lee de la cola de Hola y escribe la tabla de toohello de mensajes. Cola de Hola y tabla de Hola se crean automáticamente por funciones de Azure que se basan en definiciones de enlace de Hola. 

toomake cosas más interesantes, se escribe una función de JavaScript y Hola otro se escribe en la secuencia de comandos de C#. Esto demuestra cómo una aplicación de la función puede tener funciones en distintos lenguajes. 

En un [vídeo de Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player) se puede ver una demostración de este escenario.

## <a name="create-a-function-that-writes-toohello-queue"></a>Crear una función que escribe toohello cola

Para poder conectarse tooa cola de almacenamiento, deberá toocreate una función que carga la cola de mensajes de Hola. Esta función de JavaScript usa un desencadenador de temporizador que escribe una cola de mensajes toohello cada 10 segundos. Si ya no tiene una cuenta de Azure, visite hello [funciones de Azure intente](https://functions.azure.com/try) experiencia, o [crear su cuenta de Azure gratuita](https://azure.microsoft.com/free/).

1. Vaya toohello portal de Azure y busque la aplicación de la función.

2. Haga clic en **Nueva función** > **TimerTrigger-JavaScript**. 

3. Nombre de función hello **FunctionsBindingsDemo1**, escriba el valor de la expresión cron `0/10 * * * * *` para **programación**y, a continuación, haga clic en **crear**.
   
    ![Adición de una función desencadenada por el temporizador](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    Ahora ha creado una función desencadenada por el temporizador que se ejecuta cada 10 segundos.

5. En hello **desarrollar** , haga clic en **registros** y ver la actividad de hello en el registro de hello. Verá una entrada de registro escrita cada 10 segundos.
   
    ![Ver Hola registro tooverify Hola función funciona](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>Adición de un enlace de salida de la cola de mensajes

1. En hello **integrar** ficha, elija **nueva salida** > **almacenamiento de cola de Azure** > **seleccione**.

    ![Adición de una función de temporizador de desencadenador](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Escriba `myQueueItem` para **nombre de parámetro de mensaje** y `functions-bindings` para **nombre de la cola**, seleccione una existente **conexión de la cuenta de almacenamiento** o haga clic en **nueva** toocreate un almacenamiento de conexión de la cuenta y, a continuación, haga clic en **guardar**.  

    ![Crear cola de almacenamiento de toohello de enlace de salida de hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Nuevo en hello **desarrollar** ficha, anexar Hola después de la función de toohello de código:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Busque hello *si* instrucción aproximadamente 9 de función de Hola y de línea siguiente de Hola de inserción de código después de esa instrucción.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Este código crea un **myQueueItem** y establece su **tiempo** marca de tiempo actual toohello de propiedad. A continuación, agrega Hola nueva cola elemento toohello del contexto **myQueueItem** enlace.

3. Haga clic en **Guardar y ejecutar**.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Ver actualizaciones de almacenamiento mediante el Explorador de Storage
Puede comprobar que funciona la función ver los mensajes en cola de Hola que ha creado.  Cola de almacenamiento de tooyour puede conectarse mediante el Explorador de nube en Visual Studio. Sin embargo, portal de Hola resulta fácil tooconnect cuenta de almacenamiento de tooyour mediante el Explorador de almacenamiento de Microsoft Azure.

1. Hola **integrar** , haga clic en la cola de salida enlace > **documentación**, a continuación, mostrar hello cadena de conexión para la cuenta de almacenamiento y copie el valor de Hola. Utilice esta cuenta de almacenamiento de valor tooconnect tooyour.

    ![Descarga del explorador de Azure Storage](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Si no lo ha hecho ya, descargue e instale el [Explorador de Microsoft Azure Storage](http://storageexplorer.com). 
 
3. En el Explorador de almacenamiento, haga clic en hello tooAzure almacenamiento icono Conectar, pegue la cadena de conexión de hello en el campo de Hola y complete el Asistente de Hola.

    ![Explorador de Storage agrega una conexión](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. En **Local y conectado**, expanda **cuentas de almacenamiento** > su cuenta de almacenamiento > **colas** > **deenlacesdefunciones**y compruebe que los mensajes se escriben toohello cola.

    ![Vista de mensajes en cola de Hola](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Si la cola de hello no existe o está vacío, más probable es que hay un problema con el enlace de función o el código.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Crear una función que se lee de la cola de Hola

Ahora que tiene añadidos toohello cola de mensajes, puede crear otra función que se lee de la cola de Hola y Hola escrituras permanentemente mensajes tooan tabla de almacenamiento de Azure.

1. Haga clic en **Nueva función** > **QueueTrigger CSharp**. 
 
2. Nombre de función hello `FunctionsBindingsDemo2`, escriba **enlaces de funciones** en hello **nombre de la cola** campo, seleccione una cuenta de almacenamiento existente o crear uno y, a continuación, haga clic en **crear**.

    ![Adición de una función de temporizador de cola de salida](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (Opcional) Puede comprobar que la nueva función de hello funciona viendo la nueva cola de hello en el Explorador de almacenamiento como antes. También puede utilizar el Explorador de nube en Visual Studio.  

4. (Opcional) Actualizar hello **enlaces de funciones** poner en cola y observe que los elementos se han quitado de la cola de Hola. Hello eliminación se produce porque la función hello es toohello enlazado **enlaces de funciones** como una función de hello y desencadenador de entrada lee cola Hola de cola. 
 
## <a name="add-a-table-output-binding"></a>Adición de un enlace de salida de tabla

1. En FunctionsBindingsDemo2, haga clic en **Integrar** > **Nueva salida** > **Azure Table Storage** > **Seleccionar**.

    ![Agregar una tabla de almacenamiento de Azure de enlace tooan](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. Escriba `functionbindings` para el **nombre de la tabla** y `myTable` para el **nombre de parámetro de la tabla**, elija un **conexión de la cuenta de almacenamiento** o cree una nueva y, después, haga clic en **Guardar**.

    ![Configurar el enlace de tablas de almacenamiento de Hola](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. Hola **desarrollar** ficha, reemplace el código existente de la función de hello con siguiente hello:
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    Hola **TableItem** clase representa una fila de tabla de almacenamiento de Hola y agregar Hola elemento toohello `myTable` colección de **TableItem** objetos. Debe establecer hello **PartitionKey** y **RowKey** propiedades toobe puede tooinsert en la tabla de Hola.

4. Haga clic en **Guardar**.  Por último, puede comprobar Hola función funciona mediante la visualización de tabla de hello en el Explorador de almacenamiento o el Explorador de Visual Studio en la nube.

5. (Opcional) En la cuenta de almacenamiento en el Explorador de almacenamiento, expanda **tablas** > **functionsbindings** y compruebe que se han agregado filas de tabla toohello. Puede hacer igual hello en el Explorador de nube en Visual Studio.

    ![Vista de filas de tabla de Hola](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Si la tabla de hello no existe o está vacío, más probable es que hay un problema con el enlace de función o el código. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de las funciones de Azure, vea Hola temas siguientes:

* [Azure Functions developer reference](functions-reference.md)  
  contiene las referencias del programador para codificar funciones y definir desencadenadores y enlaces.
* [Prueba de Azure Functions](functions-test-a-function.md)  
  describe las diversas herramientas y técnicas para probar sus funciones.
* [¿Cómo tooscale las funciones de Azure](functions-scale.md)  
  Se tratan los planes de servicio disponibles con las funciones de Azure, incluido el plan de hospedaje de consumo de Hola y cómo toochoose Hola plan adecuado. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

