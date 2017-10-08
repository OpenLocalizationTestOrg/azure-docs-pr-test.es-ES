---
title: Operaciones de Synchronization Service Manager de Azure AD Connect | Microsoft Docs
description: Conocer la ficha de operaciones de hello en hello Synchronization Service Manager para Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>Uso de hello ficha operaciones de sincronización de Service Manager

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

ficha de operaciones de Hello muestra los resultados de Hola de operaciones más recientes de Hola. Esta pestaña es clave toounderstand y solucionar problemas.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Entender la información de hello visible en la ficha operaciones Hola
mitad superior de Hello muestra todas las ejecuciones en orden cronológico. De forma predeterminada, registro de operaciones de hello mantiene información acerca de hello últimos siete días, pero se puede cambiar esta configuración con hello [programador](active-directory-aadconnectsync-feature-scheduler.md). Desea toolook para cualquier serie que no se muestren el estado correcto. Puede cambiar Hola ordenar haciendo clic en los encabezados de Hola.

Hola **estado** columna es la información más importante de Hola y muestra Hola problema más grave para una ejecución. Este es un breve resumen de los estados más comunes de hello en orden de prioridad tooinvestigate (donde * indicar varias cadenas de error posibles).

| Estado | Comentario |
| --- | --- |
| stopped-* |no se pudo completar Hola ejecutar. Por ejemplo, si hello sistema remoto está inactivo y no se puede contactar. |
| stopped-error-limit |Se han generado más de 5000 errores. Hola ejecutar automáticamente se detuvo debido toohello gran número de errores. |
| completed-\*-errors |Hola ejecución se completó, pero existen errores (menos de 5000) que deben investigarse. |
| completed-\*-warnings |Hola ejecutar completó, pero algunos datos no están en estado de espera de Hola. Si se producen errores, es posible que se trate únicamente de un síntoma. Le recomendamos que primero resuelva los errores y que luego investigue las advertencias. |
| Correcto |No hay ningún problema. |

Cuando se selecciona una fila, inferior Hola actualiza los detalles de hello tooshow de que se ejecutan. toohello extremo izquierdo de la parte inferior de hello, es posible que tenga un hablados lista **paso #**. Solo aparecerá si tiene varios dominios en el bosque; cada dominio estará representado por un paso. nombre de dominio de Hello puede encontrarse bajo el encabezado de hello **partición**. En **las estadísticas de sincronización**, también puede encontrar más información acerca del número de Hola de cambios que se han procesado. Puede hacer clic en hello vínculos tooget una lista de objetos de hello cambiado. Si hay objetos con errores, estos se mostrarán en **Errores de sincronización**.

Para más información, consulte la [solución de problemas de un objeto que no se sincroniza](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md).

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
