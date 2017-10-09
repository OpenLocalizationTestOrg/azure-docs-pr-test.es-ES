---
title: "contenido de CDN de Azure por país aaaRestrict | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorestrict acceso tooyour CDN de Azure contenido con Hola la característica filtrado de replicación geográfica."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>Restricción del contenido de la red CDN de Azure por país

## <a name="overview"></a>Información general
Cuando un usuario solicita el contenido, de forma predeterminada, se sirve contenido de hello, independientemente de donde usuario Hola efectúe esta solicitud de. En algunos casos, puede que desee toorestrict tener acceso al contenido de tooyour por país. Este tema se explica cómo hello toouse **filtrado geográfica** característica en orden tooconfigure Hola servicio tooallow o bloquear el acceso por país.

> [!IMPORTANT]
> productos de Verizon y Akamai Hola proporcionan Hola la misma funcionalidad de filtrado de replicación geográfica, pero tiene una pequeña diferencia en los códigos de país te admiten. Vea el paso 3 para un diferencias toohello de vínculo.


Para obtener información acerca de las consideraciones que se aplican tooconfiguring este tipo de restricción, vea hello [consideraciones](cdn-restrict-access-by-country.md#considerations) sección final Hola de tema de Hola.  

![Filtrado por país](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>Paso 1: Definir la ruta de acceso de directorio de Hola
Seleccione el punto de conexión en el portal de Hola y esta característica se encuentra ficha filtrado geográfica de hello en hello toofind de navegación izquierdo.

Al configurar un filtro de país, debe especificar a los usuarios de hello ruta de acceso relativa toohello ubicación toowhich se permitirá o denegará el acceso. Puede aplicar el filtrado geográfico para todos los archivos mediante "/" o carpetas seleccionadas especificando las rutas de acceso de directorio "/pictures/". También puede aplicar filtrado geográfica tooa archivo único mediante la especificación de archivo hello y, omitiendo Hola barra diagonal "/ imágenes/ciudad.png".

Filtro de ruta de acceso del directorio de ejemplo:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>Paso 2: Definir la acción de hello: bloquear o permitir
**Bloquear:** a los usuarios de hello especificaron se denegarán países tooassets de acceso solicitado desde esa ruta de acceso de recursiva. Si no se han configurado otras opciones de filtrado de país para esa ubicación, a continuación, se permitirá acceso a todos los demás usuarios.

**Permitir:** solo los usuarios de hello especificaron países podrán tooassets de acceso solicitado desde esa ruta de acceso de recursiva.

## <a name="step-3-define-hello-countries"></a>Paso 3: Definir países Hola
Seleccione los países Hola que desee tooblock o permiten la ruta de acceso de Hola. 

Por ejemplo, regla de Hola de bloqueo /Photos/Estrasburgo/filtrará archivos incluidos:

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>Códigos de país
Hola **filtrado geográfica** característica utiliza país códigos toodefine Hola países desde la que pueden permitir o bloquear una solicitud para un directorio seguro. Encontrará Hola códigos de país de [códigos de país de CDN de Azure](https://msdn.microsoft.com/library/mt761717.aspx). 

## <a id="considerations"></a>Consideraciones
* Puede tardar minutos too90 Verizon, o un par de minutos con Akamai, para cambios tooyour país configuración tootake efecto del filtrado.
* Esta característica no admite caracteres comodín (por ejemplo, ‘*’).
* configuración de filtrado de replicación geográfica de Hello asociado a la ruta de acceso relativa de hello será la ruta de acceso de toothat de aplica de forma recursiva.
* Solo una regla puede ser aplicada toohello misma ruta de acceso relativa (no se puede crear varios filtros de país que toohello punto misma ruta de acceso relativa. Sin embargo, una carpeta puede tener varios filtros de país. Esto es debido a toohello recursiva naturaleza de los filtros de país. En otras palabras, se puede asignar un filtro de país diferente a una subcarpeta de una carpeta configurada previamente.

