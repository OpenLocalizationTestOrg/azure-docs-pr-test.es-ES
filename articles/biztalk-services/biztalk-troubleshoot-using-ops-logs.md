---
title: Servicios de BizTalk de aaaTroubleshoot mediante registros de operaciones | Documentos de Microsoft
description: Solucione los problemas de los Servicios de BizTalk con el uso de registros de operaciones. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>Servicios de BizTalk: solución de problemas mediante registros de operaciones

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>¿Cuáles son los registros de operaciones de Hola
Registros de operaciones es una característica de los servicios de administración disponible en hello portal de Azure clásico que le permite tooview registros históricos de las operaciones realizadas en los servicios de Azure, incluidos los servicios de BizTalk. Esto le permite tooview los datos históricos relacionados con operaciones de toomanagement en su suscripción de BizTalk Service anteriores hasta 180 días.

> [!NOTE]
> Esta característica captura solo los registros para las operaciones de administración en servicios de BizTalk, como cuando se inició el servicio de hello, copia de seguridad, y así sucesivamente. Estas operaciones se realiza un seguimiento con independencia de si se realizan desde el portal de Azure clásico de Hola o mediante hello [API de REST de servicios de BizTalk](http://msdn.microsoft.com/library/azure/dn232347.aspx). Para obtener una lista completa de las operaciones que se siguen mediante los Servicios de administración, consulte [Seguimiento de operaciones mediante Servicios de administración de Azure](#bizops).<br/><br/>
> Esto no captura registros Hola para las actividades relacionadas tooBizTalk en tiempo de ejecución de servicio (por ejemplo, el mensaje procesado por puentes etc.).. tooview estos registros, use Hola vista de seguimiento desde el portal de servicios de BizTalk Hola. Para obtener más información, consulte [Mensajes de seguimiento](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>Consulta de los registros de operaciones de los Servicios BizTalk
1. Hola portal de Azure clásico, seleccione **servicios de administración de**y, a continuación, seleccione hello **registros de operaciones** ficha.
2. Puede filtrar los registros de hello en función de distintos parámetros como suscripción, intervalo de fechas, el tipo de servicio (por ejemplo, los servicios de BizTalk), nombre del servicio o estado de operación de hello (correcto, error).
3. Hola seleccione marca de verificación tooview Hola filtra la lista. Hello imagen siguiente muestran las actividades relacionadas tootestbiztalkservice: ![ver registros de operaciones][ViewLogs] 
4. tooview más información acerca de una operación específica, seleccione la fila de Hola y haga clic en **detalles** en la barra de tareas de hello en parte inferior de Hola.

## <a name="bizops"></a>Seguimiento de operaciones mediante Servicios de administración de Azure
Hello tabla siguiente enumeran las operaciones de Hola que se realiza un seguimiento con servicios de administración de Azure de hello:

| Nombre de la operación | Tarea |
| --- | --- |
| CreateBizTalkService |Operación toocreate un nuevo BizTalk Service |
| DeleteBizTalkService |Operación toodelete un BizTalk Service |
| RestartBizTalkService |Operación toorestart un BizTalk Service |
| StartBizTalkService |Operación toostart un BizTalk Service |
| StopBizTalkService |Operación toostop un BizTalk Service |
| DisableBizTalkService |Operación toodisable un BizTalk Service |
| EnableBizTalkService |Operación tooenable un BizTalk Service |
| BackupBizTalkService |Tooback de operación de un BizTalk Service |
| RestoreBizTalkService |Operación toorestore un BizTalk Service de copia de seguridad especificada |
| SuspendBizTalkService |Operación toosuspend un BizTalk Service |
| ResumeBizTalkService |Operación tooresume un BizTalk Service |
| ScaleBizTalkService |Operación tooscale a BizTalk Service hacia arriba o hacia abajo |
| ConfigUpdateBizTalkService |Configuración de hello tooupdate de operación de un BizTalk Service |
| ServiceUpdateBizTalkService |Operación tooupgrade o degradación de una versión diferente de BizTalk Service tooa |
| PurgeBackupBizTalkService |Copias de seguridad de operación toopurge de hello BizTalk Service fuera del período de retención de Hola |

## <a name="see-also"></a>Otras referencias
* [Copia de seguridad del servicio de BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Restauración del servicio de BizTalk a partir de una copia de seguridad](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Servicios de BizTalk: gráfico del estado de aprovisionamiento](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Servicios de BizTalk: pestañas Panel, Monitor y Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Servicios de BizTalk: limitaciones](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Servicios de BizTalk: nombre del emisor y clave del emisor](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

