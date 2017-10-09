---
title: aaaIntroduction tooAzure puerta de enlace de aplicaciones | Documentos de Microsoft
description: "Esta página proporciona una visión general del servicio de puerta de enlace de aplicación hello para el equilibrio de carga de capa 7, incluidos los tamaños de puerta de enlace, afinidad de la sesión y basada en la cookie, equilibrio de carga de HTTP y la descarga de SSL."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>Introducción a Application Gateway

Microsoft Azure Application Gateway es una aplicación virtual dedicada que proporciona un controlador de entrega de aplicaciones (ADC) como servicio. Ofrece diversas funcionalidades de equilibrio de carga de nivel 7 para la aplicación. Permite a los clientes productividad de granja de servidores web toooptimize mediante la descarga de CPU intensivo SSL terminación toohello aplicación puerta de enlace. También proporciona otras capacidades de enrutamiento de capa 7 incluida round-robin distribución del tráfico entrante, afinidad de sesión basado en cookies, enrutamiento basado en la ruta de acceso de direcciones URL y Hola capacidad toohost varios sitios Web detrás de una sola puerta de enlace de la aplicación. Un servidor de aplicaciones web (WAFS) también se proporciona como parte de la puerta de enlace de aplicaciones de hello WAFS SKU. Proporciona protección de aplicaciones tooweb vulnerabilidades de web y vulnerabilidades de seguridad comunes. Application Gateway puede configurarse como una puerta de enlace orientada a Internet, una puerta de enlace solo para uso interno o una combinación de las dos. 

![escenario](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>Características

Puerta de enlace de aplicaciones proporciona actualmente Hola siguientes capacidades:


* **[Servidor de aplicaciones Web](application-gateway-webapplicationfirewall-overview.md)**  -servidor de aplicaciones web hello (WAFS) en la puerta de enlace de aplicaciones de Azure protege las aplicaciones web de ataques basados en web comunes como la inyección de código SQL, ataques XSS y apropiaciones de sesión.
* **Equilibrio de carga HTTP** : Application Gateway proporciona equilibrio de carga en operaciones por turnos. El equilibrio de carga se realiza en el nivel 7 y se usa exclusivamente para el tráfico HTTP(S).
* **Afinidad de sesión basado en cookies** -característica de afinidad de sesión basado en cookies de hello es útil cuando se desea tookeep una sesión de usuario de hello mismo back-end. Mediante el uso de cookies administrado por puerta de enlace, hello puerta de enlace de aplicación es capaz de toodirect posteriores tráfico desde un toohello de sesión de usuario mismo back-end para el procesamiento. Esta característica es importante en casos donde el estado de sesión se guarda localmente en el servidor back-end de Hola para una sesión de usuario.
* **[Descarga de Secure Sockets Layer (SSL)](application-gateway-ssl-arm.md)**  -esta función toma tarea costosa hello de descifrar el tráfico HTTPS desde los servidores web. Mediante la conexión SSL en la puerta de enlace de aplicación Hola y Hola solicitud toohello servidor sin cifrar de reenvío de Hola de terminación, servidor web de hello es unburdened por descifrado.  Puerta de enlace de aplicaciones vuelve a cifra la respuesta de hello antes de Enviar atrás toohello cliente. Esta característica es útil en escenarios donde se encuentra Hola back-end en hello mismo protegidos red virtual como Hola puerta de enlace de aplicaciones en Azure.
* **[Terminar tooEnd SSL](application-gateway-backend-ssl.md)**  -admite la puerta de enlace de aplicación finalizar tooend cifrado de tráfico. Puerta de enlace de aplicación lo hace al terminar la conexión de SSL de hello en la puerta de enlace de aplicaciones de Hola. puerta de enlace de Hello, a continuación, aplica reglas de enrutamiento de hello toohello tráfico, vuelve a cifrar el paquete de saludo y reenvía Hola paquete toohello adecuado back-end basado en reglas de enrutamiento de hello definidas. Las posibles respuestas del servidor web de hello atraviesa Hola mismo proceso de usuario de toohello back-end.
* **[Enrutamiento de contenido basado en la dirección URL](application-gateway-url-route-overview.md)**  -esta característica proporciona funcionalidad de hello toouse diferentes servidores de back-end para otro tipo de tráfico. Tráfico de una carpeta de servidor web de Hola o de una CDN podría ser enrutado tooa diferentes back-end. Esta funcionalidad reduce la carga innecesaria en los servidores back-end que no suministran contenido específico.
* **[Enrutamiento de varios sitios](application-gateway-multi-site-overview.md)**  -puerta de enlace de aplicaciones permite tooconsolidate los sitios Web de too20 en una puerta de enlace de aplicación único.
* **[Compatibilidad con websocket para](application-gateway-websocket.md)**  -otra gran característica de puerta de enlace de aplicaciones es Hola compatibilidad nativa con Websocket.
* **[Supervisión de estado](application-gateway-probe-overview.md)**  -puerta de enlace de aplicaciones proporciona toomonitor para escenarios más específicos de sondeos de estado de valor predeterminado personalizado y supervisión de recursos de back-end.
* **[Directiva SSL y cifrados](application-gateway-ssl-policy-overview.md)**  : esta característica proporciona capacidad de hello versiones del protocolo SSL de toolimit Hola y Hola cifrados de conjuntos que se admiten y Hola orden en que se procesan.
* **[Solicitar redireccionamiento](application-gateway-redirect-overview.md)**  -esta característica proporciona el agente de escucha de hello capacidad tooredirect HTTP solicitudes tooan HTTPS.
* **[Compatibilidad con servidores back-end multiinquilino](application-gateway-web-app-overview.md)**: Application Gateway admite la configuración de servicios back-end multiinquilino, por ejemplo, Azure Web Apps y API Gateway, como miembros del grupo de servidores back-end. 
* **[Diagnóstico avanzado](application-gateway-diagnostics.md)**: Application Gateway proporciona registros de diagnóstico y acceso completos. Los registros de firewall están disponibles para los recursos de puerta de enlace de aplicaciones que tienen WAF habilitado.

## <a name="benefits"></a>Ventajas

Application Gateway resulta de utilidad para:

* Las aplicaciones que requieren las solicitudes de hello mismo tooreach de sesión de usuario o cliente Hola misma máquina virtual de back-end. Ejemplos de estas aplicaciones serían las aplicaciones de carro de la compra y los servidores de correo web.
* La eliminación de la sobrecarga de terminación SSL para las granjas de servidores web.
* Las aplicaciones, como una red de entrega de contenido, que requiere varias solicitudes HTTP en hello mismo toobe de conexión de TCP de larga ejecución enrutar o servidores de back-end de toodifferent con equilibrio de carga.
* Aplicaciones que permiten el tráfico de WebSocket.
* Proteger aplicaciones web frente a ataques comunes basados en web como inyección de código SQL, ataques de scripts entre sitios y secuestros de sesiones.
* Distribución lógica del tráfico en función de diferentes criterios de enrutamiento, como la ruta de acceso URL o las cabeceras de dominio.

Application Gateway está completamente administrada por Azure, es escalable y tiene una elevada disponibilidad. Cuenta con un amplio conjunto de funcionalidades de diagnóstico y registro, lo que facilita su administración. Cuando se crea una puerta de enlace de aplicaciones, se asocia un punto de conexión (una VIP pública o una IP de ILB interna) que se utiliza como dirección IP pública para el tráfico de red de entrada. El equilibrador de carga de Azure proporciona esta dirección VIP o ILB IP funciona en el nivel de transporte (TCP/UDP) de Hola y tiene todo tráfico de red que se va a puerta de enlace de aplicaciones de carga equilibrada toohello instancias de trabajo. Hola puerta de enlace de aplicaciones, a continuación, las rutas Hola tráfico HTTP/HTTPS basándose en su configuración, ya sea una máquina virtual, servicio, interno o una dirección IP externa en la nube.

Puerta de enlace de aplicaciones equilibrio de carga como un servicio administrado de Azure permite Hola de aprovisionamiento de un equilibrador de carga de capa 7 detrás de equilibrador de carga de software de Azure Hola. El Administrador de tráfico puede ser escenario de hello toocomplete usado como se muestra en hello después de imagen, donde Traffic Manager proporciona redirección y la disponibilidad del tráfico de recursos de puerta de enlace de la aplicación de toomultiple en distintas regiones, mientras la puerta de enlace de aplicaciones proporciona cruzado de equilibrio de carga de capa 7 de región. Un ejemplo de este escenario se puede encontrar en: [servicios en la nube de Azure Hola de equilibrio de carga de mediante](../traffic-manager/traffic-manager-load-balancing-azure.md)

![escenario de Traffic Manager y Application Gateway](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>Tamaños e instancias de puerta de enlace

Application Gateway actualmente se ofrece en tres tamaños: **pequeño**, **mediano** y **grande**. Tamaños pequeños de instancia están pensados para escenarios de desarrollo y pruebas.

Puede crear hasta too50 puertas de enlace de aplicaciones por suscripción, y cada puerta de enlace de la aplicación puede tener hasta too10 instancias. Cada puerta de enlace de aplicaciones puede constar de 20 agentes de escucha HTTP. Para ver una lista completa de los límites de la puerta de enlace de aplicaciones, consulte el tema sobre los [límites de servicio de Application Gateway](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits).

Hello en la tabla siguiente muestra un rendimiento promedio para cada instancia de puerta de enlace de la aplicación con la descarga SSL habilitado:

| Respuesta de la página de back-end | Pequeña | Mediano | Grande |
| --- | --- | --- | --- |
| 6K |7,5 Mbps |13 Mbps |50 Mbps |
| 100 k |35 Mbps |100 Mbps |200 Mbps |

> [!NOTE]
> Se trata de valores aproximados para un rendimiento de puerta de enlace de aplicaciones. rendimiento real de Hello depende de varios detalles del entorno, como el tamaño medio de página, ubicación de las instancias de back-end y tooserve de tiempo de procesamiento de una página. Para los números de rendimiento exactos, debe ejecutar sus propias pruebas. Estos valores solo se proporcionan para obtener instrucciones de planeamiento de capacidad.

## <a name="health-monitoring"></a>Supervisión del estado

La puerta de enlace de aplicaciones Azure automáticamente supervisa el estado de Hola de instancias de back-end de Hola a través de sondeo de estado básico o personalizado. Mediante el uso de comprobaciones de mantenimiento, asegura que solo correcto hosts responden tootraffic. Para obtener más información, consulte [Información general sobre la supervisión de estado de Application Gateway](application-gateway-probe-overview.md).

## <a name="configuring-and-managing"></a>Configuración y administración

Para su punto de conexión, Application Gateway puede tener una dirección IP pública, privada o ambas al configurarse. Application Gateway se configura dentro de una red virtual de su propia subred. subred de Hello creado o utilizar para la puerta de enlace de aplicación no puede contener otros tipos de recursos, Hola únicos recursos que se permiten en la subred de hello son otras puertas de enlace de la aplicación. toosecure los recursos de back-end, servidores de back-end de hello pueden estar dentro de una subred diferente en hello misma red virtual como puerta de enlace de aplicación Hola. Esta subred que no se necesita para las aplicaciones de back-end de Hola. Como puerta de enlace de aplicación Hola puede tener acceso a la dirección de ip de hello, puerta de enlace de aplicación es capaz de tooprovide capacidades de ADC para servidores de back-end de Hola. 

Puede crear y administrar una puerta de enlace de aplicaciones mediante las API de REST, los cmdlets de PowerShell, la CLI de Azure o [Azure Portal](https://portal.azure.com/). Para preguntas adicionales sobre la puerta de enlace de aplicaciones, visite [preguntas más frecuentes de puerta de enlace de aplicaciones](application-gateway-faq.md) tooview comunes de una lista de preguntas más frecuentes.

## <a name="pricing"></a>Precios

El precio se basa en una tarifa por instancia de puerta de enlace por hora y una tarifa de procesamiento de datos. Por hora la puerta de enlace de precios para hello WAFS SKU están diferente de cargos de SKU estándar. Esta información sobre los precios se puede encontrar en los [detalles de precios de Application Gateway](https://azure.microsoft.com/pricing/details/application-gateway/). Procesamiento de datos siguen siendo cargos Hola igual.

## <a name="faq"></a>P+F

Para consultar las preguntas más frecuentes acerca de Application Gateway, consulte [Preguntas más frecuentes sobre Application Gateway](application-gateway-faq.md).

## <a name="next-steps"></a>Pasos siguientes

Después de aprender a puerta de enlace de aplicaciones, puede [crear una puerta de enlace de la aplicación](application-gateway-create-gateway-portal.md) o puede [crear una puerta de enlace de la aplicación la descarga de SSL](application-gateway-ssl-arm.md) conexiones HTTPS de equilibrar la tooload.

toolearn cómo toocreate una puerta de enlace de la aplicación con la dirección URL de enrutamiento basado en contenido vaya demasiado[crear una puerta de enlace de la aplicación mediante el enrutamiento basado en la dirección URL](application-gateway-create-url-route-arm-ps.md) para obtener más información.

toolearn sobre algunas de Hola otra clave redes capacidades de Azure, consulte [red de Azure](../networking/networking-overview.md).
