---
title: "aaaIIS autenticación y el servidor de MFA de Azure | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que te ayudará a implementar la autenticación de IIS y el servidor de autenticación multifactor de Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>Configuración de Servidor Azure Multi-Factor Authentication para aplicaciones web de IIS

Utilice la sección de autenticación de IIS de Hola de hello servidor Azure Multi-factor Authentication (MFA) tooenable y configurar la autenticación de IIS para la integración con aplicaciones web IIS de Microsoft. instala un complemento que puede filtrar las solicitudes realizadas toohello IIS web server tooadd la autenticación multifactor Azure Hola servidor Azure MFA. Hola complemento IIS proporciona compatibilidad para la autenticación basada en formularios y la autenticación de HTTP de Windows integrada. Direcciones IP también pueden ser tooexempt configuradas las direcciones IP internas de autenticación en dos fases de confianza.

![Autenticación IIS](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>Mediante la autenticación IIS basada en formularios con el servidor Azure Multi-Factor Authentication
toosecure un IIS aplicación que utiliza la autenticación basada en formularios web, instale Hola servidor Azure Multi-factor Authentication en el servidor web de IIS de Hola y configure Hola Server por hello siguiendo el procedimiento:

1. Hola servidor Azure Multi-factor Authentication, haga clic en el icono de autenticación de IIS de hello en el menú de la izquierda Hola.
2. Haga clic en hello **basada en formularios** ficha.
3. Haga clic en **Agregar**.
4. variables de nombre de usuario, contraseña y dominio toodetect automáticamente, escriba Hola dirección URL de inicio de sesión (por ejemplo, https://localhost/contoso/auth/login.aspx) en el cuadro de diálogo de hello automática de sitio Web y haga clic en **Aceptar**.
5. Comprobar hello **coincidencia de usuario requieren la autenticación multifactor** cuadro si todos los usuarios se han o se importarán en hello Server y la autenticación de factor de toomulti asunto. Si un número significativo de usuarios no se ha importado en hello servidor y/o se va a excluir de la autenticación multifactor, deje el cuadro de hello desactivada.
6. Si no se detectan automáticamente las variables de página de hello, haga clic en **especificar manualmente** en el cuadro de diálogo de hello automática de sitio Web.
7. En el cuadro de diálogo Agregar sitio Web de hello, escriba la página de inicio de sesión de toohello de dirección URL de hello en el campo de dirección URL de envío de Hola y escriba un nombre de la aplicación (opcional). nombre de la aplicación Hello aparece en los informes de la autenticación multifactor Azure y puede mostrarse en mensajes de autenticación SMS o aplicación móvil.
8. Seleccione el formato de solicitud correcto de Hola. Esto se establece demasiado**POST o GET** para la mayoría de las aplicaciones web.
9. Escriba la variable de nombre de usuario de hello, la variable de contraseña y la variable de dominio (si aparece en la página de inicio de sesión de hello). nombres de hello toofind de hello cuadros de entrada, navegar por la página de inicio de sesión de toohello en un explorador web, haga doble clic en la página de Hola y seleccione **ver código fuente**.
10. Comprobar hello **coincidencia de usuario requieren la autenticación multifactor Azure** cuadro si todos los usuarios se han o se importarán en hello Server y la autenticación de factor de toomulti asunto. Si un número significativo de usuarios no se ha importado en hello servidor y/o se va a excluir de la autenticación multifactor, deje el cuadro de hello desactivada.
11. Haga clic en **avanzadas** tooreview opciones avanzada, incluidas:

  - Seleccionar un archivo de página de denegación personalizado
  - Sitio Web toohello las autenticaciones correctas de caché durante un período de tiempo mediante cookies
  - Seleccione si las credenciales tooauthenticate Hola principal en un dominio de Windows, el directorio LDAP. o servidor RADIUS.

12. Haga clic en **Aceptar** cuadro de diálogo Agregar sitio Web de tooreturn toohello.
13. Haga clic en **Aceptar**.
14. Una vez Hola dirección URL y las variables de página se han detectado o especificado, datos del sitio Web de hello muestran de Hola panel basado en formularios.

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>Uso de la autenticación integrada de Windows con el servidor Azure Multi-Factor Authentication
toosecure un IIS web de aplicación que utiliza la autenticación HTTP integrada de Windows, instalar Hola servidor Azure MFA en el servidor web de IIS de Hola y configure Hola Server con hello pasos:

1. Hola servidor Azure Multi-factor Authentication, haga clic en el icono de autenticación de IIS de hello en el menú de la izquierda Hola.
2. Haga clic en hello **HTTP** ficha.
3. Haga clic en **Agregar**.
4. En el cuadro de diálogo Agregar URL Base de hello, escriba la dirección de URL de hello para el sitio Web de Hola donde se realiza la autenticación HTTP (por ejemplo, http://localhost/owa) y especifique un nombre de aplicación (opcional). nombre de la aplicación Hello aparece en los informes de la autenticación multifactor Azure y puede mostrarse en mensajes de autenticación SMS o aplicación móvil.
5. Ajustar tiempo de espera de inactividad de Hola y el máximo tiempo de sesión si Hola predeterminado no es suficiente.
6. Comprobar hello **coincidencia de usuario requieren la autenticación multifactor** cuadro si todos los usuarios se han o se importarán en hello Server y la autenticación de factor de toomulti asunto. Si un número significativo de usuarios no se ha importado en hello servidor y/o se va a excluir de la autenticación multifactor, deje el cuadro de hello desactivada.
7. Comprobar hello **caché de cookies** cuadro si lo desea.
8. Haga clic en **Aceptar**.

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>Habilitar complementos IIS para el servidor Azure Multi-Factor Authentication
Después de configurar Hola basada en formularios o las direcciones URL de autenticación de HTTP y la configuración, seleccione Hola ubicaciones donde se debe cargar Hola complementos IIS de autenticación multifactor de Azure y habilitada en IIS. Usar hello siguiendo el procedimiento:

1. Si se ejecuta en IIS 6, haga clic en hello **ISAPI** ficha. Sitio Web de hello SELECT que Hola aplicación web está ejecutando bajo (por ejemplo, sitio Web predeterminado) tooenable hello Azure Multi-factor Authentication filtro ISAPI para ese sitio.
2. Si se ejecuta en IIS 7 o posterior, haga clic en hello **módulo nativo** ficha. Seleccione servidor de hello, sitios Web o aplicaciones tooenable Hola complemento de IIS en los niveles de hello deseado.
3. Haga clic en hello **autenticación habilitar IIS** cuadro situado en la parte superior de Hola de pantalla de bienvenida. La autenticación multifactor Azure ahora es la protección de aplicación de IIS de hello seleccionado. Asegúrese de que los usuarios se han importado en hello Server.

## <a name="trusted-ips"></a>IP de confianza
Hello IP de confianza permite a los usuarios toobypass Azure la autenticación multifactor para solicitudes de sitios Web que se originan de direcciones IP o subredes específico. Por ejemplo, puede que desee tooexempt a los usuarios de Azure Multi-factor Authentication cuando inicien sesión desde office Hola. Para ello, especificaría la subred de la oficina de hello como una entrada de IP de confianza. tooconfigure direcciones IP de confianza, utilice Hola siguiendo el procedimiento:

1. Hola sección de autenticación de IIS, haga clic en hello **IP de confianza** ficha.
2. Haga clic en **Agregar**.
3. Cuando aparezca el cuadro de diálogo Agregar IP de confianza de hello, seleccione hello **IP única**, **intervalo de IP**, o **subred** botón de radio.
4. Escriba la dirección IP de hello, intervalo de direcciones IP o subred que debe estar en la lista blanca. Si especificar una subred, seleccione Hola apropiados máscara de red y haga clic en **Aceptar**. lista blanca de Hola se ha agregado.
