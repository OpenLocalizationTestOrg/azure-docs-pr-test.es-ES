---
title: "aaaGet a trabajar con el almacén de claves de Azure | Documentos de Microsoft"
description: "Use este tutorial toohelp obtendrá a trabajar con el almacén de claves de Azure toocreate un contenedor reforzado en Azure, toostore y administrar las claves criptográficas y secretos en Azure."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Introducción al Almacén de claves de Azure
Almacén de claves de Azure está disponible en la mayoría de las regiones. Para obtener más información, vea hello [almacén de claves de página de precios](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introducción
Use este tutorial toohelp obtendrá a trabajar con el almacén de claves de Azure toocreate un contenedor reforzado (un almacén) en Azure, toostore y administrar las claves criptográficas y secretos en Azure. Le guiará por proceso de Hola de uso de PowerShell de Azure toocreate un almacén que contiene una clave o contraseña que puede utilizar con una aplicación de Azure. A continuación, se explica cómo usa una aplicación esa clave o contraseña.

**Estimado toocomplete de tiempo:** 20 minutos

> [!NOTE]
> Este tutorial no incluye instrucciones de cómo toowrite Hola aplicación de Azure que incluye uno de los pasos de hello, a saber cómo tooauthorize una toouse una clave de aplicación o un secreto en clave Hola almacén.
>
> En este tutorial se usa Azure PowerShell. Para obtener instrucciones acerca de la interfaz de la línea de comandos para todas las plataformas, consulte [este tutorial equivalente](key-vault-manage-with-cli2.md).
>
>

Para obtener información general sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de clave de Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, debe tener Hola siguientes:

* Un tooMicrosoft de suscripción de Azure. Si no tiene, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell, **versión mínima: 1.1.0**. tooinstall PowerShell de Azure y asociarlo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). Si ya ha instalado Azure PowerShell y no conoce la versión de hello, desde la consola de PowerShell de Azure de hello, escriba `(Get-Module azure -ListAvailable).Version`. Si tiene Azure PowerShell versiones 0.9.1 a 0.9.8 instalado, también puede usar este tutorial con algunos cambios menores. Por ejemplo, debe usar hello `Switch-AzureMode AzureResourceManager` comando y algunos comandos de almacén de claves de Azure Hola han cambiado. Para obtener una lista de cmdlets de almacén de claves para las versiones 0.9.1 a través de 0.9.8 hello, consulte [Cmdlets del almacén de claves de Azure](/powershell/module/azurerm.keyvault/#key_vault).
* Una aplicación para que esté configurado toouse clave de Hola o la contraseña que creará en este tutorial. Una aplicación de ejemplo está disponible en hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343). Para obtener instrucciones, consulte Hola que acompaña a archivo Léame.

Este tutorial está diseñado para principiantes de PowerShell de Azure, pero da por supuesto que comprende los conceptos básicos de hello, como módulos, cmdlets y las sesiones. Para obtener más información, consulte [Introducción a Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).

tooget ayuda detallada de cualquier cmdlet que se ve en este tutorial, use hello **Get-Help** cmdlet.

    Get-Help <cmdlet-name> -Detailed

Por ejemplo, tooget ayuda para hello **AzureRmAccount de inicio de sesión** cmdlet, escriba:

    Get-Help Login-AzureRmAccount -Detailed

También puede leer Hola después tutoriales tooget familiarizado con Azure Resource Manager de Azure PowerShell:

* [¿Cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview)
* [Uso de Azure PowerShell con el Administrador de recursos](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Conectar tooyour suscripciones
Inicie una sesión de PowerShell de Azure e inicie sesión en tooyour cuenta de Azure con hello siguiente comando:  

    Login-AzureRmAccount

Tenga en cuenta que si usa una instancia específica de Azure, por ejemplo, el gobierno de Azure, use Hola - parámetro de entorno con este comando. Por ejemplo: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

En la ventana emergente del explorador de hello, escriba el nombre de usuario de cuenta de Azure y la contraseña. PowerShell de Azure Obtiene todas las suscripciones de Hola que están asociadas a esta cuenta y de forma predeterminada, usa Hola primero.

Si tiene varias suscripciones y desea toospecify un uno toouse específico para el almacén de claves de Azure, escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:

    Get-AzureRmSubscription

A continuación, toospecify Hola suscripción toouse, tipo:

    Set-AzureRmContext -SubscriptionId <subscription ID>

Para obtener más información acerca de cómo configurar Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a id="resource"></a>Creación de un nuevo grupo de recursos
Cuando se utiliza el Administrador de recursos de Azure, todos los recursos relacionados se crean dentro de un grupo de recursos. Crearemos un nuevo grupo de recursos denominado **ContosoResourceGroup** para este tutorial:

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>Creación de un Almacén de claves
Hola de uso [AzureRmKeyVault New](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate un almacén de claves. Este cmdlet tiene tres parámetros obligatorios: un **nombre del grupo de recursos**, **nombre de almacén de claves**, hello y **ubicación geográfica**.

Por ejemplo, si utiliza el nombre de almacén de Hola de **ContosoKeyVault**, nombre de grupo de recursos de Hola de **ContosoResourceGroup**y la ubicación de Hola de **Asia oriental**, tipo:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

salida de Hello de este cmdlet muestra propiedades del almacén de claves de Hola que acaba de crear. propiedades de Hello dos más importantes son:

* **El nombre del almacén**: en el ejemplo de Hola, esto es **ContosoKeyVault**. Utilizará este nombre para otros cmdlets del Almacén de claves.
* **URI de almacén**: en el ejemplo de Hola, es https://contosokeyvault.vault.azure.net/. Las aplicaciones que utilizan el almacén a través de su API de REST deben usar este identificador URI.

Su cuenta de Azure es ahora tooperform autorizado cualquier operación en esta clave de seguridad del almacén. Hasta el momento, nadie más lo está.

> [!NOTE]
> Si ve el error de hello **Hola suscripción no está registrado toouse de espacio de nombres 'Microsoft.KeyVault'** cuando intente toocreate el almacén de claves nuevo, ejecute `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` y, a continuación, vuelva a ejecutar el comando New-AzureRmKeyVault. Para más información, consulte [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).
>
>

## <a id="add"></a>Agregar una clave o un almacén de claves secretas toohello
Si desea que el almacén de claves de Azure toocreate una clave protegida por software automáticamente, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet y escriba Hola siguiente:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

Sin embargo, si tiene una clave protegida por software existente en una. Unidad tooyour de guardar el archivo PFX C:\ en un archivo denominado softkey.pfx que desea tooupload tooAzure el almacén de claves, Hola tipo después de variable de hello tooset **securepfxpwd** para una contraseña de **123** para saludo. Archivo PFX:

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

A continuación, escriba Hola siguientes clave de hello tooimport de Hola. Archivo PFX, que protege la clave de hello mediante software en hello servicio Almacén de claves:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


Ahora puede hacer referencia a esta clave que se creó o cargó tooAzure el almacén de claves, utilizando su URI. Usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obtener la versión actual de Hola y usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget esta versión específica.  

toodisplay hello URI para esta clave, tipo:

    $Key.key.kid

tooadd un almacén toohello secreta, que es una contraseña denominada SQLPassword y tiene el valor Hola de Pa$ $w0rd tooAzure el almacén de claves, convierta primero el valor de Hola de cadena segura de Pa$ $w0rd tooa escribiendo Hola siguiente:

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

A continuación, escriba lo siguiente hello:

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

Ahora puede hacer referencia a esta contraseña que agregó tooAzure el almacén de claves, mediante el uso de su URI. Usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obtener la versión actual de Hola y usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget esta versión específica.

toodisplay hello URI para este secreto, tipo:

    $secret.Id

Vamos a ver clave de Hola o el secreto que acaba de crear:

* tooview el tipo de clave,:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview el secreto, tipo:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

Ahora, el almacén de claves y la clave o el secreto está lista para toouse de aplicaciones. Debe autorizar aplicaciones toouse ellos.  

## <a id="register"></a>Registro de una aplicación con Azure Active Directory
Este paso lo haría normalmente un programador en un equipo independiente. No es específico tooAzure el almacén de claves, pero se incluye aquí para integridad.

> [!IMPORTANT]
> tutorial de hello toocomplete, tu cuenta, el almacén de Hola y aplicación hello que se registren en este paso deben ser Hola mismo directorio de Azure.
>
>

Las aplicaciones que utilizan un Almacén de claves deben autenticarse utilizando un token de Azure Active Directory. toodo, Hola propietario de la aplicación hello en primer lugar debe registrar la aplicación hello en su Azure Active Directory. Al final de Hola de registro, propietario de la aplicación hello obtiene Hola siguientes valores:

* Un **Id. de aplicación** (también conocido como un Id. de cliente) y **clave de autenticación** (también conocido como Hola secreto compartido). aplicación Hello debe presentar un token de ambos estos valores tooAzure Active Directory, tooget. Forma de la aplicación hello configurado toodo que esto depende de la aplicación hello. Para la aplicación de ejemplo de almacén de claves de hello, propietario de la aplicación hello establece estos valores en el archivo app.config de hello.

aplicación de hello tooregister en Azure Active Directory:

1. Inicie sesión en toohello portal de Azure clásico.
2. Hola izquierda, haga clic en **Active Directory**y, a continuación, seleccione directorio de hello en el que se vaya a registrar la aplicación. <br> <br> **Nota:** debe seleccionar Hola mismo directorio que contiene Hola suscripción de Azure con la que se creó el almacén de claves. Si no sabe qué directorio esto es, haga clic en **configuración**, identificar suscripción Hola con la que se creó el almacén de claves y muestra el nombre de Hola de nota del directorio de hello en la última columna de Hola.
3. Haga clic en **Aplicaciones**. Si no hay aplicaciones se han agregado tooyour directorio, esta página muestra solo hello **agregar una aplicación** vínculo. Haga clic en el vínculo de Hola o, como alternativa, puede hacer clic en **agregar** en la barra de comandos de Hola.
4. Hola **Agregar aplicación** asistente, en hello **especifique qué desea toodo?** página, haga clic en **agregar una aplicación que mi organización está desarrollando**.
5. En hello **envíenos comentarios acerca de la aplicación** página, especifique un nombre para la aplicación y, a continuación, seleccione **aplicación WEB Y/O API de WEB** (Hola de forma predeterminada). Haga clic en hello **siguiente** icono.
6. En hello **propiedades de la aplicación** página, especifique hello **dirección URL de inicio de sesión** y **APP ID URI** para la aplicación web. Si la aplicación no tiene estos valores, puede inventárselos en este paso (por ejemplo, puede especificar http://test1.contoso.com en ambos cuadros). No importa si los sitios existen. Lo importante es que esa aplicación hello identificador URI para cada aplicación es diferente para cada aplicación en el directorio. directorio de Hello usa este tooidentify de cadena de la aplicación.
7. Haga clic en hello **completar** icono toosave los cambios en el Asistente de Hola.
8. En hello **inicio rápido** página, haga clic en **configurar**.
9. Desplácese toohello **claves** sección, seleccione la duración de hello y, a continuación, haga clic en **guardar**. página de Hello actualiza y muestra ahora un valor de clave. Debe configurar la aplicación con este valor de clave y hello **Id. de cliente** valor. (las instrucciones para realizar esta configuración son específicas para la aplicación).
10. Copie el valor de identificador de cliente de Hola desde esta página, que se usará en el siguiente paso tooset permisos de hello en el almacén.

## <a id="authorize"></a>Autorizar Hola aplicación toouse Hola clave o el secreto
tooauthorize Hola aplicación tooaccess Hola clave o el secreto en el almacén de hello, use la [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.

Por ejemplo, si el nombre del almacén es **ContosoKeyVault** y aplicación hello desea tooauthorize tiene un identificador de cliente de 8f8c4bbd 485b 45fd 98f7 ec6300b7b4ed y desea tooauthorize Hola aplicación toodecrypt e inicie sesión con claves en el almacén, ejecute hello siguiente:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Si desea tooauthorize ese mismo secretos tooread de aplicación en el almacén, ejecute hello siguiente:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>Si desea que toouse un módulo de seguridad de hardware (HSM)
Para mayor seguridad, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no dejan nunca el límite de HSM Hola. Hola HSM son FIPS 140-2 nivel 2 validado. Si este requisito no aplica tooyou, omita esta sección y vaya demasiado[eliminar el almacén de claves de Hola y las claves asociadas y secretos](#delete).

toocreate estas claves protegidas con HSM, debe usar hello [claves protegidas con HSM de toosupport de nivel de servicio Premium de almacén de Azure clave](https://azure.microsoft.com/pricing/free-trial/). Además, tenga en cuenta que esta funcionalidad no está disponible para Azure China.

Cuando se crea el almacén de claves de hello, agregar hello **- SKU** parámetro:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



Puede agregar las claves protegidas por software (como se muestra anteriormente) y el almacén de claves toothis claves protegidas con HSM. toocreate una clave protegida por HSM, conjunto hello **-destino** too'HSM de parámetro ':

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

Puede usar una clave de Hola después tooimport comando una. Archivo PFX en el equipo. Este comando importa una clave hello en HSM Hola servicio Almacén de claves:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


comando siguiente de Hello importa una opción "traiga su propia clave" paquete (BYOK). Este escenario le permite generar su clave de HSM local y se transfiere tooHSMs Hola servicio de almacén de claves, sin clave Hola dejando límite de HSM hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

Para obtener más instrucciones sobre cómo toogenerate este paquete BYOK, vea [cómo toogenerate y transferencia de claves protegidas con HSM para el almacén de claves de Azure](key-vault-hsm-protected-keys.md).

## <a id="delete"></a>Eliminar el almacén de claves de Hola y las claves asociadas y secretos
Si ya no necesita el almacén de claves hello y clave de Hola o al secreto que contiene, puede eliminar el almacén de claves hello mediante hello [Remove-AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

O bien, puede eliminar un grupo de recursos de Azure completo, que incluye el almacén de claves de Hola y otros recursos que incluyen en ese grupo:

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>Otros cmdlets de Azure PowerShell
Estos son otros comandos que pueden resultar útiles para administrar el Almacén de claves de Azure.

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: este comando ofrece una presentación tabular de todas las claves y las propiedades seleccionadas.
* `$Keys[0]`: Este comando muestra una lista completa de propiedades de clave especificado Hola
* `Get-AzureKeyVaultSecret`: este comando muestra una presentación tabular de todos nombres de secretos y las propiedades que se elijan.
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Ejemplo cómo tooremove una clave específica.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Ejemplo cómo tooremove un secreto específico.

## <a id="next"></a>Pasos siguientes
Para obtener un tutorial de seguimiento que usa el Almacén de claves de Azure en una aplicación web, consulte [Uso del Almacén de claves de Azure desde una aplicación web](key-vault-use-from-web-application.md).

toosee cómo se utiliza el almacén de claves, consulte [registro de almacén de claves de Azure](key-vault-logging.md).

Para obtener una lista de cmdlets de PowerShell de Azure más recientes de hello para el almacén de claves de Azure, consulte [Cmdlets del almacén de claves de Azure](/powershell/module/azurerm.keyvault/#key_vault).

Para las referencias de programación, vea [Hola Guía del desarrollador de almacén de claves de Azure](key-vault-developers-guide.md).
