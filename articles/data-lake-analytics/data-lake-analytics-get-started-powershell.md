---
title: "aaaGet a trabajar con análisis de Data Lake de Azure con PowerShell de Azure | Documentos de Microsoft"
description: "Usar toocreate una cuenta de análisis de Data Lake de Azure PowerShell, crear un trabajo de análisis de Data Lake mediante SQL U y enviar el trabajo de Hola. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Introducción a Azure Data Lake Analytics mediante Azure PowerShell
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Obtenga información acerca de cómo toouse toocreate análisis de Azure Data Lake de Azure PowerShell de cuentas y, a continuación, enviar y ejecutar trabajos de U-SQL. Para obtener más información acerca de Análisis de Data Lake, consulte [Información general sobre Análisis de Azure Data Lake](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar este tutorial, debe tener Hola siguiente información:

* **Una cuenta de Análisis de Azure Data Lake**. Consulte [Introducción a Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Una estación de trabajo con Azure PowerShell**. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

En este tutorial se asume que sabe usar Azure PowerShell. En concreto, debe tooknow cómo toolog en tooAzure. Vea hello [empezar a trabajar con Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) si necesita ayuda.

toolog con un nombre de suscripción:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

En lugar del nombre de la suscripción de hello, también puede utilizar un toolog de Id. de suscripción en:

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

Si se realiza correctamente, la salida de hello de este comando es similar Hola siguiente texto:

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Preparar el tutorial de Hola

fragmentos de código de PowerShell de Hello en este tutorial usa estas variables toostore esta información:

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Información acerca de una cuenta de Data Lake Analytics

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>Envío de un trabajo de U-SQL

Crear una secuencia de comandos de PowerShell variable toohold Hola U-SQL.

```
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();

"@
```

Enviar el script de Hola.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

Como alternativa, podría guardar script de Hola como un archivo y enviar con el siguiente comando de hello:

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


Obtener estado de Hola de un trabajo específico. Seguir usando este cmdlet hasta que vea, se realiza el trabajo de Hola.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

En lugar de llamar a Get-AdlAnalyticsJob una y otra vez hasta que finalice un trabajo, puede usar hello AdlJob espera cmdlet.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Descargue el archivo de salida de hello.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>Otras referencias
* Hola toosee mismo tutorial con otras herramientas, haga clic en los selectores de pestaña hello en la parte superior de Hola de página Hola.
* toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).
