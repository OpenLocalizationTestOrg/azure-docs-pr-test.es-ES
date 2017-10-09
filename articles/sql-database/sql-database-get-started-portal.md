---
title: "Azure Portal: Creación de una base de datos SQL | Microsoft Docs"
description: "Obtenga información acerca de cómo toocreate un servidor lógico de la base de datos SQL, regla de firewall de nivel de servidor y bases de datos de Hola portal de Azure. Aprenderá también tooquery una base de datos de SQL Azure mediante Hola portal de Azure."
keywords: "tutorial de sql database, creación de una base de datos sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: d30352d834f2007e0b6b3eabfc3c108c61479b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-database-in-hello-azure-portal"></a>Crear una base de datos de SQL Azure en hello portal de Azure

Este tutorial de inicio rápido le guía a través de la base de datos toocreate una instancia de SQL en Azure. La base de datos de SQL Azure es una "base de datos-as-a-Service" oferta que le permite toorun y escala alta disponibilidad SQL Server las bases de datos en la nube de Hola. Este inicio rápido muestra cómo tooget iniciado mediante la creación de una base de datos SQL Hola portal de Azure.

Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="log-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure

Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

## <a name="create-a-sql-database"></a>Creación de una base de datos SQL

Se crea una instancia de Azure SQL Database con un conjunto definido de [recursos de proceso y almacenamiento](sql-database-service-tiers.md). base de datos de Hola se crea dentro de un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) y en un [servidor lógico de base de datos de SQL Azure](sql-database-features.md). 

Siga estos pasos toocreate una base de datos SQL que contiene datos de ejemplo de Hola LT de Adventure Works. 

1. Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.

2. Seleccione **bases de datos** de hello **New** página y seleccione **base de datos SQL** de hello **bases de datos** página.

   ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. Rellenar formulario de la base de datos SQL de Hola con hello después de obtener información, tal como se muestra en hello anterior imagen:   

   | Configuración       | Valor sugerido | Descripción | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre de la base de datos** | mySampleDatabase | Para conocer los nombres de base de datos válidos, consulte [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificadores de base de datos). | 
   | **Suscripción** | Su suscripción  | Para más información acerca de sus suscripciones, consulte [Suscripciones](https://account.windowsazure.com/Subscriptions). |
   | **Grupos de recursos**  | myResourceGroup | Para conocer cuáles son los nombres de grupo de recursos válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura). |
   | **Seleccionar origen** | Ejemplo (AdventureWorksLT) | Carga Hola AdventureWorksLT esquema y los datos en la base de datos |

   > [!IMPORTANT]
   > Debe seleccionar la base de datos de ejemplo de Hola en este formulario porque se utiliza en el resto de Hola de esta guía de inicio rápido.
   > 

4. En **Server**, haga clic en **establecer configuración obligatoria** y rellene Hola formato SQL server (servidor lógico) con hello después de obtener información, tal como se muestra en hello después de imagen:   

   | Configuración       | Valor sugerido | Descripción | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Cualquier nombre globalmente único | Para conocer cuáles son los nombres de servidor válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura). | 
   | **Inicio de sesión del administrador del servidor** | Cualquier nombre válido | Para conocer los nombres de inicio de sesión válidos, consulte [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificadores de base de datos). |
   | **Password** | Cualquier contraseña válida | La contraseña debe tener al menos 8 caracteres y debe contener caracteres de tres de las siguientes categorías de hello: caracteres en mayúsculas, caracteres en minúsculas, números y caracteres no alfanuméricos y guiones. |
   | **Suscripción** | Su suscripción | Para más información acerca de sus suscripciones, consulte [Suscripciones](https://account.windowsazure.com/Subscriptions). |
   | **Grupos de recursos** | myResourceGroup | Para conocer cuáles son los nombres de grupo de recursos válidos, consulte el artículo [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Convenciones de nomenclatura). |
   | **Ubicación** | Cualquier ubicación válida | Para obtener información acerca de las regiones, consulte [Regiones de Azure](https://azure.microsoft.com/regions/). |

   > [!IMPORTANT]
   > inicio de sesión de administrador de servidor de Hola y la contraseña que especifique aquí son necesario toolog en toohello server y sus bases de datos más adelante en esta guía de inicio rápido. Recuerde o grabe esta información para su uso posterior. 
   >  

   ![create database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. Cuando se haya completado el formulario de hello, haga clic en **seleccione**.

6. Haga clic en **tarifa** toospecify Hola nivel y rendimiento de nivel de servicio para la nueva base de datos. Usar Hola control deslizante tooselect **20 Dtu** y **250** GB de almacenamiento. Para más información acerca de las DTU, consulte [¿Qué es una DTU?](sql-database-what-is-a-dtu.md).

   ![create database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. Después de la cantidad de hello seleccionado de Dtu, haga clic en **aplicar**.  

8. Ahora que ha completado el formulario de la base de datos SQL de hello, haga clic en **crear** base de datos de tooprovision Hola. El aprovisionamiento tarda unos minutos. 

9. En la barra de herramientas de hello, haga clic en **notificaciones** toomonitor proceso de implementación de Hola.

   ![notificación](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Crear una regla de firewall de nivel de servidor

Hola servicio de base de datos SQL crea un firewall en hello-nivel de servidor que impide que las aplicaciones externas y las herramientas de conectar toohello server o las bases de datos en el servidor de Hola a menos que se crea una regla de firewall tooopen firewall de Hola para direcciones IP concretas. Siga estos pasos toocreate una [regla de firewall de nivel de servidor de base de datos SQL](sql-database-firewall-configure.md) para direcciones IP de su cliente y habilitar la conectividad externa a través de firewall de base de datos SQL de Hola para sólo la dirección IP. 

> [!NOTE]
> SQL Database se comunica a través del puerto 1433. Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 1433. Si es así, no se puede conectar el servidor de base de datos de SQL Azure tooyour a menos que el departamento de TI abre el puerto 1433.
>

1. Una vez finalizada la implementación de hello, haga clic en **bases de datos SQL** del menú izquierdo de hello y, a continuación, haga clic en **mySampleDatabase** en hello **bases de datos SQL** página. página de información general para abrir el base de datos, que muestra que Hola totalmente Hello calificado nombre del servidor (como **mynewserver20170313.database.windows.net**) y proporciona opciones para otra configuración. Copie dicho nombre, ya que lo tendrá que usar más adelante,

   > [!IMPORTANT]
   > Necesitará este servidor de tooyour de tooconnect de nombre completo del servidor y sus bases de datos en las siguientes guías de inicio rápidos.
   > 

   ![nombre del servidor](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Haga clic en **Configurar firewall de servidor** de barra de herramientas de hello tal y como se muestra en la imagen anterior de Hola. Hola **configuración del Firewall** se abre la página servidor de base de datos de SQL de Hola. 

   ![regla de firewall del servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. Haga clic en **agregar dirección IP del cliente** en tooadd de barra de herramientas de hello tooa nueva regla de firewall de direcciones de la IP actual. La regla de firewall puede abrir el puerto 1433 para una única dirección IP o un intervalo de direcciones IP.

4. Haga clic en **Guardar**. Se crea una regla de firewall de nivel de servidor para la dirección IP actual abrir el puerto 1433 en el servidor lógico Hola.

   ![establecer regla de firewall del servidor](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Haga clic en **Aceptar** y, a continuación, cierre hello **configuración del Firewall** página.

Ahora puede conectarse toohello servidor de base de datos SQL y sus bases de datos mediante SQL Server Management Studio u otra herramienta de su elección de esta dirección IP con cuenta de administrador de servidor hello creado anteriormente.

> [!IMPORTANT]
> De forma predeterminada, el acceso a través de firewall de base de datos SQL de hello está habilitado para todos los servicios de Azure. Haga clic en **OFF** en este toodisable de página para todos los servicios de Azure.
>

## <a name="query-hello-sql-database"></a>Base de datos SQL de Hola de consulta

Ahora que ha creado una base de datos de ejemplo en Azure, vamos a usar la herramienta de consulta integrada Hola Hola tooconfirm portal Azure que puede conectarse toohello base de datos y consultar datos de Hola. 

1. En la página de base de datos SQL de hello para la base de datos, haga clic en **herramientas** en la barra de herramientas de Hola. Hola **herramientas** se abre la página.

   ![menú herramientas](./media/sql-database-get-started-portal/tools-menu.png) 

2. Haga clic en **editor de consultas (versión preliminar)**, haga clic en hello **obtener una vista previa de los términos** casilla de verificación y, a continuación, haga clic en **Aceptar**. se abre la página del editor de consultas de Hola.

3. Haga clic en **inicio de sesión** y, a continuación, cuando se le pida, seleccione **autenticación de SQL server** y, a continuación, proporcione el inicio de sesión de hello server admin y la contraseña que creó anteriormente.

   ![login](./media/sql-database-get-started-portal/login.png) 

4. Haga clic en **Aceptar** toolog en.

5. Después de autenticarse, escriba Hola después de consulta en el panel del editor de consultas de Hola.

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. Haga clic en **ejecutar** y, a continuación, revisar los resultados de la consulta de Hola Hola **resultados** panel.

   ![resultados del editor de consultas](./media/sql-database-get-started-portal/query-editor-results.png)

7. Hola cerrar **editor de consultas** hello y página **herramientas** página.

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no necesita estos recursos para otro/tutorial de inicio rápido (vea [pasos siguientes](#next-steps)), puede eliminarlas haciendo Hola siguiente:


1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en **myResourceGroup**. 
2. En la página del grupo de recursos, haga clic en **eliminar**, tipo **myResourceGroup** en Hola cuadro de texto y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene una base de datos, puede conectarse y realizar consultas con las herramientas que desee. Para más información, seleccione una de las herramientas siguientes:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [código de Visual Studio](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)
