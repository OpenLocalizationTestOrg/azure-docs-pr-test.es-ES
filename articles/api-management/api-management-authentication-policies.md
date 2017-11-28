---
title: "las directivas de autenticación de administración de API aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de las directivas de autenticación de hello disponibles para su uso en la administración de API de Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="a812f-103">Directivas de autenticación de Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a812f-103">API Management authentication policies</span></span>
<span data-ttu-id="a812f-104">En este tema se proporciona una referencia para hello las siguientes directivas de administración de API.</span><span class="sxs-lookup"><span data-stu-id="a812f-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="a812f-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="a812f-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="a812f-106"><a name="AuthenticationPolicies"></a> Directivas de autenticación</span><span class="sxs-lookup"><span data-stu-id="a812f-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="a812f-107">[Autenticar con opción básica](api-management-authentication-policies.md#Basic) : autenticar con un servicio de back-end mediante la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="a812f-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="a812f-108">[Autenticar con certificado de cliente](api-management-authentication-policies.md#ClientCertificate) : autenticar con un servicio de back-end mediante certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="a812f-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="a812f-109"><a name="Basic"></a> Authenticate with Basic</span><span class="sxs-lookup"><span data-stu-id="a812f-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="a812f-110">Hola de uso `authentication-basic` tooauthenticate de directiva con un servicio de back-end mediante la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="a812f-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="a812f-111">Esta directiva establece eficazmente toohello de encabezado de autorización HTTP Hola valor correspondiente toohello las credenciales proporcionadas en la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="a812f-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="a812f-112">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="a812f-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="a812f-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a812f-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="a812f-114">Elementos</span><span class="sxs-lookup"><span data-stu-id="a812f-114">Elements</span></span>  
  
|<span data-ttu-id="a812f-115">Nombre</span><span class="sxs-lookup"><span data-stu-id="a812f-115">Name</span></span>|<span data-ttu-id="a812f-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="a812f-116">Description</span></span>|<span data-ttu-id="a812f-117">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a812f-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="a812f-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="a812f-118">authentication-basic</span></span>|<span data-ttu-id="a812f-119">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="a812f-119">Root element.</span></span>|<span data-ttu-id="a812f-120">Sí</span><span class="sxs-lookup"><span data-stu-id="a812f-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="a812f-121">Atributos</span><span class="sxs-lookup"><span data-stu-id="a812f-121">Attributes</span></span>  
  
|<span data-ttu-id="a812f-122">Nombre</span><span class="sxs-lookup"><span data-stu-id="a812f-122">Name</span></span>|<span data-ttu-id="a812f-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="a812f-123">Description</span></span>|<span data-ttu-id="a812f-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a812f-124">Required</span></span>|<span data-ttu-id="a812f-125">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="a812f-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="a812f-126">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="a812f-126">username</span></span>|<span data-ttu-id="a812f-127">Especifica el nombre de usuario de Hola de credencial básica hello.</span><span class="sxs-lookup"><span data-stu-id="a812f-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="a812f-128">Sí</span><span class="sxs-lookup"><span data-stu-id="a812f-128">Yes</span></span>|<span data-ttu-id="a812f-129">N/D</span><span class="sxs-lookup"><span data-stu-id="a812f-129">N/A</span></span>|  
|<span data-ttu-id="a812f-130">Contraseña</span><span class="sxs-lookup"><span data-stu-id="a812f-130">password</span></span>|<span data-ttu-id="a812f-131">Especifica la contraseña de Hola de credencial básica hello.</span><span class="sxs-lookup"><span data-stu-id="a812f-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="a812f-132">Sí</span><span class="sxs-lookup"><span data-stu-id="a812f-132">Yes</span></span>|<span data-ttu-id="a812f-133">N/D</span><span class="sxs-lookup"><span data-stu-id="a812f-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="a812f-134">Uso</span><span class="sxs-lookup"><span data-stu-id="a812f-134">Usage</span></span>  
 <span data-ttu-id="a812f-135">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="a812f-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="a812f-136">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="a812f-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="a812f-137">**Ámbitos de la directiva:** API</span><span class="sxs-lookup"><span data-stu-id="a812f-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="a812f-138"><a name="ClientCertificate"></a> Autenticación Básica</span><span class="sxs-lookup"><span data-stu-id="a812f-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="a812f-139">Hola de uso `authentication-certificate` tooauthenticate de directiva con un servicio de back-end mediante certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="a812f-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="a812f-140">certificado de Hello debe toobe [instalado en la API de administración](http://go.microsoft.com/fwlink/?LinkID=511599) primero y se identifica mediante su huella digital.</span><span class="sxs-lookup"><span data-stu-id="a812f-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="a812f-141">Instrucción de la directiva</span><span class="sxs-lookup"><span data-stu-id="a812f-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="a812f-142">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a812f-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="a812f-143">Elementos</span><span class="sxs-lookup"><span data-stu-id="a812f-143">Elements</span></span>  
  
|<span data-ttu-id="a812f-144">Nombre</span><span class="sxs-lookup"><span data-stu-id="a812f-144">Name</span></span>|<span data-ttu-id="a812f-145">Descripción</span><span class="sxs-lookup"><span data-stu-id="a812f-145">Description</span></span>|<span data-ttu-id="a812f-146">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a812f-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="a812f-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="a812f-147">authentication-certificate</span></span>|<span data-ttu-id="a812f-148">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="a812f-148">Root element.</span></span>|<span data-ttu-id="a812f-149">Sí</span><span class="sxs-lookup"><span data-stu-id="a812f-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="a812f-150">Atributos</span><span class="sxs-lookup"><span data-stu-id="a812f-150">Attributes</span></span>  
  
|<span data-ttu-id="a812f-151">Nombre</span><span class="sxs-lookup"><span data-stu-id="a812f-151">Name</span></span>|<span data-ttu-id="a812f-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="a812f-152">Description</span></span>|<span data-ttu-id="a812f-153">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="a812f-153">Required</span></span>|<span data-ttu-id="a812f-154">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="a812f-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="a812f-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="a812f-155">thumbprint</span></span>|<span data-ttu-id="a812f-156">Hola huella digital de certificado de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a812f-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="a812f-157">Sí</span><span class="sxs-lookup"><span data-stu-id="a812f-157">Yes</span></span>|<span data-ttu-id="a812f-158">N/D</span><span class="sxs-lookup"><span data-stu-id="a812f-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="a812f-159">Uso</span><span class="sxs-lookup"><span data-stu-id="a812f-159">Usage</span></span>  
 <span data-ttu-id="a812f-160">Esta directiva puede usarse en hello después de la directiva [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="a812f-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="a812f-161">**Secciones de la directiva:** entrante</span><span class="sxs-lookup"><span data-stu-id="a812f-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="a812f-162">**Ámbitos de la directiva:** API</span><span class="sxs-lookup"><span data-stu-id="a812f-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="a812f-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a812f-163">Next steps</span></span>
<span data-ttu-id="a812f-164">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a812f-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  