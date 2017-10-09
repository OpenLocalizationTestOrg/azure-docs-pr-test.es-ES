---
title: "aaaCreate una máquina virtual de Azure con Accelerated redes | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con Accelerated redes."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Creación de una máquina virtual con Accelerated Networking

En este tutorial, aprenderá cómo toocreate una máquina Virtual (VM) de Azure con Accelerated redes. Las redes aceleradas están en disponibilidad general para Windows y en versión preliminar pública para distribuciones de Linux específicas. Redes acelerada permite tooa virtualización (SR-IOV) de E/S de raíz única máquina virtual, se mejora significativamente el rendimiento de red. Esta ruta de acceso de alto rendimiento omite host Hola de ruta de datos de hello reduce la latencia y vibración, uso de CPU, para su uso con hello más exigentes red cargas de trabajo en tipos admitidos de máquina virtual. Hola la siguiente imagen se muestra en comunicación entre dos máquinas virtuales (VM) con y sin redes acelerada:

![De comparación](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Sin red acelerado, todo el tráfico de red dentro y fuera de hello VM debe atravesar host Hola y el conmutador virtual de Hola. conmutador virtual de Hello exige la aplicación de directiva de todos los, tales como grupos de seguridad de red acceso a listas de control, aislamiento y otro tráfico de toonetwork de servicios de red virtualizado. más información acerca de los modificadores virtuales, leer hello toolearn [virtualización de red de Hyper-V y el conmutador virtual](https://technet.microsoft.com/library/jj945275.aspx) artículo.

Con las redes acelerada, el tráfico de red llega a la interfaz de red (NIC) de la máquina virtual de hello y, a continuación, se reenvía toohello máquina virtual. Se aplica todas las directivas de red que Hola conmutador virtual sin redes acelerada se descarga y se aplican en hardware. Aplicar directiva de hardware permite Hola NIC tooforward tráfico de red directamente toohello VM, omitiendo el host de Hola y el conmutador virtual de hello, al tiempo que mantiene todas las directivas de Hola aplica en el host de Hola.

Hello ventajas de las redes acelerada solo aplican toohello máquina virtual que se ha habilitado en. Para obtener mejores resultados de hello, resulta ideal tooenable esta característica en al menos dos máquinas virtuales conectadas toohello misma red Virtual de Azure (VNet). Cuando se comunica a través de redes virtuales o conexión de forma local, esta característica tiene una latencia toooverall un impacto mínimo.

> [!WARNING]
> Este Linux versión preliminar pública que no tenga Hola son del mismo nivel de disponibilidad y confiabilidad como características que por lo general versión de disponibilidad. características de Hello no se admiten, pueden haber limitado las capacidades y pueden no estar disponibles en todas las ubicaciones de Azure. Para hello más las notificaciones de actualización de disponibilidad y estado de esta característica, consulte la página de actualizaciones de red Virtual de Azure de Hola.

## <a name="benefits"></a>Ventajas
* **Menor latencia / superior paquetes por segundo (pps):** conmutador virtual de hello Removing de ruta de datos de hello quita tiempo Hola dedican de paquetes en el host de hello para el procesamiento de directiva y aumenta Hola número de paquetes que se pueden procesar dentro de hello VM.
* **Reduce la vibración:** conmutador Virtual de procesamiento depende de la cantidad de Hola de directiva que necesita toobe aplicado y carga de trabajo Hola de hello CPU que realiza el procesamiento de Hola. La descarga de hardware de toohello de cumplimiento de directiva de hello quita esa variabilidad proporcionando paquetes directamente toohello máquina virtual, quite interrupciones de software y contexto de comunicación con el host tooVM hello y todos los conmutadores.
* **Reduce el uso de CPU:** omisión Hola del conmutador virtual de host de hello conduce uso de CPU que no requiere herramientas para procesar el tráfico de red.

## <a name="Limitations"></a>Limitaciones
Hola siguientes limitaciones existe cuando se usa esta capacidad:

* **Creación de interfaz de red:** Accelerated Networking solo se puede habilitar para una nueva interfaz de red. No se puede habilitar para una NIC existente.
* **Creación de máquinas virtuales:** una NIC con redes acelerada habilitada puede solo tooa adjunto VM cuando hello máquina virtual se creará. Hola NIC no puede ser tooan adjunto existente de la máquina virtual.
* **Regiones:** la mayoría de las regiones de Azure ofrecen máquinas virtuales de Windows con Accelerated Networking. En numerosas regiones se ofrecen máquinas virtuales de Linux con redes aceleradas. se está expandiendo regiones Hola esta capacidad está disponible en. Vea el blog de las actualizaciones de red Virtual de Azure de Hola a continuación para obtener información más reciente de Hola.   
* **Sistemas operativos compatibles:** para Windows, Microsoft Windows Server 2012 R2 Datacenter y Windows Server 2016. Para Linux, Ubuntu Server 16.04 LTS con kernel 4.4.0-77 o superior, SLES 12 SP2, RHEL 7.3 y CentOS 7.3 (publicado por Rogue Wave Software).
* **Tamaño de máquina virtual:** instancias de uso general y de proceso optimizado con ocho o más núcleos. Para obtener más información, vea hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) y [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículos de tamaños de máquina virtual. Hola se expandirá conjunto de tamaños de instancia de máquina virtual admitidos en hello futuras.
* **Implementación mediante Azure Resource Manager (ARM):** la funcionalidad de redes aceleradas no se puede implementar mediante ASM/RDFE.

Limitaciones de toothese de cambios se anuncian a través de hello [red Virtual de Azure actualiza](https://azure.microsoft.com/updates/accelerated-networking-in-preview) página.

## <a name="create-a-windows-vm"></a>Creación de una máquina virtual Windows
Puede usar Hola portal de Azure o Azure [PowerShell](#windows-powershell) toocreate Hola máquina virtual.

### <a name="windows-portal"></a>Portal

1. Desde un explorador de Internet, abra hello Azure [portal](https://portal.azure.com) e inicie sesión con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. En el portal de hello, haga clic en **+ nuevo** > **proceso** > **Windows Server 2016 Datacenter**. 
3. Hola **Windows Server 2016 Datacenter** hoja que aparece, deje *el Administrador de recursos* seleccionado en **seleccionar un modelo de implementación**y haga clic en **crear **.
4. Hola **Fundamentos** hoja que aparece, escriba Hola después de valores, deje Hola restantes opciones predeterminadas o seleccione o escriba sus propios valores y haga clic en hello **Aceptar** botón:

    |Configuración|Valor|
    |---|---|
    |Nombre|MyVm|
    |Grupos de recursos|Deje seleccionado **Crear nuevo** y escriba *MyResourceGroup*.|
    |Ubicación|Oeste de EE. UU. 2|

    Si es nuevo tooAzure, obtenga más información sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [suscripciones](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), y [ubicaciones](https://azure.microsoft.com/regions) (que también aparecen tooas regiones).
5. Hola **elegir un tamaño de** hoja que aparece, escriba *8* en hello **cantidad mínima de núcleos** cuadro, a continuación, haga clic en **todas las ver**.
6. Haga clic en **DS4_V2 estándar**, o cualquier admitido VM, a continuación, haga clic en hello **seleccione** botón.
7. Hola **configuración** hoja que aparece, deje todos los valores de configuración como-es, pero sin hacer clic **habilitado** en **Accelerated redes**, a continuación, haga clic en hello **Aceptar** botón. **Nota:** si, en los pasos anteriores, seleccionó valores de tamaño VM, el sistema operativo o la ubicación que no aparezcan en hello [limitaciones](#Limitations) sección de este artículo, **acelerado redes**no está visible.
8. Hola **resumen** hoja que aparece, haga clic en hello **Aceptar** botón. Azure comienza a crear Hola máquina virtual. La creación tarda unos minutos.
9. Hola tooinstall accelerated controlador de redes para Windows, Hola completa los pasos de hello [configurar Windows](#configure-windows) sección de este artículo.

### <a name="windows-powershell"></a>PowerShell
1. Instale Hola la versión más reciente de hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Si es nuevo tooAzure PowerShell, leer hello [Introducción a Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.
2. Iniciar una sesión de PowerShell haciendo clic en el botón de inicio de Windows hello, escriba **powershell**, a continuación, haga clic en **PowerShell** en los resultados de búsqueda de Hola.
3. En la ventana de PowerShell, escriba Hola `login-azurermaccount` toosign de comando con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. En el explorador, copie Hola siguiente secuencia de comandos:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. En la ventana de PowerShell, haga clic en el script de Hola toopaste e iniciará ejecutarla. Se le pide un nombre de usuario y una contraseña. Usar estas credenciales toolog en toohello VM al conectarse tooit en el paso siguiente Hola. Si se produce un error en la secuencia de comandos de Hola y cambiar valores en el script de Hola antes de ejecutarlo, confirme los valores de hello que ha utilizado para el tamaño de máquina virtual, sistema operativo, y ubicación se muestran en hello [limitaciones](#Limitations) sección de este artículo.
6. Hola tooinstall accelerated controlador de redes para Windows, Hola completa los pasos de hello [configurar Windows](#configure-windows) sección de este artículo.

### <a name="configure-windows"></a>Configuración de Windows
Una vez que cree Hola VM en Azure, debe instalar el controlador de red acelerada de Hola para Windows. Antes de completar Hola pasos, debe haber creado una máquina virtual de Windows con redes acelerada con cualquier hello [portal](#windows-portal) o [PowerShell](#windows-powershell) los pasos de este artículo. 

1. Desde un explorador de Internet, abra hello Azure [portal](https://portal.azure.com) e inicie sesión con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. En el cuadro de Hola que contiene texto hello *buscar recursos* Hola parte superior de hello portal de Azure, escriba *MyVm*. Cuando **MyVm** aparece en los resultados de búsqueda de hello, haga clic en él.
3. Hola **MyVm** hoja que aparece, haga clic en hello **conectar** botón en hello la esquina superior izquierda de la hoja de Hola. **Nota:** si **crear** está visible en hello **conectar** botón, Azure no ha terminado de crear Hola máquina virtual. Haga clic en **conectar** sólo después de que ya no verá **crear** en hello **conectar** botón.
4. Permitir su Hola de explorador toodownload **MyVm.rdp** archivo.  Una vez descargado, haga clic en hello archivo tooopen lo. 
5. Haga clic en hello **conectar** botón en hello **conexión a Escritorio remoto** cuadro que aparece, le notifica que hello no se puede identificar el Editor de conexión remota de Hola.
6. Hola **la seguridad de Windows** cuadro que aparece, haga clic en **más opciones**, a continuación, haga clic en **Use otra cuenta**. Escriba el nombre de usuario de Hola y la contraseña que especificó en el paso 4, haga clic en hello **Aceptar** botón.
7. Haga clic en hello **Sí** en botón del cuadro de conexión a Escritorio remoto de Hola que aparece, le notifica que no se puede comprobar la identidad de hello del equipo remoto Hola.
8. Haga clic en el botón de inicio de Windows hello y haga clic en **el Administrador de dispositivos**. Expanda hello **adaptadores de red** nodo. Confirme que hello **Mellanox ConnectX-3 adaptador de Ethernet de función Virtual** aparece como se muestra en hello después de imagen:
   
    ![Administrador de dispositivos](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. Las redes aceleradas ya están habilitadas para su máquina virtual.

## <a name="create-a-linux-vm"></a>Creación de una máquina virtual Linux
Puede usar Hola portal de Azure o Azure [PowerShell](#linux-powershell) toocreate un Ubuntu o SLES VM. En el caso de las máquinas virtuales RHEL y CentOS, el flujo de trabajo es diferente.  Consulte las instrucciones de hello siguientes.

### <a name="linux-portal"></a>Portal
1. Registro de hello accelerated redes de Linux preview siguiendo los pasos del 1 al 5 del programa Hola a [crear una VM Linux - PowerShell](#linux-powershell) sección de este artículo.  No se puede registrar para la vista previa de hello en el portal de Hola.
2. Complete los pasos 1-8 en hello [crear una VM de Windows - portal](#windows-portal) sección de este artículo. En el paso 2, haga clic en **Ubuntu Server 16.04 LTS** en lugar de **Windows Server 2016 Datacenter**. Para este tutorial, elija toouse una contraseña, en lugar de una clave SSH, aunque para las implementaciones de producción, puede usar. Si **Accelerated redes** no aparece cuando se completa el paso 7 de hello [crear una VM de Windows - portal](#windows-portal) sección de este artículo, es probable para uno de hello siguientes motivos:
    - No se ha registrado para la vista previa de Hola. Confirme que el estado de registro es **registrado**, tal como se describe en el paso 4 de hello [crear una VM Linux - Powershell](#linux-powershell) sección de este artículo. **Nota:** si ha participado en hello acelerado de red para la vista previa de máquinas virtuales de Windows (su ningún toouse tooregister necesarios más acelerado de redes para máquinas virtuales de Windows), no se registra automáticamente para hello acelerado red para Obtener una vista previa en máquinas virtuales de Linux. Debe registrar para hello acelerado de red para obtener una vista previa en máquinas virtuales de Linux tooparticipate en ella.
    - No se ha seleccionado un tamaño VM, el sistema operativo o la ubicación que se indica en hello [limitaciones](#limitations) sección de este artículo.
3. Hola tooinstall accelerated controlador de redes de Linux, Hola completa los pasos de hello [configurar Linux](#configure-linux) sección de este artículo.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>Si crear máquinas virtuales de Linux con redes acelerada en una suscripción y, a continuación, intente toocreate una VM de Windows con las redes acelerada de Hola misma suscripción, que puede producir un error Hola creación de VM de Windows. Durante esta versión preliminar, se recomienda probar las máquinas virtuales Windows y Linux con Accelerated Networking en suscripciones independientes.
>

1. Instale Hola la versión más reciente de hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Si es nuevo tooAzure PowerShell, leer hello [Introducción a Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo.
2. Iniciar una sesión de PowerShell haciendo clic en el botón de inicio de Windows hello, escriba **powershell**, a continuación, haga clic en **PowerShell** en los resultados de búsqueda de Hola.
3. En la ventana de PowerShell, escriba Hola `login-azurermaccount` toosign de comando con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Registrarme para hello accelerated redes de Azure preview siguiendo Hola pasos:
    - Enviar un correo electrónico demasiado[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) con su Id. de suscripción de Azure y el uso previsto. Espere a recibir una confirmación por correo electrónico de Microsoft que le indique que la suscripción está habilitada.
    - Escriba Hola después tooconfirm de comando que se registra para la vista previa de hello:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        No continúe con el paso 5 hasta que **registrado** aparece en hello después de escribir el comando anterior Hola de salida. El resultado debe ser similar siguiente de hello resultado antes de continuar:
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Si ha participado en hello acelerado de red para la vista previa de máquinas virtuales de Windows (su ningún toouse tooregister necesarios más acelerado de redes para máquinas virtuales de Windows), no se registra automáticamente para hello acelerado de la red para la vista previa de las máquinas virtuales de Linux. Debe registrar para hello acelerado de red para obtener una vista previa en máquinas virtuales de Linux tooparticipate en ella.
      >
5. En el explorador, copie Hola siguiente secuencia de comandos sustituyendo Ubuntu o SLES según sea necesario.  Redhat y CentOS tienen un flujo de trabajo diferente, que se describe a continuación:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. En la ventana de PowerShell, haga clic en el script de Hola toopaste e iniciará ejecutarla. Se le pide un nombre de usuario y una contraseña. Usar estas credenciales toolog en toohello VM al conectarse tooit en el paso siguiente Hola. Si se produce un error en la secuencia de comandos de hello, confirme:
    - Se registran para la vista previa de hello, tal como se describe en el paso 4
    - Si cambia de tamaño, el tipo de sistema operativo o los valores de ubicación en el script de Hola VM antes de ejecutarlo y que se mostrarán los valores de hello en hello [limitaciones](#Limitations) sección de este artículo.
7. Hola tooinstall accelerated controlador de redes de Linux, Hola completa los pasos de hello [configurar Linux](#configure-linux) sección de este artículo.

### <a name="configure-linux"></a>Configuración de Linux

Una vez que cree Hola VM en Azure, debe instalar el controlador de red acelerada de Hola para Linux. Antes de completar Hola pasos, debe haber creado una VM de Linux con redes acelerada con cualquier hello [portal](#linux-portal) o [PowerShell](#linux-powershell) los pasos de este artículo. 

1. Desde un explorador de Internet, abra hello Azure [portal](https://portal.azure.com) e inicie sesión con Azure [cuenta](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Si aún no dispone de una cuenta, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. En parte superior de Hola de hello portal, toohello derecha hello *buscar recursos* barra, haga clic en hello **> _** icono toostart un shell de Bash en la nube (versión preliminar). Hello panel de shell de Bash en la nube aparece en hello parte inferior del portal de Hola y después de unos segundos, se presenta un ** username@Azure:~ $** símbolo del sistema. Aunque puede SSH toohello máquina virtual desde su equipo, en lugar de shell en la nube de hello, instrucciones de hello en este tutorial en el que se supone que usa el shell de hello en la nube.
3. Hola parte superior de portal de hello, en el cuadro de Hola que contiene texto hello *buscar recursos*, tipo *MyVm*. Cuando **MyVm** aparece en los resultados de búsqueda de hello, haga clic en él.
4. Hola **MyVm** hoja que aparece, haga clic en hello **conectar** botón en hello la esquina superior izquierda de la hoja de Hola. **Nota:** si **crear** está visible en hello **conectar** botón, Azure no ha terminado de crear Hola máquina virtual. Haga clic en **conectar** sólo después de que ya no verá **crear** en hello **conectar** botón.
5. Azure abre un cuadro que indique hello tooenter `ssh adminuser@<ipaddress>`. Escriba este comando en hello en la nube shell (o copia del cuadro de Hola que aparecían en el paso 4 y péguelo en el shell de nube toohello), a continuación, presione ENTRAR.
6. ENTRAR **Sí** toohello preguntando si desea conectar toocontinue, a continuación, presionar ENTRAR.
7. Escriba la contraseña de Hola que especificó al crear Hola máquina virtual. Una vez ha iniciado sesión correctamente en toohello de máquina virtual, verá un adminuser@MyVm:~ símbolo del sistema de $. Ahora se registran en toohello máquina virtual a través de la sesión de shell de hello en la nube. **Nota:** Las sesiones de Cloud Shell agotan el tiempo de espera tras 10 minutos de inactividad.

En este momento, las instrucciones de hello varían en función de distribución de Hola que usa. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. En el símbolo del sistema de hello, escriba `uname -r` y confirme la versión de Hola para:

    * Ubuntu: "4.4.0-77-generic," o superior
    * SLES: "4.4.59-92.20-default" o superior

2. Crear un bono entre vNIC de red estándar de Hola y Hola accelerated red vNIC mediante la ejecución de los comandos de Hola que siguen. Tráfico de red usa Hola con mayor rendimiento acelerado vNIC de red, mientras bond Hola garantiza que el tráfico de red no se interrumpe en determinados cambios de configuración.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. Después de ejecutar script de Hola, Hola VM se reiniciará después de pausar un 60 segundos.
4. Una vez Hola VM se reinicia, vuelva a conectar tooit completando los pasos 5 a 7 nuevo.
5. Ejecute hello `ifconfig` comando y confirme que sale bond0 e interfaz Hola se muestra como arriba. 
 
 >[!NOTE]
      >Las aplicaciones que usan las redes acelerada deben comunicarse a través de hello *bond0* interfaz, no *eth0*.  nombre de la interfaz de Hello puede cambiar antes de que las redes acelerada alcance la disponibilidad general.

#### <a name="rhelcentos"></a>RHEL/CentOS

Creación de una Red Hat Enterprise Linux o CentOS 7.3 VM requiere algunos adicional de los pasos necesarios para SR-IOV y controlador de función Virtual (VF) de tarjeta de red de Hola Hola controladores tooload hello más recientes. Hola primera fase de instrucciones de hello prepara una imagen que puede ser utilizado toomake uno o más máquinas virtuales que tienen controladores de hello previamente cargados.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>Fase uno: preparar una imagen base de Red Hat Enterprise Linux o CentOS 7.3. 

1.  Aprovisione una máquina virtual que no sea SRIOV CentOS 7.3 en Azure.

2.  Instale LIS 4.2.2:
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  Descargue los archivos de configuración.
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Desaprovisione esta máquina virtual.

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  Desde el portal de Azure, detener esta máquina virtual; y vaya "Discos" del tooVM, capturar el URI de VHD de hello OSDisk. Este URI contiene el nombre de disco duro virtual de la imagen base de Hola y su cuenta de almacenamiento. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>Fase 2: aprovisionar nuevas máquinas virtuales en Azure

1.  Aprovisionar nuevas máquinas virtuales según con New-AzureRMVMConfig utilizando Hola base imagen VHD capturado en la primera fase, con AcceleratedNetworking habilitado en hello vNIC:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Después de arrancan las máquinas virtuales, comprobar el dispositivo de VF Hola por "lspci" y compruebe la entrada del Mellanox Hola. Por ejemplo, debemos vemos este elemento en la salida de hello lspci:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Ejecutar script de unión de Hola por:

    ```bash
    sudo bondvf.sh
    ```

4.  Reiniciar Hola nuevas máquinas virtuales:

    ```bash
    sudo reboot
    ```

Hola VM debe comenzar con hello ruta acelerado de red habilitado y bond0 configurado.  Ejecutar `ifconfig` tooconfirm.
