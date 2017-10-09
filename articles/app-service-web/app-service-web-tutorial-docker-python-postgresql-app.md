---
title: "aaaBuild una aplicación web de Python de Docker y PostgreSQL en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo una aplicación de Python Docker tooget trabajando en Azure, con conexión tooa PostgreSQL base de datos."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>Compilación de una aplicación web Docker Python con PostgreSQL en Azure

Azure Web Apps proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático. Este tutorial muestra cómo toocreate un Docker de Python básico web aplicación en Azure. Se conectará a esta base de datos de aplicación tooa PostgreSQL. Cuando haya terminado, tendrá una aplicación Python Flask que se ejecuta en un contenedor Docker en [Azure App Service Web Apps](app-service-web-overview.md).

![Aplicación Docker Python Flask en Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

Puede seguir estos pasos hello en macOS. Instrucciones de Linux y Windows son Hola igual en la mayoría de los casos, pero no se detallan las diferencias de hello en este tutorial.
 
## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

1. [Instalación de Git](https://git-scm.com/)
1. [Instalación de Python](https://www.python.org/downloads/)
1. [Instalación y ejecución de PostgreSQL](https://www.postgresql.org/download/)
1. [Instalación de Docker Community Edition](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>Prueba de la instalación local de PostgreSQL y creación de una base de datos

Abra la ventana de terminal de Hola y ejecute `psql postgres` tooconnect tooyour servidor local de PostgreSQL.

```bash
psql postgres
```

Si la conexión se realiza correctamente, significa que la base de datos PostgreSQL está en ejecución. Si no es así, asegúrese de que se ha iniciado la base de datos PostgresQL local siguiendo los pasos de hello en [descargas - PostgreSQL Core distribución](https://www.postgresql.org/download/).

Cree una base de datos denominada *eventregistration* y configure un usuario de base de datos independiente denominado *manager* cuya contraseña será *supersecretpass*.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
Tipo de *\q* cliente de tooexit Hola PostgreSQL. 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>Creación de una aplicación Python Flask local

En este paso, configurar un proyecto Python matraz Hola local.

### <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ventana de terminal de hello abierto, y `CD` tooa directorio de trabajo.  

Siguiente ejecución Hola comandos de ejemplo de Hola repositorio y vaya toohello de tooclone *initialapp 0,1* de la versión.

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

Este repositorio de ejemplo contiene una aplicación [Flask](http://flask.pocoo.org/). 

### <a name="run-hello-application"></a>Ejecutar la aplicación hello

> [!NOTE] 
> En un paso posterior simplifican este proceso mediante la creación de un toouse de contenedor de Docker con la base de datos de producción de hello.

Instalar paquetes de saludo necesario e inicie la aplicación hello.

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Cuando se ha cargado completamente la aplicación hello, verá algo similar toohello siguiente mensaje:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Navegue toohttp://127.0.0.1:5000 en un explorador. Haga clic en **Register!** (Registrarse) y cree un usuario de prueba.

![Aplicación Python Flask que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

aplicación de ejemplo matraz Hola almacena datos de usuario de base de datos de Hola. Si es correcta en el registro de un usuario, la aplicación está escribiendo la base de datos de PostgreSQL local de datos toohello.

tipo de servidor de toostop Hola matraz en cualquier momento, que Ctrl + C en hello terminal. 

## <a name="create-a-production-postgresql-database"></a>Creación de una base de datos PostgreSQL de producción

En este paso, creará una base de datos PostgreSQL en Azure. Cuando la aplicación esté implementada tooAzure, usará esta base de datos en la nube.

### <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Son ahora necesitan de curso toouse hello Azure CLI 2.0 toocreate Hola recursos toohost la aplicación de Python en el servicio de aplicación de Azure.  Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones. 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create). 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hello en el ejemplo siguiente se crea un grupo de recursos en la región del oeste de Estados Unidos de hello:

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

Hola de uso [az de servicio de aplicaciones enumerar ubicaciones](/cli/azure/appservice#list-locations) ubicaciones disponibles toolist de comandos de CLI de Azure.

### <a name="create-an-azure-database-for-postgresql-server"></a>Creación de un servidor de Azure Database for PostgreSQL

Crear un servidor de PostgreSQL con hello [az postgres servidor crear](/cli/azure/documentdb#create) comando.

En hello siguiente comando, sustitúyalo por un nombre de servidor único para hello  *\<postgresql_name >* marcador de posición y un nombre de usuario para hello  *\<admin_username >* marcador de posición . nombre del servidor Hola se usa como parte de su punto de conexión de PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), por lo que el nombre de hello necesita toobe único en todos los servidores en Azure. nombre de usuario de Hello es para la cuenta de usuario de administrador de base de datos inicial de Hola. Son solicitada toopick una contraseña para este usuario.

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

Cuando se crea Hola base de datos de Azure para servidor PostgreSQL, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>Crear una regla de firewall para hello base de datos de Azure para servidor de PostgreSQL

Ejecute hello siguiendo la base de datos de Azure CLI comando tooallow access toohello de todas las direcciones IP.

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

Hola CLI de Azure confirma la creación de reglas de firewall de hello con salida toohello similar siguiente ejemplo:

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-toohello-database"></a>Conectarse a la base de datos de Python matraz aplicación toohello

En este paso, se conectará su toohello de aplicación de ejemplo base de datos de Azure matraz de Python para servidor PostgreSQL que ha creado.

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>Creación de una base de datos vacía y configuración de un nuevo usuario de la aplicación de base de datos

Cree un usuario de base de datos con acceso tooa único solo base de datos. Usará estos tooavoid credenciales entregar Hola aplicación acceso completo toohello servidor.

Conectar la base de datos de toohello (se le pide la contraseña de administrador).

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

Crear base de datos de Hola y de usuario de hello PostgreSQL CLI.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

Tipo de *\q* cliente de tooexit Hola PostgreSQL.

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>Probar la aplicación hello localmente en la base de datos de Azure PostgreSQL de Hola 

Si vuelve ahora toohello *aplicación* carpeta de hello clona el repositorio de Github, puede ejecutar aplicación de Python matraz hello mediante la actualización de las variables de entorno de base de datos de Hola.

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Cuando se ha cargado completamente la aplicación hello, verá algo similar toohello siguiente mensaje:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Navegue toohttp://127.0.0.1:5000 en un explorador. Haga clic en **Register!** (Registrarse) y cree un registro de prueba. Ahora se escribe toohello de datos en Azure.

![Aplicación Python Flask que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>Ejecutar la aplicación hello desde un contenedor de Docker

Crear imagen de contenedor de Docker Hola.

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker muestra una confirmación de que el contenedor de hello, se creó correctamente.

```bash
Successfully built 7548f983a36b
```

Agregar el archivo de la variable de entorno entorno variables tooan de base de datos *db.env*. aplicación Hello conectará toohello base de datos de producción de PostgreSQL en Azure.

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

Ejecute la aplicación hello desde dentro del contenedor de Docker de Hola. Hola siguiente comando Especifica el archivo de variables de entorno de Hola y asigna Hola predeterminado matraz puerto 5000 toolocal puerto 5000.

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

salida de Hello es toowhat similar que vio anteriormente. Sin embargo, migración de base de datos inicial de hello ya no necesita toobe realiza y, por tanto, se omite.

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

base de datos de Hello ya contiene el registro de hello que creó anteriormente.

![Aplicación Python Flask basada en contenedor Docker que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>Cargar registro de contenedor de hello Docker contenedor tooa

En este paso, se carga del registro de contenedor de hello Docker contenedor tooa. Se usará Azure Container Registry, pero también se pueden usar otros registros conocidos, como Docker Hub.

### <a name="create-an-azure-container-registry"></a>Creación de una instancia de Azure Container Registry

Hola después de un registro de contenedor del comando toocreate reemplazar  *\<registry_name >* con un nombre de contenedor de Azure único del registro de su elección.

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

Salida
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>Recuperar las credenciales del registro de hello para insertar y extraer imágenes de Docker

las credenciales del registro de tooshow, habilite el modo de administrador en primer lugar.

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

Verá dos contraseñas. Tome nota del nombre de usuario de Hola y la contraseña primera Hola.

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-tooazure-container-registry"></a>Cargar su tooAzure de contenedor del registro de contenedor de Docker

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>Implementar hello Docker Python matraz aplicación tooAzure

En este paso, implementará la tooAzure de aplicación en la matraz de Python en el basado en el contenedor de Docker servicio de aplicaciones.

### <a name="create-an-app-service-plan"></a>Creación de un plan de App Service

Crear un plan de servicio de aplicaciones con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello en el ejemplo siguiente se crea un plan de servicio de aplicaciones basadas en Linux denominado *myAppServicePlan* con hello S1 tarifa:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

Cuando se crea el plan de servicio de aplicación Hola, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a>Creación de una aplicación web

Crear una aplicación web en hello *myAppServicePlan* plan de servicio de aplicaciones con hello [crear webapp az](/cli/azure/webapp#create) comando. 

Hola web aplicación le ofrece un hospedaje espacio toodeploy el código y proporciona una dirección URL de hello tooview implementado la aplicación. Aplicación web de uso toocreate Hola. 

Hola el siguiente comando, reemplace hello  *\<app_name >* marcador de posición con un nombre de aplicación único. Este nombre forma parte de la dirección URL predeterminada de hello para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de servicio de aplicaciones de Azure. 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Cuando se ha creado la aplicación web de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo: 

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

### <a name="configure-hello-database-environment-variables"></a>Configurar las variables de entorno de base de datos de Hola

Anteriormente en el tutorial de hello, ha definido la base de datos PostgreSQL tooyour de tooconnect de variables de entorno.

En el servicio de aplicación, establecer variables de entorno como _configuración de la aplicación_ mediante el uso de hello [az webapp configuración appsettings conjunto](/cli/azure/webapp/config#set) comando. 

Hello en el ejemplo siguiente se especifica detalles de conexión de base de datos de hello como configuración de la aplicación. También usa hello *puerto* variable toomap puerto 5000 desde el tráfico de contenedor Docker tooreceive HTTP en el puerto 80.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>Configuración de la implementación del contenedor de Docker 

App Service puede descargar automáticamente un contenedor de Docker y ejecutarlo.

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

Siempre que actualiza el contenedor de Docker de Hola o cambia la configuración de hello, reinicie la aplicación hello. Reiniciar, se garantiza que todas las configuraciones se aplican y contenedor más reciente de Hola se extrae del registro de hello.

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>Examinar la aplicación web de Azure de toohello 

Examinar toohello implementa la aplicación web mediante el explorador web. 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> aplicación web de Hello tiene más tooload como contenedor de hello tiene toobe descargará y se iniciará después de cambia la configuración del contenedor de Hola.

Vea a invitados previamente registrados que se guardaron toohello base de datos de producción de Azure en el paso anterior de Hola.

![Aplicación Python Flask basada en contenedor Docker que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**¡Enhorabuena!** Ya está ejecutando una aplicación Python Flask basada en contenedor en Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Actualización del modelo de datos y nueva implementación

En este paso es agregar el número de hello asistentes tooeach del registro de eventos mediante la actualización de modelo de invitado de Hola.

Extraer del repositorio hello *0,2 migración* versión con el siguiente comando de git de hello:

```bash
git checkout tags/0.2-migration
```

Esta versión ya realizada Hola modelo, los controladores y tooviews cambios necesarios. También incluye una migración de base de datos generada mediante *alembic* (`flask db migrate`). Puede ver todos los cambios realizados a través del siguiente comando de git de hello:

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>Prueba de los cambios localmente

Ejecute hello después comandos tootest los cambios localmente por servidor en ejecución Hola matraz.

Mac o Linux:
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Navegue toohttp://127.0.0.1:5000 los cambios de hello tooview de explorador. Cree un registro de prueba.

![Aplicación Python Flask basada en contenedor Docker que se ejecuta de forma local](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>Publicar cambios tooAzure

Crear nueva imagen de docker Hola, Insertar registro de contenedor de toohello y reiniciar la aplicación hello.

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

Navegar por la aplicación web de Azure de tooyour e inténtelo de nuevo funcionalidad nueva de Hola. Cree otro registro de eventos.

```bash 
http://<app_name>.azurewebsites.net 
```

![Aplicación Docker Python Flask en Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>Administración de la aplicación web de Azure

Vaya toohello [portal de Azure](https://portal.azure.com) toosee hello web aplicación que creó.

Hola menú izquierdo, haga clic en **servicios de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

De forma predeterminada, el portal de hello muestra la aplicación web **Introducción** página. Esta página proporciona una visión del funcionamiento de la aplicación. En este caso, también puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. pestañas: Hola a la izquierda Hola de página Hola páginas de configuración diferente de hello que puede abrir.

![Página de App Service en Azure Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>Pasos siguientes

Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre tooyour web app.

> [!div class="nextstepaction"] 
> [Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md)
