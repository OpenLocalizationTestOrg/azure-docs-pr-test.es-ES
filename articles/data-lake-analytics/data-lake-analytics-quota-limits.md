---
title: "Límites de cuota de Data Lake análisis aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se limita tooadjust y aumento de cuota en las cuentas de Azure datos Lake Analytics (ADLA)."
services: data-lake-analytics
keywords: "Análisis con Azure Data Lake"
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Límites de cuota de Azure Data Lake Analytics

Obtenga información acerca de cómo se limita tooadjust y aumento de cuota en las cuentas de Azure datos Lake Analytics (ADLA). Conocer estos límites puede ayudarle a comprender su comportamiento de trabajos de U-SQL. Todos los límites de cuota son suaves, por lo que puede aumentar los límites máximos Hola llegando toous.

## <a name="azure-subscriptions-limits"></a>Límites de las suscripciones de Azure

**Número máximo de cuentas de ADLA por suscripción:** 5

 Se trata de hello número máximo de cuentas ADLA que puede crear por suscripción. Si trata de cuenta ADLA toocreate un sexto, obtendrá un error "Se ha alcanzado Hola número máximo de cuentas de análisis de Data Lake permitidas (5) en la región con nombre de la suscripción". En este caso, elimine las cuentas de ADLA sin usar, o llegar toous por [abrir una incidencia de soporte técnico](#increase-maximum-quota-limits).

## <a name="adla-account-limits"></a>Límites de la cuenta de ADLA

**Número máximo de unidades de análisis por cuenta:** 250

Se trata de número máximo de Hola de AUs que pueden ejecutarse simultáneamente en su cuenta. Si el total de unidades de análisis entre todos los trabajos supera este límite, los trabajos nuevos se ponen en cola automáticamente. Por ejemplo:

* Si tiene sólo un trabajo ejecuta con 250 AUs, cuando se envía un segundo trabajo espera en cola de trabajos de hello hasta que se complete el primer trabajo de Hola.
* Si ya tiene cinco trabajos en ejecución y cada uno está usando 50 AUs, cuando se envía un trabajo sexto que necesita 20 AUs espera en cola de trabajos de hello hasta que hay 20 AUs disponibles.

**Número máximo de trabajos de U-SQL simultáneos por cuenta:** 20

Se trata de hello número máximo de trabajos que pueden ejecutarse simultáneamente en su cuenta. Por encima de este valor, los últimos trabajos permanecen en la cola automáticamente.

## <a name="adjust-adla-quota-limits-per-account"></a>Ajuste de los límites de cuota de ADLA por cuenta

1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Elija una cuenta de ADLA existente.
3. Haga clic en **Propiedades**.
4. Ajustar **paralelismo** y **trabajos simultáneos** toosuit sus necesidades.

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>Aumento de los límites de cuota máximos

1. Cree una petición de soporte técnico en Azure Portal.

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. Seleccione el tipo de problema de hello **cuota**.
3. Seleccione su **Suscripción** (asegúrese de que no sea una suscripción de "prueba").
4. Seleccione el tipo de cuota **Data Lake Analytics**.

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. En la hoja de problema de hello, explique el límite de incremento solicitado con **detalles** de por qué necesita esta capacidad adicional.

    ![Hoja del portal de Análisis de Azure Data Lake](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. Compruebe la información de contacto y crear solicitud de soporte técnico de Hola.

Microsoft revisa la solicitud e intenta tooaccommodate necesidades de su empresa tan pronto como sea posible.

## <a name="next-steps"></a>Pasos siguientes

* [Información general de Análisis de Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Administración de Análisis de Azure Data Lake mediante Azure Powershell](data-lake-analytics-manage-use-powershell.md)
* [Supervisión y solución de problemas de trabajos de Azure Data Lake Analytics con Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
