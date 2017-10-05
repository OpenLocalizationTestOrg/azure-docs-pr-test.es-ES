---
title: "Recursos de conexión en Azure Automation | Microsoft Docs"
description: "Los activos de conexión en Automatización de Azure contienen la información necesaria para conectarse a una aplicación o a un servicio externo desde un runbook o una configuración de DSC. En este artículo se explican los detalles de las conexiones y cómo trabajar con ellas en la creación de texto y de gráficos."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: 3cf85651332c85ddf7ef26c21619b5e3a0b89b79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connection-assets-in-azure-automation"></a>Recursos de conexión en Automatización de Azure

Un recurso de conexión de Automatización contiene la información necesaria para conectarse a una aplicación o a un servicio externos desde un runbook o una configuración de DSC. Esto puede incluir información solicitada para la autenticación, como un nombre de usuario y una contraseña, además de información de conexión, como una dirección URL o un puerto. El valor de una conexión es mantener todas las propiedades para conectarse a una aplicación determinada en un recurso, a diferencia de crear distintas variables. El usuario puede editar los valores de una conexión en un lugar y es posible pasar el nombre de una conexión a un runbook o una configuración de DSC en un solo parámetro. Es posible tener acceso a las propiedades de una conexión en el runbook o la configuración de DSC con la actividad **Get-AutomationConnection** .

Cuando crea una conexión, debe especificar un *tipo de conexión*. El tipo de conexión es una plantilla que define un conjunto de propiedades. La conexión define valores para cada propiedad definida en su tipo de conexión. Los tipos de conexión se agregan a Azure Automation en módulos de integración o se crean con la [API de Azure Automation](http://msdn.microsoft.com/library/azure/mt163818.aspx) si el módulo de integración incluye un tipo de conexión y se importa en su cuenta de Automation. En caso contrario, debe crear un archivo de metadatos para especificar un tipo de conexión de Automation.  Para obtener más información sobre esto, consulte [Módulos de integración](automation-integration-modules.md).  

>[!NOTE] 
>Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas. Estos recursos se cifran y se almacenan en Automatización de Azure con una clave única que se genera para cada cuenta de automatización. Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure. Antes de almacenar un recurso seguro, la clave de la cuenta de automatización se descifra con el certificado maestro y, a continuación, se utiliza para cifrar el recurso.

## <a name="windows-powershell-cmdlets"></a>Cmdlets de Windows PowerShell

Los cmdlets de la tabla siguiente se usan para crear y administrar conexiones de Automatización con Windows PowerShell. Se incluyen como parte del [módulo Azure PowerShell](/powershell/azure/overview) que está disponible para su uso en las configuraciones de DSC y los runbooks de Automatización.

|Cmdlet|Descripción|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Recupera una conexión. Incluye una tabla hash con los valores de los campos de la conexión.|
|[New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Crea una conexión nueva.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Quita una conexión existente.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Establece el valor de un campo determinado para una conexión existente.|

## <a name="activities"></a>Actividades

Las actividades de la siguiente tabla se usan para tener acceso a las conexiones de un runbook o de una configuración de DSC.

|Actividades|Descripción|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Obtiene una conexión para usar. Devuelve una tabla hash con las propiedades de la conexión.|

>[!NOTE] 
>Debe evitar el uso de variables con el parámetro –Name de **Get- AutomationConnection**, debido a que esto podría complicar la detección de dependencias entre runbooks o configuraciones de DSC y activos de conexión en tiempo de diseño.

## <a name="creating-a-new-connection"></a>Creación de una conexión nueva

### <a name="to-create-a-new-connection-with-the-azure-portal"></a>Para crear una conexión nueva con el Portal de Azure

1. En la cuenta de automatización, haga clic en la parte **Recursos** para abrir la hoja **Recursos**.
2. Haga clic en la parte **Conexiones** para abrir la hoja **Conexiones**.
3. Haga clic en **Agregar una conexión** en la parte superior de la hoja.
4. En el menú desplegable **Tipo** , seleccione el tipo de conexión que desea crear. El formulario presentará las propiedades de ese tipo determinado.
5. Complete el formulario y haga clic en **Crear** para guardar la conexión nueva.

### <a name="to-create-a-new-connection-with-the-azure-classic-portal"></a>Para crear una conexión nueva con el Portal de Azure clásico

1. En la cuenta de Automatización, haga clic en **Recursos** en la parte superior de la ventana.
2. En la parte inferior de la ventana, haga clic en **Agregar configuración**.
3. Haga clic en **Agregar conexión**.
4. En el menú desplegable **Tipo de conexión** , seleccione el tipo de conexión que desea crear.  El asistente presentará las propiedades de ese tipo específico.
5. Realice los pasos del asistente y haga clic en la casilla para guardar la nueva conexión.

### <a name="to-create-a-new-connection-with-windows-powershell"></a>Para crear una conexión nueva con Windows PowerShell

Cree una conexión nueva con Windows PowerShell con el cmdlet [New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection). Este cmdlet tiene un parámetro denominado **ConnectionFieldValues** que espera una [tabla hash](http://technet.microsoft.com/library/hh847780.aspx) que define los valores de cada una de las propiedades definidas por el tipo de conexión.

Si está familiarizado con la [cuenta de ejecución](automation-sec-configure-azure-runas-account.md) de Automation para autenticar runbooks con la entidad de servicio, el script de PowerShell, que se ofrece como alternativa a la creación de la cuenta de ejecución desde el portal, crea un nuevo recurso de conexión mediante los siguientes comandos de ejemplo.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Puede usar el script para crear el recurso de conexión porque cuando se crea la cuenta de Automation, este incluye automáticamente varios módulos globales de manera predeterminada junto con el tipo de conexión **AzurServicePrincipal** para crear el recurso de conexión **AzureRunAsConnection**.  Es importante tener esto cuenta, porque si intenta crear un nuevo recurso de conexión para conectarse a un servicio o aplicación con un método de autenticación diferente, se producirá un error porque el tipo de conexión no se ha definido todavía en su cuenta de Automation.  Para obtener más información sobre cómo crear su propio tipo de conexión para su módulo o instancia personalizada desde la [Galería de PowerShell](https://www.powershellgallery.com), consulte [Módulos de integración](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Uso de una conexión en un runbook o una configuración de DSC

Puede recuperar una conexión de un runbook o una configuración de DSC con el cmdlet **Get-AutomationConnection** .  No se puede utilizar la actividad [Get-AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn).  Esta actividad recupera los valores de los distintos campos en la conexión y los devuelve como una [tabla hash](http://go.microsoft.com/fwlink/?LinkID=324844) que luego se puede usar con los comandos adecuados en el runbook o la configuración de DSC.

### <a name="textual-runbook-sample"></a>Ejemplo de runbook de texto

Los siguientes comandos de ejemplo muestran cómo utilizar la cuenta de ejecución mencionada anteriormente para autenticar con recursos de Azure Resource Manager en su runbook.  Esta utiliza el recurso de conexión que representa la cuenta de ejecución, que hace referencia a la entidad de servicio basada en certificados, no a las credenciales.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Ejemplos de runbook gráfico

Para agregar una actividad **Get-AutomationConnection** a un runbook gráfico, haga clic con el botón derecho en la conexión en el panel Biblioteca del editor gráfico y, después, seleccione **Agregar a lienzo**.

![](media/automation-connections/connection-add-canvas.png)

La imagen siguiente muestra un ejemplo de cómo usar una conexión en un runbook gráfico.  Este es el mismo ejemplo expuesto anteriormente para autenticar con la cuenta de ejecución con un runbook textual.  Este ejemplo utiliza el conjunto de datos **Valor constante** para la actividad **Get RunAs Connection** que usa un objeto de conexión para la autenticación.  Aquí se usa un [vínculo de canalización](automation-graphical-authoring-intro.md#links-and-workflow) , debido a que el conjunto de parámetros ServicePrincipalCertificate espera un solo objeto.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Pasos siguientes

- Revise la sección [Vínculos de Creación gráfica](automation-graphical-authoring-intro.md#links-and-workflow) para aprender a dirigir y controlar el flujo de la lógica de sus runbooks.  

- Para obtener más información sobre el uso de Azure Automation de los módulos y los procedimientos recomendados de PowerShell para crear sus propios módulos de PowerShell a fin de que funcionen como módulos de integración en Azure Automation, consulte [Módulos de integración](automation-integration-modules.md).  
