---
title: "Inicio rápido: Creación de un servidor de Azure Database for MySQL con Azure Portal | Microsoft Docs"
description: "En este artículo pasos le guían a través de utilizando Hola tooquickly portal Azure crean un ejemplo de la base de datos de MySQL server en aproximadamente cinco minutos."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>Creación de un servidor de Azure Database for MySQL con Azure Portal
Base de datos de Azure para MySQL es un servicio administrado que le permite toorun, administrar y escalar alta disponibilidad bases de datos MySQL en la nube de Hola. Este tutorial rápido muestra cómo toocreate una Azure base de datos para el servidor de MySQL usando Hola portal de Azure en aproximadamente cinco minutos. 

Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure
Abra el explorador web y navegue toohello [portal de Microsoft Azure](https://portal.azure.com/). Escriba su credenciales toosign en toohello portal. vista predeterminada de Hello es el panel de servicio.

## <a name="create-azure-database-for-mysql-server"></a>Creación de un servidor de Azure Database for MySQL
Se crea un servidor de Azure Database for MySQL con un conjunto definido de [recursos de proceso y almacenamiento](./concepts-compute-unit-and-storage.md). servidor de Hola se crea dentro de un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md).

Siga estos toocreate pasos una base de datos de MySQL server:

1. Haga clic en hello **New** botón (+) que se encuentra en la esquina izquierda superior de Hola de hello portal de Azure.

2. Seleccione **bases de datos** de hello **New** página y seleccione **base de datos de Azure para MySQL** de hello **bases de datos** página. También puede escribir **MySQL** Hola servicio de Hola de toofind cuadro de búsqueda de página nueva.
![Azure Portal: nueva - base de datos - MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. Rellene Hola nuevo servidor detalles formulario con hello después de obtener información, como se muestra en hello anterior imagen:

    **Configuración** | **Valor sugerido** | **Descripción del campo** 
    ---|---|---
    Nombre de servidor | myserver4demo | Elija un nombre único que identifique al servidor de Azure Database for MySQL. nombre de dominio de Hello *mysql.database.azure.com* es toohello anexado nombre del servidor proporciona para las aplicaciones tooconnect a. nombre del servidor Hello puede contener solo letras minúsculas, números y caracteres de guión (-) de Hola y debe contener entre 3 y 63 caracteres.
    La suscripción | Su suscripción | Hola suscripción de Azure que quiere toouse de su servidor. Si tiene varias suscripciones, elija suscripción adecuado de hello en la que se facturan recursos Hola para.
    Grupos de recursos | myresourcegroup | Puede crear un nuevo nombre de grupo de recursos o usar uno existente de la suscripción.
    Inicio de sesión de administrador de servidor | myadmin | Realizar su propia toouse de cuenta de inicio de sesión al conectar el servidor de toohello. nombre de inicio de sesión de administrador de Hello no puede ser 'azure_superuser', 'admin', 'administrator', 'raíz', 'guest' o 'public'.
    Password | *Su elección* | Crear una nueva contraseña para la cuenta de administrador del servidor de Hola. Debe contener entre 8 caracteres too128. La contraseña debe contener caracteres de tres de hello siguientes categorías – letras en mayúsculas letras, letras minúsculas, números (0-9) y caracteres no alfanuméricos (!, $, #, %, etcetera.).
    Confirmar contraseña | *Su elección*| Confirme la contraseña de cuenta de administrador de Hola.
    Ubicación | *usuarios de Hello región más cercanos tooyour*| Elegir ubicación de Hola que sea más cercano tooyour los usuarios u otras aplicaciones de Azure.
    Versión | *Elija la versión más reciente de Hola*| Elija la versión más reciente de Hola a menos que tenga requisitos específicos.
    Nivel de precios | **Básico**, **50 unidades de proceso****50 GB** | Haga clic en **tarifa** toospecify Hola nivel y rendimiento de nivel de servicio para la nueva base de datos. Elija **nivel básico** en la pestaña de hello en la parte superior de Hola. Haga clic en el extremo izquierdo de Hola de hello **unidades de proceso** control deslizante tooadjust Hola valor toohello menos cantidad disponible para este tutorial rápido. Haga clic en **Aceptar** hello toosave selección de nivel de precios. Vea Hola siguiente captura de pantalla.
    Toodashboard de PIN | Comprobar | Comprobar hello **toodashboard Pin** opción tooallow fácil seguimiento del servidor en la página de panel frontal de Hola de su portal de Azure.

    > [!IMPORTANT]
    > inicio de sesión de administrador de servidor de Hola y la contraseña que especifique aquí son necesario toolog en toohello server y sus bases de datos más adelante en este tutorial rápido. Recuerde o grabe esta información para su uso posterior.
    > 

    ![Portal de Azure - crear MySQL proporcionando entrada de formulario de hello necesario](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  Haga clic en **crear** servidor de hello tooprovision. Aprovisionamiento tarda unos minutos, los minutos de too20 máximo.
   
5.  En la barra de herramientas de hello, haga clic en **notificaciones** proceso de implementación de (icono de campana) toomonitor Hola.

## <a name="configure-a-server-level-firewall-rule"></a>Configuración de una regla de firewall de nivel de servidor

Hola base de datos de Azure para el servicio MySQL crea un servidor de seguridad en el nivel de servidor hello. Este firewall impide que las aplicaciones externas y las herramientas conexión toohello server y las bases de datos en el servidor de hello, a menos que se crea una regla de firewall tooopen firewall de Hola para direcciones IP concretas. 

1.  Busque el servidor al finalizar la implementación de Hola. Si es necesario, puede buscarlo. Por ejemplo, haga clic en **todos los recursos** del menú izquierdo de Hola y el tipo en el nombre del servidor de hello (como ejemplo de Hola *myserver4demo*) toosearch para el servidor recién creado. Haga clic en el nombre del servidor aparece en el resultado de la búsqueda de Hola. Hola **Introducción** página para el servidor se abre y proporciona opciones para otra configuración.

2. En la página del servidor hello, seleccione **seguridad de conexión**.

3.  En hello **las reglas de Firewall** encabezado, haga clic en cuadro de texto en blanco de Hola Hola **nombre de la regla** toobegin columna Crear regla de firewall de Hola. 

    Para este tutorial rápido, vamos a permitir todas las direcciones IP en el servidor de hello rellenando en el cuadro de texto hello en cada columna con hello siguientes valores:

    Nombre de la regla | Dirección IP inicial | Dirección IP final 
    ---|---|---
    AllowAllIps (permitir todas las direcciones IP) |  0.0.0.0 | 255.255.255.255

4. En la barra de herramientas superior Hola de hello **seguridad de conexión** página, haga clic en **guardar**. Espere unos instantes y Hola de notificación que muestra que la actualización de seguridad de la conexión ha finalizado correctamente antes de continuar.

    > [!NOTE]
    > Las conexiones tooAzure base de datos de MySQL que se comunican a través de puerto 3306. Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 3306. Si es así, no será capaz de tooconnect tooyour servidor a menos que el departamento de TI abre el puerto 3306.
    > 

## <a name="get-hello-connection-information"></a>Obtener información de conexión de Hola
servidor de base de datos de tooconnect tooyour, necesita tooremember Hola credenciales de servidor completo administrador y el nombre de inicio de sesión. Puede haber tomado nota de esos valores anteriormente en el artículo de inicio rápido de Hola. En caso de que no lo hizo, se puede encontrar fácilmente servidor hello información de nombre y el inicio de sesión del servidor de hello **Introducción** página o hello **propiedades** página Hola portal de Azure.

1. Abra la página **Información general** del servidor. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**. 
    Situar el cursor sobre cada campo e icono de copiar Hola aparece toohello derecha texto hello. Haga clic en icono de copiar hello como valores de hello toocopy necesarios.

    En este ejemplo, es el nombre del servidor de hello *myserver4demo.mysql.database.azure.com*, y es el inicio de sesión de administrador de servidor de hello  *myadmin@myserver4demo* .

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>Conectar tooMySQL mediante la herramienta de línea de comandos de mysql
Hay una serie de aplicaciones puede usar tooconnect tooyour base de datos de MySQL server. Vamos a usar en primer lugar hello [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) de línea de comandos herramienta tooillustrate cómo tooconnect toohello server.  Puede usar un explorador web y Shell de nube de Azure como se describe aquí sin Hola Hola necesita tooinstall ningún software adicional. Si dispone de utilidad de mysql Hola instalado localmente en su propio equipo, puede conectarse desde allí también.

1. Iniciar Hola Shell en la nube de Azure a través del icono de terminal de hello (> _) en hello parte superior derecha de la página web del portal Azure Hola.

2. Hola Shell en la nube de Azure se abre en el explorador, lo que los comandos de shell de bash tootype.

    ![Símbolo del sistema: ejemplo de línea de comandos de mysql](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. En el símbolo del sistema de hello Shell en la nube, conectar tooyour base de datos de MySQL server escribiendo línea de comandos de mysql de hello en el símbolo del sistema de hello verde.

    Hola siguiendo el formato es tooconnect usado tooan base de datos de MySQL server con la utilidad de hello mysql:
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    Por ejemplo, hello siguiente comando conecta tooour servidor de ejemplo:
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    parámetro mysql |Valor sugerido|Descripción
    ---|---|---
    --host | *nombre del servidor* | Especifique el valor de nombre de servidor de Hola que se usó cuando creó Hola base de datos de Azure para MySQL anteriormente. El servidor de ejemplo que se muestra es myserver4demo.mysql.database.azure.com. Usar el nombre de dominio completo de hello (\*. mysql.database.azure.com) tal y como se muestra en el ejemplo de Hola. Siga los pasos Hola Hola anterior sección tooget Hola información de la conexión si no recuerda el nombre del servidor. 
    --user | *nombre de inicio de sesión del administrador del servidor* |Escriba Hola server inicio de sesión nombre de usuario administrador especificó al crear Hola base de datos de Azure para MySQL anteriormente. Siga los pasos Hola Hola anterior sección tooget Hola información de la conexión si no recuerda el nombre de usuario de Hola.  formato de Hello es  *username@servername* .
    --password | *espere hasta que se le pida* | Se le pedirá demasiado "Escriba una contraseña" después de escribe comandos Hola. Cuando se le solicite, escriba Hola misma contraseña que proporcionó cuando creó el servidor de Hola.  Hola Nota escrito contraseña caracteres no se muestran en bash Hola preguntar al escribirlos. Presione ENTRAR después de haber escrito todos los tooauthenticate de caracteres de Hola y conectarse.

   Una vez conectado, utilidad de mysql de hello muestra un `mysql>` pedir que tootype comandos. 

    Ejemplo de salida de mysql:
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Si firewall de hello no está configurado tooallow dirección IP de Hola de hello Shell en la nube de Azure, hello ocurre lo siguiente:
    >
    > ERROR 2003 (28000): Cliente con la dirección IP 123.456.789.0 no tiene a servidor de hello tooaccess.
    >
    > error de hello tooresolve, asegúrese de seguro Hola server configuration coincidencias Hola los pasos de hello *configurar una regla de firewall de nivel de servidor* sección del artículo Hola.

4. Conexión de Hola de tooensure de estado de servidor de vista es funcional. Tipo `status` en mysql hello > pedir una vez que está conectado.
    ```sql
    status
    ```

   > [!TIP]
   > Para otros comandos, consulte el [capítulo 4.5.1 del Manual de referencia de MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

5.  Crear una base de datos en blanco en mysql hello > símbolo del sistema, escriba el siguiente comando de hello:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    comando Hello puede tardar unos toocomplete momentos. 

    En un servidor de Azure Database for MySQL, puede crear una o varias bases de datos. Puede participar una base de datos por servidor tooutilize toocreate todos los recursos de Hola o crear tooshare de bases de datos de varios recursos de Hola. No hay ningún toohello limitar el número de bases de datos que se pueden crear, pero varias bases de datos comparten Hola mismos recursos de servidor. 

6. Lista de bases de datos Hola Hola mysql > símbolo del sistema, escriba el siguiente comando de hello:

    ```sql
    SHOW DATABASES;
    ```

7.  Tipo de `\q` y, a continuación, presione herramienta de mysql de entrar tooquit Hola. Puede cerrar Hola Shell en la nube de Azure cuando haya terminado.

Ahora está conectado toohello base de datos de Azure para MySQL y crea una base de datos de usuario en blanco. Continuar toohello siguiente sección toorepeat un toohello de tooconnect ejercicio similar mismo servidor mediante la herramienta común MySQL Workbench.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Conectar servidor toohello mediante la herramienta de interfaz gráfica de usuario de MySQL Workbench Hola
servidor de MySQL de tooconnect tooAzure mediante Hola GUI MySQL Workbench:

1.  Inicie Hola aplicación MySQL Workbench en el equipo cliente. Puede descargar e instalar MySQL Workbench desde [aquí](https://dev.mysql.com/downloads/workbench/).

2.  En **el programa de instalación nueva conexión** diálogo cuadro, escriba Hola siguiente información **parámetros** ficha:

    ![Configuración de una conexión nueva](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **Configuración** | **Valor sugerido** | **Descripción del campo** |
    |---|---|---|
    |   Nombre de la conexión | Conexión de demostración | Especifique una etiqueta para esta conexión. |
    | Método de conexión | Estándar (TCP/IP) | Estándar (TCP/IP) es suficiente. |
    | Nombre de host. | *nombre del servidor* | Especifique el valor de nombre de servidor de Hola que se usó cuando creó Hola base de datos de Azure para MySQL anteriormente. El servidor de ejemplo que se muestra es myserver4demo.mysql.database.azure.com. Usar el nombre de dominio completo de hello (\*. mysql.database.azure.com) tal y como se muestra en el ejemplo de Hola. Siga los pasos Hola Hola anterior sección tooget Hola información de la conexión si no recuerda el nombre del servidor.  |
    | Port | 3306 | Utilice siempre el puerto 3306 al conectarse tooAzure base de datos de MySQL. |
    | Nombre de usuario |  *nombre de inicio de sesión del administrador del servidor* | Escriba Hola server inicio de sesión nombre de usuario administrador especificó al crear Hola base de datos de Azure para MySQL anteriormente. El nombre de usuario de nuestro ejemplo es myadmin@myserver4demo. Siga los pasos Hola Hola anterior sección tooget Hola información de la conexión si no recuerda el nombre de usuario de Hola. formato de Hello es  *username@servername* .
    | Password | la contraseña | Haga clic en almacenar en el almacén de contraseñas de botón toosave Hola.... |

    Haga clic en **Probar conexión** tootest si todos los parámetros están configurados correctamente. Haga clic en Aceptar toosave Hola conexión. 

    > [!NOTE]
    > SSL se aplica de forma predeterminada en el servidor y requiere configuración adicional en orden tooconnect correctamente. Vea [tooAzure base de datos de conexión de conectividad de configurar SSL en su aplicación toosecurely para MySQL](./howto-configure-ssl.md).  Si desea toodisable SSL para este tutorial rápido, visite Hola portal de Azure y haga clic en hello conexión seguridad página toodisable Hola exigir SSL conexión botón de alternancia.

## <a name="clean-up-resources"></a>Limpieza de recursos
Limpiar los recursos de Hola que creó en el tutorial rápido de hello ya sea eliminando Hola [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md), que incluye todos los recursos de hello en el grupo de recursos de hello, o mediante la eliminación de recursos de un servidor hello si quiere tookeep Hola otros recursos intactos.

> [!TIP]
> Otras guías de inicio rápido de esta colección se basan en los valores de esta. Si tiene previsto toocontinue toowork con los siguientes tutoriales rápidos, realice la limpieza no Hola recursos creados en este tutorial rápido. Si no tiene previsto toocontinue, use Hola seguido toodelete pasos creado todos los recursos de este tutorial rápido de hello portal de Azure.
>

toodelete Hola todo grupo de recursos incluidos servidor hello recién creado:
1.  Busque el grupo de recursos en hello portal de Azure. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de Hola de su grupo de recursos, como en nuestro ejemplo **myresourcegroup**.
2.  En la página del grupo de recursos, haga clic en **Eliminar**. A continuación, Hola nombre del tipo de su grupo de recursos, como en nuestro ejemplo **myresourcegroup**en Hola eliminación de tooconfirm del cuadro de texto y, a continuación, haga clic en **eliminar**.

O bien, en su lugar, toodelete Hola recién creado servidor:
1.  Busque el servidor en hello portal de Azure, si no tiene abrir. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos**y, a continuación, busque servidor hello que ha creado.
2.  En hello **Introducción** página, haga clic en hello **eliminar** botón en el panel superior de Hola.
![Azure Database for MySQL: eliminación del servidor](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  Confirme el nombre del servidor hello desee toodelete y mostrar hello las bases de datos en lo que se ven afectados. Escriba el nombre del servidor en el cuadro de texto hello, como en nuestro ejemplo **myserver4demo**y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Diseño de la primera base de datos de Azure Database for MySQL](./tutorial-design-database-using-portal.md)

