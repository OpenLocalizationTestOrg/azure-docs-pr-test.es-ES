---
title: Portal de Azure - puerta de enlace de aplicaciones de Azure - sondeo de aaaCreate personalizado | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate personalizado de sondeo para puerta de enlace de aplicaciones mediante el portal de Hola"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Crear un sondeo personalizado para puerta de enlace de aplicaciones mediante el portal de Hola

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-probe-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

En este artículo, se agregará un sondeo personalizado tooan aplicación puerta de enlace existente a través de hello portal de Azure. Sondeos personalizados son útiles para las aplicaciones que tienen una página de comprobación de mantenimiento específico o para aplicaciones que no proporcionan una respuesta correcta en la aplicación web de hello predeterminada.

## <a name="before-you-begin"></a>Antes de empezar

Si no dispone de una puerta de enlace de aplicaciones, visite [crear una puerta de enlace de la aplicación](application-gateway-create-gateway-portal.md) toocreate un toowork de puerta de enlace de aplicaciones con.

## <a name="createprobe"></a>Crear el sondeo de Hola

Los sondeos están configurados en un proceso de dos pasos a través del portal de Hola. Hola primer paso es sondeo de hello toocreate. En el segundo paso de hello, agregar configuración Hola sondeo toohello back-end http de puerta de enlace de aplicación Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com). Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free).

1. Hola portal de Azure panel Favoritos, haga clic en todos los recursos. Haga clic en puerta de enlace de aplicaciones de Hola Hola todos los módulos de recursos. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir partners.contoso.net en hello filtro por nombre... puerta de enlace de cuadro tooeasily acceso Hola aplicaciones.

1. Haga clic en **sondeos** y haga clic en hello **agregar** botón tooadd un sondeo.

  ![Agregar hoja Sondeo con la información rellena][1]

1. En hello **sondeo de estado del complemento** hoja, rellene la información de hello necesario para la sonda de Hola y cuando haya terminado haga clic en **Aceptar**.

  |**Configuración** | **Valor** | **Detalles**|
  |---|---|---|
  |**Name**|customProbe|Este valor es un sondeo de toohello nombre descriptivo que sea accesible en el portal de Hola.|
  |**Protocolo**|HTTP o HTTPS | se utiliza el protocolo de Hola Hola de sondeo de estado.|
  |**Host**|es decir, contoso.com|Este valor es el nombre de host de Hola que se usa para la sonda de Hola. Solo se puede aplicar cuando se ha configurado un entorno multisitio en Application Gateway; de lo contrario hay que usar '127.0.0.1'. Este valor es diferente del nombre de host de máquina virtual de Hola.|
  |**Ruta de acceso**|/ u otra ruta de acceso|resto de Hola de dirección url completa de hello para el sondeo personalizado Hola. Las rutas de acceso válidas comienzan por '/'. Ruta de acceso de saludo predeterminado de http://contoso.com simplemente usar '/' |
  |**Intervalo (segundos)**|30|¿Con qué frecuencia hello sondeo se ejecuta toocheck para el estado. No se recomienda tooset Hola inferior a 30 segundos.|
  |**Tiempo de espera (segundos)**|30|cantidad de Hola de sondeo de Hola de tiempo espera antes de expirar. Hola tiempo de espera intervalo necesidades toobe lo suficientemente alto como para que se puede realizar una llamada http página de estado de back-end de hello tooensure está disponible.|
  |**Umbral incorrecto**|3|Número de error toobe intentos considera incorrecto. Un umbral de 0 significa que si se produce un error en una comprobación de mantenimiento Hola back-end se determina de forma negativa inmediatamente.|

  > [!IMPORTANT]
  > nombre de host de Hello no es Hola igual que el nombre del servidor. Este valor es nombre Hola Hola virtual del host de ejecutando en servidor de aplicaciones de Hola. sondeo de Hola se envía toohttp: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>Agregar puerta de enlace de sondeo toohello

Ahora que hello sondeo se ha creado, es el tiempo tooadd se toohello puerta de enlace. Configuración de sondeo se establece en la configuración de http de back-end de Hola de puerta de enlace de aplicación Hola.

1. Haga clic en **configuración HTTP** en puerta de enlace de aplicaciones de hello, toobring una hoja de configuración de hello, haga clic en hello back-end http configuración actual aparece en la ventana hello.

  ![ventana de configuración de https][2]

1. En hello **appGatewayBackEndHttpSettings** hoja de configuración, verificación hello **sondeo personalizado de uso** casilla y elija sondeo Hola creado en hello [sondeo de hello Create](#createprobe) sección en hello **sondeo personalizado** desplegable...
Cuando haya terminado, haga clic en **guardar** y se aplican los valores de hello.

sondeo de Hello predeterminado comprueba Hola predeterminado toohello aplicación web. Ahora que se ha creado un sondeo personalizado, puerta de enlace de aplicaciones de hello usa Hola definido por la ruta de acceso personalizada toomonitor mantenimiento para servidores de back-end de Hola. En función de criterios de Hola que se definió, puerta de enlace de aplicaciones de hello comprueba Hola ruta especificada en el sondeo de Hola. Si Hola llamar toohost:Port / ruta de acceso no devuelve HTTP 200-399 estado respuesta, servidor Hola se saca de rotación tras alcanzar el umbral de estado incorrecto de Hola. Probing continúa en hello instancia incorrecto toodetermine cuando vuelve a correcto. Una vez instancia Hola se agrega el grupo de servidores de back-toohealthy, tráfico comienza flujo tooit nuevo y sondeo toohello instancia continúa en el intervalo especificado de usuario como normal.

## <a name="next-steps"></a>Pasos siguientes

toolearn tooconfigure la descarga de SSL con la puerta de enlace de aplicaciones de Azure, vea [configurar la descarga de SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

