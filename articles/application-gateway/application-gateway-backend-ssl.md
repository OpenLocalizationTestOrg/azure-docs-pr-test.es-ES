---
title: aaaEnabling final tooend SSL en la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de hello Application Gateway final tooend compatibilidad con SSL."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>Información general sobre final tooend SSL con puerta de enlace de aplicaciones

Puerta de enlace de aplicación es compatible con la terminación SSL en la puerta de enlace de hello, después de que el tráfico fluye normalmente sin cifrar a servidores de back-end de toohello. Esta característica permite toobe de servidores web unburdened de sobrecarga de cifrado y descifrado. Pero para algunos clientes servidores back-end de comunicación sin cifrar toohello no es una opción aceptable. Esta comunicación sin cifrar puede ser debido a requisitos toosecurity, requisitos de cumplimiento, o aplicación hello solo puede aceptar una conexión segura. Para estas aplicaciones, puerta de enlace de aplicaciones admite final tooend SSL cifrado.

## <a name="overview"></a>Información general

End tooend SSL permite toosecurely transmitir cifran mientras todavía sacar partido de las ventajas de Hola de características de equilibrio de carga de nivel 7 de la puerta de enlace de la aplicación proporciona el back-end de los datos confidenciales toohello. Algunas de estas características son afinidad de sesión basado en cookies, el enrutamiento basado en dirección URL, compatibilidad para el enrutamiento se basa en sitios o capacidad tooinject X - reenviado-* encabezados.

Cuando se configura con el modo de comunicación de SSL de fin tooend, puerta de enlace de aplicación finaliza las sesiones SSL de hello en puerta de enlace de Hola y descifra el tráfico de usuario. A continuación, aplica Hola configurado reglas tooselect un back-end adecuados grupo instancia tooroute tráfico. Puerta de enlace de aplicaciones, a continuación, inicia un nuevo servidor de back-end de toohello de conexión de SSL y vuelve a cifra datos con certificado de clave pública del servidor de back-end de hello antes de transmitirlos Hola solicitud toohello back-end. Tooend final que SSL se habilita al establecer la configuración del protocolo en BackendHTTPSetting tooHTTPS, que es, a continuación, aplica tooa grupo de back-end. Cada servidor de back-end en el grupo de back-end de hello con tooend final que ha habilitado SSL debe configurarse con una comunicación segura de tooallow de certificado.

![escenario de extremo tooend ssl][1]

En este ejemplo, las solicitudes mediante TLS 1.2 son toobackend enrutado servidores Pool1 mediante final tooend SSL.

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>Terminar tooend SSL y creación de listas blancas de certificados

Puerta de enlace de aplicaciones sólo se comunica con instancias de conocidos back-end que tienen en la lista blanca de su certificado con la puerta de enlace de aplicaciones de Hola. tooenable blancas de certificados, debe cargar la clave pública de Hola de back-end server certificados toohello aplicación puerta de enlace (no el certificado de raíz hello). A continuación, se permiten solo conexiones tooknown y en la lista blanca back-ends. Hola restantes back-ends produce un error de puerta de enlace. Los certificados autofirmados son para fines de prueba que y no se recomiendan para cargas de trabajo de producción. Estos certificados tienen toobe la lista de permitidos con puerta de enlace de hello aplicación tal como se describe en hello pasos anteriores antes de que se puedan utilizar.

## <a name="next-steps"></a>Pasos siguientes

Después de aprender a final tooend SSL, vaya demasiado[habilitar final tooend SSL en la puerta de enlace de aplicaciones](application-gateway-end-to-end-ssl-powershell.md) toocreate una puerta de enlace de aplicaciones con terminar tooend SSL.

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
