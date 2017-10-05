---
title: "Creación de una aplicación de chat Node.js con Socket.IO en el Servicio de aplicaciones de Azure"
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
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Creación de una aplicación de chat Node.js con Socket.IO en el Servicio de aplicaciones de Azure
Socket.IO proporciona comunicación en tiempo real entre su servidor node.js y los clientes con WebSockets. También es compatible con la reserva a otros transportes (como el sondeo largo) que funcionan con otros exploradores. Este tutorial le guiará por el hospedaje de una aplicación de chat basada en Socket.IO como una aplicación web de Azure, y le mostrará cómo escalar la aplicación con [Caché en Redis de Azure]. Para obtener más información sobre Socket.IO, consulte <http://socket.io/>.

> [!NOTE]
> Los procedimientos de esta tarea se aplican a [App Service Web Apps]; para Cloud Services, consulte [Creación de una aplicación de chat Node.js con Socket.IO en Servicio en la nube de Azure].
> 
> 

## <a name="download-the-chat-example"></a>Descarga del ejemplo de chat
Para este proyecto, usaremos el ejemplo de chat del [repositorio de Socket.IO GitHub](en inglés). Realice los siguientes pasos para descargar el ejemplo y agréguelo al proyecto que creó anteriormente.

1. Descargue una [versión archivada ZIP o GZ] del proyecto Socket.IO (la versión 1.3.5 se ha utilizado para este documento).
2. Extraiga el archivo y copie el directorio **examples\\chat** en una ubicación nueva. Por ejemplo, **\\nodo\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Modificación de app.js e instalación de módulos
1. Cambie el nombre del archivo **index.js** a **app.js**. Esto permite a Azure detectar que se trata de una aplicación Node.js.
2. Abra el archivo **app.js** en un editor de texto. Cambie la línea que contiene `var io = require('../..')(server);` como se muestra a continuación:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Abra el archivo **package.json** y agregue una referencia a socket.io en `dependencies`, como se muestra a continuación:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. En la línea de comandos, cambie al directorio **\\node\\chat** y use npm para instalar los módulos necesarios para esta aplicación:
   
        npm install
   
    Esto instalará los módulos en una subcarpeta denominada **node_modules**.

## <a name="create-an-azure-web-app"></a>Creación de una aplicación web de Azure
Siga estos pasos para crear una aplicación web de Azure, habilite la publicación Git y, a continuación, habilite la compatibilidad de WebSocket para la aplicación web.

> [!NOTE]
> Para completar este tutorial, deberá tener una cuenta de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Evaluación gratuita de Azure</a>.
> 
> 

1. Instale la interfaz de la línea de comandos de Azure (CLI de Azure) y conéctese a su suscripción de Azure. Consulte [Instalación y configuración de la interfaz de la CLI de Azure](../cli-install-nodejs.md).
2. Si esta es la primera vez que configura un repositorio en Azure, tendrá que crear unas credenciales de inicio de sesión. En la CLI de Azure, escriba el siguiente comando:
   
        azure site deployment user set [username] [password]
3. Cambie al directorio **\\node\chat** y use el siguiente comando para crear una nueva aplicación web de Azure y un repositorio de Git local. Este comando también crea un Git remoto llamado "azure".
   
        azure site create mysitename --git
   
    Debe reemplazar "mysitename" por un nombre único para su sitio web.
4. Confirme los archivos existentes en el repositorio local usando los siguientes comandos:
   
        git add .
        git commit -m "Initial commit"
5. Inserte los archivos en el repositorio de la aplicación web de Azure con el siguiente comando:
   
        git push azure master
   
    Cuando se le solicite, escriba las credenciales del paso 2. Recibirá mensajes de estado a medida que los módulos se importen en el servidor. Después de que se haya completado este proceso, la aplicación se hospedará en su aplicación web de Azure.
   
   > [!NOTE]
   > Durante la instalación de módulos, es posible que aparezcan errores del tipo "No se ha encontrado el proyecto importado...". Se pueden ignorar con seguridad.
   > 
   > 
6. Socket.IO usa WebSockets, que no están habilitados de manera predeterminada en Azure. Para habilitar los sockets web, use el siguiente comando:
   
        azure site set -w
   
    Si se solicita, escriba el nombre de la aplicación web.
   
   > [!NOTE]
   > El comando "azure site set -w" solo funcionará con la versión 0.7.4 o superior de la interfaz de la línea de comandos de Azure. También puede habilitar la compatibilidad con WebSocket usando el [Portal de Azure](https://portal.azure.com).
   > 
   > Para habilitar WebSockets con Azure Portal, haga clic en la aplicación web en la hoja Web Apps, haga clic en **Toda la configuración** > **Configuración de la aplicación**. En **Web Sockets**, haga clic en **Activado**. A continuación, haga clic en **Guardar**.
   > 
   > 
7. Para ver la aplicación web en Azure, use el siguiente comando para iniciar su explorador web y desplazarse a la aplicación web hospedada:
   
        azure site browse

Su aplicación se está ejecutando ahora en Azure y puede retransmitir los mensajes de chat entre los diferentes clientes que usan Socket.IO.

## <a name="scale-out"></a>Escalado horizontal
Las aplicaciones Socket.IO se pueden escalar horizontalmente con un **adaptador** para distribuir mensajes y eventos entre varias instancias de aplicaciones. Aunque hay varios adaptadores disponibles, el adaptador [socket.io-redis] se puede utilizar fácilmente con la característica de Caché en Redis de Azure.

> [!NOTE]
> Un requisito adicional para el escalado horizontal de una solución Socket.IO es la compatibilidad con sesiones persistentes. Las sesiones persistentes se habilitan de manera predeterminada en las aplicaciones web de Azure con el enrutamiento de solicitudes de Azure. Para obtener más información, consulte [Afinidad de instancias en Sitios web de Azure].
> 
> 

### <a name="create-a-redis-cache"></a>Crear una caché de Redis
Realice los pasos de [Creación de una memoria caché en Caché en Redis de Azure] para crear una caché nueva.

> [!NOTE]
> Guarde el **Nombre de host** y la **Clave principal** de la caché, ya que los necesitará en los siguientes pasos.
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a>Agregue los módulos redis y socket.io-redis
1. En una línea de comandos, cambie al directorio **\\node\\chat** y use el siguiente comando.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > Las versiones indicadas en este comando son la sutilizadas al hacer las pruebas de este artículo.
   > 
   > 
2. Modifique el archivo **app.js** para agregar la siguientes líneas inmediatamente después de `var io = require('socket.io')(server);`.
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Reemplace **redishostname** y **rediskey** por el nombre de host y la clave de la caché en Redis.
   
    Esto creará un cliente de publicación y suscripción a la caché de Redis creada anteriormente. Entonces los clientes se utilizarán con el adaptador para configurar Socket.IO y utilizar la caché de Redis para pasar mensajes y eventos entre instancias de la aplicación.
   
   > [!NOTE]
   > Aunque el adaptador **socket.io-redis** se puede comunicar directamente con Redis, la versión actual no es compatible con la autenticación que requiere Azure Redis Cache. Por tanto, la conexión inicial se crea con el módulo **redis**; a continuación, el cliente se pasa al adaptador **socket.io-redis**.
   > 
   > Aunque la caché de Redis de Azure es compatible con las conexiones seguras que utilizan el puerto 6380, los módulos usados en este ejemplo no son compatibles con las conexiones seguras a partir del 14/07/2014. El código anterior utiliza el puerto predeterminado no seguro 6379.
   > 
   > 
3. Guarde el archivo **app.js** modificado

### <a name="commit-changes-and-redeploy"></a>Confirmar cambios y volver a implementar
En la línea de comandos del directorio **\\node\\chat**, utilice los siguientes comandos para confirmar los cambios y volver a implementar la aplicación.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Cuando los cambios se hayan enviado al servidor, puede escalar su sitio por varias instancias con el siguiente comando.

    azure site scale instances --instances #

Donde **#** es el número de instancias que se van a crear.

Puede conectarse a la aplicación web desde varios exploradores o equipos para verificar que los mensajes se envían correctamente a todos los clientes.

## <a name="troubleshooting"></a>Solución de problemas
### <a name="connection-limits"></a>Límites de conexión
Aplicaciones web de Azure está disponible en varios SKU, lo que determina los recursos disponibles en su sitio. Esto incluye el número permitido de conexiones WebSocket. Para obtener más información, consulte la [página Precios de aplicaciones web].

### <a name="messages-arent-being-sent-using-websockets"></a>No se están enviando los mensajes con WebSockets
Si los exploradores de los clientes siguen recurriendo al sondeo largo en lugar de utilizar WebSockets, tal vez se deba a uno de estos motivos.

* **Intente limitar el transporte a solo WebSockets**
  
    Para que Socket.IO utilice WebSockets como transporte de mensajes, tanto el servidor como el cliente deben ser compatibles con WebSockets. Si uno o el otro no lo son, Socket.IO negociará otro transporte, como el sondeo largo. La lista predeterminada de transportes utilizados por Socket.IO es ` websocket, htmlfile, xhr-polling, jsonp-polling`. Puede forzarlo a que solo utilice WebSockets si agrega el siguiente código al archivo **app.js**, después de la línea que contiene `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Tenga en cuenta que los exploradores más antiguos que no son compatibles con WebSockets no podrán conectarse al sitio, aunque el código anterior esté activo, ya que restringe la comunicación solo a WebSockets.
  > 
  > 
* **Uso de SSL**
  
    WebSockets depende de algunos encabezados HTTP menos utilizados, como el encabezado **Upgrade** . Algunos dispositivos de red intermedios, como los proxy web, pueden quitar estos encabezados. Para evitar este problema, puede establecer la conexión WebSocket por SSL.
  
    Una manera sencilla de conseguirlo es configurar Socket.IO en `match origin protocol`. Esto envía instrucciones a Socket.IO para asegurar la comunicación de WebSockets al igual que la solicitud HTTP/HTTPS original para la página web. Si un explorador utiliza una URL HTTPS para visitar su sitio web, las comunicaciones consiguientes de WebSocket a través de Socket.IO se asegurarán con SSL.
  
    Para modificar este ejemplo y habilitar esta configuración, agregue el siguiente código al archivo **app.js**, después de la línea que contiene `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Comprobación de la configuración de web.config**
  
    Las aplicaciones web de Azure que hospedan aplicaciones Node.js utilizan el archivo **web.config** para enrutar las solicitudes entrantes a la aplicación Node.js. Para que WebSockets funcione correctamente con aplicaciones Node.js, **web.config** debe contener la siguiente entrada.
  
        <webSocket enabled="false"/>
  
    Esto deshabilita el módulo WebSockets de IIS, que incluye su propia implementación de WebSockets y entra en conflicto con módulos de WebSocket específicos de Node.js, como Socket.IO. Si esta línea no está presente o se establece en `true`, puede ser el motivo por el que el transporte de WebSocket no funciona para su aplicación.
  
    Normalmente, las aplicaciones Node.js no incluyen un archivo **web.config** , por lo que Sitios web Azure generará automáticamente uno para las aplicaciones Node.js cuando se implementan. Como este archivo se genera automáticamente en el servidor, debe utilizar la URL FTP o FTPS en su sitio web para ver este archivo. Puede encontrar las direcciones URL FTP y FTPS para su sitio en el Portal clásico si selecciona la aplicación web y después el vínculo **Panel** . Las URL se muestran en la sección de **vista rápida** .
  
  > [!NOTE]
  > Sitios web de Azure solo genera el archivo **web.config** si la aplicación no lo proporciona. Si proporciona un archivo **web.config** en la raíz de su proyecto de aplicación, Aplicaciones web de Azure lo utilizará.
  > 
  > 
  
    Si la entrada no está presente, o si se ha establecido en el valor de `true`, entonces deberá crear un **web.config** en la raíz de su aplicación Node.js y especificar un valor de `false`.  Como referencia, a continuación se muestra el **web.config** predeterminado para una aplicación que usa **app.js** como punto de entrada.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Si la aplicación usa un punto de entrada distinto de **app.js**, debe reemplazar todas las apariciones de **app.js** con el punto de entrada correcto. Por ejemplo, reemplazando **app.js** por **server.js**.

> [!NOTE]
> Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [App Service], donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial aprendió a crear una aplicación de chat hospedada en una aplicación web de Azure. También puede hospedar esta aplicación como un servicio en la nube de Azure. Para conocer los pasos para lograr esto, consulte [Creación de una aplicación de chat Node.js con Socket.IO en Servicio en la nube de Azure].

Para obtener más información, consulte también el [Centro para desarrolladores de Node.js].

## <a name="whats-changed"></a>Lo que ha cambiado
* Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes].

<!-- URL List -->

[Caché en Redis de Azure]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[página Precios de aplicaciones web]: http://go.microsoft.com/fwlink/?LinkId=511643
[Creación de una aplicación de chat Node.js con Socket.IO en Servicio en la nube de Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
[Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centro para desarrolladores de Node.js]: /develop/nodejs/
[App Service]: https://azure.microsoft.com/try/app-service/
[Afinidad de instancias en Sitios web de Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[Creación de una memoria caché en Caché en Redis de Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io-redis]: https://github.com/socketio/socket.io-redis
[repositorio de Socket.IO GitHub]: https://github.com/socketio/socket.io
[versión archivada ZIP o GZ]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
