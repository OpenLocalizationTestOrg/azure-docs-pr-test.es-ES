---
title: "tamaño de la carpeta TEMP aaaDefault es demasiado pequeño para un rol | Documentos de Microsoft"
description: "Un rol de servicio de nube tiene una cantidad limitada de espacio para la carpeta TEMP de Hola. Este artículo proporciona algunas sugerencias sobre cómo tooavoid quedando sin espacio."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="52842-104">El tamaño predeterminado de la carpeta TEMP es demasiado pequeño en un rol de trabajo o web de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="52842-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="52842-105">Hola de forma predeterminada, el directorio temporal de un rol de trabajador o web de servicio de nube tiene un tamaño máximo de 100 MB, lo que puede afectar completa en algún momento.</span><span class="sxs-lookup"><span data-stu-id="52842-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="52842-106">Este artículo se describe cómo tooavoid quedando sin espacio para el directorio temporal de Hola.</span><span class="sxs-lookup"><span data-stu-id="52842-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="52842-107">¿Por qué me quedo sin espacio?</span><span class="sxs-lookup"><span data-stu-id="52842-107">Why do I run out of space?</span></span>
<span data-ttu-id="52842-108">Hola estándar Windows variables de entorno TEMP y TMP están disponible toocode que se ejecuta en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52842-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="52842-109">TEMP y TMP señalan tooa único directorio que tiene un tamaño máximo de 100 MB.</span><span class="sxs-lookup"><span data-stu-id="52842-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="52842-110">Los datos que se almacenen en este directorio no se conservan entre Hola del ciclo de vida del servicio de nube de hello; Si se reciclan instancias de rol de hello en un servicio de nube, se limpia directory Hola.</span><span class="sxs-lookup"><span data-stu-id="52842-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="52842-111">Problema de sugerencia toofix Hola</span><span class="sxs-lookup"><span data-stu-id="52842-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="52842-112">Implementar uno de hello siguientes alternativas:</span><span class="sxs-lookup"><span data-stu-id="52842-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="52842-113">Configure un recurso de almacenamiento local y acceda a él directamente, en lugar de usar TEMP o TMP.</span><span class="sxs-lookup"><span data-stu-id="52842-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="52842-114">un recurso de almacenamiento local desde el código que se ejecuta dentro de la aplicación, llamada hello tooaccess [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="52842-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="52842-115">Configurar un recurso de almacenamiento local y para señalar hello TEMP y TMP directorios toopoint toohello ruta de acceso del recurso de almacenamiento local de Hola.</span><span class="sxs-lookup"><span data-stu-id="52842-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="52842-116">Se debe realizar esta modificación en hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="52842-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="52842-117">Hello ejemplo de código siguiente muestra cómo toomodify Hola directorios de destino para TEMP y TMP en el método OnStart de hello:</span><span class="sxs-lookup"><span data-stu-id="52842-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="52842-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52842-118">Next steps</span></span>
<span data-ttu-id="52842-119">Leer un blog que describe [cómo tooincrease Hola tamaño de carpeta temporal de ASP.NET de rol de Azure Web hello](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="52842-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="52842-120">Vea más [artículos de solución de problemas](/?tag=top-support-issue&product=cloud-services) para servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="52842-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="52842-121">toolearn cómo rol de servicio de nube tootroubleshoot problemas mediante el uso de datos de diagnóstico del equipo de PaaS de Azure, ver [serie de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="52842-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
