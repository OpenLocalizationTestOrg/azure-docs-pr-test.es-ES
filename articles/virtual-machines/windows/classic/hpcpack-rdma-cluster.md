---
title: "aaaSet un aplicaciones de MPI RDMA Windows clúster toorun | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un clúster de Windows HPC Pack con tamaño H16r, H16mr, A8 o A9 VM toouse Hola aplicaciones MPI de toorun de red RDMA de Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>Configurar un clúster de Windows RDMA con aplicaciones de MPI de HPC Pack toorun
Configurar un clúster de Windows RDMA en Azure con [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) y [tamaños de máquinas virtuales de proceso de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun aplicaciones de interfaz de paso de mensajes (MPI) paralelas. Cuando configura nodos basados en Windows Server compatibles con RDMA en un clúster de HPC Pack, las aplicaciones de MPI se comunican eficazmente a través de una red de latencia baja y rendimiento alto en Azure que está basada en tecnología de acceso directo a memoria remota (RDMA).

Si desea que las cargas de trabajo MPI de toorun en máquinas virtuales de Linux red acceso Hola RDMA de Azure, consulte [configurar una aplicación de MPI de Linux RDMA clúster toorun](../../linux/classic/rdma-cluster.md).

## <a name="hpc-pack-cluster-deployment-options"></a>Opciones de implementación de clústeres de HPC Pack
Microsoft HPC Pack es una herramienta proporcionada en ningún coste adicional toocreate de clústeres de HPC local o en Azure toorun Windows o aplicaciones de HPC de Linux. HPC Pack incluye un entorno en tiempo de ejecución para la implementación de Microsoft de Hola de hello mensaje pasando interfaz para Windows (MS-MPI). Cuando se usa con compatibles con RDMA instancias que se ejecutan un sistema operativo compatible de Windows Server, HPC Pack proporciona una aplicación de MPI Windows toorun opción eficaz esa red RDMA de Azure de Hola de acceso. 

Este artículo presenta dos escenarios y vincula toodetailed tooset de instrucciones de un clúster de Windows RDMA con Microsoft HPC Pack. 

* Escenario 1. Implementación de instancias de rol de trabajo de proceso intensivo (PaaS)
* Escenario 2. Implementación de nodos de proceso en máquinas virtuales de proceso intensivo (IaaS)

Para las instancias de proceso intensivo de requisitos previos generales toouse con Windows, vea [tamaños de máquinas virtuales de proceso de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>Escenario 1: Implementación de instancias de rol de trabajo de proceso intensivo (PaaS)
En un clúster de HPC Pack existente, agregue recursos de proceso adicionales en instancias de rol de trabajo de Azure (nodos de Azure) que se ejecutan en un servicio en la nube (PaaS). Esta característica, también denominada "tooAzure ráfaga" de HPC Pack, admite una variedad de tamaños para instancias de rol de trabajo de Hola. Al agregar hello nodos de Azure, especifique uno de los tamaños de hello compatibles con RDMA.

Siguientes son consideraciones y los pasos tooburst tooRDMA compatible con instancias de Azure desde una existente (normalmente local) clúster. Utilice similar procedimientos tooadd trabajo rol instancias tooan HPC Pack nodo principal que se implementa en una máquina virtual de Azure.

> [!NOTE]
> Para una tooAzure tooburst tutorial con HPC Pack, consulte [configurar un clúster híbrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Tenga en cuenta las consideraciones de Hola Hola siguiendo los pasos que se aplican específicamente de los nodos de Azure compatibles con tooRDMA.
> 
> 

![Ráfaga tooAzure][burst]

### <a name="steps"></a>Pasos
1. **Implementación y configuración de un nodo principal de HPC Pack 2012 R2**
   
    Descargue el paquete de instalación de HPC Pack más reciente de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922). Para los requisitos e instrucciones tooprepare para ver una implementación de ráfaga de Azure, consulte [tooAzure instancias de trabajo con Microsoft HPC Pack en ráfagas](https://technet.microsoft.com/library/gg481749.aspx).
2. **Configurar un certificado de administración en hello suscripción de Azure**
   
    Configurar una conexión de hello certificado toosecure entre el nodo principal de Hola y Azure. Para las opciones y los procedimientos, consulte [Hola de escenarios tooConfigure certificado de administración de Azure para HPC Pack](http://technet.microsoft.com/library/gg481759.aspx). Para las implementaciones de prueba, HPC Pack instala un certificado predeterminado de Microsoft HPC Azure administración puede cargar rápidamente tooyour suscripción de Azure.
3. **Crear un nuevo servicio en la nube y una cuenta de almacenamiento**
   
    Usar hello Azure toocreate portal un servicio de nube y una cuenta de almacenamiento para la implementación de hello en una región donde estén disponibles las instancias de hello compatibles con RDMA.
4. **Crear una plantilla de nodo de Azure**
   
    Usar hello crear Asistente de plantilla de nodo en el Administrador de clúster de HPC. Para conocer los pasos, consulte [crear una plantilla de nodo de Azure](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) en "Pasos tooDeploy nodos de Azure con Microsoft HPC Pack".
   
    Para las pruebas iniciales, es recomendable configurar una directiva de disponibilidad manual en la plantilla de Hola.
5. **Agregar nodos toohello clúster**
   
    Usar hello Asistente de agregar nodo en el Administrador de clúster de HPC. Para obtener más información, consulte [toohello agregar nodos de Azure Windows HPC Cluster](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add).
   
    Al especificar el tamaño de Hola de nodos de hello, seleccione uno de los tamaños de instancias compatible con RDMA Hola.
   
   > [!NOTE]
   > En cada implementación de tooAzure ráfaga con instancias de proceso intensivo de hello, HPC Pack implementa automáticamente un mínimo de dos instancias compatible con RDMA (por ejemplo, A8) como nodos de proxy, además toohello instancias de rol de trabajador de Azure especifique. nodos de proxy de Hello usan núcleos que se asignan toohello suscripción y cargos junto con instancias de rol de trabajador de Azure Hola.
   > 
   > 
6. **Iniciar (provisión) de nodos de Hola y ponerlos en línea toorun trabajos**
   
    Seleccionar nodos de Hola y usar hello **iniciar** acción en el Administrador de clúster de HPC. Cuando se complete el aprovisionamiento, seleccione los nodos de Hola y usar hello **poner en conexión** acción en el Administrador de clúster de HPC. nodos de Hello son trabajos toorun listo.
7. **Enviar clúster toohello de trabajos**
   
   Utilice los trabajos de clúster de HPC Pack trabajo envío herramientas toorun. Consulte [Microsoft HPC Pack: Administración de trabajos](http://technet.microsoft.com/library/jj899585.aspx).
8. **Detener (desaprovisionar) Hola nodos**
   
   Cuando haya terminado de trabajos en ejecución, desconecte los nodos de Hola y usar hello **detener** acción en el Administrador de clúster de HPC.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>Escenario 2: Implementación de nodos de ejecución en máquinas virtuales de proceso intensivo (IaaS)
En este escenario, implemente nodo principal de HPC Pack hello y nodos de proceso del clúster en máquinas virtuales en una red virtual de Azure. HPC Pack ofrece varias [opciones de implementación de máquinas virtuales de Azure](../../linux/hpcpack-cluster-options.md), incluidos los scripts de implementación automatizados y las plantillas de inicio rápido de Azure. Por ejemplo, Hola siguientes consideraciones y pasos le guiarán hello toouse [script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) para automatizar la implementación de Hola de un clúster de HPC Pack 2012 R2 en Azure.

![Clúster en máquinas virtuales de Azure][iaas]

### <a name="steps"></a>Pasos
1. **Crear un nodo principal del clúster y máquinas virtuales de nodos de proceso mediante la ejecución de script de implementación de IaaS de HPC Pack hello en un equipo cliente**
   
    Descargar paquete de Script de implementación de IaaS de HPC Pack Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922).
   
    equipo de cliente de tooprepare hello, crear el archivo de configuración del script de Hola y script de ejecución hello, consulte [crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md). 
   
    nodos de proceso toodeploy compatibles con RDMA, Hola nota siguiente consideraciones adicionales:
   
   * **Red virtual**: especificar una nueva red virtual en una región en qué Hola compatible con RDMA y tamaño de las instancias que desea toouse está disponible.
   * **Sistema operativo Windows Server**: toosupport la conectividad RDMA, especifique un sistema operativo Windows Server 2012 R2 o Windows Server 2012 para máquinas virtuales de nodos de proceso de Hola.
   * **Servicios en la nube**: se recomienda implementar el nodo principal en un servicio en la nube y los nodos de ejecución en otro diferente.
   * **Tamaño de nodo principal**: en este escenario, considere la posibilidad de un tamaño de al menos A4 (Extra grande) para el nodo principal de Hola.
   * **Extensión HpcVmDrivers**: script de implementación de hello instala Hola agente de máquina virtual de Azure y Hola extensión HpcVmDrivers automáticamente al implementar nodos de cálculo de tamaño A8 o A9 con un sistema operativo Windows Server. HpcVmDrivers instala a controladores en máquinas virtuales de nodos de proceso de Hola para que puedan conectarse toohello de red RDMA. En máquinas virtuales compatibles con RDMA H-series, debe instalar manualmente la extensión HpcVmDrivers de Hola. Consulte [Tamaños de máquina virtual de procesos de alto rendimiento](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   * **Configuración de red de clúster**: script de implementación de hello configura automáticamente de clúster de HPC Pack hello en la topología 5 (todos los nodos de red de empresa de hello). Esta topología es obligatoria para todas las implementaciones de clúster de HPC Pack en máquinas virtuales. No cambie topología de red de clúster de hello más tarde.
2. **Poner los nodos de proceso de hello trabajos toorun en línea**
   
    Seleccionar nodos de Hola y usar hello **poner en conexión** acción en el Administrador de clúster de HPC. nodos de Hello son trabajos toorun listo.
3. **Enviar clúster toohello de trabajos**
   
    Conectar los trabajos de toosubmit del nodo principal de toohello o configurar esto un toodo del equipo local. Para obtener información, consulte [tooan enviar trabajos HPC cluster en Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
4. **Take Hola nodos sin conexión y detenga (desasigne) ellos**
   
    Cuando haya terminado de trabajos en ejecución, ponga sin conexión los nodos de hello en el Administrador de clúster de HPC. A continuación, use administración de Azure tools tooshut ellas hacia abajo.

## <a name="run-mpi-applications-on-hello-cluster"></a>Ejecutar aplicaciones MPI en clúster de Hola
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>Ejemplo: Ejecutar mpipingpong en un clúster de HPC Pack
una implementación de HPC Pack de instancias de hello compatibles con RDMA, ejecute tooverify Hola HPC Pack **mpipingpong** comando clúster Hola. **MPIPingPong** envía paquetes de datos entre nodos emparejados repetidamente toocalculate latencia de las medidas de rendimiento y las estadísticas de red de la aplicación habilitada para RDMA de Hola. Este ejemplo muestra un patrón típico para ejecutar un trabajo de MPI (en este caso, **mpipingpong**) mediante el uso de clústeres de hello **mpiexec** comando.

En este ejemplo se da por supuesto que agregó nodos de Azure en una configuración "irrumpir tooAzure" ([escenario 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article). Si ha implementado HPC Pack en un clúster de máquinas virtuales de Azure, podrá necesita toospecify de sintaxis de comando toomodify Hola otro grupo de nodos y establecer la red de toohello de tráfico de red RDMA de entorno adicionales variables toodirect.

toorun mpipingpong en clúster de hello:

1. En el nodo principal de Hola o en un equipo cliente configurado correctamente, abra un símbolo del sistema.
2. tooestimate latencia entre pares de nodos en una implementación de ráfaga de Azure de cuatro nodos, Hola de tipo siguientes comando toosubmit un mpipingpong de toorun de trabajo con un tamaño de paquete pequeño y el número de iteraciones:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    comando de Hello devuelve Hola identificador de trabajo de Hola que se envía.
   
    Si implementa el clúster de HPC Pack Hola implementado en máquinas virtuales de Azure, especifique un grupo de nodos que contiene máquinas virtuales de nodos que se implementan en un servicio de nube única de proceso y modificar hello **mpiexec** comando como sigue:
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Cuando se completa el trabajo de hello, tooview Hola de salida (en este caso, la salida de hello de la tarea 1 del trabajo de hello) Hola de tipo siguientes
   
    ```Command
    task view <JobID>.1
    ```
   
    donde &lt; *JobID* &gt; es Hola identificador de trabajo de Hola que se envió.
   
    salida de Hello incluye similar toohello siguiente de resultados de latencia.
   
    ![Latencia de ping pong][pingpong1]
4. nodos de ráfaga de rendimiento de tooestimate entre pares de Azure, escriba lo siguiente Hola comando toosubmit un toorun trabajo **mpipingpong** con un tamaño de paquete grande y unas pocas iteraciones:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    comando de Hello devuelve Hola identificador de trabajo de Hola que se envía.
   
    En un clúster de HPC Pack implementado en máquinas virtuales de Azure, modifique el comando de hello como se indicó en el paso 2.
5. Cuando se completa el trabajo de hello, tooview Hola de salida (en este caso, la salida de hello de la tarea 1 del trabajo de hello) Hola de tipo siguientes:
   
    ```Command
    task view <JobID>.1
    ```
   
   salida de Hello incluye similar toohello siguiente de resultados de rendimiento.
   
   ![Capacidad de procesamiento de ping pong][pingpong2]

### <a name="mpi-application-considerations"></a>Consideraciones de las aplicaciones de MPI
Las siguientes son consideraciones que hay que tener en cuenta para ejecutar aplicaciones de MPI con HPC Pack en Azure. Algunas aplican solo toodeployments de nodos de Azure (instancias de rol de trabajo agregados en una configuración de "ráfaga tooAzure").

* Azure reaprovisiona periódicamente y sin previo aviso las instancias de rol de trabajo en un servicio en la nube (por ejemplo, para el mantenimiento del sistema o en caso de errores en una instancia). Si se reaprovisiona una instancia mientras se está ejecutando un trabajo de MPI, instancia de hello pierde sus datos y devuelve el estado de toohello cuando se implementó por primera vez, lo que puede provocar toofail de trabajo MPI Hola. Hello más nodos que usará para un único trabajo MPI y Hola ya hello trabajo se ejecuta, hello más probable que una de las instancias de Hola se volverá a aprovisionar mientras se ejecuta un trabajo. También tenga en cuenta esto si designa un único nodo en la implementación de Hola como un servidor de archivos.
* toorun trabajos MPI en Azure, no tiene instancias de toouse Hola compatibles con RDMA. Puede usar cualquier tamaño de instancia admitido por HPC Pack. Sin embargo, se recomienda usar instancias de compatible con RDMA de Hola para ejecutar trabajos de MPI de escala relativamente grande son confidenciales toohello latencia y ancho de banda de Hola de red de Hola que conecta los nodos de Hola. Si usa otros trabajos MPI de tamaños toorun dependientes de la latencia y el ancho de banda, se recomienda ejecutar trabajos pequeños, en el que una sola tarea se ejecuta en pocos nodos.
* Las aplicaciones implementadas tooAzure instancias son toohello asunto asociados con la aplicación hello de términos de licencia. Póngase en contacto con el proveedor de Hola de cualquier aplicación comercial de licencia o a otras restricciones para la ejecución en la nube de Hola. No todos los proveedores ofrecen licencias de pago por uso.
* Instancias de Azure necesitan configurar aún más nodos de tooaccess locales, recursos compartidos y servidores de licencias. Por ejemplo, hello tooenable tooaccess de nodos de Azure un servidor de licencias local, puede configurar una red virtual de Azure de sitio a sitio.
* toorun de aplicaciones de MPI en instancias de Azure, registrar cada aplicación de MPI con Firewall de Windows en las instancias de hello ejecutando hello **hpcfwutil** comando. Esto permite tootake lugar de las comunicaciones de MPI en un puerto asignado dinámicamente por firewall de Hola.
  
  > [!NOTE]
  > Para las implementaciones de irrupción tooAzure, también puede configurar una toorun de comando de excepción de firewall automáticamente en todos los nodos de Azure nuevos que se agregan tooyour clúster. Después de ejecutar hello **hpcfwutil** de comandos y compruebe que la aplicación funciona, agregar el script de inicio de tooa de comando de Hola para los nodos de Azure. Para más información, consulte [Uso de un script de inicio para los nodos de Azure](https://technet.microsoft.com/library/jj899632.aspx).
  > 
  > 
* HPC Pack usa hello CCP_MPI_NETMASK clúster entorno variable toospecify un intervalo de direcciones aceptables para la comunicación de MPI. A partir de HPC Pack 2012 R2, variable de entorno de clúster de hello CCP_MPI_NETMASK solo afecta a la comunicación de MPI entre nodos de proceso Unidos a un dominio de clúster (de forma local o en máquinas virtuales de Azure). variable de saludo se omite por los nodos agregados en una configuración de tooAzure de ráfaga.
* No se pueden ejecutar trabajos de MPI en instancias de Azure que se implementan en servicios de nube diferente (por ejemplo, en las implementaciones de tooAzure ráfaga con distintas plantillas de nodo o nodos de proceso de máquina virtual de Azure implementados en varios servicios de nube). Si tiene varias implementaciones de nodos de Azure que se inician con distintas plantillas de nodo, debe ejecutar trabajo de MPI hello en solo un conjunto de nodos de Azure.
* Al agregar nodos de Azure tooyour clúster y ponerlos en línea, Hola servicio Programador de trabajos de HPC inmediatamente intenta toostart trabajos en nodos de Hola. Si solo una parte de la carga de trabajo puede ejecutarse en Azure, asegúrese de actualizar o crear trabajo plantillas toodefine qué trabajo tipos pueden ejecutar en Azure. Por ejemplo, tooensure que los trabajos enviados con una plantilla de trabajo solo se ejecutan en nodos de Azure, Agregar plantilla de trabajo de toohello de propiedad de nodo grupos de Hola y seleccione AzureNodes como Hola valor requerido. toocreate grupos personalizados para los nodos de Azure, utilice el cmdlet de PowerShell de HPC de Add-HpcGroup Hola.

## <a name="next-steps"></a>Pasos siguientes
* Como una alternativa toousing HPC Pack, desarrollar con hello Azure Batch servicio toorun aplicaciones de MPI en bloques administrados de nodos de proceso de Azure. Vea [varias instancias de uso tareas toorun las aplicaciones de interfaz de paso de mensajes (MPI) en Azure Batch](../../../batch/batch-mpi.md).
* Si desea que toorun Linux MPI las aplicaciones que tienen acceso a la red RDMA de Azure de hello, vea [configurar una aplicación de MPI de Linux RDMA clúster toorun](../../linux/classic/rdma-cluster.md).

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
