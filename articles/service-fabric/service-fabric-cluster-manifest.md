---
title: "aaaConfigure el clúster de independiente de Azure Service Fabric | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure su clúster de Service Fabric privado o independiente."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Opciones de configuración de clústeres de Windows independientes
Este artículo describe cómo tooconfigure un clúster de Service Fabric independientes con Hola ***ClusterConfig.JSON*** archivo. Puede utilizar esta información de toospecify de archivo como nodos de Service Fabric hello y sus direcciones IP, los distintos tipos de nodos en clúster hello, las configuraciones de seguridad de hello, así como la topología de red de hello en cuanto a dominios de error o una actualización, para su independiente clúster.

Cuando se [Descargar paquete de Service Fabric independiente de hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), algunos ejemplos de archivo de hello ClusterConfig.JSON son tooyour descargado trabajo máquina. ejemplos de Hello tener *DevCluster* en sus nombres le ayudará a crear un clúster con todos los tres nodos en hello mismo equipo, como nodos lógicos. Fuera de estos casos, al menos un nodo debe marcarse como un nodo principal. Este clúster es útil para un entorno de desarrollo o pruebas y no se admite como clúster de producción. ejemplos de Hello tener *MultiMachine* en sus nombres, le ayudará a crear un clúster de calidad de producción, donde cada nodo en un equipo independiente.

1. *ClusterConfig.Unsecure.DevCluster.JSON* y *ClusterConfig.Unsecure.MultiMachine.JSON* mostrar cómo toocreate una prueba no segura o producción de clúster respectivamente. 
2. *ClusterConfig.Windows.DevCluster.JSON* y *ClusterConfig.Windows.MultiMachine.JSON* mostrar cómo toocreate clúster de prueba o de producción, proteger mediante [la seguridad de Windows](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* y *ClusterConfig.X509.MultiMachine.JSON* mostrar cómo toocreate clúster de prueba o de producción, proteger mediante [X509 seguridad basada en certificados](service-fabric-windows-cluster-x509-security.md). 

Ahora examinaremos Hola distintas secciones de un ***ClusterConfig.JSON*** de archivos como sigue.

## <a name="general-cluster-configurations"></a>Opciones generales de configuración de clústeres
Esto cubre Hola clúster amplia configuraciones específicas de tal como se muestra en el siguiente fragmento de JSON de Hola.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

Puede proporcionar cualquier clúster de Service Fabric Nombre_descriptivo tooyour asignando toohello **nombre** variable. Hola **clusterConfigurationVersion** es el número de versión de Hola del clúster; debe aumentar cada vez que actualice el clúster de Service Fabric. Sin embargo, que debe conservarse hello **el elemento apiVersion** toohello por defecto.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Nodos de clúster de Hola
Puede configurar los nodos de hello en el clúster de Service Fabric mediante hello **nodos** sección, como el fragmento siguiente muestra de Hola.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Un clúster de Service Fabric debe contener al menos 3 nodos. Puede agregar más sección toothis de nodos según el programa de instalación. Hello en la tabla siguiente explica los valores de configuración de Hola para cada nodo.

| **Opción de configuración del nodo** | **Descripción** |
| --- | --- |
| nodeName |Puede permitir que cualquier nodo de toohello nombre descriptivo. |
| iPAddress |Obtener dirección IP de hello del nodo, abra una ventana de comandos y escriba `ipconfig`. Tenga en cuenta dirección IPV4 de Hola y asignar toohello **iPAddress** variable. |
| nodeTypeRef |Cada nodo se puede asignar a un tipo de nodo diferente. Hola [tipos de nodos](#nodetypes) se definen en la siguiente sección de Hola. |
| faultDomain |Error dominios habilitar administradores toodefine Hola físicos nodos de clúster que podrían producir un error en hello mismo tiempo debido a dependencias físico tooshared. |
| upgradeDomain |Dominios de actualización describen los conjuntos de nodos que se cierran de Service Fabric actualiza a sobre Hola mismo tiempo. Puede elegir qué toowhich tooassign de nodos de dominios de actualización, como que no están limitados por los requisitos físicos. |

## <a name="cluster-properties"></a>Propiedades de clúster
Hola **propiedades** sección en hello ClusterConfig.JSON está en clúster de hello tooconfigure usado como se indica a continuación.

<a id="reliability"></a>

### <a name="reliability"></a>Confiabilidad
concepto de Hola de **reliabilityLevel** define número Hola de réplicas o instancias de servicios del sistema de Service Fabric Hola que se pueden ejecutar en nodos principales de Hola de clúster de Hola. Determina la confiabilidad de Hola de estos servicios y, por tanto, Hola clúster. valor de Hello es calculada por el sistema de hello en tiempo de creación y actualización de clúster.

### <a name="diagnostics"></a>Diagnóstico
Hola **diagnosticsStore** sección permite diagnósticos de tooconfigure parámetros tooenable y nodo de solución de problemas o errores de clúster, tal y como se muestra en el siguiente fragmento de código de hello. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Hola **metadatos** es una descripción de los diagnósticos de clúster y se puede establecer según la configuración. Estas variables permiten recopilar registros de seguimiento ETW, volcados de memoria y contadores de rendimiento. Lea [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) y [Seguimiento ETW](https://msdn.microsoft.com/library/ms751538.aspx) para más información sobre los registros de seguimiento ETW. Todos los registros incluidos [volcados de memoria](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) y [contadores de rendimiento](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) puede ser dirigido toohello **connectionString** carpeta en su equipo. También puede usar *AzureStorage* para almacenar diagnósticos. Vea a continuación un ejemplo de fragmento de código.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Seguridad
Hola **seguridad** sección es necesario para un clúster de Service Fabric segura independiente. Hola siguiente fragmento de código muestra una parte de esta sección.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Hola **metadatos** es una descripción de su clúster segura y se pueden establecer según la configuración. Hola **ClusterCredentialType** y **ServerCredentialType** determinar el tipo de saludo de seguridad que va a implementar clústeres de Hola y nodos de Hola. Se pueden establecer tooeither *X509* para una seguridad basada en certificados, o *Windows* una seguridad basada en Azure Active Directory. Hola rest de hello **seguridad** sección se basará en el tipo de saludo de seguridad de Hola. Lectura [seguridad basada en certificados en un clúster independiente](service-fabric-windows-cluster-x509-security.md) o [la seguridad de Windows en un clúster independiente](service-fabric-windows-cluster-windows-security.md) para obtener información sobre cómo se rest toofill out Hola de hello **seguridad**sección.

<a id="nodetypes"></a>

### <a name="node-types"></a>Tipos de nodo
Hola **nodeTypes** sección describe el tipo de Hola de nodos de Hola que tiene el clúster. Debe especificarse al menos un tipo de nodo de un clúster, tal y como se muestra en el siguiente fragmento de Hola. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

Hola **nombre** es Hola nombre descriptivo para este tipo de nodo concreto. toocreate un nodo de este tipo de nodo, asignar su nombre descriptivo toohello **elemento nodeTypeRef** variable para ese nodo, como se mencionó [anteriormente](#clusternodes). Para cada tipo de nodo, definir extremos de la conexión de Hola que va a utilizar. Puede elegir cualquier número de puerto para estos puntos de conexión, siempre que no entren en conflicto con otros puntos de conexión de este clúster. En un clúster de varios nodos, habrá uno o más nodos primarios (es decir, **isPrimary** establecido demasiado*true*), en función de hello [ **reliabilityLevel** ](#reliability). Lectura [consideraciones de planear la capacidad de clúster de Service Fabric](service-fabric-cluster-capacity.md) para obtener información sobre **nodeTypes** y **reliabilityLevel**y tooknow las principales y Hola tipos de nodos no principales. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>Los extremos utilizan tipos de nodos de hello tooconfigure
* *clientConnectionEndpointPort* es el puerto de hello usado Hola cliente tooconnect toohello el clúster, al usar las API de cliente de Hola. 
* *clusterConnectionEndpointPort* es el puerto de hello en el que los nodos de hello comunican entre sí.
* *leaseDriverEndpointPort* es el puerto de hello utilizada por hello clúster concesión controlador toofind out si nodos Hola siguen estando activos. 
* *serviceConnectionEndpointPort* es el puerto de hello usado por aplicaciones de Hola y servicios implementados en un nodo, toocommunicate con cliente de Service Fabric hello en ese nodo concreto.
* *httpGatewayEndpointPort* es el puerto de hello usado Hola Service Fabric Explorer tooconnect toohello clúster.
* *ephemeralPorts* invalidar hello [puertos dinámicos utilizados Hola OS](https://support.microsoft.com/kb/929851). Service Fabric utilizará una parte de ellos como puertos de la aplicación y Hola restantes estarán disponibles para hello SO. También asignará este intervalo toohello existente intervalo presente en Hola de sistema operativo, por lo que para todos los propósitos, se pueden usar intervalos de hello en archivos JSON de ejemplo de Hola. Debe asegurarse de que diferencia Hola entre puertos Hola y de inicio de hello es al menos de 255 toomake. Puede encontrarse con conflictos si esta diferencia es demasiado baja, ya que este intervalo se comparte con el sistema operativo de Hola. Ver el intervalo de puertos dinámicos de hello configurado ejecutando `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* son puertos Hola que se usará en las aplicaciones de Service Fabric Hola. intervalo de puertos de aplicación Hola debe ser el requisito de punto de conexión de hello toocover lo suficientemente grande como de las aplicaciones. Este intervalo debe ser exclusivo del intervalo de puertos dinámicos de hello en la máquina de hello, es decir, hello *ephemeralPorts* intervalo como se establece en la configuración de Hola.  Service Fabric utilizará estos siempre que los nuevos puertos son necesarios, así como tener cuidado de abrir firewall de Hola para estos puertos. 
* *reverseProxyEndpointPort* es un punto de conexión de proxy inverso opcional. Consulte [Proxy inverso de Service Fabric](service-fabric-reverseproxy.md) para más detalles. 

### <a name="log-settings"></a>Configuración del registro
Hola **fabricSettings** sección permite tooset Hola raíz directorios de datos de Service Fabric hello y registros. Puede personalizar estos solo durante la creación de clústeres inicial de Hola. Vea el siguiente fragmento de código de ejemplo de esta sección.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

Se recomienda usar una unidad no son de SO como hello FabricDataRoot y FabricLogRoot, ya que proporciona más confiabilidad frente a bloqueos de sistema operativo. Tenga en cuenta que si personaliza sólo la raíz de datos hello, a continuación, raíz de registro de hello se colocará un nivel por debajo de la raíz de datos de Hola.

### <a name="stateful-reliable-service-settings"></a>Configuración del servicio de confianza con estado
Hola **KtlLogger** sección permite tooset Hola configuración global de servicios de confianza. Para obtener más información sobre estas opciones, lea [Configurar Reliable Services con estado](service-fabric-reliable-services-configuration.md).
ejemplo de Hola siguiente muestra cómo toochange Hola Hola compartido registro de transacciones obtiene crea tooback las recopilaciones confiables para los servicios con estado.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Características complementarias
tooconfigure características del complemento, debe ser el elemento apiVersion de hello configurado como ' 04-2017' o superior y addonFeatures necesita toobe configurado:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Compatibilidad con los contenedores
tooenable compatibilidad con un contenedor para el contenedor de windows server y el contenedor de hyper-v para clústeres independientes, característica que hello 'DnsService' debe toobe habilitado.


## <a name="next-steps"></a>Pasos siguientes
Una vez que tenga un archivo ClusterConfig.JSON completo configurado según la configuración de clúster independiente, puede implementar su clúster mediante el siguiente artículo de hello [crear un clúster de Service Fabric independientes](service-fabric-cluster-creation-for-windows-server.md) y, a continuación, continuar demasiado[visualizar el clúster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

