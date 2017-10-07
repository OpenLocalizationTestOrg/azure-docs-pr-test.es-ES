---
title: "firewall de aplicación web de aaaConfigure: puerta de enlace de aplicaciones de Azure | Documentos de Microsoft"
description: "Este artículo proporciona instrucciones sobre cómo usar toostart web servidor de aplicaciones en una puerta de enlace de aplicación nueva o existente."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Configuración del firewall de aplicaciones web en una puerta de enlace de aplicaciones nueva o existente con la CLI de Azure

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [CLI de Azure](application-gateway-web-application-firewall-cli.md)

Obtenga información acerca de cómo toocreate un servidor de seguridad de la aplicación web habilita la puerta de enlace de aplicaciones o agregar web aplicación firewall tooan aplicación puerta de enlace existente.

servidor de aplicaciones web Hello (WAFS) en la puerta de enlace de aplicaciones de Azure protege las aplicaciones web de ataques basados en web comunes como la inyección de código SQL, ataques XSS y apropiaciones de sesión.

Azure Application Gateway es un equilibrador de carga de nivel 7. Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local. Application Gateway proporciona numerosas características del controlador de entrega de aplicaciones (ADC), entre las que se incluyen el equilibrio de carga HTTP, la afinidad de sesiones basada en cookies, la descarga SSL (Capa de sockets seguros), los sondeos personalizados sobre el estado, la compatibilidad con multisitio, y muchas más. toofind una lista completa de las características admitidas, visite: [información general de Application Gateway](application-gateway-introduction.md).

Hello siguiente artículo se muestra cómo demasiado[Agregar aplicación firewall tooan existente aplicación puerta de enlace web](#add-web-application-firewall-to-an-existing-application-gateway) y [crear una puerta de enlace de la aplicación que utiliza el servidor de aplicaciones web](#create-an-application-gateway-with-web-application-firewall).

![imagen de escenario][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>Requisito previo: Instalar Hola 2.0 de CLI de Azure

Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>Diferencias de configuración de WAF

Si ha leído [crear una puerta de enlace de aplicaciones con Azure CLI](application-gateway-create-gateway-cli.md), comprender Hola SKU configuración tooconfigure al crear una puerta de enlace de la aplicación. WAFS proporciona toodefine de opciones de configuración adicionales al configurar Hola SKU en una puerta de enlace de la aplicación. No hay ningún otro cambio que realice en la puerta de enlace de aplicaciones de hello propio.

| **Configuración** | **Detalles**
|---|---|
|**SKU** |Una puerta de enlace de aplicaciones normal sin WAF admite los tamaños **Standard\_Small**, **Standard\_Medium** y **Standard\_Large**. Con la introducción de Hola de WAFS, hay dos SKU adicionales, **WAFS\_medio** y **WAFS\_grande**. No se admite WAF en puertas de enlace de aplicaciones de pequeño tamaño.|
|**Modo** | Esta opción es modo de saludo de WAFS. Los valores permitidos son **Detección** y **Prevención**. Cuando WAF está configurado en modo de detección, todas las amenazas se almacenan en un archivo de registro. En el modo de prevención, todavía se registran eventos pero atacante Hola recibe una respuesta no autorizado 403 puerta de enlace de aplicaciones de Hola.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Agregar aplicación firewall tooan existente aplicación puerta de enlace web

Hola seguir los cambios de comando estándar de la aplicación puerta de enlace tooa WAFS aplicación habilitada puerta de enlace existente.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Este comando actualiza la puerta de enlace de aplicaciones de hello con servidor de aplicaciones web. Visite [puerta de enlace de Application Diagnostics](application-gateway-diagnostics.md) toounderstand cómo tooview registros para la puerta de enlace de la aplicación. Debido a toohello la naturaleza de seguridad de WAFS, registros necesidad toobe revisarse periódicamente postura de seguridad de hello toounderstand de las aplicaciones web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Creación de una puerta de enlace de aplicaciones con el firewall de aplicaciones web

Hola siguiente comando crea una puerta de enlace de la aplicación con el servidor de aplicaciones web.

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> Las puertas de enlace de aplicaciones creadas con la configuración del firewall de aplicación de hello web básico se configuran con CRS 3.0 para protección.

## <a name="get-application-gateway-dns-name"></a>Obtención del nombre DNS de una puerta de enlace de aplicaciones

Una vez creada la puerta de enlace de hello, Hola siguiente paso es front-end de Hola de tooconfigure para la comunicación. Cuando se utiliza una dirección IP pública, la puerta de enlace de aplicaciones requiere un nombre DNS asignado dinámicamente, que no es descriptivo. los usuarios finales de tooensure puede llegar a puerta de enlace de aplicaciones de hello, un registro CNAME puede ser usado toopoint toohello extremo público de puerta de enlace de aplicación Hola. [Configuración de un nombre de dominio personalizado en Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure un registro CNAME, recuperar los detalles de puerta de enlace de aplicaciones de Hola y su nombre IP/DNS asociado con puerta de enlace de hello PublicIPAddress elemento adjunto toohello aplicación. nombre DNS de Hello aplicación la puerta de enlace debe ser toocreate usa un registro CNAME, qué nombre DNS puntos Hola dos web aplicaciones toothis. no se recomienda el uso de Hola de registros de un puesto que puede cambiar Hola VIP en el reinicio de puerta de enlace de aplicaciones.

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo las reglas de toocustomize WAFS visitando: [Personalizar reglas de firewall de aplicación web a través de hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
