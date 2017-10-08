---
title: "informe de actividad de aaaAzure inicio de sesión de Active Directory referencia de API | Documentos de Microsoft"
description: "Referencia de API de informe de actividad de hello en el inicio de sesión de Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a>Referencia de la API de informes de actividad de inicio de sesión de Azure Active Directory
Este tema forma parte de una colección de temas sobre hello Azure Active Directory API de informes.  
Reporting de Azure AD proporciona una API que permite los datos del informe de actividad de inicio de sesión tooaccess mediante código o herramientas relacionadas.
ámbito de Hola de este tema es tooprovide, con información de referencia sobre hello **API de informes de actividad de inicio de sesión**.

Consulte:

* [Actividades de inicio de sesión](active-directory-reporting-azure-portal.md#activity-reports) para obtener más información
* [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) para obtener más información acerca de la API de informes de Hola.


## <a name="who-can-access-hello-api-data"></a>¿Quién puede acceder a datos de la API de saludo?
* Los usuarios y entidades de servicio de rol de administrador de seguridad o seguridad Reader de Hola
* Administradores globales
* Cualquier aplicación que tenga autorización tooaccess Hola API (autorización de la aplicación puede ser el programa de instalación solamente basándose en el permiso del administrador Global)

acceso de tooconfigure para una aplicación tooaccess las API de seguridad tales como eventos de inicio de sesión, Hola de uso derivados de la solicitud de hello tooadd de PowerShell entidad de servicio en función de lector de seguridad de Hola

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a>Requisitos previos
Hola a tooaccess este informe a través de la API de generación de informes, debe tener:

* Tener una [edición de Azure Active Directory Premium P1 o P2](active-directory-editions.md)
* Hola completado [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md). 

## <a name="accessing-hello-api"></a>Obtener acceso a las API de Hola
Se puede tener acceso a esta API a través de hello [Explorador de gráficos](https://graphexplorer2.cloudapp.net) o mediante programación con, por ejemplo, PowerShell. En orden para PowerShell toocorrectly interpretar la sintaxis de filtros de OData Hola utilizada en las llamadas de REST de AAD Graph, debe usar acento grave hello (también conocido como: acento grave) carácter demasiado "carácter de escape" hello $. carácter de acento grave Hola actúa como [carácter de escape de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), lo que PowerShell toodo una interpretación literal de carácter de hello $ y evitar confundir como un nombre de variable de PowerShell (es decir: $filter).

Hola de este tema es Hola Explorador de gráficos. Para ver un ejemplo de PowerShell, consulte este [script de PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).

## <a name="api-endpoint"></a>Punto de conexión de API
Puede tener acceso a esta API con hello siguiente URI base:  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



Debido a toohello el volumen de datos, esta API tiene un límite de un millón de registros devueltos. 

Esta llamada devuelve datos de hello en lotes. Cada lote tiene un máximo de 1000 registros.  
tooget Hola siguiente lote de registros, use Hola siguiente vínculo. Obtener hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) información del primer conjunto de registros devueltos de Hola. token de omisión de Hello será final Hola Hola de conjunto de resultados.  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a>Filtros admitidos
Puede limitar número de Hola de registros devueltos por una API de llamar a en forma de un filtro.  
Para inicio de sesión de la API se admiten datos relacionados, Hola después de filtros:

* **$top =\<devolvió un número de registros toobe\>**  -número de hello toolimit de registros devueltos. Se trata de una operación costosa. No se debe usar este filtro si desea tooreturn miles de objetos.  
* **$filter =\<la instrucción de filtro\>**  -toospecify, en función de Hola de campos de filtro admitido, tipo de Hola de registros que le interesa

## <a name="supported-filter-fields-and-operators"></a>Operadores y campos de filtro compatibles
tipo de hello toospecify de registros que le interesa, puede crear una instrucción de filtro que puede contener uno o una combinación de hello después de los campos de filtro:

* [signinDateTime](#signindatetime) : define una fecha o un intervalo de fechas.
* [identificador de usuario](#userid) -define el identificador. del usuario de hello en función de usuario específico
* [userPrincipalName](#userprincipalname) -define el nombre principal de usuario (UPN) de un usuario de hello en función de usuario específico
* [appId](#appid) -define el identificador de la aplicación de hello en función de aplicación específica
* [appDisplayName](#appdisplayname) -define el nombre para mostrar la aplicación de hello en función de aplicación específica
* [loginStatus](#loginStatus) -define el estado de Hola de inicios de sesión de hello (éxito o error)

> [!NOTE]
> Al utilizar el Explorador de gráfico, Hola necesita toouse Hola correcto de caso para cada letra es los campos de filtro.
> 
> 

toonarrow ámbito Hola de hello devolvió datos, puede crear combinaciones de filtros de hello compatible y campos de filtro. Por ejemplo, hello siguiente instrucción devuelve Hola top 10 registros entre el 1 de julio de 2016 y 6 de julio de 2016:

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a>signinDateTime
**Operadores compatibles**: eq, ge, le, gt y lt

**Ejemplo**:

Uso de una fecha concreta

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



Uso de un intervalo de fechas    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


**Notas**:

parámetro de fecha y hora de Hello debe estar en formato de hora UTC de Hola 

- - -
### <a name="userid"></a>userId
**Operadores compatibles**: eq

**Ejemplo**:

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

**Notas**:

Hola de identificador de usuario es un valor de cadena

- - -
### <a name="userprincipalname"></a>userPrincipalName
**Operadores compatibles**: eq

**Ejemplo**:

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


**Notas**:

Hola de userPrincipalName es un valor de cadena

- - -
### <a name="appid"></a>appId
**Operadores compatibles**: eq

**Ejemplo**:

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



**Notas**:

Hola de appId es un valor de cadena

- - -
### <a name="appdisplayname"></a>appDisplayName
**Operadores compatibles**: eq

**Ejemplo**:

    $filter=appDisplayName+eq+'Azure+Portal' 


**Notas**:

Hola de appDisplayName es un valor de cadena

- - -
### <a name="loginstatus"></a>loginStatus
**Operadores compatibles**: eq

**Ejemplo**:

    $filter=loginStatus+eq+'1'  


**Notas**:

Hay dos opciones para hello loginStatus: 0 - se ejecuta correctamente, 1 - error

- - -
## <a name="next-steps"></a>Pasos siguientes
* ¿Desea toosee ejemplos de actividades de inicio de sesión filtradas? Extraer del repositorio hello [ejemplos de API de informes de actividad de inicio de sesión de Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).
* ¿Desea más información acerca de la API de generación de informes de hello Azure AD tooknow? Vea [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).

