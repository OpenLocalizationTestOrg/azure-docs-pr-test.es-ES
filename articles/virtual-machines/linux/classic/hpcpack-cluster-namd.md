---
title: "aaaNAMD con Microsoft HPC Pack en máquinas virtuales de Linux | Documentos de Microsoft"
description: "Implementación de un clúster de Microsoft HPC Pack en Azure y ejecución de una simulación de NAMD con charmrun en varios nodos de proceso de Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>Ejecución de NAMD con Microsoft HPC Pack en nodos de proceso de Linux en Azure
Este artículo muestra una manera de toorun una carga de trabajo de informática de alto rendimiento (HPC) de Linux en máquinas virtuales de Azure. En este caso, configure un [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) de Cluster Server en Azure con nodos de proceso de Linux y ejecutar un [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate de simulación y visualizar la estructura de Hola de un sistema grande biomoleculares.  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** (para el programa de Dynamics Molecular Nanoscale) es un paquete de dynamics molecular paralelo diseñado para simulación de alto rendimiento de los sistemas de gran tamaño biomoleculares que contiene una toomillions de subcomponentes. Algunos ejemplos de estos sistemas son virus, estructuras celulares y proteínas grandes. NAMD escala toohundreds de núcleos para simulaciones típicos y toomore a 500.000 núcleos para simulaciones de hello más grandes.
* **Microsoft HPC Pack** proporciona características toorun HPC a gran escala y aplicaciones en paralelo en clústeres de equipos locales o máquinas virtuales de Azure. HPC Pack, que se desarrolló originalmente como una solución para cargas de trabajo de Windows HPC, ahora admite la ejecución de las aplicaciones HPC Linux en máquinas virtuales de nodos de proceso de Linux implementadas en un clúster de HPC Pack. Consulte [Introducción a los nodos de ejecución de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para obtener información.

Para otro toorun opciones Linux HPC cargas de trabajo en Azure, consulte [recursos técnicos para el lote e informática de alto rendimiento](../../../batch/batch-hpc-solutions.md).

## <a name="prerequisites"></a>Requisitos previos
* **Clúster de HPC Pack con nodos de ejecución de Linux**: implemente un clúster de HPC Pack con nodos de proceso de Linux en Azure utilizando una [plantilla de Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o un [script de Azure PowerShell](hpcpack-cluster-powershell-script.md). Vea [empezar a trabajar con nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md) para requisitos previos de Hola y pasos para cualquiera de las opciones. Si elige Hola opción de implementación de secuencia de comandos de PowerShell, vea el archivo de configuración de ejemplo de Hola en archivos de ejemplo de Hola final Hola de este artículo. Este archivo configura un clúster basado en Azure HPC Pack que consta de un nodo principal de Windows Server 2012 R2 y cuatro nodos de ejecución de tamaño grande CentOS 6.6. Adapte este archivo según las necesidades de su entorno.
* **Archivos de software y un tutorial NAMD** -software NAMD descargar para Linux de hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) sitio (es necesario registrarse). En este artículo se basa en NAMD versión 2.10 y usa hello [x86_64 de Linux (64-bit Intel o AMD con Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive. Descargar hello [archivos del tutorial NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd). descargas de Hello son archivos .tar y necesita un archivos de Windows herramienta tooextract hello en el nodo principal del clúster de Hola. archivos de hello tooextract, siga las instrucciones de hello más adelante en este artículo. 
* **VMD** (opcional): resultados de hello toosee de su trabajo NAMD, descargue e instale programas de visualización molecular hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) en un equipo de su elección. versión actual de Hello es 1.9.2. Vea Hola VMD descargar tooget de sitio que se inició.  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Configuración de la confianza mutua entre nodos de proceso
Ejecutar un trabajo de entre nodos en varios nodos de Linux requiere Hola nodos tootrust entre sí (por **rsh** o **ssh**). Cuando se crea el clúster de HPC Pack Hola con hello script de implementación de Microsoft HPC Pack IaaS, script de Hola configura automáticamente una confianza mutua permanente para cuenta de administrador de Hola que especifique. Para crear en el dominio del clúster de Hola de los usuarios sin privilegios de administrador, deberá tooset temporal confianza mutua entre los nodos de hello cuando un trabajo se asigna a toothem. A continuación, destruir relación Hola una vez completado el trabajo de Hola. toodo esto para cada usuario, proporcione un clúster de toohello del par de claves de RSA que HPC Pack utiliza la relación de confianza de tooestablish Hola. A continuación figuran las instrucciones.

### <a name="generate-an-rsa-key-pair"></a>Generación de un par de claves RSA
Resulta fácil toogenerate un par de claves de RSA, que contiene una clave pública y una clave privada y, a continuación, ejecutando Hola Linux **ssh-keygen** comando.

1. Inicie sesión en tooa equipo Linux.
2. Ejecute el siguiente comando de hello:
   
   ```bash
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
1. [Conectarse mediante Escritorio remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nodo principal VM con Hola credenciales de dominio que ha proporcionado al implementar el clúster de hello (por ejemplo, hpc\clusteradmin). Administrar clústeres de Hola desde el nodo principal de Hola.
2. Utilice toocreate estándar de procedimientos de Windows Server una cuenta de usuario de dominio dominio del clúster de hello de Active Directory. Por ejemplo, usar hello usuario de Active Directory y la herramienta de equipos en el nodo principal de Hola. ejemplos de Hello en este artículo se supone que crea un usuario de dominio denominado hpcuser en el dominio de hello hpclab (hpclab\hpcuser).
3. Agregar clúster de HPC Pack de toohello de usuario de dominio de Hola como un usuario del clúster. Para obtener instrucciones, consulte [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx)(Adición o eliminación de usuarios de clúster).
4. Cree un archivo denominado C:\cred.xml y copiar datos de clave de RSA de hello en él. Puede encontrar un ejemplo de Hola archivos de ejemplo al final de Hola de este artículo.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. Abra un símbolo del sistema y escriba el siguiente comando hello tooset credenciales datos para hello hpclab\hpcuser cuenta de hello. Usar hello **extendeddata** toopass parámetro Hola nombre del archivo de C:\cred.xml Hola que creó para los datos clave Hola.
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Este comando se completa correctamente sin salida. Después de establecer las credenciales de Hola Hola para cuentas de usuario que necesita toorun trabajos, almacenar el archivo de cred.xml hello en una ubicación segura o elimínelo.
6. Si ha generado el par de claves RSA de hello en uno de los nodos de Linux, recuerde que las claves de hello toodelete cuando termine de utilizarlos. HPC Pack no establece una confianza mutua si encuentra un archivo id_rsa o id_rsa.pub existente.

> [!IMPORTANT]
> No se recomienda ejecutar un trabajo de Linux como un administrador de clústeres en un clúster compartido, porque un trabajo enviado por un administrador se ejecuta con la cuenta raíz de Hola Hola en nodos de Linux. Un trabajo enviado por un usuario sin privilegios de administrador se ejecuta bajo una cuenta de usuario local de Linux con hello mismo nombre como usuario de trabajo de Hola. En este caso, HPC Pack establece la confianza mutua para este usuario de Linux en todos los nodos de hello asignados toohello trabajo. Puede configurar el usuario de Linux Hola manualmente hello en nodos de Linux antes de ejecutar el trabajo de Hola o HPC Pack crea usuario Hola automáticamente cuando se envía el trabajo de Hola. Si HPC Pack crea usuario hello, HPC Pack se elimina una vez completado el trabajo de Hola. tooreduce amenaza para la seguridad, Hola se quitan las claves al finalizar la tarea hello en nodos de Hola.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Configuración de un recurso compartido de archivos para nodos de Linux
Ahora configurar un recurso compartido de archivos SMB y montar la carpeta compartida de hello en todos los nodos tooallow Hola Linux nodos tooaccess NAMD archivos de Linux con una ruta de acceso común. Estos son los pasos toomount una carpeta compartida en el nodo principal de Hola. Se recomienda un recurso compartido de distribuciones como CentOS 6.6 que actualmente no son compatibles con los servicios de archivos de Azure de Hola. Si los nodos de Linux compatibles con un recurso compartido de archivos de Azure, consulte [cómo toouse almacenamiento de archivos de Azure con Linux](../../../storage/files/storage-how-to-use-files-linux.md). Para consultas las opciones de uso compartido de archivos con HPC Pack, consulte [Introducción a los nodos de proceso de Linux en un clúster de HPC Pack en Azure](hpcpack-cluster.md).

1. Cree una carpeta en el nodo principal de Hola y compártala tooEveryone estableciendo privilegios de lectura/escritura. En este ejemplo, \\ \\CentOS66HN\Namd es el nombre de Hola de carpeta de hello, donde CentOS66HN es el nombre de host de hello del nodo principal de Hola.
2. Cree una subcarpeta denominada namd2 en la carpeta compartida de Hola. En namd2, cree otra subcarpeta denominada namdsample.
3. Extraiga los archivos NAMD de Hola de carpeta de hello mediante una versión de Windows de **tar** u otra utilidad de Windows que funciona en los archivos .tar. 
   
   * Extraer el archivo tar de hello NAMD demasiado\\\\CentOS66HN\Namd\namd2.
   * Extraer archivos del tutorial Hola en \\ \\CentOS66HN\Namd\namd2\namdsample.
4. Abra una ventana de Windows PowerShell y ejecute hello siga los comandos toomount Hola carpeta compartida hello en nodos de Linux.
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Hola primer comando crea una carpeta denominada /namd2 en todos los nodos de grupo de LinuxNodes Hola. segundo comando de Hello monta Hola compartido carpeta //CentOS66HN/Namd/namd2 en la carpeta de hello con dir_mode y file_mode too777 de conjunto de bits. Hola *nombre de usuario* y *contraseña* Hola comando debe ser credenciales de Hola de un usuario en el nodo principal de Hola.

> [!NOTE]
> Hola "\`" símbolo en el segundo comando de hello es un símbolo de escape de PowerShell. "\`,"significa Hola"," (coma) forma parte del comando de Hola.
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>Crear un toorun de secuencia de comandos de Bash un trabajo NAMD
El trabajo NAMD necesita un *nodelist* de archivos para **charmrun** toodetermine número de Hola de nodos toouse al iniciar NAMD procesos. Usar una secuencia de comandos de Bash que genera el archivo de lista de nodos de hello y se ejecuta **charmrun** con este archivo de lista de nodos. Después puede enviar un trabajo NAMD al administrador del clúster de HPC que llama a este script.

Con un editor de texto de su elección, cree una secuencia de comandos de Bash en carpeta de /namd2 de Hola que contiene los archivos de programa Hola NAMD y asígnele el nombre hpccharmrun.sh. Para una rápida de prueba de concepto, copie el script de hpccharmrun.sh de ejemplo de Hola Hola final de este artículo y vaya demasiado[enviar un trabajo NAMD](#submit-a-namd-job).

> [!TIP]
> Guarde el script como un archivo de texto con terminaciones de línea de Linux (solo LF, no CR LF). Esto garantiza que se ejecuta correctamente hello en nodos de Linux.
> 
> 

A continuación, encontrará información sobre lo que hace este script de Bash. 

1. Defina algunas variables.
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. Obtener información sobre el nodo de variables de entorno de Hola. $NODESCORES almacena una lista de palabras divididas de CCP_NODES_CORES $. $COUNT es el tamaño de Hola de $NODESCORES.
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   formato de Hello para la variable de hello $CCP_NODES_CORES es el siguiente:
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   Esta variable muestra hello número total de nodos, nombres de nodo y número de núcleos en cada nodo que se asignan toohello trabajo. Por ejemplo, si el trabajo de hello necesita 10 toorun de núcleos, valor de Hola de $CCP_NODES_CORES es similar a:
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. Si no se establece la variable de hello $CCP_NODES_CORES, inicie **charmrun** directamente. (Esto solo debe producirse al ejecutar este script directamente en los nodos de Linux).
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. O bien cree un archivo de lista de nodos para **charmrun**.
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. Ejecutar **charmrun** con el archivo de lista de nodos de hello, obtener su estado de retorno y quitar el archivo de lista de nodos de Hola Hola final.
   
   ${CCP_NUMCPUS} es otra variable de entorno establecida por el nodo principal de HPC Pack Hola. Almacena el número de hello total de núcleos asignados toothis trabajo. Usamos toospecify número de Hola de procesos para charmrun.
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. Salir con hello **charmrun** devolver el estado.
   
   ```
   exit ${RTNSTS}
   ```

A continuación encontrará información de hello en archivo de nodelist hello, qué secuencia de comandos de hello genera:

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

Por ejemplo:

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>Submit a NAMD job
Ahora está listo toosubmit un trabajo NAMD en el Administrador de clúster de HPC.

1. Conecte tooyour nodo principal del clúster e inicie el Administrador de clústeres HPC.
2. En **administración de recursos**, asegúrese de que sean nodos de proceso de Linux de Hola Hola **Online** estado. Si no lo están, selecciónelos y haga clic en **Conectar**.
3. En **Administración de trabajos**, haga clic en **Nuevo trabajo**.
4. Escriba un nombre para el trabajo como *hpccharmrun*.
   
   ![Nuevo trabajo HPC][namd_job]
5. En hello **detalles del trabajo** página, en **recursos de trabajo**, seleccione Hola tipo de recurso como **nodo** conjunto hello y **mínimo** too3. , se ejecuta el trabajo de hello en tres nodos de Linux y cada nodo tiene cuatro núcleos.
   
   ![Recursos del trabajo][job_resources]
6. Haga clic en **editar tareas** en Hola de navegación izquierdo y, a continuación, haga clic en **agregar** tooadd un trabajo de toohello de tarea.    
7. En hello **detalles de la tarea y redirección de E/S** Hola conjunto siguiente de valores de la página:
   
   * **Línea de comandos**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > Hello línea de comandos anterior es un comando único sin saltos de línea. Tooappear se ajusta en varias líneas en **línea de comandos**.
     > 
     > 
   * **Directorio de trabajo** - /namd2
   * **Mínimo** - 3
     
     ![Detalles de la tarea][task_details]
     
     > [!NOTE]
     > Establecer directorio de trabajo de hello aquí porque **charmrun** intenta toonavigate toohello mismo directorio de trabajo en cada nodo. Si no se ha configurado el directorio de trabajo de hello, HPC Pack inicia comando hello en una carpeta de forma aleatoria con nombre creada en uno de los nodos de Linux de Hola. Esto hace que Hola siguiente error en hello otros nodos: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid este problema, especifique una ruta de acceso de carpeta que puede tener acceso a todos los nodos como directorio de trabajo de Hola.
     > 
     > 
8. Haga clic en **Aceptar** y, a continuación, haga clic en **enviar** toorun este trabajo.
   
   De forma predeterminada, HPC Pack envía trabajo hello como su cuenta de usuario que ha iniciado la sesión actual. Un cuadro de diálogo le solicite tooenter Hola nombre y contraseña tras hacer clic en **enviar**.
   
   ![Credenciales del trabajo][creds]
   
   En determinadas condiciones, HPC Pack recuerda la información de usuario de hello antes de entrada y no mostrar este cuadro de diálogo. toomake HPC Pack mostrarla de nuevo, escriba Hola siguiente comando en un símbolo del sistema y, a continuación, enviar el trabajo de Hola.
   
   ```command
   hpccred delcreds
   ```
9. trabajo con Hello tarda varios toofinish minutos.
10. Buscar el registro de trabajo de hello en \\ <headnodeName>en los archivos de salida de hello y \Namd\namd2\namd2_hpccharmrun.log \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. Si lo desea, inicie VMD tooview los resultados del trabajo. pasos de Hola para visualizar los archivos de salida de hello NAMD (en este caso, un moléculas de proteínas ubiquitin en una esfera de agua) son más allá del ámbito de Hola de este artículo. Consulte el [tutorial de NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) para obtener más información.
    
    ![Resultados del trabajo][vmd_view]

## <a name="sample-files"></a>Archivos de ejemplo
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Archivo de configuración XML de ejemplo para la implementación de clústeres mediante scripts de PowerShell
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
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

### <a name="sample-hpccharmrunsh-script"></a>Script hpccharmrun.sh de ejemplo
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
