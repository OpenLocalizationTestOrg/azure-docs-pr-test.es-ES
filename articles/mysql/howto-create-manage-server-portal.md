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
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="4958f-103">Creación y administración de un servidor de Azure Database for MySQL con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4958f-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="4958f-104">Este artículo describe cómo puede crear una nueva base de datos de Azure para MySQL server y administrar el servidor de hello mediante Hola Portal de Azure rápidamente.</span><span class="sxs-lookup"><span data-stu-id="4958f-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="4958f-105">Administración de servidor incluye ver bases de datos y los detalles del servidor, restablecimiento de contraseña y eliminar servidor hello.</span><span class="sxs-lookup"><span data-stu-id="4958f-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="4958f-106">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4958f-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="4958f-107">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4958f-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="4958f-108">Creación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="4958f-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="4958f-109">Siga estos toocreate pasos una base de datos de MySQL server denominado "mysqlserver4demo"</span><span class="sxs-lookup"><span data-stu-id="4958f-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="4958f-110">1-clic **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4958f-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="4958f-111">2-seleccione **bases de datos** en nueva página de Hola y seleccione **base de datos de Azure para MySQL** desde la página de bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4958f-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="4958f-112">Se crea un servidor de Azure Database for MySQL con un conjunto definido de [recursos de proceso y almacenamiento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4958f-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="4958f-113">base de datos de Hola se crea dentro de un grupo de recursos de Azure y en una base de datos de Azure para servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="4958f-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="4958f-115">3 - rellene Hola base de datos de Azure para el formulario de MySQL con hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4958f-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="4958f-116">**Campo del formulario**</span><span class="sxs-lookup"><span data-stu-id="4958f-116">**Form Field**</span></span> | <span data-ttu-id="4958f-117">**Descripción del campo**</span><span class="sxs-lookup"><span data-stu-id="4958f-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="4958f-118">*Nombre del servidor*</span><span class="sxs-lookup"><span data-stu-id="4958f-118">*Server name*</span></span> | <span data-ttu-id="4958f-119">azure-mysql (el nombre del servidor es único globalmente)</span><span class="sxs-lookup"><span data-stu-id="4958f-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="4958f-120">*Suscripción*</span><span class="sxs-lookup"><span data-stu-id="4958f-120">*Subscription*</span></span> | <span data-ttu-id="4958f-121">MySQLaaS (seleccione en la lista desplegable)</span><span class="sxs-lookup"><span data-stu-id="4958f-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="4958f-122">*Grupos de recursos*</span><span class="sxs-lookup"><span data-stu-id="4958f-122">*Resource group*</span></span> | <span data-ttu-id="4958f-123">myresource (cree un nuevo grupo de recursos o use uno existente)</span><span class="sxs-lookup"><span data-stu-id="4958f-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="4958f-124">*Inicio de sesión del administrador del servidor*</span><span class="sxs-lookup"><span data-stu-id="4958f-124">*Server admin login*</span></span> | <span data-ttu-id="4958f-125">myadmin (dé un nombre a la cuenta de administrador)</span><span class="sxs-lookup"><span data-stu-id="4958f-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="4958f-126">*Password*</span><span class="sxs-lookup"><span data-stu-id="4958f-126">*Password*</span></span> | <span data-ttu-id="4958f-127">indique la contraseña de la cuenta de administrador</span><span class="sxs-lookup"><span data-stu-id="4958f-127">setup admin account password</span></span> |
| <span data-ttu-id="4958f-128">*Confirmar contraseña*</span><span class="sxs-lookup"><span data-stu-id="4958f-128">*Confirm password*</span></span> | <span data-ttu-id="4958f-129">confirme la contraseña de la cuenta de administrador</span><span class="sxs-lookup"><span data-stu-id="4958f-129">confirm admin account password</span></span> |
| <span data-ttu-id="4958f-130">*Ubicación*</span><span class="sxs-lookup"><span data-stu-id="4958f-130">*Location*</span></span> | <span data-ttu-id="4958f-131">Europa del Norte (seleccione entre Europa del Norte y Oeste de EE. UU.)</span><span class="sxs-lookup"><span data-stu-id="4958f-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="4958f-132">*Versión*</span><span class="sxs-lookup"><span data-stu-id="4958f-132">*Version*</span></span> | <span data-ttu-id="4958f-133">5.6 (elija la versión de Azure Database for MySQL)</span><span class="sxs-lookup"><span data-stu-id="4958f-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="4958f-134">4-Haga clic en **tarifa** toospecify Hola nivel y rendimiento de nivel de servicio para el nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="4958f-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="4958f-135">Las unidades de proceso se pueden configurar entre 50 y 100 en el nivel básico o entre 100 y 200 en el nivel estándar, y se puede agregar almacenamiento en función de la cantidad incluida.</span><span class="sxs-lookup"><span data-stu-id="4958f-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="4958f-136">En esta guía, vamos a seleccionar 50 unidades de proceso y 50 GB.</span><span class="sxs-lookup"><span data-stu-id="4958f-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="4958f-137">Haga clic en **Aceptar** toosave la selección.</span><span class="sxs-lookup"><span data-stu-id="4958f-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="4958f-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="4958f-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="4958f-139">5-haga clic en **crear** servidor de hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="4958f-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="4958f-140">El aprovisionamiento tarda unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4958f-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="4958f-141">Comprobar hello **toodashboard Pin** opción tooallow fácil realizar un seguimiento de las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="4958f-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="4958f-142">Aunque too1000GB de nivel básico y 10000GB en estándar se admitirán nivel para el almacenamiento, versión preliminar pública, de almacenamiento máximo hello es too1000GB estando limitada temporalmente.</span><span class="sxs-lookup"><span data-stu-id="4958f-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="4958f-143">Actualización de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="4958f-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="4958f-144">Después de aprovisiona el nuevo servidor, usuario tiene 2 tooedit de opciones de un servidor existente: restablecer la contraseña de administrador o escala arriba/abajo servidor hello cambiando Hola unidades de proceso.</span><span class="sxs-lookup"><span data-stu-id="4958f-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="4958f-145">Cambiar contraseña de usuario de administrador de Hola</span><span class="sxs-lookup"><span data-stu-id="4958f-145">Change hello administrator user password</span></span>
<span data-ttu-id="4958f-146">1 - en el servidor de hello **Introducción** hoja, haga clic en **de restablecimiento de contraseña** toopopulate una ventana de entrada y la confirmación de contraseña.</span><span class="sxs-lookup"><span data-stu-id="4958f-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="4958f-147">2: escriba la nueva contraseña y Confirmar contraseña hello en ventana hello como sigue: ![restablecimiento de contraseña](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="4958f-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="4958f-148">3-haga clic en **Aceptar** nueva contraseña de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="4958f-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="4958f-149">Escalar o reducir verticalmente cambiando las unidades de proceso</span><span class="sxs-lookup"><span data-stu-id="4958f-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="4958f-150">1 - en la hoja de servidor hello, en **configuración**, haga clic en **tarifa** hoja de nivel de precios tooopen Hola para hello base de datos de MySQL server.</span><span class="sxs-lookup"><span data-stu-id="4958f-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="4958f-151">2-siga los pasos 4 en **crear una base de datos de MySQL server** toochange proceso unidades en Hola mismo nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="4958f-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="4958f-152">Eliminación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="4958f-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="4958f-153">1 - en el servidor de hello **Introducción** hoja, haga clic en **eliminar** hoja de confirmación de eliminación de comando botón tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="4958f-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="4958f-154">Nombre del servidor correcto Hola de tipo 2 en el cuadro de entrada de hoja de hello confirmación dobles.</span><span class="sxs-lookup"><span data-stu-id="4958f-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="4958f-155">3-haga clic en **eliminar** nuevamente en el botón tooconfirm Eliminar acción y espere emergente "Eliminar correcto" en la barra de notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4958f-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="4958f-156">Hola de lista base de datos de Azure para las bases de datos de MySQL</span><span class="sxs-lookup"><span data-stu-id="4958f-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="4958f-157">En el servidor de hello **Introducción** hoja, desplácese hacia abajo hasta que vea base de datos de Hola icono en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="4958f-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="4958f-158">Todas las bases de datos de Hola se mostrarán en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="4958f-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="4958f-159">Haga clic en **eliminar** hoja de confirmación de eliminación de comando botón tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="4958f-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="4958f-161">Presentación de los detalles de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="4958f-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="4958f-162">Haga clic en **propiedades** en **configuración** en servidor hello hoja abrirá hello **propiedades** hoja.</span><span class="sxs-lookup"><span data-stu-id="4958f-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="4958f-163">A continuación, puede ver toda la información detallada sobre el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4958f-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4958f-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4958f-164">Next steps</span></span>

[<span data-ttu-id="4958f-165">Inicio rápido: Creación de un servidor de Azure Database for MySQL con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4958f-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
