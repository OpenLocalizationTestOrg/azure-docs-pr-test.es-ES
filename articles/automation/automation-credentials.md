---
title: "aaaCredential activos de automatización de Azure | Documentos de Microsoft"
description: "Recursos de credenciales en la automatización de Azure contienen las credenciales de seguridad que pueden ser tooresources tooauthenticate usa acceso a runbook Hola o configuración de DSC. Este artículo describe cómo toocreate activos de credenciales y usarlos en un runbook o la configuración de DSC."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Recursos de credenciales en Automatización de Azure
Un recurso de credencial de Automation contiene un objeto [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) que contiene credenciales de seguridad, como un nombre de usuario y una contraseña. Las configuraciones de runbooks y DSC pueden usar los cmdlets que aceptan un objeto PSCredential para la autenticación, o puede extraer el nombre de usuario de hello y una contraseña de hello tooprovide toosome aplicación de PSCredential objeto o servicio que requiera autenticación. propiedades de Hola para una credencial se almacenan de forma segura en automatización de Azure y puede obtenerse mediante runbook Hola o configuración de DSC con hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) actividad.

> [!NOTE]
> Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas. Estos activos se cifran y almacenan en hello automatización de Azure mediante una clave única que se genera para cada cuenta de automatización. Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure. Antes de almacenar un recurso seguro, clave de hello para la cuenta de automatización de Hola se descifra mediante certificado maestro hello y, a continuación, utilice activos de hello tooencrypt.  

## <a name="windows-powershell-cmdlets"></a>Cmdlets de Windows PowerShell
cmdlets de Hello en hello en la tabla siguiente son toocreate usado y administrar recursos de la credencial de automatización con Windows PowerShell.  Se incluyen como parte del programa Hola a [módulo Azure PowerShell](/powershell/azure/overview) que está disponible para su uso en runbooks de automatización y las configuraciones de DSC.

| Cmdlets | Descripción |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |Recupera información acerca de un recurso de credencial. Solo se puede recuperar la credencial de Hola de **Get-AutomationPSCredential** actividad. |
| [New-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Crea una nueva credencial de Automatización. |
| [Remove- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Quita una credencial de Automatización. |
| [Set- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Conjuntos de Hola propiedades de una credencial de automatización existente. |

## <a name="runbook-activities"></a>Actividades de runbook
las actividades de Hello en hello en la tabla siguiente son credenciales tooaccess usado en un runbook y las configuraciones de DSC.

| Actividades | Descripción |
|:--- |:--- |
| Get-AutomationPSCredential |Obtiene un toouse de credencial en un runbook o la configuración de DSC. Devuelve un objeto [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) . |

> [!NOTE]
> Debe evitar usar variables en Hola: parámetro Name de Get-AutomationPSCredential ya que esto puede complicar la detección de dependencias entre runbooks o configuraciones de DSC y activos de credenciales en tiempo de diseño.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Creación de un nuevo recurso de credencial

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate un nuevo recurso de credencial con hello portal de Azure
1. En su cuenta de automatización, haga clic en hello **activos** parte tooopen hello **activos** hoja.
2. Haga clic en hello **credenciales** parte tooopen hello **credenciales** hoja.
3. Haga clic en **agregar una credencial** princip Hola de hoja de Hola.
4. Rellene el formulario de Hola y haga clic en **crear** toosave Hola nueva credencial.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate un recurso de credencial nuevo con Windows PowerShell
Hello comandos de ejemplo siguientes muestran cómo toocreate una automatización nueva credencial. Un objeto PSCredential se crea por primera vez con el nombre de Hola y la contraseña y, a continuación, usa activo de credencial de toocreate Hola. Como alternativa, podría utilizar hello **Get-Credential** toobe cmdlet pide tootype en un nombre y una contraseña.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate un nuevo recurso de credencial con hello portal de Azure clásico
1. En su cuenta de automatización, haga clic en **activos** en parte superior de Hola de ventana hello.
2. En la parte inferior de Hola de ventana hello, haga clic en **Agregar configuración**.
3. Haga clic en **Agregar credencial**.
4. Hola **tipo de credencial** lista desplegable, seleccione **credencial de PowerShell**.
5. Complete el Asistente de Hola y haga clic en nueva credencial de hello casilla toosave Hola.

## <a name="using-a-powershell-credential"></a>Uso de una credencial de PowerShell
Recuperar un recurso de credencial en un runbook o la configuración de DSC con hello **Get-AutomationPSCredential** actividad. Esto devuelve un [objeto PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) que puede usar con una actividad o cmdlet que requiere un parámetro PSCredential. También puede recuperar propiedades de Hola de toouse de objeto de credencial de hello individualmente. objeto Hello tiene una propiedad Hola nombre de usuario y una contraseña segura de hello, o puede usar hello **GetNetworkCredential** método tooreturn una [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) objeto que proporcionará una no segura versión de Hola contraseña.

### <a name="textual-runbook-sample"></a>Ejemplo de runbook de texto
Hello comandos de ejemplo siguientes muestran cómo toouse un PowerShell de credenciales en un runbook. En este ejemplo, se recupera la credencial de Hola y su nombre de usuario y la contraseña asignan toovariables.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Ejemplo de runbook gráfico
Agrega un **Get-AutomationPSCredential** actividad tooa un runbook gráfico con el botón secundario en la credencial de hello en el panel de la biblioteca de Hola de editor gráfico de Hola y seleccionando **agregar toocanvas**.

![Agregar credencial toocanvas](media/automation-credentials/credential-add-canvas.png)

Hello siguiente imagen muestra un ejemplo del uso de una credencial en un runbook gráfico.  En este caso, se está autenticación tooprovide usados para los recursos de tooAzure de runbook tal como se describe en [Runbooks autenticar con la cuenta de usuario de Azure AD](automation-create-aduser-account.md).  primera actividad de Hello recupera la credencial de Hola que tiene acceso toohello suscripción de Azure.  Hola **Add-AzureAccount** actividad, a continuación, usa esta credencial tooprovide la autenticación para las actividades que venir después de ella.  Aquí se encuentra un [vínculo de canalización](automation-graphical-authoring-intro.md#links-and-workflow) , debido a que **Get-AutomationPSCredential** espera un solo objeto.  

![Agregar credencial toocanvas](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>Uso de una credencial de PowerShell en DSC
Mientras las configuraciones DSC en Automatización de Azure pueden hacer referencia a los activos de credenciales a través de **Get-AutomationPSCredential**, los activos de credenciales también se pueden pasar, si se desea, a través de los parámetros. Para obtener más información, consulte [Compilación de configuraciones en DSC de Automatización de Azure](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de los vínculos de edición gráfica, consulte [vínculos de edición gráfica](automation-graphical-authoring-intro.md#links-and-workflow)
* toounderstand Hola distintos métodos de autenticación con la automatización, vea [seguridad de automatización de Azure](automation-security-overview.md)
* tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md)
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md) 

