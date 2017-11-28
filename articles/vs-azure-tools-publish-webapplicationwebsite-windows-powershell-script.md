---
title: Publish-WebApplicationWebSite (script de Windows PowerShell) | Microsoft Docs
description: "Aprenda a publicar un proyecto web en un sitio web de Azure. Este script crea los recursos necesarios en su suscripción de Azure si no existen."
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
ms.openlocfilehash: 07d21b7ce6cd8aee1cff704d316e7a2ca8c00437
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="503f7-104">Publicación de WebApplicationWebSite (script de Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="503f7-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="503f7-105">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="503f7-105">Syntax</span></span>
<span data-ttu-id="503f7-106">Publica un proyecto web en un sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="503f7-106">Publishes a web project to an Azure website.</span></span> <span data-ttu-id="503f7-107">El script crea los recursos necesarios en su suscripción de Azure si no existen.</span><span class="sxs-lookup"><span data-stu-id="503f7-107">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="503f7-108">Configuración</span><span class="sxs-lookup"><span data-stu-id="503f7-108">Configuration</span></span>
<span data-ttu-id="503f7-109">La ruta de acceso al archivo de configuración JSON que describe los detalles de la implementación.</span><span class="sxs-lookup"><span data-stu-id="503f7-109">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="503f7-110">Parámetro</span><span class="sxs-lookup"><span data-stu-id="503f7-110">Parameter</span></span> | <span data-ttu-id="503f7-111">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="503f7-112">Alias</span><span class="sxs-lookup"><span data-stu-id="503f7-112">Aliases</span></span> |<span data-ttu-id="503f7-113">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-113">none</span></span> |
| <span data-ttu-id="503f7-114">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="503f7-114">Required?</span></span> |<span data-ttu-id="503f7-115">true</span><span class="sxs-lookup"><span data-stu-id="503f7-115">true</span></span> |
| <span data-ttu-id="503f7-116">Posición</span><span class="sxs-lookup"><span data-stu-id="503f7-116">Position</span></span> |<span data-ttu-id="503f7-117">con nombre</span><span class="sxs-lookup"><span data-stu-id="503f7-117">named</span></span> |
| <span data-ttu-id="503f7-118">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-118">Default value</span></span> |<span data-ttu-id="503f7-119">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-119">none</span></span> |
| <span data-ttu-id="503f7-120">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="503f7-120">Accept pipeline input?</span></span> |<span data-ttu-id="503f7-121">false</span><span class="sxs-lookup"><span data-stu-id="503f7-121">false</span></span> |
| <span data-ttu-id="503f7-122">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="503f7-122">Accept wildcard characters?</span></span> |<span data-ttu-id="503f7-123">false</span><span class="sxs-lookup"><span data-stu-id="503f7-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="503f7-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="503f7-124">SubscriptionName</span></span>
<span data-ttu-id="503f7-125">Nombre de la suscripción de Azure en la que desea crear el sitio web.</span><span class="sxs-lookup"><span data-stu-id="503f7-125">The name of the Azure subscription that you want to create the website in.</span></span>

| <span data-ttu-id="503f7-126">Parámetro</span><span class="sxs-lookup"><span data-stu-id="503f7-126">Parameter</span></span> | <span data-ttu-id="503f7-127">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="503f7-128">Alias</span><span class="sxs-lookup"><span data-stu-id="503f7-128">Aliases</span></span> |<span data-ttu-id="503f7-129">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-129">none</span></span> |
| <span data-ttu-id="503f7-130">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="503f7-130">Required?</span></span> |<span data-ttu-id="503f7-131">false</span><span class="sxs-lookup"><span data-stu-id="503f7-131">false</span></span> |
| <span data-ttu-id="503f7-132">Posición</span><span class="sxs-lookup"><span data-stu-id="503f7-132">Position</span></span> |<span data-ttu-id="503f7-133">con nombre</span><span class="sxs-lookup"><span data-stu-id="503f7-133">named</span></span> |
| <span data-ttu-id="503f7-134">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-134">Default value</span></span> |<span data-ttu-id="503f7-135">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-135">none</span></span> |
| <span data-ttu-id="503f7-136">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="503f7-136">Accept pipeline input?</span></span> |<span data-ttu-id="503f7-137">false</span><span class="sxs-lookup"><span data-stu-id="503f7-137">false</span></span> |
| <span data-ttu-id="503f7-138">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="503f7-138">Accept wildcard characters?</span></span> |<span data-ttu-id="503f7-139">false</span><span class="sxs-lookup"><span data-stu-id="503f7-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="503f7-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="503f7-140">WebDeployPackage</span></span>
<span data-ttu-id="503f7-141">La ruta de acceso al paquete de implementación web para publicar en el sitio web.</span><span class="sxs-lookup"><span data-stu-id="503f7-141">The path to the web deployment package to publish to the website.</span></span> <span data-ttu-id="503f7-142">Puede crear este paquete mediante el Asistente de publicación web en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="503f7-142">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="503f7-143">Para obtener más información, consulte [Introducción a Servicios en la nube de Azure y ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="503f7-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="503f7-144">Parámetro</span><span class="sxs-lookup"><span data-stu-id="503f7-144">Parameter</span></span> | <span data-ttu-id="503f7-145">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="503f7-146">Alias</span><span class="sxs-lookup"><span data-stu-id="503f7-146">Aliases</span></span> |<span data-ttu-id="503f7-147">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-147">none</span></span> |
| <span data-ttu-id="503f7-148">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="503f7-148">Required?</span></span> |<span data-ttu-id="503f7-149">false</span><span class="sxs-lookup"><span data-stu-id="503f7-149">false</span></span> |
| <span data-ttu-id="503f7-150">Posición</span><span class="sxs-lookup"><span data-stu-id="503f7-150">Position</span></span> |<span data-ttu-id="503f7-151">con nombre</span><span class="sxs-lookup"><span data-stu-id="503f7-151">named</span></span> |
| <span data-ttu-id="503f7-152">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-152">Default value</span></span> |<span data-ttu-id="503f7-153">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-153">none</span></span> |
| <span data-ttu-id="503f7-154">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="503f7-154">Accept pipeline input?</span></span> |<span data-ttu-id="503f7-155">false</span><span class="sxs-lookup"><span data-stu-id="503f7-155">false</span></span> |
| <span data-ttu-id="503f7-156">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="503f7-156">Accept wildcard characters?</span></span> |<span data-ttu-id="503f7-157">false</span><span class="sxs-lookup"><span data-stu-id="503f7-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="503f7-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="503f7-158">DatabaseServerPassword</span></span>
<span data-ttu-id="503f7-159">El nombre de usuario y la contraseña de la base de datos SQL en Azure.</span><span class="sxs-lookup"><span data-stu-id="503f7-159">The username and password for the SQL database in Azure.</span></span>

| <span data-ttu-id="503f7-160">Parámetro</span><span class="sxs-lookup"><span data-stu-id="503f7-160">Parameter</span></span> | <span data-ttu-id="503f7-161">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="503f7-162">Alias</span><span class="sxs-lookup"><span data-stu-id="503f7-162">Aliases</span></span> |<span data-ttu-id="503f7-163">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-163">none</span></span> |
| <span data-ttu-id="503f7-164">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="503f7-164">Required?</span></span> |<span data-ttu-id="503f7-165">false</span><span class="sxs-lookup"><span data-stu-id="503f7-165">false</span></span> |
| <span data-ttu-id="503f7-166">Posición</span><span class="sxs-lookup"><span data-stu-id="503f7-166">Position</span></span> |<span data-ttu-id="503f7-167">con nombre</span><span class="sxs-lookup"><span data-stu-id="503f7-167">named</span></span> |
| <span data-ttu-id="503f7-168">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-168">Default value</span></span> |<span data-ttu-id="503f7-169">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-169">none</span></span> |
| <span data-ttu-id="503f7-170">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="503f7-170">Accept pipeline input?</span></span> |<span data-ttu-id="503f7-171">false</span><span class="sxs-lookup"><span data-stu-id="503f7-171">false</span></span> |
| <span data-ttu-id="503f7-172">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="503f7-172">Accept wildcard characters?</span></span> |<span data-ttu-id="503f7-173">false</span><span class="sxs-lookup"><span data-stu-id="503f7-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="503f7-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="503f7-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="503f7-175">Si es true, imprimir mensajes del script a la secuencia de salida.</span><span class="sxs-lookup"><span data-stu-id="503f7-175">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="503f7-176">Parámetro</span><span class="sxs-lookup"><span data-stu-id="503f7-176">Parameter</span></span> | <span data-ttu-id="503f7-177">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="503f7-178">Alias</span><span class="sxs-lookup"><span data-stu-id="503f7-178">Aliases</span></span> |<span data-ttu-id="503f7-179">Ninguna</span><span class="sxs-lookup"><span data-stu-id="503f7-179">none</span></span> |
| <span data-ttu-id="503f7-180">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="503f7-180">Required?</span></span> |<span data-ttu-id="503f7-181">false</span><span class="sxs-lookup"><span data-stu-id="503f7-181">false</span></span> |
| <span data-ttu-id="503f7-182">Posición</span><span class="sxs-lookup"><span data-stu-id="503f7-182">Position</span></span> |<span data-ttu-id="503f7-183">con nombre</span><span class="sxs-lookup"><span data-stu-id="503f7-183">named</span></span> |
| <span data-ttu-id="503f7-184">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="503f7-184">Default value</span></span> |<span data-ttu-id="503f7-185">false</span><span class="sxs-lookup"><span data-stu-id="503f7-185">false</span></span> |
| <span data-ttu-id="503f7-186">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="503f7-186">Accept pipeline input?</span></span> |<span data-ttu-id="503f7-187">false</span><span class="sxs-lookup"><span data-stu-id="503f7-187">false</span></span> |
| <span data-ttu-id="503f7-188">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="503f7-188">Accept wildcard characters?</span></span> |<span data-ttu-id="503f7-189">false</span><span class="sxs-lookup"><span data-stu-id="503f7-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="503f7-190">Comentarios</span><span class="sxs-lookup"><span data-stu-id="503f7-190">Remarks</span></span>
<span data-ttu-id="503f7-191">Para obtener una explicación completa de cómo usar el script para crear entornos de desarrollo y pruebas, consulte [Usar scripts de Windows PowerShell para la publicación en entornos de desarrollo y pruebas](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="503f7-191">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="503f7-192">El archivo de configuración JSON especifica los detalles de lo que va a implementarse.</span><span class="sxs-lookup"><span data-stu-id="503f7-192">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="503f7-193">Incluye la información que especificó cuando creó el proyecto, como el nombre y el nombre de usuario para el sitio web.</span><span class="sxs-lookup"><span data-stu-id="503f7-193">It includes the information that you specified when you created the project, such as the name and username for the website.</span></span> <span data-ttu-id="503f7-194">También incluye la base de datos que se va a aprovisionar, si la hubiera.</span><span class="sxs-lookup"><span data-stu-id="503f7-194">It also includes the database to provision, if any.</span></span> <span data-ttu-id="503f7-195">El código siguiente muestra un archivo de configuración de JSON de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="503f7-195">The following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="503f7-196">Puede editar el archivo de configuración de JSON para cambiar lo que se implementa.</span><span class="sxs-lookup"><span data-stu-id="503f7-196">You can edit the JSON configuration file to change what is deployed.</span></span> <span data-ttu-id="503f7-197">Una sección webSite es obligatoria pero la sección database es opcional.</span><span class="sxs-lookup"><span data-stu-id="503f7-197">A webSite section is required, but the database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="503f7-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="503f7-198">Next steps</span></span>
<span data-ttu-id="503f7-199">Para obtener más información, consulte [Publish-WebApplicationVM (script de Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="503f7-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

