---
title: "aplicación web de dominio personalizado de aaaAdd y SSL tooan Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprepare Azure web producción toogo de aplicación mediante la adición de la marca de la empresa. Asignar Hola dominio personalizado nombre (dominio personal) tooyour web app y protéjala con un certificado SSL personalizado."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>Agregar dominio personalizado y la aplicación web de Azure de SSL tooan

Este tutorial muestra cómo tooquickly asignar una aplicación de web de Azure de tooyour de nombre de dominio personalizado y, a continuación, protegerla con un certificado SSL personalizado. 

## <a name="before-you-begin"></a>Antes de empezar

Antes de ejecutar este ejemplo, instalar hello [CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localmente.

También necesita página de configuración de acceso administrativo toohello DNS para el proveedor de dominio respectivo. Por ejemplo, tooadd `www.contoso.com`, necesita toobe tooconfigure capaz de entradas DNS para `contoso.com`.

Por último, deberá válido. Archivo PFX _y_ su contraseña de certificado SSL de Hola que desee tooupload y enlazar. Este certificado SSL debe ser el nombre de dominio personalizado de hello toosecure configurado que desee. Hola ejemplo anterior, debe proteger el certificado SSL `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Paso 1: Creación de una aplicación web de Azure

### <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Estamos ahora continuo toouse hello Azure CLI 2.0 en un recurso de ventana de terminal toocreate Hola necesarios toohost nuestra aplicación Node.js en Azure.  Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Crear un grupo de recursos   
Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create). Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran recursos de Azure como aplicaciones web, bases de datos y cuentas de almacenamiento. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee los posibles valores pueden usar para `---location`, usar hello `az appservice list-locations` comando de CLI de Azure.

## <a name="create-an-app-service-plan"></a>Creación de un plan de App Service

Crear un plan de servicio de aplicaciones con hello [Crear plan de servicio de aplicaciones az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello en el ejemplo siguiente se crea un plan de servicio de aplicaciones denominado `myAppServicePlan` con hello **básica** nivel de precios.

az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1

Cuando se ha creado el plan de servicio de aplicación Hola, Hola CLI de Azure muestra información toohello similar siguiente ejemplo. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>Creación de una aplicación web

Ahora que ha creado un plan de servicio de aplicaciones, cree una aplicación web dentro de hello `myAppServicePlan` plan de servicio de aplicaciones. proporciona de aplicación web de Hola que está un hospedaje toodeploy de espacio en el código como le proporciona una dirección URL de hello tooview implementado la aplicación. Hola de uso [crear web de servicio de aplicaciones az](/cli/azure/appservice/web#create) comando toocreate hello web app. 

En el siguiente comando de hello, sustituir por su propio nombre de aplicación único donde verá hello `<app_name>` marcador de posición. Este nombre único se utilizará como parte de Hola Hola predeterminado del nombre de dominio para la aplicación web de hello, por lo que el nombre de hello necesita toobe único en todas las aplicaciones de Azure. Más adelante puede asignar cualquier aplicación de web de toohello de entrada DNS personalizado antes de exponer tooyour a los usuarios. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Cuando se ha creado la aplicación web de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

De salida JSON, Hola `defaultHostName` muestra el nombre de dominio predeterminado de la aplicación web. En el explorador, navegue toothis dirección.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Paso 2: Configuración de la asignación de DNS

En este paso, agregará una asignación de nombre de dominio predeterminado de la aplicación web de tooyour de dominio personalizado, `<app_name>.azurewebsites.net`. Normalmente, este paso se realiza en el sitio web de su proveedor de dominios. El sitio web de cada registrador de dominios es ligeramente diferente, por lo que debe consultar la documentación de su proveedor. Sin embargo, estas son algunas directrices generales. 

### <a name="navigate-tootoodns-management-page"></a>Navegar por la página de administración de tootooDNS

En primer lugar, inicie sesión en el sitio Web del registrador de dominios tooyour.  

A continuación, Buscar página Hola para administrar registros de DNS. Busque vínculos o áreas del sitio de hello con la etiqueta **nombre de dominio**, **DNS**, o **gestión de nombre de servidor**. A menudo, puede encontrar Hola vínculo Ver información de su cuenta y, a continuación, buscando un vínculo como **Mis dominios**.

Una vez que haya encontrado esta página, busque un vínculo que le permita agregar o editar registros DNS. Podría aparecer como **Archivo de zona** o **Registros DNS**, o bien como un vínculo de **Configuración avanzada**.

### <a name="create-a-cname-record"></a>Creación de un registro CNAME

Agregar un registro CNAME que asigna el nombre de dominio de la aplicación de hello subdominio deseado nombre tooyour web predeterminado (`<app_name>.azurewebsites.net`, donde `<app_name>` es el nombre único de la aplicación).

Para hello `www.contoso.com` ejemplo, crear un CNAME que asigna hello `www` hostname demasiado`<app_name>.azurewebsites.net`.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>Paso 3: configurar el dominio personalizado de hello en la aplicación web

Cuando termine de configurar la asignación de nombre de host de hello en el sitio Web del proveedor de su dominio, le dominio personalizado de hello tooconfigure listo en la aplicación web. Hola de uso [agregar az servicio de aplicaciones web config hostname](/cli/azure/appservice/web/config/hostname#add) comando tooadd esta configuración. 

En el siguiente comando de hello, sustituya `<app_name>` con el nombre de aplicación único y < your_custom_domain > con el nombre de dominio personalizado completo hello (p. ej. `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

dominio personalizado de Hello ahora está totalmente asignado tooyour web app. En el explorador, navegue toohello nombre de dominio personalizado. Por ejemplo:

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>Paso 4: enlazar una aplicación de web de tooyour de certificado SSL personalizada

Ahora tiene una aplicación web de Azure, con nombre de dominio de Hola que desee en la barra de direcciones del explorador de Hola. Sin embargo, si navega toohello `https://<your_custom_domain>` ahora, obtendrá un error de certificado. 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Este error se produce porque la aplicación web no tiene todavía un enlace de certificado SSL que coincida con el nombre de dominio personalizado. Sin embargo, no recibirá un error si se desplaza demasiado`https://<app_name>.azurewebsites.net`. Esto es porque la aplicación, así como todas las aplicaciones de servicio de aplicaciones de Azure, está protegido con un certificado SSL para Hola Hola `*.azurewebsites.net` dominio comodín de forma predeterminada. 

En Ordenar tooaccess su aplicación web por el nombre de dominio personalizado, deberá certificado SSL de toobind hello para la aplicación web de toohello de dominio personalizado. Esto lo hará en este paso. 

### <a name="upload-hello-ssl-certificate"></a>Cargar el certificado SSL de Hola

Cargar certificado SSL de hello para la aplicación web de tooyour de dominio personalizado mediante el uso de hello [configuración ssl carga de az servicio de aplicaciones web](/cli/azure/appservice/web/config/ssl#upload) comando.

En el siguiente comando de hello, sustituya `<app_name>` con el nombre de aplicación único, `<path_to_ptx_file>` con hello tooyour de ruta de acceso. Archivo PFX, y `<password>` con la contraseña del certificado. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Cuando se carga el certificado de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

De salida JSON, Hola `thumbprint` muestra la huella digital del certificado cargado. Copie su valor para el paso siguiente de saludo.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>Enlazar la aplicación web de hello cargado SSL certificado toohello

La aplicación web tiene ahora el nombre de dominio personalizado de Hola que desee, y también tiene un certificado SSL que protege ese dominio personalizado. Hello solo lo izquierdo toodo es toobind Hola los certificados cargados toohello web app. Hacer esto mediante el uso de hello [el enlace de ssl de az servicio de aplicaciones web config](/cli/azure/appservice/web/config/ssl#bind) comando.

En el siguiente comando de hello, sustituya `<app_name>` con el nombre de aplicación único y `<thumbprint-from-previous-output>` con la huella digital de certificado de Hola que obtiene del comando anterior Hola. 

az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI

Una vez certificado hello tooyour enlazado web app, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:

{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }

En el explorador, navegue extremo tooHTTPS de nombre de dominio personalizado. Por ejemplo:

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Más recursos

[Comprar y configurar un nombre de dominio personalizado en Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Compra y configuración de un certificado SSL para Azure App Service](web-sites-purchase-ssl-web-site.md)
