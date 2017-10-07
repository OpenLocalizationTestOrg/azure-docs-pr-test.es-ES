---
title: "Diseño de la primera base de datos de Azure Database for PostgreSQL con Azure Portal | Microsoft Docs"
description: "Este tutorial muestra cómo tooDesign Azure primera base de datos de PostgreSQL mediante Hola portal de Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: fde7e9d1ae2bad4291d18bebd3356f4f8a2ac86a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-hello-azure-portal"></a>Diseñar la primera base de datos de Azure para PostgreSQL mediante Hola portal de Azure

Base de datos de Azure para PostgreSQL es un servicio administrado que le permite toorun, administrar y escalar las bases de datos de PostgreSQL altamente disponibles en la nube de Hola. Con hello portal de Azure, puede administrar el servidor fácilmente y diseñar una base de datos.

En este tutorial, utilice hello toolearn portal Azure cómo para:
> [!div class="checklist"]
> * Creación de una instancia de Azure Database for PostgreSQL
> * Configurar firewall de servidor hello
> * Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilidad toocreate una base de datos
> * Carga de datos de ejemplo
> * Datos de consulta
> * Actualización de datos
> * Restauración de datos

## <a name="prerequisites"></a>Requisitos previos
Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="log-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure
Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-postgresql"></a>Creación de una instancia de Azure Database for PostgreSQL

Un servidor de Azure Database for PostgreSQL se crea con un conjunto definido de [recursos de proceso y almacenamiento](./concepts-compute-unit-and-storage.md). servidor de Hola se crea dentro de un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md).

Siga estos toocreate pasos una base de datos de Azure para PostgreSQL servidor:
1.  Haga clic en hello **+ nuevo** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.
2.  Seleccione **bases de datos** de hello **New** página y seleccione **base de datos de Azure para PostgreSQL** de hello **bases de datos** página.
 ![Base de datos de Azure para PostgreSQL - crear base de datos de Hola](./media/tutorial-design-database-using-azure-portal/1-create-database.png)

3.  Rellene Hola nuevo servidor detalles formulario con hello después de obtener información, como se muestra en hello anterior imagen:
    - Nombre del servidor: **mypgserver 20170401** (nombre de un servidor asigna nombre tooDNS y, por tanto, es necesario toobe único global) 
    - Suscripción: Si tiene varias suscripciones, elija suscripción adecuado de hello en el que recurso de hello existe o se factura para.
    - Grupo de recursos: **myresourcegroup**
    - El inicio de sesión de administrador y la contraseña que elija para el servidor
    - Ubicación
    - Versión de PostgreSQL

  > [!IMPORTANT]
  > inicio de sesión de administrador de servidor de Hola y la contraseña que especifique aquí son necesario toolog en toohello server y sus bases de datos más adelante en esta guía de inicio rápido. Recuerde o grabe esta información para su uso posterior.

4.  Haga clic en **tarifa** toospecify Hola nivel y rendimiento de nivel de servicio para la nueva base de datos. En esta guía de inicio rápido, seleccione el nivel **Básico**, **50 Unidades de proceso** y **50 GB** de almacenamiento incluido.
 ![Base de datos de Azure para PostgreSQL - nivel de servicio de Hola de selección](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)
5.  Haga clic en **Aceptar**.
6.  Haga clic en **crear** servidor de hello tooprovision. El aprovisionamiento tarda unos minutos.

  > [!TIP]
  > Comprobar hello **toodashboard Pin** opción tooallow fácil realizar un seguimiento de las implementaciones.

7.  En la barra de herramientas de hello, haga clic en **notificaciones** toomonitor proceso de implementación de Hola.
 ![Azure Database for PostgreSQL: consulta de las notificaciones](./media/tutorial-design-database-using-azure-portal/3-notifications.png)
   
  De forma predeterminada, la base de datos de **postgres** se crea en el servidor. Hola [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de datos es una base de datos predeterminada destinado a los usuarios, utilidades y aplicaciones de otros fabricantes. 

## <a name="configure-a-server-level-firewall-rule"></a>Configuración de una regla de firewall de nivel de servidor

Hola base de datos de Azure para servicio PostgreSQL crea un servidor de seguridad en el nivel de servidor hello. Este firewall impide que las aplicaciones externas y las herramientas se conecten toohello server y las bases de datos en el servidor de Hola a menos que se crea una regla de firewall tooopen firewall de Hola para direcciones IP concretas. 

1.  Una vez finalizada la implementación de hello, haga clic en **todos los recursos** del menú izquierdo de Hola y escriba el nombre de hello **mypgserver 20170401** toosearch para el servidor recién creado. Haga clic en nombre del servidor de hello, en el resultado de la búsqueda de Hola. Hola **Introducción** página para el servidor se abre y proporciona opciones para otra configuración.
 
 ![Azure Database for PostgreSQL: búsqueda de un servidor ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  En la hoja de servidor hello, seleccione **seguridad de conexión**. 
3.  Haga clic en el cuadro de texto hello **nombre de la regla,** y agregue un nuevo firewall regla toowhitelist Hola intervalo IP para la conectividad. Para este tutorial, vamos a permitir todas las direcciones IP; para ello, escriba **Nombre de la regla = AllowAllIps**, **IP inicial = 0.0.0.0** e **IP final = 255.255.255.255** y haga clic en **Guardar**. Puede establecer una regla de firewall que abarca un intervalo IP toobe tooconnect capaz de la red.
 
 ![Azure Database for PostgreSQL: creación de una regla de firewall](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  Haga clic en **guardar** y, a continuación, haga clic en hello **X** tooclose hello **conexiones seguridad** página.

  > [!NOTE]
  > El servidor Azure PostgreSQL se comunica a través de puerto 5432. Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 5432. Si es así, no será capaz de tooconnect tooyour base de datos de SQL Azure servidor a menos que el departamento de TI abre el puerto 5432.
  >


## <a name="get-hello-connection-information"></a>Obtener información de conexión de Hola

Cuando creamos nuestra base de datos de Azure para servidor PostgreSQL, Hola predeterminado **postgres** base de datos también se crea. servidor de base de datos de tooconnect tooyour, necesita credenciales de acceso y la información de host de tooprovide.

1. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola que acaba de crear **mypgserver 20170401**.

  ![Azure Database for PostgreSQL: búsqueda de un servidor ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. Haga clic en el nombre del servidor de hello **mypgserver 20170401**.
4. Servidor de hello seleccione **Introducción** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.

 ![Azure Database for PostgreSQL: inicio de sesión del administrador del servidor](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a>Conectar la base de datos de tooPostgreSQL con psql en el Shell de nube

Vamos a usar ahora hello psql utilidad de línea de comandos tooconnect toohello base de datos de Azure para servidor de PostgreSQL. 
1. Inicie Hola Shell en la nube de Azure a través del icono de terminal de hello en el panel de navegación superior de Hola.

   ![Azure Database for PostgreSQL: icono del terminal de Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. Hola Shell en la nube de Azure se abre en el explorador, lo que le tootype intensiva de comandos.

   ![Azure Database for PostgreSQL: indicador de Bash de Azure Shell](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. En el símbolo del sistema de hello Shell en la nube, conectar tooyour base de datos de Azure para el servidor de PostgreSQL usando comandos de psql Hola. Hola siguiente formato es tooconnect usado tooan base de datos de Azure para servidor de PostgreSQL con hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilidad:
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   Por ejemplo, hello siguiente comando conecta a base de datos de toohello predeterminada denominada **postgres** en el servidor de PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizando las credenciales de acceso. Escriba la contraseña de administrador del servidor cuando se le solicite.

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a>Creación de una base de datos
Una vez que esté conectado toohello server, cree una base de datos en blanco en el símbolo del sistema de Hola.
```bash
CREATE DATABASE mypgsqldb;
```

En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch conexión toohello recién creado **mypgsqldb**.
```bash
\c mypgsqldb
```
## <a name="create-tables-in-hello-database"></a>Crear tablas de base de datos de Hola
Ahora que sabe cómo tooconnect toohello base de datos de Azure para PostgreSQL, podemos ver cómo toocomplete algunas tareas básicas.

En primer lugar, podemos crear una tabla y cargarla con algunos datos. Vamos a crear una tabla que hace el seguimiento de información del inventario.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Puede ver Hola recién creado tabla en la lista de Hola de tabvles ahora escribiendo:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Cargar datos en tablas de Hola
Ahora que tenemos una tabla, podemos insertar algunos datos en ella. En la ventana de símbolo del sistema abierto hello, ejecute hello después consulta tooinsert algunas filas de datos
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Tiene ahora dos filas de datos de ejemplo en la tabla de Hola que creó anteriormente.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Consultar y actualizar los datos de hello en tablas de Hola
Ejecute hello siguientes tooretrieve información de consulta de tabla de base de datos de Hola. 
```sql
SELECT * FROM inventory;
```

También puede actualizar los datos de hello en tablas de Hola
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

fila de Hola se actualiza en consecuencia cuando se recuperan datos.
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-tooa-previous-point-in-time"></a>Restaurar el punto de datos tooa anterior en el tiempo
Imagine que eliminó accidentalmente esta tabla. No se puede recuperar con facilidad de esta situación. Base de datos de Azure para PostgreSQL permite toogo tooany atrás en un momento (en Hola última too7 días (Basic) y 35 días (estándar)) y restaurar este punto-in-time tooa nuevo servidor. Puede usar esta nueva toorecover server los datos eliminados. Hola siguiendo los pasos restauración Hola ejemplo servidor tooa punto antes de que se ha agregado Hola tabla.

1.  En hello base de datos de Azure para la página de PostgreSQL para el servidor, haga clic en **restaurar** en la barra de herramientas de Hola. Hola **restaurar** se abre la página.
  ![Azure Portal: opciones del formulario de restauración](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)
2.  Rellene hello **restaurar** formulario con la información de hello necesario:

  ![Azure Portal: opciones del formulario de restauración](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - **Punto de restauración**: seleccione un punto-in-time que se produce antes de que se cambió el servidor hello
  - **Servidor de destino**: especifique un nuevo nombre de servidor que desee toorestore a
  - **Ubicación**: no se puede seleccionar una región hello, de forma predeterminada es igual que el servidor de origen de Hola
  - **Plan de tarifa**: no se puede cambiar este valor al restaurar un servidor. Es igual que el servidor de origen de Hola. 
3.  Haga clic en **Aceptar** toorestore Hola servidor demasiado[tooa en el momento de restaurar](./howto-restore-server-portal.md) antes de que se eliminen tablas Hola. Restauración tooa otro punto de servidor en el tiempo crea un duplicado en el servidor nuevo como servidor original Hola de punto de hello en el tiempo especificado, siempre que esté dentro del período de retención de Hola para su [nivel de servicio](./concepts-service-tiers.md).

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo toouse Hola portal de Azure y otras utilidades para:
> [!div class="checklist"]
> * Creación de una instancia de Azure Database for PostgreSQL
> * Configurar firewall de servidor hello
> * Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilidad toocreate una base de datos
> * Carga de datos de ejemplo
> * Datos de consulta
> * Actualización de datos
> * Restauración de datos

A continuación, obtenga información acerca de cómo toouse otras tareas similares toodo CLI de Azure, revise este tutorial: [diseñar la primera base de datos de Azure para PostgreSQL con CLI de Azure](tutorial-design-database-using-azure-cli.md)
