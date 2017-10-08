---
title: "aaaBuild una aplicación web de Java y MySQL en Azure"
description: "Obtenga información acerca de cómo tooget una aplicación Java que conecta servicio de base de datos de MySQL de Azure toohello trabaja en el servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Compilación de una aplicación web Java y MySQL en Azure

Este tutorial muestra cómo toocreate un Java web de aplicación en Azure y conectar tooa base de datos de MySQL. Cuando haya terminado, tendrá una aplicación [Spring Boot](https://projects.spring.io/spring-boot/) que almacena datos en [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) y que se ejecuta en [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

![Aplicación Java que se ejecuta en Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una base de datos MySQL en Azure
> * Conectarse a una base de datos de toohello de aplicación de ejemplo
> * Implementar Hola aplicación tooAzure
> * Actualizar y volver a implementar la aplicación hello
> * Transmitir registros de diagnóstico desde Azure
> * Supervisar la aplicación hello en hello portal de Azure


## <a name="prerequisites"></a>Requisitos previos

1. [Descarga e instalación de Git](https://git-scm.com/)
1. [Descargue e instale Hola Java JDK de 7 o superior](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [Descarga, instalación e inicio de MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-local-mysql"></a>Preparación de MySQL local 

En este paso, creará una base de datos en un servidor de MySQL local para su uso en pruebas aplicación hello localmente en su equipo.

### <a name="connect-toomysql-server"></a>Conecte el servidor de tooMySQL

En una ventana de terminal, conéctese tooyour local MySQL server. Puede utilizar esta ventana de terminal toorun todos los comandos de hello en este tutorial.

```bash
mysql -u root -p
```

Si se le pide una contraseña, escriba contraseña Hola de hello `root` cuenta. Si no recuerda su contraseña de la cuenta raíz, consulte [MySQL: cómo tooReset Hola contraseña raíz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Si el comando se ejecuta correctamente, significa que el servidor MySQL ya se está ejecutando. Si no es así, asegúrese de que el servidor MySQL local debe iniciarse mediante Hola siguiente [pasos posteriores a la instalación de MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database"></a>Crear una base de datos 

Hola `mysql` símbolo del sistema, cree una base de datos y una tabla para hello elementos pendientes.

```sql
CREATE DATABASE tododb;
```

Escriba `quit` para salir de la conexión del servidor.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>Crear y ejecutar la aplicación de ejemplo de Hola 

En este paso, clonar aplicación de arranque de primavera de ejemplo, configurar base de datos de MySQL local de toouse hello y ejecútelo en el equipo. 

### <a name="clone-hello-sample"></a>Ejemplo de Hola de clon

En la ventana de terminal de hello, navegue tooa trabajar repositorio de ejemplo de Hola de directorio y clone. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Configurar base de datos de hello aplicación toouse Hola MySQL

Hola de actualización `spring.datasource.password` y el valor de *spring-boot-mysql-todo/src/main/resources/application.properties* con hello misma contraseña raíz utiliza el símbolo del sistema de tooopen Hola MySQL:

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>Compilar y ejecutar el ejemplo hello

Compilar y ejecutar el ejemplo hello utilizando hello Maven contenedor incluido en el repositorio de hello:

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

Abra su toosee toohttp://localhost:8080 de explorador en el ejemplo de Hola en acción. Si agrega la lista de tareas de toohello, usar hello SQL siguiente comandos de hello MySQL datos de hello tooview pedir datos almacenados en MySQL.

```SQL
use testdb;
select * from todo_item;
```

Detener la aplicación hello pulsando `Ctrl` + `C` Hola terminal. 

## <a name="create-an-azure-mysql-database"></a>Creación de una base de datos MySQL de Azure

En este paso, creará un [base de datos de Azure para MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instancia mediante hello [CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli). Configurar toouse de aplicación de ejemplo de Hola esta base de datos más adelante en el tutorial de Hola.

Hola utilice Azure CLI 2.0 en un recurso de ventana de terminal toocreate Hola necesita toohost la aplicación de Java en el servicio de aplicaciones de Azure. Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y administran recursos relacionados como aplicaciones web, bases de datos y cuentas de almacenamiento. 

Hello en el ejemplo siguiente se crea un grupo de recursos en la región de Europa del Norte hello:

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

Puede usar para valores toosee Hola posibles `--location`, usar hello [az de servicio de aplicaciones enumerar ubicaciones](/cli/azure/appservice#list-locations) comando.

### <a name="create-a-mysql-server"></a>Creación de un servidor MySQL

Crear un servidor de base de datos de Azure para MySQL (versión preliminar) con hello [crear servidor de mysql az](/cli/azure/mysql/server#create) comando.    
Sustituya su propio nombre de servidor único de MySQL donde verá hello `<mysql_server_name>` marcador de posición. Este nombre forma parte del nombre de host del servidor MySQL, `<mysql_server_name>.mysql.database.azure.com`, por lo que necesita toobe único global. Reemplace también `<admin_user>` y `<admin_password>` por sus propios valores.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

Cuando se crea el servidor de MySQL de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a>Configuración del firewall del servidor

Cree una regla de firewall para el cliente de MySQL server tooallow conexiones con hello [crear az mysql server regla de firewall](/cli/azure/mysql/server/firewall-rule#create) comando. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure Database for MySQL (versión preliminar) no permite en este momento habilitar conexiones automáticamente desde servicios de Azure. Tal y como se asignan dinámicamente direcciones IP en Azure, es mejor tooenable todas las direcciones IP ahora. Como servicio de hello continúa su vista previa, se habilitarán los mejores métodos para proteger la base de datos.

## <a name="configure-hello-azure-mysql-database"></a>Configurar la base de datos de MySQL de Azure de Hola

En la ventana de terminal de hello en el equipo, conéctese toohello MySQL server en Azure. Usar valor de Hola que especificó anteriormente por `<admin_user>` y `<mysql_server_name>`.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>Crear una base de datos 

Hola `mysql` símbolo del sistema, cree una base de datos y una tabla para hello elementos pendientes.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>Creación de un usuario con permisos

Crear un usuario de base de datos y conceder a todos los privilegios de hello `tododb` base de datos. Reemplace los marcadores de posición de hello `<Javaapp_user>` y `<Javaapp_password>` con su propio nombre de aplicación único.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

Escriba `quit` para salir de la conexión del servidor.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Implementar el ejemplo de Hola tooAzure servicio de aplicaciones

Crear un plan de servicio de aplicaciones de Azure con hello **libre** tarifa con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando de CLI. plan de servicio de aplicaciones de Hello define Hola recursos físicos que usa toohost sus aplicaciones. Todas las aplicaciones asignadas plan de servicio de aplicaciones de tooan compartan estos recursos, permitiéndole toosave costo al hospedar varias aplicaciones. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Si plan de hello está listo, Hola que CLI de Azure muestra similar salida toohello siguiente ejemplo:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Creación de una aplicación web de Azure

 Hola de uso [crear webapp az](/cli/azure/appservice/web#create) toocreate de comando CLI una definición de aplicación web en hello `myAppServicePlan` plan de servicio de aplicaciones. definición de la aplicación Hello web proporciona una tooaccess de dirección URL a la aplicación con y configura varias toodeploy opciones tooAzure de su código. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Hola sustituto `<app_name>` marcador de posición con su propio nombre de aplicación único. Este nombre único forma parte del nombre de dominio predeterminado de hello para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de Azure. Puede asignar una aplicación web de dominio personalizado nombre entrada toohello antes de exponer tooyour a los usuarios.

Cuando la definición de la aplicación hello web está listo, Hola CLI de Azure muestra información toohello similar siguiente ejemplo: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Configuración de Java 

Establecer la configuración de tiempo de ejecución de Java de Hola que necesita la aplicación con hello [actualización de la configuración de az servicio de aplicaciones web](/cli/azure/appservice/web/config#update) comando.

Hello siguiente comando configura toorun de aplicación web de hello en una versión reciente de Java 8 JDK y [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Configurar base de datos de hello aplicación toouse Hola SQL Azure

Antes de ejecutar la aplicación de ejemplo de Hola, establecer configuración de la aplicación en hello web app toouse hello Azure base de datos MySQL que creó en Azure. Estas propiedades son de la aplicación web toohello expuesto como variables de entorno e invalidan los valores de hello establecidos en hello application.properties dentro de la aplicación web empaquetada de hello. 

Establecer la configuración de la aplicación [az webapp configuración appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) Hola CLI:

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a>Obtención de credenciales de implementación de FTP 
Puede implementar el servicio de aplicaciones de tooAzure de aplicación de varias maneras, como FTP, local Git, GitHub, Visual Studio Team Services y BitBucket. En este ejemplo, FTP toodeploy Hola. Archivo WAR generado anteriormente en el servicio de aplicaciones tooAzure de equipo local.

toodetermine sobre qué credenciales se toopass a lo largo de un toohello de comandos de ftp aplicación Web, Use [az servicio de aplicaciones web implementación lista publicación perfiles-](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) comando: 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a>Cargar la aplicación hello mediante FTP

Utilice los favoritos Hola de toodeploy de herramienta FTP. Toohello de archivo WAR */site/wwwroot/webapps* carpeta en la dirección del servidor hello tomado de Hola `URL` campo comando anterior Hola. Quitar el directorio de aplicación predeterminado (raíz) existente hello y reemplace Hola existente ROOT.war con hello. Archivo WAR integrado Hola anteriormente en el tutorial de Hola.

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a>Aplicación de prueba hello web

Examinar demasiado`http://<app_name>.azurewebsites.net/` y agregar algunas tareas toohello lista. 

![Aplicación Java que se ejecuta en Azure App Service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**¡Enhorabuena!** Ya está ejecutando una aplicación Java orientada a datos en Azure App Service.

## <a name="update-hello-app-and-redeploy"></a>Volver a implementar y aplicación de hello de actualización

Actualizar Hola aplicación tooinclude una columna adicional en la lista de tareas de Hola para que se creó el elemento de hello día. Arranque de primavera controla actualizar esquema de base de datos de Hola de como Hola cambios del modelo de datos sin modificar los registros de base de datos existente.

1. En el sistema local, se abrirán *src/main/java/com/example/fabrikam/TodoItem.java* y agregue la siguiente Hola importa toohello clase:   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. Agregar un `String` propiedad `timeCreated` demasiado*src/main/java/com/example/fabrikam/TodoItem.java*, inicializándola con una marca de tiempo en la creación del objeto. Agregar los captadores/establecedores de hello nueva `timeCreated` propiedad mientras se está editando este archivo.

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. Actualización *src/main/java/com/example/fabrikam/TodoDemoController.java* con una línea en hello `updateTodo` método tooset Hola timestamp:

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Agregar compatibilidad para el nuevo campo de hello en plantilla de hello Thymeleaf. Actualización *src/main/resources/templates/index.html* con un nuevo encabezado de tabla para la marca de tiempo de Hola y un nuevo valor del campo toodisplay Hola de marca de tiempo de hello en cada fila de datos de tabla.

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. Recompilar la aplicación hello:

    ```bash
    mvnw clean package 
    ```

6. Hola FTP que se actualiza. WAR como antes, quitar Hola existente *sitio/wwwroot/aplicaciones Web/ROOT* directorio y *ROOT.war*, a continuación, cargar Hola actualizado. Archivo WAR como ROOT.war. 

Al actualizar la aplicación hello, un **vez crea** columna es visible ahora. Cuando se agrega una nueva tarea, aplicación hello rellenará automáticamente Hola marca de tiempo. Las tareas existentes permanecen sin cambios y trabajar con la aplicación hello aunque Hola subyacente modelo de datos ha cambiado. 

![Aplicación de Java actualizada con una nueva columna](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>Transmisión de registros de diagnóstico 

Mientras se ejecuta la aplicación de Java en el servicio de aplicación de Azure, puede obtener consola Hola registros directamente canalizan tooyour terminal. De este modo, puede obtener Hola mensajes de diagnóstico del mismo toohelp depurar errores de aplicación.

registro toostart transmisión por secuencias, utilice hello [final del registro de aplicación Web az](/cli/azure/appservice/web/log#tail) comando.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Administración de la aplicación web de Azure

Vaya toohello toosee portal Azure hello web aplicación que creó.

toodo esto, inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com).

Hola menú izquierdo, haga clic en **servicio de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-java-mysql/access-portal.png)

De forma predeterminada, la hoja de la aplicación web muestra hello **Introducción** página. Esta página proporciona una visión del funcionamiento de la aplicación. En este caso, también puede realizar tareas de administración como detener, iniciar, reiniciar y eliminar. pestañas: Hola a la izquierda Hola de hoja de hello páginas de configuración diferente de hello que puede abrir.

![Hoja de App Service en Azure Portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Estas pestañas de hoja de hello mostrarán hello muchas características excepcionales, puede agregar la aplicación web de tooyour. Hola lista siguiente proporciona solo algunas de las posibilidades de hello:
* Asignación de un nombre DNS personalizado
* Enlace de un certificado SSL personalizado
* Configuración de la implementación continua
* Escalado vertical y horizontal
* Adición de la autenticación de usuarios

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no necesita estos recursos para otro tutorial (vea [pasos siguientes](#next)), puede eliminarlos mediante la ejecución de hello siguiente comando: 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>Pasos siguientes

> [!div class="checklist"]
> * Crear una base de datos MySQL en Azure
> * Conectar una aplicación de Java ejemplo toohello MySQL
> * Implementar Hola aplicación tooAzure
> * Actualizar y volver a implementar la aplicación hello
> * Transmitir registros de diagnóstico desde Azure
> * Administrar aplicación Hola Hola portal de Azure

Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre toohello aplicación.

> [!div class="nextstepaction"] 
> [Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md)
