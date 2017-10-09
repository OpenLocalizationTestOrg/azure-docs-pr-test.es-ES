---
title: 'Azure B2C Directory Active: Hacer referencia: personalizar la interfaz de usuario de un viaje de usuario con las directivas personalizadas de hello | Documentos de Microsoft'
description: Un tema acerca de las directivas personalizadas de Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Personalizar la interfaz de usuario de un viaje de usuario con las directivas personalizadas de Hola

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> Este artículo es una descripción avanzada del funcionamiento de la personalización de la interfaz de usuario y cómo tooenable con las directivas de B2C personalizado, mediante Hola Framework de la experiencia de identidad


En una solución de negocio a consumidor, es esencial una experiencia de usuario sin problemas. Por la experiencia de usuario sin problemas, se entiende una experiencia, ya sea en el dispositivo o explorador, donde no se pueden diferenciar el viaje de un usuario a través de nuestro servicio del servicio al cliente de hello están utilizando.

## <a name="understand-hello-cors-way-for-ui-customization"></a>Entender la forma CORS de hello para la personalización de la interfaz de usuario

B2C de Azure AD permite toocustomize Hola apariencia y funcionamiento de experiencia del usuario (UX) en hello varias páginas que pueden servir potencialmente y mostrar por Azure AD B2C a través de las directivas personalizadas.

Para ese fin, Azure AD B2C ejecuta el código en el explorador del consumidor y utiliza Hola enfoque moderno y standard [de uso compartido de recursos entre orígenes (CORS)](http://www.w3.org/TR/cors/) contenido personalizado de tooload desde una dirección URL específica que se especifica en una directiva personalizada plantillas de toopoint tooyour HTML5/CSS. CORS es un mecanismo que permite restringir recursos como fuentes, en un toobe de página web solicitado desde otro dominio fuera del dominio de Hola desde el que se originó el recurso de Hola.

En comparación con la forma tradicional antiguo de toohello, que son propiedad páginas de plantillas de solución de Hola donde proporciona texto limitado e imágenes, donde un control limitado sobre el diseño y el funcionamiento se proporcionó toomore inicial que dificultades tooachieve una experiencia satisfactoria, Hola CORS forma es compatible con HTML5 y CSS y le permite:

- Hospedar contenido de Hola y Hola solución inserta sus controles mediante el script del lado cliente.
- Tener control total sobre cada píxel del diseño y el funcionamiento.

Puede proporcionar tantas páginas de contenido como quiera mediante la creación de archivos HTML5/CSS según sea adecuado.

> [!NOTE]
> Por motivos de seguridad, uso de Hola de JavaScript está bloqueada actualmente para la personalización. se necesita toounblock JavaScript, uso de un nombre de dominio personalizado para su inquilino de Azure AD B2C.

En cada una de las plantillas de HTML5/CSS, proporcionar un *delimitador* elemento, que corresponde toohello necesario `<div id=”api”>` elemento Hola página HTML u Hola contenido como se muestra ahora en adelante. Azure AD B2C requiere que todas las páginas de contenido tengan este div específico.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Contenido relacionado con AD B2C Azure para la página de Hola se insertará en esta div al resto de Hola de página de hello es tuya toocontrol. código de JavaScript de Hello Azure AD B2C extrae su contenido e inyecta nuestro HTML en este elemento div específico. Azure AD B2C inserta Hola siguientes controles según corresponda: control de selector, controles de inicio de sesión, Multi-factor Authentication (actualmente basado en teléfono) controles y controles de la colección de atributos de la cuenta. Azure AD B2C garantiza que todos los controles de hello HTML5 accesible y no compatibles, pueden totalmente a un estilo a todos los controles de Hola y que no, degradará una versión de control.

Hello contenido combinado finalmente aparece como consumidor de hello documento dinámico tooyour.

tooensure de hello anterior funciona según lo previsto, debe:

- Asegurarse de que el contenido sea accesible y compatible con HTML5.
- Asegurarse de que el servidor de contenido esté habilitado para CORS.
- Servir el contenido a través de HTTPS.
- Usar direcciones URL absolutas como https://yourdomain/content para todos los vínculos y el contenido de CSS.

> [!TIP]
> tooverify que Hola va a albergar el contenido en el sitio tiene CORS habilitado y solicitudes CORS de pruebas, puede usar Hola sitio http://test-cors.org/. Sitio de toothis gracias, puede simplemente envío hello CORS solicitud tooa servidor remoto (tootest si se admite CORS), o enviar el servidor de prueba de tooa de solicitud CORS de hello (tooexplore ciertas características de CORS).

> [!TIP]
> Hola sitio http://enable-cors.org/ también constituye una más de recursos de gran utilidad en CORS.

Gracias toothis enfoque basado en CORS, los usuarios finales de hello, tendrá una experiencia coherente entre la aplicación y las páginas de hello atendidas por Azure AD B2C.

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento

Como requisito previo, debe toocreate una cuenta de almacenamiento. Necesitará un toocreate de suscripción de Azure una cuenta de almacenamiento de blobs de Azure. Puede solicitar una prueba gratuita en hello [sitio Web de Azure](https://azure.microsoft.com/en-us/pricing/free-trial/).

1. Abra una sesión de exploración y desplácese toohello [portal de Azure](https://portal.azure.com).
2. Inicie sesión con sus credenciales administrativas.
3. Haga clic en **Nuevo** > **Datos y almacenamiento** > **Cuenta de almacenamiento**.  Se abre la hoja **Crear cuenta de almacenamiento**.
4. En **nombre**, proporcione un nombre para la cuenta de almacenamiento de hello, por ejemplo, *contoso369b2c*. Este valor se hará referencia más adelante como demasiado*storageAccountName*.
5. Elija las selecciones adecuadas de Hola para hello plan de tarifa, grupo de recursos de Hola y suscripción Hola. Asegúrese de que dispone de hello **tooStartboard Pin** opción activada. Haga clic en **Crear**.
6. Retroceda toohello panel de inicio y haga clic en la cuenta de almacenamiento de Hola que acaba de crear.
7. Hola **servicios** sección, haga clic en **Blobs**. Se abre una hoja **Blob service**.
8. Haga clic en **+ Contenedor**.
9. En **nombre**, proporcione un nombre para el contenedor de hello, por ejemplo, *b2c*. Este valor será más adelante que se hace referencia tooas *containerName*.
9. Seleccione **Blob** como hello **tipo de acceso**. Haga clic en **Crear**.
10. contenedor de Hola que ha creado aparecerá en lista Hola Hola **hoja de servicio de Blob**.
11. Hola cerrar **Blobs** hoja.
12. En hello **hoja de la cuenta de almacenamiento**, haga clic en hello **clave** icono. Se abre una hoja **Claves de acceso**.  
13. Anote el valor de Hola de **key1**. Más adelante se hará referencia a este valor como *key1*.

## <a name="downloading-hello-helper-tool"></a>Descargar la herramienta de Ayudante Hola

1.  Descargar la herramienta de Ayudante Hola de [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).
2.  Guardar hello *B2C-AzureBlobStorage-Client-master.zip* archivo en el equipo local.
3.  Extraer contenido de hello del archivo hello B2C-AzureBlobStorage-Client-master.zip en el disco local, por ejemplo en hello **paquete de personalización de interfaz de usuario** carpeta. Se creará debajo una carpeta *B2C-AzureBlobStorage-Client-master*.
4.  Abra la carpeta y extraer contenido de Hola de archivo hello *B2CAzureStorageClient.zip* dentro de él.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Cargar archivos de paquete de personalización de interfaz de usuario de ejemplo de Hola

1.  Mediante el Explorador de Windows, desplazarse por las carpetas de toohello *B2C AzureBlobStorage cliente principales* ubicado en hello *paquete de personalización de interfaz de usuario* carpeta creada en la sección anterior de Hola.
2.  Ejecute hello *B2CAzureStorageClient.exe* archivo. Este programa simplemente permite cargar todos los archivos de hello en directorio de Hola que especifique la cuenta de almacenamiento de tooyour y habilitar el acceso CORS para esos archivos.
3.  Cuando se le solicite, especifique: a.  nombre de saludo de la cuenta de almacenamiento *storageAccountName*, por ejemplo *contoso369b2c*.
    b.  clave de acceso principal de Hola de su almacenamiento de blobs de azure, *key1*, por ejemplo *contoso369b2c*.
    c.  nombre de Hola de su contenedor de almacenamiento de blobs de almacenamiento, *containerName*, por ejemplo *b2c*.
    d.  ruta de acceso de Hola de hello *Starter Pack* ejemplo archivos, por ejemplo *... \B2CTemplates\wingtiptoys*.

Si ha seguido los pasos de hello anteriores, Hola archivos HTML5 y CSS de hello *paquete de personalización de interfaz de usuario* de empresa ficticia hello **wingtiptoys** ahora se apunta tooyour cuenta de almacenamiento.  Puede comprobar que se ha cargado correctamente el contenido de hello, abra la hoja de contenedor relacionados de hello en hello portal de Azure. Como alternativa, puede comprobar que se ha cargado correctamente el contenido de hello mediante el acceso a la página de Hola desde un explorador. Para obtener más información, consulte [Azure Active Directory B2C: una herramienta de Ayudante para usa la característica de personalización de la interfaz de usuario de toodemonstrate Hola página](active-directory-b2c-reference-ui-customization-helper-tool.md).

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>Asegúrese de cuenta de almacenamiento de hello tiene CORS habilitado

CORS (uso compartido recursos entre orígenes) debe estar habilitado en el punto de conexión para tooload Premium de Azure AD B2C su contenido. Esto es porque el contenido está hospedado en un dominio diferente de dominio Hola Premium de Azure AD B2C atienden a página Hola de.

tooverify que va a albergar el contenido en el almacenamiento de hello tiene CORS está habilitada, continúe con hello pasos:

1. Abra una sesión de exploración y desplácese página toohello *unified.html* mediante la dirección URL completa de Hola de su ubicación en la cuenta de almacenamiento `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`. Por ejemplo, https://contoso369b2c.blob.core.windows.net/b2c/unified.html.
2. Navegue toohttp://test-cors.org. Este sitio permite tooverify que Hola página que utilizas tiene CORS habilitado.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. En **dirección URL remota**, escriba la dirección URL completa de hello para el contenido de unified.html y haga clic en **enviar solicitud**.
4. Compruebe que los resultados del Hola Hola **resultados** sección contiene *estado XHR: 200*. Esto indica que CORS está habilitado.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
cuenta de almacenamiento de Hello debe contener ahora un contenedor de blobs denominado *b2c* en la ilustración que contiene Hola siguientes wingtiptoys plantillas de hello *Starter Pack*.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

Hello siguiente tabla describe Hola propósito de hello situado encima de páginas de HTML5.

| Plantilla HTML5 | Descripción |
|----------------|-------------|
| *phonefactor.html* | Esta página se puede usar como plantilla para una página de autenticación multifactor. |
| *resetpassword.html* | Esta página se puede usar como plantilla para una página de contraseña olvidada. |
| *selfasserted.html* | Esta página se puede usar como plantilla para una página de registro en una cuenta social, una página de registro en una cuenta local o una página de inicio de sesión en una cuenta local. |
| *unified.html* | Esta página se puede usar como plantilla para una página de inicio de sesión o registro unificada. |
| *updateprofile.html* | Esta página se puede usar como plantilla para una página de actualización de perfil. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>Agregar un viaje de usuario HTML5/CSS plantillas tooyour de vínculo tooyour

Puede agregar un viaje de usuario HTML5/CSS plantillas tooyour de vínculo tooyour mediante la edición directa de una directiva personalizada.

Hola toouse de plantillas de HTML5/CSS personalizado en su viaje de usuario tienen toobe especificado en una lista de definiciones de contenido que se puede usar en los viajes de usuario. Para ese fin, opcional  *<ContentDefinitions>*  elemento XML se debe declarar en hello  *<BuildingBlocks>*  sección de su archivo XML de directivas personalizadas.

Hello siguiente tabla describe Hola conjunto de identificadores de definición de contenido reconocidos por el motor de experiencia de hello Azure AD B2C identidad y el tipo de Hola de páginas que relaciona toothem.

| Id. de definición de contenido | Descripción |
|-----------------------|-------------|
| *api.error* | **Página de error**. Esta página se muestra cuando se produce una excepción o un error. |
| *api.idpselections* | **Página de selección del proveedor de identidades**. Esta página contiene una lista de proveedores que Hola usuario pueden elegir entre durante el inicio de sesión de identidad. Estos son los proveedores de identidades de empresa, los proveedores de identidades sociales como Facebook y Google+ o las cuentas locales (basadas en una dirección de correo electrónico o un nombre de usuario). |
| *api.idpselections.signup* | **Selección del proveedor de identidades para el registro**. Esta página contiene una lista de proveedores que Hola usuario pueden elegir al realizar el registro de identidad. Estos son los proveedores de identidades de empresa, los proveedores de identidades sociales como Facebook y Google+ o las cuentas locales (basadas en una dirección de correo electrónico o un nombre de usuario). |
| *api.localaccountpasswordreset* | **Página de contraseña olvidada**. Esta página contiene un formulario que el usuario hello tiene tooinitiate toofill para restablecer su contraseña.  |
| *api.localaccountsignin* | **Página de inicio de sesión en una cuenta local**. Esta página contiene un formulario de inicio de sesión de ese usuario hello tiene toofill en al iniciar sesión en una cuenta local que se basa en una dirección de correo electrónico o un nombre de usuario. Hola formulario puede contener un cuadro de entrada de texto y un cuadro de entrada de contraseña. |
| *api.localaccountsignup* | **Página de registro en una cuenta local**. Esta página contiene un formulario de registro que el usuario hello tiene toofill en al suscribirse a una cuenta local que se basa en una dirección de correo electrónico o un nombre de usuario. formulario de Hello puede contener diferentes controles de entrada como cuadro de entrada de texto, cuadro de entrada de contraseña, botón de radio, cuadros de lista desplegable de selección única y casillas de verificación de selección múltiple. |
| *api.phonefactor* | **Página de autenticación multifactor**. Esta página permite a los usuarios verificar sus números de teléfono (mediante texto o voz) durante el registro o el inicio de sesión. |
| *api.selfasserted* | **Página de registro en una cuenta social**. Esta página contiene un formulario de registro que el usuario hello tiene toofill al registrarse con otra cuenta de un proveedor de identidades sociales como Facebook o Google +. Esta página es similar toohello por encima de la página de registro de cuenta social con excepción de Hola de campos de entrada de contraseña de Hola. |
| *api.selfasserted.profileupdate* | **Página de actualización de perfil**. Esta página contiene un formulario de ese usuario Hola sirve tooupdate su perfil. Esta página es similar toohello por encima de la página de registro de cuenta social con excepción de Hola de campos de entrada de contraseña de Hola. |
| *api.signuporsignin* | **Página de inicio de sesión o registro unificada**.  Esta página controla tanto la suscripción como el inicio de sesión de los usuarios, que pueden usar proveedores de identidades de empresa, proveedores de identidades sociales, como Facebook o Google +, o cuentas locales.

## <a name="next-steps"></a>Pasos siguientes
[Referencia: Comprender las directivas personalizadas de cómo trabajar con hello Identity Framework de experiencia en B2C](active-directory-b2c-reference-custom-policies-understanding-contents.md)
