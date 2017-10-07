---
title: 'Portal de Azure - puerta de enlace de aplicaciones de Azure: la descarga de SSL aaaConfigure | Documentos de Microsoft'
description: "Esta página proporciona toocreate de instrucciones mediante el portal de Hola la descarga de una puerta de enlace de la aplicación con SSL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>Configurar una puerta de enlace de la aplicación para la descarga SSL mediante el portal de Hola

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-ssl-portal.md)
> * [PowerShell del Administrador de recursos de Azure](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [CLI de Azure 2.0](application-gateway-ssl-cli.md)

Puerta de enlace de aplicación de Azure puede ser configurado tooterminate Hola Secure Sockets Layer (SSL) sesión en hello puerta de enlace tooavoid costoso SSL descifrado tareas toohappen en la granja de servidores de hello web. Descarga SSL también simplifica la administración de aplicación web de Hola y el programa de instalación del servidor front-end de Hola.

## <a name="scenario"></a>Escenario

Hola siguiendo escenario va a través de configuración de la descarga de SSL en una puerta de enlace de la aplicación existente. Hello escenario se supone que ya ha seguido los pasos de hello demasiado[crear una puerta de enlace de la aplicación](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Antes de empezar

descarga SSL de tooconfigure con una puerta de enlace de la aplicación, se requiere un certificado. Este certificado se carga en la puerta de enlace de aplicaciones de hello, utiliza tooencrypt y descifrar el tráfico de hello enviado a través de SSL. certificado de Hello debe toobe en formato de intercambio de información Personal (pfx). Este formato de archivo permite Hola privada toobe clave exportado que requiere Hola aplicación puerta de enlace tooperform Hola cifrado y descifrado de tráfico.

## <a name="add-an-https-listener"></a>Incorporación de un agente de escucha HTTPS

escucha HTTPS de Hello busca tráfico basándose en su configuración y ayuda a los grupos de ruta Hola tráfico toohello back-end.

### <a name="step-1"></a>Paso 1

Navegue toohello portal de Azure y seleccione una puerta de enlace de la aplicación existente

### <a name="step-2"></a>Paso 2

Haga clic en agentes de escucha y haga clic en hello Agregar botón tooadd un agente de escucha.

![hoja de información general de puerta de enlace de aplicaciones][1]

### <a name="step-3"></a>Paso 3

Rellene Hola la información necesaria para el agente de escucha de Hola y Hola .pfx certificado de carga, cuando haya terminado, haga clic en Aceptar.

**Nombre de** -este valor es un nombre descriptivo del agente de escucha de Hola.

**Configuración de IP de Frontend** -este valor es la configuración de IP de front-end de Hola que se usa para el agente de escucha de Hola.

**Puerto de front-end (nombre/puerto)** -un nombre descriptivo para el puerto de hello usado en front-end de Hola de puerta de enlace de aplicaciones de Hola y Hola puerto real se utilizan.

**Protocolo** -un toodetermine conmutador si se utiliza https o http para front-end de Hola.

**Certificado (nombre/contraseña)** : si se usa la descarga SSL, un certificado .pfx se requiere para esta configuración, al igual que un nombre y contraseña descriptivos.

![agregar hoja del agente de escucha][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>Crear una regla y asociar el agente de escucha de toohello

se ha creado el agente de escucha de Hola. Es hora toocreate un tráfico de hello toohandle de regla de agente de escucha de Hola. Las reglas definen cómo el tráfico es enrutado toohello grupos de back-end en función de varios valores de configuración, incluso si se usa la afinidad de sesión basado en cookies, protocolo, puerto y comprobaciones de mantenimiento.

### <a name="step-1"></a>Paso 1

Haga clic en hello **reglas** de puerta de enlace de aplicación Hola y, a continuación, haga clic en Agregar.

![hoja de reglas de puerta de enlace de aplicaciones][3]

### <a name="step-2"></a>Paso 2

En hello **Agregar regla básica** hoja, escriba Hola nombre descriptivo para la regla de Hola y elija el agente de escucha de hello creado en el paso anterior de Hola. Elija grupo back-end adecuados de Hola y configuración de http y haga clic en **Aceptar**

![ventana de configuración de https][4]

configuración de Hello ahora se guarda toohello puerta de enlace de aplicaciones. Hola guardar proceso para esta configuración puede tardar unos instantes antes de que se tooview disponible a través del portal de Hola o PowerShell. Puerta de enlace de aplicaciones una vez guardado Hola controla Hola cifrado y descifrado de tráfico. Se controlará todo el tráfico entre la puerta de enlace de aplicaciones de Hola y servidores de hello back-end web a través de http. Cualquier cliente de atrás toohello comunicación si inicia a través de https se devolverán a cliente toohello cifrada.

## <a name="next-steps"></a>Pasos siguientes

toolearn cómo tooconfigure personalizada del estado de sondeo con puerta de enlace de aplicaciones de Azure, consulte [crear un sondeo de estado personalizado](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
