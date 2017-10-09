---
title: aaaThreats - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
description: "Página de categorías de amenaza de hello herramienta de modelado de amenazas de Microsoft, que contiene categorías para todos los expone genera las amenazas."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Amenazas de Microsoft Threat Modeling Tool

Hola herramienta de modelado de amenazas es un elemento básico del saludo del ciclo de vida de desarrollo de seguridad (SDL) de Microsoft. Permite que el software arquitectos tooidentify y mitigar los posibles problemas de seguridad al principio, cuando están tooresolve relativamente sencilla y rentable. Como resultado, reduce en gran medida el costo total de desarrollo de Hola. Además, se han diseñado herramienta Hola con expertos en seguridad no en mente, facilitar el modelado de amenazas para todos los programadores al proporcionar instrucciones claras sobre cómo crear y analizar los modelos de amenazas.

> Visite hello  **[herramienta de modelado de amenazas](./azure-security-threat-modeling-tool.md)**  tooget comenzar hoy!

Hola herramienta de modelado de amenazas le ayuda a responder a ciertas cuestiones, como Hola los siguientes:

* ¿Cómo un atacante puede cambiar los datos de autenticación de saludo?
* ¿Cuál es el impacto de hello si un atacante puede leer datos de perfil de usuario de hello?
* ¿Qué ocurre si se deniega el acceso base de datos de perfil de usuario de toohello?

## <a name="stride-model"></a>Modelo STRIDE

Ayuda de toobetter formular estos tipos de preguntas que apunta, modelo STRIDE de Microsoft usa hello, que clasifica los distintos tipos de amenazas y simplifica Hola conversaciones de seguridad global.

| Categoría | Descripción |
| -------- | ----------- |
| **Suplantación de identidad** | Implica el acceso y uso ilícitos de la información de autenticación de otro usuario, como el nombre de usuario y la contraseña. |
| **Alteración de datos** | Implica la modificación malintencionada de Hola de datos. Algunos ejemplos son los cambios no autorizados realizados toopersistent datos, como el que se mantienen en una base de datos y la modificación de datos Hola medida que fluye entre dos equipos a través de una red abierta, como Internet Hola |
| **Rechazo** | Asociado a los usuarios que denegación la realización de una acción sin otras entidades con cualquier forma tooprove en caso contrario, por ejemplo, un usuario realiza una operación no válida en un sistema que carezca de las operaciones de hello capacidad tootrace Hola prohibida. Sin rechazo refiere toohello capacidad de una amenazas de rechazo de sistema toocounter. Por ejemplo, un usuario que compra un producto podría tener toosign elemento Hola tras la recepción. proveedor de Hello puede, a continuación, use Hola firmado recepción como ese usuario Hola ha recibido paquetes de saludo de prueba |
| **Divulgación de información** | Implica la exposición de Hola de tooindividuals de información que no deberían toohave acceso tooit: por ejemplo, capacidad de Hola de usuarios tooread un archivo que no tenían acceso a, o hello posibilidad de que un intruso tooread los datos en tránsito entre dos equipos |
| **Denegación de servicio** | Denegar el servicio (DoS) ataques por denegación de servicio toovalid a los usuarios: por ejemplo, si realiza un servidor Web temporalmente no disponible o inutilizable. Debe proteger contra ciertos tipos de DoS amenazas simplemente tooimprove la disponibilidad del sistema y la confiabilidad |
| **Elevación de privilegios** | Un usuario sin privilegios obtiene acceso con privilegios y, por tanto, tiene suficientes toocompromise de acceso o destruir Hola todo el sistema. Elevación de amenazas de privilegios incluyen aquellas situaciones en que un atacante eficazmente ha entrado en todas las defensas del sistema y pasan a formar parte del sistema de hello confianza propio, de hecho, una situación peligrosa |

## <a name="next-steps"></a>Pasos siguientes

Continuar demasiado**[reducciones de herramienta de modelado de amenazas](./azure-security-threat-modeling-tool-mitigations.md)**  toolearn Hola maneras puede mitigar estas amenazas con Azure.
