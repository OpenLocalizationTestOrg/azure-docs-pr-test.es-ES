---
title: "aaaRADIUS autenticación y el servidor de MFA de Azure | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que te ayudará a implementar la autenticación RADIUS y servidor de autenticación multifactor de Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>Integración de la autenticación RADIUS con Servidor Azure Multi-Factor Authentication
Utilice Hola sección de autenticación RADIUS del servidor Azure MFA tooenable y configurar la autenticación RADIUS. RADIUS es un estándar de protocolo tooaccept las solicitudes de autenticación y tooprocess dichas solicitudes. Hola servidor Azure Multi-factor Authentication actúa como un servidor RADIUS. Insértelo entre el cliente RADIUS (dispositivo VPN) y el destino de autenticación, que podría ser Active Directory (AD), un directorio LDAP u otro tooadd de servidor RADIUS Azure la autenticación multifactor. Para toofunction de Azure la autenticación multifactor (MFA), debe configurar Hola servidor Azure MFA para que puedan comunicarse con servidores de cliente de Hola y de destino de autenticación de Hola. Hola servidor Azure MFA acepta solicitudes de un cliente RADIUS, valida las credenciales con el destino de la autenticación de hello, agrega Azure Multi-factor Authentication y envía a un cliente RADIUS de toohello de espera de respuesta. solicitud de autenticación de Hello solo se realiza correctamente si la autenticación principal de Hola y Hola Azure Multi-factor Authentication se realizan correctamente.

> [!NOTE]
> Hola servidor MFA solo admite PAP (Protocolo de autenticación de contraseña) y MSCHAPv2 (Protocolo de autenticación por desafío mutuo de Microsoft) RADIUS protocolos cuando actúa como un servidor RADIUS.  Otros protocolos, como EAP (Protocolo de autenticación extensible), se pueden usar cuando el servidor MFA de hello actúa como un servidor RADIUS tooanother de proxy RADIUS que admite dicho protocolo.
>
> En esta configuración, tokens unidireccionales de SMS y OATH no funcionan porque Hola servidor MFA no puede iniciar una respuesta de desafío de RADIUS correcta mediante protocolos alternativos.

![Autenticación Radius](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>Incorporación de un cliente RADIUS
autenticación de RADIUS tooconfigure, Hola instalar servidor de autenticación multifactor de Azure en un servidor de Windows. Si tiene un entorno de Active Directory, servidor hello debe toohello Unidos a un dominio de red de Hola. Usar hello después Hola de procedimiento tooconfigure servidor de autenticación multifactor de Azure:

1. Hola servidor Azure Multi-factor Authentication, haga clic en el icono de autenticación RADIUS de hello en el menú de la izquierda Hola.
2. Comprobar hello **Habilitar autenticación RADIUS** casilla de verificación.
3. En la pestaña de clientes de hello, cambiar hello autenticación y puertos de cuentas si Hola servicio RADIUS de MFA de Azure necesita toolisten para las solicitudes RADIUS en puertos no estándar.
4. Haga clic en **Agregar**.
5. Escriba la dirección IP de hello de dispositivo/servidor de Hola que autenticará toohello servidor Azure Multi-factor Authentication, un nombre de la aplicación (opcional) y un secreto compartido.

  nombre de la aplicación Hello aparece en los informes de la autenticación multifactor Azure y puede mostrarse en mensajes de autenticación SMS o aplicación móvil.

  Hola comparte necesidades secreto toobe Hola iguales en ambos Hola servidor Azure Multi-factor Authentication y dispositivo/servidor.

6. Comprobar hello **coincidencia de usuario requieren la autenticación multifactor** cuadro si todos los usuarios se han o se importarán en hello Server y la autenticación de factor de toomulti asunto. Si un número significativo de usuarios no se ha importado en hello servidor y/o se va a excluir de la verificación en dos pasos, deje el cuadro de hello desactivada.
7. Comprobar hello **token OATH de reserva Enable** cuadro si desea toouse códigos de acceso OATH desde aplicaciones móviles de comprobación como una llamada de teléfono de reserva toohello fuera de banda, SMS, o las notificaciones de inserción.
8. Haga clic en **Aceptar**.

Repita los pasos del 4 al 8 tooadd tantos clientes RADIUS adicionales según sea necesario.

## <a name="configure-your-radius-client"></a>Configuración del cliente RADIUS

1. Haga clic en hello **destino** ficha.
2. Si Hola servidor Azure MFA está instalado en un servidor unido a un dominio en un entorno de Active Directory, seleccione el dominio de Windows.
3. Si los usuarios deben autenticarse en un directorio LDAP, seleccione **Enlace LDAP**.

  un enlace LDAP toouse, haga clic en el icono de integración de directorios de Hola y editar configuración de LDAP de hello en la pestaña de configuración de Hola para que hello servidor pueda enlazar tooyour directory. Encontrará instrucciones para configurar LDAP en hello [Guía de configuración de Proxy LDAP](multi-factor-authentication-get-started-server-ldap.md).

4. Si los usuarios deben autenticarse en otro servidor RADIUS, seleccione servidores RADIUS.
5. Haga clic en **agregar** solicita tooconfigure hello toowhich Hola servidor Azure MFA will proxy saludos del servidor RADIUS.
6. En el cuadro de diálogo Agregar servidor RADIUS de hello, escriba la dirección IP de saludo del servidor RADIUS de Hola y un secreto compartido.

  Hola comparte necesidades secreto toobe Hola iguales en ambos Hola servidor Azure Multi-factor Authentication y el servidor RADIUS. Cambiar el puerto de autenticación de Hola y el puerto de cuentas si se usan puertos diferentes por servidor RADIUS de Hola.

7. Haga clic en **Aceptar**.
8. Agregar Hola servidor Azure MFA como un cliente RADIUS en hello otro servidor RADIUS para que pueda procesar las solicitudes de acceso enviadas tooit de hello servidor Azure MFA. Usar hello que mismas compartida secreto configurado en hello servidor Azure Multi-factor Authentication.

Repita estos pasos tooadd más servidores RADIUS y configurar el orden de hello en qué hello Azure MFA servidor debe llamarlos con hello **Subir** y **mover hacia abajo** botones.

Esto completa la configuración del servidor de autenticación multifactor de Azure de Hola. Hola servidor ahora escucha en los puertos de hello configurado para las solicitudes de acceso RADIUS de los clientes de hello configurado.   

## <a name="radius-client-configuration"></a>Configuración del cliente RADIUS
Hola tooconfigure cliente RADIUS, use instrucciones de hello:

* Configure su tooauthenticate dispositivo/servidor a través de la dirección IP del servidor RADIUS toohello Azure Multi-factor Authentication, que actuará como servidor RADIUS de Hola.
* Usar hello que mismas compartida secreto que configuró anteriormente.
* Configurar a tiempo de espera too30 y 60 segundos de hello RADIUS para que no haya credenciales del usuario de tiempo toovalidate hello, realizar la verificación en dos pasos, reciba la respuesta y, a continuación, responder toohello solicitud de acceso RADIUS.
