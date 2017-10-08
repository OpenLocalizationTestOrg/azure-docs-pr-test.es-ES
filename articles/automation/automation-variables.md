---
title: "aaaVariable activos de automatización de Azure | Documentos de Microsoft"
description: "Los activos de variable son valores que están disponibles tooall runbooks y las configuraciones de DSC en automatización de Azure.  En este artículo se explica los detalles de Hola de variables y cómo toowork con ellos en la creación gráfica y textual."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Recursos de variables en Automatización de Azure

Los activos de variable son valores que están disponibles tooall runbooks y las configuraciones de DSC en su cuenta de automatización. Puede crear, modificar y recuperar de hello portal de Azure, Windows PowerShell y desde un runbook o la configuración de DSC. Las variables de automatización son útiles para hello los escenarios siguientes:

- Compartir un valor entre varios runbooks o configuraciones de DSC.

- Compartir un valor entre varios trabajos de hello mismo runbook o configuración de DSC.

- Administrar un valor desde el portal de Hola o de línea de comandos de Windows PowerShell de Hola que usa runbooks o configuraciones de DSC, como un conjunto de elementos de configuración comunes como lista específica de los nombres de las VM, un grupo de recursos específico, un nombre de dominio de AD, etcetera.  

Las variables de automatización se conservan para que sigan toobe disponible incluso si se produce un error en el runbook de Hola o configuración de DSC.  Esto también permite un toobe valor establecido por un runbook que, a continuación, se utiliza por otro, o usa Hola mismo runbook o hello de configuración de DSC próxima vez que se ejecute.

Cuando se crea una variable, puede especificar que se almacene cifrada.  Cuando se cifra una variable, se almacenan de forma segura en automatización de Azure y su valor no se puede recuperar de hello [AzureRmAutomationVariable Get](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet que se suministra como parte del módulo de PowerShell de Azure de Hola.  Hello única manera que se puede recuperar un valor cifrado es con hello **Get-AutomationVariable** actividad en un runbook o la configuración de DSC.

> [!NOTE]
> Los recursos protegidos en Automatización de Azure incluyen credenciales, certificados, conexiones y variables cifradas. Estos activos se cifran y almacenan en hello automatización de Azure mediante una clave única que se genera para cada cuenta de automatización. Esta clave se cifra mediante un certificado maestro y se almacena en Automatización de Azure. Antes de almacenar un recurso seguro, clave de hello para la cuenta de automatización de Hola se descifra mediante certificado maestro hello y, a continuación, utilice activos de hello tooencrypt.

## <a name="variable-types"></a>Tipos de variables

Cuando se crea una variable con hello portal de Azure, debe especificar un tipo de datos de la lista desplegable de hello para que el portal de hello puede mostrar el control adecuado de Hola para escribir el valor de la variable Hola. Hola variable no está restringido toothis datos tipo, pero debe establecer variable de hello mediante Windows PowerShell si desea toospecify un valor de un tipo diferente. Si especifica **no definido**, valor de Hola de variable de saludo se establecerá demasiado**$null**, y se debe establecer el valor de hello con hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet o **Set-AutomationVariable** actividad.  No se puede crear o cambiar el valor de Hola para un tipo complejo de variable en el portal de Hola, pero puede proporcionar un valor de cualquier tipo de uso de Windows PowerShell. Los tipos complejos se devolverán como un [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

Puede almacenar varios valores tooa variable de tipo simple mediante la creación de una matriz o tabla hash y guardarlo toohello variable.

siguiente Hola es una lista de tipos de variable de automatización:

* String
* Entero 
* DateTime
* Booleano
* Null

## <a name="cmdlets-and-workflow-activities"></a>Cmdlets y actividades de flujo de trabajo

cmdlets de Hello en hello en la tabla siguiente son toocreate usado y administrar variables de automatización con Windows PowerShell. Se incluyen como parte del programa Hola a [módulo Azure PowerShell](../powershell-install-configure.md) que está disponible para su uso en runbooks de automatización y la configuración de DSC.

|Cmdlets|Descripción|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Recupera el valor de Hola de una variable existente.|
|[New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|Crea una nueva variable y establece su valor.|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Quita una variable existente.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Establece el valor de Hola de una variable existente.|

las actividades de flujo de trabajo de Hello en hello en la tabla siguiente son tooaccess usa las variables de automatización en un runbook. Que solo están disponibles para su uso en un runbook o la configuración de DSC y no se incluyen como parte del módulo de PowerShell de Azure de Hola.

|Actividades de flujo de trabajo|Description|
|:---|:---|
|Get-AutomationVariable|Recupera el valor de Hola de una variable existente.|
|Set-AutomationVariable|Establece el valor de Hola de una variable existente.|

> [!NOTE] 
> Debe evitar usar variables en Hola: parámetro de nombre de **Get-AutomationVariable** en un runbook o la configuración de DSC, ya que esto puede complicar la detección de dependencias entre runbooks o la configuración de DSC y la automatización variables en tiempo de diseño.

## <a name="creating-a-new-automation-variable"></a>Creación de una nueva variable de Automatización

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate una nueva variable con hello portal de Azure

1. En su cuenta de automatización, haga clic en hello **activos** icono y, a continuación, en hello **activos** hoja, seleccione **Variables**.
2. En hello **Variables** , seleccione **agregar una variable**.
3. Complete las opciones de hello en hello **nueva Variable** hoja y haga clic en **crear** guardar Hola nueva variable.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>toocreate una nueva variable con Windows PowerShell

Hola [AzureRmAutomationVariable New](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet crea una nueva variable y establece su valor inicial. Se puede recuperar el valor de hello mediante [AzureRmAutomationVariable Get](https://msdn.microsoft.com/library/mt603849.aspx). Si el valor de hello es un tipo simple, se devuelve ese mismo tipo. Si es un tipo complejo, se devuelve **PSCustomObject** .

Mostrar comandos de ejemplo siguiente Hola cómo toocreate una variable de tipo cadena y, a continuación, devolver su valor.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

Mostrar comandos de ejemplo siguiente Hola cómo toocreate una variable con un complejo escriba y, a continuación, devolver sus propiedades. En este caso, se usa un objeto de máquina virtual desde **Get-AzureRmVm**.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Uso de una variable en un runbook o una configuración de DSC

Hola de uso **Set-AutomationVariable** valores de hello tooset las actividades de una variable de automatización en un runbook o configuración de DSC, hello y **Get-AutomationVariable** tooretrieve lo.  No debe usar hello **Set-AzureAutomationVariable** o **Get-AzureAutomationVariable** cmdlets en un runbook o la configuración de DSC, ya que son menos eficientes que las actividades de flujo de trabajo de Hola.  No se puede recuperar también valor Hola de variables seguras con **Get-AzureAutomationVariable**.  Hola toocreate de manera solo una variable desde dentro de un runbook o la configuración de DSC es hello toouse [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.


### <a name="textual-runbook-samples"></a>Ejemplos de runbook textual

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Establecimiento y recuperación de un valor simple de una variable

Mostrar comandos de ejemplo siguiente Hola cómo tooset y recuperar una variable en un runbook textual. En este ejemplo, se asume que se crearon las variables de tipo entero llamadas *NumberOfIterations* y *NumberOfRunnings* y una variable de tipo cadena denominada *SampleMessage*.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Establecimiento y recuperación de un objeto completo en una variable

siguiente Hola código de ejemplo muestra cómo tooupdate una variable con un valor complejo en un runbook textual. En este ejemplo, se recupera una máquina virtual de Azure con **Get-AzureVM** y guardado tooan variable de automatización existente.  Como se explica en [Tipos de variables](#variable-types), se almacena como un PSCustomObject.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


En el siguiente código de hello, el valor de Hola se recupera de la máquina virtual de hello toostart variable y usar Hola.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Establecimiento y recuperación de una colección en una variable

siguiente Hola código de ejemplo muestra cómo toouse una variable con una colección de valores complejos en un runbook textual. En este ejemplo, se recuperan varias máquinas virtuales de Azure con **Get-AzureVM** y guardado tooan variable de automatización existente.  Como se explica en [Tipos de variables](#variable-types), se almacena como una colección de objetos PSCustomObject.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

En el siguiente código de hello, colección de Hola se recupera de la variable de Hola y toostart usa cada máquina virtual.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>Ejemplos de runbook gráfico

En un runbook gráfico, agregar hello **Get-AutomationVariable** o **Set-AutomationVariable** , haga doble clic en la variable de hello en panel de la biblioteca de Hola de editor gráfico de Hola y seleccione Hola actividad que desee.

![Agregar variable toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Configuración de valores de una variable
Hello siguiente imagen muestra ejemplo actividades tooupdate una variable con un valor simple en un runbook gráfico. En este ejemplo, se recupera una sola máquina virtual de Azure con **AzureRmVM Get** y el nombre del equipo de Hola se guarda tooan variable de automatización existente con un tipo de cadena.  No importa si hello [vínculo es una canalización o una secuencia](automation-graphical-authoring-intro.md#links-and-workflow) ya que solo se puede esperar un único objeto de salida de hello.

![Establecimiento de una variable simple](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Pasos siguientes

* toolearn más acerca de cómo conectar actividades juntos en el gráfico de creación, vea [vínculos de edición gráfica](automation-graphical-authoring-intro.md#links-and-workflow)
* tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md) 

