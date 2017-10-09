---
title: roles de aaaTroubleshoot que no se toostart | Documentos de Microsoft
description: "A continuación figuran algunas causas habituales por qué un rol de servicio de nube puede producir un error toostart. También se proporcionan soluciones problemas de toothese."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Solucionar problemas de los roles de servicio en la nube que no se toostart
Estos son algunos problemas comunes y los roles de servicios en la nube de tooAzure relacionados de soluciones que no se toostart.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>DLL o dependencias que faltan
Tanto que los roles no respondan como que alternen entre los estados **Inicializando**, **Ocupado** y **Deteniendo** puede deberse a que faltan DLL o ensamblados.

Estos son los síntomas de que faltan DLL o ensamblados:

* Una instancia de rol alterna entre los estados **Inicializando**, **Ocupado** y **Deteniendo**.
* La instancia de rol se movió demasiado**listo** pero si navega aplicación web de tooyour, no aparece la página de Hola.

Hay varios métodos recomendados para investigar estos problemas.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>Diagnóstico del problema de DLL que faltan en un rol web
Cuando vaya sitio Web de tooa que se implementa en un rol web y Explorador de hello muestra un servidor error similar toohello después, puede indicar que un archivo DLL es que faltan.

![Error del servidor en la aplicación '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>Diagnóstico de problemas mediante la desactivación de errores personalizados
Información de error más completa puede verse mediante la configuración de web.config de Hola para hello web rol tooset Hola errores personalizados modo tooOff y volver a implementar el servicio de Hola.

tooview complete más errores sin utilizar Escritorio remoto:

1. Abra la solución de hello en Microsoft Visual Studio.
2. Hola **el Explorador de soluciones**, busque el archivo web.config de hello y ábralo.
3. En el archivo web.config de hello, busque la sección system.web de Hola y agregue Hola después de línea:

    ```xml
    <customErrors mode="Off" />
    ```
4. Guarde el archivo hello.
5. Volver a empaquetar e implementar el servicio de Hola.

Una vez que se vuelve a implementar el servicio de hello, verá un mensaje de error con el nombre de Hola de hello falta el ensamblado o una DLL.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>Diagnosticar problemas comprobando error Hola de forma remota
Puede usar Escritorio remoto tooaccess Hola rol y ver información de error más completa de forma remota. Use Hola siguientes pasos le indican errores de hello tooview mediante Escritorio remoto:

1. Asegúrese de que está instalado el SDK 1.3 de Azure, o una versión posterior.
2. Durante la implementación de Hola de solución de hello mediante Visual Studio, elija demasiado "Conexiones a Escritorio remoto configurar …". Para obtener más información sobre la configuración de conexión a Escritorio remoto hello, consulte [usar Escritorio remoto con Roles de Azure](../vs-azure-tools-remote-desktop-roles.md).
3. En hello clásico portal de Microsoft Azure, una vez que la instancia de hello muestra un estado de **listo**, haga clic en una de las instancias de rol de Hola.
4. Haga clic en hello **conectar** icono Hola **acceso remoto** área no cliente de la cinta de opciones de Hola.
5. Inicie sesión en la máquina virtual de toohello mediante credenciales de Hola que se especificaron durante la configuración de escritorio remoto de Hola.
6. Abra el símbolo del sistema.
7. Escriba `IPconfig`.
8. Anote el valor de la dirección IPV4 de Hola.
9. Abra Internet Explorer.
10. Escriba la dirección de Hola y el nombre de Hola de aplicación web de Hola. Por ejemplo: `http://<IPV4 Address>/default.aspx`.

Navegar por toohello sitio Web devolverá ahora más explícitos mensajes de error:

* Error del servidor en la aplicación '/'
* Descripción: Se produjo una excepción no controlada durante la ejecución de saludo de solicitud web actual de Hola. Revise el seguimiento de la pila de Hola para obtener más información sobre el error de Hola y dónde se originó en el código de hello.
* Detalles de la excepción: System.IO.FIleNotFoundException: No se puede cargar el archivo o ensamblado ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ ni una de sus dependencias. sistema de Hello no encuentra el archivo hello especificado.

Por ejemplo:

![Error explícito del servidor en la aplicación '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Diagnosticar problemas con el emulador de proceso de Hola
Puede usar Hola Microsoft Azure compute emulator toodiagnose y solucionar los problemas de falta de dependencias y errores en web.config.

Para obtener unos mejores resultados con este método de diagnóstico, debe usar un equipo o máquina virtual que tenga una instalación limpia de Windows. toobest simular Hola entorno de Azure, use Windows Server 2008 R2 x64.

1. Instalar la versión independiente de Hola de hello [Azure SDK](https://azure.microsoft.com/downloads/).
2. En el equipo de desarrollo de hello, compile el proyecto de servicio de nube de Hola.
3. En el Explorador de Windows, desplazarse por las carpetas de toohello bin\debug del proyecto de servicio de nube de Hola.
4. Copie la carpeta de .csx de Hola y el equipo de toohello de archivo de .cscfg que utilizas problemas de hello toodebug.
5. En hello limpieza máquina, abra una ventana de símbolo del sistema de SDK de Azure y un tipo `csrun.exe /devstore:start`.
6. En hello símbolo del sistema, escriba `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.
7. Cuando se inicia el rol de hello, verá información detallada del error en Internet Explorer. También puede usar herramientas para solucionar problemas de Windows estándares toofurther diagnosticar el problema de Hola.

## <a name="diagnose-issues-by-using-intellitrace"></a>Diagnóstico de problemas mediante IntelliTrace
Para los roles web y de trabajo que usan .NET Framework 4, puede usar [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), que está disponible en Microsoft Visual Studio Enterprise.

Siga estos servicios de hello toodeploy pasos con IntelliTrace habilitado:

1. Confirme que está instalado el SDK 1.3 de Azure, o una versión posterior.
2. Implementar soluciones de hello mediante Visual Studio. Durante la implementación, compruebe hello **Habilitar IntelliTrace para roles de .NET 4** casilla de verificación.
3. Una vez que se inicia la instancia de hello, abra hello **Explorador de servidores**.
4. Expanda hello **Azure\\servicios en la nube** nodo y busque la implementación de Hola.
5. Expandir la implementación de hello hasta que vea instancias de rol de Hola. Haga doble clic en una de las instancias de Hola.
6. Elija **Ver registros de IntelliTrace**. Hola **resumen de IntelliTrace** se abrirá.
7. Busque la sección de excepciones de Hola de hello resumen. Si hay excepciones, se denominará sección hello **datos de excepción**.
8. Expanda hello **datos de excepción** y busque **System.IO.FileNotFoundException** siguiente toohello similar de errores:

![Datos de excepción, faltan archivo o ensamblado](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>Tratamiento de archivos DLL y ensamblados que faltan
tooaddress falta errores de DLL y ensamblados, siga estos pasos:

1. Abra la solución de hello en Visual Studio.
2. En **el Explorador de soluciones**, abra hello **referencias** carpeta.
3. Haga clic en ensamblado hello identificado en error Hola.
4. Hola **propiedades** panel, busque **propiedad Copy Local** y establezca el valor de hello demasiado**True**.
5. Vuelva a implementar el servicio de nube de Hola.

Una vez haya comprobado que se han solucionado todos los errores, puede implementar el servicio de hello sin comprobar hello **Habilitar IntelliTrace para roles de .NET 4** casilla de verificación.

## <a name="next-steps"></a>Pasos siguientes
Vea más [artículos de solución de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para servicios en la nube.

toolearn cómo emite tootroubleshoot rol de servicio de nube mediante el uso de datos de diagnóstico del equipo de PaaS de Azure, consulte [serie de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
