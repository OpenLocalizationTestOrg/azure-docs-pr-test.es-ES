---
title: "solución de supervisión en Azure Log Analytics aaaContainer | Documentos de Microsoft"
description: "Hola solución de supervisión de contenedor en el análisis de registros le ayuda a ver y administrar el Docker y Windows hosts de contenedor en una sola ubicación."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Solución de Supervisión de contenedores de Azure Log Analytics

![Símbolo de Containers](./media/log-analytics-containers/containers-symbol.png)

Este artículo describe cómo tooset seguridad y el uso Hola solución de supervisión de contenedor en el análisis de registros, que le ayuda a ver y administrar el Docker y Windows hosts de contenedor en una sola ubicación. Docker es un sistema de virtualización de software que usa contenedores toocreate que automatizan la implementación de software tootheir TI infraestructura.

Hola solución se muestra qué contenedores se ejecutan, ¿qué imagen de contenedor que se está ejecutando, y donde se ejecutan los contenedores. Puede ver información de auditoría detallada que muestra los comandos que se usan con los contenedores. Además, puede solucionar los contenedores de visualización y búsqueda de registros centralizados sin necesidad de vista tooremotely Docker o hosts de Windows. Puede encontrar los contenedores que están causando ruido o realizando un consumo excesivo de recursos en un host. También puede ver la información centralizada acerca de la CPU, la memoria, el almacenamiento y el uso y el rendimiento de la red en relación con los contenedores. En equipos con Windows, puede centralizar y comparar registros de Windows Server, Hyper-V y contenedores de Docker. solución de Hello admite Hola después orchestrators de contenedor:

- Docker Swarm
- DC/OS
- kubernetes
- Service Fabric
- Red Hat OpenShift


Hello siguiente diagrama muestra las relaciones de hello entre varios hosts de contenedor y los agentes con OMS.

![Diagrama de contenedores](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>Requisitos del sistema

Antes de comenzar, revise Hola después tooverify detalles cumplen los requisitos previos de Hola.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Compatibilidad con solución de supervisión de contenedores para el orquestador y la plataforma de sistema operativo de Docker
Hello tabla siguiente se describe Hola orquestación de Docker y soporte técnico de inventario de contenedor, el rendimiento y los registros de análisis de registros de supervisión del sistema operativo.   

| | ACS | Linux | Windows | Contenedor<br>Inventario | Imagen<br>Inventario | Nodo<br>Inventario | Contenedor<br>Rendimiento | Contenedor<br>Evento | Evento<br>Registro | Contenedor<br>Registro |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Servicio<br>Fabric | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat Open<br>Shift | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(independiente) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Linux Server<br>(independiente) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Versiones de docker admitidas en Linux

- Docker 1.11 too1.13
- Docker CE y EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>Las distribuciones x64 de Linux se admiten como hosts de contenedor

- Ubuntu 14.04 LTS y 16.04 LTS
- CoreOS(stable)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 y 7.3
- SLES 12
- RHEL 7.2 y 7.3
- Red Hat OpenShift Container Platform (OCP) 3.4 y 3.5
- ACS Mesosphere DC/OS 1.7.3 too1.8.8
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>Sistemas operativos Windows compatibles

- Windows Server 2016
- Windows 10 Anniversary Edition (Professional o Enterprise)

### <a name="docker-versions-supported-on-windows"></a>Versiones de docker admitidas en Windows

- Docker de 1.12 y 1.13
- Docker 17.03.0 y versiones posteriores

## <a name="installing-and-configuring-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello después tooinstall de información y configurar soluciones de Hola.

1. Agregar Hola contenedor supervisión solución tooyour OMS área de trabajo de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).

2. Instalación y uso de Docker con un agente de OMS.  En función de su sistema operativo, puede elegir entre Hola siguientes métodos:

  * En sistemas operativos de Linux compatibles, instalar y ejecutar Docker y, a continuación, instalar y configurar hello [agente de OMS para Linux](log-analytics-agent-linux.md).  
  * En CoreOS, no se puede ejecutar Hola agente de OMS para Linux. En su lugar, ejecute una versión en contenedores de hello agente de OMS para Linux. Repase las secciones [Hosts de contenedores de Linux incluido CoreOS](#for-all-linux-container-hosts-including-coreos) o [Hosts de contenedores de Azure Government Linux incluidos CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) si va a trabajar con contenedores en la nube de Azure Government.
  * En Windows Server 2016 y Windows 10, instale Hola motor de Docker y el cliente, a continuación, una información de toogather de agente de conexión y envíelo tooLog análisis.  

### <a name="container-services"></a>Servicios de contenedor

- Si tiene un entorno de Red Hat OpenShift, consulte [Configuración de un agente de OMS para Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).
- Si tiene un clúster de Kubernetes con hello servicio de contenedor de Azure, consulte [supervisar un clúster de servicio de contenedor de Azure con Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).
- Si tiene un clúster DC/OS de Azure Container Service, obtenga más información en [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md) (Uso de Operations Management Suite para supervisar un clúster DC/OS de Azure Container Service).
- Si tiene un entorno en modo Docker Swarm, obtenga más información en [Configuración de un agente de OMS para Docker Swarm](#configure-an-oms-agent-for-docker-swarm).
- Si usa contenedores con Service Fabric, obtenga más información en [Información general de Azure Service Fabric ](../service-fabric/service-fabric-overview.md).
- Hola de revisión [Docker Engine en Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artículo para obtener información adicional acerca de cómo tooinstall y configurar los motores de Docker en equipos que ejecutan Windows.

> [!IMPORTANT]
> Debe ejecutar docker **antes de** instalar hello [agente de OMS para Linux](log-analytics-agent-linux.md) en los hosts de contenedor. Si ya ha instalado el agente de hello antes de instalar Docker, necesitará tooreinstall Hola agente de OMS para Linux. Para obtener más información sobre Docker, consulte hello [sitio Web de Docker](https://www.docker.com).


## <a name="linux-container-hosts"></a>Hosts de contenedores de Linux

Después de instalar a Docker, use Hola después de configuración para el agente de Hola de tooconfigure de host de contenedor para su uso con Docker. En primer lugar debe clave, que encontrará en el portal de Azure de Hola y el identificador de área de trabajo OMS. En el área de trabajo, haga clic en **inicio rápido** > **equipos** tooview su **Id. de área de trabajo** y **Primary Key**.  Copie y pegue ambos valores en el editor que prefiera.

### <a name="for-all-linux-container-hosts-except-coreos"></a>Para todos los hosts de contenedores de Linux excepto CoreOS

- Para obtener más información y pasos acerca de cómo tooinstall Hola agente de OMS para Linux, consulte [conectar su tooOperations de equipos Linux Management Suite (OMS)](log-analytics-agent-linux.md).

### <a name="for-all-linux-container-hosts-including-coreos"></a>Para todos los hosts de contenedores de Linux incluido CoreOS

Inicie el contenedor OMS de Hola que desea toomonitor. Modifique y use el siguiente ejemplo de Hola:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>Para todos los hosts de contenedores de Linux para Azure Government, incluido CoreOS

Inicie el contenedor OMS de Hola que desea toomonitor. Modifique y use el siguiente ejemplo de Hola:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>Cambio del uso de un tooone de agente de Linux instalado en un contenedor
Si anteriormente utilizaba agente instalado directamente de Hola y desea usar tooinstead un agente en el que se ejecuta en un contenedor, primero debe quitar Hola agente de OMS para Linux. Vea [Hola Desinstalar agente de OMS para Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand cómo desinstalar toosuccessfully Hola agente.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Configuración de un agente de OMS para Docker Swarm

Puede ejecutar Hola agente de OMS como un servicio global en Docker Swarm. Usar hello después información toocreate un servicio de agente de OMS. Deberá tooinsert el Id. de área de trabajo de OMS y la clave principal.

- Ejecute hello siguiente en el nodo principal de Hola.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Configuración de un agente de OMS para Red Hat OpenShift
Hay tres maneras tooadd Hola agente de OMS tooRed Hat OpenShift toostart recopilación contenedor datos de supervisión.

* [Instale Hola agente de OMS para Linux](log-analytics-agent-linux.md) directamente en cada nodo OpenShift  
* [Habilitar la extensión de máquina virtual de Log Analytics](log-analytics-azure-vm-extension.md) en cada nodo de OpenShift que reside en Azure  
* Instalar agente de OMS Hola como un conjunto de demonio OpenShift  

En esta sección trataremos Hola pasos necesarios tooinstall Hola agente de OMS como un conjunto de demonio OpenShift.  

1. Inicio de sesión toohello OpenShift nodo y copiar hello yaml archivo maestro [omsagent.yaml ocp](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) desde GitHub tooyour maestro de nodo y modificar valor de Hola por su identificador de área de trabajo de OMS y con la clave principal.
2. Ejecutar un proyecto de hello después toocreate de comandos para OMS y establecer la cuenta de usuario de Hola.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Hola toodeploy conjunto de demonio, ejecute la siguiente de hello:

    `oc create -f ocp-omsagent.yaml`

5. tooverify está configurado y funciona correctamente, escriba Hola siguiente:

    `oc describe daemonset omsagent`  

    y debe ser similar la salida de hello:

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

Si desea toouse secretos toosecure el Id. de área de trabajo de OMS y la clave principal al utilizar Hola agente de OMS demonio conjunto yaml archivo, realizar Hola pasos.

1. Inicio de sesión toohello OpenShift nodo y copiar hello yaml archivo maestro [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) y el secreto de generar script [secretgen.sh ocp](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) desde GitHub.  Esta secuencia de comandos generará el archivo de yaml de secretos de hello para el Id. de área de trabajo de OMS y la clave principal toosecure su secrete información.  
2. Ejecutar un proyecto de hello después toocreate de comandos para OMS y establecer la cuenta de usuario de Hola. Generar script de secreto de Hola solicita el identificador de área de trabajo de OMS <WSID> y la clave principal <KEY> y tras la finalización, se crea el archivo de ocp secret.yaml de Hola.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Implementar el archivo de secreto de hello ejecutando Hola siguiente:

    `oc create -f ocp-secret.yaml`

5. Comprobar la implementación mediante la ejecución Hola siguiente:

    `oc describe secret omsagent-secret`  

    y debe ser similar la salida de hello:  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Implementar archivo de conjunto de demonio yaml de agente de OMS hello ejecutando Hola siguiente:

    `oc create -f ocp-ds-omsagent.yaml`  

7. Comprobar la implementación mediante la ejecución Hola siguiente:

    `oc describe ds oms`

    y debe ser similar la salida de hello:

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Protección de la información secreta para Docker Swarm y Kubernetes

Puede proteger el identificador de área de trabajo y las claves principales de OMS para los servicios de contenedor de Docker Swarm y Kubernetes.

#### <a name="secure-secrets-for-docker-swarm"></a>Protección de secretos de Docker Swarm

Para Docker Swarm, una vez creado el secreto de hello para el Id. de área de trabajo y la clave principal, puede ejecutar Hola crear servicio de Docker de Hola para OMSagent. Usar hello después información toocreate la información secreta.

1. Ejecute hello siguiente en el nodo principal de Hola.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. Compruebe que los secretos se crearon correctamente.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. Hola ejecución después de comando toomount Hola secretos toohello en contenedores a agente de OMS.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>Protección de secretos de Kubernetes con archivos yaml

Para Kubernetes, se usa un archivo de script toogenerate Hola secretos yaml para el Id. de área de trabajo y la clave principal. En hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) página, hay archivos que se pueden utilizar con o sin la información secreta.

- Hola DaemonSet de agente OMS predeterminado no tiene información secreta (omsagent.yaml)
- archivo yaml de Hello DaemonSet de agente de OMS utiliza información secreta (omsagent-ds-secrets.yaml) con el archivo de generación secreto scripts toogenerate Hola secretos yaml (omsagentsecret.yaml).

Puede elegir toocreate omsagent DaemonSets con o sin secretos.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>Archivo yaml de DaemonSet de OMSagent predeterminado sin secretos

- Archivo yaml de hello predeterminado DaemonSet de agente de OMS, reemplace hello `<WSID>` y `<KEY>` tooyour WSID y la clave. Copie nodo maestro de hello archivo tooyour y siguiente ejecución hello:

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>Archivo yaml de DaemonSet de OMSagent predeterminado con secretos

1. toouse DaemonSet de agente de OMS con información secreta, cree primero los secretos de Hola.
    1. Copiar script de Hola y el archivo de plantilla secreto y asegúrese de que se encuentren en hello mismo directorio.
        - Script de generación de secretos: secret-gen.sh
        - Plantilla de secretos: secret-template.yaml
    2. Ejecutar script de Hola, como el siguiente ejemplo de Hola. script de Hola solicita Hola Id. de área de trabajo de OMS y la clave principal y después escribirlos, script de Hola crea un archivo de yaml secreto para que pueda ejecutar.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Crear pod de secretos de hello ejecutando Hola siguiente:
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify, ejecute hello siguiente:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        La salida debe ser similar a lo siguiente:

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        La salida debe ser similar a lo siguiente:

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. Ejecute ``` sudo kubectl create -f omsagent-ds-secrets.yaml ``` para crear el daemon-set de omsagent

2. Compruebe que hello que daemonset de agente de OMS se está ejecutando, toohello similar después de:

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Para Kubernetes, usar un archivo de yaml de secretos de secuencia de comandos toogenerate hello para el Id. de área de trabajo y la clave principal. Hola de uso después de la información de ejemplo con hello [omsagent yaml archivo](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure la información secreta.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a>Hosts de contenedores Windows

### <a name="preparation-before-installing-windows-agents"></a>Preparación antes de instalar agentes de Windows

Antes de instalar a agentes en equipos que ejecutan Windows, necesita servicio de Docker de tooconfigure Hola. configuración de Hello permite Hola Windows hello o agente de análisis de registros máquina virtual extensión toouse Hola socket de TCP de Docker para que los agentes de hello pueden acceder remotamente demonio de Docker de Hola y toocapture datos para la supervisión.

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker y compruebe su configuración

Hay pasos necesarios tooset seguridad TCP, canalización con nombre para Windows Server:

1. En Windows PowerShell, habilite la canalización TCP y la canalización con nombre.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. Configuración de Docker con el archivo de configuración de hello de canalización TCP y la canalización con nombre. archivo de configuración de Hola se encuentra en C:\ProgramData\docker\config\daemon.json.

    En el archivo de daemon.json hello, necesitará siguiente hello:

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

Para obtener más información acerca de la configuración del demonio de Docker de hello usado con contenedores de Windows, vea [Docker Engine en Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).


### <a name="install-windows-agents"></a>Instalación de agentes de Windows

tooenable Windows y supervisión, el contenedor de Hyper-V instala Hola Microsoft Monitoring Agent (MMA) en equipos de Windows que son hosts de contenedor. Para equipos que ejecutan Windows en su entorno local, vea [tooLog de equipos de Windows conectarse análisis](log-analytics-windows-agents.md). Para las máquinas virtuales ejecutan en Azure, conéctelos tooLog análisis con hello [extensión de máquina virtual](log-analytics-azure-vm-extension.md).

Puede supervisar los contenedores de Windows que se ejecutan en Service Fabric. Sin embargo, actualmente solo las [máquinas virtuales que se ejecutan en Azure](log-analytics-azure-vm-extension.md) y en [equipos Windows de su entorno local](log-analytics-windows-agents.md) son compatibles con Service Fabric.

Puede comprobar que la solución de supervisión de contenedor de hello está establecido correctamente para Windows. toocheck si el módulo de administración de hello era descarga correctamente, busque *ContainerManagement.xxx*. archivos de Hello deben estar en la carpeta C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs de Hola.


## <a name="solution-components"></a>Componentes de soluciones

Si está utilizando a Windows agentes, a continuación, hello siguiente módulo de administración se instala en cada equipo con un agente cuando se agrega esta solución. Ninguna configuración ni mantenimiento es necesario para el módulo de administración de Hola.

- *ContainerManagement.xxx* instalado en C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs

## <a name="container-data-collection-details"></a>Información detallada sobre la recopilación de datos en contenedores
Hola solución de supervisión de contenedor recopila diversos datos de registro y métricas de rendimiento de hosts de contenedor y los contenedores con agentes que se activan.

Datos se recopilan cada tres minutos por hello siguientes tipos de agente.

- [Agente de OMS para Linux](log-analytics-linux-agents.md)
- [Agente de Windows](log-analytics-windows-agents.md)
- [Extensión de VM de Log Analytics](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>Registros de contenedor

Hello siguiente tabla muestran ejemplos de registros recopilados por la solución de supervisión de contenedor de Hola y tipos de datos de Hola que aparecen en los resultados de búsqueda de registros.

| Tipo de datos | Tipo de datos en la búsqueda de registros | Fields |
| --- | --- | --- |
| Rendimiento de hosts y contenedores | `Type=Perf` | Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem |
| Inventario de contenedor | `Type=ContainerInventory` | TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID |
| Inventario de imágenes de contenedor | `Type=ContainerImageInventory` | TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer |
| Registro de contenedor | `Type=ContainerLog` | TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID |
| Registro del servicio de contenedores | `Type=ContainerServiceLog`  | TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID |
| Inventario de nodo de contenedor | `Type=ContainerNodeInventory_CL`| TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Inventario de Kubernetes | `Type=KubePodInventory_CL` | TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| Proceso del contenedor | `Type=ContainerProcess_CL` | TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| Eventos de Kubernetes | `Type=KubeEvents_CL` | TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message |

Las etiquetas se anexan demasiado*PodLabel* tipos de datos son sus propias etiquetas personalizadas. Hello anexadas etiquetas PodLabel se muestra en la tabla de hello son ejemplos. Por lo tanto, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` se diferencian en el conjunto de datos de su entorno y genéricamente son similares a `PodLabel_yourlabel_s`.


## <a name="monitor-containers"></a>Supervisión de contenedores
Una vez haya solución Hola habilitada en el portal de OMS hello, Hola **contenedores** icono muestra información de resumen sobre los hosts de contenedor y los contenedores de Hola que se ejecutan en hosts.

![Icono de Containers](./media/log-analytics-containers/containers-title.png)

icono de Hello muestra un resumen de cuántos contenedores tiene en entorno de Hola y si está error, ejecución o detenido.

### <a name="using-hello-containers-dashboard"></a>Utilizando el panel de contenedores de Hola
Haga clic en hello **contenedores** icono. Desde allí verá las vistas organizadas por:

- **Eventos de contenedor**: muestra el estado de contenedor y los equipos con contenedores en estado de error.
- **Registros de contenedor** -muestra un gráfico de los archivos de registro de contenedor generados con el tiempo y una lista de equipos con mayor número de archivos de registro de hello.
- **Eventos de Kubernetes** -muestra un gráfico de eventos de Kubernetes generados con el tiempo y una lista de motivos de hello ¿por qué pod genera eventos de Hola. *Este conjunto de datos solo se usa en entornos Linux.*
- **Inventario de Namespace Kubernetes** : muestra el número de Hola de espacios de nombres y cajas de y muestra su jerarquía. *Este conjunto de datos solo se usa en entornos Linux.*
- **Inventario de nodo de contenedor** -muestra hello número de tipos de orquestación usada en nodos/hosts del contenedor. nodos del equipo Hola/hosts también se enumeran por número de Hola de contenedores. *Este conjunto de datos solo se usa en entornos Linux.*
- **Inventario de imágenes de contenedor** -muestra el número total de Hola de imágenes de contenedor que se utilizan y el número de tipos de imagen. número de Hola de imágenes también se muestran por etiqueta de imagen de Hola.
- **Estado de contenedores** -muestra el número total de hello del contenedor de equipos de host/nodos que tienen contenedores en ejecución. También se muestran los equipos por número de Hola de hosts en ejecución.
- **Procesos del contenedor**: muestra un gráfico de líneas de procesos de contenedor en ejecución a lo largo del tiempo. También se enumeran los contenedores según los comandos o procesos en ejecución en los contenedores. *Este conjunto de datos solo se usa en entornos Linux.*
- **Rendimiento de la CPU de contenedor** -muestra un gráfico de líneas Hola promedio de uso de CPU con el tiempo para hosts de nodos de equipo. También listas Hola equipo/hosts de nodos se basan en Media de la CPU.
- **Rendimiento de la memoria del contenedor**: muestra un gráfico de líneas del uso de memoria a lo largo del tiempo. También muestra el uso de memoria de los equipos según el nombre de la instancia.
- **Rendimiento del equipo** -muestra el porcentaje de uso de memoria con el tiempo y megabytes de espacio libre en disco de gráficos de líneas de porcentaje de Hola de rendimiento de la CPU con el tiempo, con el tiempo. Puede mantener el mouse sobre cualquier línea de un gráfico tooview más detalles.


Cada área del panel de hello es una representación visual de una búsqueda que se ejecuta en los datos recopilados.

![Panel Containers](./media/log-analytics-containers/containers-dash01.png)

![Panel Containers](./media/log-analytics-containers/containers-dash02.png)

Hola **estado de contenedor** área, haga clic en la parte superior de hello, tal y como se muestra a continuación.

![Estado de los contenedores](./media/log-analytics-containers/containers-status.png)

Búsqueda de registros, se muestra información sobre el estado de saludo de los contenedores.

![Búsqueda de registros para contenedores](./media/log-analytics-containers/containers-log-search.png)

Desde aquí, puede editar toomodify de consulta de búsqueda de hello, información específica de toofind Hola que le interesa. Para más información acerca del uso de la búsqueda de registros, consulte [Búsquedas de registros en Log Analytics](log-analytics-log-searches.md).

## <a name="troubleshoot-by-finding-a-failed-container"></a>Solución de problemas mediante la búsqueda de un contenedor con error

Log Analytics marca un contenedor como **Failed** (Error) si ha terminado con un código de salida distinto de cero. Puede ver un resumen de errores de Hola y errores en el entorno de Hola Hola **contenedores no se pudo** área.

### <a name="toofind-failed-containers"></a>toofind no se pudo contenedores
1. Haga clic en hello **estado de contenedor** área.  
   ![estado de los contenedores](./media/log-analytics-containers/containers-status.png)
2. Búsqueda de registros se abre y muestra el estado de Hola de los contenedores, toohello similar después.  
   ![estado de los contenedores](./media/log-analytics-containers/containers-log-search.png)
3. A continuación, haga clic en el valor de hello agregado de información adicional de errores contenedores tooview. Expanda **mostrar más** imagen de identificador hello tooview.  
   ![contenedores con errores](./media/log-analytics-containers/containers-state-failed.png)  
4. A continuación, escriba el siguiente de hello en la consulta de búsqueda de Hola. `Type=ContainerInventory <ImageID>`toosee los detalles acerca de la imagen de hello como tamaño de la imagen y el número de imágenes detenidas pero no lo consiguió.  
   ![contenedores con errores](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>Registros de búsqueda de datos de contenedor
Cuando esté solucionando problemas de un error específico, puede ayudar a toosee donde se lleva a cabo en su entorno. Hola siguientes tipos de registro le ayudará a crear consultas de información de hello tooreturn que desee.


- **ContainerImageInventory** : Utilice este tipo si está tratando de información de toofind organizada por información de la imagen de imagen y tooview como identificadores de imagen o tamaños.
- **ContainerInventory**: use este tipo si desea obtener información sobre la ubicación del contenedor, cuáles son sus nombres y qué imágenes se están ejecutando.
- **ContainerLog** : Use este tipo cuando se desea información de registro de toofind específica del error y las entradas.
- **ContainerNodeInventory_CL** usar este tipo cuando desee Hola información acerca de host/nodo donde se encuentran los contenedores. Proporciona información sobre la versión de Docker, el tipo de orquestación, almacenamiento y red.
- **ContainerProcess_CL** Utilice este tipo tooquickly consulte proceso Hola que se ejecuta en el contenedor de Hola.
- **ContainerServiceLog** : Use este tipo al que está tratando de información de pista de auditoría de toofind para hello demonio de Docker, como iniciar, detener, eliminar o comandos de extracción.
- **KubeEvents_CL** usar esta tipo toosee hello Kubernetes los eventos.
- **KubePodInventory_CL** usar este tipo si desea información de jerarquía de clúster de toounderstand Hola.


### <a name="toosearch-logs-for-container-data"></a>toosearch registros de datos del contenedor
* Elija una imagen que sabe que no ha funcionado recientemente y buscar registros de errores de Hola para ellos. Para empezar, busque un nombre de contenedor que esté ejecutando esa imagen con una búsqueda **ContainerInventory**. Por ejemplo, busque `Type=ContainerInventory ubuntu Failed`.  
    ![Búsqueda de contenedores de Ubuntu](./media/log-analytics-containers/search-ubuntu.png)

  Hola a continuación el nombre del contenedor de hello demasiado**nombre**y busque los registros. En este ejemplo, es `Type=ContainerLog cranky_stonebreaker`.

**Ver información de rendimiento**

Cuando está empezando tooconstruct consultas, puede ayudar a toosee lo que es posible en primer lugar. Por ejemplo, toosee buscar todos los datos de rendimiento, intente una amplia consulta escribiendo Hola después de consultar.

```
Type=Perf
```

![rendimiento de contenedores](./media/log-analytics-containers/containers-perf01.png)

Puede definir el ámbito de los datos de rendimiento de Hola que está viendo contenedor específico tooa escribiendo el nombre de hello del mismo toohello derecha de la consulta.

```
Type=Perf <containerName>
```

Que muestra la lista de Hola de métricas de rendimiento que se recopilan para un contenedor por separado.

![rendimiento de contenedores](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>Ejemplos de consultas de búsqueda de registros
A menudo útil toobuild su consulta a partir de un ejemplo o dos y, a continuación, modificándolos toofit su entorno. Como punto de partida, puede experimentar con hello **consultas de ejemplo** toohelp de área se generan las consultas más avanzadas.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas de contenedores](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>Guardado de consultas de búsqueda de registros
El guardado de consultas es una característica estándar de Log Analytics. Guárdelas para volver a usar en el futuro aquellas que haya encontrado más útiles.

Después de crear una consulta que encuentre útil, puede guardarlo si hace clic **favoritos** al principio de Hola de página de búsqueda de registros de Hola. A continuación, se puede acceder fácilmente a ella más adelante desde hello **Mi panel** página.

## <a name="next-steps"></a>Pasos siguientes
* [Buscar registros](log-analytics-log-searches.md) tooview obtener registros de datos del contenedor.
