---
title: "¿aaaWhat es el programador de Azure? | Microsoft Docs"
description: "El programador de Azure le permite toodeclaratively describen toorun de acciones en la nube de Hola. A continuación, programa y ejecuta esas acciones de forma automática."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a>¿Qué es el Programador de Azure?
El programador de Azure le permite toodeclaratively describen toorun de acciones en la nube de Hola. A continuación, programa y ejecuta esas acciones de forma automática.  Programador lo hace al utilizar [Hola portal de Azure](scheduler-get-started-portal.md), código, [API de REST](https://msdn.microsoft.com/library/mt629143.aspx), o Azure PowerShell.

El Programador crea, mantiene e invoca el trabajo programado.  El Programador no hospeda ninguna carga de trabajo ni ejecuta código. Solo *invoca* código hospedado en cualquier otro lugar (en Azure, localmente o con otro proveedor). Realiza la invocación mediante HTTP, HTTPS, una cola de almacenamiento, una cola de bus de servicio o un tema de bus de servicio.

Programaciones de programador [trabajos](scheduler-concepts-terms.md), mantiene un historial de resultados de la ejecución de trabajo que uno puede revisar y ejecutar la toobe de las cargas de trabajo de programaciones determinista y confiable. WebJobs de Azure (parte de la característica de las aplicaciones Web de hello en el servicio de aplicación de Azure) y otras capacidades de programación Azure utilizan el programador en segundo plano de Hola. Hola [API de REST de Scheduler](https://msdn.microsoft.com/library/mt629143.aspx) le ayuda a administrar las comunicaciones de Hola de estas acciones. De ese modo, el Programador admite [programaciones complejas y periodicidad avanzada](scheduler-advanced-complexity.md) con facilidad.

Hay varios escenarios que se prestan toohello uso del programador. Por ejemplo:

* *Acciones de aplicaciones recurrentes*: recopilación periódica de datos desde Twitter en una fuente.
* *Mantenimiento diario*: eliminación diaria de registros, realización de copias de seguridad y otras tareas de mantenimiento. Por ejemplo, un administrador puede elegir tooback la base de datos de Hola a la 1:00 A.M. todos los días para hello en los próximos meses nueve.

Programador permite toocreate, actualizar, eliminar, ver y administrar trabajos y [las colecciones de trabajos](scheduler-concepts-terms.md) mediante programación, mediante el uso de scripts y en el portal de Hola.

## <a name="see-also"></a>Otras referencias
 [Conceptos, terminología y jerarquía de entidades de Programador de Azure](scheduler-concepts-terms.md)

 [Empezar a usar a Scheduler en hello portal de Azure](scheduler-get-started-portal.md)

 [Planes y facturación en Programador de Azure](scheduler-plans-billing.md)

 [¿Cómo se programa toobuild complejo y periodicidad avanzada con el programador de Azure](scheduler-advanced-complexity.md)

 [Referencia de API de REST de Programador de Azure](https://msdn.microsoft.com/library/mt629143)

 [Referencia de cmdlets de PowerShell de Programador de Azure](scheduler-powershell-reference.md)

 [Alta disponibilidad y confiabilidad de Programador de Azure](scheduler-high-availability-reliability.md)

 [Límites, valores predeterminados y códigos de error de Programador de Azure](scheduler-limits-defaults-errors.md)

 [Autenticación de salida de Programador de Azure](scheduler-outbound-authentication.md)

