---
title: "aaaUse contadores de rendimiento de diagnósticos de Azure | Documentos de Microsoft"
description: "Utilice los contadores de rendimiento en los servicios de nube de Azure o los cuellos de botella toofind de máquina virtual y optimizar el rendimiento."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Creación y uso de contadores de rendimiento en una aplicación de Azure
Este artículo describen las ventajas de Hola de y cómo los contadores de rendimiento de tooput en su aplicación de Azure. Puede usar datos toocollect, encontrar cuellos de botella y ajustar el rendimiento del sistema y de aplicación.

Contadores de rendimiento disponibles para Windows Server, IIS y ASP.NET también se pueden recopilar y utilizan mantenimiento de hello toodetermine de los roles web de Azure, roles de trabajo y máquinas virtuales. Además, puede crear y usar contadores de rendimiento personalizados.  

Puede examinar los datos del contador de rendimiento.

1. Directamente en el host de la aplicación hello con la herramienta Monitor de rendimiento de hello acceder mediante Escritorio remoto
2. Con el uso de System Center Operations Manager Hola el módulo de administración de Azure
3. Con otras herramientas de supervisión que tienen acceso a Hola datos de diagnóstico transfieren tooAzure almacenamiento. Consulte [Guardar y ver datos de diagnóstico en el almacenamiento de Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obtener más información.  

Para obtener más información acerca de cómo supervisar el rendimiento de saludo de la aplicación Hola [portal de Azure](http://portal.azure.com/), consulte [cómo los servicios de nube tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Para obtener instrucciones detalladas sobre cómo crear un registro y seguimiento de la estrategia y usar diagnósticos y otros problemas de tootroubleshoot técnicas adicionales y optimizar aplicaciones de Azure, consulte [prácticas recomendadas para el desarrollo de Azure Aplicaciones](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Habilitación de la supervisión de contadores de rendimiento
Los contadores de rendimiento no están habilitados de forma predeterminada. La aplicación o una tarea de inicio debe modificar diagnósticos de forma predeterminada Hola contadores de rendimiento de específicos de Hola de agente configuración tooinclude que desea toomonitor para cada instancia de rol.

### <a name="performance-counters-available-for-microsoft-azure"></a>Contadores de rendimiento disponibles para Microsoft Azure
Azure proporciona un subconjunto de los contadores de rendimiento de hello disponibles para Windows Server, IIS y Hola pila ASP.NET. Hello tabla siguiente enumeran algunos de los contadores de rendimiento de Hola de especial interés para las aplicaciones de Azure.

| Categoría de contador: Objeto (instancia) | Nombre del contador | Referencia |
| --- | --- | --- |
| Excepciones de .NET CLR (*Global*) |Nº de excepciones producidas por segundo |Contadores de rendimiento de excepciones |
| Memoria de .NET CLR (*Global*) |% de tiempo del GC |Contadores de rendimiento de memoria |
| ASP.NET |Reinicios de la aplicación |Contadores de rendimiento para ASP.NET |
| ASP.NET |Tiempo de ejecución de solicitud |Contadores de rendimiento para ASP.NET |
| ASP.NET |Solicitudes desconectadas |Contadores de rendimiento para ASP.NET |
| ASP.NET |Reinicios del proceso de trabajo |Contadores de rendimiento para ASP.NET |
| Aplicaciones ASP.NET(**Total**) |Total de solicitudes |Contadores de rendimiento para ASP.NET |
| Aplicaciones ASP.NET(**Total**) |Solicitudes por segundo |Contadores de rendimiento para ASP.NET |
| ASP.NET v4.0.30319 |Tiempo de ejecución de solicitud |Contadores de rendimiento para ASP.NET |
| ASP.NET v4.0.30319 |Tiempo de espera de la solicitud |Contadores de rendimiento para ASP.NET |
| ASP.NET v4.0.30319 |Solicitudes actuales |Contadores de rendimiento para ASP.NET |
| ASP.NET v4.0.30319 |Solicitudes en cola |Contadores de rendimiento para ASP.NET |
| ASP.NET v4.0.30319 |Solicitudes rechazadas |Contadores de rendimiento para ASP.NET |
| Memoria |MB disponibles |Contadores de rendimiento de memoria |
| Memoria |Bytes confirmados |Contadores de rendimiento de memoria |
| Processor(_Total) |% de tiempo de procesador |Contadores de rendimiento para ASP.NET |
| TCPv4 |Errores de conexión |Objeto TCP |
| TCPv4 |Conexiones establecidas |Objeto TCP |
| TCPv4 |Restablecimiento de conexiones |Objeto TCP |
| TCPv4 |Segmentos enviados por segundo |Objeto TCP |
| Interfaz de red(*) |Bytes recibidos por segundo |Objeto de interfaz de red |
| Interfaz de red(*) |Bytes enviados por segundo |Objeto de interfaz de red |
| Interfaz de red (Adaptador de red de bus de máquina virtual de Microsoft _2) |Bytes recibidos por segundo |Objeto de interfaz de red |
| Interfaz de red (Adaptador de red de bus de máquina virtual de Microsoft _2) |Bytes enviados por segundo |Objeto de interfaz de red |
| Interfaz de red (Adaptador de red de bus de máquina virtual de Microsoft _2) |Bytes totales por segundo |Objeto de interfaz de red |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Crear y agregar la aplicación de tooyour de contadores de rendimiento personalizados
Azure tiene toocreate de soporte técnico y modificar contadores de rendimiento personalizados para roles web y roles de trabajo. contadores de Hola pueden ser usado tootrack y monitor específica de la aplicación el comportamiento. Puede crear y eliminar categorías y especificadores de contadores de rendimiento personalizados desde una tarea de inicio, un rol web o un rol de trabajo con permisos elevados.

> [!NOTE]
> Código que realiza cambios en los contadores de rendimiento toocustom debe tener un elevado toorun de permisos. Si el código de hello está en un rol web o el rol de trabajo, rol Hola debe incluir la etiqueta hello <Runtime executionContext="elevated" /> Hola ServiceDefinition.csdef de archivos para hello rol tooinitialize correctamente.
>
>

Puede enviar rendimiento personalizados contador datos tooAzure almacenamiento mediante el agente de diagnóstico de Hola.

hello que Azure procesa genera datos de contador de rendimiento estándar de Hola. La aplicación para el rol web o de trabajo debe crear los datos de contadores de rendimiento personalizados. Vea [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) para obtener información sobre tipos de Hola de datos que pueden almacenarse en contadores de rendimiento personalizados. Consulte el [ejemplo PerformanceCounters](http://code.msdn.microsoft.com/azure/) para obtener un ejemplo que crea y establece datos de contadores de rendimiento personalizados en un rol web.

## <a name="store-and-view-performance-counter-data"></a>Almacenamiento y visualización de datos de contadores de rendimiento
Azure almacena en caché los datos de contadores de rendimiento junto con otra información de diagnóstico. Estos datos están disponibles para la supervisión remota mientras se está ejecutando la instancia de rol de hello con acceso de escritorio remoto tooview herramientas como el Monitor de rendimiento. toopersist Hola fuera de la instancia de rol de hello, agente de diagnóstico de hello debe transferencia de datos de almacenamiento de hello datos tooAzure. límite de tamaño de Hola de datos del contador de rendimiento de hello en caché se puede configurar en el agente de diagnóstico de hello, o puede ser configurado toobe parte de un límite compartido para todos los datos de diagnóstico de Hola. Para obtener más información acerca de cómo establecer el tamaño del búfer de hello, consulte [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) y [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). Vea [almacenar y ver datos de diagnóstico en almacenamiento de Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obtener información general de configuración de la cuenta de almacenamiento tooa de hello diagnósticos agente tootransfer datos.

Cada instancia de contador de rendimiento configurada se registra a una velocidad de muestreo especificada y se transfieren datos de hello muestreada toohello cuenta de almacenamiento mediante una solicitud de transferencia programada o una solicitud de transferencia a petición. Se pueden programar transferencias automáticas una vez por minuto. Datos del contador de rendimiento transferidos por el agente de diagnóstico de Hola se almacenan en una tabla, WADPerformanceCountersTable, en la cuenta de almacenamiento de Hola. Se puede acceder a esta tabla y se puede consultar con métodos de API de Almacenamiento de Azure estándar. Vea [ejemplo de PerformanceCounters de Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) para obtener un ejemplo de consulta y mostrar los datos del contador de rendimiento de la tabla de WADPerformanceCountersTable Hola.

> [!NOTE]
> Dependiendo de la frecuencia de transferencia de agente de diagnóstico de Hola y latencia de la cola, hello datos de contadores de rendimiento más reciente en la cuenta de almacenamiento de hello pueden ser obsoletos varios minutos.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Habilitación de contadores de rendimiento mediante el archivo de configuración de diagnóstico
Usar hello siguiendo los contadores de rendimiento de tooenable del procedimiento en su aplicación de Azure.

## <a name="prerequisites"></a>Requisitos previos
En esta sección se da por supuesto que se haya importado el monitor de diagnóstico de hello en la aplicación y que se han agregado Hola diagnósticos configuración archivo tooyour solución de Visual Studio (diagnostics.wadcfg en SDK 2.4 y por debajo o diagnostics.wadcfgx en SDK 2.5 y versiones posteriores). Consulte los pasos 1 y 2 en [Habilitación de diagnósticos en Azure Cloud Services y en Virtual Machines](cloud-services-dotnet-diagnostics.md)para más información.

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>Paso 1: Recopilación y almacenamiento de datos de contadores de rendimiento
Después de haber agregado diagnósticos Hola archivo tooyour solución de Visual Studio, puede configurar la recopilación de Hola y el almacenamiento de datos del contador de rendimiento en una aplicación de Azure. Esto se realiza mediante la adición de archivo de diagnóstico de toohello de contadores de rendimiento. Datos de diagnóstico, incluidos los contadores de rendimiento, se recopilan primero en la instancia de Hola. datos de Hello están persistente toohello WADPerformanceCountersTable tabla Hola servicio tabla de Azure, por lo que tendrá que también necesita toospecify Hola cuenta de almacenamiento en la aplicación. Si va a probar la aplicación localmente en hello emulador de proceso, también puede almacenar datos de diagnóstico localmente en hello emulador de almacenamiento. Antes de almacenar datos de diagnóstico, debe ir primero toohello [portal de Azure](http://portal.azure.com/) y crear una cuenta de almacenamiento clásico. Una práctica recomendada es toolocate su cuenta de almacenamiento en Hola la misma ubicación geográfica que la aplicación de Azure. Por mantener Hola cuenta de aplicación y el almacenamiento de Azure están en Hola misma ubicación geográfica, evitar pagar costos externos de ancho de banda y reducir la latencia.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Agregar archivo de diagnóstico de toohello de contadores de rendimiento
Hay muchos contadores que puede usar. Hello en el ejemplo siguiente se muestra varios contadores de rendimiento que se recomiendan para web y la supervisión del rol de trabajo.

Abrir el archivo de diagnóstico de hello (diagnostics.wadcfg en SDK 2.4 y anteriores o diagnostics.wadcfgx en SDK 2.5 y versiones posteriores) y agregue Hola siguiente toohello DiagnosticMonitorConfiguration elemento:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

atributo de bufferQuotaInMB Hello, que especifica la cantidad máxima de Hola de almacenamiento del sistema de archivos que está disponible para el tipo de colección de datos de hello (registros de Azure, los registros de IIS, etcetera). Hola predeterminado es 0. Cuando se alcanza la cuota de hello, se eliminan datos más antiguos de Hola a medida que se agregan nuevos datos. suma de Hola de todas las propiedades de hello bufferQuotaInMB debe ser mayor que valor Hola del atributo de OverallQuotaInMB Hola. Para obtener una explicación más detallada de determinar la cantidad de almacenamiento que se necesitará para Hola de recopilación de datos de diagnóstico, vea Hola sección de instalación de WAD de [prácticas recomendadas para desarrollar aplicaciones de Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

atributo de scheduledTransferPeriod Hello, que especifica el intervalo de saludo entre las transferencias programadas de datos, se redondea hacia arriba toohello más cercano de minuto. Hola en los ejemplos siguientes, se establece tooPT30M (30 minutos). Hola transferencia tooa período pequeño valor de configuración, como 1 minuto, afectará negativamente al rendimiento de su aplicación en producción, pero puede ser útil para ver los diagnósticos rápidamente cuando se prueban. período de transferencia programada de Hello debe ser lo suficientemente pequeño como tooensure que los datos de diagnóstico no se sobrescribe en la instancia de hello, pero lo suficientemente grande como para que no afectará al rendimiento de saludo de la aplicación.

atributo de Hello counterSpecifier especifica toocollect de contador de rendimiento de Hola. atributo de Hello sampleRate especifica tasa de hello en el que el contador de rendimiento de hello debe realizarse el muestreo, en este caso 30 segundos.

Cuando haya agregado los contadores de rendimiento de Hola que desea toocollect, guarde el archivo de diagnóstico de toohello de cambios. A continuación, debe cuenta de almacenamiento de hello toospecify que se almacenarán los datos de diagnóstico de saludo.

### <a name="specify-hello-storage-account"></a>Especifique la cuenta de almacenamiento de Hola
toopersist su tooyour de información de diagnóstico almacenamiento de Azure de la cuenta, debe especificar una cadena de conexión en el archivo de configuración (ServiceConfiguration.cscfg) de servicio.

Para Azure SDK 2.5, puede especificarse Hola cuenta de almacenamiento en archivo de hello diagnostics.wadcfgx.

> [!NOTE]
> Estas instrucciones aplican solo tooAzure SDK 2.4 y versiones anteriores. Para Azure SDK 2.5, puede especificarse Hola cuenta de almacenamiento en archivo de hello diagnostics.wadcfgx.
>
>

cadenas de conexión de Hola tooset:

1. Abra el archivo de ServiceConfiguration.Cloud.cscfg de Hola con su editor de texto que prefiera y la cadena de conexión de Hola de conjunto para el almacenamiento. Hola *AccountName* y *AccountKey* valores se encuentran en hello portal de Azure en el panel de cuenta de almacenamiento de hello, bajo las teclas de acceso.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Guarde el archivo de ServiceConfiguration.Cloud.cscfg Hola.
3. Abra el archivo ServiceConfiguration.Local.cscfg de hello y compruebe que UseDevelopmentStorage esté establecido tootrue.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Ahora que se establecen las cadenas de conexión de hello, la aplicación conservará la cuenta de almacenamiento de tooyour de datos de diagnóstico cuando se implementa la aplicación.
4. Guarde y compile el proyecto y, a continuación, implemente la aplicación.

## <a name="step-2-optional-create-custom-performance-counters"></a>Paso 2 (opcional): Creación de contadores de rendimiento personalizados
Además toohello había definido previamente los contadores de rendimiento, puede agregar que su propio rendimiento personalizados contadores toomonitor roles de web o de trabajo. Contadores de rendimiento personalizados pueden comportamientos de específica de la aplicación tootrack y monitor de uso y se puede crear o eliminar en una tarea de inicio, el rol web o el rol de trabajo con permisos elevados.

agente de diagnóstico de Azure Hola actualiza Hola configuración contador de rendimiento desde el archivo .wadcfg de hello un minuto después de iniciar.  Si debe crear contadores de rendimiento personalizados en hello OnStart (método) y sus tareas de inicio tarden más de un minuto tooexecute, los contadores de rendimiento personalizados no se habrá creados cuando trate de agente de diagnóstico de Azure de hello tooload ellos.  En este escenario, verá que Azure Diagnostics captura correctamente todos los datos de diagnóstico, excepto los contadores de rendimiento personalizados.  tooresolve este problema, cree Hola contadores de rendimiento en una tarea de inicio o mover algunas de la tarea de inicio funcionan toohello OnStart (método) después de crear contadores de rendimiento de Hola.

Lleve a cabo Hola siguiendo los pasos toocreate un rendimiento personalizado simple contador denominado "\MyCustomCounterCategory\MyButton1Counter":

1. Abra el archivo de definición de servicio de hello (CSDEF) para la aplicación.
2. Agregue Hola elemento toohello WebRole o WorkerRole elemento tooallow ejecución con privilegios elevados:

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Guarde el archivo hello.
4. Abrir el archivo de diagnóstico de hello (diagnostics.wadcfg en SDK 2.4 y anteriores o diagnostics.wadcfgx en SDK 2.5 y versiones posteriores) y agregue Hola después toohello DiagnosticMonitorConfiguration

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Guarde el archivo hello.
6. Crear categoría de contador de rendimiento personalizados de hello en hello OnStart (método) de su rol, antes de invocar base. OnStart. Hello ejemplo C# siguiente crea una categoría personalizada, si aún no existe:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Actualizar los contadores de hello dentro de la aplicación. Hola de ejemplo siguiente actualiza un contador de rendimiento personalizado en eventos Button1_Click:

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Guarde el archivo hello.  

Monitor de diagnóstico de Azure de hello ahora recopilará datos de contador de rendimiento personalizados.

## <a name="step-3-query-performance-counter-data"></a>Paso 3: Consulta de datos de contadores de rendimiento
Una vez que la aplicación se implementa y ejecuta, se iniciará el monitor de diagnóstico de hello recopilar contadores de rendimiento y conservar ese almacenamiento tooAzure de datos. Usar herramientas como el Explorador de servidores en Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), o [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) de Cerebrata tooview Hola contadores de rendimiento de datos en hello Tabla WADPerformanceCountersTable. Puede consultar mediante programación Hola tabla servicio mediante [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), o [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Hola siguiente ejemplo de C# muestra una consulta básica contra la tabla de WADPerformanceCountersTable Hola y guarda el archivo CSV tooa de hello diagnósticos datos. Una vez que los contadores de rendimiento de Hola se guardan el archivo CSV de tooa, puede usar Hola capacidades de Microsoft Excel o algún otro dato de hello toovisualize de herramienta de creación de gráficos. Ser seguro tooadd un tooMicrosoft.WindowsAzure.Storage.dll de referencia, que se incluye en hello Azure SDK para .NET de octubre de 2012 y versiones posterior. ensamblado de Hello es directorio de programa Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ % toohello instalado.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

Las entidades asignan objetos tooC # mediante una clase personalizada derivada de **TableEntity**. Hello código siguiente define una clase de entidad que representa un contador de rendimiento en hello **WADPerformanceCountersTable** tabla.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Pasos siguientes
[Ver más artículos sobre Diagnósticos de Azure](../azure-diagnostics.md)
