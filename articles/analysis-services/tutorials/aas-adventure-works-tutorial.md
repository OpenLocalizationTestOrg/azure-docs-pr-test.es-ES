---
title: aaa "Azure Analysis Services de Adventure Works Tutorial | Documentos de Microsoft"
description: Presenta el tutorial de Adventure Works de Hola para Azure Analysis Services
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services: Tutorial de Adventure Works

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Este tutorial ofrece lecciones sobre cómo toocreate e implementar un modelo tabular en el nivel de compatibilidad de hello 1400 mediante [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Si está nuevos servicios de tooAnalysis y creación de modelos tabular, completar este tutorial es hello toolearn de manera más rápida de cómo toocreate e implementar un modelo tabular básico. Una vez que tenga requisitos previos de hello en contexto, que se debe tardar entre dos toothree horas toocomplete.  
  
## <a name="what-you-learn"></a>Conocimientos que adquirirá   
  
-   Modo de proyecto toocreate un nuevo modelo tabular en hello **nivel de compatibilidad de 1400** en SSDT.
  
-   ¿Cómo tooimport datos desde una base de datos relacional en un proyecto de modelo tabular.  
  
-   ¿Cómo toocreate y administrar las relaciones entre tablas en el modelo de Hola.  
  
-   Cómo toocreate calcula las columnas, medidas e indicadores de rendimiento de clave que le ayudan a los usuarios analizan métricas empresariales críticas.  
  
-   ¿Cómo toocreate y administrar perspectivas y jerarquías que ayudan a los usuarios más fácil examinar los datos de modelo proporcionando funciones empresariales y puntos de vista específicos de la aplicación.  
  
-   ¿Cómo toocreate particiones que dividir datos de la tabla en piezas lógicas más pequeñas que pueden procesar de forma independiente de otras particiones.  
  
-   Cómo toosecure modelo de objetos y datos mediante la creación de roles con miembros de usuario.  
  
-   ¿Cómo toodeploy un modelo tabular tooan **Azure Analysis Services** server o un servidor de Analysis Services de SQL Server de 2017 local.  
  
## <a name="prerequisites"></a>Requisitos previos  
toocomplete este tutorial, necesita:  
  
-   Un Azure Analysis Services o 2017 Analysis Services de SQL Server a la instancia toodeploy su modelo. Registrarse para obtener una [prueba gratuita de Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) y [crear un servidor](../analysis-services-create-server.md). O bien, iniciar sesión y descargar [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp). 

-   Un almacén de datos de SQL Server o el almacenamiento de datos de SQL Azure con hello [base de datos de ejemplo de AdventureWorksDW2014](http://go.microsoft.com/fwlink/?LinkID=335807). Esta base de datos de ejemplo incluye Hola datos necesarios toocomplete este tutorial. Descargar [ediciones gratuitas de SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). O bien, registrarse para obtener una [prueba gratuita de Azure SQL Database](https://azure.microsoft.com/services/sql-database/). 

    **Importante:** si instalar la base de datos de ejemplo de Hola en un servidor local de SQL, y desea implementar el servidor de Analysis Services de Azure de modelo tooan, un [puerta de enlace de datos local](../analysis-services-gateway.md) es necesario.

-   versión más reciente de Hola de [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   versión más reciente de Hola de [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Una aplicación cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) o Excel. 

## <a name="scenario"></a>Escenario  
Este tutorial se basa en Adventure Works Cycles, una compañía ficticia. Adventure Works es una empresa de fabricación multinacional dedicada y distribución de bicicletas, los elementos y los mercados de accesorios toocommercial en América del Norte, Europa y Asia. compañía de Hello tiene a 500 trabajadores. Además, Adventure Works emplea varios equipos de ventas regionales en su base comercial. El proyecto es toocreate un modelo tabular para los usuarios de ventas y marketing tooanalyze datos de base de datos de AdventureWorksDW Hola ventas por Internet.  
  
tutorial de hello toocomplete, debe completar varias lecciones. Cada lección consta de varias tareas. Es necesario para completar la lección Hola completar cada tarea en orden. Una lección en concreto puede contener varias tareas que obtienen un resultado similar, pero la manera en que se completa cada tarea es ligeramente diferente. Esta muestra de método a menudo hay más de una manera toocomplete una tarea y toochallenge mediante el uso de conocimientos que ha aprendido en tareas y lecciones anteriores.  
  
Hola de lecciones de hello sirve tooguide a través de la creación de un modelo tabular básico mediante el uso de muchas de las características de hello incluido en SSDT. Porque cada lección se basa en la lección anterior hello, debe completar las lecciones de hello en orden.
  
Este tutorial no proporciona lecciones sobre cómo administrar un servidor en el portal de Azure, administración de un servidor o base de datos con SSMS o mediante un cliente de datos del modelo de aplicación toobrowse. 


## <a name="lessons"></a>Lecciones  
Este tutorial incluye Hola siguientes lecciones:  
  
|Lección|Tiempo estimado toocomplete|  
|----------|------------------------------|  
|[1: Creación de un nuevo proyecto de modelo tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[2: Obtención de datos](../tutorials/aas-lesson-2-get-data.md)|10 minutos|  
|[3: Marcado como tabla de fechas](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 minutos|  
|[4: Creación de relaciones](../tutorials/aas-lesson-4-create-relationships.md)|10 minutos|  
|[5: Creación de columnas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 minutos|
|[6: Creación de medidas](../tutorials/aas-lesson-6-create-measures.md)|30 minutos|  
|[7: Creación de indicadores clave de rendimiento (KPI)](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 minutos|  
|[8: Creación de perspectivas](../tutorials/aas-lesson-8-create-perspectives.md)|5 minutos|  
|[9: Creación de jerarquías](../tutorials/aas-lesson-9-create-hierarchies.md)|20 minutos|  
|[10: Creación de particiones](../tutorials/aas-lesson-10-create-partitions.md)|15 minutos|  
|[11: Creación de roles](../tutorials/aas-lesson-11-create-roles.md)|15 minutos|  
|[12: Análisis en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 minutos| 
|[13: Implementación](../tutorials/aas-lesson-13-deploy.md)|5 minutos|  
  
## <a name="supplemental-lessons"></a>Lecciones complementarias  
Estas lecciones no son tutorial de hello toocomplete necesaria, pero pueden resultar útil para una mejor comprensión tabulares avanzadas del modelo características de creación.  
  
|Lección|Tiempo estimado toocomplete|  
|----------|------------------------------|  
|[Filas de detalles](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 minutos|
|[Seguridad dinámica](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 minutos|
|[Jerarquías desiguales](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 minutos| 

  
## <a name="next-steps"></a>Pasos siguientes  
tooget iniciado, consulte [lección 1: crear un nuevo proyecto de modelo Tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

