---
title: "ensamblados de aaaDevelop U-SQL para trabajos de análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se usa y reutiliza en los análisis de Data Lake trabajos toodevelop ensamblados toobe. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="7cb76-103">Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7cb76-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="7cb76-104">Obtenga información acerca de cómo tooturn código subyacente en ensamblados toobe usa y volver a usar en trabajos de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7cb76-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="7cb76-105">U-SQL hace fácil tooadd su propio personalizado de código en lenguajes. NET, como C#, Visual Basic.NET o F #.</span><span class="sxs-lookup"><span data-stu-id="7cb76-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="7cb76-106">Incluso puede implementar su propio toosupport en tiempo de ejecución de otros lenguajes.</span><span class="sxs-lookup"><span data-stu-id="7cb76-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="7cb76-107">código personalizado de Hello más fácil manera toouse es toouse hello Data Lake Tools para capacidades de código subyacente de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7cb76-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="7cb76-108">Para obtener más información, consulte [Tutorial: Desarrollo de scripts U-SQL mediante Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7cb76-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="7cb76-109">Sin embargo, usar código subyacente tiene algunas desventajas:</span><span class="sxs-lookup"><span data-stu-id="7cb76-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="7cb76-110">código fuente de Hello obtiene cargado para el envío de cada secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="7cb76-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="7cb76-111">El código subyacente no se puede compartir con otros trabajos.</span><span class="sxs-lookup"><span data-stu-id="7cb76-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="7cb76-112">tooaddress estas desventajas, puede convertir el código subyacente en ensamblados y registrar el catálogo de análisis de Data Lake de hello ensamblados toohello.</span><span class="sxs-lookup"><span data-stu-id="7cb76-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cb76-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7cb76-113">Prerequisites</span></span>
* <span data-ttu-id="7cb76-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 Update 4 o Visual Studio 2012 con Visual C ++ Instalado</span><span class="sxs-lookup"><span data-stu-id="7cb76-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="7cb76-115">SDK de Microsoft Azure para .NET versión 2.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7cb76-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="7cb76-116">Instalar mediante el instalador de plataforma Web de Hola o instalador de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7cb76-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="7cb76-117">Una cuenta de Análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="7cb76-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="7cb76-118">[Introducción a Azure Data Lake Analytics mediante Azure Portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7cb76-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="7cb76-119">Vaya a través de hello [empezar a trabajar con Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7cb76-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="7cb76-120">Conectar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7cb76-120">Connect tooAzure.</span></span>
* <span data-ttu-id="7cb76-121">Cargar datos de origen de hello, consulte [empezar a trabajar con Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7cb76-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="7cb76-122">Desarrollo de ensamblados para U-SQL</span><span class="sxs-lookup"><span data-stu-id="7cb76-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="7cb76-123">**toocreate y enviar un trabajo de SQL U**</span><span class="sxs-lookup"><span data-stu-id="7cb76-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="7cb76-124">De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7cb76-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="7cb76-125">Expanda **instalado**, **plantillas**, **Azure Data Lake**, **U-SQL(ADLA)**, seleccione hello **biblioteca de clases (para U-SQL Aplicación)** plantilla y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7cb76-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="7cb76-126">Escriba el código en Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="7cb76-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="7cb76-127">Hola aquí te mostramos un ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="7cb76-127">hello following is a code sample.</span></span>

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. <span data-ttu-id="7cb76-128">Haga clic en hello **generar** menú y, a continuación, haga clic en **generar solución** toocreate Hola dll.</span><span class="sxs-lookup"><span data-stu-id="7cb76-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="7cb76-129">Registro de ensamblados</span><span class="sxs-lookup"><span data-stu-id="7cb76-129">Register assemblies</span></span>

<span data-ttu-id="7cb76-130">Consulte [Uso del catálogo de Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="7cb76-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="7cb76-131">Usar ensamblados de Hola</span><span class="sxs-lookup"><span data-stu-id="7cb76-131">Use hello assemblies</span></span>

<span data-ttu-id="7cb76-132">Vea [usar hello Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="7cb76-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7cb76-133">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="7cb76-133">See also</span></span>
* [<span data-ttu-id="7cb76-134">Introducción a Análisis de Data Lake mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cb76-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="7cb76-135">Empezar a trabajar con análisis de Data Lake con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7cb76-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="7cb76-136">Uso de Data Lake Tools for Visual Studio para desarrollar aplicaciones de U-SQL</span><span class="sxs-lookup"><span data-stu-id="7cb76-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="7cb76-137">Uso del catálogo de Data Lake Analytics (U-SQL)</span><span class="sxs-lookup"><span data-stu-id="7cb76-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="7cb76-138">Usar hello Azure Data Lake Tools para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7cb76-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
