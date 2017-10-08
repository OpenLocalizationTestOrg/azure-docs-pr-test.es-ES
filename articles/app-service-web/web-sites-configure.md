---
title: "aaaConfigure las aplicaciones web en el servicio de aplicación de Azure"
description: "¿Cómo tooconfigure una aplicación web en servicios de aplicaciones de Azure"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a>Configuración de aplicaciones web en el Servicio de aplicaciones de Azure
Este tema explica cómo Hola tooconfigure una aplicación web con [Portal de Azure].

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>Configuración de la aplicación
1. Hola [Portal de Azure], abra hoja hello para la aplicación web de Hola.
2. Haga clic en **Toda la configuración**.
3. Haga clic en **Configuración de la aplicación**.

![Configuración de la aplicación][configure01]

Hola **configuración de la aplicación** hoja se agrupan en varias categorías de configuración.

### <a name="general-settings"></a>Configuración general
**Versiones del marco**. Configure estas opciones si su aplicación utiliza cualquiera de estos marcos: 

* **.NET framework**: versión de .NET framework de conjunto Hola. 
* **PHP**: versión de PHP de conjunto hello, o **OFF** toodisable PHP. 
* **Java**: versión de Java de hello Select o **OFF** toodisable Java. Hola de uso **contenedor Web** toochoose opción entre las versiones de Tomcat y Jetty.
* **Python**: versión de Python seleccione hello, o **OFF** toodisable Python.

Por razones técnicas, si se habilita Java para la aplicación, deshabilita las opciones. NET, PHP y Python de Hola.

<a name="platform"></a>
**Plataforma**. Seleccione si su aplicación web se ejecuta en un entorno de 32 o 64 bits. entorno de 64 bits de Hello requiere el modo básico o estándar. Los modos libre y compartido siempre se ejecutan en un entorno de 32 bits.

**Sockets web**. Establecer **ON** tooenable Hola protocolo WebSocket; por ejemplo, si su aplicación web usa [ASP.NET SignalR] o [socket.io].

<a name="alwayson"></a>
**AlwaysOn**. De forma predeterminada, las aplicaciones web se descargan si están inactivas durante algún tiempo. Esto permite que el sistema de hello conservar los recursos. En el modo básico o estándar, puede habilitar **Always On** tookeep Hola aplicación carga todo el tiempo Hola. Si la aplicación ejecuta trabajos Web continuos o se ejecuta trabajos Web desencadena mediante una expresión CRON, debe habilitar **Always On**, o trabajos de hello web no pueden ejecutar de forma confiable.

**Versión de canalización administrada**. Conjuntos de Hola IIS [el modo de canalización]. Deje este conjunto tooIntegrated (valor predeterminado de hello) a menos que tenga una aplicación heredada que requiere una versión anterior de IIS.

**Intercambio automático**. Si habilita el intercambio automático de una ranura de implementación, servicio de aplicaciones automáticamente intercambiará aplicación web de hello en producción cuando realice una inserción una ranura de toothat de actualización. Para obtener más información, consulte [implementar toostaging ranuras de las aplicaciones web de servicio de aplicaciones de Azure](web-sites-staged-publishing.md).

### <a name="debugging"></a>Depuración
**Depuración remota**. Habilita la depuración remota. Cuando está habilitada, puede utilizar a depurador remoto hello en Visual Studio tooconnect directamente tooyour aplicación web. La depuración remota permanecerá habilitada durante 48 horas. 

### <a name="app-settings"></a>Configuración de la aplicación
Esta sección contiene las parejas de nombre y valor que la aplicación web cargará al inicio. 

* En las aplicaciones .NET, estas configuraciones se insertarán en la sección de la configuración de .NET `AppSettings` en tiempo de ejecución y reemplazará la configuración existente. 
* Las aplicaciones PHP, Python, Java y Node pueden acceder a estas configuraciones como variables de entorno en tiempo de ejecución. Para cada configuración de la aplicación, se crean dos variables de entorno; uno con el nombre de hello especificado por la entrada de configuración de aplicación hello y otro con el prefijo APPSETTING_. Ambos contienen Hola mismo valor.

### <a name="connection-strings"></a>Cadenas de conexión
Cadenas de conexión para los recursos vinculados. 

Para las aplicaciones. NET, estas cadenas de conexión se insertan en la configuración de .NET `connectionStrings` configuración en tiempo de ejecución, invalidando las entradas existentes que sea igual que la clave de Hola Hola nombre vinculado de la base de datos. 

Para las aplicaciones PHP, Python, Java y Node, esta configuración estará disponible como variables de entorno en tiempo de ejecución, el prefijo con el tipo de conexión de Hola. prefijos de variable de entorno de Hello son los siguientes: 

* SQL Server: `SQLCONNSTR_`
* MySQL: `MYSQLCONNSTR_`
* Base de datos SQL: `SQLAZURECONNSTR_`
* Personalizado: `CUSTOMCONNSTR_`

Por ejemplo, si una cadena de conexión de MySql se denomina `connectionstring1`, podría tener acceso a ella a través de la variable de entorno de hello `MYSQLCONNSTR_connectionString1`.

### <a name="default-documents"></a>Documentos predeterminados
documento predeterminado de Hello es hello web página que se muestra en la dirección URL raíz de Hola para un sitio Web.  se utiliza el primer archivo coincidente Hello en lista de Hola. 

Es posible que las aplicaciones utilicen módulos que enruten en base a la URL, en lugar de ofrecer funcionalidad a contenido estático, en cuyo caso no existe realmente un documento predeterminado.    

### <a name="handler-mappings"></a>Asignaciones de controlador
Usar este solicitudes de toohandle de procesadores de script personalizado de área tooadd para determinadas extensiones de archivo. 

* **Extensión**. Controla el toobe de extensión de archivo Hello, por ejemplo, *.php o handler.fcgi. 
* **Ruta de acceso del procesador de script**. Hola ruta de acceso absoluta del procesador de script de Hola. Procesador de script de Hola procesará toofiles las solicitudes que coinciden con la extensión de archivo Hola. Usar ruta de acceso de hello `D:\home\site\wwwroot` directorio raíz de la aplicación de toorefer tooyour.
* **Argumentos adicionales**. Argumentos de línea de comandos opcionales para el procesador de script de Hola 

### <a name="virtual-applications-and-directories"></a>Directorios y aplicaciones virtuales
tooconfigure de aplicaciones virtuales y directorios, especifique cada directorio virtual y su correspondiente raíz del sitio Web de toohello relativa de ruta de acceso física. Si lo desea, puede seleccionar hello **aplicación** casilla toomark un directorio virtual como una aplicación.

## <a name="enabling-diagnostic-logs"></a>Habilitación de registros de diagnóstico
registros de diagnóstico de tooenable:

1. En la hoja de hello para la aplicación web, haga clic en **toda la configuración de**.
2. Haga clic en **Registros de diagnóstico**. 

Opciones para escribir registros de diagnóstico de una aplicación web que admita el registro: 

* **Registro de aplicaciones**. Escribe registros de la aplicación de sistema de archivos de toohello. El registro dura un período de 12 horas. 

**Nivel**. Cuando se habilita el registro de aplicación, esta opción especifica la cantidad de Hola de información que será registrados (Error, advertencia, información o detallado).

**Registro del servidor web**. Los registros se guardan en formato de archivo de registro extendido W3C de Hola. 

**Mensajes de error detallados**. Guarda archivos .htm de mensajes de error detallados. Hola archivos se guardan en /LogFiles/DetailedErrors. 

**Seguimiento de solicitudes erróneas**. Registros de error en las solicitudes tooXML archivos. Hola se guardan los archivos bajo/LogFiles/W3SVC*xxx*, donde xxx es un identificador único. Esta carpeta contiene un archivo XSL y uno o varios archivos XML. Asegúrese de Hola de toodownload seguro archivo XSL, porque proporciona la funcionalidad para dar formato y filtrar el contenido de Hola Hola de archivos de XML.

archivos de registro de hello tooview, debe crear las credenciales FTP, como se indica a continuación:

1. En la hoja de hello para la aplicación web, haga clic en **toda la configuración de**.
2. Haga clic en **Credenciales de implementación**.
3. Escriba un nombre de usuario y una contraseña.
4. Haga clic en **Guardar**.

![Configurar credenciales de implementación][configure03]

nombre de usuario FTP completo Hello es "app\username" donde *aplicación* es Hola nombre de la aplicación web. Hello nombre de usuario aparece en la hoja de la aplicación hello web, en **Essentials**.  

![Credenciales de implementación de FTP][configure02]

## <a name="other-configuration-tasks"></a>Otras tareas de configuración
### <a name="ssl"></a>SSL
En modo básico o estándar puede cargar certificados SSL para un dominio personalizado. Para más información, consulte [Habilitación de HTTPS para una aplicación web]. 

tooview los certificados cargados, haga clic en ejecutar **toda la configuración de** > **los dominios personalizados y SSL**.

### <a name="domain-names"></a>Nombres de dominio
Agregue nombres de dominio personalizados para su aplicación web. Para más información, consulte [Configuración de un nombre de dominio personalizado para una aplicación web en el servicio de aplicaciones de Azure].

tooview sus nombres de dominio, haga clic en ejecutar **toda la configuración de** > **los dominios personalizados y SSL**.

### <a name="deployments"></a>Implementaciones
* Configure la implementación continua. Vea [toodeploy Git usando las aplicaciones Web en el servicio de aplicación de Azure](web-sites-deploy.md).
* Ranuras de implementación. Vea [implementar entornos de tooStaging para las aplicaciones Web en el servicio de aplicación de Azure].

tooview las ranuras de implementación, haga clic en ejecutar **toda la configuración de** > **ranuras de implementación**.

### <a name="monitoring"></a>Supervisión
En el modo básico o estándar, puede probar la disponibilidad Hola de extremos HTTP o HTTPS, desde ubicaciones distribuidas geográficamente de toothree. Se produce un error en una prueba de supervisión si Hola código de respuesta HTTP es un error (4xx o 5xx) o respuesta de hello tarda más de 30 segundos. Un punto de conexión se considera disponible si pruebas de supervisión de hello sean correctas de todos los Hola especificado ubicaciones. 

Para obtener más información, consulte [Supervisión de estado de extremo web].

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones], donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure]
* [Habilitación de HTTPS para una aplicación en el servicio de aplicaciones de Azure]
* [Escalación de una aplicación web en el Servicio de aplicaciones de Azure]
* [Aspectos básicos de supervisión para las aplicaciones web en Servicio de aplicaciones de Azure]

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Portal de Azure]: https://portal.azure.com/
[Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure]: ./app-service-web-tutorial-custom-domain.md
[implementar entornos de tooStaging para las aplicaciones Web en el servicio de aplicación de Azure]: ./web-sites-staged-publishing.md
[Habilitación de HTTPS para una aplicación en el servicio de aplicaciones de Azure]: ./app-service-web-tutorial-custom-ssl.md
[Supervisión de estado de extremo web]: http://go.microsoft.com/fwLink/?LinkID=279906
[Aspectos básicos de supervisión para las aplicaciones web en Servicio de aplicaciones de Azure]: ./web-sites-monitor.md
[el modo de canalización]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Escalación de una aplicación web en el Servicio de aplicaciones de Azure]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[pruebe el servicio de aplicaciones]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
