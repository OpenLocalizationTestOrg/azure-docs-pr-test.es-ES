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
# <a name="enable-automatic-tuning"></a>Habilitación del ajuste automático

La base de datos de SQL Azure es un servicio de datos administrados automáticamente que supervisa las consultas e identifica que se puedan realizar tooimprove rendimiento de la carga de trabajo de acción de hello constantemente. Puede revisar las recomendaciones y aplicarlas manualmente o dejar que Azure SQL Database aplique automáticamente acciones correctoras, lo que se conoce como **modo de ajuste automático**. El ajuste automático se puede habilitar en el nivel de base de datos de Hola o de servidor de Hola.

## <a name="enable-automatic-tuning-on-server"></a>Habilitación del ajuste automático en servidor

tooenable automática para la optimización en el servidor de base de datos de SQL Azure, navegue toohello server en Azure portal y, a continuación, seleccione **el ajuste automático** en el menú de Hola. Seleccione Hola opciones de optimización automática que desee tooenable y seleccione **aplicar**:

![Server](./media/sql-database-automatic-tuning-enable/server.png)

Opciones en el servidor de optimización automáticas son bases de datos de tooall aplicados en el servidor de Hola. De forma predeterminada, todas las bases de datos heredan la configuración de Hola de su servidor principal, pero esto puede sustituirse y especificar individualmente para cada base de datos.

## <a name="configure-automatic-tuning-on-database"></a>Configuración del ajuste automático en la base de datos

Hola Azure habilita portal tooindividually especifique la configuración de optimización automática de hello en cada base de datos.

> [!NOTE]
> Hola la recomendación general es toomanage Hola configuración automática de optimización en el nivel de servidor hello así mismos valores de configuración se pueden aplicar en cada base de datos automáticamente. Configurar el ajuste automático en una base de datos individual si la base de datos de hello es diferente que otros miembros de Hola mismo servidor.
>

tooenable automática para la optimización en una sola base de datos, navegar por base de datos de toohello en hello portal de Azure y, a continuación y seleccione **el ajuste automático**. Puede configurar una sola base de datos tooinherit Hola de base de datos de hello seleccionando la casilla de verificación de Hola o puede especificar configuración de Hola para una base de datos por separado.

![Base de datos](./media/sql-database-automatic-tuning-enable/database.png)

Cuando haya seleccionado la configuración adecuada, haga clic en **Aplicar**.

## <a name="next-steps"></a>Pasos siguientes
* Hola de lectura [artículo optimización automática](sql-database-automatic-tuning.md) toolearn más información sobre el ajuste automático y cómo puede ayudarle a mejorar su rendimiento.
* Consulte [Recomendaciones de rendimiento](sql-database-advisor.md) para ver información general sobre las recomendaciones de rendimiento de Azure SQL Database.
* Vea [información de rendimiento de consultas](sql-database-query-performance.md) toolearn acerca de cómo ver el impacto en el rendimiento de las consultas principales Hola.
