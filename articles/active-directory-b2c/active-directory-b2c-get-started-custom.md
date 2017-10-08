---
title: "Azure Active Directory B2C: introducción a las directivas personalizadas | Microsoft Docs"
description: "¿Cómo tooget a trabajar con las directivas personalizadas de Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C: introducción a las directivas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Después de completar los pasos de hello en este artículo, la directiva personalizada admitirá "cuenta local" inicio de sesión o inicio de sesión a través de una dirección de correo electrónico y una contraseña. También preparará el entorno para agregar proveedores de identidades (como Facebook o Azure Active Directory). Le recomendamos que toocomplete estos pasos antes de leer sobre otros usos de hello marco de la experiencia de identidad de Azure Active Directory (Azure AD) B2C.

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar, asegúrese de que tiene un inquilino de Azure AD B2C, que es un contenedor para todos los usuarios, las aplicaciones, las directivas y mucho más. Si no tiene ninguno todavía, necesita demasiado[crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md). Se fuertemente anime a todos los desarrolladores toocomplete Hola tutoriales de directivas integradas de Azure AD B2C y configuración sus aplicaciones con directivas integradas antes de continuar. Las aplicaciones funcionarán con ambos tipos de directivas cuando haya realizado una cambio menor toohello directiva nombre tooinvoke Hola directiva personalizada.

>[!NOTE]
>edición de directivas personalizadas de tooaccess, necesita un inquilino de vinculado tooyour suscripción válida a Azure. Si no lo ha hecho [vinculado su tooan de inquilino de Azure AD B2C suscripción de Azure](active-directory-b2c-how-to-enable-billing.md) o su suscripción de Azure está deshabilitada, Hola identidad experiencia Framework botón no estará disponible.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>Agregar a inquilino de tooyour B2C de claves de firma y cifrado para su uso por las directivas personalizadas

1. Abra hello **identidad experiencia Framework** hoja en la configuración del inquilino de Azure AD B2C.
2. Seleccione **claves de directiva** claves de hello tooview disponibles en el inquilino.
3. Cree B2C_1A_TokenSigningKeyContainer si no existe:<br>
    a. Seleccione **Agregar**. <br>
    b. Seleccione **Generar**.<br>
    c. En **Nombre**, use `TokenSigningKeyContainer`. <br> 
    prefijo de Hello `B2C_1A_` podrían agregarse automáticamente.<br>
    d. En **Tipo de clave**, use **RSA**.<br>
    e. Para **fechas**, utilizar los valores predeterminados de Hola. <br>
    f. En **Uso de claves**, use **Firma**.<br>
    g. Seleccione **Crear**.<br>
4. Cree B2C_1A_TokenEncryptionKeyContainer si no existe:<br>
 a. Seleccione **Agregar**.<br>
 b. Seleccione **Generar**.<br>
 c. En **Nombre**, use `TokenEncryptionKeyContainer`. <br>
   prefijo de Hello `B2C_1A`_ podrían agregarse automáticamente.<br>
 d. En **Tipo de clave**, use **RSA**.<br>
 e. Para **fechas**, utilizar los valores predeterminados de Hola.<br>
 f. En **Uso de claves**, use **Cifrado**.<br>
 g. Seleccione **Crear**.<br>
5. Cree B2C_1A_FacebookSecret. <br>
Si ya tiene un secreto de aplicación de Facebook, agregarlo como un inquilino de tooyour clave de directiva. En caso contrario, debe crear clave de hello con un valor de marcador de posición para que las directivas de pasan la validación.<br>
 a. Seleccione **Agregar**.<br>
 b. En **Opciones**, use **Manual**.<br>
 c. En **Nombre**, use `FacebookSecret`. <br>
 prefijo de Hello `B2C_1A_` podrían agregarse automáticamente.<br>
 d. Hola **secreto** cuadro, escriba su FacebookSecret de developers.facebook.com o `0` como un marcador de posición. *No es su identificador de aplicación de Facebook.* <br>
 e. En **Uso de claves**, use **Firma**. <br>
 f. Seleccione **Crear** y confirme la creación.

## <a name="register-identity-experience-framework-applications"></a>Registro de las aplicaciones del marco de experiencia de identidad

Azure AD B2C requiere tooregister dos aplicaciones adicionales que usan Hola motor toosign seguridad e inicie sesión en los usuarios.

>[!NOTE]
>Debe crear dos aplicaciones ese inicio de sesión en habilitar utilizando cuentas locales: IdentityExperienceFramework (una aplicación web) y ProxyIdentityExperienceFramework (una aplicación nativa) con permiso de aplicación de hello IdentityExperienceFramework de delegado. Las cuentas locales solo existen en su inquilino. Los usuarios suscribirse a un tooaccess de combinación de dirección y la contraseña de correo electrónico única sus aplicaciones inquilino registrado.

### <a name="create-hello-identityexperienceframework-application"></a>Crear aplicación de hello IdentityExperienceFramework

1. Hola [portal de Azure](https://portal.azure.com), cambiar a hello [contexto de su inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md).
2. Abra hello **Azure Active Directory** hoja (no Hola **Azure AD B2C** hoja). Es posible que tenga tooselect **más servicios** toofind lo.
3. Seleccione **App registrations** (Registros de aplicaciones).
4. Seleccione **Nuevo registro de aplicaciones**.
   * En **Nombre**, use `IdentityExperienceFramework`.
   * En **Tipo de aplicación**, use **Aplicación web o API**.
   * En **Dirección URL de inicio de sesión**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, donde `yourtenant` es el nombre de dominio del inquilino de Azure AD B2C.
5. Seleccione **Crear**.
6. Una vez que se creó, seleccione aplicación hello recién creado **IdentityExperienceFramework**.<br>
   * Seleccione **Propiedades**.<br>
   * Copie el identificador de la aplicación hello y guardar para más tarde.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Crear aplicación de hello ProxyIdentityExperienceFramework

1. Seleccione **App registrations** (Registros de aplicaciones).
1. Seleccione **Nuevo registro de aplicaciones**.
   * En **Nombre**, use `ProxyIdentityExperienceFramework`.
   * En **Tipo de aplicación**, use **Nativa**.
   * En **URI de redirección**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, donde `yourtenant` es el inquilino de Azure AD B2C.
1. Seleccione **Crear**.
1. Una vez creada, seleccione la aplicación hello **ProxyIdentityExperienceFramework**.<br>
   * Seleccione **Propiedades**. <br>
   * Copie el identificador de la aplicación hello y guardar para más tarde.
1. Seleccione **Permisos necesarios**.
1. Seleccione **Agregar**.
1. Seleccione **Seleccionar una API**.
1. Busque el nombre de hello IdentityExperienceFramework. Seleccione **IdentityExperienceFramework** en Hola resultados y, a continuación, haga clic en **seleccione**.
1. Seleccione Hola casilla siguiente demasiado**acceso IdentityExperienceFramework**y, a continuación, haga clic en **seleccione**.
1. Seleccione **Listo**.
1. Seleccione **Conceder permisos** y haga clic en **Sí** para confirmar.

## <a name="download-starter-pack-and-modify-policies"></a>Descarga del paquete de inicio y modificación de directivas

Las directivas personalizadas son un conjunto de archivos XML que necesita el inquilino de Azure AD B2C tooyour toobe cargado. Proporcionamos starter módulos tooget avanzar con rapidez. Cada módulo de inicio en hello lista siguiente contiene número más pequeño de Hola de perfiles técnicos y viajes de usuario necesario escenarios de hello tooachieve que se describe:
 * LocalAccounts. Habilita el uso de Hola de las cuentas locales únicamente.
 * SocialAccounts. Habilita el uso de Hola de cuentas de sociales (o federadas).
 * **SocialAndLocalAccounts**. Usamos este archivo para ver tutorial Hola.
 * SocialAndLocalAccountsWithMFA. Aquí se incluyen otras opciones sociales, locales y de Multi-Factor Authentication.

Cada paquete de inicio contiene lo siguiente:

* Hola [archivo base](active-directory-b2c-overview-custom.md#policy-files) de directiva de Hola. Algunas modificaciones son necesaria toohello base.
* Hola [archivo de extensión](active-directory-b2c-overview-custom.md#policy-files) de directiva de Hola.  Este archivo es donde se hace la mayoría de los cambios de configuración.
* Los [archivos de usuario de confianza](active-directory-b2c-overview-custom.md#policy-files) son archivos específicos de la tarea a los que llama la aplicación.

>[!NOTE]
>Si el editor XML que admita la validación, validar los archivos de hello en esquema de XML TrustFrameworkPolicy_0.3.0.0.xsd Hola que se encuentra en el directorio raíz de Hola de módulo de inicio de Hola. La validación del esquema XML identifica los errores antes de realizar la carga.

 Comencemos:

1. Descargue active-directory-b2c-custom-policy-starterpack de GitHub. [Descargue el archivo .zip de hello](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) o ejecutar

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Abra la carpeta de SocialAndLocalAccounts Hola.  archivo de base de Hello (TrustFrameworkBase.xml) en esta carpeta contiene contenido que es necesario para las cuentas locales y social/corporativos. contenido sociales Hello no interfiere con pasos de Hola para obtener las cuentas locales y ejecutar.
3. Abra TrustFrameworkBase.xml. Si necesita un editor XML, [pruebe Visual Studio Code](https://code.visualstudio.com/download), un editor multiplataforma ligero.
4. En la raíz de hello `TrustFrameworkPolicy` elemento, actualización hello `TenantId` y `PublicPolicyUri` atributos, reemplazar `yourtenant.onmicrosoft.com` con el nombre de dominio de Hola de su inquilino de Azure AD B2C:
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`es nombre de la directiva de Hola que se ve en el portal de Hola y el nombre de Hola por el que se hace referencia a este archivo de directiva por otros archivos de directiva.

5. Guarde el archivo hello.
6. Abra TrustFrameworkExtensions.xml. Realizar los mismos cambios en dos de hello reemplazando `yourtenant.onmicrosoft.com` con su inquilino de Azure AD B2C. Asegúrese de Hola mismo reemplazo Hola `<TenantId>` (elemento) para un total de tres cambios. Guarde el archivo hello.
7. Abra SignUpOrSignIn.xml. Realizar los mismos cambios de hello reemplazando `yourtenant.onmicrosoft.com` con el inquilino de Azure AD B2C en tres lugares. Guarde el archivo hello.
8. Restablecimiento de contraseña de hello abierto y perfil editar archivos. Realizar los mismos cambios de hello reemplazando `yourtenant.onmicrosoft.com` con el inquilino de Azure AD B2C en tres lugares en cada archivo. Guardar archivos de Hola.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Agregar directiva personalizada de hello aplicación identificadores tooyour
Agregue el archivo extensiones toohello de hello aplicación identificadores (`TrustFrameworkExtensions.xml`):

1. En el archivo de extensiones de hello (TrustFrameworkExtensions.xml), busque el elemento de hello `<TechnicalProfile Id="login-NonInteractive">`.
2. Reemplace ambas instancias de `IdentityExperienceFrameworkAppId` con el Id. de aplicación Hola de hello aplicación de marco de la experiencia de identidad que creó anteriormente. Aquí tiene un ejemplo:

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. Reemplace ambas instancias de `ProxyIdentityExperienceFrameworkAppId` con el Id. de aplicación Hola de hello aplicación Framework de experiencia de identidad de Proxy que creó anteriormente.
4. Guarde el archivo de extensiones.

## <a name="upload-hello-policies-tooyour-tenant"></a>Cargar el inquilino de hello directivas tooyour

1. Hola [portal de Azure](https://portal.azure.com), cambiar a hello [contexto de su inquilino de Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), abra hello y **Azure AD B2C** hoja.
2. Seleccione **Marco de experiencia de identidad**.
3. Seleccione **Cargar directiva**.

    >[!WARNING]
    >archivos de directivas personalizadas de Hola se deben cargar en hello siguiendo el orden:

1. Cargue TrustFrameworkBase.xml.
2. Cargue TrustFrameworkExtensions.xml.
3. Cargue SignUpOrSignin.xml.
4. Cargue los restantes archivos de directiva.

Cuando se carga un archivo, se antepone al nombre de Hola Hola del archivo de directiva con `B2C_1A_`.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Probar directiva personalizada de hello mediante Ejecutar ahora

1. Abra **configuración de Azure AD B2C** y vaya demasiado**identidad experiencia Framework**.

   >[!NOTE]
   >**Ejecutar ahora** requiere al menos una aplicación toobe registrada previamente en el inquilino de Hola. Las aplicaciones deben estar registradas en el inquilino Hola B2C, ya sea mediante hello **aplicaciones** selección de menú en Azure AD B2C o mediante Hola identidad experiencia Framework tooinvoke directivas integradas y personalizadas. Solo se necesita un registro por aplicación.<br><br>
   toolearn tooregister aplicaciones, vea hello Azure AD B2C [Introducción](active-directory-b2c-get-started.md) artículo o hello [registro de la aplicación](active-directory-b2c-app-registration.md) artículo.  

2. Abra B2C_1A_signup_signin, Hola directiva personalizada de confianza (RP) de la entidad que ha cargado. Seleccione **Ejecutar ahora**.

3. Debe ser capaz de toosign utilizando una dirección de correo electrónico.

4. Inicie sesión con hello misma cuenta tooconfirm que tienes Hola configuración correcta.

>[!NOTE]
>Una causa común de los errores en el inicio de sesión es que la aplicación IdentityExperienceFramework no esté configurada correctamente.


## <a name="next-steps"></a>Pasos siguientes

### <a name="add-facebook-as-an-identity-provider"></a>Incorporación de Facebook como proveedor de identidades
tooset seguridad Facebook:
1. [Configure una aplicación de Facebook en developers.facebook.com](active-directory-b2c-setup-fb-app.md).
2. [Agregar aplicación tooyour secreto Azure AD B2C inquilino de hello Facebook](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).
3. En el archivo de directiva de hello TrustFrameworkExtensions, sustituya el valor de Hola de `client_id` con el Id. de aplicación de Facebook hello:

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Cargar el inquilino de hello TrustFrameworkExtensions.xml directiva archivo tooyour.
5. Prueba mediante el uso de **ejecutar ahora** o invocando directiva Hola directamente desde la aplicación registrada.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Adición de Azure Active Directory como proveedor de identidades
archivo de base de Hello usado en esta guía de introducción ya contiene parte del contenido de Hola que necesite para agregar otros proveedores de identidad. Para obtener información acerca de cómo configurar inicios de sesión, vea hello [Azure Active Directory B2C: inicie sesión con cuentas de Azure AD](active-directory-b2c-setup-aad-custom.md) artículo.

Para obtener información general de directivas personalizadas en Azure AD B2C que usar hello Framework de la experiencia de identidad, vea hello [Azure Active Directory B2C: las directivas personalizadas](active-directory-b2c-overview-custom.md) artículo. 
