---
title: "permisos de usuario y aaaAuthentication en los servicios de análisis de Azure | Documentos de Microsoft"
description: "Obtenga información sobre la autenticación y los permisos de usuario en Azure Analysis Services."
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
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>Autenticación y permisos de usuario
Azure Analysis Services usa Azure Active Directory (Azure AD) para la administración de identidades y la autenticación de usuarios. Cualquier usuario que crea, administración o conectar tooan Azure Analysis Services server debe tener una identidad de usuario válido un [inquilino de Azure AD](../active-directory/active-directory-administer.md) Hola misma suscripción.

Azure Analysis Services admite la [colaboración B2B de Azure AD](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md). Con B2B, los usuarios fuera de una organización pueden ser usuarios invitados en un directorio de Azure AD. Los invitados pueden provenir de otro directorio de inquilino de Azure AD o de cualquier dirección de correo electrónico válida. Una vez invitó y usuario de hello acepta Hola Enviar invitación por correo electrónico de Azure, hello identidad del usuario se agrega el directorio del inquilino toohello. Las identidades, a continuación, se pueden agregar grupos de toosecurity o como miembros de un rol de base de datos o el administrador del servidor.

![Arquitectura de autenticación de Azure Analysis Services](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>Autenticación
Todas las herramientas y las aplicaciones cliente usan uno o varios de Analysis Services de hello [bibliotecas de cliente](analysis-services-data-providers.md) (AMO, MSOLAP, ADOMD) tooconnect tooa server. 

Las tres bibliotecas de cliente admiten el flujo interactivo de Azure AD y los métodos de autenticación no interactivos. Hola dos métodos no interactivo, métodos de contraseña de Active Directory y la autenticación integrada de Active Directory se pueden utilizar en las aplicaciones que utilizan AMOMD y MSOLAP. Estos dos métodos nunca generan cuadros de diálogo emergentes.

Las aplicaciones cliente como Excel y Power BI Desktop y herramientas, como SSMS y SSDT instalan versiones más recientes de Hola de bibliotecas de hello cuando actualiza toohello última versión. Power BI Desktop, SSMS y SSDT se actualizan de manera mensual. Excel [se actualiza con Office 365](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516). Actualizaciones de Office 365 son menos frecuentes y algunas organizaciones utilizan canal aplazada hello, actualizaciones de significado se difieren los meses de toothree.

 Según la aplicación de cliente de Hola o herramienta que se usa, tipo hello de autenticación y cómo iniciar sesión puede ser diferente. Cada aplicación puede admitir características diferentes para conectar servicios toocloud como Azure Analysis Services.


### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Los servidores de Azure Analysis Services admiten conexiones desde [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) y versiones superiores mediante el uso de autenticación de Windows, autenticación de contraseñas de Active Directory y autenticación universal de Active Directory. En general, se recomienda usar la autenticación universal de Active Directory por los motivos siguientes:

*  Admite los métodos de autenticación interactivos y no interactivos.

*  Permite que los usuarios de invitado de Azure B2B invitados en el inquilino de Azure AS Hola. Al conectar el servidor de tooa, usuarios invitados deben seleccionar autenticación Universal de Active Directory cuando se conecta el servidor de toohello.

*  Admite Multi-Factor Authentication (MFA). Azure MFA ayuda a proteger acceso toodata y aplicaciones con una gama de opciones de comprobación: llamada de teléfono, mensaje de texto, las tarjetas inteligentes con pin o la notificación de aplicación móvil. MFA interactivo con Azure AD puede generar un cuadro de diálogo emergente para la validación.

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)
SSDT conecta tooAzure Analysis Services mediante la autenticación Universal de Active Directory con la compatibilidad con MFA. Los usuarios están solicitada toosign en tooAzure en la primera implementación de hello mediante su Id. de organización (correo electrónico). Los usuarios deben iniciar en tooAzure con una cuenta con permisos de administrador de servidor en servidor de saludo que está implementando. Al iniciar sesión en hello tooAzure primera vez, se asigna un token. SSDT se almacena en memoria caché Hola token en memoria para futuras conexiones.

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop se conecta mediante la autenticación Universal de Active Directory con la compatibilidad con MFA tooAzure Analysis Services. Los usuarios están solicitada toosign en tooAzure en la primera conexión de hello mediante su Id. de organización (correo electrónico). Los usuarios deben iniciar sesión tooAzure con una cuenta que se incluye en un administrador del servidor o un rol de base de datos.

### <a name="excel"></a>Excel
Los usuarios de Excel pueden conectarse tooa server mediante una cuenta de Windows, un identificador de organización (dirección de correo electrónico) o una dirección de correo electrónico externas. Las identidades de correo electrónico externas deben existir en hello Azure AD como usuario invitado.

## <a name="user-permissions"></a>Permisos de usuario

**Los administradores del servidor** son la instancia del servidor de Analysis Services de Azure tooan específico. Se conectan con herramientas como portal de Azure, SSMS, mientras que SSDT tooperform tareas como agregar bases de datos y administrar roles de usuario. De forma predeterminada, usuario de Hola que crea Hola servidor se agrega automáticamente como un administrador del servidor de Analysis Services. Es posible agregar otros administradores mediante Azure Portal o SSMS. Los administradores del servidor deben tener una cuenta de inquilino de Azure AD de Hola Hola misma suscripción. más información, consulte toolearn [administrar a los administradores de servidor](analysis-services-server-admins.md). 


**Los usuarios de la base de datos** conectarse toomodel bases de datos mediante aplicaciones cliente como Excel o Power BI. Los usuarios deben agregarse toodatabase roles. Los roles de base de datos definen permisos de administrador, proceso o lectura para una base de datos. Es importante toounderstand usuarios de base de datos en un rol con permisos de administrador es diferente a los administradores del servidor. Sin embargo, de manera predeterminada, los administradores de servidor también son administradores de base de datos. más información, consulte toolearn [administrar usuarios y roles de base de datos](analysis-services-database-users.md).

**Propietarios de recursos de Azure**. Los propietarios de recursos administran los recursos de una suscripción de Azure. Los propietarios del recurso pueden agregar tooOwner de identidades de usuario de Azure AD o Roles de colaborador dentro de una suscripción mediante **el control de acceso** en el portal de Azure o con plantillas del Administrador de recursos de Azure. 

![Control de acceso en Azure Portal](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

Roles en este nivel aplican toousers o cuentas que necesitan tooperform tareas que se pueden completar en el portal de Hola o mediante el uso de plantillas del Administrador de recursos de Azure. más información, consulte toolearn [Role-Based Access Control](../active-directory/role-based-access-control-what-is.md). 


## <a name="database-roles"></a>Roles de base de datos

 Los roles definidos para un modelo tabular son roles de base de datos. Es decir, los roles de hello contienen a miembros formada por usuarios de Azure AD y grupos de seguridad que tengan permisos específicos que definen las acciones de hello esos miembros pueden realizar en una base de datos de modelo. Un rol de base de datos se crea como un objeto independiente en la base de datos de Hola y aplica solo toohello base de datos en el que se crea ese rol.   
  
 De forma predeterminada, cuando se crea un nuevo proyecto de modelo tabular, proyecto de modelos de hello no tiene ningún rol. Roles pueden definirse mediante el uso de cuadro de diálogo Administrador de roles de hello en SSDT. Cuando los roles se definen durante el diseño del proyecto de modelo, son base de datos del área de trabajo de modelo de toohello solo aplicada. Cuando se implementa el modelo de hello, hello mismos roles son modelo aplicado toohello implementado. Una vez que se implementa un modelo, los administradores de servidor y de base de datos pueden administrar los roles y los miembros con SSMS. más información, consulte toolearn [administrar usuarios y roles de base de datos](analysis-services-database-users.md).
  


## <a name="next-steps"></a>Pasos siguientes

[Administrar acceso tooresources con grupos de Active Directory de Azure](../active-directory/active-directory-manage-groups.md)   
[Administración de usuarios y roles de base de datos](analysis-services-database-users.md)  
[Administración de administradores de servidor](analysis-services-server-admins.md)  
[Control de acceso basado en roles](../active-directory/role-based-access-control-what-is.md)  