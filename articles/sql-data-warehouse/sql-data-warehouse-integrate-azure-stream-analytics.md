---
title: Uso de Azure Stream Analytics con SQL Data Warehouse | Microsoft Docs
description: "Sugerencias para usar Análisis de transmisiones de Azure con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 14783f0464764a11d7f03a5db1c2d63728a4cb50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="44dd7-103">Uso de Análisis de transmisiones de Azure con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="44dd7-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="44dd7-104">Análisis de transmisiones de Azure es un servicio totalmente administrado que proporciona un procesamiento completo de eventos de baja latencia, alta disponibilidad y escalable a través el streaming de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="44dd7-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="44dd7-105">Para aprender los conceptos básicos, lea la [introducción a Azure Stream Analytics][Introduction to Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="44dd7-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="44dd7-106">Después puede aprender a crear una solución de un extremo a otro con Stream Analytics siguiendo el tutorial de [introducción al uso de Azure Stream Analytics][Get started using Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="44dd7-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="44dd7-107">En este artículo, aprenderá a usar la base de datos de Almacenamiento de datos SQL de Azure como receptor de salida para los trabajos de Análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="44dd7-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44dd7-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="44dd7-108">Prerequisites</span></span>
<span data-ttu-id="44dd7-109">En primer lugar, ejecute los pasos siguientes del tutorial de [introducción al uso de Azure Stream Analytics][Get started using Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="44dd7-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="44dd7-110">Creación de una entrada de Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="44dd7-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="44dd7-111">Configuración e inicio de la aplicación del generador de eventos</span><span class="sxs-lookup"><span data-stu-id="44dd7-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="44dd7-112">Aprovisionamiento de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="44dd7-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="44dd7-113">Especificación de una consulta y entrada de trabajo</span><span class="sxs-lookup"><span data-stu-id="44dd7-113">Specify job input and query</span></span>

<span data-ttu-id="44dd7-114">Luego cree una base de datos de Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="44dd7-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="44dd7-115">Especifique la salida de trabajo: base de datos de Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="44dd7-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="44dd7-116">Paso 1</span><span class="sxs-lookup"><span data-stu-id="44dd7-116">Step 1</span></span>
<span data-ttu-id="44dd7-117">En el trabajo de Stream Analytics, haga clic en **SALIDA** en la parte superior de la página y luego en **AGREGAR SALIDA**.</span><span class="sxs-lookup"><span data-stu-id="44dd7-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="44dd7-118">Paso 2</span><span class="sxs-lookup"><span data-stu-id="44dd7-118">Step 2</span></span>
<span data-ttu-id="44dd7-119">Seleccione Base de datos SQL y haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="44dd7-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="44dd7-120">Paso 3</span><span class="sxs-lookup"><span data-stu-id="44dd7-120">Step 3</span></span>
<span data-ttu-id="44dd7-121">Escriba estos valores en la página siguiente:</span><span class="sxs-lookup"><span data-stu-id="44dd7-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="44dd7-122">*Alias de salida*: escriba un nombre descriptivo para esta salida de trabajo.</span><span class="sxs-lookup"><span data-stu-id="44dd7-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="44dd7-123">*Suscripción*:</span><span class="sxs-lookup"><span data-stu-id="44dd7-123">*Subscription*:</span></span>
  * <span data-ttu-id="44dd7-124">Si la base de datos del Almacenamiento de datos SQL está en la misma suscripción que el trabajo de Análisis de transmisiones, seleccione Usar la base de datos SQL de la suscripción actual".</span><span class="sxs-lookup"><span data-stu-id="44dd7-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="44dd7-125">Si la base de datos está en una suscripción diferente, seleccione Usar la base de datos SQL de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="44dd7-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="44dd7-126">*Base de datos*: especifique el nombre de una base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="44dd7-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="44dd7-127">*Nombre del servidor*: especifique el nombre del servidor para la base de datos especificada.</span><span class="sxs-lookup"><span data-stu-id="44dd7-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="44dd7-128">Para encontrarlo, puede usar el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="44dd7-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="44dd7-129">*Nombre de usuario*: especifique el nombre de usuario de una cuenta que tenga permisos de escritura para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="44dd7-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="44dd7-130">*Contraseña*: proporcione la contraseña de la cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="44dd7-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="44dd7-131">*Tabla*: especifique el nombre de la tabla de destino en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="44dd7-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="44dd7-132">Paso 4</span><span class="sxs-lookup"><span data-stu-id="44dd7-132">Step 4</span></span>
<span data-ttu-id="44dd7-133">Haga clic en el botón de comprobación para agregar esta salida de trabajo y comprobar que Análisis de transmisiones puede conectarse correctamente a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="44dd7-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="44dd7-134">Cuando la conexión a la base de datos se realice correctamente, verá una notificación en la parte inferior del portal.</span><span class="sxs-lookup"><span data-stu-id="44dd7-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="44dd7-135">Puede hacer clic en Probar conexión en la parte inferior para probar la conexión con la base de datos.</span><span class="sxs-lookup"><span data-stu-id="44dd7-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44dd7-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44dd7-136">Next steps</span></span>
<span data-ttu-id="44dd7-137">Para obtener información general sobre la integración, consulte la [información general de la integración de SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="44dd7-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="44dd7-138">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="44dd7-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
