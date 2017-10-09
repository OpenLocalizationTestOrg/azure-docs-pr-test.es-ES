---
title: "topologías de Storm aaaApache con Visual Studio y C# - HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate topologías de Storm en C#. Crear una topología de recuento de palabras simple en Visual Studio mediante las herramientas de Hadoop de Hola para Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>Desarrollar topologías de C# para Apache Storm mediante las herramientas de Data Lake Hola para Visual Studio

Obtenga información acerca de cómo toocreate una topología de C# Storm mediante el uso de hello Azure Data Lake (Hadoop) de las herramientas de Visual Studio. Este documento le guía por el proceso de Hola de crear un proyecto de Storm en Visual Studio, pruebas de forma local e implementarla tooan Apache Storm en clúster de HDInsight de Azure.

También aprenderá cómo toocreate topologías de híbridas que utilizan los componentes de C# y Java.

> [!NOTE]
> Aunque los pasos de hello en este documento se basan en un entorno de desarrollo de Windows con Visual Studio, proyecto compilado Hola puede ser tooeither enviado un clúster de HDInsight basados en Windows o de Linux. Solo los clústeres basados en Linux creados después del 28 de octubre de 2016 admiten topologías SCP.NET.

topología de toouse C# con un clúster basado en Linux, debe actualizar Hola paquete de Microsoft.SCP.Net.SDK NuGet utilizado por el tooversion proyecto 0.10.0.6 o posterior. versión de Hola del paquete de hello también debe coincidir con la versión principal de Hola de Storm instalado en HDInsight.

| Versión de HDInsight | Versión de Storm | Versión de SCP.NET | Versión de Mono predeterminada |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(solo en HDInsight basado en Windows) | N/D |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3,5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> Topologías de C# en clústeres basados en Linux deben usar .NET 4.5 y usar toorun Mono en clúster de HDInsight Hola. Compruebe el documento de [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/) para ver las posibles incompatibilidades.

## <a name="install-visual-studio"></a>Instalación de Visual Studio

Puede desarrollar topologías de C# con SCP.NET mediante uno de hello después de versiones de Visual Studio:

* Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?LinkId=517284)

* Visual Studio 2015 o [Visual Studio Community 2015](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017 (cualquier edición)

## <a name="install-data-lake-tools-for-visual-studio"></a>Instalación de Herramientas de Data Lake para Visual Studio

herramientas de Data Lake tooinstall para Visual Studio, siga los pasos de hello en [Introducción al uso de herramientas de Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a name="install-java"></a>Instalar Java

Cuando se envía una topología de Storm desde Visual Studio, SCP.NET genera un archivo zip que contiene las dependencias y la topología de Hola. Java es toocreate usa estos archivos, zip porque utiliza un formato que sea más compatible con clústeres basados en Linux.

1. Instalar Hola Kit de desarrollador de Java (JDK) 7 o posterior en el entorno de desarrollo. Puede obtener Hola Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). También puede usar [otras distribuciones de Java](http://openjdk.java.net/).

2. Hola `JAVA_HOME` entorno debe variable punto toohello el directorio que contiene Java.

3. Hola `PATH` variable de entorno debe incluir hello `%JAVA_HOME%\bin` directory.

Puede usar Hola después de C# consola los tooverify de aplicación que se han instalado correctamente hello JDK y Java:

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Plantillas de Storm

herramientas de Data Lake de Hola para Visual Studio proporcionan Hola siguientes plantillas:

| Tipo de proyecto | Muestra |
| --- | --- |
| Storm Application |Un proyecto vacío de topología de Storm. |
| Storm Azure SQL Writer Sample |Cómo toowrite tooAzure base de datos SQL. |
| Storm Azure Cosmos DB Reader Sample |¿Cómo tooread de base de datos de Azure Cosmos. |
| Storm Azure Cosmos DB Writer Sample |Cómo toowrite tooAzure Cosmos DB. |
| Storm EventHub Reader Sample |¿Cómo tooread desde los centros de eventos de Azure. |
| Storm EventHub Writer Sample |Cómo toowrite tooAzure centros de eventos. |
| Storm HBase Reader Sample |¿Cómo tooread de HBase en HDInsight de clústeres. |
| Storm HBase Writer Sample |Cómo toowrite tooHBase en HDInsight de clústeres. |
| Storm Hybrid Sample |¿Cómo toouse un componente de Java. |
| Storm Sample |Una topología de recuento de palabras básica. |

> [!WARNING]
> No todas las plantillas funcionará con HDInsight basado en Linux. Paquetes de NuGet utilizados plantillas de hello no pueden ser compatibles con Mono. Comprobar hello [compatibilidad Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documentos y usar hello [analizador de portabilidad de .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify posibles problemas.

En los pasos de hello en este documento, use hello básico Storm aplicación proyecto tipo toocreate una topología.

### <a name="hbase-templates-notes"></a>Notas de plantillas de HBase

Hola HBase lector y plantillas de escritor usan hello API de REST de HBase, no Hola API de Java de HBase, toocommunicate con un HBase en clúster de HDInsight.

### <a name="eventhub-templates-notes"></a>Notas de plantillas de EventHub

> [!IMPORTANT]
> Hola EventHub basados en Java apetezca charlar un componente incluido con hello plantilla de lector de EventHub no funcionen con Storm en HDInsight versión 3.5 o posterior. Hay una versión actualizada de este componente disponible en [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).

Para obtener una topología de ejemplo que usa este componente y funciona con Storm en HDInsight 3.5, vea [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

## <a name="create-a-c-topology"></a>Creación de una topología de C#

1. Abra Visual Studio, seleccione **Archivo** > **Nuevo** y luego seleccione **Proyecto**.

2. De hello **nuevo proyecto** ventana, expanda **instalado** > **plantillas**y seleccione **Azure Data Lake**. En la lista Hola de plantillas, seleccione **aluvión de aplicación**. En la parte inferior de Hola de pantalla de bienvenida, escriba **WordCount** como nombre de Hola de aplicación hello.

    ![Captura de pantalla de la ventana Nuevo proyecto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. Una vez haya creado el proyecto de hello, debe tener Hola siguientes archivos:

   * **Program.cs**: este archivo define la topología de hello para el proyecto. Una topología predeterminada que consta de un spout y un bolt se crea de manera predeterminada.

   * **Spout.cs**: un spout de ejemplo que emite números aleatorios

   * **Bolt.cs**: un rayo de ejemplo que mantiene un recuento de números emitidos por pitorro Hola.

     Cuando se crea el proyecto de hello, descargas de NuGet Hola más reciente [SCP.NET paquete](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>Pitorro de hello implemente

1. Abra **Spout.cs**. Spouts son datos tooread usado en una topología de un origen externo. componentes principales de Hola para un pitorro son:

   * **NextTuple**: llama Storm cuando pitorro Hola se permite tooemit nuevas tuplas.

   * **Confirmación** (solo topología transaccional): controla confirmaciones iniciadas por otros componentes de la topología de Hola para tuplas enviados desde pitorro Hola. Confirmación de una tupla, podrá pitorro Hola saber que se procesó correctamente por componentes de nivel inferior.

   * **Un error** (solo topología transaccional): controla tuplas que se producirá un error-procesamiento de otros componentes de la topología de Hola. Implementa un método por error permite toore-emitir tupla Hola para que se pueda procesar de nuevo.

2. Reemplazar contenido Hola de hello **apetezca charlar** clase con hello después de texto. Este pitorro aleatoriamente emite una frase en la topología de Hola.

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>Implementar Hola tornillos

1. Eliminar Hola existente **Bolt.cs** archivo de proyecto de Hola.

2. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **agregar** > **nuevo elemento**. En la lista de hello, seleccione **aluvión de rayo**y escriba **Splitter.cs** como nombre de Hola. Repita este toocreate proceso denominado un rayo segundo **Counter.cs**.

   * **Splitter.cs**: implementa un bolt que divide la frase en palabras individuales y emite una nueva secuencia de palabras.

   * **Counter.cs**: implementa un rayo que cuenta cada palabra y emite una nueva secuencia de palabras y el recuento de Hola de cada palabra.

     > [!NOTE]
     > Estos tornillos de lectura y escritura toostreams, pero también puede utilizar un rayo toocommunicate con orígenes, como una base de datos o un servicio.

3. Abra **Splitter.cs**. Solo tiene un método de forma predeterminada: **Execute**. Hola método Execute se llama cuando el rayo de Hola recibe una tupla para el procesamiento. En este caso, puede leer y procesar las tuplas entrantes y emitir tuplas salientes.

4. Reemplazar contenido Hola de hello **divisor** clase con el siguiente código de hello:

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. Abra **Counter.cs**y reemplace el contenido de la clase hello con siguiente de hello:

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>Definir la topología de Hola

Spouts y tornillos se organizan en un gráfico, que define cómo fluyen los datos de hello entre los componentes. Para esta topología, el gráfico de hello es la siguiente:

![Diagrama de cómo se organizan los componentes](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

Las frases se emiten desde pitorro hello y son tooinstances distribuida de rayo divisor de Hola. tornillo del divisor de Hola divide las frases de Hola palabras, lo cual están distribuidas toohello rayo de contador.

Debido a número de palabras se conservan localmente en la instancia del contador de hello, queremos toomake seguro de que las palabras específicas fluyan toohello misma instancia del contador rayo. Cada instancia realiza el seguimiento de palabras específicas. Puesto que el rayo de hello divisor no mantiene ningún estado, realmente no importa qué instancia del divisor de hello recibe qué frase.

Abra **Program.cs**. Hola método en importancia es **GetTopologyBuilder**, que es la topología de hello toodefine utilizado que es envían tooStorm. Reemplace el contenido de Hola de **GetTopologyBuilder** con hello después de la topología de hello tooimplement de código se ha descrito anteriormente:

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>Enviar Hola topología

1. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **enviar tooStorm en HDInsight**.

   > [!NOTE]
   > Si se le pide, escriba credenciales de hello para la suscripción de Azure. Si tiene más de una suscripción, inicie sesión en toohello uno que contiene el aluvión en clúster de HDInsight.

2. Seleccione el aluvión en clúster de HDInsight de hello **clúster de Storm** lista desplegable y, a continuación, seleccione **enviar**. Puede supervisar si el envío de hello es correcto mediante hello **salida** ventana.

3. Cuando se ha enviado correctamente la topología de hello, Hola **aluvión de topologías** para clúster Hola debería aparecer. Seleccione hello **WordCount** topología de hello mostrar tooview información acerca de hello ejecutando topología.

   > [!NOTE]
   > También puede ver **topologías de Storm** desde el **Explorador de servidores**. Expanda **Azure** > **HDInsight**, haga clic con el botón derecho en un clúster de Storm en HDInsight y luego seleccione **Ver topologías de Storm**.

    tooview información sobre los componentes de Hola de topología de hello, haga doble clic en el componente de hello en el diagrama de Hola.

4. De hello **resumen de la topología** ver, haga clic en **Kill** topología de hello toostop.

   > [!NOTE]
   > Topologías de Storm continuar toorun hasta que están desactivadas o clúster de Hola se elimina.

## <a name="transactional-topology"></a>Topología transaccional

topología anterior Hello es no transaccional. componentes de Hola de topología de hello implementar mensajes tooreplaying de funcionalidad. Para obtener un ejemplo de una topología transaccional, cree un proyecto y seleccione **aluvión de ejemplo** como tipo de proyecto de Hola.

Topologías transaccionales implementan Hola después de reproducción de toosupport de datos:

* **Almacenamiento en caché de metadatos**: pitorro Hola debe almacenar metadatos sobre los datos de hello emitidos, por lo que pueden recuperar datos de Hola y emitir nuevo si se produce un error. Como datos de hello emitidos por el ejemplo hello están pequeños, datos sin procesar de hello en cada tupla se almacenan en un diccionario para la reproducción.

* **Confirmación**: pueden llamar todos los tornillos de topología de hello `this.ctx.Ack(tuple)` tooacknowledge que ha procesado correctamente una tupla. Cuando todos los tornillos tienen realizados Hola tupla, Hola `Ack` se invoca el método de pitorro Hola. Hola `Ack` método permite que los datos de tooremove de pitorro Hola que se almacenó en caché para la reproducción.

* **Un error**: pueden llamar todos los tornillos `this.ctx.Fail(tuple)` tooindicate que el procesamiento no se pudo realizar una tupla. Error de Hello propaga toohello `Fail` método de pitorro hello, donde se pueden reproducir Hola tupla mediante el uso de metadatos que están almacenados.

* **Id. de secuencia**: al emitir una tupla, se puede especificar un identificador de secuencia único. Este valor identifica tupla hello para el procesamiento de reproducción (confirmación y error). Por ejemplo, Hola pitorro en hello **aluvión de ejemplo** utiliza el proyecto siguiente Hola al emitir los datos:

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    Este código emite una tupla que contiene una secuencia predeterminada de toohello de oración, con valor de identificador de secuencia de hello contenido en **lastSeqId**. En este ejemplo, **lastSeqId** se incrementa con cada tupla emitida.

Como se muestra en hello **aluvión de ejemplo** proyecto de equipo y si un componente es transaccional pueden establecerse en tiempo de ejecución, en función de la configuración.

## <a name="hybrid-topology-with-c-and-java"></a>Topología híbrida con C# y Java

También puede usar herramientas de Data Lake para Visual Studio toocreate híbrida las topologías, donde algunos componentes estén C# y otras son Java.

Para ver un ejemplo de una topología híbrida, cree un proyecto y seleccione **Muestra híbrida de Storm**. Este tipo de ejemplo muestra hello siguientes conceptos:

* **Spout de Java** y **bolt de C#**: definidos en **HybridTopology_javaSpout_csharpBolt**.

    * Una versión transaccional se define en **HybridTopologyTx_javaSpout_csharpBolt**.

* **Spout de C#** y **bolt de Java**: definidos en **HybridTopology_csharpSpout_javaBolt**.

    * Una versión transaccional se define en **HybridTopologyTx_csharpSpout_javaBolt**.

  > [!NOTE]
  > Esta versión también muestra cómo toouse Clojure código de un archivo de texto como un componente de Java.


topología de hello tooswitch que se usa cuando se envía el proyecto de hello, basta con mover hello `[Active(true)]` topología de toohello de instrucción que desea utilizar toouse, antes de enviar toohello clúster.

> [!NOTE]
> Todos los archivos de Java de hello necesarios se proporcionan como parte de este proyecto en hello **JavaDependency** carpeta.

Tenga en cuenta los siguiente de hello cuando está creando y enviando una topología híbrida:

* Debe usar **JavaComponentConstructor** toocreate una instancia de clase de Java para un pitorro o rayo Hola.

* Debe usar **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON los objetos de datos de tooserialize entre o salga de componentes de Java en Java.

* Al enviar el servidor de toohello de topología de hello, debe usar hello **configuraciones adicionales** Hola de opción toospecify **las rutas de acceso de Java**. ruta de acceso de Hello especificada debe ser el directorio de Hola que contiene los archivos JAR de Hola que contienen las clases de Java.

### <a name="azure-event-hubs"></a>Azure Event Hubs

Versión SCP.NET 0.9.4.203 presenta una nueva clase y método específicamente para trabajar con pitorro de concentrador de eventos de hello (pitorro Java que lee los centros de eventos). Cuando se crea una topología que utiliza un pitorro concentrador de eventos, use Hola siguientes métodos:

* **EventHubSpoutConfig** clase: crea un objeto que contiene la configuración de Hola de componente de pitorro Hola.

* **TopologyBuilder.SetEventHubSpout** método: agrega topología de hello concentrador de eventos pitorro componente toohello.

> [!NOTE]
> Deberá seguir usando hello **CustomizedInteropJSONSerializer** tooserialize datos producidos por pitorro Hola.

## <a id="configurationmanager"></a>Uso de ConfigurationManager

No utilice **ConfigurationManager** tooretrieve configuración de valores comprendidos entre el tornillo y apetezca charlar componentes. Si lo hace, puede generar una excepción de puntero nulo. En su lugar, configuración de hello para el proyecto se pasó a topología aluvión de Hola como un par de clave y valor en el contexto de la topología de Hola. Cada componente que se basa en valores de configuración debe recuperarlos desde el contexto de Hola durante la inicialización.

Hello código siguiente se muestra cómo tooretrieve estos valores:

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

Si utiliza un `Get` método tooreturn una instancia del componente, debe asegurarse de que pasa tanto hello `Context` y `Dictionary<string, Object>` constructor toohello de parámetros. el ejemplo siguiente se Hello es básico `Get` método que pasa correctamente estos valores:

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>Cómo tooupdate SCP.NET

Las versiones recientes de SCP.NET admiten la actualización de paquetes a través de NuGet. Cuando está disponible una nueva actualización, recibirá una notificación de actualización. comprobación de toomanually para realizar una actualización, siga estos pasos:

1. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **administrar paquetes de NuGet**.

2. En el Administrador de paquetes de saludo, seleccione **actualizaciones**. Si hay disponible una actualización, se mostrará una lista. Haga clic en **actualización** para tooinstall de paquetes de saludo se.

> [!IMPORTANT]
> Si el proyecto se creó con una versión anterior de SCP.NET que no utilizan NuGet, debe realizar Hola después de la versión más reciente de pasos tooupdate tooa:
>
> 1. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **administrar paquetes de NuGet**.
> 2. Con hello **búsqueda** campo, busque y, a continuación, agregar, **Microsoft.SCP.Net.SDK** toohello proyecto.

## <a name="troubleshoot-common-issues-with-topologies"></a>Solución de problemas comunes de las topologías

### <a name="null-pointer-exceptions"></a>Excepciones de puntero nulo

Cuando se utiliza una topología de C# con un clúster de HDInsight basados en Linux, el tornillo y apetezca charlar componentes que usan **ConfigurationManager** tooread opciones de configuración en tiempo de ejecución pueden devolver las excepciones de puntero nulo.

configuración de Hello para el proyecto se pasó a topología aluvión de Hola como un par de clave y valor en el contexto de la topología de Hola. Se puede recuperar del objeto de diccionario de Hola que se pasa tooyour componentes cuando se inicializan.

Para obtener más información, vea hello [ConfigurationManager](#configurationmanager) sección de este documento.

### <a name="systemtypeloadexception"></a>System.TypeLoadException

Cuando se utiliza una topología de C# con un clúster de HDInsight basados en Linux, puede encontrar Hola siguiente error:

    System.TypeLoadException: Failure has occurred while loading a type.

Este error se produce cuando se usa un archivo binario que no es compatible con la versión de Hola de .NET que admita Mono.

En el caso de los clústeres de HDInsight basados en Linux, debe asegurarse de que el proyecto use archivos binarios compilados para .NET 4.5.

### <a name="test-a-topology-locally"></a>Prueba de una topología localmente

Aunque es fácil toodeploy un clúster de tooa topología, en algunos casos, puede que tenga tootest una topología localmente. Usar hello siguiendo los pasos toorun y pruebe la topología de ejemplo de Hola en este tutorial localmente en el entorno de desarrollo.

> [!WARNING]
> Las pruebas locales solo funcionan para topologías básicas de C#. No se pueden usar pruebas locales para las topologías híbridas o para las topologías que usan varias secuencias.

1. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **propiedades**. En Propiedades del proyecto hello, cambie hello **tipo de salida** demasiado**aplicación de consola**.

    ![Captura de pantalla de las propiedades del proyecto con Tipo de salida resaltado](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > Recuerde hello toochange **tipo de salida** realizar copia demasiado**biblioteca de clases** antes de implementar el clúster de hello topología tooa.

2. En **el Explorador de soluciones**, haga clic en proyecto de hello y, a continuación, seleccione **agregar** > **nuevo elemento**. Seleccione **clase**y escriba **LocalTest.cs** como nombre de la clase hello. Por último, haga clic en **Agregar**.

3. Abra **LocalTest.cs**y agregue Hola siguiente **con** declaración en la parte superior de hello:

    ```csharp
    using Microsoft.SCP;
    ```

4. Use Hola siguiente de código como contenido de Hola de hello **LocalTest** clase:

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    Tomar una tooread momento a través de comentarios de código de hello. Este código usa **LocalContext** toorun componentes de hello en el entorno de desarrollo de Hola y continúa el flujo de datos de hello entre los archivos de tootext de componentes en la unidad local Hola.

1. Abra **Program.cs**y agregue Hola después toohello **Main** método:

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. Guardar los cambios de hello y, a continuación, haga clic en **F5** o seleccione **depurar** > **Iniciar depuración** proyecto de hello toostart. Debe aparecer una ventana de consola y registrar el estado del progreso de las pruebas de Hola. Cuando **terminado las pruebas** aparece, presione cualquier ventana de hello tooclose clave.

3. Use **el Explorador de Windows** directorio de hello toolocate que contiene el proyecto. Por ejemplo: **C:\Usuarios\<su_nombre_de_usuario>\Documentos\Visual Studio 2013\Projects\WordCount\WordCount**. En este directorio, abra **Bin** y haga clic en **Depurar**. Debería ver los archivos de texto hello que se producen cuando se ejecutó hello: sentences.txt, counter.txt y splitter.txt. Abra cada archivo de texto e inspeccionar los datos de Hola.

   > [!NOTE]
   > Los datos de cadena se guardan como persistentes como una matriz de valores decimales en estos archivos. Por ejemplo, \[[97,103,111]] Hola **splitter.txt** archivo es palabra Hola *y*.

> [!NOTE]
> Estar seguro de hello tooset **tipo de proyecto** realizar copia demasiado**biblioteca de clases** antes de implementar tooa Storm en clúster de HDInsight.

### <a name="log-information"></a>Información del registro

Puede registrar fácilmente información de los componentes de la topología mediante `Context.Logger`. Por ejemplo, la siguiente Hola crea una entrada de registro informativo:

```csharp
Context.Logger.Info("Component started");
```

Puede verse información registrada de hello **registro del servicio de Hadoop**, que se encuentra en **Explorador de servidores**. Expanda la entrada de Hola para su Storm en clúster de HDInsight y, a continuación, expanda **registro del servicio de Hadoop**. Por último, seleccione tooview de archivo de registro de hello.

> [!NOTE]
> Hola registros se almacenan en hello cuenta de almacenamiento de Azure que es utilizada por el clúster. registros de hello tooview en Visual Studio, debe iniciar sesión en toohello suscripción de Azure que pertenece la cuenta de almacenamiento de Hola.

### <a name="view-error-information"></a>Visualización de la información del error

errores de tooview que se han producido en una topología de ejecución, utilice Hola siguiendo los pasos:

1. De **Explorador de servidores**, haga clic en hello Storm en clúster de HDInsight y seleccione **topologías aluvión de vista**.

2. Para hello **apetezca charlar** y **tornillos**, hello **último Error** columna contiene información sobre el último error de Hola.

3. Seleccione hello **apetezca charlar un identificador** o **Id. de rayo** para el componente de Hola que tiene un error que aparece. En página de detalles de hello es error adicional, muestra información aparece en hello **errores** sección final Hola de página Hola.

4. tooobtain obtener más información, seleccione un **puerto** de hello **ejecutor** sección de página de hello, registro de trabajo de toosee Hola aluvión de hello últimos minutos.

### <a name="errors-submitting-topologies"></a>Errores en el envío de topologías

Si se producen errores al enviar un tooHDInsight topología, puede encontrar registros para los componentes de servidor de Hola que controlan la presentación de la topología en su clúster de HDInsight. tooretrieve estos registros, Hola de uso siguiente comando desde una línea de comandos:

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

Reemplace __sshuser__ con la cuenta de usuario SSH para clúster Hola Hola. Reemplace __clustername__ con el nombre de Hola Hola del clúster de HDInsight. Para más información sobre cómo usar `scp` y `ssh` con HDInsight, vea [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Se pueden producir errores en los envíos por varios motivos:

* JDK no está instalado o no está en la ruta de acceso de Hola.
* Dependencias de Java necesarias no se incluyen en el envío de Hola.
* Dependencias no compatibles.
* Nombres de topologías duplicados.

Si hello `hdinsight-scpwebapi.out` registro contiene un `FileNotFoundException`, esto podría deberse a Hola condiciones siguientes:

* Hola JDK no está en la ruta de acceso de hello en el entorno de desarrollo de Hola. Compruebe que Hola JDK está instalado en el entorno de desarrollo de Hola y que `%JAVA_HOME%/bin` está en la ruta de acceso de Hola.
* Falta una dependencia de Java. Asegúrese de que va a incluir los archivos .jar necesarios como parte del envío de Hola.

## <a name="next-steps"></a>Pasos siguientes

Para obtener un ejemplo de procesamiento de datos desde Event Hubs, vea [Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).

Para ver un ejemplo de una topología de C# que divide los datos de una secuencia en varias secuencias, consulte [Ejemplo de Storm en C#](https://github.com/Blackmist/csharp-storm-example).

toodiscover obtener más información acerca de cómo crear topologías de C#, vea [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).

Para más toowork maneras con HDInsight y Storm más muestras de HDInsight, vea Hola siguientes documentos:

**Microsoft SCP.NET**

* [Guía de programación de SCP](hdinsight-storm-scp-programming-guide.md)

**Apache Storm en HDInsight**

* [Implementación y supervisión de topologías con Apache Storm en HDInsight](hdinsight-storm-deploy-monitor-topology.md)
* [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md)

**Apache Hadoop en HDInsight**

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)

**Apache HBase en HDInsight**

* [Introducción a HBase en HDInsight](hdinsight-hbase-tutorial-get-started.md)
