---
title: "aaaEnable automática para la optimización de base de datos de SQL de Azure | Documentos de Microsoft"
description: "Puede habilitar fácilmente el ajuste automático en Azure SQL Database."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="f1f6d-103">Habilitación del ajuste automático</span><span class="sxs-lookup"><span data-stu-id="f1f6d-103">Enable automatic tuning</span></span>

<span data-ttu-id="f1f6d-104">La base de datos de SQL Azure es un servicio de datos administrados automáticamente que supervisa las consultas e identifica que se puedan realizar tooimprove rendimiento de la carga de trabajo de acción de hello constantemente.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="f1f6d-105">Puede revisar las recomendaciones y aplicarlas manualmente o dejar que Azure SQL Database aplique automáticamente acciones correctoras, lo que se conoce como **modo de ajuste automático**.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="f1f6d-106">El ajuste automático se puede habilitar en el nivel de base de datos de Hola o de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="f1f6d-107">Habilitación del ajuste automático en servidor</span><span class="sxs-lookup"><span data-stu-id="f1f6d-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="f1f6d-108">tooenable automática para la optimización en el servidor de base de datos de SQL Azure, navegue toohello server en Azure portal y, a continuación, seleccione **el ajuste automático** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="f1f6d-109">Seleccione Hola opciones de optimización automática que desee tooenable y seleccione **aplicar**:</span><span class="sxs-lookup"><span data-stu-id="f1f6d-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![Server](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="f1f6d-111">Opciones en el servidor de optimización automáticas son bases de datos de tooall aplicados en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="f1f6d-112">De forma predeterminada, todas las bases de datos heredan la configuración de Hola de su servidor principal, pero esto puede sustituirse y especificar individualmente para cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="f1f6d-113">Configuración del ajuste automático en la base de datos</span><span class="sxs-lookup"><span data-stu-id="f1f6d-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="f1f6d-114">Hola Azure habilita portal tooindividually especifique la configuración de optimización automática de hello en cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="f1f6d-115">Hola la recomendación general es toomanage Hola configuración automática de optimización en el nivel de servidor hello así mismos valores de configuración se pueden aplicar en cada base de datos automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="f1f6d-116">Configurar el ajuste automático en una base de datos individual si la base de datos de hello es diferente que otros miembros de Hola mismo servidor.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="f1f6d-117">tooenable automática para la optimización en una sola base de datos, navegar por base de datos de toohello en hello portal de Azure y, a continuación y seleccione **el ajuste automático**.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="f1f6d-118">Puede configurar una sola base de datos tooinherit Hola de base de datos de hello seleccionando la casilla de verificación de Hola o puede especificar configuración de Hola para una base de datos por separado.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![Base de datos](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="f1f6d-120">Cuando haya seleccionado la configuración adecuada, haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1f6d-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f1f6d-121">Next steps</span></span>
* <span data-ttu-id="f1f6d-122">Hola de lectura [artículo optimización automática](sql-database-automatic-tuning.md) toolearn más información sobre el ajuste automático y cómo puede ayudarle a mejorar su rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="f1f6d-123">Consulte [Recomendaciones de rendimiento](sql-database-advisor.md) para ver información general sobre las recomendaciones de rendimiento de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="f1f6d-124">Vea [información de rendimiento de consultas](sql-database-query-performance.md) toolearn acerca de cómo ver el impacto en el rendimiento de las consultas principales Hola.</span><span class="sxs-lookup"><span data-stu-id="f1f6d-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
