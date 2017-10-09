---
title: Servicios de Service Fabric aaaPartitioning | Documentos de Microsoft
description: "Describe cómo servicios con estado de toopartition Service Fabric. Las particiones permite el almacenamiento de datos en equipos locales de Hola para que datos y el cálculo pueden escalarse juntas."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>Partición de Reliable Services de Service Fabric
Este artículo proporciona una introducción toohello conceptos básicos de creación de particiones de servicios de Azure Service Fabric confiables. Hello código fuente utilizada en el artículo hello también está disponible en [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="partitioning"></a>Creación de particiones
La partición no es único tooService tejido. De hecho, es una función básica de la compilación de servicios escalables. En un sentido más amplio, podemos pensar acerca de la partición como un concepto de dividir el estado (datos) y de proceso en el rendimiento y la escalabilidad de tooimprove accesible unidades más pequeña. Una forma conocida de partición es la [partición de datos][wikipartition] también conocida como particionamiento.

### <a name="partition-service-fabric-stateless-services"></a>Partición de los servicios sin estado de Service Fabric
Para los servicios sin estado, puede pensar en una partición como en una unidad lógica que contiene una o varias instancias de un servicio. La ilustración 1 muestra un servicio sin estado con cinco instancias distribuidas en un clúster con una partición.

![Servicio sin estado](./media/service-fabric-concepts-partitioning/statelessinstances.png)

En realidad hay dos tipos de soluciones de servicios sin estado. Hello primero uno es un servicio que conserva su estado externamente, por ejemplo en una base de datos de SQL Azure (por ejemplo, un sitio Web que almacena la información de sesión de Hola y de datos). Hello segunda es servicios solo de cálculo (por ejemplo, una miniatura calculadora o imagen) que no se administran cualquier estado persistente.

En cualquier caso, la partición de un servicio sin estado es un escenarios muy poco frecuente en el que la escalabilidad y la disponibilidad normalmente se consiguen agregando más instancias. las solicitudes de tiempo única de Hola que desea tooconsider varias particiones para las instancias de servicio sin estado es cuando se necesita toomeet especial enrutamiento.

Por ejemplo, piense en un caso en el que los usuarios con identificadores dentro de un intervalo específico deberán ser atendidos únicamente por una instancia de servicio determinada. Otro ejemplo de cuándo puede dividir un servicio sin estado es cuando tiene un backend realmente con particiones (por ejemplo, una base de datos SQL particionada) y desea toocontrol qué instancia de servicio debe escribir la partición de la base de datos de toohello--o realizar otro trabajo de preparación en Hello servicio sin estado que requiere Hola misma partición información tal como se utiliza en hello back-end. Estos tipos de escenarios también se pueden resolver de maneras diferentes y no requieren necesariamente el particionamiento del servicio.

Hola resto de este tutorial se centra en los servicios con estado.

### <a name="partition-service-fabric-stateful-services"></a>Partición de los servicios con estado de Service Fabric
Service Fabric resulta fácil toodevelop servicios con estado escalables, ya que ofrece una manera de primera clase toopartition estado (datos). Conceptualmente, puede pensar en una partición de un servicio con estado como una unidad de escala es altamente confiable a través de [réplicas](service-fabric-availability-services.md) que se distribuyen y están equilibrados en los nodos de hello en un clúster.

Creación de particiones en el contexto de hello de servicios con estado de Service Fabric hace referencia toohello proceso de determinar que una partición de servicio en particular es responsable de una parte de todo el estado del servicio de Hola Hola. (Como se mencionó anteriormente, una partición es un conjunto de [réplicas](service-fabric-availability-services.md)). Una gran ventaja de Service Fabric es que vuelve a realizar particiones de hello en nodos diferentes. Esto les permite límite de recursos del nodo de toogrow tooa. Como datos de hello crezca, particiones crecen y Service Fabric vuelve a equilibrar las particiones entre nodos. Esto garantiza Hola sigue un uso eficaz de los recursos de hardware.

toogive, por ejemplo, suponga empiezan por un clúster de 5 nodos y un servicio que esté configurado toohave 10 particiones y un destino de tres réplicas. En este caso, Service Fabric debería equilibrar y distribuir las réplicas de hello en el clúster de hello--y acabarías con dos principal [réplicas](service-fabric-availability-services.md) por nodo.
Si necesita ahora tooscale out too10 nodos del clúster de hello, Service Fabric haría reequilibrar Hola principal [réplicas](service-fabric-availability-services.md) en todos los nodos de 10. Del mismo modo, si ajusta el tamaño de nodos too5 atrás, Service Fabric haría reequilibrar todas las réplicas de hello en todos los nodos de hello 5.  

Figura 2 muestra la distribución de Hola de 10 particiones antes y después del ajuste de escala en clúster de Hola.

![Servicio con estado](./media/service-fabric-concepts-partitioning/partitions.png)

Como resultado, se consigue Hola escalabilidad desde las solicitudes de los clientes se distribuyen en varios equipos, se mejora el rendimiento general de la aplicación hello y se reduce la contención de toochunks de acceso de datos.

## <a name="plan-for-partitioning"></a>Plan para la creación de particiones
Antes de implementar un servicio, debe considerar siempre Hola estrategia que sea necesario tooscale fuera de partición. Hay diferentes maneras, pero todos ellos se centran en la aplicación hello necesita tooachieve. Para el contexto de Hola de este artículo, veamos algunos de hello aspectos más importantes.

Un buen enfoque es toothink acerca de la estructura de hello del estado de Hola que necesita toobe particiones, como primer paso de Hola.

Veamos un sencillo ejemplo. Si fuera un servicio para un sondeo countywide toobuild, podría crear una partición para cada ciudad de condado de Hola. A continuación, podría almacenar Hola votos para todas las personas en Ciudad hello en partición de hello correspondiente toothat ciudad. Figura 3 muestra un conjunto de ciudad hello y personas en las que residen.

![Partición simple](./media/service-fabric-concepts-partitioning/cities.png)

Como el rellenado de Hola de ciudades varía en gran medida, puede acabar con algunas particiones que contienen una gran cantidad de datos (p. ej., Seattle) y otras particiones con muy poco estado (p. ej., Kirkland). ¿Cuál es el impacto de Hola de tener particiones con cantidades desiguales de estado?

Si piensa volver a hello (ejemplo), puede ver fácilmente que la partición de Hola que contiene Hola los votos de Seattle obtendrá más tráfico que Kirkland Hola uno. De forma predeterminada, Service Fabric se asegura de que hay sobre Hola mismo número de réplicas principales y secundarias en cada nodo. Por lo que puede encontrarse con nodos que contienen réplicas que atienden más tráfico y otros que atienden de menos tráfico. Preferiblemente desearía tooavoid activa y las zonas frío similar a éste en un clúster.

En orden tooavoid esto, debe hacer dos cosas, desde un punto de vista partición:

* Pruebe a estado de hello toopartition para que se distribuyen uniformemente en todas las particiones.
* Carga de informes de cada una de las réplicas de hello para el servicio de Hola. (Para más información al respecto, consulte este artículo sobre [métricas y carga](service-fabric-cluster-resource-manager-metrics.md)). Service Fabric proporciona carga tooreport Hola capacidad que consumen los servicios, como la cantidad de memoria o el número de registros de. Según las métricas de hello notificadas, Service Fabric detecta los que algunas particiones trabajan cargas mayores que otros y vuelve a equilibrar clúster Hola móvil réplicas toomore adecuado nodos, por lo que en general no está sobrecargado ningún nodo.

A veces, no es posible saber la cantidad de datos que habrá en una partición determinada. Por lo que una recomendación general es toodo ambos: en primer lugar, mediante el uso de una estrategia de particiones Reparta los Hola datos uniformemente entre las particiones de hello y, después, por carga informes.  primer método de Hello evita situaciones descritas en hello votos de ejemplo, hello en segundo lugar contribuye a suavizar las diferencias temporales en access o carga con el tiempo.

Otro aspecto de la planeación de la partición es el número correcto de hello toochoose de toobegin de particiones con.
Desde la perspectiva de Service Fabric, nada le impide comenzar con un número de particiones mayor del previsto para su escenario.
De hecho, suponiendo que el número máximo de Hola de particiones es un enfoque válido.

En raras ocasiones puede acabar necesitando más particiones que las elegidas inicialmente. Como no se puede cambiar el recuento de particiones de hello después hechos hello, necesitaría tooapply algunos enfoques de partición avanzadas, como la creación de una nueva instancia de servicio del programa Hola a mismo tipo de servicio. También necesitaría tooimplement alguna lógica de cliente que enruta Hola solicita toohello: instancia de servicio correcto, según el conocimiento de cliente que debe mantener el código de cliente.

Otra consideración de planificación de la creación de particiones es recursos de los equipos disponibles Hola. Como estado de hello debe toobe al acceso y almacenamiento, son toofollow dependiente:

* Límites del ancho de banda de red
* Límites de la memoria del sistema
* Límites del almacenamiento en disco

Por lo tanto, ¿qué ocurre si se ejecuta en las restricciones de recursos en un clúster de ejecución? respuesta de Hello es que simplemente puede escalar horizontalmente nuevos requisitos de hello clúster tooaccommodate Hola.

[Guía de planificación de capacidad de Hello](service-fabric-capacity-planning.md) se ofrecen consejos sobre cómo toodetermine cuántos nodos que necesita el clúster.

## <a name="get-started-with-partitioning"></a>Introducción a la creación de particiones
Esta sección describe cómo tooget a trabajar con el servicio de creación de particiones.

En primer lugar, Service Fabric ofrece tres esquemas de partición posibles:

* Particiones de intervalo (también conocidas como UniformInt64Partition)
* Particiones con nombre. Las aplicaciones que usan este modelo suelen tener datos que se pueden incluir en cubos, dentro de un conjunto enlazado. Algunos ejemplos habituales de campos de datos que se usan como claves de partición con nombre son regiones, códigos postales, grupos de clientes u otros límites empresariales.
* Particiones de singleton. Particiones de singleton se usan normalmente cuando el servicio de hello no requiere ningún enrutamiento adicional. Por ejemplo, los servicios sin estado usan este esquema de partición de forma predeterminada.

Los esquemas de particiones con nombre y de singleton son formas especiales de particiones de intervalos. De forma predeterminada, plantillas de Visual Studio de Hola para su uso de Service Fabric un rango particiones, ya que es Hola uno más habitual y útil. resto de Hola de este artículo se centra en el esquema de partición rango Hola.

### <a name="ranged-partitioning-scheme"></a>Esquema de particiones de intervalo
Se trata de toospecify usa un entero intervalo (identificadas mediante una clave baja y clave superior) y un número de particiones (n). Crea particiones de n, uno de ellos responsables un subintervalo no superpuestos de hello general rangos con clave de partición. Por ejemplo: un esquema de partición de intervalo con una clave baja 0, una clave alta de 99 y un recuento de 4 crearía 4 particiones, tal y como se muestra a continuación.

![Creación de particiones por rangos](./media/service-fabric-concepts-partitioning/range-partitioning.png)

Un enfoque común es toocreate un hash basado en una clave única en el conjunto de datos de Hola. Algunos ejemplos comunes de claves son un número de identificación de vehículo (VIN), identificación de empleado o una cadena única. Mediante el uso de esta clave única, a continuación, podría generar un código hash, intervalo de claves de módulo hello, toouse como su clave. Puede especificar Hola superior e inferior de hello clave intervalo permitido.

### <a name="select-a-hash-algorithm"></a>Selección de un algoritmo hash
Una parte importante de los algoritmos hash es seleccionar su algoritmo hash. Debe tener en cuenta es si el objetivo de hello toogroup claves similar cerca entre sí (hash confidencial localidad)--o si la actividad debe distribuirse ampliamente en todas las particiones (hash de distribución), lo que es más común.

características de Hola de un algoritmo hash de distribución óptimas son que resulta fácil toocompute, tiene algunas de las colisiones y se distribuye uniformemente las claves de Hola. Un buen ejemplo de un algoritmo hash eficaz es hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algoritmo hash.

Un buen recurso para opciones de algoritmo de código hash general es hello [página de Wikipedia en las funciones de hash](http://en.wikipedia.org/wiki/Hash_function).

## <a name="build-a-stateful-service-with-multiple-partitions"></a>Creación de un servicio con estado con varias particiones
Vamos a crear su primer servicio con estado confiable con varias particiones. En este ejemplo, va a compilar una aplicación muy simple en el que desea toostore todos los apellidos que comienzan con hello en Hola de letra misma partición.

Antes de escribir ningún código, debe toothink acerca de las particiones de Hola y las claves de partición. Necesita 26 particiones (uno para cada letra del alfabeto hello), pero ¿qué pasa sobre Hola claves alta y bajas?
Puesto que queremos literalmente toohave una partición por letra, podemos usar 0 como clave baja de Hola y 25 como clave alta de hello, como cada letra es su propia clave.

> [!NOTE]
> Se trata de un escenario simplificado, ya que en realidad distribución Hola sería desigual. Apellidos que empiezan con las letras de hello "S" o "M" son más comunes que Hola que empiezan por "X" o "Y".
> 
> 

1. Abra **Visual Studio** > **Archivo** > **Nuevo** > **Proyecto**.
2. Hola **nuevo proyecto** diálogo cuadro, seleccione la aplicación de Service Fabric hello.
3. Llame al proyecto de Hola "AlphabetPartitions".
4. Hola **crear un servicio** diálogo cuadro, elija **Stateful** de servicio y llámelo "Alphabet.Processing" como se muestra en la imagen de hello siguiente.
       ![Cuadro de diálogo de servicio nuevo en Visual Studio][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Establecer número de Hola de particiones. Archivo de Applicationmanifest.xml de hello abierto encuentra en hello ApplicationPackageRoot carpeta de hello AlphabetPartitions proyecto y actualice parámetro hello Processing_PartitionCount too26 tal y como se muestra a continuación.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    También necesitará hello tooupdate LowKey y HighKey propiedades del elemento de StatefulService Hola Hola ApplicationManifest.xml tal y como se muestra a continuación.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Para el servicio de hello toobe accesible, abrir un extremo en un puerto mediante la adición de elemento de punto de conexión de Hola de ServiceManifest.xml (que se encuentra en la carpeta de PackageRoot hello) para hello Alphabet.Processing servicio tal y como se muestra a continuación:
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    Ahora servicio hello es toolisten configurado tooan extremo interno con 26 particiones.
7. A continuación, debe toooverride hello `CreateServiceReplicaListeners()` método de clase de procesamiento de Hola.
   
   > [!NOTE]
   > Para este ejemplo, asumimos que está usando un HttpCommunicationListener simple. Para obtener más información sobre la comunicación del servicio confiable, vea [modelo de comunicación de un servicio confiable de hello](service-fabric-reliable-services-communication.md).
   > 
   > 
8. Un patrón recomendado para URL de Hola que escucha una réplica es hello siguiendo el formato: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.
    Por lo que desee tooconfigure su toolisten de agente de escucha de comunicación en los puntos de conexión correcto de Hola y con este patrón.
   
    Varias réplicas de este servicio pueden estar hospedadas en hello mismo equipo, por lo que esta dirección debe toobe toohello única réplica. Esta es la razón por Id. de partición + Id. de réplica en la dirección URL de Hola. HttpListener puede escuchar en varias direcciones en hello que mismo número de puerto como prefijo de dirección URL de hello es único.
   
    Hola que GUID adicional es por un caso avanzado donde las réplicas secundarias también escuchan las solicitudes de solo lectura. Una vez que el caso de hello, desea toomake seguro de que una nueva dirección única se utiliza al realizar la transición desde la dirección de toosecondary principal tooforce clientes toore resolución Hola. '+' se utiliza como dirección de hello aquí para que hello réplica escucha en el código de hello con todos los hosts disponibles (IP, FQDM, localhost, etc.) a continuación muestra un ejemplo.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    También merece la pena mencionar que Hola publicado direcciones URL es ligeramente diferente de prefijo de dirección URL de escucha de Hola.
    dirección URL de escucha de Hello tiene tooHttpListener. Hola que dirección URL publicada es dirección URL de Hola que está publicada toohello tejido nomenclatura servicio, que se usa para la detección de servicios. Los clientes preguntarán por esta dirección mediante ese servicio de detección. dirección de Hola que los clientes tengan necesidades toohave Hola real IP o FQDN del nodo de hello en orden tooconnect. Por lo que necesita tooreplace '+' con Hola del nodo IP o FQDN tal como se muestra arriba.
9. Hola último paso es hello tooadd lógica toohello servicio tal y como se muestra a continuación de procesamiento.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`lecturas Hola valores de hello consulta cadena parámetro utilizado toocall Hola partición y las llamadas `AddUserAsync` diccionario confiable de tooadd Hola lastname toohello `dictionary`.
10. Vamos a agregar un toosee de proyecto de servicio sin estado toohello cómo puede llamar a una partición determinada.
    
    Este servicio actúa como una sencilla interfaz web que acepta Hola lastname como un parámetro de cadena de consulta, determina la clave de partición de Hola y lo envía toohello Alphabet.Processing servicio para su procesamiento.
11. Hola **crear un servicio** diálogo cuadro, elija **Stateless** de servicio y llámelo "Alphabet.Web", tal y como se muestra a continuación.
    
    ![Captura de pantalla de servicio sin estado](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. Actualizar la información de punto de conexión de hello en hello ServiceManifest.xml de hello Alphabet.WebApi servicio tooopen un puerto tal y como se muestra a continuación.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. Debe tooreturn una colección de ServiceInstanceListeners en la clase de hello Web. De nuevo, puede elegir tooimplement un HttpCommunicationListener simple.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. Ahora necesita lógica de procesamiento de tooimplement Hola. Hola HttpCommunicationListener llamadas `ProcessInputRequest` cuando llega una solicitud. Por lo que sigamos adelante y agregar código de hello siguiente.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    Le guiaremos paso a paso. código de Hello lee la primera letra de Hola de parámetro de cadena de consulta de hello `lastname` en un valor char. A continuación, determina clave de partición de Hola para esta letra restando el valor hexadecimal de Hola de `A` de valor hexadecimal de saludo de la primera letra de hello apellidos.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    Recuerde que, en este ejemplo, usamos 26 particiones con una clave de partición por partición.
    A continuación, obtenemos la partición de servicio de hello `partition` para esta clave mediante el uso de hello `ResolveAsync` método en hello `servicePartitionResolver` objeto. `servicePartitionResolver` se define como
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    Hola `ResolveAsync` método toma Hola servicio URI, clave de partición de Hola y un token de cancelación como parámetros. Hola URI del servicio de servicio de procesamiento de hello es `fabric:/AlphabetPartitions/Processing`. A continuación, obtenemos el punto de conexión de Hola de partición de Hola.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    Por último, se compilación dirección URL del extremo de Hola y Hola querystring y llamar al servicio de procesamiento de Hola.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    Una vez que se realiza el procesamiento de hello, se escribe un resultado Hola atrás.
15. Hola último paso es servicio de hello tootest. Visual Studio usa parámetros de aplicación para la implementación local y de nube. servicio de hello tootest con 26 particiones localmente, necesita tooupdate hello `Local.xml` archivos en la carpeta de ApplicationParameters de hello del proyecto de hello AlphabetPartitions tal y como se muestra a continuación:
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. Después de finalizar la implementación, puede comprobar el servicio de Hola y todas sus particiones de hello Service Fabric Explorer.
    
    ![Captura de pantalla del Explorador de Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. En un explorador, puede probar Hola partición lógica escribiendo `http://localhost:8081/?lastname=somename`. Verá que cada nombre de la última que se inicia con la misma letra se esté almacenando en Hola de Hola misma partición.
    
    ![Captura de pantalla de explorador](./media/service-fabric-concepts-partitioning/samplerunning.png)

Hola todo código de ejemplo de Hola está disponible en [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="next-steps"></a>Pasos siguientes
Para obtener información sobre conceptos de Service Fabric, vea Hola siguiente:

* [Disponibilidad de los servicios de Service Fabric](service-fabric-availability-services.md)
* [Escalabilidad de servicios de Service Fabric](service-fabric-concepts-scalability.md)
* [Planeación de la capacidad para las aplicaciones de Service Fabric](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png