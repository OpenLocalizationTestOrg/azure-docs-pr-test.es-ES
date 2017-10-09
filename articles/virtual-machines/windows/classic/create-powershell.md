---
title: aaaCreate una VM de Windows con PowerShell | Documentos de Microsoft
description: "Crear máquinas virtuales de Windows con PowerShell de Azure y modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>Crear una máquina virtual de Windows con el modelo de implementación clásica de hello y PowerShell
> [!div class="op_single_selector"]
> * [Azure Portal - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Estos pasos muestra cómo toocustomize un conjunto de Azure PowerShell comandos que crear y preconfigurar una máquina virtual de Azure basado en Windows mediante un enfoque de bloque de creación. Puede utilizar este proceso tooquickly crear un conjunto de comandos para una nueva máquina virtual basada en Windows y expandir una implementación existente o crear una personalizada para desarrollo y pruebas o el entorno profesional de TI toocreate varios comandos que establece rápidamente.

En estos pasos se sigue un enfoque consistente en atar cabos para crear conjuntos de comandos de Azure PowerShell. Este enfoque puede ser útil si está tooPowerShell nueva o simplemente desea tooknow qué toospecify valores para una configuración correcta. Los usuarios avanzados de PowerShell pueden tomar los comandos de Hola y sustituir sus propios valores para las variables de hello (líneas de hello comenzar con "$").

Si aún no lo ha no lo ha hecho, use las instrucciones de hello en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell en el equipo local. Después, abra el símbolo del sistema de Windows PowerShell.

## <a name="step-1-add-your-account"></a>Paso 1: agregar la cuenta
1. En el símbolo del sistema de PowerShell hello, escriba **Add-AzureAccount** y haga clic en **ENTRAR**. 
2. Escriba Hola dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **continuar**. 
3. Escribir contraseña de Hola para su cuenta. 
4. Haga clic en **Iniciar sesión**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Paso 2: establecimiento de la cuenta de suscripción y almacenamiento
Establecer la suscripción de Azure y la cuenta de almacenamiento mediante la ejecución de estos comandos en línea de comandos de Windows PowerShell de Hola. Reemplace todo el contenido de las comillas de hello, incluidos Hola < y > caracteres, con los nombres correctos de Hola.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Puede obtener nombre de la suscripción correcta de Hola de hello SubscriptionName propiedad de salida de hello de hello **Get-AzureSubscription** comando. Puede obtener nombre de cuenta de almacenamiento correcta de Hola de hello propiedad Label de salida de hello de hello **Get AzureStorageAccount** comando después de ejecutar hello **Select-AzureSubscription** comando.

## <a name="step-3-determine-hello-imagefamily"></a>Paso 3: Determinar hello ImageFamily
A continuación, necesita toodetermine Hola ImageFamily o valor de etiqueta para hello imagen específica correspondiente toohello máquina virtual de Azure que desee toocreate. Puede obtener Hola lista de valores disponibles de ImageFamily con este comando.

    Get-AzureVMImage | select ImageFamily -Unique

A continuación, se muestran algunos ejemplos de valores de ImageFamily para equipos basados en Windows:

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1
* Windows Server 2016 Technical Preview 4
* SQL Server 2012 SP1 Enterprise en Windows Server 2012

Si encuentra la imagen de Hola que está buscando, abra una nueva instancia del editor de texto hello de su elección u Hola PowerShell Integrated Scripting Environment (ISE). Copie Hola siguiente en el nuevo archivo de texto de Hola o hello PowerShell ISE, sustituyendo el valor de ImageFamily Hola.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

En algunos casos, nombre de la imagen de hello es Hola propiedad de etiqueta en lugar de hello ImageFamily valor. Si no encontró la imagen de Hola que desea para el uso de la propiedad ImageFamily hello, una lista de imágenes de Hola por su propiedad de etiqueta con este comando.

    Get-AzureVMImage | select Label -Unique

Si encuentra la imagen de la derecha Hola con este comando, abra una nueva instancia del editor de texto hello de su elección u Hola PowerShell ISE. Copie Hola siguiente en el nuevo archivo de texto de Hola o hello PowerShell ISE, sustituyendo el valor de la etiqueta de Hola.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>Paso 4: Creación del conjunto de comandos
Construir el resto de hello del comando establecer copiando el conjunto adecuado de Hola de bloques a continuación en el nuevo archivo de texto u Hola ISE y, a continuación, rellena los valores de variable de Hola y quitando Hola < y > caracteres. Vea Hola dos [ejemplos](#examples) final Hola de este artículo para obtener una idea del resultado final de Hola.

Inicie el conjunto de comandos eligiendo uno de estos dos bloques de comandos (obligatorio).

Opción 1: Especificación de un nombre de máquina virtual y un tamaño.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Opción 2: Especificación de un nombre, un tamaño y un nombre del conjunto de disponibilidad.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

Para los valores de InstanceSize Hola D, DS o máquinas virtuales de serie G, vea [Máquina Virtual y tamaños de servicio de nube de Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

> [!NOTE]
> Si tiene un contrato Enterprise con Software Assurance y piensa tootake aprovechar Hola Windows Server [ventaja del uso de híbrida](https://azure.microsoft.com/pricing/hybrid-use-benefit/), agregar el **- LicenseType** toohello parámetro  **New-AzureVMConfig** cmdlet, se pasa el valor de hello **Windows_Server** para hello típico caso de usuario.  Asegúrese de que usa una imagen que ha cargado; no se puede usar una imagen estándar de hello galería con hello híbrida ventaja de usar.
> 
> 

Si lo desea, para un equipo de Windows independiente, especifique cuentas de administrador local de Hola y contraseñas.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

Elija una contraseña segura. toocheck su nivel de seguridad, consulte [Comprobador de contraseñas: uso de contraseñas seguras](https://www.microsoft.com/security/pc-security/password-checker.aspx).

Si lo desea, tooadd Hola Windows equipo tooan dominio de Active Directory, especifique la cuenta de administrador local de Hola y contraseña, dominio hello y nombre de Hola y la contraseña de una cuenta de dominio.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Para opciones de configuración previa adicionales para máquinas virtuales basadas en Windows, vea la sintaxis de Hola para hello **Windows** y **WindowsDomain** parámetro se establece [ Agregar-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).

Opcionalmente, asigne máquina virtual de hello una dirección IP específica, conocida como una DIP estática.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

Puede comprobar que una dirección IP concreta está disponible con:

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

Opcionalmente, asigne tooa de subred específica en una red virtual para la máquina virtual Hola.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

Opcionalmente, agregue una máquina virtual de datos único disco toohello.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Para un controlador de dominio de Active Directory, establezca $hcaching demasiado "None".

Opcionalmente, agregue Hola máquina virtual tooan existente conjunto de carga equilibrada para tráfico externo.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

Por último, elija uno de estos bloques de comandos necesarios para crear la máquina virtual de Hola.

Opción 1: Crear la máquina virtual de Hola en un servicio de nube existente.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

nombre corto de Hello del servicio de nube de hello es nombre de Hola que aparece en la lista de servicios en la nube Hola Hola portal de Azure o en la lista de Hola de grupos de recursos en hello portal de Azure.

Opción 2: Crear máquina virtual de hello en un servicio en la nube y una red virtual.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>Paso 5: Ejecución del conjunto de comandos
Revise el conjunto de comandos de PowerShell de Azure Hola creado en el editor de texto u Hola PowerShell ISE que consta de varios bloques de comandos del paso 4. Asegúrese de que ha especificado todas las variables de hello necesitado y que tengan valores correctos de Hola. Además, asegúrese de que se han quitado todos los Hola < y > caracteres.

Si está utilizando un editor de texto, copia Hola comando establezca toohello Portapapeles y, a continuación, haga clic en el símbolo del sistema de abrir Windows PowerShell. Esto emitirá el conjunto de comandos de hello como una serie de comandos de PowerShell y crear la máquina virtual de Azure. Como alternativa, ejecutar comandos de hello establecido en hello PowerShell ISE.

Si va a crear esta máquina virtual de nuevo o una similar, puede:

* Guardar este conjunto de comandos como archivo de script de PowerShell (*.ps1).
* Guardar este comando establece como un runbook de automatización de Azure en hello **cuentas de automatización** sección de hello portal de Azure.

## <a id="examples"></a>Ejemplos
Presentamos dos ejemplos del uso de pasos de hello anteriores conjuntos de comandos de PowerShell de Azure toobuild que creación máquinas virtuales Azure basadas en Windows.

### <a name="example-1"></a>Ejemplo 1
Se necesita un PowerShell comando establecer máquina virtual toocreate Hola inicial para un controlador de dominio de Active Directory:

* Utiliza la imagen de Windows Server 2012 R2 Datacenter Hola.
* Tiene el nombre de hello AZDC1.
* Sea un equipo independiente.
* Tenga un disco de datos adicional de 20 GB.
* No tiene dirección IP estática de hello 192.168.244.4.
* Está en la subred de back-end de Hola de red virtual de hello AZDatacenter.
* Está en servicio de nube de hello TailspinToys de Azure.

Aquí es Hola correspondiente Azure PowerShell comando conjunto toocreate esta máquina virtual, con líneas en blanco entre cada bloque para mejorar la legibilidad.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>Ejemplo 2
Se necesita un PowerShell comando establecer toocreate una máquina virtual para un servidor de línea de negocio que:

* Utiliza la imagen de Windows Server 2012 R2 Datacenter Hola.
* Tiene el nombre de hello LOB1.
* Es un miembro de dominio de corp.contoso.com Hola.
* Tenga un disco de datos adicional de 200 GB.
* Está en la subred de front-end de Hola de red virtual de hello AZDatacenter.
* Está en servicio de nube de hello TailspinToys de Azure.

Aquí es Hola correspondiente Azure PowerShell comando conjunto toocreate esta máquina virtual.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>Pasos siguientes
Si necesita un disco del SO que es mayor que 127 GB, puede [expanda la unidad de hello OS](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

