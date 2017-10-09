---
title: "aaaInstall MongoDB en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se crea tooinstall MongoDB en una VM de Azure que ejecuta Windows Server 2012 R2 con el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Instalación y configuración de MongoDB en una máquina virtual Windows en Azure
[MongoDB](http://www.mongodb.org) es una conocida base de datos NoSQL de código abierto y alto rendimiento. Este artículo le guía a través de la instalación y configuración de MongoDB en una máquina virtual (VM) con Windows Server 2012 R2 en Azure. También es posible [instalar MongoDB en una máquina virtual Linux en Azure](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Requisitos previos
Antes de instalar y configurar MongoDB, necesita toocreate una máquina virtual y, idealmente, agregue un tooit de disco de datos. Vea Hola siguiendo artículos toocreate una máquina virtual y agregue un disco de datos:

* Crear una VM de Windows Server mediante [Hola portal de Azure](quick-create-portal.md) o [Azure PowerShell](quick-create-powershell.md).
* Adjuntar un uso de VM de Windows Server de datos disco tooa [Hola portal de Azure](attach-managed-disk-portal.md) o [Azure PowerShell](attach-disk-ps.md).

toobegin instalación y configuración de MongoDB, [tooyour VM de Windows Server de inicio de sesión](connect-logon.md) mediante Escritorio remoto.

## <a name="install-mongodb"></a>Instalación de MongoDB
> [!IMPORTANT]
> Las características de seguridad de MongoDB, como la vinculación de direcciones IP y la autenticación, no se encuentran habilitadas de forma predeterminada. Características de seguridad deben habilitarse antes de implementar el entorno de producción de MongoDB tooa. Para más información, consulte [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication) (Seguridad y autenticación de MongoDB).


1. Una vez haya conectado tooyour máquina virtual mediante Escritorio remoto, abra Internet Explorer de hello **iniciar** menú Hola máquina virtual.
2. Seleccione **Usar la configuración recomendada de compatibilidad, privacidad y seguridad** la primera vez que se abra Internet Explorer y haga clic en **Aceptar**.
3. De forma predeterminada está habilitada la configuración de seguridad mejorada de Internet Explorer. Agregar Hola MongoDB sitio Web toohello lista de sitios permitidos:
   
   * Seleccione hello **herramientas** icono en la esquina superior derecha de Hola.
   * En **opciones de Internet**, seleccione hello **seguridad** ficha y, a continuación, seleccione hello **sitios de confianza** icono.
   * Haga clic en hello **sitios** botón. Agregar *https://\*. mongodb.org* toohello lista de sitios de confianza y cuadro de diálogo de hello, a continuación, cierre.
     
     ![Configurar las opciones de seguridad de Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. Examinar toohello [MongoDB - descargas](http://www.mongodb.org/downloads) página (http://www.mongodb.org/downloads).
5. Si es necesario, seleccione hello **Community Server** edition y, a continuación, seleccione hello más reciente actual versión estable para Windows Server 2008 R2 de 64 bits y versiones posteriores. toodownload Hola instalador, haga clic en **descarga (msi)**.
   
    ![Descargue el instalador de MongoDB](./media/install-mongodb/download-mongodb.png)
   
    Ejecute el instalador de hello una vez completada la descarga de Hola.
6. Lea y acepte el contrato de licencia de Hola. Cuando se le pida, seleccione **Complete** (Completar) instalación.
7. En la pantalla final de bienvenida, haga clic en **instalar**.

## <a name="configure-hello-vm-and-mongodb"></a>Configurar Hola VM y MongoDB
1. no se actualizan las variables de ruta de acceso de Hello instalador de MongoDB Hola. Sin Hola MongoDB `bin` ubicación en la variable path, necesita ruta de acceso completa de toospecify Hola cada vez que use un archivo ejecutable de MongoDB. variable de ruta de acceso de tooadd Hola ubicación tooyour:
   
   * Menú contextual hello **iniciar** menú y seleccione **System**.
   * Haga clic en la pestaña **Configuración avanzada del sistema** y luego en **Variables de entorno**.
   * En **Variables del sistema**, seleccione **Path**, y, luego, haga clic en **Editar**.
     
     ![Configurar variables PATH](./media/install-mongodb/configure-path-variables.png)
     
     Agregar ruta de acceso de hello tooyour MongoDB `bin` carpeta. MongoDB se suele instalar en *C:\Archivos de programa\MongoDB*. Compruebe la ruta de instalación de hello en la máquina virtual. Hello en el ejemplo siguiente se agrega toohello de ubicación de instalación de hello predeterminado MongoDB `PATH` variable:
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Ser seguro tooadd Hola inicial punto y coma (`;`) tooindicate que va a agregar una ubicación tooyour `PATH` variable.

2. Cree los directorios de registro y datos de MongoDB en el disco de datos. De hello **iniciar** menú, seleccione **símbolo**. Hello en los ejemplos siguientes crea directorios de hello en la unidad F:
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Iniciar una instancia de MongoDB con hello siguiente comando, ajustar los datos de tooyour de ruta de acceso de Hola y los directorios de registro según corresponda:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Puede tardar varios minutos para MongoDB tooallocate archivos de diario de Hola y empiece a escuchar las conexiones. Todos los mensajes de registro son dirigido toohello *F:\MongoLogs\mongolog.log* archivo como `mongod.exe` server se inicia y asigna los archivos de diario.
   
   > [!NOTE]
   > símbolo de Hello permanece centrado en esta tarea mientras se ejecuta la instancia de MongoDB. Deje Hola símbolo ventana abierta toocontinue ejecutando MongoDB. O bien, instale MongoDB como servicio, tal como se detalla en el paso siguiente de saludo.

4. Para una experiencia más sólida de MongoDB, instale hello `mongod.exe` como un servicio. Creación de un servicio significa que no es necesario tooleave una línea de comandos que se ejecuta cada vez que desee toouse MongoDB. Crear servicio hello como se indica a continuación, ajustar Hola datos tooyour de ruta de acceso y los directorios de registro según corresponda:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Hello comando anterior crea un servicio denominado MongoDB, con una descripción de "Base de datos de Mongo". También se especifica Hola parámetros siguientes:
   
   * Hola `--dbpath` opción especifica la ubicación de Hola Hola del directorio de datos.
   * Hola `--logpath` opción debe ser toospecify usa un archivo de registro, porque el servicio en ejecución hello no tiene una salida de toodisplay de la ventana de comandos.
   * Hola `--logappend` opción especifica que un reinicio del servicio de hello hace el archivo de registro existente de salida tooappend toohello.
   
   servicio de MongoDB en hello toostart, ejecute el siguiente comando de hello:
   
    ```
    net start MongoDB
    ```
   
    Para obtener más información acerca de cómo crear el servicio de MongoDB hello, consulte [configurar un servicio de Windows para MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Instancia de prueba Hola MongoDB
Con MongoDB ejecutándose como una instancia individual o instalado como un servicio, ya puede comenzar la creación y uso de las bases de datos. Hola toostart MongoDB shell administrativo, abra otra ventana del símbolo del sistema de hello **iniciar** menú y escriba el siguiente comando de hello:

```
mongo  
```

Puede enumerar las bases de datos de hello con hello `db` comando. Inserte algunos datos como sigue:

```
db.foo.insert( { a : 1 } )
```

Busque datos como sigue:

```
db.foo.find()
```

Hola de salida es similar toohello siguiente ejemplo:

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Hola de salida `mongo` consola como se indica a continuación:

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Configuración de reglas del grupo de seguridad de red y del firewall
Ahora que MongoDB está instalado y en ejecución, abra un puerto en Firewall de Windows para que pueda conectarse de forma remota tooMongoDB. toocreate un nueva regla de entrada tooallow el puerto TCP 27017, abra un símbolo del sistema administrativo de PowerShell y escriba Hola siguiente comando:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

También puede crear reglas de hello mediante hello **Firewall de Windows con seguridad avanzada** herramienta de administración gráfica. Crear un nueva regla de entrada tooallow el puerto TCP 27017.

Si es necesario, cree un grupo de seguridad de red regla tooallow acceso tooMongoDB desde fuera de la subred de red virtual de Azure existente Hola. Puede crear hello las reglas del grupo de seguridad de red mediante hello [portal de Azure](nsg-quickstart-portal.md) o [Azure PowerShell](nsg-quickstart-powershell.md). Al igual que con las reglas de Firewall de Windows hello, permitir la interfaz de red virtual de TCP puerto 27017 toohello de la VM de MongoDB.

> [!NOTE]
> Puerto TCP 27017 es Hola predeterminado utilizado por MongoDB. Puede cambiar este puerto mediante hello `--port` parámetro al iniciar `mongod.exe` manualmente o desde un servicio. Si cambia el puerto de hello, realizar seguros reglas tooupdate de grupo de seguridad de red y Firewall de Windows hello en hello pasos anteriores.


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, se habrá aprendido cómo tooinstall y configurar MongoDB en la máquina virtual de Windows. Ahora puedes acceder MongoDB en su máquina virtual de Windows, por siguientes Hola temas avanzados de hello [la documentación de MongoDB](https://docs.mongodb.com/manual/).

