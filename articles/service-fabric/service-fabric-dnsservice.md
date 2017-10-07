---
title: aaaAzure servicio DNS de tejido de servicio | Documentos de Microsoft
description: "Usar servicio de dns del tejido de servicio para detectar microservicios desde dentro de clúster de Hola."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a>Servicio DNS en Azure Service Fabric
Hola servicio DNS es un servicio de sistema opcional que se puede habilitar en el clúster toodiscover otros servicios que utilicen el protocolo DNS Hola.

Muchos servicios, especialmente en los servicios en contenedores, pueden tener un nombre de dirección URL existente y que se va a tooresolve capaz de ellos mediante el protocolo DNS estándar hello (en lugar del protocolo de servicio de nomenclatura de hello) es deseable, especialmente en escenarios "Levantar y mover". Hola servicio DNS permite toomap DNS nombres tooa nombre del servicio y, por tanto, resolver direcciones IP del extremo. 

Hola servicio DNS asigna nombres de tooservice de nombres DNS, que a su vez se resuelven al extremo de servicio de hello Naming Service tooreturn Hola. nombre DNS de Hello para el servicio de Hola se proporciona en tiempo de Hola de creación. 

![puntos de conexión de servicio][0]

## <a name="enabling-hello-dns-service"></a>Habilitar el servicio DNS de Hola
En primer lugar debe servicio DNS de tooenable hello en el clúster. Obtener plantilla hello para el clúster de Hola que desea toodeploy. Puede cualquier Hola uso [plantillas de ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) o crear una plantilla de administrador de recursos. Puede habilitar el servicio DNS Hola con hello pasos:

1. Compruebe que hello `apiversion` se establece demasiado`2017-07-01-preview` para hello `Microsoft.ServiceFabric/clusters` recurso y si no es así, actualizarla como se muestra en el siguiente fragmento de código de hello:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Ahora habilitar el servicio DNS Hola agregando Hola siguientes `addonFeatures` sección tras hello `fabricSettings` sección tal y como se muestra en el siguiente fragmento de código de hello: 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. Una vez que se ha actualizado la plantilla de clúster con hello anterior cambios, aplicarlos y deje que Hola actualización completada. Una vez completado, Hola servicio del sistema DNS comienza a ejecutarse en el clúster que se denomina `fabric:/System/DnsService` en la sección de servicio de sistema en el Explorador de Service Fabric Hola. 

Como alternativa, puede habilitar Hola servicio DNS a través del portal de hello en tiempo de Hola de creación del clúster. Hola servicio DNS puede habilitarse al activar casilla de Hola para `Include DNS service` en hello `Cluster configuration` menú tal y como se muestra en la siguiente captura de pantalla de hello:

![Habilitar el servicio DNS a través del portal de Hola][2]


## <a name="setting-hello-dns-name-for-your-service"></a>Nombre DNS de hello para el servicio de configuración
Una vez Hola servicio DNS se ejecuta en el clúster, puede establecer un nombre DNS para los servicios mediante declaración para los servicios predeterminados en hello `ApplicationManifest.xml` o mediante comandos de Powershell.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Establecer nombre DNS de Hola para un servicio de manera predeterminada en hello ApplicationManifest.xml
Abra el proyecto en Visual Studio, o su editor favorito y hello `ApplicationManifest.xml` archivo. Vaya toohello sección de servicios de manera predeterminada y para cada Hola de complemento de servicio `ServiceDnsName` atributo. Hola de ejemplo siguiente muestra cómo tooset Hola nombre DNS del servicio de hello demasiado`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Una vez que se implementa la aplicación hello, instancia de servicio de hello en el Explorador de Service Fabric hello muestra el nombre DNS de Hola para esta instancia, tal y como se muestra en la figura siguiente de Hola: 

![puntos de conexión de servicio][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Establecer nombre DNS de Hola para un servicio con Powershell
Puede establecer nombre DNS de Hola para un servicio cuando se crea mediante hello `New-ServiceFabricService` Powershell. Hello en el ejemplo siguiente se crea un nuevo servicio sin estado con nombre DNS de Hola`service1.application1`

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a>Uso de DNS en los servicios
Si implementa más de un servicio, puede encontrar puntos de conexión de Hola de otro toocommunicate servicios con mediante un nombre DNS. Hola servicio DNS solo es aplicable toostateless servicios, ya que Hola protocolo DNS no puede comunicarse con servicios con estado. Para los servicios con estado, puede utilizar a proxy inverso integrados de Hola para http llamadas toocall una partición de servicio determinado.

Hello código siguiente muestra cómo toocall otro servicio, que es simplemente un http regular llamar a donde se debe proporcionar un puerto de Hola y cualquier ruta de acceso opcional como parte de la dirección URL de Hola.

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
Más información acerca de la comunicación de servicio en clúster de hello con [conectarse y comunicarse con los servicios](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
