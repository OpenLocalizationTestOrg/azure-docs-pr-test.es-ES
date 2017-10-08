---
title: "configuración de cuenta de automatización de Azure aaaValidate | Documentos de Microsoft"
description: "Este artículo describe la configuración de hello tooconfirm de su cuenta de automatización está configurado correctamente."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a>Comprobación de la autenticación con la cuenta de ejecución de Azure Automation
Una vez se haya creado correctamente una cuenta de automatización, puede realizar un tooconfirm de prueba simple puede toosuccessfully autenticar en el Administrador de recursos de Azure o Azure implementación clásica usando su cuenta de automatización Run As recién creado o actualizado.    

## <a name="automation-run-as-authentication"></a>Autenticación con la cuenta de ejecución de Automation
Utilice el siguiente código de ejemplo de Hola demasiado[crear un runbook de PowerShell](automation-creating-importing-runbook.md) autenticación tooverify mediante Hola se ejecutan como cuenta de y también en su tooauthenticate runbooks personalizados y administrar los recursos del Administrador de recursos con su cuenta de automatización.   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

Observe Hola cmdlet que se usa para autenticar en runbook hello - **agregar AzureRmAccount**, usa Hola *ServicePrincipalCertificate* conjunto de parámetros.  Se autentica mediante el certificado de la entidad de servicio, no las credenciales.  

Cuando se [ejecutar runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate su cuenta de ejecución, un [trabajo del runbook](automation-runbook-execution.md) está creado, se muestra la hoja de trabajo de Hola y muestra el estado del trabajo de Hola Hola **trabajo resumen**icono. estado del trabajo Hola se iniciará como *en cola* que indica que está esperando un runbook worker en hello toobecome de nube disponible. A continuación, moverá demasiado*iniciando* cuando un trabajador notificaciones trabajo hello y, a continuación, *ejecuta* cuando se inicia realmente Hola runbook ejecuta.  Cuando se completa el trabajo de runbook de hello, deberíamos ver estado **completado**.

toosee Hola resultados detallados de hello runbook, haga clic en hello **salida** icono.  En hello **salida** hoja, debería ver se ha autenticado correctamente y devuelve una lista de todos los recursos en todos los grupos de recursos en su suscripción.  

Recuerde solo bloque de hello tooremove de código a partir de comentarios de Hola `#Get all ARM resources from all resource groups` cuando reutilizar el código de hello para sus runbooks.

## <a name="classic-run-as-authentication"></a>Autenticación con la cuenta de ejecución del modelo de implementación clásica de Azure
Utilice el siguiente código de ejemplo de Hola demasiado[crear un runbook de PowerShell](automation-creating-importing-runbook.md) tooverify autenticación mediante Hola clásico se ejecutan como cuenta de y también en su tooauthenticate runbooks personalizados y administrar recursos en el modelo de implementación clásica de Hola.  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

Cuando se [ejecutar runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate su cuenta de ejecución, un [trabajo del runbook](automation-runbook-execution.md) está creado, se muestra la hoja de trabajo de Hola y muestra el estado del trabajo de Hola Hola **trabajo resumen**icono. estado del trabajo Hola se iniciará como *en cola* que indica que está esperando un runbook worker en hello toobecome de nube disponible. A continuación, moverá demasiado*iniciando* cuando un trabajador notificaciones trabajo hello y, a continuación, *ejecuta* cuando se inicia realmente Hola runbook ejecuta.  Cuando se completa el trabajo de runbook de hello, deberíamos ver estado **completado**.

toosee Hola resultados detallados de hello runbook, haga clic en hello **salida** icono.  En hello **salida** hoja, debería ver se ha autenticado correctamente y devuelve una lista de todas las máquinas virtuales de Azure por VMName que se implementan en su suscripción.  

Recuerde tooremove Hola cmdlet **Get-AzureVM** cuando reutilizar el código de hello para sus runbooks.

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks de PowerShell, consulte [mi primer runbook de PowerShell](automation-first-runbook-textual-powershell.md).
* toolearn más información acerca de la creación de gráficos, consulte [edición gráfica en automatización de Azure](automation-graphical-authoring-intro.md).
