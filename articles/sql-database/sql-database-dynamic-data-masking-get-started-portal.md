---
title: "Azure Portal: enmascaramiento dinámico de datos de SQL Database | Microsoft Docs"
description: "¿Cómo tooget partió enmascaramiento Hola Portal de Azure dinámico de datos de base de datos SQL"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>Empezar a trabajar con datos dinámicos de base de datos SQL de enmascaramiento con hello Portal de Azure

Este tema muestra cómo tooimplement [enmascaramiento dinámico de datos](sql-database-dynamic-data-masking-get-started.md) con hello portal de Azure. También puede implementar el enmascaramiento de datos dinámicos mediante [cmdlets de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o hello [API de REST](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Configurar el enmascaramiento dinámico de datos para la base de datos mediante Hola Portal de Azure
1. Inicio Hola Portal de Azure en [https://portal.azure.com](https://portal.azure.com).
2. Navegue toohello hoja de configuración de base de datos de Hola que incluya datos confidenciales de hello desea toomask.
3. Haga clic en hello **Dynamic Data Masking** mosaico que inicia hello **Dynamic Data Masking** hoja de configuración.
   
   * Como alternativa, puede desplazarse hacia abajo toohello **Operations** sección y haga clic en **Dynamic Data Masking**.
     
     ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. Hola **Dynamic Data Masking** hoja de configuración es posible que vea algunas columnas de la base de datos que haya marcado ese motor de recomendaciones de Hola de enmascaramiento. En orden tooaccept recomendaciones de hello, simplemente haga clic en **agregar máscara** para una o varias columnas y una máscara se creará en función de tipo de valor predeterminado de Hola para esta columna. Puede cambiar Hola función de enmascaramiento haciendo clic en la regla de enmascaramiento de Hola y Hola campo formato tooa otro formato que prefiera el enmascaramiento de edición. Ser seguro tooclick **guardar** toosave la configuración.
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. tooadd una máscara de cualquier columna de la base de datos, en parte superior de Hola de hello **Dynamic Data Masking** hoja de configuración, haga clic en **agregar máscara** tooopen hello **Agregar regla de enmascaramiento** hoja de configuración
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Seleccione hello **esquema**, **tabla** y **columna** hello toodefine designado de campo que se enmascarará.
7. Elija un **formato del campo enmascaramiento** de lista de Hola de categorías de enmascaramiento de datos confidenciales.
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Haga clic en **guardar** en conjunto de reglas hoja tooupdate Hola de reglas de directiva de enmascaramiento de datos dinámicos de Hola de enmascaramiento de enmascaramiento de datos de Hola.
9. Los usuarios SQL de tipo hello o las identidades AAD que deben excluirse del enmascaramiento y tienen datos confidenciales de toohello sin máscara de acceso. Esto debe ser una lista separada por puntos y coma de usuarios. Tenga en cuenta que los usuarios con privilegios de administrador siempre tienen datos sin enmascarar de acceso toohello original.
   
    ![Panel de navegación](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > toomake así Hola a nivel de aplicación puede mostrar datos confidenciales para los usuarios de la aplicación con privilegios, Hola usuario SQL o aplicación hello de identidad AAD utiliza base de datos de tooquery Hola. Se recomienda encarecidamente que esta lista contienen un número mínimo de exposición de toominimize de los usuarios con privilegios de los datos confidenciales de Hola.
   > 
   > 
10. Haga clic en **guardar** en directiva de enmascaramiento nuevas o actualizadas de configuración hoja toosave Hola de enmascaramiento de datos de Hola.


## <a name="next-steps"></a>Pasos siguientes

* Para obtener información general sobre el enmascaramiento dinámico de datos, consulte [este artículo](sql-database-dynamic-data-masking-get-started.md).
* También puede implementar el enmascaramiento de datos dinámicos mediante [cmdlets de base de datos de SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) o hello [API de REST](https://msdn.microsoft.com/library/dn505719.aspx).
