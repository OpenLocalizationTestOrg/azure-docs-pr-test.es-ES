---
title: "parámetros de entrada de aaaRunbook | Documentos de Microsoft"
description: "Parámetros de entrada de runbook aumentan la flexibilidad de Hola de runbooks permitiéndole toopass datos tooa runbook cuando se inicia. En este artículo se describen los distintos escenarios donde se usan parámetros de entrada en Runbooks."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Parámetros de entrada de Runbook
Parámetros de entrada de runbook aumentan la flexibilidad de Hola de runbooks permitiéndole toopass datos tooit cuando se inicie. los parámetros de Hello permiten Hola runbook acciones toobe destinado a entornos y escenarios concretos. En este artículo, le guiaremos por los distintos escenarios donde se usan parámetros de entrada en Runbooks.

## <a name="configure-input-parameters"></a>Configuración de parámetros de entrada
Los parámetros de entrada pueden configurarse en Runbooks gráficos, de PowerShell y de flujo de trabajo de PowerShell. Un Runbook puede tener varios parámetros con tipos de datos diferentes o sin parámetros. Los parámetros de entrada pueden ser obligatorios u opcionales, y puede asignar un valor predeterminado a los parámetros opcionales. Puede asignar valores de parámetros de entrada de toohello para un runbook cuando se inicia a través de uno de los métodos disponibles de Hola. Estos métodos incluyen iniciar un runbook desde el portal de Hola o un servicio web. También puede iniciarlo como Runbook secundario al que se llama insertado en otro Runbook.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>Configuración de parámetros de entrada en Runbooks de PowerShell y de flujo de trabajo de PowerShell
PowerShell y [runbooks de flujo de trabajo de PowerShell](automation-first-runbook-textual.md) en automatización de Azure admite parámetros de entrada que se definen a través de los siguientes atributos de Hola.  

| **Propiedad** | **Descripción** |
|:--- |:--- |
| Tipo |Necesario. tipo de datos de Hello esperado para el valor del parámetro hello. Es válido cualquier tipo .NET. |
| Nombre |Necesario. nombre de Hello del parámetro hello. Esto debe ser único dentro de runbook de hello y pueden contener solo letras, números o caracteres de subrayado. Debe empezar por una letra. |
| Obligatorio |Opcional. Especifica si se debe proporcionar un valor para el parámetro hello. Si se establece demasiado**$true**, a continuación, se debe proporcionar un valor al iniciar runbook Hola. Si se establece demasiado**$false**, a continuación, un valor es opcional. |
| Valor predeterminado |Opcional.  Especifica un valor que se usará para el parámetro hello si no se pasa un valor de cuando se inicie el runbook de Hola. Un valor predeterminado se puede establecer para cualquier parámetro y realizará automáticamente parámetro hello opcional independientemente Hola parámetro obligatorio. |

Windows PowerShell admite más atributos de parámetros de entrada de los enumerados aquí, como validación, alias y conjuntos de parámetros. Sin embargo, automatización de Azure admite actualmente solo Hola parámetros de entrada mencionados anteriormente.

Una definición de parámetro en los runbooks de flujo de trabajo de PowerShell tiene Hola después de forma general, donde varios parámetros se separan por comas.

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> Si va a definir parámetros, si no se especifica hello **obligatorio** atributo, de forma predeterminada, el parámetro hello se considera opcional. Además, si establece un valor predeterminado para un parámetro en los runbooks de flujo de trabajo de PowerShell, se tratará PowerShell como un parámetro opcional, con independencia de hello **obligatorio** valor de atributo.
> 
> 

Por ejemplo, vamos a configurar los parámetros de entrada de hello en un runbook de flujo de trabajo de PowerShell que proporciona detalles sobre las máquinas virtuales, una sola máquina virtual o todas las máquinas virtuales dentro de un grupo de recursos. Este runbook tiene dos parámetros, como se muestra en la siguiente captura de pantalla de Hola: nombre de Hola de máquina virtual y el nombre de Hola Hola del grupo de recursos.

![Automatización, flujo de trabajo de PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

En esta definición de parámetro, Hola parámetros **$VMName** y **$resourceGroupName** son simples parámetros de tipo cadena. Sin embargo, los Runbooks de PowerShell y de flujo de trabajo de PowerShell admiten todos los tipos simples y complejos, como **object** o **PSCredential**, como parámetros de entrada.

Si el runbook tiene un parámetro de entrada de tipo de objeto, a continuación, utilice una tabla hash de PowerShell por (nombre, valor) pares toopass en un valor. Por ejemplo, si tienes Hola después de parámetro en un runbook:

     [Parameter (Mandatory = $true)]
     [object] $FullName

A continuación, puede pasar Hola siguiendo el valor del parámetro toohello:

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>Configuración de parámetros de entrada en Runbooks gráficos
demasiado[configurar un runbook gráfico](automation-first-runbook-graphical.md) con parámetros de entrada, vamos a crear un runbook gráfico que muestra detalles acerca de las máquinas virtuales, ya sea una sola máquina virtual o todas las máquinas virtuales dentro de un grupo de recursos. La configuración de un Runbook consta de dos actividades principales, como se describe a continuación.

[**Autenticar Runbooks con la cuenta de identificación de Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate con Azure.

[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget propiedades de Hola de una máquina virtual.

Puede usar hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) nombres de actividad toooutput Hola de máquinas virtuales. Hola actividad **Get AzureRmVm** acepta dos parámetros, hello **nombre de máquina virtual** hello y **nombre del grupo de recursos**. Puesto que estos parámetros requieren valores diferentes cada vez que inicie runbook hello, puede agregar parámetros de entrada tooyour runbook. Estos son parámetros de entrada tooadd Hola pasos:

1. Seleccione Hola runbook gráfico de hello **Runbooks** hoja y, a continuación, haga clic en [ **editar** ](automation-graphical-authoring-intro.md) lo.
2. En el editor de runbook hello, haga clic en **de entrada y salida** tooopen hello **de entrada y salida** hoja.
   
    ![Runbook gráfico de Automatización](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. Hola **de entrada y salida** hoja muestra una lista de parámetros de entrada que se definen para el runbook de Hola. En esta hoja, puede agregar un nuevo parámetro de entrada o editar configuración de Hola de un parámetro de entrada existente. tooadd un nuevo parámetro hello runbook, haga clic en **Agregar entrada** tooopen hello **parámetro de entrada de Runbook** hoja. Allí, puede configurar Hola parámetros siguientes:
   
   | **Propiedad** | **Descripción** |
   |:--- |:--- |
   | Nombre |Necesario.  nombre de Hello del parámetro hello. Esto debe ser único dentro de runbook de hello y pueden contener solo letras, números o caracteres de subrayado. Debe empezar por una letra. |
   | Descripción |Opcional. Descripción sobre el propósito de hello del parámetro de entrada. |
   | Tipo |Opcional. tipo de datos de Hola que se espera que el valor del parámetro hello. Los tipos de parámetro admitidos son **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** y **Object**. Si no se selecciona un tipo de datos, el valor predeterminado es demasiado**cadena**. |
   | Obligatorio |Opcional. Especifica si se debe proporcionar un valor para el parámetro hello. Si elige **Sí**, a continuación, se debe proporcionar un valor al iniciar runbook Hola. Si elige **no**, a continuación, no se requiere un valor cuando se inicie el runbook de Hola y puede establecerse un valor predeterminado. |
   | Valor predeterminado |Opcional. Especifica un valor que se usará para el parámetro hello si no se pasa un valor de cuando se inicie el runbook de Hola. Puede establecerse un valor predeterminado para un parámetro que no sea obligatorio. Elija un valor predeterminado, tooset **personalizado**. Este valor se utiliza a menos que se proporcione otro valor cuando se inicie el runbook de Hola. Elija **ninguno** si no desea que tooprovide cualquier valor predeterminado. |
   
    ![Agregar nueva entrada](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. Crear dos parámetros con propiedades que se va a utilizar Hola siguientes de hello **AzureRmVm Get** actividad:
   
   * **Parameter1:**
     
     * Nombre: VMName
     * Tipo: String
     * Obligatorio: No
   * **Parameter2:**
     
     * Nombre: resourceGroupName
     * Tipo: String
     * Obligatorio: No
     * Valor predeterminado: Personalizado
     * Valor predeterminado personalizado - \<nombre del grupo de recursos de Hola que contiene máquinas virtuales de hello >
5. Una vez que agregue parámetros hello, haga clic en **Aceptar**.  Ahora puede ver en hello **entrada y el módulo de salida**. Haga clic en **Aceptar** de nuevo y después en **Guardar** y en **Publicar** para publicar el Runbook.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Asignar valores tooinput parámetros en runbooks
Puede pasar valores tooinput parámetros en runbooks en hello los escenarios siguientes.

### <a name="start-a-runbook-and-assign-parameters"></a>Inicio de un Runbook y asignación de parámetros
Se puede iniciar un runbook muchas maneras: a través del portal de Azure, con un webhook, con los cmdlets de PowerShell, con hello API de REST o con hello SDK Hola. A continuación, se describen distintos métodos para iniciar un Runbook y asignar parámetros.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Iniciar un runbook publicado mediante Hola portal de Azure y asignar parámetros
Cuando se [iniciar runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **iniciar Runbook** hoja se abre y puede configurar valores para parámetros de Hola que acaba de crear.

![Empezar a usar el portal de Hola](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

En etiqueta de hello debajo del cuadro de entrada de hello, puede ver los atributos de Hola que se han configurado para el parámetro hello. Entre los atributos, se incluye si es obligatorio u opcional, el tipo y el valor predeterminado. En hello ayuda globo siguiente toohello nombre del parámetro, puede ver toda información de clave de hello necesita toomake decisiones acerca de los valores de entrada de parámetro. Esta información incluye si un parámetro es obligatorio u opcional. También incluye el tipo de Hola y valor predeterminado (si existe) y otras notas útiles.

![Globo de ayuda](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> Los parámetros de tipo String admiten valores de cadena **Empty** .  Escriba **[EmptyString]** en el parámetro de entrada de hello cuadro pasará un parámetro de toohello de cadena vacía. Además, los parámetros de tipo String no permiten que se pasen valores **Null** . Si no pasa ningún parámetro de cadena de valor toohello, a continuación, PowerShell interpretará esa como null.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>Inicio de un Runbook publicado mediante cmdlets de PowerShell y asignación de parámetros
* **Cmdlets de Azure Resource Manager:** puede iniciar un Runbook de automatización creado en un grupo de recursos mediante [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).
  
  **Ejemplo:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Cmdlets de Administración de servicios de Azure:** puede iniciar un Runbook de automatización creado en un grupo de recursos predeterminado mediante [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).
  
  **Ejemplo:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> Cuando se inicia un runbook mediante cmdlets de PowerShell, un parámetro predeterminado, **MicrosoftApplicationManagementStartedBy** se crea con el valor de hello **PowerShell**. Puede ver este parámetro en hello **detalles del trabajo** hoja.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>Inicio de un Runbook con un SDK y asignación de parámetros
* **Método de administrador de recursos de Azure:** pueden iniciar un runbook mediante Hola SDK de un lenguaje de programación. A continuación, se muestra un fragmento de código C# para iniciar un Runbook en su cuenta de Automatización. Puede ver todo el código de hello en nuestro [repositorio de GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Método de administración de servicios de Azure:** pueden iniciar un runbook mediante Hola SDK de un lenguaje de programación. A continuación, se muestra un fragmento de código C# para iniciar un Runbook en su cuenta de Automatización. Puede ver todo el código de hello en nuestro [repositorio de GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart este método, crear un hello toostore de diccionario de parámetros de runbook, **VMName** y **resourceGroupName**y sus valores. A continuación, inicie runbook Hola. A continuación se muestra hello C# fragmento de código para llamar al método hello definido anteriormente.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Iniciar un runbook mediante la API de REST de Hola y asignar parámetros
Se puede crear un trabajo de runbook e inició con hello API de REST de automatización de Azure mediante hello **colocar** método con hello siguiente URI de solicitud.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

Hola URI de la solicitud, reemplace Hola parámetros siguientes:

* **subscription-id** : identificador de su suscripción a Azure.  
* **nombre del servicio de nube:** se debe enviar el nombre de Hola de solicitud de hello en la nube servicio toowhich Hola.  
* **nombre de cuenta de automatización:** nombre de Hola de su cuenta de automatización que se hospeda dentro de hello especifica el servicio en la nube.  
* **Id. de trabajo:** Hola GUID para el trabajo de Hola. Se pueden crear GUID en PowerShell mediante el uso de hello **[GUID]::NewGuid(). ToString()** comando.

En el trabajo de runbook de orden toopass parámetros toohello, utilice el cuerpo de solicitud de Hola. Toma Hola dos propiedades que se proporcionan en formato JSON siguientes:

* **Nombre del Runbook**: obligatorio. nombre de Hola de runbook de Hola para hello toostart de trabajo.  
* **Parámetros del Runbook**: opcionales. Dar formato a un diccionario de la lista de parámetros hello (nombre, valor) donde el nombre debe ser de tipo cadena y valor puede ser cualquier valor JSON válido.

Si desea que hello toostart **Get AzureVMTextual** runbook que creó anteriormente con **VMName** y **resourceGroupName** como parámetros, use Hola siguiendo el formato JSON en el cuerpo de solicitud de saludo.

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

Si se creó correctamente el trabajo de hello, se devuelve un código de estado HTTP 201. Para obtener más información sobre encabezados de respuesta y el cuerpo de respuesta de hello, consulte el artículo toohello acerca de cómo demasiado[crear un trabajo de runbook mediante Hola API de REST.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Prueba de un Runbook y asignación de parámetros
Cuando se [versión de borrador de Hola de prueba del runbook](automation-testing-runbook.md) mediante la opción de prueba de hello, Hola **probar** hoja se abre y puede configurar valores para parámetros de Hola que acaba de crear.

![Prueba y asignación de parámetros](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>Vincular un runbook de tooa de programación y asignar parámetros
También puede [vincular una programación](automation-schedules.md) tooyour runbook para ese runbook Hola se inicia en un momento determinado. Asignar parámetros de entrada cuando se crean Hola y Hola runbook usará estos valores cuando se inicia según la programación de Hola. No se puede guardar la programación de hello hasta que se proporcionan todos los valores de parámetro obligatorio.

![Programación y asignación de parámetros](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Creación de un Webhook para un Runbook y asignación de parámetros
Puede crear un [Webhook](automation-webhooks.md) para el Runbook y configurar los parámetros de entrada del Runbook. No se puede guardar hello webhook hasta que se proporcionan todos los valores de parámetro obligatorio.

![Creación de un Webhook y asignación de parámetros](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

Cuando se ejecuta un runbook mediante el uso de un webhook, Hola predefinidos de parámetro de entrada  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  se envía junto con los parámetros de entrada de Hola que ha definido. Puede hacer clic en hello tooexpand **WebhookData** parámetro para obtener más detalles.

![Parámetro WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>Pasos siguientes
* Para más información sobre la entrada y salida de Runbooks, consulte [Azure Automation: Runbook Input, Output, and Nested Runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)(Automatización de Azure: entrada y salida de Runbooks, y Runbooks anidados).
* Para obtener más información acerca de diferentes maneras toostart un runbook, consulte [a partir de un runbook](automation-starting-a-runbook.md).
* tooedit un runbook textual, consulte demasiado[editar runbooks textuales](automation-edit-textual-runbook.md).
* tooedit un runbook gráfico, consulte demasiado[edición gráfica en automatización de Azure](automation-graphical-authoring-intro.md).

