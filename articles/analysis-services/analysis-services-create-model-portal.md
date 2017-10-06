---
title: "aaaCreate un modelo tabular mediante el Diseñador de hello Web de servicios de análisis de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un modelo tabular de Analysis Services de Azure mediante el uso de Hola Diseñador Web de portal de Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Creación de un modelo en Azure Portal

característica del diseñador (versión preliminar) web Hello Azure Analysis Services en el portal de Azure proporciona una manera rápida y sencilla toocreate y editar los modelos tabulares y consulta del modelo datos directamente en el explorador. 

Tenga en cuenta, el diseñador web hello es **vista previa**. Mientras se agrega nueva funcionalidad de todo el tiempo hello, en vista previa, la funcionalidad es limitada. Para el desarrollo de modelos más avanzados y pruebas, es mejor toouse Visual Studio (SSDT) y SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Requisitos previos

- Un servidor de Analysis Services de Azure en nivel Standard o Developer de Hola. Nuevos modelos creados mediante el Diseñador de hello Web son DirectQuery, solo compatible con estos niveles.
- Un archivo Power BI Desktop (.pbix), Azure SQL Database o Azure SQL Data Warehouse como origen de datos. Los nuevos modelos creados a partir de archivos Power BI Desktop admiten orígenes de datos de Azure SQL Database, Azure SQL Data Warehouse, Oracle y Teradata.
- Una cuenta de SQL Server y la contraseña para conectarse a orígenes de datos de base de datos SQL o almacenamiento de datos de SQL Azure tooAzure.

## <a name="toocreate-a-new-tabular-model"></a>toocreate un nuevo modelo tabular

1. En la hoja del servidor **Introducción** >  **Web designer**, haga clic en **Abrir**.

    ![Creación de un modelo en Azure Portal](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. En **Web designer** > **Modelos**, haga clic en **+ Agregar**.

    ![Creación de un modelo en Azure Portal](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. En **Nuevo modelo**, escriba un nombre de modelo y, a continuación, seleccione un origen de datos.

    ![Cuadro de diálogo Nuevo modelo en Azure Portal](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. En **conectar**, especifique las propiedades de conexión de Hola. El nombre de usuario y la contraseña deben ser de una cuenta de SQL Server.

     ![Cuadro de diálogo Connect (Conexión) en Azure Portal](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. En **tablas y vistas**, seleccionar hello tooinclude de tablas en el modelo y, a continuación, haga clic en **crear**. Se crean automáticamente relaciones entre las tablas con un par de claves.

     ![Selección de tablas y vistas](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

El nuevo modelo aparece en el explorador. Desde aquí puede:   

- Consultar datos del modelo arrastrando el Diseñador de consultas de campos toohello y agregando filtros.
- Crear nuevas medidas en tablas.
- Editar los metadatos del modelo mediante el editor de json de Hola.
- Abrir el modelo de hello en Visual Studio (SSDT), Power BI Desktop o Excel.

![Selección de tablas y vistas](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> Al editar los metadatos del modelo o crear nuevas medidas en el explorador, está guardando los modelos de tooyour cambios en Azure. Si también está trabajando en el modelo en SSDT, Power BI Desktop o Excel, el modelo puede dejar de estar sincronizado.


## <a name="next-steps"></a>Pasos siguientes 
[Administración de usuarios y roles de base de datos](analysis-services-database-users.md)  
[Conexión con Excel](analysis-services-connect-excel.md)  


