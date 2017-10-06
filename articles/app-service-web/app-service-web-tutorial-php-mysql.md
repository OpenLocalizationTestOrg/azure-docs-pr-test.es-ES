---
title: "aaaBuild una aplicación web PHP y MySQL en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooget una aplicación PHP trabajando en Azure, con conexión tooa MySQL de base de datos en Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Compilación de una aplicación web PHP y MySQL en Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático. Este tutorial muestra cómo toocreate un PHP web de aplicación en Azure y conectar tooa base de datos de MySQL. Cuando haya terminado, tendrá una aplicación [Laravel](https://laravel.com/) que se ejecuta en Azure App Service Web Apps.

![Aplicación PHP que se ejecuta en Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una base de datos MySQL en Azure
> * Conectar un tooMySQL de aplicación PHP
> * Implementar Hola aplicación tooAzure
> * Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello
> * Transmitir registros de diagnóstico desde Azure
> * Administrar aplicación Hola Hola portal de Azure

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

* [Instalación de Git](https://git-scm.com/)
* [Instalación de PHP 5.6.4, o cualquier versión posterior](http://php.net/downloads.php)
* [Instalación de Composer](https://getcomposer.org/doc/00-intro.md)
* Habilitar Hola siguiendo las extensiones PHP necesidades Laravel: OpenSSL, MySQL PDO, Mbstring, Tokenizer, XML
* [Instalación e inicio de MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Preparación de MySQL local

En este paso, creará una base de datos en el servidor MySQL local para usarlo en este tutorial.

### <a name="connect-toolocal-mysql-server"></a>Conectar toolocal MySQL server

En una ventana de terminal, conéctese tooyour local MySQL server. Puede utilizar esta ventana de terminal toorun todos los comandos de hello en este tutorial.

```bash
mysql -u root -p
```

Si se le pide una contraseña, escriba contraseña Hola de hello `root` cuenta. Si no recuerda su contraseña de la cuenta raíz, consulte [MySQL: cómo tooReset Hola contraseña raíz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Si el comando se ejecuta correctamente, significa que el servidor MySQL está en ejecución. Si no es así, asegúrese de que el servidor MySQL local debe iniciarse mediante Hola siguiente [pasos posteriores a la instalación de MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Creación de una base de datos local

En hello `mysql` símbolo del sistema, cree una base de datos.

```sql 
CREATE DATABASE sampledb;
```

Escriba `quit` para salir de la conexión del servidor.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Creación de una aplicación PHP local
En este paso, obtendrá una aplicación Laravel de ejemplo, configurará la conexión a base de datos correspondiente y la ejecutará de forma local. 

### <a name="clone-hello-sample"></a>Ejemplo de Hola de clon

En la ventana de terminal de hello, `cd` tooa directorio de trabajo.

Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`tooyour directorio clonado.
Instalar paquetes de saludo necesario.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>Configuración de la conexión a MySQL

En el directorio raíz del repositorio de hello, cree un archivo denominado *.env*. Hola copia siguiendo las variables en hello *.env* archivo. Reemplace hello  _&lt;root_password >_ marcador de posición con la contraseña del usuario de hello MySQL raíz.

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

Para obtener información acerca de cómo Laravel usa hello _.env_ de archivos, consulte [Laravel configuración de entorno](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Ejecutar el ejemplo hello localmente

Ejecutar [migraciones de base de datos de Laravel](https://laravel.com/docs/5.4/migrations) toocreate Hola tablas hello las necesidades de aplicación. toosee qué tablas se crean en las migraciones de hello, busque en hello _base de datos/migraciones_ directorio en el repositorio de Git Hola.

```bash
php artisan migrate
```

Genere una nueva clave de aplicación Laravel.

```bash
php artisan key:generate
```

Ejecute la aplicación hello.

```bash
php artisan serve
```

Navegue demasiado`http://localhost:8000` en un explorador. Agregue algunas tareas en la página de Hola.

![PHP conecta correctamente tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Escriba toostop PHP, `Ctrl + C` Hola terminal.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>Creación de MySQL en Azure

En este paso, creará una base de datos MySQL en [Azure Database for MySQL (versión preliminar)](/azure/mysql). Posteriormente, configurar base de datos de hello PHP aplicación tooconnect toothis.

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>Creación de un servidor MySQL

Crear un servidor de base de datos de Azure para MySQL (versión preliminar) con hello [crear servidor de mysql az](/cli/azure/mysql/server#create) comando.

Hola siguiente comando, sustituya el nombre del servidor MySQL donde verá hello  _&lt;mysql_server_name >_ marcador de posición (los caracteres válidos son `a-z`, `0-9`, y `-`). Este nombre forma parte del nombre de host del servidor de MySQL de hello (`<mysql_server_name>.database.windows.net`), necesita toobe único global.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Cuando se crea el servidor de MySQL de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a>Configuración del firewall del servidor

Cree una regla de firewall para el cliente de MySQL server tooallow conexiones con hello [crear az mysql server regla de firewall](/cli/azure/mysql/server/firewall-rule#create) comando.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Base de datos de Azure para MySQL (versión preliminar) actualmente no limita los servicios de tooAzure solo de las conexiones. Tal y como se asignan dinámicamente direcciones IP en Azure, es mejor tooenable todas las direcciones IP. servicio de Hello está en vista previa. Se planean los mejores métodos para proteger la base de datos.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Conectar tooproduction MySQL server localmente

En la ventana de terminal de hello, conectar toohello MySQL server en Azure. Usar valor de Hola que especificó anteriormente por  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

Cuando se le pida una contraseña, utilice _tr0ngPa $$ w0rd!_, que especificó cuando creó la base de datos de Hola.

### <a name="create-a-production-database"></a>Creación de una base de datos de producción

En hello `mysql` símbolo del sistema, cree una base de datos.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>Creación de un usuario con permisos

Cree un usuario de base de datos llamado _phpappuser_ y conceder a todos los privilegios de hello `sampledb` base de datos.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Salir de conexión del servidor de hello escribiendo `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Conectar aplicaciones tooAzure MySQL

En este paso, se conectará Hola PHP aplicación toohello base de datos MySQL que creó en la base de datos de Azure para MySQL (versión preliminar).

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Configurar conexión de base de datos de Hola

En el directorio raíz del repositorio de hello, cree un _. env.production_ Hola de archivo y copie después de las variables en él. Reemplace el marcador de posición de hello  _&lt;mysql_server_name >_.

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

Guarde los cambios de Hola.

> [!TIP]
> toosecure la información de conexión de MySQL, este archivo ya está excluida de repositorio de Git de hello (vea _.gitignore_ en el directorio raíz del repositorio hello). Más adelante, aprenderá cómo variables de entorno de tooconfigure de tooyour tooconnect de servicio de aplicaciones de base de datos en la base de datos de Azure para MySQL (versión preliminar). Con las variables de entorno, no es necesario hello *.env* archivo en el servicio de aplicaciones.
>

### <a name="configure-ssl-certificate"></a>Configuración de un certificado SSL

De manera predeterminada, Azure Database for MySQL aplica las conexiones SSL de los clientes. tooconnect tooyour base de datos MySQL en Azure, debe usar un _.pem_ certificado SSL.

Abra _config/database.php_ y agregue hello _sslmode_ y _opciones_ parámetros demasiado`connections.mysql`, tal y como se muestra en el siguiente código de hello.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn cómo toogenerate esto _certificate.pem_, consulte [tooAzure base de datos de conexión de conectividad de configurar SSL en su aplicación toosecurely para MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> ruta de acceso de Hello _/ssl/certificate.pem_ señala existente tooan _certificate.pem_ archivo en el repositorio de Git Hola. Para su comodidad, en este tutorial se proporciona este archivo. Como procedimiento recomendado, no debe confirmar los certificados _.pem_ en el control de código fuente. 
>

### <a name="test-hello-application-locally"></a>Probar la aplicación hello localmente

Ejecutar migraciones de base de datos de Laravel con _. env.production_ como Hola tablas de Hola de toocreate de archivos de entorno de la base de datos MySQL en la base de datos de Azure para MySQL (versión preliminar). Recuerde que _. env.production_ tiene la base de datos MySQL tooyour de información de conexión de hello en Azure.

```bash
php artisan migrate --env=production --force
```

El archivo _.env.production_ aún no cuenta con una clave de aplicación válida. Generar una nueva contraseña para él en hello terminal.

```bash
php artisan key:generate --env=production --force
```

Ejecutar la aplicación de ejemplo Hola _. env.production_ como archivo de entorno de hello.

```bash
php artisan serve --env=production
```

Navegue demasiado`http://localhost:8000`. Si la página de Hola se carga sin errores, Hola aplicación PHP está conectando toohello base de datos MySQL en Azure.

Agregue algunas tareas en la página de Hola.

![PHP conecta correctamente tooAzure base de datos de MySQL (versión preliminar)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Escriba toostop PHP, `Ctrl + C` Hola terminal.

### <a name="commit-your-changes"></a>Confirmación de los cambios

Ejecute hello después toocommit de comandos de Git los cambios:

```bash
git add .
git commit -m "database.php updates"
```

La aplicación es listo toobe implementado.

## <a name="deploy-tooazure"></a>Implementar tooAzure

En este paso, implementará Hola conectado MySQL PHP aplicación tooAzure servicio de aplicaciones.

### <a name="create-an-app-service-plan"></a>Creación de un plan de App Service

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Creación de una aplicación web

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Versión de PHP Hola de conjunto

Versión de PHP de Hola de conjunto que Hola aplicación requiere mediante hello [conjunto de configuración de aplicación Web de az](/cli/azure/webapp/config#set) comando.

Hello siguiente comando establece Hola PHP versión too_7.0_.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Configuración de la base de datos

Como se indicó anteriormente, puede conectarse tooyour de base de datos de MySQL de Azure mediante variables de entorno de servicio de aplicaciones.

En el servicio de aplicación, establecer variables de entorno como _configuración de la aplicación_ mediante el uso de hello [az webapp configuración appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.

Hello siguiente comando configura configuración de la aplicación hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, y `DB_PASSWORD`. Reemplace los marcadores de posición de hello  _&lt;appname >_ y  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

Puede usar hello PHP [getenv](http://www.php.net/manual/function.getenv.php) método tooaccess Hola configuración. Hola Laravel código usa un [env](https://laravel.com/docs/5.4/helpers#method-env) contenedor a través de hello PHP `getenv`. Por ejemplo, configuración de MySQL de hello en _config/database.php_ aspecto Hola siguiente código:

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a>Configuración de las variables de entorno de Laravel

Laravel necesita una clave de aplicación en App Service. Puede configurarlo con valores de aplicación.

Use `php artisan` toogenerate una nueva clave de aplicación sin guardarlo too_.env_.

```bash
php artisan key:generate --show
```

Establecer tecla de aplicación Hola Hola servicio de aplicaciones de aplicación web mediante hello [az webapp configuración appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando. Reemplace los marcadores de posición de hello  _&lt;appname >_ y  _&lt;outputofphpartisankey: generar >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`indica Laravel tooreturn información de depuración cuando Hola implementa la aplicación web encuentra errores. Al ejecutar una aplicación de producción, se establece demasiado`false`, que es más seguro.

### <a name="set-hello-virtual-application-path"></a>Establecer la ruta de aplicación virtual de Hola

Establecer ruta de acceso de aplicación virtual de hello para la aplicación web de Hola. Este paso es necesario porque hello [ciclo de vida de aplicación Laravel](https://laravel.com/docs/5.4/lifecycle) comienza en hello _público_ directorio en lugar del directorio raíz de la aplicación hello. Otros marcos PHP cuyo ciclo de vida de inicio en el directorio raíz de hello pueden trabajar sin necesidad de configuración manual de hello ruta de acceso virtual.

Establecer la ruta de aplicación virtual de hello mediante el uso de hello [actualización de recursos az](/cli/azure/resource#update) comando. Reemplace hello  _&lt;appname >_ marcador de posición.

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

De forma predeterminada, el servicio de aplicación de Azure puntos de ruta de acceso de aplicación virtual de raíz de hello (_/_) directorio de raíz de toohello de hello implementa archivos de aplicación (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Configuración de un usuario de implementación

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Configurar la implementación de Git local

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>TooAzure de inserción de Git

Agregue un repositorio de Git local de Azure tooyour remoto.

```bash
git remote add azure <paste_copied_url_here>
```

Insertar la aplicación PHP de toohello toodeploy remoto Azure Hola. Se le solicite para contraseña de Hola que proporcionó anteriormente como parte de la creación de hello de usuario de implementación de Hola.

```bash
git push azure master
```

Durante la implementación, Azure App Service comunicará su progreso con Git.

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> Puede observar que el proceso de implementación de hello instala [compositor](https://getcomposer.org/) paquetes final Hola. Servicio de aplicaciones no ejecuta estos automatizaciones durante la implementación de forma predeterminada, por lo que este repositorio de ejemplo tiene tres adicionales archivos en su tooenable del directorio raíz que:
>
> - `.deployment`-Este archivo indica toorun de servicio de aplicaciones `bash deploy.sh` como script de implementación personalizada de Hola.
> - `deploy.sh`-Hola script de implementación personalizado. Si examina el archivo hello, verá que se ejecuta `php composer.phar install` después `npm install`.
> - `composer.phar`-Administrador de paquetes de saludo compositor.
>
> Puede usar este enfoque tooadd cualquier tooApp de implementación basado en Git tooyour paso servicio. Para obtener más información, consulte [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script) (Script de implementación personalizado).
>

### <a name="browse-toohello-azure-web-app"></a>Examinar la aplicación web de Azure de toohello

Examinar demasiado`http://<app_name>.azurewebsites.net` y agregar algunas tareas toohello lista.

![Aplicación PHP que se ejecuta en Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

Ya está ejecutando una aplicación PHP orientada a datos en Azure App Service.

## <a name="update-model-locally-and-redeploy"></a>Actualización local del modelo y nueva implementación

En este paso, realice un cambio sencillo toohello `task` datos de modelo y Hola webapp y, a continuación, publicar Hola actualización tooAzure.

Para el escenario de tareas de hello, modificar aplicación hello por lo que puede marcar una tarea como completa.

### <a name="add-a-column"></a>Adición de una columna

Hola terminal, vaya toohello raíz del repositorio de Git Hola.

Generar una migración de base de datos nueva para hello `tasks` tabla:

```bash
php artisan make:migration add_complete_column --table=tasks
```

Este comando mostrará Hola nombre del archivo de migración de Hola que se genera. Busque este archivo en _database/migrations_ y ábralo.

Reemplace hello `up` método con el siguiente código de hello:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Hello código anterior agrega una columna booleana en hello `tasks` tabla denominada `complete`.

Reemplace hello `down` método con hello siguiente código para la acción de reversión de hello:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

Hola terminal, ejecute las migraciones de base de datos de Laravel toomake cambios de hello en la base de datos local de Hola.

```bash
php artisan migrate
```

En función de hello [convención de nomenclatura de Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modelo de hello `Task` (vea _app/Task.php_) asigna toohello `tasks` tabla de forma predeterminada.

### <a name="update-application-logic"></a>Actualización de la lógica de aplicación

Abra hello *routes/web.php* archivo. aplicación Hello define sus rutas y aquí la lógica de negocios.

Al final de Hola de archivo hello, agregue una ruta con hello siguiente código:

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

Hello código precedente crea un modelo de datos de una sencilla actualización toohello, cambie el valor de Hola de `complete`.

### <a name="update-hello-view"></a>Actualizar vista Hola

Abra hello *resources/views/tasks.blade.php* archivo. Buscar hello `<tr>` etiqueta de apertura y reemplácela con:

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Hola anterior cambia de color fila código Hola dependiendo de si la tarea hello es completa.

En la siguiente línea hello, deberá Hola siguiente código:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Reemplace toda la línea hello con hello siguiente código:

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

Hello código anterior agrega botón de envío de Hola que hace referencia la ruta de Hola que definió anteriormente.

### <a name="test-hello-changes-locally"></a>Probar los cambios de hello localmente

Directorio raíz de hello del repositorio de Git de hello, ejecutar el servidor de desarrollo de Hola.

```bash
php artisan serve
```

Hola toosee cambio de estado de tareas, navegue demasiado`http://localhost:8000` y seleccione Hola casilla.

![Casilla de verificación agregado tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

Escriba toostop PHP, `Ctrl + C` Hola terminal.

### <a name="publish-changes-tooazure"></a>Publicar cambios tooAzure

Hola terminal, ejecutar migraciones de base de datos de Laravel con cambio Hola producción conexión cadena toomake Hola Hola base de datos de Azure.

```bash
php artisan migrate --env=production --force
```

Confirmar todos los cambios de hello en Git y, a continuación, insertar tooAzure de cambios de código de hello.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Una vez Hola `git push` es completar, navegue toohello Azure web app y prueba Hola nueva funcionalidad.

![TooAzure publiquen los cambios de modelo y la base de datos](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Si ha agregado las tareas, sí se conservan en la base de datos de Hola. Esquema de datos de las actualizaciones toohello dejar intacta la datos existentes.

## <a name="stream-diagnostic-logs"></a>Transmisión de registros de diagnóstico

Mientras Hola aplicación PHP se ejecuta en el servicio de aplicación de Azure, puede obtener registros de consola hello tooyour canalizada terminal. De este modo, puede obtener Hola mensajes de diagnóstico del mismo toohelp depurar errores de aplicación.

registro toostart transmisión por secuencias, utilice hello [final del registro de aplicación Web az](/cli/azure/webapp/log#tail) comando.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

Cuando se inicia la transmisión por secuencias de registro, actualización de aplicación web de Azure de hello en hello explorador tooget cierto tráfico web. Ahora puede ver terminal de toohello canalizada de registros de consola. Si no ve los registros de la consola de inmediato, vuelve a comprobarlo en 30 segundos.

registro de toostop de transmisión por secuencias en cualquier momento, tipo `Ctrl` + `C`.

> [!TIP]
> Una aplicación PHP puede usar el estándar de hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello consola. aplicación de ejemplo de Hola usa este enfoque en _app/Http/routes.php_.
>
> Un marco de trabajo web, [Laravel utiliza Monolog](https://laravel.com/docs/5.4/errors) como proveedor de registro de hello. toosee cómo tooget Monolog toooutput mensajes toohello consola, consulte [PHP: cómo toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Administrar la aplicación web de Azure de hello

Vaya toohello [portal de Azure](https://portal.azure.com) toomanage hello web aplicación que creó.

Hola menú izquierdo, haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-php-mysql/access-portal.png)

Podrá ver la página de información general de la aplicación web. Aquí se pueden realizar tareas de administración básicas como detener, iniciar, reiniciar, examinar y eliminar.

menú de la izquierda Hola proporciona páginas para la configuración de la aplicación.

![Página de App Service en Azure Portal](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, aprendió a:

> [!div class="checklist"]
> * Crear una base de datos MySQL en Azure
> * Conectar un tooMySQL de aplicación PHP
> * Implementar Hola aplicación tooAzure
> * Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello
> * Transmitir registros de diagnóstico desde Azure
> * Administrar aplicación Hola Hola portal de Azure

Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre tooa web app.

> [!div class="nextstepaction"]
> [Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md)
