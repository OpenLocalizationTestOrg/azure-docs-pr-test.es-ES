---
title: roles y usuarios de Azure Analysis Services de base de datos aaaManage | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage y bases de datos roles a los usuarios en un servidor de Analysis Services en Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>Administración de usuarios y roles de base de datos

En el nivel de base de datos de modelo de hello, todos los usuarios deben pertenecer tooa rol. Los roles definen los usuarios con permisos concretos para la base de datos de modelo de Hola. Cualquier usuario o grupo de seguridad agrega rol tooa debe tener una cuenta en un inquilino de Azure AD en hello misma suscripción como servidor de Hola.

Cómo definir roles es diferente dependiendo de herramienta de Hola que se usa, pero efecto hello es Hola igual.

Los permisos de los roles incluyen:
*  **Administrador** -los usuarios tienen permisos completos para la base de datos de Hola. Los roles de base de datos con permisos de administrador son distintos de los administradores de servidor.
*  **Proceso** -los usuarios pueden conectarse tooand realizar operaciones de proceso en la base de datos de Hola y analizar los datos de la base de datos de modelo.
*  **Lectura** -los usuarios pueden utilizar un cliente de aplicación tooconnect tooand analizar los datos de la base de datos de modelo.

Al crear un proyecto de modelo tabular, crea roles y agrega usuarios o grupos de roles de toothose mediante Administrador de roles de SSDT. Cuando servidor tooa implementada, se usa SSMS, [cmdlets de Analysis Services PowerShell](https://msdn.microsoft.com/library/hh758425.aspx), o [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) o quitar roles y miembros de usuario.

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd o administrar roles y usuarios en SSDT  
  
1.  En SSDT > **Explorador de modelos tabulares**, haga clic con el botón derecho en **Roles**.  
  
2.  En **Administrador de roles**, haga clic en **Nuevo**.  
  
3.  Escriba un nombre para el rol de Hola.  
  
     De forma predeterminada, nombre Hola de rol predeterminado de Hola se incrementará numéricamente para cada nuevo rol. Se recomienda que escribir un nombre que identifique claramente el tipo de miembro de hello, por ejemplo, administradores financieros o especialistas en recursos humanos.  
  
4.  Seleccione uno de los siguientes permisos de hello:  
  
    |Permiso|Descripción|  
    |----------------|-----------------|  
    |**None**|Los miembros no pueden modificar el esquema del modelo hello y no pueden consultar los datos.|  
    |**Lectura**|Los miembros pueden consultar datos (según los filtros de fila) pero no pueden modificar el esquema del modelo Hola.|  
    |**Lectura y proceso**|Los miembros pueden consultar datos (en función de filtros de nivel de fila) y las operaciones de procesar y procesar todo de ejecución, pero no pueden modificar el esquema del modelo Hola.|  
    |**Proceso**|Los modelos pueden ejecutar las operaciones Procesar y Procesar todo. No se puede modificar el esquema del modelo hello y no se puede consultar los datos.|  
    |**Administrador**|Los miembros pueden modificar el esquema del modelo de Hola y consultar todos los datos.|   
  
5.  Si el rol de hello es crear ha leído o permiso de lectura y procesamiento, puede agregar filtros de fila mediante una fórmula DAX. Haga clic en hello **filtros de fila** ficha, seleccione una tabla y, luego, haga clic en hello **filtro DAX** campo y, a continuación, escriba una fórmula DAX.
  
6.  Haga clic en **Miembros** > **Agregar externo**.  
  
8.  En **Agregar miembro externo**, escriba usuarios o grupos en Azure AD del inquilino por dirección de correo electrónico. Una vez que hace clic en Aceptar y cierra el Administrador de roles, los roles y los miembros de rol aparecen en el Explorador de modelos tabulares. 
 
     ![Roles y usuarios en el Explorador de modelos tabulares](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. Implementar el servidor de Analysis Services de Azure tooyour.


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd o administrar roles y usuarios en SSMS
tooadd roles y usuarios tooa implementado la base de datos de modelo, debe ser servidor toohello conectado como administrador del servidor o que ya esté en un rol de base de datos con permisos de administrador.

1. En el Explorador de objetos, haga clic con el botón derecho en **Rol** > **Nuevo rol**.

2. En **Crear rol**, escriba un nombre de rol y su descripción.

3. Seleccione un permiso.
   |Permiso|Descripción|  
   |----------------|-----------------|  
   |**Control total (administrador)**|Los miembros pueden modificar el esquema de modelo de hello, procesar y puede consultar todos los datos.| 
   |**Proceso de una base de datos**|Los modelos pueden ejecutar las operaciones Procesar y Procesar todo. No se puede modificar el esquema del modelo hello y no se puede consultar los datos.|  
   |**Lectura**|Los miembros pueden consultar datos (según los filtros de fila) pero no pueden modificar el esquema del modelo Hola.|  
  
4. Haga clic en **Pertenencia** y, luego, escriba un usuario o grupo en Azure AD del inquilino por dirección de correo electrónico.

     ![Agregar usuario](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. Si el rol de Hola que está creando tiene permiso de lectura, puede agregar filtros de fila mediante una fórmula DAX. Haga clic en **filtros de fila**, seleccione una tabla y, a continuación, escriba una fórmula DAX en hello **filtro DAX** campo. 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd roles y usuarios mediante un script TMSL
Puede ejecutar un script TMSL en la ventana XMLA de hello en SSMS o mediante PowerShell. Hola de uso [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) hello y comando [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) objeto.

**Script TMSL de ejemplo**

En este ejemplo, un usuario externo B2B y un grupo se agregan toohello de función de analista con permisos de lectura para la base de datos de hello SalesBI. Ambos Hola usuario externo y grupo debe estar en el mismo inquilino de Azure AD.

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd roles y usuarios con PowerShell
Hola [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) módulo proporciona la base de datos específica de la tarea de administración hello y cmdlets de uso general cmdlet Invoke-ASCmd que acepta un script o consulta de Tabular Model Scripting Language (TMSL). Hola siguientes cmdlets se usa para administrar usuarios y roles de base de datos.
  
|Cmdlet|Descripción|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Agregar un rol de base de datos de miembro tooa.| 
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Quita un miembro de un rol de base de datos.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Ejecuta un script de TMSL.|

## <a name="row-filters"></a>Filtros de fila  
Los filtros de fila definen las filas de una tabla que los miembros de un rol determinado pueden consultar. Los filtros de fila están definidos para cada tabla en un modelo mediante fórmulas DAX.  
  
Los filtros de fila solo se pueden definir para los roles con permisos de lectura y lectura y proceso. De forma predeterminada, si no se define un filtro de fila para una tabla determinada, los miembros pueden consultar todas las filas de tabla de Hola a menos que el filtrado cruzado se aplica de otra tabla.
  
 Los filtros de fila requieren una fórmula DAX, que se debe evaluar tooa valor TRUE/FALSE, filas de hello toodefine que pueden ser consultadas por los miembros de ese rol concreto. No se puede consultar las filas no incluidas en hello fórmula DAX. Por ejemplo, Hola tabla Customers con la siguiente expresión de filtros de fila, de hello *= clientes [Country] = "EE"*, los miembros del rol de ventas de hello solo pueden ver los clientes de Estados Unidos de Hola.  
  
Aplicar filtros de fila toohello especificada filas y filas relacionadas. Si una tabla tiene varias relaciones, los filtros aplican seguridad para la relación de Hola que está activo. Los filtros de fila forman una intersección con otros filtros de fila definidos para las tablas relacionadas, por ejemplo:  
  
|Tabla|Expresión DAX|  
|-----------|--------------------|  
|Region|=Region[Country]="EE. UU."|  
|ProductCategory|=ProductCategory[Name]="Bicicletas"|  
|Transacciones|=Transactions[Year]=2016|  
  
 efecto neto de Hello es miembros pueden consultar filas de datos donde es cliente de hello en Estados Unidos de hello, Hola categoría de producto sea bicycles y año de hello es 2016. Los usuarios no pueden consultar las transacciones fuera de Estados Unidos de hello, las transacciones que no cumplan o transacciones no están en 2016 a menos que sean miembro de otro rol que les conceda estos permisos.
  
 Puede utilizar el filtro de hello, *=FALSE()*, toodeny filas de tooall de acceso para una tabla completa.

## <a name="next-steps"></a>Pasos siguientes
  [Administración de administradores del servidor](analysis-services-server-admins.md)   
  [Administración de Azure Analysis Services con PowerShell](analysis-services-powershell.md)  
  [Referencia Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

