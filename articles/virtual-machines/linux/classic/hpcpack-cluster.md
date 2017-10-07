---
title: "aaaLinux compute máquinas virtuales en un clúster de HPC Pack | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y use un módulo de HPC cluster en Azure para las cargas de trabajo (HPC) de informática de alto rendimiento de Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure
Configure un clúster de [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) en Azure que contenga un nodo principal en el que se ejecute Windows Server y varios nodos de proceso en los que se ejecute una distribución de Linux compatible. Explorar opciones toomove datos entre nodos de Linux de Hola y el nodo principal de Windows hello de clúster de Hola. Obtenga información acerca de cómo toosubmit Linux HPC trabajos toohello clúster.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

En un nivel alto, hello siguiente diagrama muestra clúster de HPC Pack Hola crear y trabajar con.

![Clúster de HPC con nodos de Linux][scenario]

Para otro toorun opciones Linux HPC cargas de trabajo en Azure, consulte [recursos técnicos para el lote e informática de alto rendimiento](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Implementación de un clúster de HPC Pack con nodos de proceso de Linux
Este artículo muestra dos opciones toodeploy un clúster de HPC Pack en Azure con nodos de proceso de Linux. Los dos métodos utilizan una imagen de Marketplace de Windows Server con el nodo principal de HPC Pack toocreate Hola. 

* **Plantilla de administrador de recursos de Azure** -utilizar una plantilla de hello Azure Marketplace o una plantilla de inicio rápido de comunidad de hello, creación de tooautomate de clúster de hello en el modelo de implementación del Administrador de recursos de Hola. Por ejemplo, hello [clúster de HPC Pack para cargas de trabajo de Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) plantilla en hello Azure Marketplace crea una infraestructura de clúster de HPC Pack completa para Linux HPC las cargas de trabajo.
* **Script de PowerShell** -Hola de uso [script de implementación de Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate una implementación de clúster completa en el modelo de implementación clásica de Hola. Este script de PowerShell de Azure usa una imagen de máquina virtual de HPC Pack en hello Azure Marketplace para la implementación rápida y proporciona un conjunto completo de toodeploy de parámetros de configuración de nodos de proceso de Linux.

Para obtener más información acerca de las opciones de implementación de clúster de HPC Pack en Azure, consulte [opciones toocreate y administrar clústeres de informática de alto rendimiento (HPC) en Azure con Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Requisitos previos
* **Suscripción de Azure** -puede usar una suscripción en cualquier servicio Global de Azure o Azure China Hola. En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos.
* **Cuota de núcleos** -podría necesita tooincrease Hola cuota de núcleos, especialmente si elige toodeploy varios nodos de clúster con tamaños de máquinas virtuales con varios núcleos. tooincrease una cuota, abra una solicitud de soporte técnico al cliente en línea sin coste adicional.
* **Las distribuciones de Linux** -actualmente HPC Pack admite Hola siguiendo las distribuciones de Linux para nodos de proceso. Puede usar versiones de Marketplace de estas distribuciones cuando estén disponibles o proporcionar las suyas.
  
  * **Basado en CentOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC y 7.1 HPC
  * **Red Hat Enterprise Linux**: 6.7, 6.8 y 7.2
  * **SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 para HPC y SLES 12 para HPC (Premium)
  * **Ubuntu Server**: 14.04 LTS y 16.04 LTS
    
    > [!TIP]
    > red de toouse Hola RDMA de Azure con uno de los tamaños de VM Hola compatibles con RDMA, especifique una imagen de SUSE Linux Enterprise Server 12 HPC o basado en CentOS HPC de hello Azure Marketplace. Para más información, consulte [Tamaños de máquina virtual de procesos de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Clúster de Hola de toodeploy de requisitos previos adicionales mediante el uso de script de implementación de IaaS de HPC Pack hello:

* **Equipo cliente** -necesita un script de implementación de cliente basada en Windows equipo toorun Hola clúster.
* **Azure PowerShell** - [instale y configure Azure PowerShell](/powershell/azure/overview) (versión 0.8.10 o posterior) en el equipo cliente.
* **Script de implementación de IaaS de HPC Pack** : Descargue y descomprima la versión más reciente de Hola de script de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Puede comprobar Hola versión del script de Hola ejecutando `.\New-HPCIaaSCluster.ps1 –Version`. En este artículo se basa en la versión 4.4.1 o posterior del script de Hola.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Opción de implementación 1. Usar una plantilla de Resource Manager
1. Vaya toohello [clúster de HPC Pack para cargas de trabajo de Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) plantilla en hello Azure Marketplace y haga clic en **implementar**.
2. Hola portal de Azure, revise la información de hello y, a continuación, haga clic en **crear**.
   
    ![Creación del portal][portal]
3. En hello **Fundamentos** hoja, escriba un nombre para el clúster de hello, que también nombres de máquina virtual del nodo principal Hola. Puede elegir un grupo de recursos existente o crear un grupo para la implementación de hello en una ubicación que sea tooyou disponible. Hello ubicación afecta a la disponibilidad de Hola de determinados tamaños de máquina virtual y otros servicios de Azure (consulte [productos disponibles por región](https://azure.microsoft.com/regions/services/)).
4. En hello **principal de la configuración del nodo** hoja, para una implementación de la primera, por lo general puede aceptar valores predeterminados de Hola. 
   
   > [!NOTE]
   > Hola **URL de script posterior a la configuración de** es opcional establecer toospecify una secuencia de comandos de Windows PowerShell disponible públicamente que desea toorun en la máquina virtual del nodo principal Hola después de que se está ejecutando. 
   > 
   > 
5. En hello **configuración de nodo de proceso** hoja, seleccione un modelo de nomenclatura para los nodos de hello, número de Hola y tamaño de los nodos de Hola y Hola toodeploy de distribución de Linux.
6. En hello **configuración de infraestructura** hoja, escribe los nombres de red virtual de Hola y Active Directory dominio, dominio y las credenciales de administrador de máquina virtual y un patrón de nomenclatura para las cuentas de almacenamiento de Hola.
   
   > [!NOTE]
   > HPC Pack utiliza usuarios de clústeres de tooauthenticate de dominio de Active Directory de Hola. 
   > 
   > 
7. Después de ejecutarán pruebas de validación de Hola y revise los términos de Hola de uso, haga clic en **compra**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Opción de implementación 2. Usar script de implementación de IaaS de Hola
Siguientes son requisitos previos adicionales con toodeploy Hola clústeres mediante el uso de script de implementación de IaaS de HPC Pack hello:

* **Equipo cliente** -necesita un script de implementación de cliente basada en Windows equipo toorun Hola clúster.
* **Azure PowerShell** - [instale y configure Azure PowerShell](/powershell/azure/overview) (versión 0.8.10 o posterior) en el equipo cliente.
* **Script de implementación de IaaS de HPC Pack** : Descargue y descomprima la versión más reciente de Hola de script de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Puede comprobar Hola versión del script de Hola ejecutando `.\New-HPCIaaSCluster.ps1 –Version`. En este artículo se basa en la versión 4.4.1 o posterior del script de Hola.

**Archivo de configuración XML**

Hola script de implementación de IaaS de HPC Pack utiliza un archivo de configuración XML como clúster de HPC de entrada toodescribe Hola. Hello siguiente archivo de configuración de ejemplo especifica un clúster pequeño que consta de un nodo principal de HPC Pack y dos nodos de cálculo de tamaño A7 CentOS 7.0 Linux. 

Modifique el archivo hello según sea necesario para su entorno y la configuración de clúster deseado y guárdelo con un nombre como HPCDemoConfig.xml. Por ejemplo, debe toosupply el nombre de la suscripción y un nombre de la cuenta de almacenamiento único y el nombre del servicio de nube. Además, es recomendable toochoose otro admite la imagen de Linux para nodos de proceso de Hola. Para obtener más información acerca de los elementos de hello en el archivo de configuración de hello, consulte el archivo Manual.rtf de hello en la carpeta de script de Hola y [crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**Hola toorun script de implementación de IaaS de HPC Pack**

1. Abra Windows PowerShell en el equipo de cliente hello como administrador.
2. Cambiar carpeta toohello del directorio donde es el script de Hola instalado (E:\IaaSClusterScript en este ejemplo).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Ejecute hello después de clúster de HPC Pack de comando toodeploy Hola. En este ejemplo se da por supuesto que se encuentra ese archivo de configuración de hello en E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. Dado que hello **AdminPassword** no se especifica en Hola anterior comando esté tooenter solicitadas contraseña Hola usuario *MyAdminName*.
   
    b. script de Hola, a continuación, inicia el archivo de configuración de toovalidate Hola. Esta operación puede tardar tooseveral minutos depende de la conexión de red de Hola.
   
    ![Validación][validate]
   
    c. Una vez que pasen las validaciones, script de Hola presenta toocreate de recursos de clúster de Hola. Escriba *Y* toocontinue.
   
    ![Recursos][resources]
   
    d. script de Hola inicia el clúster de HPC Pack toodeploy hello y completa Hola configuración sin más pasos manuales. puede ejecutar el script de Hola durante varios minutos.
   
    ![Implementación][deploy]
   
   > [!NOTE]
   > En este ejemplo, hello script genera un archivo de registro automáticamente desde hello **- LogFile** parámetro no se especifica. Hola registros no se escriben en tiempo real, pero se recopilan final Hola de validación de Hola y la implementación de Hola. Si Hola proceso de PowerShell se detiene mientras se ejecuta el script de Hola, algunos archivos de registro se pierden.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Conectar el nodo principal de toohello
Después de implementar el clúster de HPC Pack hello en Azure, [conectarse mediante Escritorio remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nodo principal VM con Hola credenciales de dominio que ha proporcionado al implementar el clúster de hello (por ejemplo, *hpc\\ clusteradmin*). Administrar clústeres de Hola desde el nodo principal de Hola.

En el nodo principal de hello, inicie estado de hello toocheck de administrador de clústeres de HPC de clúster de HPC Pack Hola. Puede administrar y supervisar los nodos de proceso de Linux hello igual que funcionan con Windows nodos de proceso. Por ejemplo, verá nodos de Linux de hello enumerados en **administración de recursos** (estos nodos se implementan con hello **LinuxNode** plantilla).

![Administración de nodos][management]

También verá los nodos de Linux Hola Hola **mapa térmico** vista.

![Mapa térmico][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>¿Cómo toomove datos en un clúster con nodos de Linux
Tiene varias opciones toomove datos entre nodos de Linux y el nodo principal de Windows hello de clúster de Hola. Estos son tres métodos comunes, que se describe con más detalle en hello las secciones siguientes:

* **Archivos de Azure** -expone un administrado datos toostore del recurso compartido de archivos SMB de archivos en almacenamiento de Azure. Nodos de Windows y Linux puede montar un recurso compartido de archivos de Azure como una unidad o carpeta en hello mismo tiempo, incluso si se implementen en diferentes redes virtuales.
* **Nodo principal SMB compartir** -monta una carpeta compartida de Windows estándar del nodo principal de hello en nodos de Linux.
* **Servidor NFS del nodo principal**: proporciona una solución de uso compartido de archivos para un entorno mixto de Windows y Linux.

### <a name="azure-file-storage"></a>Almacenamiento de archivos de Azure
Hola [archivos de Azure](https://azure.microsoft.com/services/storage/files/) servicio expone recursos compartidos de archivos mediante el protocolo de SMB 2.1 estándar Hola. Máquinas virtuales de Azure y servicios en la nube pueden compartir datos de archivos a través de los componentes de la aplicación a través de recursos compartidos montados y aplicaciones locales pueden tener acceso a datos de archivos en un recurso compartido a través de la API de almacenamiento de archivo Hola. 

Para obtener pasos detallados toocreate un archivo de Azure comparten y montar en el nodo principal de hello, consulte [Introducción al almacenamiento de archivos de Azure en Windows](../../../storage/files/storage-how-to-use-files-windows.md). recurso compartido de archivos de Azure de toomount Hola Hola en nodos de Linux, consulte [cómo toouse almacenamiento de archivos de Azure con Linux](../../../storage/files/storage-how-to-use-files-linux.md). tooset las conexiones persistentes, consulte [Persisting conexiones tooMicrosoft archivos de Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

En el siguiente ejemplo de Hola, cree un recurso compartido de archivos de Azure en una cuenta de almacenamiento. Hola toomount compartir en el nodo principal de hello, abra un símbolo del sistema y escriba Hola siguientes comandos:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

En este ejemplo, allvhdsje es el nombre de cuenta de almacenamiento, storageaccountkey es la clave de cuenta de almacenamiento y rdma es el nombre del recurso compartido de archivos de Azure Hola. recurso compartido de archivos de Azure de Hola se monta como Z: en el nodo principal de Hola.

recurso compartido de archivos de Azure de toomount hello en los nodos de Linux, ejecute un **clusrun** comando en el nodo principal de Hola. **[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  es una útil toocarry de herramienta de HPC Pack tareas administrativas en varios nodos. (consulte también [ClusRun para nodos de Linux](#Clusrun-for-Linux-nodes) en este artículo).

Abra una ventana de Windows PowerShell y escriba Hola siguientes comandos:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

Hola primer comando crea una carpeta denominada /rdma en todos los nodos de grupo de LinuxNodes Hola. segundo comando de Hello monta hello Azure archivo recurso compartido allvhdsjw.file.core.windows.net/rdma en la carpeta de /rdma Hola con dir y el archivo too777 de conjunto de bits de modo. En el segundo comando hello, allvhdsje es el nombre de cuenta de almacenamiento y storageaccountkey es la clave de cuenta de almacenamiento.

> [!NOTE]
> Hola "\`" símbolo en el segundo comando de hello es un símbolo de escape de PowerShell. "\`,"significa que Hola"," (coma) forma parte del comando de Hola.
> 
> 

### <a name="head-node-share"></a>Recurso compartido del nodo principal
Como alternativa, puede montar una carpeta compartida de nodo principal de hello en nodos de Linux. Proporciona de un recurso compartido de archivos de tooshare de manera más sencillos de hello, pero el nodo principal de Hola y todos los nodos de Linux deben implementarse en hello misma red virtual. Estos son los pasos de Hola.

1. Cree una carpeta en el nodo principal de Hola y compartirlo tooEveryone con permisos de lectura/escritura. Por ejemplo, compartir D:\OpenFOAM en el nodo principal de hello como \\CentOS7RDMA HN\OpenFOAM. Aquí CentOS7RDMA HN es nombre de host de hello del nodo principal de Hola.
   
    ![Permisos del recurso compartido de archivos][fileshareperms]
   
    ![Uso compartido de archivos][filesharing]
2. Abra una ventana de Windows PowerShell y ejecute hello siguientes comandos:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Hola primer comando crea una carpeta denominada /openfoam en todos los nodos de grupo de LinuxNodes Hola. segundo comando de Hello monta Hola compartido carpeta //CentOS7RDMA-HN/OpenFOAM en la carpeta de hello con dir y el archivo too777 de conjunto de bits de modo. Hello username y password de comando hello deben ser Hola nombre de usuario y la contraseña de un usuario del clúster en el nodo principal de Hola. Consulte [Adición o eliminación de usuarios de clúster](https://technet.microsoft.com/library/ff919330.aspx).

> [!NOTE]
> Hola "\`" símbolo en el segundo comando de hello es un símbolo de escape de PowerShell. "\`,"significa que Hola"," (coma) forma parte del comando de Hola.
> 
> 

### <a name="nfs-server"></a>Servidor NFS
Hola servicio NFS permite tooshare y migra archivos entre equipos que ejecutan el sistema operativo de hello Windows Server 2012 mediante el protocolo SMB de Hola y equipos basados en Linux mediante el protocolo NFS de Hola. Hello servidor NFS y todos los demás nodos tienen toobe implementado en hello misma red virtual. Proporciona mayor compatibilidad con los nodos de Linux en comparación con un recurso compartido de SMB. Por ejemplo, admite vínculos de archivo.

1. tooinstall y configurar un servidor NFS, siga los pasos de hello en [servidor de sistema primer recurso compartido de red End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Por ejemplo, cree un recurso compartido NFS con el nombre de nfs con hello propiedades siguientes:
   
    ![Autorización de NFS][nfsauth]
   
    ![Permisos del recurso compartido de NFS][nfsshare]
   
    ![Permisos de NTFS de NFS][nfsperm]
   
    ![Propiedades de administración de NFS][nfsmanage]
2. Abra una ventana de Windows PowerShell y ejecute hello siguientes comandos:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   Hola primer comando crea una carpeta denominada /nfsshared en todos los nodos de grupo de LinuxNodes Hola. segundo comando montajes hello NFS Hello compartir HN CentOS7RDMA: / nfs en Hola carpeta. Aquí CentOS7RDMA HN: / nfs es la ruta de acceso remoto de Hola de su recurso compartido de NFS.

## <a name="how-toosubmit-jobs"></a>¿Cómo toosubmit trabajos
Hay clúster HPC Pack toosubmit trabajos toohello de varias maneras:

* Administrador de clústeres HPC o GUI del Administrador de trabajos de HPC
* Portal web de HPC
* API de REST

Envío de trabajos con clúster toohello en Azure a través de herramientas de interfaz gráfica de usuario de HPC Pack y el portal web de HPC Hola se Hola igual que para los nodos de proceso de Windows. Vea [Administrador de trabajos de HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) y [cómo toosubmit trabajos desde un equipo de cliente local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

trabajos de toosubmit a través de hello API de REST, consulte demasiado[crear y enviar trabajos usando Hola API de REST en Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). toosubmit trabajos desde un cliente de Linux, consulte también toohello ejemplo de Python en hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>ClusRun para nodos de Linux
Hola HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) herramienta puede ser comandos tooexecute usado en nodos de Linux a través de un símbolo del sistema o administrador de clústeres HPC. A continuación se muestran algunos ejemplos básicos.

* Mostrar nombres de usuario actuales en todos los nodos de clúster de Hola.
  
    ```command
    clusrun whoami
    ```
* Instalar hello **gdb** herramienta del depurador con **yum** en todos los nodos hello linuxnodes de grupo y, a continuación, reiniciar los nodos de hello después de 10 minutos.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Crear una secuencia de comandos de shell que mostrar cada número del 1 al 10 de un segundo en cada nodo de Linux en clúster de hello, ejecutarlo y mostrar resultados desde nodos Hola inmediatamente.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Es posible que tenga toouse determinados caracteres de escape **clusrun** comandos. Como se muestra en este ejemplo, utilice ^ en un hello tooescape de símbolo del sistema ">" símbolos.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Pruebe escalado Hola clúster tooa mayor número de nodos, o ejecutar una carga de trabajo de Linux en clúster de Hola. Para ver un ejemplo, consulte [Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure](hpcpack-cluster-namd.md).
* Intente un clúster con [máquinas virtuales compatibles con RDMA, proceso intensivo](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun cargas de trabajo MPI. Para ver un ejemplo, consulte [Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure](hpcpack-cluster-openfoam.md).
* Si está interesado en trabajar con nodos de Linux en un clúster de HPC Pack local, vea hello [guía TechNet](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
