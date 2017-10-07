---
title: aaaConnect tooAzure Analysis Services con Excel | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooan Azure Analysis Services server mediante el uso de Excel."
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a>Conexión con Excel

Una vez que haya creado un servidor de Azure e implementa un modelo tabular tooit, está listo tooconnect y empezar a explorar los datos.


## <a name="connect-in-excel"></a>Conexión en Excel

Conectar el servidor de tooa en Excel se admite mediante obtener datos en Excel 2016. No se puede conectar usando Hola Asistente para importación de tabla de PowerPivot. 

**tooconnect en Excel 2016**

1. En Excel 2016, en hello **datos** la cinta de opciones, haga clic en **obtener datos externos** > **desde otros orígenes** > **de Analysis Services** .

2. En Hola Asistente para la conexión de datos, en **nombre del servidor**, escriba nombre del servidor hello incluidos el protocolo y URI. A continuación, en **las credenciales de inicio de sesión**, seleccione **Hola de uso después de nombre de usuario y contraseña**y, a continuación, escriba nombre de usuario de la organización de hello, por ejemplo nancy@adventureworks.comy la contraseña.

    ![Conexión desde el inicio de sesión de Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. En **Seleccionar base de datos y tabla**, seleccione la base de datos de Hola y modelo o perspectiva y, a continuación, haga clic en **finalizar**.
   
    ![Conexión desde el modelo de selección de Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>Consulte también
[Bibliotecas de cliente](analysis-services-data-providers.md)   
[Administración del servidor](analysis-services-manage.md)     


