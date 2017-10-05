---
title: "Always Encrypted: Azure SQL Database: almacén de certificados de Windows | Microsoft Docs"
description: "En este artículo se muestra cómo proteger los datos confidenciales de una base de datos SQL con cifrado de base de datos mediante el asistente de Always Encrypted en SQL Server Management Studio (SSMS). También muestra cómo almacenar las claves de cifrado en el almacén de certificados de Windows."
keywords: cifrar datos, cifrado sql, cifrado de base de datos, datos confidenciales, Always Encrypted
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: d1fdfc4f739e65ff532b159eefaffe1622ad0963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-the-windows-certificate-store"></a><span data-ttu-id="e4ad7-105">Always Encrypted: protección de los datos confidenciales en Base de datos SQL y almacenamiento de las claves de cifrado en el almacén de certificados de Windows</span><span class="sxs-lookup"><span data-stu-id="e4ad7-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in the Windows certificate store</span></span>

<span data-ttu-id="e4ad7-106">En este artículo se muestra cómo proteger los datos confidenciales de una base de datos SQL con cifrado de base de datos mediante el [asistente de Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) en [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-106">This article shows you how to secure sensitive data in a SQL database with database encryption by using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="e4ad7-107">También muestra cómo almacenar las claves de cifrado en el almacén de certificados de Windows.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-107">It also shows you how to store your encryption keys in the Windows certificate store.</span></span>

<span data-ttu-id="e4ad7-108">Always Encrypted es una nueva tecnología de cifrado de datos de Base de datos SQL de Azure y SQL Server que ayuda a proteger los datos confidenciales en reposo en el servidor durante el movimiento entre cliente y servidor, y cuando los datos están en uso, lo que garantiza que los datos confidenciales nunca van a aparecer como texto no cifrado dentro del sistema de base de datos.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use, ensuring that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="e4ad7-109">Después de cifrar los datos, solo las aplicaciones cliente o los servidores de aplicaciones que tienen acceso a las claves pueden acceder a los datos de texto no cifrado.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-109">After you encrypt data, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="e4ad7-110">Para más información, consulte [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="e4ad7-111">Después de configurar la base de datos para usar Always Encrypted, creará una aplicación cliente en C# con Visual Studio para trabajar con los datos cifrados.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-111">After configuring the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="e4ad7-112">Siga los pasos de este artículo y aprenda a configurar Always Encrypted para una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-112">Follow the steps in this article to learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="e4ad7-113">En este artículo, aprenderá a realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e4ad7-113">In this article, you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="e4ad7-114">Usar el asistente de Always Encrypted en SSMS para crear [claves de Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-114">Use the Always Encrypted wizard in SSMS to create [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="e4ad7-115">Crear una [clave maestra de columna (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="e4ad7-116">Crear una [clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="e4ad7-117">Crear una tabla de base de datos y cifrar columnas.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="e4ad7-118">Crear una aplicación que inserta, selecciona y muestra los datos de las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-118">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4ad7-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e4ad7-119">Prerequisites</span></span>
<span data-ttu-id="e4ad7-120">Para este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="e4ad7-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="e4ad7-121">Una cuenta y una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-121">An Azure account and subscription.</span></span> <span data-ttu-id="e4ad7-122">Si no tiene una, suscríbase para [una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e4ad7-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versión 13.0.700.242 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="e4ad7-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o posterior (en el equipo cliente).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="e4ad7-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="e4ad7-126">Crear una base de datos SQL en blanco</span><span class="sxs-lookup"><span data-stu-id="e4ad7-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="e4ad7-127">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-127">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e4ad7-128">Haga clic en **Nuevo** > **Datos y almacenamiento** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="e4ad7-129">Cree una base de datos **en blanco** denominada **Clinic** en un servidor nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="e4ad7-130">Si desea obtener instrucciones detalladas para crear una base de datos en Azure Portal, consulte [Su primera base de datos de Azure SQL Database](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-130">For detailed instructions about creating a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Crear una base de datos en blanco](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="e4ad7-132">Necesitará el nombre de la cadena de conexión más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-132">You will need the connection string later in the tutorial.</span></span> <span data-ttu-id="e4ad7-133">Después de crear la base de datos, vaya a la nueva base de datos Clinic y copie la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-133">After the database is created, go to the new Clinic database and copy the connection string.</span></span> <span data-ttu-id="e4ad7-134">Puede obtener la cadena de conexión en cualquier momento, pero es fácil copiarla si está en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-134">You can get the connection string at any time, but it's easy to copy it when you're in the Azure portal.</span></span>

1. <span data-ttu-id="e4ad7-135">Haga clic en **Bases de datos SQL** > **Clinic** > **Mostrar las cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="e4ad7-136">Copie la cadena de conexión para **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-136">Copy the connection string for **ADO.NET**.</span></span>
   
    ![Copiar la cadena de conexión](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="e4ad7-138">Conéctese a la base de datos con SSMS</span><span class="sxs-lookup"><span data-stu-id="e4ad7-138">Connect to the database with SSMS</span></span>
<span data-ttu-id="e4ad7-139">Abra SSMS y conéctese al servidor con la base de datos Clinic.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-139">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="e4ad7-140">Abra SSMS.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-140">Open SSMS.</span></span> <span data-ttu-id="e4ad7-141">(Haga clic en **Conectar** > **Motor de base de datos** para abrir la ventana **Conectar con el servidor** si no está abierta).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-141">(Click **Connect** > **Database Engine** to open the **Connect to Server** window if it is not open).</span></span>
2. <span data-ttu-id="e4ad7-142">Escriba su nombre del servidor y las credenciales.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-142">Enter your server name and credentials.</span></span> <span data-ttu-id="e4ad7-143">El nombre del servidor puede encontrarse en la hoja de la base de datos SQL y en la cadena de conexión que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-143">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="e4ad7-144">Escriba el nombre de servidor completo (incluido *database.windows.net*).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-144">Type the complete server name including *database.windows.net*.</span></span>
   
    ![Copiar la cadena de conexión](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="e4ad7-146">Si se abre la ventana **Nueva regla de firewall** , inicie sesión en Azure y permita que SSMS cree una nueva regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-146">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="e4ad7-147">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="e4ad7-147">Create a table</span></span>
<span data-ttu-id="e4ad7-148">En esta sección, creará una tabla para almacenar datos de pacientes.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-148">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="e4ad7-149">Inicialmente será una tabla normal; configurará el cifrado en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-149">This will be a normal table initially--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="e4ad7-150">Expanda **Bases de datos**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="e4ad7-151">Haga clic con el botón derecho en la base de datos **Clinic** y haga clic en **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-151">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="e4ad7-152">Pegue el siguiente código Transact-SQL (T-SQL) en la nueva ventana de consulta y haga clic en **Ejecutar** .</span><span class="sxs-lookup"><span data-stu-id="e4ad7-152">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="e4ad7-153">Cifrado de columnas (configurar Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="e4ad7-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="e4ad7-154">SSMS proporciona un asistente para configurar Always Encrypted de forma fácil mediante la configuración automática de CMK, CEK y columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-154">SSMS provides a wizard to easily configure Always Encrypted by setting up the CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="e4ad7-155">Expandaa **Bases de datos** > **Clinic** > **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="e4ad7-156">Haga clic con el botón derecho en la tabla **Patients** y seleccione **Cifrar columnas** para abrir el asistente de Always Encrypted:</span><span class="sxs-lookup"><span data-stu-id="e4ad7-156">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![Cifrar columnas](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="e4ad7-158">El asistente de Always Encrypted incluye las siguientes secciones: **Selección de columnas**, **Configuración de la clave maestra** (CMK), **Validación** y **Resumen**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-158">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="e4ad7-159">Selección de columnas</span><span class="sxs-lookup"><span data-stu-id="e4ad7-159">Column Selection</span></span>
<span data-ttu-id="e4ad7-160">En la página **Introducción**, haga clic en **Siguiente** para abrir la página **Selección de columnas**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-160">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="e4ad7-161">En esta página, seleccione las columnas que desea cifrar, [el tipo de cifrado y qué clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) desea usar.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-161">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="e4ad7-162">Cifre la información **SSN** y **BirthDate** de cada paciente.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="e4ad7-163">La columna **SSN** usará cifrado determinista, que admite búsquedas de igualdad, combinaciones y agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-163">The **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="e4ad7-164">La columna **BirthDate** usará cifrado aleatorio, que no admite operaciones.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-164">The **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="e4ad7-165">Establezca el **Tipo de cifrado** de la columna **SSN** en **Determinista** y la columna **BirthDate** en **Aleatoria**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-165">Set the **Encryption Type** for the **SSN** column to **Deterministic** and the **BirthDate** column to **Randomized**.</span></span> <span data-ttu-id="e4ad7-166">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-166">Click **Next**.</span></span>

![Cifrar columnas](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="e4ad7-168">Configuración de la clave maestra</span><span class="sxs-lookup"><span data-stu-id="e4ad7-168">Master Key Configuration</span></span>
<span data-ttu-id="e4ad7-169">En la página **Configuración de la clave maestra** se configura la clave maestra de columna (CMK) y se selecciona el proveedor del almacén de claves donde se almacenará la CMK.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-169">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="e4ad7-170">Actualmente, puede almacenar una CMK en el almacén de certificados de Windows, en Almacén de claves de Azure o en un módulo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-170">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="e4ad7-171">En este tutorial se muestra cómo almacenar las claves en el almacén de certificados de Windows.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-171">This tutorial shows how to store your keys in the Windows certificate store.</span></span>

<span data-ttu-id="e4ad7-172">Compruebe que el **almacén de certificados de Windows** esté seleccionado y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Configuración de la clave maestra](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="e4ad7-174">Validación</span><span class="sxs-lookup"><span data-stu-id="e4ad7-174">Validation</span></span>
<span data-ttu-id="e4ad7-175">Puede cifrar las columnas ahora o guardar un script de PowerShell para ejecutarlo más tarde.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-175">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="e4ad7-176">Para este tutorial, seleccione **Continuar para finalizar ahora** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-176">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="e4ad7-177">Resumen</span><span class="sxs-lookup"><span data-stu-id="e4ad7-177">Summary</span></span>
<span data-ttu-id="e4ad7-178">Compruebe que la configuración sea correcta y haga clic en **Finalizar** para completar la configuración de Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-178">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![Resumen](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="e4ad7-180">Comprobación de las acciones del asistente</span><span class="sxs-lookup"><span data-stu-id="e4ad7-180">Verify the wizard's actions</span></span>
<span data-ttu-id="e4ad7-181">Una vez finalizado el asistente, la base de datos estará configurada para Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-181">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="e4ad7-182">El asistente habrá realizado las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="e4ad7-182">The wizard performed the following actions:</span></span>

* <span data-ttu-id="e4ad7-183">Crea un CMK.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-183">Created a CMK.</span></span>
* <span data-ttu-id="e4ad7-184">Crea un CMK.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-184">Created a CEK.</span></span>
* <span data-ttu-id="e4ad7-185">Configuración de las columnas seleccionadas para el cifrado.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-185">Configured the selected columns for encryption.</span></span> <span data-ttu-id="e4ad7-186">La tabla **Patients** aún no tiene datos, pero los datos existentes en las columnas seleccionadas ahora están cifrados.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-186">Your **Patients** table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="e4ad7-187">Para comprobar la creación de las claves en SSMS, vaya a **Clinic** > **Seguridad** > **Claves de Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-187">You can verify the creation of the keys in SSMS by going to **Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="e4ad7-188">Ahora puede ver las nuevas claves que el asistente generó para usted.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-188">You can now see the new keys that the wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="e4ad7-189">Crear una aplicación cliente que funcione con los datos cifrados</span><span class="sxs-lookup"><span data-stu-id="e4ad7-189">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="e4ad7-190">Ahora que Always Encrypted está configurado, vamos a crear una aplicación que realice operaciones de *inserción* y *selección* en las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span> <span data-ttu-id="e4ad7-191">Para ejecutar correctamente la aplicación de ejemplo, debe ejecutarla en el mismo equipo en el que ejecutó el asistente de Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-191">To successfully run the sample application, you must run it on the same computer where you ran the Always Encrypted wizard.</span></span> <span data-ttu-id="e4ad7-192">Para ejecutar la aplicación en otro equipo, debe implementar los certificados de Always Encrypted en el equipo que ejecuta la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-192">To run the application on another computer, you must deploy your Always Encrypted certificates to the computer running the client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e4ad7-193">La aplicación debe usar objetos [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) al pasar datos de texto no cifrado al servidor con columnas de Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="e4ad7-194">Se generará una excepción al pasar valores literales sin usar objetos SqlParameter.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="e4ad7-195">Abra Visual Studio y cree una nueva aplicación de consola C#.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="e4ad7-196">Asegúrese de que el proyecto esté establecido en **.NET Framework 4.6** o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-196">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="e4ad7-197">Asigne al proyecto el nombre **AlwaysEncryptedConsoleApp** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-197">Name the project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Nueva aplicación de consola](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="e4ad7-199">Modificar la cadena de conexión para habilitar Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="e4ad7-199">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="e4ad7-200">En esta sección se explica cómo habilitar Always Encrypted en la cadena de conexión de su base de datos.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-200">This section explains how to enable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="e4ad7-201">La aplicación de consola que acaba de crear se modifica en la siguiente sección, “Aplicación de consola de ejemplo de Always Encrypted”.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-201">You will modify the console app you just created in the next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="e4ad7-202">Para habilitar Always Encrypted, debe agregar la palabra clave **Column Encryption Setting** a la cadena de conexión y establecerla en **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-202">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="e4ad7-203">Puede establecerla directamente en la cadena de conexión o mediante [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-203">You can set this directly in the connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="e4ad7-204">La aplicación de ejemplo de la siguiente sección muestra cómo usar **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-204">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="e4ad7-205">Este es el único cambio necesario en una aplicación cliente específica de Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-205">This is the only change required in a client application specific to Always Encrypted.</span></span> <span data-ttu-id="e4ad7-206">Si tiene una aplicación existente que almacena su cadena de conexión de forma externa (es decir, en un archivo de configuración) puede habilitar Always Encrypted sin cambiar ningún código.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able to enable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="e4ad7-207">Modificar Always Encrypted en la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="e4ad7-207">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="e4ad7-208">Agregue la siguiente palabra clave en la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="e4ad7-208">Add the following keyword to your connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="e4ad7-209">Habilitar Always Encrypted con un SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="e4ad7-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="e4ad7-210">El siguiente código muestra cómo habilitar Always Encrypted estableciendo [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) en [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-210">The following code shows how to enable Always Encrypted by setting the [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="e4ad7-211">Aplicación de consola de ejemplo de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="e4ad7-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="e4ad7-212">En este ejemplo se muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="e4ad7-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="e4ad7-213">Modificar la cadena de conexión para habilitar Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-213">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="e4ad7-214">Insertar datos en las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-214">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="e4ad7-215">Seleccionar un registro mediante el filtrado de un valor específico de una columna cifrada.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="e4ad7-216">Reemplace el contenido de **Program.cs** por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-216">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="e4ad7-217">Reemplace la cadena de conexión para la variable global connectionString en la línea directamente anterior al método Main por una cadena de conexión válida desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-217">Replace the connection string for the global connectionString variable in the line directly above the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="e4ad7-218">Este es el único cambio que necesita realizar en este código.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-218">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="e4ad7-219">Ejecute la aplicación para ver Always Encrypted en acción.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-219">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from the Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for the connection.
            // This is the only change specific to Always Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update the connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign the updated connection string to our global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records to restart this demo app.
            ResetPatientsTable();

            // Add sample data to the Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data to the database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // The example allows duplicate SSN entries so we will return all records
            // that match the provided value and store the results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter to exit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("The following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key to exit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in the Patients table to reset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="e4ad7-220">Comprobación del cifrado de los datos</span><span class="sxs-lookup"><span data-stu-id="e4ad7-220">Verify that the data is encrypted</span></span>
<span data-ttu-id="e4ad7-221">Para comprobar rápidamente si los datos reales en el servidor se están cifrando, consulte los datos de **Patients** con SSMS.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-221">You can quickly check that the actual data on the server is encrypted by querying the **Patients** data with SSMS.</span></span> <span data-ttu-id="e4ad7-222">(Use su conexión actual si la configuración de cifrado de columnas no está habilitado aún).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-222">(Use your current connection where the column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="e4ad7-223">Ejecute la siguiente consulta en la base de datos Clinic.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-223">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="e4ad7-224">Puede ver que las columnas cifradas no contienen datos de texto no cifrado.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-224">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="e4ad7-226">Par usar SSMS para obtener acceso a los datos de texto no cifrado, puede agregar el parámetro **Column Encryption Setting=enabled** a la conexión.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-226">To use SSMS to access the plaintext data, you can add the **Column Encryption Setting=enabled** parameter to the connection.</span></span>

1. <span data-ttu-id="e4ad7-227">En SSMS, haga clic con el botón derecho en el servidor en el **Explorador de objetos** y haga clic en **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="e4ad7-228">Haga clic en **Conectar** > **Motor de base de datos** para abrir la ventana **Conectar con el servidor** y haga clic en **Opciones**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-228">Click **Connect** > **Database Engine** to open the **Connect to Server** window, and then click **Options**.</span></span>
3. <span data-ttu-id="e4ad7-229">Haga clic en **Parámetros de conexión adicionales** y escriba **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="e4ad7-231">Ejecute la siguiente consulta en la base de datos **Clinic** .</span><span class="sxs-lookup"><span data-stu-id="e4ad7-231">Run the following query on the **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="e4ad7-232">Ahora puede ver los datos de texto no cifrado en las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-232">You can now see the plaintext data in the encrypted columns.</span></span>

    ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="e4ad7-234">Si se conecta con SSMS (o cualquier cliente) desde un equipo diferente, no tendrá acceso a las claves de cifrado y no podrá descifrar los datos.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-234">If you connect with SSMS (or any client) from a different computer, it will not have access to the encryption keys and will not be able to decrypt the data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e4ad7-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4ad7-235">Next steps</span></span>
<span data-ttu-id="e4ad7-236">Después de crear una base de datos que usa Always Encrypted, es posible que quiera hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e4ad7-236">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="e4ad7-237">Ejecutar este ejemplo desde un equipo diferente.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-237">Run this sample from a different computer.</span></span> <span data-ttu-id="e4ad7-238">No tendrá acceso a las claves de cifrado, por lo que no tendrá acceso a los datos de texto no cifrado y no se ejecutará correctamente.</span><span class="sxs-lookup"><span data-stu-id="e4ad7-238">It won't have access to the encryption keys, so it will not have access to the plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="e4ad7-239">[Rotar y limpiar las claves](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="e4ad7-240">[Migrar los datos que ya están cifrados con Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="e4ad7-241">[Implementar certificados de Always Encrypted en otros equipos cliente](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (consulte la sección “Disponibilidad de los certificados para las aplicaciones y los usuarios”).</span><span class="sxs-lookup"><span data-stu-id="e4ad7-241">[Deploy Always Encrypted certificates to other client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see the "Making Certificates Available to Applications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="e4ad7-242">Información relacionada</span><span class="sxs-lookup"><span data-stu-id="e4ad7-242">Related information</span></span>
* [<span data-ttu-id="e4ad7-243">Always Encrypted (desarrollo de clientes)</span><span class="sxs-lookup"><span data-stu-id="e4ad7-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="e4ad7-244">Cifrado de datos transparente</span><span class="sxs-lookup"><span data-stu-id="e4ad7-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="e4ad7-245">Cifrado de SQL Server</span><span class="sxs-lookup"><span data-stu-id="e4ad7-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="e4ad7-246">Asistente de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="e4ad7-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="e4ad7-247">Blog de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="e4ad7-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

