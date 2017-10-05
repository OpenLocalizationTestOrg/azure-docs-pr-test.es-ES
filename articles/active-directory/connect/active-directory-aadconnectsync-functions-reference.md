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
ms.openlocfilehash: 926f52ef64eb79205dbfb344edc7d9bece2a6947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="4c145-103">Azure AD Connect Sync: referencia de funciones</span><span class="sxs-lookup"><span data-stu-id="4c145-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="4c145-104">En Azure AD Connect, las funciones se usan para manipular un valor de atributo durante la sincronización.</span><span class="sxs-lookup"><span data-stu-id="4c145-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="4c145-105">La sintaxis de las funciones se expresa con el siguiente formato: </span><span class="sxs-lookup"><span data-stu-id="4c145-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="4c145-106">Si una función está sobrecargada y acepta varias sintaxis, se enumeran todas las sintaxis válidas.</span><span class="sxs-lookup"><span data-stu-id="4c145-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="4c145-107">Las funciones están fuertemente tipadas y comprueban que el tipo pasado coincide con el tipo documentado.</span><span class="sxs-lookup"><span data-stu-id="4c145-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="4c145-108">Si el tipo no coincide, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="4c145-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="4c145-109">Los tipos se expresan con la siguiente sintaxis:</span><span class="sxs-lookup"><span data-stu-id="4c145-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="4c145-110">**bin** : binario</span><span class="sxs-lookup"><span data-stu-id="4c145-110">**bin** – Binary</span></span>
* <span data-ttu-id="4c145-111">**bool** : booleano</span><span class="sxs-lookup"><span data-stu-id="4c145-111">**bool** – Boolean</span></span>
* <span data-ttu-id="4c145-112">**dt** : fecha y hora UTC</span><span class="sxs-lookup"><span data-stu-id="4c145-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="4c145-113">**enum** : enumeración de constantes conocidas</span><span class="sxs-lookup"><span data-stu-id="4c145-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="4c145-114">**exp** : expresión, que se espera que evalúe en un booleano</span><span class="sxs-lookup"><span data-stu-id="4c145-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="4c145-115">**mvbin** : binario de varios valores</span><span class="sxs-lookup"><span data-stu-id="4c145-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="4c145-116">**mvstr** : cadena multivalor</span><span class="sxs-lookup"><span data-stu-id="4c145-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="4c145-117">**mvref** : referencia multivalor</span><span class="sxs-lookup"><span data-stu-id="4c145-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="4c145-118">**num** : numérico</span><span class="sxs-lookup"><span data-stu-id="4c145-118">**num** – Numeric</span></span>
* <span data-ttu-id="4c145-119">**ref** : referencia</span><span class="sxs-lookup"><span data-stu-id="4c145-119">**ref** – Reference</span></span>
* <span data-ttu-id="4c145-120">**str** : cadena</span><span class="sxs-lookup"><span data-stu-id="4c145-120">**str** – String</span></span>
* <span data-ttu-id="4c145-121">**var** : una variante de (casi) cualquier otro tipo</span><span class="sxs-lookup"><span data-stu-id="4c145-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="4c145-122">**void** : no devuelve un valor</span><span class="sxs-lookup"><span data-stu-id="4c145-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="4c145-123">Las funciones con los tipos **mvbin**, **mvstr** y **mvref** solo pueden funcionar en atributos con varios valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="4c145-124">Las funciones con **bin**, **str** y **ref** funcionan en atributos con un solo valor y con varios valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="4c145-125">Referencia de funciones</span><span class="sxs-lookup"><span data-stu-id="4c145-125">Functions Reference</span></span>
| <span data-ttu-id="4c145-126">Lista de funciones</span><span class="sxs-lookup"><span data-stu-id="4c145-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4c145-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="4c145-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="4c145-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="4c145-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="4c145-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="4c145-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="4c145-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="4c145-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="4c145-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="4c145-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="4c145-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="4c145-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="4c145-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="4c145-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="4c145-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="4c145-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="4c145-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="4c145-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="4c145-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="4c145-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="4c145-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="4c145-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="4c145-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="4c145-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="4c145-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="4c145-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="4c145-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="4c145-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="4c145-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="4c145-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="4c145-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="4c145-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="4c145-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="4c145-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="4c145-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="4c145-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="4c145-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="4c145-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="4c145-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="4c145-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="4c145-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="4c145-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="4c145-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="4c145-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="4c145-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="4c145-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="4c145-150">**Conversión**</span><span class="sxs-lookup"><span data-stu-id="4c145-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="4c145-151">CBool</span><span class="sxs-lookup"><span data-stu-id="4c145-151">CBool</span></span>](#cbool) |[<span data-ttu-id="4c145-152">CDate</span><span class="sxs-lookup"><span data-stu-id="4c145-152">CDate</span></span>](#cdate) |[<span data-ttu-id="4c145-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="4c145-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="4c145-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="4c145-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="4c145-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="4c145-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="4c145-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="4c145-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="4c145-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="4c145-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="4c145-158">CNum</span><span class="sxs-lookup"><span data-stu-id="4c145-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="4c145-159">CRef</span><span class="sxs-lookup"><span data-stu-id="4c145-159">CRef</span></span>](#cref) |[<span data-ttu-id="4c145-160">CStr</span><span class="sxs-lookup"><span data-stu-id="4c145-160">CStr</span></span>](#cstr) |[<span data-ttu-id="4c145-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="4c145-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="4c145-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="4c145-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="4c145-163">**Fecha y hora**</span><span class="sxs-lookup"><span data-stu-id="4c145-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="4c145-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="4c145-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="4c145-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="4c145-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="4c145-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="4c145-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="4c145-167">Now</span><span class="sxs-lookup"><span data-stu-id="4c145-167">Now</span></span>](#now) | |
| [<span data-ttu-id="4c145-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="4c145-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="4c145-169">**Directorio**</span><span class="sxs-lookup"><span data-stu-id="4c145-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="4c145-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="4c145-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="4c145-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="4c145-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="4c145-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="4c145-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="4c145-173">**Evaluación**</span><span class="sxs-lookup"><span data-stu-id="4c145-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="4c145-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="4c145-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="4c145-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="4c145-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="4c145-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="4c145-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="4c145-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="4c145-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="4c145-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="4c145-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="4c145-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="4c145-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="4c145-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="4c145-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="4c145-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="4c145-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="4c145-182">IsString</span><span class="sxs-lookup"><span data-stu-id="4c145-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="4c145-183">**Matemáticas**</span><span class="sxs-lookup"><span data-stu-id="4c145-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="4c145-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="4c145-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="4c145-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="4c145-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="4c145-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="4c145-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="4c145-187">**Con varios valores**</span><span class="sxs-lookup"><span data-stu-id="4c145-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="4c145-188">Contains</span><span class="sxs-lookup"><span data-stu-id="4c145-188">Contains</span></span>](#contains) |[<span data-ttu-id="4c145-189">Recuento</span><span class="sxs-lookup"><span data-stu-id="4c145-189">Count</span></span>](#count) |[<span data-ttu-id="4c145-190">Elemento</span><span class="sxs-lookup"><span data-stu-id="4c145-190">Item</span></span>](#item) |[<span data-ttu-id="4c145-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="4c145-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="4c145-192">Join</span><span class="sxs-lookup"><span data-stu-id="4c145-192">Join</span></span>](#join) |[<span data-ttu-id="4c145-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="4c145-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="4c145-194">Dividir</span><span class="sxs-lookup"><span data-stu-id="4c145-194">Split</span></span>](#split) | | |
| <span data-ttu-id="4c145-195">**Flujo de programa**</span><span class="sxs-lookup"><span data-stu-id="4c145-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="4c145-196">Error</span><span class="sxs-lookup"><span data-stu-id="4c145-196">Error</span></span>](#error) |[<span data-ttu-id="4c145-197">IIF</span><span class="sxs-lookup"><span data-stu-id="4c145-197">IIF</span></span>](#iif) |[<span data-ttu-id="4c145-198">Select</span><span class="sxs-lookup"><span data-stu-id="4c145-198">Select</span></span>](#select) |[<span data-ttu-id="4c145-199">Switch</span><span class="sxs-lookup"><span data-stu-id="4c145-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="4c145-200">Where</span><span class="sxs-lookup"><span data-stu-id="4c145-200">Where</span></span>](#where) |[<span data-ttu-id="4c145-201">With</span><span class="sxs-lookup"><span data-stu-id="4c145-201">With</span></span>](#with) | | | |
| <span data-ttu-id="4c145-202">**Texto**</span><span class="sxs-lookup"><span data-stu-id="4c145-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="4c145-203">GUID</span><span class="sxs-lookup"><span data-stu-id="4c145-203">GUID</span></span>](#guid) |[<span data-ttu-id="4c145-204">InStr</span><span class="sxs-lookup"><span data-stu-id="4c145-204">InStr</span></span>](#instr) |[<span data-ttu-id="4c145-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="4c145-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="4c145-206">LCase</span><span class="sxs-lookup"><span data-stu-id="4c145-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="4c145-207">Left</span><span class="sxs-lookup"><span data-stu-id="4c145-207">Left</span></span>](#left) |[<span data-ttu-id="4c145-208">Len</span><span class="sxs-lookup"><span data-stu-id="4c145-208">Len</span></span>](#len) |[<span data-ttu-id="4c145-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="4c145-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="4c145-210">Mid</span><span class="sxs-lookup"><span data-stu-id="4c145-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="4c145-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="4c145-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="4c145-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="4c145-212">PadRight</span></span>](#padright) |[<span data-ttu-id="4c145-213">PCase</span><span class="sxs-lookup"><span data-stu-id="4c145-213">PCase</span></span>](#pcase) |[<span data-ttu-id="4c145-214">Sustituya</span><span class="sxs-lookup"><span data-stu-id="4c145-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="4c145-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="4c145-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="4c145-216">Right</span><span class="sxs-lookup"><span data-stu-id="4c145-216">Right</span></span>](#right) |[<span data-ttu-id="4c145-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="4c145-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="4c145-218">Trim</span><span class="sxs-lookup"><span data-stu-id="4c145-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="4c145-219">UCase</span><span class="sxs-lookup"><span data-stu-id="4c145-219">UCase</span></span>](#ucase) |[<span data-ttu-id="4c145-220">Word</span><span class="sxs-lookup"><span data-stu-id="4c145-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="4c145-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="4c145-221">BitAnd</span></span>
<span data-ttu-id="4c145-222">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-222">**Description:**</span></span>  
<span data-ttu-id="4c145-223">: la función BitAnd establece los bits especificados en un valor.</span><span class="sxs-lookup"><span data-stu-id="4c145-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="4c145-224">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="4c145-225">value1, value2: valores numéricos que deberían estar unidos por el operador AND</span><span class="sxs-lookup"><span data-stu-id="4c145-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="4c145-226">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-226">**Remarks:**</span></span>  
<span data-ttu-id="4c145-227">: esta función convierte ambos parámetros en la representación binaria y establece un bit en los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="4c145-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="4c145-228">0: si uno o ambos de los bits correspondientes en *mask* y *flag* son 0</span><span class="sxs-lookup"><span data-stu-id="4c145-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="4c145-229">1: si ambos de los bits correspondientes son 1.</span><span class="sxs-lookup"><span data-stu-id="4c145-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="4c145-230">En otras palabras, devuelve 0 en todos los casos excepto cuando los bits correspondientes de los dos parámetros son 1.</span><span class="sxs-lookup"><span data-stu-id="4c145-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="4c145-231">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="4c145-232">devuelve 7 porque los valores hexadecimales "F" y "F7" se evalúan en este valor.</span><span class="sxs-lookup"><span data-stu-id="4c145-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="4c145-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="4c145-233">BitOr</span></span>
<span data-ttu-id="4c145-234">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-234">**Description:**</span></span>  
<span data-ttu-id="4c145-235">: la función BitOr establece los bits especificados en un valor.</span><span class="sxs-lookup"><span data-stu-id="4c145-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="4c145-236">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="4c145-237">value1, value2: valores numéricos que deberían estar unidos por el operador OR</span><span class="sxs-lookup"><span data-stu-id="4c145-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="4c145-238">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-238">**Remarks:**</span></span>  
<span data-ttu-id="4c145-239">: esta función convierte ambos parámetros en la representación binaria y establece un bit en 1 si uno o ambos de los bits correspondientes de la máscara y marca son 1, y en 0 si son 0.</span><span class="sxs-lookup"><span data-stu-id="4c145-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="4c145-240">En otras palabras, devuelve 1 en todos los casos excepto cuando los bits correspondientes de ambos parámetros son 0.</span><span class="sxs-lookup"><span data-stu-id="4c145-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="4c145-241">CBool</span><span class="sxs-lookup"><span data-stu-id="4c145-241">CBool</span></span>
<span data-ttu-id="4c145-242">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-242">**Description:**</span></span>  
<span data-ttu-id="4c145-243">: la función CBool devuelve un valor booleano basado en la expresión evaluada.</span><span class="sxs-lookup"><span data-stu-id="4c145-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="4c145-244">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="4c145-245">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-245">**Remarks:**</span></span>  
<span data-ttu-id="4c145-246">Si la expresión se evalúa en un valor distinto de cero, CBool devuelve True. En caso contrario, devuelve False.</span><span class="sxs-lookup"><span data-stu-id="4c145-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="4c145-247">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="4c145-248">Devuelve True si ambos atributos tienen el mismo valor.</span><span class="sxs-lookup"><span data-stu-id="4c145-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="4c145-249">CDate</span><span class="sxs-lookup"><span data-stu-id="4c145-249">CDate</span></span>
<span data-ttu-id="4c145-250">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-250">**Description:**</span></span>  
<span data-ttu-id="4c145-251">: la función CDate devuelve un valor DateTime UTC a partir de una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="4c145-252">DateTime no es un tipo de atributo nativo en Sincronización pero lo usan algunas funciones.</span><span class="sxs-lookup"><span data-stu-id="4c145-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="4c145-253">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="4c145-254">Valor: una cadena con una fecha, hora y opcionalmente, una zona horaria</span><span class="sxs-lookup"><span data-stu-id="4c145-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="4c145-255">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-255">**Remarks:**</span></span>  
<span data-ttu-id="4c145-256">: la cadena devuelta siempre es UTC.</span><span class="sxs-lookup"><span data-stu-id="4c145-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="4c145-257">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="4c145-258">devuelve un valor DateTime basado en la hora de inicio del empleado.</span><span class="sxs-lookup"><span data-stu-id="4c145-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="4c145-259">Devuelve un valor DateTime que representa "2013-01-11 12:00 AM".</span><span class="sxs-lookup"><span data-stu-id="4c145-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="4c145-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="4c145-260">CertExtensionOids</span></span>
<span data-ttu-id="4c145-261">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-261">**Description:**</span></span>  
<span data-ttu-id="4c145-262">Devuelve los valores de Oid de todas las extensiones esenciales de un objeto de certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="4c145-263">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="4c145-264">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-265">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="4c145-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="4c145-266">CertFormat</span></span>
<span data-ttu-id="4c145-267">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-267">**Description:**</span></span>  
<span data-ttu-id="4c145-268">Devuelve el nombre del formato de este certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="4c145-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="4c145-269">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="4c145-270">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-271">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="4c145-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="4c145-272">CertFriendlyName</span></span>
<span data-ttu-id="4c145-273">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-273">**Description:**</span></span>  
<span data-ttu-id="4c145-274">Devuelve el alias asociado de un certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="4c145-275">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="4c145-276">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-277">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="4c145-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="4c145-278">CertHashString</span></span>
<span data-ttu-id="4c145-279">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-279">**Description:**</span></span>  
<span data-ttu-id="4c145-280">Devuelve el valor de hash SHA1 del certificado X.509v3 en forma de una cadena hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="4c145-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="4c145-281">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="4c145-282">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-283">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="4c145-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="4c145-284">CertIssuer</span></span>
<span data-ttu-id="4c145-285">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-285">**Description:**</span></span>  
<span data-ttu-id="4c145-286">Devuelve el nombre de la entidad de certificación que emitió el certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="4c145-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="4c145-287">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="4c145-288">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-289">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="4c145-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="4c145-290">CertIssuerDN</span></span>
<span data-ttu-id="4c145-291">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-291">**Description:**</span></span>  
<span data-ttu-id="4c145-292">Devuelve el nombre distintivo del emisor del certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="4c145-293">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="4c145-294">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-295">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="4c145-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="4c145-296">CertIssuerOid</span></span>
<span data-ttu-id="4c145-297">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-297">**Description:**</span></span>  
<span data-ttu-id="4c145-298">Devuelve el Oid del emisor del certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="4c145-299">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="4c145-300">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-301">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="4c145-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="4c145-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="4c145-303">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-303">**Description:**</span></span>  
<span data-ttu-id="4c145-304">Devuelve la información del algoritmo de clave de este certificado X.509v3 como una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="4c145-305">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="4c145-306">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-307">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="4c145-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="4c145-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="4c145-309">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-309">**Description:**</span></span>  
<span data-ttu-id="4c145-310">Devuelve los parámetros del algoritmo de clave del certificado X.509v3 como una cadena hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="4c145-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="4c145-311">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="4c145-312">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-313">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="4c145-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="4c145-314">CertNameInfo</span></span>
<span data-ttu-id="4c145-315">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-315">**Description:**</span></span>  
<span data-ttu-id="4c145-316">Devuelve el asunto y el emisor de nombres de un certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="4c145-317">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="4c145-318">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-319">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="4c145-320">X509NameType: el valor X509NameType para el sujeto.</span><span class="sxs-lookup"><span data-stu-id="4c145-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="4c145-321">includesIssuerName: true para incluir el nombre del emisor; en caso contrario, false.</span><span class="sxs-lookup"><span data-stu-id="4c145-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="4c145-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="4c145-322">CertNotAfter</span></span>
<span data-ttu-id="4c145-323">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-323">**Description:**</span></span>  
<span data-ttu-id="4c145-324">Devuelve la fecha en hora local después de la cual un certificado ya no es válido.</span><span class="sxs-lookup"><span data-stu-id="4c145-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="4c145-325">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="4c145-326">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-327">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="4c145-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="4c145-328">CertNotBefore</span></span>
<span data-ttu-id="4c145-329">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-329">**Description:**</span></span>  
<span data-ttu-id="4c145-330">Devuelve la fecha en hora local después de la cual un certificado se convierte en válido.</span><span class="sxs-lookup"><span data-stu-id="4c145-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="4c145-331">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="4c145-332">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-333">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="4c145-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="4c145-334">CertPublicKeyOid</span></span>
<span data-ttu-id="4c145-335">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-335">**Description:**</span></span>  
<span data-ttu-id="4c145-336">Devuelve el Oid de la clave pública del certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="4c145-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="4c145-337">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="4c145-338">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-339">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="4c145-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="4c145-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="4c145-341">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-341">**Description:**</span></span>  
<span data-ttu-id="4c145-342">Devuelve el Oid de los parámetros de clave pública del certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="4c145-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="4c145-343">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="4c145-344">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-345">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="4c145-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="4c145-346">CertSerialNumber</span></span>
<span data-ttu-id="4c145-347">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-347">**Description:**</span></span>  
<span data-ttu-id="4c145-348">Devuelve el número de serie del certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="4c145-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="4c145-349">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="4c145-350">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-351">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="4c145-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="4c145-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="4c145-353">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-353">**Description:**</span></span>  
<span data-ttu-id="4c145-354">Devuelve el Oid del algoritmo utilizado para crear la firma de un certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="4c145-355">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="4c145-356">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-357">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="4c145-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="4c145-358">CertSubject</span></span>
<span data-ttu-id="4c145-359">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-359">**Description:**</span></span>  
<span data-ttu-id="4c145-360">Obtiene el nombre distintivo del sujeto de un certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="4c145-361">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="4c145-362">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-363">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="4c145-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="4c145-364">CertSubjectNameDN</span></span>
<span data-ttu-id="4c145-365">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-365">**Description:**</span></span>  
<span data-ttu-id="4c145-366">Devuelve el nombre distintivo del sujeto de un certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="4c145-367">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="4c145-368">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-369">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="4c145-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="4c145-370">CertSubjectNameOid</span></span>
<span data-ttu-id="4c145-371">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-371">**Description:**</span></span>  
<span data-ttu-id="4c145-372">Devuelve el Oid del nombre del sujeto de un certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="4c145-373">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="4c145-374">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-375">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="4c145-376">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="4c145-376">CertThumbprint</span></span>
<span data-ttu-id="4c145-377">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-377">**Description:**</span></span>  
<span data-ttu-id="4c145-378">Devuelve la huella digital de un certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="4c145-379">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="4c145-380">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-381">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="4c145-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="4c145-382">CertVersion</span></span>
<span data-ttu-id="4c145-383">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-383">**Description:**</span></span>  
<span data-ttu-id="4c145-384">Devuelve la versión de formato X.509 de un certificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="4c145-385">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="4c145-386">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-387">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="4c145-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="4c145-388">CGuid</span></span>
<span data-ttu-id="4c145-389">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-389">**Description:**</span></span>  
<span data-ttu-id="4c145-390">: la función CGuid convierte la representación de cadena de un GUID en su representación binaria.</span><span class="sxs-lookup"><span data-stu-id="4c145-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="4c145-391">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="4c145-392">Una cadena con un formato que sigue este patrón: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx o {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="4c145-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="4c145-393">Contains</span><span class="sxs-lookup"><span data-stu-id="4c145-393">Contains</span></span>
<span data-ttu-id="4c145-394">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-394">**Description:**</span></span>  
<span data-ttu-id="4c145-395">: la función Contains busca una cadena dentro de un atributo multivalor.</span><span class="sxs-lookup"><span data-stu-id="4c145-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="4c145-396">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-396">**Syntax:**</span></span>  
<span data-ttu-id="4c145-397">`num Contains (mvstring attribute, str search)` - distingue mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="4c145-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="4c145-398">`num Contains (mvref attribute, str search)` - distingue mayúsculas y minúsculas</span><span class="sxs-lookup"><span data-stu-id="4c145-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="4c145-399">attribute: el atributo con varios valores de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4c145-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="4c145-400">search: cadena para buscar en el atributo.</span><span class="sxs-lookup"><span data-stu-id="4c145-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="4c145-401">Casetype: CaseInsensitive o CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="4c145-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="4c145-402">Devuelve el índice en el atributo de varios valores donde se ha encontrado la cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="4c145-403">Si no se encuentra la cadena, se devuelve 0.</span><span class="sxs-lookup"><span data-stu-id="4c145-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="4c145-404">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-404">**Remarks:**</span></span>  
<span data-ttu-id="4c145-405">: para los atributos de cadena multivalor, la búsqueda encuentra subcadenas en los valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="4c145-406">Para los atributos de referencia, la cadena de búsqueda debe coincidir exactamente con el valor para que se considere una coincidencia.</span><span class="sxs-lookup"><span data-stu-id="4c145-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="4c145-407">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="4c145-408">Si el atributo proxyAddresses tiene una dirección de correo electrónico principal (indicada mediante las mayúsculas "SMTP:"), devuelve el atributo proxyAddress. De lo contrario, devuelve un error.</span><span class="sxs-lookup"><span data-stu-id="4c145-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="4c145-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="4c145-409">ConvertFromBase64</span></span>
<span data-ttu-id="4c145-410">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-410">**Description:**</span></span>  
<span data-ttu-id="4c145-411">: la función ConvertFromBase64 convierte el valor codificado en base64 especificado en una cadena normal.</span><span class="sxs-lookup"><span data-stu-id="4c145-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="4c145-412">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-412">**Syntax:**</span></span>  
<span data-ttu-id="4c145-413">`str ConvertFromBase64(str source)` da por hecho que se usará Unicode para la codificación.</span><span class="sxs-lookup"><span data-stu-id="4c145-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="4c145-414">source: cadena codificada en Base64</span><span class="sxs-lookup"><span data-stu-id="4c145-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="4c145-415">Codificación: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="4c145-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="4c145-416">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="4c145-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="4c145-417">Ambos ejemplos devuelven "*Hola a todos*"</span><span class="sxs-lookup"><span data-stu-id="4c145-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="4c145-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="4c145-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="4c145-419">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-419">**Description:**</span></span>  
<span data-ttu-id="4c145-420">: la función ConvertFromUTF8Hex convierte el valor codificado hexadecimal UTF8 especificado en una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="4c145-421">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="4c145-422">origen: cadena codificada de 2 bytes UTF8</span><span class="sxs-lookup"><span data-stu-id="4c145-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="4c145-423">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-423">**Remarks:**</span></span>  
<span data-ttu-id="4c145-424">La diferencia entre esta función y ConvertFromBase64([],UTF8) es que el resultado es descriptivo para el atributo DN.</span><span class="sxs-lookup"><span data-stu-id="4c145-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="4c145-425">Azure Active Directory utiliza este formato como DN.</span><span class="sxs-lookup"><span data-stu-id="4c145-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="4c145-426">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="4c145-427">devuelve "*Hello world!*".</span><span class="sxs-lookup"><span data-stu-id="4c145-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="4c145-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="4c145-428">ConvertToBase64</span></span>
<span data-ttu-id="4c145-429">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-429">**Description:**</span></span>  
<span data-ttu-id="4c145-430">La función ConvertToBase64 convierte una cadena en una en base64 de Unicode.</span><span class="sxs-lookup"><span data-stu-id="4c145-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="4c145-431">Convierte el valor de una matriz de enteros en su representación de cadena equivalente que se codifica con dígitos de base 64.</span><span class="sxs-lookup"><span data-stu-id="4c145-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="4c145-432">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="4c145-433">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="4c145-434">devuelve "SABlAGwAbABvACAAdwBvAHIAbABkACEA".</span><span class="sxs-lookup"><span data-stu-id="4c145-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="4c145-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="4c145-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="4c145-436">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-436">**Description:**</span></span>  
<span data-ttu-id="4c145-437">: la función ConvertToUTF8Hex convierte una cadena en un valor codificado hexadecimal UTF8.</span><span class="sxs-lookup"><span data-stu-id="4c145-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="4c145-438">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="4c145-439">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-439">**Remarks:**</span></span>  
<span data-ttu-id="4c145-440">: Azure Active Directory usa el formato de salida de esta función como formato de atributo DN.</span><span class="sxs-lookup"><span data-stu-id="4c145-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="4c145-441">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="4c145-442">devuelve 48656C6C6F20776F726C6421.</span><span class="sxs-lookup"><span data-stu-id="4c145-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="4c145-443">Recuento</span><span class="sxs-lookup"><span data-stu-id="4c145-443">Count</span></span>
<span data-ttu-id="4c145-444">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-444">**Description:**</span></span>  
<span data-ttu-id="4c145-445">: la función Count devuelve el número de elementos en un atributo multivalor.</span><span class="sxs-lookup"><span data-stu-id="4c145-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="4c145-446">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="4c145-447">CNum</span><span class="sxs-lookup"><span data-stu-id="4c145-447">CNum</span></span>
<span data-ttu-id="4c145-448">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-448">**Description:**</span></span>  
<span data-ttu-id="4c145-449">: la función CNum toma una cadena y devuelve un tipo de datos numérico.</span><span class="sxs-lookup"><span data-stu-id="4c145-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="4c145-450">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="4c145-451">CRef</span><span class="sxs-lookup"><span data-stu-id="4c145-451">CRef</span></span>
<span data-ttu-id="4c145-452">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-452">**Description:**</span></span>  
<span data-ttu-id="4c145-453">: convierte una cadena en un atributo de referencia.</span><span class="sxs-lookup"><span data-stu-id="4c145-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="4c145-454">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="4c145-455">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="4c145-456">CStr</span><span class="sxs-lookup"><span data-stu-id="4c145-456">CStr</span></span>
<span data-ttu-id="4c145-457">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-457">**Description:**</span></span>  
<span data-ttu-id="4c145-458">: la función CStr se convierte en un tipo de datos de cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="4c145-459">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="4c145-460">value: puede ser un valor numérico, un atributo de referencia o un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="4c145-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="4c145-461">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="4c145-462">podría devolver "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="4c145-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="4c145-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="4c145-463">DateAdd</span></span>
<span data-ttu-id="4c145-464">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-464">**Description:**</span></span>  
<span data-ttu-id="4c145-465">: devuelve un valor Date que contiene una fecha a la que se ha agregado un intervalo de tiempo especificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="4c145-466">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="4c145-467">interval: expresión de cadena que es el intervalo de tiempo que desea agregar.</span><span class="sxs-lookup"><span data-stu-id="4c145-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="4c145-468">La cadena debe tener uno de los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="4c145-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="4c145-469">yyyy Año</span><span class="sxs-lookup"><span data-stu-id="4c145-469">yyyy Year</span></span>
  * <span data-ttu-id="4c145-470">q Trimestre</span><span class="sxs-lookup"><span data-stu-id="4c145-470">q Quarter</span></span>
  * <span data-ttu-id="4c145-471">m Mes</span><span class="sxs-lookup"><span data-stu-id="4c145-471">m Month</span></span>
  * <span data-ttu-id="4c145-472">y Día del año</span><span class="sxs-lookup"><span data-stu-id="4c145-472">y Day of year</span></span>
  * <span data-ttu-id="4c145-473">d Día</span><span class="sxs-lookup"><span data-stu-id="4c145-473">d Day</span></span>
  * <span data-ttu-id="4c145-474">w Día de la semana</span><span class="sxs-lookup"><span data-stu-id="4c145-474">w Weekday</span></span>
  * <span data-ttu-id="4c145-475">ww Semana</span><span class="sxs-lookup"><span data-stu-id="4c145-475">ww Week</span></span>
  * <span data-ttu-id="4c145-476">h Hora</span><span class="sxs-lookup"><span data-stu-id="4c145-476">h Hour</span></span>
  * <span data-ttu-id="4c145-477">n Minuto</span><span class="sxs-lookup"><span data-stu-id="4c145-477">n Minute</span></span>
  * <span data-ttu-id="4c145-478">s Segundo</span><span class="sxs-lookup"><span data-stu-id="4c145-478">s Second</span></span>
* <span data-ttu-id="4c145-479">value: el número de unidades que desea agregar.</span><span class="sxs-lookup"><span data-stu-id="4c145-479">value: The number of units you want to add.</span></span> <span data-ttu-id="4c145-480">Puede ser positivo (para obtener fechas futuras) o negativo (para obtener fechas del pasado).</span><span class="sxs-lookup"><span data-stu-id="4c145-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="4c145-481">date: DateTime que representa la fecha a la que se agrega el intervalo.</span><span class="sxs-lookup"><span data-stu-id="4c145-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="4c145-482">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="4c145-483">agrega 3 meses y devuelve un valor DateTime que representa "2001-04-01".</span><span class="sxs-lookup"><span data-stu-id="4c145-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="4c145-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="4c145-484">DateFromNum</span></span>
<span data-ttu-id="4c145-485">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-485">**Description:**</span></span>  
<span data-ttu-id="4c145-486">: la función DateFromNum convierte un valor con formato de fecha de AD en un tipo DateTime.</span><span class="sxs-lookup"><span data-stu-id="4c145-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="4c145-487">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="4c145-488">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="4c145-489">devuelve un valor DateTime que representa 2012-01-01 23:00:00.</span><span class="sxs-lookup"><span data-stu-id="4c145-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="4c145-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="4c145-490">DNComponent</span></span>
<span data-ttu-id="4c145-491">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-491">**Description:**</span></span>  
<span data-ttu-id="4c145-492">: la función DNComponent devuelve el valor de un componente DN especificado empezando por la izquierda.</span><span class="sxs-lookup"><span data-stu-id="4c145-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="4c145-493">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="4c145-494">dn: el atributo de referencia que interpretar</span><span class="sxs-lookup"><span data-stu-id="4c145-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="4c145-495">ComponentNumber: el componente en DN que devolver</span><span class="sxs-lookup"><span data-stu-id="4c145-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="4c145-496">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="4c145-497">si dn es "cn=Joe,ou=…", devuelve Joe.</span><span class="sxs-lookup"><span data-stu-id="4c145-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="4c145-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="4c145-498">DNComponentRev</span></span>
<span data-ttu-id="4c145-499">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-499">**Description:**</span></span>  
<span data-ttu-id="4c145-500">: la función DNComponentRev devuelve el valor de un componente DN especificado empezando por la derecha (final).</span><span class="sxs-lookup"><span data-stu-id="4c145-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="4c145-501">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="4c145-502">dn: el atributo de referencia que interpretar</span><span class="sxs-lookup"><span data-stu-id="4c145-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="4c145-503">ComponentNumber: el componente en DN que devolver</span><span class="sxs-lookup"><span data-stu-id="4c145-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="4c145-504">Opciones: DC, ignora todos los componentes con “dc=”</span><span class="sxs-lookup"><span data-stu-id="4c145-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="4c145-505">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-505">**Example:**</span></span>  
<span data-ttu-id="4c145-506">Si dn es "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="4c145-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="4c145-507">Ambos devuelven US.</span><span class="sxs-lookup"><span data-stu-id="4c145-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="4c145-508">Error</span><span class="sxs-lookup"><span data-stu-id="4c145-508">Error</span></span>
<span data-ttu-id="4c145-509">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-509">**Description:**</span></span>  
<span data-ttu-id="4c145-510">: la función Error se usa para devolver un error personalizado.</span><span class="sxs-lookup"><span data-stu-id="4c145-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="4c145-511">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="4c145-512">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="4c145-513">si el atributo accountName no está presente, se produce un error en el objeto.</span><span class="sxs-lookup"><span data-stu-id="4c145-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="4c145-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="4c145-514">EscapeDNComponent</span></span>
<span data-ttu-id="4c145-515">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-515">**Description:**</span></span>  
<span data-ttu-id="4c145-516">: la función EscapeDNComponent toma un componente de DN y genera secuencias de escape para poder representarlo en LDAP.</span><span class="sxs-lookup"><span data-stu-id="4c145-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="4c145-517">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="4c145-518">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="4c145-519">se asegura de que el objeto se puede crear en un directorio LDAP incluso si el atributo displayName tiene caracteres para los que deben generarse secuencias de escape en LDAP.</span><span class="sxs-lookup"><span data-stu-id="4c145-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="4c145-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="4c145-520">FormatDateTime</span></span>
<span data-ttu-id="4c145-521">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-521">**Description:**</span></span>  
<span data-ttu-id="4c145-522">: la función FormatDateTime se usa para dar formato a un valor DateTime en una cadena con un formato especificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="4c145-523">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="4c145-524">value: un valor con el formato DateTime</span><span class="sxs-lookup"><span data-stu-id="4c145-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="4c145-525">format: una cadena que representa el formato de conversión.</span><span class="sxs-lookup"><span data-stu-id="4c145-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="4c145-526">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-526">**Remarks:**</span></span>  
<span data-ttu-id="4c145-527">Se pueden encontrar aquí los valores posibles para el formato: [Formatos de fecha y hora definidos por el usuario (función Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="4c145-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="4c145-528">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="4c145-529">Genera "2007-12-25".</span><span class="sxs-lookup"><span data-stu-id="4c145-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="4c145-530">Puede generar "20140905081453.0Z".</span><span class="sxs-lookup"><span data-stu-id="4c145-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="4c145-531">GUID</span><span class="sxs-lookup"><span data-stu-id="4c145-531">GUID</span></span>
<span data-ttu-id="4c145-532">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-532">**Description:**</span></span>  
<span data-ttu-id="4c145-533">: la función GUID genera un nuevo GUID aleatorio.</span><span class="sxs-lookup"><span data-stu-id="4c145-533">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="4c145-534">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="4c145-535">IIF</span><span class="sxs-lookup"><span data-stu-id="4c145-535">IIF</span></span>
<span data-ttu-id="4c145-536">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-536">**Description:**</span></span>  
<span data-ttu-id="4c145-537">: la función IIF devuelve uno de un conjunto de valores posibles según una condición especificada.</span><span class="sxs-lookup"><span data-stu-id="4c145-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="4c145-538">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="4c145-539">condition: cualquier valor o expresión que pueda evaluarse en True o False.</span><span class="sxs-lookup"><span data-stu-id="4c145-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="4c145-540">valueIfTrue: si la condición se evalúa como true, el valor devuelto.</span><span class="sxs-lookup"><span data-stu-id="4c145-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="4c145-541">valueIfTrue: si la condición se evalúa como false, el valor devuelto.</span><span class="sxs-lookup"><span data-stu-id="4c145-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="4c145-542">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="4c145-543">Si el usuario está en prácticas, devuelve el alias de un usuario al que agrega "t-" al principio. De lo contrario, el alias del usuario se queda como está.</span><span class="sxs-lookup"><span data-stu-id="4c145-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="4c145-544">InStr</span><span class="sxs-lookup"><span data-stu-id="4c145-544">InStr</span></span>
<span data-ttu-id="4c145-545">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-545">**Description:**</span></span>  
<span data-ttu-id="4c145-546">: la función InStr busca la primera repetición de una subcadena en una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="4c145-547">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="4c145-548">stringcheck: cadena que se va a buscar</span><span class="sxs-lookup"><span data-stu-id="4c145-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="4c145-549">stringmatch: cadena que se tiene que encontrar</span><span class="sxs-lookup"><span data-stu-id="4c145-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="4c145-550">start: posición de inicio para encontrar la subcadena</span><span class="sxs-lookup"><span data-stu-id="4c145-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="4c145-551">compare: vbTextCompare o vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="4c145-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="4c145-552">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-552">**Remarks:**</span></span>  
<span data-ttu-id="4c145-553">: devuelve la posición en la que se encontró la subcadena o 0 si no se encuentra.</span><span class="sxs-lookup"><span data-stu-id="4c145-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="4c145-554">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="4c145-555">se evalúa en 5.</span><span class="sxs-lookup"><span data-stu-id="4c145-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="4c145-556">Se evalúa en 7.</span><span class="sxs-lookup"><span data-stu-id="4c145-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="4c145-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="4c145-557">InStrRev</span></span>
<span data-ttu-id="4c145-558">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-558">**Description:**</span></span>  
<span data-ttu-id="4c145-559">: la función InStrRev busca la última repetición de una subcadena en una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="4c145-560">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="4c145-561">stringcheck: cadena que se va a buscar</span><span class="sxs-lookup"><span data-stu-id="4c145-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="4c145-562">stringmatch: cadena que se tiene que encontrar</span><span class="sxs-lookup"><span data-stu-id="4c145-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="4c145-563">start: posición de inicio para encontrar la subcadena</span><span class="sxs-lookup"><span data-stu-id="4c145-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="4c145-564">compare: vbTextCompare o vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="4c145-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="4c145-565">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-565">**Remarks:**</span></span>  
<span data-ttu-id="4c145-566">: devuelve la posición en la que se encontró la subcadena o 0 si no se encuentra.</span><span class="sxs-lookup"><span data-stu-id="4c145-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="4c145-567">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="4c145-568">devuelve 7.</span><span class="sxs-lookup"><span data-stu-id="4c145-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="4c145-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="4c145-569">IsBitSet</span></span>
<span data-ttu-id="4c145-570">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-570">**Description:**</span></span>  
<span data-ttu-id="4c145-571">la función IsBitSet prueba si un bit se establece o no.</span><span class="sxs-lookup"><span data-stu-id="4c145-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="4c145-572">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="4c145-573">value: un valor numérico que es evaluated.flag: un valor numérico que tiene el bit que se va a evaluar</span><span class="sxs-lookup"><span data-stu-id="4c145-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="4c145-574">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="4c145-575">devuelve True porque el bit "4" se establece en el valor hexadecimal "F".</span><span class="sxs-lookup"><span data-stu-id="4c145-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="4c145-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="4c145-576">IsDate</span></span>
<span data-ttu-id="4c145-577">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-577">**Description:**</span></span>  
<span data-ttu-id="4c145-578">si la expresión se puede evaluar como un tipo DateTime, la función IsDate se evalúa en True.</span><span class="sxs-lookup"><span data-stu-id="4c145-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="4c145-579">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="4c145-580">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-580">**Remarks:**</span></span>  
<span data-ttu-id="4c145-581">se usa para determinar si CDate() será correcto.</span><span class="sxs-lookup"><span data-stu-id="4c145-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="4c145-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="4c145-582">IsCert</span></span>
<span data-ttu-id="4c145-583">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-583">**Description:**</span></span>  
<span data-ttu-id="4c145-584">Devuelve true si los datos sin procesar se pueden serializar en el objeto de certificado X509Certificate2. NET.</span><span class="sxs-lookup"><span data-stu-id="4c145-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="4c145-585">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="4c145-586">certificateRawData: representación de matriz de bytes de un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="4c145-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="4c145-587">La matriz de bytes puede ser de datos X.509 codificados en Base64 o codificados en binario (DER).</span><span class="sxs-lookup"><span data-stu-id="4c145-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="4c145-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="4c145-588">IsEmpty</span></span>
<span data-ttu-id="4c145-589">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-589">**Description:**</span></span>  
<span data-ttu-id="4c145-590">si el atributo está presente en CS o MV, pero se evalúa en una cadena vacía, la función IsEmpty se evalúa en True.</span><span class="sxs-lookup"><span data-stu-id="4c145-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="4c145-591">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="4c145-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="4c145-592">IsGuid</span></span>
<span data-ttu-id="4c145-593">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-593">**Description:**</span></span>  
<span data-ttu-id="4c145-594">si la cadena se pudo convertir en un GUID, la función IsGuid evaluada en True.</span><span class="sxs-lookup"><span data-stu-id="4c145-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="4c145-595">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="4c145-596">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-596">**Remarks:**</span></span>  
<span data-ttu-id="4c145-597">un GUID se define como una cadena que sigue uno de estos patrones: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}.</span><span class="sxs-lookup"><span data-stu-id="4c145-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="4c145-598">Se usa para determinar si CGuid() es correcto.</span><span class="sxs-lookup"><span data-stu-id="4c145-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="4c145-599">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="4c145-600">Si StrAttribute tiene un formato GUID, devuelve una representación binaria. De lo contrario, devuelve un valor Null.</span><span class="sxs-lookup"><span data-stu-id="4c145-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="4c145-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="4c145-601">IsNull</span></span>
<span data-ttu-id="4c145-602">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-602">**Description:**</span></span>  
<span data-ttu-id="4c145-603">si la expresión se evalúa como Null, la función IsNull devuelve True.</span><span class="sxs-lookup"><span data-stu-id="4c145-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="4c145-604">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="4c145-605">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-605">**Remarks:**</span></span>  
<span data-ttu-id="4c145-606">para un atributo, un valor Null se expresa mediante la ausencia del atributo.</span><span class="sxs-lookup"><span data-stu-id="4c145-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="4c145-607">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="4c145-608">devuelve True si el atributo no está presente en CS o MV.</span><span class="sxs-lookup"><span data-stu-id="4c145-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="4c145-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="4c145-609">IsNullOrEmpty</span></span>
<span data-ttu-id="4c145-610">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-610">**Description:**</span></span>  
<span data-ttu-id="4c145-611">si la expresión es Null o una cadena vacía, la función IsNullOrEmpty devuelve True.</span><span class="sxs-lookup"><span data-stu-id="4c145-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="4c145-612">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="4c145-613">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-613">**Remarks:**</span></span>  
<span data-ttu-id="4c145-614">para un atributo, esto se evaluaría como True si el atributo no está presente o está presente, pero es una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="4c145-615">La función contraria a esta es IsPresent.</span><span class="sxs-lookup"><span data-stu-id="4c145-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="4c145-616">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="4c145-617">devuelve True si el atributo no está presente o si es una cadena vacía en CS o MV.</span><span class="sxs-lookup"><span data-stu-id="4c145-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="4c145-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="4c145-618">IsNumeric</span></span>
<span data-ttu-id="4c145-619">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-619">**Description:**</span></span>  
<span data-ttu-id="4c145-620">la función IsNumeric devuelve un valor booleano que indica si una expresión se puede evaluar como un tipo de número.</span><span class="sxs-lookup"><span data-stu-id="4c145-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="4c145-621">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="4c145-622">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-622">**Remarks:**</span></span>  
<span data-ttu-id="4c145-623">se usa para determinar si CNum() analizará correctamente la expresión.</span><span class="sxs-lookup"><span data-stu-id="4c145-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="4c145-624">IsString</span><span class="sxs-lookup"><span data-stu-id="4c145-624">IsString</span></span>
<span data-ttu-id="4c145-625">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-625">**Description:**</span></span>  
<span data-ttu-id="4c145-626">si la expresión se puede evaluar en un tipo de cadena, la función IsString se evalúa en True.</span><span class="sxs-lookup"><span data-stu-id="4c145-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="4c145-627">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="4c145-628">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-628">**Remarks:**</span></span>  
<span data-ttu-id="4c145-629">se usa para determinar si CStr() puede analizar correctamente la expresión.</span><span class="sxs-lookup"><span data-stu-id="4c145-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="4c145-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="4c145-630">IsPresent</span></span>
<span data-ttu-id="4c145-631">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-631">**Description:**</span></span>  
<span data-ttu-id="4c145-632">si la expresión se evalúa como una cadena que no es Null y no está vacía, la función IsPresent devuelve True.</span><span class="sxs-lookup"><span data-stu-id="4c145-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="4c145-633">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="4c145-634">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-634">**Remarks:**</span></span>  
<span data-ttu-id="4c145-635">la función contraria a esta es IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="4c145-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="4c145-636">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="4c145-637">Elemento</span><span class="sxs-lookup"><span data-stu-id="4c145-637">Item</span></span>
<span data-ttu-id="4c145-638">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-638">**Description:**</span></span>  
<span data-ttu-id="4c145-639">la función Item devuelve un elemento de un atributo o una cadena de varios valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="4c145-640">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="4c145-641">attribute: atributo de varios valores</span><span class="sxs-lookup"><span data-stu-id="4c145-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="4c145-642">index: índice para un elemento en la cadena de varios valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="4c145-643">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-643">**Remarks:**</span></span>  
<span data-ttu-id="4c145-644">la función Item es útil con la función Contains puesto que esta última función devuelve el índice a un elemento en el atributo de varios valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="4c145-645">Se produce un error si el índice está fuera de los límites.</span><span class="sxs-lookup"><span data-stu-id="4c145-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="4c145-646">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="4c145-647">devuelve la dirección de correo electrónico principal.</span><span class="sxs-lookup"><span data-stu-id="4c145-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="4c145-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="4c145-648">ItemOrNull</span></span>
<span data-ttu-id="4c145-649">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-649">**Description:**</span></span>  
<span data-ttu-id="4c145-650">la función ItemOrNull devuelve un elemento de un atributo o una cadena de varios valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="4c145-651">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="4c145-652">attribute: atributo de varios valores</span><span class="sxs-lookup"><span data-stu-id="4c145-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="4c145-653">index: índice para un elemento en la cadena de varios valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="4c145-654">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-654">**Remarks:**</span></span>  
<span data-ttu-id="4c145-655">la función ItemOrNull es útil con la función Contains puesto que esta última función devuelve el índice a un elemento en el atributo de varios valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="4c145-656">Si el índice está fuera de los límites, devuelve un valor Null.</span><span class="sxs-lookup"><span data-stu-id="4c145-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="4c145-657">Join</span><span class="sxs-lookup"><span data-stu-id="4c145-657">Join</span></span>
<span data-ttu-id="4c145-658">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-658">**Description:**</span></span>  
<span data-ttu-id="4c145-659">la función Join toma una cadena de varios valores y devuelve una cadena de valor único con un separador especificado insertado entre cada elemento.</span><span class="sxs-lookup"><span data-stu-id="4c145-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="4c145-660">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="4c145-661">attribute: atributo de varios valores que contiene cadenas para combinar.</span><span class="sxs-lookup"><span data-stu-id="4c145-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="4c145-662">delimiter: cualquier cadena utilizada para separar las subcadenas en la cadena devuelta.</span><span class="sxs-lookup"><span data-stu-id="4c145-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="4c145-663">Si se omite, se usa el carácter de espacio ("").</span><span class="sxs-lookup"><span data-stu-id="4c145-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="4c145-664">Si delimitador es una cadena de longitud cero ("") o nada, todos los elementos de la lista se concatenan sin delimitadores.</span><span class="sxs-lookup"><span data-stu-id="4c145-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="4c145-665">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-665">**Remarks**</span></span>  
<span data-ttu-id="4c145-666">hay paridad entre las funciones Join y Split.</span><span class="sxs-lookup"><span data-stu-id="4c145-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="4c145-667">La función Join toma una matriz de cadenas y las combina con una cadena de delimitación para devolver una sola cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="4c145-668">La función Split toma una cadena y la separa en el delimitador para devolver una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="4c145-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="4c145-669">Sin embargo, una diferencia clave es que Join puede concatenar cadenas con cualquier cadena de delimitación, mientras que attribute puede separar solo cadenas mediante un delimitador de carácter único.</span><span class="sxs-lookup"><span data-stu-id="4c145-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="4c145-670">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="4c145-671">Podría devolver: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="4c145-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="4c145-672">LCase</span><span class="sxs-lookup"><span data-stu-id="4c145-672">LCase</span></span>
<span data-ttu-id="4c145-673">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-673">**Description:**</span></span>  
<span data-ttu-id="4c145-674">la función LCase convierte todos los caracteres de una cadena a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="4c145-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="4c145-675">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="4c145-676">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="4c145-677">devuelve "test".</span><span class="sxs-lookup"><span data-stu-id="4c145-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="4c145-678">Left</span><span class="sxs-lookup"><span data-stu-id="4c145-678">Left</span></span>
<span data-ttu-id="4c145-679">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-679">**Description:**</span></span>  
<span data-ttu-id="4c145-680">la función Left devuelve un número especificado de caracteres desde la izquierda de una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="4c145-681">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="4c145-682">string: la cadena desde la que devolver los caracteres</span><span class="sxs-lookup"><span data-stu-id="4c145-682">string: the string to return characters from</span></span>
* <span data-ttu-id="4c145-683">NumChars: un número que identifica el número de caracteres que devolver desde el principio (izquierdo) de la cadena</span><span class="sxs-lookup"><span data-stu-id="4c145-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="4c145-684">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-684">**Remarks:**</span></span>  
<span data-ttu-id="4c145-685">una cadena que contiene los primeros caracteres numChars de la cadena:</span><span class="sxs-lookup"><span data-stu-id="4c145-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="4c145-686">Con numChars = 0, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="4c145-687">Con numChars < 0, se devuelve una cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="4c145-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="4c145-688">Si la cadena es null, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-688">If string is null, return empty string.</span></span>

<span data-ttu-id="4c145-689">Si la cadena contiene menos caracteres que el número especificado en numChars, se devuelve una cadena idéntica a la cadena (es decir, que contiene todos los caracteres en el parámetro 1).</span><span class="sxs-lookup"><span data-stu-id="4c145-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="4c145-690">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="4c145-691">devuelve “Joh”.</span><span class="sxs-lookup"><span data-stu-id="4c145-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="4c145-692">Len</span><span class="sxs-lookup"><span data-stu-id="4c145-692">Len</span></span>
<span data-ttu-id="4c145-693">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-693">**Description:**</span></span>  
<span data-ttu-id="4c145-694">la función Len devuelve un número de caracteres de una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="4c145-695">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="4c145-696">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="4c145-697">devuelve 8.</span><span class="sxs-lookup"><span data-stu-id="4c145-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="4c145-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="4c145-698">LTrim</span></span>
<span data-ttu-id="4c145-699">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-699">**Description:**</span></span>  
<span data-ttu-id="4c145-700">la función LTrim quita los espacios en blanco del principio de una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="4c145-701">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="4c145-702">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="4c145-703">devuelve "Test".</span><span class="sxs-lookup"><span data-stu-id="4c145-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="4c145-704">Mid</span><span class="sxs-lookup"><span data-stu-id="4c145-704">Mid</span></span>
<span data-ttu-id="4c145-705">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-705">**Description:**</span></span>  
<span data-ttu-id="4c145-706">la función Mid devuelve un número especificado de caracteres desde una posición especificada en una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="4c145-707">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="4c145-708">string: la cadena desde la que devolver los caracteres</span><span class="sxs-lookup"><span data-stu-id="4c145-708">string: the string to return characters from</span></span>
* <span data-ttu-id="4c145-709">start: un número que identifica la posición de inicio en una cadena desde la que devolver los caracteres</span><span class="sxs-lookup"><span data-stu-id="4c145-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="4c145-710">NumChars: un número que identifica el número de caracteres que devolver desde la posición en una cadena</span><span class="sxs-lookup"><span data-stu-id="4c145-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="4c145-711">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-711">**Remarks:**</span></span>  
<span data-ttu-id="4c145-712">devuelve caracteres numChars que comienzan por la posición de inicio en una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="4c145-713">Una cadena que contiene caracteres numChars de la posición de inicio en una cadena:</span><span class="sxs-lookup"><span data-stu-id="4c145-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="4c145-714">Con numChars = 0, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="4c145-715">Con numChars < 0, se devuelve una cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="4c145-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="4c145-716">Con start >,  la longitud de la cadena devuelve la cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="4c145-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="4c145-717">Con start <= 0, se devuelve la cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="4c145-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="4c145-718">Si la cadena es null, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-718">If string is null, return empty string.</span></span>

<span data-ttu-id="4c145-719">Si no hay caracteres numChar restantes en la cadena de la posición de inicio, se devuelve el máximo de caracteres posible.</span><span class="sxs-lookup"><span data-stu-id="4c145-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="4c145-720">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="4c145-721">devuelve “hn Do”.</span><span class="sxs-lookup"><span data-stu-id="4c145-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="4c145-722">Devuelve "Doe".</span><span class="sxs-lookup"><span data-stu-id="4c145-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="4c145-723">Now</span><span class="sxs-lookup"><span data-stu-id="4c145-723">Now</span></span>
<span data-ttu-id="4c145-724">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-724">**Description:**</span></span>  
<span data-ttu-id="4c145-725">la función Now devuelve DateTime que especifica la fecha y hora actuales, según la fecha y hora del sistema del equipo.</span><span class="sxs-lookup"><span data-stu-id="4c145-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="4c145-726">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="4c145-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="4c145-727">NumFromDate</span></span>
<span data-ttu-id="4c145-728">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-728">**Description:**</span></span>  
<span data-ttu-id="4c145-729">la función NumFromDate devuelve una fecha en formato de fecha de AD.</span><span class="sxs-lookup"><span data-stu-id="4c145-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="4c145-730">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="4c145-731">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="4c145-732">devuelve 129699324000000000.</span><span class="sxs-lookup"><span data-stu-id="4c145-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="4c145-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="4c145-733">PadLeft</span></span>
<span data-ttu-id="4c145-734">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-734">**Description:**</span></span>  
<span data-ttu-id="4c145-735">la función PadLeft rellena en la parte izquierda una cadena con una longitud especificada mediante un carácter de espaciado interno proporcionado.</span><span class="sxs-lookup"><span data-stu-id="4c145-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="4c145-736">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="4c145-737">string: la cadena que rellenar.</span><span class="sxs-lookup"><span data-stu-id="4c145-737">string: the string to pad.</span></span>
* <span data-ttu-id="4c145-738">length: un número entero que representa la longitud deseada de la cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="4c145-739">padCharacter: una cadena que consta de un solo carácter que se usará como el carácter controlador</span><span class="sxs-lookup"><span data-stu-id="4c145-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="4c145-740">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-740">**Remarks:**</span></span>

* <span data-ttu-id="4c145-741">Si la longitud de cadena es inferior a la longitud, padCharacter se anexa repetidamente  al principio (izquierda) de la cadena hasta que tenga una longitud igual a la longitud.</span><span class="sxs-lookup"><span data-stu-id="4c145-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="4c145-742">PadCharacter puede ser un carácter de espacio, pero no puede ser un valor Null.</span><span class="sxs-lookup"><span data-stu-id="4c145-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="4c145-743">Si la longitud de cadena es igual o mayor que la longitud, la cadena se devuelve sin cambios.</span><span class="sxs-lookup"><span data-stu-id="4c145-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="4c145-744">Si la cadena tiene una longitud mayor que o igual que la longitud, se devuelve una cadena idéntica a la cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="4c145-745">Si la longitud de cadena es menor que la longitud, se devuelve una cadena nueva de la longitud deseada que contiene una cadena rellenada con un padCharacter.</span><span class="sxs-lookup"><span data-stu-id="4c145-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="4c145-746">Si la cadena es Null, la función devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="4c145-747">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="4c145-748">devuelve "000000User".</span><span class="sxs-lookup"><span data-stu-id="4c145-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="4c145-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="4c145-749">PadRight</span></span>
<span data-ttu-id="4c145-750">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-750">**Description:**</span></span>  
<span data-ttu-id="4c145-751">la función PadRight rellena en la parte derecha una cadena con una longitud especificada mediante un carácter de espaciado interno proporcionado.</span><span class="sxs-lookup"><span data-stu-id="4c145-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="4c145-752">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="4c145-753">string: la cadena que rellenar.</span><span class="sxs-lookup"><span data-stu-id="4c145-753">string: the string to pad.</span></span>
* <span data-ttu-id="4c145-754">length: un número entero que representa la longitud deseada de la cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="4c145-755">padCharacter: una cadena que consta de un solo carácter que se usará como el carácter controlador</span><span class="sxs-lookup"><span data-stu-id="4c145-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="4c145-756">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-756">**Remarks:**</span></span>

* <span data-ttu-id="4c145-757">Si la longitud de cadena es inferior a la longitud, padCharacter se anexa repetidamente  al final (derecha) de la cadena hasta que tenga una longitud igual a la longitud.</span><span class="sxs-lookup"><span data-stu-id="4c145-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="4c145-758">PadCharacter puede ser un carácter de espacio, pero no puede ser un valor Null.</span><span class="sxs-lookup"><span data-stu-id="4c145-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="4c145-759">Si la longitud de cadena es igual o mayor que la longitud, la cadena se devuelve sin cambios.</span><span class="sxs-lookup"><span data-stu-id="4c145-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="4c145-760">Si la cadena tiene una longitud mayor que o igual que la longitud, se devuelve una cadena idéntica a la cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="4c145-761">Si la longitud de cadena es menor que la longitud, se devuelve una cadena nueva de la longitud deseada que contiene una cadena rellenada con un padCharacter.</span><span class="sxs-lookup"><span data-stu-id="4c145-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="4c145-762">Si la cadena es Null, la función devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="4c145-763">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="4c145-764">devuelve "User000000".</span><span class="sxs-lookup"><span data-stu-id="4c145-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="4c145-765">PCase</span><span class="sxs-lookup"><span data-stu-id="4c145-765">PCase</span></span>
<span data-ttu-id="4c145-766">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-766">**Description:**</span></span>  
<span data-ttu-id="4c145-767">la función PCase convierte el primer carácter de cada palabra delimitada por espacios de una cadena a mayúsculas, y todos los demás caracteres se convierten a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="4c145-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="4c145-768">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="4c145-769">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-769">**Remarks:**</span></span>

* <span data-ttu-id="4c145-770">Esta función no proporciona por el momento un uso de mayúsculas correcto para convertir una palabra que esté completamente en mayúsculas, como un acrónimo.</span><span class="sxs-lookup"><span data-stu-id="4c145-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="4c145-771">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="4c145-772">devuelve "test".</span><span class="sxs-lookup"><span data-stu-id="4c145-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="4c145-773">devuelve "Test".</span><span class="sxs-lookup"><span data-stu-id="4c145-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="4c145-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="4c145-774">RandomNum</span></span>
<span data-ttu-id="4c145-775">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-775">**Description:**</span></span>  
<span data-ttu-id="4c145-776">la función RandomNum devuelve un número aleatorio entre un intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="4c145-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="4c145-777">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="4c145-778">start: un número que identifica el límite inferior del valor aleatorio que se va a generar</span><span class="sxs-lookup"><span data-stu-id="4c145-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="4c145-779">end: un número que identifica el límite superior del valor aleatorio que generar</span><span class="sxs-lookup"><span data-stu-id="4c145-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="4c145-780">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="4c145-781">puede devolver 734.</span><span class="sxs-lookup"><span data-stu-id="4c145-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="4c145-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="4c145-782">RemoveDuplicates</span></span>
<span data-ttu-id="4c145-783">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-783">**Description:**</span></span>  
<span data-ttu-id="4c145-784">la función RemoveDuplicates toma una cadena multivalor y garantiza que cada valor es único.</span><span class="sxs-lookup"><span data-stu-id="4c145-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="4c145-785">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="4c145-786">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="4c145-787">devuelve un atributo proxyAddress saneado donde se han quitado todos los valores duplicados.</span><span class="sxs-lookup"><span data-stu-id="4c145-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="4c145-788">Sustituya</span><span class="sxs-lookup"><span data-stu-id="4c145-788">Replace</span></span>
<span data-ttu-id="4c145-789">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-789">**Description:**</span></span>  
<span data-ttu-id="4c145-790">la función Replace reemplaza todas las apariciones de una cadena por otra cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="4c145-791">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="4c145-792">string: una cadena en la que se reemplazarán los valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="4c145-793">OldValue: la cadena que se va a buscar y reemplazar.</span><span class="sxs-lookup"><span data-stu-id="4c145-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="4c145-794">NewValue: la cadena que reemplazar.</span><span class="sxs-lookup"><span data-stu-id="4c145-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="4c145-795">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-795">**Remarks:**</span></span>  
<span data-ttu-id="4c145-796">la función reconoce los siguientes monikers especiales:</span><span class="sxs-lookup"><span data-stu-id="4c145-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="4c145-797">\n: nueva línea</span><span class="sxs-lookup"><span data-stu-id="4c145-797">\n – New Line</span></span>
* <span data-ttu-id="4c145-798">\r: retorno de carro</span><span class="sxs-lookup"><span data-stu-id="4c145-798">\r – Carriage Return</span></span>
* <span data-ttu-id="4c145-799">\t: tabulación</span><span class="sxs-lookup"><span data-stu-id="4c145-799">\t – Tab</span></span>

<span data-ttu-id="4c145-800">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="4c145-801">reemplaza CRLF por una coma y un espacio, y podría originar "One Microsoft Way, Redmond, WA, USA".</span><span class="sxs-lookup"><span data-stu-id="4c145-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="4c145-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="4c145-802">ReplaceChars</span></span>
<span data-ttu-id="4c145-803">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-803">**Description:**</span></span>  
<span data-ttu-id="4c145-804">la función ReplaceChars reemplaza todas las apariciones de caracteres encontrados en la cadena ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="4c145-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="4c145-805">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="4c145-806">string: una cadena por la que reemplazar los caracteres.</span><span class="sxs-lookup"><span data-stu-id="4c145-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="4c145-807">ReplacePattern: una cadena que contiene un diccionario con caracteres que reemplazar.</span><span class="sxs-lookup"><span data-stu-id="4c145-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="4c145-808">El formato es {source1}:{target1},{source2}:{target2},{sourceN},{targetN} donde source es el carácter que buscar y target la cadena por la que reemplazar.</span><span class="sxs-lookup"><span data-stu-id="4c145-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="4c145-809">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-809">**Remarks:**</span></span>

* <span data-ttu-id="4c145-810">La función toma cada aparición de los orígenes definidos y los reemplaza por los destinos.</span><span class="sxs-lookup"><span data-stu-id="4c145-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="4c145-811">El origen debe ser exactamente un carácter (unicode).</span><span class="sxs-lookup"><span data-stu-id="4c145-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="4c145-812">El origen no puede estar vacío ni puede tener más de un carácter (error de análisis).</span><span class="sxs-lookup"><span data-stu-id="4c145-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="4c145-813">El destino puede tener varios caracteres, por ejemplo, ö:oe, β:ss.</span><span class="sxs-lookup"><span data-stu-id="4c145-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="4c145-814">El destino puede estar vacío, lo que indica que el carácter debe quitarse.</span><span class="sxs-lookup"><span data-stu-id="4c145-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="4c145-815">El origen distingue mayúsculas y minúsculas, y debe ser una coincidencia exacta.</span><span class="sxs-lookup"><span data-stu-id="4c145-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="4c145-816">La coma (,) y los dos puntos (:) son caracteres reservados y no se puede reemplazar utilizando esta función.</span><span class="sxs-lookup"><span data-stu-id="4c145-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="4c145-817">Se omiten los espacios y otros caracteres en blanco en la cadena ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="4c145-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="4c145-818">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="4c145-819">Devuelve Raksmorgas.</span><span class="sxs-lookup"><span data-stu-id="4c145-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="4c145-820">Devuelve "ONeil"; se define la marca única para quitarla.</span><span class="sxs-lookup"><span data-stu-id="4c145-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="4c145-821">Right</span><span class="sxs-lookup"><span data-stu-id="4c145-821">Right</span></span>
<span data-ttu-id="4c145-822">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-822">**Description:**</span></span>  
<span data-ttu-id="4c145-823">la función Right devuelve un número especificado de caracteres desde la derecha (final) de una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="4c145-824">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="4c145-825">string: la cadena desde la que devolver los caracteres</span><span class="sxs-lookup"><span data-stu-id="4c145-825">string: the string to return characters from</span></span>
* <span data-ttu-id="4c145-826">NumChars: un número que identifica el número de caracteres que devolver desde el final (derecho) de la cadena</span><span class="sxs-lookup"><span data-stu-id="4c145-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="4c145-827">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-827">**Remarks:**</span></span>  
<span data-ttu-id="4c145-828">los caracteres NumChars se devuelven a partir de la última posición de la cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="4c145-829">Una cadena que contiene los últimos caracteres numChars de la cadena:</span><span class="sxs-lookup"><span data-stu-id="4c145-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="4c145-830">Con numChars = 0, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="4c145-831">Con numChars < 0, se devuelve una cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="4c145-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="4c145-832">Si la cadena es null, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-832">If string is null, return empty string.</span></span>

<span data-ttu-id="4c145-833">Si la cadena contiene menos caracteres que el número especificado en NumChars, se devuelve una cadena idéntica a la cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="4c145-834">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="4c145-835">devuelve "Doe".</span><span class="sxs-lookup"><span data-stu-id="4c145-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="4c145-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="4c145-836">RTrim</span></span>
<span data-ttu-id="4c145-837">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-837">**Description:**</span></span>  
<span data-ttu-id="4c145-838">la función RTrim quita los espacios en blanco del final de una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="4c145-839">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="4c145-840">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="4c145-841">devuelve "Test".</span><span class="sxs-lookup"><span data-stu-id="4c145-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="4c145-842">Seleccionar</span><span class="sxs-lookup"><span data-stu-id="4c145-842">Select</span></span>
<span data-ttu-id="4c145-843">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-843">**Description:**</span></span>  
<span data-ttu-id="4c145-844">Procesa todos los valores de un atributo de valor múltiple (o el resultado de una expresión) según la función especificada.</span><span class="sxs-lookup"><span data-stu-id="4c145-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="4c145-845">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="4c145-846">item: representa un elemento del atributo de valor múltiple</span><span class="sxs-lookup"><span data-stu-id="4c145-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="4c145-847">attribute: el atributo de valor múltiple</span><span class="sxs-lookup"><span data-stu-id="4c145-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="4c145-848">expression: una expresión que devuelve una colección de valores</span><span class="sxs-lookup"><span data-stu-id="4c145-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="4c145-849">condition: cualquier función que pueda procesar un elemento en el atributo</span><span class="sxs-lookup"><span data-stu-id="4c145-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="4c145-850">**Ejemplos:**</span><span class="sxs-lookup"><span data-stu-id="4c145-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="4c145-851">Devuelva todos los valores del atributo de valor múltiple otherPhone una vez que se han quitado los guiones (-).</span><span class="sxs-lookup"><span data-stu-id="4c145-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="4c145-852">Dividir</span><span class="sxs-lookup"><span data-stu-id="4c145-852">Split</span></span>
<span data-ttu-id="4c145-853">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-853">**Description:**</span></span>  
<span data-ttu-id="4c145-854">la función Split toma una cadena separada por un delimitador y la convierte en una cadena multivalor.</span><span class="sxs-lookup"><span data-stu-id="4c145-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="4c145-855">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="4c145-856">value: la cadena con un carácter delimitador que separar.</span><span class="sxs-lookup"><span data-stu-id="4c145-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="4c145-857">delimiter: carácter único que usar como delimitador.</span><span class="sxs-lookup"><span data-stu-id="4c145-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="4c145-858">limit: número máximo de valores que se pueden devolver.</span><span class="sxs-lookup"><span data-stu-id="4c145-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="4c145-859">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="4c145-860">devuelve una cadena multivalor con dos elementos útiles para el atributo proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="4c145-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="4c145-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="4c145-861">StringFromGuid</span></span>
<span data-ttu-id="4c145-862">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-862">**Description:**</span></span>  
<span data-ttu-id="4c145-863">la función StringFromGuid toma un GUID binario y lo convierte en una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="4c145-864">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="4c145-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="4c145-865">StringFromSid</span></span>
<span data-ttu-id="4c145-866">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-866">**Description:**</span></span>  
<span data-ttu-id="4c145-867">la función StringFromSid convierte una matriz de bytes o una matriz de bytes multivalor que contiene un identificador de seguridad en una cadena o en una cadena multivalor.</span><span class="sxs-lookup"><span data-stu-id="4c145-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="4c145-868">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="4c145-869">Switch</span><span class="sxs-lookup"><span data-stu-id="4c145-869">Switch</span></span>
<span data-ttu-id="4c145-870">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-870">**Description:**</span></span>  
<span data-ttu-id="4c145-871">la función Switch se utiliza para devolver un único valor según las condiciones evaluadas.</span><span class="sxs-lookup"><span data-stu-id="4c145-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="4c145-872">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="4c145-873">expr: expresión variante que desea evaluar.</span><span class="sxs-lookup"><span data-stu-id="4c145-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="4c145-874">value: valor que se va a devolver si la expresión correspondiente es True.</span><span class="sxs-lookup"><span data-stu-id="4c145-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="4c145-875">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-875">**Remarks:**</span></span>  
<span data-ttu-id="4c145-876">la lista de argumentos de la función Switch consta de pares de expresiones y valores.</span><span class="sxs-lookup"><span data-stu-id="4c145-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="4c145-877">Las expresiones se evalúan de izquierda a derecha y se devuelve el valor asociado a la primera expresión que evaluar en True.</span><span class="sxs-lookup"><span data-stu-id="4c145-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="4c145-878">Si los elementos no están emparejados correctamente, se produce un error en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4c145-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="4c145-879">Por ejemplo, si expr1 es True, Switch devuelve value1.</span><span class="sxs-lookup"><span data-stu-id="4c145-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="4c145-880">Si expr-1 es False, pero expr-2 es True, Switch devuelve value-2, etc.</span><span class="sxs-lookup"><span data-stu-id="4c145-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="4c145-881">Switch devuelve Nothing si:</span><span class="sxs-lookup"><span data-stu-id="4c145-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="4c145-882">Ninguna de las expresiones son True.</span><span class="sxs-lookup"><span data-stu-id="4c145-882">None of the expressions are True.</span></span>
* <span data-ttu-id="4c145-883">La primera expresión True tiene un valor correspondiente que es Null.</span><span class="sxs-lookup"><span data-stu-id="4c145-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="4c145-884">Switch evalúa todas las expresiones, aunque devuelva solo una de ellas.</span><span class="sxs-lookup"><span data-stu-id="4c145-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="4c145-885">Por este motivo, debe vigilar efectos secundarios no deseados.</span><span class="sxs-lookup"><span data-stu-id="4c145-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="4c145-886">Por ejemplo, si la evaluación de cualquier expresión tiene como resultado una división por cero, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="4c145-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="4c145-887">El valor puede ser también la función Error que devolvería una cadena personalizada.</span><span class="sxs-lookup"><span data-stu-id="4c145-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="4c145-888">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="4c145-889">Devuelve el idioma hablado en las ciudades más importantes. De lo contrario, devuelve un error.</span><span class="sxs-lookup"><span data-stu-id="4c145-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="4c145-890">Trim</span><span class="sxs-lookup"><span data-stu-id="4c145-890">Trim</span></span>
<span data-ttu-id="4c145-891">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-891">**Description:**</span></span>  
<span data-ttu-id="4c145-892">la función Trim quita los espacios en blanco del principio y del final de una cadena.</span><span class="sxs-lookup"><span data-stu-id="4c145-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="4c145-893">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="4c145-894">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="4c145-895">devuelve "test".</span><span class="sxs-lookup"><span data-stu-id="4c145-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="4c145-896">Quita los espacios del principio y del final de cada valor en el atributo proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="4c145-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="4c145-897">UCase</span><span class="sxs-lookup"><span data-stu-id="4c145-897">UCase</span></span>
<span data-ttu-id="4c145-898">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-898">**Description:**</span></span>  
<span data-ttu-id="4c145-899">: la función UCase convierte todos los caracteres de una cadena a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="4c145-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="4c145-900">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="4c145-901">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="4c145-902">devuelve "test".</span><span class="sxs-lookup"><span data-stu-id="4c145-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="4c145-903">Where</span><span class="sxs-lookup"><span data-stu-id="4c145-903">Where</span></span>

<span data-ttu-id="4c145-904">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-904">**Description:**</span></span>  
<span data-ttu-id="4c145-905">Devuelve un subconjunto de valores de un atributo de valor múltiple (o el resultado de una expresión) según la función especificada.</span><span class="sxs-lookup"><span data-stu-id="4c145-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="4c145-906">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="4c145-907">item: representa un elemento del atributo de valor múltiple</span><span class="sxs-lookup"><span data-stu-id="4c145-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="4c145-908">attribute: el atributo de valor múltiple</span><span class="sxs-lookup"><span data-stu-id="4c145-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="4c145-909">condition: cualquier expresión que pueda evaluarse en True o False</span><span class="sxs-lookup"><span data-stu-id="4c145-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="4c145-910">expression: una expresión que devuelve una colección de valores</span><span class="sxs-lookup"><span data-stu-id="4c145-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="4c145-911">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="4c145-912">Devuelva los valores de certificado en el atributo de valor múltiple userCertificate que no han expirado.</span><span class="sxs-lookup"><span data-stu-id="4c145-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="4c145-913">With</span><span class="sxs-lookup"><span data-stu-id="4c145-913">With</span></span>
<span data-ttu-id="4c145-914">**Descripción:**</span><span class="sxs-lookup"><span data-stu-id="4c145-914">**Description:**</span></span>  
<span data-ttu-id="4c145-915">La función With proporciona una manera de simplificar una expresión compleja usando una variable para representar una subexpresión que aparece una o varias veces en la expresión compleja.</span><span class="sxs-lookup"><span data-stu-id="4c145-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="4c145-916">**Sintaxis:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="4c145-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="4c145-917">variable: representa la subexpresión.</span><span class="sxs-lookup"><span data-stu-id="4c145-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="4c145-918">subExpression: la que la variable representa.</span><span class="sxs-lookup"><span data-stu-id="4c145-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="4c145-919">complexExpression: una expresión compleja.</span><span class="sxs-lookup"><span data-stu-id="4c145-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="4c145-920">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="4c145-921">Es funcionalmente equivalente a:</span><span class="sxs-lookup"><span data-stu-id="4c145-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="4c145-922">Que devuelve solo los valores de los certificados que no han expirado en el atributo userCertificate.</span><span class="sxs-lookup"><span data-stu-id="4c145-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="4c145-923">Word</span><span class="sxs-lookup"><span data-stu-id="4c145-923">Word</span></span>
<span data-ttu-id="4c145-924">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="4c145-924">**Description:**</span></span>  
<span data-ttu-id="4c145-925">: la función Word devuelve una palabra incluida en una cadena, según los parámetros que describen los delimitadores que se usarán y el número de palabras que se devolverán.</span><span class="sxs-lookup"><span data-stu-id="4c145-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="4c145-926">**Sintaxis:**</span><span class="sxs-lookup"><span data-stu-id="4c145-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="4c145-927">string: la cadena desde la que devolver una palabra.</span><span class="sxs-lookup"><span data-stu-id="4c145-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="4c145-928">WordNumber: un número que identifica qué número de palabras debe devolver.</span><span class="sxs-lookup"><span data-stu-id="4c145-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="4c145-929">delimiters: una cadena que representa los delimitadores que deben usarse para identificar palabras</span><span class="sxs-lookup"><span data-stu-id="4c145-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="4c145-930">**Comentarios:**</span><span class="sxs-lookup"><span data-stu-id="4c145-930">**Remarks:**</span></span>  
<span data-ttu-id="4c145-931">: cada cadena de caracteres en la cadena separada por uno de los caracteres en los delimitadores se identifica como palabras:</span><span class="sxs-lookup"><span data-stu-id="4c145-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="4c145-932">Si el número es < 1, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="4c145-933">Si la cadena es Null, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="4c145-934">Si la cadena contiene menos palabras o si la cadena no contiene palabras identificadas por los delimitadores, se devuelve una cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="4c145-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="4c145-935">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="4c145-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="4c145-936">devuelve "brown".</span><span class="sxs-lookup"><span data-stu-id="4c145-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="4c145-937">devolvería "has".</span><span class="sxs-lookup"><span data-stu-id="4c145-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c145-938">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4c145-938">Additional Resources</span></span>
* [<span data-ttu-id="4c145-939">Explicación de las expresiones declarativas de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="4c145-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="4c145-940">Sincronización de Azure AD Connect: personalización de las opciones de sincronización</span><span class="sxs-lookup"><span data-stu-id="4c145-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4c145-941">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c145-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
