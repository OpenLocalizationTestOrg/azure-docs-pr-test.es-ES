---
title: "aaaRun runbooks en Hybrid Runbook Worker de automatización de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información acerca de cómo ejecutar runbooks en equipos de su centro de datos local o el proveedor de nube con el rol de hello Hybrid Runbook Worker."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Ejecución de runbooks en Hybrid Runbook Worker 
No hay ninguna diferencia en la estructura de Hola de runbooks que se ejecutan en automatización de Azure y los que se ejecutan en un Runbook Worker híbrido. Runbooks que se utilizan con cada uno de ellos más probable es que difieren de forma significativa aunque runbooks que se dirige a un Runbook Worker híbrido normalmente administran recursos en el mismo equipo local de Hola o con recursos en entorno local de Hola donde se implementa, mientras runbooks en la automatización de Azure suelen administrar recursos de nube de Azure Hola.

Puede editar un runbook para Hybrid Runbook Worker de automatización de Azure, pero puede tener dificultades si intentas tootest Hola runbook en el editor de Hola.  módulos de PowerShell de Hola que tienen acceso a recursos locales de hello podrán no esté instalados en su entorno de automatización de Azure en cuyo caso, no podrá prueba Hola.  Si instala Hola necesario módulos, a continuación, Hola runbook se ejecutará, pero no será capaz de tooaccess recursos locales para una prueba completa.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>Inicio de un runbook en Hybrid Runbook Worker
[Inicio de un runbook en Automatización de Azure](automation-starting-a-runbook.md) describe los distintos métodos para iniciar un runbook.  Hybrid Runbook Worker agrega un **RunOn** opción donde puede especificar el nombre de Hola de un grupo de Hybrid Runbook Worker.  Si se especifica un grupo, a continuación, Hola runbook recuperan y ejecutar de trabajadores de hello en ese grupo.  Si no se especifica esta opción, se ejecuta en Automatización de Azure de la manera normal.

Cuando se inicia un runbook en hello portal de Azure, se le presentará una **ejecutar en** opción donde puede seleccionar **Azure** o **Hybrid Worker**.  Si selecciona **Hybrid Worker**, después, puede seleccionar el grupo de hello en una lista desplegable.

Hola de uso **RunOn** parámetro.  Puede usar Hola después comando toostart un runbook denominado Test-Runbook en un grupo de Hybrid Runbook Worker denominado MyHybridGroup mediante Windows PowerShell.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Hola **RunOn** parámetro agregó toohello **Start-AzureAutomationRunbook** cmdlet en la versión 0.9.1 de Microsoft Azure PowerShell.  Debería [descargar la versión más reciente de hello](https://azure.microsoft.com/downloads/) si tienes una anterior instalada.  Solo necesita tooinstall esta versión en una estación de trabajo donde está iniciando runbook Hola desde Windows PowerShell.  No es necesario tooinstall en el equipo de trabajo de Hola a menos que piense toostart runbooks desde ese equipo.  Actualmente no se puede iniciar un runbook en un Hybrid Runbook Worker desde otro runbook, ya que esto requeriría la versión más reciente de Hola de toobe de Powershell de Azure instalado en su cuenta de automatización.  versión más reciente de Hola se actualizan automáticamente en automatización de Azure y automáticamente trasladará trabajadores toohello pronto.
>
>

## <a name="runbook-permissions"></a>Permisos de runbooks
Runbooks que se ejecutan en un Runbook Worker híbrido no puede usar Hola mismo método que se utiliza normalmente para runbooks autenticar tooAzure recursos, ya que obtiene acceso a recursos fuera de Azure.  Hola runbook puede proporcionar su propia autenticación toolocal recursos, o bien puede especificar un tooprovide de cuenta de RunAs un contexto de usuario para todos los runbooks.

### <a name="runbook-authentication"></a>Autenticación de runbook
De forma predeterminada, los runbooks se ejecutarán en el contexto de saludo de la cuenta de sistema local de hello en el equipo local de hello, por lo que deben proporcionar sus propios tooresources de autenticación que tendrá acceso.  

Puede usar [credencial](http://msdn.microsoft.com/library/dn940015.aspx) y [certificado](http://msdn.microsoft.com/library/dn940013.aspx) activos en su runbook con los cmdlets que le permiten toospecify credenciales para poder autenticar a los recursos de toodifferent.  Hello en el ejemplo siguiente se muestra una parte de un runbook que se reinicia un equipo.  Recupera las credenciales de un nombre de credencial hello y activos del equipo de Hola desde un recurso de variable y, a continuación, usa estos valores con el cmdlet de hello Restart-Computer.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

También puede aprovechar la [InlineScript](automation-powershell-workflow.md#inlinescript), que le permite toorun bloques de código en otro equipo con las credenciales especificadas por hello [parámetro común de PSCredential](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>Cuenta RunAs
En lugar de tener runbooks proporcionar su propia autenticación toolocal recursos, puede especificar un **RunAs** cuenta para un grupo de Hybrid worker.  Especifica un [activo de credencial](automation-credentials.md) que tiene acceso a los recursos de toolocal y todos los runbooks se ejecutan en estas credenciales cuando se ejecuta en un Hybrid Runbook Worker en grupo de Hola.  

nombre de usuario de Hello para la credencial de hello debe estar en uno de hello siguientes formatos:

* dominio\nombre de usuario
* username@domain
* nombre de usuario (por equipo de cuentas local toohello local)

Usar hello siguiendo el procedimiento toospecify una cuenta de ejecución para un grupo de Hybrid worker:

1. Crear un [activo de credencial](automation-credentials.md) con acceso a los recursos de toolocal.
2. Abrir cuenta de automatización de Hola Hola portal de Azure.
3. Seleccione hello **grupos de trabajo híbrido** icono y, a continuación, seleccione el grupo de Hola.
4. Seleccione **Toda la configuración** y luego **Configuración del grupo de Hybrid Worker**.
5. Cambio **ejecución** de **predeterminado** demasiado**personalizado**.
6. Seleccione la credencial de Hola y haga clic en **guardar**.

### <a name="automation-run-as-account"></a>Cuenta de ejecución de Automation
Como parte del proceso automatizado de compilación para implementar recursos en Azure, puede requerir acceso local tooon sistemas toosupport una tarea o un conjunto de pasos en la secuencia de implementación.  autenticación de toosupport con Azure con la cuenta de identificación de hello, debe tooinstall Hola ejecutar como certificado de cuenta.  

Hola siguiente runbook de PowerShell, *RunAsCertificateToHybridWorker de exportación*, exporta Hola ejecutar como certificado de la cuenta de automatización de Azure y descarga y lo importa en el almacén de certificados del equipo local de hello en un Worker híbrido conectado toohello misma cuenta.  Una vez completado este paso, comprueba trabajo Hola puede autenticar correctamente tooAzure con hello cuenta de ejecución.

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

Guardar hello *exportación RunAsCertificateToHybridWorker* runbook tooyour equipo con un `.ps1` extensión.  Importar a la cuenta de automatización y editar runbook hello, cambiar valor Hola de variable de hello `$Password` con su propia contraseña.  Publicar y, a continuación, ejecutar runbook Hola grupo Hybrid Worker de Hola que se ejecutan y autenticar runbooks mediante Hola cuenta de ejecución de destino.  Hola trabajo flujo informes Hola intento tooimport Hola certificado en el almacén del equipo local de Hola y sigue con varias líneas, dependiendo de cuántas de las cuentas de automatización se definen en la suscripción y si la autenticación es correcta.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Solución de problemas de runbooks en Hybrid Runbook Worker
Los registros se almacenan localmente en cada Hybrid Worker en C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Worker híbrido también registra los errores y eventos en el registro de eventos de Windows hello en **aplicaciones y servicios Logs\Microsoft-SMA\Operational**.  Eventos relacionados con toorunbooks que se ejecuta en el trabajo de Hola se escriben demasiado**aplicaciones y servicios Logs\Microsoft-Automation\Operational**.  Hola **Microsoft SMA** registro incluye muchos más eventos relacionados toohello runbook toohello insertado hello y trabajo procesamiento de trabajos de runbook de Hola.  Mientras hello **automatización de Microsoft** registro de eventos no tiene muchos eventos con detalles a prestar asistencia con hello solución de problemas de ejecución de un runbook, al menos, encontrará resultados Hola de trabajo de runbook de Hola.  

[Runbook de salida y mensajes](automation-runbook-output-and-messages.md) se envían tooAzure automatización de hybrid Worker simplemente como trabajos de runbook en la nube Hola.  También puede habilitar Hola detallado y Hola secuencias de progreso de la misma manera que lo haría para otros runbooks.  

Si no se completan correctamente los runbooks y resumen de trabajos de hello muestra un estado de **Suspended**, revise el artículo de solución de problemas de hello [Hybrid Runbook Worker: un trabajo de runbook finaliza con el estado Suspende](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de métodos diferentes de Hola que pueden ser utilizado toostart un runbook, consulte [a partir de un Runbook en automatización de Azure](automation-starting-a-runbook.md).  
* toounderstand Hola diferentes procedimientos para trabajar con runbooks de flujo de trabajo de PowerShell y PowerShell en automatización de Azure mediante el editor de texto hello, vea [editar un Runbook en automatización de Azure](automation-edit-textual-runbook.md)
