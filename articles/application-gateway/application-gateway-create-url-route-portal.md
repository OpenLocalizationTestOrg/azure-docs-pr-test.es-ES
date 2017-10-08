---
title: 'aaaCreate basada en una ruta de acceso de regla: puerta de enlace de aplicaciones de Azure: Portal de Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toocreate una regla basada en la ruta de acceso para una puerta de enlace de la aplicación mediante el uso de Hola portal"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Crear una regla basada en la ruta de acceso para una puerta de enlace de la aplicación mediante el portal de Hola

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell de Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [CLI de Azure 2.0](application-gateway-create-url-route-cli.md)

Enrutamiento basado en la ruta de acceso de direcciones URL permite tooassociate rutas basándose en la ruta de acceso de dirección URL de saludo de solicitud Http. Comprueba si hay un grupo de back-end de ruta tooa configurado para la dirección URL de hello mencionada en hello Application Gateway y envía toohello de tráfico de red de hello definido grupo back-end. Un uso común de enrutamiento basado en la dirección URL es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de diferentes tipos de contenido.

Enrutamiento basado en dirección URL, presenta una puerta de enlace de tooapplication de tipo de regla nueva. Application Gateway tiene dos tipos de reglas: básicas y basadas en la ruta de acceso. tipo de regla básica de Hola, proporciona round robin servicio back-end de Hola grupos mientras las reglas basadas en la ruta de acceso de distribución Round robin de tooround Además, también tiene modelo de ruta de acceso de dirección URL de solicitud de hello en cuenta al elegir grupo back-end adecuados de Hola.

## <a name="scenario"></a>Escenario

Hello escenario siguiente va a crear una regla basada en la ruta de acceso en una puerta de enlace de la aplicación existente.
Hello escenario se supone que ya ha seguido los pasos de hello demasiado[crear una puerta de enlace de la aplicación](application-gateway-create-gateway-portal.md).

![ruta de dirección URL][scenario]

## <a name="createrule"></a>Crear regla basada en ruta de acceso de Hola

Una regla basada en la ruta de acceso requiere su propio agente de escucha, antes de crear la regla de hello ser tooverify seguro de que tiene un agente de escucha disponible toouse.

### <a name="step-1"></a>Paso 1

Navegue toohello [portal de Azure](http://portal.azure.com) y seleccione una puerta de enlace de la aplicación existente. Haga clic en **Reglas**

![Introducción a Application Gateway][1]

### <a name="step-2"></a>Paso 2

Haga clic en **basado en la ruta de acceso** botón tooadd una nueva regla de ruta de acceso.

### <a name="step-3"></a>Paso 3

Hola **Agregar regla de ruta de acceso-based** hoja tiene dos secciones. Hola primera sección es donde se definen el agente de escucha de hello, el nombre de Hola de regla de Hola y la configuración de ruta de acceso predeterminada de Hola. configuración de ruta de acceso predeterminada de Hello es para las rutas que no entran en la ruta de hello personalizado basado en la ruta de acceso. Hola segunda sección de hello **Agregar regla de ruta de acceso-based** hoja es donde se definen reglas basadas en la ruta de acceso de Hola por sí mismos.

**Configuración básica**

* **Nombre de** -este valor es una regla de toohello nombre descriptivo que sea accesible en el portal de Hola.
* **Agente de escucha** -este valor es el agente de escucha de Hola que se usa para la regla de Hola.
* **Predeterminado grupo back-end** -esta configuración es Hola que define toobe de back-end de hello utilizado para la regla predeterminada de Hola
* **Configuración predeterminada de HTTP** -esta configuración es Hola que define toobe de configuración de hello HTTP utilizado para la regla predeterminada de Hola.

**Reglas basadas en ruta de acceso**

* **Nombre de** -este valor es una regla basada en toopath de nombre descriptivo.
* **Las rutas de acceso** -esta opción define Hola ruta Hola regla busca al reenviar tráfico
* **Grupo back-end** -esta configuración es Hola que define hello toobe de back-end usado para regla de Hola
* **Configuración de HTTP** -esta configuración es Hola que define toobe de configuración de hello HTTP utilizado para regla de Hola.

> [!IMPORTANT]
> Rutas de acceso: lista de Hola de toomatch de patrones de ruta de acceso. Cada uno de ellos debe comenzar con / hello solo lugar y un "\*" se permite es Hola final. Algunos ejemplos válidos son /xyz, /xyz* o /xyz/*.  

![Agregar hoja de regla basada en ruta de acceso con información completada][2]

Agregar una regla basada en la ruta de acceso tooan puerta de enlace de aplicaciones existente es un proceso sencillo a través del portal de Hola. Una vez creada una regla basada en la ruta de acceso, puede ser editado tooadd de reglas adicionales. 

![agregar reglas basadas en ruta de acceso adicionales][3]

Este paso configura una regla basada en la ruta de acceso. Es importante toounderstand que las solicitudes no vuelven a escribirse, como las solicitudes procedan de puerta de enlace de aplicación inspecciona solicitud hello y basic en hello url patrón envía Hola solicitud toohello adecuado back-end.

## <a name="next-steps"></a>Pasos siguientes

toolearn tooconfigure la descarga de SSL con la puerta de enlace de aplicaciones de Azure, vea [configurar la descarga de SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
