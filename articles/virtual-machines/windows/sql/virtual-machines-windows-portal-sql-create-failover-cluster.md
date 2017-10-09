---
title: "aaaSQL servidor FCI - máquinas virtuales de Azure | Documentos de Microsoft"
description: "Este artículo se explica cómo toocreate instancia de clúster de conmutación por error SQL Server en máquinas virtuales de Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Configuración de una instancia de clúster de conmutación por error de SQL Server en Azure Virtual Machines

Este artículo explica cómo toocreate una conmutación por error SQL Server Cluster (FCI) de la instancia en máquinas virtuales de Azure en el modelo de administrador de recursos. Esta solución usa [espacios de almacenamiento directo de Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) como una SAN virtual basada en software que sincroniza el almacenamiento de hello (discos de datos) entre los nodos de hello (máquinas virtuales de Azure) en un Clúster de Windows. S2D es una novedad de Windows Server 2016.

Hello siguiente diagrama muestra la solución completa de hello en máquinas virtuales de Azure:

![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Hola anterior diagrama muestra:

- Dos máquinas virtuales de Azure en un clúster de conmutación por error de Windows. Cuando una máquina virtual está en un clúster de conmutación por error también se denomina un *nodo de clúster* o *nodos*.
- Cada máquina virtual tiene dos, o más, discos de datos.
- S2D sincroniza los datos de hello en disco de datos de Hola y presenta Hola sincronizado almacenamiento como un grupo de almacenamiento.
- grupo de almacenamiento de Hello presenta un clúster de conmutación por error de clúster volumen compartido (CSV) toohello.
- rol de clúster de SQL Server FCI Hello usa Hola CSV hello las unidades de datos.
- Una carga de Azure equilibrador toohold Hola dirección IP para hello FCI de SQL Server.
- Un conjunto de disponibilidad de Azure contiene todos los recursos de Hola.

   >[!NOTE]
   >Todos los recursos de Azure están en el diagrama de hello en hello mismo grupo de recursos.

Para más información acerca de S2D, consulte [Espacios de almacenamiento directo \(S2D\) de Windows Server 2016 Datacenter Edition](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

S2D admite dos tipos de arquitecturas, convergidas e hiperconvergidas. arquitectura de Hello en este documento es hiperconvergente. Un almacenamiento de hello hiperconvergente infraestructura lugares en Hola mismos servidores esa aplicación hello en clúster de host. En esta arquitectura, el almacenamiento de hello es en cada nodo de FCI de SQL Server.

### <a name="example-azure-template"></a>Plantilla de Azure de ejemplo

Puede crear toda la solución hello en Azure desde una plantilla. Un ejemplo de una plantilla está disponible en hello GitHub [plantillas de inicio rápido de Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). Este ejemplo no se ha diseñado para ninguna carga de trabajo específica ni se ha probado para ella. Puede ejecutar Hola plantilla toocreate una FCI de SQL Server con dominio de S2D almacenamiento tooyour conectado. Puede evaluar la plantilla de Hola y modificarlo para sus fines.

## <a name="before-you-begin"></a>Antes de empezar

Hay algunas cosas que debe tooknow y un par de cosas que necesita en su lugar antes de continuar.

### <a name="what-tooknow"></a>¿Qué tooknow
Debe estar familiarizado operativa de hello siguientes tecnologías:

- [Tecnologías de clúster de Windows](http://technet.microsoft.com/library/hh831579.aspx)
-  [Instancias del clúster de conmutación por error de SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).

Además, debe tener un conocimiento general de hello siguientes tecnologías:

- [Solución hiperconvergida con Espacios de almacenamiento directo en Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Grupos de recursos de Azure](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>¿Qué toohave

Antes de seguir las instrucciones de hello en este artículo, ya debe tener:

- Una suscripción de Microsoft Azure.
- Un dominio de Windows en máquinas virtuales de Azure.
- Una cuenta con los objetos de máquina virtual de Azure hello toocreate permiso.
- Una red virtual de Azure y una subred con suficiente espacio de direcciones IP para saludo de los componentes siguientes:
   - Ambas máquinas virtuales.
   - dirección IP de clúster de conmutación por error de Hola.
   - Una dirección IP para cada FCI.
- DNS configurado en la red de Azure, que señala a los controladores de dominio toohello Hola.

Una vez que cumpla los requisitos previos, puede pasar a la creación de un clúster de conmutación por error. Hola primer paso es máquinas virtuales de toocreate Hola.

## <a name="step-1-create-virtual-machines"></a>Paso 1: Crear máquinas virtuales

1. Inicie sesión en toohello [portal de Azure](http://portal.azure.com) con su suscripción.

1. [Cree un conjunto de disponibilidad de Azure](../tutorial-availability-sets.md).

   disponibilidad de Hello conjunto de máquinas virtuales de grupos entre dominios de error y dominios de actualización. conjunto de disponibilidad de Hola se asegura de que la aplicación no se ve afectada por puntos únicos de error, como el conmutador de red de Hola o fuente de alimentación de Hola de un conjunto de servidores.

   Si no ha creado el grupo de recursos de Hola para las máquinas virtuales, hágalo cuando se crea un conjunto de disponibilidad de Azure. Si usas el conjunto de disponibilidad de hello toocreate portal Azure hello, Hola lo siguiente:

   - Hola portal de Azure, haga clic en  **+**  tooopen hello Azure Marketplace. Busque **Conjunto de disponibilidad**.
   - Haga clic en **Conjunto de disponibilidad**.
   - Haga clic en **Crear**.
   - En hello **crear conjunto de disponibilidad** hoja, Hola conjunto siguiente de valores:
      - **Nombre**: un nombre para el conjunto de disponibilidad de Hola.
      - **Suscripción**: su suscripción a Azure.
      - **Grupo de recursos**: si desea que toouse un grupo existente, haga clic en **utilizar existente** y grupo de hello seleccione de la lista desplegable de Hola. En caso contrario, elija **crear nuevo** y escriba un nombre para el grupo de Hola.
      - **Ubicación**: Establecer ubicación de Hola donde piensa toocreate las máquinas virtuales.
      - **Dominios de error**: usar Hola predeterminado (3).
      - **Actualizar dominios**: usar Hola predeterminado (5).
   - Haga clic en **crear** conjunto de disponibilidad de toocreate Hola.

1. Crear máquinas virtuales de hello en el conjunto de disponibilidad de Hola.

   Aprovisionar dos máquinas virtuales de SQL Server en el conjunto de disponibilidad de Azure Hola. Para obtener instrucciones, consulte [aprovisionar una máquina virtual de SQL Server en el portal de Azure hello](virtual-machines-windows-portal-sql-server-provision.md).

   Coloque ambas máquinas virtuales:

   - Hola mismo grupo de recursos de Azure que establezca su disponibilidad está en.
   - En la misma red que el controlador de dominio de hello.
   - En una subred con suficiente espacio de direcciones IP para ambas máquinas virtuales y todas las FCI que finalmente puede utilizar en este clúster.
   - En el conjunto de disponibilidad de Azure Hola.   

      >[!IMPORTANT]
      >Una vez creada una máquina virtual el conjunto de disponibilidad no se puede establecer o cambiar.

   Elija una imagen de hello Azure Marketplace. Puede usar un mercado imagen con la que incluye Windows Server y SQL Server o simplemente hello Windows Server. Para más información, consulte [Información general de SQL Server en máquinas virtuales de Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)

   imágenes de SQL Server oficiales de Hola Hola Galería de Azure incluyen una instancia instalada de SQL Server, además de software de instalación de SQL Server de Hola y clave necesaria Hola.

   Elija la imagen de la derecha Hola según toohow que desea toopay de licencia de SQL Server de hello:

   - **Pago por uso de licencias**: Hola por minuto de estas imágenes comprenda Hola licencias de SQL Server:
      - **SQL Server 2016 Enterprise en Windows Server Datacenter 2016**
      - **SQL Server 2016 Standard en Windows Server Datacenter 2016**
      - **SQL Server 2016 Developer en Windows Server Datacenter 2016**

   - **Traiga su propia licencia (BYOL)**

      - **{BYOL} SQL Server 2016 Enterprise en Windows Server Datacenter 2016**
      - **{BYOL} SQL Server 2016 Standard en Windows Server Datacenter 2016**

   >[!IMPORTANT]
   >Después de crear la máquina virtual de hello, quitar instancia de SQL Server de hello previamente instalar de forma independiente. Después de configurar el clúster de conmutación por error de Hola y S2D utilizará Hola previamente instalado SQL Server media toocreate Hola FCI de SQL Server.

   Como alternativa, puede utilizar imágenes de Azure Marketplace con solo el sistema de operativo Hola. Elija un **Windows Server 2016 Datacenter** imagen e instalar Hola FCI de SQL Server después de configurar el clúster de conmutación por error de Hola y S2D. Esta imagen no contiene los medios de instalación de SQL Server. Coloque los medios de instalación de hello en una ubicación donde puede ejecutar la instalación de SQL Server de Hola para cada servidor.

1. Después de que Azure cree las máquinas virtuales, conectar máquinas virtuales de tooeach con RDP.

   Cuando se conecta primero tooa virtual machine con RDP, equipo de Hola le preguntará si desea tooallow esta toobe PC pueda detectarse en red Hola. Haga clic en **Sí**.

1. Si utilizas una de las imágenes de máquina virtual basada en SQL Server de hello, quitar instancia de SQL Server de Hola.

   - En **Programas y características**, haga clic con el botón derecho en **Microsoft SQL Server 2016 (64 bits)** y haga clic en **Desinstalar o cambiar**.
   - Haga clic en **Quitar**.
   - Seleccione la instancia predeterminada de Hola.
   - Quite todas las características en **Servicios de motor de base de datos**. No quite **Características compartidas**. Vea Hola después de imagen:

      ![Quitar características](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Haga clic en **Siguiente** y, después, en **Quitar**.

1. <a name="ports"></a>Abrir puertos del firewall Hola.

   En cada máquina virtual, abra Hola después de puertos en Firewall de Windows hello.

   | Propósito | Puerto TCP | Notas
   | ------ | ------ | ------
   | SQL Server | 1433 | Puerto normal para las instancias predeterminadas de SQL Server. Si utiliza una imagen de galería de hello, este puerto se abre automáticamente.
   | Sondeo de mantenimiento | 59999 | Cualquier puerto TCP abierto. En un paso posterior, configure el equilibrador de carga de hello [sondeo de estado](#probe) y Hola toouse de clúster en este puerto.  

1. Agregar máquina virtual de almacenamiento toohello. Para más información, consulte [Almacenamiento premium: almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../../storage/common/storage-premium-storage.md).

   Ambas máquinas virtuales necesitan al menos dos discos de datos.

   Conecte discos sin procesar (discos cuyo formato no es NTFS).
      >[!NOTE]
      >Si conecta discos con formato NTFS, solo puede habilitar S2D sin comprobación de la idoneidad del disco.  

   Adjuntar un mínimo de dos tooeach de almacenamiento Premium (discos SSD) máquina virtual. Se recomienda usar, como mínimo, discos P30 (1 TB).

   Host de conjunto de almacenamiento en caché demasiado**de sólo lectura**.

   capacidad de almacenamiento de Hello que usar en entornos de producción depende de la carga de trabajo. los valores de Hello descritos en este artículo son para la demostración y pruebas.

1. [Agregar dominio preexistente de hello máquinas virtuales tooyour](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

Después de hello las máquinas virtuales se crean y configuran, puede configurar el clúster de conmutación por error de Hola.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>Paso 2: Configurar el clúster de conmutación por error de Windows hello con S2D

Hola siguiente paso es clúster de conmutación por error de hello tooconfigure con S2D. En este paso, realizará Hola siguientes pasos:

1. Agregue la característica Agrupación en clústeres de conmutación por error de Windows
1. Validar clúster Hola
1. Crear el clúster de conmutación por error de Hola
1. Crear el testigo de hello en la nube
1. Agregue almacenamiento

### <a name="add-windows-failover-clustering-feature"></a>Agregue la característica Agrupación en clústeres de conmutación por error de Windows

1. toobegin, conectar la máquina virtual de la primera toohello con RDP con una cuenta de dominio que es miembro de los administradores locales y tiene objetos de toocreate de permisos en Active Directory. Utilice esta cuenta para el resto de Hola de configuración de Hola.

1. [Agregar máquina virtual tooeach característica de agrupación en clústeres de conmutación por error](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   Hola tooinstall característica de agrupación en clústeres de conmutación por error de hello interfaz de usuario, siga los pasos en ambas máquinas virtuales.
   - En **Administrador del servidor**, haga clic en **Administrar** y, después, en **Agregar roles y características**.
   - En **agregar Roles y características Asistente**, haga clic en **siguiente** hasta llegar demasiado**seleccionar características**.
   - En **Seleccionar características**, haga clic en **Clústeres de conmutación por error**. Incluye todas las características necesarias y herramientas de administración de Hola. Haga clic en **Agregar características**.
   - Haga clic en **siguiente** y, a continuación, haga clic en **finalizar** características de hello tooinstall.

   tooinstall Hola agrupación en clústeres de conmutación por error característica con PowerShell, ejecute hello siguiente secuencia de comandos desde una sesión de PowerShell de administrador en una de las máquinas virtuales de Hola.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Como referencia, los pasos siguientes de Hola siguen instrucciones de hello en el paso 3 de [solución convergente Hyper mediante espacios de almacenamiento directo en Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Validar clúster Hola

Esta guía hace referencia tooinstructions en [validar clúster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Validación de clúster de Hola Hola interfaz de usuario o con PowerShell.

clúster de hello toovalidate con interfaz de usuario, hello Hola siguiendo los pasos de una de las máquinas virtuales de Hola.

1. En **Administrador del servidor**, haga clic en **Herramientas** y, después, en **Administrador de clústeres de conmutación por error**.
1. En **Administrador de clústeres de conmutación por error**, haga clic en **Acción** y, después, en **Validar configuración...**.
1. Haga clic en **Siguiente**.
1. En **seleccionar servidores o un clúster de**, nombre de tipo hello de las máquinas virtuales.
1. En **Opciones de pruebas**, elija **Ejecutar solo las pruebas que seleccione**. Haga clic en **Siguiente**.
1. En **Selección de pruebas**, incluya todas las pruebas, excepto **Almacenamiento**. Vea Hola después de imagen:

   ![Pruebas de validación](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. Haga clic en **Siguiente**.
1. En **Confirmación**, haga clic en **Siguiente**.

Hola **validar un asistente de configuración** Hola de ejecuciones de pruebas de validación.

clúster de hello toovalidate con PowerShell, ejecute hello siguiente secuencia de comandos desde una sesión de PowerShell de administrador en una de las máquinas virtuales de Hola.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Después de validar clúster hello, crear el clúster de conmutación por error de Hola.

### <a name="create-hello-failover-cluster"></a>Crear el clúster de conmutación por error de Hola

Esta guía hace referencia demasiado[crear clúster de conmutación por error de hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

clúster de conmutación por error de hello toocreate, necesita:
- nombres de Hola de máquinas virtuales de Hola que pasan a ser nodos de clúster de Hola.
- Un nombre para el clúster de conmutación por error de Hola
- Una dirección IP de clúster de conmutación por error de Hola. Puede usar una dirección IP que no se utiliza en hello misma red virtual y subred como Hola nodos del clúster.

Hola después de PowerShell crea un clúster de conmutación por error. Actualizar script de Hola con nombres de Hola de nodos de hello (nombres de máquina virtual de hello) y una dirección IP disponible de hello red virtual de Azure:

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Creación de un testigo en la nube

Testigo en la nube es un nuevo tipo de testigo de quórum de clúster almacenado en una instancia de Azure Storage Blob. Esto elimina la necesidad de Hola de una máquina virtual independiente hospeda un testigo de recurso compartido.

1. [Crear un testigo en la nube para clúster de conmutación por error de hello](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Cree un contenedor de blobs.

1. Guardar las claves de acceso de Hola y Hola dirección URL del contenedor.

1. Configurar a testigo de quórum de clúster de clúster de conmutación por error de Hola. Ver, [configurar testigo de quórum de hello en la interfaz de usuario de hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) en la interfaz de usuario de Hola.

### <a name="add-storage"></a>Agregue almacenamiento

es necesario que los discos de Hola para S2D toobe vacía y sin particiones u otros datos. siguen discos tooclean [Hola los pasos de esta guía](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Habilite Espacios de almacenamiento directo \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   Hola después PowerShell permite espacios de almacenamiento directos.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   En **Administrador de clústeres de conmutación por error**, ahora puede ver el grupo de almacenamiento de Hola.

1. [Cree un volumen](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Una de las características de Hola de S2D es que crea automáticamente un grupo de almacenamiento cuando se habilita. Ya estás listo toocreate un volumen. Hola PowerShell commandlet `New-Volume` automatiza el proceso de creación de volumen de hello, como el formato, Agregar clúster toohello y creación de un volumen compartido de clúster (CSV). Hola de ejemplo siguiente crea un 800 gigabyte (GB) CSV.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   Una vez que se completa este comando, se monta un volumen de 800 GB como recurso del clúster. volumen de Hello es en `C:\ClusterStorage\Volume1\`.

   Hola siguiente diagrama muestra un volumen compartido de clúster con S2D:

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>Paso 3: Probar la conmutación por error del clúster de conmutación por error

En el Administrador de clústeres de conmutación por error, compruebe que puede mover toohello de recursos de almacenamiento de hello otro nodo del clúster. Si se puede conectar clúster de conmutación por error de toohello con **Administrador de clústeres de conmutación por error** y mover el almacenamiento de Hola desde un nodo toohello otros, está listo tooconfigure Hola FCI.

## <a name="step-4-create-sql-server-fci"></a>Paso 4: Crear la FCI de SQL Server

Después de haber configurado el clúster de conmutación por error de Hola y todos los componentes de clúster, incluido el almacenamiento, puede crear Hola FCI de SQL Server.

1. Conecte la máquina virtual de la primera toohello con RDP.

1. En **Administrador de clústeres de conmutación por error**, asegúrese de que todos los recursos principales de clúster estén en la máquina virtual de primera Hola. Si es necesario, mueva la máquina virtual de todos los recursos toothis.

1. Busque los medios de instalación de Hola. Si máquina virtual de hello utiliza una de las imágenes de Azure Marketplace de hello, se encuentra en medio de hello `C:\SQLServer_<version number>_Full`. Haga clic en **Configuración**.

1. Hola **centro de instalación de SQL Server**, haga clic en **instalación**.

1. Haga clic en **Nueva instalación de clúster de conmutación por error de SQL Server**. Siga las instrucciones de Hola Hola Hola de tooinstall Asistente FCI de SQL Server.

   directorios de datos de Hello FCI necesitan toobe en almacenamiento en clúster. Con S2D, no es un disco compartido, pero un volumen de tooa de punto de montaje en cada servidor. S2D sincroniza volumen Hola entre ambos nodos. volumen de Hola se presenta toohello clúster como un volumen compartido de clúster. Utilizar el punto de montaje CSV de hello en los directorios de datos de Hola.

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Después de completar al Asistente de hello, el programa de instalación instalará una FCI de SQL Server en el primer nodo de Hola.

1. Después de que el programa de instalación instala correctamente Hola FCI en el primer nodo de hello, conecte toohello segundo nodo con RDP.

1. Abra hello **centro de instalación de SQL Server**. Haga clic en **Instalación**.

1. Haga clic en **clúster de conmutación por error de SQL Server de agregar nodos tooa**. Siga las instrucciones de hello en SQL server de hello Asistente tooinstall y agregue este toohello servidor FCI.

   >[!NOTE]
   >Si usa una imagen de la Galería de Azure Marketplace con SQL Server, herramientas de SQL Server se incluían en la imagen de Hola. Si no usó esta imagen, instalar herramientas de SQL Server de Hola por separado. Consulte [Descarga de SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>Paso 5: Crear un equilibrador de carga de Azure

En máquinas virtuales de Azure, los clústeres usen un toohold de equilibrador de carga de una dirección IP que necesita toobe en un nodo de clúster en un momento. En esta solución, el equilibrador de carga de hello contiene dirección IP Hola Hola FCI de SQL Server.

[Creación y configuración de un equilibrador de carga de Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Crear el equilibrador de carga de Hola Hola portal de Azure

equilibrador de carga de Hola toocreate:

1. Hola portal de Azure, vaya toohello grupo de recursos con máquinas virtuales de Hola.

1. Haga clic en **+ Agregar**. Hola de búsqueda Marketplace para **equilibrador de carga**. Haga clic en **Equilibrador de carga**.

1. Haga clic en **Crear**.

1. Configure el equilibrador de carga de hello con:

   - **Nombre**: un nombre que identifique el equilibrador de carga de Hola.
   - **Tipo de**: equilibrador de carga de hello puede ser público o privado. Puede tener acceso a un equilibrador de carga privada desde Hola misma red virtual. La mayoría de las aplicaciones de Azure pueden usar un equilibrador de carga privado. Si la aplicación necesita acceso tooSQL Server directamente a través de Internet de hello, use un equilibrador de carga pública.
   - **Red virtual**: Hola misma red que las máquinas virtuales Hola.
   - **Subred**: Hola la misma subred que hello las máquinas virtuales.
   - **La dirección IP privada**: Hola la misma dirección IP que ha asignado el recurso de red de clústeres de toohello FCI de SQL Server.
   - **Suscripción**: su suscripción a Azure.
   - **Grupo de recursos**: Use Hola mismo grupo de recursos que las máquinas virtuales.
   - **Ubicación**: Use Hola misma ubicación de Azure como las máquinas virtuales.
   Vea Hola después de imagen:

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Configurar grupo de back-end de equilibradores de carga de Hola

1. Devolver toohello grupo de recursos de Azure con máquinas virtuales de Hola y busque el equilibrador de carga nueva Hola. Es posible que tenga la vista de hello toorefresh en hello grupo de recursos. Haga clic en el equilibrador de carga de Hola.

1. En la hoja de equilibrador de carga de hello, haga clic en **grupos back-end**.

1. Haga clic en **+ agregar** tooadd un grupo back-end.

1. Escriba un nombre para el grupo de back-end de Hola.

1. Haga clic en **Agregar una máquina virtual**.

1. En hello **elegir máquinas virtuales** hoja, haga clic en **elegir un conjunto de disponibilidad**.

1. Elija que coloquen máquinas de virtuales de SQL Server de hello en el conjunto de disponibilidad de Hola.

1. En hello **elegir máquinas virtuales** hoja, haga clic en **elegir máquinas virtuales de hello**.

   El portal de Azure debe ser similar Hola después de imagen:

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Haga clic en **seleccione** en hello **elegir máquinas virtuales** hoja.

1. Haga clic en **Aceptar** dos veces.

### <a name="configure-a-load-balancer-health-probe"></a>Configuración de un sondeo de mantenimiento de un equilibrador de carga

1. En la hoja de equilibrador de carga de hello, haga clic en **sondeos de estado**.

1. Haga clic en **+ Agregar**.

1. En hello **sondeo de estado del complemento** hoja, <a name="probe"> </a>establecer parámetros de sondeo de estado de hello:

   - **Nombre**: un nombre para el sondeo de estado de Hola.
   - **Protocolo**: TCP.
   - **Puerto**: establecer tooan puertos TCP disponibles. Dicho puerto requiere un puerto de firewall abierto. Hola de uso [mismo puerto](#ports) se establece para el sondeo de estado de hello en firewall de Hola.
   - **Intervalo**: 5 segundos.
   - **Umbral incorrecto**: dos errores consecutivos.

1. Haga clic en Aceptar.

### <a name="set-load-balancing-rules"></a>Establecimiento de reglas de equilibrio de carga

1. En la hoja de equilibrador de carga de hello, haga clic en **reglas de equilibrio de carga**.

1. Haga clic en **+ Agregar**.

1. Establecer parámetros de reglas de equilibrio de carga de hello:

   - **Nombre**: un nombre para las reglas de equilibrio de carga de Hola.
   - **Dirección IP de Frontend**: Use una dirección IP Hola para hello recurso de red de clústeres de SQL Server FCI.
   - **Puerto**: establecer para el puerto TCP de SQL Server FCI Hola. puerto de instancia de Hello predeterminado es 1433.
   - **Puerto de back-end**: este valor usa Hola mismo número de puerto como hello **puerto** valor cuando se habilita el **IP flotante (direct server devuelto)**.
   - **Grupo back-end**: nombre de grupo de back-end de Hola de uso que configuró anteriormente.
   - **Sondeo de estado**: sondeo de estado de Hola de uso que configuró anteriormente.
   - **Persistencia de la sesión**: no.
   - **Tiempo de espera de inactividad (minutos)**: 4.
   - **IP flotante (Direct Server Return)**: habilitado

1. Haga clic en **Aceptar**.

## <a name="step-6-configure-cluster-for-probe"></a>Paso 6: Configurar el clúster para el sondeo

Establecer el parámetro de puerto de sondeo de clúster de hello en PowerShell.

tooset Hola parámetro de puerto de sondeo de clúster, actualice las variables Hola siguiente secuencia de comandos de su entorno.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>Paso 7: Probar la conmutación por error de la FCI

Probar la conmutación por error de hello funcionalidad de clústeres de toovalidate FCI. Hola lo siguiente:

1. Conecte tooone de nodos de clúster de SQL Server FCI Hola con RDP.

1. Abra el **Administrador de clústeres de conmutación por error**. Haga clic en **Roles**. Observe qué nodo posee el rol de SQL Server FCI de Hola.

1. Haga clic en el rol de hello FCI de SQL Server.

1. Haga clic en **Mover** y, después, en **Mejor nodo posible**.

**El Administrador de clústeres de conmutación por error** muestra Hola rol y sus recursos se ponen sin conexión. Hello recursos, a continuación, mover y ponerse en línea hello en otro nodo.

### <a name="test-connectivity"></a>Comprobación de la conectividad

conectividad tootest de registro en la máquina virtual de tooanother Hola misma red virtual. Abra **SQL Server Management Studio** y nombre de SQL Server FCI toohello connect.

>[!NOTE]
>Si es necesario, puede [descargar SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Limitaciones
En máquinas virtuales de Azure, Coordinador de transacciones distribuidas de Microsoft (DTC) no se admite en fci porque Hola puerto RPC no es compatible con el equilibrador de carga de Hola.

## <a name="see-also"></a>Otras referencias

[Instalación de S2D con escritorio remoto (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[Solución hiperconvergida con Espacios de almacenamiento directo en Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Espacios de almacenamiento directo en Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[Compatibilidad de SQL Server con S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
