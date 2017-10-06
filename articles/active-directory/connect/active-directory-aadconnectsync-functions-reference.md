---
title: 'Azure AD Connect Sync: referencia de funciones | Microsoft Docs'
description: "Referencia de expresiones declarativas de aprovisionamiento en la sincronización de Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="8380a-103">Azure AD Connect Sync: referencia de funciones</span><span class="sxs-lookup"><span data-stu-id="8380a-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="8380a-104">En Azure AD Connect, las funciones son toomanipulate usa un valor de atributo durante la sincronización.</span><span class="sxs-lookup"><span data-stu-id="8380a-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="8380a-105">Sintaxis de las funciones de Hola Hola se expresa mediante Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="8380a-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="8380a-106">Si una función está sobrecargada y acepta varias sintaxis, se enumeran todas las sintaxis válidas.</span><span class="sxs-lookup"><span data-stu-id="8380a-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="8380a-107">Hola funciones están fuertemente tipadas y comprueban que coincide con el tipo de hello documentado pasado tipo hello.</span><span class="sxs-lookup"><span data-stu-id="8380a-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="8380a-108">Si no coincide con el tipo de hello, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="8380a-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="8380a-109">tipos de Hola se expresan con hello según la sintaxis:</span><span class="sxs-lookup"><span data-stu-id="8380a-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="8380a-110">**bin** : binario</span><span class="sxs-lookup"><span data-stu-id="8380a-110">**bin** – Binary</span></span>
* <span data-ttu-id="8380a-111">**bool** : booleano</span><span class="sxs-lookup"><span data-stu-id="8380a-111">**bool** – Boolean</span></span>
* <span data-ttu-id="8380a-112">**dt** : fecha y hora UTC</span><span class="sxs-lookup"><span data-stu-id="8380a-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="8380a-113">**enum** : enumeración de constantes conocidas</span><span class="sxs-lookup"><span data-stu-id="8380a-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="8380a-114">**EXP** : esperaba una expresión, que es tooevaluate tooa un valor booleano</span><span class="sxs-lookup"><span data-stu-id="8380a-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="8380a-115">**mvbin** : binario de varios valores</span><span class="sxs-lookup"><span data-stu-id="8380a-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="8380a-116">**mvstr** : cadena multivalor</span><span class="sxs-lookup"><span data-stu-id="8380a-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="8380a-117">**mvref** : referencia multivalor</span><span class="sxs-lookup"><span data-stu-id="8380a-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="8380a-118">**num** : numérico</span><span class="sxs-lookup"><span data-stu-id="8380a-118">**num** – Numeric</span></span>
* <span data-ttu-id="8380a-119">**ref** : referencia</span><span class="sxs-lookup"><span data-stu-id="8380a-119">**ref** – Reference</span></span>
* <span data-ttu-id="8380a-120">**str** : cadena</span><span class="sxs-lookup"><span data-stu-id="8380a-120">**str** – String</span></span>
* <span data-ttu-id="8380a-121">**var** : una variante de (casi) cualquier otro tipo</span><span class="sxs-lookup"><span data-stu-id="8380a-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="8380a-122">**void** : no devuelve un valor</span><span class="sxs-lookup"><span data-stu-id="8380a-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="8380a-123">Hola las funciones tienen tipos de hello **mvbin**, **mvstr**, y **mvref** sólo puede trabajar en atributos con varios valores.</span><span class="sxs-lookup"><span data-stu-id="8380a-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="8380a-124">Las funciones con **bin**, **str** y **ref** funcionan en atributos con un solo valor y con varios valores.</span><span class="sxs-lookup"><span data-stu-id="8380a-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="8380a-125">Referencia de funciones</span><span class="sxs-lookup"><span data-stu-id="8380a-125">Functions Reference</span></span>
| <span data-ttu-id="8380a-126">Lista de funciones</span><span class="sxs-lookup"><span data-stu-id="8380a-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8380a-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="8380a-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="8380a-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="8380a-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="8380a-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="8380a-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="8380a-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="8380a-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="8380a-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="8380a-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="8380a-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="8380a-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="8380a-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="8380a-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="8380a-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="8380a-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="8380a-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="8380a-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="8380a-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="8380a-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="8380a-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="8380a-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="8380a-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="8380a-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="8380a-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="8380a-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="8380a-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="8380a-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="8380a-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="8380a-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="8380a-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="8380a-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="8380a-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="8380a-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="8380a-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="8380a-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="8380a-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="8380a-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="8380a-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="8380a-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="8380a-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="8380a-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="8380a-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="8380a-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="8380a-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="8380a-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="8380a-150">**Conversión**</span><span class="sxs-lookup"><span data-stu-id="8380a-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="8380a-151">CBool</span><span class="sxs-lookup"><span data-stu-id="8380a-151">CBool</span></span>](#cbool) |[<span data-ttu-id="8380a-152">CDate</span><span class="sxs-lookup"><span data-stu-id="8380a-152">CDate</span></span>](#cdate) |[<span data-ttu-id="8380a-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="8380a-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="8380a-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="8380a-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="8380a-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="8380a-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="8380a-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="8380a-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="8380a-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="8380a-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="8380a-158">CNum</span><span class="sxs-lookup"><span data-stu-id="8380a-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="8380a-159">CRef</span><span class="sxs-lookup"><span data-stu-id="8380a-159">CRef</span></span>](#cref) |[<span data-ttu-id="8380a-160">CStr</span><span class="sxs-lookup"><span data-stu-id="8380a-160">CStr</span></span>](#cstr) |[<span data-ttu-id="8380a-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="8380a-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="8380a-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="8380a-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="8380a-163">**Fecha y hora**</span><span class="sxs-lookup"><span data-stu-id="8380a-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="8380a-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="8380a-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="8380a-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="8380a-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="8380a-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="8380a-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="8380a-167">Now</span><span class="sxs-lookup"><span data-stu-id="8380a-167">Now</span></span>](#now) | |
| [<span data-ttu-id="8380a-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="8380a-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="8380a-169">**Directorio**</span><span class="sxs-lookup"><span data-stu-id="8380a-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="8380a-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="8380a-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="8380a-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="8380a-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="8380a-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="8380a-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="8380a-173">**Evaluación**</span><span class="sxs-lookup"><span data-stu-id="8380a-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="8380a-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="8380a-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="8380a-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="8380a-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="8380a-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="8380a-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="8380a-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="8380a-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="8380a-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="8380a-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="8380a-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="8380a-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="8380a-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="8380a-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="8380a-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="8380a-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="8380a-182">IsString</span><span class="sxs-lookup"><span data-stu-id="8380a-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="8380a-183">**Matemáticas**</span><span class="sxs-lookup"><span data-stu-id="8380a-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="8380a-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="8380a-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="8380a-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="8380a-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="8380a-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="8380a-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="8380a-187">**Con varios valores**</span><span class="sxs-lookup"><span data-stu-id="8380a-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="8380a-188">Contains</span><span class="sxs-lookup"><span data-stu-id="8380a-188">Contains</span></span>](#contains) |[<span data-ttu-id="8380a-189">Recuento</span><span class="sxs-lookup"><span data-stu-id="8380a-189">Count</span></span>](#count) |[<span data-ttu-id="8380a-190">Elemento</span><span class="sxs-lookup"><span data-stu-id="8380a-190">Item</span></span>](#item) |[<span data-ttu-id="8380a-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="8380a-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="8380a-192">Join</span><span class="sxs-lookup"><span data-stu-id="8380a-192">Join</span></span>](#join) |[<span data-ttu-id="8380a-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="8380a-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="8380a-194">Dividir</span><span class="sxs-lookup"><span data-stu-id="8380a-194">Split</span></span>](#split) | | |
| <span data-ttu-id="8380a-195">**Flujo de programa**</span><span class="sxs-lookup"><span data-stu-id="8380a-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="8380a-196">Error</span><span class="sxs-lookup"><span data-stu-id="8380a-196">Error</span></span>](#error) |[<span data-ttu-id="8380a-197">IIF</span><span class="sxs-lookup"><span data-stu-id="8380a-197">IIF</span></span>](#iif) |[<span data-ttu-id="8380a-198">Select</span><span class="sxs-lookup"><span data-stu-id="8380a-198">Select</span></span>](#select) |[<span data-ttu-id="8380a-199">Switch</span><span class="sxs-lookup"><span data-stu-id="8380a-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="8380a-200">Where</span><span class="sxs-lookup"><span data-stu-id="8380a-200">Where</span></span>](#where) |[<span data-ttu-id="8380a-201">With</span><span class="sxs-lookup"><span data-stu-id="8380a-201">With</span></span>](#with) | | | |
| <span data-ttu-id="8380a-202">**Texto**</span><span class="sxs-lookup"><span data-stu-id="8380a-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="8380a-203">GUID</span><span class="sxs-lookup"><span data-stu-id="8380a-203">GUID</span></span>](#guid) |[<span data-ttu-id="8380a-204">InStr</span><span class="sxs-lookup"><span data-stu-id="8380a-204">InStr</span></span>](#instr) |[<span data-ttu-id="8380a-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="8380a-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="8380a-206">LCase</span><span class="sxs-lookup"><span data-stu-id="8380a-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="8380a-207">Left</span><span class="sxs-lookup"><span data-stu-id="8380a-207">Left</span></span>](#left) |[<span data-ttu-id="8380a-208">Len</span><span class="sxs-lookup"><span data-stu-id="8380a-208">Len</span></span>](#len) |[<span data-ttu-id="8380a-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="8380a-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="8380a-210">Mid</span><span class="sxs-lookup"><span data-stu-id="8380a-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="8380a-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="8380a-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="8380a-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="8380a-212">PadRight</span></span>](#padright) |[<span data-ttu-id="8380a-213">PCase</span><span class="sxs-lookup"><span data-stu-id="8380a-213">PCase</span></span>](#pcase) |[<span data-ttu-id="8380a-214">Sustituya</span><span class="sxs-lookup"><span data-stu-id="8380a-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="8380a-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="8380a-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="8380a-216">Right</span><span class="sxs-lookup"><span data-stu-id="8380a-216">Right</span></span>](#right) |[<span data-ttu-id="8380a-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="8380a-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="8380a-218">Trim</span><span class="sxs-lookup"><span data-stu-id="8380a-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="8380a-219">UCase</span><span class="sxs-lookup"><span data-stu-id="8380a-219">UCase</span></span>](#ucase) |[<span data-ttu-id="8380a-220">Word</span><span class="sxs-lookup"><span data-stu-id="8380a-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="8380a-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="8380a-221">BitAnd</span></span>
<span data-ttu-id="8380a-222">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-222">**Description:**</span></span>  
<span data-ttu-id="8380a-223">Hola función BitAnd establece los bits especificados en un valor.</span><span class="sxs-lookup"><span data-stu-id="8380a-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="8380a-224">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="8380a-225">value1, value2: valores numéricos que deberían estar unidos por el operador AND</span><span class="sxs-lookup"><span data-stu-id="8380a-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="8380a-226">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-226">**Remarks:**</span></span>  
<span data-ttu-id="8380a-227">Esta función convierte ambos representación binaria de parámetros toohello y establece un bit:</span><span class="sxs-lookup"><span data-stu-id="8380a-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="8380a-228">0 - si uno o ambos bits correspondientes de Hola *máscara* y *marca* son 0</span><span class="sxs-lookup"><span data-stu-id="8380a-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="8380a-229">1 - si ambos bits correspondientes de hello son 1.</span><span class="sxs-lookup"><span data-stu-id="8380a-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="8380a-230">En otras palabras, devuelve 0 en todos los casos excepto cuando los bits correspondientes de Hola de ambos parámetros son 1.</span><span class="sxs-lookup"><span data-stu-id="8380a-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="8380a-231">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="8380a-232">Devuelve 7 porque hexadecimal "F" y "F7" evaluación el valor de toothis.</span><span class="sxs-lookup"><span data-stu-id="8380a-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="8380a-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="8380a-233">BitOr</span></span>
<span data-ttu-id="8380a-234">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-234">**Description:**</span></span>  
<span data-ttu-id="8380a-235">Hola función BitOr establece los bits especificados en un valor.</span><span class="sxs-lookup"><span data-stu-id="8380a-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="8380a-236">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="8380a-237">value1, value2: valores numéricos que deberían estar unidos por el operador OR</span><span class="sxs-lookup"><span data-stu-id="8380a-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="8380a-238">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-238">**Remarks:**</span></span>  
<span data-ttu-id="8380a-239">Esta función convierte ambos representación binaria de parámetros toohello y establece un bit too1 si uno o ambos bits correspondientes de Hola de máscara y marca son 1 y too0 si ambos bits correspondientes de hello son 0.</span><span class="sxs-lookup"><span data-stu-id="8380a-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="8380a-240">En otras palabras, devuelve 1 en todos los casos excepto cuando los bits correspondientes de Hola de ambos parámetros son 0.</span><span class="sxs-lookup"><span data-stu-id="8380a-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="8380a-241">CBool</span><span class="sxs-lookup"><span data-stu-id="8380a-241">CBool</span></span>
<span data-ttu-id="8380a-242">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-242">**Description:**</span></span>  
<span data-ttu-id="8380a-243">Hola función CBool devuelve que un valor booleano en función de hello evaluar expresión</span><span class="sxs-lookup"><span data-stu-id="8380a-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="8380a-244">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="8380a-245">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-245">**Remarks:**</span></span>  
<span data-ttu-id="8380a-246">Si Hola se evalúa como tooa valor distinto de cero, CBool devuelve True, en caso contrario devuelve False.</span><span class="sxs-lookup"><span data-stu-id="8380a-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="8380a-247">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="8380a-248">Devuelve True si ambos atributos tienen Hola el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="8380a-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="8380a-249">CDate</span><span class="sxs-lookup"><span data-stu-id="8380a-249">CDate</span></span>
<span data-ttu-id="8380a-250">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-250">**Description:**</span></span>  
<span data-ttu-id="8380a-251">Hola función CDate devuelve una fecha y hora UTC de una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="8380a-252">DateTime no es un tipo de atributo nativo en Sincronización pero lo usan algunas funciones.</span><span class="sxs-lookup"><span data-stu-id="8380a-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="8380a-253">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="8380a-254">Valor: una cadena con una fecha, hora y opcionalmente, una zona horaria</span><span class="sxs-lookup"><span data-stu-id="8380a-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="8380a-255">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-255">**Remarks:**</span></span>  
<span data-ttu-id="8380a-256">Hola devolvió una cadena siempre es en UTC.</span><span class="sxs-lookup"><span data-stu-id="8380a-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="8380a-257">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="8380a-258">Devuelve una fecha y hora según el tiempo de inicio del empleado de Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="8380a-259">Devuelve un valor DateTime que representa "2013-01-11 12:00 AM".</span><span class="sxs-lookup"><span data-stu-id="8380a-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="8380a-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="8380a-260">CertExtensionOids</span></span>
<span data-ttu-id="8380a-261">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-261">**Description:**</span></span>  
<span data-ttu-id="8380a-262">Devuelve Hola valores de Oid de todas las extensiones críticas Hola de un objeto de certificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="8380a-263">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="8380a-264">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-265">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="8380a-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="8380a-266">CertFormat</span></span>
<span data-ttu-id="8380a-267">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-267">**Description:**</span></span>  
<span data-ttu-id="8380a-268">Devuelve Hola nombre del formato de Hola de este certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="8380a-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="8380a-269">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="8380a-270">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-271">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="8380a-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="8380a-272">CertFriendlyName</span></span>
<span data-ttu-id="8380a-273">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-273">**Description:**</span></span>  
<span data-ttu-id="8380a-274">Devuelve Hola alias asociado para un certificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="8380a-275">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="8380a-276">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-277">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="8380a-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="8380a-278">CertHashString</span></span>
<span data-ttu-id="8380a-279">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-279">**Description:**</span></span>  
<span data-ttu-id="8380a-280">Devuelve Hola valor hash SHA1 de certificados X.509v3 hello como una cadena hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="8380a-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="8380a-281">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="8380a-282">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-283">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="8380a-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="8380a-284">CertIssuer</span></span>
<span data-ttu-id="8380a-285">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-285">**Description:**</span></span>  
<span data-ttu-id="8380a-286">Devuelve Hola nombre de entidad emisora de certificados de Hola que emitió el certificado X.509v3 de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="8380a-287">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="8380a-288">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-289">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="8380a-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="8380a-290">CertIssuerDN</span></span>
<span data-ttu-id="8380a-291">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-291">**Description:**</span></span>  
<span data-ttu-id="8380a-292">Devuelve Hola nombre distintivo del emisor de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="8380a-293">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="8380a-294">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-295">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="8380a-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="8380a-296">CertIssuerOid</span></span>
<span data-ttu-id="8380a-297">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-297">**Description:**</span></span>  
<span data-ttu-id="8380a-298">Devuelve Hola Oid del emisor de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="8380a-299">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="8380a-300">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-301">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="8380a-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="8380a-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="8380a-303">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-303">**Description:**</span></span>  
<span data-ttu-id="8380a-304">Devuelve información de algoritmo de clave de Hola de este certificado X.509v3 como una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="8380a-305">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="8380a-306">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-307">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="8380a-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="8380a-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="8380a-309">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-309">**Description:**</span></span>  
<span data-ttu-id="8380a-310">Devuelve los parámetros de algoritmo de clave de hello certificado X.509v3 de hello como una cadena hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="8380a-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="8380a-311">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="8380a-312">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-313">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="8380a-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="8380a-314">CertNameInfo</span></span>
<span data-ttu-id="8380a-315">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-315">**Description:**</span></span>  
<span data-ttu-id="8380a-316">Devuelve emisor y el asunto de hello nombres de un certificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="8380a-317">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="8380a-318">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-319">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="8380a-320">X509NameType: Hola valor X509NameType asunto Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="8380a-321">includesIssuerName: nombre de emisor de hello tooinclude true; en caso contrario, false.</span><span class="sxs-lookup"><span data-stu-id="8380a-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="8380a-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="8380a-322">CertNotAfter</span></span>
<span data-ttu-id="8380a-323">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-323">**Description:**</span></span>  
<span data-ttu-id="8380a-324">Devuelve la fecha de hello en hora local después del cual un certificado ya no es válido.</span><span class="sxs-lookup"><span data-stu-id="8380a-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="8380a-325">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="8380a-326">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-327">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="8380a-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="8380a-328">CertNotBefore</span></span>
<span data-ttu-id="8380a-329">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-329">**Description:**</span></span>  
<span data-ttu-id="8380a-330">Devuelve la fecha de hello en hora local en el que un certificado es válido.</span><span class="sxs-lookup"><span data-stu-id="8380a-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="8380a-331">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="8380a-332">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-333">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="8380a-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="8380a-334">CertPublicKeyOid</span></span>
<span data-ttu-id="8380a-335">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-335">**Description:**</span></span>  
<span data-ttu-id="8380a-336">Devuelve Hola Oid de clave pública de hello certificado X.509v3 de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="8380a-337">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="8380a-338">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-339">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="8380a-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="8380a-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="8380a-341">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-341">**Description:**</span></span>  
<span data-ttu-id="8380a-342">Devuelve Hola Oid de parámetros de clave pública de hello certificado X.509v3 de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="8380a-343">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="8380a-344">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-345">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="8380a-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="8380a-346">CertSerialNumber</span></span>
<span data-ttu-id="8380a-347">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-347">**Description:**</span></span>  
<span data-ttu-id="8380a-348">Devuelve el número de serie de Hola de certificado X.509v3 de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="8380a-349">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="8380a-350">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-351">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="8380a-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="8380a-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="8380a-353">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-353">**Description:**</span></span>  
<span data-ttu-id="8380a-354">Hola devuelve Oid del algoritmo de hello utiliza firma de hello toocreate de un certificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="8380a-355">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="8380a-356">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-357">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="8380a-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="8380a-358">CertSubject</span></span>
<span data-ttu-id="8380a-359">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-359">**Description:**</span></span>  
<span data-ttu-id="8380a-360">Obtiene Hola nombre distintivo del sujeto de un certificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="8380a-361">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="8380a-362">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-363">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="8380a-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="8380a-364">CertSubjectNameDN</span></span>
<span data-ttu-id="8380a-365">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-365">**Description:**</span></span>  
<span data-ttu-id="8380a-366">Devuelve Hola nombre distintivo del sujeto de un certificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="8380a-367">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="8380a-368">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-369">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="8380a-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="8380a-370">CertSubjectNameOid</span></span>
<span data-ttu-id="8380a-371">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-371">**Description:**</span></span>  
<span data-ttu-id="8380a-372">Devuelve Hola Oid del nombre de sujeto de Hola de un certificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="8380a-373">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="8380a-374">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-375">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="8380a-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="8380a-376">CertThumbprint</span></span>
<span data-ttu-id="8380a-377">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-377">**Description:**</span></span>  
<span data-ttu-id="8380a-378">Devuelve Hola huella digital de un certificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="8380a-379">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="8380a-380">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-381">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="8380a-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="8380a-382">CertVersion</span></span>
<span data-ttu-id="8380a-383">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-383">**Description:**</span></span>  
<span data-ttu-id="8380a-384">Devuelve Hola versión en formato de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="8380a-385">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="8380a-386">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-387">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="8380a-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="8380a-388">CGuid</span></span>
<span data-ttu-id="8380a-389">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-389">**Description:**</span></span>  
<span data-ttu-id="8380a-390">Hola función CGuid convierte la representación de cadena de Hola de una representación binaria de tooits GUID.</span><span class="sxs-lookup"><span data-stu-id="8380a-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="8380a-391">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="8380a-392">Una cadena con un formato que sigue este patrón: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="8380a-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="8380a-393">Contains</span><span class="sxs-lookup"><span data-stu-id="8380a-393">Contains</span></span>
<span data-ttu-id="8380a-394">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-394">**Description:**</span></span>  
<span data-ttu-id="8380a-395">función de Hello Contains busca una cadena dentro de un atributo multivalor</span><span class="sxs-lookup"><span data-stu-id="8380a-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="8380a-396">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-396">**Syntax:**</span></span>  
<span data-ttu-id="8380a-397">`num Contains (mvstring attribute, str search)` - distingue mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="8380a-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="8380a-398">`num Contains (mvref attribute, str search)` - distingue mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="8380a-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="8380a-399">atributo: Hola atributo multivalor toosearch.</span><span class="sxs-lookup"><span data-stu-id="8380a-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="8380a-400">búsqueda: cadena toofind en atributo Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="8380a-401">Casetype: CaseInsensitive o CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="8380a-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="8380a-402">Devuelve el índice de atributo multivalor Hola donde se encontró la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="8380a-403">se devuelve 0 si no se encuentra la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="8380a-404">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-404">**Remarks:**</span></span>  
<span data-ttu-id="8380a-405">Para los atributos de cadena multivalor, Hola encontrar subcadenas en valores de hello.</span><span class="sxs-lookup"><span data-stu-id="8380a-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="8380a-406">Para los atributos de referencia, hello cadena buscada debe coincidir exactamente con hello valor toobe considera a una coincidencia.</span><span class="sxs-lookup"><span data-stu-id="8380a-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="8380a-407">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="8380a-408">Si el atributo proxyAddresses de hello tiene una dirección de correo electrónico principal (indicada por las mayúsculas "SMTP:"), a continuación, devolver el atributo proxyAddress de hello, devolver un error en caso contrario.</span><span class="sxs-lookup"><span data-stu-id="8380a-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="8380a-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="8380a-409">ConvertFromBase64</span></span>
<span data-ttu-id="8380a-410">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-410">**Description:**</span></span>  
<span data-ttu-id="8380a-411">Hola ConvertFromBase64 función convierte Hola especifica cadena base64 del valor tooa regular.</span><span class="sxs-lookup"><span data-stu-id="8380a-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="8380a-412">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-412">**Syntax:**</span></span>  
<span data-ttu-id="8380a-413">`str ConvertFromBase64(str source)` da por hecho que se usará Unicode para la codificación.</span><span class="sxs-lookup"><span data-stu-id="8380a-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="8380a-414">source: cadena codificada en Base64</span><span class="sxs-lookup"><span data-stu-id="8380a-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="8380a-415">Codificación: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="8380a-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="8380a-416">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="8380a-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="8380a-417">Ambos ejemplos devuelven "*Hola a todos*"</span><span class="sxs-lookup"><span data-stu-id="8380a-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="8380a-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="8380a-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="8380a-419">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-419">**Description:**</span></span>  
<span data-ttu-id="8380a-420">Hola ConvertFromUTF8Hex función convierte Hola especifica la cadena de tooa valor codificado en hexadecimal UTF8.</span><span class="sxs-lookup"><span data-stu-id="8380a-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="8380a-421">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="8380a-422">origen: cadena codificada de 2 bytes UTF8</span><span class="sxs-lookup"><span data-stu-id="8380a-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="8380a-423">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-423">**Remarks:**</span></span>  
<span data-ttu-id="8380a-424">Hola diferencia entre esta función y ConvertFromBase64([],UTF8) que dan lugar a hello es descriptivo para el atributo DN de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="8380a-425">Azure Active Directory utiliza este formato como DN.</span><span class="sxs-lookup"><span data-stu-id="8380a-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="8380a-426">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="8380a-427">devuelve "*Hello world!*".</span><span class="sxs-lookup"><span data-stu-id="8380a-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="8380a-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="8380a-428">ConvertToBase64</span></span>
<span data-ttu-id="8380a-429">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-429">**Description:**</span></span>  
<span data-ttu-id="8380a-430">Hola función ConvertToBase64 convierte una cadena base64 de Unicode tooa de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="8380a-431">Convierte el valor de Hola de una matriz de representación de cadena equivalente de tooits de enteros que se codifica con dígitos de base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="8380a-432">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="8380a-433">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="8380a-434">devuelve "SABlAGwAbABvACAAdwBvAHIAbABkACEA".</span><span class="sxs-lookup"><span data-stu-id="8380a-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="8380a-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="8380a-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="8380a-436">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-436">**Description:**</span></span>  
<span data-ttu-id="8380a-437">Hola función ConvertToUTF8Hex convierte un valor codificado en hexadecimal UTF8 tooa de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="8380a-438">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="8380a-439">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-439">**Remarks:**</span></span>  
<span data-ttu-id="8380a-440">formato de salida de Hello de esta función se utiliza por Azure Active Directory como formato del atributo DN.</span><span class="sxs-lookup"><span data-stu-id="8380a-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="8380a-441">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="8380a-442">devuelve 48656C6C6F20776F726C6421.</span><span class="sxs-lookup"><span data-stu-id="8380a-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="8380a-443">Recuento</span><span class="sxs-lookup"><span data-stu-id="8380a-443">Count</span></span>
<span data-ttu-id="8380a-444">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-444">**Description:**</span></span>  
<span data-ttu-id="8380a-445">Hola función Count devuelve el número de Hola de elementos de un atributo multivalor</span><span class="sxs-lookup"><span data-stu-id="8380a-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="8380a-446">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="8380a-447">CNum</span><span class="sxs-lookup"><span data-stu-id="8380a-447">CNum</span></span>
<span data-ttu-id="8380a-448">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-448">**Description:**</span></span>  
<span data-ttu-id="8380a-449">Hola función CNum toma una cadena y devuelve un tipo de datos numéricos.</span><span class="sxs-lookup"><span data-stu-id="8380a-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="8380a-450">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="8380a-451">CRef</span><span class="sxs-lookup"><span data-stu-id="8380a-451">CRef</span></span>
<span data-ttu-id="8380a-452">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-452">**Description:**</span></span>  
<span data-ttu-id="8380a-453">Convierte un atributo de referencia de cadena tooa</span><span class="sxs-lookup"><span data-stu-id="8380a-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="8380a-454">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="8380a-455">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="8380a-456">CStr</span><span class="sxs-lookup"><span data-stu-id="8380a-456">CStr</span></span>
<span data-ttu-id="8380a-457">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-457">**Description:**</span></span>  
<span data-ttu-id="8380a-458">Hello para la función CStr Convierte el tipo de datos de cadena de tooa.</span><span class="sxs-lookup"><span data-stu-id="8380a-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="8380a-459">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="8380a-460">value: puede ser un valor numérico, un atributo de referencia o un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="8380a-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="8380a-461">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="8380a-462">podría devolver "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="8380a-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="8380a-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="8380a-463">DateAdd</span></span>
<span data-ttu-id="8380a-464">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-464">**Description:**</span></span>  
<span data-ttu-id="8380a-465">Devuelve una fecha que contiene un toowhich de fecha que se ha agregado un intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="8380a-466">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="8380a-467">intervalo: expresión de cadena que es el intervalo de saludo de tiempo que desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="8380a-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="8380a-468">cadena de Hello debe tener uno de hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="8380a-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="8380a-469">yyyy Año</span><span class="sxs-lookup"><span data-stu-id="8380a-469">yyyy Year</span></span>
  * <span data-ttu-id="8380a-470">q Trimestre</span><span class="sxs-lookup"><span data-stu-id="8380a-470">q Quarter</span></span>
  * <span data-ttu-id="8380a-471">m Mes</span><span class="sxs-lookup"><span data-stu-id="8380a-471">m Month</span></span>
  * <span data-ttu-id="8380a-472">y Día del año</span><span class="sxs-lookup"><span data-stu-id="8380a-472">y Day of year</span></span>
  * <span data-ttu-id="8380a-473">d Día</span><span class="sxs-lookup"><span data-stu-id="8380a-473">d Day</span></span>
  * <span data-ttu-id="8380a-474">w Día de la semana</span><span class="sxs-lookup"><span data-stu-id="8380a-474">w Weekday</span></span>
  * <span data-ttu-id="8380a-475">ww Semana</span><span class="sxs-lookup"><span data-stu-id="8380a-475">ww Week</span></span>
  * <span data-ttu-id="8380a-476">h Hora</span><span class="sxs-lookup"><span data-stu-id="8380a-476">h Hour</span></span>
  * <span data-ttu-id="8380a-477">n Minuto</span><span class="sxs-lookup"><span data-stu-id="8380a-477">n Minute</span></span>
  * <span data-ttu-id="8380a-478">s Segundo</span><span class="sxs-lookup"><span data-stu-id="8380a-478">s Second</span></span>
* <span data-ttu-id="8380a-479">valor: Hola número de unidades que desea tooadd.</span><span class="sxs-lookup"><span data-stu-id="8380a-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="8380a-480">Puede ser positivo (tooget fechas en hello futuras) o negativo (tooget fechas en hello anterior).</span><span class="sxs-lookup"><span data-stu-id="8380a-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="8380a-481">fecha: fecha y hora se agrega el intervalo de saludo de toowhich de fecha que representa.</span><span class="sxs-lookup"><span data-stu-id="8380a-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="8380a-482">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="8380a-483">agrega 3 meses y devuelve un valor DateTime que representa "2001-04-01".</span><span class="sxs-lookup"><span data-stu-id="8380a-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="8380a-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="8380a-484">DateFromNum</span></span>
<span data-ttu-id="8380a-485">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-485">**Description:**</span></span>  
<span data-ttu-id="8380a-486">Hola función DateFromNum convierte el valor de tooa de formato de fecha de AD tipo DateTime.</span><span class="sxs-lookup"><span data-stu-id="8380a-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="8380a-487">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="8380a-488">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="8380a-489">devuelve un valor DateTime que representa 2012-01-01 23:00:00.</span><span class="sxs-lookup"><span data-stu-id="8380a-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="8380a-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="8380a-490">DNComponent</span></span>
<span data-ttu-id="8380a-491">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-491">**Description:**</span></span>  
<span data-ttu-id="8380a-492">Hola función DNComponent devuelve el valor Hola de un componente DN especificado desde la izquierda.</span><span class="sxs-lookup"><span data-stu-id="8380a-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="8380a-493">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="8380a-494">DN: Hola referencia atributo toointerpret</span><span class="sxs-lookup"><span data-stu-id="8380a-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="8380a-495">ComponentNumber: componente hello en hello DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="8380a-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="8380a-496">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="8380a-497">si dn es "cn=Joe,ou=…", devuelve Joe.</span><span class="sxs-lookup"><span data-stu-id="8380a-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="8380a-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="8380a-498">DNComponentRev</span></span>
<span data-ttu-id="8380a-499">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-499">**Description:**</span></span>  
<span data-ttu-id="8380a-500">Hola función DNComponentRev devuelve valor Hola de un componente DN especificado desde la derecha (Hola final).</span><span class="sxs-lookup"><span data-stu-id="8380a-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="8380a-501">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="8380a-502">DN: Hola referencia atributo toointerpret</span><span class="sxs-lookup"><span data-stu-id="8380a-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="8380a-503">ComponentNumber - componente hello en hello DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="8380a-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="8380a-504">Opciones: DC, ignora todos los componentes con “dc=”</span><span class="sxs-lookup"><span data-stu-id="8380a-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="8380a-505">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-505">**Example:**</span></span>  
<span data-ttu-id="8380a-506">Si dn es "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="8380a-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="8380a-507">Ambos devuelven US.</span><span class="sxs-lookup"><span data-stu-id="8380a-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="8380a-508">Error</span><span class="sxs-lookup"><span data-stu-id="8380a-508">Error</span></span>
<span data-ttu-id="8380a-509">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-509">**Description:**</span></span>  
<span data-ttu-id="8380a-510">Hola función de Error es tooreturn usado un error personalizado.</span><span class="sxs-lookup"><span data-stu-id="8380a-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="8380a-511">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="8380a-512">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="8380a-513">Si Hola atributo accountName no está presente, produce un error en el objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="8380a-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="8380a-514">EscapeDNComponent</span></span>
<span data-ttu-id="8380a-515">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-515">**Description:**</span></span>  
<span data-ttu-id="8380a-516">Hola función EscapeDNComponent toma un componente de un DN y secuencias de escape, por lo que puede representarse en LDAP.</span><span class="sxs-lookup"><span data-stu-id="8380a-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="8380a-517">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="8380a-518">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="8380a-519">Se asegura de objeto Hola puede crearse en un directorio LDAP, incluso si el atributo de hello displayName tiene caracteres que deben tener escape en LDAP.</span><span class="sxs-lookup"><span data-stu-id="8380a-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="8380a-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="8380a-520">FormatDateTime</span></span>
<span data-ttu-id="8380a-521">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-521">**Description:**</span></span>  
<span data-ttu-id="8380a-522">función FormatDateTime de Hello es tooformat usa una cadena de fecha y hora tooa con un formato especificado</span><span class="sxs-lookup"><span data-stu-id="8380a-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="8380a-523">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="8380a-524">valor: un valor en formato de fecha y hora de Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="8380a-525">formato: una cadena que representa Hola formato tooconvert a.</span><span class="sxs-lookup"><span data-stu-id="8380a-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="8380a-526">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-526">**Remarks:**</span></span>  
<span data-ttu-id="8380a-527">Hola valores posibles para el formato de hello puede encontrarse aquí: [formatos de fecha y hora definidos por el usuario (función Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="8380a-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="8380a-528">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="8380a-529">Genera "2007-12-25".</span><span class="sxs-lookup"><span data-stu-id="8380a-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="8380a-530">Puede generar "20140905081453.0Z".</span><span class="sxs-lookup"><span data-stu-id="8380a-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="8380a-531">GUID</span><span class="sxs-lookup"><span data-stu-id="8380a-531">GUID</span></span>
<span data-ttu-id="8380a-532">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-532">**Description:**</span></span>  
<span data-ttu-id="8380a-533">Hola función GUID genera un nuevo GUID aleatorio</span><span class="sxs-lookup"><span data-stu-id="8380a-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="8380a-534">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="8380a-535">IIF</span><span class="sxs-lookup"><span data-stu-id="8380a-535">IIF</span></span>
<span data-ttu-id="8380a-536">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-536">**Description:**</span></span>  
<span data-ttu-id="8380a-537">Hola función IIF devuelve uno de un conjunto de valores posibles basado en una condición especificada.</span><span class="sxs-lookup"><span data-stu-id="8380a-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="8380a-538">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="8380a-539">condición: cualquier valor o expresión que se puede evaluar tootrue o false.</span><span class="sxs-lookup"><span data-stu-id="8380a-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="8380a-540">ValorSiVerdadero: si la condición de Hola se evalúa como tootrue, Hola devolvió el valor.</span><span class="sxs-lookup"><span data-stu-id="8380a-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="8380a-541">valorSiFalse: si la condición de Hola se evalúa como toofalse, Hola devolvió el valor.</span><span class="sxs-lookup"><span data-stu-id="8380a-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="8380a-542">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="8380a-543">Si el usuario de hello es una persona en prácticas, devuelve Hola alias de un usuario con "t-" agregados toohello a partir de ella, else devuelve los alias del usuario de hello tal cual.</span><span class="sxs-lookup"><span data-stu-id="8380a-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="8380a-544">InStr</span><span class="sxs-lookup"><span data-stu-id="8380a-544">InStr</span></span>
<span data-ttu-id="8380a-545">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-545">**Description:**</span></span>  
<span data-ttu-id="8380a-546">Hola función InStr busca Hola primera aparición de una subcadena en una cadena</span><span class="sxs-lookup"><span data-stu-id="8380a-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="8380a-547">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="8380a-548">comprobarcadena: cadena toobe buscada</span><span class="sxs-lookup"><span data-stu-id="8380a-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="8380a-549">coincidircadena: cadena toobe encuentra</span><span class="sxs-lookup"><span data-stu-id="8380a-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="8380a-550">inicio: iniciar posición toofind Hola subcadena</span><span class="sxs-lookup"><span data-stu-id="8380a-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="8380a-551">compare: vbTextCompare o vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="8380a-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="8380a-552">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-552">**Remarks:**</span></span>  
<span data-ttu-id="8380a-553">Posición de hello devuelve donde se encontró la subcadena de Hola o 0 si no encuentra.</span><span class="sxs-lookup"><span data-stu-id="8380a-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="8380a-554">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="8380a-555">Evalues too5</span><span class="sxs-lookup"><span data-stu-id="8380a-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="8380a-556">Se evalúa como too7</span><span class="sxs-lookup"><span data-stu-id="8380a-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="8380a-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="8380a-557">InStrRev</span></span>
<span data-ttu-id="8380a-558">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-558">**Description:**</span></span>  
<span data-ttu-id="8380a-559">Hola función InStrRev busca la última aparición de una subcadena de hello en una cadena</span><span class="sxs-lookup"><span data-stu-id="8380a-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="8380a-560">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="8380a-561">comprobarcadena: cadena toobe buscada</span><span class="sxs-lookup"><span data-stu-id="8380a-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="8380a-562">coincidircadena: cadena toobe encuentra</span><span class="sxs-lookup"><span data-stu-id="8380a-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="8380a-563">inicio: iniciar posición toofind Hola subcadena</span><span class="sxs-lookup"><span data-stu-id="8380a-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="8380a-564">compare: vbTextCompare o vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="8380a-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="8380a-565">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-565">**Remarks:**</span></span>  
<span data-ttu-id="8380a-566">Posición de hello devuelve donde se encontró la subcadena de Hola o 0 si no encuentra.</span><span class="sxs-lookup"><span data-stu-id="8380a-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="8380a-567">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="8380a-568">devuelve 7.</span><span class="sxs-lookup"><span data-stu-id="8380a-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="8380a-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="8380a-569">IsBitSet</span></span>
<span data-ttu-id="8380a-570">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-570">**Description:**</span></span>  
<span data-ttu-id="8380a-571">función Hello IsBitSet pruebas si un bit está establecido o no</span><span class="sxs-lookup"><span data-stu-id="8380a-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="8380a-572">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="8380a-573">valor: un valor numérico que es evalúa. Flag: un valor numérico que tiene Hola bit toobe evaluada</span><span class="sxs-lookup"><span data-stu-id="8380a-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="8380a-574">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="8380a-575">Devuelve el valor True porque bit "4" está establecido en el valor hexadecimal de Hola "F"</span><span class="sxs-lookup"><span data-stu-id="8380a-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="8380a-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="8380a-576">IsDate</span></span>
<span data-ttu-id="8380a-577">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-577">**Description:**</span></span>  
<span data-ttu-id="8380a-578">Si expresión Hola puede ser evalúa como un tipo de fecha y hora, Hola función IsDate evalúa tooTrue.</span><span class="sxs-lookup"><span data-stu-id="8380a-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="8380a-579">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="8380a-580">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-580">**Remarks:**</span></span>  
<span data-ttu-id="8380a-581">Usar toodetermine si CDate() pueda realizarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="8380a-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="8380a-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="8380a-582">IsCert</span></span>
<span data-ttu-id="8380a-583">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-583">**Description:**</span></span>  
<span data-ttu-id="8380a-584">Devuelve true si se pueden serializar los datos sin procesar de hello en el objeto de certificado X509Certificate2. NET.</span><span class="sxs-lookup"><span data-stu-id="8380a-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="8380a-585">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="8380a-586">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="8380a-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8380a-587">matriz de bytes de Hello puede ser (DER) codifica datos binarios o X.509 codificado base 64.</span><span class="sxs-lookup"><span data-stu-id="8380a-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="8380a-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="8380a-588">IsEmpty</span></span>
<span data-ttu-id="8380a-589">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-589">**Description:**</span></span>  
<span data-ttu-id="8380a-590">Si el atributo de hello está presente en hello CS o MV pero da como resultado una cadena vacía tooan, IsEmpty (función) Hola evalúa tooTrue.</span><span class="sxs-lookup"><span data-stu-id="8380a-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="8380a-591">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="8380a-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="8380a-592">IsGuid</span></span>
<span data-ttu-id="8380a-593">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-593">**Description:**</span></span>  
<span data-ttu-id="8380a-594">Si la cadena de hello podría ser convertido tooa GUID, función isguid da como resultado de hello evalúa tootrue.</span><span class="sxs-lookup"><span data-stu-id="8380a-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="8380a-595">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="8380a-596">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-596">**Remarks:**</span></span>  
<span data-ttu-id="8380a-597">un GUID se define como una cadena que sigue uno de estos patrones: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}.</span><span class="sxs-lookup"><span data-stu-id="8380a-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="8380a-598">Usar toodetermine si CGuid() pueda realizarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="8380a-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="8380a-599">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="8380a-600">Si hello StrAttribute tiene un formato GUID, devuelve una representación binaria, en caso contrario, devuelven un valor Null.</span><span class="sxs-lookup"><span data-stu-id="8380a-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="8380a-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="8380a-601">IsNull</span></span>
<span data-ttu-id="8380a-602">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-602">**Description:**</span></span>  
<span data-ttu-id="8380a-603">Si expresión Hola se evalúa como tooNull, función de hello IsNull devuelve true.</span><span class="sxs-lookup"><span data-stu-id="8380a-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="8380a-604">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="8380a-605">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-605">**Remarks:**</span></span>  
<span data-ttu-id="8380a-606">Para un atributo, un valor Null se expresa por falta de hello del atributo Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="8380a-607">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="8380a-608">Devuelve True si el atributo de hello no está presente en hello CS o MV.</span><span class="sxs-lookup"><span data-stu-id="8380a-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="8380a-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="8380a-609">IsNullOrEmpty</span></span>
<span data-ttu-id="8380a-610">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-610">**Description:**</span></span>  
<span data-ttu-id="8380a-611">Si la expresión de hello es null o una cadena vacía, función de hello IsNullOrEmpty devuelve true.</span><span class="sxs-lookup"><span data-stu-id="8380a-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="8380a-612">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="8380a-613">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-613">**Remarks:**</span></span>  
<span data-ttu-id="8380a-614">Para un atributo, da como resultado tooTrue si el atributo de hello no está presente o está presente pero es una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="8380a-615">inverso de Hola de esta función se denomina IsPresent.</span><span class="sxs-lookup"><span data-stu-id="8380a-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="8380a-616">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="8380a-617">Devuelve True si el atributo de hello no está presente o es una cadena vacía en hello CS o MV.</span><span class="sxs-lookup"><span data-stu-id="8380a-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="8380a-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="8380a-618">IsNumeric</span></span>
<span data-ttu-id="8380a-619">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-619">**Description:**</span></span>  
<span data-ttu-id="8380a-620">Hola función IsNumeric devuelve un valor booleano que indica si una expresión se puede evaluar como un tipo de número.</span><span class="sxs-lookup"><span data-stu-id="8380a-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="8380a-621">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="8380a-622">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-622">**Remarks:**</span></span>  
<span data-ttu-id="8380a-623">Usar toodetermine si CNum() puede ser una expresión de hello tooparse correcta.</span><span class="sxs-lookup"><span data-stu-id="8380a-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="8380a-624">IsString</span><span class="sxs-lookup"><span data-stu-id="8380a-624">IsString</span></span>
<span data-ttu-id="8380a-625">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-625">**Description:**</span></span>  
<span data-ttu-id="8380a-626">Si la expresión de hello puede se evaluado tooa tipo string, función isstring da de hello evalúa tooTrue.</span><span class="sxs-lookup"><span data-stu-id="8380a-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="8380a-627">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="8380a-628">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-628">**Remarks:**</span></span>  
<span data-ttu-id="8380a-629">Usar toodetermine si CStr() puede ser una expresión de hello tooparse correcta.</span><span class="sxs-lookup"><span data-stu-id="8380a-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="8380a-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="8380a-630">IsPresent</span></span>
<span data-ttu-id="8380a-631">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-631">**Description:**</span></span>  
<span data-ttu-id="8380a-632">Si expresión Hola se evalúa como cadena tooa que no es Null y no está vacío, a continuación, Hola IsPresent función devuelve true.</span><span class="sxs-lookup"><span data-stu-id="8380a-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="8380a-633">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="8380a-634">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-634">**Remarks:**</span></span>  
<span data-ttu-id="8380a-635">inverso de Hola de esta función se denomina IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="8380a-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="8380a-636">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="8380a-637">Elemento</span><span class="sxs-lookup"><span data-stu-id="8380a-637">Item</span></span>
<span data-ttu-id="8380a-638">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-638">**Description:**</span></span>  
<span data-ttu-id="8380a-639">Hola función Item devuelve un elemento de un cadena o atributo multivalor.</span><span class="sxs-lookup"><span data-stu-id="8380a-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="8380a-640">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="8380a-641">attribute: atributo de varios valores</span><span class="sxs-lookup"><span data-stu-id="8380a-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="8380a-642">índice: elemento de tooan de índice de cadena multivalor Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="8380a-643">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-643">**Remarks:**</span></span>  
<span data-ttu-id="8380a-644">Hola función Item es útil junto con hello función Contains, ya que esta última función de hello devuelve el elemento de tooan de índice de Hola de atributo con varios valores de hello.</span><span class="sxs-lookup"><span data-stu-id="8380a-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="8380a-645">Se produce un error si el índice está fuera de los límites.</span><span class="sxs-lookup"><span data-stu-id="8380a-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="8380a-646">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="8380a-647">Devuelve Hola dirección de correo electrónico principal.</span><span class="sxs-lookup"><span data-stu-id="8380a-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="8380a-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="8380a-648">ItemOrNull</span></span>
<span data-ttu-id="8380a-649">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-649">**Description:**</span></span>  
<span data-ttu-id="8380a-650">Hola función ItemOrNull devuelve un elemento de un cadena o atributo multivalor.</span><span class="sxs-lookup"><span data-stu-id="8380a-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="8380a-651">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="8380a-652">attribute: atributo de varios valores</span><span class="sxs-lookup"><span data-stu-id="8380a-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="8380a-653">índice: elemento de tooan de índice de cadena multivalor Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="8380a-654">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-654">**Remarks:**</span></span>  
<span data-ttu-id="8380a-655">Hola función ItemOrNull es útil junto con hello función Contains, ya que esta última función de hello devuelve el elemento de tooan de índice de Hola de atributo con varios valores de hello.</span><span class="sxs-lookup"><span data-stu-id="8380a-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="8380a-656">Si el índice está fuera de los límites, devuelve un valor Null.</span><span class="sxs-lookup"><span data-stu-id="8380a-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="8380a-657">Join</span><span class="sxs-lookup"><span data-stu-id="8380a-657">Join</span></span>
<span data-ttu-id="8380a-658">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-658">**Description:**</span></span>  
<span data-ttu-id="8380a-659">función de combinación de Hello toma una cadena multivalor y devuelve una cadena de un solo valor con el separador especificado insertado entre cada elemento.</span><span class="sxs-lookup"><span data-stu-id="8380a-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="8380a-660">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="8380a-661">atributo: atributo multivalor que contiene cadenas toobe unido.</span><span class="sxs-lookup"><span data-stu-id="8380a-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="8380a-662">delimitador: cualquier cadena, tooseparate usado Hola subcadenas en hello devuelve la cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="8380a-663">Si se omite, Hola carácter de espacio ("") se utiliza.</span><span class="sxs-lookup"><span data-stu-id="8380a-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="8380a-664">Si Delimiter es una cadena de longitud cero ("") o Nothing, todos los elementos de lista de Hola se concatenan sin delimitadores.</span><span class="sxs-lookup"><span data-stu-id="8380a-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="8380a-665">**Comentarios**</span><span class="sxs-lookup"><span data-stu-id="8380a-665">**Remarks**</span></span>  
<span data-ttu-id="8380a-666">Hay paridad entre las funciones de división y combinación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="8380a-667">Hola función Join toma una matriz de cadenas y une mediante una cadena de delimitador, tooreturn una sola cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="8380a-668">Hola función Split toma una cadena y la separa en delimitador de hello, tooreturn una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="8380a-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="8380a-669">Sin embargo, una diferencia clave es que Join puede concatenar cadenas con cualquier cadena de delimitación, mientras que attribute puede separar solo cadenas mediante un delimitador de carácter único.</span><span class="sxs-lookup"><span data-stu-id="8380a-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="8380a-670">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="8380a-671">Podría devolver: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="8380a-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="8380a-672">LCase</span><span class="sxs-lookup"><span data-stu-id="8380a-672">LCase</span></span>
<span data-ttu-id="8380a-673">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-673">**Description:**</span></span>  
<span data-ttu-id="8380a-674">Hola función LCase convierte todos los caracteres en un caso de toolower de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="8380a-675">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="8380a-676">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="8380a-677">devuelve "test".</span><span class="sxs-lookup"><span data-stu-id="8380a-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="8380a-678">Left</span><span class="sxs-lookup"><span data-stu-id="8380a-678">Left</span></span>
<span data-ttu-id="8380a-679">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-679">**Description:**</span></span>  
<span data-ttu-id="8380a-680">función Left Hola devuelve un número especificado de caracteres desde la izquierda de Hola de una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="8380a-681">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="8380a-682">cadena: Hola tooreturn caracteres de una cadena de</span><span class="sxs-lookup"><span data-stu-id="8380a-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="8380a-683">NumChars: un número que identifica el número de Hola de tooreturn de caracteres desde el principio de hello (izquierda) de cadena</span><span class="sxs-lookup"><span data-stu-id="8380a-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="8380a-684">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-684">**Remarks:**</span></span>  
<span data-ttu-id="8380a-685">Una cadena que contiene los primeros caracteres numChars hello en cadena:</span><span class="sxs-lookup"><span data-stu-id="8380a-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="8380a-686">Con numChars = 0, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="8380a-687">Con numChars < 0, se devuelve una cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="8380a-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="8380a-688">Si la cadena es null, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-688">If string is null, return empty string.</span></span>

<span data-ttu-id="8380a-689">Si la cadena contiene menos caracteres que el número de hello especificado en numChars, se devuelve un toostring idénticos de cadena (que es, que contiene todos los caracteres en el parámetro 1).</span><span class="sxs-lookup"><span data-stu-id="8380a-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="8380a-690">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="8380a-691">devuelve “Joh”.</span><span class="sxs-lookup"><span data-stu-id="8380a-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="8380a-692">Len</span><span class="sxs-lookup"><span data-stu-id="8380a-692">Len</span></span>
<span data-ttu-id="8380a-693">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-693">**Description:**</span></span>  
<span data-ttu-id="8380a-694">Hola función Len devuelve el número de caracteres en una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="8380a-695">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="8380a-696">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="8380a-697">devuelve 8.</span><span class="sxs-lookup"><span data-stu-id="8380a-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="8380a-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="8380a-698">LTrim</span></span>
<span data-ttu-id="8380a-699">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-699">**Description:**</span></span>  
<span data-ttu-id="8380a-700">Hola función LTrim quita los espacios en blanco de una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="8380a-701">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="8380a-702">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="8380a-703">devuelve "Test".</span><span class="sxs-lookup"><span data-stu-id="8380a-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="8380a-704">Mid</span><span class="sxs-lookup"><span data-stu-id="8380a-704">Mid</span></span>
<span data-ttu-id="8380a-705">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-705">**Description:**</span></span>  
<span data-ttu-id="8380a-706">Hola Mid función devuelve un número especificado de caracteres desde la posición especificada en una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="8380a-707">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="8380a-708">cadena: Hola tooreturn caracteres de una cadena de</span><span class="sxs-lookup"><span data-stu-id="8380a-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="8380a-709">iniciar: un número que identifica Hola a partir de la posición en la cadena de caracteres de tooreturn de</span><span class="sxs-lookup"><span data-stu-id="8380a-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="8380a-710">NumChars: un número que identifica el número de Hola de tooreturn de caracteres desde la posición en la cadena</span><span class="sxs-lookup"><span data-stu-id="8380a-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="8380a-711">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-711">**Remarks:**</span></span>  
<span data-ttu-id="8380a-712">devuelve caracteres numChars que comienzan por la posición de inicio en una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="8380a-713">Una cadena que contiene caracteres numChars de la posición de inicio en una cadena:</span><span class="sxs-lookup"><span data-stu-id="8380a-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="8380a-714">Con numChars = 0, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="8380a-715">Con numChars < 0, se devuelve una cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="8380a-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="8380a-716">Si iniciar > Hola longitud de cadena, devuelven la cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="8380a-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="8380a-717">Con start <= 0, se devuelve la cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="8380a-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="8380a-718">Si la cadena es null, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-718">If string is null, return empty string.</span></span>

<span data-ttu-id="8380a-719">Si no hay caracteres numChar restantes en la cadena de la posición de inicio, se devuelve el máximo de caracteres posible.</span><span class="sxs-lookup"><span data-stu-id="8380a-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="8380a-720">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="8380a-721">devuelve “hn Do”.</span><span class="sxs-lookup"><span data-stu-id="8380a-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="8380a-722">Devuelve "Doe".</span><span class="sxs-lookup"><span data-stu-id="8380a-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="8380a-723">Now</span><span class="sxs-lookup"><span data-stu-id="8380a-723">Now</span></span>
<span data-ttu-id="8380a-724">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-724">**Description:**</span></span>  
<span data-ttu-id="8380a-725">Hello ahora función devuelve una fecha y hora especificar Hola fecha y hora, actual según tooyour fecha del sistema del equipo y la hora.</span><span class="sxs-lookup"><span data-stu-id="8380a-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="8380a-726">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="8380a-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="8380a-727">NumFromDate</span></span>
<span data-ttu-id="8380a-728">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-728">**Description:**</span></span>  
<span data-ttu-id="8380a-729">Hola función NumFromDate devuelve una fecha en formato de fecha de AD.</span><span class="sxs-lookup"><span data-stu-id="8380a-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="8380a-730">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="8380a-731">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="8380a-732">devuelve 129699324000000000.</span><span class="sxs-lookup"><span data-stu-id="8380a-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="8380a-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="8380a-733">PadLeft</span></span>
<span data-ttu-id="8380a-734">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-734">**Description:**</span></span>  
<span data-ttu-id="8380a-735">función de Hello PadLeft rellena hacia la izquierda un tooa de cadena especificado longitud mediante el carácter de relleno proporcionado.</span><span class="sxs-lookup"><span data-stu-id="8380a-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="8380a-736">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="8380a-737">cadena: Hola toopad de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-737">string: hello string toopad.</span></span>
* <span data-ttu-id="8380a-738">longitud: un entero que representa Hola deseado longitud de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="8380a-739">padCharacter: una cadena que consta de un toouse único carácter como carácter de relleno de Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="8380a-740">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-740">**Remarks:**</span></span>

* <span data-ttu-id="8380a-741">Si la longitud de Hola de cadena es menor que la longitud, padCharacter es toohello repetidamente anexados principio (izquierda) de cadena hasta que tenga un toolength de igual longitud.</span><span class="sxs-lookup"><span data-stu-id="8380a-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="8380a-742">PadCharacter puede ser un carácter de espacio, pero no puede ser un valor Null.</span><span class="sxs-lookup"><span data-stu-id="8380a-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="8380a-743">Si la longitud de Hola de cadena es mayor que la longitud de tooor igual, la cadena se devuelve sin cambios.</span><span class="sxs-lookup"><span data-stu-id="8380a-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="8380a-744">Si la cadena tiene una longitud mayor que o igual toolength, se devuelve un toostring idénticos de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="8380a-745">Si la longitud de Hola de cadena es menor que la longitud, una nueva cadena de hello deseado se devuelve la longitud que contiene una cadena rellenada con un padCharacter.</span><span class="sxs-lookup"><span data-stu-id="8380a-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="8380a-746">Si la cadena es null, la función hello devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="8380a-747">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="8380a-748">devuelve "000000User".</span><span class="sxs-lookup"><span data-stu-id="8380a-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="8380a-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="8380a-749">PadRight</span></span>
<span data-ttu-id="8380a-750">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-750">**Description:**</span></span>  
<span data-ttu-id="8380a-751">función de Hello PadRight rellena hacia la derecha un tooa de cadena especificado longitud mediante el carácter de relleno proporcionado.</span><span class="sxs-lookup"><span data-stu-id="8380a-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="8380a-752">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="8380a-753">cadena: Hola toopad de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-753">string: hello string toopad.</span></span>
* <span data-ttu-id="8380a-754">longitud: un entero que representa Hola deseado longitud de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="8380a-755">padCharacter: una cadena que consta de un toouse único carácter como carácter de relleno de Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="8380a-756">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-756">**Remarks:**</span></span>

* <span data-ttu-id="8380a-757">Si la longitud de Hola de cadena es menor que la longitud, padCharacter es toohello repetidamente anexados final (derecha) de cadena, hasta que tenga un toolength de igual longitud.</span><span class="sxs-lookup"><span data-stu-id="8380a-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="8380a-758">PadCharacter puede ser un carácter de espacio, pero no puede ser un valor Null.</span><span class="sxs-lookup"><span data-stu-id="8380a-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="8380a-759">Si la longitud de Hola de cadena es mayor que la longitud de tooor igual, la cadena se devuelve sin cambios.</span><span class="sxs-lookup"><span data-stu-id="8380a-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="8380a-760">Si la cadena tiene una longitud mayor que o igual toolength, se devuelve un toostring idénticos de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="8380a-761">Si la longitud de Hola de cadena es menor que la longitud, una nueva cadena de hello deseado se devuelve la longitud que contiene una cadena rellenada con un padCharacter.</span><span class="sxs-lookup"><span data-stu-id="8380a-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="8380a-762">Si la cadena es null, la función hello devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="8380a-763">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="8380a-764">devuelve "User000000".</span><span class="sxs-lookup"><span data-stu-id="8380a-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="8380a-765">PCase</span><span class="sxs-lookup"><span data-stu-id="8380a-765">PCase</span></span>
<span data-ttu-id="8380a-766">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-766">**Description:**</span></span>  
<span data-ttu-id="8380a-767">Hola función PCase convierte el primer carácter de cada palabra delimitada por espacios en el caso de tooupper de cadena de Hola y todos los demás caracteres se convierten toolower caso.</span><span class="sxs-lookup"><span data-stu-id="8380a-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="8380a-768">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="8380a-769">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-769">**Remarks:**</span></span>

* <span data-ttu-id="8380a-770">Esta función no proporciona actualmente tooconvert grafía apropiada una palabra que esté completamente en mayúscula, por ejemplo, un acrónimo.</span><span class="sxs-lookup"><span data-stu-id="8380a-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="8380a-771">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="8380a-772">devuelve "test".</span><span class="sxs-lookup"><span data-stu-id="8380a-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="8380a-773">devuelve "Test".</span><span class="sxs-lookup"><span data-stu-id="8380a-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="8380a-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="8380a-774">RandomNum</span></span>
<span data-ttu-id="8380a-775">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-775">**Description:**</span></span>  
<span data-ttu-id="8380a-776">Hola función RandomNum devuelve un número aleatorio entre un intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="8380a-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="8380a-777">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="8380a-778">iniciar: un número identificación Hola límite inferior de hello valor aleatorio toogenerate</span><span class="sxs-lookup"><span data-stu-id="8380a-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="8380a-779">extremo: un número identificación Hola límite superior de hello valor aleatorio toogenerate</span><span class="sxs-lookup"><span data-stu-id="8380a-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="8380a-780">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="8380a-781">puede devolver 734.</span><span class="sxs-lookup"><span data-stu-id="8380a-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="8380a-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="8380a-782">RemoveDuplicates</span></span>
<span data-ttu-id="8380a-783">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-783">**Description:**</span></span>  
<span data-ttu-id="8380a-784">Hola función RemoveDuplicates toma una cadena multivalor y asegúrese de que cada valor sea único.</span><span class="sxs-lookup"><span data-stu-id="8380a-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="8380a-785">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="8380a-786">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="8380a-787">devuelve un atributo proxyAddress saneado donde se han quitado todos los valores duplicados.</span><span class="sxs-lookup"><span data-stu-id="8380a-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="8380a-788">Sustituya</span><span class="sxs-lookup"><span data-stu-id="8380a-788">Replace</span></span>
<span data-ttu-id="8380a-789">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-789">**Description:**</span></span>  
<span data-ttu-id="8380a-790">Hola función Replace reemplaza todas las apariciones de una cadena de tooanother de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="8380a-791">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="8380a-792">cadena: una cadena tooreplace valores en.</span><span class="sxs-lookup"><span data-stu-id="8380a-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="8380a-793">OldValue: Hola cadena toosearch para y tooreplace.</span><span class="sxs-lookup"><span data-stu-id="8380a-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="8380a-794">NewValue: Hola tooreplace de cadena a.</span><span class="sxs-lookup"><span data-stu-id="8380a-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="8380a-795">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-795">**Remarks:**</span></span>  
<span data-ttu-id="8380a-796">función Hello reconoce Hola después monikers especiales:</span><span class="sxs-lookup"><span data-stu-id="8380a-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="8380a-797">\n: nueva línea</span><span class="sxs-lookup"><span data-stu-id="8380a-797">\n – New Line</span></span>
* <span data-ttu-id="8380a-798">\r: retorno de carro</span><span class="sxs-lookup"><span data-stu-id="8380a-798">\r – Carriage Return</span></span>
* <span data-ttu-id="8380a-799">\t: tabulación</span><span class="sxs-lookup"><span data-stu-id="8380a-799">\t – Tab</span></span>

<span data-ttu-id="8380a-800">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="8380a-801">Reemplaza CRLF por una coma y un espacio y podría provocar demasiado "One Microsoft Way, Redmond, WA, EE"</span><span class="sxs-lookup"><span data-stu-id="8380a-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="8380a-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="8380a-802">ReplaceChars</span></span>
<span data-ttu-id="8380a-803">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-803">**Description:**</span></span>  
<span data-ttu-id="8380a-804">Hola función ReplaceChars reemplaza todas las apariciones de caracteres que se encuentran en hello cadena ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="8380a-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="8380a-805">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="8380a-806">cadena: caracteres de una cadena tooreplace de.</span><span class="sxs-lookup"><span data-stu-id="8380a-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="8380a-807">ReplacePattern: una cadena que contiene un diccionario con caracteres tooreplace.</span><span class="sxs-lookup"><span data-stu-id="8380a-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="8380a-808">formato de Hello es {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetN} que el origen es Hola carácter toofind y destino Hola cadena tooreplace con.</span><span class="sxs-lookup"><span data-stu-id="8380a-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="8380a-809">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-809">**Remarks:**</span></span>

* <span data-ttu-id="8380a-810">función Hello toma cada aparición de los orígenes definidos y los reemplaza con destinos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="8380a-811">origen de Hello debe ser exactamente un carácter (unicode).</span><span class="sxs-lookup"><span data-stu-id="8380a-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="8380a-812">origen de Hello no puede estar vacío ni ser más de un carácter (error de análisis).</span><span class="sxs-lookup"><span data-stu-id="8380a-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="8380a-813">destino de Hello puede tener varios caracteres, por ejemplo ö:oe, β.</span><span class="sxs-lookup"><span data-stu-id="8380a-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="8380a-814">destino de Hello puede estar vacía que indica que se deben quitar los caracteres de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="8380a-815">origen de Hello distingue mayúsculas de minúsculas y debe ser una coincidencia exacta.</span><span class="sxs-lookup"><span data-stu-id="8380a-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="8380a-816">Hola, (coma) y: (dos puntos) son caracteres reservados y no se puede reemplazar utilizando esta función.</span><span class="sxs-lookup"><span data-stu-id="8380a-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="8380a-817">Se omiten los espacios y otros caracteres en blanco en hello cadena ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="8380a-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="8380a-818">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="8380a-819">Devuelve Raksmorgas.</span><span class="sxs-lookup"><span data-stu-id="8380a-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="8380a-820">Devuelve "oneil", ya único TIC de hello es toobe definido quitado.</span><span class="sxs-lookup"><span data-stu-id="8380a-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="8380a-821">Right</span><span class="sxs-lookup"><span data-stu-id="8380a-821">Right</span></span>
<span data-ttu-id="8380a-822">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-822">**Description:**</span></span>  
<span data-ttu-id="8380a-823">función Right Hola devuelve un número especificado de caracteres de hello derecho (final) de una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="8380a-824">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="8380a-825">cadena: Hola tooreturn caracteres de una cadena de</span><span class="sxs-lookup"><span data-stu-id="8380a-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="8380a-826">NumChars: un número que identifica el número de Hola de tooreturn de caracteres de fin de hello (derecha) de cadena</span><span class="sxs-lookup"><span data-stu-id="8380a-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="8380a-827">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-827">**Remarks:**</span></span>  
<span data-ttu-id="8380a-828">Se devuelven caracteres NumChars desde la última posición de Hola de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="8380a-829">Una cadena que contiene los últimos caracteres numChars hello en cadena:</span><span class="sxs-lookup"><span data-stu-id="8380a-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="8380a-830">Con numChars = 0, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="8380a-831">Con numChars < 0, se devuelve una cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="8380a-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="8380a-832">Si la cadena es null, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-832">If string is null, return empty string.</span></span>

<span data-ttu-id="8380a-833">Si la cadena contiene menos caracteres que Hola número especificado en NumChars, se devuelve un toostring idénticos de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="8380a-834">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="8380a-835">devuelve "Doe".</span><span class="sxs-lookup"><span data-stu-id="8380a-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="8380a-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="8380a-836">RTrim</span></span>
<span data-ttu-id="8380a-837">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-837">**Description:**</span></span>  
<span data-ttu-id="8380a-838">Hola función RTrim quita los espacios en blanco de una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="8380a-839">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="8380a-840">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="8380a-841">devuelve "Test".</span><span class="sxs-lookup"><span data-stu-id="8380a-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="8380a-842">Seleccionar</span><span class="sxs-lookup"><span data-stu-id="8380a-842">Select</span></span>
<span data-ttu-id="8380a-843">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="8380a-843">**Description:**</span></span>  
<span data-ttu-id="8380a-844">Procesa todos los valores de un atributo de valor múltiple (o el resultado de una expresión) según la función especificada.</span><span class="sxs-lookup"><span data-stu-id="8380a-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="8380a-845">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="8380a-846">elemento: representa un elemento atributo multivalor Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="8380a-847">atributo: atributo multivalor Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="8380a-848">expression: una expresión que devuelve una colección de valores</span><span class="sxs-lookup"><span data-stu-id="8380a-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="8380a-849">condición: cualquier función que puede procesar un elemento atributo Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="8380a-850">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="8380a-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="8380a-851">Devolver todos los valores de hello Hola atributo multivalor OtroTeléfono una vez que se han quitado los guiones (-).</span><span class="sxs-lookup"><span data-stu-id="8380a-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="8380a-852">Dividir</span><span class="sxs-lookup"><span data-stu-id="8380a-852">Split</span></span>
<span data-ttu-id="8380a-853">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-853">**Description:**</span></span>  
<span data-ttu-id="8380a-854">Hola función Split toma una cadena separada por un delimitador y hace que una cadena multivalor.</span><span class="sxs-lookup"><span data-stu-id="8380a-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="8380a-855">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="8380a-856">valor: Hola cadena con un tooseparate de carácter delimitador.</span><span class="sxs-lookup"><span data-stu-id="8380a-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="8380a-857">delimitador: único toobe de caracteres que se usa como delimitador de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="8380a-858">limit: número máximo de valores que se pueden devolver.</span><span class="sxs-lookup"><span data-stu-id="8380a-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="8380a-859">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="8380a-860">Devuelve una cadena multivalor con 2 elementos útiles para el atributo proxyAddress de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="8380a-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="8380a-861">StringFromGuid</span></span>
<span data-ttu-id="8380a-862">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-862">**Description:**</span></span>  
<span data-ttu-id="8380a-863">Hola función StringFromGuid toma un GUID binario y lo convierte en la cadena de tooa</span><span class="sxs-lookup"><span data-stu-id="8380a-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="8380a-864">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="8380a-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="8380a-865">StringFromSid</span></span>
<span data-ttu-id="8380a-866">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-866">**Description:**</span></span>  
<span data-ttu-id="8380a-867">Hola función StringFromSid convierte una matriz de bytes que contiene una cadena de tooa del identificador de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8380a-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="8380a-868">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="8380a-869">Switch</span><span class="sxs-lookup"><span data-stu-id="8380a-869">Switch</span></span>
<span data-ttu-id="8380a-870">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-870">**Description:**</span></span>  
<span data-ttu-id="8380a-871">función de conmutador de Hello es tooreturn usa un valor único basado en condiciones evaluadas.</span><span class="sxs-lookup"><span data-stu-id="8380a-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="8380a-872">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="8380a-873">expr: expresión Variant que desee tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="8380a-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="8380a-874">valor: toobe de valor devuelto si la expresión correspondiente de hello es True.</span><span class="sxs-lookup"><span data-stu-id="8380a-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="8380a-875">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-875">**Remarks:**</span></span>  
<span data-ttu-id="8380a-876">Hola argumento de la función de conmutador lista está formada por pares de expresiones y valores.</span><span class="sxs-lookup"><span data-stu-id="8380a-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="8380a-877">Hola las expresiones se evalúan de izquierda tooright y se devuelve el valor de hello asociada Hola primera expresión tooevaluate tooTrue.</span><span class="sxs-lookup"><span data-stu-id="8380a-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="8380a-878">Si las partes de hello no están correctamente emparejadas, se produce un error en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8380a-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="8380a-879">Por ejemplo, si expr1 es True, Switch devuelve value1.</span><span class="sxs-lookup"><span data-stu-id="8380a-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="8380a-880">Si expr-1 es False, pero expr-2 es True, Switch devuelve value-2, etc.</span><span class="sxs-lookup"><span data-stu-id="8380a-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="8380a-881">Switch devuelve Nothing si:</span><span class="sxs-lookup"><span data-stu-id="8380a-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="8380a-882">Ninguna de las expresiones de hello son True.</span><span class="sxs-lookup"><span data-stu-id="8380a-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="8380a-883">la primera expresión es True de Hello tiene un valor correspondiente que es Null.</span><span class="sxs-lookup"><span data-stu-id="8380a-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="8380a-884">Switch evalúa todas las expresiones, aunque devuelva solo una de ellas.</span><span class="sxs-lookup"><span data-stu-id="8380a-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="8380a-885">Por este motivo, debe vigilar efectos secundarios no deseados.</span><span class="sxs-lookup"><span data-stu-id="8380a-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="8380a-886">Por ejemplo, si la evaluación de Hola de cualquier expresión tiene como resultado una división por cero error, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="8380a-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="8380a-887">Valor también puede ser la función de Error de hello, lo que devolvería una cadena personalizada.</span><span class="sxs-lookup"><span data-stu-id="8380a-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="8380a-888">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="8380a-889">Devuelve el idioma de hello hablado en algunas ciudades importantes, en caso contrario, devuelve un Error.</span><span class="sxs-lookup"><span data-stu-id="8380a-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="8380a-890">Trim</span><span class="sxs-lookup"><span data-stu-id="8380a-890">Trim</span></span>
<span data-ttu-id="8380a-891">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-891">**Description:**</span></span>  
<span data-ttu-id="8380a-892">función Trim Hello quita iniciales y finales de espacios en blanco de una cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="8380a-893">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="8380a-894">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="8380a-895">devuelve "test".</span><span class="sxs-lookup"><span data-stu-id="8380a-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="8380a-896">Quita espacios para cada valor de atributo proxyAddress de hello iniciales y finales.</span><span class="sxs-lookup"><span data-stu-id="8380a-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="8380a-897">UCase</span><span class="sxs-lookup"><span data-stu-id="8380a-897">UCase</span></span>
<span data-ttu-id="8380a-898">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-898">**Description:**</span></span>  
<span data-ttu-id="8380a-899">Hola función UCase convierte todos los caracteres en un caso de tooupper de cadena.</span><span class="sxs-lookup"><span data-stu-id="8380a-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="8380a-900">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="8380a-901">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="8380a-902">devuelve "test".</span><span class="sxs-lookup"><span data-stu-id="8380a-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="8380a-903">Where</span><span class="sxs-lookup"><span data-stu-id="8380a-903">Where</span></span>

<span data-ttu-id="8380a-904">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="8380a-904">**Description:**</span></span>  
<span data-ttu-id="8380a-905">Devuelve un subconjunto de valores de un atributo de valor múltiple (o el resultado de una expresión) según la función especificada.</span><span class="sxs-lookup"><span data-stu-id="8380a-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="8380a-906">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="8380a-907">elemento: representa un elemento atributo multivalor Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="8380a-908">atributo: atributo multivalor Hola</span><span class="sxs-lookup"><span data-stu-id="8380a-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="8380a-909">condición: cualquier expresión que se puede evaluar tootrue o false</span><span class="sxs-lookup"><span data-stu-id="8380a-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="8380a-910">expression: una expresión que devuelve una colección de valores</span><span class="sxs-lookup"><span data-stu-id="8380a-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="8380a-911">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="8380a-912">Devolver valores de certificado de hello en hello userCertificate de atributo con varios valores que no se ha caducado.</span><span class="sxs-lookup"><span data-stu-id="8380a-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="8380a-913">With</span><span class="sxs-lookup"><span data-stu-id="8380a-913">With</span></span>
<span data-ttu-id="8380a-914">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-914">**Description:**</span></span>  
<span data-ttu-id="8380a-915">Hola con función proporciona un toosimplify de forma una expresión compleja mediante el uso de una variable toorepresent una subexpresión que aparece una o varias veces en la expresión compleja Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="8380a-916">**Sintaxis:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="8380a-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="8380a-917">variable: representa Hola subexpresión.</span><span class="sxs-lookup"><span data-stu-id="8380a-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="8380a-918">subExpression: la que la variable representa.</span><span class="sxs-lookup"><span data-stu-id="8380a-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="8380a-919">complexExpression: una expresión compleja.</span><span class="sxs-lookup"><span data-stu-id="8380a-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="8380a-920">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="8380a-921">Es funcionalmente equivalente a:</span><span class="sxs-lookup"><span data-stu-id="8380a-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="8380a-922">Que devuelve solo los valores de los certificados vigentes en el atributo userCertificate de Hola.</span><span class="sxs-lookup"><span data-stu-id="8380a-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="8380a-923">Word</span><span class="sxs-lookup"><span data-stu-id="8380a-923">Word</span></span>
<span data-ttu-id="8380a-924">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="8380a-924">**Description:**</span></span>  
<span data-ttu-id="8380a-925">Hola función Word devuelve una palabra contenida dentro de una cadena según los parámetros que describen toouse de delimitadores de Hola y Hola word número tooreturn.</span><span class="sxs-lookup"><span data-stu-id="8380a-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="8380a-926">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="8380a-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="8380a-927">cadena: Hola tooreturn de cadena de una palabra.</span><span class="sxs-lookup"><span data-stu-id="8380a-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="8380a-928">WordNumber: un número que identifica qué número de palabras debe devolver.</span><span class="sxs-lookup"><span data-stu-id="8380a-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="8380a-929">delimitadores: una cadena que representa los delimitadores de Hola que deben ser utilizados tooidentify palabras</span><span class="sxs-lookup"><span data-stu-id="8380a-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="8380a-930">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="8380a-930">**Remarks:**</span></span>  
<span data-ttu-id="8380a-931">Cada cadena de caracteres de cadena separados por hello uno de los caracteres de hello en los delimitadores se identifican como palabras:</span><span class="sxs-lookup"><span data-stu-id="8380a-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="8380a-932">Si el número es < 1, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="8380a-933">Si la cadena es Null, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="8380a-934">Si la cadena contiene menos palabras o si la cadena no contiene palabras identificadas por los delimitadores, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="8380a-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="8380a-935">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8380a-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="8380a-936">devuelve "brown".</span><span class="sxs-lookup"><span data-stu-id="8380a-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="8380a-937">devolvería "has".</span><span class="sxs-lookup"><span data-stu-id="8380a-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8380a-938">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8380a-938">Additional Resources</span></span>
* [<span data-ttu-id="8380a-939">Explicación de las expresiones declarativas de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="8380a-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="8380a-940">Sincronización de Azure AD Connect: personalización de las opciones de sincronización</span><span class="sxs-lookup"><span data-stu-id="8380a-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="8380a-941">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8380a-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
