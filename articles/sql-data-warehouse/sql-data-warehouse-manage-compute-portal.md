---
title: "capacidad de almacenamiento de datos de SQL Azure (portal de Azure) de cálculo aaaManage | Documentos de Microsoft"
description: Capacidad de proceso de tareas del portal Azure toomanage. Escalado de los recursos de proceso ajustando DWU. O bien, puede pausar y reanudar los costos de toosave de recursos de proceso.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (Portal de Azure)
> [!div class="op_single_selector"]
> * [Información general](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>Escalado de la potencia de proceso
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

recursos de proceso de toochange:

1. Abra hello [portal de Azure][Azure portal], abra la base de datos y haga clic en **escala**.

    ![Haga clic en Escala][1]
2. En la hoja de la escala de hello, mover regulador Hola a la izquierda o hacia la derecha toochange configuración de la unidad de Hola.

    ![Mueva el control deslizante][2]
3. Haga clic en **Save**. Aparece un mensaje de confirmación. Haga clic en **Sí** tooconfirm o **no** toocancel.

    ![Haga clic en Guardar][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Pausa del proceso
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause una base de datos:

1. Abra hello [portal de Azure] [ Azure portal] y abra la base de datos. Tenga en cuenta que Hola estado es **Online**.

    ![Estado En línea][6]
2. Haga clic en recursos de proceso y memoria de toosuspend, **pausa**, y, a continuación, aparece un mensaje de confirmación. Haga clic en **Sí** tooconfirm o **no** toocancel.

    ![Confirme la pausa][7]
3. Durante el almacenamiento de datos SQL es inicio de base de datos de hello, estado de hello es **pausar**.
4. Cuando el estado de hello es **en pausa**, se realiza la operación de pausa de Hola y se ya no se le cobrará por a Dwu.

    ![Estado de pausa][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Reanudación del proceso
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume una base de datos:

1. Abra hello [portal de Azure] [ Azure portal] y abra la base de datos. Tenga en cuenta que Hola estado es **en pausa**.

    ![Base de datos de pausa][4]
2. Haga clic en el base de datos de hello tooresume **iniciar**, y, a continuación, aparece un mensaje de confirmación. Haga clic en **Sí** tooconfirm o **no** toocancel.

    ![Confirme la reanudación][5]
3. Durante el almacenamiento de datos SQL es inicio de base de datos de hello, el estado de hello es "Reanudar".
4. Cuando el estado de hello es **en línea**, base de datos de hello está listo.

    ![Estado En línea][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Pasos siguientes
Para más información, consulte [Introducción a la administración][Management overview].

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
