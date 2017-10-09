---
title: panel de servicio del Administrador de aaaStorSimple | Documentos de Microsoft
description: "Describe el panel de servicio del Administrador de StorSimple de Hola y explica cómo toouse, estado de hello toomonitor de la solución StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>Usar el panel de servicio del Administrador de StorSimple de Hola
## <a name="overview"></a>Información general
página del panel de servicio de administrador de StorSimple de Hello proporciona un resumen de todos los dispositivos de Hola que están conectado toohello servicio de StorSimple Manager y resalta los que necesitan la atención del administrador del sistema. Este tutorial presenta la página de panel de hello, explica la función y el contenido del panel de Hola y describe las tareas de Hola que puede realizar desde esta página.

![Panel del servicio](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

panel de servicio de StorSimple Manager Hello muestra hello siguiente información:

* Hola **gráfico** área, puede ver gráfico de métricas pertinente de Hola para sus dispositivos. Puede ver el almacenamiento principal de hello (localmente anclado y niveles) utilizado en todos los dispositivos de hello, así como el almacenamiento en nube Hola utilizado por dispositivos durante un período de tiempo. Usar controles de hello en la esquina superior derecha de Hola de hello gráfico toospecify una escala de tiempo de 1 semana, 1 mes, 3 meses o 1 año.
* Hola **información general del uso** muestra Hola almacenamiento principal aprovisionado y utilizado por todos los dispositivos toohello relativa almacenamiento total disponible en todos los dispositivos. **Aprovisionar** hace referencia toohello cantidad de almacenamiento que está preparado y asignado para su uso, mientras **usado** hace referencia toousage de volúmenes tal como lo ven los iniciadores de Hola que son dispositivos toohello conectado.
* Hola **alertas** área proporciona una instantánea de todas las alertas activas de hello en todos los dispositivos de hello, agrupadas por gravedad de alerta. Al hacer clic en el nivel de gravedad de hello abre hello **alertas** page, tooshow ámbito esas alertas. En hello **alertas** página, puede hacer clic en un detalles adicionales de tooview alertas individuales sobre esa alerta, incluido cualquier acción recomendada. También puede desactivar alerta Hola si se ha resuelto el problema de Hola.
* Hola **trabajos** área proporciona una instantánea de los trabajos recientes en todos los dispositivos que están conectados tooyour servicio. Hay vínculos que pueden usar toolook trabajos que están actualmente en curso, que han dado error en hello últimas 24 horas, o aquellos que están programados toorun Hola próximas 24 horas.
* Hola **vista rápida** área proporciona información útil, como el estado del servicio, el número de dispositivos conectados toohello servicio, la ubicación del servicio de Hola y detalles de suscripción de Hola que está asociado con el servicio de Hola. También hay un registro de operaciones de toohello de vínculo. Haga clic en hello vínculo toosee una lista de todas las operaciones de servicio de StorSimple Manager completadas.

Puede usar hello StorSimple Manager servicio panel página tooinitiate Hola siguientes tareas:

* Ver o volver a generar clave de registro del servicio de Hola.
* Cambiar la clave de cifrado de datos del servicio de Hola.
* Ver registros de operaciones de Hola.

## <a name="view-or-regenerate-hello-service-registration-key"></a>Ver o volver a generar clave de registro del servicio de Hola
clave de registro del servicio de Hello es tooregister usa un dispositivo de StorSimple de Microsoft Azure con el servicio StorSimple Manager hello, por lo que hello dispositivo aparece en hello portal de Azure clásico para otras acciones de administración. clave de Hola se creó en el primer dispositivo de Hola y comparte con el resto de Hola de los dispositivos.

Haga clic en **clave de registro** (final Hola de página Hola) se abre hello **clave de registro del servicio** cuadro de diálogo, siempre que sea posible cualquier copia Hola servicio Registro toohello clave Portapapeles actual o regenerar la clave de registro del servicio de Hola.

Regenerando la clave de hello no afecta a los dispositivos registrados anteriormente: afecta a solo los dispositivos de Hola que están registrados con el servicio de hello después Hola clave se regenera.

Para obtener más información sobre cómo ver y generar go clave, del registro de servicio Hola demasiado[clave de registro del servicio de Get hello](storsimple-manage-service.md#get-the-service-registration-key).

## <a name="change-hello-service-data-encryption-key"></a>Cambiar la clave de cifrado de datos del servicio de Hola
Claves de cifrado de datos de servicio son tooencrypt usado cliente confidencial datos, como las credenciales de cuenta de almacenamiento, que se envían desde el dispositivo de StorSimple de toohello de servicio de StorSimple Manager. Necesitará toochange estas claves periódicamente si su organización de TI tiene una directiva de rotación de claves en dispositivos de almacenamiento de Hola. Hello proceso de cambio de clave puede ser ligeramente diferente dependiendo de si hay un único dispositivo o varios dispositivos administrados por el servicio StorSimple Manager Hola.

Cambiar clave de cifrado de datos de servicio de hello es un proceso de 3 pasos:

1. Con hello portal de Azure clásico, autorizar a una clave de cifrado de datos de servicio de dispositivo toochange Hola.
2. Uso de Windows PowerShell para StorSimple, iniciar el cambio de clave de cifrado de datos de servicio de Hola.
3. Si tiene más de un dispositivo de StorSimple, actualizar clave de cifrado de datos de servicio de hello en hello otros dispositivos.

Hello pasos siguientes describen proceso de sustitución de hello para la clave de cifrado de datos del servicio de Hola.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>Ver registros de operaciones de Hola
Puede ver registros de operaciones de hello haciendo clic en vínculo de registros de operación Hola disponibles en hello **vista rápida** panel del panel de Hola de. Esto le llevará toohello administración página Servicios, donde puede filtrar y ver Hola registra el servicio StorSimple Manager tooyour específico.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[solucionar problemas de un dispositivo de StorSimple](storsimple-troubleshoot-operational-device.md).
* Más información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

