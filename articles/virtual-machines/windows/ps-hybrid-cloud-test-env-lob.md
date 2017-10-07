---
title: "entorno de prueba de aplicación aaaLOB | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate basada en web, línea de aplicaciones empresariales en un híbrido en la nube de entorno de TI pro o las pruebas de desarrollo."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Configuración de una aplicación de LOB basada en web en una nube híbrida para pruebas
En este tema se le guiará en el proceso de creación de un entorno de nube híbrida simulada para probar una aplicación de línea de negocio (LOB) basada en web hospedada en Microsoft Azure. Esta es la configuración resultante de Hola.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Esta configuración consta de:

* Una red de simulada en entornos hospedada en Azure (Hola TestLab VNet).
* Una red virtual entre locales hospedada en Azure (TestVNET).
* Una conexión VPN de red virtual a red virtual.
* Un servidor LOB basado en web, SQL server y el controlador de dominio secundario en la red virtual de hello TestVNET.

Esta configuración proporciona una base y un punto de partida común desde el que puede:

* Desarrollar y probar aplicaciones de LOB hospedadas en Internet Information Services (IIS) con un back-end de base de datos de SQL Server 2014 en Azure.
* Realizar pruebas de esta carga de trabajo de TI basada en la nube híbrida simulada.

Hay tres toosetting fases principales en este entorno de prueba de nube híbrida:

1. Configurar el entorno de nube híbrida simulada Hola.
2. Configurar el equipo con hello SQL server (SQL1).
3. Configurar servidor LOB de hello (LOB1).

Esta carga de trabajo requiere una suscripción de Azure. Si tiene una suscripción de MSDN o de Visual Studio, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Para obtener un ejemplo de una aplicación LOB hospedada en Azure de producción, vea hello **línea de aplicaciones empresariales** plano técnico de arquitectura en [diagramas de arquitectura de Software de Microsoft y planos](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>Fase 1: Configurar el entorno de nube híbrida simulada Hola
Crear hello [entorno de prueba de nube híbrida simulada](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Dado que este entorno de prueba no requiere la presencia de Hola de servidor hello APP1 en la subred Corpnet de hello, puede cerrarlo por ahora.

Se trata de la configuración actual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>Fase 2: Configurar el equipo con hello SQL server (SQL1)
Empezar desde Hola portal de Azure, equipo de DC2 Hola si es necesario.

Después, cree una máquina virtual para SQL1 con estos comandos en un símbolo del sistema de Azure PowerShell en el equipo local. Toorunning anterior estos comandos, rellene Hola valores de las variables y quitar Hola < y > caracteres.

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Usar hello Azure tooconnect portal tooSQL1 con cuenta de administrador local de Hola de SQL1.

A continuación, configure la conectividad básica pruebas de tooallow de reglas de Firewall de Windows y el tráfico de SQL Server. Desde un símbolo del sistema de Windows PowerShell con nivel de administrador en SQL1, ejecute estos comandos.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

comando ping de Hello debe producir cuatro respuestas correcta de la dirección IP 192.168.0.4.

A continuación, agregue Hola disco de datos adicionales en SQL1 como un volumen nuevo con una letra de unidad de hello F:.

1. En el panel izquierdo del administrador del servidor de hello, haga clic en **File and Storage Services**y, a continuación, haga clic en **discos**.
2. En panel de contenido de hello, Hola **discos** grupo, haga clic en **disco 2** (con hello **partición** establecido demasiado**desconocido**).
3. Haga clic en **Tareas** y luego haga clic en **Nuevo volumen**.
4. En hello antes de comenzar la página del Asistente para nuevo volumen hello, haga clic en **siguiente**.
5. En el servidor seleccione Hola de Hola y página de disco, haga clic en **disco 2**y, a continuación, haga clic en **siguiente**. Cuando se le solicite, haga clic en **Aceptar**.
6. En especificar el tamaño de Hola de página de volumen de Hola Hola, haga clic en **siguiente**.
7. En hello asignar tooa unidad carpeta o letra de página, haga clic en **siguiente**.
8. En la página Configuración del sistema seleccione archivo hello, haga clic en **siguiente**.
9. En la página Confirmar selecciones de hello, haga clic en **crear**.
10. Cuando haya terminado, haga clic en **Cerrar**.

Ejecute estos comandos en línea de comandos de Windows PowerShell de hello en SQL1:

    md f:\Data
    md f:\Log
    md f:\Backup

A continuación, unirse a dominio de CORP Windows Server Active Directory de toohello SQL1 con estos comandos en el símbolo del sistema de Windows PowerShell de hello en SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Usar cuenta de hello CORP\User1 cuando se le solicite credenciales de cuenta de dominio toosupply de hello **Add-Computer** comando.

Después de reiniciar, use hello Azure tooconnect portal tooSQL1 *con la cuenta de administrador local de Hola de SQL1*.

A continuación, configure SQL Server 2014 toouse Hola la unidad F: para nuevas bases de datos y de los permisos de cuenta de usuario.

1. En la pantalla de inicio de bienvenida, escriba **administración de SQL Server**y, a continuación, haga clic en **SQL Server 2014 Management Studio**.
2. En **conectar tooServer**, haga clic en **conectar**.
3. En el panel de árbol del explorador de objetos de hello, haga clic en **SQL1**y, a continuación, haga clic en **propiedades**.
4. Hola **propiedades del servidor** ventana, haga clic en **configuración de base de datos**.
5. Busque hello **ubicaciones predeterminadas de la base de datos** y establecer estos valores: 
   * Para **datos**, ruta de acceso del tipo hello **f:\Data**.
   * Para **registro**, ruta de acceso del tipo hello **f:\Log**.
   * Para **copia de seguridad**, ruta de acceso del tipo hello **f:\Backup**.
   * Nota: Solo las bases de datos nuevas utilizan estas ubicaciones.
6. Haga clic en hello **Aceptar** ventana de hello tooclose.
7. Hola **Explorador de objetos** panel del árbol, abra **seguridad**.
8. Haga clic con el botón derecho en **Inicios de sesión** y luego haga clic en **Nuevo inicio de sesión**.
9. En **Nombre de inicio de sesión**, escriba **CORP\User1**.
10. En hello **Roles de servidor** página, haga clic en **sysadmin**y, a continuación, haga clic en **Aceptar**.
11. Cierre Microsoft SQL Server Management Studio.

Se trata de la configuración actual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>Fase 3: Configurar el servidor LOB de hello (LOB1)
Primero, cree una máquina virtual para LOB1 con estos comandos en línea de comandos de PowerShell de Azure de hello en el equipo local.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

A continuación, use hello Azure tooconnect portal tooLOB1 con credenciales de Hola de cuenta de administrador local de Hola de LOB1.

A continuación, configure un tráfico de tooallow de regla de Firewall de Windows para probar la conectividad básica. Desde un símbolo del sistema de Windows PowerShell con nivel de administrador en LOB1, ejecute estos comandos.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

comando ping de Hello debe producir cuatro respuestas correcta de la dirección IP 192.168.0.4.

A continuación, unirse a dominio de Active Directory de CORP toohello de LOB1 con estos comandos en el símbolo del sistema de hello Windows PowerShell.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Usar cuenta de hello CORP\User1 cuando se le solicite credenciales de cuenta de dominio toosupply de hello **Add-Computer** comando.

Después de reiniciar, use hello Azure tooconnect portal tooLOB1 con hello CORP\User1 cuentas y contraseñas.

A continuación, configure LOB1 para IIS y pruebe el acceso desde CLIENT1.

1. En Administrador del servidor, haga clic en **Agregar roles y características**.
2. En hello **antes de comenzar** página, haga clic en **siguiente**.
3. En hello **Seleccionar tipo de instalación** página, haga clic en **siguiente**.
4. En hello **Seleccionar servidor de destino** página, haga clic en **siguiente**.
5. En hello **roles de servidor** página, haga clic en **servidor Web (IIS)** en la lista de Hola de **Roles**.
6. Cuando se le solicite, haga clic en **Agregar características** y después en **Siguiente**.
7. En hello **seleccionar características** página, haga clic en **siguiente**.
8. En hello **servidor Web (IIS)** página, haga clic en **siguiente**.
9. En hello **seleccionar servicios de rol** , seleccione o desactive casillas de verificación de Hola para servicios de Hola que necesita para probar la aplicación de LOB y, a continuación, haga clic en **siguiente**.
10. En hello **Confirmar selecciones de instalación** página, haga clic en **instalar**.
11. Espere hasta que haya completado la instalación de Hola de componentes y, a continuación, haga clic en **cerrar**.
12. Desde Hola portal de Azure, conectar toohello CLIENT1 equipo con las credenciales de cuenta de hello CORP\User1 y, a continuación, inicie Internet Explorer.
13. En la barra de direcciones de hello, escriba **http://lob1/** y, a continuación, presione ENTRAR. Debería ver la página web de hello predeterminada IIS 8.

Se trata de la configuración actual.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Este entorno es ahora está listo para que se toodeploy su aplicación web sobre las funciones LOB1 y prueba de CLIENT1 en la subred Corpnet de Hola.

## <a name="next-step"></a>Paso siguiente
* Agregar una nueva máquina virtual con hello [portal de Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

