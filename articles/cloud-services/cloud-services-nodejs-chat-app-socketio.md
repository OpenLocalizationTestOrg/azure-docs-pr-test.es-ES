---
title: "aplicación de aaaNode.js con Socket.io | Documentos de Microsoft"
description: "Obtenga información acerca de cómo alojar toouse socket.io en una aplicación node.js en Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Creación de una aplicación de chat Node.js con Socket.IO en un servicio en la nube de Azure
Socket.IO proporciona comunicación en tiempo real entre su servidor node.js y los clientes. Este tutorial le llevara por el hospedaje de una aplicación de chat basada en socket.IO en Azure. Para obtener más información sobre Socket.IO, consulte <http://socket.io/>.

Una captura de pantalla de la aplicación hello completado es menor que:

![Una ventana del explorador mostrar servicio Hola hospedado en Azure][completed-app]  

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que Hola siguientes productos y versiones son ejemplo de Hola completa toosuccessfully instalada en este artículo:

* Instalar [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)
* Instalar [Node.js](https://nodejs.org/download/)
* Instalar [Python versión 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Creación de un proyecto de servicio en la nube
Hello pasos siguientes crean proyecto de servicio de nube de Hola que hospedará la aplicación de hello Socket.IO.

1. De hello **menú Inicio** o **pantalla Inicio**, busque **Windows PowerShell**. Finalmente, haga clic con el botón derecho en **Windows PowerShell** y seleccione **Ejecutar como administrador**.
   
    ![Icono de Azure PowerShell][powershell-menu]
2. Cree un directorio denominado **c:\\node**. 
   
        PS C:\> md node
3. Cambie los directorios toohello **c:\\nodo** directory
   
        PS C:\> cd node
4. Escriba Hola después comandos toocreate una nueva solución denominada **chatapp** y un rol de trabajo denominado **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Verá Hola después de respuesta:
   
    ![salida de Hello de hello nueva-azureservice y azurenodeworkerrolecmdlets agregar](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Descargar Hola ejemplo Chat
Para este proyecto, usaremos hello (ejemplo) chat de hello [repositorio de Socket.IO GitHub]. Realizar Hola siguiente ejemplo de Hola toodownload de pasos y Agregar proyecto toohello que creó anteriormente.

1. Crear una copia local del repositorio de hello mediante hello **clon** botón. También puede usar hello **código postal** proyecto de botón toodownload Hola.
   
   ![Una ventana del explorador ven https://github.com/LearnBoost/socket.io/tree/master/examples/chat, con el icono de descarga de hello ZIP resaltado][chat-example-view]
2. Explorar la estructura de directorios de hello del repositorio local Hola hasta que llegue al hello **ejemplos\\chat** directory. Copie el contenido de Hola de este directorio toothe **C:\\nodo\\chatapp\\WorkerRole1** directorio creado anteriormente.
   
   ![El explorador, mostrar contenido de Hola de ejemplos de hello\\directorio chat extraído del archivo Hola][chat-contents]
   
   los elementos resaltados en la captura de pantalla de hello anterior Hello son archivos de hello copiados de hello **ejemplos\\chat** directory
3. Hola **C:\\nodo\\chatapp\\WorkerRole1** directorio, delete hello **server.js** de archivos y, a continuación, cambie el nombre hello **app.js**archivo demasiado**server.js**. Esto quita el valor predeterminado de hello **server.js** archivo creado anteriormente por hello **Add-AzureNodeWorkerRole** cmdlet y los reemplaza con la aplicación hello de archivos de ejemplo de chat de Hola.

### <a name="modify-serverjs-and-install-modules"></a>Modificar el archivo server.js e instalar los módulos
Antes de la aplicación de prueba Hola Hola emulador de Azure, debemos hacer algunas modificaciones menores. Lleve a cabo Hola pasos toothe server.js archivo siguiente:

1. Abra hello **server.js** archivo en Visual Studio o en cualquier editor de texto.
2. Buscar hello **las dependencias del módulo** sección al principio de Hola de server.js y cambiar Hola línea que contiene **sio = require('.. //.. lib//Socket.IO')** demasiado**sio = require('socket.io')** tal y como se muestra a continuación:
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. aplicación de hello tooensure escucha en el puerto correcto de hello, abra server.js en el Bloc de notas o su editor favorito y, a continuación, cambie la siguiente línea reemplazando **3000** con **process.env.port** tal como se muestra a continuación:
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

Después de guardar los cambios de hello demasiado**server.js**usar hello siguiendo los pasos para instalar los módulos necesarios y, a continuación, pruebe la aplicación hello en el emulador de Azure:

1. Usando **Azure PowerShell**, cambie los directorios toohello **C:\\nodo\\chatapp\\WorkerRole1** Hola de directorio y el uso después de comando tooinstall hello módulos requeridos por la aplicación:
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Este modo se instalará módulos de hello enumerados en el archivo de hello package.json. Una vez completado el comando de hello, debería ver resultados similares toothe siguiente:
   
   ![comando de instalación de la salida de Hello de hello npm][The-output-of-the-npm-install-command]
2. Dado que este ejemplo originalmente formaba parte del repositorio de Socket.IO GitHub de Hola y hace referencia directamente a biblioteca de hello Socket.IO ruta de acceso relativa, Socket.IO no se hace referencia en el archivo de package.json hello, por lo que debemos instalarlo mediante la emisión de hello siguiente comando:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Prueba e implementación
1. Inicie el emulador de hello emitiendo Hola siguiente comando:
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > Si tiene algún problema con el emulador de inicio, por ejemplo; Start-AzureEmulator : Error inesperado.  Detalles: Se encontró un error inesperado Hola comunicación objeto, System.ServiceModel.Channels.ServiceChannel, no puede utilizarse para la comunicación porque está en estado Faulted de hello.
   
      Vuelva a instalar AzureAuthoringTools v 2.7.1 y AzureComputeEmulator v 2.7. Asegúrese de que coincida con esa versión.
   >
   >


2. Abra un explorador y navegue demasiado**http://127.0.0.1**.
3. Cuando se abre la ventana del explorador de hello, escriba un alias y, a continuación, presione ENTRAR.
   Esto le permitirá toopost mensajes como un alias específico. funcionalidad de varios usuarios tootest, abrir ventanas adicionales del explorador utilizando la misma dirección URL y escriba los alias diferentes.
   
   ![Dos ventanas de explorador que muestran mensajes de chat de User1 y User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. Después de la aplicación de prueba hello, detener el emulador de hello emitiendo el comando siguiente:
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. toodeploy Hola aplicación tooAzure, use la **AzureServiceProject publicar** cmdlet. Por ejemplo:
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Ser un nombre único de toouse seguro, en caso contrario Hola publicar proceso producirá un error. Una vez finalizada la implementación de hello, Explorador de Hola se abrirá y navegue toohello implementado service.
   > 
   > Si recibe un error que indica que ese Hola proporcionado nombre de la suscripción no existe en hello importar perfil de publicación, debe descargar e importar el perfil de publicación de Hola para su suscripción antes de implementar tooAzure. Vea hello **implementar Hola aplicación tooAzure** sección de [compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Una ventana del explorador mostrar servicio Hola hospedado en Azure][completed-app]
   
   > [!NOTE]
   > Si recibe un error que indica que ese Hola proporcionado nombre de la suscripción no existe en hello importar perfil de publicación, debe descargar e importar el perfil de publicación de Hola para su suscripción antes de implementar tooAzure. Vea hello **implementar Hola aplicación tooAzure** sección de [compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

Su aplicación se está ejecutando ahora en Azure y puede retransmitir los mensajes de chat entre los diferentes clientes que usan Socket.IO.

> [!NOTE]
> Para simplificar, este ejemplo es toochatting limitado entre los usuarios conectados toohello misma instancia. Esto significa que si el servicio en la nube Hola crea dos instancias de rol de trabajo, los usuarios solo podrán toochat con otros usuarios conectados toohello misma instancia de rol de trabajo. tooscale hello toowork de aplicación con varias instancias de rol, podría utilizar una tecnología como Service Bus tooshare hello Socket.IO almacenar el estado en todas las instancias. Para obtener ejemplos, vea ejemplos de uso de hello temas y colas de Bus de servicio en hello [Azure SDK para el repositorio de Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial ha aprendido cómo toocreate una aplicación básica de chat hospedada en un servicio de nube de Azure. toolearn toohost esta aplicación en un sitio Web de Azure, vea [compilar una aplicación de Chat de Node.js con Socket.IO en un sitio Web de Azure][chatwebsite].

Para obtener más información, vea también hello [Centro para desarrolladores de Node.js](/develop/nodejs/).

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[repositorio de Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


