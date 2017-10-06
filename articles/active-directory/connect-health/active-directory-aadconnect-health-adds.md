---
title: Azure AD Connect Health con AD DS aaaUsing | Documentos de Microsoft
description: "Trata de hello Azure AD Connect Health página que veremos cómo toomonitor AD DS."
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Uso de Azure AD Connect Health con AD DS
Hola siguiendo documentación es específico toomonitoring servicios de dominio de Active Directory con Azure AD Connect Health. Hola admitida versiones de AD DS son: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 y Windows Server 2016.

Para más información sobre la supervisión de AD FS con Azure AD Connect Health, consulte [Uso de Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md). Para obtener información adicional sobre la supervisión de Azure AD Connect (Sync) con Azure AD Connect Health, consulte [Uso de Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md).

![Azure AD Connect Health para AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Alertas de Azure AD Connect Health para AD DS
Hola sección de alertas en Azure AD Connect Health para AD DS, proporciona una lista de alertas activas y resueltas, controladores de dominio de tooyour relacionados. Seleccionar una alerta activa o resuelto abre una nueva hoja con información adicional, junto con los pasos de resolución y vínculos a documentación de toosupporting. Cada tipo de alerta puede tener una o varias instancias, que corresponden tooeach Hola de controladores de dominio afectados por esa alerta determinada. En parte inferior de Hola de hoja de alerta de hello, haga doble clic en un tooopen de controlador de dominio afectado una hoja con más detalles acerca de esa instancia de alerta adicional.

En esta hoja, puede habilitar las notificaciones de correo electrónico para alertas y cambiar el intervalo de tiempo de hello en la vista. Al expandir el intervalo de tiempo de hello permite toosee de alertas resueltas anteriores.

![Error de sincronización de Azure AD Connect](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Panel de controladores de dominio
Este panel proporciona una vista topológica del entorno, junto con métricas clave de funcionamiento y el estado de mantenimiento de cada uno de los controladores de dominio supervisados. las métricas de Hello presentan identificar tooquickly, los controladores de dominio que pueden requerir más investigación. De forma predeterminada, se muestra solo un subconjunto de columnas de Hola. Sin embargo, puede encontrar el conjunto completo de Hola de columnas disponibles, haciendo doble clic en el comando de columnas de Hola. Seleccionar las columnas de Hola que más le interesa, activa este panel en una sola y fácil colocar mantenimiento de hello tooview de su entorno de AD DS.

![Controladores de dominio](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

Controladores de dominio se pueden agrupar por su respectivo de dominio o un sitio, lo cual es útil para comprender la topología de entorno Hola. Por último, si hace doble clic en encabezado de hoja de hello, panel de hello maximiza tooutilize Hola pantalla disponibilidad inmobiliaria. Esta vista más grande es útil cuando se muestran varias columnas.

## <a name="replication-status-dashboard"></a>Panel del estado de replicación
Este panel proporciona una vista de topología de replicación y el estado de replicación de Hola de los controladores de dominio supervisado. estado de Hola de intento de replicación más reciente de Hola se muestra, junto con documentación útil para los errores que se encuentran. Hacer doble clic en un controlador de dominio con un error, tooopen una nueva hoja con información como: detalles sobre el error de hello, pasos de resolución, se recomienda y se proporcionan vínculos a documentación de tootroubleshooting.

![Estado de replicación](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Supervisión
Esta característica proporciona tendencias del gráficas de contadores de rendimiento que se recopilan de forma continua de cada uno de los controladores de dominio de hello supervisado. El rendimiento de un controlador de dominio se puede comparar fácilmente con el de todos los demás controladores de dominio supervisados del bosque. Además, puede ver varios contadores de rendimiento en paralelo, lo cual resulta útil al solucionar problemas en su entorno.

![Supervisión](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

De forma predeterminada, nos hemos preseleccionado cuatro contadores de rendimiento; Sin embargo, puede incluir otros usuarios al hacer clic en el comando de filtro de Hola y seleccionando o anulando la selección de todos los contadores de rendimiento deseados. Además, puede hacer doble clic un tooopen de gráfico del contador de rendimiento una nueva hoja, lo que incluye puntos de datos para cada uno de los controladores de dominio de hello supervisado.

## <a name="related-links"></a>Vínculos relacionados
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalación del agente de Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operaciones de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso de Azure AD Connect Health con AD FS](active-directory-aadconnect-health-adfs.md)
* [Uso de Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md)
* [Preguntas más frecuentes de Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historial de versiones de Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)

