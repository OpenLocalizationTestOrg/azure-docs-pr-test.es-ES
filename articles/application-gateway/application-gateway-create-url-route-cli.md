---
title: "aaaCreate de reglas de una puerta de enlace de la aplicación mediante el enrutamiento de direcciones URL - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Esta página proporcionan instrucciones toocreate, configure una puerta de enlace de la aplicación de Azure mediante las reglas de enrutamiento de direcciones URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Creación de una puerta de enlace de aplicaciones mediante enrutamiento basado en rutas de acceso con la CLI de Azure 2.0

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-url-route-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [CLI de Azure 2.0](application-gateway-create-url-route-cli.md)

Enrutamiento basado en la ruta de acceso de direcciones URL permite tooassociate rutas basándose en la ruta de acceso de dirección URL de Hola de una solicitud Http. Comprueba si hay un grupo de back-end de ruta tooa configurado para dirección URL de hello presentado en Application Gateway hello y envía toohello de tráfico de red de hello definido grupo back-end. Un uso común de enrutamiento basado en la dirección URL es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de diferentes tipos de contenido.

Enrutamiento basado en dirección URL, presenta una puerta de enlace de tooapplication de tipo de regla nueva. Application Gateway tiene dos tipos de reglas: básicas y PathBasedRouting. Tipo de regla básica proporciona servicio round robin para hello back-end grupos al PathBasedRouting además de la distribución competitiva tooround, también tiene modelo de ruta de acceso de dirección URL de solicitud de hello en cuenta al elegir grupo back-end de Hola.

## <a name="scenario"></a>Escenario

En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com con dos grupos de servidor back-end: un grupo de servidor predeterminado y un grupo de servidores de la imagen.

Las solicitudes para http://contoso.com/image * son enruta el grupo de servidores de tooimage (imagesBackendPool), si hello no coincide con el patrón de ruta de acceso, se selecciona un grupo de servidores de forma predeterminada (appGatewayBackendPool).

![ruta de dirección URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Abra hello **Microsoft Azure Command Prompt**e inicie sesión. 

```azurecli
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

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>Agregar una regla basada en la ruta de acceso tooan aplicación puerta de enlace existente

Cree una puerta de enlace de aplicaciones con una regla de ruta definida.

### <a name="create-a-new-back-end-pool"></a>Creación de un nuevo grupo de back-end

Configuración de puerta de enlace de aplicaciones **imagesBackendPool** para tráfico con equilibrio de carga de red de hello en grupo back-end de Hola. En este ejemplo, configurará la configuración de otro grupo back-end para nuevos grupos de back-end de Hola. Cada grupo de back-end puede tener su propia configuración de grupo de back-end.  Configuración de HTTP de back-end se usa por miembros del grupo de reglas tooroute tráfico toohello correcta back-end. Esto determina el protocolo de Hola y el puerto que se usa al enviar tráfico toohello los miembros del grupo back-end. Configuración de HTTP de back-end de hello también dependen de las sesiones basado en cookies.  Si está habilitada, la afinidad de sesión basado en cookies envía tráfico toohello mismo back-end como solicitudes anteriores para cada paquete.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Creación de un nuevo puerto de front-end

Configurar puerto front-end de Hola para una puerta de enlace de la aplicación. objeto de configuración de puerto front-end de Hello utiliza un agente de escucha toodefine qué puerto de escucha de puerta de enlace de aplicación hello para el tráfico en el agente de escucha de Hola.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Creación de un nuevo agente de escucha

Configurar el agente de escucha de Hola. Este paso configura el agente de escucha de hello para la dirección IP pública hello y utiliza el puerto tooreceive tráfico de red entrante. Hola siguiente ejemplo toma la configuración de IP de front-end de hello configurado previamente, la configuración de puerto front-end y un protocolo (http o https) y configura el agente de escucha de Hola. En este ejemplo, el agente de escucha de hello escucha tooHTTP tráfico en el puerto 82 dirección IP pública Hola que creó anteriormente.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>Crear mapa de ruta de acceso de dirección Url de Hola

Configurar rutas de acceso de regla de dirección URL para grupos de back-end de Hola. Este paso configura Hola ruta de acceso relativa utilizado por asignación para hello toodefine aplicación puerta de enlace entre la ruta de acceso de dirección URL y qué grupo back-end se asigna el tráfico entrante toohandle Hola.

> [!IMPORTANT]
> Cada ruta de acceso debe comenzar con / hello solo lugar y un "\*" está permitida, está al final de Hola. Algunos ejemplos válidos son /xyz, /xyz* o /xyz/*. Hello cadena fed buscador de coincidencias de ruta de acceso de toohello no incluye cualquier texto después de hello primero "?" o "#" y los caracteres no se permiten. 

Hello en el ejemplo siguiente se crea una regla de "/ imágenes / *" ruta de acceso de enrutamiento de tráfico tooback-end "imagesBackendPool." Esta regla garantiza que el tráfico para cada conjunto de direcciones URL es toohello enrutado back-end. Por ejemplo, va demasiado http://adatum.com/images/figure1.jpg "imagesBackendPool." Si la ruta de acceso de hello no coincide con ninguna de las reglas de ruta de acceso definida previamente hello, configuración del mapa de ruta de acceso de regla de hello también configura un grupo de direcciones de back-end de manera predeterminada. Por ejemplo, http://adatum.com/shoppingcart/test.html va toopool1 tal y como se define como grupo predeterminado de hello para el tráfico no coincidente.

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a>Pasos siguientes

Si desea toolearn sobre la descarga de capa de Sockets seguros (SSL), consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
