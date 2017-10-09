---
title: aaaPublish-WebApplicationWebSite (script de Windows PowerShell) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toopublish un sitio web del proyecto tooan sitio Web de Azure. Este script crea recursos Hola necesario en su suscripción de Azure si no existen."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="5c92e-104">Publicación de WebApplicationWebSite (script de Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="5c92e-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="5c92e-105">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="5c92e-105">Syntax</span></span>
<span data-ttu-id="5c92e-106">Publica un tooan de proyecto web sitio Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c92e-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="5c92e-107">script de Hola crea recursos Hola necesario en su suscripción de Azure si no existen.</span><span class="sxs-lookup"><span data-stu-id="5c92e-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="5c92e-108">Configuración</span><span class="sxs-lookup"><span data-stu-id="5c92e-108">Configuration</span></span>
<span data-ttu-id="5c92e-109">Hola ruta de acceso toohello archivo de configuración JSON que describe los detalles de Hola de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c92e-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="5c92e-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="5c92e-110">Parameter</span></span> | <span data-ttu-id="5c92e-111">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="5c92e-112">Alias</span><span class="sxs-lookup"><span data-stu-id="5c92e-112">Aliases</span></span> |<span data-ttu-id="5c92e-113">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-113">none</span></span> |
| <span data-ttu-id="5c92e-114">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="5c92e-114">Required?</span></span> |<span data-ttu-id="5c92e-115">true</span><span class="sxs-lookup"><span data-stu-id="5c92e-115">true</span></span> |
| <span data-ttu-id="5c92e-116">Posición</span><span class="sxs-lookup"><span data-stu-id="5c92e-116">Position</span></span> |<span data-ttu-id="5c92e-117">con nombre</span><span class="sxs-lookup"><span data-stu-id="5c92e-117">named</span></span> |
| <span data-ttu-id="5c92e-118">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-118">Default value</span></span> |<span data-ttu-id="5c92e-119">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-119">none</span></span> |
| <span data-ttu-id="5c92e-120">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="5c92e-120">Accept pipeline input?</span></span> |<span data-ttu-id="5c92e-121">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-121">false</span></span> |
| <span data-ttu-id="5c92e-122">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="5c92e-122">Accept wildcard characters?</span></span> |<span data-ttu-id="5c92e-123">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="5c92e-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="5c92e-124">SubscriptionName</span></span>
<span data-ttu-id="5c92e-125">nombre de Hola de suscripción de Azure que desea incluir el sitio Web de hello toocreate en hello.</span><span class="sxs-lookup"><span data-stu-id="5c92e-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="5c92e-126">Parámetro</span><span class="sxs-lookup"><span data-stu-id="5c92e-126">Parameter</span></span> | <span data-ttu-id="5c92e-127">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="5c92e-128">Alias</span><span class="sxs-lookup"><span data-stu-id="5c92e-128">Aliases</span></span> |<span data-ttu-id="5c92e-129">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-129">none</span></span> |
| <span data-ttu-id="5c92e-130">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="5c92e-130">Required?</span></span> |<span data-ttu-id="5c92e-131">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-131">false</span></span> |
| <span data-ttu-id="5c92e-132">Posición</span><span class="sxs-lookup"><span data-stu-id="5c92e-132">Position</span></span> |<span data-ttu-id="5c92e-133">con nombre</span><span class="sxs-lookup"><span data-stu-id="5c92e-133">named</span></span> |
| <span data-ttu-id="5c92e-134">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-134">Default value</span></span> |<span data-ttu-id="5c92e-135">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-135">none</span></span> |
| <span data-ttu-id="5c92e-136">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="5c92e-136">Accept pipeline input?</span></span> |<span data-ttu-id="5c92e-137">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-137">false</span></span> |
| <span data-ttu-id="5c92e-138">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="5c92e-138">Accept wildcard characters?</span></span> |<span data-ttu-id="5c92e-139">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="5c92e-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="5c92e-140">WebDeployPackage</span></span>
<span data-ttu-id="5c92e-141">Hola ruta de acceso toohello web paquete toopublish toohello sitio Web de implementación.</span><span class="sxs-lookup"><span data-stu-id="5c92e-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="5c92e-142">Puede crear este paquete con el Asistente de publicación Web de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c92e-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="5c92e-143">Para obtener más información, consulte [Introducción a Servicios en la nube de Azure y ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="5c92e-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="5c92e-144">Parámetro</span><span class="sxs-lookup"><span data-stu-id="5c92e-144">Parameter</span></span> | <span data-ttu-id="5c92e-145">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="5c92e-146">Alias</span><span class="sxs-lookup"><span data-stu-id="5c92e-146">Aliases</span></span> |<span data-ttu-id="5c92e-147">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-147">none</span></span> |
| <span data-ttu-id="5c92e-148">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="5c92e-148">Required?</span></span> |<span data-ttu-id="5c92e-149">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-149">false</span></span> |
| <span data-ttu-id="5c92e-150">Posición</span><span class="sxs-lookup"><span data-stu-id="5c92e-150">Position</span></span> |<span data-ttu-id="5c92e-151">con nombre</span><span class="sxs-lookup"><span data-stu-id="5c92e-151">named</span></span> |
| <span data-ttu-id="5c92e-152">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-152">Default value</span></span> |<span data-ttu-id="5c92e-153">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-153">none</span></span> |
| <span data-ttu-id="5c92e-154">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="5c92e-154">Accept pipeline input?</span></span> |<span data-ttu-id="5c92e-155">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-155">false</span></span> |
| <span data-ttu-id="5c92e-156">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="5c92e-156">Accept wildcard characters?</span></span> |<span data-ttu-id="5c92e-157">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="5c92e-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="5c92e-158">DatabaseServerPassword</span></span>
<span data-ttu-id="5c92e-159">nombre de usuario de Hola y la contraseña de base de datos SQL de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="5c92e-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="5c92e-160">Parámetro</span><span class="sxs-lookup"><span data-stu-id="5c92e-160">Parameter</span></span> | <span data-ttu-id="5c92e-161">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="5c92e-162">Alias</span><span class="sxs-lookup"><span data-stu-id="5c92e-162">Aliases</span></span> |<span data-ttu-id="5c92e-163">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-163">none</span></span> |
| <span data-ttu-id="5c92e-164">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="5c92e-164">Required?</span></span> |<span data-ttu-id="5c92e-165">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-165">false</span></span> |
| <span data-ttu-id="5c92e-166">Posición</span><span class="sxs-lookup"><span data-stu-id="5c92e-166">Position</span></span> |<span data-ttu-id="5c92e-167">con nombre</span><span class="sxs-lookup"><span data-stu-id="5c92e-167">named</span></span> |
| <span data-ttu-id="5c92e-168">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-168">Default value</span></span> |<span data-ttu-id="5c92e-169">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-169">none</span></span> |
| <span data-ttu-id="5c92e-170">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="5c92e-170">Accept pipeline input?</span></span> |<span data-ttu-id="5c92e-171">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-171">false</span></span> |
| <span data-ttu-id="5c92e-172">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="5c92e-172">Accept wildcard characters?</span></span> |<span data-ttu-id="5c92e-173">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="5c92e-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="5c92e-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="5c92e-175">Si es true, imprimir mensajes de Hola script toohello flujo de salida.</span><span class="sxs-lookup"><span data-stu-id="5c92e-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="5c92e-176">Parámetro</span><span class="sxs-lookup"><span data-stu-id="5c92e-176">Parameter</span></span> | <span data-ttu-id="5c92e-177">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="5c92e-178">Alias</span><span class="sxs-lookup"><span data-stu-id="5c92e-178">Aliases</span></span> |<span data-ttu-id="5c92e-179">Ninguna</span><span class="sxs-lookup"><span data-stu-id="5c92e-179">none</span></span> |
| <span data-ttu-id="5c92e-180">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="5c92e-180">Required?</span></span> |<span data-ttu-id="5c92e-181">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-181">false</span></span> |
| <span data-ttu-id="5c92e-182">Posición</span><span class="sxs-lookup"><span data-stu-id="5c92e-182">Position</span></span> |<span data-ttu-id="5c92e-183">con nombre</span><span class="sxs-lookup"><span data-stu-id="5c92e-183">named</span></span> |
| <span data-ttu-id="5c92e-184">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c92e-184">Default value</span></span> |<span data-ttu-id="5c92e-185">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-185">false</span></span> |
| <span data-ttu-id="5c92e-186">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="5c92e-186">Accept pipeline input?</span></span> |<span data-ttu-id="5c92e-187">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-187">false</span></span> |
| <span data-ttu-id="5c92e-188">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="5c92e-188">Accept wildcard characters?</span></span> |<span data-ttu-id="5c92e-189">false</span><span class="sxs-lookup"><span data-stu-id="5c92e-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="5c92e-190">Comentarios</span><span class="sxs-lookup"><span data-stu-id="5c92e-190">Remarks</span></span>
<span data-ttu-id="5c92e-191">Para obtener una explicación completa de cómo toouse Hola script toocreate Dev y entornos de prueba, consulte [entornos de prueba y el uso de Scripts de Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="5c92e-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="5c92e-192">archivo de configuración de JSON de Hello especifica detalles de Hola de novedades toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="5c92e-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="5c92e-193">Incluye información de Hola que se especificó cuando creó el proyecto de hello, como el nombre de Hola y el nombre de usuario para el sitio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c92e-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="5c92e-194">También incluye hello tooprovision de base de datos, si lo hay.</span><span class="sxs-lookup"><span data-stu-id="5c92e-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="5c92e-195">Hola siguiente código muestra un archivo de configuración de JSON de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5c92e-195">hello following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="5c92e-196">Puede editar el archivo de configuración de hello JSON toochange lo que se implementa.</span><span class="sxs-lookup"><span data-stu-id="5c92e-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="5c92e-197">Se requiere una sección del sitio Web, pero Hola sección de base de datos es opcional.</span><span class="sxs-lookup"><span data-stu-id="5c92e-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c92e-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c92e-198">Next steps</span></span>
<span data-ttu-id="5c92e-199">Para obtener más información, consulte [Publish-WebApplicationVM (script de Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="5c92e-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

