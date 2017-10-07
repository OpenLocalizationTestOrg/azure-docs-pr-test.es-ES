---
title: "Análisis de transmisiones de Azure con el almacenamiento de datos de SQL aaaUse | Documentos de Microsoft"
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
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="7fc89-103">Uso de Análisis de transmisiones de Azure con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="7fc89-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="7fc89-104">Análisis de transmisiones de Azure es un servicio completamente administrado, lo que proporciona el procesamiento de eventos complejos de baja latencia, alta disponibilidad y escalable en transmisión de datos en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fc89-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="7fc89-105">Aprenderá los conceptos básicos de hello leyendo [Introducción tooAzure análisis de transmisiones][Introduction tooAzure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="7fc89-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="7fc89-106">A continuación, aprenderá cómo toocreate una solución end-to-end con análisis de transmisiones siguiendo Hola [Introducción al uso de análisis de transmisiones de Azure] [ Get started using Azure Stream Analytics] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7fc89-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="7fc89-107">En este artículo, aprenderá cómo toouse el almacenamiento de datos de SQL Azure base de datos como un receptor de salida para los trabajos de análisis de secuencia.</span><span class="sxs-lookup"><span data-stu-id="7fc89-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fc89-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7fc89-108">Prerequisites</span></span>
<span data-ttu-id="7fc89-109">En primer lugar, recorra Hola siguiendo los pasos de hello [Introducción al uso de análisis de transmisiones de Azure] [ Get started using Azure Stream Analytics] tutorial.</span><span class="sxs-lookup"><span data-stu-id="7fc89-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="7fc89-110">Creación de una entrada de Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="7fc89-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="7fc89-111">Configuración e inicio de la aplicación del generador de eventos</span><span class="sxs-lookup"><span data-stu-id="7fc89-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="7fc89-112">Aprovisionamiento de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7fc89-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="7fc89-113">Especificación de una consulta y entrada de trabajo</span><span class="sxs-lookup"><span data-stu-id="7fc89-113">Specify job input and query</span></span>

<span data-ttu-id="7fc89-114">Luego cree una base de datos de Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="7fc89-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="7fc89-115">Especifique la salida de trabajo: base de datos de Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="7fc89-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="7fc89-116">Paso 1</span><span class="sxs-lookup"><span data-stu-id="7fc89-116">Step 1</span></span>
<span data-ttu-id="7fc89-117">En el trabajo de análisis de transmisiones, haga clic en **salida** de arriba Hola de página de hello y, a continuación, haga clic en **agregar salida**.</span><span class="sxs-lookup"><span data-stu-id="7fc89-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="7fc89-118">Paso 2</span><span class="sxs-lookup"><span data-stu-id="7fc89-118">Step 2</span></span>
<span data-ttu-id="7fc89-119">Seleccione Base de datos SQL y haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="7fc89-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="7fc89-120">Paso 3</span><span class="sxs-lookup"><span data-stu-id="7fc89-120">Step 3</span></span>
<span data-ttu-id="7fc89-121">Escriba Hola después los valores en la página siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="7fc89-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="7fc89-122">*Alias de salida*: escriba un nombre descriptivo para esta salida de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7fc89-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="7fc89-123">*Suscripción*:</span><span class="sxs-lookup"><span data-stu-id="7fc89-123">*Subscription*:</span></span>
  * <span data-ttu-id="7fc89-124">Si la base de datos de almacenamiento de datos de SQL está en hello misma suscripción que el trabajo de análisis de transmisiones de hello, seleccione Usar base de datos SQL de la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="7fc89-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="7fc89-125">Si la base de datos está en una suscripción diferente, seleccione Usar la base de datos SQL de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="7fc89-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="7fc89-126">*Base de datos*: especifique Hola nombre de una base de datos de destino.</span><span class="sxs-lookup"><span data-stu-id="7fc89-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="7fc89-127">*Nombre del servidor*: especificar Hola nombre del servidor de base de datos de Hola que acaba de especificar.</span><span class="sxs-lookup"><span data-stu-id="7fc89-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="7fc89-128">Ya puede utilizarla hello toofind de Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="7fc89-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="7fc89-129">*Nombre de usuario*: especifique Hola de nombre de usuario de una cuenta que tenga permisos de escritura para la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fc89-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="7fc89-130">*Contraseña*: proporcionar contraseña Hola Hola cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="7fc89-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="7fc89-131">*Tabla*: especifique el nombre de Hola de tabla de destino de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fc89-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="7fc89-132">Paso 4</span><span class="sxs-lookup"><span data-stu-id="7fc89-132">Step 4</span></span>
<span data-ttu-id="7fc89-133">Haga clic en tooadd de botón de comprobación de hello esta salida del trabajo y tooverify que análisis de transmisiones puede conectar correctamente la base de datos de toohello.</span><span class="sxs-lookup"><span data-stu-id="7fc89-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="7fc89-134">Cuando se realiza correctamente la base de datos de hello conexión toohello, verá una notificación en la parte inferior de hello del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fc89-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="7fc89-135">Puede hacer clic en Probar conexión en base de datos de hello inferior tootest Hola conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="7fc89-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fc89-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7fc89-136">Next steps</span></span>
<span data-ttu-id="7fc89-137">Para obtener información general sobre la integración, consulte la [información general de la integración de SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="7fc89-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="7fc89-138">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="7fc89-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
