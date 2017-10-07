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
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="f2c60-103">Servicio DNS en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f2c60-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="f2c60-104">Hola servicio DNS es un servicio de sistema opcional que se puede habilitar en el clúster toodiscover otros servicios que utilicen el protocolo DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="f2c60-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="f2c60-105">Muchos servicios, especialmente en los servicios en contenedores, pueden tener un nombre de dirección URL existente y que se va a tooresolve capaz de ellos mediante el protocolo DNS estándar hello (en lugar del protocolo de servicio de nomenclatura de hello) es deseable, especialmente en escenarios "Levantar y mover".</span><span class="sxs-lookup"><span data-stu-id="f2c60-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="f2c60-106">Hola servicio DNS permite toomap DNS nombres tooa nombre del servicio y, por tanto, resolver direcciones IP del extremo.</span><span class="sxs-lookup"><span data-stu-id="f2c60-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="f2c60-107">Hola servicio DNS asigna nombres de tooservice de nombres DNS, que a su vez se resuelven al extremo de servicio de hello Naming Service tooreturn Hola.</span><span class="sxs-lookup"><span data-stu-id="f2c60-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="f2c60-108">nombre DNS de Hello para el servicio de Hola se proporciona en tiempo de Hola de creación.</span><span class="sxs-lookup"><span data-stu-id="f2c60-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![puntos de conexión de servicio][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="f2c60-110">Habilitar el servicio DNS de Hola</span><span class="sxs-lookup"><span data-stu-id="f2c60-110">Enabling hello DNS service</span></span>
<span data-ttu-id="f2c60-111">En primer lugar debe servicio DNS de tooenable hello en el clúster.</span><span class="sxs-lookup"><span data-stu-id="f2c60-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="f2c60-112">Obtener plantilla hello para el clúster de Hola que desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f2c60-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="f2c60-113">Puede cualquier Hola uso [plantillas de ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) o crear una plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="f2c60-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="f2c60-114">Puede habilitar el servicio DNS Hola con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="f2c60-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="f2c60-115">Compruebe que hello `apiversion` se establece demasiado`2017-07-01-preview` para hello `Microsoft.ServiceFabric/clusters` recurso y si no es así, actualizarla como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="f2c60-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="f2c60-116">Ahora habilitar el servicio DNS Hola agregando Hola siguientes `addonFeatures` sección tras hello `fabricSettings` sección tal y como se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="f2c60-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="f2c60-117">Una vez que se ha actualizado la plantilla de clúster con hello anterior cambios, aplicarlos y deje que Hola actualización completada.</span><span class="sxs-lookup"><span data-stu-id="f2c60-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="f2c60-118">Una vez completado, Hola servicio del sistema DNS comienza a ejecutarse en el clúster que se denomina `fabric:/System/DnsService` en la sección de servicio de sistema en el Explorador de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="f2c60-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="f2c60-119">Como alternativa, puede habilitar Hola servicio DNS a través del portal de hello en tiempo de Hola de creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="f2c60-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="f2c60-120">Hola servicio DNS puede habilitarse al activar casilla de Hola para `Include DNS service` en hello `Cluster configuration` menú tal y como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="f2c60-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![Habilitar el servicio DNS a través del portal de Hola][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="f2c60-122">Nombre DNS de hello para el servicio de configuración</span><span class="sxs-lookup"><span data-stu-id="f2c60-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="f2c60-123">Una vez Hola servicio DNS se ejecuta en el clúster, puede establecer un nombre DNS para los servicios mediante declaración para los servicios predeterminados en hello `ApplicationManifest.xml` o mediante comandos de Powershell.</span><span class="sxs-lookup"><span data-stu-id="f2c60-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="f2c60-124">Establecer nombre DNS de Hola para un servicio de manera predeterminada en hello ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f2c60-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="f2c60-125">Abra el proyecto en Visual Studio, o su editor favorito y hello `ApplicationManifest.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="f2c60-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="f2c60-126">Vaya toohello sección de servicios de manera predeterminada y para cada Hola de complemento de servicio `ServiceDnsName` atributo.</span><span class="sxs-lookup"><span data-stu-id="f2c60-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="f2c60-127">Hola de ejemplo siguiente muestra cómo tooset Hola nombre DNS del servicio de hello demasiado`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="f2c60-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="f2c60-128">Una vez que se implementa la aplicación hello, instancia de servicio de hello en el Explorador de Service Fabric hello muestra el nombre DNS de Hola para esta instancia, tal y como se muestra en la figura siguiente de Hola:</span><span class="sxs-lookup"><span data-stu-id="f2c60-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![puntos de conexión de servicio][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="f2c60-130">Establecer nombre DNS de Hola para un servicio con Powershell</span><span class="sxs-lookup"><span data-stu-id="f2c60-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="f2c60-131">Puede establecer nombre DNS de Hola para un servicio cuando se crea mediante hello `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="f2c60-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="f2c60-132">Hello en el ejemplo siguiente se crea un nuevo servicio sin estado con nombre DNS de Hola`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="f2c60-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="f2c60-133">Uso de DNS en los servicios</span><span class="sxs-lookup"><span data-stu-id="f2c60-133">Using DNS in your services</span></span>
<span data-ttu-id="f2c60-134">Si implementa más de un servicio, puede encontrar puntos de conexión de Hola de otro toocommunicate servicios con mediante un nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="f2c60-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="f2c60-135">Hola servicio DNS solo es aplicable toostateless servicios, ya que Hola protocolo DNS no puede comunicarse con servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="f2c60-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="f2c60-136">Para los servicios con estado, puede utilizar a proxy inverso integrados de Hola para http llamadas toocall una partición de servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="f2c60-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="f2c60-137">Hello código siguiente muestra cómo toocall otro servicio, que es simplemente un http regular llamar a donde se debe proporcionar un puerto de Hola y cualquier ruta de acceso opcional como parte de la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2c60-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f2c60-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2c60-138">Next steps</span></span>
<span data-ttu-id="f2c60-139">Más información acerca de la comunicación de servicio en clúster de hello con [conectarse y comunicarse con los servicios](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="f2c60-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
