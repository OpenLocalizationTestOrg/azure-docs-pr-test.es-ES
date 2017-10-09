---
title: aaaRDG y servidor de MFA de Azure con RADIUS | Documentos de Microsoft
description: "Se trata de una página de autenticación multifactor de Azure de Hola que te ayudará a implementar la puerta de enlace de escritorio remoto (RD) y servidor de Azure Multi-factor Authentication con RADIUS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>Puerta de enlace de Escritorio remoto y Servidor Azure Multi-Factor Authentication con RADIUS
Puerta de enlace de escritorio remoto (RD) usa a menudo, los usuarios de tooauthenticate local de servicios de directivas de redes (NPS) de Hola. Este artículo describe cómo tooroute RADIUS solicita de hello puerta de enlace de escritorio remoto (a través de Hola NPS local) toohello servidor Multi-factor Authentication. Hello combinación de Azure MFA y puerta de enlace de escritorio remoto significa que los usuarios pueden acceder a sus entornos de trabajo desde cualquier lugar mientras se realiza una autenticación segura. 

Puesto que no se admite la autenticación de Windows para los servicios de terminal Server 2012 R2, utilice toointegrate de puerta de enlace de escritorio remoto y RADIUS con el servidor MFA. 

Instalar Hola servidor Azure Multi-factor Authentication en un servidor independiente, los servidores proxy que solicitar Hola RADIUS encenderlo toohello NPS Hola servidor de puerta de enlace de escritorio remoto. Después de que NPS valide la contraseña y nombre de usuario de hello, devuelve un toohello respuesta del servidor de autenticación multifactor. A continuación, Hola servidor MFA realiza el segundo factor de autenticación de Hola y devuelve una puerta de enlace de toohello de resultado.

## <a name="prerequisites"></a>Requisitos previos

- Un servidor Azure MFA unido a un dominio. Si no tiene uno ya instalada, siga los pasos de hello en [introducción con hello servidor Azure Multi-factor Authentication](multi-factor-authentication-get-started-server.md).
- Una Puerta de enlace de Escritorio remoto que se autentica con los servicios de la directiva de red.

## <a name="configure-hello-remote-desktop-gateway"></a>Configurar Hola puerta de enlace de escritorio remoto
Configurar Hola puerta de enlace de escritorio remoto toosend RADIUS autenticación tooan servidor Azure Multi-factor Authentication. 

1. En el Administrador de puerta de enlace de escritorio remoto, haga clic en el nombre del servidor de Hola y seleccione **propiedades**.
2. Vaya toohello **almacén de CAP de RD** pestaña y seleccione **servidor Central que ejecuta NPS**. 
3. Agregue uno o más servidores de autenticación multifactor de Azure como servidores RADIUS, escriba el nombre de Hola o dirección IP de cada servidor. 
4. Cree un secreto compartido para cada servidor.

## <a name="configure-nps"></a>Configuración de NPS
Hola puerta de enlace de escritorio remoto usa NPS toosend Hola RADIUS solicitud tooAzure la autenticación multifactor. tooconfigure NPS, cambie primero configuración de tiempo de espera de hello tooprevent Hola puerta de enlace de escritorio remoto desde el tiempo de espera antes de que se ha completado verificacion de Hola. A continuación, actualice las autenticaciones RADIUS de tooreceive NPS desde el servidor MFA. Usar hello siguiendo el procedimiento tooconfigure NPS:

### <a name="modify-hello-timeout-policy"></a>Modificar la directiva de tiempo de espera de Hola

1. En NPS, abra hello **clientes RADIUS y servidor** menú Hola dejado la columna y seleccione **grupos de servidores RADIUS remotos**. 
2. Seleccione hello **grupo de servidores de puerta de enlace de TS**. 
3. Vaya toohello **equilibrio de carga** ficha. 
4. Cambiar ambos hello **quita el número de segundos sin respuesta antes de solicitud se considera** hello y **número de segundos entre solicitudes cuando el servidor se identifica como no disponible** toobetween 30 y 60 segundos. (Si se encuentra que ese servidor hello todavía expira durante la autenticación, puede regresar a este punto y aumente Hola número de segundos.)
5. Vaya toohello **/cuenta de autenticación** pestaña y compruebe que los puertos RADIUS Hola especifican ese Hola servidor Multi-factor Authentication está escuchando en los puertos Hola de coincidencia.

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>Preparar las autenticaciones de tooreceive NPS de hello servidor MFA

1. Haga clic en **clientes RADIUS** en clientes RADIUS y servidores de hello dejado la columna y seleccione **nuevo**.
2. Agregar Hola servidor Azure Multi-factor Authentication como cliente RADIUS. Elija un nombre descriptivo y especifique un secreto compartido.
3. Abra hello **directivas** menú Hola dejado la columna y seleccione **directivas de solicitud de conexión**. Debe ver una directiva denominada DIRECTIVA DE AUTORIZACIÓN DE PUERTA DE ENLACE TS creada al configurar la puerta de enlace RD. Esta directiva reenvía las solicitudes RADIUS toohello servidor Multi-factor Authentication.
4. Haga clic en **DIRECTIVA DE AUTORIZACIÓN DE PUERTA DE ENLACE TS** y seleccione **Duplicar directiva**. 
5. Abra la nueva directiva y vaya toohello de hello **condiciones** ficha.
6. Agregar una condición que coincida con el nombre descriptivo del cliente con el nombre descriptivo de hello establecido en el paso 2 para el cliente RADIUS del servidor Azure Multi-factor Authentication de Hola Hola. 
7. Vaya toohello **configuración** pestaña y seleccione **autenticación**.
8. Cambiar proveedor de autenticación de hello demasiado**autenticar solicitudes en este servidor**. Esta directiva garantiza que cuando NPS recibe una solicitud RADIUS de hello servidor Azure MFA, la autenticación de Hola se produce localmente en lugar de enviar una solicitud RADIUS atrás toohello servidor de autenticación multifactor de Azure, que daría lugar a una condición de bucle. 
9. tooprevent una condición de bucle, asegúrese de que la nueva directiva de Hola está ordenada por encima de la directiva original de Hola Hola **directivas de solicitud de conexión** panel.

## <a name="configure-azure-multi-factor-authentication"></a>Configuración de Azure Multi-Factor Authentication

Hola servidor Azure Multi-factor Authentication está configurado como proxy RADIUS entre la puerta de enlace de escritorio remoto y NPS.  Debe instalarse en un servidor unido a un dominio que es independiente del servidor de puerta de enlace de escritorio remoto de Hola. Usar hello después Hola de procedimiento tooconfigure servidor Azure Multi-factor Authentication.

1. Abra Hola servidor Azure Multi-factor Authentication y seleccione el icono de autenticación RADIUS Hola. 
2. Comprobar hello **Habilitar autenticación RADIUS** casilla de verificación.
3. En la pestaña de clientes de hello, asegúrese de puertos de hello coinciden con lo que se configura en NPS, a continuación, seleccione **agregar**.
4. Agregue la dirección IP del servidor de puerta de enlace de escritorio remoto de hello, nombre de la aplicación (opcional) y un secreto compartido. Hola compartido secretas necesidades toobe mismo Hola Hola servidor Azure Multi-factor Authentication y puerta de enlace de escritorio remoto.
3. Vaya toohello **destino** ficha y seleccione hello **servidores RADIUS** botón de radio.
4. Seleccione **agregar** y escriba la dirección IP de hello, secreto compartido y puertos del servidor NPS de Hola. A menos que utilice un NPS central, se Hola mismo Hola cliente RADIUS y el destino RADIUS. secreto compartido Hola debe coincidir con el programa de instalación de uno de hello en la sección de cliente RADIUS del servidor NPS de Hola Hola.

![Autenticación Radius](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>Pasos siguientes

- Integración de Azure MFA y [aplicaciones web de IIS](multi-factor-authentication-get-started-server-iis.md)

- Obtenga respuestas en hello [P+F de autenticación multifactor de Azure](multi-factor-authentication-faq.md)
