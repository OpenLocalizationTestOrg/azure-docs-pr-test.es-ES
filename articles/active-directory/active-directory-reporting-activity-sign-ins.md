---
title: informes de actividad aaaSign en el portal de Azure Active Directory Hola | Documentos de Microsoft
description: "Informes de actividad toosign introducción en el portal de Azure Active Directory Hola"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Informes de actividad de inicio de sesión en el portal de Azure Active Directory Hola

Con Azure Active Directory (Azure AD) informes en hello [portal de Azure](https://portal.azure.com), puede obtener información de hello necesita toodetermine cómo está haciendo su entorno.

Hola reporting arquitectura en Azure Active Directory consta de Hola de los componentes siguientes:

- **Actividad** 
    - **Las actividades de inicio de sesión** : información sobre el uso de Hola de las aplicaciones administradas y las actividades de inicio de sesión de usuario
    - **Registros de auditoría**: información de la actividad del sistema sobre los usuarios y la administración de grupos, sus aplicaciones administradas y actividades de directorio.
- **Seguridad** 
    - **Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario. Para más información, consulte Inicios de no seguros.
    - **Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro. Para más información, consulte la sección Usuarios marcados en riesgo.

Este tema ofrece una visión general de las actividades de inicio de sesión de Hola.

## <a name="pre-requisite"></a>Requisito previo

### <a name="who-can-access-hello-data"></a>¿Quién puede tener acceso a datos de hello?
* Usuarios de rol de administrador de seguridad o seguridad lector Hola
* Administradores globales
* Cualquier usuario (no administradores) puede acceder a sus propios inicios de sesión 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>¿Qué licencia de Azure AD necesita tooaccess actividad de inicio de sesión?
* El inquilino debe tener una licencia de Azure AD Premium asociada toosee Hola todo inicio de sesión-informe de actividad


## <a name="signs-in-activities"></a>Actividades de inicio de sesión

Con información de hello proporcionada por informe de inicio de sesión de usuario de hello, encontrar respuestas tooquestions como:

* ¿Qué es el patrón de inicio de sesión de Hola de un usuario?
* ¿Cuántos usuarios tienen usuarios que han iniciado sesión durante una semana?
* ¿Cuál es el estado de Hola de estos inicios de sesión?

Las primera entrada tooall de punto de inicio de sesión en las actividades datos están **inicios de sesión** en la sección de la actividad de hello **Azure Active**.


![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/61.png "Actividad de inicio de sesión")


Un registro de auditoría tiene una vista de lista predeterminada que muestra:

- usuario relacionado Hola
- usuario de la aplicación Hola Hola ha iniciado sesión en
- estado de inicio de sesión de Hola
- hora de inicio de sesión Hola

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/41.png "Actividad de inicio de sesión")

Puede personalizar la vista de lista Hola haciendo clic en **columnas** en la barra de herramientas de Hola.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/19.png "Actividad de inicio de sesión")

Esto permite los campos adicionales de toodisplay o quitar los campos que ya se muestran.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/42.png "Actividad de inicio de sesión")

Si hace clic en un elemento en la vista de lista de hello, obtener todos los detalles disponibles sobre él.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/43.png "Actividad de inicio de sesión")


## <a name="filtering-sign-in-activities"></a>Filtrado de actividades de inicio de sesión

toonarrow hacia abajo Hola informó de un nivel de tooa de datos que funciona para usted, puede filtrar datos de inicios de sesión de hello mediante Hola siguientes campos:

- Intervalo de tiempo
- Usuario
- Application
- Cliente
- Estado de inicio de sesión

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/44.png "Actividad de inicio de sesión")


Hola **intervalo de tiempo** filtro permite tooyou toodefine un período de tiempo para hello devolvió datos.  
Los valores posibles son:

- 1 mes
- 7 días
- 24 horas
- Personalizado

Cuando se selecciona un intervalo de tiempo personalizado, puede configurar una hora de inicio y una hora de finalización.

Hola **usuario** filtro le permite toospecify nombre de Hola u Hola nombre principal de usuario (UPN) del usuario de Hola que le interesa.

Hola **aplicación** filtro permite un nombre de hello toospecify de aplicación Hola que le interesa.

Hola **cliente** filtro le permite toospecify información acerca del dispositivo de Hola que le interesa.

Hola **estado de inicio de sesión** filtro le permite tooselect de hello siguiente filtro:

- Todo
- Correcto
- Error


## <a name="sign-in-activities-shortcuts"></a>Métodos abreviados de las actividades de inicio de sesión

Además tooAzure Active Directory, Hola portal de Azure le ofrece dos toosign en actividades de datos de puntos de entrada adicional:

- Usuarios y grupos
- Aplicaciones empresariales


### <a name="users-and-groups-sign-ins-activities"></a>Actividades de inicios de sesión de usuarios y grupos

Con información de hello proporcionada por informe de inicio de sesión de usuario de hello, encontrar respuestas tooquestions como:

- ¿Qué es el patrón de inicio de sesión de Hola de un usuario?
- ¿Cuántos usuarios tienen usuarios que han iniciado sesión durante una semana?
- ¿Cuál es el estado de Hola de estos inicios de sesión?



Los datos de toothis de punto de entrada están Hola usuario inicio de sesión gráfico Hola **Introducción** sección en **usuarios y grupos**.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/45.png "Actividad de inicio de sesión")

gráfico de inicio de sesión de usuario de Hello muestra agregaciones semanales de inicio de sesión inicios para todos los usuarios en un período de tiempo determinado. valor predeterminado de Hola para hello período de tiempo es 30 días.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/46.png "Actividad de inicio de sesión")

Al hacer clic en un día en el gráfico de inicio de sesión de hello, obtendrá una lista detallada de las actividades de inicio de sesión de Hola para este día.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/41.png "Actividad de inicio de sesión")

Cada fila de la lista encontrará hello las actividades de inicio de sesión que Hola información detallada sobre el inicio de sesión en hello seleccionado como:

* ¿Quién ha iniciado sesión?
* ¿Cuál era hello relacionado con el UPN?
* ¿La aplicación era destino Hola del inicio de sesión de hello?
* ¿Cuál es la dirección IP de hello del inicio de sesión de hello?
* ¿Cuál era el estado de hello del inicio de sesión de hello?

Hola **inicios de sesión** opción ofrece una descripción completa de todos los inicios de sesión.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/51.png "Actividad de inicio de sesión")



## <a name="usage-of-managed-applications"></a>Uso de las aplicaciones administradas

Con una vista centrada en la aplicación de los datos de inicio de sesión, puede responder a preguntas tales como:

* ¿Quién está usando mis aplicaciones?
* ¿Qué Hola 3 las aplicaciones principales de su organización?
* Recientemente he implementado una aplicación. ¿Cómo sigue?

Los datos de toothis de punto de entrada están Hola 3 las aplicaciones principales de su organización en último informe de 30 días Hola Hola **Introducción** sección bajo **aplicaciones empresariales**.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/64.png "Actividad de inicio de sesión")

Hola aplicación gráfico semanal agregaciones de uso de inicios de sesión para las aplicaciones de la parte superior a 3 en un período de tiempo determinado. valor predeterminado de Hola para hello período de tiempo es 30 días.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/47.png "Actividad de inicio de sesión")

Si desea, puede establecer el foco de hello en una aplicación específica.


![Informes](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Informes")

Al hacer clic en un día en el gráfico de uso de aplicación Hola, obtendrá una lista detallada de las actividades de inicio de sesión de Hola.


![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/48.png "Actividad de inicio de sesión")


Hola **inicios de sesión** opción ofrece una descripción completa de todas las aplicaciones de tooyour de inicio de sesión de eventos.

![Actividad de inicio de sesión](./media/active-directory-reporting-activity-sign-ins/49.png "Actividad de inicio de sesión")



## <a name="next-steps"></a>Pasos siguientes

Si desea más información acerca de los códigos de error de inicio de sesión de la actividad tooknow, vea hello [inicio de sesión de códigos de error de actividad informes en el portal de Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).

