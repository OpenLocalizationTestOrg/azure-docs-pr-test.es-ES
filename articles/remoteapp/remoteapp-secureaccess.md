---
title: aaaSecuring acceso tooAzure RemoteApp etc. | Documentos de Microsoft
description: "Obtenga información acerca de cómo proteger acceso tooAzure RemoteApp con el acceso condicional en Azure Active Directory"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>Proteger acceso tooAzure RemoteApp etc.
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

En este artículo se le ofrecerá una visión general de cómo un administrador puede establecer un canal de un acceso seguro a partir de saludo del usuario final, a través de RemoteApp de Azure y finalizando en un recurso seguro, como una base de datos SQL o de otra aplicación back-end. objetivo de Hello es toomake seguro de que sólo los usuarios autorizados Hola reunión deseado condiciones pueden tener acceso a las aplicaciones remotas, y que Hola back-end seguro solo son accesibles desde el entorno de Azure RemoteApp Hola controlada y no desde otras ubicaciones.

Hay 3 Hola, administrador necesita toolook en las áreas principales:

![Consideraciones de acceso condicional de Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Siga leyendo para obtener información y respuestas preguntas toothese.

## <a name="who-can-access-hello-collection"></a>¿Quién puede acceder a la colección de hello?
Administrador de Hello elige los usuarios de Hola que pueden tener acceso a las aplicaciones remotas en la colección de Hola. Puede usar cuentas profesionales o educativas (anteriormente denominadas "cuentas de organización") de Azure Active Directory (Azure AD) o cuentas de Microsoft (por ejemplo, @outlook.com). La mayoría de los escenarios de empresa use cuentas de Azure AD; le permiten usar características de acceso condicional que se describe más adelante y también Hola solo para las colecciones Unidos a un dominio. resto de Hola de artículo Hola supone que usa cuentas de Azure AD con Azure RemoteApp.

**¿Qué hemos logrado?**

Uso de Azure AD cuentas toocontrol acceso tooAzure que RemoteApp nos da dos cosas:

1. Siempre se sabe quién puede acceder a Hola aplicaciones se publicaron y tener acceso a cualquier back-end esas aplicaciones se conectan a.
2. Se controla Hola subyacente Azure AD, por lo que podemos crear y eliminar cuentas de usuario, conjunto de directivas de contraseña, utilizan la autenticación multifactor, etcetera. 

## <a name="how-is-hello-collection-accessed-from-where"></a>¿Cómo tiene acceso la colección de hello? ¿Desde dónde?
Normalmente los administradores deseen usar directivas de toodefine para tener acceso a un entorno de conexión a Internet público, como Azure RemoteApp. Por ejemplo, desean tooensure que los usuarios que acceden al entorno de Hola desde fuera de la red corporativa de hello tienen acceso de toogain de la autenticación multifactor (MFA) de toouse; o quizás debe bloquearse por completo.

Administradores de Azure RemoteApp pueden usar la funcionalidad de hello disponible a través de directivas de acceso condicional de Azure AD Premium tooset para su entorno de Azure RemoteApp. También pueden usar alertas toomonitor de características, ¿cómo se tiene acceso a entorno de Hola y de informes enriquecidos.

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>Cómo tooset el acceso condicional de RemoteApp de Azure
Estamos toowalk continuo a través de un escenario de ejemplo: Administrador de RemoteApp de Azure de hello desea entorno toohello de tooblock acceso cuando los usuarios están fuera de la red corporativa de Hola.

> [!NOTE]
> Suponemos que se ha actualizado toohello nivel Premium de Azure AD y que ha creado al menos una colección de RemoteApp de Azure.
> 
> 

1. En el portal de Azure, haga clic en hello **Active Directory** ficha. A continuación, haga clic en el directorio de hello desea tooconfigure.
   
   Recuerde: Acceso condicional es una propiedad de su directorio y no de RemoteApp de Azure, por lo que toda la configuración se realiza en el nivel del directorio Hola. Esto también significa que necesita toobe Hola directory administrador toomake estos cambios.
2. Haga clic en **aplicaciones**y, a continuación, haga clic en **Microsoft Azure RemoteApp** tooset el acceso condicional. Tenga en cuenta que puede configurar el acceso condicional para cada aplicación de "software como servicio" en su directorio por separado.
   ![Configuración de acceso condicional para Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. En hello **configurar** pestaña, establezca **habilitar reglas de acceso** tooON.
   ![Habilitación de reglas de acceso para Azure RemoteApp](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. Ahora puede configurar varias reglas y elegir con quién tooapply en:
   
   1. Elija **bloquear el acceso fuera del trabajo** toocompletely impedir que los usuarios tengan acceso a Azure RemoteApp fuera del entorno de red de Hola que especifique.
   2. Haga clic en las opciones de hello siguientes toodefine intervalos de direcciones IP de Hola que constituyen su "red de confianza". Se rechazarán las direcciones fuera de este intervalo.
5. Probar la configuración al ejecutar el cliente de Azure RemoteApp Hola desde una dirección IP fuera de intervalo de hello especificado. Después de haber iniciado sesión con sus credenciales de Azure AD, verá un mensaje similar al siguiente:

![Acceso denegado tooAzure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Futuras características del acceso condicional
equipo de Azure Active Directory de Hello está trabajando en las nuevas capacidades de acceso condicional. Los administradores será capaz de toocreate nuevos tipos de reglas más allá de las reglas de ubicación en función de red. Vista previa pública de la nueva funcionalidad de hello debe estar disponible pronto.

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>¿Cómo toomonitor acceso tooAzure RemoteApp
Un toouse gran función junto con el acceso condicional es la funcionalidad de informes de Azure Active Directory Premium de Hola. Puede usar informes toomonitor quién tiene acceso a su entorno y detectar cualquier actividad sospechosa.

Por ejemplo, puede ver los nombres Hola usuarios Hola que han accedido a Azure RemoteApp, cuántas veces lo logró y cuándo.

1. En el Portal de Azure, haga clic en **Active Directory**y después haga clic en el directorio.
2. Vaya toohello **informes** ficha.
3. En la lista Hola de informes, seleccione **uso de la aplicación** en **aplicaciones integradas**.
   
   Podrá ver algunas estadísticas agregadas para Azure RemoteApp. 
   ![Estadísticas de acceso de Azure RemoteApp agregadas](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Haga clic en información de tooreveal de la aplicación hello sobre usuarios que acceden a Azure RemoteApp.
   ![Uso de estadísticas de acceso para Azure RemoteApp](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Resumen
Con Azure Active Directory Premium puede configurar reglas tooAzure RemoteApp de acceso (y otro software como una aplicación de servicio disponible a través de Azure AD). Las reglas son limitada actualmente toonetwork directivas de ubicación según pero Hola futuras se extenderá tooother aspectos de la administración corporativa.

Azure AD Premium también ofrece informes y las funciones que amplían aún más control Hola Hola, Administrador de seguimiento que tiene en su entorno de Azure RemoteApp.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>¿Cómo puedo asegurarme de que mis recursos seguros solo son accesible desde mi entorno de Azure RemoteApp?
En las secciones anteriores de este artículo se centra en proteger el entorno de Azure RemoteApp toohello de acceso. Hemos logra elegir Hola quienes tienen permitidos el acceso y establecer el control de acceso a las reglas toofurther cómo pueden utilizar el servicio de Hola.

Un escenario común para las implementaciones de Azure RemoteApp es que las aplicaciones remotas de hello necesitan toocommunicate con un recurso de back-end, por ejemplo una base de datos SQL. Este recurso se hospeda de forma local (por ejemplo, en una red corporativa) o en la nube de hello (por ejemplo, en IaaS de Azure). A menudo, los administradores deseen toomake seguro de que recurso de back-end de hello solo son accesibles por las aplicaciones implementadas a través de RemoteApp de Azure y no como una aplicación ejecuta directamente en el equipo del usuario y obtener acceso a través de Internet pública. RemoteApp de Azure se ve a menudo como Hola administrado centralmente y entorno protegido y, por tanto, Hola única ruta de acceso a través del cual los usuarios deben interactuar con Hola recursos de back-end.

solución de Hello es tooplace ambos Hola entorno de Azure RemoteApp y recurso seguro de hello en Hola misma red Virtual de Azure (VNET). Si el recurso de hello está en un sitio diferente, puede establecer una conexión VPN de sitio a sitio, por ejemplo toocreate un centro de datos de Azure de hello expansión de red virtual y el entorno de hello cliente local.

Azure RemoteApp admite dos tipos de implementaciones de colección, donde puede proporcionar su propia red virtual:

* No unidos a un dominio: hello las aplicaciones tendrán "línea de visión" del programa Hola a otros recursos de red virtual de Hola. Por ejemplo, esto puede ser usado tooconnect aplicaciones tooa base de datos SQL que utilice la autenticación de SQL (las aplicaciones autenticarse usuario Hola directamente en la base de datos de hello)
* Unido a un dominio: máquinas virtuales de hello usa RemoteApp de Azure son tooa Unidos a un controlador de dominio en hello red virtual. Esto es útil cuando las aplicaciones de hello necesitan tooauthenticate en un controlador de dominio de Windows en orden tooget acceso tooa back-end de recursos.
  ![Colección unida a dominio de Azure RemoteApp](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>¿Cómo toocreate una conexión segura entre Azure y mi entorno local
Hay varias opciones de configuración para la conexión de los entornos de Azure y local. Una buena información general de las opciones de hello está disponible aquí.

Con Azure RemoteApp es necesario tooconfigure la red virtual en primer lugar y, a continuación, utilizarlo durante el proceso de creación de hello de la colección. 

## <a name="hello-complete-solution"></a>solución completa de Hola
diagrama de Hello siguiente muestra la solución completa de Hola que hemos creado un canal de proteger el acceso de saludo del usuario final, a través de RemoteApp Azure (ARA), en recursos de back-end de Hola.
![Proteger Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) en la fase 1 se Hola usuarios seleccionados y crean reglas de acceso que rigen cómo se puede tener acceso a ARA. En el siguiente ejemplo de Hola se sólo permitir el acceso para los usuarios que trabajan desde la red corporativa de Hola. Los usuarios no compatible no estarán entorno ARA de tooaccess capaz de hello en absoluto.
En la fase 2 se han expone recursos de back-end de hello sólo a través de la configuración de red virtual/VPN Hola que se controla. RemoteApp de Azure se ha colocado en hello misma red virtual. resultado final de Hello es recursos Hola solo son accesibles en los entornos, ARA Hola.

