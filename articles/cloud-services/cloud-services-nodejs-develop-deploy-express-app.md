---
title: "aaaWeb aplicación con Express (Node.js) | Documentos de Microsoft"
description: "Un tutorial que se basa en el tutorial de servicio de nube de Hola y muestra cómo toouse Hola módulo Express."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Compilación de una aplicación web Node.js mediante Express en un servicio en la nube de Azure
Node.js incluye un conjunto mínimo de funcionalidad en tiempo de ejecución de hello core.
Los desarrolladores suelen utilizar 3rd funcionalidad adicional de entidad módulos tooprovide al desarrollar una aplicación Node.js. En este tutorial creará una nueva aplicación mediante hello [Express] [ Express] módulo, que proporciona un marco MVC para crear aplicaciones web de Node.js.

Una captura de pantalla de la aplicación hello completado es menor que:

![Un explorador web mostrar tooExpress bienvenida en Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Creación de un proyecto de servicio en la nube
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Realizar Hola siguientes pasos toocreate un nuevo proyecto de servicio de nube con el nombre 'expressapp':

1. De hello **menú Inicio** o **pantalla Inicio**, busque **Windows PowerShell**. Finalmente, haga clic con el botón derecho en **Windows PowerShell** y seleccione **Ejecutar como administrador**.
   
    ![Icono de Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Cambie los directorios toohello **c:\\nodo** directorio y, a continuación, escriba Hola después comandos toocreate una nueva solución denominada **expressapp** y un rol web denominado **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > De forma predeterminada, **Add-AzureNodeWebRole** usa una versión anterior de Node.js. Hola **AzureServiceProjectRole conjunto** instrucción anterior indica a Azure toouse v0.10.21 del nodo.  Tenga en cuenta los parámetros de hello distinguen mayúsculas de minúsculas.  Puede comprobar la versión correcta de Hola de Node.js se ha seleccionado mediante la comprobación de hello **motores** propiedad en **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Instalación de Express
1. Instalar generador de Express Hola emitiendo Hola siguiente comando:
   
        PS C:\node\expressapp> npm install express-generator -g
   
    resultado de Hello de comando de npm Hola debería ser resultado de toohello similar a continuación. 
   
    ![Comando rápida de instalación de Windows PowerShell mostrar salida de hello de hello npm.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Cambie los directorios toohello **WebRole1** directorio y uso Hola comando express toogenerate una nueva aplicación:
   
        PS C:\node\expressapp\WebRole1> express
   
    También será toooverwrite solicitada su aplicación anterior. Escriba **y** o **Sí** toocontinue. Express generará el archivo de app.js hello y una estructura de carpetas para la creación de la aplicación.
   
    ![salida de Hello de comando express Hola](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. dependencias adicionales tooinstall definidas en el archivo de package.json hello, escriba Hola siguiente comando:
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![comando de instalación de la salida de Hello de hello npm](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Siguiente Hola de uso del comando hello toocopy **bin/www** archivo demasiado**server.js**. Esto es para que servicio de nube de hello pueda encontrar el punto de entrada de Hola para esta aplicación.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   Una vez completado este comando, debe tener un **server.js** archivo hello WebRole1 directorio.
5. Modificar hello **server.js** tooremove uno de hello '.' caracteres de hello después de línea.
   
       var app = require('../app');
   
   Después de realizar esta modificación, la línea hello debería aparecer como sigue.
   
       var app = require('./app');
   
   Este cambio es necesario puesto que se movió el archivo hello (anteriormente **bin/www**,) toohello mismo directorio que el archivo de aplicación hello que se requiere. Después de realizar este cambio, guardar hello **server.js** archivo.
6. Usar hello tras la aplicación de comando toorun Hola Hola emulador de Azure:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Una página web que contiene tooexpress bienvenida.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Hola Modificar vista
Ahora modificar Hola ver toodisplay Hola mensaje "Bienvenida tooExpress en Azure".

1. Escriba Hola comando tooopen hello index.jade archivo siguiente:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Hola contenido de hello index.jade archivo.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade es el motor de vistas de hello predeterminado utilizado por las aplicaciones de Express. Para obtener más información sobre el motor de vista Jade hello, consulte [http://jade-lang.com][http://jade-lang.com].
2. Modificar la última línea de texto de hello anexando **en Azure**.
   
   ![archivo de index.jade Hello, última línea de hello lee: p Bienvenido demasiado\#{título} en Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Guarde el archivo hello y salga el Bloc de notas.
4. Actualice el explorador para ver los cambios.
   
   ![Una ventana del explorador, la página de hello contiene tooExpress bienvenida en Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

Después de la aplicación de prueba hello, usar hello **AzureEmulator Stop** emulador de cmdlet toostop Hola.

## <a name="publishing-hello-application-tooazure"></a>Publicación tooAzure de aplicación Hola
En la ventana de PowerShell de Azure de hello, usar hello **AzureServiceProject publicar** servicio de nube de cmdlet toodeploy Hola aplicación tooa

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Una vez completada la operación de implementación de hello, el explorador abrirá y mostrar la página web de Hola.

![Un explorador web mostrar hello Express página. dirección URL de Hello indica que ahora se hospede en Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de Node.js](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


