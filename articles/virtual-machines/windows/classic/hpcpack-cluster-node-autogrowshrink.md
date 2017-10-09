---
title: "nodos de clúster de HPC Pack aaaAutoscale | Documentos de Microsoft"
description: "Automáticamente aumentar y reducir el número de Hola de nodos de proceso de clúster de HPC Pack en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Automáticamente aumentar y reducir los recursos de clúster de HPC Pack hello en Azure según la carga de trabajo de clúster toohello
Si implementar nodos de Azure "irrumpir" en el clúster de HPC Pack, o crear un clúster de HPC Pack en máquinas virtuales de Azure, puede que desee una manera de aumentar o reducir los recursos de clúster de hello como nodos o núcleos según la carga de trabajo de hello en clúster de hello automáticamente. Ajuste de escala en recursos de clúster de Hola de esta manera permite toouse los recursos de Azure más eficazmente y controlar los costes.

Este artículo muestra dos maneras de HPC Pack proporciona recursos de proceso de tooautoscale:

* propiedad de clúster de HPC Pack Hello **AutoGrowShrink**

* Hola **AzureAutoGrowShrink.ps1** script de PowerShell de HPC

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Actualmente solo se pueden aumentar y reducir automáticamente los nodos de proceso de HPC Pack que ejecutan un sistema operativo Windows Server.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Establecer la propiedad de clúster de hello AutoGrowShrink
### <a name="prerequisites"></a>Requisitos previos

* **HPC Pack 2012 R2 Update 2 o posterior clúster** -nodo principal del clúster Hola puede ser implementado de forma local o en una máquina virtual de Azure. Vea [configurar un clúster híbrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget a trabajar con un nodo principal en local y nodos de ráfaga de Azure"". Vea hello [script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly implementar un clúster de HPC Pack en máquinas virtuales de Azure.

* **Para un clúster con un nodo principal en Azure (modelo de implementación de Resource Manager)**: a partir de HPC Pack 2016, la autenticación de certificado en una aplicación de Azure Active Directory se usa para aumentar y reducir automáticamente las máquinas virtuales del clúster implementadas mediante Azure Resource Manager. Configure un certificado de la manera siguiente:

  1. Después de la implementación de clúster, conéctese al nodo principal de tooone de escritorio remoto.

  2. Cargue el nodo principal de hello certificado (formato PFX con clave privada) tooeach e instale tooCert:\LocalMachine\My y Cert: \LocalMachine\Root.

  3. Iniciar Azure PowerShell como administrador y ejecute hello siguientes comandos en un nodo principal:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Si su cuenta está en más de un inquilino de Azure Active Directory o suscripción de Azure, puede ejecutar Hola siguiente comando inquilino correcto de tooselect Hola y de suscripción:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Ejecute hello después tooview comando hello seleccionada actualmente inquilino y la suscripción:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Ejecute la siguiente secuencia de comandos de Hola

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    donde

    **DisplayName**: nombre para mostrar de la aplicación Azure Active Directory. Si la aplicación hello no existe, se crea en Azure Active Directory.

    **Página principal de** -página principal de Hola de aplicación hello. Puede configurar una dirección URL ficticia, como en el anterior ejemplo de Hola.

    **IdentifierUri** -identificador de la aplicación hello. Puede configurar una dirección URL ficticia, como en el anterior ejemplo de Hola.

    **CertificateThumbprint** -huella digital del certificado de hello instalado en el nodo principal de hello en el paso 1.

    **TenantId**: id. del inquilino de Azure Active Directory. Puede obtener Id. de inquilino de Hola desde el portal de Azure Active Directory hello **propiedades** página.

    Para más información sobre **ConfigARMAutoGrowShrinkCert.ps1**, ejecute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **Para un clúster con un nodo principal en Azure (modelo de implementación clásica)** : Si utiliza Hola IaaS de HPC Pack implementación script toocreate Hola clúster en el modelo de implementación clásica de hello, habilitar hello **AutoGrowShrink** clúster propiedad estableciendo la opción de AutoGrowShrink de hello en el archivo de configuración del clúster de Hola. Para obtener más información, consulte documentación de Hola que acompaña hello [descarga del script](https://www.microsoft.com/download/details.aspx?id=44949).

    También puede habilitar hello **AutoGrowShrink** propiedad del clúster después de implementar el clúster de hello mediante PowerShell de HPC comandos descrito en hello pasos de la sección. tooprepare para esto, primera Hola completa siguiendo los pasos:

  1. Configurar un certificado de administración de Azure en el nodo principal de Hola y Hola suscripción de Azure. Para una implementación de prueba, puede usar Hola predeterminado Microsoft HPC Azure certificado autofirmado que HPC Pack se instala en el nodo principal de hello y, a continuación, cargar ese tooyour certificado suscripción de Azure. Para las opciones y los pasos, vea hello [Guía de la biblioteca de TechNet](https://technet.microsoft.com/library/gg481759.aspx).

  2. Ejecutar **regedit** en el nodo principal de hello, vaya tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo y agregue un valor de cadena. Establece el nombre del valor de hello demasiado "Huella digital" y datos de valor toohello huella digital del certificado de hello en el paso 1.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>Propiedad de tooset hello AutoGrowShrink de comandos de PowerShell de HPC
Estos son tooset de comandos de PowerShell de HPC de ejemplo **AutoGrowShrink** y tootune su comportamiento con parámetros adicionales. Vea [AutoGrowShrink parámetros](#AutoGrowShrink-parameters) más adelante en este artículo para la lista completa de Hola de configuración.

toorun estos comandos, inicie HPC PowerShell en el nodo principal del clúster de hello como administrador.

**Hola tooenable AutoGrowShrink propiedad**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**Hola toodisable AutoGrowShrink propiedad**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**Hola toochange aumentan el intervalo en minutos**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**Hola toochange reducir el intervalo en minutos**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**configuración actual de hello tooview de AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**grupos de nodos de tooexclude de AutoGrowShrink**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Este parámetro se admite a partir de HPC Pack 2016.
>

### <a name="autogrowshrink-parameters"></a>Parámetros de AutoGrowShrink
Hello siguientes son AutoGrowShrink parámetros que se pueden modificar mediante el uso de hello **HpcClusterProperty conjunto** comando.

* **EnableGrowShrink** : cambiar tooenable o deshabilitar hello **AutoGrowShrink** propiedad.
* **ParamSweepTasksPerCore** -número de barrido paramétrico tareas toogrow un núcleo. valor predeterminado de Hello es toogrow un núcleo por tarea.

  > [!NOTE]
  > Cambios de HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** demasiado**TasksPerResourceUnit**. Se basa en el tipo de recurso de trabajo de Hola y puede ser el nodo, un socket o core.
  >
  >
* **GrowThreshold** -umbral de crecimiento automático de tootrigger de tareas en cola. valor predeterminado de Hello es 1, lo que significa que si hay 1 o más tareas en Hola estado en cola, expandir automáticamente los nodos.
* **GrowInterval** -intervalo de crecimiento automático de tootrigger de minutos. intervalo de saludo predeterminado es 5 minutos.
* **ShrinkInterval** -intervalo en minutos tootrigger reducirse de forma automática. intervalo de saludo predeterminado es 5 minutos. |
* **ShrinkIdleTimes** -número de comprobaciones continua tooshrink tooindicate Hola nodos está inactivo. valor predeterminado de Hello es 3 veces. Por ejemplo, si hello **ShrinkInterval** es 5 minutos, HPC Pack comprueba si el nodo de hello está inactivo cada 5 minutos. Si hay nodos de hello en estado de inactividad de Hola tras 3 continua comprobaciones (15 minutos), HPC Pack se reduce a ese nodo.
* **ExtraNodesGrowRatio** -porcentaje adicional de toogrow de nodos para los trabajos de la interfaz de paso de mensajes (MPI). valor predeterminado de Hello es 1, lo que significa que HPC Pack crece nodos 1% para los trabajos MPI.
* **GrowByMin** -cambiar tooindicate si están basada en directivas de crecimiento automático de hello en recursos de hello mínimos requeridos para el trabajo de Hola. Hola es false, lo que significa que HPC Pack crece nodos para los trabajos según los recursos de hello máximo requeridos para trabajos de Hola.
* **SoaJobGrowThreshold** -umbral de entrante Hola de tootrigger SOA solicitudes automática crecer proceso. valor predeterminado de Hello es 50000.

  > [!NOTE]
  > Este parámetro se admite a partir de HPC Pack 2012 R2 Update 3.
  >
  >
* **SoaRequestsPerCore** -número de SOA entrante solicitudes toogrow un núcleo. valor predeterminado de Hello es 20000.

  > [!NOTE]
  > Este parámetro se admite a partir de HPC Pack 2012 R2 Update 3.
  >
* **ExcludeNodeGroups** : los nodos en hello especificar grupos de nodos aumentar y reducir de forma automática.
  
  > [!NOTE]
  > Este parámetro se admite a partir de HPC Pack 2016.
  >

### <a name="mpi-example"></a>Ejemplo de MPI
De forma predeterminada HPC Pack crece 1% nodos adicionales para los trabajos MPI (**ExtraNodesGrowRatio** se establece too1). motivo de Hello es que MPI puede requerir varios nodos, y solo se puede ejecutar el trabajo de hello cuando todos los nodos están listos. En ocasiones cuando Azure inicia nodos, un nodo que tenga más toostart de tiempo que otras, haciendo que otros toobe nodos inactivo mientras se espera que tooget nodo preparado. Al aumentar los nodos adicionales, HPC Pack reduce este tiempo de espera de recursos y podría ahorrar costos. porcentaje de hello tooincrease de nodos adicionales para los trabajos MPI (por ejemplo, too10%), ejecute un comando similar a

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>Ejemplo de SOA
De forma predeterminada, **SoaJobGrowThreshold** se establece too50000 y **SoaRequestsPerCore** se establece too200000. Si envía un trabajo SOA con 70 000 solicitudes, hay una tarea en cola y las solicitudes entrantes son 70 000. En este caso HPC Pack crece 1 núcleo de hello en cola tareas y para las solicitudes entrantes, crece (70000 50000) / principales 20000 = 1, por lo que en total crece 2 núcleos para este trabajo SOA.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Ejecutar script de Hola AzureAutoGrowShrink.ps1
### <a name="prerequisites"></a>Requisitos previos

* **HPC Pack 2012 R2 Update 1 o posterior clúster** : hello **AzureAutoGrowShrink.ps1** está instalado en la carpeta Hola % CCP_HOME % bin. nodo principal del clúster Hola puede ser implementado de forma local o en una máquina virtual de Azure. Vea [configurar un clúster híbrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget a trabajar con un nodo principal en local y nodos de ráfaga de Azure"". Vea hello [script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly implementar un clúster de HPC Pack en máquinas virtuales de Azure o use un [plantilla de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **Azure PowerShell 1.4.0** -script de Hola actualmente depende de esta versión específica de Azure PowerShell.
* **Para un clúster con Azure en ráfagas nodos** -ejecutar script de Hola en un equipo cliente donde se instaló el paquete de HPC, o en el nodo principal de Hola. Si se ejecuta en un equipo cliente, asegúrese de establecer hello $env variable: nodo principal de CCP_SCHEDULER toopoint toohello. se deben agregar nodos de Azure «"ráfaga" Hello toohello clúster, pero pueden encontrarse en hello estado no implementado.
* **Para un clúster implementado en máquinas virtuales de Azure (modelo de implementación de administrador de recursos)** -para un clúster de máquinas virtuales de Azure implementadas en el modelo de implementación del Administrador de recursos de hello, el script de Hola admite dos métodos para la autenticación de Azure: inicie sesión en tooyour cuenta de Azure script de Hola toorun cada vez (mediante la ejecución de `Login-AzureRmAccount`, o configurar un tooauthenticate principal de servicio con un certificado. HPC Pack proporciona el script de Hola **ConfigARMAutoGrowShrinkCert.ps** toocreate una entidad de servicio con el certificado. script de Hola crea una aplicación de Azure Active Directory (Azure AD) y una entidad de servicio y asigna la entidad de servicio de toohello de rol de colaborador de Hola. script de Hola toorun, iniciar Azure PowerShell como administrador y ejecute hello siguientes comandos:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Para más información sobre **ConfigARMAutoGrowShrinkCert.ps1**, ejecute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.

* **Para un clúster implementado en máquinas virtuales de Azure (modelo de implementación clásica)** -ejecutar script de Hola en máquina virtual del nodo principal Hola porque depende de hello **Start-HpcIaaSNode.ps1** y **Stop-HpcIaaSNode.ps1**secuencias de comandos que están instalados allí. Esas scripts requieren además un certificado de administración de Azure o un archivo de configuración de publicación (consulte [Administrar nodos de ejecución en un clúster de HPC Pack en Azure](hpcpack-cluster-node-manage.md)). Asegúrese de que Hola todas las máquinas virtuales que se necesita del nodo ya se han agregado toohello clúster de proceso. Pueden encontrarse en estado detenido Hola.



### <a name="syntax"></a>Sintaxis
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>parameters
* **NodeTemplates** -nombres de toodefine de plantillas de nodo de Hola Hola ámbito para toogrow de nodos de Hola y reducir. Si no se especifica (valor predeterminado de hello es @()), todos los nodos de hello **AzureNodes** grupo de nodos están dentro del ámbito cuando **NodeType** tiene un valor de AzureNodes y todos los nodos en hello **ComputeNodes** grupo de nodos están dentro del ámbito cuando **NodeType** tiene un valor de ComputeNodes.
* **JobTemplates** -nombres de hello ámbito plantillas toodefine Hola Hola nodos toogrow del trabajo.
* **NodeType** : tipo de nodo toogrow de Hola y reducir. Los valores admitidos son:

  * **AzureNodes** : para los nodos (ráfaga) de Azure PaaS en un clúster de Azure IaaS o local.
  * **ComputeNodes** : para máquinas virtuales de nodos de ejecución solo en un clúster de Azure IaaS.

* **NumOfQueuedJobsPerNodeToGrow** -número de trabajos en cola requiere toogrow un nodo.
* **NumOfQueuedJobsToGrowThreshold** -número de umbral de Hola de hello toostart de trabajos en cola crezca proceso.
* **NumOfActiveQueuedTasksPerNodeToGrow** -número de Hola de tareas en cola activas necesarias toogrow un nodo. Si se especifica **NumOfQueuedJobsPerNodeToGrow** con un valor superior a 0, se omite este parámetro.
* **NumOfActiveQueuedTasksToGrowThreshold** -número de umbral de Hola de Hola de tareas en cola activas toostart aumenta de proceso.
* **NumOfInitialNodesToGrow** : hello inicial número mínimo de nodos toogrow si todos los nodos de hello en el ámbito son **no implementado** o **detenido (desasignado)**.
* **GrowCheckIntervalMins** -intervalo de saludo en minutos entre comprobaciones toogrow.
* **ShrinkCheckIntervalMins** -intervalo de saludo en minutos entre comprobaciones tooshrink.
* **ShrinkCheckIdleTimes** -Hola número de comprobaciones de reducción continuas (separadas por **ShrinkCheckIntervalMins**) tooindicate Hola nodos están inactivos.
* **UseLastConfigurations** -Hola configuraciones anteriores guardadas en un archivo de argumento Hola.
* **ArgFile**: Hola nombre de toosave de archivo que se utiliza de argumento de Hola y Hola configuraciones toorun Hola script de actualización.
* **LogFilePrefix** -nombre del prefijo Hola Hola del archivo de registro. Puede especificar una ruta de acceso. De forma predeterminada el registro de hello está escrito toohello directorio de trabajo actual.

### <a name="example-1"></a>Ejemplo 1
Hello en el ejemplo siguiente se configura hello Azure irrumpir nodos implementados con la plantilla AzureNode predeterminada toogrow y reducir automáticamente. Si todos los nodos están inicialmente en hello **no implementado** estado, se inician al menos 3 nodos. Si el número de Hola de trabajos en cola supera los 8, el script de Hola inicia nodos hasta que su número supera la relación de Hola de trabajos en cola para **NumOfQueuedJobsPerNodeToGrow**. Si un nodo no se encuentra inactivo en 3 tiempos de inactividad consecutivas toobe, se detiene.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Ejemplo 2
Hello en el ejemplo siguiente se configura hello Azure compute máquinas virtuales de nodos que se implementa con hello plantilla ComputeNode predeterminada toogrow y reducir automáticamente.
trabajos de Hello configurados por plantilla de trabajo predeterminada de hello definen ámbito de hello de la carga de trabajo en clúster de Hola. Si inicialmente se detienen todos los nodos de hello, se inician al menos 5 nodos. Si el número de Hola de tareas en cola activas supera las 15, el script de Hola inicia nodos hasta que su número supera relación de Hola de tareas en cola activas demasiado**NumOfActiveQueuedTasksPerNodeToGrow**. Si un nodo no se encuentra inactivo en 10 tiempos de inactividad consecutivas toobe, se detiene.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
