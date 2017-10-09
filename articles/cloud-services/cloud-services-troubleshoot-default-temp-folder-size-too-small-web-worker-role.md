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
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>El tamaño predeterminado de la carpeta TEMP es demasiado pequeño en un rol de trabajo o web de servicio en la nube.
Hola de forma predeterminada, el directorio temporal de un rol de trabajador o web de servicio de nube tiene un tamaño máximo de 100 MB, lo que puede afectar completa en algún momento. Este artículo se describe cómo tooavoid quedando sin espacio para el directorio temporal de Hola.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>¿Por qué me quedo sin espacio?
Hola estándar Windows variables de entorno TEMP y TMP están disponible toocode que se ejecuta en la aplicación. TEMP y TMP señalan tooa único directorio que tiene un tamaño máximo de 100 MB. Los datos que se almacenen en este directorio no se conservan entre Hola del ciclo de vida del servicio de nube de hello; Si se reciclan instancias de rol de hello en un servicio de nube, se limpia directory Hola.

## <a name="suggestion-toofix-hello-problem"></a>Problema de sugerencia toofix Hola
Implementar uno de hello siguientes alternativas:

* Configure un recurso de almacenamiento local y acceda a él directamente, en lugar de usar TEMP o TMP. un recurso de almacenamiento local desde el código que se ejecuta dentro de la aplicación, llamada hello tooaccess [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.
* Configurar un recurso de almacenamiento local y para señalar hello TEMP y TMP directorios toopoint toohello ruta de acceso del recurso de almacenamiento local de Hola. Se debe realizar esta modificación en hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) método.

Hello ejemplo de código siguiente muestra cómo toomodify Hola directorios de destino para TEMP y TMP en el método OnStart de hello:

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

## <a name="next-steps"></a>Pasos siguientes
Leer un blog que describe [cómo tooincrease Hola tamaño de carpeta temporal de ASP.NET de rol de Azure Web hello](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Vea más [artículos de solución de problemas](/?tag=top-support-issue&product=cloud-services) para servicios en la nube.

toolearn cómo rol de servicio de nube tootroubleshoot problemas mediante el uso de datos de diagnóstico del equipo de PaaS de Azure, ver [serie de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
