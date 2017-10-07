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
# <a name="service-fabric-container-networking-modes"></a>Modos de redes de contenedor de Service Fabric

Hello modo de red predeterminado que se ofrece en hello Service Fabric clúster para los servicios de contenedor es hello `nat` modo de red. Con hello `nat` redes modo, tener más de un contenedores servicio escucha toohello mismo número de puerto da como resultado errores de implementación. Para ejecutar varios servicios que escuchen en hello admite el mismo puerto, Service Fabric Hola `open` modo de red (versión 5.7 o superior). Con hello `open` modo de red, cada servicio de contenedor obtiene una dirección IP asignada dinámicamente internamente, permitir que varios servicios toolisten toohello mismo puerto.   

Por lo tanto, tiene un tipo de servicio único con un extremo estático definido en el manifiesto de servicio de hello, nuevos servicios pueden crearse y eliminarse sin errores de implementación con hello `open` modo de red. De igual forma, se pueden usar Hola mismo `docker-compose.yml` archivo con asignaciones de puertos estáticos para crear varios servicios.

Uso Hola asignada dinámicamente los servicios de toodiscover IP no es aconsejable desde Hola cambios en la dirección IP cuando se reinicia o desplaza tooanother nodo servicio de Hola. Usar solo hello **servicio de nomenclatura de tejido de servicio** o hello **servicio DNS** detección de servicios. 


> [!WARNING]
> Solo se permiten 4096 direcciones IP en total por red virtual en Azure. Por lo tanto, los suma Hola del número de Hola de nodos y número de Hola de instancias de servicio de contenedor (con `open` red) no puede superar los 4096 dentro de una red virtual. Para estos escenarios de alta densidad, Hola `nat` se recomienda el modo de red.
>

## <a name="setting-up-open-networking-mode"></a>Configuración del modo de redes abierto

1. Configurar la plantilla de Azure Resource Manager Hola habilitando el servicio DNS y Hola proveedor IP bajo `fabricSettings`. 

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

2. Configurar perfil de red de hello sección tooallow toobe configurado en cada nodo del clúster de hello las direcciones IP de varios. Hello en el ejemplo siguiente se configura cinco direcciones IP por nodo (lo que puede tener cinco instancias de servicio que escucha el puerto toohello en cada nodo) para un clúster de Windows Service Fabric.

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

    Para los clústeres de Linux, una configuración de IP pública adicional se agrega conectividad saliente tooallow. Hello fragmento de código siguiente establece el cinco direcciones IP por cada nodo de un clúster de Linux.

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

3. Para Windows clústeres solo, configurar un NSG regla abre el puerto UDP/53 para la red virtual de hello con hello siguientes valores:

   | Prioridad |    Nombre    |    Origen      |  Destino   |   Servicio    | Acción |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | VirtualNetwork | VirtualNetwork | DNS (UDP/53) | PERMITIR  |


4. Especificar el modo de red de hello en el manifiesto de aplicación Hola para cada servicio `<NetworkConfig NetworkType="open">`.  modo de Hello `open` da como resultado servicio Hola obtener una dirección IP dedicada. Si no se especifica un modo, su valor predeterminado es básico toohello `nat` modo. Por lo tanto, en el siguiente manifiesto de ejemplo de Hola `NodeContainerServicePackage1` y `NodeContainerServicePackage2` puede cada toohello escucha mismo puerto (ambos servicios están escuchando en `Endpoint1`).

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
Puede mezclar y combinar diferentes modos de redes en todos los servicios dentro de una aplicación para un clúster de Windows. Por lo tanto, puede tener algunos servicios en modo `open` y otros en modo de redes `nat`. Cuando se configura un servicio con `nat`, puerto de hello es toomust escucha ser únicos. La combinación de modos de redes para los diferentes servicios no se admite en clústeres de Linux. 


## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha obtenido información sobre los modos de redes que ofrece Service Fabric.  

* [Modelo de aplicación de Service Fabric](service-fabric-application-model.md)
* [Recursos de manifiesto de servicio de Service Fabric](service-fabric-application-model.md)
* [Implementar un tooService de contenedor de Windows Fabric en Windows Server 2016](service-fabric-get-started-containers.md)
* [Implementar un tooService de contenedor de Docker Fabric en Linux](service-fabric-get-started-containers-linux.md)
