---
title: "nivel de compatibilidad del modelo de aaaData en los servicios de análisis de Azure | Documentos de Microsoft"
description: "Descripción del nivel de compatibilidad del modelo de datos tabulares."
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
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Nivel de compatibilidad para los modelos tabulares de Analysis Services

*Nivel de compatibilidad* hace referencia a comportamientos específicos de toorelease en el motor de Analysis Services de Hola. Nivel de compatibilidad de cambios toohello normalmente coincida con las versiones principales de SQL Server. Estos cambios también se implementan en paridad de toomaintain Azure Analysis Services entre ambas plataformas. Los cambios de nivel de compatibilidad también afectan a las características disponibles en los modelos tabulares. Por ejemplo, los metadatos de objetos tabulares y de DirectQuery tienen implementaciones diferentes según el nivel de compatibilidad de Hola. 

Azure Analysis Services es compatible con los modelos tabulares en niveles de compatibilidad de hello 1200 y 1400.

nivel de compatibilidad más reciente de Hello es 1400. Este nivel se corresponde a SQL Server 2017 Analysis Services. Principales características de nivel de compatibilidad de hello 1400 incluyen:

*  Nueva infraestructura para la conectividad de datos y la importación en los modelos tabulares con compatibilidad con las API de TOM y el scripting de TMSL. Esta nueva característica habilita la compatibilidad con orígenes de datos adicionales como Azure Blob Storage.
*  Funcionalidades de transformación de datos y mashup de datos mediante el uso de expresiones Get Data y M.
*  Las medidas admiten una propiedad de filas de detalles con una expresión DAX. Esta propiedad habilita las herramientas de cliente como Microsoft Excel toodrill toodetailed datos de un informe de agregado. Por ejemplo, cuando los usuarios ver las ventas totales para una región y el mes, pueden ver detalles del pedido Hola asociado. 
*  Seguridad de nivel de objeto de tabla y columna de nombres, además toohello datos dentro de ellos.
*  Compatibilidad mejorada para las jerarquías desiguales.
*  Mejoras en el rendimiento y la supervisión.
  
## <a name="set-compatibility-level"></a>Establecimiento del nivel de compatibilidad 
 Al crear un nuevo proyecto de modelo tabular en SSDT, puede especificar el nivel de compatibilidad de hello en hello **Diseñador de modelos tabulares** cuadro de diálogo. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Si selecciona hello **no volver a mostrar este mensaje** opción, todos los proyectos posteriores utilizan nivel de compatibilidad de hello especificado como valor predeterminado de Hola. Puede cambiar el nivel de compatibilidad de hello predeterminado en SSDT en **herramientas** > **opciones**.  
  
 tooupgrade un proyecto de modelo tabular existente en SSDT, conjunto hello **nivel de compatibilidad** propiedad en el modelo de hello **propiedades** ventana. Tenga en cuenta que, actualizar el nivel de compatibilidad de hello es irreversible.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Compruebe el nivel de compatibilidad para una base de datos de modelo tabular en SQL Server Management Studio 
 En SSMS, haga clic en el nombre de base de datos de hello > **propiedades** > **nivel de compatibilidad**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Comprobación del nivel de compatibilidad admitido para un servidor en SSMS  
 En SSMS, haga clic en el nombre del servidor de hello > **propiedades** > **nivel de compatibilidad admitido**.  
  
 Esta propiedad especifica Hola máximo nivel de compatibilidad de una base de datos que se ejecutará en el servidor de hello (excepto la vista previa). no se puede cambiar el nivel de compatibilidad de Hello compatible.  

## <a name="next-steps"></a>Pasos siguientes
  [Creación de un modelo en Azure Portal](analysis-services-create-model-portal.md)   
  [Administración de Analysis Services](analysis-services-manage.md)  
