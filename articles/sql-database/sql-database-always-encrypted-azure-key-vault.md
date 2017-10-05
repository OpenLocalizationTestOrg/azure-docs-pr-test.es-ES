---
title: 'Always Encrypted: SQL Database: Azure Key Vault | Microsoft Docs'
description: "En este artículo se muestra cómo proteger los datos confidenciales de una base de datos SQL con cifrado de datos mediante el asistente de Always Encrypted en SQL Server Management Studio. También incluye instrucciones para almacenar cada clave de cifrado en Almacén de claves de Azure."
keywords: cifrado de datos, clave de cifrado, cifrado en la nube
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 61bfd420425b4740f6d4ebc01a403a88ff351382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="346fb-105">Always Encrypted: protección de datos confidenciales en Base de datos SQL y almacenamiento de las claves de cifrado en Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="346fb-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="346fb-106">En este artículo se muestra cómo proteger los datos confidenciales de una base de datos SQL con cifrado de datos mediante el [asistente de Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) en [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-106">This article shows you how to secure sensitive data in a SQL database with data encryption using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="346fb-107">También incluye instrucciones para almacenar cada clave de cifrado en Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="346fb-107">It also includes instructions that will show you how to store each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="346fb-108">Always Encrypted es una nueva tecnología de cifrado de datos de Base de datos SQL de Azure y SQL Server que ayuda a proteger los datos confidenciales en reposo en el servidor durante el traslado entre el cliente y el servidor, y mientras los datos están en uso.</span><span class="sxs-lookup"><span data-stu-id="346fb-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use.</span></span> <span data-ttu-id="346fb-109">Always Encrypted garantiza que los datos confidenciales nunca van a aparecer como texto no cifrado dentro del sistema de base de datos.</span><span class="sxs-lookup"><span data-stu-id="346fb-109">Always Encrypted ensures that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="346fb-110">Después de configurar el cifrado de datos, solo las aplicaciones cliente o los servidores de aplicaciones que tienen acceso a las claves pueden acceder a los datos de texto no cifrado.</span><span class="sxs-lookup"><span data-stu-id="346fb-110">After you configure data encryption, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="346fb-111">Para más información, consulte [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="346fb-112">Después de configurar la base de datos para usar Always Encrypted, creará una aplicación cliente en C# con Visual Studio para trabajar con los datos cifrados.</span><span class="sxs-lookup"><span data-stu-id="346fb-112">After you configure the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="346fb-113">Siga los pasos de este artículo y aprenda a configurar Always Encrypted para una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="346fb-113">Follow the steps in this article and learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="346fb-114">En este artículo aprenderá a realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="346fb-114">In this article you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="346fb-115">Usar el asistente de Always Encrypted en SSMS para crear [claves de Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="346fb-115">Use the Always Encrypted wizard in SSMS to create [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="346fb-116">Crear una [clave maestra de columna (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="346fb-117">Crear una [clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="346fb-118">Crear una tabla de base de datos y cifrar columnas.</span><span class="sxs-lookup"><span data-stu-id="346fb-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="346fb-119">Crear una aplicación que inserta, selecciona y muestra los datos de las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="346fb-119">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="346fb-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="346fb-120">Prerequisites</span></span>
<span data-ttu-id="346fb-121">Para este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="346fb-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="346fb-122">Una cuenta y una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="346fb-122">An Azure account and subscription.</span></span> <span data-ttu-id="346fb-123">Si no tiene una, suscríbase para [una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="346fb-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="346fb-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versión 13.0.700.242 o posterior.</span><span class="sxs-lookup"><span data-stu-id="346fb-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="346fb-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o posterior (en el equipo cliente).</span><span class="sxs-lookup"><span data-stu-id="346fb-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="346fb-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="346fb-127">[Azure PowerShell](/powershell/azure/overview), versión 1.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="346fb-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="346fb-128">Escriba **(Get-Module azure -ListAvailable).Version** para ver qué versión de PowerShell se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="346fb-128">Type **(Get-Module azure -ListAvailable).Version** to see what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-to-access-the-sql-database-service"></a><span data-ttu-id="346fb-129">Habilitación de la aplicación cliente para obtener acceso al servicio de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="346fb-129">Enable your client application to access the SQL Database service</span></span>
<span data-ttu-id="346fb-130">Primero debe habilitar la aplicación cliente para obtener acceso al servicio SQL Database; para ello, configure la autenticación necesaria y obtenga los valores de *ClientId* y *Secret* necesarios para autenticar la aplicación en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="346fb-130">You must enable your client application to access the SQL Database service by setting up the required authentication and acquiring the *ClientId* and *Secret* that you will need to authenticate your application in the following code.</span></span>

1. <span data-ttu-id="346fb-131">Abra el [Portal de Azure clásico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="346fb-131">Open the [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="346fb-132">Seleccione **Active Directory** y haga clic en la instancia de Active Directory que la aplicación usará.</span><span class="sxs-lookup"><span data-stu-id="346fb-132">Select **Active Directory** and click the Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="346fb-133">Haga clic en **Aplicaciones** y luego en **AGREGAR**.</span><span class="sxs-lookup"><span data-stu-id="346fb-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="346fb-134">Escriba un nombre para la aplicación (por ejemplo: *myClientApp*), seleccione **APLICACIÓN WEB**y haga clic en la flecha para continuar.</span><span class="sxs-lookup"><span data-stu-id="346fb-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click the arrow to continue.</span></span>
5. <span data-ttu-id="346fb-135">En **URL DE INICIO DE SESIÓN** y **URI DE ID. DE APLICACIÓN**, escriba una dirección URL válida (por ejemplo, *http://myClientApp*) y continúe.</span><span class="sxs-lookup"><span data-stu-id="346fb-135">For the **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="346fb-136">Haga clic en **CONFIGURAR**.</span><span class="sxs-lookup"><span data-stu-id="346fb-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="346fb-137">Copie el **ID. DE CLIENTE**.</span><span class="sxs-lookup"><span data-stu-id="346fb-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="346fb-138">(Necesitará este valor en el código más adelante).</span><span class="sxs-lookup"><span data-stu-id="346fb-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="346fb-139">En la sección **Claves**, seleccione **1 año** en la lista desplegable **Seleccionar duración**.</span><span class="sxs-lookup"><span data-stu-id="346fb-139">In the **keys** section, select **1 year** from the  **Select duration** drop-down list.</span></span> <span data-ttu-id="346fb-140">(Copiará la clave después de guardar en el paso 13).</span><span class="sxs-lookup"><span data-stu-id="346fb-140">(You will copy the key after you save in step 13.)</span></span>
9. <span data-ttu-id="346fb-141">Desplácese hacia abajo y haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="346fb-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="346fb-142">Deje **MOSTRAR** en **Aplicaciones de Microsoft** y seleccione **API de administración de servicios de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="346fb-142">Leave **SHOW** set to **Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="346fb-143">Haga clic en la marca de verificación para continuar.</span><span class="sxs-lookup"><span data-stu-id="346fb-143">Click the checkmark to continue.</span></span>
11. <span data-ttu-id="346fb-144">En la lista desplegable **Permisos delegados**, seleccione **Acceso a administración de servicios de Azure...**</span><span class="sxs-lookup"><span data-stu-id="346fb-144">Select **Access Azure Service Management...** from the **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="346fb-145">Haga clic en **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="346fb-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="346fb-146">Una vez finalizada la operación de guardar, copie el valor de clave en la sección **keys** .</span><span class="sxs-lookup"><span data-stu-id="346fb-146">After the save finishes, copy the key value in the **keys** section.</span></span> <span data-ttu-id="346fb-147">(Necesitará este valor en el código más adelante).</span><span class="sxs-lookup"><span data-stu-id="346fb-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-to-store-your-keys"></a><span data-ttu-id="346fb-148">Creación de un almacén de claves para guardar las claves</span><span class="sxs-lookup"><span data-stu-id="346fb-148">Create a key vault to store your keys</span></span>
<span data-ttu-id="346fb-149">Ahora que la aplicación cliente está configurada y tiene el identificador de cliente, es el momento de crear un almacén de claves y configurar su directiva de acceso para que el usuario y su aplicación puedan acceder a los secretos del almacén (las claves de Always Encrypted).</span><span class="sxs-lookup"><span data-stu-id="346fb-149">Now that your client app is configured and you have your client ID, it's time to create a key vault and configure its access policy so you and your application can access the vault's secrets (the Always Encrypted keys).</span></span> <span data-ttu-id="346fb-150">Los permisos *create*, *get*, *list*, *sign*, *verify*, *wrapKey* y *unwrapKey* son necesarios para crear una nueva clave maestra de columna y configurar el cifrado con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="346fb-150">The *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="346fb-151">Para crear rápidamente un almacén de claves, ejecute el script siguiente.</span><span class="sxs-lookup"><span data-stu-id="346fb-151">You can quickly create a key vault by running the following script.</span></span> <span data-ttu-id="346fb-152">Para obtener una explicación detallada de estos cmdlets y más información sobre cómo crear y configurar un almacén de claves, consulte [Introducción a Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="346fb-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="346fb-153">Crear una base de datos SQL en blanco</span><span class="sxs-lookup"><span data-stu-id="346fb-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="346fb-154">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="346fb-154">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="346fb-155">Vaya a **Nuevo** > **Datos y almacenamiento** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="346fb-155">Go to **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="346fb-156">Cree una base de datos **en blanco** denominada **Clinic** en un servidor nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="346fb-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="346fb-157">Para obtener instrucciones detalladas para crear una base de datos en Azure Portal, consulte [Su primera instancia de Azure SQL Database](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="346fb-157">For detailed directions about how to create a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Crear una base de datos en blanco](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="346fb-159">Necesitará la cadena de conexión más adelante en el tutorial; por lo tanto, después de crear la base de datos, vaya a la nueva base de datos Clinic y copie la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="346fb-159">You will need the connection string later in the tutorial, so after you create the database, browse to the new  Clinic database and copy the connection string.</span></span> <span data-ttu-id="346fb-160">Puede obtener la cadena de conexión en cualquier momento, pero es fácil copiarla en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="346fb-160">You can get the connection string at any time, but it's easy to copy it in the Azure portal.</span></span>

1. <span data-ttu-id="346fb-161">Vaya a **Bases de datos SQL** > **Clinic** > **Mostrar las cadenas de conexión de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="346fb-161">Go to **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="346fb-162">Copie la cadena de conexión para **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="346fb-162">Copy the connection string for **ADO.NET**.</span></span>
   
    ![Copiar la cadena de conexión](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="346fb-164">Conéctese a la base de datos con SSMS</span><span class="sxs-lookup"><span data-stu-id="346fb-164">Connect to the database with SSMS</span></span>
<span data-ttu-id="346fb-165">Abra SSMS y conéctese al servidor con la base de datos Clinic.</span><span class="sxs-lookup"><span data-stu-id="346fb-165">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="346fb-166">Abra SSMS.</span><span class="sxs-lookup"><span data-stu-id="346fb-166">Open SSMS.</span></span> <span data-ttu-id="346fb-167">(Vaya a **Conectar** > **Motor de base de datos** para abrir la ventana **Conectar con el servidor** si no está abierta).</span><span class="sxs-lookup"><span data-stu-id="346fb-167">(Go to **Connect** > **Database Engine** to open the **Connect to Server** window if it isn't open.)</span></span>
2. <span data-ttu-id="346fb-168">Escriba su nombre del servidor y las credenciales.</span><span class="sxs-lookup"><span data-stu-id="346fb-168">Enter your server name and credentials.</span></span> <span data-ttu-id="346fb-169">El nombre del servidor puede encontrarse en la hoja de la base de datos SQL y en la cadena de conexión que copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="346fb-169">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="346fb-170">Escriba el nombre de servidor completo, incluido *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="346fb-170">Type the complete server name, including *database.windows.net*.</span></span>
   
    ![Copiar la cadena de conexión](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="346fb-172">Si se abre la ventana **Nueva regla de firewall** , inicie sesión en Azure y permita que SSMS cree una nueva regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="346fb-172">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="346fb-173">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="346fb-173">Create a table</span></span>
<span data-ttu-id="346fb-174">En esta sección, creará una tabla para almacenar datos de pacientes.</span><span class="sxs-lookup"><span data-stu-id="346fb-174">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="346fb-175">Inicialmente no están cifrados; configurará el cifrado en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="346fb-175">It's not initially encrypted--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="346fb-176">Expanda **Bases de datos**.</span><span class="sxs-lookup"><span data-stu-id="346fb-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="346fb-177">Haga clic con el botón derecho en la base de datos **Clinic** y haga clic en **Nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="346fb-177">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="346fb-178">Pegue el siguiente código Transact-SQL (T-SQL) en la nueva ventana de consulta y haga clic en **Ejecutar** .</span><span class="sxs-lookup"><span data-stu-id="346fb-178">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="346fb-179">Cifrado de columnas (configurar Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="346fb-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="346fb-180">SSMS proporciona un asistente para ayudar a configurar Always Encrypted fácilmente, que configura automáticamente la clave maestra de columna, la clave de cifrado de columna y las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="346fb-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up the column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="346fb-181">Expandaa **Bases de datos** > **Clinic** > **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="346fb-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="346fb-182">Haga clic con el botón derecho en la tabla **Patients** y seleccione **Cifrar columnas** para abrir el asistente de Always Encrypted:</span><span class="sxs-lookup"><span data-stu-id="346fb-182">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![Cifrar columnas](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="346fb-184">El asistente de Always Encrypted incluye las siguientes secciones: **Selección de columnas**, **Configuración de la clave maestra**, **Validación** y **Resumen**.</span><span class="sxs-lookup"><span data-stu-id="346fb-184">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="346fb-185">Selección de columnas</span><span class="sxs-lookup"><span data-stu-id="346fb-185">Column Selection</span></span>
<span data-ttu-id="346fb-186">En la página **Introducción**, haga clic en **Siguiente** para abrir la página **Selección de columnas**.</span><span class="sxs-lookup"><span data-stu-id="346fb-186">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="346fb-187">En esta página, seleccione las columnas que desea cifrar, [el tipo de cifrado y qué clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) desea usar.</span><span class="sxs-lookup"><span data-stu-id="346fb-187">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="346fb-188">Cifre la información **SSN** y **BirthDate** de cada paciente.</span><span class="sxs-lookup"><span data-stu-id="346fb-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="346fb-189">La columna SSN usará cifrado determinista, que admite búsquedas de igualdad, combinaciones y agrupaciones.</span><span class="sxs-lookup"><span data-stu-id="346fb-189">The SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="346fb-190">La columna BirthDate usará cifrado aleatorio, que no admite operaciones.</span><span class="sxs-lookup"><span data-stu-id="346fb-190">The BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="346fb-191">Establezca el **Tipo de cifrado** de la columna SSN en **Determinista** y la columna BirthDate en **Aleatoria**.</span><span class="sxs-lookup"><span data-stu-id="346fb-191">Set the **Encryption Type** for the SSN column to **Deterministic** and the BirthDate column to **Randomized**.</span></span> <span data-ttu-id="346fb-192">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="346fb-192">Click **Next**.</span></span>

![Cifrar columnas](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="346fb-194">Configuración de la clave maestra</span><span class="sxs-lookup"><span data-stu-id="346fb-194">Master Key Configuration</span></span>
<span data-ttu-id="346fb-195">En la página **Configuración de la clave maestra** se configura la clave maestra de columna (CMK) y se selecciona el proveedor del almacén de claves donde se almacenará la CMK.</span><span class="sxs-lookup"><span data-stu-id="346fb-195">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="346fb-196">Actualmente, puede almacenar una CMK en el almacén de certificados de Windows, en Almacén de claves de Azure o en un módulo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="346fb-196">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="346fb-197">En este tutorial se muestra cómo almacenar las claves en Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="346fb-197">This tutorial shows how to store your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="346fb-198">Seleccione **Almacén de claves de Azure**.</span><span class="sxs-lookup"><span data-stu-id="346fb-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="346fb-199">Seleccione el almacén de claves deseado en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="346fb-199">Select the desired key vault from the drop-down list.</span></span>
3. <span data-ttu-id="346fb-200">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="346fb-200">Click **Next**.</span></span>

![Configuración de la clave maestra](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="346fb-202">Validación</span><span class="sxs-lookup"><span data-stu-id="346fb-202">Validation</span></span>
<span data-ttu-id="346fb-203">Puede cifrar las columnas ahora o guardar un script de PowerShell para ejecutarlo más tarde.</span><span class="sxs-lookup"><span data-stu-id="346fb-203">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="346fb-204">Para este tutorial, seleccione **Continuar para finalizar ahora** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="346fb-204">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="346fb-205">Resumen</span><span class="sxs-lookup"><span data-stu-id="346fb-205">Summary</span></span>
<span data-ttu-id="346fb-206">Compruebe que la configuración sea correcta y haga clic en **Finalizar** para completar la configuración de Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="346fb-206">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![Resumen](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="346fb-208">Comprobación de las acciones del asistente</span><span class="sxs-lookup"><span data-stu-id="346fb-208">Verify the wizard's actions</span></span>
<span data-ttu-id="346fb-209">Una vez finalizado el asistente, la base de datos estará configurada para Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="346fb-209">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="346fb-210">El asistente habrá realizado las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="346fb-210">The wizard performed the following actions:</span></span>

* <span data-ttu-id="346fb-211">Creación de una clave maestra de columna (CMK) y almacenamiento en Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="346fb-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="346fb-212">Creación de una clave de cifrado de columna (CMK) y almacenamiento en Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="346fb-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="346fb-213">Configuración de las columnas seleccionadas para el cifrado.</span><span class="sxs-lookup"><span data-stu-id="346fb-213">Configured the selected columns for encryption.</span></span> <span data-ttu-id="346fb-214">La tabla Patients aún no tiene datos, pero los datos existentes en las columnas seleccionadas ahora están cifrados.</span><span class="sxs-lookup"><span data-stu-id="346fb-214">The Patients table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="346fb-215">Para comprobar la creación de las claves en SSMS, expanda **Clinic** > **Seguridad** > **Claves de Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="346fb-215">You can verify the creation of the keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="346fb-216">Crear una aplicación cliente que funcione con los datos cifrados</span><span class="sxs-lookup"><span data-stu-id="346fb-216">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="346fb-217">Ahora que Always Encrypted está configurado, vamos a crear una aplicación que realice operaciones de *inserción* y *selección* en las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="346fb-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="346fb-218">La aplicación debe usar objetos [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) al pasar datos de texto sin cifrar al servidor con columnas de Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="346fb-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="346fb-219">Se generará una excepción al pasar valores literales sin usar objetos SqlParameter.</span><span class="sxs-lookup"><span data-stu-id="346fb-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="346fb-220">Abra Visual Studio y cree una nueva **Aplicación de consola** de C# (Visual Studio 2015 y versiones anteriores) o una **Aplicación de consola (.NET Framework)** (Visual Studio 2017 y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="346fb-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="346fb-221">Asegúrese de que el proyecto esté establecido en **.NET Framework 4.6** o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="346fb-221">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="346fb-222">Use el nombre **AlwaysEncryptedConsoleAKVApp** para el proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="346fb-222">Name the project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="346fb-223">Instale los siguientes paquetes NuGet; para ello, vaya a**Herramientas** > **Administrador de paquetes NuGet** > **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="346fb-223">Install the following NuGet packages by going to **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="346fb-224">Ejecute estas dos líneas de código en la Consola del Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="346fb-224">Run these two lines of code in the Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="346fb-225">Modificar la cadena de conexión para habilitar Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="346fb-225">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="346fb-226">En esta sección se explica cómo habilitar Always Encrypted en la cadena de conexión de su base de datos.</span><span class="sxs-lookup"><span data-stu-id="346fb-226">This section  explains how to enable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="346fb-227">Para habilitar Always Encrypted, debe agregar la palabra clave **Column Encryption Setting** a la cadena de conexión y establecerla en **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="346fb-227">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="346fb-228">Puede establecerla directamente en la cadena de conexión o mediante [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-228">You can set this directly in the connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="346fb-229">La aplicación de ejemplo de la siguiente sección muestra cómo usar **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="346fb-229">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="346fb-230">Modificar Always Encrypted en la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="346fb-230">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="346fb-231">Agregue la siguiente palabra clave a la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="346fb-231">Add the following keyword to your connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="346fb-232">Habilitar Always Encrypted con SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="346fb-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="346fb-233">El siguiente código muestra cómo habilitar Always Encrypted estableciendo [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) en [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-233">The following code shows how to enable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-the-azure-key-vault-provider"></a><span data-ttu-id="346fb-234">Registro del proveedor de Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="346fb-234">Register the Azure Key Vault provider</span></span>
<span data-ttu-id="346fb-235">El código siguiente muestra cómo registrar el proveedor de Almacén de claves de Azure con el controlador de ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="346fb-235">The following code shows how to register the Azure Key Vault provider with the ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="346fb-236">Aplicación de consola de ejemplo de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="346fb-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="346fb-237">En este ejemplo se muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="346fb-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="346fb-238">Modificar la cadena de conexión para habilitar Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="346fb-238">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="346fb-239">Registrar Almacén de claves de Azure como proveedor de almacén de claves de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="346fb-239">Register Azure Key Vault as the application's key store provider.</span></span>  
* <span data-ttu-id="346fb-240">Insertar datos en las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="346fb-240">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="346fb-241">Seleccionar un registro mediante el filtrado de un valor específico de una columna cifrada.</span><span class="sxs-lookup"><span data-stu-id="346fb-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="346fb-242">Reemplace el contenido de **Program.cs** por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="346fb-242">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="346fb-243">Reemplace la cadena de conexión para la variable global connectionString en la línea directamente anterior al método Main por una cadena de conexión válida desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="346fb-243">Replace the connection string for the global connectionString variable in the line that directly precedes the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="346fb-244">Este es el único cambio que necesita realizar en este código.</span><span class="sxs-lookup"><span data-stu-id="346fb-244">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="346fb-245">Ejecute la aplicación para ver Always Encrypted en acción.</span><span class="sxs-lookup"><span data-stu-id="346fb-245">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"<connection string from the portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed to obtain the access token");
            return result.AccessToken;
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



## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="346fb-246">Comprobación del cifrado de los datos</span><span class="sxs-lookup"><span data-stu-id="346fb-246">Verify that the data is encrypted</span></span>
<span data-ttu-id="346fb-247">Para comprobar rápidamente que los datos reales del servidor están cifrados, podemos consultar los datos de los pacientes con SSMS (mediante la conexión actual en la que el parámetro **Column Encryption Setting** aún no está habilitado).</span><span class="sxs-lookup"><span data-stu-id="346fb-247">You can quickly check that the actual data on the server is encrypted by querying the Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="346fb-248">Ejecute la siguiente consulta en la base de datos Clinic.</span><span class="sxs-lookup"><span data-stu-id="346fb-248">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="346fb-249">Puede ver que las columnas cifradas no contienen datos de texto no cifrado.</span><span class="sxs-lookup"><span data-stu-id="346fb-249">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="346fb-251">Par usar SSMS para obtener acceso a los datos de texto no cifrado, puede agregar el parámetro *Column Encryption Setting=enabled* a la conexión.</span><span class="sxs-lookup"><span data-stu-id="346fb-251">To use SSMS to access the plaintext data, you can add the *Column Encryption Setting=enabled* parameter to the connection.</span></span>

1. <span data-ttu-id="346fb-252">En SSMS, haga clic con el botón derecho en el servidor en el **Explorador de objetos** y elija **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="346fb-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="346fb-253">Haga clic en **Conectar** > **Motor de base de datos** para abrir la ventana **Conectar con el servidor** y haga clic en **Opciones**.</span><span class="sxs-lookup"><span data-stu-id="346fb-253">Click **Connect** > **Database Engine** to open the **Connect to Server** window and click **Options**.</span></span>
3. <span data-ttu-id="346fb-254">Haga clic en **Parámetros de conexión adicionales** y escriba **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="346fb-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="346fb-256">Ejecute la siguiente consulta en la base de datos Clinic.</span><span class="sxs-lookup"><span data-stu-id="346fb-256">Run the following query on the Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="346fb-257">Ahora puede ver los datos de texto no cifrado en las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="346fb-257">You can now see the plaintext data in the encrypted columns.</span></span>

    ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="346fb-259">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="346fb-259">Next steps</span></span>
<span data-ttu-id="346fb-260">Después de crear una base de datos que usa Always Encrypted, es posible que quiera hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="346fb-260">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="346fb-261">[Rotar y limpiar las claves](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="346fb-262">[Migrar los datos que ya están cifrados con Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="346fb-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="346fb-263">Información relacionada</span><span class="sxs-lookup"><span data-stu-id="346fb-263">Related information</span></span>
* [<span data-ttu-id="346fb-264">Always Encrypted (desarrollo de clientes)</span><span class="sxs-lookup"><span data-stu-id="346fb-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="346fb-265">Cifrado de datos transparente</span><span class="sxs-lookup"><span data-stu-id="346fb-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="346fb-266">Cifrado de SQL Server</span><span class="sxs-lookup"><span data-stu-id="346fb-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="346fb-267">Asistente de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="346fb-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="346fb-268">Blog de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="346fb-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

