---
title: "aaaConfigure el servicio de administración de API con Git - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosave y configurar la configuración del servicio de administración de API con Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>¿Cómo toosave y configurar la configuración del servicio de administración de API con Git
> 
> 

Cada instancia de servicio de administración de API mantiene una base de datos de configuración que contiene información sobre la configuración de Hola y metadatos de instancia de servicio de Hola. Pueden realizarse cambios instancia del servicio toohello cambiar una configuración en el portal para desarrolladores de hello, mediante un cmdlet de PowerShell, o realizar una llamada de API de REST. Además métodos toothese, también puede administrar la configuración de la instancia de servicio con Git, permite escenarios de administración de servicios como:

* Control de versiones de configuración: descargue y almacene versiones diferentes de la configuración del servicio
* Cambios de configuración de forma masiva: realizar cambios toomultiple partes de la configuración del servicio en el repositorio local e integrar el servidor de toohello atrás de cambios de hello con una sola operación
* Familiar Git la cadena de herramientas y flujo de trabajo - usar herramientas de Git de Hola y flujos de trabajo que ya están familiarizados con

Hola siguiente diagrama muestra un resumen de tooconfigure de maneras diferentes de hello su instancia de servicio de administración de API.

![Configuración de GIT][api-management-git-configure]

Al realizar cambios de servicio de tooyour mediante el portal para desarrolladores de hello, cmdlets de PowerShell o API de REST de hello, administra la base de datos de configuración de servicio con hello `https://{name}.management.azure-api.net` extremo, tal y como se muestra en hello derecha del diagrama de Hola. Hola lado izquierdo del diagrama de hello, muestra cómo puede administrar la configuración del servicio mediante Git y repositorio de Git para el servicio que encontrará en `https://{name}.scm.azure-api.net`.

Hola pasos proporciona información general de la administración de la instancia de servicio de administración de API con Git.

1. Acceso a la configuración de Git en el servicio
2. Guardar el repositorio de Git servicio tooyour de base de datos de configuración
3. Clonar máquina local de hello Git repositorio tooyour
4. Extracción repositorio más reciente de hello tooyour en los equipos local y confirme e inserte repositorio de back-tooyour de cambios
5. Implementar cambios de Hola desde el repositorio en la base de datos de configuración de servicio

Este artículo se describe cómo tooenable y usar Git toomanage la configuración del servicio y proporciona una referencia de hello archivos y carpetas en el repositorio de Git Hola.

## <a name="access-git-configuration-in-your-service"></a>Acceso a la configuración de Git en el servicio
Puede ver rápidamente estado de saludo de la configuración de Git viendo el icono de Git de hello en la esquina superior derecha de Hola de portal para desarrolladores de Hola. En este ejemplo, el mensaje de bienvenida de estado indica que hay repositorio de toohello de los cambios no guardados. Esto es porque la base de datos de configuración de servicio de administración de API de hello aún no se ha guardado toohello repositorio.

![Estado de Git][api-management-git-icon-enable]

tooview y configurar las opciones de configuración de Git, puede haga clic en el icono de Git de hello, o haga clic en hello **seguridad** menú y vaya toohello **repositorio de configuración** ficha.

![Habilitar GIT][api-management-enable-git]

> [!IMPORTANT]
> Los secretos que no estén definidos como propiedades se almacenan en el repositorio de Hola y permanecerán en su historial de hasta que deshabilite y vuelva a habilitar el acceso de Git. Propiedades proporcionan un lugar seguro toomanage valores de cadena constante, incluidos los secretos, a través de todas las directivas y configuración de API de modo que no tenga toostore directamente en las instrucciones de directiva. Para obtener más información, consulte [cómo toouse propiedades en las directivas de administración de API de Azure](api-management-howto-properties.md).
> 
> 

Para obtener información sobre la habilitación o deshabilitación del acceso de Git con hello API de REST, consulte [habilitar o deshabilitar el acceso de Git con la API de REST de hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>repositorio de Git toosave Hola servicio configuración toohello
Hola primer paso antes de la clonación repositorio hello es estado actual de hello toosave del repositorio de toohello de configuración de servicio de Hola. Haga clic en **Guardar configuración toorepository**.

![Guardar configuración][api-management-save-configuration]

Realice los cambios deseados en la pantalla de confirmación de bienvenida y haga clic en **Aceptar** toosave.

![Guardar configuración][api-management-save-configuration-confirm]

Transcurridos unos instantes se guarda la configuración de Hola y se muestra el estado de la configuración del repositorio de Hola Hola, incluidos Hola fecha y hora del último cambio de configuración de Hola y última sincronización de hello entre la configuración del servicio de Hola y Hola repositorio.

![Estado de configuración][api-management-configuration-status]

Una vez Hola configuración se ha guardado toohello repositorio, se puede clonar.

Para obtener información acerca de cómo realizar esta operación mediante la API de REST de hello, consulte [configuración de confirmación de instantáneas mediante la API de REST de hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>equipo local de tooclone Hola repositorio tooyour
tooclone un repositorio, deberá tooyour repositorio de hello dirección URL, un nombre de usuario y una contraseña. Hello nombre de usuario y la dirección URL se muestran en parte superior de Hola de hello **repositorio de configuración** ficha.

![Clonación de git][api-management-configuration-git-clone]

contraseña de Hola se genera en parte inferior de Hola de Hola **repositorio de configuración** ficha.

![Generar contraseña][api-management-generate-password]

toogenerate una contraseña, asegúrese en primer lugar ese hello **caducidad** toohello deseado fecha de expiración y la hora del juego y, a continuación, haga clic en **generar Token**.

![Password][api-management-password]

> [!IMPORTANT]
> Anote esta contraseña. Una vez que abandona esta contraseña de Hola de página no se mostrará nuevo.
> 
> 

Hola uso Hola Git Bash en los ejemplos siguientes de la herramienta de [Git para Windows](http://www.git-scm.com/downloads) , pero puede utilizar cualquier herramienta de Git que estás familiarizado con.

Abra la herramienta de Git en la carpeta que desee hello y ejecute Hola siguiendo el equipo local del tooyour de repositorio de comando tooclone Hola git, mediante comandos Hola proporcionada por el portal para desarrolladores de Hola.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Proporcione el nombre de usuario de hello y una contraseña cuando se le solicite.

Si aparece algún error, intente modificar la `git clone` comando tooinclude Hola nombre y contraseña, como se muestra en el siguiente ejemplo de Hola.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Si se trata de un error, pruebe a parte de la contraseña del comando de Hola Hola de codificación de direcciones URL. Toodo de una forma rápida es tooopen Visual Studio y comando siguiente de Hola de problema en hello **ventana Inmediato**. Hola tooopen **ventana Inmediato**, abra ninguna solución ni proyecto en Visual Studio (o cree una nueva aplicación de consola vacía) y elija **Windows**, **inmediato** desde Hola **depurar** menú.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Usar la contraseña de hello codificado junto con su nombre y del repositorio ubicación tooconstruct Hola git comando user.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Una vez que se clona repositorio Hola puede ver y trabajar con ellos en el sistema de archivos local. Para más información, consulte [Referencia de estructura de archivo y carpeta del repositorio local de Git](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate el repositorio local con la configuración de instancia de servicio más reciente de Hola
Si realiza la instancia de servicio de administración de API de cambios tooyour en portal para desarrolladores de Hola o mediante la API de REST de hello, debe guardar estos repositorio de toohello de cambios para que pueda actualizar el repositorio local con los cambios más recientes de Hola. toodo, haga clic en **Guardar configuración toorepository** en hello **repositorio de configuración** pestaña en el portal para desarrolladores de hello y, a continuación, emita Hola siguiente comando en el repositorio local.

```
git pull
```

Antes de ejecutar `git pull` Asegúrese de que se encuentra en la carpeta de hello para el repositorio local. Si acaba de completar el Hola `git clone` comando, tendrá que cambiar tooyour repositorio de hello directorio mediante la ejecución de un comando similar al siguiente Hola.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>cambios de toopush desde el repositorio de servidor toohello repositorio local
toopush cambia desde el repositorio del servidor toohello repositorio local, debe confirmar los cambios y, a continuación, insertarlas toohello repositorio del servidor. toocommit los cambios, abra la herramienta de comandos Git, conmutador toohello directorio del repositorio local y Hola problema después de comandos.

```
git add --all
git commit -m "Description of your changes"
```

toopush todos Hola confirma toohello server, ejecute Hola después del comando.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy las instancias del servicio de administración de API de servicio configuración cambios toohello
Una vez que los cambios locales están insertadas y sin confirmar toohello repositorio del servidor, puede implementarlos tooyour instancia del servicio de administración de API.

![Implementación][api-management-configuration-deploy]

Para obtener información acerca de cómo realizar esta operación mediante la API de REST de hello, consulte [implementar Git cambia mediante Hola API de REST de base de datos de tooconfiguration](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Referencia de estructura de archivo y carpeta del repositorio local de Git
Hello archivos y carpetas en el repositorio de git local Hola contienen Hola información de configuración acerca de la instancia de servicio de Hola.

| Elemento | Description |
| --- | --- |
| carpeta raíz de la administración de API |Contiene la configuración de nivel superior para la instancia de servicio de Hola |
| carpeta de API |Contiene la configuración de Hola de hello API de instancia de servicio de Hola |
| carpeta de grupos |Contiene configuración de Hola para grupos de hello en la instancia de servicio de Hola |
| carpeta de directivas |Contiene directivas de hello en la instancia de servicio de Hola |
| carpeta portalStyles |Contiene la configuración de Hola de personalizaciones del portal para desarrolladores hello en la instancia de servicio de Hola |
| carpeta de productos |Contiene configuración de Hola para productos de hello en la instancia de servicio de Hola |
| carpeta de plantillas |Contiene la configuración de Hola de plantillas de correo electrónico de hello en la instancia de servicio de Hola |

Cada carpeta puede contener uno o varios archivos y, en algunos casos, una o varias carpetas; por ejemplo, una carpeta para cada API, producto o grupo. Hola archivos dentro de cada carpeta son específicos para el tipo de entidad Hola descrito por el nombre de la carpeta de Hola.

| Tipo de archivo | Propósito |
| --- | --- |
| json |Información de configuración acerca de la entidad respectiva Hola |
| html |Descripciones de entidad de hello, a menudo se muestran en el portal para desarrolladores de Hola |
| xml |Policy statements |
| css |Hojas de estilo para la personalización del portal para desarrolladores |

Estos archivos pueden crear, eliminar, editar y administran en el sistema de archivos local e implementen los cambios de hello toohello espera su instancia de servicio de administración de API.

> [!NOTE]
> Hola entidades siguientes no están contenidas en el repositorio de Git de hello y no se puede configurar mediante Git.
> 
> * Usuarios
> * Suscripciones
> * Propiedades
> * Entidades del portal de desarrolladores distintas de los estilos
> 
> 

### <a name="root-api-management-folder"></a>Carpeta raíz de la administración de API
raíz de Hello `api-management` carpeta contiene un `configuration.json` archivo que contiene información acerca de la instancia de servicio de Hola Hola siguiendo el formato de nivel superior.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

Hola primero cuatro opciones (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, y `UserRegistrationTermsConsentRequired`) asignar toohello siguiente configuración de hello **identidades** ficha hello **seguridad** sección.

| Configuración de identidad | Se asigna demasiado|
| --- | --- |
| RegistrationEnabled |**Redirigir a los usuarios anónimos en toosign página** casilla de verificación |
| UserRegistrationTerms |**Condiciones de uso del registro de usuario** |
| UserRegistrationTermsEnabled |**Mostrar condiciones de uso en la página de registro** |
| UserRegistrationTermsConsentRequired |**Requerir consentimiento** |

![Configuración de identidad][api-management-identity-settings]

Hola siguientes cuatro valores (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, y `DelegationValidationKey`) asignar toohello siguiente configuración de hello **delegación** ficha hello **seguridad** sección.

| Configuración de delegación | Se asigna demasiado|
| --- | --- |
| DelegationEnabled |Casilla **Delegar inicio de sesión y registro** |
| DelegationUrl |**Dirección URL del punto de conexión de delegación** |
| DelegatedSubscriptionEnabled |**Delegar suscripción de producto** |
| DelegationValidationKey |**Delegar clave de validación** |

![Configuración de delegación][api-management-delegation-settings]

Hola valor final, `$ref-policy`, asigna el archivo de instrucciones de directiva global toohello para la instancia de servicio de Hola.

### <a name="apis-folder"></a>carpeta de API
Hola `apis` carpeta contiene una carpeta para cada API de instancia de servicio de Hola que contiene los siguientes elementos de Hola.

* `apis\<api name>\configuration.json`-Esto es configuración de Hola para hello API y contiene información acerca de la dirección URL del servicio de back-end de Hola y las operaciones de Hola. Se trata de hello misma información que se devolverían si estuviera toocall [obtener una API específica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) con `export=true` en `application/json` formato.
* `apis\<api name>\api.description.html`-Esto es una descripción de Hola de hello API y corresponde toohello `description` propiedad de hello [entidad de API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`-Esta carpeta contiene `<operation name>.description.html` archivos que se asignan las operaciones de toohello Hola API. Cada archivo contiene la descripción de Hola de una sola operación Hola API que se asigna toohello `description` propiedad de hello [entidad de operación](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) Hola API de REST.

### <a name="groups-folder"></a>carpeta de grupos
Hola `groups` carpeta contiene una carpeta para cada grupo definido en la instancia de servicio de Hola.

* `groups\<group name>\configuration.json`-es configuración de hello para el grupo de Hola. Se trata de hello misma información que se devolverían si estuviera hello toocall [obtener un grupo específico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operación.
* `groups\<group name>\description.html`-Esto es Hola descripción del grupo de Hola y corresponde toohello `description` propiedad de hello [grupo entidad](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>carpeta de directivas
Hola `policies` carpeta contiene las instrucciones de directiva de hello para la instancia de servicio.

* `policies\global.xml` : contiene las directivas definidas en el ámbito global para la instancia de servicio.
* `policies\apis\<api name>\`: si tiene directivas definidas en el ámbito de la API, se encuentran en esta carpeta.
* `policies\apis\<api name>\<operation name>\`carpeta - si tiene las directivas definidas en el ámbito de la operación, se incluyen en esta carpeta en `<operation name>.xml` archivos que se asignan las instrucciones de directiva de toohello para cada operación.
* `policies\products\`-Si tiene las directivas definidas en el ámbito del producto, se incluyen en esta carpeta, que contiene `<product name>.xml` archivos que se asignan las instrucciones de directiva de toohello para cada producto.

### <a name="portalstyles-folder"></a>carpeta portalStyles
Hola `portalStyles` carpeta contiene la configuración y hojas de estilo para las personalizaciones de portal de desarrollador para la instancia de servicio de Hola.

* `portalStyles\configuration.json`-contiene nombres de Hola Hola de hojas de estilos utilizados por el portal para desarrolladores de Hola
* `portalStyles\<style name>.css`-cada `<style name>.css` archivo contiene estilos para el portal para desarrolladores de hello (`Preview.css` y `Production.css` de forma predeterminada).

### <a name="products-folder"></a>carpeta de productos
Hola `products` carpeta contiene una carpeta para cada producto definido en la instancia de servicio de Hola.

* `products\<product name>\configuration.json`-se trata de configuración de hello para el producto de Hola. Se trata de hello misma información que se devolverían si estuviera hello toocall [obtener un producto específico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operación.
* `products\<product name>\product.description.html`-Esto es una descripción de Hola de producto de Hola y corresponde toohello `description` propiedad de hello [entidad product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) Hola API de REST.

### <a name="templates"></a>plantillas
Hola `templates` carpeta contiene la configuración de hello [plantillas de correo electrónico](api-management-howto-configure-notifications.md) de instancia de servicio de Hola.

* `<template name>\configuration.json`-se trata de configuración de hello para la plantilla de correo electrónico de Hola.
* `<template name>\body.html`-Éste es Hola cuerpo de plantilla de correo electrónico de Hola.

## <a name="next-steps"></a>Pasos siguientes
Para obtener información sobre otra maneras de toomanage su instancia de servicio, vea:

* Administrar la instancia de servicio con hello siguientes cmdlets de PowerShell
  * [Azure API Management Deployment Management Cmdlets (Cmdlets de administración de la implementación de Administración de API de Azure)](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Azure API Management Service Management Cmdlets (Cmdlets de administración del servicio Administración de API de Azure)](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Administrar la instancia de servicio en el portal para desarrolladores de Hola
  * [Administración de su primera API en Administración de API de Azure](api-management-get-started.md)
* Administrar la instancia de servicio mediante la API de REST de Hola
  * [API Management REST API (API de REST de Administración de API)](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>Vea un vídeo de introducción.
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




