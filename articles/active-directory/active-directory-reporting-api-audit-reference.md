---
title: "auditoría de Active Directory aaaAzure referencia de API | Documentos de Microsoft"
description: "¿Cómo tooget partió Hola API de auditoría de Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a>Referencia de la API de auditoría de Azure Active Directory
Este tema forma parte de una colección de temas sobre hello Azure Active Directory API de informes.  
Reporting de Azure AD proporciona una API que permite los datos de auditoría tooaccess mediante código o herramientas relacionadas.
ámbito de Hola de este tema es tooprovide, con información de referencia sobre hello **API de auditoría**.

Consulte:

* [Registros de auditoría](active-directory-reporting-azure-portal.md#activity-reports) para más información conceptual

* [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) para obtener más información acerca de la API de informes de Hola.


Si desea:

- Conocer las preguntas más frecuentes, lea nuestras [Preguntas más frecuentes](active-directory-reporting-faq.md) 

- En caso de problemas, [abra una incidencia de soporte técnico](active-directory-troubleshooting-support-howto.md) 


## <a name="who-can-access-hello-data"></a>¿Quién puede tener acceso a datos de hello?
* Usuarios de rol de administrador de seguridad o seguridad lector Hola
* Administradores globales
* Cualquier aplicación que tenga autorización tooaccess Hola API (autorización de la aplicación puede ser el programa de instalación solamente basándose en el permiso del administrador Global)

## <a name="prerequisites"></a>Requisitos previos
En este informe a través de tooaccess de orden Hola API de informes, debe tener:

* Una [edición de Azure Active Directory gratis o superior](active-directory-editions.md)
* Hola completado [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Obtener acceso a las API de Hola
Se puede tener acceso a esta API a través de hello [Explorador de gráficos](https://graphexplorer2.cloudapp.net) o mediante programación con, por ejemplo, PowerShell. En orden para PowerShell toocorrectly interpretar la sintaxis de filtros de OData Hola utilizada en las llamadas de REST de AAD Graph, debe usar acento grave hello (también conocido como: acento grave) carácter demasiado "carácter de escape" hello $. carácter de acento grave Hola actúa como [carácter de escape de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), lo que PowerShell toodo una interpretación literal de carácter de hello $ y evitar confundir como un nombre de variable de PowerShell (es decir: $filter).

Hola de este tema es Hola Explorador de gráficos. Para ver un ejemplo de PowerShell, consulte este [script de PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).

## <a name="api-endpoint"></a>Punto de conexión de API
Puede tener acceso a esta API con hello siguiente URI:  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

No hay ningún límite en hello número de registros devueltos por la API de auditoría de hello Azure AD (uso de la paginación de OData).
Para ver los límites de retención de los datos de informes, consulte [Directivas de retención de informes](active-directory-reporting-retention.md).

Esta llamada devuelve datos de hello en lotes. Cada lote tiene un máximo de 1000 registros.  
tooget Hola siguiente lote de registros, use Hola siguiente vínculo. Obtener información de skiptoken de hello del primer conjunto de registros devueltos de Hola. token de omisión de Hello será final Hola Hola de conjunto de resultados.  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a>Filtros admitidos
Puede limitar número de Hola de registros devueltos por una API de llamar a en forma de un filtro.  
Para inicio de sesión de la API se admiten datos relacionados, Hola después de filtros:

* **$top =\<devolvió un número de registros toobe\>**  -número de hello toolimit de registros devueltos. Se trata de una operación costosa. No se debe usar este filtro si desea tooreturn miles de objetos.     
* **$filter =\<la instrucción de filtro\>**  -toospecify, en función de Hola de campos de filtro admitido, tipo de Hola de registros que le interesa

## <a name="supported-filter-fields-and-operators"></a>Operadores y campos de filtro compatibles
tipo de hello toospecify de registros que le interesa, puede crear una instrucción de filtro que puede contener uno o una combinación de hello después de los campos de filtro:

* [activityDate](#activitydate): define una fecha o un intervalo de fechas
* [categoría](#category) -define la categoría de hello en la que desee toofilter.
* [activityStatus](#activitystatus) -define el estado de saludo de una actividad
* [activityType](#activitytype) -define el tipo de saludo de una actividad
* [actividad](#activity) -define actividad hello como cadena  
* [nombre delactor/](#actorname) -define actor hello en formato de nombre del actor Hola
* [actor/objectid](#actorobjectid) -define actores de Hola en formato de Id. de actor Hola   
* [actor/upn](#actorupn) -define actores hello en formato de nombre principal de usuario del actor hello (UPN) 
* [nombre dedestino/](#targetname) -define el destino de hello en forma de nombre del actor Hola
* [destino/objectid](#targetobjectid) -define el destino de hello en forma de identificador del destino de Hola  
* [destino/upn](#targetupn) -define actores hello en formato de nombre principal de usuario del actor hello (UPN)   

- - -
### <a name="activitydate"></a>activityDate
**Operadores compatibles**: eq, ge, le, gt y lt

**Ejemplo**:

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

**Notas**:

datetime debe estar en formato UTC.

- - -
### <a name="category"></a>categoría

**Valores admitidos**:

| Categoría                         | Valor     |
| :--                              | ---       |
| Core Directory (Directorio principal)                   | Directorio |
| Self-service Password Management (Administración de contraseñas de autorservicio) | SSPR      |
| Self-service Group Management (Administración de grupos de autoservicio)    | SSGM      |
| Account Provisioning (Aprovisionamiento de cuentas)             | Sync      |
| Automated Password Rollover (Sustitución automática de contraseña)      | Automated Password Rollover (Sustitución automática de contraseña) |
| Protección de identidad              | IdentityProtection |
| Invited Users (Usuarios invitados)                    | Invited Users (Usuarios invitados) |
| MIM Service (Servicio MIM)                      | MIM Service (Servicio MIM) |



**Operadores compatibles**: eq

**Ejemplo**:

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a>activityStatus

**Valores admitidos**:

| Estado de la actividad | Valor |
| :--             | ---   |
| Correcto         | 0     |
| Error         | - 1   |

**Operadores compatibles**: eq

**Ejemplo**:

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a>activityType
**Operadores compatibles**: eq

**Ejemplo**:

    $filter=activityType eq 'User'    

**Notas**:

Distingue mayúsculas de minúsculas.

- - -
### <a name="activity"></a>activity
**Operadores compatibles**: eq, contains y startsWith

**Ejemplo**:

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

**Notas**:

Distingue mayúsculas de minúsculas.

- - -
### <a name="actorname"></a>actor/name
**Operadores compatibles**: eq, contains y startsWith

**Ejemplo**:

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

**Notas**:

No distingue mayúsculas de minúsculas.

- - -
### <a name="actorobjectid"></a>actor/objectid
**Operadores compatibles**: eq

**Ejemplo**:

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a>target/namde
**Operadores compatibles**: eq, contains y startsWith

**Ejemplo**:

    $filter=targets/any(t: t/name eq 'some name')    

**Notas**:

No distingue mayúsculas de minúsculas.

- - -
### <a name="targetupn"></a>target/upn
**Operadores compatibles**: eq y startsWith

**Ejemplo**:

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

**Notas**:

* No distingue mayúsculas de minúsculas.
* Se necesita espacio de nombres completo de tooadd Hola consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity

- - -
### <a name="targetobjectid"></a>target/objectid
**Operadores compatibles**: eq

**Ejemplo**:

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a>actor/upn
**Operadores compatibles**: eq y startsWith

**Ejemplo**:

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

**Notas**:

* No distingue mayúsculas de minúsculas. 
* Se necesita espacio de nombres completo de tooadd Hola consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity

- - -
## <a name="next-steps"></a>Pasos siguientes
* ¿Desea toosee ejemplos para las actividades de filtrado de sistema? Extraer del repositorio hello [ejemplos de API de auditoría de Azure Active Directory](active-directory-reporting-api-audit-samples.md).
* ¿Desea más información acerca de la API de generación de informes de hello Azure AD tooknow? Vea [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).

