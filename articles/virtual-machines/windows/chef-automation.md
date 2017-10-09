---
title: "implementación de máquina virtual de aaaAzure con Chef | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Chef toodo automatiza la implementación de máquina virtual y la configuración en Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Automatización de la implementación de la máquina virtual de Azure con Chef
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef es una fantástica herramienta para ofrecer automatización y las configuraciones de estado que desee.

Con la versión más reciente de api de la nube, Chef proporciona una perfecta integración con Azure, lo que le ofrece Hola tooprovision de capacidad e implementar los Estados de configuración a través de un solo comando.

En este artículo, mostraré cómo tooset seguridad su tooprovision de entorno virtual de Azure de Chef máquinas y le guían en la creación de una directiva o un "Libro de cocina" y, a continuación, implementar esta máquina virtual de Azure tooan de libro de cocina.

Vamos a comenzar

## <a name="chef-basics"></a>Conceptos básicos de Chef
Antes de comenzar, le sugiero que revise los conceptos básicos de Hola de Chef. Hay gran material <a href="http://www.chef.io/chef" target="_blank">aquí</a> y recomiendo una lectura rápida antes de realizar este tutorial. Sin embargo se resumen de conceptos básicos de hello antes de empezar.

Hola siguiente diagrama muestra la arquitectura de Chef de alto nivel de Hola.

![][2]

Chef tiene tres componentes de arquitectura principales: servidor de Chef, cliente de Chef (nodo) y estación de trabajo de Chef.

Hola el servidor de Chef es el punto de administración y hay dos opciones para el servidor de Chef hello: una solución hospedada o una solución local. Vamos a usar una solución hospedada.

Cliente de Chef Hello (nodo) es agente de Hola que se ubica en los servidores de hello que está administrando.

Hola la estación de trabajo es nuestra estación de trabajo de administración donde se crean nuestras directivas y ejecutan los comandos de la administración. Ejecutamos hello **knife** nuestra infraestructura de comandos de hello toomanage de la estación de trabajo.

También hay concepto de Hola de "Cocina" y "Recetas". Estas son las directivas de Hola se defina y aplican tooour servidores.

## <a name="preparing-hello-workstation"></a>Preparar la estación de trabajo de Hola
En primer lugar, permite la estación de trabajo de preparación Hola. Estoy usando una estación de trabajo de Windows estándar. Necesitamos toocreate un toostore directory nuestros archivos de configuración y los libros de cocina.

En primer lugar, cree un directorio denominado C:\chef.

A continuación, cree un segundo directorio denominado c:\chef\cookbooks.

Ahora necesitamos toodownload nuestro archivo de configuración de Azure para que Chef pueda comunicarse con nuestra suscripción de Azure.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
Descargar su configuración mediante hello PowerShell Azure de publicación [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) comando. 

Guardar Hola publicar el archivo de configuración en C:\chef.

## <a name="creating-a-managed-chef-account"></a>Crear una cuenta de Chef administrada
Regístrese para una cuenta de Chef hospedada [aquí](https://manage.chef.io/signup).

Durante el proceso de registro de hello, estará más frecuentes toocreate una nueva organización.

![][3]

Una vez creada la organización, descargue el starter kit de Hola.

![][4]

> [!NOTE]
> Si recibe un mensaje que le advierte de que las claves se restablecerá, es aceptar tooproceed tal y como se dispone de ninguna infraestructura configurada todavía.
> 
> 

El archivo zip del starter kit contiene sus claves y archivos de configuración de la organización.

## <a name="configuring-hello-chef-workstation"></a>Configurar la estación de trabajo de Chef Hola
Extraer contenido de Hola de hello chef starter.zip tooC:\chef.

Copie todos los archivos en el repositorio de chef starter\chef\.chef tooyour c:\chef directory.

El directorio debe ser ahora algo parecido a Hola siguiente ejemplo.

![][5]

Ahora debería tener cuatro archivos incluidos Hola archivo de publicación de Azure en la raíz de Hola de c:\chef.

archivos PEM de Hello contienen la organización y administración de claves privadas para la comunicación al archivo de hello knife.rb contiene la configuración de knife. Necesitamos archivo knife.rb de tooedit hello.

Abra el archivo hello en el editor que prefiera y modificar cookbook_path"hello" mediante la eliminación de Hola /... / desde la ruta de acceso de Hola por lo que parece tal y como se muestra a continuación.

    cookbook_path  ["#{current_dir}/cookbooks"]

Agregar siguiente Hola línea reflejan nombre Hola de Azure publicar el archivo de configuración.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

El archivo knife.rb debe ser ahora similar toohello siguiente ejemplo.

![][6]

Estas líneas garantizará que hace referencia a directorio de guías de hello en c:\chef\cookbooks Knife y también usa el archivo de configuración de publicación de Azure durante las operaciones de Azure.

## <a name="installing-hello-chef-development-kit"></a>Hola Chef Development Kit de instalación
Siguiente [descargar e instalar](http://downloads.getchef.com/chef-dk/windows) Hola tooset ChefDK (Chef Development Kit) de la estación de trabajo de Chef.

![][7]

Instalar en la ubicación predeterminada de Hola de c:\opscode. Esta instalación tardará unos 10 minutos.

Confirme que la variable PATH contiene entradas para C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin

Si no están ahí, asegúrese de agregar estas rutas de acceso.

*Tenga en cuenta Hola orden de Hola ruta de acceso es importante.* Si las rutas de acceso de opscode no están en orden correcto de hello tendrán problemas.

Reinicie la estación de trabajo antes de continuar.

A continuación, se instalará la extensión de Azure de Knife Hola. Esto proporciona cuchilla con hello "Complemento de Azure".

Ejecutar el siguiente comando de Hola.

    chef gem install knife-azure ––pre

> [!NOTE]
> argumento de Hello – pre garantiza que recibe la versión más reciente de RC Hola de hello complemento de Azure de Knife que proporciona acceso toohello último conjunto de API.
> 
> 

Es probable que también se instala un número de dependencias en hello mismo tiempo.

![][8]

tooensure que todo está configurado correctamente, Hola ejecución siguiente comando.

    knife azure image list

Si todo está configurado correctamente, verá una lista de imágenes de Azure disponibles en desplazamiento.

¡Enhorabuena! ¡se configura la estación de trabajo de Hola!

## <a name="creating-a-cookbook"></a>Crear una guía
Se utiliza un libro de cocina por Chef toodefine un conjunto de comandos que desea tooexecute en el cliente administrado. Crear un libro de cocina es sencillo y usamos hello **chef generar el libro de cocina** comando toogenerate la plantilla de libro de cocina. Llamaré a mi servidor web de Cookbook ya que me gustaría una directiva que implemente IIS automáticamente.

En el directorio C:\Chef ejecute hello siguiente comando.

    chef generate cookbook webserver

Esto generará un conjunto de archivos en el directorio de hello C:\Chef\cookbooks\webserver. Ahora necesitamos conjunto de hello toodefine de comandos que nos gustaría nuestro tooexecute de cliente de Chef en la máquina virtual administrado.

comandos de Hola se almacenan en hello archivo default.rb. En este archivo, podrá definir un conjunto de comandos que se instala IIS, IIS se inicia y se copia una carpeta de plantilla archivo toohello wwwroot.

Modificar el archivo de C:\chef\cookbooks\webserver\recipes\default.rb hello y agregue Hola siguiendo las líneas.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

Guarde el archivo hello cuando haya terminado.

## <a name="creating-a-template"></a>Crear una plantilla
Como mencionamos anteriormente, necesitamos toogenerate un archivo de plantilla que se usará como nuestra página de default.html.

Ejecute hello después de la plantilla del comando toogenerate Hola.

    chef generate template webserver Default.htm

Ahora, explore toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb archivo. Editar archivo hello agregando código HTML "Hello World" simple y, a continuación, guarde el archivo hello.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Cargar Hola libro de cocina toohello el servidor de Chef
En este paso, estamos teniendo una copia del programa Hola libro de cocina que hemos creado en el equipo local y cargarlo toohello el servidor de Chef hospedada. Una vez cargado, Hola libro de cocina aparecerá en hello **directiva** ficha.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Implementar una máquina virtual con Knife Azure
Ahora agregaremos implementar una máquina virtual de Azure y aplicar Hola libro de cocina "Webserver" que se instalará nuestra página de web IIS web predeterminada y el servicio.

En el orden toodo esto, usar hello **crear servidor de azure de knife** comando.

Estoy de ejemplo de Hola comando aparece a continuación.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

parámetros de Hello son autoexplicativos. Sustituir sus variables concretas y ejecutar.

> [!NOTE]
> A través de la línea de comandos de Hola Hola, estoy automatizar mis reglas de filtro de red de punto de conexión mediante el uso de parámetros de los puntos de conexión de tcp: Hola. He abierto los puertos 80 y 3389 tooprovide acceso toomy web página y sesión RDP.
> 
> 

Una vez que ejecute el comando hello, vaya toohello Azure portal y verá su equipo empezar tooprovision.

![][13]

símbolo de Hello aparece a continuación.

![][10]

Una vez completada la implementación de hello, deberíamos estar servicio web de tooconnect puede toohello en el puerto 80 tal y como se hubiera abierto el puerto de hello cuando se aprovisiona máquina virtual de hello con hello comando Knife de Azure. Puesto que esta máquina virtual es Hola de máquina virtual solo en mi servicio de nube, conectará con la dirección url del servicio de nube de Hola.

![][11]

Como puede observar, me ha entrado la creatividad con mi código HTML.

No olvide que también podemos conectarnos a través de una sesión RDP de hello portal de Azure en el puerto 3389.

Espero que esto les haya resultado útil. Empiece hoy su viaje de su infraestructura como código con Azure.

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
