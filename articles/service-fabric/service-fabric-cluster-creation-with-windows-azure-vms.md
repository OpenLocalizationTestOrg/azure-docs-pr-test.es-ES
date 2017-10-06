---
title: "aaaCreate una independiente del clúster con máquinas virtuales de Azure que ejecutan Windows | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y administrar un clúster de Azure Service Fabric en máquinas virtuales de Azure con Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server (Creación de un clúster independiente de tres nodos de Service Fabric con máquinas virtuales de Azure con Windows Server)
Este artículo describe cómo toocreate un clúster en Windows Azure máquinas virtuales (VM), usar Hola instalador independiente de Service Fabric para Windows Server. escenario de Hello es un caso especial de [crear y administrar un clúster que se ejecuta en Windows Server](service-fabric-cluster-creation-for-windows-server.md) donde son máquinas virtuales de hello [máquinas virtuales de Azure que ejecuta Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json); sin embargo, no está creando [un Azure clúster basado en la nube de Service Fabric](service-fabric-cluster-creation-via-portal.md). distinción de Hello en seguir este patrón es ese clúster de Service Fabric Hola independiente creado por hello pasos completamente administrado por usted, mientras que administra y actualizar Hola Service Fabric Hola clústeres de Azure en la nube Service Fabric proveedor de recursos.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Clúster de pasos toocreate Hola independiente
1. Inicie sesión en toohello portal de Azure y cree un nuevo Windows Server 2012 R2 Datacenter o máquina virtual de Windows Server 2016 centro de datos en un grupo de recursos. Leer el artículo de hello [crear una VM de Windows en el portal de Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obtener más detalles.
2. Agregar un par toohello máquinas virtuales más mismo grupo de recursos. Asegúrese de que cada una de las máquinas virtuales de hello ha Hola mismo nombre de usuario administrador y la contraseña cuando se crea. Una vez creados, debería ver todas las máquinas tres virtuales Hola misma red virtual.
3. Conectar tooeach de hello las máquinas virtuales y desactivar Hola Firewall de Windows con hello [administrador del servidor, el panel de servidor Local](https://technet.microsoft.com/library/jj134147.aspx). Esto garantiza que el tráfico de red Hola puede comunicarse entre máquinas Hola. Al equipo tooeach conectado, obtener dirección IP de hello, abra un símbolo del sistema y escriba `ipconfig`. También puede ver Hola IP dirección de cada máquina en el portal de hello, seleccionando el recurso de red virtual de hello para el grupo de recursos de Hola y comprobación de interfaces de red de hello creadas para cada una de estas máquinas.
4. Conecte tooone de hello las máquinas virtuales y prueba que puede hacer ping Hola otros dos máquinas virtuales correctamente.
5. Conectar tooone de hello las máquinas virtuales y [Descargar paquete de Service Fabric Hola independiente para Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) en una carpeta nueva en hello automático y extraer el paquete de saludo.
6. Abra hello *ClusterConfig.Unsecure.MultiMachine.json* un archivo en el Bloc de notas y editar cada nodo con las direcciones IP de máquinas de Hola Hola tres. Cambiar nombre de clúster de hello en la parte superior de Hola y guarde el archivo hello.  A continuación, se muestra un ejemplo parcial Hola del manifiesto de clúster.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Si piensa que este toobe un clúster segura, decidir medida de seguridad de Hola que cabe como toouse y siga los pasos de Hola de hello asociados vínculo: [X509 certificado](service-fabric-windows-cluster-x509-security.md) o [la seguridad de Windows](service-fabric-windows-cluster-windows-security.md). Si la configuración de clúster de hello mediante la seguridad de Windows, deberá tooset seguridad un toomanage de controlador de dominio Active Directory. Tenga en cuenta no se admite el uso de una máquina de controlador de dominio como un nodo de Service Fabric.
8. Abra una [ventana de PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Desplazarse por las carpetas de toohello donde extrajo el paquete del instalador independiente descargado hello y había guarda el archivo de configuración del clúster de Hola. Ejecute hello después de clúster de Hola de toodeploy de comandos de PowerShell:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

script de Hola configura cada clúster de Service Fabric Hola de manera remota y debe notificar el progreso como implementación pone a través de.

9. Después de aproximadamente un minuto, puede comprobar si el clúster de hello esté operativo conectándose toohello Service Fabric Explorer utilizando uno de la dirección IP de la máquina de hello direcciones, por ejemplo mediante el uso de `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Pasos siguientes
* [Creación de clústeres independientes de Service Fabric en Windows Server o Linux](service-fabric-deploy-anywhere.md)
* [Agregar o quitar el clúster de Service Fabric de nodos tooa independiente](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Opciones de configuración de clústeres de Windows independientes](service-fabric-cluster-manifest.md)
* [Proteger un clúster independiente en Windows mediante la seguridad de Windows](service-fabric-windows-cluster-windows-security.md)
* [Protección de un clúster de Windows independiente mediante certificados](service-fabric-windows-cluster-x509-security.md)

