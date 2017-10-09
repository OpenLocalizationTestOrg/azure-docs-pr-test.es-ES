---
title: "aaaConnection activos de automatización de Azure | Documentos de Microsoft"
description: "Activos de conexión de automatización de Azure contienen Hola información necesaria tooconnect tooan externo servicio o aplicación a partir de un runbook o la configuración de DSC. En este artículo se explica los detalles de Hola de conexiones y cómo toowork con ellos en la creación gráfica y textual."
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
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Recursos de conexión en Automatización de Azure

Un recurso de conexión de automatización contiene Hola información necesaria tooconnect tooan externo servicio o aplicación a partir de un runbook o la configuración de DSC. Esto puede incluir información necesaria para la autenticación como un nombre de usuario y una contraseña en la información de tooconnection de suma, como una dirección URL o un puerto. valor de Hola de una conexión mantiene todas propiedades de hello para la conexión tooa de aplicación determinado en un recurso, como toocreating lugar varias variables. usuario de Hello puede editar valores de hello para una conexión en un solo lugar y se puede pasar el nombre de Hola de un runbook de tooa de conexión o la configuración de DSC en un solo parámetro. Hola propiedades para que se puede tener acceso a una conexión de runbook de Hola o configuración de DSC con hello **Get-AutomationConnection** actividad.

Cuando crea una conexión, debe especificar un *tipo de conexión*. tipo de conexión de Hello es una plantilla que define un conjunto de propiedades. conexión de Hello define los valores para cada propiedad definida en su tipo de conexión. Tipos de conexión se agregó tooAzure automatización en módulos de integración o creado con hello [API de automatización de Azure](http://msdn.microsoft.com/library/azure/mt163818.aspx) si el módulo de integración de hello incluye un tipo de conexión y se importa a su cuenta de automatización. En caso contrario, deberá toocreate un toospecify de archivo de metadatos un tipo de conexión de automatización.  Para obtener más información sobre esto, consulte [Módulos de integración](automation-integration-modules.md).  

>[!NOTE] 
>Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas. Estos activos se cifran y almacenan en hello automatización de Azure mediante una clave única que se genera para cada cuenta de automatización. Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure. Antes de almacenar un recurso seguro, clave de hello para la cuenta de automatización de Hola se descifra mediante certificado maestro hello y, a continuación, utilice activos de hello tooencrypt.

## <a name="windows-powershell-cmdlets"></a>Cmdlets de Windows PowerShell

cmdlets de Hello en hello en la tabla siguiente son toocreate usado y administrar conexiones de automatización con Windows PowerShell. Se incluyen como parte del programa Hola a [módulo Azure PowerShell](/powershell/azure/overview) que está disponible para su uso en runbooks de automatización y las configuraciones de DSC.

|Cmdlet|Descripción|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Recupera una conexión. Incluye una tabla hash con valores de hello de campos de la conexión de Hola.|
|[New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Crea una conexión nueva.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Quita una conexión existente.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Establece el valor de Hola de un campo determinado de una conexión existente.|

## <a name="activities"></a>Actividades

las actividades de Hello en hello en la tabla siguiente son conexiones tooaccess usado en un runbook o la configuración de DSC.

|Actividades|Descripción|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Obtiene un toouse de conexión. Devuelve una tabla hash con propiedades de Hola de conexión de Hola.|

>[!NOTE] 
>Debe evitar usar variables con Hola: parámetro de nombre de **Get - AutomationConnection** porque esto puede complicar la detección de dependencias entre runbooks o configuraciones de DSC y los activos de conexión en tiempo de diseño.

## <a name="creating-a-new-connection"></a>Creación de una conexión nueva

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate una nueva conexión con hello portal de Azure

1. En su cuenta de automatización, haga clic en hello **activos** parte tooopen hello **activos** hoja.
2. Haga clic en hello **conexiones** parte tooopen hello **conexiones** hoja.
3. Haga clic en **agregar una conexión** princip Hola de hoja de Hola.
4. Hola **tipo** lista desplegable Tipo de select Hola de conexión que desee toocreate. formulario de Hello presentará propiedades Hola para ese tipo.
5. Rellene el formulario de Hola y haga clic en **crear** toosave Hola nueva conexión.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>toocreate una nueva conexión con hello portal de Azure clásico

1. En su cuenta de automatización, haga clic en **activos** en parte superior de Hola de ventana hello.
2. En la parte inferior de Hola de ventana hello, haga clic en **Agregar configuración**.
3. Haga clic en **Agregar conexión**.
4. Hola **tipo de conexión** lista desplegable Tipo de select Hola de conexión que desee toocreate.  Asistente de Hello presentará propiedades Hola para ese tipo.
5. Complete el Asistente de Hola y haga clic en nueva conexión de hello casilla toosave Hola.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>toocreate una nueva conexión con Windows PowerShell

Crear una nueva conexión con Windows PowerShell con hello [AzureRmAutomationConnection New](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet. Este cmdlet tiene un parámetro denominado **ConnectionFieldValues** que espera un [tabla hash](http://technet.microsoft.com/library/hh847780.aspx) definir valores para cada una de las propiedades de hello definidas por tipo de conexión de Hola.

Si está familiarizado con hello automatización [cuenta de ejecución](automation-sec-configure-azure-runas-account.md) runbooks tooauthenticate con entidad de servicio de Hola Hola script de PowerShell que se proporciona como una alternativa toocreating Hola Hola cuenta de ejecución desde el portal de hello, crea un nuevo recurso de conexión mediante los siguientes comandos de ejemplo de Hola.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Está activo de conexión de toouse capaz de hello script toocreate Hola porque cuando se crea la cuenta de automatización, incluye automáticamente varios módulos globales predeterminada junto con el tipo de conexión de hello **AzurServicePrincipal**hello toocreate **AzureRunAsConnection** activo de conexión.  Esto es importante tookeep en mente, porque si intenta toocreate un nuevo servicio de tooa de tooconnect de recurso de conexión o una aplicación con un método de autenticación diferentes, producirá un error porque el tipo de conexión de hello ya no está definida en su cuenta de automatización.  Para obtener más información sobre cómo toocreate tipo de su propia conexión para el módulo de Hola o personalizada [Galería de PowerShell](https://www.powershellgallery.com), consulte [módulos de integración](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Uso de una conexión en un runbook o una configuración de DSC

Recuperar una conexión en un runbook o la configuración de DSC con hello **Get-AutomationConnection** cmdlet.  No se puede usar hello [AzureRmAutomationConnection Get](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) actividad.  Esta actividad recupera los valores de hello de diferentes campos de Hola de conexión de Hola y los devuelve como una [tabla hash](http://go.microsoft.com/fwlink/?LinkID=324844) que, a continuación, puede utilizarse con los comandos adecuados hello en runbook Hola o configuración de DSC.

### <a name="textual-runbook-sample"></a>Ejemplo de runbook de texto

Hello comandos de ejemplo siguientes muestran cómo toouse Hola cuenta de ejecución se ha mencionado anteriormente, tooauthenticate con recursos de Azure Resource Manager en su runbook.  Utiliza la conexión de hello asset que representa Hola cuenta de ejecución, que hace referencia a entidad de servicio basada en certificados de hello, no las credenciales.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Ejemplos de runbook gráfico

Agrega un **Get-AutomationConnection** actividad tooa un runbook gráfico con el botón secundario en la conexión de hello en el panel de la biblioteca de Hola de editor gráfico de Hola y seleccionando **agregar toocanvas**.

![](media/automation-connections/connection-add-canvas.png)

Hello siguiente imagen muestra un ejemplo del uso de una conexión en un runbook gráfico.  Se trata de hello mismo ejemplo expuesto anteriormente para autenticar con hello ejecutar como cuenta con un runbook textual.  Este ejemplo utiliza hello **valor constante** conjunto de datos para hello **obtener conexión de RunAs** actividad que usa un objeto de conexión para la autenticación.  A [vínculo de canalización](automation-graphical-authoring-intro.md#links-and-workflow) se usa aquí ya hello ServicePrincipalCertificate conjunto de parámetros está esperando un único objeto.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Pasos siguientes

- Revisión [vínculos de edición gráfica](automation-graphical-authoring-intro.md#links-and-workflow) toounderstand cómo hello toodirect y control de flujo de la lógica de sus runbooks.  

- toolearn más información acerca del uso de automatización de Azure de los módulos de PowerShell y los procedimientos recomendados para crear su propio toowork de módulos de PowerShell como módulos de integración en automatización de Azure, consulte [módulos de integración](automation-integration-modules.md).  
