---
title: "aplicaciones de aaaPublish con el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Publicación en la nube local aplicaciones toohello con el Proxy de aplicación de Azure AD en el portal clásico de Hola."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7926998314c65521ae48aebcceb33cb0c67e0b87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a>Publicación de aplicaciones mediante el proxy de aplicación de Azure AD

> [!div class="op_single_selector"]
> * [Azure Portal](application-proxy-publish-azure-portal.md)
> * [Portal de Azure clásico](active-directory-application-proxy-publish.md)

El Proxy de aplicación de Azure AD le ayuda a los trabajadores remotos mediante la publicación de toobe de aplicaciones local tiene acceso a través de hello internet. Hasta este momento, debe tener ya [habilitado Proxy de aplicación de portal de Azure clásico de Hola](active-directory-application-proxy-enable.md). Este artículo le guía a través de aplicaciones toopublish de hello pasos que se ejecutan en la red local y proporcionar acceso remoto seguro desde fuera de la red. Después de completar este artículo, le aplicación de hello tooconfigure listo con requisitos de seguridad o la información personalizada.

> [!NOTE]
> Proxy de aplicación es una característica que solo está disponible si ha actualizado toohello Premium o edición básica de Azure Active Directory. Para obtener más información, consulte [Ediciones de Azure Active Directory](active-directory-editions.md). Si desea toouse Proxy de aplicación, puede [publicar aplicaciones de portal de Azure hello](application-proxy-publish-azure-portal.md).

## <a name="publish-an-app-using-hello-wizard"></a>Publicar una aplicación mediante el Asistente de Hola
1. Inicie sesión como administrador en hello [portal de Azure clásico](https://manage.windowsazure.com/).
2. Vaya tooActive Directory y active directory Hola donde haya habilitado el Proxy de aplicación.
   
    ![Active Directory (icono)](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Haga clic en hello **aplicaciones** ficha y, a continuación, haga clic en hello **agregar** situado en la parte inferior de Hola de pantalla de bienvenida
   
    ![Agregar aplicación](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Seleccione **Publicar una aplicación que estará accesible desde fuera de la red**.
   
    ![Publicar una aplicación que estará accesible desde fuera de la red](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Proporcionar Hola después de obtener información acerca de la aplicación:
   
   * **Nombre**: nombre descriptivo de hello para la aplicación. Debe ser único en el directorio.
   * **Dirección URL interna**: dirección de Hola que Hola conector del Proxy de aplicación usa la aplicación de hello tooaccess desde dentro de su red privada. Puede proporcionar una ruta de acceso específica de toopublish de servidor de back-end de hello, mientras está sin publicar rest Hola de servidor hello. De esta manera, puede publicar sitios diferentes en Hola el mismo servidor y proporcionar a cada uno de sus propias reglas de acceso y nombre.
     
     > [!TIP]
     > Si publica una ruta de acceso, asegúrese de que incluye todas las imágenes necesarias de hello, scripts y hojas de estilos para la aplicación. Por ejemplo, si la aplicación está en https://yourapp/app y usa las imágenes que se encuentra en https://yourapp/media, debe publicar https://yourapp/ como ruta de acceso de Hola.
     > 
     > 
   * **Método de autenticación previa**: cómo los Proxy de aplicación comprueba los usuarios antes de concederles acceso tooyour aplicación. Elija una de las opciones de Hola desde el menú desplegable de Hola.
     
     * Azure Active Directory: Proxy de aplicación redirige toosign de los usuarios con Azure AD, que autentica los permisos para el directorio de Hola y de aplicación.
     * Acceso directo: Los usuarios no tengan aplicación hello de tooauthenticate tooaccess.
     
     ![Propiedades de la aplicación](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. Asistente de hello toofinish, haga clic en la marca de verificación de hello en parte inferior de Hola de pantalla de bienvenida. Ahora está definida por la aplicación Hello en Azure AD.

## <a name="assign-users-and-groups-toohello-application"></a>Asignar usuarios y grupos de aplicación toohello
En orden para los usuarios tooaccess la aplicación publicada, deberá tooassign ellos individualmente o en grupos. (Recuerde tooassign usted mismo acceso demasiado.) Cada usuario que asigna necesita una licencia para Azure básico o superior. Puede asignar licencias individualmente o toogroups. Para obtener más información, consulte [asignar usuarios de aplicación de tooan](active-directory-applications-guiding-developers-assigning-users.md). 

Para las aplicaciones que requieren autenticación previa, se asigna a un usuario concede aplicación hello de toouse de permiso. Para las aplicaciones que no requieren autenticación previa, se asigna a un usuario significa que ese usuario Hola puede tener acceso a la aplicación hello a través del panel de acceso de Hola.

1. Una vez acabado asistente Agregar aplicación de hello, vea Hola inicio rápido de página de la aplicación. toomanage que tenga acceso toohello aplicación, seleccione **usuarios y grupos**.
   
    ![Asignación de usuarios en el inicio rápido del proxy de la aplicación (captura de pantalla)](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Busque grupos específicos en el directorio o muestre todos los usuarios. resultados de búsqueda de toodisplay hello, haga clic en la marca de verificación de Hola.
   
      ![Buscar grupos o usuarios (captura de pantalla)](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Seleccione cada usuario o grupo que desee tooassign toothis aplicación y haga clic en **asignar**. Es más frecuentes tooconfirm esta acción.

> [!NOTE]
> En el caso de las aplicaciones de autenticación integrada de Windows, solo puede asignar aquellos usuarios y grupos que se sincronizan desde la versión local de Active Directory. A los usuarios que inicien sesión con una cuenta de Microsoft y a los invitados no se les pueden asignar aplicaciones publicadas con el proxy de aplicación de Azure Active Directory. Asegúrese de que los usuarios iniciar sesión con credenciales que forman parte del programa Hola mismo dominio que la aplicación hello va a publicar.
> 
> 

## <a name="test-your-published-application"></a>Prueba de la aplicación publicada
Una vez que ha publicado la aplicación, puede probar horizontal desplazándose toohello URL que se publicó. Asegúrese de que puede acceder a ella, que se representa correctamente y que todo funciona como cabría esperar. Si tiene dificultades al o aparece un mensaje de error, intente hello [Guía de solución de problemas](active-directory-application-proxy-troubleshoot.md).

## <a name="configure-your-application"></a>Configuración de la aplicación
Puede modificar las aplicaciones publicadas o configurar opciones avanzadas en la página de configuración de Hola. En esta página, puede personalizar su aplicación cambiando el nombre de Hola o cargar un logotipo. También puede administrar las reglas de acceso como Hola método de autenticación previa o la autenticación multifactor.

![Configuración avanzada](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Después de publicar aplicaciones mediante Azure aplicación Proxy de Active Directory, que aparecen en la lista de aplicaciones de hello en Azure AD y se pueden administrar.

Si deshabilita los servicios de Proxy de aplicación después de publicar aplicaciones, aplicaciones de hello dejan de estar accesibles desde fuera de su red privada. Los usuarios todavía pueden acceso Hola aplicaciones locales como de costumbre.

tooview una aplicación y asegúrese de que está seguro de que sea accesible, haga doble clic en el nombre de Hola de aplicación hello. Si se deshabilita el servicio Proxy de aplicación Hola y aplicación hello no está disponible, aparece un mensaje de advertencia en la parte superior de Hola de pantalla de bienvenida.

toodelete una aplicación, seleccione una aplicación en la lista de hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes
* [Publicar aplicaciones mediante su propio nombre de dominio](active-directory-application-proxy-custom-domains.md)
* [Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md)
* [Habilitar el acceso condicional](active-directory-application-proxy-conditional-access.md)
* [Trabajar con las aplicaciones para notificaciones](active-directory-application-proxy-claims-aware-apps.md)

Para obtener las actualizaciones y noticias más recientes de hello, visite hello [blog de Proxy de aplicación](http://blogs.technet.com/b/applicationproxyblog/)

