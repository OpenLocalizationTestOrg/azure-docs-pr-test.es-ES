---
title: "aaaConfigure la autenticación multifactor - SQL de Azure | Documentos de Microsoft"
description: Use Multi-Factor Authentication con SSMS para SQL Database y SQL Data Warehouse.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>Configuración de la autenticación multifactor para SQL Server Management Studio y Azure AD

Este tema muestra cómo toouse Azure Active Directory la autenticación multifactor (MFA) con SQL Server Management Studio. MFA de Azure AD puede usarse cuando se conecta SSMS o SqlPackage.exe tooAzure base de datos SQL y almacenamiento de datos de SQL Azure.

Para obtener información general de la autenticación multifactor de Azure SQL Database, vea [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Pasos de configuración

1. **Configurar Azure Active Directory** : para obtener más información, consulte [administrar su directorio Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [integrar las identidades locales con Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Agregar su propios tooAzure de nombre de dominio AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure ahora admite la federación con Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), y [administrar Azure AD mediante Windows PowerShell ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **Configurar MFA**: para obtener instrucciones detalladas, consulte [¿Qué es Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md), [Acceso condicional (MFA) con Azure SQL Database y Data Warehouse](sql-database-conditional-access.md). (El acceso condicional completo requiere una versión Premium de Azure Active Directory (Azure AD). MFA limitado está disponible con la versión estándar de Azure AD).
3. **Configurar la base de datos SQL o almacenamiento de datos de SQL para la autenticación de Azure AD** : para obtener instrucciones detalladas, consulte [tooSQL de conexión base de datos o SQL datos almacenamiento mediante Azure Active Directory autenticación](sql-database-aad-authentication.md).
4. **Descargar SSMS** : en el equipo de cliente hello, descargar Hola de SSMS más recientes, de [descargar SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Para todas las características de hello en este tema, utilice al menos de 2017 de julio, versión 17,2.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>Conexión mediante autenticación universal con SSMS

Hola siguientes pasos muestra cómo tooconnect tooSQL base de datos o almacenamiento de datos de SQL mediante el uso de Hola de SSMS más recientes.

1. tooconnect usando la autenticación Universal, en hello **conectar tooServer** cuadro de diálogo, seleccione **Active Directory - Universal con la compatibilidad con MFA**. (Si ve **Universal autenticación de Active Directory** no está en la versión más reciente de Hola de SSMS.)  
   ![1mfa-universal-connect][1]  
2. Hola completa **nombre de usuario** cuadro con las credenciales de Azure Active Directory de hello, en formato de hello `user_name@domain.com`.  
   ![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. Si va a conectar como un usuario invitado, debe hacer clic en **opciones**y en hello **propiedad de conexión** cuadro de diálogo, Hola completa **identificador de inquilino o el nombre de dominio de AD** cuadro. Para más información, consulte [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)](sql-database-ssms-mfa-authentication.md).
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. Como de costumbre para base de datos SQL y almacenamiento de datos de SQL, debe hacer clic **opciones** y especifique la base de datos de hello en hello **opciones** cuadro de diálogo. (Si Hola conectado el usuario es un usuario invitado (es decir, joe@outlook.com), debe casilla hello y agregar el identificador de inquilino o el nombre de dominio de hello actual de AD como parte de las opciones. Consulte [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)]()(sql-database-ssms-mfa-authentication.md. Haga clic en **Conectar**.  
5. Cuando Hola **iniciar sesión en la cuenta de tooyour** aparece el cuadro de diálogo, proporcione la cuenta de hello y la contraseña de su identidad de Azure Active Directory. Si un usuario pertenece a un dominio federado con Azure AD, no se requiere contraseña.  
   ![2mfa-sign-in][2]  

   > [!NOTE]
   > Para Autenticación universal con una cuenta que no requiere MFA, conéctese en este momento. Para los usuarios que necesitan MFA, continúe con hello pasos:
   >  
   
6. Pueden aparecer dos cuadros de diálogo de configuración de MFA. Una vez operación depende de configuración de administrador MFA de hello y, por tanto, puede ser opcional. Este paso para un dominio de MFA habilitado a veces es predefinido (por ejemplo, dominio Hola requiere toouse a los usuarios una tarjeta inteligente y pin).  
   ![3mfa-setup][3]  
7. Hola posible segundo cuadro de diálogo le permite obtener información detallada de tooselect Hola del método de autenticación de una vez. las opciones posibles de Hello están configuradas por el administrador.  
   ![4mfa-verify-1][4]  
8. Hello Azure Active Directory envía Hola confirmar tooyou de información. Cuando se recibe el código de comprobación de hello, escribirlo en hello **introduzca el código de comprobación** cuadro y haga clic en **iniciar sesión en**.  
   ![5mfa-verify-2][5]  

Cuando se complete la comprobación, SSMS se conectará de manera habitual, siempre que haya acceso de firewall y credenciales válidas.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información general de la autenticación multifactor de Azure SQL Database, consulte [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)](sql-database-ssms-mfa-authentication.md).
* Conceda otros usuarios tienen acceso a la base de datos de tooyour: [autorización y autenticación de base de datos de SQL: conceder acceso](sql-database-manage-logins.md)  
Asegúrese de que otros usuarios pueden conectarse a través de firewall de hello: [regla de firewall de configurar un nivel de servidor de base de datos de SQL Azure mediante Hola portal de Azure](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

