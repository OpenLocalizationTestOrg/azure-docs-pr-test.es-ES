---
title: "directivas de acceso de aaaData en visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "En este tutorial, aprenderá toomanage las directivas de acceso de datos en información de la serie de tiempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Conceder el entorno de visión de la serie de tiempo de datos access tooa mediante el portal de Azure

Los entornos de Time Series Insights tienen dos tipos independientes de directivas de acceso:

* Directivas de acceso de administración
* Directivas de acceso a datos

Ambas directivas conceden a las entidades de Azure Active Directory (usuarios y aplicaciones) distintos permisos en un entorno concreto. Hello las entidades de seguridad (usuarios y aplicaciones) deben pertenecer toohello active directory (o "Inquilino de Azure") asociado a la suscripción de Hola que contiene el entorno de Hola.

Directivas de administración de acceso conceder toohello relacionadas de la configuración de permisos del entorno de hello, como
*   Creación y eliminación del entorno de hello, orígenes de eventos, hacer referencia a conjuntos de datos, y
*   Administración de directivas de acceso de datos de Hola.

Las directivas de acceso de datos conceder permisos en las consultas de datos tooissue, manipulan los datos de referencia de entorno de Hola y compartan las consultas guardadas y perspectivas asociadas con el entorno de Hola.

dos tipos de directivas de Hello permiten una separación clara entre administración de toohello de acceso de entorno de Hola y acceder a los datos dentro del entorno de hello toohello. Por ejemplo, es posible toosetup un entorno de forma que Hola propietario/creador del entorno de Hola se quita del acceso a datos de Hola. Así como a los usuarios y servicios que se permiten tooread datos desde el entorno de hello no pueden concederse ninguna configuración de toohello de acceso de entorno de Hola.

## <a name="grant-data-access"></a>Concesión de acceso a datos
Hello pasos siguientes muestran cómo tener acceso datos toogrant para una entidad de seguridad de usuario:

1.  Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2.  Haga clic en "Todos los recursos" en el menú Hola izquierda Hola de hello portal de Azure.
3.  Seleccione el entorno de Time Series Insights.

  ![Administrar el origen de información de la serie de tiempo de hello: entorno](media/data-access/getstarted-grant-data-access1.png)

4.  Seleccione “Acceso a plano de datos” y haga clic en “Agregar”.

  ![Administrar el origen de información de la serie de tiempo de hello: agregar](media/data-access/getstarted-grant-data-access2.png)

5.  Haga clic en "Seleccionar usuario".
6.  Busque y seleccione el usuario por correo electrónico de Hola.
7.  Haga clic en "Seleccionar" en la hoja "Seleccionar usuarios".

  ![Administrar el origen de información de la serie de tiempo de hello: seleccione el usuario](media/data-access/getstarted-grant-data-access3.png)

8.  Haga clic en "Seleccionar rol".
9.  Seleccione "Colaborador" Si desea que los datos de referencia de tooallow usuario toochange y compartir las consultas guardadas y las perspectivas con otros usuarios del entorno de Hola. En caso contrario, seleccionar datos de consulta de usuario de "Lectura" tooallow entorno hello y guarde personales consultas (no compartidas) en el entorno de Hola.
10. Haga clic en "Aceptar" en la hoja de Hola "Seleccionar rol".

  ![Administrar el origen de información de la serie de tiempo de hello: Seleccionar rol](media/data-access/getstarted-grant-data-access4.png)

11. Haga clic en "Aceptar" en la hoja de Hola "Seleccionar rol de usuario".
12. Debería ver lo siguiente:

  ![Administrar el origen de información de la serie de tiempo de hello: resultados](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Pasos siguientes

* [Creación de un origen de eventos](time-series-insights-add-event-source.md)
* [Enviar eventos](time-series-insights-send-events.md) toohello origen del evento
* Vea el entorno en el [portal de Time Series Insights](https://insights.timeseries.azure.com)
