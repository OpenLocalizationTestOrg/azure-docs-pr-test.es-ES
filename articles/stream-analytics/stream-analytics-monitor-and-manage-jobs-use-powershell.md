---
title: "aaaMonitor y administrar los trabajos de análisis de transmisiones con PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomonitor de PowerShell de Azure y los cmdlets de toouse y administrar los trabajos de análisis de transmisiones."
keywords: azure powershell, cmdlets de azure powershell, comando de powershell, scripting de powershell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Supervisar y administrar los trabajos de Análisis de transmisiones con los cmdlets de Azure PowerShell
Obtenga información acerca de cómo toomonitor y administrar los recursos de análisis de transmisiones con cmdlets de PowerShell de Azure y secuencias de comandos de powershell que se ejecutan las tareas básicas de análisis de transmisiones.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Requisitos previos para ejecutar cmdlets de Azure PowerShell en Análisis de transmisiones
* Cree un grupo de recursos de Azure en su suscripción. Hola aquí te mostramos una secuencia de comandos de PowerShell de Azure de ejemplo. Para obtener información sobre Azure PowerShell, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).  

Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0:  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Los trabajos de Análisis de transmisiones creados mediante programación no tienen la supervisión habilitada de forma predeterminada.  Puede habilitar la supervisión en hello Azure Portal desplazándose página del Monitor del trabajo toohello manualmente y haga clic en el botón Habilitar de Hola o se puede hacer esto mediante programación siguiendo los pasos de hello ubicados en [análisis de transmisiones de Azure - secuencia de Monitor Análisis de trabajos mediante programación](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Cmdlets de PowerShell de Azure en Análisis de transmisiones
Hola siguientes cmdlets de PowerShell de Azure puede ser toomonitor usado y administrar los trabajos de análisis de transmisiones de Azure. Tenga en cuenta que Azure PowerShell tiene versiones diferentes. 
**En los ejemplos de Hola Hola enumerados primer comando es para Azure PowerShell 0.9.8, segundo comando de hello es para Azure PowerShell 1.0.** comandos de Hello Azure PowerShell 1.0 siempre tendrá "AzureRM" en el comando de Hola.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Obtiene información sobre el trabajo sobre un trabajo específico dentro de un grupo de recursos o muestra todos los trabajos de análisis de transmisiones definidos en la suscripción de Azure de Hola o grupo de recursos especificado.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob

Este comando de PowerShell devuelve información acerca de todos los trabajos de análisis de transmisiones de Hola Hola suscripción de Azure.

**Ejemplo 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Este comando de PowerShell devuelve información acerca de todos los trabajos de análisis de transmisiones de hello en grupo de recursos de hello StreamAnalytics predeterminado-centro de EE.

**Ejemplo 3**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Este comando de PowerShell devuelve información sobre el trabajo de análisis de transmisiones de hello StreamingJob en grupo de recursos de hello StreamAnalytics predeterminado-centro de EE.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Enumera todas las entradas de Hola que se definen en un trabajo de análisis de transmisiones especificado u obtiene información sobre una entrada específica.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Este comando de PowerShell devuelve información acerca de todas las entradas de hello definidos en el trabajo de hello StreamingJob.

**Ejemplo 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Este comando de PowerShell devuelve información acerca de la entrada de hello denominado EntryStream definido en el trabajo de hello StreamingJob.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Enumera todas las salidas de Hola que se definen en un trabajo de análisis de transmisiones especificado u obtiene información sobre un resultado concreto.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Este comando de PowerShell devuelve información sobre definidas en el trabajo de hello StreamingJob salidas de Hola.

**Ejemplo 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Este comando de PowerShell devuelve información acerca de la salida de hello denominado salida definida en el trabajo de hello StreamingJob.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Obtiene información sobre la cuota de Hola de transmisión por secuencias unidades en una región determinada.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Este comando de PowerShell devuelve información acerca de la cuota de Hola y el uso de unidades de streaming en la región de EE. UU. Central Hola.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Obtiene información sobre una transformación específica definida en un trabajo de Análisis de transmisiones.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Este comando de PowerShell devuelve información sobre la transformación de hello denominado StreamingJob en el trabajo de hello StreamingJob.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput
Crea otra entrada en un trabajo de Análisis de transmisiones o actualiza una determinada entrada existente.

Hello nombre de entrada de hello puede especificarse en el archivo .json de Hola o en línea de comandos de Hola. Si se especifican ambos, debe Hola igual que hello en el archivo hello nombre hello en línea de comandos de Hola.

Si especifica una entrada que ya existe y no se especifica hello: parámetro Force, Hola cmdlet le preguntará si o no tooreplace Hola los datos existentes.

Si especifica Hola: el parámetro Force y especifique otra entrada nombre, entrada Hola se reemplazará sin confirmación.

Para obtener información detallada sobre la estructura de archivos JSON de Hola y de contenido, consulte toohello [crear entrada (análisis de transmisiones de Azure)] [ msdn-rest-api-create-stream-analytics-input] sección de hello [API de REST de administración de análisis de transmisiones Biblioteca de referencia de][stream.analytics.rest.api.reference].

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Este comando de PowerShell crea una nueva entrada de archivo hello Input.json. Si ya hay definida una entrada existente con el nombre de hello especificado en el archivo de definición de entrada de hello, Hola cmdlet le preguntará si tooreplace se.

**Ejemplo 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Este comando de PowerShell crea una nueva entrada en el trabajo de hello denominado EntryStream. Si una entrada existente con este nombre ya está definida, Hola cmdlet le preguntará si tooreplace se.

**Ejemplo 3**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Este comando de PowerShell reemplaza la definición de Hola Hola existente de origen de entrada llamado EntryStream con definición Hola desde archivo hello.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob
Crea un nuevo trabajo de análisis de transmisiones de Microsoft Azure o actualiza la definición de Hola de un trabajo existente especificado.

nombre de Hello del trabajo de hello puede especificarse en el archivo .json de Hola o en línea de comandos de Hola. Si se especifican ambos, debe Hola igual que hello en el archivo hello nombre hello en línea de comandos de Hola.

Si especifica un nombre de trabajo que ya existe y no se especifica hello: parámetro Force, Hola cmdlet le preguntará si o no tooreplace Hola trabajo existente.

Si especifica Hola: el parámetro Force y especificar un nombre de trabajo existente, se reemplazará la definición del trabajo Hola sin confirmación.

Para obtener información detallada sobre la estructura de archivos JSON de Hola y de contenido, consulte toohello [crear trabajo de Stream Analytics] [ msdn-rest-api-create-stream-analytics-job] sección de hello [referencia de API de REST de administración de análisis de transmisiones Biblioteca][stream.analytics.rest.api.reference].

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Este comando de PowerShell crea un nuevo trabajo de definición de hello en JobDefinition.json. Si ya está definido un trabajo existente con el nombre de hello especificado en el archivo de definición de trabajo de hello, Hola cmdlet le preguntará si tooreplace se.

**Ejemplo 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Este comando de PowerShell reemplaza la definición del trabajo Hola para StreamingJob.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput
Crea una salida en un trabajo de Análisis de transmisiones o actualiza una salida existente.  

nombre de Hola de salida de hello puede especificarse en el archivo .json de Hola o en línea de comandos de Hola. Si se especifican ambos, debe Hola igual que hello en el archivo hello nombre hello en línea de comandos de Hola.

Si especifica una salida que ya existe y no se especifica hello: parámetro Force, Hola cmdlet le preguntará si o no tooreplace Hola salida existente.

Si especifica Hola: el parámetro Force y especifique el nombre de salida de una existente, se reemplazará la salida de hello sin confirmación.

Para obtener información detallada sobre la estructura de archivos JSON de Hola y de contenido, consulte toohello [crear salida (análisis de transmisiones de Azure)] [ msdn-rest-api-create-stream-analytics-output] sección de hello [API de REST de administración de análisis de transmisiones Biblioteca de referencia de][stream.analytics.rest.api.reference].

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Este comando de PowerShell crea una nueva llamada "salida" en el trabajo de hello StreamingJob de salida. Si una salida existente con este nombre ya está definida, Hola cmdlet le preguntará si tooreplace se.

**Ejemplo 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Este comando de PowerShell reemplaza la definición de Hola de "salida" en el trabajo de hello StreamingJob.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation
Crea una nueva transformación dentro de un trabajo de análisis de transmisiones o actualiza transformación existente Hola.

nombre de Hola de transformación de Hola puede especificarse en el archivo .json de Hola o en línea de comandos de Hola. Si se especifican ambos, debe Hola igual que hello en el archivo hello nombre hello en línea de comandos de Hola.

Si especifica una transformación que ya existe y no se especifica hello: parámetro Force, Hola cmdlet le preguntará si o no tooreplace Hola transformación existente.

Si especifica Hola: el parámetro Force y especificar un nombre de la transformación existente, se reemplazará la transformación de hello sin confirmación.

Para obtener información detallada sobre la estructura de archivos JSON de Hola y de contenido, consulte toohello [crear una transformación (análisis de transmisiones de Azure)] [ msdn-rest-api-create-stream-analytics-transformation] sección de hello [administración de análisis de transmisiones Biblioteca de referencia de API de REST][stream.analytics.rest.api.reference].

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Este comando de PowerShell crea una nueva transformación denominada StreamingJobTransform en el trabajo de hello StreamingJob. Si una transformación existente ya está definida con este nombre, Hola cmdlet le preguntará si tooreplace se.

**Ejemplo 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 Este comando de PowerShell reemplaza la definición de Hola de StreamingJobTransform en el trabajo de hello StreamingJob.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput
Elimina de forma asincrónica una entrada específica desde un trabajo de Análisis de transmisiones en Microsoft Azure.  
Si especifica hello: parámetro Force, Hola de entrada se eliminará sin confirmación.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Este comando de PowerShell quita Hola EventStream de entrada en el trabajo de hello StreamingJob.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob
Elimina de forma asincrónica un trabajo específico de Análisis de transmisiones en Microsoft Azure.  
Si especifica hello: parámetro Force, Hola trabajo será eliminado sin confirmación.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Este comando de PowerShell quita el trabajo de hello StreamingJob.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput
Elimina de forma asincrónica un resultado concreto de un trabajo de Análisis de transmisiones en Microsoft Azure.  
Si especifica hello: parámetro Force, Hola resultado será eliminado sin confirmación.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Este comando de PowerShell quita hello salida salida en el trabajo de hello StreamingJob.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob
Implementa e inicia un trabajo de Análisis de transmisiones de Microsoft Azure de forma asincrónica.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0:  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Este comando de PowerShell inicia Hola trabajo StreamingJob con una hora de inicio de salida personalizada establece tooDecember 12, 2012, 12:12:12 UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
Detiene la ejecución de un trabajo de Análisis de transmisiones en Microsoft Azure y desasigna recursos que se usaban de forma asincrónica. Hello metadatos y la definición de trabajo seguirán estando disponibles dentro de su suscripción a través de hello portal de Azure y API de administración, por ejemplo, que hello trabajo puede editar y reiniciar. No se le cobrará por un trabajo en el estado de hello detenido.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Este comando de PowerShell detiene el trabajo de hello StreamingJob.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput
Posibilidad de Hola de pruebas de análisis de transmisiones tooconnect tooa especifica la entrada.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Este estado de conexión de PowerShell comando pruebas Hola de hello EntryStream en StreamingJob de entrada.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput
Posibilidad de Hola de pruebas de análisis de transmisiones tooconnect tooa especifica la salida.

**Ejemplo 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Este estado de conexión de PowerShell comando pruebas Hola de hello salida salida en StreamingJob.  

## <a name="get-support"></a>Obtención de soporte técnico
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics). 

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

