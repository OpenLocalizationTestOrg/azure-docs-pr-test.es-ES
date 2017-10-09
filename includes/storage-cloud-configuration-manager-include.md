Hola [biblioteca de Configuration Manager de Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) proporciona una clase para analizar una cadena de conexión desde un archivo de configuración. Hola [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) clase analiza los valores de configuración, independientemente de si está ejecutando la aplicación de cliente de hello en escritorio hello, en un dispositivo móvil, en una máquina virtual de Azure, o en un servicio de nube de Azure.

tooreference Hola CloudConfigurationManager paquete, agregue los siguientes hello `using` directiva:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Este es un ejemplo que muestra cómo tooretrieve una cadena de conexión desde un archivo de configuración:

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

Uso de hello Azure Configuration Manager es opcional. También puede utilizar una API como Hola .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) clase.

