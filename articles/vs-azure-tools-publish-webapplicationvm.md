---
title: aaaPublish-WebApplicationVM | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy una máquina virtual de web application tooa. Este script crea recursos Hola necesario en su suscripción de Azure si no existen."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="62bf1-104">Publish-WebApplicationVM (script de Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="62bf1-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="62bf1-105">Implementa una máquina virtual de web application tooa.</span><span class="sxs-lookup"><span data-stu-id="62bf1-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="62bf1-106">script de Hola crea recursos Hola necesario en su suscripción de Azure si no existen.</span><span class="sxs-lookup"><span data-stu-id="62bf1-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="62bf1-107">Configuración</span><span class="sxs-lookup"><span data-stu-id="62bf1-107">Configuration</span></span>
<span data-ttu-id="62bf1-108">Hola ruta de acceso toohello archivo de configuración JSON que describe los detalles de Hola de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="62bf1-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="62bf1-109">Alias</span><span class="sxs-lookup"><span data-stu-id="62bf1-109">Aliases</span></span> | <span data-ttu-id="62bf1-110">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="62bf1-111">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="62bf1-111">Required?</span></span> |<span data-ttu-id="62bf1-112">true</span><span class="sxs-lookup"><span data-stu-id="62bf1-112">true</span></span> |
| <span data-ttu-id="62bf1-113">Posición</span><span class="sxs-lookup"><span data-stu-id="62bf1-113">Position</span></span> |<span data-ttu-id="62bf1-114">con nombre</span><span class="sxs-lookup"><span data-stu-id="62bf1-114">named</span></span> |
| <span data-ttu-id="62bf1-115">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="62bf1-115">Default value</span></span> |<span data-ttu-id="62bf1-116">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-116">none</span></span> |
| <span data-ttu-id="62bf1-117">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="62bf1-117">Accept pipeline input?</span></span> |<span data-ttu-id="62bf1-118">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-118">false</span></span> |
| <span data-ttu-id="62bf1-119">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="62bf1-119">Accept wildcard characters?</span></span> |<span data-ttu-id="62bf1-120">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="62bf1-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="62bf1-121">SubscriptionName</span></span>
<span data-ttu-id="62bf1-122">nombre de Hola de Hola suscripción de Azure en que desea que la máquina virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="62bf1-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="62bf1-123">Alias</span><span class="sxs-lookup"><span data-stu-id="62bf1-123">Aliases</span></span> | <span data-ttu-id="62bf1-124">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="62bf1-125">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="62bf1-125">Required?</span></span> |<span data-ttu-id="62bf1-126">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-126">false</span></span> |
| <span data-ttu-id="62bf1-127">Posición</span><span class="sxs-lookup"><span data-stu-id="62bf1-127">Position</span></span> |<span data-ttu-id="62bf1-128">con nombre</span><span class="sxs-lookup"><span data-stu-id="62bf1-128">named</span></span> |
| <span data-ttu-id="62bf1-129">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="62bf1-129">Default value</span></span> |<span data-ttu-id="62bf1-130">Usa Hola primera suscripción en el archivo de suscripción de hello</span><span class="sxs-lookup"><span data-stu-id="62bf1-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="62bf1-131">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="62bf1-131">Accept pipeline input?</span></span> |<span data-ttu-id="62bf1-132">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-132">false</span></span> |
| <span data-ttu-id="62bf1-133">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="62bf1-133">Accept wildcard characters?</span></span> |<span data-ttu-id="62bf1-134">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="62bf1-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="62bf1-135">WebDeployPackage</span></span>
<span data-ttu-id="62bf1-136">Hola ruta de acceso toohello web implementación paquete toopublish toohello la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="62bf1-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="62bf1-137">Puede crear este paquete con el Asistente de publicación Web de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62bf1-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="62bf1-138">Consulte [Cómo crear un paquete de implementación web en Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="62bf1-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="62bf1-139">Alias</span><span class="sxs-lookup"><span data-stu-id="62bf1-139">Aliases</span></span> | <span data-ttu-id="62bf1-140">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="62bf1-141">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="62bf1-141">Required?</span></span> |<span data-ttu-id="62bf1-142">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-142">false</span></span> |
| <span data-ttu-id="62bf1-143">Posición</span><span class="sxs-lookup"><span data-stu-id="62bf1-143">Position</span></span> |<span data-ttu-id="62bf1-144">con nombre</span><span class="sxs-lookup"><span data-stu-id="62bf1-144">named</span></span> |
| <span data-ttu-id="62bf1-145">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="62bf1-145">Default value</span></span> |<span data-ttu-id="62bf1-146">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-146">none</span></span> |
| <span data-ttu-id="62bf1-147">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="62bf1-147">Accept pipeline input?</span></span> |<span data-ttu-id="62bf1-148">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-148">false</span></span> |
| <span data-ttu-id="62bf1-149">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="62bf1-149">Accept wildcard characters?</span></span> |<span data-ttu-id="62bf1-150">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="62bf1-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="62bf1-151">AllowUntrusted</span></span>
<span data-ttu-id="62bf1-152">Si es true, permite el uso de Hola de certificados que no están firmados por una entidad emisora raíz de confianza.</span><span class="sxs-lookup"><span data-stu-id="62bf1-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="62bf1-153">Alias</span><span class="sxs-lookup"><span data-stu-id="62bf1-153">Aliases</span></span> | <span data-ttu-id="62bf1-154">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="62bf1-155">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="62bf1-155">Required?</span></span> |<span data-ttu-id="62bf1-156">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-156">false</span></span> |
| <span data-ttu-id="62bf1-157">Posición</span><span class="sxs-lookup"><span data-stu-id="62bf1-157">Position</span></span> |<span data-ttu-id="62bf1-158">con nombre</span><span class="sxs-lookup"><span data-stu-id="62bf1-158">named</span></span> |
| <span data-ttu-id="62bf1-159">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="62bf1-159">Default value</span></span> |<span data-ttu-id="62bf1-160">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-160">false</span></span> |
| <span data-ttu-id="62bf1-161">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="62bf1-161">Accept pipeline input?</span></span> |<span data-ttu-id="62bf1-162">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-162">false</span></span> |
| <span data-ttu-id="62bf1-163">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="62bf1-163">Accept wildcard characters?</span></span> |<span data-ttu-id="62bf1-164">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="62bf1-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="62bf1-165">VMPassword</span></span>
<span data-ttu-id="62bf1-166">credenciales de Hola para cuenta de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="62bf1-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="62bf1-167">Ejemplo: - VMPassword @{nombre = "admin"; Contraseña = "contraseña"}</span><span class="sxs-lookup"><span data-stu-id="62bf1-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="62bf1-168">Alias</span><span class="sxs-lookup"><span data-stu-id="62bf1-168">Aliases</span></span> | <span data-ttu-id="62bf1-169">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="62bf1-170">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="62bf1-170">Required?</span></span> |<span data-ttu-id="62bf1-171">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-171">false</span></span> |
| <span data-ttu-id="62bf1-172">Posición</span><span class="sxs-lookup"><span data-stu-id="62bf1-172">Position</span></span> |<span data-ttu-id="62bf1-173">con nombre</span><span class="sxs-lookup"><span data-stu-id="62bf1-173">named</span></span> |
| <span data-ttu-id="62bf1-174">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="62bf1-174">Default value</span></span> |<span data-ttu-id="62bf1-175">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-175">none</span></span> |
| <span data-ttu-id="62bf1-176">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="62bf1-176">Accept pipeline input?</span></span> |<span data-ttu-id="62bf1-177">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-177">false</span></span> |
| <span data-ttu-id="62bf1-178">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="62bf1-178">Accept wildcard characters?</span></span> |<span data-ttu-id="62bf1-179">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="62bf1-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="62bf1-180">DatabaseServerPassword</span></span>
<span data-ttu-id="62bf1-181">Hola las credenciales de base de datos SQL de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="62bf1-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="62bf1-182">Ejemplo: - DatabaseServerPassword @{nombre = "admin"; Contraseña = "contraseña"}</span><span class="sxs-lookup"><span data-stu-id="62bf1-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="62bf1-183">Alias</span><span class="sxs-lookup"><span data-stu-id="62bf1-183">Aliases</span></span> | <span data-ttu-id="62bf1-184">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="62bf1-185">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="62bf1-185">Required?</span></span> |<span data-ttu-id="62bf1-186">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-186">false</span></span> |
| <span data-ttu-id="62bf1-187">Posición</span><span class="sxs-lookup"><span data-stu-id="62bf1-187">Position</span></span> |<span data-ttu-id="62bf1-188">con nombre</span><span class="sxs-lookup"><span data-stu-id="62bf1-188">named</span></span> |
| <span data-ttu-id="62bf1-189">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="62bf1-189">Default value</span></span> |<span data-ttu-id="62bf1-190">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-190">none</span></span> |
| <span data-ttu-id="62bf1-191">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="62bf1-191">Accept pipeline input?</span></span> |<span data-ttu-id="62bf1-192">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-192">false</span></span> |
| <span data-ttu-id="62bf1-193">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="62bf1-193">Accept wildcard characters?</span></span> |<span data-ttu-id="62bf1-194">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="62bf1-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="62bf1-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="62bf1-196">Si es true, imprimir mensajes de Hola script toohello flujo de salida.</span><span class="sxs-lookup"><span data-stu-id="62bf1-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="62bf1-197">Alias</span><span class="sxs-lookup"><span data-stu-id="62bf1-197">Aliases</span></span> | <span data-ttu-id="62bf1-198">Ninguna</span><span class="sxs-lookup"><span data-stu-id="62bf1-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="62bf1-199">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="62bf1-199">Required?</span></span> |<span data-ttu-id="62bf1-200">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-200">false</span></span> |
| <span data-ttu-id="62bf1-201">Posición</span><span class="sxs-lookup"><span data-stu-id="62bf1-201">Position</span></span> |<span data-ttu-id="62bf1-202">con nombre</span><span class="sxs-lookup"><span data-stu-id="62bf1-202">named</span></span> |
| <span data-ttu-id="62bf1-203">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="62bf1-203">Default value</span></span> |<span data-ttu-id="62bf1-204">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-204">false</span></span> |
| <span data-ttu-id="62bf1-205">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="62bf1-205">Accept pipeline input?</span></span> |<span data-ttu-id="62bf1-206">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-206">false</span></span> |
| <span data-ttu-id="62bf1-207">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="62bf1-207">Accept wildcard characters?</span></span> |<span data-ttu-id="62bf1-208">false</span><span class="sxs-lookup"><span data-stu-id="62bf1-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="62bf1-209">Comentarios</span><span class="sxs-lookup"><span data-stu-id="62bf1-209">Remarks</span></span>
<span data-ttu-id="62bf1-210">Para obtener una explicación completa de cómo toouse Hola script toocreate Dev y entornos de prueba, consulte [entornos de prueba y el uso de Scripts de Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="62bf1-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="62bf1-211">archivo de configuración de JSON de Hello especifica detalles de Hola de novedades toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="62bf1-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="62bf1-212">Incluye información de Hola que se especificó cuando creó el proyecto de hello, como nombre de hello, grupo de afinidad, imagen de disco duro virtual y el tamaño de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="62bf1-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="62bf1-213">También incluye los extremos de hello en la máquina virtual de hello, hello tooprovision de bases de datos, si procede y parámetros de implementación web.</span><span class="sxs-lookup"><span data-stu-id="62bf1-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="62bf1-214">Hola siguiente código muestra un archivo de configuración de JSON de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="62bf1-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="62bf1-215">Puede editar el archivo de configuración de hello JSON toochange lo que se aprovisiona.</span><span class="sxs-lookup"><span data-stu-id="62bf1-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="62bf1-216">Una máquina virtual y un servicio de nube son necesarias, pero la sección de la base de datos de hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="62bf1-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

