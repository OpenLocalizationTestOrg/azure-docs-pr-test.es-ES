---
title: "Active Directory Domain Services: guía de administración | Microsoft Docs"
description: "Unir un máquina virtual tooa administrado dominio de Windows con PowerShell de Azure y modelo de implementación clásica de Hola."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>Unirse a un máquina virtual tooa administrado dominio de Windows Server con PowerShell
> [!div class="op_single_selector"]
> * [Portal de Azure clásico - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación clásica de Hola. Servicios de dominio de Azure AD no admite actualmente el modelo del Administrador de recursos de Hola.
>
>

Estos pasos muestra cómo toocustomize un conjunto de Azure PowerShell comandos que crear y preconfigurar una máquina virtual de Azure basado en Windows mediante un enfoque de bloque de creación. Estos pasos le permiten crear una máquina virtual de Azure basado en Windows y unirse a dominio administrado de tooan servicios de dominio de AD de Azure.

En estos pasos se sigue un enfoque consistente en atar cabos para crear conjuntos de comandos de Azure PowerShell. Este enfoque puede ser útil si es nuevo tooPowerShell o desea tooknow qué toospecify valores para una configuración correcta. Los usuarios avanzados de PowerShell pueden tomar los comandos de Hola y sustituir sus propios valores para las variables de hello (líneas de hello comenzar con "$").

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

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>Paso 3: Tutorial paso a paso: aprovisionar la máquina virtual de Hola y unirse a dominio administrados toohello
Aquí es Hola correspondiente Azure PowerShell comando conjunto toocreate esta máquina virtual, con líneas en blanco entre cada bloque para mejorar la legibilidad.

Especifique la información sobre toobe de máquina virtual de Windows hello aprovisionado.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

Para los valores de InstanceSize Hola D, DS o máquinas virtuales de serie G, vea [Máquina Virtual y tamaños de servicio de nube de Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

Proporciona información sobre el dominio administrado Hola.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Especifique el nombre de hello del servicio de nube de Hola.

    $svcname="Contoso100-test"

Especificar nombre de Hola de Hola Hola de toowhich de red virtual que debe estar unida la máquina virtual. Asegúrese de que ese dominio de AAD-DS administrados Hola está disponible en esta red virtual.

    $vnetname="MyPreviewVnet"

Seleccione Hola VM imagen toobe utiliza tooprovision Hola máquina virtual.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Configurar Hola VM - nombre de la máquina virtual de conjunto, toobe & imagen de tamaño de instancia utiliza.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Obtener credenciales de administrador local para hello máquina virtual. Elija una contraseña segura de administrador local.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Obtener credenciales para una cuenta de usuario que pertenecen a toojoin VM toohello administrado dominio del grupo los administradores de controlador de dominio de too'AAD de. No especificar nombre de dominio de hello - de instancia, en nuestro ejemplo, especificamos 'bob' como nombre de usuario de Hola.

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

Configure Hola VM: especifique el requisito de unión de dominio y las credenciales necesarias.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Establecer una subred de VM de Hola.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

Opcional: La dirección IP de toohello de punto de dominio Hola. Si establece las direcciones IP Hola de Hola Hola de toobe de dominio administrados de servicios de dominio de AD de Azure servidores DNS para la red virtual de hello, este paso no es necesario.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

Ahora, Hola aprovisionar Unidos al dominio VM de Windows.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Script tooprovision una VM de Windows y automáticamente unirse a dominio administrado de los servicios de dominio de AAD de tooan
Este conjunto de comandos de PowerShell crea una máquina virtual para un servidor de línea de negocio que:

* Utiliza la imagen de Windows Server 2012 R2 Datacenter Hola.
* Es una máquina virtual extra pequeña.
* Tiene el nombre de hello Contoso100-prueba.
* Es automáticamente toohello Unidos a un dominio contoso100 el dominio administrado.
* Se agrega toohello misma red virtual que Hola administrados dominio.

Este es Hola máquina de virtual de Windows de ejemplo completo script toocreate hello y automáticamente unirse a dominio administrado de toohello servicios de dominio de AD de Azure.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>Contenido relacionado
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)](active-directory-ds-admin-guide-administer-domain.md)
