---
title: "aaaCreate una puerta de enlace de la aplicación de Azure - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una puerta de enlace de la aplicación mediante el uso de Hola 2.0 de CLI de Azure en el Administrador de recursos"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Crear una puerta de enlace de la aplicación mediante el uso de hello 2.0 de CLI de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Plantilla de Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [CLI de Azure 1.0](application-gateway-create-gateway-cli.md)
> * [CLI de Azure 2.0](application-gateway-create-gateway-cli.md)

Application Gateway es una aplicación virtual dedicada que ofrece un controlador de entrega de aplicaciones (ADC) que se ofrece como servicio y que proporciona numerosas funcionalidades de equilibrio de carga de nivel 7 para una aplicación.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello

Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

* [Azure 1.0 de CLI](application-gateway-create-gateway-cli-nodejs.md) -nuestro CLI para modelos de implementación de administración de recursos y clásico Hola.
* [Azure 2.0 CLI](application-gateway-create-gateway-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="prerequisite-install-hello-azure-cli-20"></a>Requisito previo: Instalar Hola 2.0 de CLI de Azure

Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Si no tiene una cuenta de Azure, necesitará una. Regístrese para [obtener una prueba gratuita aquí](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Escenario

En este escenario, aprenderá cómo toocreate una puerta de enlace de aplicaciones con Hola portal de Azure.

En este escenario:

* Creará una puerta de enlace de aplicaciones media con dos instancias.
* Creará una red virtual denominada AdatumAppGatewayVNET con un bloque CIDR reservado de 10.0.0.0/16.
* Creará una subred denominada Appgatewaysubnet que usa 10.0.0.0/28 como bloque CIDR.

> [!NOTE]
> Las comprobaciones de la configuración adicional de puerta de enlace de aplicaciones de hello, incluido el estado personalizado, se configuran las direcciones de grupo back-end y reglas adicionales después de configura la puerta de enlace de aplicaciones de hello y no durante la implementación inicial.

## <a name="before-you-begin"></a>Antes de empezar

Azure Application Gateway requiere su propia subred. Al crear una red virtual, asegúrese de dejar suficiente toohave de espacio de direcciones en varias subredes. Una vez que se implementa una subred tooa de puerta de enlace de aplicaciones, las puertas de enlace de la aplicación solo adicionales pueden agregarse toohello subred.

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Abra hello **Microsoft Azure Command Prompt**e inicie sesión. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> También puede usar `az login` sin el modificador de hello para el inicio de sesión de dispositivo que requiere proporcionar un código en aka.ms/devicelogin.

Una vez que escriba Hola anterior ejemplo, se proporciona un código. Navegue toohttps://aka.ms/devicelogin en un proceso de inicio de sesión de explorador toocontinue Hola.

![cmd que muestra el inicio de sesión de dispositivos][1]

En el Explorador de hello, escriba el código de hello que ha recibido. Está página de inicio de sesión tooa redirigida.

![código de tooenter de explorador][2]

Una vez que se ha especificado el código de hello ha iniciado sesión, cierre Hola explorador toocontinue con el escenario de Hola.

![ha iniciado sesión correctamente][3]

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

Antes de crear la puerta de enlace de aplicaciones de hello, un grupo de recursos se crea la puerta de enlace de aplicaciones de toocontain Hola. siguiente Hello muestra comandos de Hola.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Crear puerta de enlace de aplicación Hola

direcciones IP de Hello usadas para hello back-end son direcciones IP de hello para el servidor back-end. Estos valores pueden ser cualquier IP privadas en la red virtual de hello, direcciones IP públicas o nombres de dominio completo para los servidores back-end. Hello en el ejemplo siguiente se crea una puerta de enlace de la aplicación tiene opciones de configuración de http, los puertos y las reglas de configuración adicionales.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

Hello en el ejemplo anterior se muestra muchas propiedades que no son necesarios durante la creación de hello de una puerta de enlace de la aplicación. Hola el ejemplo de código siguiente crea una puerta de enlace de la aplicación con información de hello necesario.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> Para obtener una lista de parámetros que se pueden proporcionar durante el siguiente comando de Hola de creación que se ejecute: `az network application-gateway create --help`.

Este ejemplo crea una puerta de enlace de aplicaciones básica con la configuración predeterminada para el agente de escucha de hello, grupo back-end, configuración de http de back-end y reglas. Puede modificar estos toosuit configuración su implementación una vez que el aprovisionamiento de hello es correcta.
Si ya tiene la aplicación web definida con el grupo de back-end de Hola Hola anteriores pasos, una vez creados, equilibrio de carga comienza.

## <a name="get-application-gateway-dns-name"></a>Obtención del nombre DNS de una puerta de enlace de aplicaciones

Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación. Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo. los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola. [Configuración de un nombre de dominio personalizado en Azure](../dns/dns-custom-domain.md). tooconfigure un alias, recuperar los detalles de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación. nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis. no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a>Eliminación de todos los recursos

toodelete todos los recursos que se crean en este artículo, Hola completa pasos:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo sondeos de estado personalizado de toocreate visitando [crear un sondeo de estado personalizados](application-gateway-create-probe-portal.md)

Obtenga información acerca de cómo tooconfigure la descarga de SSL y descifrado de SSL costoso de toman Hola desactivado los servidores web visitando [configurar la descarga de SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
