---
title: eventos de ciclo de vida de servicio de nube aaaHandle | Documentos de Microsoft
description: "Obtenga información acerca de cómo pueden usarse los métodos del ciclo de vida de Hola de un rol de servicio de nube en .NET"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Personalizar Hola del ciclo de vida de un rol Web o de trabajo en .NET
Cuando se crea un rol de trabajo, ampliar hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) clase que proporciona métodos de toooverride que le permite responder a eventos de toolifecycle. Para los roles web esta clase es opcional, por lo que debe usar toorespond toolifecycle eventos.

## <a name="extend-hello-roleentrypoint-class"></a>Extender la clase de hello RoleEntryPoint
Hola [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) clase incluye métodos que se llaman Azure cuando lo **inicia**, **ejecuta**, o **detiene** un rol web o de trabajo. Opcionalmente, puede invalidar estos métodos toomanage rol inicialización, secuencias de apagado de rol o subproceso de ejecución de Hola de rol de Hola. 

Al extender **RoleEntryPoint**, debe ser consciente de hello siguientes comportamientos de hello métodos:

* Hola [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) y [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) métodos devuelven un valor booleano, por lo que es posible tooreturn **false** de estos métodos.
  
   Si el código devuelve **false**, Hola rol proceso finaliza precipitadamente, sin ejecutar ninguna secuencia de cierre que pueda tener en su lugar. En general, se recomienda evitar devolver **false** de hello **OnStart** método.
* Cualquier excepción no detectada en una sobrecarga de un método **RoleEntryPoint** se trata como una excepción no controlada.
  
   Si se produce una excepción dentro de uno de los métodos del ciclo de vida de hello, Azure desencadenará hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) eventos, y, a continuación, se termina el proceso de Hola. Tras la desconexión del rol, se reiniciará Azure. Cuando una excepción no controlada se produce, hello [detener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) no se produce el evento y Hola **OnStop** no se llama el método.

Si el rol no se inicia o se recicla entre Hola inicializando, ocupados y deteniendo Estados, el código puede producir una excepción no controlada dentro de uno de los eventos de ciclo de vida de Hola que se reinicia cada rol de Hola de tiempo. En este caso, utilice hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) eventos toodetermine Hola a causa de la excepción de Hola y administrarla correctamente. Puede que su rol también se puede devolver desde hello [ejecutar](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método, que hace que Hola rol toorestart. Para obtener más información acerca de los Estados de implementación, consulte [tooRecycle problemas que causa Roles comunes](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

> [!NOTE]
> Si usas hello **Azure Tools para Microsoft Visual Studio** toodevelop su aplicación, plantillas de proyecto de rol de hello extienden automáticamente hello **RoleEntryPoint** clase Hola *WebRole.cs* y *WorkerRole.cs* archivos.
> 
> 

## <a name="onstart-method"></a>Método OnStart
Hola **OnStart** método se llama cuando la instancia de rol se pone en línea a Azure. Mientras se está ejecutando código de OnStart hello, instancia de rol de Hola se marca como **ocupado** y ningún tráfico externo será dirigido tooit equilibrador de carga de Hola. Puede invalidar este trabajo de inicialización tooperform de método, como implementar controladores de eventos e iniciar [diagnósticos de Azure](cloud-services-how-to-monitor.md).

Si **OnStart** devuelve **true**, Hola instancia se inicializó correctamente y Azure llama hello **RoleEntryPoint.Run** método. Si **OnStart** devuelve **false**, rol de hello termina inmediatamente, sin ejecutar las secuencias de apagado planeado.

Hola siguiendo el ejemplo de código muestra cómo hello toooverride **OnStart** método. Este método configura e inicia el monitor de diagnóstico cuando la instancia de rol de Hola se inicia y se configura una transferencia del inicio de sesión de cuenta de almacenamiento de datos tooa:

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>Método OnStop
Hola **OnStop** método se llama después de una instancia de rol se ha desconectado por Azure y antes de que salga del proceso de Hola. Puede reemplazar este código de toocall método necesario para su toocleanly de instancia de rol apagar.

> [!IMPORTANT]
> Código que se ejecuta en hello **OnStop** método tiene un período de tiempo limitado toofinish cuando se llama por motivos distintos a un cierre iniciado por el usuario. Después de transcurrido este tiempo, Hola proceso finaliza, debe asegurarse de que el código de hello **OnStop** método puede ejecutarse rápidamente o que tolera toocompletion no se está ejecutando. Hola **OnStop** método se llama después de hello **detener** evento se desencadena.
> 
> 

## <a name="run-method"></a>Método Run
Puede invalidar hello **ejecutar** método tooimplement un subproceso de ejecución prolongada para la instancia de rol.

Reemplazar hello **ejecutar** método no es necesario; la implementación predeterminada de hello inicia un subproceso que se mantiene en espera indefinidamente. Si invalida hello **ejecutar** método, el código debe bloquearse indefinidamente. Si hello **ejecutar** método devuelve, rol Hola se recicla automáticamente sin problemas; es decir, Azure desencadena hello **detener** Hola eventos y llamadas **OnStop** método para que se puedan ejecutar las secuencias de cierre antes Hola rol se quede sin conexión.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Implementar métodos de ciclo de vida ASP.NET de Hola para un rol web
Puede utilizar métodos de ciclo de vida ASP.NET de hello, además proporciona hello toothose **RoleEntryPoint** de la clase, las secuencias de inicialización y cierre de toomanage para un rol web. Esto puede ser útil con fines de compatibilidad si va a trasladar una tooAzure de aplicación de ASP.NET existente. métodos de ciclo de vida ASP.NET de Hola se llaman desde dentro de hello **RoleEntryPoint** métodos. Hola **aplicación\_iniciar** método se llama después de hello **RoleEntryPoint.OnStart** método finaliza. Hola **aplicación\_final** método se llama antes de hello **RoleEntryPoint.OnStop** se llama al método.

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo demasiado[crear un paquete de servicios de nube](cloud-services-model-and-package.md).

