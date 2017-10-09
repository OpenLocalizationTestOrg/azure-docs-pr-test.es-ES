---
title: "Guía de programación aaaSCP.NET | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse SCP.NET toocreate. Topologías de Storm basada en la red para usan con Storm en HDInsight."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a>Guía de programación de SCP
SCP es una plataforma toobuild en tiempo real, la aplicación de procesamiento de datos confiable, coherente y de alto rendimiento. Se genera en la parte superior de [Apache Storm](http://storm.incubator.apache.org/) --una secuencia sistema diseñado por Comunidades de hello OSS de procesamiento. Storm ha sido diseñado por Nathan Marz con código abierto en Twitter. Aprovecha [ZooKeeper Apache](http://zookeeper.apache.org/), Apache otro proyecto tooenable altamente confiable distribuida coordinación y administración de Estados. 

No sólo proyecto Hola SCP portar Storm en Windows, sino también proyecto Hola agrega personalización ecosistema de Windows hello y extensiones. extensiones de Hello incluyen experiencia del desarrollador de .NET y las bibliotecas, personalización de hello incluye la implementación basada en Windows. 

personalización y extensión de Hola se realiza de forma que no necesitamos proyectos de OSS hello toofork y podríamos aprovechamos derivados ecosistemas creados sobre Storm.

## <a name="processing-model"></a>Modelo de procesamiento
datos de Hello en SCP se modelan como un flujo continuo de tuplas. Normalmente Hola tuplas fluyen en alguna cola en primer lugar, entonces recoge y transformará lógica de negocios que se hospeda dentro de una topología de Storm, por último salida de hello se canalizan como tuplas tooanother SCP sistema o ser confirmada toostores como sistema de archivos distribuido o las bases de datos, como SQL Server.

![Un diagrama de una cola que incorpore datos tooprocessing, las fuentes de un almacén de datos](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

En Storm, una topología de aplicación define un gráfico de cálculo. Cada nodo de la topología contiene lógica de procesamiento y los vínculos entre nodos indican del flujo de datos. datos de entrada tooinject de Hello nodos en la topología de Hola se denominan Spouts, que pueden ser utilizados toosequence Hola datos. Hello entradas los datos pueden residir en registros de archivos, bases de datos transaccionales, contador de rendimiento del sistema se denominan nodos de hello etc. con dos flujos de datos de entrada y salida tornillos, que Hola filtrado de datos reales y selecciones y agregación.

SCP admite procesamiento de datos de tipo best-effort, at-least-once y exactly-once. En una aplicación distribuida de procesamiento de transmisiones se pueden producir varios errores durante el procesamiento de datos, como una interrupción de la red, errores de equipo, errores en el código de usuario, etc. Mínimo: una vez como procesamiento garantiza que se procesarán todos los datos al menos una vez por reproducir automáticamente Hola mismos datos cuando se produce el error. El procesamiento at-least-once es sencillo y confiable, y es muy adecuado para muchas aplicaciones. Sin embargo, cuando la aplicación hello requiere recuento exacto, por ejemplo, menos de una vez como procesamiento no es suficiente porque hello mismos datos potencialmente se pudieron reproducir en la topología de la aplicación hello. En ese caso, exactamente-una vez que se ha diseñado el procesamiento toomake resultado de hello seguro es correcta, aunque se pueden reproducir los datos hello y procesar varias veces.

SCP habilita aplicaciones de proceso de datos de .NET a los desarrolladores toodevelop en tiempo real mientras Aproveche Hola Máquina Virtual Java (JVM) según Storm bajo cubierta Hola. Hola .NET y JVM comunicarán a través de socket TCP local. Básicamente cada pitorro/rayo es un par de proceso de .net/Java, donde se ejecuta la lógica de usuario de hello en proceso de .net como un complemento.

toobuild una aplicación en la parte superior SCP de procesamiento de datos, que son necesarios varios pasos:

* Diseñar e implementar hello Spouts toopull en los datos de la cola.
* Diseño e implementación tooprocess tornillos Hola datos de entrada y guardar datos tooexternal se almacena como base de datos.
* Diseñar la topología de hello, a continuación, enviar y ejecutar topología Hola. Hello topología define vértices y los datos de hello flujos entre vértices Hola. SCP tomará la especificación de topología de Hola y lo implementará en un clúster de Storm, donde cada vértice se ejecuta en un nodo lógico. conmutación por error de Hola y ajustar la escala nos ocuparemos de programador de tareas de Storm Hola.

Este documento va a utilizar algunos toowalk sencillos ejemplos por el proceso de aplicación de procesamiento de datos de toobuild con SCP.

## <a name="scp-plugin-interface"></a>Interfaz de complemento de SCP
Complementos de SCP (o aplicaciones) son archivos ejecutables independientes que se puedan ejecutar dentro de Visual Studio durante la fase de desarrollo de Hola e incluirse en la canalización de Storm Hola después de la implementación en producción. Escribir Hola SCP complemento es simplemente Hola igual que escribir cualquier otra aplicación de consola Windows estándar. Plataforma SCP.NET declara alguna interfaz de pitorro/rayo y código de complemento de hello usuario debería implementar estas interfaces. propósito principal de Hola de este diseño es que el usuario Hola pueda centrarse en su propia lógica de negocios y dejando otro toobe cosas controlar SCP.NET plataforma.

código de complemento de Hello usuario debería implementar una de las interfaces de hello siguiente, depende de si la topología de hello es transaccional o no transaccional y si el componente de hello es pitorro o rayo.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin es la interfaz común de Hola para todos los tipos de complementos. Actualmente es una interfaz ficticia.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout es la interfaz de Hola para pitorro no transaccional.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

Cuando `NextTuple()` se denomina hello C\# código de usuario puede emitir una o más tuplas. Si no hay nada tooemit, este método debe devolver sin emitir nada. Debe señalarse que `NextTuple()`, `Ack()` y `Fail()` se llaman todas en un bucle cerrado en un solo subproceso del proceso de C\#. Cuando no hay ningún tooemit tuplas, es toohave cortés NextTuple suspensión de un breve período de tiempo (por ejemplo, 10 milisegundos) así como no toowaste demasiada CPU.

`Ack()` y `Fail()` solo se llamarán cuando el mecanismo de confirmación esté habilitado en el archivo de especificación. Hola `seqId` es tooidentify usado Hola tupla que está realizados o no correctamente. Por lo que si está habilitada la confirmación de topología no transaccionales, Hola siguen emit función debe usarse en pitorro:

    public abstract void Emit(string streamId, List<object> values, long seqId); 

Si no se admite la confirmación de topología no transaccionales, Hola `Ack()` y `Fail()` pueden dejarse como función vacía.

Hola `parms` parámetros de entrada en estas funciones son diccionario vacío, se reservan para uso futuro.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt es la interfaz de Hola para rayo no transaccional.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

Cuando hay nueva tupla, Hola `Execute()` función llamará tooprocess lo.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout es la interfaz de Hola para pitorro transaccional.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

Del mismo modo que su contrapartida no transaccional, `NextTx()`, `Ack()` y `Fail()` se llaman todas en un bucle cerrado en un solo subproceso del proceso de C\#. Cuando no hay ningún tooemit de datos, es toohave cortés `NextTx` suspensión durante un breve período de tiempo (10 milisegundos), así como no toowaste demasiada CPU.

`NextTx()`es importante, toostart una nueva transacción, hello parámetro `seqId` es tooidentify usado Hola transacción, que también se utiliza en `Ack()` y `Fail()`. En `NextTx()`, usuario puede emitir comandos de tooJava de datos. Hola datos se almacenarán en reproducción de toosupport ZooKeeper. Porque la capacidad de Hola de ZooKeeper es muy limitada, usuario solo debe emitir metadatos, no los datos de forma masiva en pitorro transaccional.

Storm reproducirá automáticamente la transacción en caso de error, por lo que no se debe llamar a `Fail()` en condiciones normales. Pero si SCP puede comprobar los metadatos de hello emitidos por pitorro transaccional, puede llamar a `Fail()` cuando Hola metadatos no son válida.

Hola `parms` parámetros de entrada en estas funciones son diccionario vacío, se reservan para uso futuro.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt es la interfaz de Hola para rayo transaccional.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`se llama cuando hay nueva tupla que llegan al rayo Hola. `FinishBatch()` se llama cuando esta transacción finaliza. Hola `parms` parámetro de entrada está reservado para uso futuro.

En el caso de una topología transaccional, existe un concepto importante, `StormTxAttempt`. Tiene dos campos, `TxId` y `AttemptId`. `TxId`es tooidentify usa una transacción específica y para una transacción determinada, puede haber varios intento si transacción Hola se produce un error y es volver a reproducir. SCP.NET nuevo le un diferentes ISCPBatchBolt objeto tooprocess cada `StormTxAttempt`, igual que ¿en qué Storm en lado de Java. propósito de Hola de este diseño es toosupport procesamiento de transacciones paralelas. Usuario debe mantenerlo en cuenta que si finaliza el intento de transacción, se destruirá el objeto ISCPBatchBolt correspondiente de Hola y el recolector.

## <a name="object-model"></a>Modelo de objetos
SCP.NET también proporciona un sencillo conjunto de objetos de clave para los desarrolladores tooprogram con. Son **Context**, **StateStore** y **SCPRuntime**. Se explicará en parte del resto de Hola de esta sección.

### <a name="context"></a>Context
Contexto proporciona una aplicación en ejecución entorno toohello. Cada instancia de ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) tiene su correspondiente instancia de Context. funcionalidad de Hello proporcionada por contexto puede dividirse en dos partes: parte estática (1) Hola que está disponible en Hola todo C\# procesar parte dinámica de hello (2), que solo está disponible para la instancia de contexto específica de Hola.

### <a name="static-part"></a>Parte estática
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger` se proporciona con fines de registro.

`pluginType`es utiliza el tipo de complemento de hello tooindicate de hello C\# proceso. Si Hola C\# proceso se ejecuta en modo de prueba local (sin Java), el tipo de complemento de hello es `SCP_NET_LOCAL`.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`se proporciona tooget parámetros de configuración del lado de Java. Hola parámetros se pasan desde el lado de Java cuando C\# se inicializa el complemento. Hola `Config` parámetros se dividen en dos partes: `stormConf` y `pluginConf`.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`es parámetros definidos por Storm y `pluginConf` es parámetros Hola definidos por el SCP. Por ejemplo:

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`es proporcionado por el contexto de topología de hello tooget, es muy útil para los componentes con varios paralelismo. Aquí tiene un ejemplo:

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a>Parte dinámica
Hola siguientes interfaces es pertinente tooa cierto instancia de contexto. instancia de contexto de Hello es creada por plataforma SCP.NET y pasa toohello código de usuario:

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

Por pitorro no transaccional que admite la confirmación, se proporciona Hola siguiente método:

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

Para admitir la confirmación de rayo no transaccionales, lo que debería explícitamente `Ack()` o `Fail()` Hola tupla que recibió. Y cuando se emiten nueva tupla, también debe especificar delimitadores de Hola de hello nueva tupla. Hola siguiendo métodos se proporciona.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore` proporciona servicios de metadatos, generación de secuencias monotónicas y coordinación sin espera. En `StateStore`, se pueden compilar abstracciones de simultaneidad distribuidas de nivel más alto, como bloqueos distribuidos, colas distribuidas, barreras y servicios de transacciones.

Aplicaciones de SCP pueden utilizar hello `State` objeto toopersist cierta información en ZooKeeper, especialmente para la topología transaccional. Así, si pitorro transaccional se bloquea y se reinicia, puede recuperar la información necesaria de Hola de ZooKeeper y reiniciar canalización Hola.

Hola `StateStore` objeto principalmente tiene estos métodos:

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

Hola `State` objeto principalmente tiene estos métodos:

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

Para hello `Commit()` método, cuando simpleMode se establece tootrue, eliminará simplemente Hola correspondiente ZNode en ZooKeeper. En caso contrario, se eliminarán Hola ZNode actual y agregar un nuevo nodo en hello confirmado\_ruta de acceso.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime proporciona Hola siguiendo dos métodos.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`es el entorno de runtime de hello SCP de tooinitialize usado. En este método, Hola C\# proceso conectará toohello lado de Java y obtiene los parámetros de configuración y el contexto de topología.

`LaunchPlugin()`se usa tookick desactivar mensajes de bienvenida del bucle de procesamiento. En este bucle Hola C\# complemento recibirá mensajes forma parte de Java (incluidas las señales de control y tuplas) y, a continuación, proporcionan mensajes de saludo de proceso, quizás una llamada a método de interfaz de hello mediante código de usuario de Hola. parámetro de entrada de Hello para el método `LaunchPlugin()` es un delegado que puede devolver un objeto que implementa la interfaz de ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

Para ISCPBatchBolt, podemos obtener `StormTxAttempt` de `parms`y usar toojudge si es un intento de reproducido. Esto se hace normalmente en rayo de confirmación de Hola y se muestra en hello `HelloWorldTx` ejemplo.

Por lo general, Hola SCP complementos se puede ejecutar en dos modos aquí:

1. Modo de prueba local: En este modo, Hola SCP complementos (Hola C\# código de usuario) ejecute dentro de Visual Studio durante la fase de desarrollo de Hola. `LocalContext`puede usarse en este modo, que proporciona el método tooserialize Hola genera tuplas toolocal archivos y vuelva toomemory a leerlos.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. Modo normal: En este modo, Hola SCP complementos se inician por proceso de java de storm.
   
    A continuación se ofrece un ejemplo de inicio de un complemento de SCP:
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a>Lenguaje de especificación de topologías
La especificación de topologías de SCP es un lenguaje específico de dominios para la descripción y configuración de topologías de SCP. Se basa en Clojure DSL de Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) y se amplía con SCP.

Especificaciones de la topología pueden enviarse directamente toostorm de clúster para la ejecución a través de hello ***runspec*** comando.

SCP.NET ha Agregar seguimiento funciones toodefine Hola topología transaccional:

| **Nuevas funciones** | **Parámetros** | **Descripción** |
| --- | --- | --- |
| **tx-topolopy** |topology-name<br />spout-map<br />bolt-map |Definir una topología transaccional con el nombre de la topología de hello, &nbsp;spouts mapa de definición y mapa de definición de tornillos de Hola |
| **scp-tx-spout** |exec-name<br />args<br />fields |Permite definir un spout transaccional. Se ejecutará la aplicación hello con ***nombre exec*** con ***args***.<br /><br />Hola ***campos*** es los campos de salida de hello para pitorro |
| **scp-tx-batch-bolt** |exec-name<br />args<br />fields |Permite definir un bolt de lote. Se ejecutará la aplicación hello con ***nombre exec*** con ***args.***<br /><br />Hello campos es hello campos de salida para el rayo. |
| **scp-tx-commit-bolt** |exec-name<br />args<br />fields |Permite definir un bolt de autor. Se ejecutará la aplicación hello con ***nombre exec*** con ***args***.<br /><br />Hola ***campos*** es los campos de salida de hello de rayo |
| **nontx-topolopy** |topology-name<br />spout-map<br />bolt-map |Definir una topología no transaccionales con el nombre de la topología de hello,&nbsp; spouts mapa de definición y mapa de definición de tornillos de Hola |
| **scp-spout** |exec-name<br />args<br />fields<br />Parámetros |Permite definir un spout no transaccional. Se ejecutará la aplicación hello con ***nombre exec*** con ***args***.<br /><br />Hola ***campos*** es los campos de salida de hello para pitorro<br /><br />Hola ***parámetros*** es opcional, con toospecify algunos parámetros, como "nontransactional.ack.enabled". |
| **scp-bolt** |exec-name<br />args<br />fields<br />Parámetros |Permite definir un bolt no transaccional. Se ejecutará la aplicación hello con ***nombre exec*** con ***args***.<br /><br />Hola ***campos*** es los campos de salida de hello de rayo<br /><br />Hola ***parámetros*** es opcional, con toospecify algunos parámetros, como "nontransactional.ack.enabled". |

SCP.NET tiene definidas las siguientes palabras clave:

| **Palabras clave** | **Descripción** |
| --- | --- |
| **:name** |Definir Hola topología nombre |
| **:topology** |Definir Hola topología mediante Hola por encima de las funciones y se generan en los que se. |
| **:p** |Definir la sugerencia de paralelismo de Hola para cada pitorro o rayo. |
| **:config** |Definir parámetro configura o actualización hello las existentes |
| **:schema** |Definir Hola esquema de secuencia. |

Y los parámetros de uso frecuente:

| **Parámetro** | **Descripción** |
| --- | --- |
| **"plugin.name"** |nombre de archivo ejecutable de complemento de hello C# |
| **"plugin.args"** |Argumentos del complemento |
| **"output.schema"** |Esquema de salida |
| **"nontransactional.ack.enabled"** |Indica si se ha habilitado confirmación para una topología no transaccional |

comando de Hello runspec se implementará junto con los bits de Hola, uso de hello es similar:

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

Hola ***recursos dir*** parámetro es opcional, deberá toospecify, cuando se desea tooplug una C\# aplicación y este directorio contendrá la aplicación hello, dependencias de Hola y las configuraciones.

Hola ***classpath*** parámetro también es opcional. Es utilizado toospecify Hola Java classpath si archivo especificaciones de hello contiene apetezca charlar Java o rayo.

## <a name="miscellaneous-features"></a>Características varias
### <a name="input-and-output-schema-declaration"></a>Declaración de esquema de entrada y salida
usuario de Hello puede emitir la tupla en C\# procesar, hello plataforma necesita tooserialize Hola tupla en byte [], transferencia tooJava lado, y Storm transferirá este destinos de toohello de tupla. Mientras tanto en el componente de nivel inferior, Hola C\# proceso recibirá tupla desde el lado de java y convertir los tipos originales de toohello por plataforma, todas estas operaciones se ocultan de forma Hola plataforma.

serialización de hello toosupport y la deserialización, el código de usuario debe toodeclare esquema de Hola de hello entradas y salidas.

esquema de flujo de entrada/salida de Hello, se definen como un diccionario, clave de hello es hello StreamId y valor hello es Hola tipos de columnas de Hola. componente de Hello puede tener varias secuencias declarados.

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


En el objeto de contexto, tenemos Hola agrega la siguiente API:

    public void DeclareComponentSchema(ComponentStreamSchema schema)

Código de usuario debe asegurarse de que tuplas Hola genera obedecen a esquema Hola definido para esa secuencia o sistema Hola producirá una excepción en tiempo de ejecución.

### <a name="multi-stream-support"></a>Compatibilidad con varias transmisiones
SCP admite usuario código tooemit o recibir mensajes de varias secuencias distintas a Hola mismo tiempo. compatibilidad de Hola se refleja en el objeto de contexto de hello como Hola Emit método toma un parámetro de identificador de secuencia opcional.

Se han agregado dos métodos de hello objeto de contexto de SCP.NET. Únicamente son utilizados tooemit tupla o tuplas toospecify StreamId. Hola StreamId es una cadena y debe toobe coherentes en ambos C\# y Hola especificación de definición de topología.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

secuencia de inexistente emitir de tooa Hola darán lugar a excepciones de tiempo de ejecución.

### <a name="fields-grouping"></a>Agrupación de campos
Hola que compilación en campos de agrupación en Strom no funciona correctamente en SCP.NET. Hola lado de Proxy de Java, todos los tipos de datos de campos de hello son realmente el byte [] y campos de hello agrupación utilizará Hola byte [] objeto hash tooperform Hola agrupación de código. código hash de Hello byte [] objeto es la dirección de Hola de este objeto en memoria. Modo de agrupación Hola serán incorrecto para dos bytes [] objetos ese Hola de recurso compartido mismo contenido pero no Hola la misma dirección.

SCP.NET agrega un método de agrupación personalizada, y va a utilizar contenido Hola de agrupación de hello byte [] toodo Hola. En **especificación** archivo, la sintaxis de hello es similar:

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


Aquí,

1. "scp-field-group" significa "Agrupación personalizada de campos implementada mediante SCP".
2. ":tx" o ":non-tx" indica si se trata de una topología transaccional. Necesitamos esta información desde Hola índice de inicio es diferente en tx frente a topologías no tx.
3. [0,1] indica un hashset de campos de identificadores, a partir de 0.

### <a name="hybrid-topology"></a>Topologías híbridas
Hola que Storm nativo se escribe en Java. Y SCP.Net ha mejorado tooenable nuestro toowrite aduaneras C\# código toohandle su lógica de negocios. Pero también admitimos topologías híbridas que no solo contengan spouts y bolts de C\#, sino también spouts y bolts de Java.

### <a name="specify-java-spoutbolt-in-spec-file"></a>Especificación de spout o bolt de Java en el archivo de especificación
En el archivo de especificación, "scp pitorro" y "scp rayo" también pueden ser usado toospecify Java Spouts y tornillos, este es un ejemplo:

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

Aquí `microsoft.scp.example.HybridTopology.Generator` es nombre Hola de hello clase apetezca charlar Java.

### <a name="specify-java-classpath-in-runspec-command"></a>Especificación de classpath de Java en el comando runSpec
Si desea que la topología toosubmit que contiene Spouts Java o tornillos, es necesario toofirst compilación hello Spouts Java o tornillos y obtener los archivos Jar de Hola. A continuación, debe especificar Hola classpath de java que contiene los archivos Jar de hello al enviar la topología. Aquí tiene un ejemplo:

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

Aquí **ejemplos\\HybridTopology\\java\\destino\\**  es Hola carpeta que contiene archivos Jar de Java pitorro/rayo de Hola.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Serialización y deserialización entre Java y C\
El componente de SCP incluye Java y C\#. En orden toointeract con Spouts/tornillos de Java nativo, serialización/deserialización debe llevarse a cabo entre el lado de Java y C\# en paralelo, como se muestra en hello después de gráfico.

![diagrama de componente de java enviar componente tooSCP enviar tooJava componente](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Serialización en Java y deserialización en C\#**
   
   En primer lugar, proporcionamos la implementación predeterminada de serialización en la parte Java y deserialización en la parte C\#. método de serialización de Hello en el lado de Java puede especificarse en el archivo de especificación:
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   Hola método de deserialización en C\# lado debe especificarse en C\# código de usuario:
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Esta implementación predeterminada debe controlar la mayoría de los casos si el tipo de datos de hello no es demasiado complejo. En ciertos casos, ya sea porque hello tipo de datos de usuario es demasiado complejo o porque hello resultados de la implementación predeterminada no satisfacen Hola a requisito del usuario, el complemento de usuario pueden su propia implementación.
   
   Hola serializar la interfaz en java lado se define como:
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   Hola deserializar interfaz en C\# lado se define como:
   
   public interface ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **Serialización en C\# y deserialización en Java**
   
   método de serialización de C de Hola\# lado debe especificarse en C\# código de usuario:
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   Hola método de deserialización en el lado de Java debe especificarse en el archivo de especificación:
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   Aquí "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" es el nombre de hello del deserializador, y "microsoft.scp.example.HybridTopology.Person" es se deserializan datos de Hola de clase de destino de Hola.
   
   El usuario también puede usar su propia implementación de serializador de C\# y deserializador de Java. Se trata de interfaz de Hola para C\# serializador:
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   Ésta es la interfaz de Hola para deserializador de Java:
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>Modo host de SCP
En este modo, usuario puede compilar su tooDLL de códigos y usar SCPHost.exe proporcionada por la topología de toosubmit SCP. archivo de especificación de Hello tiene el siguiente aspecto:

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

En este caso, `plugin.name` se especifica como `SCPHost.exe` proporcionado por el SDK de SCP. SCPHost.exe que acepta exactamente tres parámetros:

1. Hello primero uno es nombre de la DLL de hello, que es `"HelloWorld.dll"` en este ejemplo.
2. segunda Hello es nombre de clase de hello, que es `"Scp.App.HelloWorld.Generator"` en este ejemplo.
3. Hello en tercer lugar uno es Hola nombre de un método estático público, que puede ser invocado tooget una instancia de ISCPPlugin.

En modo host, el código de usuario se compila como DLL y lo invoca la plataforma SCP. Por lo que plataforma SCP puede obtener el control completo de la lógica de procesamiento completo de Hola. Por lo que recomendamos a nuestros clientes toosubmit topología en modo de host de SCP ya que puede simplificar la experiencia de desarrollo de Hola y traiga más flexibilidad y mejor compatibilidad con versiones anteriores para versiones posteriores también.

## <a name="scp-programming-examples"></a>Ejemplos de programación de SCP
### <a name="helloworld"></a>HelloWorld
**HelloWorld** es un ejemplo muy sencillo tooshow un sabor de SCP.Net. Se usa una topología no transaccional, con un spout llamado **generator** y dos bolts llamados **splitter** y **counter**. pitorro Hello **generador** aleatoriamente generará algunas frases y emitir estas frases demasiado**divisor**. tornillo de Hello **divisor** se divide Hola frases toowords y emitir estas palabras demasiado**contador** rayo. Hola rayo "counter" usa un número de aparición de diccionario toorecord Hola de cada palabra.

En este ejemplo, hay dos archivos de especificación, **HelloWorld.spec** y **HelloWorld\_EnableAck.spec**. Hola C\# código, puede averiguar si está habilitada la confirmación obteniendo hello pluginConf de lado de Java.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

En pitorro hello, si está habilitada la confirmación, un diccionario es toocache usado Hola tuplas que no han sido realizados. Si se llama a Fail(), hello error tupla se reproduzca:

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a>HelloWorldTx
Hola **HelloWorldTx** en el ejemplo se muestra cómo tooimplement transaccional topología. Incluye un spout denominado **generator**, un bolt de lote denominado **partial-count** y un bolt de confirmación denominado **count-sum**. Existen también tres archivos txt creados previamente: **DataSource0.txt**, **DataSource1.txt** y **DataSource2.txt**.

En cada transacción, Hola pitorro **generador** aleatoriamente se elija dos archivos de hello previamente creado tres archivos y emitir toohello de nombres de archivo de hello dos **parcial recuento** rayo. tornillo de Hello **parcial recuento** primero obtendrá el nombre del archivo de hello de la tupla de hello recibido, Hola abrir archivo y recuento Hola el número de palabras en este archivo y finalmente emitir hello word número toohello **desumaderecuento**rayo. Hola **recuento suma** rayo mostrará un resumen de recuento total de Hola.

tooachieve **exactamente una vez** semántica, rayo de confirmación de hello **recuento suma** necesita toojudge si es una transacción reproducida. En este ejemplo se incluye una variable de miembro estática:

    public static long lastCommittedTxId = -1; 

Cuando se crea una instancia de ISCPBatchBolt, obtendrá hello `txAttempt` de parámetros de entrada:

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

Cuando `FinishBatch()` se llama, hello `lastCommittedTxId` será la actualización si no es una transacción reproducida.

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a>HybridTopology
Esta topología contiene un spout de Java y un bolt de C\#. Utiliza la implementación de serialización y deserialización de la predeterminada de hello proporcionada por la plataforma de SCP. Inicie Hola ref **HybridTopology.spec** en **ejemplos\\HybridTopology** carpeta para obtener detalles de especificación de archivo de hello, y **SubmitTopology.bat** para saber cómo toospecify Java classpath.

### <a name="scphostdemo"></a>SCPHostDemo
En este ejemplo se Hola igual que HelloWorld en esencia. Hello la única diferencia es que se compila código de usuario de hello como DLL y topología de Hola se envía mediante SCPHost.exe. Realice una sección de hello ref "Modo de Host de SCP" para ver una explicación más detallada.

## <a name="next-steps"></a>Pasos siguientes
Para obtener ejemplos de topologías de Storm siguieron SCP, vea Hola siguiente:

* [Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [Creación de varios flujos de datos en una topología de Storm en C#](hdinsight-storm-twitter-trending.md)
* [Usar datos de Power Bi toovisualize de una topología de Storm](hdinsight-storm-power-bi-topology.md)
* [Procesamiento de los datos de sensor del vehículo desde Centros de eventos usando Storm en HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [Extracción, transformación y carga (ETL) de los centros de eventos de Azure tooHBase](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [Poner en correlación eventos con Storm y HBase en HDInsight](hdinsight-storm-correlation-topology.md)

