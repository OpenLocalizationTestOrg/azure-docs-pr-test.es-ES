---
title: "aaaCreate una puerta de enlace de la aplicación de Azure - 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una puerta de enlace de la aplicación mediante el uso de Hola 1.0 de CLI de Azure en el Administrador de recursos"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Crear una puerta de enlace de la aplicación mediante el uso de hello CLI de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Plantilla de Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [CLI de Azure 1.0](application-gateway-create-gateway-cli.md)
> * [CLI de Azure 2.0](application-gateway-create-gateway-cli.md)
> 
> 

Azure Application Gateway es un equilibrador de carga de nivel 7. Proporciona conmutación por error, enrutamiento de rendimiento de las solicitudes HTTP entre diferentes servidores, independientemente de si están en la nube de Hola o de forma local. Puerta de enlace de aplicaciones tiene Hola siguientes características de entrega de aplicación: cargar los sondeos de personalizada del estado de equilibrio, afinidad de sesión basado en cookies y descarga de capa de Sockets seguros (SSL), HTTP y la compatibilidad de varios sitios.

## <a name="prerequisite-install-hello-azure-cli"></a>Requisito previo: Instalar Hola CLI de Azure

Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](../xplat-cli-install.md) y necesita demasiado[tooAzure de inicio de sesión](../xplat-cli-connect.md). 

> [!NOTE]
> Si no tiene una cuenta de Azure, necesitará una. Regístrese para [obtener una prueba gratuita aquí](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Escenario

En este escenario, aprenderá cómo toocreate una puerta de enlace de aplicaciones con Hola portal de Azure.

En este escenario:

* Creará una puerta de enlace de aplicaciones media con dos instancias.
* Creará una red virtual denominada ContosoVNET con un bloque CIDR reservado de 10.0.0.0/16.
* Creará una subred denominada subnet01 que usa 10.0.0.0/28 como bloque CIDR.

> [!NOTE]
> Las comprobaciones de la configuración adicional de puerta de enlace de aplicaciones de hello, incluido el estado personalizado, se configuran las direcciones de grupo back-end y reglas adicionales después de configura la puerta de enlace de aplicaciones de hello y no durante la implementación inicial.

## <a name="before-you-begin"></a>Antes de empezar

Azure Application Gateway requiere su propia subred. Al crear una red virtual, asegúrese de dejar suficiente toohave de espacio de direcciones en varias subredes. Una vez que se implementa una subred tooa de puerta de enlace de aplicaciones, las puertas de enlace de aplicaciones únicas opciones adicionales son toobe puede agregar subred toohello.

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Abra hello **Microsoft Azure Command Prompt**e inicie sesión. 

```azurecli-interactive
azure login
```

Una vez que escriba Hola anterior ejemplo, se proporciona un código. Navegue toohttps://aka.ms/devicelogin en un proceso de inicio de sesión de explorador toocontinue Hola.

![cmd que muestra el inicio de sesión de dispositivos][1]

En el Explorador de hello, escriba el código de hello que ha recibido. Está página de inicio de sesión tooa redirigida.

![código de tooenter de explorador][2]

Una vez que se ha especificado el código de hello ha iniciado sesión, cierre Hola explorador toocontinue con el escenario de Hola.

![ha iniciado sesión correctamente][3]

## <a name="switch-tooresource-manager-mode"></a>Cambiar tooResource modo de administrador

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

Antes de crear la puerta de enlace de aplicaciones de hello, un grupo de recursos se crea la puerta de enlace de aplicaciones de toocontain Hola. siguiente Hello muestra comandos de Hola.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Crear una red virtual

Una vez creado el grupo de recursos de hello, se crea una red virtual de puerta de enlace de aplicación Hola.  En el siguiente ejemplo de Hola, espacio de direcciones de hello era tan 10.0.0.0/16 tal como se define en hello anterior notas de escenario.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Creación de una subred

Después de crea la red virtual de hello, se agrega una subred de puerta de enlace de aplicación Hola.  Si tiene previsto toouse la puerta de enlace de aplicaciones con una aplicación web hospedado en hello mismo virtual de red como puerta de enlace de aplicación Hola, tooleave seguro espacio suficiente para otra subred.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Crear puerta de enlace de aplicación Hola

Una vez que se crean, subred y red virtual de hello requisitos previos de hello para la puerta de enlace de aplicaciones de hello están completos. Además, un archivo .pfx exportado anteriormente hello y certificado contraseña Hola certificado son necesarios para hello siguiendo el paso: direcciones IP de hello utilizadas para hello back-end son direcciones IP de hello para el servidor back-end. Estos valores pueden ser cualquier IP privadas en la red virtual de hello, direcciones IP públicas o nombres de dominio completo para los servidores back-end.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Para obtener una lista de parámetros que se pueden proporcionar durante la creación de ejecutar el siguiente comando de hello: **crear aplicación-puerta de enlace de red de azure--ayuda**.

Este ejemplo crea una puerta de enlace de aplicaciones básica con la configuración predeterminada para el agente de escucha de hello, grupo back-end, configuración de http de back-end y reglas. Puede modificar estos toosuit configuración su implementación una vez que el aprovisionamiento de hello es correcta.
Si ya tiene la aplicación web definida con el grupo de back-end de Hola Hola anteriores pasos, una vez creados, equilibrio de carga comienza.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo sondeos de estado personalizado de toocreate visitando [crear un sondeo de estado personalizados](application-gateway-create-probe-portal.md)

Obtenga información acerca de cómo tooconfigure la descarga de SSL y descifrado de SSL costoso de toman Hola desactivado los servidores web visitando [configurar la descarga de SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
