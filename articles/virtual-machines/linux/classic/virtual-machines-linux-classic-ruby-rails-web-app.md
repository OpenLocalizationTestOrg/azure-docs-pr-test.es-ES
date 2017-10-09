---
title: "aaaHost un Ruby en el sitio Web de raíles en una VM Linux | Documentos de Microsoft"
description: "Configure y hospede un sitio web basado en Ruby on Rails en Azure usando una máquina virtual de Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Aplicación web de Ruby on Rails en una máquina virtual de Azure
Este tutorial se muestra cómo toohost un Ruby en el sitio Web de raíles en Azure con una máquina virtual Linux.  

Este tutorial se validó con Ubuntu Server 14.04 LTS. Si utiliza una distribución de Linux diferente, tendrá que toomodify Hola pasos tooinstall raíles.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.
>
>

## <a name="create-an-azure-vm"></a>Creación de una máquina virtual de Azure
Empiece por crear una máquina virtual de Azure con una imagen de Linux.

toocreate Hola VM, puede usar hello portal de Azure u Hola interfaz de línea de comandos (CLI) de Azure.

### <a name="azure-portal"></a>Azure Portal
1. Inicio de sesión en hello [portal de Azure](https://portal.azure.com)
2. Haga clic en **nuevo**, a continuación, escriba "Ubuntu Server 14.04" en el cuadro de búsqueda de Hola. Haga clic en la entrada Hola devuelto por la búsqueda de Hola. Para el modelo de implementación de hello, seleccione **clásico**, a continuación, haga clic en "Crear".
3. En la hoja de conceptos básicos de hello, proporcionar valores para campos de hello necesaria: nombre (para Hola VM), nombre de usuario, tipo de autenticación y las credenciales correspondientes de hello, suscripción de Azure, grupo de recursos y ubicación.

   ![Creación de una imagen Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Después de aprovisiona Hola VM, haga clic en el nombre de la máquina virtual de Hola y haga clic en **extremos** en hello **configuración** categoría. Buscar el punto de conexión SSH de hello, aparecen en **independiente**.

   ![Punto de conexión predeterminado](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>CLI de Azure
Siga los pasos de hello en [crear una máquina Virtual ejecuta Linux][vm-instructions].

Después de aprovisiona Hola VM, puede obtener el punto de conexión de hello SSH ejecutando el siguiente comando de hello:

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>Instalación de Ruby on Rails
1. Utilizar SSH tooconnect toohello máquina virtual.
2. Desde la sesión de SSH de hello, usar hello siga comandos tooinstall Ruby en hello VM:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    instalación de Hello puede tardar unos minutos. Cuando se complete, use Hola después tooverify de comando que está instalado Ruby:

        ruby -v

3. Siguiente Hola de uso de comandos de raíles de tooinstall:

        sudo gem install rails --no-rdoc --no-ri -V

    Usar hello--rdoc n y--tooskip marcas ri no instalar la documentación de hello, que es más rápido.
    Este comando es probable que tardará mucho tiempo tooexecute, por lo que agregar Hola -V mostrará información sobre el progreso de la instalación de Hola.

## <a name="create-and-run-an-app"></a>Creación y ejecución de una aplicación
Sin cerrar la sesión a través de SSH, ejecute hello siguientes comandos:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Hola [nueva](http://guides.rubyonrails.org/command_line.html#rails-new) comando crea una nueva aplicación de raíles. Hola [server](http://guides.rubyonrails.org/command_line.html#rails-server) comando inicia Hola WEBrick servidor de web que se incluye con los raíles. (Para su uso en producción, probablemente querría toouse un servidor diferente, como unicornio o pasajeros.)

Debería aparecer resultados similares toohello siguiente.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Agregación de un extremo
1. Vaya toohello [portal de Azure] [https://portal.azure.com] y seleccione la máquina virtual.

2. Seleccione **EXTREMOS** en hello **configuración** a lo largo de la página de Hola de hello borde izquierdo.

3. Haga clic en **agregar** al principio de Hola de página de Hola.

4. Hola **Agregar extremo** cuadro de diálogo página, escriba Hola siguiente información:

   * **Nombre**: HTTP
   * **Protocolo**: TCP
   * **Puerto público**: 80
   * **Puerto privado**: 3000
   * **Dirección IP flotante**: deshabilitada
   * **Lista de control de acceso - orden**: 1001 u otro valor que establece la prioridad de Hola de esta regla de acceso.
   * **Lista de control de acceso - Nombre**: allowHTTP
   * **Lista de control de acceso - Acción**: permit
   * **Lista de control de acceso - Subred remota**: 1.0.0.0/16

     Este punto de conexión tiene un puerto público 80 que se usará para enrutar el tráfico toohello puerto privado de 3000, donde está escuchando el servidor de raíles de Hola. regla de lista de control de acceso de Hello permite el tráfico público en el puerto 80.

     ![nuevo-punto-de-conexión](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Haga clic en el punto de conexión de Aceptar toosave Hola.

6. Debería aparecer un mensaje que indique: **Guardando el punto de conexión de la máquina virtual**. Una vez que este mensaje desaparece, el punto de conexión de hello está activo. Ahora puede probar la aplicación desplazándose toohello nombre DNS de la máquina virtual. sitio Web de Hello debe aparecer toohello similar a continuación:

    ![Página predeterminada de Rails][default-rails-cloud]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, se hizo la mayoría de los pasos de hello manualmente. En un entorno de producción, también podría escribir la aplicación en un equipo de desarrollo e implementarlo toohello máquina virtual de Azure. Además, la mayoría de los entornos de producción hospedan la aplicación de raíles de hello junto con otro proceso de servidor, como Apache o NginX, que controla solicitudes enrutamiento de toomultiple de instancias de aplicación de raíles de hello y que sirve al recursos estáticos. Para obtener más información, consulte http://rubyonrails.org/deploy/.

toolearn más información acerca de Ruby sobre raíles, visite hello [Ruby en guías de raíles][rails-guides].

Servicios de Azure de toouse desde la aplicación Ruby, vea:

* [Almacenamiento de datos no estructurados con blobs][blobs]
* [Almacenamiento de parejas de clave/valor con tablas][tables]
* [Servir el contenido de gran ancho de banda con hello red de entrega de contenido][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
