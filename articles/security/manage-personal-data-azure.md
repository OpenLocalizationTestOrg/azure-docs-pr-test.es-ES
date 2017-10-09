---
title: aaaManage datos personales en Microsoft Azure | Documentos de Microsoft
description: "instrucciones sobre cómo toocorrect, actualizar, eliminar y exportar datos personales en Azure Active Directory y la base de datos de SQL Azure"
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
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="251f3-103">Administración de datos personales en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="251f3-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="251f3-104">Este artículo proporciona instrucciones sobre cómo toocorrect, actualizar, eliminar y exportar datos personales en Azure Active Directory y la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="251f3-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="251f3-105">Escenario</span><span class="sxs-lookup"><span data-stu-id="251f3-105">Scenario</span></span>

<span data-ttu-id="251f3-106">Una empresa de Dublin proporciona todo lo necesario para bodas de destino de gama alta Irlanda y alrededor de Hola a todos para una base de clientes local e internacional.</span><span class="sxs-lookup"><span data-stu-id="251f3-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="251f3-107">Tienen oficinas, clientes, empleados y proveedores ubicados en todo recintos hello world toofully servicio Hola ofrecen.</span><span class="sxs-lookup"><span data-stu-id="251f3-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="251f3-108">Entre otros muchos aspectos, empresa Hola realiza un seguimiento de confirmaciones de asistencia que incluyen alergias y las preferencias de la.</span><span class="sxs-lookup"><span data-stu-id="251f3-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="251f3-109">Los invitados novia pueden registrar para varias actividades como explorar, botes a caballo conducir, llevar a, etc. e incluso interactúan entre sí en una página web central durante los meses de hello conduzcan toohello eventos.</span><span class="sxs-lookup"><span data-stu-id="251f3-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="251f3-110">empresa Hola recopila información personal de empleados, proveedores, los clientes y los invitados novia.</span><span class="sxs-lookup"><span data-stu-id="251f3-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="251f3-111">Debido a Hola naturaleza internacional de empresa de hello business Hola debe cumplir con varios niveles de la normativa.</span><span class="sxs-lookup"><span data-stu-id="251f3-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="251f3-112">Declaración del problema</span><span class="sxs-lookup"><span data-stu-id="251f3-112">Problem statement</span></span>

- <span data-ttu-id="251f3-113">Administradores de datos deben ser capaz de toocorrect correcta actualización e información incompleta o que cambian personal información personal.</span><span class="sxs-lookup"><span data-stu-id="251f3-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="251f3-114">Necesidad de administradores de datos debe ser capaz de toodelete información personal tras la solicitud de Hola de un asunto de datos.</span><span class="sxs-lookup"><span data-stu-id="251f3-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="251f3-115">Administradores de datos necesitan los datos de tooexport y proporcionan a tooa asunto de datos en un formato común y estructurado en su solicitud.</span><span class="sxs-lookup"><span data-stu-id="251f3-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="251f3-116">Objetivos de la empresa</span><span class="sxs-lookup"><span data-stu-id="251f3-116">Company goals</span></span>

- <span data-ttu-id="251f3-117">La información personal poco precisa o incompleta de clientes, invitados, empleados y proveedores debe corregirse o actualizarse en Azure Active Directory y Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="251f3-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="251f3-118">Información personal debe eliminarse en Azure Active Directory y la base de datos de SQL Azure tras la solicitud de saludo de un asunto de datos.</span><span class="sxs-lookup"><span data-stu-id="251f3-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="251f3-119">Datos personales deben exportarse en un formato común y estructurado tras la solicitud de saludo de un asunto de datos.</span><span class="sxs-lookup"><span data-stu-id="251f3-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="251f3-120">Soluciones</span><span class="sxs-lookup"><span data-stu-id="251f3-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="251f3-121">Azure Active Directory: rectificación o corrección de datos personales poco precisos o incompletos y eliminación o borrado de perfiles de usuario o datos personales.</span><span class="sxs-lookup"><span data-stu-id="251f3-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="251f3-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) es el directorio multiinquilino basado en la nube y el servicio de administración de identidades de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="251f3-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="251f3-123">Puede corregir, actualizar o eliminar los perfiles de usuario de clientes y empleados y la información de trabajo de usuario que contienen datos personales, como nombre, título de trabajo, dirección o número de teléfono, un usuario en su [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) entorno con hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="251f3-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="251f3-124">Debe iniciar sesión con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f3-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="251f3-125">¿Cómo puedo corregir o actualizar el perfil de usuario y la información laboral en Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="251f3-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="251f3-126">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f3-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="251f3-127">Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="251f3-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="251f3-129">En hello **usuarios y grupos** hoja, seleccione **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="251f3-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="251f3-131">En hello **a los usuarios y grupos: los usuarios** hoja, seleccione un usuario de la lista de hello y, a continuación, en la hoja de hello para el usuario seleccionado de hello, seleccione **perfil** tooview información de perfil de usuario de Hola que necesita toobe corregido o actualizados.</span><span class="sxs-lookup"><span data-stu-id="251f3-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="251f3-133">Corregir o actualizar la información de hello y, a continuación, en la barra de comandos de hello, seleccione **guardar.**</span><span class="sxs-lookup"><span data-stu-id="251f3-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="251f3-134">En la hoja de hello para el usuario seleccionado de hello, seleccione **de trabajo información** información tooview de trabajo del usuario que necesita toobe corrección o actualización.</span><span class="sxs-lookup"><span data-stu-id="251f3-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="251f3-136">Corregir o actualizar la información de trabajo de usuario de hello y, a continuación, en la barra de comandos de hello, seleccione **guardar.**</span><span class="sxs-lookup"><span data-stu-id="251f3-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="251f3-137">¿Cómo elimino un perfil de usuario en Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="251f3-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="251f3-138">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f3-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="251f3-139">Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="251f3-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="251f3-140">En hello **usuarios y grupos** hoja, seleccione **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="251f3-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="251f3-142">En hello **a los usuarios y grupos: los usuarios** hoja, seleccione un usuario de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f3-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="251f3-144">En la hoja de hello para el usuario seleccionado de hello, seleccione **Introducción**y, a continuación, en la barra de comandos de hello, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="251f3-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="251f3-145">SQL Database: rectificación o corrección de datos personales poco precisos o incompletos, eliminación o borrado de datos personales y exportación de información personal</span><span class="sxs-lookup"><span data-stu-id="251f3-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="251f3-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) es una base de datos en la nube que ayuda a los desarrolladores a crear y mantener aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="251f3-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="251f3-147">Los datos personales pueden actualizarse en [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) mediante consultas SQL estándares, y también se pueden eliminar.</span><span class="sxs-lookup"><span data-stu-id="251f3-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="251f3-148">Además, los datos personales pueden exportarse desde la base de datos de SQL con una variedad de métodos, incluidos Hola importación de Azure SQL Server y el Asistente para exportación y en una variedad de formatos, incluido un archivo BACPAC.</span><span class="sxs-lookup"><span data-stu-id="251f3-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="251f3-149">¿Cómo puedo corregir, actualizar o borrar datos personales en SQL Database?</span><span class="sxs-lookup"><span data-stu-id="251f3-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="251f3-150">toolearn cómo toocorrect o actualización de datos personales en la base de datos de SQL, visite hello [actualización (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [actualizar texto](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [actualizar con la expresión de tabla común](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), o [ Actualizar texto escribir](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentación.</span><span class="sxs-lookup"><span data-stu-id="251f3-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="251f3-151">toolearn cómo toodelete datos personales en la base de datos de SQL, visite hello [eliminar (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentación.</span><span class="sxs-lookup"><span data-stu-id="251f3-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="251f3-152">¿Cómo se puede exportar archivo BACPAC de tooa de datos personales en la base de datos SQL?</span><span class="sxs-lookup"><span data-stu-id="251f3-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="251f3-153">Un archivo BACPAC incluye los metadatos y datos de la base de datos SQL de Hola y es un archivo zip con una extensión BACPAC.</span><span class="sxs-lookup"><span data-stu-id="251f3-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="251f3-154">Esto puede hacerse mediante hello [portal de Azure](https://portal.azure.com/), Hola utilidad de línea de comandos SQLPackage, SQL Server Management Studio (SSMS) o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="251f3-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="251f3-155">toolearn cómo archivo BACPAC tooa tooexport datos, visite hello [exportar un archivo BACPAC de tooa de base de datos de SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-export) página, que incluye instrucciones detalladas para cada método mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="251f3-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="251f3-156">¿Cómo se puede exportar datos personales de la base de datos de SQL con SQL Server Import hello y Asistente para exportación?</span><span class="sxs-lookup"><span data-stu-id="251f3-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="251f3-157">Este asistente le ayuda a copiar los datos de un origen tooa destino.</span><span class="sxs-lookup"><span data-stu-id="251f3-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="251f3-158">Para que un asistente de toohello introducción, incluido cómo tooget, información sobre permisos, y cómo ayudar tooget con la herramienta de hello, visitan Hola [importar y exportar datos con SQL Server Import hello y Asistente para exportación de](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) página web.</span><span class="sxs-lookup"><span data-stu-id="251f3-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="251f3-159">Para obtener información general de las etapas de Asistente de hello, visite hello [los pasos de hello importación de SQL Server y el Asistente para exportación de](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) página web.</span><span class="sxs-lookup"><span data-stu-id="251f3-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="251f3-160">Pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="251f3-160">Next Steps:</span></span>

[<span data-ttu-id="251f3-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="251f3-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="251f3-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="251f3-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

