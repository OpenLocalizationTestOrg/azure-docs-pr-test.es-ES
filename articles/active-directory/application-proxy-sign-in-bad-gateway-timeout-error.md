---
title: "aaa \"no se puede tener acceso a este error de aplicaciones corporativas al usar una aplicación de Proxy de aplicación | Documentos de Microsoft\""
description: "Cómo acceso común tooresolve problemas con aplicaciones de Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 490b106b7d774ee43fc076cc5d082997a1df85e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a>Error "Can't Access this Corporate Application" al usar una aplicación de Proxy de aplicación

Este artículo le ayudará tootroubleshoot problemas comunes que se enfrentan cuando aparece un error "no se puede obtener acceso a esta aplicación corporativa" en una aplicación de Proxy de aplicación de Azure AD.

## <a name="overview"></a>Información general
Cuando aparece este error, página de hello también compartan un código de estado. Ese código es probablemente una de las siguientes de hello:

-   **Tiempo de espera de puerta de enlace**: hello servicio Proxy de aplicación es el conector de hello tooreach no se puede. Esto suele indicar un problema con la asignación de conector de hello, conector propiamente dicho u Hola reglas en torno a conector de Hola a redes.

-   **Puerta de enlace errónea**: conector de hello es aplicación de back-end de hello tooreach no se puede. Esto podría indicar un error de configuración de la aplicación hello.

-   **Prohibido**: Hola usuario no está autorizado tooaccess Hola aplicación. Esto puede ocurrir cuando el usuario de hello no se asigna toohello aplicación en Azure Active Directory, o si en back-end de Hola Hola usuario no tiene aplicación hello de permiso tooaccess.

código de hello toofind, vistazo texto hello en la parte inferior izquierda de Hola Hola del mensaje de error para el campo de "Código de estado" Hola. Buscar las notas de la parte inferior de Hola de página Hola con sugerencias adicionales.

   ![Error de tiempo de espera agotado para la puerta de enlace](./media/application-proxy/connection-problem.png)

Para obtener detalles sobre cómo tootroubleshoot Hola a causa de estos errores y obtener más detalles sobre las correcciones sugeridas, vea Hola correspondiente sección.

## <a name="gateway-timeout-errors"></a>Errores Gateway Timeout (Tiempo de espera agotado para la puerta de enlace)

Se produce un tiempo de espera de la puerta de enlace al servicio de hello trata de conector de hello tooreach y ventana de tiempo de espera de hello toowithin no se puede. Esto se debe normalmente a una aplicación asignada tooa grupo de conectores con conectores no funcionen o algunos puertos requeridos por hello conector no están abiertos.


## <a name="bad-gateway-errors"></a>Errores Bad Gateway (Puerta de enlace incorrecta)

Un error de puerta de enlace incorrecta indica que dicho conector hello es aplicación de back-end de hello tooreach no se puede. Asegúrese de que ha publicado la aplicación correcta de hello. Errores comunes que provocan este error:

-   Un error de escritura o un error en la dirección URL interna de Hola

-   Raíz de hello no publicación de aplicación hello. Por ejemplo, la publicación <http://expenses/reimbursement> pero intentar tooaccess <http://expenses>

-   Problemas con la configuración de delegación limitada de Kerberos (KCD) Hola

-   Problemas con la aplicación de back-end de hello

## <a name="forbidden-errors"></a>Errores Forbidden (Prohibido)

No se ha asignado toohello aplicación Hola usuario si ve un error prohibido. Podría tratarse de Azure Active Directory o en la aplicación hello back-end.

toolearn tooassign usuarios toohello application en Azure, vea hello [documentación sobre la configuración](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).

Si lo confirma que está asignado el usuario de hello toohello aplicación en Azure, compruebe la configuración de usuario de hello en la aplicación de back-end de hello. Si está utilizando la delegación limitada de Kerberos/autenticación integrada de Windows, consulte nuestra página de solución de problemas de KCD para algunas directrices.

## <a name="check-hello-applications-internal-url"></a>Compruebe la dirección URL interna de la aplicación hello

Como primer paso rápido, vuelve a revisar, comprobar y corregir URL interna Hola abriendo aplicación Hola a través de **aplicaciones empresariales**, a continuación, seleccionar hello **Proxy de aplicación** menú. Compruebe que esto es URL interna correcta de hello, Hola uno utilizan desde su aplicación de Hola de tooaccess de red local.

## <a name="check-hello-application-is-assigned-tooa-working-connector-group"></a>Compruebe la aplicación hello se asigna tooa conector de grupo de trabajo

aplicación de hello tooverify se asigna tooa conector de grupo de trabajo:

1.  Abrir aplicación hello en el portal de hello yendo demasiado**Azure Active Directory**, haga clic en **aplicaciones empresariales**, a continuación, **todas las aplicaciones.** Abra la aplicación hello, a continuación, seleccione **Proxy de aplicación** desde el menú de la izquierda Hola.

2.  Buscar en el campo de grupo de conectores de Hola. Si no hay ningún conector de active en grupo de hello, verá una advertencia. Si no ve las advertencias, pasar demasiado "comprobar todos los puertos necesarios están en la lista blanca".

3.  Si se trata de hello incorrecto de conector de grupo, utilice Hola desplegable grupo correcto de tooselect hello y confirme ya no verá las advertencias. Si se trata de hello diseñado grupo de conectores, haga clic en página hello tooopen de mensaje de advertencia de hello con administración del conector.

4.  Desde aquí, hay algunos toodrill de formas en más:

  * Mover un conector active grupo hello: si tiene un conector activo que debería pertenecer toothis grupo y tiene la aplicación de línea de visión toohello destino back-end, puede mover Hola conector en el grupo de hello asignado. toodo por lo tanto, haga clic en el conector de Hola. En el campo de "Grupo de conectores" Hola, usar grupo correcto de hello tooselect desplegable hello y haga clic en Guardar.

  * Descargar un nuevo conector de ese grupo: desde esta página, puede obtener el vínculo de hello demasiado[descargar un nuevo conector](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download). necesidades del conector Hello toobe instalado en un equipo con aplicaciones de línea de visión directa toohello back-end y se coloca normalmente en Hola mismo servidor que la aplicación hello. Hola uso descargar toodownload de vínculo de conector un conector en el equipo de destino Hola. A continuación, haga clic en hello conector y usar Hola "Grupo de conectores" desplegable toomake pertenece grupo adecuado toohello seguro.

  * Investigar un conector inactivo: si se muestra como inactivo en un conector, es servicio de hello tooreach no se puede. Esto suele ser debido a puertos toosome requerido que se va a bloquear. toosolve este problema, el movimiento en demasiado "comprobar todos los puertos necesarios están en la lista blanca".

Después de usar estos pasos aplicación hello de tooensure es grupo tooa asignado al trabajo conectores, vuelva a la aplicación de Hola de prueba. Si sigue sin funcionar, continuar toohello próxima sección.

## <a name="check-all-required-ports-are-whitelisted"></a>Comprobación de que todos los puertos necesarios están en la lista de permitidos

tooverify todos los necesarios puertos están abiertos, vea la documentación sobre cómo abrir puertos. Si Hola a todos los puertos necesarios están abiertos, mover toohello siguiente sección.

## <a name="check-for-other-connector-errors"></a>Búsqueda de otros errores de los conectores

Si ninguno de hello anterior resuelve el problema de Hola Hola siguiente paso es toolook para problemas o errores con hello conector propiamente dicho. Puede ver algunos errores comunes de hello [documento de solución de problemas](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). 

También puede buscar directamente en hello conector registros tooidentify los errores. Muchos de los mensajes de error ser capaz de tooshare recomendaciones más específicas para realizar correcciones. toolearn cómo ver los registros de hello tooview, [nuestra documentación conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="additional-resolutions"></a>Soluciones adicionales

Si Hola anterior no soluciona el problema de hello, hay varias causas posibles diferentes. problema de Hola tooidentify:

Si la aplicación es toouse configurado la autenticación de Windows integrada (IWA), aplicación de hello de prueba sin inicio de sesión único. Si no es así, mueva el párrafo siguiente toohello. aplicación de hello toocheck sin inicio de sesión único, abra la aplicación a través de **aplicaciones empresariales,** y vaya toohello **Single Sign-On** menú. Hola de cambio de lista desplegable de "Autenticación de Windows integrada" demasiado "inicio de sesión único en Azure AD disabled". 

Ahora, abra un explorador y probar tooaccess Hola nuevo aplicación. Se debe solicitar autenticación y obtener en la aplicación hello. Si esto funciona, es problema de hello con la configuración de delegación limitada de Kerberos (KCD) Hola que habilita el inicio de sesión único en Hola. Consulte la página de solución de problemas de KCD Hola.

Si continúa el error de hello toosee, vaya a toohello máquina donde hello conector está instalado, abra un explorador e intente tooreach Hola interno dirección URL utilizada para la aplicación hello. Hello conector actúa como otro cliente de hello mismo equipo. Si no se puede alcanzar la aplicación hello, investigue por qué que esta aplicación de hello tooreach no se puede o utilizar un conector en un servidor que es capaz de tooaccess Hola aplicación.

Si puede llegar a la aplicación hello desde ese equipo, toolook para problemas o errores con hello conector propiamente dicho. Puede ver algunos errores comunes de hello [documento de solución de problemas](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). También puede buscar directamente en hello conector registros tooidentify los errores. Muchos de los mensajes de error ser capaz de tooshare recomendaciones más específicas para realizar correcciones. toolearn cómo ver los registros de hello tooview, [nuestra documentación conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="next-steps"></a>Pasos siguientes
[Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)
