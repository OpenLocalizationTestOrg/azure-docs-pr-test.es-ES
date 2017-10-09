---
title: "autenticación de Azure Active Directory aaaConfigure - SQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconnect tooSQL base de datos y almacenamiento de datos de SQL mediante autenticación de Azure Active Directory."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Configuración y administración de la autenticación de Azure Active Directory con SQL Database o SQL Data Warehouse

Este artículo muestra cómo toocreate rellenar Azure AD y, a continuación, usar Azure AD con la base de datos de SQL Azure y almacenamiento de datos de SQL. Para ver un resumen, consulte [Autenticación con Azure Active Directory](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Conexión tooSQL servidor se ejecuta en una VM de Azure no es compatible con una cuenta de Azure Active Directory. Utilice en su lugar una cuenta de Active Directory del dominio.

## <a name="create-and-populate-an-azure-ad"></a>Crear y rellenar una instancia de Azure AD.
Cree una instancia de Azure AD y rellénela con usuarios y grupos. Azure AD puede ser el dominio administrado de Azure AD del dominio inicial. Hola. Azure AD también puede ser un local Active Directory Domain Services que se federa con hello Azure AD.

Para obtener más información, consulte [integrar las identidades locales con Azure Active Directory](../active-directory/active-directory-aadconnect.md), [agregar su propios tooAzure de nombre de dominio AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure ahora admite la federación con Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [administrar su directorio Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [administrar Azure AD mediante Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), y [identidad híbrida Puertos y protocolos necesarios](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>Opcional: Asociar o cambiar Hola active directory que está asociada actualmente con la suscripción de Azure
tooassociate la base de datos con el directorio de hello Azure AD para su organización, asegúrese de directorio Hola un directorio de confianza para base de datos de hello hospedaje de hello suscripción de Azure. Para obtener más información, consulte [Cómo se asocian las suscripciones a Azure con Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).

**Información adicional:** cada suscripción de Azure tiene una relación de confianza con una instancia de Azure AD. Esto significa que confía en ese directorio tooauthenticate usuarios, servicios y dispositivos. Varias suscripciones pueden confiar Hola mismo directorio, pero una suscripción confía en un único directorio. Puede ver qué directorio confía en su suscripción bajo hello **configuración** ficha en [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Esta relación de confianza que tiene una suscripción con un directorio es distinto de la relación de Hola que tiene una suscripción con todos los demás recursos de Azure (sitios Web, bases de datos etc.), que son más parecidos a los recursos secundarios de una suscripción. Si una suscripción expira, acceder a toothose otros recursos asociados con la suscripción de hello también se detiene. Pero Hola directorio permanece en Azure, y puede asociar otra suscripción a ese directorio y continuar a los usuarios de toomanage Hola directorio. Para más información sobre recursos, consulte [Descripción de acceso a los recursos de Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Hello procedimientos siguientes muestran cómo toochange Hola asocia directorio para una suscripción determinada.
1. Conectar tooyour [Portal clásico de Azure](https://manage.windowsazure.com/) mediante el Administrador de una suscripción de Azure.
2. En el encabezado de la izquierda hello, seleccione **configuración**.
3. Las suscripciones aparecen en la pantalla de configuración de bienvenida. Si Hola deseado suscripción no aparece, haga clic en **suscripciones** en la parte superior de hello, lista desplegable hello **filtro por directorio** cuadro y seleccione directorio de Hola que contiene las suscripciones y, a continuación, haga clic en **Aplicar**.
   
    ![seleccionar suscripción][4]
4. Hola **configuración** área, haga clic en la suscripción y, a continuación, haga clic en **editar directorio** final Hola de página Hola.
   
    ![portal de configuración de ad][5]
5. Hola **editar directorio** cuadro, seleccione hello Azure Active Directory que está asociado a su almacén de datos de SQL o SQL Server y, a continuación, haga clic en hello flecha siguiente.
   
    ![selección de editar directorio][6]
6. Hola **confirmar** directorio cuadro de diálogo de asignación, confirme que "**se quitarán todos los coadministradores.**"
   
    ![confirmación de editar directorio][7]
7. Haga clic en el portal de hello comprobación tooreload Hola.

   > [!NOTE]
   > Cuando cambie el directorio de hello, coadministradores tooall de acceso, usuarios de Azure AD y los grupos y se quitan usuarios de recurso basado en el directorio y ya no tienen acceso toothis suscripción o a sus recursos. Solo, como un administrador de servicios, puede configurar el acceso para las entidades de seguridad basados en el nuevo directorio de Hola. Este cambio puede tardar una cantidad considerable de recursos de tooall toopropagate de tiempo. Cambiando el directorio de hello, también cambios hello Administrador de Azure AD para la base de datos SQL y almacenamiento de datos de SQL y denegar el acceso de la base de datos para los usuarios de Azure AD existentes. Hola Azure AD, administrador debe restablecer (tal y como se describe a continuación) y Azure nuevo se deben crear usuarios de AD.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Creación de un administrador de Azure AD para Azure SQL Server
Cada servidor de SQL Azure (que hospeda una base de datos SQL o almacenamiento de datos SQL) se inicia con una cuenta de administrador de servidor único que es administrador de Hola de hello todo Azure SQL server. Se debe crear un segundo administrador de SQL Server que sea una cuenta de Azure AD. Esta entidad de seguridad se crea como un usuario de base de datos independiente en la base de datos maestra Hola. Como administradores, cuentas de administrador del servidor de hello son miembros de hello **db_owner** rol en todos los usuarios de base de datos y escriba cada base de datos de usuario como hello **dbo** usuario. Para obtener más información acerca de las cuentas de administrador de servidor hello, consulte [administrar bases de datos e inicios de sesión en la base de datos de SQL Azure](sql-database-manage-logins.md).

Al usar Azure Active Directory con replicación geográfica, Administrador de Azure Active Directory de hello debe configurarse para hello principal y los servidores secundarios de Hola. Si un servidor no tiene un administrador de Azure Active Directory, a continuación, los usuarios e inicios de sesión de Azure Active Directory reciben un error de tooserver "No se puede conectar".

> [!NOTE]
> Los usuarios que no se basan en una cuenta de Azure AD (incluida la cuenta de administrador de servidor de SQL Azure de hello), no se puede crear usuarios basados en AD de Azure, porque no tienen toovalidate permiso propuesto a los usuarios de base de datos con hello Azure AD.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Aprovisionamiento de un administrador de Azure Active Directory para el servidor de Azure SQL Server

Hola dos procedimientos siguientes muestra cómo tooprovision un administrador de Azure Active Directory para el servidor de SQL Azure en hello portal de Azure y mediante el uso de PowerShell.

### <a name="azure-portal"></a>Azure Portal
1. Hola [portal de Azure](https://portal.azure.com/), en Hola esquina superior derecha, haga clic en el toodrop de conexión hacia abajo en una lista de posibles directorios de Active Directory. Elija Hola corregir Active Directory como valor predeterminado de hello Azure AD. Este paso vínculos Hola asociación de la suscripción con Active Directory con el servidor de SQL Azure asegurándose de que Hola misma suscripción se usa para Azure AD y SQL Server. (servidor de SQL Azure Hola puede hospedar base de datos de SQL Azure o almacenamiento de datos de SQL Azure.)   
    ![choose-ad][8]   
    
2. Hola izquierda Seleccione pancarta **servidores SQL Server**, seleccione la **SQL server**y, a continuación, en hello **SQL Server** hoja, haga clic en **Administrador de Active Directory**.   
3. Hola **Administrador de Active Directory** hoja, haga clic en **Set admin**.   
    ![Seleccionar Active Directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. Hola **Agregar administrador** hoja, buscar un usuario, usuario seleccione Hola o toobe un administrador de grupo y, a continuación, haga clic en **seleccione**. (hoja de administración de Active Directory de hello muestra todos los miembros y grupos de Active Directory. No se pueden seleccionar los usuarios o grupos que aparecen atenuados porque no se admiten como administradores de Azure AD. (Ver lista de Hola de administradores admitidos en hello **características de Azure AD y limitaciones** sección de [Use Azure autenticación de Active Directory para la autenticación con la base de datos SQL o almacenamiento de datos de SQL](sql-database-aad-authentication.md).) Control de acceso basado en roles (RBAC) aplica solo toohello portal y no es propagado tooSQL Server.   
    ![Seleccionar administrador](./media/sql-database-aad-authentication/select-admin.png)  
    
5. En parte superior de Hola de hello **Administrador de Active Directory** hoja, haga clic en **guardar**.   
    ![Guardar administrador](./media/sql-database-aad-authentication/save-admin.png)   

proceso de Hello del cambio de administrador de hello puede tardar varios minutos. Aparecerá el nuevo administrador de Hola Hola **Administrador de Active Directory** cuadro.

   > [!NOTE]
   > Al configurar el Administrador de hello Azure AD, Hola nuevo nombre de administrador (usuario o grupo) no puede estar ya presente en la base de datos maestra Hola virtual como un usuario de autenticación de SQL Server. Si está presente, se producirá un error en el programa de instalación de administración de hello Azure AD; revertir su creación y que indica que este tipo administrador (nombre) ya existe. Puesto que este tipo un usuario de autenticación de SQL Server no forma parte del programa Hola a Azure AD, se produce un error en cualquier servidor de toohello de tooconnect esfuerzo mediante autenticación de Azure AD.
   > 


toolater quitar un administrador, en parte superior de Hola de hello **Administrador de Active Directory** hoja, haga clic en **quitar administrador**y, a continuación, haga clic en **guardar**.

### <a name="powershell"></a>PowerShell
toorun cmdlets de PowerShell, necesita toohave PowerShell de Azure instalada y en ejecución. Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

tooprovision un administrador de Azure AD, ejecute hello siga los comandos de PowerShell de Azure:

* Add-AzureRmAccount
* Select-AzureRmSubscription

Cmdlets usa tooprovision y administrar la administración de Azure AD:

| Nombre del cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Aprovisiona un administrador de Azure Active Directory para Azure SQL Server o para Azure SQL Data Warehouse. (Debe ser de la suscripción actual de hello). |
| [Remove-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Quita un administrador de Azure Active Directory para Azure SQL Server o para Azure SQL Data Warehouse. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Devuelve información acerca de un administrador de Active Directory de Azure configurada actualmente para el servidor de SQL Azure de Hola o almacenamiento de datos de SQL Azure. |

Usar PowerShell comando get-help toosee se ofrecen más detalles para cada uno de estos comandos, por ejemplo ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Hola siguiendo las disposiciones de secuencia de comandos con nombre de un grupo de administradores de Azure AD **DBA_Group** (Id. de objeto `40b79501-b343-44ed-9ce7-da4c8cc7353f`) para hello **demo_server** servidor en un grupo de recursos denominado **23 de grupo** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Hola **DisplayName** parámetro de entrada acepta el nombre para mostrar hello Azure AD u Hola nombre Principal de usuario. Por ejemplo, ``DisplayName="John Smith"`` y ``DisplayName="johns@contoso.com"``. Para hello solo de grupos de AD de Azure AD de Azure se admite el nombre para mostrar.

> [!NOTE]
> Hola comando de PowerShell de Azure ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` no le impide desde el aprovisionamiento de administradores de Azure AD para que los usuarios no admitidos. Un usuario no compatible se puede aprovisionar, pero no puede conectar la base de datos de tooa. 
> 

Hello en el ejemplo siguiente se usa Hola opcional **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Hello Azure AD **ObjectID** es necesaria cuando hello **DisplayName** no es único. Hola tooretrieve **ObjectID** y **DisplayName** valores, utilice Hola sección de Active Directory del Portal de Azure clásico y ver propiedades de Hola de un usuario o grupo.
> 

Hola siguiente ejemplo devuelve información acerca de Hola actual de Azure AD, Administrador de servidor de SQL Azure:

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

Hola de ejemplo siguiente quita un administrador de Azure AD:

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

También puede aprovisionar un administrador de Azure Active Directory mediante las API de REST de Hola. Para obtener más información, consulte [Service Management REST API Reference and Operations for Azure SQL Databases](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>CLI  
También puede aprovisionar un administrador de Azure AD mediante la llamada Hola siga los comandos CLI:
| Comando | Descripción |
| --- | --- |
|[az sql server ad-admin create](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Aprovisiona un administrador de Azure Active Directory para Azure SQL Server o para Azure SQL Data Warehouse. (Debe ser de la suscripción actual de hello). |
|[az sql server ad-admin delete](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Quita un administrador de Azure Active Directory para Azure SQL Server o para Azure SQL Data Warehouse. |
|[az sql server ad-admin list](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Devuelve información acerca de un administrador de Active Directory de Azure configurada actualmente para el servidor de SQL Azure de Hola o almacenamiento de datos de SQL Azure. |
|[az sql server ad-admin update](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Actualiza el Administrador de Active Directory de Hola para un servidor de SQL Azure o el almacenamiento de datos de SQL Azure. |

Para más información acerca de los comandos de la CLI, consulte [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>Configurar los equipos cliente.
En todos los equipos cliente, desde el que las aplicaciones o los usuarios conectan tooAzure base de datos SQL o almacenamiento de datos de SQL Azure mediante identidades de Azure AD, debe instalar Hola siguiente software:

* .NET Framework 4.6 o una versión posterior de [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* Biblioteca de autenticación de Azure Active Directory para SQL Server (**ADALSQL. DLL**) está disponible en varios idiomas (x86 y amd64) desde el centro de descarga de hello en [Microsoft biblioteca de autenticación de Active Directory para Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

Puede cumplir estos requisitos mediante:

* Instalar cualquiera [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) o [SQL Server Data Tools para Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) cumple Hola requisito de .NET Framework 4.6.
* SSMS instala la versión de Hola x86 de **ADALSQL. DLL**.
* SSDT instala la versión de Hola amd64 de **ADALSQL. DLL**.
* Hola más reciente de Visual Studio desde [descargas de Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) cumple el requisito de hello 4.6 de .NET Framework, pero no instala Hola amd64 necesario versión de **ADALSQL. DLL**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Crear usuarios de base de datos independiente en la base de datos asignado tooAzure identidades de AD

Autenticación de Azure Active Directory requiere toobe de los usuarios de base de datos creado como usuarios de base de datos independiente. Un usuario de base de datos independiente en función de una identidad de Azure AD, es un usuario de base de datos que no tiene un inicio de sesión en la base de datos maestra de Hola y qué identidad de tooan mapas en Hola directorio de Azure AD que está asociado a la base de datos de Hola. Hola identidad de Azure AD puede ser una cuenta de usuario individual o un grupo. Para más información sobre los usuarios de bases de datos independientes, vea [Usuarios de bases de datos independientes: cómo hacer que la base de datos sea portátil](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Los usuarios de base de datos (con excepción de Hola de administradores) no se puede crear mediante el portal. Los roles RBAC no son propagado tooSQL servidor, base de datos SQL o almacenamiento de datos SQL. Las funciones de RBAC Azure se utilizan para administrar recursos de Azure y no aplican permisos toodatabase. Por ejemplo, hello **SQL Server colaborador** rol no concede acceso tooconnect toohello base de datos SQL o almacenamiento de datos SQL. debe tener permiso de acceso de Hello directamente en la base de datos de hello mediante instrucciones Transact-SQL.
>

toocreate un usuario de base de datos de contenido basados en AD Azure (distinto de hello administrador del servidor que pertenece la base de datos de hello), conectar la base de datos de toohello con una identidad de Azure AD, como un usuario con al menos Hola **ALTER ANY USER** permiso. A continuación, usar hello la sintaxis de Transact-SQL:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* puede ser el nombre principal de usuario de Hola de un nombre para mostrar Azure AD Hola o de usuario para un grupo de Azure AD.

**Ejemplos:** toocreate un usuario de base de datos independiente que representa un anuncio de Azure federados o administrados de usuario de dominio:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate un usuario de base de datos independiente que representa un anuncio de Azure o federado grupo de dominio, proporcionar Hola nombre para mostrar de un grupo de seguridad:
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate un usuario de base de datos independiente que represente una aplicación que se conecte mediante un símbolo (token) de Azure AD:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  No se puede crear directamente un usuario de Azure Active Directory que no sea de hello Azure Active Directory que está asociada a su suscripción de Azure. Sin embargo, los miembros de otros directorios de Active Directory que son los usuarios importados en hello asociados Active Directory (conocidos como los usuarios externos) se pueden agregar grupo de Active Directory de tooan en Active Directory del inquilino de Hola. Mediante la creación de un usuario de base de datos independiente para ese grupo de AD, hello los usuarios de hello externo de Active Directory pueden tener acceso tooSQL base de datos.   

Para más información sobre la creación de usuarios de bases de datos independientes basados en identidades de Azure Active Directory, vea [CREAR USUARIO (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Quitar Administrador de Azure Active Directory de Hola de Azure SQL server impide que cualquier usuario de autenticación de Azure AD conectar el servidor de toohello. Si es necesario, un administrador de SQL Database puede quitar manualmente a usuarios de Azure AD no utilizados.   

>  [!NOTE]
>  Si recibe un **tiempo de espera de conexión expirado**, puede que necesite tooset hello `TransparentNetworkIPResolution` parámetro de toofalse de cadena de conexión de Hola. Para más información, consulte [Connection timeout issue with .NET Framework 4.6.1 – TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/) (Problema de tiempo de espera de conexión agotado con .NET Framework 4.6.1: TransparentNetworkIPResolution).   

   
Cuando se crea un usuario de base de datos, ese usuario recibe hello **conectar** permiso y se puede conectar la base de datos de toothat como miembro del programa Hola a **público** rol. Hola inicialmente solo permisos de usuario de toohello disponibles son los permisos conceden toohello **público** rol o los permisos conceden tooany grupos de Windows que son miembros de. Una vez se aprovisiona un usuario de base de datos de contenido basados en AD Azure, puede conceder permisos adicionales del usuario de hello, Hola de igual forma en que se concede permiso tooany otro tipo de usuario. Normalmente conceder permisos toodatabase roles y agregar usuarios tooroles. Para obtener más información, consulte [Conceptos básicos de los permisos de los motores de las bases de datos](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx). Para obtener más información sobre los roles especiales de SQL Database, consulte [Administrar bases de datos e inicios de sesión en Azure SQL Database](sql-database-manage-logins.md).
Un usuario de dominio federado que se importa en un dominio de administrar, debe usar identidad de dominio de hello administrado.

> [!NOTE]
> Usuarios de Azure AD se marcan en los metadatos de la base de datos de hello con tipo E (EXTERNAL_USER) y para grupos con tipo X (EXTERNAL_GROUPS). Para obtener más información, consulte [sys.database_principals (Transact-SQL)](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>Conectar almacenamiento de base de datos o datos de usuario de toohello mediante SSMS o SSDT  
Administrador de hello Azure AD tooconfirm está configurado correctamente, conéctese toohello **maestro** base de datos mediante la cuenta de administrador de hello Azure AD.
tooprovision un usuario de base de datos de contenido basados en AD Azure (distinto de hello administrador del servidor que pertenece la base de datos de hello), conectar la base de datos de toohello con una identidad de Azure AD que tenga la base de datos de access toohello.

> [!IMPORTANT]
> La autenticación de Azure Active Directory es compatible con [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) y [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) en Visual Studio 2015. Hola versión de agosto de 2016 de SSMS también incluye compatibilidad para Universal autenticación de Active Directory, que permite a los administradores toorequire la autenticación multifactor usando una llamada de teléfono, mensaje de texto, las tarjetas inteligentes con pin o la notificación de aplicación móvil.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>Usar un tooconnect de identidad de Azure AD con SSMS o SSDT  

Hola procedimientos siguientes muestra cómo tooconnect tooa SQL de base de datos con una identidad de Azure AD mediante SQL Server Management Studio o las herramientas de base de datos de SQL Server.

### <a name="active-directory-integrated-authentication"></a>Autenticación integrada de Active Directory

Utilice este método si se registran en tooWindows con sus credenciales de Azure Active Directory de un dominio federado.

1. Inicie Management Studio o herramientas de datos y en hello **conectar tooServer** (o **conectar tooDatabase motor**) cuadro de diálogo hello **autenticación** , seleccione **Integrada en active Directory -**. Ninguna contraseña es necesaria o se puede especificar porque sus credenciales existentes se presentará para conexión de Hola.   

    ![Selección de autenticación integrada de Active Directory][11]
2. Haga clic en hello **opciones** botón y en hello **propiedades de conexión** página Hola **conectar toodatabase** cuadro, escriba un nombre Hola de base de datos de usuario de hello desea tooconnect Para. (hello **identificador de inquilino o el nombre de dominio de AD**"opción solo se admite para **Universal con conexión de MFA** las opciones, en caso contrario se atenúa.)  

    ![Seleccione el nombre de la base de datos de Hola][13]

## <a name="active-directory-password-authentication"></a>Autenticación de contraseña de Active Directory

Use este método cuando se conecta con un nombre de entidad de seguridad de Azure AD con hello Azure AD administra el dominio. También puede usar para una cuenta federada sin dominio toohello de acceso, por ejemplo, cuando trabajan de forma remota.

Utilice este método si se registran en tooWindows usando las credenciales de un dominio que no está federado con Azure, o cuando se usa la autenticación de Azure AD mediante Azure AD en función de saludo inicial u Hola dominio del cliente.

1. Inicie Management Studio o herramientas de datos y en hello **conectar tooServer** (o **conectar tooDatabase motor**) cuadro de diálogo hello **autenticación** , seleccione **Active Directory: contraseña**.
2. Hola **nombre de usuario** , escriba su nombre de usuario de Azure Active Directory en formato de hello  **username@domain.com** . Debe ser una cuenta de hello Azure Active Directory o una cuenta de un dominio federar con hello Azure Active Directory.
3. Hola **contraseña** cuadro, escriba la contraseña de usuario para la cuenta de Azure Active Directory de Hola o federado cuenta de dominio.

    ![Selección de autenticación de contraseña de Active Directory][12]
4. Haga clic en hello **opciones** botón y en hello **propiedades de conexión** página Hola **conectar toodatabase** cuadro, escriba un nombre Hola de base de datos de usuario de hello desea tooconnect Para. (Consulte el gráfico de hello en la opción anterior hello).

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>Usar un tooconnect de identidad de Azure AD desde una aplicación cliente

Hola procedimientos siguientes muestra cómo tooconnect tooa SQL de base de datos con una identidad de Azure AD desde una aplicación cliente.

###  <a name="active-directory-integrated-authentication"></a>Autenticación integrada de Active Directory

toouse la autenticación de Windows integrada, de Active Directory el dominio debe ser federado con Azure Active Directory. Debe estar ejecutándose la aplicación de cliente (o un servicio) conectar toohello base de datos en un equipo unido a un dominio con credenciales de dominio de un usuario.

tooconnect tooa base de datos mediante la autenticación y una identidad de Azure AD, palabra clave de autenticación de hello en la cadena de conexión de base de datos de hello debe establecerse tooActive Directory integrado. Hello siguiente ejemplo de código de C# utiliza ADO. NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

palabra clave de cadena de conexión de Hola ``Integrated Security=True`` no se admite para la conexión tooAzure base de datos SQL. Al realizar una conexión ODBC, necesitará tooremove espacios y establecer autenticación too'ActiveDirectoryIntegrated'.

### <a name="active-directory-password-authentication"></a>Autenticación de contraseña de Active Directory

tooconnect tooa base de datos mediante la autenticación y una identidad de Azure AD, palabra clave de autenticación de hello debe establecerse tooActive contraseña del directorio. cadena de conexión de Hello debe contener valores y palabras clave de contraseña/PWD y UID/Id. de usuario. Hello siguiente ejemplo de código de C# utiliza ADO. NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Obtener más información sobre los métodos de autenticación de Azure AD con ejemplos de código de demostración de hello disponibles en [demostración de GitHub de autenticación de Azure AD](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Token de Azure AD
Este método de autenticación permite servicios de nivel medio tooconnect tooAzure base de datos SQL o almacenamiento de datos de SQL Azure al obtener un token de Azure Active Directory (AAD). Permite escenarios sofisticados, incluida la autenticación basada en certificados. Debe completar los cuatro pasos básicos toouse Azure símbolo (token) de autenticación de AD:

1. Registrar la aplicación con Azure Active Directory y obtener el identificador de cliente de hello para el código. 
2. Cree una aplicación de Hola que representan de usuario de base de datos. (Completado anteriormente en el paso 6).
3. Cree un certificado en las ejecuciones de equipo de cliente hello aplicación hello.
4. Agregar certificado de hello como una clave para la aplicación.

Cadena de conexión de ejemplo:

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Para más información, consulte el [blog de seguridad de SQL Server](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).

### <a name="sqlcmd"></a>sqlcmd

Hola siguiendo las instrucciones, conéctese mediante versión 13.1 de sqlcmd, que está disponible en hello [centro de descarga de](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Pasos siguientes
- Para obtener información general de acceso y control en SQL Database, consulte [Control de acceso a Azure SQL Database](sql-database-control-access.md).
- Para obtener información general de los inicios de sesión, usuarios y roles de base de datos de SQL Database, consulte [Control y concesión de acceso a bases de datos](sql-database-manage-logins.md).
- Para más información acerca de las entidades de seguridad de bases de datos, consulte [Entidades de seguridad](https://msdn.microsoft.com/library/ms181127.aspx).
- Para más información acerca de los roles de base de datos, consulte [Roles de nivel de base de datos](https://msdn.microsoft.com/library/ms189121.aspx).
- Para más información general acerca de las reglas de firewall de SQL Database, consulte [Introducción a las reglas de firewall de Azure SQL Database](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

