---
title: "Administración de datos personales en Microsoft Azure | Microsoft Docs"
description: "Guía sobre cómo corregir, actualizar, eliminar y exportar datos personales en Azure Active Directory y Azure SQL Database"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: b04c745feb710d3d1d8a1fce23807168d6e6fa3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="0d396-103">Administración de datos personales en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0d396-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="0d396-104">En este artículo se ofrece una guía sobre cómo corregir, actualizar, eliminar y exportar datos personales en Azure Active Directory y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0d396-104">This article provides guidance on how to correct, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="0d396-105">Escenario</span><span class="sxs-lookup"><span data-stu-id="0d396-105">Scenario</span></span>

<span data-ttu-id="0d396-106">Una empresa de Dublín ofrece una plataforma de venta centralizada para bodas con destinos exclusivos en Irlanda y en todo el mundo orientada a una cartera de clientes local e internacional.</span><span class="sxs-lookup"><span data-stu-id="0d396-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around the world for both a local and international customer base.</span></span> <span data-ttu-id="0d396-107">Tienen oficinas, clientes, empleados y proveedores ubicados en todo el mundo para una cobertura total de los centros que ofrece.</span><span class="sxs-lookup"><span data-stu-id="0d396-107">They have offices, customers, employees, and vendors located around the world to fully service the venues they offer.</span></span>

<span data-ttu-id="0d396-108">Entre otros muchos elementos, la empresa realiza un seguimiento de RSVP, como las alergias alimentarias y las preferencias dietéticas.</span><span class="sxs-lookup"><span data-stu-id="0d396-108">Among many other items, the company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="0d396-109">Los invitados de la boda pueden registrarse en distintas actividades, como montar a caballo, practicar surf, paseos en barco, etc., e incluso interactuar entre ellos en una página web central durante los meses previos al evento.</span><span class="sxs-lookup"><span data-stu-id="0d396-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during the months leading up to the event.</span></span> <span data-ttu-id="0d396-110">La empresa recopila información personal de los empleados, los proveedores, los clientes y los invitados de la boda.</span><span class="sxs-lookup"><span data-stu-id="0d396-110">The company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="0d396-111">Debido a la naturaleza internacional de la empresa, la compañía debe cumplir varios niveles de regulación.</span><span class="sxs-lookup"><span data-stu-id="0d396-111">Because of the international nature of the business the company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="0d396-112">Declaración del problema</span><span class="sxs-lookup"><span data-stu-id="0d396-112">Problem statement</span></span>

- <span data-ttu-id="0d396-113">Los administradores de datos deben tener la capacidad de corregir información personal poco precisa y de actualizar los datos incompletos o realizar modificaciones.</span><span class="sxs-lookup"><span data-stu-id="0d396-113">Data admins must be able to correct inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="0d396-114">Necesidad de administradores de datos debe ser capaz de eliminar la información personal en la solicitud de un asunto de datos.</span><span class="sxs-lookup"><span data-stu-id="0d396-114">Data admins need must be able to delete personal information upon the request of a data subject.</span></span>

- <span data-ttu-id="0d396-115">También deben tener competencias para exportar datos y proporcionarlos a una persona registrada con un formato común y estructurado cuando los solicite.</span><span class="sxs-lookup"><span data-stu-id="0d396-115">Data admins need to export data and provide it to a data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="0d396-116">Objetivos de la empresa</span><span class="sxs-lookup"><span data-stu-id="0d396-116">Company goals</span></span>

- <span data-ttu-id="0d396-117">La información personal poco precisa o incompleta de clientes, invitados, empleados y proveedores debe corregirse o actualizarse en Azure Active Directory y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0d396-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="0d396-118">La información personal debe eliminarse de Azure Active Directory y Azure SQL Database a petición de una persona registrada.</span><span class="sxs-lookup"><span data-stu-id="0d396-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon the request of a data subject.</span></span>

- <span data-ttu-id="0d396-119">Los datos personales deben exportarse en un formato común y estructurado a petición de una persona registrada.</span><span class="sxs-lookup"><span data-stu-id="0d396-119">Personal data must be exported in a common, structured format upon the request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="0d396-120">Soluciones</span><span class="sxs-lookup"><span data-stu-id="0d396-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="0d396-121">Azure Active Directory: rectificación o corrección de datos personales poco precisos o incompletos y eliminación o borrado de perfiles de usuario o datos personales.</span><span class="sxs-lookup"><span data-stu-id="0d396-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="0d396-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) es el directorio multiinquilino basado en la nube y el servicio de administración de identidades de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0d396-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="0d396-123">Puede corregir, actualizar o eliminar los perfiles de usuario de clientes y empleados y la información de trabajo de usuario que contienen datos personales, como el nombre de usuario, el cargo, la dirección o el número de teléfono, en el entorno de [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) mediante [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0d396-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="0d396-124">Tiene que iniciar sesión con una cuenta que sea administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="0d396-124">You must sign in with an account that’s a global admin for the directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="0d396-125">¿Cómo puedo corregir o actualizar el perfil de usuario y la información laboral en Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d396-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="0d396-126">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="0d396-126">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="0d396-127">Seleccione **Más servicios**, escriba **Usuarios y grupos** en el cuadro de texto y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="0d396-127">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="0d396-129">En la hoja **Usuarios y grupos**, seleccione **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0d396-129">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="0d396-131">En la hoja **Usuarios y grupos - Usuarios**, seleccione un usuario de la lista y después, en la hoja del usuario seleccionado, seleccione **Perfil** para ver la información de perfil de usuario que hay que corregir o actualizar.</span><span class="sxs-lookup"><span data-stu-id="0d396-131">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view the user profile information that needs to be corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="0d396-133">Corrija o actualice la información y, después, en la barra de comandos, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0d396-133">Correct or update the information, and then, in the command bar, select **Save.**</span></span>

6.  <span data-ttu-id="0d396-134">En la hoja del usuario seleccionado, seleccione **Información laboral** para ver la información laboral del usuario que debe corregirse o actualizarse.</span><span class="sxs-lookup"><span data-stu-id="0d396-134">On the blade for the selected user, select **Work Info** to view user work information that needs to be corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="0d396-136">Corrija o actualice la información laboral del usuario y, después, en la barra de comandos, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0d396-136">Correct or update the user work information, and then, in the command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="0d396-137">¿Cómo elimino un perfil de usuario en Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d396-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="0d396-138">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="0d396-138">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="0d396-139">Seleccione **Más servicios**, escriba **Usuarios y grupos** en el cuadro de texto y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="0d396-139">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="0d396-140">En la hoja **Usuarios y grupos**, seleccione **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0d396-140">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="0d396-142">En la hoja **Usuarios y grupos - Usuarios** , seleccione un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="0d396-142">On the **Users and groups - Users** blade, select a user from the list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="0d396-144">En la hoja del usuario seleccionado, seleccione **Información general** y, después, en la barra de comandos, seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0d396-144">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="0d396-145">SQL Database: rectificación o corrección de datos personales poco precisos o incompletos, eliminación o borrado de datos personales y exportación de información personal</span><span class="sxs-lookup"><span data-stu-id="0d396-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="0d396-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) es una base de datos en la nube que ayuda a los desarrolladores a crear y mantener aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0d396-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="0d396-147">Los datos personales pueden actualizarse en [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) mediante consultas SQL estándares, y también se pueden eliminar.</span><span class="sxs-lookup"><span data-stu-id="0d396-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="0d396-148">Además, los datos personales se pueden exportar desde SQL Database con diferentes métodos, como el Asistente para importación y exportación de Azure SQL Server, y en distintos formatos, como un archivo BACPAC.</span><span class="sxs-lookup"><span data-stu-id="0d396-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including the Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="0d396-149">¿Cómo puedo corregir, actualizar o borrar datos personales en SQL Database?</span><span class="sxs-lookup"><span data-stu-id="0d396-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="0d396-150">Para obtener información sobre cómo corregir o actualizar datos personales en SQL Database, consulte la documentación sobre [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update With Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql) o [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="0d396-150">To learn how to correct or update personal data in SQL Database, visit the [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="0d396-151">Para obtener información sobre cómo eliminar datos personales en SQL Database, consulte la documentación sobre [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="0d396-151">To learn how to delete personal data in SQL Database, visit the [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-to-a-bacpac-file-in-sql-database"></a><span data-ttu-id="0d396-152">¿Cómo puedo exportar datos personales a un archivo BACPAC en SQL Database?</span><span class="sxs-lookup"><span data-stu-id="0d396-152">How do I export personal data to a BACPAC file in SQL Database?</span></span>

<span data-ttu-id="0d396-153">Un archivo BACPAC incluye los metadatos y datos de SQL Database y es un archivo ZIP con una extensión BACPAC.</span><span class="sxs-lookup"><span data-stu-id="0d396-153">A BACPAC file includes the SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="0d396-154">Esto puede hacerse con [Azure Portal](https://portal.azure.com/), la utilidad de línea de comandos SQLPackage, SQL Server Management Studio (SSMS) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d396-154">This can be done using the [Azure portal](https://portal.azure.com/), the SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="0d396-155">Para obtener información sobre cómo exportar datos a un archivo BACPAC, visite la página [Exportación de una base de datos de Azure SQL Database a un archivo BACPAC](https://docs.microsoft.com/azure/sql-database/sql-database-export), que incluye instrucciones detalladas para cada método mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0d396-155">To learn how to export data to a BACPAC file, visit the [Export an Azure SQL database to a BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="0d396-156">¿Cómo puedo exportar datos personales de SQL Database con el Asistente para importación y exportación de SQL Server?</span><span class="sxs-lookup"><span data-stu-id="0d396-156">How do I export personal data from SQL Database with the SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="0d396-157">Este asistente ayuda a copiar datos desde un origen a un destino.</span><span class="sxs-lookup"><span data-stu-id="0d396-157">This wizard helps you copy data from a source to a destination.</span></span> <span data-ttu-id="0d396-158">Para obtener una introducción al asistente, incluida la información sobre cómo obtenerlo, datos sobre permisos y cómo obtener ayuda con la herramienta, visite la página web [Importar y exportar datos con el Asistente para importación y exportación de SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).</span><span class="sxs-lookup"><span data-stu-id="0d396-158">For an introduction to the wizard, including how to get it, permissions information, and how to get help with the tool, visit the [Import and Export Data with the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="0d396-159">Para obtener información general de los pasos del asistente, visite la página web [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) (Pasos del Asistente para importación y exportación de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="0d396-159">For an overview of steps for the wizard, visit the [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d396-160">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0d396-160">Next Steps:</span></span>

[<span data-ttu-id="0d396-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0d396-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="0d396-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d396-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

