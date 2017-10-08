---
title: "grupos de aaaPopulate dinámicamente en función de atributos de objeto en Azure Active Directory | Documentos de Microsoft"
description: "Cómo: a toocreate avanzada de reglas para admite la inclusión de pertenencia al grupo Operadores de regla de expresión y los parámetros."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 04813a42-d40a-48d6-ae96-15b7e5025884
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: fe22829118ed8f5137a619d93fa6f9bf80835863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="populate-groups-dynamically-based-on-object-attributes"></a>Rellenado dinámico de grupos en función de los atributos de objeto
Hola portal de Azure clásico proporciona Hola capacidad tooenable más compleja basada en atributos pertenencia dinámica a grupos de Azure Active Directory (Azure AD).  

Cuando los atributos de un cambio de usuario o dispositivo, sistema de hello evalúa todas las reglas de grupo dinámico en un directorio toosee si cambio de hello activaría cualquier grupo agrega o quita. Si un usuario o dispositivo cumple una regla de un grupo, se agrega a este como miembro. Si ya no cumplen la regla de hello, se quitan.

> [!NOTE]
> - Puede configurar una regla de pertenencia dinámica a grupos de seguridad o en grupos de Office 365.
>
> - Esta característica requiere una licencia de Azure AD Premium P1 para cada grupo dinámico de usuario miembro agregado tooat menos uno.
>
> - Puede crear un grupo dinámico para dispositivos o usuarios, pero no se puede crear una regla que contenga tanto objetos de usuario como de dispositivo.

> - En el momento de hello no es posible toocreate un grupo de dispositivos basado en atributos de usuario de propietario. Reglas de pertenencia de dispositivo pueden solo inmediata atributos de referencia de objetos de dispositivo en el directorio de Hola.

## <a name="toocreate-an-advanced-rule"></a>toocreate una regla avanzada
1. Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory**y, a continuación, abra el directorio de su organización.
2. Seleccione hello **grupos** ficha y un grupo de hello, a continuación, abra desea tooedit.
3. Seleccione hello **configurar** ficha, seleccione hello **regla avanzada** opción y, a continuación, escriba Hola avanzada regla en el cuadro de texto de Hola.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Construir el cuerpo de Hola de una regla avanzada
Hola regla avanzada que se puede crear para hello pertenencia dinámica a grupos es esencialmente una expresión binaria que consta de tres partes y los resultados en un resultado true o false. Hola tres partes son:

* Parámetro a la izquierda
* Operador binario
* Constante a la derecha

Una regla avanzada completa busca toothis similar: (Parámetroizquierdo Operadorbinario "Constantederecha"), cuando es necesario para la expresión binaria completa de Hola Hola abriendo y un paréntesis de cierre, comillas dobles son necesarias para la constante derecha hello y sintaxis de Hola para hello parámetro izquierdo es usuario.propiedad. Una regla avanzada puede constar de varias expresiones binarias separadas por hello- y-, o bien y - operadores lógicos no.
siguiente Hola es ejemplos de una regla avanzada construida correctamente:

* (user.department -eq "Sales") -or (user.department -eq "Marketing")
* (user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")

Para hello lista completa de parámetros admitidos y operadores de regla de expresión, vea las siguientes secciones.


Tenga en cuenta que propiedad Hola debe ir precedido por tipo de objeto correcto de hello: usuario o dispositivo.
Hola por debajo de la regla se producirá un error de validación de hello: correo ne: null

regla de Hello correcta sería:

user.mail –ne null

longitud total de Hello del cuerpo de saludo de la regla avanzada no puede superar los 2048 caracteres.

> [!NOTE]
> Las operaciones de cadena y regex no distinguen mayúsculas de minúsculas.
> Las cadenas que contienen comillas " deben convertirse en escape con caracteres '; por ejemplo, user.department -eq \`"Sales".
> Utilice comillas solamente para los valores de tipo cadena y solo use comillas inglesas.
>
>

## <a name="supported-expression-rule-operators"></a>Operadores de regla de expresión admitidos
Hello tabla siguiente enumeran todos los operadores de regla de expresión de hello compatibles y su toobe de sintaxis que utilizar en el cuerpo de Hola de hello avanzada regla:

| operador | Sintaxis |
| --- | --- |
| Not Equals |-ne |
| Equals |-eq |
| Not Starts With |-notStartsWith |
| Starts With |-startsWith |
| Not Contains |-notContains |
| Contains |-contains |
| Not Match |-notMatch |
| Match |-match |
| En el | -in |
| No en el | -notIn |

## <a name="operator-precedence"></a>Precedencia de operadores

Todos los operadores se enumeran a continuación por prioridad, de menor toohigher, operador en la misma línea se encuentran en la misma precedencia-cualquier - all - o - y - no - eq - ne - startsWith - notStartsWith-contiene - notContains-coincide con: notMatch-en - notIn

Todos los operadores se pueden utilizar con o sin prefijo de guión.

Tenga en cuenta que paréntesis no son necesarias siempre, sólo necesita tooadd paréntesis cuando prioridad no cumplen los requisitos como por ejemplo:

   user.department –eq "Marketing" –and user.country –eq "US"

equivale a:

   (user.department –eq "Marketing") –and (user.country –eq "US")

## <a name="using-hello--in-and--notin-operators"></a>Uso de Hola - en - notIn operadores y

Si desea toocompare Hola valor de un atributo de usuario con un número de valores diferentes que puede usar hello - en - notIn operadores o. Este es un ejemplo utilizando Hola - In (operador):

    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]

Tenga en cuenta use Hola de hello "[" y "]" principio de Hola y el final de la lista de Hola de valores. Esta condición se evalúa como tooTrue del valor de Hola de user.department es igual a uno de los valores de hello en lista de Hola.

## <a name="query-error-remediation"></a>Corrección de errores de consulta
Hello tabla siguiente muestran posibles errores y cómo toocorrect ellos si se producen

| Error de análisis de consulta | Uso con error | Uso corregido |
| --- | --- | --- |
| Error: no se admite el atributo. |(user.invalidProperty -eq "Value") |(user.department -eq "value")<br/>Propiedad debe coincidir con uno de hello [admite la lista de propiedades](#supported-properties). |
| Error: no se admite el operador en el atributo. |(user.accountEnabled -contains true) |(user.accountEnabled -eq true)<br/>La propiedad es de tipo booleano. Usar operadores de hello admitida (-eq o - ne) en un tipo booleano de Hola por encima de la lista. |
| Error: error de compilación de consulta. |(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext") |(user.department -eq "Sales") -and (user.department -eq "Marketing")<br/>Operador lógico debe coincidir con uno de hello admitido propiedades aparecen más arriba. (user.userPrincipalName-coincide con ". *@domain.ext") o (user.userPrincipalName-coincide con "@domain.ext$") Error en la expresión regular. |
| Error: la expresión binaria no está en un formato adecuado. |(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>La consulta tiene varios errores. El paréntesis no está en el lugar correcto. |
| Error: se ha producido un error desconocido durante la configuración de pertenencias dinámicas. |(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>La consulta tiene varios errores. El paréntesis no está en el lugar correcto. |

## <a name="supported-properties"></a>Propiedades admitidas
siguiente Hola es todas las propiedades de usuario de Hola que puede usar la regla avanzada:

### <a name="properties-of-type-boolean"></a>Propiedades de tipo booleano
Operadores permitidos

* -eq
* -ne

| Propiedades | Valores permitidos | Uso |
| --- | --- | --- |
| accountEnabled |true false |user.accountEnabled -eq true |
| dirSyncEnabled |true false |user.dirSyncEnabled -eq true |

### <a name="properties-of-type-string"></a>Propiedades de tipo cadena
Operadores permitidos

* -eq
* -ne
* -notStartsWith
* -startsWith
* -contains
* -notContains
* -match
* -notMatch
* -in
* -notIn

| Propiedades | Valores permitidos | Uso |
| --- | --- | --- |
| city |Cualquier valor de cadena o $null |(user.city -eq "value") |
| country |Cualquier valor de cadena o $null |(user.country -eq "value") |
| companyName | Cualquier valor de cadena o $null | (user.companyName -eq "value") |
| department |Cualquier valor de cadena o $null |(user.department -eq "value") |
| DisplayName |Cualquier valor de cadena |(user.displayName -eq "value") |
| facsimileTelephoneNumber |Cualquier valor de cadena o $null |(user.facsimileTelephoneNumber -eq "value") |
| givenName |Cualquier valor de cadena o $null |(user.givenName -eq "value") |
| jobTitle |Cualquier valor de cadena o $null |(user.jobTitle -eq "value") |
| mail |Cualquier valor de cadena o $null (dirección SMTP del usuario de hello) |(user.mail -eq "value") |
| mailNickName |Cualquier valor de cadena (alias de correo electrónico del usuario de hello) |(user.mailNickName -eq "value") |
| mobile |Cualquier valor de cadena o $null |(user.mobile -eq "value") |
| objectId |GUID del objeto de usuario de Hola |(user.objectId -eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier | Identificador de seguridad local (SID) para los usuarios que se han sincronizado desde local toohello en la nube. |(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies -eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |Cualquier valor de cadena o $null |(user.physicalDeliveryOfficeName -eq "value") |
| postalCode |Cualquier valor de cadena o $null |(user.postalCode -eq "value") |
| preferredLanguage |Código ISO 639-1 |(user.preferredLanguage -eq "en-US") |
| sipProxyAddress |Cualquier valor de cadena o $null |(user.sipProxyAddress -eq "value") |
| state |Cualquier valor de cadena o $null |(user.state -eq "value") |
| streetAddress |Cualquier valor de cadena o $null |(user.streetAddress -eq "value") |
| surname |Cualquier valor de cadena o $null |(user.surname -eq "value") |
| telephoneNumber |Cualquier valor de cadena o $null |(user.telephoneNumber -eq "value") |
| usageLocation |Código de país con dos letras |(user.usageLocation -eq "US") |
| userPrincipalName |Cualquier valor de cadena |(user.userPrincipalName -eq "alias@domain") |
| userType |miembro invitado $null |(user.userType -eq "Member") |

### <a name="properties-of-type-string-collection"></a>Propiedades de colección de cadenas de tipo
Operadores permitidos

* -contains
* -notContains

| Propiedades | Valores permitidos | Uso |
| --- | --- | --- |
| otherMails |Cualquier valor de cadena |(user.otherMails -contains "alias@domain") |
| proxyAddresses |SMTP: alias@domain smtp: alias@domain |(user.proxyAddresses -contains "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>Propiedades de varios valores
Operadores permitidos

* -cualquier (satisfecho cuando al menos un elemento de colección de hello cumple la condición de hello)
* -(cumplen todas cuando todos los elementos de la colección de hello coincide con la condición de hello)

| Propiedades | Valores | Uso |
| --- | --- | --- |
| assignedPlans |Cada objeto de colección de hello expone Hola propiedades de cadena siguientes: capabilityStatus, servicio, servicePlanId |user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled") |

Valores múltiples propiedades son colecciones de objetos de hello mismo tipo. Puede usar - any y - all tooapply operadores tooone de una condición o la totalidad del programa Hola a los elementos de colección de hello, respectivamente. Por ejemplo:

assignedPlans es una propiedad de varios valor que enumera todos los planes de servicio toohello usuario asignados. Hola por debajo de la expresión seleccionará los usuarios que tienen el plan del servicio de Exchange Online (Plan 2) Hola que también está en estado habilitado:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(identificador Guid de hello identifica el plan de servicio de Exchange Online (Plan 2) Hola.)

> [!NOTE]
> Esto es útil si desea tooidentify todos los usuarios para los que un Office 365 (u otro servicio en línea de Microsoft) se ha habilitado la capacidad para tootarget de ejemplo con un determinado conjunto de directivas.

Hello expresión siguiente seleccionará todos los usuarios con cualquier plan de servicio que está asociado con hello al servicio de Intune (identificado por el nombre de servicio "SCO"):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Uso de valores nulos

toospecify un valor nulo en una regla, puede usar "null" o $null. Ejemplo:

   user.mail –ne null equivale a user.mail –ne $null

## <a name="extension-attributes-and-custom-attributes"></a>Atributos de extensión y atributos personalizados
Se admiten los atributos de extensión y los atributos personalizados en las reglas de pertenencia dinámica.

Atributos de extensión se sincronizan desde el servidor local de la ventana de AD y toman Hola formato de "ExtensionAttributeX", donde X es igual a 1 y 15.
Un ejemplo de una regla que utiliza un atributo de extensión sería

(user.extensionAttribute15 -eq "Marketing")

Atributos personalizados se sincronizan desde AD del servidor de Windows local o desde conectado SaaS hello y aplicación Hola formato "user.extension_[GUID]\__ [Attribute]", donde [GUID] es el identificador único de hello en AAD para la aplicación hello que atributo de hello creado en AAD y [Attribute] es el nombre de hello del atributo de hello tal y como se creó.
Un ejemplo de una regla que utiliza un atributo personalizado es

user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  

Hello nombre de atributo personalizado puede encontrarse en el directorio de hello consultando un usuario del atributo con el Explorador de gráfico y buscar el nombre del atributo de Hola.

## <a name="direct-reports-rule"></a>Regla de "subordinados directos"
Puede crear un grupo con todos los subordinados directos de un administrador. Cuando cambian los informes directos del Administrador de Hola Hola futuras, Hola pertenencia a grupo se ajustarán automáticamente.

> [!NOTE]
> 1. Para toowork de regla de hello, que seguro Hola **Id. de administrador** propiedad está establecida correctamente en los usuarios de su inquilino. Puede comprobar el valor actual de Hola para un usuario en su **ficha perfil**.
> 2. Esta regla admite solo subordinados **directos**. Actualmente no es posible toocreate un grupo para una jerarquía anidada, por ejemplo, un grupo que incluya los subordinados directos y sus informes.

**grupo de hello tooconfigure**

1. Siga los pasos del 1 al 5 de la sección [toocreate Hola avanzada regla](#to-create-the-advanced-rule)y seleccione un **tipo de pertenencia** de **dinámica de usuario**.
2. En hello **reglas de pertenencia dinámica** hoja, escriba regla Hola con hello según la sintaxis:

    *Direct Reports for "{obectID_of_manager}"*

    Ejemplo de una regla válida:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. Después de guardar la regla de hello, todos los usuarios con hello especificarán el valor de Id. de administrador se agregarán toohello grupo.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>Utilizando las reglas de toocreate de atributos para los objetos de dispositivo
También puede crear una regla que selecciona objetos de dispositivo para la pertenencia de un grupo. se puede utilizar Hola siguientes atributos de dispositivo:

| Propiedades              | Valores permitidos                  | Uso                                                       |
|-------------------------|---------------------------------|-------------------------------------------------------------|
| accountEnabled          | true false                      | (device.accountEnabled -eq true)                            |
| DisplayName             | Cualquier valor de cadena                | (device.displayName -eq "Rob Iphone”)                       |
| deviceOSType            | Cualquier valor de cadena                | (device.deviceOSType -eq "IOS")                             |
| deviceOSVersion         | Cualquier valor de cadena                | (device.OSVersion -eq "9.1")                                |
| deviceCategory          | Cualquier valor de cadena                | (device.deviceCategory -eq "")                              |
| deviceManufacturer      | Cualquier valor de cadena                | (device.deviceManufacturer - eq "Microsoft")                 |
| deviceModel             | Cualquier valor de cadena                | (device.deviceModel -eq "IPhone 7+")                        |
| deviceOwnership         | Cualquier valor de cadena                | (device.deviceOwnership -eq "")                             |
| domainName              | Cualquier valor de cadena                | (device.domainName -eq "contoso.com")                       |
| enrollmentProfileName   | Cualquier valor de cadena                | (device.enrollmentProfileName -eq "")                       |
| isRooted                | true false                      | (device.deviceOSType -eq true)                              |
| managementType          | Cualquier valor de cadena                | (device.managementType -eq "")                              |
| organizationalUnit      | Cualquier valor de cadena                | (device.organizationalUnit -eq "")                          |
| deviceId                | un valor válido de deviceId                | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d") |
| objectId                | un valor de objectId de AAD válido            | (device.objectId -eq "76ad43c9-32c5-45e8-a272-7b58b58f596d") |

> [!NOTE]
> Estas reglas de dispositivo no se puede crear mediante la lista desplegable de "regla simple" Hola Hola portal de Azure clásico.
>
>

## <a name="next-steps"></a>Pasos siguientes
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Solución de problemas relacionados con las pertenencias dinámicas para grupos](active-directory-accessmanagement-troubleshooting.md)
* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [Cmdlets de Azure Active Directory para configurar las opciones de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
