---
title: "Guía de solución de problemas de Azure Active Directory Domain Services | Microsoft Docs"
description: "Guía de solución de problemas Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Guía de solución de problemas de Azure AD Domain Services
En este artículo se ofrecen sugerencias de solución de problemas para los problemas que puede encontrar al configurar o administrar Servicios de dominio de Azure Active Directory (AD).

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>No puede habilitar Azure AD Domain Services para su directorio de Azure AD
Esta sección le ayuda a solucionar errores cuando intente tooenable servicios de dominio de AD de Azure para su directorio y se produce un error u obtiene activar o desactivar too'Disabled atrás '.

Elija Hola pasos correspondientes toohello mensaje de error que se produce para solucionar problemas.

| **Mensaje de error** | **Resolución** |
| --- |:--- |
| *Hola nombre contoso100.com ya está en uso en esta red. Especifique un nombre que no esté en uso.* |[Conflicto de nombres de dominio en la red virtual de Hola](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *No se pudieron habilitar los servicios de dominio en este inquilino de Azure AD. servicio de Hello no tiene los permisos adecuados aplicación de toohello denominado 'Sync de servicios de dominio de Active Directory de Azure'. Eliminar aplicación Hola denominado 'Sync de servicios de dominio de Active Directory de Azure' y vuelva a intentar tooenable los servicios de dominio de su inquilino de Azure AD.* |[Los servicios de dominio no tiene la aplicación de sincronización de los servicios de dominio de Azure AD toohello de los permisos adecuados](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *No se pudieron habilitar los servicios de dominio en este inquilino de Azure AD. Hola servicios de dominio de no haber Hola aplicación en su inquilino de Azure AD requiere permisos tooenable los servicios de dominio. Eliminar aplicación Hola con d87dcbc6-a371-462e-88e3-28ad15ec4e64 de identificador de aplicación hello y vuelva a intentar tooenable servicios de dominio para el inquilino de Azure AD.* |[Hola aplicación de servicios de dominio no está configurado correctamente en el inquilino](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *No se pudieron habilitar los servicios de dominio en este inquilino de Azure AD. Hola aplicación de Microsoft Azure AD está deshabilitado en el inquilino de Azure AD. Habilitar la aplicación hello con 00000002-0000-0000-c000-000000000000 de identificador de aplicación hello y vuelva a intentar tooenable servicios de dominio para el inquilino de Azure AD.* |[Hola aplicación de Microsoft Graph está deshabilitada en el inquilino de Azure AD](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>Conflicto de nombres de dominio
**Mensaje de error:**

*Hola nombre contoso100.com ya está en uso en esta red. Especifique un nombre que no esté en uso.*

**Corrección:**

Asegúrese de que no tiene un dominio existente con hello mismo nombre de dominio disponible en la red virtual. Por ejemplo, suponga que tiene un dominio denominado "contoso.com" ya está disponible en la red virtual seleccionada de Hola. Más adelante, intente tooenable un dominio administrado de los servicios de dominio de AD de Azure con hello mismo nombre de dominio (es decir, "contoso.com") en la red virtual. Detecta un error al tratar de servicios de dominio de tooenable Azure AD.

Este error es debido a conflictos de tooname por nombre de dominio de hello en la red virtual. En esta situación, debe usar un nombre diferente tooset su dominio administrado de los servicios de dominio de AD de Azure. Como alternativa, puede Desaprovisionamiento de dominio existente de hello y, a continuación, continuar tooenable Azure AD los servicios de dominio.

### <a name="inadequate-permissions"></a>Permisos insuficientes
**Mensaje de error:**

*No se pudieron habilitar los servicios de dominio en este inquilino de Azure AD. servicio de Hello no tiene los permisos adecuados aplicación de toohello denominado 'Sync de servicios de dominio de Active Directory de Azure'. Eliminar aplicación Hola denominado 'Sync de servicios de dominio de Active Directory de Azure' y vuelva a intentar tooenable los servicios de dominio de su inquilino de Azure AD.*

**Corrección:**

Compruebe toosee si hay una aplicación con el nombre de hello 'Sync de servicios de dominio de Active Directory de Azure' en el directorio de Azure AD. Si existe, elimínela y vuelva a habilitar Azure AD Domain Services.

Realizar Hola siguientes pasos toocheck presencia de Hola de aplicación hello y toodelete, si existe la aplicación hello:

1. Navegue toohello **portal de Azure clásico** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. Seleccione hello **Active Directory** nodo en el panel izquierdo de Hola.
3. Inquilino seleccione hello Azure AD (directorio) para que le gustaría tooenable de servicios de dominio de AD de Azure.
4. Navegue toohello **aplicaciones** ficha.
5. Seleccione hello **aplicaciones tiene mi compañía** opción en la lista desplegable de Hola.
6. Busque una aplicación llamada **Sincronización de Azure AD Domain Services**. Si existe en la aplicación hello, continúe toodelete lo.
7. Una vez haya eliminado la aplicación hello, vuelva a servicios de dominio de Azure AD tooenable una vez.

### <a name="invalid-configuration"></a>Configuración no válida
**Mensaje de error:**

*No se pudieron habilitar los servicios de dominio en este inquilino de Azure AD. Hola servicios de dominio de no haber Hola aplicación en su inquilino de Azure AD requiere permisos tooenable los servicios de dominio. Eliminar aplicación Hola con d87dcbc6-a371-462e-88e3-28ad15ec4e64 de identificador de aplicación hello y vuelva a intentar tooenable servicios de dominio para el inquilino de Azure AD.*

**Corrección:**

Compruebe toosee si tiene una aplicación con el nombre de hello 'AzureActiveDirectoryDomainControllerServices' (con un identificador de aplicación de d87dcbc6-a371-462e-88e3-28ad15ec4e64) en el directorio de Azure AD. Si no existe esta aplicación, necesita toodelete y, a continuación, volver a habilitar servicios de dominio de Azure AD.

Usar hello tras la aplicación de Hola de toofind de secuencia de comandos de PowerShell y elimínelo.

> [!NOTE]
> Este script usa cmdlets de **Azure AD PowerShell versión 2**. Para obtener una lista completa de todos los cmdlets disponibles y módulo de hello toodownload, leer hello [documentación de referencia AzureAD PowerShell](https://msdn.microsoft.com/library/azure/mt757189.aspx).
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Microsoft Graph deshabilitado
**Mensaje de error:**

No se pudo habilitar Domain Services en este inquilino de Azure AD. Hola aplicación de Microsoft Azure AD está deshabilitado en el inquilino de Azure AD. Habilitar la aplicación hello con 00000002-0000-0000-c000-000000000000 de identificador de aplicación hello y vuelva a intentar tooenable servicios de dominio para el inquilino de Azure AD.

**Corrección:**

Compruebe toosee si ha desactivado una aplicación con el identificador hello 00000002-0000-0000-c000-000000000000. Esta aplicación es la aplicación de Microsoft Azure AD de hello y proporciona a API Graph acceso tooyour Azure AD inquilinos. Servicios de dominio de Azure AD necesita este toosynchronize toobe habilitado de aplicación administrado de su tooyour de inquilino de Azure AD dominio.

tooresolve este error, habilitar esta aplicación y, a continuación, intentar tooenable los servicios de dominio de su inquilino de Azure AD.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>Los usuarios son no se puede toosign en toohello dominio administrado de los servicios de dominio de AD de Azure
Si uno o más usuarios en su inquilino de Azure AD se no se puede toosign en el dominio administrado toohello recién creado, siga Hola siguiendo los pasos de solución de problemas:

* **Inicie sesión con el formato UPN:** intente toosign en formato UPN de hello (por ejemplo, 'joeuser@contoso.com') en lugar de formato de SAMAccountName hello ('CONTOSO\joeuser'). Hola SAMAccountName puede generarse automáticamente para los usuarios cuyo prefijo UPN es demasiado largo u Hola igual como otro usuario en el dominio administrado Hola. formato de UPN de Hola se garantiza toobe único dentro de un inquilino de Azure AD.

> [!NOTE]
> Se recomienda utilizar toosign de formato UPN de hello en el dominio administrado de toohello servicios de dominio de AD de Azure.
>
>

* Asegúrese de que tiene [habilitada la sincronización de contraseña](active-directory-ds-getting-started-password-sync.md) con arreglo a los pasos de Hola que se describen en la Guía de introducción de Hola.
* **Las cuentas externas:** Asegúrese de que la cuenta de usuario de hello afectado no es una cuenta externa en el inquilino de hello Azure AD. Entre los ejemplos de las cuentas externas se incluyen las cuentas de Microsoft; por ejemplo, "joe@live.com" o las cuentas de usuario de un directorio de Azure AD externo. Puesto que los servicios de dominio de AD de Azure no tiene credenciales para estas cuentas de usuario, estos usuarios no pueden iniciar sesión en el dominio administrado toohello.
* **Las cuentas se sincronizó:** si las cuentas de usuario de hello afectado se sincronizan desde un directorio local, compruebe que:

  * Ha implementado o actualizado toohello [más reciente recomienda versión de Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
  * Se configuró Azure AD Connect demasiado[realizar una sincronización completa](active-directory-ds-getting-started-password-sync.md).
  * Según el tamaño de hello del directorio, puede tardar un poco para cuentas de usuario y credenciales hashes toobe disponibles en los servicios de dominio de Active Directory de Azure. Asegúrese de que esperar durante el tiempo suficiente antes de volver a intentar la autenticación (según el tamaño de Hola de su directorio - unas pocas horas al día tooa o dos directorios grandes).
  * Si Hola continúa después de comprobar Hola pasos anteriores, pruebe a reiniciar Hola servicio de sincronización de Microsoft Azure AD. Desde el equipo de sincronización, inicie un símbolo del sistema y ejecute hello siguientes comandos:

    1. net stop 'Microsoft Azure AD Sync'
    2. net start 'Microsoft Azure AD Sync'
* **Solo en la nube cuentas**: si la cuenta de usuario de hello afectado es una cuenta de usuario solo en la nube, asegúrese de que ese usuario Hola ha cambiado su contraseña después de habilitar los servicios de dominio de AD de Azure. Este paso hace credencial Hola códigos hash requeridos para toobe de servicios de dominio de Azure AD genera.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Los usuarios quitados del inquilino de Azure AD no se quitan de su dominio administrado
Azure AD protege contra la eliminación accidental de objetos de usuario. Cuando se elimina una cuenta de usuario de inquilino de Azure AD, el objeto de usuario correspondiente de hello es toohello ha movido la Papelera de reciclaje. Cuando esta operación de eliminación es dominio administrado tooyour sincronizados, hace que Hola correspondiente toobe de cuenta de usuario marcado deshabilitado. Esta característica le permite recuperar o restaurar la cuenta de usuario de hello más tarde.

Hola permanece en Hola deshabilitada estado en el dominio administrado de la cuenta de usuario, incluso si vuelve a crear una cuenta de usuario con Hola mismo UPN en su directorio Azure AD. cuenta de usuario de hello tooremove desde el dominio administrado, deberá tooforce eliminarlo del inquilino de Azure AD.

cuenta de usuario de hello tooremove completamente de su dominio administrado, eliminar usuario Hola de forma permanente del inquilino de Azure AD. Use el cmdlet de PowerShell de Remove-MsolUser de hello con hello '-RemoveFromRecycleBin' opción, tal como se describe en este [artículo de MSDN](https://msdn.microsoft.com/library/azure/dn194132.aspx).

## <a name="contact-us"></a>Ponerse en contacto con nosotros
Póngase en contacto con el equipo de producto de servicios de dominio de Active Directory de Azure de hello demasiado[compartir comentarios o para la compatibilidad con](active-directory-ds-contact-us.md).
