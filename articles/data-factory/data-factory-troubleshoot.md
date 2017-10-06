---
title: problemas de aaaTroubleshoot Data Factory de Azure
description: "Obtenga información acerca de cómo tootroubleshoot problemas con el uso de Data Factory de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a>Solución de problemas de la factoría de datos
En este artículo se proporcionan consejos para solución de problemas surgidos al usar Data Factory de Azure. En este artículo no enumera todos los posibles problemas de hello cuando se usa el servicio de hello, pero se tratan algunos problemas y sugerencias de solución de problemas generales.   

## <a name="troubleshooting-tips"></a>Sugerencias de solución de problemas
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Error: suscripción de hello no está registrado toouse de espacio de nombres 'Microsoft.DataFactory'
Si recibe este error, no se registró el proveedor de recursos de hello Data Factory de Azure en su equipo. Hola siguientes:

1. Inicie Azure PowerShell.
2. Inicie sesión en tooyour cuenta de Azure mediante el siguiente comando de Hola.

    ```powershell
    Login-AzureRmAccount
    ```
3. Ejecute hello después de proveedor del comando tooregister Hola Data Factory de Azure.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Problema: error no autorizado al ejecutar un cmdlet de Factoría de datos
Probablemente no utilizas Hola derecha cuenta de Azure o suscripción con hello Azure PowerShell. Usar hello después cmdlets tooselect Hola derecha toouse de cuenta y suscripción de Azure con hello Azure PowerShell.

1. Inicio de sesión-AzureRmAccount - Id. de usuario de uso hello y una contraseña
2. Get-AzureRmSubscription - vista todos Hola suscripciones de cuenta de hello.
3. Seleccione AzureRmSubscription &lt;nombre de la suscripción&gt; -seleccione Hola derecho suscripción. Use Hola mismo que usar toocreate una factoría de datos en hello portal de Azure.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Problema: No toolaunch instalación de Express de puerta de enlace de datos de administración del portal de Azure
el programa de instalación rápida de Hola para hello Data Management Gateway requiere Internet Explorer o un explorador de web compatible con Microsoft ClickOnce. Si el programa de instalación de Express de Hola no toostart, siga uno de los procedimientos de hello:

* Utilice Internet Explorer o un explorador web compatible con Microsoft ClickOnce.

    Si usas Chrome, vaya toohello [almacén web de Chrome](https://chrome.google.com/webstore/), buscar con la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce hello e instalarlo.

    Hola mismo para Firefox (complemento de instalación). Haga clic en el botón de menú Abrir en la barra de herramientas de hello (tres líneas horizontales en la esquina superior derecha de hello), haga clic en los complementos, buscar con la palabra clave "ClickOnce", elija una de las extensiones de ClickOnce hello e instalarlo.
* Hola de uso **el programa de instalación Manual** vínculo se muestra en hello misma hoja en el portal de Hola. Use este archivo de instalación de toodownload de enfoque y ejecutarlo manualmente. Tras instalación hello es correcta, se mostrará el cuadro de diálogo de configuración de puerta de enlace de administración de datos de Hola. Hola copia **clave** de pantalla de portal de bienvenida y utilizar en hello configuration manager toomanually registrar puerta de enlace de hello con servicio Hola.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Problema: No tooconnect tooon local SQL Server
Iniciar **Administrador de configuración de Data Management Gateway** Hola máquina de puerta de enlace y usar hello **solución de problemas** ficha tootest Hola conexión tooSQL Server de la máquina de puerta de enlace de Hola. Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Problema: Los segmentos de entrada están en el estado En espera de forma permanente.
segmentos de Hello pudieron estar en **espera** estado debido a motivos de toovarious. Uno de los motivos comunes de hello es ese hello **externo** propiedad no se establece demasiado**true**. Cualquier conjunto de datos que es ámbito producidos Hola fuera de Data Factory de Azure debe marcarse con **externo** propiedad. Esta propiedad indica que Hola datos externos y no con el respaldo de las canalizaciones de factoría de datos de Hola. segmentos de datos de Hola se marcan como **listo** una vez Hola datos están disponibles en tienda respectiva Hola.

Vea Hola siguiente ejemplo para el uso de Hola de hello **externo** propiedad. Opcionalmente, puede especificar **externalData*** al establecer tootrue externo.

Consulte el artículo [Conjuntos de datos](data-factory-create-datasets.md) para obtener más información sobre esta propiedad.

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

tooresolve Hola error, agregue hello **externo** hello opcional y la propiedad **externalData** sección toohello definición de JSON de tabla de entrada de Hola y vuelva a crear tabla Hola.

### <a name="problem-hybrid-copy-operation-fails"></a>Problema: la operación de copia híbrida produce un error.
Vea [solucionar problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para pasos tootroubleshoot problemas con la copia de un dato local almacenan utilizando Hola Data Management Gateway.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Problema: El aprovisionamiento de HDInsight a petición produce un error
Cuando se utiliza un servicio vinculado de tipo HDInsightOnDemand, deberá toospecify un linkedServiceName que señala tooan almacenamiento de blobs de Azure. Servicio de factoría de datos usa este almacenamiento toostore registros y archivos auxiliares para el clúster de HDInsight a petición.  Se produce un error en ocasiones, el aprovisionamiento de un clúster de HDInsight a petición con hello siguiente error:

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Este error suele indicar que no es ubicación Hola de cuenta de almacenamiento de hello especificada en hello linkedServiceName Hola ubicación donde sucede el aprovisionamiento de hello HDInsight del centro de datos mismas. Ejemplo: si su factoría de datos es zona horaria del Pacífico occidental y Hola almacenamiento de Azure está en UU, Hola a petición se produce un error aprovisionamiento zona horaria del Pacífico occidental.

Además, hay una segunda propiedad de JSON additionalLinkedServiceNames, donde puede se especifiquen cuentas de almacenamiento adicionales en HDInsight a petición. Las cuentas de almacenamiento vinculado adicional deben ser Hola se produce un error en la misma ubicación que el clúster de HDInsight de hello, o bien con hello mismo error.

### <a name="problem-custom-net-activity-fails"></a>Problema: La actividad de .NET personalizada produce un error
Consulte [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) (Depurar una canalización con una actividad personalizada) para obtener pasos detallados.

## <a name="use-azure-portal-tootroubleshoot"></a>Usar tootroubleshoot de portal de Azure
### <a name="using-portal-blades"></a>Uso de hojas del Portal
Consulte [Supervisión de la canalización](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) para ver los pasos.

### <a name="using-monitor-and-manage-app"></a>Uso de la aplicación de supervisión y administración
Consulte [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) (Supervisar y administrar canalizaciones de Data Factory con una aplicación de supervisión y administración) para obtener más información.

## <a name="use-azure-powershell-tootroubleshoot"></a>Usar tootroubleshoot de PowerShell de Azure
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Usar PowerShell de Azure tootroubleshoot un error
Consulte [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) (Supervisar canalizaciones de Data Factory con Azure PowerShell) para obtener más información.

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
