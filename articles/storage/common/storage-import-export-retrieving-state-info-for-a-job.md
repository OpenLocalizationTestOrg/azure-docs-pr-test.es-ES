---
title: "información de estado de aaaRetrieving para un trabajo de importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooobtain información de estado para los trabajos de servicio de importación y exportación de Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>Recuperación de la información de estado de un trabajo de Import/Export
Puede llamar a hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operación tooretrieve saber ambos importar y exportar los trabajos. información de Hello devuelta incluye:

-   estado actual de Hola de trabajo de Hola.

-   porcentaje aproximado de Hola que cada trabajo se ha completado.

-   estado actual de Hola de cada unidad.

-   URI de blobs que contienen registros de errores e información de registro detallada (si está habilitada).

Hello las secciones siguientes explican información de hello devuelta por hello `Get Job` operación.

## <a name="job-states"></a>Estados de trabajo
tabla de Hola y diagrama de estado de hello siguientes describen los Estados de Hola que un trabajo recorre durante su ciclo de vida. se puede determinar el estado actual de Hola de trabajo de Hola mediante Hola que realiza la llamada `Get Job` operación.

![Estados de trabajo](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "Estados de trabajo")

Hello siguiente tabla describe cada estado que puede pasar un trabajo.

|Estado de trabajo|Descripción|
|---------------|-----------------|
|`Creating`|Después de llamar a la operación Put Job de hello, se crea un trabajo y su estado se establece demasiado`Creating`. Mientras se encuentra el trabajo de hello en hello `Creating` estado, Hola servicio de importación/exportación se da por supuesto que las unidades de hello no han sido enviados toohello centro de datos. Un trabajo puede permanecer en hello `Creating` estado tootwo semanas, después de que este se eliminará automáticamente por el servicio de Hola.<br /><br /> Si se llama a operación Actualizar propiedades del trabajo de hello mientras está trabajo Hola Hola `Creating` de estado, el trabajo de hello permanece en Hola `Creating` de estado y tiempo de espera de Hola intervalo es restablecer tootwo semanas.|
|`Shipping`|Después de enviar el paquete, debe llamar a Hola actualizar propiedades del trabajo operación Hola estado de actualización de trabajo de hello demasiado`Shipping`. Hola trasvase estado puede establecerse solo si hello `DeliveryPackage` (transportista y número de seguimiento) hello y `ReturnAddress` propiedades se han configurado para el trabajo de Hola.<br /><br /> Hola trabajo permanecerá en estado de envío de Hola para tootwo semanas. Si han pasado dos semanas y aún no han recibido las unidades de hello, operadores de servicio de importación y exportación de hello le notificará.|
|`Received`|Después de que todas las unidades se han recibido en el centro de datos de hello, se establecerá el estado del trabajo de hello toohello estado recibido.|
|`Transferring`|Después de que las unidades de Hola se han recibido en el centro de datos de Hola y al menos una unidad ha comenzado el procesamiento, se establecerá el estado del trabajo de hello toohello `Transferring` estado. Vea hello `Drive States` sección para obtener información detallada.|
|`Packaging`|Cuando todas las unidades de procesamiento han completado, el trabajo de Hola se colocarán en hello `Packaging` estado hasta que las unidades de hello son cliente enviada toohello back.|
|`Completed`|Una vez todas las unidades se han enviado toohello back-cliente, si se ha completado el trabajo de hello sin errores, a continuación, Hola se establecerá toohello `Completed` estado. Hello trabajo se eliminarán automáticamente después de 90 días en hello `Completed` estado.|
|`Closed`|Una vez todas las unidades se han enviado toohello back-cliente, si ha habido algún error durante el procesamiento de Hola de trabajo de hello, a continuación, Hola se establecerá toohello `Closed` estado. Hello trabajo se eliminarán automáticamente después de 90 días en hello `Closed` estado.|

Un trabajo solo se puede cancelar con determinados estados. Un trabajo cancelado omite el paso de copia de datos de hello, pero en caso contrario, sigue Hola mismo transiciones de estado como un trabajo que no se ha cancelado.

Hello tabla siguiente describen los errores que pueden aparecer para cada estado del trabajo, así como el efecto de hello en el trabajo de hello cuando se produce un error.

|Estado de trabajo|Evento|Resolución y pasos siguientes|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|Ha llegado una o varias unidades para un trabajo, pero trabajo hello no está en hello `Shipping` estado o no hay ningún registro de trabajo de hello en el servicio de Hola.|equipo de operaciones de servicio de importación y exportación de Hola se intente toocontact Hola cliente toocreate o actualizar el trabajo de hello con trabajo al día de la información necesaria toomove Hola.<br /><br /> Si equipo de operaciones de hello está cliente de hello toocontact no se puede menos de dos semanas, equipo de operaciones de hello intentarán tooreturn Hola unidades.<br /><br /> En caso de Hola que no se puede devolver las unidades de hello y no se puede alcanzar el cliente de hello, unidades de Hola se destruirán segura de 90 días.<br /><br /> Tenga en cuenta que no se puede procesar un trabajo hasta que su estado se actualiza demasiado`Shipping`.|
|`Shipping`|paquete de Hola de un trabajo no ha llegado durante más de dos semanas.|equipo de operaciones de Hello notificará a cliente hello del paquete falta Hola. En función de la respuesta del cliente de hello, equipo de operaciones de Hola se en ampliar Hola intervalo toowait para tooarrive de paquete de hello, o en Cancelar trabajo Hola.<br /><br /> En caso de hello ese cliente hello no se pondrá en contacto o no responde dentro de 30 días, equipo de operaciones de Hola iniciará el trabajo de acción toomove Hola de hello `Shipping` estado directamente toohello `Closed` estado.|
|`Completed/Closed`|Hola unidades nunca alcanza el remite Hola o se dañaron durante el envío (se aplica solo tooan trabajo de exportación).|Si Hola unidades no llegan a la dirección de devolución de Hola, cliente hello debe operación Get Job de primera llamada Hola o comprobar el estado del trabajo de hello en Hola tooensure portal ese Hola unidades de disco. Si se han enviado las unidades de Hola, cliente hello debe póngase en contacto con hello envío proveedor tootry y busque Hola unidades.<br /><br /> Si Hola unidades se dañaron durante el envío, cliente hello quizás desee toorequest otro trabajo de exportación, o blobs que faltan de Hola de descarga.|
|`Transferring/Packaging`|El trabajo no tiene dirección de devolución o es incorrecta.|equipo de operaciones de Hola se dirigirá la persona de contacto toohello Hola trabajo tooobtain Hola dirección es correcta.<br /><br /> En caso de hello ese cliente hello no se puede alcanzar, Hola unidades de disco se destruirán de forma segura en 90 días.|
|`Creating / Shipping/ Transferring`|Una unidad que no aparece en la lista de Hola de toobe unidades importado se incluye en hello paquete de envío.|Hello unidades adicionales no se procesará y se devolverá al cliente de toohello cuando se completa el trabajo de Hola.|

## <a name="drive-states"></a>Estados de unidad
tabla de Hola y diagrama de hello siguiente describen el ciclo de vida de Hola de una unidad de disco individual durante su transición a través de un trabajo de importación o exportación. Puede recuperar el estado actual de la unidad de Hola por Hola que realiza la llamada `Get Job` operación e inspeccionando hello `State` elemento de hello `DriveList` propiedad.

![Estados de unidad](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "Estados de unidad")

Hello siguiente tabla describe cada estado que puede pasar una unidad.

|Estado de la unidad|Descripción|
|-----------------|-----------------|
|`Specified`|Para un trabajo de importación, cuando se crea el trabajo de hello con hello operación Put Job, estado inicial de Hola para una unidad es hello `Specified` estado. Para un trabajo de exportación, ya que no se especifica ninguna unidad cuando se crea el trabajo de hello, estado de la unidad de disco inicial de hello es hello `Received` estado.|
|`Received`|unidad de Hello cambia toohello `Received` estado cuando hello operador del servicio de importación y exportación ha procesado las unidades de Hola que se han recibido de hello trasvase de empresa para un trabajo de importación. Para un trabajo de exportación, estado de la unidad de disco inicial de hello es hello `Received` estado.|
|`NeverReceived`|unidad de disco de Hello pasará toohello `NeverReceived` estado cuando hello llega el paquete de un trabajo pero paquete hello no contiene la unidad de Hola. También puede mover una unidad a este estado si han pasado dos semanas ya que Hola servicio ha recibido información de envío de hello, pero paquete Hola aún no ha llegado al centro de datos de Hola.|
|`Transferring`|Una unidad de disco pasará toohello `Transferring` estado cuando hello servicio comienza tootransfer datos de hello unidad tooWindows almacenamiento de Azure.|
|`Completed`|Una unidad de disco pasará toohello `Completed` estado al servicio de hello haya transferido correctamente todos los datos de hello sin errores.|
|`CompletedMoreInfo`|Una unidad de disco pasará toohello `CompletedMoreInfo` estado al servicio Hola haya encontrado algún problema mientras copiaba datos desde o unidad de toohello. Hola información puede incluir errores, advertencias o mensajes informativos sobre sobrescribir blobs.|
|`ShippedBack`|unidad de disco de Hello pasará toohello `ShippedBack` estado cuando se ha enviado desde la dirección de retorno de toohello de hello datos centro de nuevo.|

Hello tabla siguiente describen los Estados de error de unidad de Hola y las acciones de hello realizadas para cada estado.

|Estado de la unidad|Evento|Resolución y paso siguiente|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|Una unidad que está marcada como `NeverReceived` (porque no se recibió como parte de envío del trabajo de hello) llega en otro envío.|equipo de operaciones de Hello moverá Hola unidad toohello `Received` estado.|
|`N/A`|Una unidad que no forma parte de cualquier trabajo llega al centro de datos de hello como parte de otro trabajo.|unidad de Hola se marcará como una unidad de disco adicional y se devolverá al cliente de toohello cuando se completa el trabajo de hello asociado con el paquete original Hola.|

## <a name="faulted-states"></a>Estados de error
Cuando un trabajo o una unidad no puede tooprogress normalmente a través de su ciclo de vida esperado, el trabajo de Hola o unidad se moverán a un `Faulted` estado. En ese momento, el equipo de operaciones de hello pondrá en contacto con cliente de Hola por correo electrónico o teléfono. Una vez resuelto el problema de hello, Hola generó un error de trabajo o unidad pasará fuera hello `Faulted` estado y se pondrá en hello adecuados estado.

## <a name="next-steps"></a>Pasos siguientes

* [Usar servicio de importación y exportación de hello API de REST](storage-import-export-using-the-rest-api.md)
