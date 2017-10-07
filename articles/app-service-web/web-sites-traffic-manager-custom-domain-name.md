---
title: "aaaConfigure un nombre de dominio personalizado para una aplicación web en el servicio de aplicaciones de Azure que utiliza el Administrador de tráfico de equilibrio de carga."
description: "Use un nombre de dominio personalizado para un una aplicación web en el Servicio de aplicaciones de Azure que incluya el Administrador de tráfico para el equilibrio de carga."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>Configuración de un nombre de dominio personalizado para una aplicación web en Servicio de aplicaciones de Azure utilizando el Administrador de tráfico
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

En este artículo se ofrecen instrucciones generales para usar un nombre de dominio personalizado con el Servicio de aplicaciones de Azure que usa el Administrador de tráfico para el equilibrio de carga.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Descripción de los registros DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>Configuración de las aplicaciones web para el modo estándar
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Incorporación de un registro DNS para el dominio personalizado
> [!NOTE]
> Si ha adquirido el dominio a través de aplicaciones de Web del servicio de aplicación de Azure, a continuación, omita los pasos y consulte toohello paso final de [comprar dominio para las aplicaciones Web](custom-dns-web-site-buydomains-web-app.md) artículo.
> 
> 

tooassociate su dominio personalizado con una aplicación web en el servicio de aplicación de Azure, debe agregar una nueva entrada en la tabla de hello DNS para su dominio personalizado mediante el uso de herramientas proporcionadas por el registrador de dominios de Hola que adquirió su nombre de dominio de. Utilice Hola siguiendo los pasos toolocate y herramientas DNS de Hola.

1. Inicie sesión en la cuenta de tooyour en el registrador de dominios y busque una página para administrar los registros DNS. Busque los vínculos correspondientes o áreas del sitio de hello etiquetada como **nombre de dominio**, **DNS**, o **gestión de nombre de servidor**. A menudo un vínculo de página toothis puede encontrarse puede ver la información de cuenta y, a continuación, busca un vínculo como **Mis dominios**.
2. Una vez haya encontrado la página de administración de hello para el nombre de dominio, busque un vínculo que permite los registros DNS de hello tooedit. Debe aparecer como **archivo Zona**, **Registros DNS** o como un vínculo de configuración de **Opciones avanzadas**.
   
   * página de Hello probablemente tendrá unos registros ya creados, por ejemplo, una asociación de entrada '**@**'o'\*' con una página 'estacionamiento de dominio'. Es posible también que contenga registros para los subdominios más comunes, como **www**.
   * página de Hola se menciona **registros CNAME**, o proporcionar un tooselect de la lista desplegable un tipo de registro. También es posible que mencione otros registros, como los **registros A** y los **registros MX**. En algunos casos, los registros CNAME tendrán otros nombres, como **Registro de Alias**.
   * página de Hello también tendrá los campos que permiten demasiado**mapa** desde una **nombre de Host** o **nombre de dominio** tooanother nombre de dominio.
3. Aunque los detalles de Hola de cada registrador varían, por lo general se asigna *de* nombre de dominio personalizado (como **contoso.com**,) *a* nombre de dominio de Traffic Manager de hello (**contoso.trafficmanager.net**) que se utiliza para la aplicación web.
   
   > [!NOTE]
   > O bien, si un registro ya está en uso y necesita toopreemptively enlazar su tooit de aplicaciones, puede crear un registro CNAME adicional. Por ejemplo, enlace de toopreemptively **www.contoso.com** tooyour web app, cree un registro CNAME de **awverify.www** demasiado**contoso.trafficmanager.net**. A continuación, puede agregar tooyour "www.contoso.com" aplicación Web sin cambiar el registro CNAME de Hola "www". Para más información, consulte [Creación de registros DNS para una aplicación web en un dominio personalizado][CREATEDNS].
   > 
   > 
4. Cuando haya terminado de agregar o modificar los registros DNS en el registrador, guardar los cambios de Hola.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>Habilitación del Administrador de tráfico
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea hello [Centro para desarrolladores de Node.js](/develop/nodejs/).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
