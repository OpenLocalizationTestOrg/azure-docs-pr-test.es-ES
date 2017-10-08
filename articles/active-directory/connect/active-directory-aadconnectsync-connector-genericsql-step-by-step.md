---
title: aaaGeneric conector de SQL paso a paso | Documentos de Microsoft
description: "En este artículo es recorrer a través de un sistema de recursos humanos simple utilizando paso a paso Hola conector de SQL genérico."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>Conector de SQL genérico paso a paso
Este tema es una guía paso a paso. Crea una sencilla base de datos de ejemplo de Recursos Humanos y la usa para importar algunos usuarios y su pertenencia a grupos.

## <a name="prepare-hello-sample-database"></a>Preparar la base de datos de ejemplo de Hola
En un servidor que ejecuta SQL Server, ejecute el script SQL de Hola se encuentra en [Apéndice A](#appendix-a). Este script crea una base de datos de ejemplo con el nombre de hello GSQLDEMO. modelo de objetos de Hola para hello crea base de datos parece esta imagen:  
![Modelo de objetos](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

Crear un usuario de base de datos de toouse tooconnect toohello. En este tutorial, se denomina FABRIKAM\SQLUser usuario Hola y se encuentra en dominio Hola.

## <a name="create-hello-odbc-connection-file"></a>Crear archivo de conexión de ODBC Hola
Hola genérico conector de SQL está usando el servidor remoto de ODBC tooconnect toohello. Primero necesitamos toocreate un archivo con hello información de conexión de ODBC.

1. Iniciar la utilidad de administración de ODBC hello en el servidor:  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. Pestaña Hola seleccione **DSN de archivo**. Haga clic en **Agregar...**.  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. Hello out-of-box controlador funciona bien, por lo que selecciónelo y haga clic en **siguiente >**.  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. Asigne un nombre, como de archivo hello **GenericSQL**.  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. Haga clic en **Finalizar**.  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. Conexión en tiempo de tooconfigure Hola. Proporcionar una buena descripción de origen de datos de Hola y proporcione Hola nombre del servidor de Hola que ejecuta SQL Server.  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. Seleccione cómo tooauthenticate con SQL. En este caso, usaremos Autenticación de Windows.  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Proporcione Hola nombre de base de datos de ejemplo de Hola **GSQLDEMO**.  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. Mantenga las opciones predeterminadas de esta pantalla. Haga clic en **Finalizar**.  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. tooverify que todo funciona según lo esperado, haga clic en **origen de datos de prueba**.  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Asegúrese de que la prueba de hello es correcta.  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. archivo de configuración de ODBC de Hello ahora debe estar visible en el DSN de archivo.  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

Ahora tenemos archivos de Hola se necesita y puede empezar a crear Hola conector.

## <a name="create-hello-generic-sql-connector"></a>Crear hello conector de SQL genérico
1. Hola UI Synchronization Service Manager, seleccione **conectores** y **crear**. Seleccione **SQL genérico (Microsoft)** y asígnele un nombre descriptivo.  
   ![Conector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Buscar archivo DSN de hello que creó en la sección anterior de Hola y cargarlo toohello server. Proporcionar la base de datos de hello credenciales tooconnect toohello.  
   ![Conector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. En este tutorial, hemos optado por una opción sencilla y hemos tenido en cuenta que hay dos tipos de objetos, **User** y **Group**.
   ![Conector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. atributos de hello toofind, queremos Hola conector toodetect esos atributos examinando la propia tabla de Hola. Puesto que **usuarios** es una palabra reservada en SQL, necesitamos tooprovide en cuadrado corchetes [].  
   ![Conector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. Atributo de delimitador de tiempo toodefine hello y atributo DN de Hola. Para **usuarios**, usamos la combinación de Hola de nombre de usuario de hello dos atributos y EmployeeID. Para **Group**, usamos GroupName (aunque no sea muy realista para la vida real, para este tutorial funciona).
   ![Conector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. No todos los tipos de atributo se pueden detectar en una base de datos SQL, tipo de atributo de referencia de Hello en particular no puede. Para tipo de objeto de grupo de hello, necesitamos toochange Hola OwnerID y MemberID tooreference.  
   ![Conector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. atributos de Hello seleccionamos como atributos de referencia en el paso anterior de hello requieren estos valores son una referencia al tipo de objeto de Hola. En nuestro caso, Hola tipo de objeto de usuario.  
   ![Conector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. En la página de parámetros globales de hello, seleccione **marca de agua** como estrategia de hello delta. Escribir en formato de fecha y hora de hello **aaaa-MM-dd hh**.
   ![Conector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. En hello **configurar particiones y jerarquías** , seleccione ambos tipos de objeto.
   ![Conector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. En hello **seleccionar tipos de objeto** y **seleccionar los atributos**, seleccione los tipos de objeto y todos los atributos. En hello **configurar delimitadores** página, haga clic en **finalizar**.

## <a name="create-run-profiles"></a>Creación de perfiles de ejecución
1. Hola UI Synchronization Service Manager, seleccione **conectores**, y **configurar perfiles de ejecución**. Haga clic en **New Profile**(Nuevo perfil). Comenzaremos por **Full Import**(Importación completa).  
   ![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Seleccione el tipo de hello **importación completa (solo etapa)**.  
   ![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Seleccione la partición de hello **objeto = usuario**.  
   ![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. Seleccione **Table** (Tabla) y escriba **[USERS]**. Desplácese hacia abajo de la sección de tipo de objeto con varios valores de toohello y escriba datos Hola Hola después de la imagen. Seleccione **finalizar** paso de hello toosave.  
   ![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. Seleccione **New step**(Nuevo paso). Esta vez, seleccione **OBJECT=Group**. En la última página de hello, utilice la configuración de hello en hello después de la imagen. Haga clic en **Finalizar**  
   ![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. Opcional: si lo desea, puede configurar perfiles de ejecución adicionales. En este tutorial, se usa solo Hola importación completa.
7. Haga clic en **Aceptar** toofinish cambiar perfiles de ejecución.

## <a name="add-some-test-data-and-test-hello-import"></a>Agregue algunos importación de Hola de datos y de prueba de prueba
Rellene algunos datos de prueba en la base de datos de ejemplo. Cuando haya terminado, seleccione **Run** (Ejecutar) y **Full import** (Importación completa).

Este usuario tiene dos números de teléfono y un grupo con algunos miembros.  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>Apéndice A
**Base de datos de ejemplo de Hola de toocreate SQL script**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
