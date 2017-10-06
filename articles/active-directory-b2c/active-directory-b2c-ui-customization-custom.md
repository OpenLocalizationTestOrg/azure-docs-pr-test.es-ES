---
title: "Personalización de la interfaz de usuario con directivas personalizadas - Azure AD B2C | Microsoft Docs"
description: "Información acerca de cómo personalizar una interfaz de usuario (IU) con directivas personalizadas en Azure AD B2C."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Azure Active Directory B2C: configuración de la interfaz de usuario personalizada en una directiva personalizada

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Después de completar este artículo, tendrá una directiva personalizada de registro e inicio de sesión con su marca y apariencia. Con Azure Active Directory B2C (Azure AD B2C), obtendrá control casi lleno de contenido HTML y CSS de Hola que ha presentado toousers. Cuando se usa una directiva personalizada, configure personalización de la interfaz de usuario en XML en lugar de utilizar controles Hola portal de Azure. 

## <a name="prerequisites"></a>Requisitos previos

Antes de continuar, lea el artículo de [introducción a las directivas personalizadas](active-directory-b2c-get-started-custom.md). Debe tener una directiva personalizada activa para registrar e iniciar sesión de cuentas locales.

## <a name="page-ui-customization"></a>Personalización de la interfaz de usuario de la página

Mediante la característica de personalización de interfaz de usuario de hello página, puede personalizar Hola apariencia y comportamiento de cualquier directiva personalizada. También puede mantener la coherencia visual y de la marca entre la aplicación y Azure AD B2C.

Funciona de la siguiente manera: Azure AD B2C ejecuta código en el explorador del consumidor y usa un enfoque moderno denominado [Uso compartido de recursos entre orígenes (CORS)](http://www.w3.org/TR/cors/). En primer lugar, especifique una dirección URL de la directiva personalizada de hello con contenido HTML personalizado. Azure AD B2C combina elementos de interfaz de usuario con contenido HTML que se carga desde la dirección URL y, a continuación, se muestra al cliente toohello de página de Hola Hola.

## <a name="create-your-html5-content"></a>Creación de contenido HTML5

Crear contenido con el nombre de la marca de su producto HTML en el título de Hola.

1. Copie Hola siguiente fragmento de HTML. Está bien formado HTML5 con un elemento vacío denominado  *\<div id = "api"\>\</div\>*  ubicados en hello  *\<cuerpo\>*  etiquetas. Este elemento indica la ubicación contenido de Azure AD B2C toobe insertado.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >Por motivos de seguridad, uso de Hola de JavaScript está bloqueada actualmente para la personalización.

2. Pegue el fragmento de código de hello copiado en un editor de texto y, a continuación, guarde el archivo hello como *ui.html personalizar*.

## <a name="create-an-azure-blob-storage-account"></a>Creación de una cuenta de Almacenamiento de blobs de Azure

>[!NOTE]
> En este artículo, utilizamos toohost de almacenamiento de blobs de Azure nuestro contenido. Puede elegir toohost su contenido en un servidor web, pero deberá [habilitar CORS en el servidor web](https://enable-cors.org/server.html).

toohost este contenido HTML en el almacenamiento de blobs, Hola siguientes:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En hello **concentrador** menú, seleccione **New** > **almacenamiento** > **cuenta de almacenamiento**.
3. Escriba un **Nombre** único para la cuenta de almacenamiento.
4. El **Modelo de implementación** puede permanecer como **Resource Manager**.
5. Cambio **tipo de cuenta** demasiado**almacenamiento de blobs**.
6. El **Rendimiento** puede permanecer como **Estándar**.
7. La **Replicación** puede permanecer como **RA-GRS**.
8. El **Nivel de acceso** puede permanecer **Activo**.
9. El **Cifrado del servicio de almacenamiento** puede permanecer **Deshabilitado**.
10. Seleccione una **Suscripción** para la cuenta de almacenamiento.
11. Cree un **Grupo de recursos** o seleccione uno existente.
12. Seleccione hello **ubicación geográfica** para su cuenta de almacenamiento.
13. Haga clic en **crear** cuenta de almacenamiento de toocreate Hola.  
    Una vez completada la implementación de hello, Hola **cuenta de almacenamiento** hoja se abre automáticamente.

## <a name="create-a-container"></a>Crear un contenedor

toocreate un contenedor público en el almacenamiento de blobs, Hola siguientes:

1. Haga clic en hello **Introducción** ficha.
2. Haga clic en **Contenedor**.
3. En **Nombre**, escriba **$root**.
4. Establecer **tipo de acceso** demasiado**Blob**.
5. Haga clic en **$root** nuevo contenedor de tooopen Hola.
6. Haga clic en **Cargar**.
7. Haga clic en el icono de carpeta de hello siguiente demasiado**seleccionar un archivo**.
8. Vaya demasiado**ui.html personalizar**, que creó anteriormente en hello [personalización Page UI](#the-page-ui-customization-feature) sección.
9. Haga clic en **Cargar**.
10. Seleccione los blobs de ui.html personalizar Hola que se cargan.
11. Siguiente demasiado**URL**, haga clic en **copia**.
12. En un explorador, Hola pegar copia dirección URL y vaya toohello sitio. Si el sitio de hello es inaccesible, asegúrese de que tipo de acceso de contenedor de Hola se establece demasiado**blob**.

## <a name="configure-cors"></a>Configuración de CORS

Configurar el almacenamiento de blobs para uso compartido de recursos entre orígenes haciendo Hola siguiente:

>[!NOTE]
>¿Deseado tootry característica de personalización de interfaz de usuario de hello mediante nuestro contenido HTML y CSS de ejemplo? Proporcionamos [una herramienta auxiliar sencilla](active-directory-b2c-reference-ui-customization-helper-tool.md) que carga y configura el contenido de ejemplo en la cuenta de Blob Storage. Si utiliza la herramienta de hello, pasar demasiado[modificar la directiva personalizada de registro o inicio de sesión](#modify-your-sign-up-or-sign-in-custom-policy).

1. En hello **almacenamiento** hoja, en **configuración**, abra **CORS**.
2. Haga clic en **Agregar**.
3. Para los **Orígenes permitidos**, escriba un asterisco (\*).
4. Hola **verbos permitidos** lista desplegable, seleccione **obtener** y **opciones**.
5. Para los **Encabezados permitidos**, escriba un asterisco (\*).
6. Para los **Encabezados expuestos**, escriba un asterisco (\*).
7. Para **Antigüedad máxima (segundos)**, escriba **200**.
8. Haga clic en **Agregar**.

## <a name="test-cors"></a>Prueba de CORS

Validar que está listo haciendo Hola siguiente:

1. Vaya toohello [prueba cors.org](http://test-cors.org/) sitio Web y, a continuación, pegar Hola URL Hola **dirección URL remota** cuadro.
2. Haga clic en **Send Request** (Enviar solicitud).  
    Si recibe un error, asegúrese de que la [configuración de CORS](#configure-cors) sea correcta. También, tal vez necesite tooclear la memoria caché del explorador o abrir una sesión de exploración privada presionando Ctrl + Mayús + P.

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>Modificación de la directiva de inicio de sesión o de registro

En el nivel superior de hello  *\<TrustFrameworkPolicy\>*  etiqueta, debería encontrar  *\<BuildingBlocks\>*  etiqueta. Dentro de hello  *\<BuildingBlocks\>*  etiquetas, agregue un  *\<ContentDefinitions\>*  etiqueta copiando el siguiente ejemplo de Hola. Reemplace *your_storage_account* con el nombre de saludo de la cuenta de almacenamiento.

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>Carga de la directiva personalizada actualizada

1. Hola [portal de Azure](https://portal.azure.com), [cambiar al contexto de Hola de su inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)y, a continuación, abra hello **Azure AD B2C** hoja.
2. Haga clic en **Todas las directivas**.
3. Haga clic en **Cargar directiva**.
4. Cargar `SignUpOrSignin.xml` con hello  *\<ContentDefinitions\>*  etiqueta que agregó anteriormente.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Probar directiva personalizada de hello mediante **ejecutar ahora**

1. En hello **Azure AD B2C** hoja, vaya demasiado**todas las directivas de**.
2. Active la directiva personalizada hello que ha cargado y haga clic en hello **ejecutar ahora** botón.
3. Debe ser capaz de toosign seguridad mediante una dirección de correo electrónico.

## <a name="reference"></a>Referencia

Aquí encontrará plantillas de ejemplo de personalización de interfaz de usuario:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

carpeta de Hello sample_templates/wingtip contiene Hola siguientes archivos HTML:

| Plantilla HTML5 | Descripción |
|----------------|-------------|
| *phonefactor.html* | Use este archivo como plantilla para una página de autenticación multifactor. |
| *resetpassword.html* | Use este archivo como plantilla para una página de recuperación de contraseña. |
| *selfasserted.html* | Use este archivo como plantilla para una página de registro en una cuenta social, una página de registro en una cuenta local o una página de inicio de sesión en una cuenta local. |
| *unified.html* | Use este archivo como plantilla para una página de inicio de sesión o registro unificada. |
| *updateprofile.html* | Use este archivo como plantilla para una página de actualización de perfil. |

Hola [modificar la sección de directiva personalizada de registro o inicio de sesión](#modify-your-sign-up-or-sign-in-custom-policy), ha configurado la definición de contenido de Hola para `api.idpselections`. Hola completa de identificadores que son reconocidos por el marco de trabajo de hello Azure AD B2C identidad experiencia y sus descripciones de definición de contenido están en hello en la tabla siguiente:

| Id. de definición de contenido | Descripción | 
|-----------------------|-------------|
| *api.error* | **Página de error**. Esta página se muestra cuando se produce una excepción o un error. |
| *api.idpselections* | **Página de selección del proveedor de identidades**. Esta página contiene una lista de proveedores que Hola usuario pueden elegir entre durante el inicio de sesión de identidad. Estas opciones son proveedores de identidades de empresa, proveedores de identidades sociales como Facebook y Google+ o cuentas locales. |
| *api.idpselections.signup* | **Selección del proveedor de identidades para el registro**. Esta página contiene una lista de proveedores que Hola usuario pueden elegir al realizar el registro de identidad. Estas opciones son proveedores de identidades de empresa, proveedores de identidades sociales como Facebook y Google+ o cuentas locales. |
| *api.localaccountpasswordreset* | **Página de contraseña olvidada**. Esta página contiene un formulario de ese usuario Hola debe completar tooinitiate un restablecimiento de contraseña.  |
| *api.localaccountsignin* | **Página de inicio de sesión en una cuenta local**. Esta página contiene un formulario de registro con una cuenta local basada en una dirección de correo electrónico o un nombre de usuario. Hola formulario puede contener un cuadro de entrada de texto y un cuadro de entrada de contraseña. |
| *api.localaccountsignup* | **Página de registro en una cuenta local**. Esta página contiene un formulario de registro para una cuenta local basada en una dirección de correo electrónico o un nombre de usuario. formulario de Hello puede contener varios controles de entrada, como un cuadro de entrada de texto, un cuadro de entrada de contraseña, un botón de radio, cuadros de lista desplegable de selección única y casillas de verificación de selección múltiple. |
| *api.phonefactor* | **Página de autenticación multifactor**. Esta página permite a los usuarios verificar sus números de teléfono (mediante texto o voz) durante el registro o el inicio de sesión. |
| *api.selfasserted* | **Página de registro en una cuenta social**. Esta página contiene un formulario de registro que los usuarios tienen que rellenar al registrarse con una cuenta existente de un proveedor de identidades social, como Facebook o Google+. Esta página es similar toohello anterior página de inicio de sesión de cuenta sociales, salvo los campos de entrada de contraseña de Hola. |
| *api.selfasserted.profileupdate* | **Página de actualización de perfil**. Esta página contiene un formulario que los usuarios pueden usar tooupdate su perfil. Esta página es similar toohello sociales página cuenta de inicio de sesión, salvo los campos de entrada de contraseña de Hola. |
| *api.signuporsignin* | **Página de inicio de sesión o registro unificada**. Esta página controla ambos Hola registrarse e iniciar sesión de usuarios, que pueden usar proveedores de identidades de empresa, proveedores de identidades sociales como Facebook o Google + o las cuentas locales.  |

## <a name="next-steps"></a>Pasos siguientes

Para información adicional sobre los elementos de la interfaz de usuario que se pueden personalizar, consulte la [guía de referencia para la personalización de la interfaz de usuario para las directivas integradas](active-directory-b2c-reference-ui-customization.md).
