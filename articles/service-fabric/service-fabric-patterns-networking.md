---
title: patrones de aaaNetworking para Azure Service Fabric | Documentos de Microsoft
description: "Describe los patrones comunes de redes de Service Fabric y cómo toocreate un clúster mediante el uso de características de red de Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Patrones de redes de Service Fabric
Puede integrar el clúster de Azure Service Fabric con otras características de red de Azure. En este artículo, le mostraremos cómo toocreate clústeres ese Hola de uso siguientes características:

- [Subred y red virtual existentes](#existingvnet)
- [Dirección IP pública estática](#staticpublicip)
- [Equilibrador de carga solo interno](#internallb)
- [Equilibrador de carga interno y externo](#internalexternallb)

Service Fabric se ejecuta en un conjunto de escalado de máquinas virtuales estándar. Cualquier funcionalidad que pueda usar en un conjunto de escalado de máquinas virtuales, puede usarse con un clúster de Service Fabric. Hola red secciones de plantillas de Azure Resource Manager Hola para conjuntos de escalas de máquina virtual y el tejido de servicio son idénticas. Después de implementar tooan existente de la red virtual, es fácil tooincorporate otra características, como ExpressRoute de Azure, la puerta de enlace de VPN de Azure, un grupo de seguridad de red e intercambio de tráfico de red virtual de red.

Service Fabric es único en relación con otras características de red en un aspecto. Hola [portal de Azure](https://portal.azure.com) internamente utiliza Hola Service Fabric proveedor toocall tooa clúster tooget información sobre recursos nodos y aplicaciones. proveedor de recursos de Service Fabric Hola requiere acceso de entrada es accesible públicamente toohello HTTP puerta de enlace (puerto 19080, de forma predeterminada) en el extremo de administración de Hola. [Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md) usa Hola toomanage de punto de conexión de administración del clúster. proveedor de recursos de Service Fabric Hello también usa esta información de tooquery de puerto relativa al clúster, toodisplay Hola portal de Azure. 

Si el puerto 19080 no es accesible desde el proveedor de recursos de Service Fabric hello, al igual que un mensaje *nodos no se encontró* aparece en el portal de hello, y la lista de nodo y la aplicación aparece vacía. Si desea toosee el clúster en hello portal de Azure, el equilibrador de carga debe exponer una dirección IP pública y el grupo de seguridad de red debe permitir el tráfico de puerto 19080 entrante. Si el programa de instalación no cumple estos requisitos, Hola portal de Azure no mostrar estado de hello del clúster.

## <a name="templates"></a>Plantillas

Todas las plantillas de Service Fabric están en [un archivo de descarga](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip). Debe ser capaz de toodeploy plantillas de hello como-consiste en usar Hola siga los comandos de PowerShell. Si va a implementar Hola plantilla de red Virtual de Azure existente u Hola plantilla de IP pública estática, lea primero hello [Initial setup](#initialsetup) sección de este artículo.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>Configuración inicial

### <a name="existing-virtual-network"></a>Red virtual existente

En el siguiente ejemplo de Hola, empezaremos con una red virtual existente con el nombre de red virtual ExistingRG, Hola **ExistingRG** grupo de recursos. subred de Hola se denomina de forma predeterminada. Estos recursos de forma predeterminada se crean cuando se usa hello toocreate portal Azure una máquina virtual estándar (VM). Puede crear red virtual de Hola y subred sin necesidad de crear Hola VM, pero objetivo principal de Hola de agregar una red virtual de clúster tooan existente es tooother de conectividad de red de tooprovide las máquinas virtuales. Hola crear VM proporciona un buen ejemplo de cómo una red virtual existente por lo general se usa la. Si su clúster de Service Fabric usa solo un equilibrador de carga interno, sin una dirección IP pública, puede usar Hola VM y su dirección IP pública como una ubicación segura *saltar cuadro*.

### <a name="static-public-ip-address"></a>Dirección IP pública estática

Por lo general, una dirección IP pública estática es un recurso dedicado que se administra independientemente del Hola VM o máquinas virtuales que se asigna a. Se aprovisiona en un grupo de recursos de red dedicado (como tooin opuestos Hola Service Fabric grupo de recursos de sí misma). Crear una dirección IP pública estática denominada staticIP1 Hola mismo grupo de recursos de ExistingRG, Hola portal de Azure o mediante el uso de PowerShell:

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Plantilla de Service Fabric

En los ejemplos de hello en este artículo, usamos Hola Service Fabric template.json. Puede utilizar la plantilla de Hola de toodownload de asistente estándar del portal de Hola desde el portal de hello antes de crear un clúster. También puede utilizar una de las plantillas de Hola Hola [Galería de plantillas de](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), como hello [clúster de cinco nodos Service Fabric](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>Subred y red virtual existentes

1. Cambiar nombre de toohello del parámetro hello subred de red existente de hello y, a continuación, agregue dos nuevos parámetros tooreference Hola red virtual existente:

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. Hola de cambio `vnetID` variable toopoint toohello red virtual:

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Quite `Microsoft.Network/virtualNetworks` de los recursos, para que Azure no cree una nueva red virtual:

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Comenta la red virtual de Hola de hello `dependsOn` atributo de `Microsoft.Compute/virtualMachineScaleSets`, por lo que no depende de crear una nueva red virtual:

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Implementar la plantilla de hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    Después de la implementación, debe incluir la red virtual nueva escala de hello establece las máquinas virtuales. tipo de nodo de conjunto de escala de máquina virtual de Hello debe mostrar subred y red virtual existente de Hola. También puede usar protocolo de escritorio remoto (RDP) tooaccess Hola VM que se encontraba en la red virtual de Hola y conjunto de tooping Hola nueva escala de máquinas virtuales:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

Para obtener otro ejemplo, vea [uno que no sea específico tooService tejido](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>Dirección IP pública estática

1. Agregar parámetros para el nombre de Hola de hello existente de grupo de recursos IP estática, el nombre y el nombre de dominio completo (FQDN):

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Quitar hello `dnsName` parámetro. (dirección IP estática de hello ya tiene uno).

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. Agregue una variable tooreference Hola dirección IP estática existente:

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Quite `Microsoft.Network/publicIPAddresses` de los recursos, para que Azure no cree una nueva dirección IP:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Comenta la dirección IP de Hola de hello `dependsOn` atributo de `Microsoft.Network/loadBalancers`, por lo que no depende de crear una nueva dirección IP:

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. Hola `Microsoft.Network/loadBalancers` recurso, cambio hello `publicIPAddress` elemento de `frontendIPConfigurations` tooreference Hola existente dirección IP estática en lugar de uno recién creada:

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. Hola `Microsoft.ServiceFabric/clusters` recurso, cambio `managementEndpoint` toohello FQDN de DNS de la dirección IP estática de Hola. Si está usando un clúster seguro, asegúrese de cambiar *http://* demasiado*https://*. (Tenga en cuenta que este paso se aplica solo los clústeres de tejido de tooService. Si está empleando un conjunto de escalado de máquinas virtuales, omita este paso).

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Implementar la plantilla de hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

Después de la implementación, puede ver que el equilibrador de carga es la dirección IP estática pública del toohello enlazado de hello otro grupo de recursos. Hola de extremo de conexión de cliente de Service Fabric y [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello de punto de punto de conexión de dirección IP estática de hello las DNS FQDN.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>Equilibrador de carga solo interno

Este escenario reemplaza el equilibrador de carga externo de hello en plantilla de Service Fabric Hola predeterminada con un equilibrador de carga solo para uso interno. Para implicaciones de hello portal de Azure y de proveedor de recursos de Service Fabric hello, vea Hola sección anterior.

1. Quitar hello `dnsName` parámetro. (No es necesario).

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. Si lo desea, puede agregar un parámetro de dirección IP estática, si usa el método de asignación estático. Si usa un método de asignación dinámica, no es necesario toodo este paso.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Quite `Microsoft.Network/publicIPAddresses` de los recursos, para que Azure no cree una nueva dirección IP:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Quite la dirección IP de hello `dependsOn` atributo de `Microsoft.Network/loadBalancers`, por lo que no depende de crear una nueva dirección IP. Agregar la red virtual de hello `dependsOn` atributo porque equilibrador de carga de hello ahora depende de subred de Hola de red virtual de hello:

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Cambiar del equilibrador de carga de hello `frontendIPConfigurations` configuración del uso de un `publicIPAddress`, toousing una subred y `privateIPAddress`. `privateIPAddress` usa una dirección IP interna estática predefinida. toouse una dirección IP dinámica, quitar hello `privateIPAddress` elemento y, a continuación, cambie `privateIPAllocationMethod` demasiado**dinámica**.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. Hola `Microsoft.ServiceFabric/clusters` recurso, cambio `managementEndpoint` dirección de equilibrador de carga interno de toopoint toohello. Si utiliza un clúster segura, asegúrese de cambiar *http://* demasiado*https://*. (Tenga en cuenta que este paso se aplica solo los clústeres de tejido de tooService. Si está empleando un conjunto de escalado de máquinas virtuales, omita este paso).

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Implementar la plantilla de hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

Después de la implementación, el equilibrador de carga utiliza la dirección IP de hello 10.0.0.250 estático privado. Si tiene otro equipo en esa misma red virtual, puede ir toohello interno [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) punto de conexión. Tenga en cuenta que se conecta tooone de nodos de hello detrás de equilibrador de carga de Hola.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>Equilibrador de carga interno y externo

En este escenario, comience con el equilibrador de carga externo de tipo de nodo único existente de Hola y agregar un equilibrador de carga interno para hello mismo tipo de nodo. Puede asignarse a un grupo de direcciones de back-end de tooa de puerto de back-end que se adjunta solo tooa equilibrador de carga única. Elija qué equilibrador de carga tendrá los puertos de la aplicación y cuál tendrá los puntos de conexión de administración (puertos 19000 y 19080). Si coloca los puntos de conexión de administración de hello en el equilibrador de carga interno de Hola, tenga en hello cuenta recursos de Service Fabric restricciones de proveedor descritas anteriormente en el artículo de Hola. En el ejemplo de Hola que usamos, extremos de administración de hello permanecen en equilibrador de carga externo Hola. También agregue un puerto de aplicación 80 y colocarlo en el equilibrador de carga interno de Hola.

En un clúster de dos tipo de nodo, un tipo de nodo está en el equilibrador de carga externo Hola. Hello otro tipo de nodo está en el equilibrador de carga interno de Hola. toouse un clúster de dos tipo de nodo, en hello portal plantilla creada por el tipo de nodo de dos (que viene con dos de los equilibradores de carga), cambie el equilibrador de carga interno para tooan el segundo equilibrador de carga Hola. Para obtener más información, vea hello [equilibrador de carga interno solo](#internallb) sección.

1. Agregue el parámetro de dirección IP de equilibrador de carga interno estático de Hola. (Para notas relacionada toousing una dirección IP dinámica, consulte las secciones anteriores de este artículo).

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. Agregue un parámetro de puerto 80 de aplicación.

3. tooadd versiones interno de hello las redes variables, copie y pegue ellos y agregue "-Int" toohello nombre:

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. Si empieza con plantilla generados por el portal de Hola que usa el puerto 80 de aplicación, plantilla del portal de Hola predeterminado agrega AppPort1 (puerto 80) en el equilibrador de carga externo Hola. En este caso, quite AppPort1 de equilibrador de carga externo hello `loadBalancingRules` y sondeos, para que pueda agregar equilibrador de carga interno de toohello:

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. Agregue un segundo recurso `Microsoft.Network/loadBalancers`. Parece que el equilibrador de carga interno toohello similar creado en hello [equilibrador de carga interno solo](#internallb) sección, pero usa Hola "-Int" cargar equilibrador variables e implementa sólo Hola aplicación el puerto 80. Este procedimiento quita también `inboundNatPools`, tookeep puntos de conexión RDP en el equilibrador de carga públicos Hola. Si desea RDP en el equilibrador de carga interno de hello, mueva `inboundNatPools` de toothis de equilibrador de carga externo Hola interno equilibrador de carga:

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. En `networkProfile` para hello `Microsoft.Compute/virtualMachineScaleSets` recursos, Agregar grupo de direcciones de back-end interno de hello:

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Implementar la plantilla de hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

Después de la implementación, puede ver dos equilibradores de carga en el grupo de recursos de Hola. Si examina los equilibradores de carga de hello, puede ver la dirección IP pública hello y dirección IP pública de toohello de puntos de conexión (puertos 19000 y 19080) asignados de administración. También puede ver Hola estático interno IP dirección y aplicación de punto de conexión (puerto 80) asignado toohello interno equilibrador de carga. Uso de equilibradores de carga mismo escalas de máquina virtual hello Establecer grupo back-end.

## <a name="next-steps"></a>Pasos siguientes
[Creación de un clúster](service-fabric-cluster-creation-via-arm.md)
