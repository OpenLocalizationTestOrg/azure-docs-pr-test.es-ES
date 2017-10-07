---
title: aaaMitigations - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
description: "Página mitigaciones para toohello Hola herramienta de modelado de amenazas de Microsoft de las soluciones posibles resaltado más expuesto genera las amenazas."
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
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Mitigaciones de Microsoft Threat Modeling Tool

Hola herramienta de modelado de amenazas es un elemento básico del saludo del ciclo de vida de desarrollo de seguridad (SDL) de Microsoft. Permite que el software arquitectos tooidentify y mitigar los posibles problemas de seguridad al principio, cuando están tooresolve relativamente sencilla y rentable. Como resultado, reduce en gran medida el costo total de desarrollo de Hola. Además, se han diseñado herramienta Hola con expertos en seguridad no en mente, facilitar el modelado de amenazas para todos los programadores al proporcionar instrucciones claras sobre cómo crear y analizar los modelos de amenazas.

Visite hello  **[herramienta de modelado de amenazas](./azure-security-threat-modeling-tool.md)**  tooget comenzar hoy!

## <a name="mitigation-categories"></a>Categorías de mitigación

las mitigaciones de herramienta de modelado de amenazas de Hola se clasifican según toohello marco de seguridad de aplicaciones Web, que consta de hello siguiente:

| Categoría | Descripción |
| -------- | ----------- |
| **[Auditoría y registro](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | ¿Quién hizo qué y cuándo? Auditoría y registro, consulte toohow sus eventos relacionados con la seguridad de registros de aplicación |
| **[Autenticación](./azure-security-threat-modeling-tool-authentication.md)** | ¿Quién es usted? La autenticación es el proceso Hola donde una entidad demuestra la identidad de Hola de otra entidad, normalmente a través de las credenciales, como un nombre de usuario y una contraseña |
| **[Autorización](./azure-security-threat-modeling-tool-authorization.md)** | ¿Qué puede hacer? La autorización es la forma en que la aplicación proporciona controles de acceso para los recursos y operaciones. |
| **[Seguridad en las comunicaciones](./azure-security-threat-modeling-tool-communication-security.md)** | ¿Con quién está hablando? La seguridad de comunicaciones garantiza que todas las comunicaciones realizadas sean lo más seguras posibles. |
| **[Administración de configuración](./azure-security-threat-modeling-tool-configuration-management.md)** | ¿Quién ejecuta la aplicación? ¿A qué bases de datos se conecta? ¿Cómo se administra la aplicación? ¿Cómo se protege esta configuración? Administración de configuración refiere toohow la aplicación controla estos problemas de funcionamiento |
| **[Criptografía](./azure-security-threat-modeling-tool-cryptography.md)** | ¿Cómo mantiene los secretos (confidencialidad)? ¿Cómo altera y corrige los datos o las bibliotecas (integridad)? ¿Cómo proporciona valores de inicialización para valores aleatorios que deben ser de alta seguridad criptográfica? La criptografía refiere toohow la aplicación aplica confidencialidad e integridad |
| **[Administración de excepciones](./azure-security-threat-modeling-tool-exception-management.md)** | Cuando se produce un error en una llamada al método en la aplicación, ¿qué hace la aplicación? ¿Cuánta información revela? ¿Devuelven error descriptivo tooend información que los usuarios? ¿Pase el autor de llamada de excepción valiosa información toohello atrás? ¿La aplicación da errores leves? |
| **[Validación de entradas](./azure-security-threat-modeling-tool-input-validation.md)** | ¿Cómo sé que recibe de la aplicación de entrada de hello es válido y seguro? Validación de entrada hace referencia toohow la aplicación filtra, anula o rechaza la entrada antes del procesamiento adicional. Considere la posibilidad de restringir las entradas a través de puntos de entrada y de codificar las salidas a través de puntos de salida. ¿Confía en datos de orígenes como bases de datos y recursos compartidos de archivos? |
| **[Información confidencial](./azure-security-threat-modeling-tool-sensitive-data.md)** | ¿Cómo maneja la aplicación la información confidencial? Los datos confidenciales refieren toohow que la aplicación controla los datos que deben protegerse en la memoria, a través de la red hello, o en almacenes permanentes |
| **[Administración de sesiones](./azure-security-threat-modeling-tool-session-management.md)** | ¿Cómo controla y protege la aplicación las sesiones de usuario? Una sesión refiere tooa serie de interacciones relacionadas entre un usuario y la aplicación Web |

Esto ayuda a identificar:

* Donde es hello más comunes cometidos.
* Donde es hello las mejoras más procesables

Como resultado, utilice estos toofocus categorías y priorizar el trabajo de seguridad, por lo que si sabe que se producen problemas de seguridad más frecuentes de hello en categorías de validación, la autenticación y autorización de entrada hello, puede empezar por ahí. Para obtener más información, consulte **[este vínculo de patente](https://www.google.com/patents/US7818788)**

## <a name="next-steps"></a>Pasos siguientes

Visite  **[amenazas de herramienta de modelado de amenazas](./azure-security-threat-modeling-tool-threats.md)**  toolearn más información sobre Hola amenaza para la herramienta de categorías hello usa toogenerate amenazas de diseño posible.
