---
title: "aaaRun OpenFOAM con HPC Pack en máquinas virtuales de Linux | Documentos de Microsoft"
description: "Implemente un clúster de Microsoft HPC Pack en Azure y ejecute un trabajo de OpenFOAM en varios nodos de ejecución de Linux en una red RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Ejecución de OpenFoam con Microsoft HPC Pack en un clúster de Linux RDMA en Azure
Este artículo muestra una manera de toorun OpenFoam en máquinas virtuales de Azure. Aquí se implementa un clúster de Microsoft HPC Pack con nodos de proceso de Linux en Azure y se ejecuta un trabajo de [OpenFoam](http://openfoam.com/) con Intel MPI. Puede usar máquinas virtuales de Azure compatibles con RDMA para nodos de proceso de hello, para que los nodos de proceso de hello comunican a través de la red RDMA de Azure de Hola. Otro toorun opciones OpenFoam en Azure son totalmente configurado comerciales imágenes disponibles en hello Marketplace, como del UberCloud [OpenFoam 2.3 de CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)y mediante la ejecución en [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/). 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM (del inglés, operación y manipulación de campo abierto) es un paquete de software de código abierto de cálculo de dinámicas de fluidos (CFD) que se utiliza ampliamente en ingeniería y ciencias en organizaciones académicas y comerciales. Incluye herramientas para la creación de mallas, especialmente snappyHexMesh, una herramienta de creación de mallas en paralelo para las geometrías complejas de CAD y para el preprocesamiento y el posprocesamiento. Casi todos los procesos que se ejecutan en paralelo, lo que permite a los usuarios tootake aprovechar hardware del equipo a su disposición.  

Microsoft HPC Pack proporciona características toorun HPC a gran escala y aplicaciones en paralelo, incluidas las aplicaciones de MPI, acerca de los clústeres de máquinas virtuales de Microsoft Azure. HPC Pack también admite la ejecución de aplicaciones Linux HPC en máquinas virtuales de nodos de proceso Linux implementadas en un clúster de HPC Pack. Vea [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para un toousing Introducción nodos con HPC Pack de ejecución de Linux.

> [!NOTE]
> Este artículo se explica cómo toorun una carga de trabajo de Linux MPI con HPC Pack. Se supone que tiene cierta familiaridad con la administración del sistema Linux y con la ejecución de cargas de trabajo MPI en clústeres de Linux. Si se usan versiones de MPI y OpenFOAM diferente de Hola que se muestran en este artículo, podría tener toomodify algunos pasos de instalación y configuración. 
> 
> 

## <a name="prerequisites"></a>Requisitos previos
* **Clúster de HPC Pack con nodos de proceso de Linux compatibles con RDMA**: implemente un clúster de HPC Pack con nodos de proceso de Linux de tamaño A8, A9, H16r o H16rm mediante una [plantilla de Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o un [script de Azure PowerShell](hpcpack-cluster-powershell-script.md). Vea [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para requisitos previos de Hola y pasos para cualquiera de las opciones. Si elige Hola opción de implementación de secuencia de comandos de PowerShell, vea el archivo de configuración de ejemplo de Hola en archivos de ejemplo de Hola final Hola de este artículo. Utilice este clúster de HPC Pack toodeploy un basado en Azure de configuración que consta de un nodo principal de tamaño A8 Windows Server 2012 R2 y tamaño 2 A8 SUSE Linux Enterprise Server 12 nodos de proceso. Sustituya los valores apropiados por su nombre de suscripción y de servicio. 
  
  **Aspectos adicionales tooknow**
  
  * Para los requisitos previos de red de Linux RDMA en Azure, consulte [Tamaños de máquina virtual de procesos de alto rendimiento](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  * Si usas Hola opción de implementación de secuencia de comandos de Powershell, implementar todos los nodos de proceso de Linux de hello dentro de la conexión de red de una nube servicio toouse Hola RDMA.
  * Después de implementar nodos de Linux de hello, conectar SSH tooperform las tareas administrativas adicionales. Busca los detalles de conexión de SSH de Hola para cada VM de Linux en hello portal de Azure.  
* **Intel MPI** -toorun OpenFOAM en SLES 12 HPC nodos de cálculo en Azure, deberá tooinstall en tiempo de ejecución Hola Intel MPI biblioteca 5 de hello [Intel.com sitio](https://software.intel.com/en-us/intel-mpi-library/). (Intel MPI 5 ya está instalado en las imágenes de HPC basadas en CentOS).  En un paso posterior, si es necesario, instale Intel MPI en los nodos de proceso de Linux. tooprepare para este paso después de registrarse con Intel, siga Hola vínculo de página de web relacionados de hello confirmación correo electrónico toohello. A continuación, el vínculo para archivo .tgz de hello para la versión adecuada de Hola de MPI Intel de descarga de Hola de copia. Este artículo se basa en Intel MPI versión 5.0.3.048.
* **Módulo de origen OpenFOAM** -descargar el software de módulo de origen OpenFOAM de Hola de Linux de hello [sitio OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/). Este artículo se basa en la versión del paquete de origen 2.3.1, disponible para su descarga como OpenFOAM 2.3.1.tgz. Siga las instrucciones de hello más adelante en este artículo toounpack y compile OpenFOAM Hola compute en nodos de Linux.
* **EnSight** (opcional): resultados de hello toosee de la simulación OpenFOAM, descargue e instale hello [EnSight](https://www.ceisoftware.com/download/) programa de visualización y análisis. Información de licencia y descarga son en el sitio de EnSight Hola.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Configuración de la confianza mutua entre nodos de proceso
Ejecutar un trabajo de entre nodos en varios nodos de Linux requiere Hola nodos tootrust entre sí (por **rsh** o **ssh**). Cuando se crea el clúster de HPC Pack Hola con hello script de implementación de Microsoft HPC Pack IaaS, script de Hola configura automáticamente una confianza mutua permanente para cuenta de administrador de Hola que especifique. Para crear en el dominio del clúster de Hola de los usuarios sin privilegios de administrador, deberá tooset temporal confianza mutua entre los nodos de hello cuando un trabajo asignado toothem y destruir relación Hola una vez completado el trabajo de Hola. confianza tooestablish para cada usuario, proporcione un clúster de toohello de par de claves de RSA que HPC Pack se usa para la relación de confianza de Hola.

### <a name="generate-an-rsa-key-pair"></a>Generación de un par de claves RSA
Resulta fácil toogenerate un par de claves de RSA, que contiene una clave pública y una clave privada y, a continuación, ejecutando Hola Linux **ssh-keygen** comando.

1. Inicie sesión en tooa equipo Linux.
2. Ejecute el siguiente comando de hello:
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Presione **ENTRAR** toouse Hola predeterminados hasta que se complete el comando Hola. No escriba aquí una frase de contraseña. Cuando se le pida una contraseña, solo tiene que presionar **Entrar**.
   > 
   > 
   
   ![Generación de un par de claves RSA][keygen]
3. Cambie el directorio toohello ~/.ssh directorio. clave privada de Hola se almacena en la clave pública de hello y id_rsa en id_rsa.pub.
   
   ![Claves públicas y privadas][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Agregar clúster de HPC Pack en toohello Hola par de claves
1. Asegúrese de un nodo principal de escritorio remoto conexión tooyour con su cuenta de administrador de HPC Pack (cuenta de administrador Hola configurar cuando se ejecuta la secuencia de comandos de implementación de hello).
2. Utilice toocreate estándar de procedimientos de Windows Server una cuenta de usuario de dominio dominio del clúster de hello de Active Directory. Por ejemplo, usar hello usuario de Active Directory y la herramienta de equipos en el nodo principal de Hola. ejemplos de Hello en este artículo se supone que crea un usuario de dominio denominado hpclab\hpcuser.
3. Cree un archivo denominado C:\cred.xml y copiar datos de clave de RSA de hello en él. Un ejemplo de archivo de cred.xml es final Hola de este artículo.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. Abra un símbolo del sistema y escriba el siguiente comando hello tooset credenciales datos para hello hpclab\hpcuser cuenta de hello. Usar hello **extendeddata** toopass parámetro Hola nombre del archivo de C:\cred.xml que creó para datos de clave de saludo.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Este comando se completa correctamente sin salida. Después de establecer las credenciales de Hola Hola para cuentas de usuario que necesita toorun trabajos, almacenar el archivo de cred.xml hello en una ubicación segura o elimínelo.
5. Si ha generado el par de claves RSA de hello en uno de los nodos de Linux, recuerde que las claves de hello toodelete cuando termine de utilizarlos. Si HPC Pack encuentra un archivo id_rsa o id_rsa.pub existentes, no establece una confianza mutua.

> [!IMPORTANT]
> No se recomienda ejecutar un trabajo de Linux como un administrador de clústeres en un clúster compartido, porque un trabajo enviado por un administrador se ejecuta con la cuenta raíz de Hola Hola en nodos de Linux. Sin embargo, un trabajo enviado por un usuario sin privilegios de administrador se ejecuta bajo una cuenta de usuario local de Linux con hello mismo nombre como usuario de trabajo de Hola. En este caso, HPC Pack establece la confianza mutua para este usuario de Linux en todos los nodos de hello asignados toohello trabajo. Puede configurar el usuario de Linux Hola manualmente hello en nodos de Linux antes de ejecutar el trabajo de Hola o HPC Pack crea usuario Hola automáticamente cuando se envía el trabajo de Hola. Si HPC Pack crea usuario hello, HPC Pack se elimina una vez completado el trabajo de Hola. amenazas de seguridad tooreduce, HPC Pack quita las claves de hello tras la finalización del trabajo.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Configuración de un recurso compartido de archivos para nodos de Linux
Ahora debe configurar un recurso compartido de SMB estándar en una carpeta en el nodo principal de Hola. tooallow Hola Linux nodos tooaccess archivos de aplicación con una ruta de acceso común, montaje Hola compartido carpeta hello en nodos de Linux. Si lo desea, puede usar otra opción para compartir archivos, como un recurso compartido de archivos de Azure, recomendado para muchos escenarios, o un recurso compartido NFS. Vea el archivo hello compartir información y pasos detallados en [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).

1. Cree una carpeta en el nodo principal de Hola y compártala tooEveryone estableciendo privilegios de lectura/escritura. Por ejemplo, compartir C:\OpenFOAM en el nodo principal de hello como \\ \\SUSE12RDMA HN\OpenFOAM. En este caso, *SUSE12RDMA HN* es Hola de nombre de host del nodo principal de Hola.
2. Abra una ventana de Windows PowerShell y ejecute hello siguientes comandos:
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

Hola primer comando crea una carpeta denominada /openfoam en todos los nodos de grupo de LinuxNodes Hola. segundo comando de Hello monta Hola compartido carpeta //SUSE12RDMA-HN/OpenFOAM hello en nodos de Linux con dir_mode y file_mode too777 de conjunto de bits. Hola *nombre de usuario* y *contraseña* Hola comando debe ser credenciales de Hola de un usuario en el nodo principal de Hola.

> [!NOTE]
> Hola "\`" símbolo en el segundo comando de hello es un símbolo de escape de PowerShell. "\`,"significa Hola"," (coma) forma parte del comando de Hola.
> 
> 

## <a name="install-mpi-and-openfoam"></a>Instalación de MPI y OpenFOAM
toorun OpenFOAM como un trabajo de MPI en red RDMA de hello, deberá toocompile OpenFOAM con bibliotecas de MPI Intel Hola. 

En primer lugar, ejecutar varios **clusrun** comandos tooinstall bibliotecas de MPI de Intel (si no está ya instalado) y OpenFOAM en los nodos de Linux. Recurso compartido de nodo principal de hello uso previamente configurado archivos de instalación de hello tooshare entre los nodos de Linux de Hola.

> [!IMPORTANT]
> Estos pasos de instalación y compilación son ejemplos. Debe conocer algo de tooensure de administración de sistema de Linux que las bibliotecas y compiladores dependientes están instaladas correctamente. Podría necesitar toomodify determinadas variables de entorno u otras opciones para las versiones de MPI de Intel y OpenFOAM. Para más información, consulte [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) (Guía de instalación de la biblioteca Intel MPI para Linux) y [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) (Instalación del paquete de origen de OpenFOAM) para su entorno.
> 
> 

### <a name="install-intel-mpi"></a>Instalación de Intel MPI
Guardar paquete de instalación descargado de Hola para Intel MPI (l_mpi_p_5.0.3.048.tgz en este ejemplo) en C:\OpenFoam en el nodo principal de Hola para nodos de Linux de hello pueden tener acceso a este archivo desde /openfoam. A continuación, ejecute **clusrun** biblioteca de MPI Intel tooinstall en todos los nodos de Linux de Hola.

1. a continuación Hola comandos del paquete de instalación copia hello y extráigalo demasiado/opt/intel en cada nodo.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. tooinstall Intel MPI Library en modo silencioso, utilice un archivo de silent.cfg. Puede encontrar un ejemplo de Hola archivos de ejemplo al final de Hola de este artículo. Coloque este archivo en hello comparte /openfoam de carpeta. Para obtener más información sobre el archivo de silent.cfg hello, consulte [Intel MPI Library for Linux Installation Guide - instalación silenciosa](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).
   
   > [!TIP]
   > Asegúrese de que guarda el archivo silent.cfg como un archivo de texto con finales de línea de Linux (solo LF, no CR LF). Este paso garantiza que se ejecuta correctamente hello en nodos de Linux.
   > 
   > 
3. Instale la biblioteca Intel MPI en modo silencioso.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>Configuración de MPI
Para las pruebas, deberá agregar Hola seguidas de cada uno de los nodos de Linux de hello las líneas toohello /etc/security/limits.conf:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


Reinicie los nodos de Linux de Hola después de actualizar el archivo de hello limits.conf. Por ejemplo, use Hola siguiente **clusrun** comando:

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

Después de reiniciar, asegúrese de que esa carpeta compartida Hola se monta como /openfoam.

### <a name="compile-and-install-openfoam"></a>Compilación e instalación de OpenFOAM
Guardar el paquete de instalación descargado de Hola para hello tooC:\OpenFoam OpenFOAM del paquete de origen (OpenFOAM 2.3.1.tgz en este ejemplo) en el nodo principal de Hola para que los nodos de Linux de hello pueden tener acceso a este archivo desde /openfoam. A continuación, ejecute **clusrun** comandos Hola a toocompile OpenFOAM en todos los nodos de Linux.

1. Cree una carpeta /opt/OpenFOAM en cada nodo de Linux, copia Hola paquete toothis carpeta de origen y extráigalo no existe.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. toocompile OpenFOAM con hello Intel MPI Library, primero configure algunas variables de entorno para MPI de Intel y OpenFOAM. Usar un script de bash llamado settings.sh tooset Hola variables. Puede encontrar un ejemplo de Hola archivos de ejemplo al final de Hola de este artículo. Coloque este archivo (que se guarda con el fin de línea de Linux) en hello comparte /openfoam de carpeta. Este archivo también contiene valores de hello MPI y OpenFOAM tiempos de ejecución que utilice toorun más adelante un trabajo de OpenFOAM.
3. Instale los paquetes dependientes necesitados toocompile OpenFOAM. Dependiendo de la distribución de Linux, puede que tenga tooadd un repositorio. Ejecutar **clusrun** comandos toohello similar a continuación:
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    Si es necesario, Hola SSH tooeach Linux nodo toorun comandos tooconfirm que se ejecuta correctamente.
4. Siguiente ejecución Hola comando toocompile OpenFOAM. proceso de compilación de Hello tarda algún tiempo toocomplete y genera una gran cantidad de salida de toostandard de información de registro, por lo que usar hello **/ intercalar** opción de salida de hello toodisplay intercalada.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > Hola "\`" símbolo de comando hello es un símbolo de escape de PowerShell. "\`&" significa Hola "&" forma parte del comando de Hola.
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Preparar un trabajo de OpenFOAM de toorun
Ahora toorun listo de get un trabajo de MPI llamado sloshingTank3D, que es uno de los ejemplos de hello OpenFoam, en dos nodos de Linux. 

### <a name="set-up-hello-runtime-environment"></a>Configurar el entorno de tiempo de ejecución de Hola
tooset entornos en tiempo de ejecución de Hola de MPI y OpenFOAM hello en nodos de Linux, ejecute hello siguiente comando en una ventana de Windows PowerShell en el nodo principal de Hola. (Este comando sólo es válido para SUSE Linux).

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>Preparación de datos de ejemplo
Recurso compartido de nodo principal de Hola de uso que configuró anteriormente tooshare archivos entre los nodos de Linux de hello (montados como /openfoam).

1. Nodos de proceso de tooone SSH de su Linux.
2. Ejecute hello después comando tooset el entorno de tiempo de ejecución de hello OpenFOAM, si aún no lo ha hecho ya.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Copie la carpeta compartida de hello sloshingTank3D ejemplo toohello y navegue tooit.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. Cuando se usan parámetros de saludo predeterminado de este ejemplo, puede tardar decenas de minutos toorun, por lo que conviene toomodify algunos toomake de parámetros que ejecute más rápido. Una opción simple es toomodify Hola tiempo paso variables deltaT y writeInterval en el archivo de sistema/controlDict hello. Este archivo almacena todos los datos de entrada relacionados con toohello control de tiempo de lectura y escritura y datos de la solución. Por ejemplo, puede cambiar valor Hola de deltaT de 0,05 too0.5 y el valor de Hola de writeInterval de too0.5 0,05.
   
   ![Modificar variables de paso][step_variables]
5. Especifique los valores deseados para las variables de hello en el archivo de sistema/decomposeParDict hello. Este ejemplo utiliza dos nodos de Linux cada con 8 núcleos, por tanto, establecer numberOfSubdomains too16 y n de hierarchicalCoeffs too(1 1 16), lo que significa que ejecuta OpenFOAM en paralelo con 16 procesos. Para más información, consulte [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)(Guía de usuario de OpenFOAM: 3.4 Ejecución de aplicaciones en paralelo).
   
   ![Descomponer procesos][decompose]
6. Ejecute hello siguientes comandos de datos de ejemplo de Hola sloshingTank3D directory tooprepare Hola.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. En el nodo principal de hello, debería ver los archivos de datos de ejemplo de Hola se copian en C:\OpenFoam\sloshingTank3D. (C:\OpenFoam es carpeta compartida de hello en el nodo principal de hello).
   
   ![Archivos de datos en el nodo principal de Hola][data_files]

### <a name="host-file-for-mpirun"></a>Archivo de host para mpirun
En este paso, creará un archivo de host (una lista de nodos de proceso) que hello **mpirun** comando usa.

1. En uno de los nodos de Linux de hello, cree un archivo denominado archivo de host en /openfoam, por lo que este archivo se puede alcanzar en /openfoam/hostfile en todos los nodos de Linux.
2. Escriba los nombres de los nodos de Linux en este archivo. En este ejemplo, archivo hello contiene Hola después de nombres:
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > También puede crear este archivo en C:\OpenFoam\hostfile en el nodo principal de Hola. Si elige esta opción, guarde el script como archivo de texto con finales de línea de Linux (solo LF, no CR LF). Esto garantiza que se ejecuta correctamente hello en nodos de Linux.
   > 
   > 
   
   **Contenedor de script de Bash**
   
   Si tiene muchos nodos de Linux y desea que su toorun de trabajo sólo en algunas de ellas, no es un toouse buena idea un host fijo de archivos, porque no sabe qué nodos se asignarán tooyour trabajo. En este caso, escribir un contenedor de secuencias de comandos de bash para **mpirun** toocreate Hola archivo host automáticamente. Puede buscar un contenedor de secuencias de comandos de bash en el ejemplo se llama hpcimpirun.sh final Hola de este artículo y guárdelo como /openfoam/hpcimpirun.sh. Este script de ejemplo Hola siguientes:
   
   1. Establece las variables de entorno de Hola para **mpirun**y algún trabajo de MPI de adición comando parámetros toorun Hola a través de la red RDMA de Hola. En este caso, Establece Hola siguientes variables:
      
      * I_MPI_FABRICS=shm:dapl
      * I_MPI_DAPL_PROVIDER=ofa-v2-ib0
      * I_MPI_DYNAMIC_CONNECTION=0
   2. Crea un archivo de host según toohello $ de variable de entorno CCP_NODES_CORES, que se establece mediante el nodo principal de HPC de hello cuando se activa el trabajo de Hola.
      
      formato de Hola de $CCP_NODES_CORES sigue este patrón:
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      donde
      
      * `<Number of nodes>`-número de Hola de nodos asignados toothis trabajo.  
      * `<Name of node_n_...>`-nombre de Hola de cada nodo asignada toothis trabajo.
      * `<Cores of node_n_...>`-Hola número de núcleos en el trabajo de hello nodo toothis asignado.
      
      Por ejemplo, si el trabajo de hello necesita toorun de dos nodos, es similar a $CCP_NODES_CORES
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. Hola llamadas **mpirun** comando y anexa la línea de comandos de dos parámetros toohello.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-crea la ruta de acceso de Hola de script de Hola del archivo de host de Hola
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-una variable de entorno establecida por nodo de principal de HPC Pack hello, que almacena Hola número total de núcleos asignados toothis trabajo. En este caso, especifica el número de Hola de procesos de **mpirun**.

## <a name="submit-an-openfoam-job"></a>Envío de un trabajo OpenFOAM
Ahora puede enviar un trabajo en el Administrador de clústeres HPC. Necesitará toopass Hola script hpcimpirun.sh en líneas de comandos de Hola para algunas de las tareas de trabajo de Hola.

1. Conecte tooyour nodo principal del clúster e inicie el Administrador de clústeres HPC.
2. **En administración de recursos**, asegúrese de que sean nodos de proceso de Linux de Hola Hola **Online** estado. Si no lo están, selecciónelos y haga clic en **Conectar**.
3. En **Administración de trabajos**, haga clic en **Nuevo trabajo**.
4. Escriba un nombre para el trabajo como *sloshingTank3D*.
   
   ![Detalles del trabajo][job_details]
5. En **recursos de trabajo**, elija Hola tipo de recurso como "Nodo" y establezca Hola mínimo too2. Esta configuración ejecuta el trabajo de hello en dos nodos de Linux, cada uno de los cuales tiene ocho núcleos en este ejemplo.
   
   ![Recursos del trabajo][job_resources]
6. Haga clic en **editar tareas** en Hola de navegación izquierdo y, a continuación, haga clic en **agregar** tooadd un trabajo de toohello de tarea. Agregue cuatro tareas toohello trabajo con hello siguientes líneas de comandos y configuración.
   
   > [!NOTE]
   > Ejecuta `source /openfoam/settings.sh` configura entornos en tiempo de ejecución OpenFOAM y MPI de hello, por lo que cada uno de los siguiente las tareas de hello lo llama antes de hello OpenFOAM comando.
   > 
   > 
   
   * **Tarea 1**. Ejecutar **decomposePar** toogenerate archivos de datos para ejecutar **interDyMFoam** en paralelo.
     
     * Asignar una tarea de toohello de nodo
     * **Línea de comandos** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **Directorio de trabajo** : /openfoam/sloshingTank3D
     
     Vea Hola figura siguiente. Configurar las tareas restantes de Hola de forma similar.
     
     ![Detalles de la tarea 1][task_details1]
   * **Tarea 2**. Ejecutar **interDyMFoam** en el ejemplo de Hola a toocompute paralelas.
     
     * Asignar dos nodos toohello tarea
     * **Línea de comandos** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **Directorio de trabajo** : /openfoam/sloshingTank3D
   * **Tarea 3**. Ejecutar **reconstructPar** toomerge Hola conjuntos de directorios de tiempo de cada directorio processor_N_ en un único conjunto.
     
     * Asignar una tarea de toohello de nodo
     * **Línea de comandos** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **Directorio de trabajo** : /openfoam/sloshingTank3D
   * **Tarea 4**. Ejecutar **foamToEnsight** en paralelo tooconvert archivos de resultados de hello OpenFOAM en EnSight, dar formato y coloque los archivos de EnSight de hello en un directorio denominado Ensight en directorio mayúsculas Hola.
     
     * Asignar dos nodos toohello tarea
     * **Línea de comandos** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **Directorio de trabajo** : /openfoam/sloshingTank3D
7. Agregar tareas de toothese de dependencias de forma ascendente de la tarea.
   
   ![Dependencias de las tareas][task_dependencies]
8. Haga clic en **enviar** toorun este trabajo.
   
   De forma predeterminada, HPC Pack envía trabajo hello como su cuenta de usuario que ha iniciado la sesión actual. Tras hacer clic en **enviar**, verá un cuadro de diálogo solicitándole que tooenter Hola nombre y contraseña.
   
   ![Credenciales del trabajo][creds]
   
   En determinadas condiciones, HPC Pack recuerda la información de usuario de hello antes de entrada y no mostrar este cuadro de diálogo. toomake HPC Pack mostrarla de nuevo, escriba Hola siguiente comando en un símbolo del sistema y, a continuación, enviar el trabajo de Hola.
   
   ```
   hpccred delcreds
   ```
9. trabajo con Hello tarda de decenas de minutos tooseveral horas según los parámetros de toohello que haya definido para el ejemplo hello. En el mapa térmico de hello, vea trabajo hello en ejecución hello en nodos de Linux. 
   
   ![Mapa térmico][heat_map]
   
   En cada nodo se inician ocho procesos.
   
   ![Procesos de Linux][linux_processes]
10. Cuando finalice el trabajo de hello, buscar resultados de trabajo de hello en las carpetas bajo C:\OpenFoam\sloshingTank3D y archivos de registro de hello en C:\OpenFoam.

## <a name="view-results-in-ensight"></a>Visualización de los resultados en EnSight
Utilizar opcionalmente [EnSight](https://www.ceisoftware.com/) toovisualize y analizar los resultados de Hola de trabajo de OpenFOAM Hola. Para obtener más información acerca de la visualización y la animación en EnSight, consulte esta [guía de vídeo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).

1. Después de instalar EnSight en el nodo principal de hello, inícielo.
2. Abra C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.
   
   Verá un depósito en el Visor de Hola.
   
   ![Depósito de EnSight][tank]
3. Crear un **Isosurface** de **internalMesh**y, a continuación, elija variable hello **alpha_water**.
   
   ![Crear una isosuperficie][isosurface]
4. Establecer color de Hola para **Isosurface_part** creado en el paso anterior de Hola. Por ejemplo, establézcala toowater azul.
   
   ![Editar color de la isosuperficie][isosurface_color]
5. Crear un **Iso-volume** de **paredes** seleccionando **paredes** en hello **elementos** panel y haga clic en hello **Isosurfaces**  botón de barra de herramientas de Hola.
6. En el cuadro de diálogo de hello, seleccione **tipo** como **Isovolume** y establezca Hola Min de **Isovolume intervalo** too0.5. toocreate Hola isovolume, haga clic en **crear con partes seleccionadas**.
7. Establecer color de Hola para **Iso_volume_part** creado en el paso anterior de Hola. Por ejemplo, establézcala toodeep agua azul.
8. Establecer color de Hola para **paredes**. Por ejemplo, establézcala tootransparent blanco.
9. Ahora haga clic en **reproducir** resultados de hello toosee de simulación de Hola.
   
    ![Depósito resultante][tank_result]

## <a name="sample-files"></a>Archivos de ejemplo
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Archivo de configuración XML de ejemplo para la implementación de clústeres mediante scripts de PowerShell
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a>Archivo cred.xml de ejemplo
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>Ejemplo silent.cfg archivo tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>Script de ejemplo settings.sh
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>Script hpcimpirun.sh de ejemplo
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
