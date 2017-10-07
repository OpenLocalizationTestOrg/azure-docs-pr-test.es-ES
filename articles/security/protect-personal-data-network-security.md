---
title: "características de seguridad de red de aaaProtect datos personales con Azure | Documentos de Microsoft"
description: "Protección de datos personales mediante las características de Azure Network Security"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a>Protección de datos personales con las características de seguridad de red: Azure Application Gateway y los grupos de seguridad de red

Este artículo proporciona información y procedimientos que le ayudarán a utilizar grupos de seguridad de red y puerta de enlace de aplicaciones de Azure tooprotect los datos personales.

Un elemento importante de privacidad seguridad multicapa estrategia tooprotect Hola de datos personales es una defensa contra los ataques de vulnerabilidad comunes, como la inyección de código SQL o scripting entre sitios. Mantener el tráfico de red no deseado fuera de su red virtual de Azure ayuda a proteger contra el riesgo potencial de datos confidenciales y proporciona Microsoft Azure toohelp de herramientas proteger los datos frente a los atacantes.

## <a name="scenario"></a>Escenario

Una empresa cruise grandes, con sede en Estados Unidos de hello, está ampliando sus itinerarios toooffer de operaciones en Hola Mediterráneo, Adriático y Mar Báltico, así como Hola británicas. En el desarrollo de los esfuerzos, ha adquirido varios más pequeños disfrutar líneas basadas en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido

la compañía Hola utiliza Microsoft Azure toostore los datos corporativos en hello en la nube y ejecutan aplicaciones en máquinas virtuales que procesan y tener acceso a estos datos. Estos datos incluyen información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito de su clientela global. También incluye información de recursos humanos tradicionales como direcciones, números de teléfono, los números de identificación fiscal y médica información acerca de los empleados de la compañía en todas las ubicaciones. línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad que incluye información personal tootrack relaciones con los clientes actuales y pasados.

Red de Hola de acceso de los empleados corporativos de oficinas remotas y la Agencia de viajes ubicado en todo el mundo de Hola Hola empresa tiene acceso a recursos de empresa de toosome y utilizar aplicaciones basadas en web hospedadas en máquinas virtuales de Azure toointeract con él.

## <a name="problem-statement"></a>Declaración del problema

empresa Hola debe proteger la privacidad de Hola de los clientes y datos personales de los empleados de los intrusos que utilizar software vulnerabilidades toorun código malintencionado que podría exponer datos personales almacenan o utilizan por aplicaciones de la compañía de hello en la nube.

## <a name="company-goal"></a>Objetivo de la empresa

Hello tooensure de objetivo de la empresa que no autorizado a las personas no puede tener acceso a aplicaciones de Hola y redes virtuales de Azure corporativas y datos que residirán allí aprovechando las vulnerabilidades más comunes. 

## <a name="solutions"></a>Soluciones

Microsoft Azure proporciona seguridad mecanismos toohelp evitar tráfico no deseado entraran en redes virtuales de Azure. Los firewalls han realizado normalmente el control del tráfico entrante y saliente. En Azure, puede usar Hola Application Gateway con hello Firewall de aplicación Web y grupos de seguridad de red (NSG), que actúan como un servidor de seguridad distribuido simple. Estas herramientas le permiten toodetect y bloquear tráfico de red no deseado.

### <a name="application-gatewayweb-application-firewall"></a>Application Gateway y firewall de aplicaciones web

Hola [Firewall de aplicación Web](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) componente (WAFS) de hello [puerta de enlace de aplicaciones de Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protege las aplicaciones web, que son cada vez más destinos de los ataques malintencionados que aprovecha conocidos comunes vulnerabilidades. Un WAF centralizado protege frente a ataques web y simplifica la administración de seguridad sin necesidad de realizar ningún cambio en las aplicaciones.

El firewall de aplicaciones web de Azure permite hacer frente a distintas categorías de ataques tales como la inyección de código SQL, el scripting entre sitios, las infracciones de protocolos HTTP, y a las anomalías, bots, rastreadores, escáneres, errores de configuración de aplicaciones habituales, denegación del servicio HTTP y a otros ataques frecuentes como la inyección de comandos, contrabando de solicitudes HTTP, división de respuestas HTTP y ataques remotos de inclusión de archivos. 

Puede crear una puerta de enlace de la aplicación con WAFS o agregar la puerta de enlace de aplicaciones existente de WAFS tooan. En ambos casos, Azure Application Gateway requiere su propia subred.

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a>Creación de una puerta de enlace de aplicaciones con WAF 

Hola toocreate una nueva puerta de enlace de aplicaciones con WAFS habilitada, después de:

1. Registro en toohello portal de Azure y en hello **favoritos** de portal de hello, haga clic en **nuevo**

2. Hola **New** hoja, haga clic en **red**.

3. Haga clic en **Application Gateway**.

4. Navegue toohello portal de Azure, **haga clic en nuevo \> red \> Application Gateway.**

   ![creación de puertas de enlace de aplicaciones](media/protect-netsec/app-gateway-01.png)

5. Hola **conceptos básicos** hoja que aparece, escriba los valores de hello de hello siguientes campos: nombre, nivel (Standard Edition o WAFS), tamaño SKU (pequeño, mediano o grande), (2 para lograr alta disponibilidad), número de instancias suscripción, grupo de recursos, y Ubicación.

6. Hola **configuración** hoja que aparece bajo **red Virtual**, haga clic en **elegir una red virtual**. Este paso abre escriba Hola elija hoja de red virtual.

7. Haga clic en **crear nuevo** tooopen hello **crear red virtual** hoja.

8. Escriba Hola siguientes valores: nombre, espacio de direcciones, subred, intervalo de direcciones de subred. Haga clic en **Aceptar**.

9. En hello **configuración** hoja bajo **configuración Frontend IP**, elija el tipo de dirección IP de Hola.

10. Haga clic en **Elegir una dirección IP pública** y, a continuación, en **Crear nueva**.

11. Acepte el valor predeterminado de Hola y haga clic en **Aceptar.**

12. En hello **configuración** hoja bajo **configuración de agente de escucha**, seleccione toouse HTTP o HTTPS en **protocolo**. toouse HTTPS, se requiere un certificado.

13. Establecer una configuración específica de hello WAFS: **estado del Firewall** (**habilitado**) y **modo Firewall** (**prevención**). Si elige **detección** como modo de hello, solo se registra el tráfico.

14. Hola de revisión **resumen** página y haga clic en **Aceptar**. Ahora puerta de enlace de aplicaciones de hello está puesto en la cola y creado.

Una vez creada la puerta de enlace de aplicaciones de hello, puede navegar tooit en el portal de Hola y continuar con la configuración de puerta de enlace de aplicación Hola.

![puerta de enlace de aplicaciones creada](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a>¿Cómo se puede agregar aplicación de WAFS tooan existente?

tooupdate un WAFS de toosupport de puerta de enlace de aplicación existentes en el modo de prevención, Hola siguientes:

1. En el portal de Azure hello **favoritos** panel, haga clic en **todos los recursos**.

2. Haga clic en Hola puerta de enlace de aplicación existente en hello **todos los recursos** hoja. 
>[!NOTE]
Nota: Si la suscripción de Hola que ha seleccionado ya tiene varios recursos en ella, puede escribir el nombre de Hola Hola filtro por nombre... zona DNS de cuadro tooeasily acceso Hola.
3. Haga clic en **firewall de aplicación Web** y actualizar la configuración de puerta de enlace de aplicación Hola: **actualizar tooWAF capa** (activada), **estado del Firewall** (habilitada),  **Modo de Firewall** (prevención). También necesita tooconfigure Hola conjunto de reglas y configurar las reglas deshabilitadas.

Para obtener más información acerca de cómo toocreate una nueva puerta de enlace de aplicaciones con WAFS y cómo tooadd WAFS tooan aplicación puerta de enlace existente, vea [crear una puerta de enlace de la aplicación con el servidor de aplicaciones web mediante el portal de Hola.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)

### <a name="network-security-groups"></a>Grupos de seguridad de red

A [grupo de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contiene una lista de reglas de seguridad que permiten o deniegan tooresources de tráfico de red conectado demasiado[redes virtuales de Azure](https://docs.microsoft.com/azure/virtual-network/) (VNet). Los NSG pueden toosubnets asociado o máquinas virtuales individuales. Cuando un NSG está asociado tooa subred, Hola reglas aplican tooall recursos toohello conectado subred. Tráfico puede restringir aún más mediante la asociación también un tooa NSG VM o NIC.

Los grupos de seguridad de red contienen cuatro propiedades: Nombre, Región, Grupo de recursos y Reglas.
>[!Note]
Aunque un NSG existe en un grupo de recursos, puede ser tooresources asociados en un grupo de recursos, como recurso de hello forma parte del programa Hola misma región de Azure como hello NSG.

Las reglas de los grupos de seguridad de red contienen nueve propiedades: Nombre, Protocolo (TCP, UDP o \*, que incluye ICMP así como UDP y TCP), Intervalo de puertos de origen, Intervalo de puertos de destino, Prefijo de dirección de origen, Prefijo de dirección de destino, Dirección (entrante o saliente), Prioridad (entre 100 y 4096) y Tipo de acceso (permitir o denegar). Todos los NSG contienen un conjunto de reglas predeterminadas que se puedan eliminar o se reemplaza por las reglas de Hola que crea.

#### <a name="how-do-i-implement-nsgs"></a>¿Cómo se implementan los grupos de seguridad de red?

Implementar los NSG requiere una planeación, y hay varias consideraciones de diseño debe tootake en cuenta. Puede tratarse de límites en número de Hola de NSG por suscripción y las reglas por NSG; Diseño de red virtual y subred, reglas especiales, el tráfico ICMP, el aislamiento de niveles con subredes, equilibradores de carga y mucho más.

Para más instrucciones sobre cómo planear e implementar grupos de seguridad de red y un escenario de implementación de ejemplo, consulte [Filtrado del tráfico de red con grupos de seguridad de red](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).

#### <a name="how-do-i-create-rules-in-an-nsg"></a>Creación de reglas en un grupo de seguridad de red

toocreate reglas en un NSG existente de entrada, Hola siguientes:

1. Haga clic en **Examinar** y, a continuación, en **Grupos de seguridad de red**.

2. En la lista de Hola de NSG, haga clic en **front-end de NSG**y, a continuación, **reglas de seguridad de entrada.**

3. Hola lista de reglas de seguridad de entrada, haga clic en **agregar.**

4. Escriba los valores de hello en hello siguientes campos: Name, prioridad, Source, protocolo, origen de intervalo, destino, destino de intervalo de puertos y acción.

nueva regla de Hello aparecerá en hello NSG después de unos segundos.

![reglas de seguridad de red](media/protect-netsec/inbound-security.png)

Para obtener más instrucciones sobre cómo crear reglas toocreate NSG en subredes y asociar un NSG a una subred de front-end y back-end, vea [crear grupos de seguridad de red mediante Hola portal de Azure.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)

## <a name="next-steps"></a>Pasos siguientes

[Azure Network Security](https://azure.microsoft.com/blog/azure-network-security/)

[Procedimientos recomendados de Azure Network Security](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[Obtención de información acerca de un grupo de seguridad de red](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[Firewall de aplicaciones web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
