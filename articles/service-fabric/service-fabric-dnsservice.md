---
title: Servicio DNS de Azure Service Fabric | Microsoft Docs
description: "Use el servicio DNS de Service Fabric para detectar microservicios desde dentro del clúster."
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
ms.openlocfilehash: 9871bc5aa4e74ab0faef401d67c4e9558eb5e14b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="dfe08-103">Servicio DNS en Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dfe08-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="dfe08-104">El servicio DNS es un servicio de sistema opcional que se puede habilitar en el clúster para detectar otros servicios que usan el protocolo DNS.</span><span class="sxs-lookup"><span data-stu-id="dfe08-104">The DNS Service is an optional system service that you can enable in your cluster to discover other services using the DNS protocol.</span></span>

<span data-ttu-id="dfe08-105">Muchos servicios, sobre todo los servicios en contenedores, pueden tener un nombre de dirección URL existente. El poder resolverlos mediante el protocolo DNS estándar (en lugar del protocolo Servicio de nombres) es deseable, en particular en escenarios "lift-and-shift".</span><span class="sxs-lookup"><span data-stu-id="dfe08-105">Many services, especially containerized services, can have an existing URL name, and being able to resolve them using the standard DNS protocol (rather than the Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="dfe08-106">El servicio DNS permite asignar nombres DNS a un nombre de servicio y, por tanto, resolver direcciones IP del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="dfe08-106">The DNS service enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="dfe08-107">El servicio DNS asigna nombres DNS a nombres de servicio que el protocolo Servicio de nombres resuelve para devolver el punto de conexión del servicio.</span><span class="sxs-lookup"><span data-stu-id="dfe08-107">The DNS service maps DNS names to service names, which in turn are resolved by the Naming Service to return the service endpoint.</span></span> <span data-ttu-id="dfe08-108">El nombre DNS para el servicio se proporciona en el momento de la creación.</span><span class="sxs-lookup"><span data-stu-id="dfe08-108">The DNS name for the service is provided at the time of creation.</span></span> 

![puntos de conexión de servicio][0]

## <a name="enabling-the-dns-service"></a><span data-ttu-id="dfe08-110">Habilitar el servicio DNS</span><span class="sxs-lookup"><span data-stu-id="dfe08-110">Enabling the DNS service</span></span>
<span data-ttu-id="dfe08-111">Primero debe habilitar el servicio DNS en el clúster.</span><span class="sxs-lookup"><span data-stu-id="dfe08-111">First you need to enable the DNS service in your cluster.</span></span> <span data-ttu-id="dfe08-112">Obtenga la plantilla del clúster que desea implementar.</span><span class="sxs-lookup"><span data-stu-id="dfe08-112">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="dfe08-113">Puede usar las [plantillas de ejemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) o crear una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dfe08-113">You can either use the [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="dfe08-114">Puede habilitar el servicio DNS con los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dfe08-114">You can enable the DNS service with the following steps:</span></span>

1. <span data-ttu-id="dfe08-115">Compruebe que `apiversion` está establecido en `2017-07-01-preview` para el recurso `Microsoft.ServiceFabric/clusters` y, si no es así, actualícelo como se muestra en el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="dfe08-115">Check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in the following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="dfe08-116">Ahora, habilite el servicio DNS al agregar la siguiente sección `addonFeatures` después de la sección `fabricSettings`, como se muestra en el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="dfe08-116">Now enable the DNS service by adding the following `addonFeatures` section after the `fabricSettings` section as shown in the following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="dfe08-117">Una vez actualizada la plantilla del clúster con los cambios anteriores, aplíquelos y deje que se complete la actualización.</span><span class="sxs-lookup"><span data-stu-id="dfe08-117">Once you have updated your cluster template with the preceding changes, apply them and let the upgrade complete.</span></span> <span data-ttu-id="dfe08-118">Una vez completada, el servicio de sistema DNS comienza a ejecutarse en el clúster denominado `fabric:/System/DnsService` en la sección de servicios del sistema de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="dfe08-118">Once complete, the DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in the Service Fabric explorer.</span></span> 

<span data-ttu-id="dfe08-119">También puede habilitar el servicio DNS a través del portal en el momento de la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="dfe08-119">Alternatively, you can enable the DNS service through the portal at the time of cluster creation.</span></span> <span data-ttu-id="dfe08-120">El servicio DNS puede habilitarse si se activa la casilla `Include DNS service` en el menú `Cluster configuration`, como se muestra en la captura de pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="dfe08-120">The DNS service can be enabled by checking the box for `Include DNS service` in the `Cluster configuration` menu as shown in the following screenshot:</span></span>

![Habilitación del servicio DNS a través del portal][2]


## <a name="setting-the-dns-name-for-your-service"></a><span data-ttu-id="dfe08-122">Definición del nombre DNS para el servicio</span><span class="sxs-lookup"><span data-stu-id="dfe08-122">Setting the DNS name for your service</span></span>
<span data-ttu-id="dfe08-123">Una vez que el servicio DNS se esté ejecutando en el clúster, puede establecer un nombre DNS para los servicios ya sea mediante declaración para los servicios predeterminados en `ApplicationManifest.xml` o a través de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dfe08-123">Once the DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in the `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-the-dns-name-for-a-default-service-in-the-applicationmanifestxml"></a><span data-ttu-id="dfe08-124">Definición del nombre DNS de un servicio predeterminado en ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="dfe08-124">Setting the DNS name for a default service in the ApplicationManifest.xml</span></span>
<span data-ttu-id="dfe08-125">Abra el proyecto en Visual Studio, o su editor favorito, y abra el archivo `ApplicationManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="dfe08-125">Open your project in Visual Studio, or your favorite editor, and open the `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="dfe08-126">Vaya a la sección de servicios predeterminados y, para cada servicio, agregue el atributo `ServiceDnsName`.</span><span class="sxs-lookup"><span data-stu-id="dfe08-126">Go to the default services section, and for each service add the `ServiceDnsName` attribute.</span></span> <span data-ttu-id="dfe08-127">En el ejemplo siguiente se muestra cómo establecer el nombre DNS del servicio en `service1.application1`.</span><span class="sxs-lookup"><span data-stu-id="dfe08-127">The following example shows how to set the DNS name of the service to `service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="dfe08-128">Una vez implementada la aplicación, la instancia de servicio de Service Fabric Explorer muestra el nombre DNS de esta instancia, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="dfe08-128">Once the application is deployed, the service instance in the Service Fabric explorer shows the DNS name for this instance, as shown in the following figure:</span></span> 

![puntos de conexión de servicio][1]

### <a name="setting-the-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="dfe08-130">Definición del nombre DNS de un servicio mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfe08-130">Setting the DNS name for a service using Powershell</span></span>
<span data-ttu-id="dfe08-131">Puede establecer el nombre DNS de un servicio cuando se crea mediante el PowerShell `New-ServiceFabricService`.</span><span class="sxs-lookup"><span data-stu-id="dfe08-131">You can set the DNS name for a service when creating it using the `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="dfe08-132">En el ejemplo siguiente se crea un servicio sin estado nuevo con el nombre DNS `service1.application1`.</span><span class="sxs-lookup"><span data-stu-id="dfe08-132">The following example creates a new stateless service with the DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="dfe08-133">Uso de DNS en los servicios</span><span class="sxs-lookup"><span data-stu-id="dfe08-133">Using DNS in your services</span></span>
<span data-ttu-id="dfe08-134">Si implementa más de un servicio, puede buscar los puntos de conexión de otros servicios con los que comunicarse mediante un nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="dfe08-134">If you deploy more than one service, you can find the endpoints of other services to communicate with  by using a DNS name.</span></span> <span data-ttu-id="dfe08-135">El servicio DNS solo se aplica a los servicios sin estado, ya que el protocolo DNS no puede comunicarse con servicios con estado.</span><span class="sxs-lookup"><span data-stu-id="dfe08-135">The DNS service is only applicable to stateless services, since the DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="dfe08-136">En el caso de los servicios con estado, puede usar el proxy inverso integrado para llamadas HTTP para llamar a una partición de servicio determinada.</span><span class="sxs-lookup"><span data-stu-id="dfe08-136">For stateful services, you can use the built-in reverse proxy for http calls to call a particular service partition.</span></span>

<span data-ttu-id="dfe08-137">El código siguiente muestra cómo llamar a otro servicio, lo que constituye una llamada http normal donde se proporcionan el puerto y cualquier ruta de acceso opcional como parte de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="dfe08-137">The following code shows how to call another service, which is simply a regular http call where you provide the port and any optional path as part of the URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dfe08-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dfe08-138">Next steps</span></span>
<span data-ttu-id="dfe08-139">Para más información sobre la comunicación de servicios dentro del clúster, vea [Conexión y comunicación con servicios](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="dfe08-139">Learn more about service communication within the cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
