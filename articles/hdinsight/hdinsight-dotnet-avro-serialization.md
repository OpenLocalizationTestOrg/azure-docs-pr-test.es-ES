---
title: datos de aaaSerialize en Hadoop - Microsoft Avro Library - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooserialize y deserializar los datos en Hadoop en HDInsight con hello Microsoft Avro Library toopersist toomemory, una base de datos o archivo."
keywords: avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>Serializar datos en Hadoop con hello Microsoft Avro Library

>[!NOTE]
>Hola Avro SDK ya no es compatible con Microsoft. biblioteca de Hello es la Comunidad de código abierto que admite. orígenes de Hello para la biblioteca de Hola se encuentran en [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

Este tema se muestra cómo hello toouse [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objetos y otros datos de las estructuras en secuencias toopersist les toomemory, una base de datos o un archivo. También se muestra cómo toodeserialize ellos objetos originales de toorecover Hola.

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
Hola <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implementa Hola Apache Avro sistema de serialización de datos para el entorno de Microsoft.NET Hola. Apache Avro proporciona un formato compacto de intercambio de datos binarios para la serialización. Usa <a href="http://www.json.org" target="_blank">JSON</a> toodefine un esquema independiente del idioma que emite la interoperabilidad entre lenguajes. Los datos serializados en un lenguaje se pueden leer en otro. Actualmente, se admiten C, C++, C#, Java, PHP, Python y Ruby. Encontrará información detallada en formato de hello en hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">especificación de Apache Avro</a>. 

>[!NOTE]
>Hola Microsoft Avro Library no admite Hola procedimiento remoto (RPC) llamadas parte de esta especificación.
>

representación en forma de Hello serializado de un objeto en hello Avro sistema consta de dos partes: esquema y el valor real. un esquema de Avro Hola describe el modelo de datos independiente del lenguaje de Hola de datos de hello serializar con JSON. Se presenta en paralelo con una representación binaria de los datos. Tener esquema Hola independiente de la representación binaria de hello permite que cada toobe objeto escrito con ningún sobrecargas por valor, realizar serialización rápido y hello representación en forma de pequeños.

## <a name="hello-hadoop-scenario"></a>escenario de Hello Hadoop
formato de serialización de Apache Avro Hola se usa ampliamente en HDInsight de Azure y otros entornos de Apache Hadoop. Avro proporciona una manera cómoda de toorepresent las estructuras de datos complejos en un trabajo de Hadoop MapReduce. formato de Hola de Avro archivos (Avro objeto contenedor) ha sido diseñado toosupport Hola distribuida MapReduce modelo de programación. característica clave de Hola que habilita la distribución de hello es que los archivos de Hola son "divisibles" en el sentido de Hola que uno puede buscar cualquier punto en un archivo e iniciar la lectura de un bloque específico.

## <a name="serialization-in-avro-library"></a>Serialización de Avro Library
Hola biblioteca .NET para Avro admite dos formas de serialización de objetos:

* **reflexión** -esquema JSON de Hola para tipos de hello es automáticamente compilado a partir Hola datos atributos de contrato de toobe de tipos .NET Hola serializado.
* **registro genérico** -esquema A JSON se especifica explícitamente en un registro representado por hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) clase cuando no hay tipos de .NET están presentes esquema toodescribe Hola Hola datos toobe serializar.

Cuando se conoce el esquema de datos de Hola escritor de hello tooboth y un lector de secuencia de Hola, pueden enviarse datos Hola sin su esquema. En los casos cuando se utiliza un archivo de contenedor de objetos de Avro, esquema de Hola se almacena en el archivo hello. Se pueden especificar otros parámetros, como el códec de hello utilizado para la compresión de datos. Estos escenarios se describen con más detalle y se muestra en hello ejemplos de código siguientes:

## <a name="install-avro-library"></a>Instalación de Avro Library
Hola se necesita siguiente antes de instalar biblioteca de hello:

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (v5.6.0.4 o posterior)

Tenga en cuenta que hello Newtonsoft.Json.dll dependencia se descarga automáticamente con la instalación de Hola de hello Microsoft Avro Library. procedimiento de Hola se proporciona en hello pasos de la sección:

Hola Microsoft Avro Library se distribuye como un paquete de NuGet que puede instalarse desde Visual Studio a través de hello siguiendo el procedimiento:

1. Seleccione hello **proyecto** -> pestaña **administrar paquetes de NuGet...**
2. Busque "Microsoft.Hadoop.Avro" Hola **buscar en línea** cuadro.
3. Haga clic en hello **instalar** aparece al lado demasiado**biblioteca Avro de Microsoft Azure HDInsight**.

Tenga en cuenta que hello Newtonsoft.Json.dll (> = 6.0.4) dependencia también se descarga automáticamente con hello Microsoft Avro Library.

Hola código fuente de Microsoft Avro Library está disponible en [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

## <a name="compile-schemas-using-avro-library"></a>Compilación de esquemas con Avro Library
Hola Microsoft Avro Library contiene una generación de código previamente definidas por la utilidad que permite crear tipos de C# automáticamente en función de hello esquema JSON. utilidad de generación de código de Hello no se distribuye como un archivo ejecutable binario, pero se puede crear fácilmente a través de hello siguiendo el procedimiento:

1. Descargar archivo de .zip hello con la versión más reciente de Hola de código fuente de SDK de HDInsight desde <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">de Hadoop de Microsoft .NET SDK</a>. (Haga clic en hello **descargar** icono, y no Hola **descarga** ficha.)
2. Extraer Hola directorio tooa de SDK de HDInsight en la máquina de hello con .NET Framework 4 había instalado y conectado toohello Internet para descargar paquetes de NuGet dependencia necesaria. A continuación, se supone que el código fuente de hello es tooC:\SDK extraídos.
3. Vaya toohello carpeta C:\SDK\src\Microsoft.Hadoop.Avro.Tools y ejecute build.bat. (Hola MSBuild del archivo llamadas de distribución de 32 bits de Hola de hello .NET Framework. Si desea que la versión de 64 bits de hello toouse, edite build.bat, sigue Hola comentarios dentro de archivo hello.) Asegúrese de que la compilación de hello es correcta. (En algunos sistemas, MSBuild puede producir advertencias. Estas advertencias no afectan a la utilidad de hello siempre que no hay ningún error de compilación.)
4. utilidad de Hello compilado se encuentra en C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.

tooget familiarizado con la sintaxis de línea de comandos de hello, ejecute hello siguiente comando desde la carpeta Hola donde se encuentra la utilidad de generación de código de hello:`Microsoft.Hadoop.Avro.Tools help /c:codegen`

utilidad de hello tootest, puede generar clases de C# desde proporcionado con el código de origen de Hola de archivo del esquema JSON de ejemplo Hola. Ejecute el siguiente comando de hello:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

Esto debe tooproduce C# dos archivos en el directorio actual de hello: SensorData.cs y Location.cs.

lógica de hello toounderstand que está usando la utilidad de generación de código de hello al convertir tipos tooC # esquema JSON de hello, vea archivo hello GenerationVerification.feature ubicado en C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.

Espacios de nombres se extraen del esquema JSON de hello, mediante una lógica Hola que se describe en archivo hello mencionado en el párrafo anterior Hola. Espacios de nombres que se extrae del esquema de hello tienen prioridad sobre lo que se proporciona con el parámetro/n. de hello en línea de comandos de utilidad Hola. Si desea que los espacios de nombres Hola de toooverride dentro de esquema de hello, use el parámetro de /nf de Hola. Por ejemplo, toochange todos los espacios de nombres de hello SampleJSONSchema.avsc toomy.own.nspace, ejecute Hola comando siguiente:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>Acerca de los ejemplos de hello
Seis ejemplos proporcionados en este tema ilustran escenarios diferentes compatibles con Microsoft Avro Library Hola. Hola Microsoft Avro Library está diseñada toowork con cualquier flujo. En estos ejemplos, los datos se manipulan usando secuencias de memoria en lugar de secuencias de archivos o bases de datos por simplicidad y coherencia. enfoque de Hello realizada en un entorno de producción depende de los requisitos de escenario exacto de hello, origen de datos y volumen, las restricciones de rendimiento y otros factores.

Hola primera dos ejemplos se muestra cómo tooserialize y deserializar los datos en búferes de secuencia de memoria mediante el uso de registros genéricos y reflexión. Hello en estos dos casos se asume el esquema toobe compartida Hola lectores y escritores fuera de banda.

Hola tercero y cuarto ejemplos muestran cómo tooserialize y deserializar los datos mediante el uso de archivos de contenedor de objeto de hello Avro. Cuando los datos se almacenan en un archivo de contenedor de Avro, su esquema siempre se almacena con él porque el esquema de hello debe compartirse para la deserialización.

Hello que contiene el ejemplo hello primeros cuatro puede descargar los ejemplos de hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">ejemplos de código de Azure</a> sitio.

Hola quinto ejemplo se muestra cómo toouse un códec de compresión personalizada para Avro objeto archivos de contenedor. Un ejemplo que contiene código de hello para este ejemplo puede descargarse desde hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">ejemplos de código de Azure</a> sitio.

ejemplo de Hola a sexto muestra cómo toouse Avro serialización tooupload datos tooAzure almacenamiento de blobs y, a continuación, se analizan mediante subárbol con un clúster de HDInsight (Hadoop). Se puede descargar desde hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">ejemplos de código de Azure</a> sitio.

Estos son vínculos toohello seis muestras que se describe en el tema de hello:

* <a href="#Scenario1">**Serialización con reflexión** </a> -esquema JSON de Hola para toobe tipos serializado es automáticamente compilado a partir Hola datos atributos de contrato.
* <a href="#Scenario2">**Serialización con registro genérico** </a> -esquema JSON de Hola se especifica explícitamente en un registro cuando ningún tipo de .NET esté disponible para la reflexión.
* <a href="#Scenario3">**Serialización mediante archivos de contenedor de objeto mediante la reflexión** </a> -esquema JSON de hello automáticamente se genera y compartido junto con datos de hello serializar a través de un archivo de contenedor de objetos de Avro.
* <a href="#Scenario4">**Serialización con archivos de contenedor de objeto de registro genérico** </a> -esquema JSON de hello explícitamente se especifica antes de la serialización de Hola y compartido junto con datos de Hola a través de un archivo de contenedor de objetos de Avro.
* <a href="#Scenario5">**Serialización mediante archivos de contenedor de objeto con un códec de compresión personalizada** </a> -Hola ilustra cómo toocreate una Avro objeto archivo contenedor con una implementación personalizada de .NET de códec de compresión de datos de hello Deflate.
* <a href="#Scenario6">**Utilizando los datos de tooupload de Avro para hello servicio Microsoft Azure HDInsight** </a> -Hola ilustra cómo interactúa la serialización de Avro con hello servicio HDInsight. Un activo Azure acceso y suscripción tooan clúster de HDInsight de Azure requiere toorun en este ejemplo.

## <a name="Scenario1"></a>Muestra 1: serialización mediante el uso de reflexión
esquema JSON de Hola para tipos de hello puede crearse automáticamente por hello Microsoft Avro Library a través de reflexión de datos de hello atributos de contrato de hello C# objetos toobe serializado. Hello Microsoft Avro Library se crea un [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify Hola campos toobe serializado.

En este ejemplo, objetos (un **SensorData** clase con un miembro **ubicación** struct) son tooa serializado secuencia de memoria y, a su vez se deserializa esta secuencia. Hello resultado es comparado toohello inicial instancia tooconfirm ese hello **SensorData** objeto recuperado es idéntico toohello original.

esquema de Hello en este ejemplo se supone toobe compartida entre Hola lectores y escritores, de modo que el formato de contenedor de objeto de hello Avro no es necesario. Para obtener un ejemplo de cómo tooserialize y deserializar los datos en búferes de memoria utilizando la reflexión con formato de contenedor de objeto de hello al esquema de hello debe compartirse con datos de hello, consulte <a href="#Scenario3">serialización mediante archivos de contenedor de objeto mediante la reflexión</a>.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a>Ejemplo 2: Serialización con un registro genérico
Un esquema JSON se puede especificar explícitamente en un registro genérico cuando no se puede usar la reflexión porque no se puede representar datos de Hola a través de las clases de .NET con un contrato de datos. Este método es más lento que cuando se utiliza la reflexión. En tales casos, Hola esquema para los datos de hello puede también ser dinámico, es decir, no se conoce en tiempo de compilación. Datos representados como valores separados por comas (CSV) archivos cuyo esquema se encuentra desconocido hasta que se transforme toohello el formato Avro en tiempo de ejecución es un ejemplo de este tipo de escenario dinámico.

Este ejemplo se muestra cómo toocreate y utilizar una [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly especificar un esquema JSON, cómo toopopulate con datos de hello y, a continuación, cómo tooserialize y deserializarla. a continuación, se compara el resultado de Hello toohello tooconfirm de instancias inicial que Hola registro recuperado es idéntico toohello original.

esquema de Hello en este ejemplo se supone toobe compartida entre Hola lectores y escritores, de modo que el formato de contenedor de objeto de hello Avro no es necesario. Para obtener un ejemplo de cómo tooserialize y deserializar los datos en búferes de memoria mediante un registro genérico con formato de contenedor de objeto de hello al esquema Hola se debe incluir datos Hola serializar, consulte hello <a href="#Scenario4">serialización mediante el contenedor de objetos archivos de registro genérico</a> ejemplo.

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>Ejemplo 3: Serialización mediante el uso de archivos contenedores de objetos y serialización con reflexión
En este ejemplo es similar toohello escenario en hello <a href="#Scenario1"> primer ejemplo</a>, donde el esquema de hello implícitamente se especifica mediante la reflexión. Hola diferencia es que en este caso, esquema de Hola se supone que no toobe conocida lector toohello que lo deserializa. Hola **SensorData** toobe de objetos serializado y su esquema implícitamente especificado se almacenan en un archivo de contenedor de objeto Avro representado por hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) clase.

en este ejemplo con los datos de Hola se serializan [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) y deserializados con [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). resultado de Hello es, a continuación, toohello comparados instancias iniciales tooensure identidad.

Hola Hola objeto de datos se comprime el archivo de contenedor a través del valor predeterminado de hello [ **Deflate** ] [ deflate-100] códec de compresión de .NET Framework 4. Vea hello <a href="#Scenario5"> quinto ejemplo</a> en este tema toolearn cómo toouse una versión más reciente y superior de hello [ **Deflate** ] [ deflate-110] compresión códec disponible en .NET Framework 4.5.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>Ejemplo 4: Serialización mediante el uso de archivos contenedores de objetos y serialización con registro genérico
En este ejemplo es similar toohello escenario en hello <a href="#Scenario2"> segundo ejemplo</a>, donde se especifica explícitamente el esquema de hello con JSON. Hola diferencia es que en este caso, esquema de Hola se supone que no toobe conocida lector toohello que lo deserializa.

conjunto de datos de prueba Hello se recopila una en una lista de [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objetos a través de un esquema definido explícitamente de JSON y, a continuación, se almacenan en un archivo de contenedor del objeto representado por hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) clase. Este archivo contenedor crea un sistema de escritura que son datos de hello tooserialize utilizados, no lo está, secuencia de memoria tooa que, a continuación, se guarda el archivo tooa. Hola [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parámetro usado para crear el lector de hello especifica que estos datos no se comprimen.

datos Hello, a continuación, se lee desde archivo hello y deserializa en una colección de objetos. Esta colección es toohello en comparación con la lista inicial de Avro tooconfirm de registros que son idénticos.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>Ejemplo 5: Serialización mediante el uso de archivos contenedores de objetos con un códec de compresión personalizado
Hola quinto ejemplo se muestra cómo toouse un códec de compresión personalizada para Avro objeto archivos de contenedor. Un ejemplo que contiene código de hello para este ejemplo puede descargarse desde hello [ejemplos de código de Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) sitio.

Hola [especificación de Avro](http://avro.apache.org/docs/current/spec.html#Required+Codecs) permite el uso de un códec de compresión opcional (además demasiado**Null** y **Deflate** valores predeterminados). En este ejemplo se implementa un códec nueva como Snappy (mencionadas como un códec opcional compatible en hello [Avro especificación](http://avro.apache.org/docs/current/spec.html#snappy)). Muestra cómo toouse Hola implementación de .NET Framework 4.5 de hello [ **Deflate** ] [ deflate-110] códec, que proporciona un mejor algoritmo de compresión basado en hello [zlib](http://zlib.net/) biblioteca de compresión que la versión de .NET Framework 4 hello predeterminada.

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>Ejemplo 6: Usar datos de tooupload de Avro para hello servicio HDInsight de Azure de Microsoft
ejemplo de Hola a sexto muestra algunos toointeracting de programación técnicas relacionadas con el servicio de HDInsight de Azure de Hola. Un ejemplo que contiene código de hello para este ejemplo puede descargarse desde hello [ejemplos de código de Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) sitio.

ejemplo de Hola Hola las siguientes tareas:

* Se conecta tooan existente HDInsight servicio de cluster Server.
* Serializa varios archivos CSV y carga el almacenamiento de blobs de hello resultado tooAzure. (archivos CSV de Hola se distribuyen junto con el ejemplo hello y representan una extracción de datos históricos de American Express existencias distribuidos por [Infochimps](http://www.infochimps.com/) durante el período de hello 1970-2010. ejemplo de Hola lee datos del archivo CSV, convierte Hola tooinstances registros de hello **existencias** clase y, a continuación, se serializa utilizando la reflexión. Definición de tipo estándar se crea a partir de un esquema JSON a través de la utilidad de generación de código de Microsoft Avro Library Hola.
* Crea una nueva tabla externa denominada **las existencias** en el subárbol y se proporcionan vínculos toohello datos cargados en el paso anterior de Hola.
* Ejecuta una consulta a través de Hive hello **las existencias** tabla.

Además, ejemplo de Hola realiza un procedimiento de limpieza antes y después de realizar operaciones principales. Durante el saludo limpieza, todos los de hello relacionados se quitan las carpetas y los datos de Blob de Azure, y se quita la tabla de Hive de Hola. También puede invocar el procedimiento de limpieza de Hola desde línea de comandos de ejemplo de Hola.

ejemplo de Hola tiene Hola siguiendo los requisitos previos:

* Una suscripción activa a Microsoft Azure y su identificador de suscripción.
* Un certificado de administración de la suscripción de hello con clave privada correspondiente de Hola. Hola certificado debe estar instalado en hello actual usuario privada almacenamiento muestra de Hola Hola a toorun máquina que se usa.
* Un clúster de HDInsight activo.
* Una cuenta de almacenamiento de Azure vinculada clúster de HDInsight de toohello de requisitos previos anterior de hello, junto con la clave de acceso principal o secundaria correspondiente Hola.

Antes de ejecuta el ejemplo hello toda información de Hola de requisitos previos de hello debe ser archivo de configuración de ejemplo de toohello especificado. Hay dos toodo de formas:

* Editar el archivo app.config de hello en el directorio raíz del ejemplo hello y, a continuación, compilar el ejemplo de Hola
* Compilar primero el ejemplo hello y, a continuación, edite AvroHDISample.exe.config en directorio de compilación de Hola

En ambos casos, todas las ediciones deberían realizarse en hello  **<appSettings>**  sección de configuración. Siga comentarios Hola Hola del archivo.
Hello ejemplo se ejecuta desde la línea de comandos de hello ejecutando el siguiente comando (donde hello archivo .zip con el ejemplo hello supuso tooC:\AvroHDISample toobe extraído; si Hola relevante en caso contrario, utilice ruta de acceso) de hello:

    AvroHDISample run C:\AvroHDISample\Data

tooclean clúster hello, ejecute el siguiente comando de hello:

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
