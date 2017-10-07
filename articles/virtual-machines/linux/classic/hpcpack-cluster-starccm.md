---
title: "aaaRun estrella-CCM + con HPC Pack en máquinas virtuales de Linux | Documentos de Microsoft"
description: "Implemente un clúster de Microsoft HPC Pack en Azure y ejecute un trabajo STAR-CCM+ en varios nodos de proceso Linux en una red RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Ejecución de STAR-CCM+ con Microsoft HPC Pack en un clúster de Linux RDMA en Azure
Este artículo muestra cómo agrupar toodeploy un Microsoft HPC Pack en Azure y se ejecuta un [CD-adapco estrella-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) trabajo en varios nodos de ejecución de Linux que se interconectan con InfiniBand.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Microsoft HPC Pack proporciona características toorun una variedad de HPC a gran escala y aplicaciones en paralelo, incluidas las aplicaciones de MPI, acerca de los clústeres de máquinas virtuales de Microsoft Azure. HPC Pack también admite la ejecución de aplicaciones Linux HPC en máquinas virtuales de nodos de proceso Linux implementadas en un clúster de HPC Pack. Para nodos con HPC Pack de ejecución de un toousing Introducción Linux, consulte [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).

## <a name="set-up-an-hpc-pack-cluster"></a>Configuración de un clúster de HPC Pack
Descargar scripts de implementación de IaaS de HPC Pack Hola de hello [centro de descarga de](https://www.microsoft.com/en-us/download/details.aspx?id=44949) y extráigalos localmente.

Azure PowerShell es un requisito previo. Si PowerShell no está configurado en el equipo local, lea el artículo de hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

En tiempo de Hola de redactar este artículo, las imágenes de Linux de Hola de hello Azure Marketplace (que contiene controladores de InfiniBand Hola de Azure) son para SLES 12, CentOS 6.5 y CentOS 7.1. En este artículo se basa en el uso de Hola de SLES 12. nombre de hello tooretrieve de todas las imágenes de Linux compatibles con HPC en hello Marketplace, puede ejecutar Hola siguiente comando de PowerShell:

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

la salida de Hello muestra la ubicación de hello en el que están disponibles estas imágenes y Hola nombre de imagen (**ImageName**) toobe utilizado en la plantilla de implementación de hello más tarde.

Antes de implementar el clúster de hello, tendrá toobuild un archivo de plantilla de implementación de HPC Pack. Dado que estamos usando como objetivo un clúster pequeño, nodo principal de Hola se controlador de dominio de Hola y hospedar una base de datos local de SQL.

Hello plantilla siguiente se implementa este tipo de nodo principal, cree un archivo XML denominado **MyCluster.xml**y reemplace los valores de hello de **SubscriptionId**, **StorageAccount**,  **Ubicación**, **VMName**, y **ServiceName** con la suya.

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

Iniciar la creación del nodo principal de hello mediante la ejecución de comandos de PowerShell de hello en un símbolo del sistema con privilegios elevados:

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

Después de 20 minutos de too30, nodo principal de hello debería estar listo. Puede conectarse tooit desde Hola portal de Azure, haga clic en hello **conectar** icono de la máquina virtual de Hola.

Finalmente, es posible que tenga el reenviador de DNS de toofix Hola. toodo por lo tanto, inicie el Administrador de DNS.

1. Nombre del servidor secundario hello en el Administrador de DNS, seleccione **propiedades**y, a continuación, haga clic en hello **reenviadores** ficha.
2. Haga clic en hello **editar** tooremove los reenviadores y, a continuación, haga clic en **Aceptar**.
3. Asegúrese de que ese hello **usar sugerencias de raíz si los reenviadores no están disponibles** casilla de verificación está seleccionada y, a continuación, haga clic en **Aceptar**.

## <a name="set-up-linux-compute-nodes"></a>Configuración de nodos de proceso Linux
Implementar nodos de proceso de hello Linux mediante Hola misma plantilla de implementación que ha usado el nodo principal de toocreate Hola.

Archivo de copia hello **MyCluster.xml** desde el nodo principal de equipo local toohello y actualización hello **NodeCount** etiquetar con número de Hola de nodos que desea toodeploy (< = 20). Ser toohave cuidado suficientes núcleos disponibles en su cuota de Azure, ya que cada instancia A9 consumirá 16 núcleos en su suscripción. Puede usar instancias de A8 (8 núcleos) en lugar de A9 si desea toouse más máquinas virtuales en hello mismo presupuesto.

En el nodo principal de hello, copie los scripts de implementación de IaaS de HPC Pack Hola.

Ejecute hello siga los comandos de PowerShell de Azure en un símbolo del sistema con privilegios elevados:

1. Ejecutar **Add-AzureAccount** tooconnect tooyour suscripción de Azure.
2. Si tiene varias suscripciones, ejecute **Get-AzureSubscription** toolist ellos.
3. Establezca una suscripción de manera predeterminada, ejecute hello **Select-AzureSubscription - SubscriptionName xxxx-predeterminado** comando.
4. Ejecutar **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart implementar nodos de proceso de Linux.
   
   ![Implementación del nodo principal en acción][hndeploy]

Abra la herramienta de administrador de clústeres de HPC Pack Hola. Después de algunos minutos, normalmente los nodos de proceso Linux aparecerán en la lista de nodos de proceso del clúster. Con el modo de implementación clásica de hello, las máquinas virtuales IaaS se crean secuencialmente. Por lo que si el número de Hola de nodos es importante, obtenerlas todos implementado pueden tardar una cantidad considerable de tiempo.

![Nodos Linux en el administrador de clústeres de HPC Pack][clustermanager]

Ahora que todos los nodos están activados y ejecutándose en el clúster de hello, hay toomake de configuración de infraestructura adicionales.

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>Configuración de un recurso compartido de archivos de Azure para nodos Linux y Windows
Puede utilizar secuencias de comandos de toostore de servicios de archivos de Azure de hello, paquetes de aplicaciones y archivos de datos. El servicio de archivos de Azure proporciona funcionalidades CIFS en el almacenamiento de blobs de Azure como un almacén persistente. Tenga en cuenta que esto no es la solución más escalable de hello, pero es hello uno más simple y no requiere máquinas virtuales dedicadas.

Crear un recurso compartido de archivos de Azure siguiendo las instrucciones de hello en el artículo hello [Introducción al almacenamiento de archivos de Azure en Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).

Mantenga Hola nombre de la cuenta de almacenamiento como **saname**, nombre de recurso compartido de archivo hello como **sharename**y la clave de cuenta de almacenamiento de hello como **sakey**.

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>Montar el recurso compartido de archivos de Azure de hello en el nodo principal de Hola
Abra un símbolo del sistema con privilegios elevados y ejecute hello siguiendo las credenciales de comando toostore hello en el almacén del equipo local de hello:

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

A continuación, toomount hello Azure recurso compartido de archivos, ejecute:

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Montar el recurso compartido de archivos de Azure de hello en nodos de proceso de Linux
Una útil herramienta que se incluye con HPC Pack es Hola clusrun. Puede usar este Hola de toorun de herramienta de línea de comandos mismo comando simultáneamente en un conjunto de nodos de proceso. En nuestro caso, se ha utilizado el recurso compartido de archivos de Azure de Hola de toomount y enviarlo toosurvive reinicios.
En un símbolo con privilegios elevados en el nodo principal de hello, ejecute hello siga los comandos.

directorio de montaje de Hola toocreate:

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

Hola toomount recurso compartido de archivos de Azure:

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

recurso compartido de toopersist Hola montaje:

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>Instalación de STAR-CCM+
Las instancias A8 y A9 de máquina virtual de Azure proporcionan compatibilidad con InfiniBand y funcionalidad de RDMA. controladores de kernel de Hola que permiten estas capacidades están disponibles para Windows Server 2012 R2, SUSE 12, CentOS 6.5 e imágenes de CentOS 7.1 en hello Azure Marketplace. Microsoft MPI y MPI Intel (versión 5.x) son dos bibliotecas de MPI de Hola que admiten estos controladores en Azure.

Se incluyen CD-Adapco StarCCM+ versión 11.x y posteriores con la versión 5.x de Intel MPI, por lo que se proporciona compatibilidad con InfiniBand para Azure.

Obtener hello Linux64 estrella-CCM + paquete de hello [CD-adapco portal](https://steve.cd-adapco.com). En nuestro caso, se usa la versión 11.02.010 en precisión mixta.

En el nodo principal de hello, Hola **/hpcdata** archivos de Azure compartir, cree un script de shell denominado **setupstarccm.sh** con hello siguen contenido. Este script se ejecutará en cada tooset de nodo de proceso una estrella-CCM + localmente.

#### <a name="sample-setupstarcmsh-script"></a>Script setupstarcm.sh de ejemplo
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
Ahora, tooset una estrella-CCM + en todos los Linux nodos de proceso, abra un símbolo del sistema con privilegios elevados y ejecute hello siguiente comando:

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Mientras se ejecuta el comando de hello, puede supervisar el uso de CPU de hello mediante mapa térmico de hello del Administrador de clústeres. Tras unos minutos todos los nodos deberían estar correctamente configurados.

## <a name="run-star-ccm-jobs"></a>Ejecución de trabajos de STAR-CCM+
HPC Pack se utiliza para sus capacidades de programador de trabajo en orden toorun estrella-CCM + trabajos. toodo por lo tanto, se necesitamos Hola soporte técnico de algunos scripts que son utilizados toostart trabajo de Hola y ejecute estrella-CCM +. datos de entrada de Hola se mantienen en el recurso compartido de archivos de Azure de hello primeros por simplicidad.

Hola siguiente script de PowerShell es tooqueue usa una estrella-CCM + trabajo. Toma tres argumentos:

* nombre del modelo Hola
* número de Hola de toobe de nodos que se usa
* número de Hola de núcleos en cada toobe de nodo que se usa

Dado que estrella-CCM + puede rellenar ancho de banda de memoria de hello, es mejor toouse menos núcleos por nodos de proceso y agregar nuevos nodos. Hola número exacto de núcleos por nodo dependerá de familia del procesador hello y velocidad de interconexión de Hola.

nodos de Hola se asignan exclusivamente para el trabajo de hello y no puede compartirse con otros trabajos. trabajo de Hello no se inicia como un trabajo de MPI directamente. Hola **runstarccm.sh** secuencia de comandos de shell iniciará el selector MPI Hola.

Hola entrada hello y modelo **runstarccm.sh** script se almacenan en hello **/hpcdata** recurso compartido al que previamente se ha montado.

Archivos de registro se denominan con el Id. de trabajo de Hola y se almacenan en hello **/hpcdata share**, junto con hello estrella-CCM + archivos de salida.

#### <a name="sample-submitstarccmjobps1-script"></a>Script SubmitStarccmJob.ps1 de ejemplo
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
Reemplace **runner.java** por el iniciador de modelo Java de STAR-CCM+ y el código de registro que prefiera.

#### <a name="sample-runstarccmsh-script"></a>Script runstarccm.sh de ejemplo
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

En nuestra prueba, se ha utilizado un token de licencia Power-On-Demand. Para ese token, deberá hello tooset **$CDLMD_LICENSE_FILE** variable de entorno demasiado **1999@flex.cd-adapco.com**  y la clave de Hola Hola **- podkey** opción de línea de comandos de Hola .

Después de algunas operaciones de inicialización, el script de Hola extrae--hello **CCP_NODES_CORES $** variables de entorno que establezca HPC Pack: Hola lista de toobuild de nodos que se usa un archivo de host que Hola selector MPI. Este archivo de host contendrá la lista de Hola de nombres del nodo de proceso que se usan para el trabajo de hello, un nombre por línea.

formato de Hola de **CCP_NODES_CORES $** sigue este patrón:

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

Donde:

* `<Number of nodes>`es el número de Hola de nodos asignados toothis trabajo.
* `<Name of node_n_...>`es el nombre de Hola de cada nodo asignada toothis trabajo.
* `<Cores of node_n_...>`es el número de Hola de núcleos en el nodo de hello asignada toothis trabajo.

número de núcleos de Hola (**$NBCORES**) también es calculada hello en función de número de nodos (**$NBNODES**) y Hola número de núcleos por nodo (proporcionado como parámetro **$NBCORESPERNODE**).

Para ver opciones de MPI hello, hello las que se utilizan con Intel MPI en Azure son:

* `-mpi intel`toospecify MPI de Intel.
* `-fabric UDAPL`toouse Azure InfiniBand verbos.
* `-cpubind bandwidth,v`ancho de banda de toooptimize de MPI con estrella-CCM +.
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI trabajar con Azure InfiniBand y tooset Hola requiere el número de núcleos por nodo.
* `-batch`toostart estrella-CCM + en modo por lotes con ninguna interfaz de usuario.

Por último, toostart un trabajo, asegúrese de que los nodos estén en ejecución y que están en línea en el Administrador de clústeres. Después, desde un símbolo del sistema de PowerShell, ejecute esto:

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>Detención de nodos
Más adelante cuando haya terminado con las pruebas, puede usar hello después toostop de comandos de PowerShell de HPC Pack e iniciar nodos:

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>Pasos siguientes
Pruebe a ejecutar otras cargas de trabajo Linux. Por ejemplo, consulte:

* [Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure](hpcpack-cluster-namd.md)
* [Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
