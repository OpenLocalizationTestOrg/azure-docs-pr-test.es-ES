---
title: "aaaCreate una aplicación de chat de Node.js con Socket.IO en el servicio de aplicación de Azure"
description: "Este tutorial muestra el uso de socket.io en una aplicación web node.js hospedada en Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Creación de una aplicación de chat Node.js con Socket.IO en el Servicio de aplicaciones de Azure
Socket.IO proporciona comunicación en tiempo real entre su servidor node.js y los clientes con WebSockets. También es compatible con los transportes de reserva tooother (por ejemplo, el sondeo prolongado) que funcionan con los exploradores más antiguos. Este tutorial se le guían a través de aloja una aplicación de chat Socket.IO según como una aplicación web de Azure y le muestran cómo tooscale Hola aplicación usando [Azure Redis Cache]. Para obtener más información sobre Socket.IO, consulte <http://socket.io/>.

> [!NOTE]
> procedimientos de Hello en esta tarea se aplican demasiado[aplicación del servicio de aplicaciones Web]; para servicios en la nube, consulte [compilar una aplicación de Chat de Node.js con Socket.IO en un servicio de nube de Azure].
> 
> 

## <a name="download-hello-chat-example"></a>Descargar el ejemplo de Hola chat
Para este proyecto, usaremos hello (ejemplo) chat de hello [repositorio de Socket.IO GitHub]. Realizar Hola siguiente ejemplo de Hola toodownload de pasos y Agregar proyecto toohello que creó anteriormente.

1. Descargar un [ZIP o GZ archivado versión] del proyecto de hello Socket.IO (versión 1.3.5 se utilizó para este documento)
2. Extraer Hola Hola de archivo y copia **ejemplos\\chat** tooa nueva ubicación de directorio. Por ejemplo, **\\nodo\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Modificación de app.js e instalación de módulos
1. Cambiar el nombre de hello **index.js** archivo demasiado**app.js**. Esto permite que toodetect de Azure que se trata de una aplicación Node.js.
2. Abra hello **app.js** archivo en un editor de texto. Que contiene la línea de saludo de cambio `var io = require('../..')(server);` tal y como se muestra a continuación:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Abra hello **package.json** de archivos y agregue un toosocket.io de referencia en `dependencies`, tal y como se muestra a continuación:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Desde la línea de comandos de hello, cambiar toohello  **\\nodo\\chat** directorio y uso tooinstall Hola módulos npm requeridos por la aplicación:
   
        npm install
   
    Este modo se instalará módulos hello en una subcarpeta denominada **node_modules**.

## <a name="create-an-azure-web-app"></a>Creación de una aplicación web de Azure
Siga estos toocreate pasos una aplicación web de Azure, habilitar la publicación de Git y, a continuación, habilitar la compatibilidad de WebSocket para la aplicación web de Hola.

> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Evaluación gratuita de Azure</a>.
> 
> 

1. Instale hello Azure interfaz de línea de comandos (CLI de Azure) y conecte tooyour suscripción de Azure. Vea [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).
2. Si se trata de la primera configuración de tiempo de un repositorio de Azure, necesita credenciales de inicio de sesión de toocreate. En el saludo CLI de Azure, escriba Hola siguiente comando:
   
        azure site deployment user set [username] [password]
3. Cambiar toohello  **\\node\chat** directorio y siguientes de Hola de uso de comandos toocreate una nueva aplicación web de Azure y un repositorio Git local. Este comando también crea un Git remoto llamado "azure".
   
        azure site create mysitename --git
   
    Debe reemplazar "mysitename" por un nombre único para su sitio web.
4. Confirmar repositorio local de hello existente archivos toohello mediante el uso de hello siguientes comandos:
   
        git add .
        git commit -m "Initial commit"
5. Insertar repositorio de aplicaciones Web de Azure de hello archivos toohello con hello siguiente comando:
   
        git push azure master
   
    Cuando se le solicite, escriba las credenciales del paso 2. Recibirá mensajes de estado de los módulos se importan en el servidor de Hola. Cuando haya completado este proceso, la aplicación hello se hospedará en la aplicación web de Azure.
   
   > [!NOTE]
   > Durante la instalación del módulo, es podrán que encuentre errores que ' hello proyecto importado... no se encontró '. Se pueden ignorar con seguridad.
   > 
   > 
6. Socket.IO usa WebSockets, que no están habilitados de manera predeterminada en Azure. tooenable web sockets, Hola de uso siguiente comando:
   
        azure site set -w
   
    Si se le pide, escriba el nombre de Hola de aplicación web de hello.
   
   > [!NOTE]
   > Hola will de comando 'sitio de azure set -w' sólo funcionan con la versión 0.7.4 o posterior del programa Hola a la interfaz de línea de comandos de Azure. También puede habilitar la compatibilidad de WebSocket con hello [Portal de Azure](https://portal.azure.com).
   > 
   > uso de WebSockets de tooenable Hola Portal de Azure, haga clic en la aplicación web de hello de hoja de aplicaciones Web de hello, haga clic en **toda la configuración de** > **configuración de la aplicación**. En **Web Sockets**, haga clic en **Activado**. A continuación, haga clic en **Guardar**.
   > 
   > 
7. tooview hello web aplicación en Azure, use a continuación Hola comando toolaunch el explorador web y navegar por la aplicación web de toohello hospedado:
   
        azure site browse

Su aplicación se está ejecutando ahora en Azure y puede retransmitir los mensajes de chat entre los diferentes clientes que usan Socket.IO.

## <a name="scale-out"></a>Escalado horizontal
Aplicaciones de Socket.IO se pueden escalar horizontalmente mediante el uso de un **adaptador** toodistribute mensajes y eventos entre varias instancias de aplicación. Aunque hay varios adaptadores, Hola [socket.io redis] adaptador se puede usar fácilmente con la característica de caché en Redis de Azure de Hola.

> [!NOTE]
> Un requisito adicional para el escalado horizontal de una solución Socket.IO es la compatibilidad con sesiones persistentes. Las sesiones persistentes se habilitan de manera predeterminada en las aplicaciones web de Azure con el enrutamiento de solicitudes de Azure. Para obtener más información, consulte [Afinidad de instancias en Sitios web de Azure].
> 
> 

### <a name="create-a-redis-cache"></a>Crear una caché de Redis
Realice los pasos de Hola de [crear una memoria caché en Redis de Azure] toocreate una nueva memoria caché.

> [!NOTE]
> Guardar hello **nombre de Host** y **clave principal** para la memoria caché, como estas se necesitará en Hola pasos siguientes.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Agregar redis hello y módulos socket.io redis
1. Desde una línea de comandos, cambiar toohello  **\\nodo\\chat** Hola de directorio y el uso siguiente comando.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > versiones de Hello especificadas en este comando son versiones de hello utilizadas al probar este artículo.
   > 
   > 
2. Modificar hello **app.js** siguientes de Hola de archivo tooadd líneas inmediatamente después de`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Reemplace **redishostname** y **rediskey** con nombre de host de Hola y la clave de la memoria caché de Redis.
   
    Esto creará una publicación y suscripción cliente toohello caché en Redis creado anteriormente. los clientes de Hello, a continuación, se usan con hello adaptador tooconfigure caché en Redis hello Socket.IO toouse para pasar mensajes y eventos entre instancias de la aplicación
   
   > [!NOTE]
   > Mientras hello **socket.io redis** adaptador puede comunicarse directamente tooRedis, versión actual de hello no admite la autenticación de hello requerida por la caché en Redis de Azure. Por lo que la conexión inicial Hola se crea utilizando hello **redis** módulo, el cliente de hello, a continuación, se pasa toohello **socket.io redis** adaptador.
   > 
   > Mientras que caché en Redis de Azure admite conexiones seguras mediante el puerto 6380, módulos de hello usados en este ejemplo no admiten conexiones seguras a partir de 7/14/2014. Hola por encima de código usa Hola de forma predeterminada, el puerto no seguro de 6379.
   > 
   > 
3. Hola guardar modificado **app.js**

### <a name="commit-changes-and-redeploy"></a>Confirmar cambios y volver a implementar
Desde la línea de comandos en Hola Hola  **\\nodo\\chat** directorio, use Hola siguientes comandos toocommit cambios y volver a implementar la aplicación hello.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Una vez que se hayan insertado cambios hello toohello server, puede escalar el sitio en varias instancias utilizando el siguiente comando de Hola.

    azure site scale instances --instances #

Donde  **#**  es Hola número de instancias toocreate.

Puede conectarse tooyour web app desde varios tooverify exploradores o equipos que los mensajes se envían correctamente los clientes de tooall.

## <a name="troubleshooting"></a>Solución de problemas
### <a name="connection-limits"></a>Límites de conexión
Las aplicaciones Web de Azure está disponible en varias SKU, que determinan el sitio de hello recursos tooyour disponible. Esto incluye Hola número de conexiones permitidas de WebSocket. Para obtener más información, vea hello [página de precios de las aplicaciones Web].

### <a name="messages-arent-being-sent-using-websockets"></a>No se están enviando los mensajes con WebSockets
Si los exploradores de cliente mantengan revirtiendo toolong sondeo en lugar de usar WebSockets, puede ser debido a uno de los siguientes Hola.

* **Pruebe a limitar Hola transporte toojust WebSockets**
  
    Para Socket.IO toouse WebSockets como Hola transporte de mensajería, servidor hello y del cliente deben admitir WebSockets. Si uno o hello otro no es así, Socket.IO negociará otro transporte, como el sondeo largo. lista predeterminada de Hola de transportes utilizados por Socket.IO es ` websocket, htmlfile, xhr-polling, jsonp-polling`. Puede forzar la tooonly use WebSockets agregando Hola después código toohello **app.js** archivo, después de la línea que contiene de hello `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Observe que exploradores más antiguos que no admiten WebSockets no será capaz de tooconnect toohello sitio mientras Hola por encima del código está activa, tal y como se restringe únicamente tooWebSockets de comunicación.
  > 
  > 
* **Uso de SSL**
  
    WebSockets se basa en algunos encabezados HTTP menor uso, como Hola **actualizar** encabezado. Algunos dispositivos de red intermedios, como los proxy web, pueden quitar estos encabezados. tooavoid este problema, puede establecer la conexión de WebSocket de Hola a través de SSL.
  
    Una manera sencilla de tooaccomplish es demasiado tooconfigure Socket.IO`match origin protocol`. Esto indica a Hola de comunicación de WebSockets Socket.IO toosecure igual Hola HTTP/HTTPS que se originan de solicitud para la página web de Hola. Si un explorador utiliza una dirección URL HTTPS toovisit su sitio Web, se protegerán posteriores WebSocket las comunicaciones a través Socket.IO a través de SSL.
  
    toomodify este tooenable ejemplo esta configuración, agregar Hola después código toohello **app.js** archivo después de la línea que contiene de hello `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Comprobación de la configuración de web.config**
  
    Aplicaciones web de Azure que hospedan aplicaciones Node.js usan hello **web.config** tooroute archivo entrante solicita toohello Node.js aplicación. Para WebSockets toofunction correctamente con aplicaciones Node.js, Hola **web.config** debe contener la siguiente entrada de Hola.
  
        <webSocket enabled="false"/>
  
    Esto deshabilita el módulo WebSockets de IIS de hello, que incluye su propia implementación de WebSockets y entra en conflicto con los módulos de WebSocket específicos de Node.js como Socket.IO. Si esta línea no está presente o se establece demasiado`true`, esto puede ser motivo de Hola que transporte de WebSocket de hello no funciona para su aplicación.
  
    Normalmente, las aplicaciones Node.js no incluyen un archivo **web.config** , por lo que Sitios web Azure generará automáticamente uno para las aplicaciones Node.js cuando se implementan. Puesto que este archivo se genera automáticamente en el servidor de hello, debe usar Hola FTP o FTPS dirección URL para el sitio Web tooview este archivo. Puede encontrar Hola FTP y FTPS direcciones URL para el sitio en el portal clásico de hello seleccionando la aplicación web y Hola, a continuación, **panel** vínculo. Hello las direcciones URL aparecen en hello **vista rápida** sección.
  
  > [!NOTE]
  > Hola **web.config** archivo solo se genera por los sitios Web de Azure si la aplicación no proporciona uno. Si proporciona un **web.config** archivo en la raíz de Hola de su proyecto de aplicación, se utilizará por aplicaciones Web de Azure.
  > 
  > 
  
    Si entrada hello no está presente o se establece el valor de tooa de `true`, a continuación, debe crear un **web.config** en Hola raíz de la aplicación Node.js y especifique un valor de `false`.  Como referencia, Hola siguiente es un valor predeterminado **web.config** para una aplicación que utiliza **app.js** como punto de entrada de Hola.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Si la aplicación utiliza un punto de entrada distinto de **app.js**, debe reemplazar todas las apariciones de **app.js** con hello corregir el punto de entrada. Por ejemplo, reemplazando **app.js** por **server.js**.

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones], donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial ha aprendido cómo toocreate una aplicación de chat hospedada en una aplicación web de Azure. También puede hospedar esta aplicación como un servicio en la nube de Azure. Para conocer los pasos sobre cómo tooaccomplish, vea [compilar una aplicación de Chat de Node.js con Socket.IO en un servicio de nube de Azure].

Para obtener más información, vea también hello [Centro para desarrolladores de Node.js].

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente].

<!-- URL List -->

[Azure Redis Cache]: /documentation/services/redis-cache/
[aplicación del servicio de aplicaciones Web]: http://go.microsoft.com/fwlink/?LinkId=529714
[página de precios de las aplicaciones Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[compilar una aplicación de Chat de Node.js con Socket.IO en un servicio de nube de Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centro para desarrolladores de Node.js]: /develop/nodejs/
[pruebe el servicio de aplicaciones]: https://azure.microsoft.com/try/app-service/
[Afinidad de instancias en Sitios web de Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[crear una memoria caché en Redis de Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[repositorio de Socket.IO GitHub]: https://github.com/socketio/socket.io
[ZIP o GZ archivado versión]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
