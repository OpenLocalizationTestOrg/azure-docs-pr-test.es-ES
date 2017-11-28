---
title: aaaConfigure modos para servicios de contenedor de Azure Service Fabric de red | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup Hola diferentes modos de red que Azure Service Fabric es compatible con."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="70988-103">Modos de redes de contenedor de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="70988-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="70988-104">Hello modo de red predeterminado que se ofrece en hello Service Fabric clúster para los servicios de contenedor es hello `nat` modo de red.</span><span class="sxs-lookup"><span data-stu-id="70988-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="70988-105">Con hello `nat` redes modo, tener más de un contenedores servicio escucha toohello mismo número de puerto da como resultado errores de implementación.</span><span class="sxs-lookup"><span data-stu-id="70988-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="70988-106">Para ejecutar varios servicios que escuchen en hello admite el mismo puerto, Service Fabric Hola `open` modo de red (versión 5.7 o superior).</span><span class="sxs-lookup"><span data-stu-id="70988-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="70988-107">Con hello `open` modo de red, cada servicio de contenedor obtiene una dirección IP asignada dinámicamente internamente, permitir que varios servicios toolisten toohello mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="70988-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="70988-108">Por lo tanto, tiene un tipo de servicio único con un extremo estático definido en el manifiesto de servicio de hello, nuevos servicios pueden crearse y eliminarse sin errores de implementación con hello `open` modo de red.</span><span class="sxs-lookup"><span data-stu-id="70988-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="70988-109">De igual forma, se pueden usar Hola mismo `docker-compose.yml` archivo con asignaciones de puertos estáticos para crear varios servicios.</span><span class="sxs-lookup"><span data-stu-id="70988-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="70988-110">Uso Hola asignada dinámicamente los servicios de toodiscover IP no es aconsejable desde Hola cambios en la dirección IP cuando se reinicia o desplaza tooanother nodo servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="70988-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="70988-111">Usar solo hello **servicio de nomenclatura de tejido de servicio** o hello **servicio DNS** detección de servicios.</span><span class="sxs-lookup"><span data-stu-id="70988-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="70988-112">Solo se permiten 4096 direcciones IP en total por red virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="70988-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="70988-113">Por lo tanto, los suma Hola del número de Hola de nodos y número de Hola de instancias de servicio de contenedor (con `open` red) no puede superar los 4096 dentro de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="70988-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="70988-114">Para estos escenarios de alta densidad, Hola `nat` se recomienda el modo de red.</span><span class="sxs-lookup"><span data-stu-id="70988-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="70988-115">Configuración del modo de redes abierto</span><span class="sxs-lookup"><span data-stu-id="70988-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="70988-116">Configurar la plantilla de Azure Resource Manager Hola habilitando el servicio DNS y Hola proveedor IP bajo `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="70988-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="70988-117">Configurar perfil de red de hello sección tooallow toobe configurado en cada nodo del clúster de hello las direcciones IP de varios.</span><span class="sxs-lookup"><span data-stu-id="70988-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="70988-118">Hello en el ejemplo siguiente se configura cinco direcciones IP por nodo (lo que puede tener cinco instancias de servicio que escucha el puerto toohello en cada nodo) para un clúster de Windows Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="70988-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="70988-119">Para los clústeres de Linux, una configuración de IP pública adicional se agrega conectividad saliente tooallow.</span><span class="sxs-lookup"><span data-stu-id="70988-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="70988-120">Hello fragmento de código siguiente establece el cinco direcciones IP por cada nodo de un clúster de Linux.</span><span class="sxs-lookup"><span data-stu-id="70988-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="70988-121">Para Windows clústeres solo, configurar un NSG regla abre el puerto UDP/53 para la red virtual de hello con hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="70988-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="70988-122">Prioridad</span><span class="sxs-lookup"><span data-stu-id="70988-122">Priority</span></span> |    <span data-ttu-id="70988-123">Nombre</span><span class="sxs-lookup"><span data-stu-id="70988-123">Name</span></span>    |    <span data-ttu-id="70988-124">Origen</span><span class="sxs-lookup"><span data-stu-id="70988-124">Source</span></span>      |  <span data-ttu-id="70988-125">Destino</span><span class="sxs-lookup"><span data-stu-id="70988-125">Destination</span></span>   |   <span data-ttu-id="70988-126">Servicio</span><span class="sxs-lookup"><span data-stu-id="70988-126">Service</span></span>    | <span data-ttu-id="70988-127">Acción</span><span class="sxs-lookup"><span data-stu-id="70988-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="70988-128">2000</span><span class="sxs-lookup"><span data-stu-id="70988-128">2000</span></span> | <span data-ttu-id="70988-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="70988-129">Custom_Dns</span></span> | <span data-ttu-id="70988-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="70988-130">VirtualNetwork</span></span> | <span data-ttu-id="70988-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="70988-131">VirtualNetwork</span></span> | <span data-ttu-id="70988-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="70988-132">DNS (UDP/53)</span></span> | <span data-ttu-id="70988-133">PERMITIR</span><span class="sxs-lookup"><span data-stu-id="70988-133">Allow</span></span>  |


4. <span data-ttu-id="70988-134">Especificar el modo de red de hello en el manifiesto de aplicación Hola para cada servicio `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="70988-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="70988-135">modo de Hello `open` da como resultado servicio Hola obtener una dirección IP dedicada.</span><span class="sxs-lookup"><span data-stu-id="70988-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="70988-136">Si no se especifica un modo, su valor predeterminado es básico toohello `nat` modo.</span><span class="sxs-lookup"><span data-stu-id="70988-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="70988-137">Por lo tanto, en el siguiente manifiesto de ejemplo de Hola `NodeContainerServicePackage1` y `NodeContainerServicePackage2` puede cada toohello escucha mismo puerto (ambos servicios están escuchando en `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="70988-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="70988-138">Puede mezclar y combinar diferentes modos de redes en todos los servicios dentro de una aplicación para un clúster de Windows.</span><span class="sxs-lookup"><span data-stu-id="70988-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="70988-139">Por lo tanto, puede tener algunos servicios en modo `open` y otros en modo de redes `nat`.</span><span class="sxs-lookup"><span data-stu-id="70988-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="70988-140">Cuando se configura un servicio con `nat`, puerto de hello es toomust escucha ser únicos.</span><span class="sxs-lookup"><span data-stu-id="70988-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="70988-141">La combinación de modos de redes para los diferentes servicios no se admite en clústeres de Linux.</span><span class="sxs-lookup"><span data-stu-id="70988-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="70988-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="70988-142">Next steps</span></span>
<span data-ttu-id="70988-143">En este artículo, ha obtenido información sobre los modos de redes que ofrece Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="70988-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="70988-144">Modelo de aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="70988-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="70988-145">Recursos de manifiesto de servicio de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="70988-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="70988-146">Implementar un tooService de contenedor de Windows Fabric en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="70988-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="70988-147">Implementar un tooService de contenedor de Docker Fabric en Linux</span><span class="sxs-lookup"><span data-stu-id="70988-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
