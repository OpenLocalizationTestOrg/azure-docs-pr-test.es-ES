---
title: "aaaSet seguridad Apache Tomcat en una máquina virtual Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset una Tomcat7 Apache mediante el uso de máquinas virtuales de Azure ejecutan Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>Configuración de Tomcat7 en una máquina virtual con Linux con Azure
Apache Tomcat (o simplemente Tomcat, también se denominaba Tomcat Yakarta) es un contenedor de servlet desarrollado por hello Apache Software Foundation (ASF) y el servidor web de código abierto. Tomcat implementa hello Servlet de Java y especificaciones de hello JavaServer Pages (JSP) de Sun Microsystems. Tomcat proporciona un entorno puro de servidor de web HTTP de Java en qué toorun código Java. Configuración más sencilla de hello, Tomcat se ejecuta en un proceso de sistema operativo único. Este proceso ejecuta una máquina virtual de Java (JVM). Todas las solicitudes HTTP desde un explorador tooTomcat se procesan como un subproceso independiente en el proceso de Tomcat Hola.  

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [Azure Resource Manager y el modelo clásico](../../../resource-manager-deployment-model.md). Este artículo trata cómo toouse Hola modelo de implementación clásica. Se recomienda el uso de modelo del Administrador de recursos de hello en implementaciones más nuevas. toouse un toodeploy de plantilla de administrador de recursos una VM de Ubuntu con Openjdk y Tomcat, consulte [este artículo](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).

En este artículo, instalará Tomcat7 en una imagen de Linux y la implementará en Azure.  

Aprenderá a:  

* ¿Cómo toocreate una máquina virtual en Azure.
* ¿Cómo tooprepare Hola máquina virtual para Tomcat7.
* Cómo tooinstall Tomcat7.

Se supone que ya tiene una suscripción a Azure.  Si no es así, puede suscribirse a una prueba gratuita en [Hola sitio Web de Azure](https://azure.microsoft.com/). Si tiene una suscripción de MSDN, consulte [Precios especiales de Microsoft Azure: Ventajas de MSDN, MPN y Bizspark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39). toolearn más información acerca de Azure, consulte [¿qué es Azure?](https://azure.microsoft.com/overview/what-is-azure/).

En este artículo se supone que tiene conocimientos prácticos básicos de Tomcat y Linux.  

## <a name="phase-1-create-an-image"></a>Fase 1: Creación de una imagen
En esta fase, creará una máquina virtual mediante una imagen de Linux en Azure.  

### <a name="step-1-generate-an-ssh-authentication-key"></a>Paso 1: Generación de una clave de autenticación SSH
SSH es una herramienta importante para los administradores del sistema. Pero no se recomienda configurar la seguridad del acceso mediante una contraseña determinada por personas. Los usuarios malintencionados pueden acceder a su sistema si está protegido por un nombre de usuario y una contraseña débiles.

buenas noticias de Hello son que hay una forma de acceso remoto tooleave abrir y no se preocupe acerca de las contraseñas. Este método consiste en la autenticación con criptografía asimétrica. Hello clave privada del usuario es hello que concede autenticación Hola. Incluso puede bloquear la cuenta de usuario de hello toonot permitir la autenticación de contraseña.

Otra ventaja de este método es que no es necesario toosign contraseñas diferentes en los servidores de toodifferent. Puede autenticar mediante clave privada de hello personal en todos los servidores, lo que evitará tener tooremember varias contraseñas.



Siga estos pasos toogenerate Hola autenticación la clave SSH.

1. Descargue e instale PuTTYgen desde Hola ubicación siguiente: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Ejecute Puttygen.exe.
3. Haga clic en **generar** claves de hello toogenerate. En el proceso de hello, puede crecer aleatoriedad con el mouse de hello móvil en área en blanco de hello en ventana hello.  
   ![Captura de pantalla de generador de claves puTTY que muestra hello generar nuevo botón clave][1]
4. Una vez Hola generar proceso, Puttygen.exe mostrará la nueva clave pública.  
   ![Captura de pantalla de generador de claves puTTY que muestra la nueva clave pública de Hola y Hola guardar botón clave privada][2]
5. Seleccione y copie la clave pública de Hola y guardarlo en un archivo denominado publicKey.pem. No haga clic en **guardar de clave pública**, ya que es diferente de la clave pública de hello queremos Hola guarda el formato de archivo de la clave pública.
6. Haga clic en **Guardar clave privada** y guárdela en un archivo denominado privateKey.ppk.

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>Paso 2: Crear la imagen de Hola Hola portal de Azure
1. Hola [portal](https://portal.azure.com/), haga clic en **New** Hola de tareas de la barra toocreate una imagen. A continuación, elija la imagen de Linux de Hola que se basa en sus necesidades. Hello en el ejemplo siguiente se usa Hola Ubuntu 14.04 imagen.
![Captura de pantalla de portal de Hola que muestra el botón nuevo Hola][3]

2. Para **nombre de Host**, especificar nombre de Hola de dirección URL de Hola que clientes de Internet y se utilizará tooaccess esta máquina virtual. Definir la última parte del nombre DNS de hello, por ejemplo, tomcatdemo de Hola. Azure, a continuación, generará la dirección URL de hello como tomcatdemo.cloudapp.net.  

3. Para **clave de autenticación SSH**, copie el valor de clave de Hola desde archivo publicKey.pem de hello, que contiene la clave pública de hello generada por PuTTYgen.  
![Cuadro clave de autenticación de SSH en el portal de Hola][4]

4. Configure otras opciones según sea necesario y, luego, haga clic en **Crear**.  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>Fase 2: Preparación de la máquina virtual para Tomcat7
En esta fase, configurará un punto de conexión para el tráfico de Tomcat y, a continuación, conecte la nueva máquina virtual de tooyour.

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>Paso 1: Abra Hola HTTP puerto tooallow web access
Los puntos de conexión en Azure constan de un protocolo TCP o UDP, junto con un puerto público y privado. Hola privada Hola puerto es que el servicio de hello está escuchando máquina virtual de tooon Hola. Puerto público Hello es puerto Hola Hola servicio de nube de Azure escucha tooexternally para el tráfico entrante, basado en Internet.  

El puerto TCP 8080 es el número de puerto predeterminado de Hola que Tomcat usa toolisten. Si se abre este puerto con un punto de conexión de Azure, usted y otros clientes de Internet pueden acceder a páginas de Tomcat.  

1. En el portal de hello, haga clic en **examinar** > **máquinas virtuales**y, a continuación, haga clic en la máquina virtual Hola que creó.  
   ![Captura de pantalla de directorio de máquinas virtuales de Hola][5]
2. tooadd una máquina virtual de tooyour de punto de conexión, haga clic en hello **extremos** cuadro.
   ![Captura de pantalla que muestra el cuadro de puntos de conexión de Hola][6]
3. Haga clic en **Agregar**.  

   1. Para el extremo de hello, escriba un nombre de extremo de hello en **extremo**y, a continuación, escriba 80 en **puerto público**.  

      Si se establece too80, no es necesario tooinclude número de puerto de hello en dirección URL de Hola que es usado tooaccess Tomcat. Por ejemplo, http://tomcatdemo.cloudapp.net.    

      Si se establece el valor de tooanother, como 81, deberá tooadd Hola puerto número toohello URL tooaccess Tomcat. Por ejemplo, http://tomcatdemo.cloudapp.net:81/.
   2. Escriba 8080 en **Puerto privado**. De manera predeterminada, Tomcat escucha en el puerto TCP 8080. Si ha cambiado el puerto de escucha de predeterminado Hola de Tomcat, debe actualizar **puerto privado** toobe Hola igual Hola puerto de escucha de Tomcat.  
      ![Captura de pantalla de interfaz de usuario que muestra Agregar comando, Puerto público y Puerto privado][7]
4. Haga clic en **Aceptar** tooadd Hola extremo tooyour virtual machine.

### <a name="step-2-connect-toohello-image-you-created"></a>Paso 2: Conectar imagen toohello que ha creado
Puede elegir cualquier máquina virtual SSH herramienta tooconnect tooyour. En este ejemplo, se usa PuTTY.  

1. Obtener el nombre DNS de hello de la máquina virtual del portal de Hola.
    1. Haga clic en **Examinar** > **Máquinas virtuales**.
    2. Seleccione Hola nombre de la máquina virtual y, a continuación, haga clic en **propiedades**.
    3. Hola **propiedades** icono, mire en hello **nombre de dominio** nombre DNS del cuadro de tooget Hola.  

2. Obtener el número de puerto de Hola para las conexiones de SSH de hello **SSH** cuadro.  
![Captura de pantalla que muestra el número de puerto de conexión de SSH de Hola][8]

3. Descargue [PuTTY](http://www.putty.org/).  

4. Después de la descarga, haga clic en el archivo ejecutable hello Putty.exe. En configuración de PuTTY, configurar las opciones básicas de hello con el nombre de host de Hola y el puerto número que se obtiene de las propiedades de saludo de la máquina virtual.   
![Captura de pantalla que muestra las opciones de nombre y el puertos de host de configuración PuTTY de Hola][9]

5. En el panel izquierdo de hello, haga clic en **conexión** > **SSH** > **Auth**y, a continuación, haga clic en **examinar** toospecify ubicación de Hello del archivo de privateKey.ppk de Hola. archivo privateKey.ppk de Hello contiene la clave privada de hello generadas por PuTTYgen anteriormente en hello "fase 1: crear una imagen" sección de este artículo.  
![Captura de pantalla que muestra la jerarquía de directorios de conexión de Hola y el botón Examinar][10]

6. Haga clic en **Abrir**. Puede recibir una alerta en un cuadro de mensaje. Si se ha configurado el nombre DNS de Hola y el número de puerto correctamente, haga clic en **Sí**.
![Captura de pantalla que muestra la notificación de Hola][11]

7. Se está tooenter solicitada su nombre de usuario.  
![Captura de pantalla que muestra un caso donde el nombre de usuario de tooenter][12]

8. Escribir nombre de usuario de Hola que usa máquinas virtuales de toocreate Hola Hola "fase 1: crear una imagen" anteriormente en este artículo. Verá algo parecido a Hola siguiente:  
![Captura de pantalla que muestra la confirmación de la autenticación de Hola][13]

## <a name="phase-3-install-software"></a>Fase 3: Instalación del software
En esta fase, instale el entorno de tiempo de ejecución de Java de hello, Tomcat7 y otros componentes de Tomcat7.  

### <a name="java-runtime-environment"></a>Java Runtime Environment
Tomcat está escrito en Java. Existen dos tipos de kits de desarrollo de Java (JDK): OpenJDK y JDK de Oracle. Puede elegir Hola que desee.  

> [!NOTE]
> Tanto JDK tiene casi Hola el mismo código para las clases de Hola Hola API Java y código de hello para la máquina virtual de hello es diferente. OpenJDK suele bibliotecas abiertas toouse, mientras que Oracle JDK tiende toouse cerrado los. JDK de Oracle tiene más clases y algunos errores corregidos. Además, JDK de Oracle es más estable que OpenJDK.

#### <a name="install-openjdk"></a>Instalación de OpenJDK  

Usar hello después toodownload OpenJDK de comando.   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* toocreate un toocontain directory Hola archivos JDK:  

        sudo mkdir /usr/lib/jvm  
* archivos JDK de hello tooextract en el directorio/usr/lib/jvm/hello:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>Instalación de JDK de Oracle


Usar hello siguientes toodownload comando Oracle JDK de sitio Web de Oracle Hola.  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* toocreate un toocontain directory Hola archivos JDK:  

        sudo mkdir /usr/lib/jvm  
* archivos JDK de hello tooextract en el directorio/usr/lib/jvm/hello:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* tooset Oracle JDK como Hola máquina virtual Java a predeterminada:  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>Confirmación de que la instalación de Java es correcta
Puede utilizar un comando como Hola después tootest si Hola Java runtime environment está instalado correctamente:  

    java -version  

Si ha instalado OpenJDK, verá un mensaje similar Hola siguiente: ![mensaje de instalación OpenJDK correcta][14]

Si ha instalado Oracle JDK, verá un mensaje similar Hola siguiente: ![mensaje de instalación de JDK correcta de Oracle][15]

### <a name="install-tomcat7"></a>Instalación de Tomcat7
Usar hello después comando tooinstall Tomcat7.  

    sudo apt-get install tomcat7  

Si no utilizas Tomcat7, utilice variación correspondiente de Hola de este comando.  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>Confirmación de que la instalación de Tomcat7 es correcta
toocheck si Tomcat7 se instala correctamente, busque nombre DNS del servidor de Tomcat tooyour. En este artículo, dirección URL de ejemplo de Hola es http://tomcatexample.cloudapp.net/. Si ve un mensaje similar siguiente hello, Tomcat7 está instalado correctamente.
![Mensaje de instalación Tomcat7 correcta][16]

### <a name="install-other-tomcat7-components"></a>Instalación de otros componentes de Tomcat7
Hay otros componentes de Tomcat opcionales que puede instalar.  

Hola de uso **tomcat7 de búsqueda de caché apt sudo** comando toosee todos los componentes disponibles de Hola. Usar hello después comandos tooinstall algunos componentes útiles.  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>Fase 4: Configuración de Tomcat7
En esta fase es donde se administra Tomcat.

### <a name="start-and-stop-tomcat7"></a>Inicio y detención de Tomcat7
servidor de Tomcat7 Hola se inicia automáticamente cuando se instala. También puede iniciarlo con hello siguiente comando:   

    sudo /etc/init.d/tomcat7 start

toostop Tomcat7:

    sudo /etc/init.d/tomcat7 stop

estado de hello tooview de Tomcat7:

    sudo /etc/init.d/tomcat7 status

Servicios de Tomcat toorestart: 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Administración de Tomcat7
Puede editar tooset del archivo de configuración de hello Tomcat usuario sus credenciales de administrador. Usar hello siguiente comando:  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

Aquí tiene un ejemplo:  
![Captura de pantalla que muestra el resultado del comando hello sudo vi][17]  

> [!NOTE]
> Crear una contraseña segura para el nombre de usuario de administrador de Hola.  

Después de editar este archivo, debe reiniciar servicios Tomcat7 con hello después tooensure de comando que Hola cambios surten efecto:  

    sudo /etc/init.d/tomcat7 restart  

Abra el explorador y escriba **http://<your tomcat server DNS name>/administrador/html** como Hola dirección URL. Por ejemplo hello en este artículo, dirección URL de hello es http://tomcatexample.cloudapp.net/manager/html.  

Después de conectarse, verá algo similar siguiente toohello:  
![Captura de pantalla de hello Administrador de aplicaciones Web Tomcat][18]

## <a name="common-issues"></a>Problemas comunes
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>No puede acceder a la máquina virtual de hello con Tomcat y Moodle de hello Internet
#### <a name="symptom"></a>Síntoma  
  Tomcat se está ejecutando pero no puede ver la página predeterminada de hello Tomcat con el explorador.
#### <a name="possible-root-cause"></a>Posible causa principal   

  * puerto de escucha de Hello Tomcat no se Hola igual que el puerto privado de Hola de punto de conexión de su máquina virtual para el tráfico de Tomcat.  

     Compruebe su puerto público y privado configuración de punto de conexión del puerto y asegúrese de que el puerto privado hello es Hola igual Hola Tomcat el puerto de escucha. Consulte la sección de este artículo "Fase 1: Crear una imagen" para obtener instrucciones acerca de cómo configurar puntos de conexión para la máquina virtual.  

     Hola toodetermine Tomcat puerto de escucha, abra /etc/httpd/conf/httpd.conf (versión de Red Hat) o /etc/tomcat7/server.xml (Debian versión). De forma predeterminada, puerto de escucha de Tomcat hello es 8080. Aquí tiene un ejemplo:  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     Si utilizas una máquina virtual como Debian o Ubuntu y desea que toochange Hola predeterminado puerto de Tomcat escuchar (por ejemplo 8081), también debe abrir los puertos de hello para el sistema operativo de Hola. En primer lugar, abra el perfil de hello:  

        sudo vi /etc/default/tomcat7  

     A continuación, quite la última línea de Hola y cambiar "no" demasiado "Sí".  

        AUTHBIND=yes
  2. firewall de Hello deshabilitó Hola puerto de escucha de Tomcat.

     Sólo puede ver la página de hello Tomcat predeterminada desde el host local de Hola. problema de Hello es muy probable que el puerto de hello, que es tooby escuchaba Tomcat, está bloqueado por firewall de Hola. Puede usar la página de Web de hello w3m herramienta toobrowse Hola. Hello siguientes comandos instalación w3m y examinar la página predeterminada de Tomcat de toohello:  


        sudo yum install w3m w3m-img


        w3m http://localhost:8080  
#### <a name="solution"></a>Solución

  * Si Hola puerto de escucha de Tomcat no se hello igual como puerto privado de Hola de punto de conexión de hello para la máquina virtual de tráfico toohello, es necesario cambiar el puerto privado hello toobe Hola igual Hola puerto de escucha de Tomcat.   
  2. Si el problema de hello está provocado por firewall/iptables, agregue Hola después líneas demasiado/etcetera/sysconfig/iptables. segunda línea de Hello solo es necesario para el tráfico https:  

      -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT

      -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT  

     > [!IMPORTANT]
     > Asegúrese de que líneas anteriores Hola se colocan por encima de todas las líneas que global se podrían restringir el acceso, como siguiente hello: - A -j rechazar--icmp-host-prohibido con rechazo de entrada



tooreload hello iptables, ejecute el siguiente comando de hello:

    service iptables restart

Esto se ha probado en CentOS 6.3.

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>Permiso denegado al cargar el proyecto archivos demasiado/var/lib/tomcat7/aplicaciones Web /
#### <a name="symptom"></a>Síntoma
  Al usar una máquina virtual SFTP cliente (por ejemplo, FileZilla) tooconnect tooyour y navegue demasiado/var/lib/tomcat7/aplicaciones Web/toopublish su sitio, obtendrá un siguiente de toohello similar de mensaje de error:  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>Posible causa principal
  No tener ninguna carpeta de /var/lib/tomcat7/webapps de permisos tooaccess Hola.  
#### <a name="solution"></a>Solución  
  Necesita permiso de tooget de cuenta de hello raíz. Puede cambiar la propiedad de Hola de esa carpeta de nombre de usuario raíz toohello que usó al aprovisionar la máquina de Hola. Este es un ejemplo con el nombre de la cuenta de hello azureuser:  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  Usar permisos de hello -R opción tooapply Hola para todos los archivos dentro de un directorio demasiado.  

  Este comando también funciona para directorios. cambios en las opciones -R Hola Hola permisos para todos los archivos y directorios dentro del directorio de Hola. Aquí tiene un ejemplo:  

     sudo chown -R username:group directory  

  Este comando cambia la propiedad (usuario y grupo) de todos los archivos y directorios que están dentro del directorio de Hola.  

  Hello siguiente comando solo cambia Hola permisos de directorio de la carpeta de Hola. Hola archivos y carpetas dentro del directorio de hello no cambian.  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
