---
title: "aaaConfigure Hola grupo de disponibilidad AlwaysOn en una máquina virtual de Azure mediante PowerShell | Documentos de Microsoft"
description: "Este tutorial utiliza los recursos que se crearon con el modelo de implementación clásica de Hola. Usar PowerShell toocreate un grupo de disponibilidad AlwaysOn en Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>Configurar Hola grupo de disponibilidad AlwaysOn en una máquina virtual de Azure con PowerShell
> [!div class="op_single_selector"]
> * [Portal de Azure clásico: interfaz de usuario](../classic/portal-sql-alwayson-availability-groups.md)
> * [Clásico: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Antes de comenzar, considere que ahora puede completar esta tarea en un modelo de Azure Resource Manager. Se recomienda el modelo de Azure Resource Manager para las implementaciones nuevas. Consulte [Grupos de disponibilidad de SQL Server AlwaysOn en máquinas virtuales de Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT]
> Se recomienda el uso de modelo del Administrador de recursos de hello en implementaciones más nuevas. Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación clásica de Hola.

Máquinas virtuales (VM) Azure puede ayudar a costo de Hola de toolower de los administradores de base de datos de un sistema de SQL Server de alta disponibilidad. Este tutorial muestra cómo agrupar tooimplement una disponibilidad mediante el uso de SQL Server Always On-to-end dentro de un entorno de Azure. Al final de Hola de tutorial de hello, la solución SQL Server Always On en Azure constará de hello siguientes elementos:

* Una red virtual que contiene varias subredes, incluida una subred front-end y back-end.
* Un controlador de dominio con un dominio de Active Directory.
* Dos VM de SQL Server que son implementados toohello subred de back-end y toohello Unidos a un dominio de Active Directory.
* Un clúster de conmutación por error de Windows tres nodos con el modelo de quórum de mayoría de nodo de Hola.
* Un grupo de disponibilidad con dos réplicas de confirmación sincrónica de una base de datos de disponibilidad.

Este escenario es una buena opción debido a su simplicidad en Azure, no por su rentabilidad ni otros factores. Por ejemplo, puede minimizar Hola número de máquinas virtuales para una toosave de grupo de disponibilidad de dos réplicas en horas de proceso en Azure mediante el controlador de dominio de hello como testigo de recurso compartido de archivos de hello quórum en un clúster de conmutación por error de dos nodos. Este método reduce el recuento VM de hello en uno de Hola por encima de la configuración.

Este tutorial está concebido tooshow Hola pasos tooset requiere seguridad Hola describe la solución anterior, sin profundizar en los detalles de Hola de cada paso. Por lo tanto, en lugar de proporcionar los pasos de configuración Hola GUI, usa scripting tootake de PowerShell se rápidamente a través cada paso. Este tutorial se da por supuesto siguiente hello:

* Ya tiene una cuenta de Azure con la suscripción de la máquina virtual de Hola.
* Ha instalado hello [cmdlets de PowerShell de Azure](/powershell/azure/overview).
* Ya tiene un conocimiento sólido de grupos de disponibilidad AlwaysOn para soluciones locales. Para obtener más información, consulte [Grupos de disponibilidad AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Conectar tooyour suscripción de Azure y crear red virtual de Hola
1. En una ventana de PowerShell en el equipo local, importar Hola módulo de Azure, descargue Hola máquina de tooyour del archivo de configuración de publicación y conectar su tooyour de sesión de PowerShell suscripción de Azure importando la configuración de publicación de hello descargado.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    Hola **Get-AzurePublishSettingsFile** comando genera un certificado de administración con Azure automáticamente y descarga tooyour máquina. Un explorador se abre automáticamente y le tooenter solicitadas hello las credenciales de cuenta de Microsoft para su suscripción de Azure. Hola descargado **.publishsettings** archivo contiene toda la información de Hola que necesita toomanage su suscripción de Azure. Después de guardar este directorio local de tooa de archivo, impórtelo mediante el uso de hello **importación-AzurePublishSettingsFile** comando.

   > [!NOTE]
   > archivo .publishsettings de Hello contiene las credenciales (sin codificar) que son utilizado tooadminister sus servicios y suscripciones de Azure. práctica recomendada de seguridad de Hola para este archivo es toostore lo temporalmente fuera de los directorios de origen (por ejemplo, en la carpeta bibliotecas\documentos Hola) y, a continuación, eliminarlo una vez ha finalizado la importación de Hola. Un usuario malintencionado que obtenga el archivo .publishsettings de acceso toohello puede modificar, crear y eliminar los servicios de Azure.

2. Defina una serie de variables que podrá usar toocreate su infraestructura de TI en la nube.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    Pagar toohello atención después tooensure que los comandos se ejecutarán correctamente después:

   * Las variables **$storageAccountName** y **$dcServiceName** debe ser único porque se encuentran utilizan tooidentify su cuenta de almacenamiento de nube y servidor de nube, respectivamente, en hello Internet.
   * Hola nombres especificados para las variables **$affinityGroupName** y **$virtualNetworkName** se configuran en el documento de configuración de red virtual de Hola que va a utilizar más adelante.
   * **$sqlImageName** especifica el nombre de hello actualizado de imagen de máquina virtual de Hola que contiene SQL Server 2012 Service Pack 1 Enterprise Edition.
   * Para simplificar, **Contoso! 000** es Hola misma contraseña que se utiliza a lo largo de todo el tutorial Hola.

3. Cree un grupo de afinidad.

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. Cree una red virtual importando un archivo de configuración.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    archivo de configuración de Hello contiene Hola siguiente documento XML. En resumen, especifica una red virtual denominada **ContosoNET** en el grupo de afinidad de hello denominado **ContosoAG**. Tiene espacio de direcciones de hello **10.10.0.0/16** y dos subredes, **10.10.1.0/24** y **10.10.2.0/24**, que son subred front-end de Hola y subred back-end, respectivamente. subred de front-end de Hello es donde puede colocar las aplicaciones cliente como Microsoft SharePoint. subred de back-end de Hello es donde colocará la VM de hello SQL Server. Si cambia hello **$affinityGroupName** y **$virtualNetworkName** variables anteriores, debe cambiar también Hola correspondientes nombres siguientes.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Cree una cuenta de almacenamiento que esté asociada con el grupo de afinidad de Hola que creó y establézcalo como cuenta de almacenamiento actual de hello en su suscripción.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Crear servidor de controlador de dominio de hello en conjunto de nube nuevo servicio y la disponibilidad de Hola.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    Estos comandos canalizados Hola siguientes cosas:

   * **New-AzureVMConfig** crea una configuración de máquina virtual.
   * **Agregar-AzureProvisioningConfig** proporciona Hola parámetros de configuración de un servidor independiente de Windows.
   * **Agregar-AzureDataDisk** agrega Hola disco de datos que va a utilizar para almacenar los datos de Active Directory, con la opción set tooNone el almacenamiento en caché de Hola.
   * **New-AzureVM** crea un nuevo servicio de nube y crea Hola nueva máquina virtual de Azure Hola nuevo servicio en nube.

7. Espere Hola nueva VM toobe aprovisionado por completo y descargar el directorio de trabajo de tooyour Hola archivo de escritorio remoto. Hola como hello nueva máquina virtual de Azure tiene un tooprovision mucho tiempo, `while` bucle continúa toopoll Hola nueva máquina virtual hasta que estén listo para su uso.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

servidor de controlador de dominio de Hello ahora se aprovisionó correctamente. A continuación, configurará el dominio de Active Directory de hello en este servidor de controlador de dominio. Vulnerable la ventana de PowerShell de hello en el equipo local. Se usará nuevo toocreate posterior Hola dos VM de SQL Server.

## <a name="configure-hello-domain-controller"></a>Configurar el controlador de dominio de Hola
1. Conectar servidor de controlador de dominio toohello iniciando Hola archivo de escritorio remoto. Usar nombre de usuario AzureAdmin y la contraseña del administrador del equipo de hello **Contoso! 000**, que especificó cuando creó Hola nueva máquina virtual.
2. Abra una ventana de Azure PowerShell en modo de administrador.
3. Ejecute hello siguiente **DCPROMO. EXE** tooset comando seguridad hello **corp.contoso.com** dominio con directorios de datos de hello en la unidad M.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Cuando finaliza el comando de hello, Hola VM se reinicia automáticamente.

4. Conéctese de nuevo servidor de controlador de dominio toohello iniciando Hola archivo de escritorio remoto. Esta vez, inicie sesión como **CORP\Administrador**.
5. Abra una ventana de PowerShell en modo de administrador e importe el módulo de Active Directory PowerShell de hello mediante el uso de hello siguiente comando:

        Import-Module ActiveDirectory

6. Siguiente ejecución Hola comandos tooadd tres usuarios toohello dominio.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** es tooconfigure usado todo lo relacionado con toohello instancias de servicio de SQL Server, el clúster de conmutación por error de Hola y el grupo de disponibilidad de Hola. **CORP\SQLSvc1** y **CORP\SQLSvc2** se usan como cuentas de servicio de SQL Server de Hola para hello dos VM de SQL Server.
7. Siguiente Hola de continuación, ejecute comandos toogive **CORP\Install** Hola objetos de equipo de toocreate de permisos en el dominio de Hola.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    Hola GUID especificado anteriormente es hello GUID para el tipo de objeto de equipo de Hola. Hola **CORP\Install** cuenta necesita hello **leer todas las propiedades** y **crear objetos de equipo** Hola de permiso toocreate Active directo de objetos para la conmutación por error de Hola clúster. Hola **leer todas las propiedades** permiso ya se proporciona tooCORP\Install de forma predeterminada, por lo que no es necesario toogrant lo explícitamente. Para obtener más información sobre los permisos que necesita el clúster de conmutación por error de hello toocreate, consulte [guía paso a paso de clúster de conmutación por error: configurar cuentas en Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).

    Ahora que has terminado de configurar Active Directory y objetos de usuario de hello, creará dos VM de SQL Server y combinarlos toothis dominio.

## <a name="create-hello-sql-server-vms"></a>Crear máquinas virtuales de hello SQL Server
1. Continuar la ventana de PowerShell de hello toouse que está abierto en el equipo local. Definir Hola siguientes variables adicionales:

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    Hola dirección IP **10.10.0.4** normalmente se asigna a toohello primera máquina virtual que cree en hello **10.10.0.0/16** las subredes de la red virtual de Azure. Debe comprobar que se trata Hola dirección de su servidor de controlador de dominio mediante la ejecución de **IPCONFIG**.
2. Hola ejecución sigue Hola de comandos canalizados toocreate primero máquina virtual en clúster de conmutación por error de hello, denominado **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    Tenga en cuenta los siguientes de hello sobre Hola comando anterior:

   * **New-AzureVMConfig** crea una configuración de máquina virtual con el nombre del conjunto de disponibilidad deseado Hola. Hello VM siguientes se creará con hello mismo nombre de conjunto de disponibilidad para que se está unido toohello mismo conjunto de disponibilidad.
   * **Agregar-AzureProvisioningConfig** combinaciones Hola dominio de Active Directory de toohello de máquina virtual que ha creado.
   * **Conjunto AzureSubnet** lugares Hola a máquina virtual en la subred back-end de Hola.
   * **New-AzureVM** crea un nuevo servicio de nube y crea Hola nueva máquina virtual de Azure Hola nuevo servicio en nube. Hola **DnsSettings** parámetro especifica el servidor DNS Hola para servidores de servicio de nube nuevo Hola hello tiene dirección IP de hello **10.10.0.4**. Se trata de dirección IP de Hola de servidor de controlador de dominio de Hola. Este parámetro es necesario tooenable Hola nuevas máquinas virtuales en el dominio de Active Directory de toohello toojoin del servicio de la nube Hola correctamente. Sin este parámetro, debe establecer manualmente una configuración de IPv4 hello en el servidor de controlador de dominio de máquina virtual toouse hello como servidor DNS principal de hello cuando Hola VM esté aprovisionado y, a continuación, unir el dominio de Active Directory de hello VM toohello.
3. Hola ejecución sigue canalizada comandos toocreate hello las máquinas virtuales de SQL Server, denominado **ContosoSQL1** y **ContosoSQL2**.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    Tenga en cuenta los siguientes de hello con respecto a los comandos de hello anteriores:

   * **New-AzureVMConfig** usa Hola el mismo nombre de conjunto de disponibilidad como servidor de controlador de dominio de Hola y utiliza Hola imagen de SQL Server 2012 Service Pack 1 Enterprise Edition en la Galería de máquinas virtuales de Hola. También establece Hola operativo sistema tooread caché de disco sólo (sin caching de escritura). Se recomienda que migre Hola base de datos archivos tooa disco de datos independiente que adjuntar toohello máquina virtual y configurarlo con ninguna lectura o la caché de escritura. Sin embargo, lo mejor de hello siguiente es tooremove la caché de escritura en disco del sistema operativo Hola porque no se puede quitar lee almacenamiento en caché en el disco del sistema operativo de Hola.
   * **Agregar-AzureProvisioningConfig** combinaciones Hola dominio de Active Directory de toohello de máquina virtual que ha creado.
   * **Conjunto AzureSubnet** lugares Hola a máquina virtual en la subred back-end de Hola.
   * **Agregar-AzureEndpoint** agrega extremos de acceso para que las aplicaciones cliente pueden tener acceso a estas instancias de servicios de SQL Server en hello Internet. Se proporcionan puertos diferentes tooContosoSQL1 y ContosoSQL2.
   * **New-AzureVM** crea Hola nueva VM de SQL Server en hello mismo servicio en la nube como ContosoQuorum. Debe colocar las máquinas virtuales de hello en hello mismo servicio en la nube si desea toobe en Hola el mismo conjunto de disponibilidad.
4. Espere cada toobe VM aprovisionado por completo y para cada toodownload VM su directorio de trabajo de tooyour de archivo de escritorio remoto. Hola `for` bucle recorre Hola tres nuevas VM y ejecuta comandos Hola dentro de llaves de nivel superior de Hola para cada uno de ellos.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    Hola VM de SQL Server están aprovisionadas y en ejecución, pero está instalado con SQL Server con las opciones predeterminadas.

## <a name="initialize-hello-failover-cluster-vms"></a>Inicializar el clúster de conmutación por error de hello las máquinas virtuales
En esta sección, deberá toomodify Hola tres servidores que va a utilizar en la instalación de SQL Server de Hola y clúster de conmutación por error de Hola. Concretamente:

* Todos los servidores: necesita hello tooinstall **agrupación en clústeres de conmutación por error** característica.
* Todos los servidores: necesita tooadd **CORP\Install** como máquina de hello **administrador**.
* ContosoSQL1 y ContosoSQL2 únicamente: necesita tooadd **CORP\Install** como un **sysadmin** rol de base de datos de hello predeterminada.
* ContosoSQL1 y ContosoSQL2 únicamente: necesita tooadd **NT AUTHORITY\System** como un inicio de sesión de con hello los siguientes permisos:

  * Modificar cualquier grupo de disponibilidad
  * Conectar SQL
  * Ver estado del servidor
* ContosoSQL1 y ContosoSQL2 únicamente: Hola **TCP** protocolo ya está habilitado en hello VM de SQL Server. Sin embargo, todavía necesita tooopen firewall de hello para el acceso remoto de SQL Server.

Ahora, está listo toostart. A partir de **ContosoQuorum**, siga estos pasos hello:

1. Conectar demasiado**ContosoQuorum** iniciando Hola archivos de escritorio remoto. Usar nombre de usuario del administrador del equipo de hello **AzureAdmin** y la contraseña **Contoso! 000**, que se especificó cuando creó hello las máquinas virtuales.
2. Compruebe que los equipos de Hola se han unido correctamente demasiado**corp.contoso.com**.
3. Espere a que toofinish de instalación de SQL Server de hello ejecutar tareas de inicialización de hello automatizada antes de continuar.
4. Abra una ventana de Azure PowerShell en modo de administrador.
5. Instale la característica de agrupación en clústeres de conmutación por error de Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Agregue **CORP\Install** como administrador local.

        net localgroup administrators "CORP\Install" /Add
7. Cierre sesión en ContosoQuorum. Ya está listo con este servidor.

        logoff.exe

A continuación, inicialice **ContosoSQL1** y **ContosoSQL2**. Siga los pasos de hello siguientes, que son idénticos para ambos VM de SQL Server.

1. Conéctese toohello dos VM de SQL Server iniciando los archivos de escritorio remoto de Hola. Usar nombre de usuario del administrador del equipo de hello **AzureAdmin** y la contraseña **Contoso! 000**, que se especificó cuando creó hello las máquinas virtuales.
2. Compruebe que los equipos de Hola se han unido correctamente demasiado**corp.contoso.com**.
3. Espere a que toofinish de instalación de SQL Server de hello ejecutar tareas de inicialización de hello automatizada antes de continuar.
4. Abra una ventana de Azure PowerShell en modo de administrador.
5. Instale la característica de agrupación en clústeres de conmutación por error de Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Agregue **CORP\Install** como administrador local.

        net localgroup administrators "CORP\Install" /Add
7. Importar Hola proveedor de PowerShell de SQL Server.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. Agregar **CORP\Install** como sysadmin de hello para la instancia de SQL Server de hello predeterminada.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. Agregar **NT AUTHORITY\System** como un inicio de sesión de con permisos de hello tres se ha descrito anteriormente.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. Abra firewall de hello para el acceso remoto de SQL Server.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. Cierre sesión en ambas máquinas virtuales.

         logoff.exe

Por último, está listo tooconfigure grupo de disponibilidad de Hola. Deberá usar tooperform de SQL Server PowerShell Provider Hola todos Hola funcionan de **ContosoSQL1**.

## <a name="configure-hello-availability-group"></a>Configurar grupo de disponibilidad de Hola
1. Conectar demasiado**ContosoSQL1** nuevo iniciando los archivos de escritorio remoto de Hola. En lugar de iniciar sesión mediante el uso de la cuenta de equipo de hello, inicie sesión con **CORP\Install**.
2. Abra una ventana de Azure PowerShell en modo de administrador.
3. Definir Hola siguientes variables:

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. Importar Hola proveedor de PowerShell de SQL Server.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. Cambiar la cuenta de servicio de SQL Server de Hola para ContosoSQL1 tooCORP\SQLSvc1.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. Cambiar la cuenta de servicio de SQL Server de Hola para ContosoSQL2 tooCORP\SQLSvc2.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. Descargar **CreateAzureFailoverCluster.ps1** de [crear el clúster de conmutación por error para grupos de disponibilidad AlwaysOn en Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello directorio de trabajo local. Usará este toohelp de secuencia de comandos crea un clúster de conmutación por error funcional. Para obtener información importante sobre cómo interactúa la agrupación en clústeres de conmutación por error de Windows con hello Azure de red, consulte [alta disponibilidad y recuperación ante desastres para SQL Server en máquinas virtuales Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).
8. Cambie el directorio de trabajo tooyour y creación de clúster de conmutación por error de hello con script de Hola descargado.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Habilitar grupos de disponibilidad AlwaysOn para las instancias de SQL Server predeterminadas de hello en **ContosoSQL1** y **ContosoSQL2**.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. Cree un directorio de copia de seguridad y conceder permisos para las cuentas de servicio de SQL Server de Hola. Usará esta base de datos de disponibilidad de directorio tooprepare hello en la réplica secundaria de Hola.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. Crear una base de datos en **ContosoSQL1** llama **MyDB1**, realice una copia de seguridad completa y una copia de seguridad de registros y restáurelas en **ContosoSQL2** con hello **WITH NORECOVERY** opción.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Cree extremos del grupo de disponibilidad de hello en hello VM de SQL Server y establezca los permisos apropiados de hello en los puntos de conexión de Hola.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Crear réplicas de disponibilidad, Hola.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. Finalmente, cree el grupo de disponibilidad de Hola y grupo de disponibilidad de toohello de combinación Hola réplica secundaria.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>Pasos siguientes
Ha implementado correctamente SQL Server AlwaysOn mediante la creación de un grupo de disponibilidad en Azure. tooconfigure un agente de escucha para este grupo de disponibilidad, consulte [configurar un agente de escucha ILB para grupos de disponibilidad AlwaysOn en Azure](../classic/ps-sql-int-listener.md).

Para más información sobre el uso de SQL Server en Azure, consulte [SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
