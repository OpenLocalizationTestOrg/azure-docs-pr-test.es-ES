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
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="acb53-103">Lista de errores y soluciones para Logic Apps B2B</span><span class="sxs-lookup"><span data-stu-id="acb53-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="acb53-104">Este artículo le ayuda a solucionar los errores que puedan ocurrir en escenarios de Logic Apps B2B y le sugiere las acciones adecuadas para corregirlos.</span><span class="sxs-lookup"><span data-stu-id="acb53-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="acb53-105">Resolución de contrato</span><span class="sxs-lookup"><span data-stu-id="acb53-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="acb53-106">*No agreement found (No se encontró ningún contrato)</span><span class="sxs-lookup"><span data-stu-id="acb53-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="acb53-107">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-107">Error description</span></span> | <span data-ttu-id="acb53-108">No se encontró ningún contrato con parámetros de resolución de contrato</span><span class="sxs-lookup"><span data-stu-id="acb53-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="acb53-109">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-109">User action</span></span> | <span data-ttu-id="acb53-110">Se debe agregar el contrato a la cuenta de integración con identidades de negocio acordadas.</span><span class="sxs-lookup"><span data-stu-id="acb53-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="acb53-111">Las identidades de negocio deben coincidir con los identificadores de mensaje de entrada</span><span class="sxs-lookup"><span data-stu-id="acb53-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="acb53-112">* No se encontró ningún contrato con las identidades</span><span class="sxs-lookup"><span data-stu-id="acb53-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="acb53-113">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-113">Error description</span></span> | <span data-ttu-id="acb53-114">No se encontró ningún contrato con las identidades: 'AS2Identity'::'Partner1' y 'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="acb53-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="acb53-115">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-115">User action</span></span> | <span data-ttu-id="acb53-116">AS2-From o AS2-To configurados para el contrato no válidos.</span><span class="sxs-lookup"><span data-stu-id="acb53-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="acb53-117">Corrija los encabezados AS2-From o AS2-To del mensaje AS2 o el contrato para que coincidan con los identificadores AS2 en los encabezados del mensaje AS2 con configuraciones de contrato</span><span class="sxs-lookup"><span data-stu-id="acb53-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="acb53-118">AS2</span><span class="sxs-lookup"><span data-stu-id="acb53-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="acb53-119">* Missing AS2 message headers (Faltan encabezados del mensaje AS2)</span><span class="sxs-lookup"><span data-stu-id="acb53-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="acb53-120">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-120">Error description</span></span>| <span data-ttu-id="acb53-121">Encabezados AS2 no válidos.</span><span class="sxs-lookup"><span data-stu-id="acb53-121">Invalid AS2 headers.</span></span> <span data-ttu-id="acb53-122">Uno de los encabezados "AS2-To" o "AS2-From" está vacío</span><span class="sxs-lookup"><span data-stu-id="acb53-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="acb53-123">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-123">User action</span></span> | <span data-ttu-id="acb53-124">Se recibió un mensaje AS2 que no contenía el encabezado AS2-From, el AS2-To o ambos.</span><span class="sxs-lookup"><span data-stu-id="acb53-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="acb53-125">Compruebe los encabezados AS2-From y AS2-To del mensaje AS2 y corríjalos basándose en la configuración del contrato</span><span class="sxs-lookup"><span data-stu-id="acb53-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="acb53-126">* Missing AS2 message body and headers (Faltan el cuerpo y los encabezados del mensaje AS2)</span><span class="sxs-lookup"><span data-stu-id="acb53-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="acb53-127">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-127">Error description</span></span>| <span data-ttu-id="acb53-128">El contenido de la solicitud es nulo o está vacío</span><span class="sxs-lookup"><span data-stu-id="acb53-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="acb53-129">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-129">User action</span></span> | <span data-ttu-id="acb53-130">Se recibió un mensaje AS2 que no contenía el cuerpo del mensaje</span><span class="sxs-lookup"><span data-stu-id="acb53-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="acb53-131">* AS2 message decryption failure (Error de descifrado del mensaje AS2)</span><span class="sxs-lookup"><span data-stu-id="acb53-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="acb53-132">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-132">Error description</span></span> |  <span data-ttu-id="acb53-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="acb53-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="acb53-134">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-134">User action</span></span> | <span data-ttu-id="acb53-135">Agregue @base64ToBinary a AS2Message antes de enviarlo al asociado</span><span class="sxs-lookup"><span data-stu-id="acb53-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="acb53-136">* MDN decryption failure﻿ (Error de descifrado de MDN)</span><span class="sxs-lookup"><span data-stu-id="acb53-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="acb53-137">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-137">Error description</span></span> |  <span data-ttu-id="acb53-138">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="acb53-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="acb53-139">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-139">User action</span></span> | <span data-ttu-id="acb53-140">Agregue @base64ToBinary a la MDN antes de enviarlo al asociado</span><span class="sxs-lookup"><span data-stu-id="acb53-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="acb53-141">* Missing signing certificate (Falta el certificado de firma)</span><span class="sxs-lookup"><span data-stu-id="acb53-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="acb53-142">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-142">Error description</span></span>| <span data-ttu-id="acb53-143">El certificado de firma no se ha configurado para la entidad AS2.</span><span class="sxs-lookup"><span data-stu-id="acb53-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="acb53-144">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="acb53-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="acb53-145">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-145">User action</span></span> | <span data-ttu-id="acb53-146">Configure el contrato AS2 con el certificado correcto para la firma</span><span class="sxs-lookup"><span data-stu-id="acb53-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="acb53-147">X12 y EDIFACT</span><span class="sxs-lookup"><span data-stu-id="acb53-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="acb53-148">* Espacio inicial o final detectado</span><span class="sxs-lookup"><span data-stu-id="acb53-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="acb53-149">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-149">Error description</span></span> | <span data-ttu-id="acb53-150">Error al analizar.</span><span class="sxs-lookup"><span data-stu-id="acb53-150">Error encountered during parsing.</span></span> <span data-ttu-id="acb53-151">El conjunto de transacciones Edifact con Id. '123456' contenido en el intercambio (sin grupo) con Id. '987654', Id. de remitente 'Partner1' e Id. de destinatario 'Partner2' se está suspendiendo por los errores siguientes: Separador final encontrado</span><span class="sxs-lookup"><span data-stu-id="acb53-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="acb53-152">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-152">User action</span></span> | <span data-ttu-id="acb53-153">Se debe definir la configuración de contrato para que permita espacios iniciales y finales.</span><span class="sxs-lookup"><span data-stu-id="acb53-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="acb53-154">Edite la configuración de contrato para permitir un espacio inicial y final</span><span class="sxs-lookup"><span data-stu-id="acb53-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![permitir espacio](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="acb53-156">* Duplicate check has enabled in the agreement (Comprobación de duplicados habilitada en el contrato)</span><span class="sxs-lookup"><span data-stu-id="acb53-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="acb53-157">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-157">Error description</span></span> | <span data-ttu-id="acb53-158">Número de control duplicado</span><span class="sxs-lookup"><span data-stu-id="acb53-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="acb53-159">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-159">User action</span></span> | <span data-ttu-id="acb53-160">Este error indica que el mensaje recibido tiene números de control duplicados.</span><span class="sxs-lookup"><span data-stu-id="acb53-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="acb53-161">Corrija el número de control y vuelva a enviar el mensaje</span><span class="sxs-lookup"><span data-stu-id="acb53-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="acb53-162">* Missing schema in the agreement (Falta un esquema en el contrato)</span><span class="sxs-lookup"><span data-stu-id="acb53-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="acb53-163">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-163">Error description</span></span> | <span data-ttu-id="acb53-164">Error al analizar.</span><span class="sxs-lookup"><span data-stu-id="acb53-164">Error encountered during parsing.</span></span> <span data-ttu-id="acb53-165">El conjunto de transacciones X12 con Id. '564220001', contenido en el grupo funcional con Id. '56422', en el intercambio con Id. '000056422', con Id. de remitente '12345678' e Id. de destinatario '87654321' se suspende por los siguientes errores. "El mensaje tiene un tipo de documento desconocido y no se resolvió en ninguno de los esquemas existentes configurados en el contrato"</span><span class="sxs-lookup"><span data-stu-id="acb53-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="acb53-166">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-166">User action</span></span> | <span data-ttu-id="acb53-167">Configure el esquema en la configuración del contrato</span><span class="sxs-lookup"><span data-stu-id="acb53-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="acb53-168">* Incorrect schema in the agreement (Esquema incorrecto en el contrato)</span><span class="sxs-lookup"><span data-stu-id="acb53-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="acb53-169">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-169">Error description</span></span> | <span data-ttu-id="acb53-170">El mensaje tiene un tipo de documento desconocido y no se resolvió en ninguno de los esquemas existentes configurados en el contrato.</span><span class="sxs-lookup"><span data-stu-id="acb53-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="acb53-171">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-171">User action</span></span> | <span data-ttu-id="acb53-172">Configure el esquema correcto en la configuración del contrato</span><span class="sxs-lookup"><span data-stu-id="acb53-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="acb53-173">Archivo plano</span><span class="sxs-lookup"><span data-stu-id="acb53-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="acb53-174">* Input message with no body (Mensaje de entrada sin cuerpo)</span><span class="sxs-lookup"><span data-stu-id="acb53-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="acb53-175">Descripción del error</span><span class="sxs-lookup"><span data-stu-id="acb53-175">Error description</span></span> | <span data-ttu-id="acb53-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="acb53-176">InvalidTemplate.</span></span> <span data-ttu-id="acb53-177">No se pueden procesar las expresiones de lenguaje de plantilla en las entradas de la acción 'Flat_File_Decoding' en la línea '1' y la columna '1902': 'La propiedad obligatoria 'content' espera un valor pero obtuvo nulo.</span><span class="sxs-lookup"><span data-stu-id="acb53-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="acb53-178">Ruta de acceso ''.'.</span><span class="sxs-lookup"><span data-stu-id="acb53-178">Path ''.'.</span></span> |
| <span data-ttu-id="acb53-179">Acción del usuario</span><span class="sxs-lookup"><span data-stu-id="acb53-179">User action</span></span> | <span data-ttu-id="acb53-180">Este error indica que el mensaje de entrada no contiene un cuerpo</span><span class="sxs-lookup"><span data-stu-id="acb53-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="acb53-181">Más información</span><span class="sxs-lookup"><span data-stu-id="acb53-181">Learn more</span></span>
[<span data-ttu-id="acb53-182">Más información acerca de Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="acb53-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)