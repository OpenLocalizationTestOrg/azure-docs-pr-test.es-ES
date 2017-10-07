---
title: "aaaWhat toodo en caso de hello de una interrupción del servicio de Azure que afecta al almacén de claves de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué toodo en caso de hello de una interrupción del servicio de Azure que afecta al almacén de claves de Azure."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Redundancia y disponibilidad del Almacén de claves de Azure
Almacén de claves de Azure ofrece varios niveles de redundancia toomake seguro de que sus claves y secretos seguirán siendo aplicación tooyour disponible incluso si los componentes individuales de hello producirá un error de servicio.

Hello contenido de su almacén de claves se replica dentro de la región de Hola y región secundaria tooa al menos 150 millas inmediatamente, pero dentro de hello mismo geography. Así se mantiene la durabilidad de las claves y los secretos. Vea hello [Azure emparejado regiones](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) documento para obtener más información sobre los pares de región específica.

Si se produce un error en componentes individuales de servicio de almacén de claves de hello, componentes alternativos dentro de la región de hello paso en tooserve su toomake solicitud seguro de que no hay ninguna degradación de la funcionalidad. No es necesario tootake cualquier acción tootrigger esto. Se produce automáticamente y será tooyou transparente.

En el caso poco frecuente de Hola que toda una región de Azure no está disponible, automáticamente se enrutan las solicitudes de hello realizados de almacén de claves de Azure en dicha región (*conmutarán por error*) tooa de región secundaria. Cuando la región principal de hello esté disponible de nuevo, las solicitudes se enrutan volver (*no se pudo volver*) toohello de región principal. Una vez más, no es necesario tootake ninguna acción porque esto sucede automáticamente.

Hay unos toobe advertencias en cuenta:

* En caso de hello de una región de conmutación por error, puede tardar unos minutos para hello servicio toofail. Las solicitudes realizadas durante este período, pueden producir un error hasta que se complete la conmutación por error de Hola.
* Una vez finalizada una conmutación por error, el almacén de claves se encontrará en modo de solo lectura. Las solicitudes compatibles con este modo son las siguientes:
  * Enumeración de almacenes de claves
  * Obtención de propiedades de los almacenes de claves
  * Enumeración de secretos
  * Obtención de secretos
  * Enumeración de claves
  * Obtención de (propiedades de) claves
  * Cifrar
  * Descifrado
  * Encapsulado
  * Desencapsulado
  * Verify
  * Firma
  * Copia de seguridad
* Cuando tenga lugar la conmutación por error, todos los tipos de solicitudes (incluidas de lectura *y* escritura) pasarán a estar disponibles.

