---
title: "aaaBuild una aplicación de gran escala en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse distintos servicios de Azure toomaximize Hola rendimiento de una aplicación ASP.NET en Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Creación de una aplicación web a gran escala en Azure

Este tutorial muestra cómo tooscale fuera una aplicación web ASP.NET en Azure toomaximize usuario solicita.

Antes de iniciar este tutorial, asegúrese de que [Hola CLI de Azure está instalado](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en su equipo. Además, necesitará [Visual Studio](https://www.visualstudio.com/vs/) en la aplicación de ejemplo de Hola de toorun de equipo local.

## <a name="step-1---get-sample-application"></a>Paso 1: Obtención de la aplicación de ejemplo
En este paso, configurar un proyecto ASP.NET local Hola.

### <a name="clone-hello-application-repository"></a>Repositorio de aplicación Hola de clon

Terminal de línea de comandos de hello abierto de su elección y `CD` tooa directorio de trabajo. A continuación, siguiente ejecución Hola comandos tooclone aplicación de ejemplo de Hola. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Ejecutar la aplicación de ejemplo de Hola en Visual Studio

Abra la solución de hello en Visual Studio.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Tipo de `F5` aplicación de hello toorun.

Esta aplicación web ASP.NET de ejemplo proviene de la plantilla predeterminada de Hola y continúa usuario sesiones y se utiliza Hola memoria caché de resultados. Eche un vistazo a `HighScaleApp\Controllers\HomeController.cs`. Hola `Index()` método agrega una parte de la sesión de toohello de datos.

```csharp
Session.Add("visited", "true"); 
```

Hello y `About()` y `Contact()` métodos caché su resultado.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>Paso 2: implementar tooAzure
En este paso, creará una aplicación web de Azure e implementar su tooit de aplicación de ASP.NET de ejemplo.

### <a name="create-a-resource-group"></a>Crear un grupo de recursos   
Use [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) toocreate una [grupo de recursos](../azure-resource-manager/resource-group-overview.md) en la región de Europa occidental Hola. Un grupo de recursos es donde se colocan todas las Hola recursos de Azure que desea toomanage juntos, como aplicación web de hello y cualquier base de datos SQL back-end.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee los posibles valores pueden usar para `---location`, usar hello [az de servicio de aplicaciones enumerar ubicaciones](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) comando.

### <a name="create-an-app-service-plan"></a>Creación de un plan de App Service
Use [Crear plan de servicio de aplicaciones az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate un "B1" [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Un plan de servicio de aplicaciones es una unidad de escala, que puede incluir cualquier número de aplicaciones que desee tooscale seguridad o out over junto Hola misma infraestructura de servicio de aplicaciones. A cada plan se le asigna también un [plan de tarifa](https://azure.microsoft.com/en-us/pricing/details/app-service/). Los niveles superiores incluyen mejor hardware y más características, por ejemplo, más instancias de escalado horizontal.

Para este tutorial, B1 es el nivel mínimo de Hola que permite escalar horizontalmente toothree instancias. La aplicación siempre puede mover hacia arriba o abajo Hola tarifa más adelante mediante la ejecución de [actualización de plan de servicio de aplicaciones de az](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Creación de una aplicación web
Use [crear web de servicio de aplicaciones az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate una aplicación web con un nombre único en `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Configurar credenciales de implementación
Use [conjunto de usuarios de implementación de web de servicio de aplicaciones de az](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset las credenciales de la implementación de nivel de la cuenta de servicio de aplicaciones.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Configuración de la implementación de Git
Use [control de código fuente de web de servicio de aplicaciones en az config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure implementación de Git local.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Este comando proporciona una salida similar Hola siguiente:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Hola de uso devuelve URL tooconfigure la Git remoto. Hello siguiente comando usa Hola anterior ejemplo de salida.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Implementar la aplicación de ejemplo de Hola
Se está ahora listo toodeploy la aplicación de ejemplo. Ejecute `git push`.

```powershell
git push azure master
```

Cuando se le solicite una contraseña, use la contraseña de Hola que especificó cuando ejecutó `az appservice web deployment user set`.

### <a name="browse-tooazure-web-app"></a>Examinar la aplicación web de tooAzure
Use [explorar el servicio de aplicaciones web az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee la aplicación que se ejecutan en Azure, ejecute este comando.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>Paso 3: conectar tooRedis
En este paso, configurar caché en Redis de Azure como una aplicación web de Azure de tooyour de memoria caché externo y colocados. Puede usar rápidamente Redis toocache el resultado de la página. Además, al escalar horizontalmente las aplicaciones web más adelante, Redis le ayuda a conservar las sesiones de usuario entre varias instancias de forma confiable.

### <a name="create-an-azure-redis-cache"></a>Creación de una instancia de Caché en Redis de Azure
Use [crear redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate almacenar en caché un Redis de Azure y guardar Hola de salida JSON. Use un nombre único en `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Configurar toouse de aplicación Hola Redis
Cadena de conexión de Hola de formato de la memoria caché.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

segunda línea de Hello debe darle una salida similar a esto:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

En Visual Studio, cree un archivo de configuración web en la raíz del proyecto denominado `redis.config` y pegar Hola siguiente código en él. En `value`, usar cadena de conexión de Hola de hello salida de PowerShell.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Si observa hello `.gitignore` archivo en el repositorio Git, verá que este archivo está excluido del control de código fuente. De este modo se mantiene segura la información confidencial. 

Abra `Web.config`. Hola aviso `<appSettings file="redis.config">` elemento, que obtiene la configuración de Hola que creó en `redis.config`. 

Buscar comentarios Hola sección que incluya `<sessionState>` y `<caching>`. Quite el comentario de esta sección.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Este código busca de cadena de conexión de hello Redis ha definido en `RedisConnection`. 

La aplicación ahora usa Redis toomanage sesiones y almacenamiento en caché. Tipo de `F5` aplicación de hello toorun. Si lo desea, puede descargar una Redis administración cliente toovisualize Hola de datos que se guardan toohello caché.

### <a name="configure-hello-connection-string-in-azure"></a>Configurar la cadena de conexión de hello en Azure

Para toowork de su aplicación en Azure, necesitará tooconfigure Hola la misma cadena de conexión de Redis en la aplicación web de Azure. Puesto que `redis.config` no se mantiene en el control de código fuente, no está implementado tooAzure cuando se ejecuta la implementación de Git.

Use [actualizar az servicio de aplicaciones web configuración appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) cadena de conexión de hello tooadd con hello mismo nombre (`RedisConnection`).

az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup

Recuerde que `$connstring` contiene la cadena de conexión de hello con formato.

### <a name="redeploy-hello-application-tooazure"></a>Volver a implementar Hola aplicación tooAzure
Usar Git comandos toopush su tooAzure de cambios

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Cuando se le solicite una contraseña, use la contraseña de Hola que especificó cuando ejecutó `az appservice web deployment user set`.

### <a name="browse-toohello-azure-web-app"></a>Examinar la aplicación web de Azure de toohello
Use [explorar el servicio de aplicaciones web az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) cambios de hello toosee residen en Azure.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>Paso 4: instancias de toomultiple de escala
Hola plan de servicio de aplicaciones es la unidad de escala de Hola para las aplicaciones web de Azure. tooscale horizontalmente su aplicación web, escalar Hola plan de servicio de aplicaciones.

Use [actualización de plan de servicio de aplicaciones de az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale instancias de toothree de plan de servicio de aplicaciones de hello, que es Hola número máximo permitido por hello B1 nivel de precios. Recuerde que B1 es hello que eligió al crear Hola anteriormente el plan de servicio de aplicaciones de nivel de precios. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Paso 5: Escalado geográfico
Cuando se escala geográficamente, ejecute la aplicación en varias regiones de hello nube de Azure. Equilibra la carga de la aplicación que más se basa en la geografía de este programa de instalación y reduce el tiempo de respuesta de hello mediante la colocación de los exploradores de tooclient más de cerca de aplicación.

En este paso, escalar su ASP.NET web app tooa segunda región con [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Al final de Hola de paso de hello, tendrá una aplicación web que se ejecuta en Europa occidental (ya creado) y una aplicación web que se ejecuta en sudeste de Asia (aún no se ha creado). Ambas aplicaciones se servirá de hello misma dirección URL del Administrador de tráfico.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Escalar verticalmente hello tooStandard capa de aplicación de Europa
En el servicio de aplicaciones, integración con Azure Traffic Manager requiere Hola de tarifa estándar. Use [actualización de plan de servicio de aplicaciones de az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale seguridad su tooS1 del plan de servicio de aplicaciones. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Crear un perfil de Traffic Manager 
Use [Crear perfil de administrador de tráfico de red az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate un Traffic Manager cree un perfil y agregar grupo de recursos de tooyour. Use un nombre DNS único en $dnsName.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Especifica que este perfil [enruta el extremo más cercano de usuario tráfico toohello](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Obtener Id. de recurso de Hola de aplicación de hello Europa
Use [show de web de servicio de aplicaciones de az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Hola el Id. de recurso de la aplicación web.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Agregar un extremo de Traffic Manager para la aplicación de hello Europa
Usar [crear punto de conexión de administrador de tráfico de red de az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un perfil de Traffic Manager tooyour de punto de conexión y el Id. de recurso de Hola de uso de la aplicación web como Hola destino.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Obtener dirección URL del extremo de hello Traffic Manager
El perfil de Traffic Manager tiene ahora un punto de conexión en esa aplicación web de puntos tooyour existente. Use [mostrar de perfil de administrador de tráfico de red az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget su dirección URL. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Copiar el resultado de hello en el explorador. Debería ver la aplicación web nuevo.

### <a name="create-an-azure-redis-cache-in-asia"></a>Creación de una instancia de Azure Redis Cache en Asia
Ahora, replica su región de Sudeste de Asia de toohello de aplicación web de Azure. toostart, use [crear redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate un segundo servicio Azure Redis Cache del sudeste asiático. Esta memoria caché debe toobe colocado en su aplicación en Asia.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`Proporciona Hola nombre Hola de caché de hello caché Europa occidental, con hello `-asia` sufijo.

### <a name="create-an-app-service-plan-in-asia"></a>Creación de un plan de App Service en Asia
Use [Crear plan de servicio de aplicaciones az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate un segundo servicio de aplicación previsto en la región de hello sudeste de Asia, mediante Hola S1 mismo nivel como plan de hello Europa occidental.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Creación de una aplicación web en Asia
Use [crear web de servicio de aplicaciones az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate una segunda aplicación web.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`Proporciona Hola nombre de aplicación Hola de aplicación de hello Europa occidental, con hello `-asia` sufijo.

### <a name="configure-hello-connection-string-for-redis"></a>Configurar la cadena de conexión de Hola para Redis
Use [actualizar az servicio de aplicaciones web configuración appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web aplicación Hola cadena de conexión para hello caché sudeste de Asia.

az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>Configurar la implementación de Git para la aplicación de hello Asia.
Use [control de código fuente de web de servicio de aplicaciones en az config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure de implementación de Git local para la aplicación web de la segunda Hola.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Este comando proporciona una salida similar Hola siguiente:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Hola de uso devuelve URL tooconfigure una segunda Git remoto para el repositorio local. Hello siguiente comando usa Hola anterior ejemplo de salida.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Implementación de la aplicación de ejemplo
Ejecutar `git push` toodeploy el ejemplo aplicación toohello segundo Git control remoto. 

```bash
git push azure-asia master
```

Cuando se le solicite una contraseña, use la contraseña de Hola que especificó cuando ejecutó `az appservice web deployment user set`.

### <a name="browse-toohello-asia-app"></a>Examinar toohello Asia aplicación
Use [explorar el servicio de aplicaciones web az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify que la aplicación se ejecuta en vivo en Azure.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Obtener Id. de recurso de Hola de aplicación de hello Asia
Use [show de web de servicio de aplicaciones de az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Hola el Id. de recurso de la aplicación web en sudeste de Asia.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Agregar un extremo de Traffic Manager para la aplicación de hello Asia
Use [crear punto de conexión de administrador de tráfico de red de az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un toohello de punto de conexión segundo perfil de Traffic Manager.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>Agregar aplicaciones de tooweb de identificador de región
Use [actualizar az servicio de aplicaciones web configuración appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd una variable de entorno específicas de la región.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

El código de aplicación ya usa esta configuración de aplicación. Eche un vistazo a `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>¡Listo!

Ahora, intente tooaccess Hola URL de su perfil de Traffic Manager de exploradores en regiones geográficas diferentes. Los exploradores de cliente de Europa deben mostrar "ASP.NET Europa Occidental" y el explorador de cliente de Asia debe mostrar "ASP.NET "Sudeste Asiático".

## <a name="more-resources"></a>Más recursos
