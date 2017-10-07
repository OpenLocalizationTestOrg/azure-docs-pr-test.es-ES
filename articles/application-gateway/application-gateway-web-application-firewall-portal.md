---
title: "aaaCreate o actualizar una puerta de enlace de la aplicación de Azure con firewall de aplicación web | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una puerta de enlace de la aplicación con el servidor de aplicaciones web mediante el uso de Hola portal"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Crear una puerta de enlace de la aplicación con el servidor de aplicaciones web mediante el portal de Hola

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [CLI de Azure](application-gateway-web-application-firewall-cli.md)

Obtenga información acerca de cómo toocreate un servidor de seguridad de la aplicación web habilita la puerta de enlace de aplicaciones.

servidor de aplicaciones web Hello (WAFS) en la puerta de enlace de aplicaciones de Azure protege las aplicaciones web de ataques basados en web comunes como la inyección de código SQL, ataques XSS y apropiaciones de sesión. Aplicación Web protege contra muchos de hello OWASP top 10 web las vulnerabilidades más comunes.

## <a name="scenarios"></a>Escenarios

En este artículo, hay dos escenarios:

En el primer escenario hello, aprenderá demasiado[crear una puerta de enlace de la aplicación con el servidor de aplicaciones web](#create-an-application-gateway-with-web-application-firewall)

En el segundo escenario hello, aprenderá demasiado[Agregar aplicación firewall tooan existente aplicación puerta de enlace web](#add-web-application-firewall-to-an-existing-application-gateway).

![Escenario de ejemplo][scenario]

> [!NOTE]
> Las comprobaciones de la configuración adicional de puerta de enlace de aplicaciones de hello, incluido el estado personalizado, se configuran las direcciones de grupo back-end y reglas adicionales después de configura la puerta de enlace de aplicaciones de hello y no durante la implementación inicial.

## <a name="before-you-begin"></a>Antes de empezar

Azure Application Gateway requiere su propia subred. Al crear una red virtual, asegúrese de dejar suficiente toohave de espacio de direcciones en varias subredes. Una vez que se implementa una subred tooa de puerta de enlace de aplicaciones, las puertas de enlace de aplicaciones únicas opciones adicionales son toobe puede agregar subred toohello.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Agregar aplicación firewall tooan existente aplicación puerta de enlace web

En este ejemplo se actualiza una aplicación puerta de enlace toosupport web aplicación firewall existente en el modo de prevención.

1. En el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**. Haga clic en Hola puerta de enlace de aplicación existente en hello **todos los recursos** hoja. Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir nombre de Hola Hola **filtrar por nombre...** zona DNS de cuadro tooeasily acceso Hola.

   ![Creación de una puerta de enlace de aplicaciones][1]

1. Haga clic en **firewall de aplicación Web** y actualizar la configuración de puerta de enlace de aplicación Hola. Cuando haya terminado, haga clic en **Guardar**

    Hola configuración tooupdate un servidor de aplicaciones web existentes del toosupport de puerta de enlace aplicación son:

   | **Configuración** | **Valor** | **Detalles**
   |---|---|---|
   |**Actualizar tooWAF capa**| Activado | Esto establece el nivel de Hola Hola puerta de enlace toohello WAFS del nivel de aplicación.|
   |**Estado de Firewall**| habilitado | Esta configuración habilita el firewall de hello en hello WAFS.|
   |**Modo de firewall** | Prevención | Esta configuración hace referencia a cómo el firewall de aplicaciones web se ocupa del tráfico malintencionado. **Detección de** modo sólo registra los eventos de hello, donde **prevención** modo registra eventos de Hola y se detiene Hola tráfico malintencionado.|
   |**Conjunto de reglas**|3.0|Esta configuración determina hello [principales del conjunto de reglas](application-gateway-web-application-firewall-overview.md#core-rule-sets) que es usado tooprotect Hola back-end los miembros del grupo.|
   |**Configurar reglas deshabilitadas**|Varía|tooprevent posibles falsos positivos, esta configuración le permite toodisable determinados [y grupos de reglas](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Cuando se actualiza una existente toohello de puerta de enlace de aplicaciones WAFS SKU, Hola SKU tamaño cambios demasiado**medio**. Este cambio se puede reconfigurar una vez finalizada la configuración.

    ![hoja que muestra configuración básica][2-1]

    > [!NOTE]
    > registros de firewall en la aplicación web de tooview, diagnósticos deben estar habilitados y ApplicationGatewayFirewallLog seleccionado. Para las pruebas se puede elegir 1 en Número de instancias. Es importante tooknow que cualquier instancia de recuento de instancias en dos no está cubierto por hello SLA y, por tanto, se recomienda que no. Las puertas de enlace pequeñas no están disponibles cuando se usa el firewall de aplicaciones web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>crear una puerta de enlace de aplicaciones con el firewall de aplicaciones web

En este escenario:

* Creará una puerta de enlace de aplicaciones de firewall de aplicaciones web con dos instancias.
* Creará una red virtual denominada AdatumAppGatewayVNET con un bloque CIDR reservado de 10.0.0.0/16.
* Creará una subred denominada Appgatewaysubnet que usa 10.0.0.0/28 como bloque CIDR.
* Configurará un certificado para la descarga SSL.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com). Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free).
1. En panel de favoritos de Hola de portal de hello, haga clic en **nuevo**
1. Hola **New** hoja, haga clic en **red**. Hola **red** hoja, haga clic en **Application Gateway**, tal y como se muestra en hello después de imagen:
1. Navegue toohello portal de Azure, haga clic en **New** > **red** > **puerta de enlace de aplicaciones**

    ![Creación de una puerta de enlace de aplicaciones][1]

1. Hola **Fundamentos** hoja que aparece, escriba Hola después de valores, a continuación, haga clic en **Aceptar**:

   | **Configuración** | **Valor** | **Detalles**
   |---|---|---|
   |**Name**|AdatumAppGateway|nombre de Hola de puerta de enlace de aplicación Hola|
   |**Nivel**|WAF|Los valores disponibles son Estándar y WAF. Visite [firewall de aplicación web](application-gateway-web-application-firewall-overview.md) toolearn más información sobre WAFS.|
   |**Tamaño de la SKU**|Mediano|Las opciones al elegir el nivel Estándar son pequeño, mediano y grande. Al elegir el nivel de WAF, las opciones solo son mediano y grande.|
   |**Recuento de instancias**|2|Número de instancias de puerta de enlace de aplicaciones de Hola para lograr alta disponibilidad. Los recuentos de instancias de 1 solo deben usarse para fines de pruebas.|
   |**Suscripción**|[Su suscripción]|Seleccione una puerta de enlace de suscripción toocreate Hola aplicación en.|
   |**Grupos de recursos**|**Crear nuevo:** AdatumAppGatewayRG|Cree un grupo de recursos. nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado. más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) artículo de información general.|
   |**Ubicación**|Oeste de EE. UU.||

   ![hoja que muestra configuración básica][2-2]

1. Hola **configuración** hoja que aparece bajo **red Virtual**, haga clic en **elegir una red virtual**. Este paso abre escriba hello **red virtual de elegir** hoja.  Haga clic en **crear nuevo** tooopen hello **crear red virtual** hoja.

   ![Elegir una red virtual][2]

1. En hello **Crear hoja de red virtual** escriba Hola después de valores, a continuación, haga clic en **Aceptar**. Este paso cierra hello **crear red virtual** y **red virtual de elegir** hojas. Este modo rellenará hello **subred** campo hello **configuración** hoja con subred Hola elegido.

   |**Configuración** | **Valor** | **Detalles** |
   |---|---|---|
   |**Name**|AdatumAppGatewayVNET|Nombre de puerta de enlace de aplicación Hola|
   |**Espacio de direcciones**|10.0.0.0/16| Este valor es el espacio de direcciones de hello para la red virtual de Hola|
   |**Nombre de subred**|AppGatewaySubnet|Nombre de subred de Hola para puerta de enlace de aplicación Hola|
   |**Intervalo de direcciones de subred**|10.0.0.0/28 | Esta subred permite más subredes adicionales en la red virtual de Hola para los miembros del grupo back-end|

1. En hello **configuración** hoja bajo **configuración Frontend IP**, elija **público** como hello **tipo de dirección IP**

1. En hello **configuración** hoja bajo **dirección IP pública**, haga clic en **elegir una dirección IP pública**, este paso abre hello **Elegir dirección IP pública**hoja, haga clic en **crear nuevo**.

   ![Elegir una dirección IP pública][3]

1. En hello **Crear dirección IP pública** hoja, acepte el valor predeterminado de Hola y haga clic en **Aceptar**. Este paso cierra hello **Elegir dirección IP pública** hoja, hello **Crear dirección IP pública** hoja y rellenar **dirección IP pública** con la dirección IP pública Hola elegida.

1. En hello **configuración** hoja bajo **configuración de agente de escucha**, haga clic en **HTTP** en **protocolo**. toouse **https**, se requiere un certificado. clave privada de Hello del certificado de hello es necesaria para que una exportación .pfx del certificado de hello necesita toobe proporcionado y Hola contraseña para el archivo hello.

1. Configurar hello **WAFS** unos valores específicos.

   |**Configuración** | **Valor** | **Detalles** |
   |---|---|---|
   |**Estado de Firewall**| habilitado| Esta opción activa o desactiva WAF.|
   |**Modo de firewall** | Prevención| Esta configuración determina las acciones de hello que WAFS toma en tráfico malintencionado. Si se elige **Detección** , solo se registra el tráfico.  Si se elige **Prevención** , el tráfico se registra y se detiene con una respuesta de error 403 no autorizado.|


1. Revise la página Resumen de Hola y haga clic en **Aceptar**.  Ahora puerta de enlace de aplicaciones de hello está puesto en la cola y creado.

1. Una vez creada la puerta de enlace de aplicaciones de hello, navegue tooit en la configuración de portal toocontinue Hola de puerta de enlace de aplicación Hola.

    ![Vista de recursos de Application Gateway][10]

Estos pasos crea una puerta de enlace de aplicaciones básica con la configuración predeterminada para el agente de escucha de hello, grupo back-end, configuración de http de back-end y reglas. Se puede modificar estos toosuit configuración la implementación cuando se realiza correctamente el aprovisionamiento de Hola

> [!NOTE]
> Las puertas de enlace de aplicaciones creadas con la configuración del firewall de aplicación de hello web básico se configuran con CRS 3.0 para protección.

## <a name="next-steps"></a>Pasos siguientes

A continuación, aprenderá cómo tooconfigure un alias de dominio personalizado para hello [dirección IP pública](../dns/dns-custom-domain.md#public-ip-address) con DNS de Azure u otro proveedor DNS.

Obtenga información acerca de cómo tooconfigure el registro de diagnóstico, eventos de hello toolog si se detecta o prevenir con servidor de aplicaciones web visitando [diagnóstico de puerta de enlace de aplicaciones](application-gateway-diagnostics.md)

Obtenga información acerca de cómo sondeos de estado personalizado de toocreate visitando [crear un sondeo de estado personalizados](application-gateway-create-probe-portal.md)

Obtenga información acerca de cómo tooconfigure la descarga de SSL y descifrado de SSL costoso de toman Hola desactivado los servidores web visitando [configurar la descarga de SSL](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
