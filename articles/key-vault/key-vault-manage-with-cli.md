---
title: "aaaManage con CLI del almacén de claves de Azure | Documentos de Microsoft"
description: "Usar tareas de este tutorial tooautomate en el almacén de claves mediante Hola CLI"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a>Administración del Almacén de claves mediante CLI

Almacén de claves de Azure está disponible en la mayoría de las regiones. Para obtener más información, vea hello [almacén de claves de página de precios](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introducción

Use este tutorial toohelp obtendrá a trabajar con el almacén de claves de Azure toocreate un contenedor reforzado (un almacén) en Azure, toostore y administrar las claves criptográficas y secretos en Azure. Le guiará por proceso de Hola de uso de interfaz de línea de comandos entre plataformas de Azure toocreate un almacén que contiene una clave o contraseña que puede utilizar con una aplicación de Azure. A continuación, se explica cómo utiliza una aplicación esa clave o contraseña.

**Estimado toocomplete de tiempo:** 20 minutos

> [!NOTE]
> Este tutorial no incluye instrucciones sobre cómo toowrite Hola aplicación de Azure que incluye uno de los pasos de hello, que muestra cómo tooauthorize una toouse una clave de aplicación o un secreto de clave de hello almacén.
> 
> Actualmente, no se puede configurar el almacén de claves de Azure en hello portal de Azure. En su lugar, use estas instrucciones sobre la interfaz de la línea de comandos multiplataforma. O bien, para obtener instrucciones de Azure PowerShell, consulte [este tutorial equivalente](key-vault-get-started.md).
> 
> 

Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial, debe tener Hola siguientes:

* Un tooMicrosoft de suscripción de Azure. Si no tiene una, puede registrarse para obtener una versión de [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial).
* Versión 0.9.1 o una posterior de la interfaz de la línea de comandos. tooinstall Hola versión más reciente y conectar tooyour suscripción de Azure, consulte [instalar y configurar la interfaz de línea de comandos entre plataformas de Azure de Hola](../cli-install-nodejs.md).
* Una aplicación para que esté configurado toouse clave de Hola o la contraseña que creará en este tutorial. Una aplicación de ejemplo está disponible en hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Para obtener instrucciones, consulte Hola que acompaña a archivo Léame.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Obtención de ayuda con la interfaz de la línea de comandos entre plataformas de Azure

Este tutorial se da por supuesto que está familiarizado con la interfaz de línea de comandos de hello (intensiva de errores, Terminal, símbolo del sistema)

Hello--ayuda o -h parámetro puede ser utilizados tooview ayuda para comandos específicos. Como alternativa, help hello azure [comando] [opciones] formato también puede ser usado tooreturn Hola misma información. Por ejemplo, siguiente Hola comandos devuelven todos los Hola la misma información:

    azure account set --help

    azure account set -h

    azure help account set

En caso de duda acerca de los parámetros de hello necesarios para un comando, consulte usar toohelp--ayuda, -h o azure help [comando].

También puede leer Hola después tutoriales tooget familiarizado con Azure Resource Manager en el interfaz de línea de comandos de plataforma cruzada de Azure:

* [¿Cómo tooinstall y configurar la interfaz de línea de comandos entre plataformas de Azure](../cli-install-nodejs.md)
* [Uso de la interfaz de la línea de comandos entre plataformas de Azure con el Administrador de recursos de Azure](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a>Conectar tooyour suscripciones

toolog sesión con una cuenta profesional, Hola de uso siguiente comando:

    azure login -u username -p password

o si desea toolog escribiendo interactivamente

    azure login

> [!NOTE]
> método de inicio de sesión de Hello solo funciona con la cuenta de la organización. Una cuenta profesional es un usuario administrado por su organización y definido en su inquilino de Azure Active Directory de la organización.
> 
> 

Si no tiene actualmente una cuenta profesional y está usando un toolog de cuenta de Microsoft en tooyour suscripción de Azure, puede crear fácilmente uno que use Hola lo siguiente.

1. Toohello de inicio de sesión de inicio de sesión toohello [Portal de administración de Azure](https://manage.windowsazure.com/)y haga clic en Active Directory.
2. Si no existe ningún directorio, seleccione crear su directorio y Hola de proporcionar la información solicitada.
3. Seleccione su directorio y agregue un nuevo usuario. Este nuevo usuario es una cuenta profesional. Durante la creación del usuario de Hola Hola será proporcionado con una dirección de correo electrónico para el usuario de hello y una contraseña temporal. Guarde esta información para usarla en otro paso.
4. En el portal de hello, seleccione Configuración y, a continuación, seleccione los administradores. Seleccione Agregar y agregar Hola nuevo usuario como Coadministrador. Esto permite Hola cuenta profesional toomanage su suscripción de Azure.
5. Por último, cierre la sesión de hello portal de Azure y, a continuación, volver a iniciar sesión con la nueva cuenta organizativa de Hola. Si ésta es la primera vez que inicia sesión con esta cuenta de hello, será la contraseña de hello toochange solicitadas.

Para obtener más información acerca de cómo usar una cuenta profesional con Microsoft Azure, consulte [Inicio de sesión como organización en Microsoft Azure](../active-directory/sign-up-organization.md).

Si tiene varias suscripciones y desea toospecify un uno toouse específico para el almacén de claves de Azure, escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:

    azure account list

A continuación, toospecify Hola suscripción toouse, tipo:

    azure account set <subscription name>

Para obtener más información acerca de cómo configurar la interfaz de línea de comandos entre plataformas de Azure, consulte [cómo tooInstall y configurar Azure multiplataforma de línea de comandos interfaz](../cli-install-nodejs.md).

## <a name="switch-toousing-azure-resource-manager"></a>Conmutador toousing Azure Resource Manager
Hola el almacén de claves requiere Azure Resource Manager, así que escriba Hola siguiendo el modo de tooswitch tooAzure Resource Manager:

    azure config mode arm

## <a name="create-a-new-resource-group"></a>Creación de un nuevo grupo de recursos
Cuando se utiliza el Administrador de recursos de Azure, todos los recursos relacionados se crean dentro de un grupo de recursos. Crearemos un nuevo grupo de recursos denominado 'ContosoResourceGroup' para este tutorial.

    azure group create 'ContosoResourceGroup' 'East Asia'

Hola primer parámetro es el nombre del grupo de recursos y Hola segundo parámetro es la ubicación de Hola. Para la ubicación, utilice el comando de hello `azure location list` tooidentify cómo toospecify una ubicación alternativa toohello uno en este ejemplo. Si necesita más información, escriba: `azure help location`

## <a name="register-hello-key-vault-resource-provider"></a>Registrar el proveedor de recursos de almacén de claves de Hola
Asegúrese de que el proveedor de recursos de Almacén de claves está registrado en la suscripción:

`azure provider register Microsoft.KeyVault`

Solo es necesario toobe efectuar una vez por cada suscripción.

## <a name="create-a-key-vault"></a>Creación de un Almacén de claves

Hola de uso `azure keyvault create` comando toocreate un almacén de claves. Esta secuencia de comandos tiene tres parámetros obligatorios: un nombre de grupo de recursos, un nombre de almacén de claves y la ubicación geográfica de Hola.

Por ejemplo, si utiliza el nombre de almacén de Hola de ContosoKeyVault, nombre de grupo de recursos de Hola de ContosoResourceGroup y la ubicación de Hola de Asia oriental, escriba:

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

salida de Hello de este comando muestra propiedades del almacén de claves de Hola que acaba de crear. propiedades de Hello dos más importantes son:

* **Nombre**: en el ejemplo de Hola es ContosoKeyVault. Utilizará este nombre para otros cmdlets del Almacén de claves.
* **vaultUri**: en el ejemplo de Hola es https://contosokeyvault.vault.azure.net. Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.

Su cuenta de Azure es ahora tooperform autorizado cualquier operación en esta clave de seguridad del almacén. Hasta el momento, nadie más lo está.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Agregar una clave o un almacén de claves secretas toohello

Si desea que el almacén de claves de Azure toocreate una clave protegida por software automáticamente, use hello `azure key create` de comandos y escriba Hola siguiente:

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

Sin embargo, si tiene una clave existente en un archivo PEM guardado como archivo local en un archivo denominado softkey.pem que desea tooupload tooAzure el almacén de claves, escriba Hola siguientes clave de hello tooimport de Hola. Archivo PEM, que protege la clave de hello mediante software en hello servicio Almacén de claves:

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

Ahora puede hacer referencia a clave de Hola que creó o cargó tooAzure el almacén de claves, utilizando su URI. Usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obtener la versión actual de Hola y usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget esta versión específica.

tooadd un almacén toohello secreta, que es una contraseña denominada SQLPassword y no tiene valor de Hola de Pa$ $w0rd tooAzure el almacén de claves, Hola de tipo siguientes:

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

Ahora puede hacer referencia a esta contraseña que agregó tooAzure el almacén de claves, mediante el uso de su URI. Usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obtener la versión actual de Hola y usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget esta versión específica.

Vamos a ver clave de Hola o el secreto que acaba de crear:

* tooview el tipo de clave,:`azure keyvault key list --vault-name 'ContosoKeyVault'`
* tooview el secreto, tipo:`azure keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Registro de una aplicación con Azure Active Directory

Este paso lo haría normalmente un programador en un equipo independiente. No es específico tooAzure el almacén de claves, pero se incluye aquí para integridad.

> [!IMPORTANT]
> tutorial de hello toocomplete, tu cuenta, el almacén de Hola y aplicación hello que se registren en este paso deben ser Hola mismo directorio de Azure.
> 
> 

Las aplicaciones que utilizan un Almacén de claves deben autenticarse utilizando un token de Azure Active Directory. toodo, Hola propietario de la aplicación hello en primer lugar debe registrar la aplicación hello en su Azure Active Directory. Al final de Hola de registro, propietario de la aplicación hello obtiene Hola siguientes valores:

* Un **Id. de aplicación** (también conocido como un Id. de cliente) y **clave de autenticación** (también conocido como Hola secreto compartido). aplicación Hello debe presentar ambos de estos tooAzure valores tooget un símbolo (token) de Active Directory. Forma de la aplicación hello configurado toodo que esto depende de la aplicación hello. Para la aplicación de ejemplo de almacén de claves de hello, propietario de la aplicación hello establece estos valores en el archivo app.config de hello.

aplicación de hello tooregister en Azure Active Directory:

1. Inicie sesión en toohello portal de Azure.
2. Hola izquierda, haga clic en **Active Directory**y, a continuación, seleccione directorio de hello en el que se vaya a registrar la aplicación. <br> <br> 

>[!NOTE] 
> Debe seleccionar Hola mismo directorio que contiene Hola suscripción de Azure con la que se creó el almacén de claves. Si no sabe qué directorio esto es, haga clic en **configuración**, identificar suscripción Hola con la que se creó el almacén de claves y muestra el nombre de Hola de nota del directorio de hello en la última columna de Hola.

3. Haga clic en **Aplicaciones**. Si no hay aplicaciones se han agregado tooyour directorio, esta página mostrará solo hello **agregar una aplicación** vínculo. Haga clic en el vínculo de Hola o, como alternativa, puede hacer clic en hello **agregar** en la barra de comandos de Hola.
4. Hola **Agregar aplicación** asistente, en hello **especifique qué desea toodo?** página, haga clic en **agregar una aplicación que mi organización está desarrollando**.
5. En hello **envíenos comentarios acerca de la aplicación** página, especifique un nombre para la aplicación y seleccione **aplicación WEB Y/O API de WEB** (Hola de forma predeterminada). Haga clic en el icono siguiente Hola.
6. En hello **propiedades de la aplicación** página, especifique hello **dirección URL de inicio de sesión** y **APP ID URI** para la aplicación web. Si la aplicación no tiene estos valores, puede inventárselos en este paso (por ejemplo, puede especificar http://test1.contoso.com en ambos cuadros). No importa estos sitios, si existen. lo importante es que esa aplicación hello identificador URI para cada aplicación es diferente para cada aplicación en el directorio. directorio de Hello usa este tooidentify de cadena de la aplicación.
7. Haga clic en hello icono completa toosave los cambios en el Asistente de Hola.
8. En la página de inicio rápido de hello, haga clic en **configurar**.
9. Desplácese toohello **claves** sección, seleccione la duración de hello y, a continuación, haga clic en **guardar**. página de Hello actualiza y muestra ahora un valor de clave. Debe configurar la aplicación con este valor de clave y hello **Id. de cliente** valor. (Las instrucciones para realizar esta configuración serán específicas para la aplicación).
10. Copie el valor de identificador de cliente de Hola desde esta página, que se usará en el siguiente paso tooset permisos de hello en el almacén.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Autorizar Hola aplicación toouse Hola clave o el secreto
tooauthorize Hola aplicación tooaccess Hola clave o el secreto en el almacén de hello, use hello `azure keyvault set-policy` comando.

Por ejemplo, si el nombre del almacén es aplicación hello y ContosoKeyVault desea tooauthorize tiene un identificador de cliente de 8f8c4bbd 485b 45fd 98f7 ec6300b7b4ed, y desea tooauthorize Hola aplicación toodecrypt e inicie sesión con las claves en el almacén, a continuación, ejecute hello Después de:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> Si se ejecutan en el símbolo del sistema de Windows, debe reemplazar las comillas simples entre comillas dobles y también de escape las comillas dobles interno Hola. Por ejemplo: "[\"decrypt\",\"sign\"]".
> 
> 

Si desea tooauthorize ese mismo secretos tooread de aplicación en el almacén, ejecute hello siguiente:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Si desea que toouse un módulo de seguridad de hardware (HSM)
Para mayor seguridad, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no dejan nunca el límite de HSM Hola. Hola HSM son FIPS 140-2 nivel 2 validado. Si este requisito no aplica tooyou, omita esta sección y vaya demasiado[eliminar el almacén de claves de Hola y las claves asociadas y secretos](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate estas claves protegidas con HSM, debe tener una suscripción de almacén que admita claves protegidas con HSM.

Cuando creas hello keyvault, Agregar parámetro de "sku" hello:

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

Puede agregar las claves protegidas por software (como se muestra anteriormente) y del almacén de claves protegidas con HSM toothis. toocreate una clave protegida por HSM, too'HSM del parámetro de destino de conjunto hello':

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

Puede usar Hola siguientes comando tooimport una clave de un archivo PEM en el equipo. Este comando importa una clave hello en HSM Hola servicio Almacén de claves:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

comando siguiente de Hello importa una opción "traiga su propia clave" paquete (BYOK). Esto le permite generar su clave de HSM local y se transfiere tooHSMs Hola servicio de almacén de claves, sin clave Hola dejando límite de HSM hello:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

Para obtener más instrucciones sobre cómo toogenerate este paquete BYOK, vea [cómo toouse HSM-Protected claves al almacén de claves de Azure](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Eliminar el almacén de claves de Hola y las claves asociadas y secretos
Si ya no necesita el almacén de claves hello y clave de Hola o al secreto que contiene, puede eliminar el almacén de claves de hello mediante comando de eliminación de keyvault hello azure:

    azure keyvault delete --vault-name 'ContosoKeyVault'

O bien, puede eliminar un grupo de recursos de Azure completo, que incluye el almacén de claves de Hola y otros recursos que incluyen en ese grupo:

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Otros comandos de la interfaz de la línea de comandos entre plataformas de Azure
Estos son otros comandos que pueden resultar útiles para administrar el Almacén de claves de Azure.

Este comando ofrece una presentación tabular de todas las claves y las propiedades seleccionadas.

    azure keyvault key list --vault-name 'ContosoKeyVault'

Este comando muestra una lista completa de propiedades para la clave especificada de hello:

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Este comando muestra una presentación tabular de todos nombres de secretos y las propiedades que se elijan.

    azure keyvault secret list --vault-name 'ContosoKeyVault'

Este es un ejemplo de cómo tooremove una clave específica:

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Este es un ejemplo de cómo tooremove un secreto específico:

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a>Pasos siguientes
Para las referencias de programación, vea [Hola Guía del desarrollador de almacén de claves de Azure](key-vault-developers-guide.md).

