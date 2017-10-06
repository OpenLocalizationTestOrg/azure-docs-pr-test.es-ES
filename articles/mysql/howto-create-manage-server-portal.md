---
title: aaaCreate y administrar la base de datos de Azure para servidor de MySQL mediante el portal de Azure | Documentos de Microsoft
description: "Este artículo describe cómo puede crear una nueva base de datos de Azure para MySQL server y administrar el servidor de hello mediante Hola Portal de Azure rápidamente."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a>Creación y administración de un servidor de Azure Database for MySQL con Azure Portal
Este artículo describe cómo puede crear una nueva base de datos de Azure para MySQL server y administrar el servidor de hello mediante Hola Portal de Azure rápidamente. Administración de servidor incluye ver bases de datos y los detalles del servidor, restablecimiento de contraseña y eliminar servidor hello.

## <a name="log-in-toohello-azure-portal"></a>Inicie sesión en toohello portal de Azure
Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

## <a name="create-an-azure-database-for-mysql-server"></a>Creación de un servidor de Azure Database for MySQL
Siga estos toocreate pasos una base de datos de MySQL server denominado "mysqlserver4demo"

1-clic **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.

2-seleccione **bases de datos** en nueva página de Hola y seleccione **base de datos de Azure para MySQL** desde la página de bases de datos de Hola.

> Se crea un servidor de Azure Database for MySQL con un conjunto definido de [recursos de proceso y almacenamiento](./concepts-compute-unit-and-storage.md). base de datos de Hola se crea dentro de un grupo de recursos de Azure y en una base de datos de Azure para servidor MySQL.

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

3 - rellene Hola base de datos de Azure para el formulario de MySQL con hello siguiente información:

| **Campo del formulario** | **Descripción del campo** |
|----------------|-----------------------|
| *Nombre del servidor* | azure-mysql (el nombre del servidor es único globalmente) |
| *Suscripción* | MySQLaaS (seleccione en la lista desplegable) |
| *Grupos de recursos* | myresource (cree un nuevo grupo de recursos o use uno existente) |
| *Inicio de sesión del administrador del servidor* | myadmin (dé un nombre a la cuenta de administrador) |
| *Password* | indique la contraseña de la cuenta de administrador |
| *Confirmar contraseña* | confirme la contraseña de la cuenta de administrador |
| *Ubicación* | Europa del Norte (seleccione entre Europa del Norte y Oeste de EE. UU.) |
| *Versión* | 5.6 (elija la versión de Azure Database for MySQL) |

4-Haga clic en **tarifa** toospecify Hola nivel y rendimiento de nivel de servicio para el nuevo servidor. Las unidades de proceso se pueden configurar entre 50 y 100 en el nivel básico o entre 100 y 200 en el nivel estándar, y se puede agregar almacenamiento en función de la cantidad incluida. En esta guía, vamos a seleccionar 50 unidades de proceso y 50 GB. Haga clic en **Aceptar** toosave la selección.
![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)

5-haga clic en **crear** servidor de hello tooprovision. El aprovisionamiento tarda unos minutos.

> Comprobar hello **toodashboard Pin** opción tooallow fácil realizar un seguimiento de las implementaciones.
> [!NOTE]
> Aunque too1000GB de nivel básico y 10000GB en estándar se admitirán nivel para el almacenamiento, versión preliminar pública, de almacenamiento máximo hello es too1000GB estando limitada temporalmente. 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a>Actualización de un servidor de Azure Database for MySQL
Después de aprovisiona el nuevo servidor, usuario tiene 2 tooedit de opciones de un servidor existente: restablecer la contraseña de administrador o escala arriba/abajo servidor hello cambiando Hola unidades de proceso.

### <a name="change-hello-administrator-user-password"></a>Cambiar contraseña de usuario de administrador de Hola
1 - en el servidor de hello **Introducción** hoja, haga clic en **de restablecimiento de contraseña** toopopulate una ventana de entrada y la confirmación de contraseña.

2: escriba la nueva contraseña y Confirmar contraseña hello en ventana hello como sigue: ![restablecimiento de contraseña](./media/howto-create-manage-server-portal/reset-password.png)

3-haga clic en **Aceptar** nueva contraseña de toosave Hola.

### <a name="scale-updown-by-changing-compute-units"></a>Escalar o reducir verticalmente cambiando las unidades de proceso

1 - en la hoja de servidor hello, en **configuración**, haga clic en **tarifa** hoja de nivel de precios tooopen Hola para hello base de datos de MySQL server.

2-siga los pasos 4 en **crear una base de datos de MySQL server** toochange proceso unidades en Hola mismo nivel de precios.

## <a name="delete-an-azure-database-for-mysql-server"></a>Eliminación de un servidor de Azure Database for MySQL

1 - en el servidor de hello **Introducción** hoja, haga clic en **eliminar** hoja de confirmación de eliminación de comando botón tooopen Hola.

Nombre del servidor correcto Hola de tipo 2 en el cuadro de entrada de hoja de hello confirmación dobles.

3-haga clic en **eliminar** nuevamente en el botón tooconfirm Eliminar acción y espere emergente "Eliminar correcto" en la barra de notificación de Hola.

## <a name="list-hello-azure-database-for-mysql-databases"></a>Hola de lista base de datos de Azure para las bases de datos de MySQL
En el servidor de hello **Introducción** hoja, desplácese hacia abajo hasta que vea base de datos de Hola icono en la parte inferior de Hola. Todas las bases de datos de Hola se mostrarán en la tabla de Hola. Haga clic en **eliminar** hoja de confirmación de eliminación de comando botón tooopen Hola.

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a>Presentación de los detalles de un servidor de Azure Database for MySQL
Haga clic en **propiedades** en **configuración** en servidor hello hoja abrirá hello **propiedades** hoja. A continuación, puede ver toda la información detallada sobre el servidor de Hola.

## <a name="next-steps"></a>Pasos siguientes

[Inicio rápido: Creación de un servidor de Azure Database for MySQL con Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md)
