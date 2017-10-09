---
title: "aaaCustomize el inicio de sesión en la página en hello Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd una página de toohello inicio de sesión Azure de personalización de marca de empresa"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Agregar marcas tooyour página de inicio de sesión en hello Azure Active Directory de empresa
tooavoid confusión, muchas compañías desean tooapply una apariencia coherente en todos los sitios Web de Hola y servicios que administran. Azure Active Directory ofrece esta funcionalidad permitiéndole apariencia de hello toocustomize de página de inicio de sesión de hello con el logotipo de la compañía y combinaciones de colores personalizadas. página de inicio de sesión de Hello es la página de Hola que aparece al iniciar sesión en tooOffice 365 u otras aplicaciones basadas en web que usan Azure AD como proveedor de identidades. Interactuar con este tooenter página sus credenciales.

Si desea que tooshow su marca de empresa, colores y otros elementos personalizables en esta página, vea Hola después imágenes toounderstand Hola diferenciar dos experiencias de Hola.

Hola siguiente captura de pantalla muestra y ejemplo de página de inicio de sesión de hello Office 365 en un equipo de escritorio **antes de** una personalización:

![Página de inicio de sesión de Office 365 antes de la personalización](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Hola siguiente captura de pantalla muestra y ejemplo de página de inicio de sesión de hello Office 365 en un equipo de escritorio **después** una personalización:

![Página de inicio de sesión de Office 365 después de la personalización](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Personalizar la página de inicio de sesión de Hola
Por lo general, si tiene aplicaciones de acceso basado en explorador tooyour en la nube y los servicios que su organización se suscribe a, utilice página de inicio de sesión de Hola.

Si ha aplicado la página de inicio de sesión de tooyour de cambios, puede tardar una hora tooan Hola cambios tooappear.

Las páginas de inicio de sesión con marca solamente aparecen cuando se visita un servicio con una dirección URL específica del inquilino, como https://outlook.com/**contoso**.com o https://mail.**contoso**.com.

Si visita un servicio con direcciones URL que no son específicas de un inquilino (por ejemplo, https://mail.office365.com), aparece una página de inicio de sesión sin marca. En este caso, la marca solamente aparecerá una vez que haya especificado el identificador de usuario o haya seleccionado un icono de usuario.

> [!NOTE]
> * El nombre de dominio debe aparecer como "Activo" Hola **dominios** parte de Hola portal de Azure en el que se ha configurado la marca. Para más información, consulte [cómo agregar nombres de dominio personalizados](active-directory-domains-add-azure-portal.md).
> * Personalización de la página de inicio de sesión no dirige toohello consumidor inicio de sesión en la página de Microsoft. Si inicia sesión con una cuenta de Microsoft, puede ver una lista con marca de mosaicos de los usuarios presentada por Azure AD, pero Hola la marca de su organización no aplicará toohello página de inicio de sesión de cuenta de Microsoft.
>
>

En la página de inicio de sesión, Hola **mantener la sesión iniciada** casilla permite un tooremain usuario inicie sesión cuando cierre y vuelva a abre su explorador.

   ![Mantener la sesión iniciada](./media/active-directory-branding-custom-signon-azure-portal/01.png)

No afecta a la duración de la sesión. Puede ocultar Hola casilla en la página de inicio de sesión de Azure Active Directory de Hola.
Si se muestra la casilla de verificación de hello depende de la configuración de Hola de **mantener la sesión iniciada en deshabilitado**.

   ![Mantener la sesión iniciada](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide Hola casilla, configure esta opción demasiado**Sí**.

> [!NOTE]
> Algunas características de SharePoint Online y Office 2010 dependen de los usuarios que están toocheck capaz de este cuadro. Si configura esta toohidden de configuración, los usuarios pueden ver mensajes adicionales e inesperadas en toosign.
>
>

**tooadd marca tooyour directorio de la empresa:**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

   ![Apertura de Administración de usuarios](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. En hello **usuarios y grupos** hoja, seleccione **información de marca**.
4. En hello **a los usuarios y grupos: personalización de marca de empresa** hoja, seleccione hello **editar** comando.

    ![Edición de la personalización de marca](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modificar elementos de hello desea toocustomize. Todos los elementos son opcionales.
6. Haga clic en **Guardar**.

Puede tardar hasta hora tooan para cualquier cambio realizado toohello inicio de sesión página tooappear personalización de marca.

## <a name="next-steps"></a>Pasos siguientes
[Agregar información de marca de empresa específica de un idioma](active-directory-branding-localize-azure-portal.md)
