---
title: "aaaCertificate activos de automatización de Azure | Documentos de Microsoft"
description: "Certificados se pueden almacenar de forma segura en automatización de Azure para que se pueden obtener acceso por runbooks o tooauthenticate de configuraciones de DSC en Azure y recursos de otros fabricantes.  En este artículo se explica los detalles de Hola de certificados y cómo toowork con ellos en la creación gráfica y textual."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Activos de certificados en Automatización de Azure

Certificados pueden ser almacenados de forma segura en automatización de Azure para que se pueden obtener acceso por runbooks o configuraciones de DSC mediante hello **AzureRmAutomationRmCertificate Get** actividad para los recursos de Azure Resource Manager. Esto le permite toocreate runbooks y las configuraciones de DSC que usan certificados para la autenticación o agrega recursos tooAzure o de terceros.

> [!NOTE] 
> Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas. Estos activos se cifran y almacenan en hello automatización de Azure mediante una clave única que se genera para cada cuenta de automatización. Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure. Antes de almacenar un recurso seguro, clave de hello para la cuenta de automatización de Hola se descifra mediante certificado maestro hello y, a continuación, utilice activos de hello tooencrypt.
> 

## <a name="windows-powershell-cmdlets"></a>Cmdlets de Windows PowerShell

cmdlets de Hello en hello en la tabla siguiente son toocreate usado y administrar recursos de certificado de automatización con Windows PowerShell. Se incluyen como parte del programa Hola a [módulo Azure PowerShell](../powershell-install-configure.md) que está disponible para su uso en runbooks de automatización y las configuraciones de DSC.

|Cmdlets|Descripción|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Recupera información sobre una toouse de certificado en un runbook o la configuración de DSC. Solo puede recuperar el propio certificado Hola de actividad de Get-AutomationCertificate.|
|[New-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Crea un certificado nuevo en Azure Automation.|
[Remove-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Quita un certificado a Automatización de Azure.|Crea un certificado nuevo en Azure Automation.
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Establece las propiedades de Hola de un certificado existente, incluidas la carga de archivo de certificado de hello y establecer la contraseña para un .pfx Hola.|
|[Add-AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Cargas de un servicio de certificados para hello especifican servicio en la nube.|


## <a name="creating-a-new-certificate"></a>Creación de un certificado nuevo

Cuando se crea un nuevo certificado, cargue un archivo .cer o .pfx tooAzure automatización. Si marca certificado hello como exportable, puede transferir fuera del almacén de certificados de automatización de Azure Hola. Si no es exportable, a continuación, solo se puede utilizar para firmar dentro de runbook de Hola o configuración de DSC.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate un nuevo certificado con hello portal de Azure

1. En su cuenta de automatización, haga clic en hello **activos** icono tooopen hello **activos** hoja.
1. Haga clic en hello **certificados** icono tooopen hello **certificados** hoja.
1. Haga clic en **agregar un certificado** princip Hola de hoja de Hola.
2. Escriba un nombre para el certificado de Hola Hola **nombre** cuadro.
2. Haga clic en **seleccionar un archivo** en **cargar un archivo de certificado** toobrowse para un archivo .cer o .pfx.  Si selecciona un archivo .pfx, especifique una contraseña y si debe permitirse toobe exportado.
1. Haga clic en **crear** toosave Hola nuevo certificado activo.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate un nuevo certificado con Windows PowerShell

Hello ejemplo siguiente se muestra cómo toocreate una automatización nueva de certificados y marcarla exportable. Esta acción importa un archivo pfx ya existente.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Uso de un certificado

Debe usar hello **Get-AutomationCertificate** toouse actividad un certificado. No se puede usar hello [AzureRmAutomationCertificate Get](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet debido a que devuelve información sobre el activo de certificado de hello, pero no Hola propio certificado.

### <a name="textual-runbook-sample"></a>Ejemplo de runbook de texto

Hola siguiendo el ejemplo de código muestra cómo el servicio en un runbook de la nube de tooadd un tooa de certificado. En este ejemplo, contraseña de Hola se recupera de una variable de automatización cifrada.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Ejemplo de runbook gráfico

Agrega un **Get-AutomationCertificate** tooa un runbook gráfico con el botón secundario en hello en el certificado Hola biblioteca panel del editor gráfico de Hola y seleccionando **agregar toocanvas**.

![Agregar certificado toohello lienzo](media/automation-certificates/automation-certificate-add-to-canvas.png)

Hello siguiente imagen muestra un ejemplo del uso de un certificado en un runbook gráfico.  Se trata de hello mismo ejemplo expuesto anteriormente para agregar un servicio de nube de tooa de certificado desde un runbook textual.

![Creación gráfica de ejemplo ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Pasos siguientes

- toolearn más sobre cómo trabajar con un flujo lógico Hola de vínculos toocontrol de actividades del runbook está diseñado tooperform, consulte [vínculos de edición gráfica](automation-graphical-authoring-intro.md#links-and-workflow). 
