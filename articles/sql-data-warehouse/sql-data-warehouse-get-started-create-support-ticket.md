---
title: "aaaHow toocreate una incidencia de soporte técnico para el almacenamiento de datos SQL | Documentos de Microsoft"
description: "¿Cómo toocreate una compatibilidad con vales en el almacén de datos de SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>¿Cómo toocreate compatibilidad vale para almacenamiento de datos SQL
Si tiene algún problema con su instancia de SQL Data Warehouse, cree una incidencia de soporte técnico para que nuestro equipo de ingenieros pueda ayudarle.

> [!NOTE] 
> A partir de 20/12/2016, comprobación de mantenimiento de recursos de Hola Hola portal de Azure no es exacta. Estamos trabajando activamente toofix este problema. 


## <a name="create-a-support-ticket"></a>Creación de una incidencia de soporte técnico
1. Abra hello [portal de Azure][Azure portal].
2. En la pantalla de inicio de bienvenida, haga clic en hello **ayuda y soporte técnico** icono.
   
    ![Ayuda y soporte técnico](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. En Hola ayuda + hoja de soporte técnico, haga clic en **crear solicitud de soporte técnico**.
   
    ![Nueva solicitud de soporte](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Seleccione hello **tipo de solicitud**.
   
    ![Tipo de solicitud](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > De forma predeterminada, cada servidor SQL (por ejemplo, myserver.database.windows.net) tiene una **Cuota de DTU** de 45.000. Esta cuota es simplemente un límite de seguridad. Puede aumentar la cuota mediante la creación de una incidencia de soporte técnico y seleccionar *cuota* como tipo de solicitud de saludo. toocalculate necesita, multiplique la DTU Hola 7.5 por hello total [DWU] [ DWU] necesarios. Por ejemplo, al igual que toohost dos DW6000s en un servidor SQL server, a continuación, debe solicitar una cuota DTU de 90.000.  Puede ver el consumo de DTU actual de la hoja de hello SQL server en el portal de Hola. Bases de datos en pausa y continuó cuentan para la cuota de DTU Hola. 
   > 
   > 
5. Seleccione hello **suscripción** que hosts Hola base de datos con el que se informe de problemas de Hola.
   
    ![La suscripción](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Seleccione **almacenamiento de datos SQL** como Hola recursos.
   
    ![Recurso](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. Seleccione su [Plan de soporte técnico de Azure][Azure support plan].
   
   * **facturación, las cuotas y la administración de suscripciones** .
   * El soporte técnico para problemas de tipo **Break-fix** se proporciona a través de los niveles [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] o [Premier][Premier]. Problemas de break-fix en línea son problemas de los clientes que se ha producido durante el uso de Azure donde hay una expectativa razonable ese problema de Hola de Microsoft que se produjo.
   * **Desarrollador de asesoría** y **servicios de consultoría** están disponibles en hello [Professional Direct] [ Professional Direct] y [principal] [ Premier] niveles de compatibilidad. 
     
     Si tienes un Premier admitir plan, también puede notificar el almacenamiento de datos de SQL relacionada con problemas en hello [portal en línea de Microsoft Premier][Microsoft Premier online portal].  Vea [planes de soporte técnico de Azure] [ Azure support plan] toolearn más información acerca de saludo diversos admiten planes, incluidos el ámbito, tiempos de respuesta, precios, etcetera.  Si desea ver las preguntas más frecuentes sobre el soporte técnico de Azure, consulte [Preguntas más frecuentes de soporte técnico de Azure][Azure support FAQs].  
     
     ![Plan de soporte técnico](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Seleccione hello **tipo de problema** y **categoría**. En este ejemplo, que hemos elegido "Herramientas" como tipo de problema de Hola y "Herramientas de cliente" como categoría de Hola. 
   
    ![Categoría del tipo de problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Describa el problema de Hola y elegir Hola nivel de impacto empresarial.
   
    ![Descripción del problema](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Su **información de contacto** para esta incidencia de soporte técnico se rellenará automáticamente. Actualice si es necesario.
    
    ![Información de contacto](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Haga clic en **crear** solicitud de soporte técnico de toosubmit Hola.

## <a name="monitor-a-support-ticket"></a>Supervisión de una incidencia de soporte técnico
Una vez ha enviado la solicitud de soporte técnico de Hola, equipo de soporte técnico de Azure de Hola se comunicará con usted. toocheck el estado de la solicitud y los detalles, haga clic en **administrar solicitudes de soporte técnico** en el panel de Hola.

![Comprobar estado](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Otros recursos
Además, puede conectarse con hello Comunidad de almacenamiento de datos SQL en [desbordamiento de la pila] [ Stack Overflow] o en hello [foro de MSDN de almacenamiento de datos de SQL Azure] [ Azure SQL Data Warehouse MSDN forum].

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

