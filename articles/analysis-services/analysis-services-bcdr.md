---
title: alta disponibilidad de Analysis Services aaaAzure | Documentos de Microsoft
description: Garantizar una alta disponibilidad de Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Alta disponibilidad de Azure Analysis Services
En este artículo se describe cómo garantizar la alta disponibilidad de los servidores de Azure Analysis Services. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>Garantizar la alta disponibilidad durante una interrupción del servicio
Aunque es poco habitual, en los centros de datos de Azure pueden producirse interrupciones. Cuando esto ocurre, provoca también una interrupción en el negocio que podría extenderse unos pocos minutos o incluso horas. La alta disponibilidad se suele lograr con la redundancia de servidores. Con Azure Analysis Services, la redundancia se obtiene gracias a la creación de servidores secundarios adicionales en una o varias regiones. Al crear servidores redundantes, datos de hello tooassure y metadatos en esos servidores está sincronizado con el servidor de hello en una región que se ha desconectado, puede:

* Implementar modelos tooredundant servidores en otras regiones. Este método requiere el procesamiento en paralelo de los datos en el servidor principal y en los servidores redundantes, lo que asegura que todos los servidores están sincronizados.

* Realizar copias de seguridad de las bases de datos del servidor principal y restaurarlas en los servidores redundantes. Por ejemplo, puede automatizar el almacenamiento de copias de seguridad por la noche tooAzure y restaurar tooother servidores redundantes en otras regiones. 

En cualquier caso, si el servidor principal produce una interrupción, debe cambiar las cadenas de conexión de hello en los clientes tooconnect toohello servidor en otro centro de datos regional de informes. Este cambio debe considerarse un último recurso y solo si se produce una interrupción catastrófica del centro de datos regional. Es más probable que una interrupción en el centro de datos que hospeda el servidor principal se recupere antes de que se puedan actualizar las conexiones en todos los clientes. 



## <a name="related-information"></a>Información relacionada
[Copia de seguridad y restauración](analysis-services-backup.md)   
[Administración de Azure Analysis Services](analysis-services-manage.md) 

