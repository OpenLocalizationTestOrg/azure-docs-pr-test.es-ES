---
title: aaaHow toouse almacenamiento de tabla de Azure con hello SDK de WebJobs
description: "Obtenga información acerca de cómo toouse Azure tabla almacenamiento con hello SDK de WebJobs. Crear tablas, agregar entidades tootables y leer las tablas existentes."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>Cómo toouse Azure tabla almacenamiento con hello SDK de WebJobs
## <a name="overview"></a>Información general
Esta guía proporcionan ejemplos de código de C# que muestran cómo tablas tooread y escritura de almacenamiento de Azure mediante el uso de [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versión 1.x.

Guía de Hola se supone que sabe [cómo cadenas toocreate un proyecto WebJob en Visual Studio con una conexión de esa cuenta de almacenamiento de punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o demasiado[varias cuentas de almacenamiento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Algunos de los fragmentos de código de hello mostrar hello `Table` atributo utilizado en las funciones que son [llama manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), es decir, no mediante uno de los atributos de desencadenador de Hola. 

## <a id="ingress"></a>La tabla de tooadd entidades tooa
tabla de tooa tooadd entidades, use hello `Table` atributo con un `ICollector<T>` o `IAsyncCollector<T>` parámetro donde `T` especifica el esquema de Hola de entidades de hello desea tooadd. constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre de Hola de tabla de Hola. 

Hello siguiente ejemplo de código agrega `Person` tabla de entidades tooa denominada *entrada*.

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

Hola normalmente el tipo que se utiliza con `ICollector` deriva `TableEntity` o implementa `ITableEntity`, pero no es necesario. Cualquiera de los siguientes hello `Person` clases con código de hello mostrado en hello anterior `Ingress` método.

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

Si desea que toowork directamente con hello API de almacenamiento de Azure, puede agregar un `CloudStorageAccount` firma del método toohello parámetro.

## <a id="monitor"></a> Supervisión en tiempo real
Dado que las funciones de entrada de datos a menudo procesan grandes volúmenes de datos, panel de SDK de WebJobs Hola proporciona datos de supervisión en tiempo real. Hola **invocación registro** sección indica si la función hello se está ejecutando.

![Función de entrada en ejecución](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

Hola **detalles de invocación** página informes Hola progreso de la función (número de entidades que escriben) mientras se está ejecutando y proporciona una oportunidad tooabort lo. 

![Función de entrada en ejecución](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Cuando función hello finalice, hello **detalles de invocación** página notifica el número de Hola de filas escritas.

![Función de entrada finalizada](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>¿Cómo tooread varias entidades de una tabla
tooread una tabla, utilice hello `Table` atributo con un `IQueryable<T>` parámetro donde escribir `T` deriva `TableEntity` o que implemente `ITableEntity`.

lee Hello siguiente ejemplo de código y registros de todas las filas de hello `Ingress` tabla:

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

### <a id="readone"></a>¿Cómo tooread una sola entidad de una tabla
Hay un `Table` constructor de atributo con dos parámetros adicionales que le permiten especificar la clave de partición de Hola y clave de fila cuando se desea toobind tooa tabla única entidad.

ejemplo de código siguiente Hello lee una fila de tabla para una `Person` entidad en función de clave y la fila de claves de partición recibidos en un mensaje de cola:  

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


Hola `Person` clase en este ejemplo no tiene tooimplement `ITableEntity`.

## <a id="storageapi"></a>¿Cómo toouse Hola API de almacenamiento de .NET directamente toowork con una tabla
También puede usar hello `Table` atribuir a un `CloudTable` objeto para una mayor flexibilidad cuando se trabaja con una tabla.

usos de ejemplo de código siguiente Hola un `CloudTable` objeto tooadd una sola entidad toohello *entrada* tabla. 

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

Para obtener más información acerca de cómo hello toouse `CloudTable` de objetos, consulte [cómo toouse almacenamiento de tablas de .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Temas relacionados cubiertos por las colas de hello cómo-tooarticle
Para obtener información acerca de cómo el procesamiento de tabla toohandle desencadenada por un mensaje de la cola, o de trabajos Web escenarios SDK no procesar, consulte específica tootable [cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Los temas tratados en dicho artículo Hola siguientes:

* Funciones asincrónicas
* Varias instancias
* Apagado correcto
* Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función
* Establecer las cadenas de conexión de SDK de hello en el código
* Establecer valores para los parámetros del constructor del SDK de WebJobs en el código
* Desencadenar una función manualmente
* Escribir registros

## <a id="nextsteps"></a> Pasos siguientes
Esta guía proporciona código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con tablas de Azure. Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [Azure trabajos Web recomienda recursos](http://go.microsoft.com/fwlink/?linkid=390226).

