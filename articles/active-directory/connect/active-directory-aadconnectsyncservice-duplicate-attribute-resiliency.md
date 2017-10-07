---
title: "resistencia de atributo de sincronización y duplicado aaaIdentity | Documentos de Microsoft"
description: "Nuevo comportamiento de cómo toohandle los objetos con el UPN o ProxyAddress conflictos durante la sincronización de directorios con Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>Sincronización de identidades y resistencia de atributos duplicados
La resistencia de atributos duplicados es una característica de Azure Active Directory que eliminará la fricción causada por los conflictos entre **UserPrincipalName** y **ProxyAddress** al ejecutar una de las herramientas de sincronización de Microsoft.

Estos dos atributos son suelen necesitar toobe único en todas las **usuario**, **grupo**, o **póngase en contacto con** objetos en un inquilino de Azure Active Directory determinado.

> [!NOTE]
> Solo los usuarios pueden tener UPN.
> 
> 

Hola nuevo comportamiento que permite esta característica es en parte de la nube de Hola de canalización de sincronización de hello, por lo tanto es cliente independiente y relevante para cualquier producto de sincronización de Microsoft incluidos Azure AD Connect, DirSync y MIM + conector. término genérico Hola "cliente de sincronización" se usa en este toorepresent documento cualquiera de estos productos.

## <a name="current-behavior"></a>Comportamiento actual
Si se produce un intento de tooprovision un nuevo objeto con un valor UPN o ProxyAddress que infringe esta restricción de unicidad, Azure Active Directory bloquea ese objeto desde el que se creó. De forma similar, si un objeto se actualiza con un UPN o ProxyAddress no es único, hello no se puede actualizar. Hola aprovisionamiento intento o update se vuelve a intentar por el cliente de sincronización de hello en cada ciclo de exportación y continúa toofail hasta que se resuelva el conflicto de Hola. Un correo electrónico de informes de error se genera tras cada intento y se registra un error por el cliente de sincronización de Hola.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>Comportamiento con resistencia de atributos duplicados
En lugar de completamente superan tooprovision o actualizar un objeto con un atributo duplicado, Azure Active Directory "pone en cuarentena" atributo duplicado de Hola que infringiría la restricción de unicidad de Hola. Si este atributo es necesario para el aprovisionamiento, como UserPrincipalName, servicio de hello asigna un valor de marcador de posición. formato de Hola de estos valores temporales es  
"***<OriginalPrefix>+<Número4Dígitos>@<InitialTenantDomain>.onmicrosoft.com***".  
Si no se requiere el atributo de hello, como un **ProxyAddress**, Azure Active Directory simplemente pone en cuarentena el atributo de conflicto de Hola y continúa con la creación de objetos de Hola o actualización.

Al poner en cuarentena atributo hello, se envía información sobre conflictos de Hola Hola usa el mismo correo electrónico de informe de error en comportamiento anterior de Hola. Sin embargo, esta información sólo aparece en el informe de errores de hello una vez, cuando se produce la cuarentena de hello, que no continúe toobe en el futuro registra mensajes de correo electrónico. Además, puesto que se ha realizado correctamente la exportación de Hola para este objeto, cliente de sincronización de hello no registra un error y Hola de reintento no crear / actualizar operación en ciclos de sincronización posterior.

toosupport que este comportamiento un nuevo atributo ha sido agregado clases de objetos User, Group y Contact toohello:  
**DirSyncProvisioningErrors**

Se trata de un atributo multivalor que usa toostore Hola atributos en conflicto que infringen restricción de unicidad de Hola se deben agregar normalmente es. Se ha habilitado una tarea en segundo plano temporizador en Azure Active Directory que se ejecuta cada toolook horas si hay conflictos de atributo duplicados que se han resuelto y quita automáticamente los atributos de hello en cuestión de cuarentena.

### <a name="enabling-duplicate-attribute-resiliency"></a>Habilitación de resistencia de atributos duplicados
Resistencia de atributo duplicada será el comportamiento predeterminado de la nueva Hola entre todos los inquilinos de Azure Active Directory. Será de forma predeterminada para todos los inquilinos que habilita la sincronización de Hola la primera vez en el 22 de agosto de 2016 o posterior. Los inquilinos que habilita la sincronización anterior toothis fecha tendrá habilitada en lotes de la característica de Hola. Esta implementación se iniciará en septiembre de 2016, y se enviará una notificación por correo electrónico notificación técnica póngase en contacto con del inquilino tooeach con fecha concreta hello cuando se habilitará la característica de Hola.

> [!NOTE]
> Una vez que se ha activado la resistencia de atributo duplicados no se puede deshabilitar.

toocheck si está habilitada la característica de hello para el inquilino, puede hacerlo por descargar la versión más reciente de Hola de módulo de PowerShell de Azure Active Directory de Hola y ejecutar:

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> No podrá usar la característica de resistencia de atributo duplicada de Set-MsolDirSyncFeature cmdlet tooproactively habilitar Hola antes de que está activado para el inquilino. característica de toobe tootest capaz de hello, deberá toocreate un nuevo inquilino de Azure Active Directory.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>Identificación de objetos con el atributo DirSyncProvisioningErrors
Hay actualmente dos métodos tooidentify objetos que tienen estos errores debidos hello Portal de administración de Office 365, Azure Active Directory PowerShell y tooduplicate propiedad entra en conflicto. No hay planes tooextend tooadditional portal basado reporting Hola futuras.

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
Para hello cmdlets de PowerShell en este tema, Hola aquí te mostramos true:

* Todos Hola después cmdlets distinguen mayúsculas de minúsculas.
* Hola **: ErrorCategory PropertyConflict** siempre se deben incluir. Actualmente no hay ningún otro tipo de **ErrorCategory**, pero esto puede ampliarse en hello futuras.

En primer lugar, comience con la ejecución de **Connect-MsolService** y escriba las credenciales de un administrador de inquilinos.

A continuación, usar hello siguientes errores de tooview de cmdlets y los operadores de maneras diferentes:

1. [Ver todos](#see-all)
2. [Por tipo de propiedad](#by-property-type)
3. [Por valor en conflicto](#by-conflicting-value)
4. [Mediante una búsqueda de cadena](#using-a-string-search)
5. [Ordenados](#sorted)
6. [En una cantidad limitada o todos](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>Ver todos
Una vez conectado, toosee una lista de los errores en el inquilino de Hola de aprovisionamiento de atributo ejecute:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

Esto genera un resultado similar Hola siguiente:  
 ![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "MsolDirSyncProvisioningError Get")  

#### <a name="by-property-type"></a>Por tipo de propiedad
errores de toosee por tipo de propiedad, agregar hello **- PropertyName** marca con hello **UserPrincipalName** o **ProxyAddresses** argumento:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

O

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>Por valor en conflicto
errores de toosee relacionados con la propiedad específica de tooa agregar hello **- PropertyValue** marca (**- PropertyName** debe usarse también al agregar esta marca):

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>Mediante una búsqueda de cadena
toodo una búsqueda de cadena amplia usar hello **- SearchString** marca. Esto se pueden utilizar independientemente de todos Hola por encima de marcas, con excepción de Hola de **- ErrorCategory PropertyConflict**, que siempre es necesario:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>En una cantidad limitada o todos
1. **MaxResults <Int>**  se puede usar toolimit Hola consulta tooa específico un número de valores.
2. **Todos los** pueden ser utilizado tooensure se recuperan todos los resultados en caso de Hola que existe un gran número de errores.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Portal de administración de Office 365
Puede ver los errores de sincronización de directorios en el centro de administración de Office 365 Hola. Hola informes en el portal solo muestra de Hola Office 365 **usuario** objetos que tienen estos errores. No se muestran datos acerca de los conflictos entre los objetos **Groups**, **Contacts**.

![Usuarios activos](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Usuarios activos")

Para obtener instrucciones sobre cómo center tooview los errores de sincronización de directorios en Office 365 Hola, administrador, consulte [identificar los errores de sincronización de directorios en Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).

### <a name="identity-synchronization-error-report"></a>Informe de errores de sincronización de identidades
Cuando se controla un objeto con un conflicto de atributo duplicado con este nuevo comportamiento que una notificación se incluye en el estándar de hello informe de errores de sincronización de identidades de correo electrónico que se envía toohello notificación técnica póngase en contacto con el inquilino de Hola. Sin embargo, hay un cambio importante en este comportamiento. Hola anteriores, información sobre un conflicto de atributo duplicado se incluiría en cada informe de errores posteriores hasta que se ha resuelto el conflicto de Hola. Con este nuevo comportamiento, notificación de errores de hello si hay un conflicto determinado solo aparecen una vez - en tiempo de hello atributo en conflicto Hola se pone en cuarentena.

Este es un ejemplo de la notificación de correo electrónico de hello aspecto si hay un conflicto de ProxyAddress:  
    ![Usuarios activos](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Usuarios activos")  

## <a name="resolving-conflicts"></a>Resolución de conflictos
Solución de problemas de tácticas de estrategia y la resolución de estos errores no debe diferenciarse de manera Hola Hola anterior se administran los errores de atributo duplicado. Hola única diferencia es que Hola temporizador tarea sucias a través del inquilino de hello en hello lado del servicio tooautomatically Agregar atributo Hola en objeto apropiado de pregunta toohello una vez que se resuelve el conflicto de Hola.

Hello artículo siguiente describe diversas estrategias de solución de problemas y resolución: [duplicado o atributos no válidos impiden la sincronización de directorios en Office 365](https://support.microsoft.com/kb/2647098).

## <a name="known-issues"></a>Problemas conocidos
Ninguno de estos problemas conocidos provoca la degradación del servicio o la pérdida de datos. Varios de ellos son estéticos, otras producen estándar "*resistencia previa*" atributo duplicado errores toobe genera en lugar de poner en cuarentena el atributo de conflicto de hello y otro hace cierto errores toorequire manual adicional revisión de seguridad.

**Comportamiento básico:**

1. Los objetos con configuraciones de atributo concreto siguen tooreceive errores de exportación como lugar toohello duplicados atributos ponen en cuarentena.  
   Por ejemplo:
   
    a. Se crea un nuevo usuario en AD con un UPN de **Joe@contoso.com** y ProxyAddress **smtp:Joe@contoso.com**
   
    b. Hello propiedades de este objeto entran en conflicto con un grupo existente, donde es ProxyAddress  **SMTP:Joe@contoso.com** .
   
    c. Durante la exportación, un **ProxyAddress conflicto** error se produce en lugar de tener atributos de conflicto de hello en cuarentena. Hola se reintenta en cada ciclo de sincronización subsiguientes, tal y como lo habría sido antes de habilita la característica de resistencia de Hola.
2. Si se crean dos grupos locales con hello misma dirección SMTP, tooprovision un se produce un error en primer intento de hello con un estándar duplicado **ProxyAddress** error. Sin embargo, valor duplicado hello es correctamente en cuarentena en hello siguiente ciclo de sincronización.

**Informe del Portal de Office**:

1. mensaje de error detallado de Hola para dos objetos en un conjunto de conflicto UPN es Hola igual. Esto indica que se ha modificado o puesto en cuarentena el UPN de ambos cuando, en realidad, solo se modificaron los datos de uno de ellos.
2. mensaje de error detallado de Hello si hay un conflicto UPN muestra hello displayName incorrecto para un usuario que ha tenido sus UPN cambiado/en cuarentena. Por ejemplo:
   
    a. El **usuario A** se sincroniza primero con **UPN = User@contoso.com**.
   
    b. **El usuario B** se ha intentado toobe sincronizado próxima con **UPN = User@contoso.com** .
   
    c. **Usuario B** UPN se cambia demasiado **User1234@contoso.onmicrosoft.com**  y  **User@contoso.com**  se agrega demasiado**DirSyncProvisioningErrors**.
   
    d. mensaje de error de Hola para **usuario B** debe indicar **usuario A** ya tiene  **User@contoso.com**  como se muestra en un UPN, pero **usuario B** propio displayName.

**Informe de errores de sincronización de identidades**:

vínculo de Hola para *pasos sobre cómo tooresolve este problema* es incorrecto:  
    ![Usuarios activos](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Usuarios activos")  

Debe señalar demasiado[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).

## <a name="see-also"></a>Otras referencias
* [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
* [Identificar problemas de sincronización de directorios en Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

