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
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="a2adf-103">Introducción a Azure Data Lake Analytics mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2adf-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="a2adf-104">Obtenga información acerca de cómo toouse toocreate análisis de Azure Data Lake de Azure PowerShell de cuentas y, a continuación, enviar y ejecutar trabajos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a2adf-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="a2adf-105">Para obtener más información acerca de Análisis de Data Lake, consulte [Información general sobre Análisis de Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2adf-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2adf-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a2adf-106">Prerequisites</span></span>

<span data-ttu-id="a2adf-107">Antes de comenzar este tutorial, debe tener Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="a2adf-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="a2adf-108">**Una cuenta de Análisis de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="a2adf-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="a2adf-109">Consulte [Introducción a Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="a2adf-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="a2adf-110">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a2adf-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="a2adf-111">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2adf-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="a2adf-112">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="a2adf-112">Log in tooAzure</span></span>

<span data-ttu-id="a2adf-113">En este tutorial se asume que sabe usar Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2adf-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="a2adf-114">En concreto, debe tooknow cómo toolog en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a2adf-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="a2adf-115">Vea hello [empezar a trabajar con Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) si necesita ayuda.</span><span class="sxs-lookup"><span data-stu-id="a2adf-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="a2adf-116">toolog con un nombre de suscripción:</span><span class="sxs-lookup"><span data-stu-id="a2adf-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="a2adf-117">En lugar del nombre de la suscripción de hello, también puede utilizar un toolog de Id. de suscripción en:</span><span class="sxs-lookup"><span data-stu-id="a2adf-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="a2adf-118">Si se realiza correctamente, la salida de hello de este comando es similar Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="a2adf-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="a2adf-119">Preparar el tutorial de Hola</span><span class="sxs-lookup"><span data-stu-id="a2adf-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="a2adf-120">fragmentos de código de PowerShell de Hello en este tutorial usa estas variables toostore esta información:</span><span class="sxs-lookup"><span data-stu-id="a2adf-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="a2adf-121">Información acerca de una cuenta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a2adf-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="a2adf-122">Envío de un trabajo de U-SQL</span><span class="sxs-lookup"><span data-stu-id="a2adf-122">Submit a U-SQL job</span></span>

<span data-ttu-id="a2adf-123">Crear una secuencia de comandos de PowerShell variable toohold Hola U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a2adf-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

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

<span data-ttu-id="a2adf-124">Enviar el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2adf-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="a2adf-125">Como alternativa, podría guardar script de Hola como un archivo y enviar con el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a2adf-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="a2adf-126">Obtener estado de Hola de un trabajo específico.</span><span class="sxs-lookup"><span data-stu-id="a2adf-126">Get hello status of a specific job.</span></span> <span data-ttu-id="a2adf-127">Seguir usando este cmdlet hasta que vea, se realiza el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a2adf-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="a2adf-128">En lugar de llamar a Get-AdlAnalyticsJob una y otra vez hasta que finalice un trabajo, puede usar hello AdlJob espera cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a2adf-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="a2adf-129">Descargue el archivo de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="a2adf-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="a2adf-130">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a2adf-130">See also</span></span>
* <span data-ttu-id="a2adf-131">Hola toosee mismo tutorial con otras herramientas, haga clic en los selectores de pestaña hello en la parte superior de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="a2adf-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="a2adf-132">toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a2adf-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="a2adf-133">Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a2adf-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
