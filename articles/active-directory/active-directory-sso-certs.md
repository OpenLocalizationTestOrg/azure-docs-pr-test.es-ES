---
title: "certificados de federación aaaManage en Azure AD | Documentos de Microsoft"
description: "Obtenga información acerca de la fecha de expiración de hello toocustomize para los certificados de federación y cómo toorenew certificados que caducará pronto."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Administrar certificados para inicio de sesión único federado en Azure Active Directory
Este artículo tratan las preguntas más frecuentes e información relacionada con certificados toohello que Azure Active Directory (Azure AD) crea tooestablish federado single sign-on (SSO) tooyour aplicaciones SaaS. Agregar aplicaciones desde la Galería de aplicaciones de Azure AD de Hola o mediante una plantilla de aplicación distinta de la galería. Configurar aplicación hello con opción de SSO de hello federado.

Este artículo es relevante tooapps solo que son toouse configurado Azure AD SSO a través de federación de SAML, tal y como se muestra en el siguiente ejemplo de Hola:

![Inicio de sesión único de Azure AD ](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Generación automática de certificado para aplicaciones de la galería y ajenas a la misma
Al agregar una nueva aplicación de galería de Hola y configurar una inicio de sesión en basado en SAML, Azure AD genera un certificado para la aplicación de Hola que es válida durante tres años. Puede descargar este certificado de hello **el certificado de firma de SAML** sección. Para las aplicaciones de la galería, esta sección podría mostrar un certificado de opción toodownload Hola o metadatos, en función de los requisitos de Hola de aplicación hello.

![Inicio de sesión único de Azure AD](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>Personalizar la fecha de expiración de hello para el certificado de la federación y ponerla en un nuevo certificado tooa
De forma predeterminada, los certificados se establecen tooexpire después de tres años. Puede elegir una fecha de caducidad diferentes para el certificado siguiendo los pasos de Hola.
capturas de pantalla de Hello usan Salesforce para simplificar ejemplo hello, pero estos pasos pueden aplicar la aplicación de SaaS tooany federado.

1. Hola [portal de Azure](https://aad.portal.azure.com), haga clic en **aplicación empresarial** en Hola panel izquierdo y, a continuación, haga clic en **nueva aplicación** en hello **Introducción** página:

   ![Asistente para configuración de SSO de hello abierto](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Busque la aplicación de la Galería de hello y, a continuación, seleccione aplicación hello que desea tooadd. Si no se encuentra la aplicación hello necesario, Agregar aplicación hello mediante hello **aplicación gallery no** opción. Esta característica solo está disponible en hello SKU de Azure AD Premium (P1 y P2).

    ![Inicio de sesión único de Azure AD](./media/active-directory-sso-certs/add_gallery_application.png)

3. Haga clic en hello **inicio de sesión único** vínculo Hola panel y cambio de apertura **modo de inicio de sesión único** demasiado**sesión basado en SAML**. Este paso genera un certificado de tres años para la aplicación.

4. toocreate un nuevo certificado, haga clic en hello **crear un nuevo certificado** vínculo Hola **el certificado de firma de SAML** sección.

    ![Generar un certificado nuevo](./media/active-directory-sso-certs/create_new_certficate.png)

5. Hola **crear un nuevo certificado** vínculo abre el control de calendario Hola. Puede establecer cualquier fecha y hora toothree años de hello fecha actual. Hola seleccionado Fecha y hora es nueva fecha de expiración de Hola y la hora de su certificado nuevo. Haga clic en **Guardar**.

    ![Descargar, a continuación, cargar el certificado de Hola](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. Ahora Hola nuevo certificado es toodownload disponible. Haga clic en hello **certificado** toodownload de vínculo se. En este momento, el certificado no está activo. Si desea tooroll sobre toothis certificado, seleccione hello **activar el nuevo certificado** casilla de verificación y haga clic en **guardar**. Desde ese punto, Azure AD inicia con hello nuevo certificado de firma de respuesta de Hola.

7.  toolearn cómo hello tooupload certificado tooyour aplicación de SaaS concreta, haga clic en hello **tutorial de configuración de aplicación de vista** vínculo.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Renovar un certificado que expirará pronto
Hello renovación pasos deben producir ningún tiempo de inactividad significativo para los usuarios. capturas de pantalla de Hello en esta característica de sección Salesforce como un ejemplo, pero estos pasos pueden aplicar la aplicación de SaaS tooany federado.

1. En hello **Azure Active Directory** aplicación **inicio de sesión único** página, generar Hola nuevo certificado para su aplicación. Puede hacerlo haciendo clic en hello **crear un nuevo certificado** vínculo Hola **el certificado de firma de SAML** sección.

    ![Generar un certificado nuevo](./media/active-directory-sso-certs/create_new_certficate.png)

2. Seleccione Hola deseado fecha de expiración y la hora para el nuevo certificado y haga clic en **guardar**.

3. Descargar certificado de Hola Hola **certificado de firma de SAML** opción. Pantalla de configuración de inicio de sesión único de carga Hola certificado toohello SaaS la nueva aplicación. toolearn cómo toodo esto para su aplicación SaaS en particular, haga clic en hello **tutorial de configuración de aplicación de vista** vínculo.
   
4. nuevo certificado en Azure AD, seleccione Hola de Hola de tooactivate **activar el nuevo certificado** casilla de verificación y haga clic en hello **guardar** situado en la parte superior de Hola de página de Hola. Esta acción pone a través de un nuevo certificado hello en hello lado de Azure AD. Hola estado del certificado de hello cambia de **New** demasiado**Active**. Desde ese punto, Azure AD inicia con hello nuevo certificado de firma de respuesta de Hola. 
   
    ![Generar un certificado nuevo](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>Artículos relacionados
* [Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Solución de problemas de inicio de sesión único basado en SAML](active-directory-saml-debugging.md)
