---
title: "aaaSet un aplicaciones de MPI de Linux RDMA clúster toorun | Documentos de Microsoft"
description: "Crear un clúster de Linux de tamaño H16r, H16mr, A8 o A9 VM toouse aplicaciones de MPI de hello RDMA de Azure red toorun"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>Configurar una aplicación de MPI Linux RDMA toorun de clúster
Obtenga información acerca de cómo agrupar tooset seguridad un Linux RDMA en Azure con [tamaños de máquinas virtuales de proceso de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun aplicaciones de interfaz de paso de mensajes (MPI) paralelas. Este artículo proporciona pasos tooprepare un toorun de imagen de Linux HPC MPI de Intel en un clúster. Después de preparar, implementar un clúster de máquinas virtuales usando esta imagen y uno de los tamaños de máquina virtual de Azure compatibles con RDMA hello (actualmente H16r, H16mr, A8 o A9). Utilice hello toorun MPI las aplicaciones de clúster que se comunican de manera eficiente a través de una red de baja latencia y alto rendimiento basada en la tecnología de memoria directa remota (RDMA) de acceso.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) y el clásico. Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

## <a name="cluster-deployment-options"></a>Opciones de implementación de clúster
Siguientes son métodos que puede usar un clúster de Linux RDMA toocreate con o sin un programador de trabajos.

* **Las secuencias de comandos CLI Azure**: como se muestra más adelante en este artículo, use hello [interfaz de línea de comandos de Azure](../../../cli-install-nodejs.md) implementación de Hola de tooscript (CLI) de un clúster de máquinas virtuales compatibles con RDMA. Hola CLI en el modo de administración de servicios crea Hola nodos de clúster en serie en el modelo de implementación clásica de hello, por lo que implementar muchos nodos de proceso puede tardar varios minutos. Hola tooenable conexión de red RDMA cuando se usa el modelo de implementación clásica de hello, implementar máquinas virtuales de Hola Hola mismo servicio en la nube.
* **Plantillas de administrador de recursos de Azure**: también puede utilizar toodeploy de modelo de implementación un clúster de máquinas virtuales compatibles con RDMA que conecta la red RDMA de toohello de hello Administrador de recursos. También puede [crear su propia plantilla](../../../resource-group-authoring-templates.md), o consulte hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) para plantillas aportadas por Microsoft o hello Comunidad toodeploy Hola solución deseada. Plantillas de administrador de recursos pueden proporcionar un toodeploy de manera rápida y confiable de un clúster de Linux. Hola tooenable conexión de red RDMA cuando se usa el modelo de implementación del Administrador de recursos de hello, implementar máquinas virtuales de Hola Hola mismo conjunto de disponibilidad.
* **HPC Pack**: crear un clúster de Microsoft HPC Pack en Azure y agregar nodos de cálculo compatibles con RDMA que se ejecutan en una red RDMA de Linux distribución tooaccess Hola admitida. Para más información, consulte [Introducción a los nodos de ejecución de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).

## <a name="sample-deployment-steps-in-hello-classic-model"></a>Los pasos de implementación de ejemplo de modelo clásico Hola
Hello pasos siguientes muestran cómo personalizarlo toouse hello Azure CLI toodeploy una máquina virtual de HPC de SUSE Linux Enterprise Server (SLES) 12 SP1 de hello Azure Marketplace y crear una imagen de máquina virtual personalizada. A continuación, puede usar la implementación de hello tooscript Hola una imagen de un clúster de máquinas virtuales compatibles con RDMA.

> [!TIP]
> Usar un clúster de máquinas virtuales compatibles con RDMA basado en imágenes de CentOS-based HPC en Azure Marketplace Hola similar toodeploy de pasos. Es posible que, como se indica, algunos pasos sean ligeramente distintos. 
>
>

### <a name="prerequisites"></a>Requisitos previos
* **Equipo cliente**: se necesita un toocommunicate de equipo de cliente de Windows, Linux o Mac con Azure. Estos pasos se supone que está usado un cliente Linux.
* **Suscripción de Azure**: si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en un par de minutos. En los clústeres más grandes, considere la posibilidad de una suscripción de pago por uso u otras opciones de compra.
* **Disponibilidad de tamaño VM**: Hola siguientes tamaños de instancias es compatibles con RDMA: H16r, H16mr, A8 y A9. Para ver la disponibilidad en las regiones de Azure, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/) .
* **Cuota de núcleos**: es posible que tenga cuota de hello tooincrease de núcleos toodeploy un clúster de máquinas virtuales de proceso intensivo. Por ejemplo, necesita al menos 128 núcleos si desea toodeploy 8 A9 VM como se muestra en este artículo. La suscripción también puede limitar el número de Hola de núcleos que se puede implementar en ciertas familias de tamaño de máquina virtual, incluyendo Hola H-series. aumentar una cuota de toorequest, [abrir una solicitud de soporte al cliente en línea](../../../azure-supportability/how-to-create-azure-support-request.md) sin cargo.
* **CLI de Azure**: [instalar](../../../cli-install-nodejs.md) Hola CLI de Azure y [conectar tooyour suscripción de Azure](../../../xplat-cli-connect.md) desde el equipo cliente de Hola.

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>Aprovisionamiento de una máquina virtual de HPC de SLES 12 SP1
Después de iniciar sesión en tooAzure con hello CLI de Azure, ejecute `azure config list` tooconfirm que Hola salida muestra el modo de administración de servicios. Si no es así, establecer el modo de hello, ejecute este comando:

    azure config mode asm


Escriba Hola después a toolist todas las suscripciones de hello son toouse autorizado:

    azure account list

suscripción activa de Hello actual se identifica con `Current` establecido demasiado`true`. Si esta suscripción no Hola uno que desea toouse toocreate Hola clúster, establecer Id. de suscripción adecuado de hello como suscripción activa de hello:

    azure account set <subscription-Id>

toosee Hola disponibles públicamente imágenes SLES 12 SP1 HPC en Azure, ejecute un comando como Hola sigue, suponiendo que el entorno de shell es compatible con **grep**:

    azure vm image list | grep "suse.*hpc"

El aprovisionamiento de una máquina virtual compatible con RDMA con una imagen de HPC de SLES 12 SP1 mediante la ejecución de un comando como Hola siguiente:

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

Donde:

* Hola tamaño (A9 en este ejemplo) es uno de los tamaños de máquinas virtuales de hello compatibles con RDMA.
* número de puerto SSH Hola externo (22 en este ejemplo, que es hello predeterminada SSH) es cualquier número de puerto válido. número de puerto SSH interno Hola se establece too22.
* Un nuevo servicio de nube se crea en Hola especificada por la ubicación de Hola de región de Azure. Especifique una ubicación en qué Hola VM tamaño elegido está disponible.
* Para obtener soporte de prioridad SUSE (que incurre en cargos adicionales), nombre de la imagen de hello SLES 12 SP1 actualmente puede ser una de estas dos opciones: 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>Personalizar Hola VM
Al finalizar Hola VM aprovisionamiento, SSH toohello VM mediante el uso de Hola dirección IP externa de la máquina virtual (o nombre DNS) y Hola número de puerto externo configurado y, a continuación, personalizarlo. Para obtener detalles de conexión, consulte [cómo toolog en la máquina virtual de tooa ejecutan Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ejecute comandos como usuario de hello configurado en Hola de máquina virtual, a menos que el acceso a la raíz es toocomplete requiere un paso.

> [!IMPORTANT]
> Microsoft Azure no proporciona acceso a la raíz tooLinux las máquinas virtuales. acceso administrativo de toogain cuando se conecta como un toohello de usuario de máquina virtual, ejecute los comandos mediante el uso de `sudo`.
>
>

* **Actualizaciones**: instale las actualizaciones mediante zypper. Puede que le interese tooinstall utilidades NFS.

  > [!IMPORTANT]
  > En una VM de HPC SLES 12 SP1, se recomienda no aplicar actualizaciones de kernel, lo que pueden causar problemas con hello Linux RDMA controladores.
  >
  >
* **Intel MPI**: completar la instalación de Hola de MPI de Intel en hello SLES 12 SP1 HPC VM ejecutando Hola siguiente comando:

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **Bloquear la memoria**: para MPI códigos toolock Hola memoria disponible para RDMA, agregar o cambiar los Hola después de la configuración en el archivo de hello /etc/security/limits.conf. Necesita tooedit de acceso raíz de este archivo.

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > Para realizar pruebas, también puede establecer memlock toounlimited. Por ejemplo: `<User or group name>    hard    memlock unlimited`. Para más información, consulte los [métodos más conocidos para definir el tamaño de memoria bloqueada](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).
  >
  >
* **Claves SSH para máquinas virtuales de SLES**: generar SSH claves tooestablish relación de confianza para su cuenta de usuario entre Hola nodos de ejecución Hola SLES clúster cuando se ejecutan trabajos MPI. Si implementó una máquina virtual de HPC basada en CentOS, no siga este paso. Consulte las instrucciones más adelante en este tooset artículo passwordless confianza SSH entre los nodos del clúster Hola después de capturar imagen de hello e implementar clústeres de Hola.

    claves de SSH toocreate, ejecute el siguiente comando de Hola. Cuando se le pida para la entrada, seleccione **ENTRAR** toogenerate claves de hello en ubicación predeterminada de hello sin establecer una contraseña.

        ssh-keygen

    Anexar el archivo de authorized_keys toohello de clave pública de Hola para las claves públicas conocidas.

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    En el directorio de ~/.ssh hello, editar o crear el archivo de configuración de Hola. Proporcionar el intervalo de direcciones IP de Hola de red privada de Hola que planea toouse en Azure (10.32.0.0/16 en este ejemplo):

        host 10.32.0.*
        StrictHostKeyChecking no

    Como alternativa, lista dirección IP de red privada de Hola de cada máquina virtual en el clúster como se indica a continuación:

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > Configurar `StrictHostKeyChecking no` puede crear un posible riesgo de seguridad cuando no se especifica una dirección IP o un intervalo concretos.
  >
  >
* **Aplicaciones**: instalar ninguna aplicación necesita o realizar otras personalizaciones antes de capturar imagen de Hola.

### <a name="capture-hello-image"></a>Capturar imagen de Hola
imagen de hello toocapture, primero ejecute hello siguiente comando en hello VM de Linux. Este comando desactiva Hola VM pero mantiene las cuentas de usuario y las claves SSH que configuró.

```
sudo waagent -deprovision
```

Desde el equipo cliente, ejecute hello después de la imagen de Hola de toocapture de comandos de CLI de Azure. Para obtener más información, consulte [cómo toocapture una máquina virtual de Linux clásica como imagen](capture-image.md).  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

Después de ejecutar estos comandos, se captura la imagen de máquina virtual de Hola para su uso y Hola máquina virtual se elimina. Ahora tiene la toodeploy listo de imagen personalizada un clúster.

### <a name="deploy-a-cluster-with-hello-image"></a>Implementar un clúster con la imagen de Hola
Modifica Hola siguiente secuencia de comandos de Bash con los valores adecuados para su entorno y lo ejecuta desde el equipo cliente. Dado que Azure implementa máquinas virtuales de hello en serie en el modelo de implementación clásica de hello, tarda unos minutos toodeploy Hola ocho máquinas virtuales de A9 sugeridas en esta secuencia de comandos.

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>Consideraciones para un clúster de HPC de CentOS
Si desea tooset un clúster basado en una de las imágenes HPC basado en CentOS de hello en hello Azure Marketplace en lugar de SLES 12 para HPC, siga los pasos generales Hola Hola sección anterior. Tenga en cuenta hello las siguientes diferencias cuando se aprovisiona y configura Hola VM:

- Intel MPI ya está instalado en una máquina virtual aprovisionada desde una imagen de HPC basada en CentOS.
- Configuración de la memoria de bloqueo ya se han agregado en archivo de la máquina virtual de hello /etc/security/limits.conf.
- No se generan claves SSH en hello VM aprovisione para la captura. En su lugar, se recomienda configurar la autenticación basada en usuario después de implementar el clúster de Hola. Para obtener más información, vea Hola pasos de la sección.  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>Establecer una confianza SSH passwordless en clúster de Hola
En un clúster HPC basado en CentOS, existen dos métodos para establecer la confianza entre los nodos de proceso de hello: autenticación basada en host y la autenticación basada en usuario. Autenticación basada en host está fuera del ámbito de Hola de este artículo y generalmente debe realizarse a través de una secuencia de comandos de extensión durante la implementación. Autenticación basada en usuario resulta útil para establecer la confianza después de la implementación y requiere la generación de Hola y uso compartido de las claves SSH entre Hola nodos de ejecución Hola clúster. Este método se suele conocer como inicio de sesión SSH sin contraseña y es necesario al ejecutar trabajos de MPI.

Está disponible en una secuencia de comandos de ejemplo que proceden de la Comunidad de hello [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable autenticación de usuario sencilla en un clúster HPC basado en CentOS. Descargue y use este script mediante el uso de hello pasos. También puede modificar esta secuencia de comandos o usar cualquier otro método tooestablish passwordless autenticación de SSH entre nodos de proceso del clúster de Hola.

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

script de Hola toorun, se necesita un prefijo de hello tooknow para las direcciones IP de subred. Obtiene el prefijo de hello ejecutando Hola siguiente comando en uno de los nodos de clúster de Hola. El resultado debe ser similar a 10.1.3.5 y prefijo de hello es parte de hello 10.1.3.

    ifconfig eth0 | grep -w inet | awk '{print $2}'

Ahora ejecutar script de Hola con tres parámetros: nombre de usuario común de hello en hello nodos de proceso, contraseña común de Hola para ese usuario en hello nodos de proceso y del prefijo de subred de Hola que se devolvió desde el comando anterior Hola.

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

Este script Hola siguientes:

* Crea un directorio en el nodo de host de hello denominado .ssh, que es necesario para el inicio de sesión passwordless.
* Crea un archivo de configuración en el directorio de .ssh Hola que indica el inicio de sesión de inicio de sesión passwordless tooallow desde cualquier nodo de clúster de Hola.
* Crea archivos que contienen nombres de nodo de Hola y direcciones IP del nodo para todos los nodos Hola Hola clúster. Estos archivos se mantienen después de ejecutar script de Hola para consultarlos más adelante.
* Crea un par de claves público y privado para cada nodo del clúster (incluido el nodo de host de hello) y crea entradas en el archivo de hello authorized_keys.

> [!WARNING]
> La ejecución de este script puede crear un posible riesgo de seguridad. Asegúrese de que no se distribuye información de clave pública de hello en ~/.ssh.
>
>

## <a name="configure-intel-mpi"></a>Configuración de Intel MPI
aplicaciones de MPI toorun en RDMA de Linux de Azure, necesita tooconfigure determinada variables de entorno específicas tooIntel MPI. Aquí es un toorun ejemplo Bash script tooconfigure hello las variables que se necesita una aplicación. Cambiar toompivars.sh de ruta de acceso de hello según sea necesario para la instalación de Intel MPI.

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

Hola formato de archivo de host de hello es el siguiente. Agregue una línea para cada nodo del clúster. Especifique las direcciones IP privadas de la red virtual de hello definen anteriormente, no los nombres DNS. Por ejemplo, para los dos hosts con direcciones IP 10.32.0.1 y 10.32.0.2, archivo hello contiene siguiente hello:

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>Ejecución de MPI en un clúster de dos nodos básico
Si aún no lo ha hecho, en primer lugar configurar Hola entorno para Intel MPI.

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>Ejecución de un comando de MPI
Ejecutar un comando MPI en uno de tooshow de nodos de proceso de Hola que MPI esté instalado correctamente y se puede comunicar entre al menos dos nodos de proceso. siguiente Hello **mpirun** comando ejecuta hello **hostname** comando dos nodos.

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
La salida debe enumerar nombres Hola de todos los nodos de Hola que pasan como entrada para `-hosts`. Por ejemplo, un **mpirun** comando con dos nodos devuelve resultados similares a Hola siguientes:

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>Ejecución de una prueba comparativa de MPI
Hola siguiente comando de MPI Intel ejecuta una pingpong prueba comparativa tooverify Hola configuración y conexión toohello RDMA red del clúster.

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

En un clúster de trabajar con dos nodos, obtendrá unos resultados similares a los siguientes Hola. En la red RDMA de Azure de hello, espera latencia en o por debajo de 3 microsegundos para tamaños de mensaje seguridad too512 bytes.

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>Pasos siguientes
* Implemente y ejecute las aplicaciones Linux MPI en el clúster de Linux.
* Vea hello [documentación de la biblioteca de MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) para obtener instrucciones sobre MPI de Intel.
* Intente una [plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate un Lustre Intel de clúster mediante una imagen basada en CentOS HPC. Para más información, consulte [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/) (Implementación de la edición de nube de Intel para Lustre en Microsoft Azure).
