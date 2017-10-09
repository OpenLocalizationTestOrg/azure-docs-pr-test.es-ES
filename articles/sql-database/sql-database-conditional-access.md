---
title: aaaConditional acceso - base de datos de SQL Azure y almacenamiento de datos | Documento de Microsoft
description: "Obtener información sobre el proceso tooconfigure de acceso condicional para la base de datos de SQL Azure y almacenamiento de datos."
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Acceso condicional (MFA) con Azure SQL Database y Data Warehouse  

Tanto SQL Database como SQL Data Warehouse admiten Acceso condicional de Microsoft. Hola siguientes pasos muestran cómo tooenforce de base de datos SQL de tooconfigure una directiva de acceso condicional.  

## <a name="prerequisites"></a>Requisitos previos  
- Debe configurar la autenticación de Azure Active Directory de toosupport de base de datos SQL o almacenamiento de datos SQL. Para ver pasos concretos, consulte [Configuración y administración de la autenticación de Azure Active Directory con SQL Database o SQL Data Warehouse](sql-database-aad-authentication-configure.md).  
- Cuando se habilita la autenticación multifactor, debe conectarse con en una herramienta admitida, como Hola de SSMS más recientes. Para más información, consulte [Configuración de Multi-Factor Authentication de Azure SQL Database para SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Configuración de la CA para Azure SQL DB/DW  
1.  Inicio de sesión toohello Portal, seleccione **Azure Active Directory**y, a continuación, seleccione **acceso condicional**. Para más información, consulte [Referencia técnica del acceso condicional de Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![Hoja Acceso condicional](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  Hola **directivas de acceso condicional** hoja, haga clic en **nueva directiva**, proporcione un nombre y, a continuación, haga clic en **configurar reglas de**.  
3.  En **asignaciones**, seleccione **usuarios y grupos**, comprobar **Seleccionar usuarios y grupos**y, a continuación, seleccione Hola usuario o grupo para el acceso condicional. Haga clic en **seleccione**y, a continuación, haga clic en **realiza** tooaccept la selección.  
  ![Seleccionar usuarios y grupos](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Seleccione **Aplicaciones en la nube** y haga clic en **Seleccionar aplicaciones**. Verá todas las aplicaciones disponibles para el acceso condicional. Seleccione **base de datos de SQL Azure**, en la parte inferior de hello, haga clic en **seleccione**y, a continuación, haga clic en **realiza**.  
  ![Seleccionar SQL Database](./media/sql-database-conditional-access/select-sql-database.png)  
  Si no se puede encontrar **base de datos de SQL Azure** aparece en la siguiente captura de pantalla de terceros de hello, completar Hola pasos:   
  - Inicie sesión en la instancia de Azure SQL DB/DW tooyour con SSMS con una cuenta de administrador AAD.  
  - Ejecute `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Inicie sesión en tooAAD y compruebe que base de datos de SQL Azure y almacenamiento de datos aparecen en las aplicaciones de hello en el AAD.  

5.  Seleccione **tener acceso a controles**, seleccione **Grant**y, a continuación, comprobar la directiva de hello desea tooapply. Para este ejemplo, se selecciona **Requerir autenticación multifactor**.  
  ![Seleccionar Conceder acceso](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Resumen  
aplicación Hola seleccionado (base de datos de SQL Azure) que permite tooconnect tooAzure SQL DB/DW con Azure AD Premium, ahora aplica la directiva de acceso condicional de hello seleccionado, **requiere la autenticación multifactor.**  
Si tiene preguntas sobre Azure SQL Database y Data Warehouse con respecto a la autenticación multifactor, póngase en contacto con MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Pasos siguientes  

Para ver un tutorial, consulte [Protección de Azure SQL Database](sql-database-security-tutorial.md).
