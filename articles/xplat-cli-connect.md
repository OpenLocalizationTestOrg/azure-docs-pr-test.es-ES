---
title: aaaLog en tooAzure de hello CLI | Documentos de Microsoft
description: "Conectar tooyour suscripción de Azure de hello interfaz de línea de comandos (CLI de Azure) de Azure para Mac, Linux y Windows"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>Inicie sesión en tooAzure de hello CLI de Azure
Hola CLI de Azure es un conjunto de comandos de código abierto, multiplataforma para trabajar con recursos de Azure. Este artículo describe tooprovide de maneras diferentes de Hola la CLI de Azure de Hola de cuenta de Azure credenciales tooconnect tooyour suscripción de Azure:

* Ejecute hello `azure login` tooauthenticate de comando CLI a través de Azure Active Directory. Esto deja de método que acceder a los comandos de tooCLI tanto en [comando modos](#cli-command-modes). Cuando se ejecuta el comando hello sin opciones adicionales, `azure login` le pide que toocontinue inician sesión de forma interactiva a través de un portal web. Para más `azure login` opciones de comando, vea escenarios de hello en este artículo, o escriba `azure login --help`.
* Si solo necesita comandos CLI del modo de administración de servicios de Azure de toouse (no recomendados para la mayoría de las nuevas implementaciones), puede descargar e instalar un archivo de configuración de publicación en el equipo.

Si aún no ha instalado Hola CLI, consulte [Install hello Azure CLI](cli-install-nodejs.md). Si carece de una suscripción de Azure, puede crear una [cuenta de prueba gratuita](http://azure.microsoft.com/free/) en tan solo unos minutos.

Para obtener más información general sobre las diferentes identidades de cuenta y suscripciones de Azure, consulte [Asociación de las suscripciones de Azure con Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="scenario-1-azure-login-with-interactive-login"></a>Escenario 1: Inicio de sesión de Azure con inicio de sesión interactivo
Con algunas cuentas Hola CLI requiere toorun `azure login` y, a continuación, continuar el proceso de inicio de sesión de hello con un explorador web a través de un portal web, un proceso denominado *inicio de sesión interactivo*. Un motivo habitual es cuando se tiene una cuenta profesional o educativa (también denominado una *cuenta profesional*) que está configurado en la autenticación multifactor toorequire. Usar inicio de sesión interactivo con su cuenta de Microsoft, si desea que los comandos de modo de administrador de recursos de toouse.

Inicio de sesión interactivo es fácil: tipo `azure login` --sin ninguna opción--tal y como se muestra en el siguiente ejemplo de Hola:

```
azure login
```                                                                                             

salida de Hello aparece algo parecido a Hola siguiente:

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Copiar código de hello ofrecida tooyou en la salida del comando hello y abra un toohttp://aka.ms/devicelogin explorador u otra página si se especifica. (Puede abrir un explorador en hello mismo equipo, o en un dispositivo o equipo diferente.) Introduzca el código de hello y, a continuación, son tooenter solicitadas Hola username y password para identidad de hello desea toouse. Cuando se completa el proceso, shell de comandos de hello completa el inicio de sesión de Hola. Sería algo parecido a lo siguiente:

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> Con el inicio de sesión interactivo, la autenticación y la autorización se realizan con Azure Active Directory. Si usa una identidad de cuenta de Microsoft, proceso de inicio de sesión de hello tiene acceso a su dominio predeterminado de Azure Active Directory. (Si se registro para obtener una cuenta de Azure gratuita, Azure Active Directory creó automáticamente un dominio predeterminado para la cuenta).
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>Escenario 2: Inicio de sesión de Azure con un nombre de usuario y contraseña
Hola de uso `azure login` comando con el nombre de usuario de hello (`-u`) tooauthenticate del parámetro si desea que toouse un trabajo o escuela de la cuenta que no requiere la autenticación multifactor. Se le pida en línea de comandos de Hola para contraseña de hello (o si lo desea, puede pasar contraseña Hola como un parámetro adicional de hello `azure login` comando). Hello en el ejemplo siguiente se pasa Hola nombre de usuario de una cuenta de organización:

    azure login -u myUserName@contoso.onmicrosoft.com

Es, a continuación, se le pida tooenter la contraseña:

    info:    Executing command login
    Password: *********

a continuación, finaliza el proceso de inicio de sesión de Hola.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

Si se trata de su primera vez que inicia sesión con estas credenciales, se le preguntará tooverify que desea toocache un token de autenticación. Este mensaje también se produce si utilizara previamente hello `azure logout` comando (se describe más adelante en el artículo de hello). toobypass este símbolo del sistema para escenarios de automatización, ejecute `azure login` con hello `-q` parámetro.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>Escenario 3: Inicio de sesión de Azure con una entidad de servicio
Si crea una entidad de servicio para una aplicación de Active Directory y entidad de servicio de hello tiene permisos en su suscripción, puede usar hello `azure login` entidad de servicio de comando tooauthenticate Hola. Según el escenario, podría proporcionar credenciales de Hola de entidad de servicio de hello como parámetros explícitos de hello `azure login` comando. Por ejemplo, hello siguiente comando pasa nombre principal de servicio de Hola y el Id. de inquilino de Active Directory:

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

Son, a continuación, tooprovide solicitada Hola contraseña. También puede proporcionar las credenciales de Hola a través de un código de aplicación o secuencia de comandos CLI, o usar a una entidad de servicio de certificado tooauthenticate Hola de manera no interactiva para escenarios de automatización. Para ver información más detallada y ejemplos, consulte [Autenticación de una entidad de servicio con Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).

## <a name="scenario-4-use-a-publish-settings-file"></a>Escenario 4: Uso de un archivo de configuración de publicación
Si solo necesita comandos de CLI (por ejemplo, toodeploy máquinas virtuales de Azure en el modelo de implementación clásica de Hola) para el modo de administración de servicios de Azure de Hola toouse, puede conectarse mediante un archivo de configuración de publicación. Este método instala un certificado en el equipo local que le permite tooperform tareas de administración de como certificado de Hola y la suscripción de hello son válidos.

* **archivo de configuración de publicación de hello toodownload** para su cuenta, asegúrese de que Hola CLI está en modo de administración de servicios escribiendo `azure config mode asm`. A continuación, ejecute hello siguiente comando:

        azure account download

Esto abre el explorador predeterminado y se le pide que toosign en toohello [portal de Azure clásico](https://manage.windowsazure.com). Después de iniciar sesión, se descarga un archivo `.publishsettings` . Tome nota de dónde se guarda este archivo.

> [!NOTE]
> Si su cuenta está asociada a varios inquilinos de Azure Active Directory, es posible que tooselect solicitada que Active Directory que se va a toodownload una configuración de publicación de archivos para.
>
>

Una vez que se seleccionan mediante la página de descarga de Hola o visitando Hola portal de Azure clásico, hello seleccionados de Active Directory se convierte en hello predeterminado utilizado por el portal clásico de Hola y página de descarga. Una vez que se ha establecido el valor predeterminado, consulte texto hello '**haga clic aquí página de selección de tooreturn toohello**' al principio de Hola de página de descarga de Hola. Usar hello proporcionada la página de selección de vínculo tooreturn toohello.

* **archivo de configuración de publicación de hello tooimport**, ejecute hello comando siguiente:

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> Después de importar la configuración de publicación, primero debe eliminar hello `.publishsettings` archivo. Ya no es necesario por hello Azure CLI y presenta un riesgo de seguridad porque podría toogain usa acceso tooyour suscripción.
>
>

## <a name="cli-command-modes"></a>Modos de comando de CLI
Hola CLI de Azure proporciona dos modos de comando para trabajar con recursos de Azure, con distintos conjuntos de comandos:

* **Modo de administrador de recursos** : para trabajar con recursos de Azure en el modelo de implementación del Administrador de recursos de Hola. tooset este modo, ejecute `azure config mode arm`.
* **Modo de administración de servicios** : para trabajar con recursos de Azure en el modelo de implementación clásica de Hola. tooset este modo, ejecute `azure config mode asm`.

Cuando instala por primera vez, Hola versión actual de hello que CLI está en modo de administrador de recursos.

> [!NOTE]
> modo de administrador de recursos de Hola y el modo de administración de servicios son mutuamente excluyentes. Es decir, no se pueden administrar recursos creados en un modo de hello otro modo.
>
>

## <a name="multiple-subscriptions"></a>Varias suscripciones
Si tiene varias suscripciones de Azure, conectar tooAzure concede acceso suscripciones tooall asociadas con sus credenciales. Una suscripción es seleccionada como valor predeterminado de Hola y Hola CLI de Azure utiliza al realizar operaciones. Puede ver las suscripciones de hello, como la suscripción predeterminada actual de hello, mediante hello, `azure account list` comando. Este comando devuelve la siguiente toohello similar de información:

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

Hola precede a lista, Hola **actual** columna indica la suscripción predeterminada actual de hello como Azure-sub-1. toochange Hola suscripción predeterminada y se use hello `azure account set` comando y especifique que desea predeterminado de hello toobe de suscripción de Hola. Por ejemplo:

    azure account set Azure-sub-2

Esto cambia Hola predeterminado suscripción tooAzure-sub-2.

> [!NOTE]
> Cambiar la suscripción predeterminada de hello surte efecto inmediatamente y es un cambio global; nuevos comandos de CLI de Azure, si los ejecuta desde Hola misma instancia de línea de comandos o una instancia diferente, utilice suscripción predeterminada de la nueva Hola.
>
>

Si desea toouse una suscripción no predeterminadas con hello CLI de Azure, pero no desea toochange Hola actual de forma predeterminada, puede usar hello `--subscription` opción de comando de Hola y proporcione el nombre de Hola de suscripción de hello desea toouse para la operación de Hola.

Una vez que esté conectado tooyour suscripción de Azure, puede empezar a usar toowork de comandos de CLI de Azure de hello con recursos de Azure.

## <a name="storage-of-cli-settings"></a>Almacenamiento de la configuración de la CLI
Si inicia una sesión con hello `azure login` comando o importar la configuración de publicación, el perfil CLI y los registros se almacenan en un `.azure` directorio ubicado en el `user` directory. El directorio `user` está protegido por el sistema operativo. Sin embargo, recomendamos que realice pasos adicionales tooencrypt su `user` directory. Puede hacerlo en hello siguientes maneras:

* En Windows, modificar las propiedades de directorio de Hola o usar BitLocker.
* En el equipo Mac, activar FileVault para directorio Hola.
* En Ubuntu, utilizar la característica de directorio de inicio de cifrado de Hola. Otras distribuciones de Linux ofrecen características similares.

## <a name="logging-out"></a>Cerrar sesión
toolog out, Hola de uso siguiente comando:

    azure logout -u <username>

Si las suscripciones de hello asociadas con solo se autenticar la cuenta de hello con Active Directory, cerrar la sesión elimina información de suscripción de Hola de perfil local Hola. Sin embargo, si también se importa un archivo de configuración de publicación para las suscripciones de hello, cerrar la sesión solo elimina Active Directory relacionados con la información del perfil local Hola.

## <a name="next-steps"></a>Pasos siguientes
* toouse comandos de CLI de Azure, consulte [comandos de CLI de Azure en el modo de administrador de recursos](virtual-machines/azure-cli-arm-commands.md) y [comandos de CLI de Azure en el modo de administración de servicios](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* toolearn más información acerca de hello CLI de Azure, descargar código fuente, informar de problemas, o contribuir proyecto toohello, visite hello [repositorio de GitHub para hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Si se producen problemas al usar Hola CLI de Azure o Azure, visite hello [foros de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).
