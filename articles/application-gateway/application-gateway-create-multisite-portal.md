---
title: aaaHost varios sitios con la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Esta página proporciona instrucciones tooconfigure una puerta de enlace de la aplicación de Azure existente para hospedar varias aplicaciones web en hello misma puerta de enlace con hello portal de Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>Configuración de una puerta de enlace de aplicaciones existente para hospedar varias aplicaciones web

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-create-multisite-portal.md)
> * [PowerShell del Administrador de recursos de Azure](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

Alojamiento de varios sitios permite toodeploy más de una aplicación web en hello misma puerta de enlace de la aplicación. Se basa en la presencia del encabezado de host en la solicitud HTTP entrante hello, toodetermine qué agente de escucha reciba tráfico. agente de escucha de Hello, a continuación, dirige el grupo de back-end de tráfico tooappropriate como está configurado en la definición de las reglas de Hola de puerta de enlace de Hola. En las aplicaciones web se ha habilitado SSL, puerta de enlace de aplicaciones se basa en hello indicación de nombre de servidor (SNI) extensión toochoose Hola correcto agente de escucha para el tráfico de web Hola. Un uso común de alojamiento de varios sitios es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de dominios de web diferente. De igual forma varios subdominios de hello también se puede hospedar el dominio raíz del mismo en Hola misma puerta de enlace de la aplicación.

## <a name="scenario"></a>Escenario

En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com y fabrikam.com con dos grupos de servidor back-end: contoso grupo de servidores y el grupo de servidores de fabrikam. El programa de instalación similar podría ser subdominios toohost usado como app.contoso.com y blog.contoso.com.

![escenario multisitio][multisite]

## <a name="before-you-begin"></a>Antes de empezar

Este escenario agrega la puerta de enlace de aplicaciones existentes de compatibilidad con varios sitios tooan. toocomplete toobe disponibles tooconfigure es necesario este escenario, una puerta de enlace de la aplicación existente. Visite [crear una puerta de enlace de la aplicación mediante el portal de hello](application-gateway-create-gateway-portal.md) toolearn cómo toocreate una puerta de enlace de aplicaciones básica en el portal de Hola.

siguiente Hola es pasos de hello necesarios puerta de enlace de aplicaciones de tooupdate hello:

1. Crear grupos de back-end toouse para cada sitio.
2. Cree un agente de escucha para cada puerta de enlace de aplicaciones del sitio que lo admitirá.
3. Crear reglas toomap cada agente de escucha con hello adecuado back-end.

## <a name="requirements"></a>Requisitos

* **Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola. direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP. También puede utilizarse el FQDN.
* **Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies. Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.
* **Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola. Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.
* **Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL). En el caso de las puertas de enlace de aplicaciones con sitios múltiples habilitados, también se agregan el nombre de host y los indicadores de SNI.
* **Regla:** regla Hola enlaza el agente de escucha de hello, grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado. Las reglas se procesan en orden de hello aparecen y se dirigirá el tráfico a través de la regla primera Hola que coincida con independientemente de especificidad. Por ejemplo, si tiene una regla mediante un agente de escucha básico y una regla mediante una escucha de varios sitio ambos en hello misma regla de puerto, Hola con el agente de escucha de hello multisitio debe aparecer antes de la regla de hello con un agente de escucha básico de hello en orden para hello toofunction de regla de multisitio como se esperaba. 
* **Certificados:** cada agente de escucha requiere un certificado único, en este ejemplo se crean dos agentes de escucha para varios sitios. Dos certificados .pfx y las contraseñas de Hola para ellos deben toobe creado.

## <a name="create-back-end-pools-for-each-site"></a>Creación de grupos de back-end para cada sitio

Se necesita un grupo de back-end para cada sitio que va a admitir esa puerta de enlace de aplicaciones; en este caso se crearán dos, uno para contoso11.com y otro para fabrikam11.com.

### <a name="step-1"></a>Paso 1

Navegue tooan la puerta de enlace de aplicación existente en hello portal de Azure (https://portal.azure.com). Seleccione **Grupos de back-end** y haga clic en **Agregar**.

![adición de grupos de back-end][7]

### <a name="step-2"></a>Paso 2

Rellene la información de hello para el grupo de back-end de hello **pool1**, agregar direcciones ip de Hola o FQDN para servidores de back-end de Hola y haga clic en **Aceptar**

![configuración del grupo de back-end grupo1][8]

### <a name="step-3"></a>Paso 3

En la hoja de grupos de back-end de hello haga clic en **agregar** tooadd un grupo back-end adicional **pool2**, agregar direcciones ip de Hola o FQDN para servidores de back-end de Hola y haga clic en **Aceptar**

![configuración del grupo de back-end grupo2][9]

## <a name="create-listeners-for-each-back-end"></a>Creación de agentes de escucha para cada back-end

Puerta de enlace de aplicaciones se basa en HTTP 1.1 toohost de encabezados de host, más de un sitio Web en Hola la misma dirección IP pública y el puerto. escucha básica Hello creada en portal de hello no contiene esta propiedad.

### <a name="step-1"></a>Paso 1

Haga clic en **los agentes de escucha** Hola puerta de enlace de aplicación existente y haga clic en **multisitio** primer agente de escucha de tooadd Hola.

![hoja de información general de los agentes de escucha][1]

### <a name="step-2"></a>Paso 2

Rellene la información de hello para el agente de escucha de Hola. En este ejemplo se configura la terminación SSL y se crea un nuevo puerto de front-end. Cargar toobe de certificado .pfx Hola utilizado para la terminación SSL. Hola única diferencia en esta hoja de agente de escucha básico estándar toohello hoja en comparación con es el nombre de host de Hola.

![hoja de propiedades del agente de escucha][2]

### <a name="step-3"></a>Paso 3

Haga clic en **multisitio** y crear otro agente de escucha tal como se describe en el paso anterior de Hola para otro sitio de Hola. Asegúrese de toouse seguro de un certificado diferente para el agente de escucha de segundo de Hola. Hola única diferencia en esta hoja de agente de escucha básico estándar toohello hoja en comparación con es el nombre de host de Hola. Rellene la información de hello para el agente de escucha de Hola y haga clic en **Aceptar**.

![hoja de propiedades del agente de escucha][3]

> [!NOTE]
> La creación de agentes de escucha de hello portal de Azure para puerta de enlace de aplicaciones es una tarea de ejecución prolongada, podría tardar algunos Hola de toocreate tiempo dos agentes de escucha en este escenario. Cuando los agentes de escucha de hello completa se muestran en el portal de hello tal como se muestra en hello después de imagen:

![información general del agente de escucha][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>Crear reglas de grupos de toobackend de agentes de escucha de toomap

### <a name="step-1"></a>Paso 1

Navegue tooan la puerta de enlace de aplicación existente en hello portal de Azure (https://portal.azure.com). Seleccione **reglas** y elija la regla predeterminada existente de hello **rule1** y haga clic en **editar**.

### <a name="step-2"></a>Paso 2

Rellene la hoja de reglas de Hola tal como se muestra en hello después de la imagen. Elegir el primer agente de escucha de Hola y el primer grupo y haga clic en **guardar** cuando haya terminado.

![edición de una regla existente][6]

### <a name="step-3"></a>Paso 3

Haga clic en **reglas básicas** segunda regla de toocreate Hola. Rellene el formulario de hello con hello segundo agente de escucha y el segundo grupo back-end y haga clic en **Aceptar** toosave.

![adición de una hoja de reglas básicas][10]

Este escenario completa la configuración de una puerta de enlace de aplicaciones existentes con soporte para varios sitio a través de hello portal de Azure.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooprotect sus sitios Web con [puerta de enlace de aplicaciones - servidor de aplicaciones Web](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
