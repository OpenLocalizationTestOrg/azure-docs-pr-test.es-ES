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
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="90377-103">Lista de errores y soluciones para Logic Apps B2B</span><span class="sxs-lookup"><span data-stu-id="90377-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="90377-104">Este artículo le ayuda a solucionar los errores que puedan ocurrir en escenarios de Logic Apps B2B y le sugiere las acciones adecuadas para corregirlos.</span><span class="sxs-lookup"><span data-stu-id="90377-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="90377-105">Resolución de contrato</span><span class="sxs-lookup"><span data-stu-id="90377-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="90377-106">*No agreement found (No se encontró ningún contrato)</span><span class="sxs-lookup"><span data-stu-id="90377-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="90377-107">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-107">Error description</span></span> | <span data-ttu-id="90377-108">No se encontró ningún contrato con parámetros de resolución de contrato</span><span class="sxs-lookup"><span data-stu-id="90377-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="90377-109">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-109">User action</span></span> | <span data-ttu-id="90377-110">acuerdo de Hello debe agregarse toohello cuenta de integración con las identidades de negocio acordada.</span><span class="sxs-lookup"><span data-stu-id="90377-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="90377-111">las identidades de negocio Hola deben coincidir con el Id. de mensaje de entrada de toohello</span><span class="sxs-lookup"><span data-stu-id="90377-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="90377-112">* No se encontró ningún contrato con las identidades</span><span class="sxs-lookup"><span data-stu-id="90377-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="90377-113">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-113">Error description</span></span> | <span data-ttu-id="90377-114">No se encontró ningún contrato con las identidades: 'AS2Identity'::'Partner1' y 'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="90377-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="90377-115">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-115">User action</span></span> | <span data-ttu-id="90377-116">AS2 no válido-desde o AS2-tooconfigured para el acuerdo.</span><span class="sxs-lookup"><span data-stu-id="90377-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="90377-117">Mensaje de AS2 correcto AS2-de o identificadores de toomatch AS2 AS2 tooheaders o acuerdo AS2 encabezados con configuraciones de contrato de mensaje</span><span class="sxs-lookup"><span data-stu-id="90377-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="90377-118">AS2</span><span class="sxs-lookup"><span data-stu-id="90377-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="90377-119">* Missing AS2 message headers (Faltan encabezados del mensaje AS2)</span><span class="sxs-lookup"><span data-stu-id="90377-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="90377-120">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-120">Error description</span></span>| <span data-ttu-id="90377-121">Encabezados AS2 no válidos.</span><span class="sxs-lookup"><span data-stu-id="90377-121">Invalid AS2 headers.</span></span> <span data-ttu-id="90377-122">Uno de los encabezados "AS2-To" o "AS2-From" está vacío</span><span class="sxs-lookup"><span data-stu-id="90377-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="90377-123">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-123">User action</span></span> | <span data-ttu-id="90377-124">Se recibió un mensaje AS2 que no contenía Hola AS2-de o AS2 tooor ambos encabezados.</span><span class="sxs-lookup"><span data-stu-id="90377-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="90377-125">Compruebe el mensaje AS2 AS2-de y tooheaders de AS2 y corríjalas en función de la configuración del acuerdo</span><span class="sxs-lookup"><span data-stu-id="90377-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="90377-126">* Missing AS2 message body and headers (Faltan el cuerpo y los encabezados del mensaje AS2)</span><span class="sxs-lookup"><span data-stu-id="90377-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="90377-127">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-127">Error description</span></span>| <span data-ttu-id="90377-128">contenido de la solicitud de Hello es nulo o está vacío</span><span class="sxs-lookup"><span data-stu-id="90377-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="90377-129">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-129">User action</span></span> | <span data-ttu-id="90377-130">Se recibió un mensaje AS2 que no contiene el cuerpo del mensaje Hola</span><span class="sxs-lookup"><span data-stu-id="90377-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="90377-131">* AS2 message decryption failure (Error de descifrado del mensaje AS2)</span><span class="sxs-lookup"><span data-stu-id="90377-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="90377-132">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-132">Error description</span></span> |  <span data-ttu-id="90377-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="90377-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="90377-134">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-134">User action</span></span> | <span data-ttu-id="90377-135">Agregar @base64ToBinary tooAS2Message antes de enviar toopartner</span><span class="sxs-lookup"><span data-stu-id="90377-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="90377-136">* MDN decryption failure﻿ (Error de descifrado de MDN)</span><span class="sxs-lookup"><span data-stu-id="90377-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="90377-137">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-137">Error description</span></span> |  <span data-ttu-id="90377-138">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="90377-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="90377-139">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-139">User action</span></span> | <span data-ttu-id="90377-140">Agregar @base64ToBinary tooMDN antes de enviar toopartner</span><span class="sxs-lookup"><span data-stu-id="90377-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="90377-141">* Missing signing certificate (Falta el certificado de firma)</span><span class="sxs-lookup"><span data-stu-id="90377-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="90377-142">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-142">Error description</span></span>| <span data-ttu-id="90377-143">Hello certificado de firma no se configuró para la entidad AS2.</span><span class="sxs-lookup"><span data-stu-id="90377-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="90377-144">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="90377-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="90377-145">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-145">User action</span></span> | <span data-ttu-id="90377-146">Configure el contrato AS2 con el certificado correcto para la firma</span><span class="sxs-lookup"><span data-stu-id="90377-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="90377-147">X12 y EDIFACT</span><span class="sxs-lookup"><span data-stu-id="90377-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="90377-148">* Espacio inicial o final detectado</span><span class="sxs-lookup"><span data-stu-id="90377-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="90377-149">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-149">Error description</span></span> | <span data-ttu-id="90377-150">Error al analizar.</span><span class="sxs-lookup"><span data-stu-id="90377-150">Error encountered during parsing.</span></span> <span data-ttu-id="90377-151">Hola conjunto de transacciones con Id. ' 123456 'contenido en el intercambio (sin grupo) con el identificador ' 987654', Id. de remitente 'Partner1', Id. de destinatario 'Asociado2' se está suspendiendo por los errores siguientes: A la izquierda finales separador que se encuentra</span><span class="sxs-lookup"><span data-stu-id="90377-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="90377-152">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-152">User action</span></span> | <span data-ttu-id="90377-153">Hola acuerdo configuración toobe configurado tooallow espacios iniciales y finales.</span><span class="sxs-lookup"><span data-stu-id="90377-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="90377-154">Editar acuerdo configuración tooallow espacios iniciales y finales</span><span class="sxs-lookup"><span data-stu-id="90377-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![permitir espacio](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="90377-156">* Comprobación de duplicados habilitó en el acuerdo de Hola</span><span class="sxs-lookup"><span data-stu-id="90377-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="90377-157">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-157">Error description</span></span> | <span data-ttu-id="90377-158">Número de control duplicado</span><span class="sxs-lookup"><span data-stu-id="90377-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="90377-159">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-159">User action</span></span> | <span data-ttu-id="90377-160">Este error indica que el mensaje Hola recibido tiene números de control duplicados.</span><span class="sxs-lookup"><span data-stu-id="90377-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="90377-161">Corrija el número de control de Hola y enviar mensajes de bienvenida</span><span class="sxs-lookup"><span data-stu-id="90377-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="90377-162">* Esquema que falta en el acuerdo de Hola</span><span class="sxs-lookup"><span data-stu-id="90377-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="90377-163">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-163">Error description</span></span> | <span data-ttu-id="90377-164">Error al analizar.</span><span class="sxs-lookup"><span data-stu-id="90377-164">Error encountered during parsing.</span></span> <span data-ttu-id="90377-165">conjunto de transacciones de Hello X12 con Id. '564220001' contenidos en el grupo funcional con Id. '56422', en el intercambio con Id. '000056422', Id. de remitente ' 12345678', Id. de destinatario ' 87654321' se está suspendiendo por los errores siguientes "mensaje de saludo tiene un ty de documento desconocido PE y no se resolvió tooany de esquemas existente Hola configurado en el acuerdo de hello "</span><span class="sxs-lookup"><span data-stu-id="90377-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="90377-166">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-166">User action</span></span> | <span data-ttu-id="90377-167">Configurar el esquema de configuración de un acuerdo Hola</span><span class="sxs-lookup"><span data-stu-id="90377-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="90377-168">* Esquema incorrecto en el acuerdo de Hola</span><span class="sxs-lookup"><span data-stu-id="90377-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="90377-169">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-169">Error description</span></span> | <span data-ttu-id="90377-170">mensaje de saludo tiene un tipo de documento desconocido y no resolvió tooany de esquemas existente Hola configurado en el acuerdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="90377-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="90377-171">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-171">User action</span></span> | <span data-ttu-id="90377-172">Configurar el esquema correcto en la configuración de acuerdo Hola</span><span class="sxs-lookup"><span data-stu-id="90377-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="90377-173">Archivo plano</span><span class="sxs-lookup"><span data-stu-id="90377-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="90377-174">* Input message with no body (Mensaje de entrada sin cuerpo)</span><span class="sxs-lookup"><span data-stu-id="90377-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="90377-175">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="90377-175">Error description</span></span> | <span data-ttu-id="90377-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="90377-176">InvalidTemplate.</span></span> <span data-ttu-id="90377-177">Expresiones de lenguaje de plantilla no se puede tooprocess en entradas de acción 'Flat_File_Decoding' en línea '1' y '1902' de la columna: ' requiere la propiedad 'content' espera un valor pero se obtuvo null.</span><span class="sxs-lookup"><span data-stu-id="90377-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="90377-178">Ruta de acceso ''.'.</span><span class="sxs-lookup"><span data-stu-id="90377-178">Path ''.'.</span></span> |
| <span data-ttu-id="90377-179">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="90377-179">User action</span></span> | <span data-ttu-id="90377-180">Este error indica el mensaje de entrada de hello no contiene un cuerpo</span><span class="sxs-lookup"><span data-stu-id="90377-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="90377-181">Más información</span><span class="sxs-lookup"><span data-stu-id="90377-181">Learn more</span></span>
[<span data-ttu-id="90377-182">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="90377-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
