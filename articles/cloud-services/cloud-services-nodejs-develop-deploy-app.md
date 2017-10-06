---
title: "aaaNode.js Guía de introducción | Documentos de Microsoft"
description: "Conozca cómo toocreate una Node.js simple aplicación web e implementarlo tooan servicio de nube de Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure

Este tutorial se muestra cómo un simple Node.js toocreate aplicación que se ejecuta en un servicio de nube de Azure. Servicios en la nube son bloques de creación de hello de aplicaciones de nube escalables en Azure. Permitir la separación de Hola y administración independiente y escalabilidad de los componentes front-end y back-end de la aplicación.  Los Servicios en la nube proporcionan una máquina virtual dedicada y robusta para hospedar cada rol de forma fiable.

Para obtener más información sobre los servicios en la nube, y cómo se comparan tooAzure sitios Web y máquinas virtuales, consulte [comparación de sitios Web de Azure, servicios en la nube y máquinas virtuales].

> [!TIP]
> ¿Busca un sitio Web sencillo toobuild? Si el escenario solo requiere un sencillo front-end para sitios web, considere la posibilidad de [utilizar una aplicación web ligera]. Puede actualizar fácilmente tooa servicio en la nube que crezca su aplicación web y cambian sus requisitos.

Siguiendo este tutorial, podrá compilar una aplicación web sencilla hospedada en un rol web. Se usen tootest de emulador de proceso de hello su aplicación localmente, a continuación, implementarlo mediante herramientas de línea de comandos de PowerShell.

aplicación Hello es una sencilla aplicación "Hola a todos":

![Un explorador web Mostrar página web de Hola Hola a todos][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Requisitos previos
> [!NOTE]
> Este tutorial usa PowerShell de Azure, que requiere Windows.

* Instale y configure [Azure PowerShell].
* Descargue e instale hello [Azure SDK para .NET 2.7]. Hola, instalar el programa de instalación, seleccione:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Cree un proyecto del servicio de nube de Azure
Lleve a cabo Hola después tareas toocreate un nuevo proyecto de servicio de nube de Azure, junto con scaffolding de Node.js básica:

1. Ejecutar **Windows PowerShell** como administrador; de hello **menú Inicio** o **pantalla Inicio**, busque **Windows PowerShell**.
2. [Conectar PowerShell] tooyour suscripción.
3. Escriba Hola después proyecto Hola de PowerShell cmdlet toocreate toocreate:

        New-AzureServiceProject helloworld

    ![resultado de Hello de comando de hello New-AzureService helloworld][hello result of hello New-AzureService helloworld command]

    Hola **AzureServiceProject New** genera una estructura básica para publicar un tooa de aplicación Node.js servicio en la nube. Contiene archivos de configuración necesarios para la publicación tooAzure. cmdlet de Hello también cambia el directorio de toohello del directorio de trabajo para el servicio de Hola.

    Hola crea Hola siguientes archivos:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** y **ServiceDefinition.csdef**: estos archivos específicos de Azure son necesarios para publicar la aplicación. Para obtener más información, consulte [Información general de la creación de un servicio hospedado para Azure].
   * **deploymentSettings.json**: almacena la configuración local que se usa por hello cmdlets de implementación de Azure PowerShell.
4. Escriba Hola después comando tooadd un nuevo rol web:

       Add-AzureNodeWebRole

   ![salida de Hello de hello comando Add-AzureNodeWebRole][hello output of hello Add-AzureNodeWebRole command]

   Hola **Add-AzureNodeWebRole** crea una aplicación básica de Node.js. También modifica hello **. csfg** y **.csdef** tooadd entradas de configuración para el nuevo rol de Hola de archivos.

   > [!NOTE]
   > Si no especifica un nombre de rol, se usa el nombre predeterminado. Puede proporcionar un nombre como primer parámetro de cmdlet hello:`Add-AzureNodeWebRole MyRole`

aplicación Node.js de Hello se define en el archivo hello **server.js**, ubicada en el directorio de hello para el rol web de hello (**WebRole1** de forma predeterminada). Este es el código de hello.

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Este código es básicamente Hola igual Hola "¡Hello World" de ejemplo de Hola [nodejs.org] sitio Web, excepto en que utiliza el número de puerto de hello asignado por el entorno de nube de Hola.

## <a name="deploy-hello-application-tooazure"></a>Implementar Hola aplicación tooAzure

> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. Puede [activar sus beneficios de suscriptor a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) o [registrarse para obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Descargar hello Azure configuración de publicación
toodeploy tooAzure de su aplicación, primero debe descargar Hola publicar la configuración de la suscripción de Azure.

1. Ejecute hello siguiente cmdlet de PowerShell de Azure:

       Get-AzurePublishSettingsFile

   Esto va a usar el explorador toonavigate toohello publicar la página de descarga de configuración. Es posible que toolog solicitada con una Account de Microsoft. Si es así, usar cuenta de hello asociada con su suscripción de Azure.

   Guardar Hola descarga puedan acceder fácilmente a la ubicación del archivo tooa de perfil.
2. Ejecutar la siguiente cmdlet tooimport Hola descargó el perfil de publicación:

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Después de importar hello, configuración de publicación, considere la posibilidad de eliminar Hola descargado el archivo .publishSettings, ya que contiene información que podría permitir que alguien tooaccess tu cuenta.

### <a name="publish-hello-application"></a>Publicar la aplicación hello
toopublish, ejecute hello siguientes comandos:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** especifica el nombre de hello para la implementación de Hola. Debe ser un nombre único, de lo contrario Hola publicar proceso producirá un error. Hola **Get-Date** elementos de fijación de comando en una cadena de fecha y hora que debe realizar nombre hello único.
* **-Location** especifica el centro de datos de Hola que se hospedará la aplicación hello en. una lista de centros de datos disponibles, utilice hello toosee **AzureLocation Get** cmdlet.
* **-Ejecute** abre una ventana del explorador y navega toohello hospedado servicio una vez completada la implementación.

Después de la publicación se realiza correctamente, verá un siguiente toohello similar de respuesta:

![salida de Hello de hello comando Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> Puede tardar varios minutos para toodeploy de aplicación hello y están disponible cuando se publicó por primera vez.

Cuando haya completado la implementación de hello, una ventana del explorador abrirá y navegar por el servicio en la nube toohello.

![Una ventana del explorador mostrar hello hello world página; dirección URL de Hello indica página Hola se hospeda en Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

La aplicación ya se está ejecutando en Azure.

Hola **AzureServiceProject publicar** cmdlet realiza Hola pasos:

1. Crea un paquete toodeploy. paquete de Hello contiene todos los archivos de hello en la carpeta de la aplicación.
2. Crea una nueva **cuenta de almacenamiento** si no hay ninguna disponible. Hola cuenta de almacenamiento de Azure es paquete de aplicación Hola toostore usado durante la implementación. Puede eliminar cuenta de almacenamiento de hello después de que se realice la implementación.
3. Crea un nuevo **servicio en la nube** si no hay ninguno disponible. A **servicio en la nube** es contenedor hello en el que se hospeda la aplicación cuando está implementado tooAzure. Para obtener más información, consulte [Información general de la creación de un servicio hospedado para Azure].
4. Publica tooAzure de paquete de implementación de Hola.

## <a name="stopping-and-deleting-your-application"></a>Detención y eliminación de la aplicación
Después de implementar la aplicación, puede que desee toodisable, por lo que puede evitar costos adicionales. Azure factura las instancias de rol web por hora consumida de tiempo de servidor. Hora del servidor se consume una vez implementada la aplicación, incluso si instancias de hello no se están ejecutando y están en estado de hello detenido.

1. En la ventana de Windows PowerShell de hello, detener la implementación de servicio de hello creado en la sección anterior de hello con hello siguiente cmdlet:

       Stop-AzureService

   Deteniendo el servicio de hello puede tardar varios minutos. Cuando se detiene el servicio de hello, recibirá un mensaje que indica que se ha detenido.

   ![estado de saludo del comando de hello Stop-AzureService][hello status of hello Stop-AzureService command]
2. servicio de hello toodelete, Hola llamada siguiente cmdlet:

       Remove-AzureService

   Cuando se le solicite, escriba **Y** toodelete servicio de Hola.

   Eliminando el servicio de hello puede tardar varios minutos. Después de que se ha eliminado el servicio de hello recibirá un mensaje que indica que el servicio de Hola se eliminó.

   ![estado de saludo del comando de hello Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Eliminando el servicio de hello no eliminar la cuenta de almacenamiento de Hola que se creó cuando se publicó inicialmente servicio hello y continuará toobe facturada almacenamiento utilizado. Si nada más usa el almacenamiento de hello, quizá le interese toodelete lo.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de Node.js].

<!-- URL List -->

[comparación de sitios Web de Azure, servicios en la nube y máquinas virtuales]: ../app-service-web/choose-web-site-cloud-service-vm.md
[utilizar una aplicación web ligera]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK para .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Conectar PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Información general de la creación de un servicio hospedado para Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centro para desarrolladores de Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
