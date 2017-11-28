---
title: "Always Encrypted: Azure SQL Database: almacén de certificados de Windows | Microsoft Docs"
description: "Este artículo muestra cómo toosecure datos confidenciales en una base de datos SQL con cifrado de base de datos mediante el uso de Hola a Asistente para Always Encrypted en SQL Server Management Studio (SSMS). También muestra cómo toostore las claves de cifrado en los certificados de Windows hello almacenan."
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
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="1e27f-105">Always Encrypted: Proteger los datos confidenciales en la base de datos SQL y almacenar las claves de cifrado en el almacén de certificados de Windows hello</span><span class="sxs-lookup"><span data-stu-id="1e27f-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="1e27f-106">Este artículo muestra cómo toosecure datos confidenciales en una instancia de SQL de base de datos con el cifrado de base de datos mediante el uso de hello [Asistente para Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) en [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="1e27f-107">También muestra cómo toostore las claves de cifrado en los certificados de Windows hello almacenan.</span><span class="sxs-lookup"><span data-stu-id="1e27f-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="1e27f-108">Always Encrypted es una nueva tecnología de cifrado de datos en la base de datos de SQL Azure y SQL Server que ayuda a proteger los datos confidenciales almacenados en el servidor de hello, durante el movimiento entre cliente y servidor y garantizar que los datos confidenciales nunca aparece mientras Hola están en uso, como texto no cifrado en el sistema de bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e27f-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="1e27f-109">Después de cifrar datos, solo las aplicaciones cliente o servidores de aplicaciones que tienen teclas de acceso toohello pueden tener acceso a datos de texto simple.</span><span class="sxs-lookup"><span data-stu-id="1e27f-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="1e27f-110">Para más información, consulte [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="1e27f-111">Después de configurar toouse de base de datos de hello Always Encrypted, creará una aplicación de cliente en C# con toowork de Visual Studio con datos cifrado de saludo.</span><span class="sxs-lookup"><span data-stu-id="1e27f-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="1e27f-112">Siga los pasos de hello en este artículo toolearn cómo tooset seguridad Always Encrypted para una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1e27f-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="1e27f-113">En este artículo, aprenderá cómo hello tooperform siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="1e27f-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="1e27f-114">Asistente de Always Encrypted Hola de uso en SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="1e27f-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="1e27f-115">Crear una [clave maestra de columna (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="1e27f-116">Crear una [clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="1e27f-117">Crear una tabla de base de datos y cifrar columnas.</span><span class="sxs-lookup"><span data-stu-id="1e27f-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="1e27f-118">Crear una aplicación que inserta, se selecciona y muestra los datos de columnas de hello cifrado.</span><span class="sxs-lookup"><span data-stu-id="1e27f-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e27f-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1e27f-119">Prerequisites</span></span>
<span data-ttu-id="1e27f-120">Para este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="1e27f-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="1e27f-121">Una cuenta y una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e27f-121">An Azure account and subscription.</span></span> <span data-ttu-id="1e27f-122">Si no tiene una, suscríbase para [una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e27f-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1e27f-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versión 13.0.700.242 o posterior.</span><span class="sxs-lookup"><span data-stu-id="1e27f-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="1e27f-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o posterior (en el equipo de cliente hello).</span><span class="sxs-lookup"><span data-stu-id="1e27f-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="1e27f-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="1e27f-126">Crear una instancia en blanco en SQL Database</span><span class="sxs-lookup"><span data-stu-id="1e27f-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="1e27f-127">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1e27f-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1e27f-128">Haga clic en **Nuevo** > **Datos y almacenamiento** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="1e27f-129">Cree una base de datos **en blanco** denominada **Clinic** en un servidor nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="1e27f-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="1e27f-130">Para obtener instrucciones detalladas sobre cómo crear una base de datos en hello portal de Azure, consulte [la primera base de datos de SQL Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1e27f-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Crear una base de datos en blanco](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="1e27f-132">Necesitará la cadena de conexión de hello más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="1e27f-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="1e27f-133">Después de crea la base de datos de hello, vaya toohello nueva Clinic base de datos y copia Hola cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="1e27f-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="1e27f-134">Puede obtener la cadena de conexión de Hola en cualquier momento, pero resulta fácil toocopy cuando se encuentra en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e27f-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="1e27f-135">Haga clic en **Bases de datos SQL** > **Clinic** > **Mostrar las cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="1e27f-136">Copie la cadena de conexión de Hola para **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Copie la cadena de conexión de Hola](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="1e27f-138">Conectar la base de datos de toohello con SSMS</span><span class="sxs-lookup"><span data-stu-id="1e27f-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="1e27f-139">Abra SSMS y conecte el servidor de toohello con base de datos de hello Clinic.</span><span class="sxs-lookup"><span data-stu-id="1e27f-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="1e27f-140">Abra SSMS.</span><span class="sxs-lookup"><span data-stu-id="1e27f-140">Open SSMS.</span></span> <span data-ttu-id="1e27f-141">(Haga clic en **conectar** > **motor de base de datos** tooopen hello **conectar tooServer** ventana si no está abierto).</span><span class="sxs-lookup"><span data-stu-id="1e27f-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="1e27f-142">Escriba su nombre del servidor y las credenciales.</span><span class="sxs-lookup"><span data-stu-id="1e27f-142">Enter your server name and credentials.</span></span> <span data-ttu-id="1e27f-143">nombre del servidor Hello puede encontrarse en la hoja de base de datos SQL de Hola y de cadena de conexión de Hola copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1e27f-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="1e27f-144">Tipo hello servidor completo nombre incluidos *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="1e27f-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Copie la cadena de conexión de Hola](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="1e27f-146">Si hello **nueva regla de Firewall** ventana se abre, inicie sesión en tooAzure y SSMS permiten crear una nueva regla de firewall para usted.</span><span class="sxs-lookup"><span data-stu-id="1e27f-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="1e27f-147">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="1e27f-147">Create a table</span></span>
<span data-ttu-id="1e27f-148">En esta sección, creará un paciente de datos de toohold tabla.</span><span class="sxs-lookup"><span data-stu-id="1e27f-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="1e27f-149">Se trata de una tabla normal inicialmente--que va a configurar el cifrado en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="1e27f-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="1e27f-150">Expanda **Bases de datos**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="1e27f-151">Menú contextual hello **Clinic** la base de datos y haga clic en **nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="1e27f-152">Hola pegar después de Transact-SQL (T-SQL) en la nueva ventana de consulta de Hola y **Execute** lo.</span><span class="sxs-lookup"><span data-stu-id="1e27f-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="1e27f-153">Cifrado de columnas (configurar Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="1e27f-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="1e27f-154">SSMS proporciona un asistente tooeasily configurar Always Encrypted mediante la configuración de hello CMK, CEK y las columnas cifradas para usted.</span><span class="sxs-lookup"><span data-stu-id="1e27f-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="1e27f-155">Expandaa **Bases de datos** > **Clinic** > **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="1e27f-156">Menú contextual hello **pacientes** de tabla y seleccione **cifrar columnas** Asistente para Always Encrypted de tooopen Hola:</span><span class="sxs-lookup"><span data-stu-id="1e27f-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Cifrar columnas](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="1e27f-158">Asistente para Always Encrypted Hello incluye hello las secciones siguientes: **selección de columna**, **Master Key Configuration** (CMK), **validación**, y  **Resumen de**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="1e27f-159">Selección de columnas</span><span class="sxs-lookup"><span data-stu-id="1e27f-159">Column Selection</span></span>
<span data-ttu-id="1e27f-160">Haga clic en **siguiente** en hello **Introducción** Hola de página tooopen **selección de columna** página.</span><span class="sxs-lookup"><span data-stu-id="1e27f-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="1e27f-161">En esta página, seleccionará las columnas que desee tooencrypt, [Hola tipo de cifrado y qué clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="1e27f-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="1e27f-162">Cifre la información **SSN** y **BirthDate** de cada paciente.</span><span class="sxs-lookup"><span data-stu-id="1e27f-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="1e27f-163">Hola **SSN** columna usará el cifrado determinista, que admite búsquedas de igualdad, combinaciones y group by.</span><span class="sxs-lookup"><span data-stu-id="1e27f-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="1e27f-164">Hola **BirthDate** va a usar el cifrado aleatorio, que no admite operaciones de columna.</span><span class="sxs-lookup"><span data-stu-id="1e27f-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="1e27f-165">Conjunto hello **tipo de cifrado** para hello **SSN** columna demasiado**Deterministic** hello y **BirthDate** columna demasiado **Aleatorio**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="1e27f-166">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-166">Click **Next**.</span></span>

![Cifrar columnas](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="1e27f-168">Configuración de la clave maestra</span><span class="sxs-lookup"><span data-stu-id="1e27f-168">Master Key Configuration</span></span>
<span data-ttu-id="1e27f-169">Hola **Master Key Configuration** página es donde se configura la las CMK y el proveedor de almacén de claves de hello seleccione hello CMK se almacenarán.</span><span class="sxs-lookup"><span data-stu-id="1e27f-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="1e27f-170">Actualmente, puede almacenar una CMK de almacén de certificados de Windows hello, almacén de claves de Azure o un módulo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="1e27f-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="1e27f-171">Este tutorial muestra cómo toostore las claves de certificado de Windows hello almacenan.</span><span class="sxs-lookup"><span data-stu-id="1e27f-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="1e27f-172">Compruebe que el **almacén de certificados de Windows** esté seleccionado y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Configuración de la clave maestra](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="1e27f-174">Validación</span><span class="sxs-lookup"><span data-stu-id="1e27f-174">Validation</span></span>
<span data-ttu-id="1e27f-175">Puede cifrar columnas Hola ahora o guardar una toorun de secuencia de comandos de PowerShell más adelante.</span><span class="sxs-lookup"><span data-stu-id="1e27f-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="1e27f-176">Para este tutorial, seleccione **continuar ahora toofinish** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="1e27f-177">Resumen</span><span class="sxs-lookup"><span data-stu-id="1e27f-177">Summary</span></span>
<span data-ttu-id="1e27f-178">Compruebe que configuración de hello es correctos y haga clic en **finalizar** el programa de instalación hello toocomplete para Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="1e27f-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Resumen](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="1e27f-180">Comprobar acciones del Asistente de Hola</span><span class="sxs-lookup"><span data-stu-id="1e27f-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="1e27f-181">Una vez finalizado el Asistente de hello, la base de datos se configura para Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="1e27f-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="1e27f-182">Asistente para realizar de Hola Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="1e27f-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="1e27f-183">Crea un CMK.</span><span class="sxs-lookup"><span data-stu-id="1e27f-183">Created a CMK.</span></span>
* <span data-ttu-id="1e27f-184">Crea un CMK.</span><span class="sxs-lookup"><span data-stu-id="1e27f-184">Created a CEK.</span></span>
* <span data-ttu-id="1e27f-185">Hola configurado seleccionado columnas para el cifrado.</span><span class="sxs-lookup"><span data-stu-id="1e27f-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="1e27f-186">Su **pacientes** tabla actualmente no tiene datos, pero ahora se cifran los datos existentes en las columnas de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="1e27f-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="1e27f-187">Puede comprobar la creación de hello de claves de hello en SSMS yendo demasiado**Clinic** > **seguridad** > **Always Encrypted Keys**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="1e27f-188">Ahora puede ver claves nuevas Hola que Hola genera automáticamente con un asistente.</span><span class="sxs-lookup"><span data-stu-id="1e27f-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="1e27f-189">Crear una aplicación cliente que funciona con datos cifrado de saludo</span><span class="sxs-lookup"><span data-stu-id="1e27f-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="1e27f-190">Ahora que Always Encrypted está configurado, puede compilar una aplicación que realiza *inserta* y *selecciona* en hello las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="1e27f-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="1e27f-191">toosuccessfully al ejecutar la aplicación de ejemplo de Hola, debe ejecutarla en hello mismo equipo donde se ejecutó el Asistente de Always Encrypted Hola.</span><span class="sxs-lookup"><span data-stu-id="1e27f-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="1e27f-192">aplicación de hello toorun en otro equipo, debe implementar el equipo que toohello certificados Always Encrypted ejecuta la aplicación de cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="1e27f-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1e27f-193">La aplicación debe utilizar [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objetos al pasar el servidor de toohello de datos de texto simple con columnas siempre cifradas.</span><span class="sxs-lookup"><span data-stu-id="1e27f-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="1e27f-194">Se generará una excepción al pasar valores literales sin usar objetos SqlParameter.</span><span class="sxs-lookup"><span data-stu-id="1e27f-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="1e27f-195">Abra Visual Studio y cree una nueva aplicación de consola C#.</span><span class="sxs-lookup"><span data-stu-id="1e27f-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="1e27f-196">Asegúrese de que el proyecto se establece demasiado**.NET Framework 4.6** o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="1e27f-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="1e27f-197">Proyecto de hello Name **AlwaysEncryptedConsoleApp** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Nueva aplicación de consola](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="1e27f-199">Modificar su tooenable de cadena de conexión Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="1e27f-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="1e27f-200">Esta sección se explica cómo tooenable siempre cifrado en la cadena de conexión de base de datos.</span><span class="sxs-lookup"><span data-stu-id="1e27f-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="1e27f-201">Se modificará la aplicación de consola de hello que acaba de crear en la siguiente sección hello, "Aplicación de consola de ejemplo de cifrado siempre".</span><span class="sxs-lookup"><span data-stu-id="1e27f-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="1e27f-202">tooenable Always Encrypted, necesita hello tooadd **Column Encryption Setting** conexión tooyour de palabra clave de cadena y establézcalo demasiado**habilitado**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="1e27f-203">Puede establecer directamente en la cadena de conexión de hello, o se puede establecer mediante una [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="1e27f-204">aplicación de ejemplo de Hola Hola siguiente sección se muestra cómo toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="1e27f-205">Se trata de hello cambio solo necesario en una aplicación de cliente específico tooAlways cifrada.</span><span class="sxs-lookup"><span data-stu-id="1e27f-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="1e27f-206">Si tiene una aplicación existente que almacena la cadena de conexión externamente (es decir, en un archivo de configuración), es posible que pueda tooenable Always Encrypted sin cambiar ningún código.</span><span class="sxs-lookup"><span data-stu-id="1e27f-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="1e27f-207">Habilitar Always Encrypted en la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="1e27f-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="1e27f-208">Agregue Hola después de la cadena de conexión de palabra clave tooyour:</span><span class="sxs-lookup"><span data-stu-id="1e27f-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="1e27f-209">Habilitar Always Encrypted con un SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="1e27f-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="1e27f-210">Hello código siguiente muestra cómo Hola tooenable Always Encrypted estableciendo [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) demasiado[habilitado](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="1e27f-211">Aplicación de consola de ejemplo de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="1e27f-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="1e27f-212">En este ejemplo se muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="1e27f-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="1e27f-213">Modifique su tooenable de cadena de conexión siempre se cifran.</span><span class="sxs-lookup"><span data-stu-id="1e27f-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="1e27f-214">Insertar datos en columnas de hello cifrado.</span><span class="sxs-lookup"><span data-stu-id="1e27f-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="1e27f-215">Seleccionar un registro mediante el filtrado de un valor específico de una columna cifrada.</span><span class="sxs-lookup"><span data-stu-id="1e27f-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="1e27f-216">Reemplace el contenido de Hola de **Program.cs** con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="1e27f-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="1e27f-217">Reemplace la cadena de conexión de hello para la variable de connectionString global de hello en línea hello directamente encima de hello método Main con la cadena de conexión válida de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e27f-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="1e27f-218">Se trata de hello cambio solo se necesita toomake toothis código.</span><span class="sxs-lookup"><span data-stu-id="1e27f-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="1e27f-219">Ejecutar toosee de aplicación Hola Always Encrypted en acción.</span><span class="sxs-lookup"><span data-stu-id="1e27f-219">Run hello app toosee Always Encrypted in action.</span></span>

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
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

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
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
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

            Console.WriteLine("Press Enter tooexit...");
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
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
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


        // This method simply deletes all records in hello Patients table tooreset our demo.
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


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="1e27f-220">Compruebe que se cifren los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="1e27f-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="1e27f-221">Puede comprobar fácilmente que se cifran datos reales de hello en servidor hello consultando hello **pacientes** datos con SSMS.</span><span class="sxs-lookup"><span data-stu-id="1e27f-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="1e27f-222">(Use donde todavía no está habilitado el valor de cifrado de columnas de hello de la conexión actual).</span><span class="sxs-lookup"><span data-stu-id="1e27f-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="1e27f-223">Ejecute hello después de consulta en la base de datos de hello Clinic.</span><span class="sxs-lookup"><span data-stu-id="1e27f-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="1e27f-224">Puede ver que columnas Hola cifra no contienen los datos de texto simple.</span><span class="sxs-lookup"><span data-stu-id="1e27f-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="1e27f-226">toouse SSMS tooaccess Hola datos de texto simple, puede agregar hello **Column Encryption Setting = habilitado** conexión toohello de parámetro.</span><span class="sxs-lookup"><span data-stu-id="1e27f-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="1e27f-227">En SSMS, haga clic con el botón derecho en el servidor en el **Explorador de objetos** y haga clic en **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="1e27f-228">Haga clic en **conectar** > **motor de base de datos** tooopen hello **conectar tooServer** ventana y, a continuación, haga clic en **opciones**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="1e27f-229">Haga clic en **Parámetros de conexión adicionales** y escriba **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="1e27f-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="1e27f-231">Ejecución hello consulta en hello siguiente **Clinic** base de datos.</span><span class="sxs-lookup"><span data-stu-id="1e27f-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="1e27f-232">Ahora puede ver datos de texto simple de hello en columnas de hello cifrado.</span><span class="sxs-lookup"><span data-stu-id="1e27f-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="1e27f-234">Si se conecta con SSMS (o cualquier cliente) en un equipo diferente, no tendrá acceso a claves de cifrado de toohello y no será capaz de toodecrypt datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e27f-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1e27f-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e27f-235">Next steps</span></span>
<span data-ttu-id="1e27f-236">Después de crear una base de datos que usa Always Encrypted, puede que desee siguiente de Hola toodo:</span><span class="sxs-lookup"><span data-stu-id="1e27f-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="1e27f-237">Ejecutar este ejemplo desde un equipo diferente.</span><span class="sxs-lookup"><span data-stu-id="1e27f-237">Run this sample from a different computer.</span></span> <span data-ttu-id="1e27f-238">No tendrá acceso a claves de cifrado de toohello, por lo que no tendrá acceso a datos de texto simple de toohello y no se ejecutará correctamente.</span><span class="sxs-lookup"><span data-stu-id="1e27f-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="1e27f-239">[Rotar y limpiar las claves](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="1e27f-240">[Migrar los datos que ya están cifrados con Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e27f-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="1e27f-241">[Implementar máquinas del cliente de Always Encrypted certificados tooother](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (consulte la sección "Hacer que los certificados disponibles tooApplications y los usuarios" de hello).</span><span class="sxs-lookup"><span data-stu-id="1e27f-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="1e27f-242">Información relacionada</span><span class="sxs-lookup"><span data-stu-id="1e27f-242">Related information</span></span>
* [<span data-ttu-id="1e27f-243">Always Encrypted (desarrollo de clientes)</span><span class="sxs-lookup"><span data-stu-id="1e27f-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="1e27f-244">Cifrado de datos transparente</span><span class="sxs-lookup"><span data-stu-id="1e27f-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="1e27f-245">Cifrado de SQL Server</span><span class="sxs-lookup"><span data-stu-id="1e27f-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="1e27f-246">Asistente de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="1e27f-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="1e27f-247">Blog de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="1e27f-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

