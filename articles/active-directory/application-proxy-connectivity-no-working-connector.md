---
title: "grupo de conectores de trabajo aaaNo encontró para una aplicación de Proxy de aplicación | Documentos de Microsoft"
description: "Solucionar problemas que pueden surgir cuando no hay ningún trabajo conector en un grupo de conectores para su aplicación con hello Proxy de aplicación de Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>No se encontró ningún grupo de conectores en funcionamiento para una aplicación de proxy de aplicación

La Ayuda de este artículo se problemas comunes de hello tooresolve enfrentados cuando no hay un conector detectado para una aplicación de Proxy de aplicación integrada con Azure Active Directory.

## <a name="overview-of-steps"></a>Introducción a los pasos
Si no hay ningún trabajo conector en un grupo de conectores para la aplicación, hay algunos problemas de Hola de tooresolve maneras:

-   Si no tiene ningún conector de grupo de hello, hacer lo siguiente:

    -   Descargar un nuevo conector en servidor de derecho local de Hola y asignar toothis grupo

    -   Mover un conector active Hola grupo

-   Si no tiene ningún conector de active en grupo de hello, puede:

    -   Identificar el motivo de hello que el conector está inactivo y resolver

    -   Mover un conector active Hola grupo

tooknow cuál de estos es problema de hello, abra el menú de "Proxy de aplicación" hello en la aplicación y mire el mensaje de advertencia de grupo de conectores de Hola. Especifique ese grupo de hello necesita al menos un conector (no hay ninguno en el grupo de hello) o que no tiene ningún conector de active (aunque es probable que tenga conectores inactivos).

   ![Selección de grupos de conectores en Azure Portal](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

Para obtener detalles sobre cada una de estas opciones, vea Hola correspondiente sección. Cada una de ellas se da por supuesto que se inicia desde la página de administración del conector de Hola. Si se trata de mensaje de error de saludo anterior, puede ir toothis página haciendo clic en el mensaje de advertencia de saludo. En caso contrario, se puede encontrar yendo demasiado**Azure Active Directory**, haga clic en **aplicaciones empresariales**, a continuación, **Proxy de aplicación.**

   ![Administración de grupos de conectores en Azure Portal](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>Descarga de un nuevo conector

toodownload un conector nuevo, use el botón de "Descargar el conector" de hello al principio de Hola de página de Hola.

las necesidades de conector de hello Nota toobe instalado en un equipo con aplicaciones de línea de visión directa toohello back-end y se coloca normalmente en Hola mismo servidor que la aplicación hello. Después de descargar, Hola conector debe aparecer en este menú. Haga clic en hello conector y usar Hola "Grupo de conectores" desplegable toomake pertenece grupo adecuado toohello seguro. Guarde el cambio de Hola.

   ![Descargar conector Hola de hello Portal de Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>Movimiento de un conector activo

Si tiene un conector activo que debería pertenecer toohello grupo y tiene la aplicación de línea de visión toohello destino back-end, puede mover Hola conector en el grupo de hello asignado. toodo por lo tanto, haga clic en el conector de Hola. En el campo de "Grupo de conectores" Hola, usar grupo correcto de hello tooselect desplegable hello y haga clic en Guardar.

## <a name="resolve-an-inactive-connector"></a>Resolución de un conector inactivo

Si hello solo conectores de grupo de hello están inactivos, es probable que en un equipo que no han desbloqueado todos los puertos necesarios Hola.

Consulte los puertos de hello documento de solución de problemas para obtener más información sobre la investigación de este problema.

## <a name="next-steps"></a>Pasos siguientes
[Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)


