---
title: "aaaOverview de lógica de conectores de aplicaciones | Documentos de Microsoft"
description: "Información general sobre los conectores que pueden utilizarse en una aplicación lógica"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>Uso de conectores en una aplicación lógica
Los conectores proporcionan acceso rápido tooevents, los datos y las acciones a través de servicios, protocolos y plataformas.  lista completa de Hola de conectores que admite la lógica de aplicaciones puede [encontrarse aquí](apis-list.md).  Conectores puede usarse como un desencadenador o una acción en una aplicación de la lógica y pueden requerir un objeto configurado *conexión* toouse (por ejemplo: autorizar un Twitter cuenta tooaccess o publicar en su nombre).

## <a name="basics"></a>Aspectos básicos
Los conectores son los servicios hospedados que puede tener acceso como parte de una toointegrate de aplicación lógica con otros servicios como Dynamics, Azure, Salesforce, [y más](apis-list.md).  Microsoft se encarga de implementarlos y administrarlos, de modo que usted puede crear sus flujos de trabajo de integración sin preocuparse del escalado, el rendimiento y la seguridad.  Puede agregar una aplicación de lógica de conector tooa, buscar y seleccione una acción de conector o desencadenador en **API administradas de Microsoft mostrar**.

![Menú de acción para seleccionar un desencadenador][1]

Cada acción de conector o desencadenador tendrá su conjunto de propiedades tooconfigure.  Puede hacer clic en hello información botones toolearn más información acerca de la acción o su documentación de referencia [toolearn más](apis-list.md).

Si desea toointegrate con un servicio o API que no es aún un conector, también puede extender las aplicaciones lógicas a través de un [conector personalizado](../logic-apps/logic-apps-create-api-app.md) o simplemente llamar directamente a toohello servicio a través de un protocolo como HTTP.

## <a name="triggers"></a>Desencadenadores
Algunos conectores tienen un desencadenador, lo que significa un evento desde dicho conector desencadenará una aplicación lógica y pasar los datos como parte del desencadenador de Hola.  Un desencadenador siempre es Hola primer paso en una aplicación de lógica.  Algunos desencadenadores comunes son operaciones, como:

* Periodicidad: se ejecuta cada hora
* Cuando se recibe una solicitud HTTP
* Cuando se agrega un elemento tooa cola
* Cuando se recibe un correo electrónico

Algunos de los desencadenadores activarán Hola instantánea produce un evento a través de una aplicación de lógica de notificación toohello y otros tendrá un intervalo de periodicidad configurado en la frecuencia con hello aplicación lógica comprobará servicio Hola para un evento (arriba tooevery 15 segundos).  

Una vez que se recibe un evento, se activará la aplicación de la lógica de hello ejecutar y acciones de hello en el flujo de trabajo de Hola se iniciará.  También será capaz de tooaccess cualquier dato de hello desencadenar a lo largo de flujo de trabajo de hello (para hello de ejemplo 'en un tweet nueva' desencadenador pasará tweet hello en hello ejecutar).

## <a name="actions"></a>Acciones
Mayoría de los conectores tiene una o varias acciones que se pueden ejecutar como parte del flujo de trabajo de Hola.  Las acciones son los pasos que se producen después de ejecutar Hola ha activado desde un desencadenador.  tooadd una acción, haga clic en hello **nuevo paso** botón y busque Hola conector que desee toouse.  Una vez seleccionado (y después de configurar cualquiera [conexiones](#connections) que pueden requerir), verá la tarjeta de acción de hello puede configurar.  Puede seleccionar datos de los pasos anteriores, haga clic en cualquiera de los tokens de Hola para salidas, o escriba en cualquier otra configuración según sea necesario.

![Configuración de una acción de conector][2]

## <a name="connections"></a>Conexiones
La mayoría de los conectores requiere tooconfigure una *conexión* para poder usar el conector de Hola.  A *conexión* es cualquier inicio de sesión o configuración de conexión requiere conector de hello tooaccess.  Para los conectores que usar OAuth, cree una conexión significa que iniciar sesión en el servicio de hello (como Office 365, Salesforce o GitHub) donde el token de acceso puede cifrarse y almacenan de forma segura en un almacén de secreto de Azure.  Otros conectores (por ejemplo, FTP y SQL) necesitan una conexión con una determinada configuración; por ejemplo, la dirección del servidor, el nombre de usuario y la contraseña.  Estos detalles sobre la configuración de la conexión también se cifran y se almacenan de forma segura.  Las conexiones serán tooaccess capaz de servicio de Hola para siempre y cuando el servicio Hola permite.  Para las conexiones de OAuth de Azure Active Directory (como Office 365 y Dynamics) que podamos seguir token de acceso de hello toorefresh indefinidamente.  Otros servicios pueden imponer restricciones en el tiempo durante el que puede utilizarse un token sin actualizarlo.  Por lo general, algunas acciones, como los cambios de contraseña, invalidarán todos los tokens de acceso.  

Para ver y administrar las conexiones en Azure, haga clic en **Examinar** y seleccione **Conexiones de API**.  De hello recursos de conexiones de API puede ver, editar, actualizar o volver a autorizar las conexiones que ha creado.

## <a name="next-steps"></a>Pasos siguientes
* [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md)
* [Ejemplos de aplicaciones lógicas y escenarios comunes](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Información general sobre Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
