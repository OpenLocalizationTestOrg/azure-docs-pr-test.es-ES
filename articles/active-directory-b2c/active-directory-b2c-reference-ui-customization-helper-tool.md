---
title: "Azure Active Directory B2C: herramienta auxiliar de personalización de la interfaz de usuario de página | Microsoft Docs"
description: "Una herramienta de Ayudante usa la característica de personalización de interfaz de usuario de página de toodemonstrate hello en Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>Azure B2C directorio activo: Una herramienta de Ayudante para usa la característica de personalización de la interfaz de usuario de toodemonstrate Hola página
Este artículo es una toohello complementaria [artículo de personalización de interfaz de usuario principal](active-directory-b2c-reference-ui-customization.md) en Azure Active Directory (Azure AD) B2C. Hello pasos siguientes describen cómo tooexercise Hola característica de personalización de interfaz de usuario de página mediante el uso de contenido de HTML y CSS de ejemplo que hemos proporcionado.

## <a name="get-an-azure-ad-b2c-tenant"></a>Obtención de un inquilino de Azure AD B2C
Antes de poder personalizar nada, necesitará demasiado[obtener un inquilino de Azure AD B2C](active-directory-b2c-get-started.md) si aún no tiene uno.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Creación de una directiva de registro o de inicio de sesión
Hello hemos proporcionado el contenido de ejemplo puede ser usado toocustomze dos páginas en una [directiva de inicio de sesión o inicio de sesión](active-directory-b2c-reference-policies.md): Hola [página de inicio de sesión unificada](active-directory-b2c-reference-ui-customization.md) hello y [atributos autoafirmadas página](active-directory-b2c-reference-ui-customization.md). Al [crear una directiva de registro o de inicio de sesión](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), agregue Cuenta local (dirección de correo electrónico), Facebook, Google y Microsoft como **proveedores de identidades**. Estos son Hola solo IDPs que acepte nuestro contenido HTML de ejemplo.  También puede agregar un subconjunto de estos IDP si lo desea.

## <a name="register-an-application"></a>Registro de una aplicación
Necesitará demasiado[registrar una aplicación](active-directory-b2c-app-registration.md) en su B2C inquilino que puede ser tooexecute usa la directiva. Después de registrar la aplicación, tiene algunas opciones que puede usar tooactually ejecutar la directiva de inicio de sesión:

* Genere una hello Azure AD B2C enumerar las aplicaciones de inicio rápido en sección Hola "Introducción" de [iniciar una copia de seguridad e inicie sesión en los consumidores en las aplicaciones](active-directory-b2c-overview.md#get-started).
* Hola uso pregenerada [prueba para Azure AD B2C](https://aadb2cplayground.azurewebsites.net) aplicación. Si elige playground de hello toouse, debe registrar una aplicación en su inquilino de B2C con hello **URI de redireccionamiento** `https://aadb2cplayground.azurewebsites.net/`.
* Hola de uso **ejecutar ahora** botón en la directiva en hello [portal de Azure](https://portal.azure.com/).

## <a name="customize-your-policy"></a>Personalización de la directiva
toocustomize Hola apariencia y funcionamiento de la directiva, necesita toofirst crear archivos HTML y CSS con hello convenciones específicas de Azure AD B2C. A continuación, puede cargar la ubicación disponible públicamente tooa contenido estático para que Azure AD B2C puede tener acceso a él. Esta ubicación podría ser su propio servidor web dedicado, el Almacenamiento de blobs de Azure, la Red de entrega de contenido de Azure o cualquier otro proveedor de hospedaje de recursos estático. Hola únicos requisitos son que el contenido está disponible a través de HTTPS y puede tener acceso mediante el uso de CORS. Una vez que ha expuesto el contenido estático en web de hello, puede editar la ubicación de directiva toopoint toothis y presente que los clientes tooyour de contenido. Hola [artículo de personalización de interfaz de usuario principal](active-directory-b2c-reference-ui-customization.md) describe con detalle cómo funciona la característica de personalización de hello Azure AD B2C.

Para fines de Hola de este tutorial, ya hemos creado algún contenido de ejemplo y hospedadas en almacenamiento de blobs de Azure. contenido de ejemplo de Hola es una personalización básica en el tema Hola de nuestra empresa ficticia, "Wingtip Toys". tootry horizontal en su propia directiva, siga estos pasos:

1. Inicie sesión en el inquilino de tooyour en hello [portal de Azure](https://portal.azure.com/) y navegar por hoja de características toohello B2C.
2. Haga clic en **Directivas de inicio de sesión o registro** y en su directiva (por ejemplo, "b2c\_1\_sign\_up\_sign\_in").
3. Haga clic en **Personalización de la interfaz de usuario de la página** y, luego, en **Página unificada de inicio de sesión o de registro**.
4. Hola de alternancia **página personalizada de uso** cambiar demasiado**Sí**. Hola **URI de la página personalizada** , escriba `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. Haga clic en **Aceptar**.
5. Haga clic en **Página de suscripción de cuenta local**. Hola de alternancia **utilizar una plantilla personalizada** cambiar demasiado**Sí**. Hola **URI de la página personalizada** , escriba `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
6. Repita Hola mismo paso a paso para hello **página de inicio de sesión de cuenta sociales**.
   Haga clic en **Aceptar** hojas de personalización tooclose Hola UI dos veces.
7. Haga clic en **Guardar**.

Ahora puede probar la directiva personalizada. Puede usar su propia prueba de Azure AD B2C de aplicación o hello para si desea, pero puede hacer simplemente clic en hello **ejecutar ahora** comando en la hoja de la directiva de Hola. Seleccione la aplicación en el cuadro de lista desplegable de Hola y elija Hola adecuado el URI de redireccionamiento. Haga clic en hello **ejecutar ahora** botón. Se abrirá una nueva pestaña de explorador y se pueden ejecutar a través de la experiencia del usuario Hola de suscribirse a la aplicación con el nuevo contenido en lugar de Hola!

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Cargar tooAzure de contenido de ejemplo de Hola almacenamiento de blobs
Si desea que toouse almacenamiento de blobs de Azure toohost su contenido, puede crear su propia cuenta de almacenamiento y usar nuestro tooupload de herramienta de Ayudante B2C los archivos de la página.

### <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **+ Nuevo** > **Datos y almacenamiento** > **Cuenta de almacenamiento**. Necesitará un toocreate de suscripción de Azure una cuenta de almacenamiento de blobs de Azure. Puede solicitar una prueba gratuita en hello [sitio Web de Azure](https://azure.microsoft.com/pricing/free-trial/).
3. Proporcionar un **nombre** para la cuenta de almacenamiento de hello (por ejemplo, "contoso") y selección hello las selecciones adecuadas para **tarifa**, **grupo de recursos** y  **Suscripción**. Asegúrese de que dispone de hello **tooStartboard Pin** opción activada. Haga clic en **Crear**.
4. Retroceda toohello panel de inicio y haga clic en la cuenta de almacenamiento de Hola que acaba de crear.
5. Hola **resumen** sección, haga clic en **contenedores**y, a continuación, haga clic en **+ agregar**.
6. Proporcionar un **nombre** para el contenedor de hello (por ejemplo, "b2c") y seleccione **Blob** como hello **tipo de acceso**. Haga clic en **Aceptar**.
7. contenedor de Hola que ha creado aparecerá en lista Hola Hola **Blobs** hoja. Anote Hola URL del contenedor de hello; Por ejemplo, debería ser similar demasiado`https://contoso.blob.core.windows.net/b2c`. Hola cerrar **Blobs** hoja.
8. En la hoja de la cuenta de almacenamiento de hello, haga clic en **claves** y anote los valores de hello de hello **nombre de la cuenta de almacenamiento** y **clave de acceso principal** campos.

> [!NOTE]
> **Clave de acceso primaria** es una credencial de seguridad importante.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Descargar archivos de ejemplo y la herramienta de la aplicación auxiliar de Hola
Puede descargar hello [los archivos de ejemplo y la herramienta de Ayudante almacenamiento de blobs de Azure como un archivo .zip](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) o clonar desde GitHub:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Este repositorio contiene un directorio `sample_templates\wingtip` , que contiene HTML, CSS e imágenes de ejemplo. En estas plantillas tooreference su propia cuenta de almacenamiento de blobs de Azure, necesitará los archivos de hello HTML tooedit. Abra `unified.html` y `selfasserted.html` y reemplace todas las instancias de `https://localhost` por dirección URL de Hola de su propio contenedor que anotó en los pasos anteriores de Hola. Debe usar la ruta de acceso absoluta de Hola de hello HTML archivos porque en este caso, se servirá Hola HTML con Azure AD, en el dominio de hello `https://login.microsoftonline.com`.

### <a name="upload-hello-sample-files"></a>Cargar archivos de ejemplo de Hola
En el mismo repositorio de Hola, descomprima `B2CAzureStorageClient.zip` ejecución hello y `B2CAzureStorageClient.exe` dentro de archivos. Este programa simplemente permite cargar todos los archivos de hello en directorio de Hola que especifique la cuenta de almacenamiento de tooyour y habilitar el acceso CORS para esos archivos. Si ha seguido los pasos de hello anteriores, hello HTML y archivos CSS se apuntar ahora tooyour cuenta de almacenamiento. Tenga en cuenta que Hola nombre de la cuenta de almacenamiento forma parte de Hola que precede a `blob.core.windows.net`; por ejemplo, `contoso`. Puede comprobar que se ha cargado correctamente el contenido de hello realizando tooaccess `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` en un explorador. Usar [http://test-cors.org/](http://test-cors.org/) toomake seguro de que el contenido de hello ahora CORS habilitado. (Busque "estado XHR: 200" en el resultado de hello.)

### <a name="customize-your-policy-again"></a>Personalización de la directiva, de nuevo
Ahora que ha cargado la cuenta de almacenamiento propios de tooyour contenido de ejemplo de Hola, debe modificar su tooreference de directiva de suscripción a él. Repita los pasos de Hola de hello ["Personalizar la directiva"](#customize-your-policy) sección anterior, esta vez utilizando las direcciones URL de su propia cuenta de almacenamiento. Hola, por ejemplo, la ubicación de su `unified.html` archivo sería `<url-of-your-container>/wingtip/unified.html`.

Ahora puede usar hello **ejecutar ahora** botón o su propia aplicación tooexecute la directiva de nuevo. Hola resultado debe busque casi exactamente hello mismo--utilizó Hola iguales en ambos casos de ejemplo HTML y CSS. Sin embargo, las directivas se hace referencia ahora a su propia instancia de almacenamiento de blobs de Azure y están tooedit libre y cargar archivos de hello nuevo que tenga. Para obtener más información acerca de cómo personalizar hello HTML y CSS, consulte toohello [artículo principal de personalización de interfaz de usuario](active-directory-b2c-reference-ui-customization.md).

