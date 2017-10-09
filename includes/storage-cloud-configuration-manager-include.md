<span data-ttu-id="956df-101">Hola [biblioteca de Configuration Manager de Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) proporciona una clase para analizar una cadena de conexión desde un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="956df-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="956df-102">Hola [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) clase analiza los valores de configuración, independientemente de si está ejecutando la aplicación de cliente de hello en escritorio hello, en un dispositivo móvil, en una máquina virtual de Azure, o en un servicio de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="956df-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="956df-103">tooreference Hola CloudConfigurationManager paquete, agregue los siguientes hello `using` directiva:</span><span class="sxs-lookup"><span data-stu-id="956df-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="956df-104">Este es un ejemplo que muestra cómo tooretrieve una cadena de conexión desde un archivo de configuración:</span><span class="sxs-lookup"><span data-stu-id="956df-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="956df-105">Uso de hello Azure Configuration Manager es opcional.</span><span class="sxs-lookup"><span data-stu-id="956df-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="956df-106">También puede utilizar una API como Hola .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) clase.</span><span class="sxs-lookup"><span data-stu-id="956df-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

