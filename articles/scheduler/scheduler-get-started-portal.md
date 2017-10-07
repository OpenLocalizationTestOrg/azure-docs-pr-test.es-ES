---
title: aaaGet a trabajar con el programador de Azure en el portal de Azure | Documentos de Microsoft
description: "Introducción al Programador de Azure en el Portal de Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Introducción al Programador de Azure en el Portal de Azure
Es fácil toocreate programar trabajos en el programador de Azure. En este tutorial, aprenderá cómo toocreate un trabajo. También aprenderá las funcionalidades de supervisión y administración del Programador.

## <a name="create-a-job"></a>Creación de un trabajo
1. Inicie sesión en demasiado[portal de Azure](https://portal.azure.com/).  
2. Haga clic en **+ nuevo** > tipo *programador* en el cuadro de búsqueda de hello > seleccione **programador** en resultados > haga clic en **crear**.
   
    ![][marketplace-create]
3. Vamos a crear un trabajo que simplemente selecciona http://www.microsoft.com/ con una solicitud GET. Hola **trabajo del programador** pantalla, escriba Hola siguiente información:
   
   1. **Nombre:**`getmicrosoft`  
   2. **Suscripción** : su suscripción a Azure.   
   3. **Colección de trabajos:** seleccione una colección de trabajos existente o haga clic en **Crear nueva** y escriba un nombre.
4. Después, en **configuración de la acción**, definir Hola siguientes valores:
   
   1. **Tipo de acción:**` HTTP`  
   2. **Método:**`GET`  
   3. **URL:**` http://www.microsoft.com`  
      
      ![][action-settings]
5. Por último, vamos a definir una programación. trabajo de Hello puede definirse como un trabajo único, pero vamos a seleccionar una programación de periodicidad:
   
   1. **Periocidad**: `Recurring`
   2. **Inicio**: la fecha de hoy
   3. **Repetir cada**: `12 Hours`
   4. **Finalización**: dos días a partir de hoy  
      
      ![][recurrence-schedule]
6. Haga clic en **Crear**

## <a name="manage-and-monitor-jobs"></a>Administración y supervisión de trabajos
Una vez que se crea un trabajo, aparece en el panel de Azure principal Hola. Haga clic en trabajo hello y una nueva ventana se abrirá con hello siguientes pestañas:

1. Propiedades  
2. Configuración de la acción  
3. Schedule  
4. Historial
5. Usuarios
   
   ![][job-overview]

### <a name="properties"></a>Propiedades
Estas propiedades de sólo lectura describen los metadatos de la administración de hello para el trabajo del programador de Hola.

   ![][job-properties]

### <a name="action-settings"></a>Configuración de la acción
Al hacer clic en un trabajo en hello **trabajos** pantalla le permite tooconfigure ese trabajo. Esto le permite configurar opciones avanzadas, si no configura Hola Asistente de creación rápida.

Para todos los tipos de acción, puede cambiar la directiva de reintentos hello y acción de error de Hola.

Para los tipos de acción de trabajo HTTP y HTTPS, puede cambiar Hola método tooany permitida el verbo HTTP. También se pueden agregar, eliminar o cambiar los encabezados de Hola y la información de autenticación básica.

Para los tipos de acción de cola de almacenamiento, puede cambiar la cuenta de almacenamiento de hello, nombre de la cola, token SAS y cuerpo.

Para los tipos de acción de bus de servicio, puede cambiar el espacio de nombres de hello, ruta de acceso de cola/tema, configuración de autenticación, tipo de transporte, propiedades del mensaje y el cuerpo del mensaje.

   ![][job-action-settings]

### <a name="schedule"></a>Schedule
Esto le permite volver a configurar programación de hello, si desea que la programación de hello toochange que creó en hello Asistente de creación rápida.

Se trata de una oportunidad toobuild [programaciones complejas y periodicidad avanzada en el trabajo](scheduler-advanced-complexity.md)

Puede cambiar la fecha de inicio de Hola y Hola, la programación de periodicidad y la hora fecha de finalización y hora (si el trabajo de hello es periódico).

   ![][job-schedule]

### <a name="history"></a>Historial
Hola **historial** pestaña muestra las métricas seleccionadas para cada ejecución del trabajo de sistema de hello para el trabajo seleccionado de Hola. Estas métricas proporcionan valores en tiempo real con respecto a estado Hola de Scheduler:

1. Estado  
2. Detalles  
3. Número de reintentos
4. Periodicidad: 1ª, 2ª, 3ª, etc.
5. Hora de inicio de ejecución  
6. Hora de finalización de ejecución
   
   ![][job-history]

Puede hacer clic en una ejecución tooview su **detalles del historial de**, incluida la respuesta completa de Hola para cada ejecución. Este cuadro de diálogo también permite Portapapeles toohello de toocopy Hola respuesta.

   ![][job-history-details]

### <a name="users"></a>Usuarios
El control de acceso basado en roles (RBAC) de Azure permite realizar una administración detallada del acceso al Programador de Azure. toolearn cómo toouse Hola ficha de usuarios, consulte demasiado[Azure Role-Based el Control de acceso](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>Otras referencias
 [¿Qué es Programador?](scheduler-intro.md)

 [Jerarquía de entidades, terminología y conceptos del Programador](scheduler-concepts-terms.md)

 [Planes y facturación en Programador de Azure](scheduler-plans-billing.md)

 [¿Cómo se programa toobuild complejo y periodicidad avanzada con el programador de Azure](scheduler-advanced-complexity.md)

 [Referencia de API de REST del Programador](https://msdn.microsoft.com/library/mt629143)

 [Referencia de cmdlets de PowerShell del Programador](scheduler-powershell-reference.md)

 [Alta disponibilidad y confiabilidad del Programador](scheduler-high-availability-reliability.md)

 [Límites, valores predeterminados y códigos de error de Programador](scheduler-limits-defaults-errors.md)

 [Autenticación de salida del Programador](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
