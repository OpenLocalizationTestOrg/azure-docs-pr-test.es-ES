---
title: "aaaLDAP autenticación y el servidor de MFA de Azure | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que te ayudará a implementar la autenticación LDAP y el servidor de autenticación multifactor de Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>Servidor de autenticación LDAP y Azure Multi-Factor Authentication
De forma predeterminada, Hola servidor Azure Multi-factor Authentication está configurado tooimport o sincronizar usuarios desde Active Directory. Sin embargo, puede ser configurado toobind toodifferent LDAP directorios, como un directorio ADAM o un controlador de dominio de Active Directory específico. Cuando tooa conectado directorio mediante LDAP, Hola servidor Azure Multi-factor Authentication puede actuar como un autenticaciones tooperform de proxy LDAP. También permite Hola uso del enlace LDAP como destino RADIUS para la autenticación previa de usuarios con la autenticación de IIS, o para la autenticación principal en el portal de usuarios de Azure MFA Hola.

toouse Azure Multi-factor Authentication como proxy LDAP, inserte Hola servidor Azure Multi-factor Authentication entre Hola de cliente LDAP (por ejemplo, el dispositivo VPN, la aplicación) y el servidor de directorio LDAP de Hola. Hola servidor Azure Multi-factor Authentication debe estar configurado toocommunicate con los servidores de cliente de Hola y directorio LDAP de Hola. En esta configuración, Hola servidor Azure Multi-factor Authentication acepta solicitudes LDAP de servidores de cliente y las aplicaciones y los reenvía toohello destino LDAP directory toovalidate Hola principales credenciales del servidor. Si el directorio LDAP de hello valida las credenciales principales de hello, la autenticación multifactor Azure lleva a cabo una verificación de identidad segundo y envía a un cliente LDAP de toohello de espera de respuesta. autenticación en su totalidad Hola sin errores solo si la autenticación de servidor LDAP de Hola y comprobación del segundo paso de Hola se realizan correctamente.

## <a name="configure-ldap-authentication"></a>Configuración de la autenticación LDAP
autenticación de LDAP tooconfigure, Hola instalar servidor de autenticación multifactor de Azure en un servidor de Windows. Usar hello siguiendo el procedimiento:

### <a name="add-an-ldap-client"></a>Agregue un cliente LDAP.

1. Hola servidor Azure Multi-factor Authentication, seleccione el icono de autenticación LDAP de hello en el menú de la izquierda Hola.
2. Comprobar hello **Habilitar autenticación LDAP** casilla de verificación.

   ![Autenticación LDAP](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. En la pestaña de clientes de hello, cambia el puerto TCP de Hola y el puerto SSL si Hola servicio LDAP de autenticación multifactor de Azure debe enlazar puertos estándar toonon toolisten para las solicitudes LDAP.
4. Si tiene previsto toouse LDAPS desde Hola cliente toohello servidor Azure Multi-factor Authentication, debe instalarse un certificado SSL en hello mismo servidor como servidor de MFA. Haga clic en **examinar** toohello siguiente SSL de certificados y seleccione un toouse de certificado de conexión segura de Hola.
5. Haga clic en **Agregar**.
6. En el cuadro de diálogo Agregar cliente LDAP de hello, escriba la dirección IP de hello de dispositivo de hello, servidor o aplicación que autentica toohello servidor y un nombre de la aplicación (opcional). nombre de la aplicación Hello aparece en los informes de la autenticación multifactor Azure y puede mostrarse en mensajes de autenticación SMS o aplicación móvil.
7. Comprobar hello **coincidencia de usuario requieren la autenticación multifactor Azure** cuadro si todos los usuarios se han o se importarán en hello Server y la comprobación de paso tootwo de asunto. Si un número significativo de usuarios no se ha importado en hello servidor y/o está exento de la verificación en dos pasos, deje el cuadro de hello desactivada. Consulte el archivo de Ayuda de servidor MFA de Hola para obtener información adicional acerca de esta característica.

Repita a estos pasos tooadd adicionales LDAP los clientes.

### <a name="configure-hello-ldap-directory-connection"></a>Configurar conexión de directorio LDAP de Hola

Una vez hello Azure la autenticación multifactor tooreceive configurado las autenticaciones de LDAP, debe actuar como proxy esos directorio LDAP de toohello de autenticaciones. Por lo tanto, pestaña de destino de Hola solo muestra una única atenuada opción toouse un destino LDAP.

1. Hola tooconfigure conexión de directorio LDAP, haga clic en hello **integración de directorios** icono.
2. En la pestaña de configuración de hello, seleccione hello **utilizar la configuración LDAP específica** botón de radio.
3. Seleccione **Editar...**
4. En el cuadro de diálogo Editar configuración de LDAP de hello, rellenar los campos de hello con el directorio LDAP de hello información necesaria tooconnect toohello. Se incluyen descripciones de campos de hello en el archivo de Ayuda del servidor de autenticación multifactor de Azure de Hola.

    ![Integración de directorios](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Probar conexión de LDAP de hello haciendo clic en hello **prueba** botón.
6. Si la prueba de conexión de LDAP de hello fue correcta, haga clic en hello **Aceptar** botón.
7. Haga clic en hello **filtros** Hola ficha servidor está preconfigurado tooload contenedores, grupos de seguridad y usuarios de Active Directory. Si el enlace tooa otro directorio LDAP, es probable que necesite filtros de hello tooedit mostrados. Haga clic en hello **ayuda** vínculo para obtener más información acerca de los filtros.
8. Haga clic en hello **atributos** Hola ficha servidor está preconfigurado toomap atributos de Active Directory.
9. Si está enlazando tooa otro directorio o toochange Hola preconfigurado asignaciones de atributos LDAP, haga clic en **editar...**
10. En el cuadro de diálogo Editar atributos de hello, modificar asignaciones de atributos LDAP de hello para el directorio. Nombres de atributo se pueden escribir o seleccionar haciendo clic en hello **...** botón siguiente tooeach campo. Haga clic en hello **ayuda** vínculo para obtener más información sobre atributos.
11. Haga clic en hello **Aceptar** botón.
12. Haga clic en hello **configuración de la empresa** icono y seleccione hello **resolución de nombre de usuario** ficha.
13. Si se está conectando tooActive directorio desde un servidor unido a un dominio, deje hello **identificadores de seguridad (SID) de usar Windows para la coincidencia de nombres de usuario** botón de radio seleccionado. En caso contrario, seleccione hello **atributo del identificador único usar LDAP para la coincidencia de nombres de usuario** botón de radio. 

Cuando Hola **atributo del identificador único usar LDAP para la coincidencia de nombres de usuario** botón de radio está seleccionado, Hola servidor Azure Multi-factor Authentication intenta tooresolve cada nombre de usuario tooa único identificador hello directorio LDAP. Se realiza una búsqueda LDAP en el nombre de usuario de hello atributos definidos en hello integración de directorios -> pestaña atributos. Cuando un usuario se autentica, el nombre de usuario de hello es toohello resolver el identificador único en el directorio LDAP de Hola. Identificador único de Hello sirve para usuario Hola coincidentes en el archivo de datos de la autenticación multifactor Azure Hola. Esto permite comparaciones que no distinguen mayúsculas de minúsculas, así como formatos largo y corto de nombres de usuario.

Después de completar estos pasos, Hola servidor MFA escucha en los puertos de hello configurado para las solicitudes de acceso LDAP de hello configura los clientes y actúa como un proxy para las solicitudes de toohello directorio LDAP para la autenticación.

## <a name="configure-ldap-client"></a>Configuración del cliente LDAP
Hola tooconfigure cliente LDAP, use instrucciones de hello:

* Configurar su dispositivo, el servidor o la aplicación tooauthenticate a través de LDAP toohello servidor Azure Multi-factor Authentication como si fuese el directorio LDAP. Use Hola misma configuración que usaría normalmente tooconnect directamente tooyour directorio LDAP, excepto el nombre del servidor de Hola o la dirección IP que será de hello servidor Azure Multi-factor Authentication.
* Configurar a tiempo de espera too30 y 60 segundos de hello LDAP por lo que no hay credenciales de usuario de tiempo toovalidate Hola con directorio LDAP de hello, realizar la comprobación del segundo paso de hello, reciba la respuesta y responder toohello solicitud de acceso LDAP.
* Si usa LDAPS, hello dispositivo o el servidor que realiza consultas LDAP de hello debe confiar Hola certificado SSL instalado en hello servidor Azure Multi-factor Authentication.

