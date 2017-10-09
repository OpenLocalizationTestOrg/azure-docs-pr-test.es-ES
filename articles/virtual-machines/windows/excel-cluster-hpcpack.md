---
title: "aaaHPC módulo de clúster para Excel y SOA | Documentos de Microsoft"
description: "Introducción a la ejecución de cargas de trabajo de Excel y SOA a gran escala en un clúster de HPC Pack en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Introducción a la ejecución de cargas de trabajo de Excel y SOA en un clúster de HPC Pack en Azure
Este artículo muestra cómo toodeploy Microsoft HPC Pack 2012 R2 de clúster en máquinas virtuales de Azure mediante el uso de una plantilla de inicio rápido de Azure o, opcionalmente, un script de implementación de Azure PowerShell. clúster de Hello usa Azure Marketplace VM imágenes diseñadas toorun Microsoft Excel o cargas de trabajo de arquitectura orientada a servicios (SOA) con HPC Pack. Puede usar hello toorun de clúster HPC de Excel y servicios SOA desde un equipo de cliente local. Servicios de HPC de Excel de Hello incluyen la descarga del libro de Excel y funciones definidas por el usuario de Excel o UDF.

> [!IMPORTANT] 
> Este artículo se basa en características, plantillas y scripts de HPC Pack 2012 R2. Este escenario no se admite actualmente en HPC Pack 2016.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

En un nivel alto, hello siguiente diagrama muestra clúster de HPC Pack Hola que haya creado.

![Clúster HPC con nodos que ejecutan cargas de trabajo de Excel][scenario]

## <a name="prerequisites"></a>Requisitos previos
* **Equipo cliente** -necesita un cliente basado en Windows equipo toosubmit ejemplo Excel y SOA trabajos toohello clúster. También necesita un hello toorun de equipo de Windows Azure PowerShell script de implementación de clúster (si elige ese método de implementación).
* **Suscripción de Azure** : si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) en un par de minutos.
* **Cuota de núcleos** -podría necesita tooincrease Hola cuota de núcleos, especialmente si implementa varios nodos de clúster con tamaños de máquinas virtuales con varios núcleos. Si está utilizando una plantilla de inicio rápido de Azure, cuota de núcleos de hello en el Administrador de recursos es por región de Azure. En ese caso, tendrá que tooincrease cuota de hello en una región específica. Consulte [Límites, cuotas y restricciones de suscripción de Azure](../../azure-subscription-service-limits.md). tooincrease una cuota, [abrir una solicitud de soporte al cliente en línea](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sin cargo.
* **Licencia de Microsoft Office**: si implementa nodos de proceso con una imagen de máquina virtual de Marketplace HPC Pack 2012 R2 con Microsoft Excel, se instala una versión de evaluación de 30 días de Microsoft Excel Professional Plus 2013. Tras el período de evaluación de hello, necesita tooprovide un válido Microsoft Office licencia tooactivate Excel toocontinue toorun cargas de trabajo. Consulte [Activación de Excel](#excel-activation) que aparece más adelante en este artículo. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>Paso 1. Configuración e un clúster de HPC Pack en Azure
Se muestra dos tooset opciones de clúster de HPC Pack 2012 R2 hello: en primer lugar, mediante una plantilla de inicio rápido de Azure y Hola portal de Azure; y, después, mediante un script de implementación de PowerShell de Azure.

### <a name="option-1-use-a-quickstart-template"></a>Opción 1. Uso de una plantilla de inicio rápido
Use un tooquickly de plantilla de inicio rápido de Azure implementar un clúster de HPC Pack en hello portal de Azure. Cuando se abre la plantilla de hello en el portal de hello, obtendrá una interfaz de usuario simple donde escribir valores de hello para el clúster. Estos son los pasos de Hola. 

> [!TIP]
> Si lo desea, use una [plantilla de Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) que crea un clúster similar específicamente para cargas de trabajo de Excel. pasos de Hello difieren ligeramente de siguiente Hola.
> 
> 

1. Visite hello [página de la plantilla de creación de clústeres de HPC en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). Si lo desea, revise la información de plantilla de Hola y código fuente de Hola.
2. Haga clic en **implementar tooAzure** toostart una implementación con plantilla Hola Hola portal de Azure.
   
   ![Implementar la plantilla tooAzure][github]
3. En el portal de hello, siga estos parámetros de hello tooenter pasos para la plantilla de clúster HPC de Hola.
   
   a. En hello **parámetros** página, escriba o modifique los valores de parámetros de plantilla de Hola. (Haga clic en configuración tooeach Hola icono siguiente para obtener información de ayuda.) Se muestran valores de ejemplo Hola después de la pantalla. Este ejemplo crea un clúster denominado *hpc01* en hello *hpc.local* nodos de proceso de dominio que consta de un nodo principal y 2. nodos de proceso de Hola se crean a partir de una imagen de máquina virtual de HPC Pack que incluye Microsoft Excel.
   
   ![Escribir parámetros][parameters-new-portal]
   
   > [!NOTE]
   > nodo principal de Hello máquinas virtuales se crean automáticamente a partir de hello [última imagen de Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) de HPC Pack 2012 R2 en Windows Server 2012 R2. Actualmente la image de Hola se basa en HPC Pack 2012 R2 Update 3.
   > 
   > Máquinas virtuales de nodos de cálculo se crean a partir de la imagen más reciente de Hola de familia de nodo de proceso de hello seleccionado. Seleccione hello **ComputeNodeWithExcel** opción para hello más reciente HPC Pack proceso nodo imagen que incluye una versión de evaluación de Microsoft Excel Professional Plus 2013. toodeploy un clúster para las sesiones SOA generales o para la descarga de UDF de Excel, elija hello **ComputeNode** opción (sin Excel instalado).
   > 
   > 
   
   b. Elija la suscripción de Hola.
   
   c. Crear un grupo de recursos de clúster de hello, como *hpc01RG*.
   
   d. Elegir una ubicación para el grupo de recursos de hello, como Central US.
   
   e. En hello **condiciones legales** página, revise los términos de Hola. Si está de acuerdo, haga clic en **Comprar**. A continuación, haga clic en cuando haya terminado de establecer los valores de hello para la plantilla de hello, **crear**.
4. Cuando finalice la implementación de hello (normalmente tarda unos 30 minutos), exportar el archivo de certificado de clúster de Hola desde el nodo principal del clúster Hola. En un paso posterior, importa este certificado público en hello tooprovide Hola servidor autenticación del equipo cliente para el enlace HTTP seguro.
   
   a. Hola portal de Azure, vaya toohello panel, nodo principal de hello seleccione y haga clic en **conectar** en parte superior de Hola de hello página tooconnect mediante Escritorio remoto.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Utilice los procedimientos estándares de certificado de nodo principal de hello tooexport de administrador de certificados (que se encuentra bajo Cert: \LocalMachine\My) sin clave privada de Hola. En este ejemplo, exporte *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Exportar certificado Hola][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Opción 2. Usar script de implementación de IaaS de HPC Pack Hola
Hola script de implementación de IaaS de HPC Pack proporciona otro toodeploy versátil forma un clúster de HPC Pack. Crea un clúster en el modelo de implementación clásica de hello, mientras que la plantilla Hola utiliza el modelo de implementación de hello Azure Resource Manager. Además, el script de Hola es compatible con una suscripción en hello Global de Azure o el servicio de Azure China.

**Requisitos previos adicionales**

* **Azure PowerShell** - [instale y configure Azure PowerShell](/powershell/azure/overview) (versión 0.8.10 o posterior) en el equipo cliente.
* **Script de implementación de IaaS de HPC Pack** : Descargue y descomprima la versión más reciente de Hola de script de Hola de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Comprobar la versión de Hola de script de Hola ejecutando `New-HPCIaaSCluster.ps1 –Version`. En este artículo se basa en la versión 4.5.0 o posterior del script de Hola.

**Crear archivo de configuración de Hola**

 Hola script de implementación de IaaS de HPC Pack utiliza un archivo de configuración XML como entrada que describe la infraestructura de Hola Hola del clúster de HPC. toodeploy un clúster que consta de un nodo principal y 18 proceso nodos creados a partir de la imagen del nodo de proceso de Hola que incluye Microsoft Excel, sustituya los valores para el entorno en el siguiente archivo de configuración de ejemplo de Hola. Para obtener más información sobre el archivo de configuración de hello, consulte el archivo Manual.rtf de hello en la carpeta de script de Hola y [crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Notas sobre el archivo de configuración de Hola**

* Hola **VMName** del nodo principal de hello **debe** Hola igual como hello **ServiceName**, o toorun producirán errores en trabajos SOA.
* Asegúrese de especificar **EnableWebPortal** para que hello certificado del nodo principal se genera y se exportan.
* archivo Hello especifica un script de PowerShell de configuración posteriores a la PostConfig.ps1 que se ejecuta en el nodo principal de Hola. Hola siguiente secuencia de comandos de ejemplo configura la cadena de conexión de almacenamiento de Azure de hello, quita el rol de nodo de proceso de Hola de nodo principal de Hola y pone todos los nodos en línea cuando se implementan. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Ejecutar script de Hola**

1. Abra la consola de PowerShell de hello en el equipo de cliente hello como administrador.
2. Cambiar la carpeta de secuencia de comandos de toohello de directorio (E:\IaaSClusterScript en este ejemplo).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. clúster de HPC Pack en hello toodeploy, ejecute el siguiente comando de Hola. En este ejemplo se da por supuesto que se encuentra ese archivo de configuración de hello en E:\HPCDemoConfig.xml.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

Hola script de implementación de HPC Pack se ejecuta durante algún tiempo. Un script de Hola lo hace es tooexport y descargar certificado de clúster de Hola y guárdelo en la carpeta documentos del usuario actual de hello en el equipo cliente de Hola. script de Hola genera un siguiente toohello similar de mensaje. En un paso siguiente, importar certificado hello en el almacén de certificados adecuado de Hola.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>Paso 2: Descarga de libros de Excel y ejecución de UDF desde un cliente local
### <a name="excel-activation"></a>Activación de Excel
Cuando use Hola imagen ComputeNodeWithExcel VM para cargas de trabajo de producción, debe tooprovide un válido Microsoft Office licencia clave tooactivate Excel en los nodos de proceso de Hola. En caso contrario, versión de evaluación de Hola de Excel expira después de 30 días, y ejecutar libros de Excel se producirá un error con hello COMException (0x800AC472). 

Puede rearmar Excel durante otros 30 días del período de evaluación: inicie sesión en el nodo principal de toohello y clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` en Excel todos los nodos mediante el Administrador de clústeres de HPC de ejecución. Puede rearmar un máximo de dos veces. Después de eso, debe proporcionar una clave de licencia de Office válida.

Hola Office Professional Plus 2013 instalado en la imagen de máquina virtual de hello es una edición de volumen con una clave de licencia de volumen genérica (GVLK). Puede activarla mediante el Servicio de administración de claves (KMS)/activación basada en Active Directory (AD-BA) o la clave de activación múltiple (MAK). 

    * toouse KMS/AD-BA, use un servidor KMS existente o configurar uno nuevo mediante el uso de hello paquete de licencia de volumen de Microsoft Office 2013. (Si desea, configurar servidor de hello en el nodo principal de Hola.) A continuación, activar la clave de host KMS de Hola a través de Internet de Hola o por teléfono. A continuación, clusrun `ospp.vbs` tooset Hola servidor KMS y el puerto y activar Office en todos los nodos de cálculo de Excel de Hola. 

    * toouse MAK, primer clusrun `ospp.vbs` tooinput Hola clave y, a continuación, activar todos los nodos de cálculo de Excel de Hola a través de Internet de Hola o por teléfono. 

> [!NOTE]
> Las claves de producto comercial de Office Professional Plus 2013 no se pueden usar con esta imagen de VM. Si tiene claves y medios de instalación válidos para ediciones de Office o Excel distintas de esta edición por volumen de Office Professional Plus 2013, puede usarlas. En primer lugar desinstale esta edición de volumen e instale la edición de Hola que se tenga. Hola volver a instalar Excel de nodos de proceso se pueden capturar como un toouse de imagen de máquina virtual personalizada en una implementación a escala.
> 
> 

### <a name="offload-excel-workbooks"></a>Descarga de libros de Excel
Siga estos toooffload pasos un libro de Excel para que se ejecute en el clúster de HPC Pack hello en Azure. toodo esto, debe tener Excel 2010 o 2013 ya instalados en el equipo cliente de Hola.

1. Utilice una de las opciones de hello en un clúster de HPC Pack con hello Excel del paso 1 toodeploy de proceso de imagen del nodo. Obtenga el archivo de certificado de clúster de hello (.cer) y nombre de usuario del clúster y una contraseña.
2. En el equipo de cliente hello, importe el certificado de clúster de hello en Cert: \CurrentUser\Root.
3. Asegúrese de que Excel está instalado. Cree un archivo Excel.exe.config con hello siguiente contenido en hello misma carpeta que Excel.exe en el equipo cliente de Hola. Este paso garantiza que Hola complemento HPC Pack 2012 R2 Excel COM se carga correctamente.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Configurar el clúster de HPC Pack Hola cliente toosubmit trabajos toohello. Una opción es hello toodownload completa [instalación de HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) e instalar el cliente de HPC Pack Hola. O bien, descargue e instale hello [utilidades de cliente de HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) y Hola adecuado Visual C++ 2010 redistributable para el equipo ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. En este ejemplo, usamos un libro de Excel de ejemplo denominado ConvertiblePricing_Complete.xlsb. Puede descargarlas [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Copie la carpeta de trabajo de tooa en libro de Excel de hello como D:\Excel\Run.
7. Abra el libro de Excel de Hola. En hello **desarrollar** la cinta de opciones, haga clic en **complementos COM** y confirme que hello complemento COM de Excel de HPC Pack se cargó correctamente.
   
   ![Complemento de Excel para HPC Pack][addin]
8. Macro VBA Hola editar HPCControlMacros en Excel cambiando Hola líneas comentadas tal y como se muestra en la siguiente secuencia de comandos de Hola. Sustituya los valores adecuados para su entorno.
   
   ![Macro de Excel para HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Copie el directorio carga tooan de libro de Excel de hello como D:\Excel\Upload. Este directorio se especifica en la constante de HPC_DependsFiles de Hola de macro VBA Hola.
10. libro de hello toorun en clúster de hello en Azure, haga clic en hello **clúster** botón en la hoja de cálculo de Hola.

### <a name="run-excel-udfs"></a>Ejecución de UDF de Excel
toorun UDF de Excel, siga Hola pasos anteriores tooset 1-3-el equipo de cliente de Hola. En las UDF de Excel, no es necesario toohave aplicación de Excel hello instalado en nodos de proceso. Por lo tanto, al crear el clúster de nodos de proceso, puede elegir la imagen de un nodo de proceso normal en lugar de hello calcule la imagen del nodo con Excel.

> [!NOTE]
> Hay un límite de 34 caracteres Hola Excel 2010 y el cuadro de diálogo de conector de clúster de 2013. Utilice este clúster de Hola de toospecify de cuadro de diálogo que ejecuta las UDF de Hola. Si el nombre completo del clúster de hello es mayor (por ejemplo, hpcexcelhn01.southeastasia.cloudapp.azure.com), no cabe en el cuadro de diálogo de Hola. Hola solución alternativa es tooset una variable de todo el equipo como *CCP_IAASHN* con valor de Hola de nombre de clúster largo Hola. A continuación, escriba *CCP_IAASHN %* en cuadro de diálogo de hello como nombre de nodo principal del clúster de Hola. 
> 
> 

Después de que el clúster de Hola se implementa correctamente, continúe con hello siguiendo los pasos toorun integrada una ejemplo UDF de Excel. En las UDF de Excel personalizada, vea estas [recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Hola XLL e implementarlas en clúster de IaaS de Hola.

1. Abra un nuevo libro de Excel. En hello **desarrollar** la cinta de opciones, haga clic en **Add-Ins**. Haga clic en el cuadro de diálogo de hello, **examinar**, desplazarse por las carpetas de %CCP_HOME%Bin\XLL32 toohello y seleccione el ejemplo hello ClusterUDF32.xll. Si hello no existe ClusterUDF32 en el equipo de cliente hello, copiarlo de carpeta de %CCP_HOME%Bin\XLL32 de hello en el nodo principal de Hola.
   
   ![Seleccione Hola UDF][udf]
2. Haga clic en **Archivo** > **Opciones** > **Avanzadas**. En **fórmulas**, comprobar **permitir toorun funciones XLL definido por el usuario en un clúster de cálculo**. A continuación, haga clic en **opciones** y escriba el nombre completo del clúster de hello en **nombre de nodo principal del clúster**. (Como se indicó anteriormente este cuadro de entrada es limitado too34 caracteres, por lo que no puede ajustarse a un nombre de clúster largo. Para un nombre de clúster largo, aquí puede usar una variable a nivel de la máquina).
   
   ![Configurar Hola UDF][options]
3. Hola toorun cálculo UDF en clúster de hello, haga clic en la celda de hello con valor =XllGetComputerNameC() y presione ENTRAR. función Hello simplemente recupera Hola nombre del nodo de proceso de hello en qué Hola UDF se ejecuta. Para hello ejecuta por primera vez, un cuadro de diálogo de credenciales solicita Hola username y password tooconnect toohello clúster de IaaS.
   
   ![Ejecución de UDF][run]
   
   Cuando hay muchas toocalculate de celdas, presione Mayús-Alt-Ctrl + cálculo de hello toorun F9 en todas las celdas.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>Paso 3: Ejecución de una carga de trabajo de SOA desde un cliente local
toorun aplicaciones generales de SOA en clúster de IaaS de HPC Pack hello, en primer lugar usar uno de los métodos de hello en clúster de Hola de toodeploy de paso 1. Especifique la imagen de un nodo de proceso genérico en este caso, dado que no necesitan Excel en los nodos de proceso de Hola. A continuación, siga estos pasos.

1. Después de recuperar el certificado de clúster de hello, importarlo en el equipo de cliente de hello en Cert: \CurrentUser\Root.
2. Instalar hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) y [utilidades de cliente de HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923). Estas herramientas le permiten toodevelop y ejecutan aplicaciones de cliente SOA.
3. Descargar hello HelloWorldR2 [código de ejemplo](https://www.microsoft.com/download/details.aspx?id=41633). Abra Hola HelloWorldR2.sln en Visual Studio 2010 o 2012. (Este ejemplo no es compatible actualmente con las versiones más recientes de Visual Studio).
4. Compile el proyecto de EchoService de hello en primer lugar. A continuación, implemente el clúster de IaaS de hello servicio toohello Hola se implementan igual tooan local clúster. Para obtener instrucciones detalladas, consulte Hola Léame.doc en HelloWordR2. Modificar y crear hello HellWorldR2 y otros proyectos, como se describe en hello siguiendo la sección toogenerate Hola SOA las aplicaciones cliente que se ejecutan en un clúster de IaaS de Azure.

### <a name="use-http-binding-with-azure-storage-queue"></a>Uso del enlace Http con colas de almacenamiento de Azure
enlace Http de toouse con una cola de almacenamiento de Azure, realizar algunos cambios de código de ejemplo de toohello.

* Nombre del clúster de Hola de actualización.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* Opcionalmente, utilice Hola predeterminada TransportScheme SessionStartInfo o establecerlo explícitamente tooHttp.

```
    info.TransportScheme = TransportScheme.Http;
```

* Usar enlace predeterminado para hello BrokerClient.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    O establezca explícitamente utilizando basicHttpBinding Hola.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* Opcionalmente, establezca hello UseAzureQueue marca tootrue en SessionStartInfo. Si no se establece, se establecerá tootrue de forma predeterminada cuando el nombre del clúster de hello tiene sufijos de dominio de Azure y hello TransportScheme es Http.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Uso del enlace Http sin colas de almacenamiento de Azure
enlace Http de toouse sin una cola de almacenamiento de Azure, explícitamente conjunto hello UseAzureQueue marca toofalse Hola SessionStartInfo.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>Uso del enlace NetTcp
toouse NetTcp de enlace, configuración de hello es clúster local de similar tooconnecting tooan. Debe tooopen unos puntos de conexión en la máquina virtual del nodo principal Hola. Si utiliza clústeres de hello IaaS de HPC Pack implementación script toocreate hello, por ejemplo, establecer extremos de hello en Hola portal de Azure como se indica a continuación.

1. Detener Hola máquina virtual.
2. Agregar puertos TCP de hello 9090, 9087, 9091, 9094 para hello sesión, Broker, agente de trabajo y servicios de datos, respectivamente
   
    ![Configuración de extremos][endpoint-new-portal]
3. Iniciar VM Hola.

aplicación de cliente SOA de Hello no requiere ningún cambio excepto Modificar Hola principal toohello IaaS clúster: nombre completo.

## <a name="next-steps"></a>Pasos siguientes
* Consulte [estos recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para obtener más información sobre cómo ejecutar las cargas de trabajo de Excel con HPC Pack.
* Consulte [Administración de servicios de SOA en Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) para obtener más información sobre la implementación y administración de servicios de SOA con HPC Pack.

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
