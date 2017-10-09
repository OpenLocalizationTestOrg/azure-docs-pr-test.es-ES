---
title: hace que aaaCommon de reciclaje de roles de servicio en la nube | Documentos de Microsoft
description: Un rol del servicio en la nube que se recicla repentinamente puede causar un considerable tiempo de inactividad. Estas son algunas causas comunes que provocan toobe roles reciclada, que puede ayudar a reducir el tiempo de inactividad.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>Problemas comunes que hacen toorecycle de roles
En este artículo se describen algunas de las causas comunes de problemas de implementación de Hola y proporciona sugerencias de solución de problemas toohelp resolver estos problemas. Una indicación de que existe un problema con una aplicación es cuando se produce un error en la instancia de rol de hello toostart, o cuando entra en los Estados de inicializar, ocupado y deteniendo Hola.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>Dependencias en tiempo de ejecución que faltan
Si un rol de la aplicación se basa en cualquier ensamblado que no forma parte del programa Hola biblioteca administrada de .NET Framework o hello Azure, debe incluir explícitamente ese ensamblado en paquete de aplicación Hola. Tenga presente que otros marcos de trabajo de Microsoft no están disponibles en Azure de forma predeterminada. Si su rol se basa en un marco de trabajo, debe agregar el paquete de la aplicación toohello de esos ensamblados.

Antes de compilar y empaquetar la aplicación, compruebe Hola siguiente:

* Si utiliza Visual studio, que seguro Hola **Copy Local** propiedad se establece demasiado**True** para cada uno de ellos al que hace referencia el ensamblado en el proyecto que no forma parte del programa Hola a Azure SDK u Hola .NET Framework.
* Asegúrese de que el archivo web.config de hello no hace referencia a los ensamblados no usados en el elemento de compilación de Hola.
* Hola **acción de compilación** de cada .cshtml se establece demasiado archivo**contenido**. Esto garantiza que los archivos Hola aparezcan correctamente en el paquete de Hola y permite que otros tooappear de archivos que se hace referencia en el paquete de Hola.

## <a name="assembly-targets-wrong-platform"></a>El ensamblado tiene como destino la plataforma equivocada
Azure es un entorno de 64 bits. Por lo tanto, los ensamblados de .NET compilados para un destino de 32 bits no funcionarán en Azure.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>El rol genera excepciones no controladas cuando se inicializa o se detiene
Las excepciones producidas por los métodos de Hola de hello [RoleEntryPoint] (clase), que incluye hello [OnStart], [OnStop], y [ejecutar]métodos, son las excepciones no controladas. Si se produce una excepción no controlada en uno de estos métodos, se reciclará el rol de Hola. Si el rol de Hola se recicla de forma repetida, puede producir una excepción no controlada cada vez que intente toostart.

## <a name="role-returns-from-run-method"></a>El rol se devuelve del método Run
Hola [ejecutar] método está previsto toorun indefinidamente. Si el código invalida hello [ejecutar] método, debe estar en espera indefinidamente. Si hello [ejecutar] método vuelve, Hola rol se recicla.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>Configuración incorrecta de DiagnosticsConnectionString
Si la aplicación utiliza diagnóstico de Azure, el archivo de configuración de servicio debe especificar hello `DiagnosticsConnectionString` opción de configuración. Este valor debe especificar una cuenta de almacenamiento de tooyour de conexión HTTPS en Azure.

tooensure que su `DiagnosticsConnectionString` configuración sea correcta antes de implementar su tooAzure de paquete de aplicación, compruebe Hola siguiente:  

* Hola `DiagnosticsConnectionString` establecer puntos de cuenta de almacenamiento válida tooa en Azure.  
  De forma predeterminada, este valor apunta toohello emulada cuenta de almacenamiento, por lo que se debe cambiar explícitamente esta configuración antes de implementar el paquete de aplicación. Si no cambia esta configuración, se produce una excepción cuando trate de instancia de rol de hello toostart monitor de diagnóstico de Hola. Esto puede provocar toorecycle de instancia de rol de hello indefinidamente.
* Hello especifica cadena de conexión es siguiente hello [formato](../storage/common/storage-configure-connection-string.md). (el protocolo de hello debe especificarse como HTTPS). Reemplace *MyAccountName* con el nombre de saludo de la cuenta de almacenamiento y *MyAccountKey* con su clave de acceso:    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  Si está desarrollando la aplicación con Azure Tools para Microsoft Visual Studio, puede usar tooset de páginas de propiedades de hello este valor.

## <a name="exported-certificate-does-not-include-private-key"></a>El certificado exportado no incluye una clave privada
toorun un rol web con SSL, debe asegurarse de que el certificado de administración exportado incluye la clave privada de Hola. Si usas hello *Administrador de certificados de Windows* tooexport certificado de hello, ser seguro tooselect **Sí** para hello **clave privada de exportación hello** opción. certificado de Hello debe exportarse en formato PFX de hello, que es Hola formato solo admitida actualmente.

## <a name="next-steps"></a>Pasos siguientes
Vea más [artículos de solución de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para servicios en la nube.

En la [series de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)puede ver más escenarios de reciclaje de roles.

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[ejecutar]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
