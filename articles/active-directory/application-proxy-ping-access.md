---
title: "autenticación basada en aaaHeader con PingAccess para el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Publicar aplicaciones con Proxy de aplicación y PingAccess toosupport encabezado autenticación basada en."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>Autenticación basada en el encabezado para el inicio de sesión único con el proxy de aplicación y PingAccess

Azure Proxy de aplicación de Active Directory y PingAccess se han asociado juntos los clientes de Azure Active Directory de tooprovide con acceso tooeven más aplicaciones. PingAccess expande hello [ofertas de Proxy de aplicación existentes](active-directory-application-proxy-get-started.md) tooinclude tooapplications de acceso de inicio de sesión único que utilizan encabezados para la autenticación.

## <a name="what-is-pingaccess-for-azure-ad"></a>¿Qué es PingAccess para Azure AD?

PingAccess para Azure Active Directory es una oferta de PingAccess que permite el acceso a los usuarios toogive y tooapplications de inicio de sesión único que utilizan encabezados para la autenticación. Proxy de aplicación trata estas aplicaciones como cualquier otro, con acceso a tooauthenticate de Azure AD y, a continuación, pasar el tráfico a través del servicio de conector de Hola. PingAccess se coloca delante de aplicaciones de Hola y token de acceso de Hola de Azure AD se traduce en un encabezado para que aplicación hello recibe autenticación hello en formato de hello puede leer.

Los usuarios no notarás algo diferente cuando inician sesión en toouse las aplicaciones corporativas. Podrán seguir trabajando desde cualquier lugar y en cualquier dispositivo. 

Puesto que los conectores de Proxy de aplicación Hola dirigir tráfico remoto tooall aplicaciones independientemente de su tipo de autenticación, continuará saldo tooload automáticamente, así como.

## <a name="how-do-i-get-access"></a>¿Cómo puedo obtener acceso?

Dado que este escenario se ofrece a través de una asociación entre Azure Active Directory y PingAccess, se necesitarán licencias de ambos servicios. Sin embargo, las suscripciones de Azure Active Directory Premium incluyen una licencia de PingAccess básica que incluya las aplicaciones de too20. Si necesita más de 20 encabezado las aplicaciones basadas en toopublish, puede adquirir una licencia adicional de PingAccess. 

Para obtener más información, consulte [Ediciones de Azure Active Directory](active-directory-editions.md).

## <a name="publish-your-application-in-azure"></a>Publicación de una aplicación en Azure

Este artículo está pensado para las personas que va a publicar una aplicación con este escenario para hello primera vez. Recorre cómo tooget a trabajar con aplicaciones y PingAccess, además toohello pasos de publicación. Si ya configuró ambos servicios pero desea un actualizador de hello pasos de publicación, puede omitir la instalación del conector de Hola y mover demasiado[agregar su tooAzure aplicación AD con el Proxy de aplicación](#add-your-app-to-Azure-AD-with-Application-Proxy).

>[!NOTE]
>Puesto que este escenario es una asociación entre Azure AD y PingAccess, algunas de las instrucciones de hello existan en hello sitio identidades de Ping.

### <a name="install-an-application-proxy-connector"></a>Instalación de un conector del proxy de la aplicación

Si ya tiene habilitado el Proxy de aplicación y tiene un conector instalado, puede omitir esta sección y pasar demasiado[agregar su tooAzure aplicación AD con el Proxy de aplicación](#add-your-app-to-azure-ad-with-application-proxy).

conector del Proxy de aplicación Hello es un servidor de Windows servicio que dirige el tráfico de Hola de su empleados remotos tooyour las aplicaciones publicadas. Para obtener más instrucciones de instalación, consulte [habilitar Proxy de aplicación en el portal de Azure hello](active-directory-application-proxy-enable.md).

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador global.
2. Seleccione **Azure Active Directory** > **Proxy de la aplicación**.
3. Seleccione **descargar conector** descarga de conector de Proxy de aplicación de toostart Hola. Siga las instrucciones de instalación de Hola.

   ![Habilitar el Proxy de aplicación y descargar conector Hola](./media/application-proxy-ping-access/install-connector.png)

4. Descargar conector Hola automáticamente debe habilitar Proxy de aplicación para el directorio, pero si no se puede seleccionar **habilitar Proxy de aplicación**.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>Agregue su tooAzure aplicación AD con el Proxy de aplicación

Hay dos acciones necesita tootake Hola portal de Azure. En primer lugar, se necesita toopublish su aplicación con el Proxy de aplicación. A continuación, deberá toocollect cierta información acerca de la aplicación hello que puede utilizar durante los pasos de PingAccess Hola.

Siga estos pasos toopublish la aplicación. Para obtener un tutorial más detallado de los pasos 1 a 8, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](application-proxy-publish-azure-portal.md).

1. Si no lo ha hecho en la última sección de hello, inicie sesión en toohello [portal de Azure](https://portal.azure.com) como administrador global.
2. Seleccione **Azure Active Directory** > **Aplicaciones empresariales**.
3. Seleccione **agregar** princip Hola de hoja de Hola.
4. Seleccione **Aplicación local**.
5. Rellene los campos de hello necesario con información sobre la aplicación nuevo. Usar hello instrucciones para la configuración de hello:
   - **Dirección URL interna**: normalmente proporciona dirección URL de Hola que le guíe el inicio de sesión de la aplicación toohello en la página cuando esté en la red corporativa de Hola. Para este escenario Hola debe conector tootreat hello PingAccess proxy como página de aplicación hello Hola. Use este formato: `https://<host name of your PA server>:<port>`. puerto de Hello es 3000 de forma predeterminada, pero puede configurarlo en PingAccess.
   - **Método de autenticación previa**: Azure Active Directory.
   - **Traducir URL en encabezados**: No.

   >[!NOTE]
   >Si se trata de la primera aplicación, utilice el puerto 3000 toostart y vuelven a estar tooupdate esta opción si cambia la configuración de PingAccess. Si se trata de la aplicación de la segunda o posterior, lo que deberá hello toomatch agente de escucha que se ha configurado en PingAccess. Obtenga más información sobre [escucha en PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).

6. Seleccione **agregar** final Hola de hoja de Hola. Se agrega la aplicación, y abre el menú de inicio rápido de Hola.
7. En el menú de inicio rápido de hello, seleccione **asigna a un usuario para realizar pruebas**y agregue al menos un usuario toohello aplicación. Asegúrese de que esta cuenta de prueba tiene la aplicación de access toohello local.
8. Seleccione **asignar** asignación de usuario de prueba de toosave Hola.
9. En la hoja de administración de aplicaciones de hello, seleccione **inicio de sesión único**.
10. Elija **basado en el encabezado de inicio de sesión** desde el menú desplegable de Hola. Seleccione **Guardar**.

   >[!TIP]
   >Si se trata de la primera vez que usa basada en el encabezado de inicio de sesión único, deberá tooinstall PingAccess. toomake seguro de que su suscripción de Azure se asocia automáticamente con la instalación de PingAccess, usar la aplicación vínculo hello en este toodownload PingAccess de página de inicio de sesión único. Puede abrir el sitio de descarga de hello ahora o volver a verle toothis página. 

   ![Selección del inicio de sesión basado en encabezados](./media/application-proxy-ping-access/sso-header.PNG)

11. Cierre la hoja de aplicaciones de empresa de Hola o desplácese menú de todos los Hola forma toohello tooreturn izquierdo toohello Azure Active Directory.
12. Seleccione **App registrations** (Registros de aplicaciones).

   ![Selección de los registros de aplicaciones](./media/application-proxy-ping-access/app-registrations.png)

13. Aplicación de hello seleccione acaba de agregar, a continuación, **direcciones URL de respuesta**.

   ![Selección de las direcciones URL de respuesta](./media/application-proxy-ping-access/reply-urls.png)

14. Compruebe toosee si dirección URL externa de Hola que tooyour asignado aplicación en el paso 5 en la lista de direcciones URL de respuesta de Hola. Si no está, agréguela ahora.
15. En la hoja de configuración de aplicación Hola, seleccione **los permisos necesarios**.

  ![Selección de los permisos necesarios](./media/application-proxy-ping-access/required-permissions.png)

16. Seleccione **Agregar**. Para la API de hello, elija **Windows Azure Active Directory**, a continuación, **seleccione**. Para los permisos de hello, elija **lectura y escribir todas las aplicaciones** y **iniciar sesión y leer el perfil de usuario**, a continuación, **seleccione** y **realiza**.  

  ![Selección de permisos](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Recopilar información de pasos de hello PingAccess

1. En la hoja de configuración de la aplicación, seleccione **Propiedades**. 

  ![Selección de las propiedades](./media/application-proxy-ping-access/properties.png)

2. Guardar hello **Id. de aplicación** valor. Esto se usa para el Id. de cliente de hello cuando configura PingAccess.
3. En la hoja de configuración de aplicación Hola, seleccione **claves**.

  ![Selección de las claves](./media/application-proxy-ping-access/Keys.png)

4. Cree una clave, escriba una descripción de la clave y elija una fecha de expiración del menú desplegable de Hola.
5. Seleccione **Guardar**. Un GUID aparece en hello **valor** campo.

  Guardar este valor ahora, como no será capaz de toosee lo nuevo después de cerrar esta ventana.

  ![Creación de una nueva clave](./media/application-proxy-ping-access/create-keys.png)

6. Cierre la hoja de los registros de aplicación Hola o desplácese menú de todos los Hola forma toohello tooreturn izquierdo toohello Azure Active Directory.
7. Seleccione **Propiedades**.
8. Guardar hello **Id. de directorio** GUID.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>(Opcional) campos personalizados de actualización GraphAPI toosend

Para obtener una lista de los tokens de seguridad que Azure AD envía para la autenticación, consulte la [referencia de tokens de Azure AD](./develop/active-directory-token-and-claims.md). Si necesita una demanda personalizada que envía otros tokens, use campos de aplicación Hola de GraphAPI tooset *acceptMappedClaims* demasiado**True**. Puede utilizar el Explorador de Azure AD Graph o MS Graph toomake esta configuración. 

En este ejemplo se usa el Explorador de Graph:

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>Descarga de PingAccess y configuración de la aplicación

Ahora que ha completado todos los pasos de instalación de Azure Active Directory de hello, puede mover en tooconfiguring PingAccess. 

Hello pasos detallados para hello PingAccess parte de este escenario continúan Hola documentación de Ping Identity, [PingAccess configurar para Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).

Estos pasos le guiarán por proceso Hola de obtener una cuenta de PingAccess si aún no tiene uno, instalar hello PingAccess Server y crear una conexión de proveedor de Azure AD OIDC con hello Id. de directorio que copió de hello portal de Azure. A continuación, utilice Hola Id. de aplicación y la clave valores toocreate una sesión Web en PingAccess. Después, puede configurar la asignación de identidades y crear un host virtual, un sitio y una aplicación.

### <a name="test-your-app"></a>Prueba de la aplicación

Cuando haya completado todos los pasos, la aplicación debería estar en funcionamiento. tootest, abra un explorador y navegue toohello dirección URL externa que crea cuando publica la aplicación hello en Azure. Inicie sesión con la cuenta de prueba de hello ese toohello asignado aplicación.

## <a name="next-steps"></a>Pasos siguientes

- [Configuración de PingAccess para Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [¿Cómo permite el proxy de aplicación de Azure AD el inicio de sesión único?](application-proxy-sso-overview.md)
- [Solucionar problemas de Proxy de aplicación](active-directory-application-proxy-troubleshoot.md)
