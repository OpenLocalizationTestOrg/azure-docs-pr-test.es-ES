---
title: aaaConnect tooAzure Analysis Services con Power BI | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooan Azure Analysis Services server mediante el uso de Power BI."
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a>Conexión con Power BI

Una vez que haya creado un servidor de Azure e implementa un modelo tabular tooit, los usuarios de su organización son tooconnect listo y empezar a explorar los datos. 

> [!TIP]
> Estar seguro de versión más reciente de Hola de toouse de [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Conexión en Power BI Desktop

1. En Power BI Desktop, haga clic en **Obtener datos** > **Azure** > **Base de datos de Azure Analysis Services**.

2. En **servidor**, escriba el nombre del servidor de Hola. 
    
    Ser seguro tooinclude Hola dirección URL completa. Por ejemplo, asazure://westcentralus.asazure.windows.net/advworks.

3. En **base de datos**, si conoce el nombre de Hola de base de datos de modelo tabular de Hola o una perspectiva que desee tooconnect a, péguelo aquí. En caso contrario, puede dejar este campo en blanco y seleccionar una base de datos o una perspectiva más adelante.

4. Deje Hola predeterminado **conectar en directo** opción, a continuación, presione **conectar**. 

5. Escriba sus credenciales de inicio de sesión, si se le solicitan. 

6. En **navegador**, expanda servidor hello y luego seleccione el modelo de Hola o una perspectiva que desee tooconnect para, a continuación, haga clic en **conectar**. Haga clic en un modelo o perspectiva tooshow todos los objetos de Hola para esa vista.

    modelo de Hola se abre en Power BI Desktop con un informe en blanco en la vista de informe. lista de campos de Hello muestra todos los objetos de modelo no ocultos. Estado de la conexión se muestra en la esquina inferior derecha de Hola.

## <a name="connect-in-power-bi-service"></a>Conexión en Power BI (servicio)

1. Crear un archivo de Power BI Desktop que tiene un modelo de tooyour de conexión dinámica en el servidor.
2. En [Power BI](https://powerbi.microsoft.com), haga clic en **Obtener datos** > **archivos**. Localice y seleccione el archivo.



## <a name="see-also"></a>Otras referencias
[Conectar tooAzure Analysis Services](analysis-services-connect.md)   
[Bibliotecas de cliente](analysis-services-data-providers.md)

