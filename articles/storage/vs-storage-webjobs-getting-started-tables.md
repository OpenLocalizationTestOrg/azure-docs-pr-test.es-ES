---
title: aaaGetting iniciado con el almacenamiento de Azure y servicios conectados de Visual Studio (proyectos de trabajo Web)
description: "Cómo tooget iniciado mediante el almacenamiento de tabla de Azure en un proyecto de trabajos Web de Azure en Visual Studio después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Introducción a Almacenamiento de Azure (proyectos de WebJobs de Azure)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Información general
Este artículo se proporcionan ejemplos de código de C# que muestran muestran cómo toouse Hola versión del SDK de WebJobs de Azure 1.x con hello servicio de almacenamiento de tabla de Azure. ejemplos de código de Hello usan hello [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versión 1.x.

Hola servicio de almacenamiento de tabla de Azure permite toostore grandes cantidades de datos estructurados. servicio de Hello es un almacén de datos NoSQL que acepta llamadas autenticadas de dentro y fuera Hola nube de Azure. Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales.  Consulte [Introducción al Almacenamiento de tablas de Azure mediante .NET](storage-dotnet-how-to-use-tables.md#create-a-table) para más información.

Algunos de los fragmentos de código de hello mostrar hello **tabla** atributo utilizado en las funciones que se llaman manualmente, es decir, no con uno de los atributos de desencadenador de Hola.

## <a name="how-tooadd-entities-tooa-table"></a>La tabla de tooadd entidades tooa
tabla de tooa tooadd entidades, use hello **tabla** atributo con un **ICollector<T>**  o **IAsyncCollector<T>**  parámetro donde **T** especifica el esquema de Hola de entidades de hello desea tooadd. constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre de Hola de tabla de Hola.

Hello siguiente ejemplo de código agrega **persona** tabla de entidades tooa denominada *entrada*.

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() {
                        PartitionKey = "Test",
                        RowKey = i.ToString(),
                        Name = "Name" }
                    );
            }
        }

Hola normalmente el tipo que se utiliza con **ICollector** deriva **TableEntity** o implementa **ITableEntity**, pero no es necesario. Cualquiera de los siguientes hello **persona** clases con código de hello mostrado en hello anterior **entrada** método.

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

Si desea que toowork directamente con hello API de almacenamiento de Azure, puede agregar un **CloudStorageAccount** firma del método toohello parámetro.

## <a name="real-time-monitoring"></a>Supervisión en tiempo real
Dado que las funciones de entrada de datos a menudo procesan grandes volúmenes de datos, panel de SDK de WebJobs Hola proporciona datos de supervisión en tiempo real. Hola **invocación registro** sección indica si la función hello se está ejecutando.

![Función de entrada en ejecución](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Hola **detalles de invocación** página informes Hola progreso de la función (número de entidades que escriben) mientras se está ejecutando y proporciona una oportunidad tooabort lo.

![Función de entrada en ejecución](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Cuando función hello finalice, hello **detalles de invocación** página notifica el número de Hola de filas escritas.

![Función de entrada finalizada](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>¿Cómo tooread varias entidades de una tabla
tooread una tabla, utilice hello **tabla** atributo con un **IQueryable<T>**  parámetro donde escribir **T** deriva **TableEntity**o implementa **ITableEntity**.

lee Hello siguiente ejemplo de código y registros de todas las filas de hello **entrada** tabla:

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}",
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <a name="how-tooread-a-single-entity-from-a-table"></a>¿Cómo tooread una sola entidad de una tabla
Hay un **tabla** constructor de atributo con dos parámetros adicionales que le permiten especificar la clave de partición de Hola y clave de fila cuando se desea toobind tooa tabla única entidad.

ejemplo de código siguiente Hello lee una fila de tabla para una **persona** entidad en función de clave y la fila de claves de partición recibidos en un mensaje de cola:  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


Hola **persona** clase en este ejemplo no tiene tooimplement **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>¿Cómo toouse Hola API de almacenamiento de .NET directamente toowork con una tabla
También puede usar hello **tabla** atributo con un **CloudTable** objeto para una mayor flexibilidad cuando se trabaja con una tabla.

usos de ejemplo de código siguiente Hola un **CloudTable** objeto tooadd una sola entidad toohello *entrada* tabla.

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

Para obtener más información acerca de cómo hello toouse **CloudTable** de objetos, consulte [Introducción al almacenamiento de tabla de Azure mediante .NET](storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Temas relacionados cubiertos por las colas de hello cómo-tooarticle
Para obtener información acerca de cómo el procesamiento de tabla toohandle desencadenada por un mensaje de la cola, o de trabajos Web escenarios SDK no procesar, consulte específica tootable [Introducción al almacenamiento de cola de Azure y Visual Studio conectado servicios (proyectos de trabajo Web) ](vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Pasos siguientes
En este artículo ha proporcionado el código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con tablas de Azure. Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).

