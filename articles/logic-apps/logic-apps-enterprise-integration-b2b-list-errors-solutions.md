---
title: 'Lista de errores y soluciones para Logic Apps B2B: Azure App Service | Microsoft Docs'
description: Lista de errores y soluciones para Logic Apps B2B
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Lista de errores y soluciones para Logic Apps B2B  
Este artículo le ayuda a solucionar los errores que puedan ocurrir en escenarios de Logic Apps B2B y le sugiere las acciones adecuadas para corregirlos.


## <a name="agreement-resolution"></a>Resolución de contrato

### <a name="no-agreement-found"></a>*No agreement found (No se encontró ningún contrato) 

|   |   |  
|---|---|
| Descripción del error | No se encontró ningún contrato con parámetros de resolución de contrato|    
| Acción del usuario | acuerdo de Hello debe agregarse toohello cuenta de integración con las identidades de negocio acordada.</br> las identidades de negocio Hola deben coincidir con el Id. de mensaje de entrada de toohello|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* No se encontró ningún contrato con las identidades

|   |   | 
|---|---|
| Descripción del error | No se encontró ningún contrato con las identidades: 'AS2Identity'::'Partner1' y 'AS2Identity'::'Partner3'| 
| Acción del usuario | AS2 no válido-desde o AS2-tooconfigured para el acuerdo. </br> Mensaje de AS2 correcto AS2-de o identificadores de toomatch AS2 AS2 tooheaders o acuerdo AS2 encabezados con configuraciones de contrato de mensaje |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* Missing AS2 message headers (Faltan encabezados del mensaje AS2)  

|   |   |  
|---|---|
| Descripción del error| Encabezados AS2 no válidos. Uno de los encabezados "AS2-To" o "AS2-From" está vacío| 
| Acción del usuario | Se recibió un mensaje AS2 que no contenía Hola AS2-de o AS2 tooor ambos encabezados. </br> Compruebe el mensaje AS2 AS2-de y tooheaders de AS2 y corríjalas en función de la configuración del acuerdo |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* Missing AS2 message body and headers (Faltan el cuerpo y los encabezados del mensaje AS2)    

|   |   |  
|---|---|
| Descripción del error| contenido de la solicitud de Hello es nulo o está vacío | 
| Acción del usuario | Se recibió un mensaje AS2 que no contiene el cuerpo del mensaje Hola |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* AS2 message decryption failure (Error de descifrado del mensaje AS2)

|   |   | 
|---|---|
| Descripción del error |  [processed/Error: decryption-failed] | 
| Acción del usuario | Agregar @base64ToBinary tooAS2Message antes de enviar toopartner 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* MDN decryption failure﻿ (Error de descifrado de MDN)

|   |   | 
|---|---|
| Descripción del error |  [processed/Error: decryption-failed] | 
| Acción del usuario | Agregar @base64ToBinary tooMDN antes de enviar toopartner 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* Missing signing certificate (Falta el certificado de firma)

|   |   |  
|---|---|
| Descripción del error| Hello certificado de firma no se configuró para la entidad AS2. </br> AS2-From: partner1 AS2-To: partner2 | 
| Acción del usuario | Configure el contrato AS2 con el certificado correcto para la firma |
|  |  | 

## <a name="x12-and-edifact"></a>X12 y EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* Espacio inicial o final detectado    
    
|   |   | 
|---|---|
| Descripción del error | Error al analizar. Hola conjunto de transacciones con Id. ' 123456 'contenido en el intercambio (sin grupo) con el identificador ' 987654', Id. de remitente 'Partner1', Id. de destinatario 'Asociado2' se está suspendiendo por los errores siguientes: A la izquierda finales separador que se encuentra |
| Acción del usuario | Hola acuerdo configuración toobe configurado tooallow espacios iniciales y finales. </br> Editar acuerdo configuración tooallow espacios iniciales y finales |
|   |   |

![permitir espacio](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Comprobación de duplicados habilitó en el acuerdo de Hola

|   |   | 
|---|---| 
| Descripción del error | Número de control duplicado |
| Acción del usuario | Este error indica que el mensaje Hola recibido tiene números de control duplicados. </br> Corrija el número de control de Hola y enviar mensajes de bienvenida |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Esquema que falta en el acuerdo de Hola

|   |   | 
|---|---| 
| Descripción del error | Error al analizar. conjunto de transacciones de Hello X12 con Id. '564220001' contenidos en el grupo funcional con Id. '56422', en el intercambio con Id. '000056422', Id. de remitente ' 12345678', Id. de destinatario ' 87654321' se está suspendiendo por los errores siguientes "mensaje de saludo tiene un ty de documento desconocido PE y no se resolvió tooany de esquemas existente Hola configurado en el acuerdo de hello " |
| Acción del usuario | Configurar el esquema de configuración de un acuerdo Hola  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Esquema incorrecto en el acuerdo de Hola

|   |   | 
|---|---| 
| Descripción del error | mensaje de saludo tiene un tipo de documento desconocido y no resolvió tooany de esquemas existente Hola configurado en el acuerdo de Hola. |
| Acción del usuario | Configurar el esquema correcto en la configuración de acuerdo Hola  |
|   |   |

## <a name="flat-file"></a>Archivo plano

### <a name="-input-message-with-no-body"></a>* Input message with no body (Mensaje de entrada sin cuerpo)

|   |   | 
|---|---|
| Descripción del error | InvalidTemplate. Expresiones de lenguaje de plantilla no se puede tooprocess en entradas de acción 'Flat_File_Decoding' en línea '1' y '1902' de la columna: ' requiere la propiedad 'content' espera un valor pero se obtuvo null. Ruta de acceso ''.'. |
| Acción del usuario | Este error indica el mensaje de entrada de hello no contiene un cuerpo |
|   |   | 

## <a name="learn-more"></a>Más información
[Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md)
