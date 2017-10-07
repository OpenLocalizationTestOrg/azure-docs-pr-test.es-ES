---
title: "aaaCustomize el inicio de sesión en la página en hello Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd una página de toohello inicio de sesión Azure de personalización de marca de empresa"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a>Inicio rápido: Agregar marcas tooyour página de inicio de sesión en Azure AD de empresa
tooavoid confusión, muchas compañías desean tooapply una apariencia coherente en todos los sitios Web de Hola y servicios que administran. Azure Active Directory (Azure AD) proporciona esta capacidad, ya que permite la apariencia de hello toocustomize de página de inicio de sesión de hello con el logotipo de la compañía y combinaciones de colores personalizadas. página de inicio de sesión de Hello es la página de Hola que aparece al iniciar sesión en tooOffice 365 u otras aplicaciones basadas en web que usan Azure AD como proveedor de identidades. Interactuar con este tooenter página sus credenciales.

> [!NOTE]
> * Marcas de empresa solo está disponible si ha actualizado toohello Premium o edición básica de Azure AD, o tener una licencia de Office 365. toolearn si una característica es compatible con el tipo de licencia, compruebe hello [página de información de precios de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).
> 
> * Azure Active Directory Premium y básicas ediciones están disponibles para los clientes de China mediante Hola instancia internacional de Azure Active Directory. Azure Active Directory Premium y las ediciones básicas no se admiten actualmente en el servicio de Microsoft Azure Hola operado por 21Vianet en China. Para obtener más información, póngase en contacto con nosotros en hello [foro de Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).

## <a name="customizing-hello-sign-in-page"></a>Personalizar la página de inicio de sesión de Hola

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

Empresa las personalizaciones de marca aparecen en la página de inicio de sesión de hello Azure AD cuando los usuarios tienen acceso a una dirección URL específica del inquilino como [ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com).

Cuando los usuarios visiten una URL genérica como www.office.com, página de inicio de sesión de hello no contiene marcas personalizaciones porque el sistema de hello no sabe quién es el usuario de Hola de empresa. La marca de la empresa aparecerá una vez que los usuarios escriban su id. de usuario o seleccionen un icono de usuario.

> [!NOTE]
> * El nombre de dominio debe aparecer como "Activo" Hola **dominios** parte de Hola portal de Azure en el que se ha configurado la marca. Para más información, vea [Incorporación de un nombre de dominio personalizado](add-custom-domain.md).
> * Personalización de la página de inicio de sesión no dirige toohello página de inicio de sesión para cuentas de Microsoft personales. Si los empleados o invitados de negocio iniciar sesión con una cuenta Microsoft personal, su página de inicio de sesión no refleja Hola personalización de marca de su organización.


### <a name="banner-logo"></a>Logotipo del banner 

Descripción | Restricciones | Recomendaciones
------- | ------- | ----------
logotipo del banner Hola se muestra en el inicio de sesión de Hola y páginas de panel de acceso de Hola.<br>En la página de inicio de sesión hello, esto muestra una vez que se determina la organización del usuario de hello, normalmente después de que se incluye el nombre de usuario de Hola.  | JPG o PNG transparente<br>Alto máximo: 36 px<br>Ancho máximo: 245 px | Use el logotipo de su organización aquí.<br>Use una imagen transparente. No suponga que el fondo de hello estará en blanco.<br>No agrega relleno alrededor de su logotipo en la imagen de Hola o su logotipo tendrá un aspecto desproporcionadamente pequeño.

### <a name="username-hint"></a>Sugerencia de nombre de usuario   
Descripción | Restricciones | Recomendaciones
------- | ------- | ----------
Personaliza el texto de sugerencia de hello en el campo de nombre de usuario de Hola. | Texto Unicode too64 caracteres<br>Solo texto sin formato | Se recomienda no establecer este valor si espera que los usuarios invitados fuera de su toosign de organización en la aplicación tooyour.
            
### <a name="sign-in-page-text"></a>Texto de la página de inicio de sesión   
Descripción | Restricciones | Recomendaciones
------- | ------- | ----------
Esto aparece en parte inferior de hello del formulario de inicio de sesión de Hola y puede ser usado toocommunicate información adicional como departamento de soporte de número de teléfono de hello tooyour o una declaración legal. | Texto Unicode too256 caracteres<br>Solo texto sin formato (sin vínculos ni etiquetas HTML) 

### <a name="sign-in-page-image"></a>Imagen de la página de inicio de sesión  
Descripción | Restricciones | Recomendaciones
------- | ------- | ----------
Esto aparece en segundo plano de Hola de página de inicio de sesión hello, es toohello anclado centro de espacio visible de hello y se escale y recortar toofill ventana del explorador Hola.  <br>En las pantallas estrechas, como las de teléfonos móviles, no se muestra esta imagen.<br>Una máscara de color negra con opacidad 0,55 se aplicará sobre esta imagen en el código cuando se carga la página de Hola. | JPG o PNG<br>Dimensiones de la imagen: 1920 x 1080 px<br>Tamaño de archivo: &gt; 300 KB | <br>Use imágenes allí donde no haya un enfoque del asunto sólido. el formulario de inicio de sesión opaco de Hello aparece sobre center Hola de esta imagen y puede cubrir cualquier parte de la imagen de hello según tamaño Hola de ventana del explorador de Hola.<br>Mantener el tamaño del archivo de hello tan pequeño como tiempos de carga rápida de tooensure posible. 

### <a name="background-color"></a>Color de fondo
Descripción | Restricciones | Recomendaciones
------- | ------- | ----------
Este color se utiliza en lugar de la imagen de fondo de hello en conexiones de ancho de banda bajo. |   Color RGB en formato hexadecimal (ejemplo: #FFFFFF) | Se recomienda utilizar el color principal de hello del logotipo del banner Hola o su organización.

### <a name="show-option-tooremain-signed-in"></a>Mostrar opción tooremain iniciado sesión
Descripción | Restricciones | Recomendaciones
------- | ------- | ----------
Inicio de sesión de AD de Azure en proporciona Hola usuario Hola opción tooremain iniciado sesión cuando cierre y vuelva a abre su explorador. Utilice este toohide esa opción.<br>Establezca esta demasiado "No" toohide esta opción de los usuarios. | &nbsp; | No afecta a la duración de la sesión.<br>Algunas características de SharePoint Online y Office 2010 dependen de los usuarios que están tooremain toochoose capaz de sesión. Si establece este toobe oculta, los usuarios pueden ver mensajes adicionales e inesperadas en toosign.

> [!NOTE]
> Todos los elementos son opcionales. Por ejemplo, si especifica un logotipo del banner con ninguna imagen de fondo, página de inicio de sesión de hello mostrará la imagen de fondo del logotipo y hello para el sitio de destino de hello (por ejemplo, Office 365).

## <a name="add-company-branding-tooyour-directory"></a>Agregar marcas tooyour directorio de empresa

1. Inicie sesión en demasiado[Hola portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

   ![Apertura de Administración de usuarios](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. En hello **usuarios y grupos** hoja, seleccione **información de marca**.
4. En hello **a los usuarios y grupos: personalización de marca de empresa** hoja, seleccione hello **editar** comando.

    ![Edición de la personalización de marca](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Modificar elementos de hello desea toocustomize. Todos los elementos son opcionales.
6. Haga clic en **Guardar**.

Puede tardar hasta hora tooan para cualquier cambio realizado toohello inicio de sesión página tooappear personalización de marca.

## <a name="add-language-specific-company-branding-tooyour-directory"></a>Agregar marcas tooyour directorio de empresa específicas de idioma

1. Inicie sesión en toohello [centro de administración de Azure AD](https://aad.portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

   ![Apertura de Administración de usuarios](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. En hello **usuarios y grupos** hoja, seleccione **información de marca**.
4. En hello **a los usuarios y grupos: personalización de marca de empresa** hoja, seleccione hello **Agregar idioma** comando.

    ![Adición de elementos de personalización de marca específicos del idioma](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. Modificar elementos de hello desea toocustomize. Todos los elementos son opcionales.
6. Haga clic en **Guardar**.

Puede tardar hasta hora tooan para cualquier cambio realizado toohello inicio de sesión página tooappear personalización de marca.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo tooadd empresa marca directory tooyour Azure AD. 

Puede usar Hola siguiendo el vínculo tooconfigure su marcas en Azure AD de hello Azure portal de empresa.

> [!div class="nextstepaction"]
> [Configuración de la personalización de marca de la compañía](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 