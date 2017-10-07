---
title: aaaDesign Azure primero la base de datos para la base de datos de MySQL - Portal de Azure | Documentos de Microsoft
description: "Este tutorial le explica cómo toocreate y administrar la base de datos de MySQL server y base de datos mediante el Portal de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Diseño de la primera base de datos de Azure Database for MySQL
Base de datos de Azure para MySQL es un servicio administrado que le permite toorun, administrar y escalar alta disponibilidad bases de datos MySQL en la nube de Hola. Con hello portal de Azure, puede administrar el servidor fácilmente y diseñar una base de datos.

En este tutorial, utilice hello toolearn portal Azure cómo para:

> [!div class="checklist"]
> * Creación de una instancia de Azure Database for MySQL
> * Configurar firewall de servidor hello
> * Use la herramienta de línea de comandos de mysql toocreate una base de datos
> * Carga de datos de ejemplo
> * Datos de consulta
> * Actualización de datos
> * Restauración de datos

## <a name="sign-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure
Abra el explorador web favoritas y visite hello [portal de Microsoft Azure](https://portal.azure.com/). Escriba su credenciales toosign en toohello portal. vista predeterminada de Hello es el panel de servicio.

## <a name="create-an-azure-database-for-mysql-server"></a>Creación de un servidor de Azure Database for MySQL
Se crea un servidor de Azure Database for MySQL con un conjunto definido de [recursos de proceso y almacenamiento](./concepts-compute-unit-and-storage.md). servidor de Hola se crea dentro de un [grupo de recursos de Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

1. Navegue demasiado**bases de datos** > **base de datos de Azure para MySQL**. Si no se puede encontrar el servidor de MySQL en **bases de datos** categoría, haga clic en **ver todas** tooshow disponible todos los servicios de base de datos. También puede escribir **base de datos de Azure para MySQL** en tooquickly de cuadro de búsqueda de hello busque servicio Hola.
![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. Haga clic en el icono **Azure Database for MySQL** y, después, en **Crear**.

En nuestro ejemplo, rellene Hola base de datos de Azure para el formulario de MySQL con hello siguiente información:

| **Configuración** | **Valor sugerido** | **Descripción del campo** |
|---|---|---|
| *Nombre del servidor* | myserver4demo  | Nombre del servidor tiene toobe único global. |
| *Suscripción* | mysubscription | Seleccione la suscripción en Hola de lista desplegable. |
| *Grupos de recursos* | myresourcegroup | Cree un grupo de recursos o use uno existente. |
| *Inicio de sesión del administrador del servidor* | myadmin | Nombre de la cuenta de administrador de configuración. |
| *Password* |  | Configure una contraseña de la cuenta de administrador segura. |
| *Confirmar contraseña* |  | Confirme la contraseña de cuenta de administrador de Hola. |
| *Ubicación* |  | Seleccione una región disponible. |
| *Versión* | 5.7 | Elija la versión más reciente de Hola. |
| *Configurar rendimiento* | Básico, 50 unidades de proceso, 50 GB  | Seleccione **Plan de tarifa**, **Unidades de proceso**, **Almacenamiento (GB)** y, finalmente, haga clic en **Aceptar**. |
| *TooDashboard de PIN* | Comprobar | Recomienda toocheck esta casilla para que puede encontrar fácilmente más adelante en servidor hello |
A continuación, haga clic en **Crear**. En un minuto o dos, una nueva base de datos de Azure para servidor MySQL se está ejecutando en la nube de Hola. Puede hacer clic en **notificaciones** botón en el proceso de implementación de hello barra de herramientas toomonitor Hola.

## <a name="configure-firewall"></a>Configuración del firewall
Las bases de datos de Azure para MySQL están protegidas con un firewall. De forma predeterminada, se rechazan todas las conexiones toohello hello y servidor de bases de datos dentro de servidor hello. Antes de conectarse tooAzure base de datos MySQL para hello primera vez, configure la dirección IP de red pública de la máquina de hello firewall tooadd Hola cliente (o intervalo de direcciones IP).

1. Haga clic en el servidor recién creado y, luego, en **Seguridad de la conexión**.
   ![3-1 Seguridad de conexión](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. Puede **agregar su dirección IP** o configurar aquí las reglas de firewall. Recuerde tooclick **guardar** después de haber creado reglas Hola.
Ahora puede conectarse server toohello mediante la herramienta de línea de comandos de mysql o herramienta de interfaz gráfica de usuario de MySQL Workbench.

> [!TIP]
> El servidor de Azure Database for MySQL se comunica a través del puerto 3306. Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 3306. Si es así, no se puede conectar tooAzure MySQL server a menos que el departamento de TI abre el puerto 3306.

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Hola Get completo **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor** para la base de datos de Azure para servidor de MySQL de hello portal de Azure. Usa Hola completo nombre tooconnect tooyour server mediante la herramienta de línea de comandos de mysql. 

1. En [portal de Azure](https://portal.azure.com/), haga clic en **todos los recursos** desde el menú izquierdo hello, nombre de tipo hello y busque la base de datos de Azure para servidor MySQL. Seleccione detalles hello tooview nombre del servidor de Hola.

2. En configuración de hello encabezado, haga clic en **propiedades**. Anote los valores de **NOMBRE DEL SERVIDOR** y **NOMBRE DE INICIO DE SESIÓN DEL ADMINISTRADOR DEL SERVIDOR**. Puede hacer clic en hello Copiar botón siguiente tooeach campo toocopy toohello Portapapeles.
   ![4-2 Propiedades del servidor](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

En este ejemplo, es el nombre del servidor de hello *myserver4demo.mysql.database.azure.com*, y es el inicio de sesión de administrador de servidor de hello  *myadmin@myserver4demo* .

## <a name="connect-toohello-server-using-mysql"></a>Conectar con mysql de servidor de toohello
Use [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish una tooyour de conexión base de datos de MySQL server. Puede ejecutar herramienta de línea de comandos de mysql Hola de hello Shell en la nube de Azure en el Explorador de Hola o de su propia máquina mediante herramientas de mysql instaladas de forma local. Hola toolaunch Shell en la nube de Azure, haga clic en hello `Try It` situado en un bloque de código en este artículo, o visite Hola portal de Azure y haga clic en hello `>_` icono en la barra de herramientas derecha Hola superior. 

Escriba Hola comando tooconnect:
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>Crear una base de datos en blanco
Una vez que esté conectado toohello server, cree un toowork de base de datos en blanco con.
```sql
CREATE DATABASE mysampledb;
```

En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch conexión toothis recién creado:
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Crear tablas de base de datos de Hola
Ahora que sabe cómo tooconnect toohello base de datos de Azure para la base de datos MySQL, podemos ver cómo toocomplete algunas tareas básicas.

En primer lugar, podemos crear una tabla y cargarla con algunos datos. Vamos a crear una tabla que almacena la información del inventario.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Cargar datos en tablas de Hola
Ahora que tenemos una tabla, podemos insertar algunos datos en ella. En la ventana de símbolo del sistema abierto hello, ejecute hello después consulta tooinsert algunas filas de datos.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Ahora tiene dos filas de datos de ejemplo en la tabla de Hola que creó anteriormente.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Consultar y actualizar los datos de hello en tablas de Hola
Ejecute hello siguientes tooretrieve información de consulta de tabla de base de datos de Hola.
```sql
SELECT * FROM inventory;
```

También puede actualizar los datos de hello en tablas de Hola.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

fila de Hola se actualiza en consecuencia cuando se recuperan datos.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurar un punto anterior de tooa de base de datos en el tiempo
Imagine que ha eliminado accidentalmente una tabla de base de datos importantes y no puede recuperar datos de hello fácilmente. Base de datos de Azure para MySQL permite toorestore Hola server tooa punto en el tiempo, crear una copia de las bases de datos de hello en el nuevo servidor. Puede usar esta nueva toorecover server los datos eliminados. Hola siguiendo los pasos restauración Hola ejemplo servidor tooa punto antes de que se ha agregado Hola tabla.

1. Hola portal de Azure, busque la base de datos MySQL. En hello **Introducción** página, haga clic en **restaurar** en la barra de herramientas de Hola. se abre la página de la restauración de Hola.

   ![10-1 Restaurar una base de datos](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Rellene hello **restaurar** formulario con la información de hello necesario.
   
   ![10-2 Formulario de restauración](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **Punto de restauración**: seleccione un punto-in-time que desea toorestore, plazo Hola enumerados. Asegúrese de tooconvert seguro su tooUTC de zona horaria local.
   - **Restaurar el servidor de toonew**: especifique un nuevo nombre de servidor que desee toorestore a.
   - **Ubicación**: Hola región es el mismo que el servidor de origen de hello y no se puede cambiar.
   - **Nivel de precios**: Hola tarifa es hello igual Hola servidor de origen y no se puede cambiar.
   
3. Haga clic en **Aceptar** toorestore Hola servidor demasiado[tooa punto de restauración tiempo](./howto-restore-server-portal.md) antes de que se eliminó la tabla de Hola. Restaurar un servidor, crea una nueva copia del servidor, hello, desde el punto de hello en el tiempo que especifique. 

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, utilice hello toolearned portal Azure cómo para:

> [!div class="checklist"]
> * Creación de una instancia de Azure Database for MySQL
> * Configurar firewall de servidor hello
> * Use la herramienta de línea de comandos de mysql toocreate una base de datos
> * Carga de datos de ejemplo
> * Datos de consulta
> * Actualización de datos
> * Restauración de datos

> [!div class="nextstepaction"]
> [Cómo tooconnect tooAzure de las aplicaciones de base de datos de MySQL](./howto-connection-string.md)
