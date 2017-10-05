---
title: "Directivas de autenticación de Azure API Management | Microsoft Docs"
description: "Aprenda sobre las directivas de autenticación disponibles para su uso en Azure API Management."
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
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="66de1-103">Directivas de autenticación de Azure API Management</span><span class="sxs-lookup"><span data-stu-id="66de1-103">API Management authentication policies</span></span>
<span data-ttu-id="66de1-104">En este tema se proporciona una referencia para las siguientes directivas de API Management.</span><span class="sxs-lookup"><span data-stu-id="66de1-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="66de1-105">Para obtener más información sobre cómo agregar y configurar directivas, consulte [Directivas en Administración de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="66de1-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="66de1-106"><a name="AuthenticationPolicies"></a> Directivas de autenticación</span><span class="sxs-lookup"><span data-stu-id="66de1-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="66de1-107">[Autenticar con opción básica](api-management-authentication-policies.md#Basic) : autenticar con un servicio de back-end mediante la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="66de1-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="66de1-108">[Autenticar con certificado de cliente](api-management-authentication-policies.md#ClientCertificate) : autenticar con un servicio de back-end mediante certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="66de1-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="66de1-109"><a name="Basic"></a> Authenticate with Basic</span><span class="sxs-lookup"><span data-stu-id="66de1-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="66de1-110">Use la directiva `authentication-basic` para realizar la autenticación con upolicy to authenticate with a n servicio de back-end mediante autenticación Básica.</span><span class="sxs-lookup"><span data-stu-id="66de1-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="66de1-111">Esta directiva establece eficazmente el encabezado de autorización HTTP en el valor correspondiente a las credenciales proporcionadas en la directiva.</span><span class="sxs-lookup"><span data-stu-id="66de1-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="66de1-112">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="66de1-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="66de1-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="66de1-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="66de1-114">Elementos</span><span class="sxs-lookup"><span data-stu-id="66de1-114">Elements</span></span>  
  
|<span data-ttu-id="66de1-115">Nombre</span><span class="sxs-lookup"><span data-stu-id="66de1-115">Name</span></span>|<span data-ttu-id="66de1-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="66de1-116">Description</span></span>|<span data-ttu-id="66de1-117">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="66de1-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="66de1-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="66de1-118">authentication-basic</span></span>|<span data-ttu-id="66de1-119">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="66de1-119">Root element.</span></span>|<span data-ttu-id="66de1-120">Sí</span><span class="sxs-lookup"><span data-stu-id="66de1-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="66de1-121">Atributos</span><span class="sxs-lookup"><span data-stu-id="66de1-121">Attributes</span></span>  
  
|<span data-ttu-id="66de1-122">Nombre</span><span class="sxs-lookup"><span data-stu-id="66de1-122">Name</span></span>|<span data-ttu-id="66de1-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="66de1-123">Description</span></span>|<span data-ttu-id="66de1-124">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="66de1-124">Required</span></span>|<span data-ttu-id="66de1-125">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="66de1-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="66de1-126">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="66de1-126">username</span></span>|<span data-ttu-id="66de1-127">Especifica el nombre de usuario de la credencial básica.</span><span class="sxs-lookup"><span data-stu-id="66de1-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="66de1-128">Sí</span><span class="sxs-lookup"><span data-stu-id="66de1-128">Yes</span></span>|<span data-ttu-id="66de1-129">N/D</span><span class="sxs-lookup"><span data-stu-id="66de1-129">N/A</span></span>|  
|<span data-ttu-id="66de1-130">contraseña</span><span class="sxs-lookup"><span data-stu-id="66de1-130">password</span></span>|<span data-ttu-id="66de1-131">Especifica la contraseña de usuario de la credencial básica.</span><span class="sxs-lookup"><span data-stu-id="66de1-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="66de1-132">Sí</span><span class="sxs-lookup"><span data-stu-id="66de1-132">Yes</span></span>|<span data-ttu-id="66de1-133">N/D</span><span class="sxs-lookup"><span data-stu-id="66de1-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="66de1-134">Uso</span><span class="sxs-lookup"><span data-stu-id="66de1-134">Usage</span></span>  
 <span data-ttu-id="66de1-135">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="66de1-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="66de1-136">**Secciones de la directiva:** inbound</span><span class="sxs-lookup"><span data-stu-id="66de1-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="66de1-137">**Ámbitos de la directiva:** API</span><span class="sxs-lookup"><span data-stu-id="66de1-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="66de1-138"><a name="ClientCertificate"></a> Autenticación Básica</span><span class="sxs-lookup"><span data-stu-id="66de1-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="66de1-139">Use la directiva `authentication-certificate` para realizar la autenticación con un servicio de back-end mediante un certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="66de1-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="66de1-140">El certificado se debe [instalar primero en API Management](http://go.microsoft.com/fwlink/?LinkID=511599) y se identifica mediante su huella digital.</span><span class="sxs-lookup"><span data-stu-id="66de1-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="66de1-141">Declaración de directiva</span><span class="sxs-lookup"><span data-stu-id="66de1-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="66de1-142">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="66de1-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="66de1-143">Elementos</span><span class="sxs-lookup"><span data-stu-id="66de1-143">Elements</span></span>  
  
|<span data-ttu-id="66de1-144">Nombre</span><span class="sxs-lookup"><span data-stu-id="66de1-144">Name</span></span>|<span data-ttu-id="66de1-145">Descripción</span><span class="sxs-lookup"><span data-stu-id="66de1-145">Description</span></span>|<span data-ttu-id="66de1-146">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="66de1-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="66de1-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="66de1-147">authentication-certificate</span></span>|<span data-ttu-id="66de1-148">Elemento raíz.</span><span class="sxs-lookup"><span data-stu-id="66de1-148">Root element.</span></span>|<span data-ttu-id="66de1-149">Sí</span><span class="sxs-lookup"><span data-stu-id="66de1-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="66de1-150">Atributos</span><span class="sxs-lookup"><span data-stu-id="66de1-150">Attributes</span></span>  
  
|<span data-ttu-id="66de1-151">Nombre</span><span class="sxs-lookup"><span data-stu-id="66de1-151">Name</span></span>|<span data-ttu-id="66de1-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="66de1-152">Description</span></span>|<span data-ttu-id="66de1-153">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="66de1-153">Required</span></span>|<span data-ttu-id="66de1-154">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="66de1-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="66de1-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="66de1-155">thumbprint</span></span>|<span data-ttu-id="66de1-156">La huella digital del certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="66de1-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="66de1-157">Sí</span><span class="sxs-lookup"><span data-stu-id="66de1-157">Yes</span></span>|<span data-ttu-id="66de1-158">N/D</span><span class="sxs-lookup"><span data-stu-id="66de1-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="66de1-159">Uso</span><span class="sxs-lookup"><span data-stu-id="66de1-159">Usage</span></span>  
 <span data-ttu-id="66de1-160">Esta directiva puede usarse en las siguientes [secciones](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) y [ámbitos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de directiva.</span><span class="sxs-lookup"><span data-stu-id="66de1-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="66de1-161">**Secciones de la directiva:** inbound</span><span class="sxs-lookup"><span data-stu-id="66de1-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="66de1-162">**Ámbitos de la directiva:** API</span><span class="sxs-lookup"><span data-stu-id="66de1-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="66de1-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66de1-163">Next steps</span></span>
<span data-ttu-id="66de1-164">Para más información sobre cómo trabajar con directivas, consulte a [Directivas de API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="66de1-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  