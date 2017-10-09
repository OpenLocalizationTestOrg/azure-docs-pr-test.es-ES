---
title: proxy inverso de aaaAzure Service Fabric | Documentos de Microsoft
description: "Utiliza a un proxy inverso de Service Fabric para toomicroservices de comunicación desde el interior y exterior clúster Hola."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Proxy inverso en Azure Service Fabric
proxy inverso de Hola que está integrado en Azure Service Fabric direcciones microservicios en clúster de Service Fabric Hola que expone los extremos HTTP.

## <a name="microservices-communication-model"></a>Modelo de comunicación de microservicios
Microservicios en Service Fabric suele ejecutan en un subconjunto de máquinas virtuales en clúster de Hola y pueden pasar tooanother de una máquina virtual por distintas razones. Por lo tanto, los puntos de conexión de Hola para microservicios pueden cambiar dinámicamente. Hola patrón típico toocommunicate toohello microservicio es siguiente Hola resolver bucle:

1. Resolver la ubicación del servicio Hola inicialmente a través del servicio de nombres de Hola.
2. Conectar el servicio toohello.
3. Determinar la causa de Hola de errores de conexión y resolver la ubicación del servicio Hola de nuevo cuando sea necesario.

Este proceso implica generalmente bibliotecas de comunicación de cliente en un bucle de reintento que implementa directivas de resolución e inténtelo de nuevo del servicio de Hola de ajuste.
Para más información, consulte [Conexión y comunicación con los servicios](service-fabric-connect-and-communicate-with-services.md).

### <a name="communicating-by-using-hello-reverse-proxy"></a>Comunicarse con el proxy inverso Hola
proxy inverso de Hello en el tejido de servicio se ejecuta en todos los nodos Hola Hola clúster. Realiza el proceso de resolución de servicio completo de hello en nombre del cliente y, a continuación, reenvía la solicitud de cliente de Hola. Por lo tanto, los clientes que se ejecutan en el clúster de hello pueden usar cualquier servicio de destino de cliente HTTP comunicación bibliotecas tootalk toohello mediante el uso de proxy inverso de Hola que se ejecuta localmente en Hola mismo nodo.

![Comunicación interna][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Alcanzar microservicios de clúster de hello exterior
modelo de comunicación externa Hola predeterminado para microservicios es un modelo de participación en donde no se puede tener acceso a cada servicio directamente desde los clientes externos. [El equilibrador de carga Azure](../load-balancer/load-balancer-overview.md), que es un límite de red entre microservicios y los clientes externos, realiza la traducción de direcciones de red y externo reenvía solicitudes de puntos de conexión de toointernal IP: Port. toomake clientes de tooexternal directamente accesibles de punto de conexión de microservicio, primero debe configurar tooforward tráfico tooeach puerto que Hola servicio utiliza el equilibrador de carga en el clúster de Hola. Además, la mayoría microservicios, especialmente con estado microservicios, no en vivo en todos los nodos del clúster de Hola. Hola microservicios pueden mover entre los nodos de conmutación por error. En tales casos, equilibrador de carga no se puede determinar eficazmente ubicación Hola del nodo de destino de Hola de hello réplicas toowhich debe reenviar el tráfico.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Microservicios a través de proxy inverso de Hola de clúster de hello fuera de alcance
En lugar de configurar el puerto Hola de un servicio individual en el equilibrador de carga, puede configurar solo Hola puerto de proxy inverso de hello en el equilibrador de carga. Esta configuración permite a los clientes fuera del clúster de hello tener acceso a servicios en clúster de hello mediante proxy inverso de hello sin ninguna configuración adicional.

![Comunicación externa][0]

> [!WARNING]
> Cuando se configura el puerto de proxy inverso de hello en equilibrador de carga, son direccionables desde fuera de clúster de hello microservicios todos los clúster de Hola que exponen un extremo HTTP.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>Formato URI para tener acceso a servicios mediante el uso de proxy inverso de Hola
usos de proxy inverso de Hola que se debería reenviar una uniforme de recursos específico (URI) de identificador formato tooidentify Hola partición toowhich Hola entrantes solicitud de servicio:

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **http:** proxy inverso de Hola puede ser configurado tooaccept HTTP o el tráfico HTTPS. Para el reenvío de HTTPS, consulte demasiado[conectar el servicio seguro tooa con proxy inverso de hello](service-fabric-reverseproxy-configure-secure-communication.md) una vez que haya toolisten el programa de instalación de proxy inverso en HTTPS.
* **Nombre de dominio completo (FQDN) de clúster | dirección IP interna:** para los clientes externos, puede configurar el proxy inverso de Hola para que sea accesible a través del dominio del clúster hello, como mycluster.eastus.cloudapp.azure.com. De forma predeterminada, proxy inverso de Hola se ejecuta en cada nodo. Para el tráfico interno, puede tener acceso proxy inverso de hello en el host local o en cualquier dirección IP de nodo interno, por ejemplo, 10.0.0.1.
* **Puerto:** se trata de puerto de hello, como 19081, que se ha especificado para el proxy inverso Hola.
* **ServiceInstanceName:** trata Hola completo nombre de instancia de servicio de hello implementada que se está intentando tooreach sin Hola "fabric: /" esquema. Por ejemplo, tooreach hello *fabric: / myapp/myservice/* servicio, usaría *myapp/myservice*.

    nombre de instancia de servicio de Hello distingue mayúsculas de minúsculas. Utilizando un distinguen mayúsculas de minúsculas para el nombre de instancia de servicio de hello en dirección URL de hello hace Hola solicitudes toofail con 404 (no encontrado).
* **Ruta de acceso de sufijo:** es Hola real ruta de acceso URL, como *myapi/valores/agregar/3*, para servicio de Hola que desee tooconnect a.
* **PartitionKey:** para un servicio con particiones, esta es la clave de partición calculada de Hola de partición de Hola que desea tooreach. Tenga en cuenta que esto es *no* Hola GUID de Id. de partición. Este parámetro no es necesario para los servicios que utilizan el esquema de partición de singleton de Hola.
* **PartitionKind:** se trata de esquema de partición de servicio de Hola. El valor puede ser Int64Range o Con nombre. Este parámetro no es necesario para los servicios que utilizan el esquema de partición de singleton de Hola.
* **ListenerName** los extremos de Hola de servicio de hello tienen formato de Hola {"Extremos": {"Listener1": "Endpoint1", "Listener2": "Endpoint2"...}}. Cuando el servicio de hello expone varios puntos de conexión, se identifica el punto de conexión de hello esa solicitud de cliente de Hola se debería reenviar a. Esto se puede omitir si el servicio de hello tiene sólo un agente de escucha.
* **TargetReplicaSelector** especifica cómo se debe seleccionar instancia o la réplica de destino de Hola.
  * Cuando el servicio de destino de hello está activo, hello TargetReplicaSelector puede ser uno de los siguientes Hola: 'PrimaryReplica', 'RandomSecondaryReplica' o 'RandomReplica'. Si no se especifica este parámetro, valor predeterminado de hello es 'PrimaryReplica'.
  * Cuando el servicio de destino de hello no tiene estado, proxy inverso toma una instancia de solicitud hello tooforward de partición de servicio de Hola a aleatorio.
* **Tiempo de espera:** Esto especifica el tiempo de espera de Hola para solicitud de hello HTTP creado por toohello servicio de proxy inverso de hello en nombre de la solicitud de cliente de Hola. valor de Hello predeterminado es 60 segundos. Se trata de un parámetro opcional.

### <a name="example-usage"></a>Ejemplo de uso
Por ejemplo, vamos a echar hello *fabric: / MyApp/MyService* servicio que se abre un agente de escucha HTTP en hello después de la dirección URL:

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

Siguientes son recursos de hello para el servicio de hello:

* `/index.html`
* `/api/users/<userId>`

Si servicio de hello utiliza singleton Hola esquema de partición, Hola *PartitionKey* y *PartitionKind* parámetros de cadena de consulta no son necesarios, y puede tener acceso al servicio de hello mediante el uso de la puerta de enlace de hello como:

* Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* Internamente: `http://localhost:19081/MyApp/MyService`

Si el servicio de Hola usa Hola Int64 uniforme esquema de partición, Hola *PartitionKey* y *PartitionKind* parámetros de cadena de consulta deben ser tooreach usa una partición de servicio de hello:

* Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* Internamente: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

recursos de hello tooreach que expone el servicio de hello, basta con colocar la ruta de acceso de recursos de Hola después de nombre de servicio de hello en dirección URL de hello:

* Externamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* Internamente: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

puerta de enlace de Hello, a continuación, reenvía la dirección URL del servicio estas solicitudes toohello:

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>Control especial de los servicios de uso compartido de puertos
La puerta de enlace de aplicaciones Azure intenta tooresolve un servicio nuevo de direcciones y vuelva a intentar la solicitud de hello cuando un servicio no se puede obtener acceso. Se trata de una de las ventajas principal de puerta de enlace de aplicación porque el código de cliente no necesita tooimplement su propia resolución de servicio y resolver el bucle.

Por lo general, cuando no se puede alcanzar un servicio, instancia de servicio de Hola o réplica ha movido tooa otro nodo como parte de su ciclo de vida normal. Cuando esto sucede, puerta de enlace de aplicaciones puede recibir una conexión de red error que indica que un punto de conexión es que no abierto más tiempo en hello originalmente resolver direcciones.

Sin embargo, las instancias del servicio o las réplicas pueden compartir un proceso de host y un puerto cuando un servidor web basado en http.sys las hospeda; por ejemplo:

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [ASP.NET Core WebListener](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

En esta situación, es probable que el servidor web Hola está disponible en el proceso de host de Hola y responde toorequests pero Hola resolver la instancia del servicio o réplica ya no está disponible en el host de Hola. En este caso, la puerta de enlace de hello recibirá una respuesta HTTP 404 de servidor web de Hola. Este tipo de respuesta tiene dos lecturas diferentes:

- Caja #1: la dirección de servicio de hello es correcta, pero el recurso Hola Hola usuario solicitado no existe.
- Caso #2: la dirección de servicio de hello es incorrecto y recurso de Hola Hola el usuario solicitó puede encontrarse en otro nodo.

Hola primer caso es un error 404 de HTTP normal, que se considera un error de usuario. Sin embargo, en el segundo caso hello, usuario Hola ha solicitado un recurso que existen. Puerta de enlace de aplicaciones era toolocate que se ha movido porque Hola propio servicio. Aplicación puerta de enlace necesidades tooresolve Hola dirección nuevo y solicitud de Hola de reintento.

Puerta de enlace de aplicaciones, por tanto, necesita un toodistinguish forma entre estos dos casos. toomake que existe una distinción, una sugerencia de servidor hello es necesaria.

* De forma predeterminada, puerta de enlace de aplicaciones se da por supuesto caso #2 y trata tooresolve y emitir solicitudes de Hola de nuevo.
* tooindicate caso &#1; tooApplication puerta de enlace, el servicio de hello debería devolver Hola siguiente encabezado de respuesta HTTP:

  `X-ServiceFabric : ResourceNotFound`

Este encabezado de respuesta HTTP indica una situación de HTTP 404 normal en qué Hola recurso solicitado no existe y puerta de enlace de aplicaciones no intentará volver a dirección de servicio de tooresolve Hola.

## <a name="setup-and-configuration"></a>Instalación y configuración

### <a name="enable-reverse-proxy-via-azure-portal"></a>Habilitar proxy inverso mediante Azure Portal

Portal de Azure proporciona a un proxy inverso de tooenable opción al crear un nuevo clúster de Service Fabric.
En **clúster crear Service Fabric**, paso 2: configuración del clúster, configuración de tipo de nodo, seleccione también Hola casilla "Habilitar proxy inverso".
Para configurar el proxy inverso segura, se puede especificar certificado SSL en el paso 3: seguridad, establecer la configuración de seguridad de clúster, seleccione Hola casilla demasiado "Incluyen un certificado SSL para el proxy inverso" y escriba los detalles del certificado de Hola.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Habilitar proxy inverso mediante plantillas de Azure Resource Manager

Puede usar hello [plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable Hola proxy inverso de Service Fabric para clúster Hola.

Consulte demasiado[Proxy inverso de HTTPS configurar en un clúster segura](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) ejemplos de plantilla para el Administrador de recursos de Azure tooconfigure proxy inverso seguro con un certificado y el control de sustitución del certificado.

En primer lugar, obtendrá plantilla hello para el clúster de Hola que desea toodeploy. Puede usar plantillas de ejemplo de Hola o crear una plantilla personalizada que el Administrador de recursos. A continuación, puede habilitar a proxy inverso de hello mediante Hola pasos:

1. Definir un puerto de proxy inverso de Hola Hola [sección parámetros](../azure-resource-manager/resource-group-authoring-templates.md) de plantilla de Hola.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. Especifique el puerto de Hola para cada uno de los objetos de nodetype Hola Hola **clúster** [sección de recursos de tipo](../azure-resource-manager/resource-group-authoring-templates.md).

    puerto de Hola se identifica mediante el nombre del parámetro hello, reverseProxyEndpointPort.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. Hola tooaddress proxy inverso de hello exterior clúster de Azure, configurar reglas de equilibrador de carga de Azure de hello para el puerto de Hola que especificó en el paso 1.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. tooconfigure certificados SSL en el puerto de hello para el proxy inverso de hello, agregar Hola certificado toohello ***reverseProxyCertificate*** propiedad Hola **clúster** [sección de tipo de recurso](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Compatibilidad con un certificado de proxy inverso que es diferente del certificado de clúster de Hola
 Si el certificado de proxy inverso de hello es distinto del certificado de Hola que protege el clúster de hello, a continuación, Hola especificado anteriormente certificado debe instalarse en la máquina virtual de Hola y agrega la lista de control de acceso (ACL) de toohello para que puedan Service Fabric obtener acceso a él. Esto puede hacerse en hello **virtualMachineScaleSets** [sección de recursos de tipo](../resource-group-authoring-templates.md). Para la instalación, agregue ese osProfile toohello de certificado. sección de extensión de Hola de plantilla de hello puede actualizar el certificado de Hola Hola ACL.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> Cuando se usan certificados que son diferentes de hello clúster certificado tooenable Hola proxy inverso en un clúster existente, instalar certificado de proxy inverso de Hola y actualizar Hola ACL en clúster de hello antes de habilitar el proxy inverso Hola. Hola completa [plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) implementación mediante la configuración de hello mencionadas anteriormente antes de iniciar un proxy inverso de implementación tooenable hello en los pasos 1 a 4.

## <a name="next-steps"></a>Pasos siguientes
* Vea un ejemplo de comunicación HTTP entre los servicios de un [proyecto de ejemplo en GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Reenvío de servicio de toosecure HTTP con proxy inverso de Hola](service-fabric-reverseproxy-configure-secure-communication.md)
* [Llamadas a procedimiento remoto con la comunicación remota de Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [API web que usa OWIN en Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicación WCF con la utilización de Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* Para opciones adicionales de la configuración del proxy inverso, consulte la sección de ApplicationGateway/Http en [Personalización de la configuración del clúster de Service Fabric](service-fabric-cluster-fabric-settings.md).

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
