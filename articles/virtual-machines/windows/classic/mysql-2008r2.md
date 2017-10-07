---
title: "aaaCreate una VM de Azure clásico ejecute MySQL | Documentos de Microsoft"
description: "Cree una máquina virtual de Azure ejecuta Windows Server 2012 R2 y Hola base de datos de MySQL con el modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Instalar MySQL en una máquina virtual creada con el modelo de implementación clásica de Hola que ejecute Windows Server 2016
[MySQL](https://www.mysql.com) L es una conocida base de datos SQL de código abierto. Este tutorial muestra cómo tooinstall y ejecute hello **versión de comunidad de MySQL 5.7.18** como un servidor MySQL en una máquina virtual ejecuta **Windows Server 2016**. La experiencia podría ser ligeramente diferente con otras versiones de Windows Server o de MySQL.

Para obtener instrucciones sobre cómo instalar MySQL en Linux, consulte: [cómo tooinstall MySQL en Azure](../../linux/mysql-install.md).

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Crear una máquina virtual con Windows Server 2016
Si aún no tiene una máquina virtual que ejecute Windows Server 2016, puede usar esta [tutorial](./tutorial.md) máquina virtual de toocreate Hola.

## <a name="attach-a-data-disk"></a>Acoplamiento de un disco de datos
Después de crear la máquina virtual de hello, opcionalmente, puede adjuntar un disco de datos. Agregar que un disco de datos se recomienda para las cargas de trabajo de producción y tooavoid quedando sin espacio en la unidad del sistema operativo (C:) hello, que incluye el sistema operativo de Hola.

Vea [cómo tooattach datos de un disco de máquina virtual de Windows tooa](../attach-managed-disk-portal.md) y siga las instrucciones de Hola para conectar un disco vacío. Establecer Hola host caché demasiado**ninguno** o **de sólo lectura**.

## <a name="log-on-toohello-virtual-machine"></a>Inicie sesión en la máquina virtual de toohello
A continuación, podrá [inicie sesión en la máquina virtual de toohello](./connect-logon.md) por lo que puede instalar MySQL.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Instalar y ejecutar MySQL Community Server en la máquina virtual de Hola
Siga estos pasos tooinstall, configurar y ejecutar la versión de la Comunidad de Hola de MySQL Server:

> [!NOTE]
> Al descargar los elementos mediante Internet Explorer, puede establecer IE de hello **configuración de seguridad mejorada** tooOff y simplificar el proceso de descarga de Hola. Desde el menú de inicio de hello, haga clic en servidor de Manager/Local/servidor de herramientas administrativas, haga clic en Internet Explorer **configuración de seguridad mejorada** y establecer tooOff de configuración de hello).
>
>

1. Una vez haya conectado la máquina virtual de toohello mediante Escritorio remoto, haga clic en **Internet Explorer** de pantalla de inicio de bienvenida.
2. Seleccione hello **herramientas** situado en la esquina superior derecha de hello (icono de rueda cogged Hola) y, a continuación, haga clic en **opciones de Internet**. Haga clic en hello **seguridad** , haga clic en hello **sitios de confianza** icono y, a continuación, haga clic en hello **sitios** botón. Agregue http://*.mysql.com toohello lista de sitios de confianza. Haga clic en **Cerrar** y después en **Aceptar**.
3. En hello barra de direcciones de Internet Explorer, escriba https://dev.mysql.com/downloads/mysql/.
4. Use Hola MySQL sitio toolocate y descargar la versión más reciente de Hola de hello instalador de MySQL para Windows. Al elegir Hola instalador de MySQL, descargue la versión de Hola cuya Hola complete el conjunto de archivos (por ejemplo, hello mysql-instalador-Comunidad-5.7.18.0.msi con un tamaño de archivo de 352.8 MB) y guarde el instalador Hola.
5. Cuando haya acabado la descarga del instalador de hello, haga clic en **ejecutar** toolaunch el programa de instalación.
6. En hello **contrato de licencia** página, acepte el contrato de licencia de Hola y haga clic en **siguiente**.
7. En hello **elegir un tipo de instalación** página, haga clic en el tipo de instalación de Hola que desee y, a continuación, haga clic en **siguiente**. Hello siguientes pasos supone selección Hola de hello **sólo para el servidor** tipo de instalación.
8. Si hello **comprobar requisitos** muestra la página, haga clic en **Execute** el programa de instalación de toolet Hola instala los componentes que faltan. Siga las instrucciones que se muestran como Hola C++ Redistributable en tiempo de ejecución.
9. En hello **instalación** página, haga clic en **Execute**. Cuando la instalación se haya completado, haga clic en **Siguiente**.

10. En hello **configuración del producto** página, haga clic en **siguiente**.

11. En hello **redes y tipo** página, especifique los tipo y la conectividad de opciones de configuración deseadas, incluido el puerto TCP Hola si es necesario. Seleccione **Mostrar opciones avanzadas** y después haga clic en **Siguiente**.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. En hello **cuentas y Roles** página, especifique una contraseña segura de raíz de MySQL. Agregue cuentas de usuario de MySQL adicionales según sea necesario y haga clic en **Siguiente**.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. En hello **servicio de Windows** página, especifique toohello cambia la configuración del valor predeterminado para ejecutar Hola MySQL Server como un servicio de Windows según sea necesario y, a continuación, haga clic en **siguiente**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. Hola opciones en hello **complementos y extensiones** página son opcionales. Haga clic en **siguiente** toocontinue.
15. En hello **opciones avanzadas** página, especifique las opciones de toologging de cambios según sea necesario y, a continuación, haga clic en **siguiente**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. En hello **aplicar configuración de servidor** página, haga clic en **Execute**. Una vez completados los pasos de configuración de hello, haga clic en **finalizar**.
17. En hello **configuración del producto** página, haga clic en **siguiente**.
18. En hello **instalación finalizada** página, haga clic en **tooClipboard de copiar el registro** si desea tooexamine más tarde y, a continuación, haga clic en **finalizar**.
19. En la pantalla de inicio de bienvenida, escriba **mysql**y, a continuación, haga clic en **cliente de línea de comandos de MySQL 5.7**.
20. Escriba la contraseña de raíz de Hola que especificó en el paso 12 y se presentan con un símbolo del sistema donde puede emitir comandos tooconfigure MySQL. Para obtener detalles de Hola de comandos y la sintaxis, vea [manuales de referencia de MySQL](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. También puede configurar el servidor predeterminado de configuración como Hola base y directorios de datos y las unidades. Para más información, vea [6.1.2 Server Configuration Defaults (Valores predeterminados de configuración de Server 6.1.2)](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).

## <a name="configure-endpoints"></a>Configuración de extremos

Para los equipos de tooclient disponible toobe y servicio de MySQL hello en hello Internet, debe configurar un extremo para el puerto TCP de Hola y crear una regla de Firewall de Windows. valor de puerto predeterminado de Hello en qué servidor MySQL Hola servicio realiza escuchas para los clientes de MySQL es 3306. Puede especificar otro puerto, siempre que sea coherente con el valor de hello proporcionado en hello puerto hello **redes y tipo** página (paso 11 del procedimiento anterior de hello).

> [!NOTE]
> Para su uso en producción, considere la posibilidad de hello implicaciones de seguridad de hacer que Hola MySQL Server equipos de servicio tooall disponible en hello Internet. Puede definir conjunto de Hola de direcciones IP de origen que se permiten el extremo de hello toouse con una lista de Control de acceso (ACL). Para obtener más información, consulte [cómo tooSet extremos tooa Máquina Virtual](setup-endpoints.md).
>
>

tooconfigure un extremo para hello servicio MySQL Server:

1. Hola portal de Azure, haga clic en **máquinas virtuales (clásicas)**, haga clic en nombre de saludo de la máquina virtual de MySQL y, a continuación, haga clic en **extremos**.
2. En la barra de comandos de hello, haga clic en **agregar**.
3. En hello **Agregar extremo** página, escriba un nombre único para **nombre**.
4. Seleccione **TCP** como protocolo de Hola.
5. Escriba el número de puerto de hello, como **3306**, tanto en **puerto público** y **puerto privado**y, a continuación, haga clic en **Aceptar**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Agregar un tooallow de regla de Firewall de Windows tráfico de MySQL
tooadd una regla de Firewall de Windows que permite el tráfico de MySQL desde Hola Internet, ejecute hello siguiente comando en un _símbolo de Windows PowerShell con privilegios elevados_ en la máquina virtual de hello MySQL server.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Probar la conexión remota
tootest su Hola ejecución de conexión remota toohello Azure VM MySQL Server del servicio, debe proporcionar Hola de nombre DNS del servicio de nube de Hola que contiene Hola VN.

1. Hola portal de Azure, haga clic en **máquinas virtuales (clásicas)**, haga clic en nombre de saludo de la máquina virtual de MySQL server y, a continuación, haga clic en **Introducción**.
2. En el panel de la máquina virtual de hello, tenga en cuenta hello **nombre DNS** valor. Aquí tiene un ejemplo:

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. Desde un equipo local que ejecute MySQL o cliente de MySQL de hello, ejecución Hola después toolog de comando en como un usuario de MySQL.

     mysql -u <yourMysqlUsername> -p -h <yourDNSname>

   Por ejemplo, utilizando Hola nombre de usuario de MySQL _dbadmin3_ hello y _testmysql.cloudapp.net_ de nombres DNS para la máquina virtual de hello, podría empezar MySQL mediante Hola siguiente comando:

     mysql -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>Pasos siguientes
toolearn más sobre la ejecución de MySQL, vea hello [documentación de MySQL](http://dev.mysql.com/doc/).
