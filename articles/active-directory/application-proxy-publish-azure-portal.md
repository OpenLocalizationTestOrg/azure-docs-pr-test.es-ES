---
title: "aplicaciones de aaaPublish con el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Publicar en la nube local aplicaciones toohello con el Proxy de aplicación de Azure AD en hello portal de Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publicación de aplicaciones mediante el proxy de aplicación de Azure AD

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Portal de Azure clásico](active-directory-application-proxy-publish.md)

Proxy de aplicación de Azure Active Directory (AD) le ayuda a los trabajadores remotos mediante la publicación de toobe de aplicaciones local tiene acceso a través de hello internet. Puede publicar estas aplicaciones a través de hello tooprovide portal Azure el acceso remoto seguro desde fuera de la red.

Este artículo le guiará a través de hello pasos toopublish una aplicación local con el Proxy de aplicación. Después de completar este artículo, los usuarios le puede tooaccess capaz de la aplicación de forma remota. Podrá tooconfigure listo con características adicionales para la aplicación hello como un único inicio de sesión, información personalizada y requisitos de seguridad.

Si tiene tooApplication nuevo Proxy, obtener más información sobre esta característica con el artículo hello [cómo tooprovide el acceso remoto a aplicaciones locales de tooon](active-directory-application-proxy-get-started.md).


## <a name="publish-an-on-premises-app-for-remote-access"></a>Publicación de una aplicación local para el acceso remoto

Siga estos pasos toopublish sus aplicaciones con Proxy de aplicación. Si ya no ha descargado y ha configurado un conector para su organización, vaya demasiado[empezar a trabajar con el Proxy de aplicación e instalar el conector de hello](active-directory-application-proxy-enable.md) primero y, a continuación, publicar la aplicación.

> [!TIP]
> Si va a probar los Proxy de aplicación para hello primera vez, elija una aplicación que está configurada para autenticación basada en contraseña. Proxy de aplicación es compatible con otros tipos de autenticación, pero en aplicaciones basadas en contraseña son hello tooget más fácil seguridad a trabajar de inmediato. 

1. Inicie sesión como administrador en hello [portal de Azure](https://portal.azure.com/).
2. Seleccione **Azure Active Directory** > **Aplicaciones empresariales** > **Nueva aplicación**.

  ![Adición de una aplicación empresarial](./media/application-proxy-publish-azure-portal/add-app.png)

3. Seleccione **Todo** y, después, seleccione **Aplicación local**.  

  ![Adición de su propia aplicación](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. Proporcionar Hola después de obtener información acerca de la aplicación:

   - **Nombre**: nombre de Hola de aplicación Hola que va a aparecer en el panel de acceso de Hola y Hola portal de Azure. 

   - **Dirección URL interna**: Hola dirección URL que usan la aplicación de hello tooaccess desde dentro de su red privada. Puede proporcionar una ruta de acceso específica de toopublish de servidor de back-end de hello, mientras está sin publicar rest Hola de servidor hello. De esta manera, puede publicar sitios diferentes en Hola el mismo servidor que las diferentes aplicaciones y asigne cada uno de sus propias reglas de acceso y nombre.

     > [!TIP]
     > Si publica una ruta de acceso, asegúrese de que incluye todas las imágenes necesarias de hello, scripts y hojas de estilos para la aplicación. Por ejemplo, si la aplicación está en https://yourapp/app y usa las imágenes que se encuentra en https://yourapp/media, debe publicar https://yourapp/ como ruta de acceso de Hola. Esta dirección URL interna no tiene página de aterrizaje de hello toobe que verán los usuarios. Para más información, consulte [Establecimiento de una página principal personalizada para aplicaciones publicadas mediante el proxy de aplicación de Azure AD](application-proxy-office365-app-launcher.md).

   - **Dirección URL externa**: Hola dirección los usuarios irá tooin orden tooaccess aplicación hello desde fuera de la red. Si no desea dominio de Proxy de aplicación de toouse Hola predeterminado, que conozca [dominios personalizados en el Proxy de aplicación de Azure AD](active-directory-application-proxy-custom-domains.md).
   - **Autenticación previa**: cómo los Proxy de aplicación comprueba los usuarios antes de concederles acceso tooyour aplicación. 

     - Azure Active Directory: Proxy de aplicación redirige toosign de los usuarios con Azure AD, que autentica los permisos para el directorio de Hola y de aplicación. Se recomienda mantener esta opción como valor predeterminado de hello, por lo que puede aprovechar las características de seguridad de Azure AD como acceso condicional y la autenticación multifactor.
     - Acceso directo: Los usuarios no tengan tooauthenticate con aplicaciones de Azure Active Directory tooaccess Hola. Todavía puede configurar los requisitos de autenticación en hello back-end.
   - **Grupo de conectores**: conectores proceso Hola acceso remoto tooyour aplicación y grupos de conectores que le ayudarán a organizar los conectores y las aplicaciones por región, red o propósito. Si no tiene ningún grupo de conector creado todavía, la aplicación se asigna demasiado**predeterminado**.

   ![Configuración de la aplicación](./media/application-proxy-publish-azure-portal/configure-app.png)
5. Si es necesario, configure opciones adicionales. En la mayoría de las aplicaciones, debe mantener esta configuración en su estado predeterminado. 
   - **Tiempo de espera de aplicación de back-end**: establezca este valor demasiado**largo** únicamente si la aplicación es lenta tooauthenticate y conectarse. 
   - **Traducir las direcciones URL en encabezados**: mantener este valor como **Sí** a menos que la aplicación requiere el encabezado de host original de hello en solicitud de autenticación de Hola.
   - **Traducir las direcciones URL en el cuerpo de la aplicación**: mantener este valor como **No** a menos que tienen aplicaciones locales HTML codificado vínculos tooother y no usar dominios personalizados. Para más información, consulte sobre la [traducción de vínculos con el proxy de aplicación](application-proxy-link-translation.md).
   
   ![Configuración de la aplicación](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. Seleccione **Agregar**.


## <a name="add-a-test-user"></a>Adición de un usuario de prueba 

tootest que la aplicación se publicó correctamente, agregue una cuenta de usuario de prueba. Compruebe que esta cuenta ya tiene permisos tooaccess Hola aplicación desde dentro de la red corporativa de Hola.

1. En la hoja de inicio rápido de hello, seleccione **asigna a un usuario para realizar pruebas**.

  ![Asignar un usuario de prueba](./media/application-proxy-publish-azure-portal/assign-user.png)

2. En usuarios de Hola y hoja de grupos, seleccione **agregar**.

  ![Agregar un usuario o grupo](./media/application-proxy-publish-azure-portal/add-user.png)

3. En la hoja de hello Agregar asignación, seleccione **usuarios y grupos** a continuación, elija la cuenta de hello desea tooadd. 
4. Seleccione **Asignar**.

## <a name="test-your-published-app"></a>Prueba de la aplicación publicada

En el explorador, navegue toohello dirección URL externa que configuró durante Hola publicar paso. Debería ver la pantalla de inicio de Hola y ser capaz de toosign con cuenta de prueba de hello configurar.

![Prueba de la aplicación publicada](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a>Pasos siguientes
- [Descargar conectores](active-directory-application-proxy-enable.md) y [crear grupos de conectores](active-directory-application-proxy-connectors-azure-portal.md) toopublish aplicaciones en ubicaciones y redes independientes.

- [Configure el inicio de sesión único](application-proxy-sso-azure-portal.md) para la aplicación publicada recientemente.
