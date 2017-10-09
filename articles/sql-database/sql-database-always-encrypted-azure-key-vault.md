---
title: 'Always Encrypted: SQL Database: Azure Key Vault | Microsoft Docs'
description: "Este artículo muestra cómo toosecure datos confidenciales en una base de datos SQL con el uso de cifrado de datos Hola a Asistente para Always Encrypted en SQL Server Management Studio. También se incluyen instrucciones que le mostrará cómo toostore cada clave de cifrado en el almacén de claves de Azure."
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
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="bf861-105">Always Encrypted: protección de datos confidenciales en Base de datos SQL y almacenamiento de las claves de cifrado en Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="bf861-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="bf861-106">Este artículo muestra cómo toosecure datos confidenciales en una instancia de SQL de base de datos con cifrado de datos con hello [Asistente para Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) en [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="bf861-107">También se incluyen instrucciones que le mostrará cómo toostore cada clave de cifrado en el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf861-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="bf861-108">Always Encrypted es una nueva tecnología de cifrado de datos en la base de datos de SQL Azure y SQL Server que ayuda a proteger los datos confidenciales almacenados en el servidor de hello, durante un movimiento entre cliente y servidor, y mientras Hola están en uso.</span><span class="sxs-lookup"><span data-stu-id="bf861-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="bf861-109">Siempre cifrado garantiza que los datos confidenciales nunca aparecen como texto no cifrado en el sistema de bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf861-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="bf861-110">Después de configurar el cifrado de datos, solo las aplicaciones cliente o servidores de aplicaciones que tienen teclas de acceso toohello pueden tener acceso a datos de texto simple.</span><span class="sxs-lookup"><span data-stu-id="bf861-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="bf861-111">Para más información, consulte [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="bf861-112">Después de configurar toouse de base de datos de hello Always Encrypted, creará una aplicación de cliente en C# con toowork de Visual Studio con datos cifrado de saludo.</span><span class="sxs-lookup"><span data-stu-id="bf861-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="bf861-113">Siga los pasos de hello en este artículo y obtenga información acerca de cómo tooset seguridad Always Encrypted para una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bf861-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="bf861-114">En este artículo aprenderá cómo hello tooperform siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="bf861-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="bf861-115">Asistente de Always Encrypted Hola de uso en SSMS toocreate [claves de Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="bf861-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="bf861-116">Crear una [clave maestra de columna (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="bf861-117">Crear una [clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="bf861-118">Crear una tabla de base de datos y cifrar columnas.</span><span class="sxs-lookup"><span data-stu-id="bf861-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="bf861-119">Crear una aplicación que inserta, se selecciona y muestra los datos de columnas de hello cifrado.</span><span class="sxs-lookup"><span data-stu-id="bf861-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf861-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bf861-120">Prerequisites</span></span>
<span data-ttu-id="bf861-121">Para este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="bf861-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="bf861-122">Una cuenta y una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf861-122">An Azure account and subscription.</span></span> <span data-ttu-id="bf861-123">Si no tiene una, suscríbase para [una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf861-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bf861-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versión 13.0.700.242 o posterior.</span><span class="sxs-lookup"><span data-stu-id="bf861-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="bf861-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o posterior (en el equipo de cliente hello).</span><span class="sxs-lookup"><span data-stu-id="bf861-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="bf861-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="bf861-127">[Azure PowerShell](/powershell/azure/overview), versión 1.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="bf861-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="bf861-128">Tipo **(Get-Module azure - ListAvailable). Versión** toosee qué versión de PowerShell está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="bf861-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="bf861-129">Habilitar el servicio de base de datos SQL de cliente aplicación tooaccess Hola</span><span class="sxs-lookup"><span data-stu-id="bf861-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="bf861-130">Debe habilitar el servicio de base de datos SQL de cliente aplicación tooaccess hello mediante la configuración de autenticación necesaria de Hola y Hola adquisición *ClientId* y *secreto* que necesitará tooauthenticate la aplicación en el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="bf861-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="bf861-131">Abra hello [portal de Azure clásico](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bf861-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bf861-132">Seleccione **Active Directory** y haga clic en la instancia de Active Directory de Hola que va a usar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf861-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="bf861-133">Haga clic en **Aplicaciones** y luego en **AGREGAR**.</span><span class="sxs-lookup"><span data-stu-id="bf861-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="bf861-134">Escriba un nombre para la aplicación (por ejemplo: *myClientApp*), seleccione **aplicación WEB**y haga clic en hello flecha toocontinue.</span><span class="sxs-lookup"><span data-stu-id="bf861-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="bf861-135">Para hello **dirección URL de inicio de sesión** y **APP ID URI** puede escribir una dirección URL válida (por ejemplo, *http://myClientApp*) y continuar.</span><span class="sxs-lookup"><span data-stu-id="bf861-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="bf861-136">Haga clic en **CONFIGURAR**.</span><span class="sxs-lookup"><span data-stu-id="bf861-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="bf861-137">Copie el **ID. DE CLIENTE**.</span><span class="sxs-lookup"><span data-stu-id="bf861-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="bf861-138">(Necesitará este valor en el código más adelante).</span><span class="sxs-lookup"><span data-stu-id="bf861-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="bf861-139">Hola **claves** sección, seleccione **1 año** de hello **seleccione duración** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="bf861-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="bf861-140">(Copiará clave Hola después de guardar en el paso 13.)</span><span class="sxs-lookup"><span data-stu-id="bf861-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="bf861-141">Desplácese hacia abajo y haga clic en **Agregar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="bf861-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="bf861-142">Deje **mostrar** establecido demasiado**Microsoft Apps** y seleccione **API de administración de servicios de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="bf861-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="bf861-143">Haga clic en hello toocontinue de marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="bf861-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="bf861-144">Seleccione **tener acceso a la administración de servicios de Azure...**  de hello **permisos delegados** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="bf861-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="bf861-145">Haga clic en **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="bf861-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="bf861-146">Después de hello guardar finalice, copie el valor de clave de Hola Hola **claves** sección.</span><span class="sxs-lookup"><span data-stu-id="bf861-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="bf861-147">(Necesitará este valor en el código más adelante).</span><span class="sxs-lookup"><span data-stu-id="bf861-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="bf861-148">Crear un almacén de claves toostore las claves</span><span class="sxs-lookup"><span data-stu-id="bf861-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="bf861-149">Ahora que se configura la aplicación cliente y tener su ID de cliente, es hora toocreate un almacén de claves y configurar la directiva de acceso para usted y su aplicación pueden acceder a los secretos del almacén de hello (claves de Always Encrypted Hola).</span><span class="sxs-lookup"><span data-stu-id="bf861-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="bf861-150">Hola *crear*, *obtener*, *lista*, *inicio de sesión*, *comprobar*, *wrapKey*, y *unwrapKey* permisos son necesarios para crear una nueva clave maestra de columna y para configurar el cifrado con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="bf861-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="bf861-151">Puede crear rápidamente un almacén de claves mediante la ejecución de hello siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="bf861-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="bf861-152">Para obtener una explicación detallada de estos cmdlets y más información sobre cómo crear y configurar un almacén de claves, consulte [Introducción a Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bf861-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

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




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="bf861-153">Crear una instancia en blanco en SQL Database</span><span class="sxs-lookup"><span data-stu-id="bf861-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="bf861-154">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bf861-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bf861-155">Vaya demasiado**New** > **datos + almacenamiento** > **base de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="bf861-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="bf861-156">Cree una base de datos **en blanco** denominada **Clinic** en un servidor nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="bf861-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="bf861-157">Para obtener instrucciones detalladas sobre cómo toocreate una base de datos en hello portal de Azure, vea [la primera base de datos de SQL Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bf861-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Crear una base de datos en blanco](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="bf861-159">Se necesita Hola cadena de conexión más adelante en el tutorial de hello, por lo que después de crear la base de datos de hello, busque toohello nueva Clinic base de datos y copia Hola cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="bf861-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="bf861-160">Puede obtener la cadena de conexión de Hola en cualquier momento, pero resulta fácil toocopy en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf861-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="bf861-161">Vaya demasiado**bases de datos SQL** > **Clinic** > **mostrar cadenas de conexión de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="bf861-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="bf861-162">Copie la cadena de conexión de Hola para **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="bf861-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Copie la cadena de conexión de Hola](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="bf861-164">Conectar la base de datos de toohello con SSMS</span><span class="sxs-lookup"><span data-stu-id="bf861-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="bf861-165">Abra SSMS y conecte el servidor de toohello con base de datos de hello Clinic.</span><span class="sxs-lookup"><span data-stu-id="bf861-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="bf861-166">Abra SSMS.</span><span class="sxs-lookup"><span data-stu-id="bf861-166">Open SSMS.</span></span> <span data-ttu-id="bf861-167">(Vaya demasiado**conectar** > **motor de base de datos** tooopen hello **conectar tooServer** ventana si no está abierto.)</span><span class="sxs-lookup"><span data-stu-id="bf861-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="bf861-168">Escriba su nombre del servidor y las credenciales.</span><span class="sxs-lookup"><span data-stu-id="bf861-168">Enter your server name and credentials.</span></span> <span data-ttu-id="bf861-169">nombre del servidor Hello puede encontrarse en la hoja de base de datos SQL de Hola y de cadena de conexión de Hola copió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bf861-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="bf861-170">Nombre completo del servidor de tipo hello, incluidos los *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="bf861-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![Copie la cadena de conexión de Hola](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="bf861-172">Si hello **nueva regla de Firewall** ventana se abre, inicie sesión en tooAzure y SSMS permiten crear una nueva regla de firewall para usted.</span><span class="sxs-lookup"><span data-stu-id="bf861-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="bf861-173">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="bf861-173">Create a table</span></span>
<span data-ttu-id="bf861-174">En esta sección, creará un paciente de datos de toohold tabla.</span><span class="sxs-lookup"><span data-stu-id="bf861-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="bf861-175">No es inicialmente cifra--que va a configurar el cifrado en la sección siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf861-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="bf861-176">Expanda **Bases de datos**.</span><span class="sxs-lookup"><span data-stu-id="bf861-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="bf861-177">Menú contextual hello **Clinic** la base de datos y haga clic en **nueva consulta**.</span><span class="sxs-lookup"><span data-stu-id="bf861-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="bf861-178">Hola pegar después de Transact-SQL (T-SQL) en la nueva ventana de consulta de Hola y **Execute** lo.</span><span class="sxs-lookup"><span data-stu-id="bf861-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="bf861-179">Cifrado de columnas (configurar Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="bf861-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="bf861-180">SSMS proporciona a un asistente que le ayuda a configurar Always Encrypted fácilmente mediante la configuración de la clave maestra de columna de hello, clave de cifrado de columna y las columnas cifradas para usted.</span><span class="sxs-lookup"><span data-stu-id="bf861-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="bf861-181">Expandaa **Bases de datos** > **Clinic** > **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="bf861-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="bf861-182">Menú contextual hello **pacientes** de tabla y seleccione **cifrar columnas** Asistente para Always Encrypted de tooopen Hola:</span><span class="sxs-lookup"><span data-stu-id="bf861-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Cifrar columnas](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="bf861-184">Asistente para Always Encrypted Hello incluye hello las secciones siguientes: **selección de columna**, **Master Key Configuration**, **validación**, y **resumen** .</span><span class="sxs-lookup"><span data-stu-id="bf861-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="bf861-185">Selección de columnas</span><span class="sxs-lookup"><span data-stu-id="bf861-185">Column Selection</span></span>
<span data-ttu-id="bf861-186">Haga clic en **siguiente** en hello **Introducción** Hola de página tooopen **selección de columna** página.</span><span class="sxs-lookup"><span data-stu-id="bf861-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="bf861-187">En esta página, seleccionará las columnas que desee tooencrypt, [Hola tipo de cifrado y qué clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="bf861-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="bf861-188">Cifre la información **SSN** y **BirthDate** de cada paciente.</span><span class="sxs-lookup"><span data-stu-id="bf861-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="bf861-189">columna de Hello SSN usará el cifrado determinista, que admite búsquedas de igualdad, combinaciones y group by.</span><span class="sxs-lookup"><span data-stu-id="bf861-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="bf861-190">columna de fecha de nacimiento de Hello usará el cifrado aleatorio, que no admite las operaciones.</span><span class="sxs-lookup"><span data-stu-id="bf861-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="bf861-191">Conjunto hello **tipo de cifrado** de columna Hola SSN demasiado**Deterministic** y Hola columna BirthDate demasiado**aleatorio**.</span><span class="sxs-lookup"><span data-stu-id="bf861-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="bf861-192">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bf861-192">Click **Next**.</span></span>

![Cifrar columnas](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="bf861-194">Configuración de la clave maestra</span><span class="sxs-lookup"><span data-stu-id="bf861-194">Master Key Configuration</span></span>
<span data-ttu-id="bf861-195">Hola **Master Key Configuration** página es donde se configura la las CMK y el proveedor de almacén de claves de hello seleccione hello CMK se almacenarán.</span><span class="sxs-lookup"><span data-stu-id="bf861-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="bf861-196">Actualmente, puede almacenar una CMK de almacén de certificados de Windows hello, almacén de claves de Azure o un módulo de seguridad de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="bf861-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="bf861-197">Este tutorial se muestra cómo toostore las claves en el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf861-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="bf861-198">Seleccione **Almacén de claves de Azure**.</span><span class="sxs-lookup"><span data-stu-id="bf861-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="bf861-199">Seleccione el almacén de claves deseado Hola de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf861-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="bf861-200">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bf861-200">Click **Next**.</span></span>

![Configuración de la clave maestra](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="bf861-202">Validación</span><span class="sxs-lookup"><span data-stu-id="bf861-202">Validation</span></span>
<span data-ttu-id="bf861-203">Puede cifrar columnas Hola ahora o guardar una toorun de secuencia de comandos de PowerShell más adelante.</span><span class="sxs-lookup"><span data-stu-id="bf861-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="bf861-204">Para este tutorial, seleccione **continuar ahora toofinish** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bf861-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="bf861-205">Resumen</span><span class="sxs-lookup"><span data-stu-id="bf861-205">Summary</span></span>
<span data-ttu-id="bf861-206">Compruebe que configuración de hello es correctos y haga clic en **finalizar** el programa de instalación hello toocomplete para Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="bf861-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Resumen](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="bf861-208">Comprobar acciones del Asistente de Hola</span><span class="sxs-lookup"><span data-stu-id="bf861-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="bf861-209">Una vez finalizado el Asistente de hello, la base de datos se configura para Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="bf861-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="bf861-210">Asistente para realizar de Hola Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="bf861-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="bf861-211">Creación de una clave maestra de columna (CMK) y almacenamiento en Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf861-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="bf861-212">Creación de una clave de cifrado de columna (CMK) y almacenamiento en Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf861-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="bf861-213">Hola configurado seleccionado columnas para el cifrado.</span><span class="sxs-lookup"><span data-stu-id="bf861-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="bf861-214">tabla de pacientes Hello no tiene actualmente ningún dato, pero ahora se cifran los datos existentes en las columnas de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="bf861-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="bf861-215">Puede comprobar la creación de hello de claves de hello en SSMS expandiendo **Clinic** > **seguridad** > **Always Encrypted Keys**.</span><span class="sxs-lookup"><span data-stu-id="bf861-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="bf861-216">Crear una aplicación cliente que funciona con datos cifrado de saludo</span><span class="sxs-lookup"><span data-stu-id="bf861-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="bf861-217">Ahora que Always Encrypted está configurado, puede compilar una aplicación que realiza *inserta* y *selecciona* en hello las columnas cifradas.</span><span class="sxs-lookup"><span data-stu-id="bf861-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="bf861-218">La aplicación debe utilizar [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objetos al pasar el servidor de toohello de datos de texto simple con columnas siempre cifradas.</span><span class="sxs-lookup"><span data-stu-id="bf861-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="bf861-219">Se generará una excepción al pasar valores literales sin usar objetos SqlParameter.</span><span class="sxs-lookup"><span data-stu-id="bf861-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="bf861-220">Abra Visual Studio y cree una nueva **Aplicación de consola** de C# (Visual Studio 2015 y versiones anteriores) o una **Aplicación de consola (.NET Framework)** (Visual Studio 2017 y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="bf861-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="bf861-221">Asegúrese de que el proyecto se establece demasiado**.NET Framework 4.6** o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="bf861-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="bf861-222">Proyecto de hello Name **AlwaysEncryptedConsoleAKVApp** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bf861-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="bf861-223">Instalar Hola siguientes paquetes de NuGet yendo demasiado**herramientas** > **Administrador de paquetes de NuGet** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="bf861-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="bf861-224">Ejecute estas dos líneas de código en la consola de administrador de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="bf861-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="bf861-225">Modificar su tooenable de cadena de conexión Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="bf861-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="bf861-226">Esta sección se explica cómo tooenable siempre cifrado en la cadena de conexión de base de datos.</span><span class="sxs-lookup"><span data-stu-id="bf861-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="bf861-227">tooenable Always Encrypted, necesita hello tooadd **Column Encryption Setting** conexión tooyour de palabra clave de cadena y establézcalo demasiado**habilitado**.</span><span class="sxs-lookup"><span data-stu-id="bf861-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="bf861-228">Puede establecer directamente en la cadena de conexión de hello, o se puede establecer mediante [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="bf861-229">aplicación de ejemplo de Hola Hola siguiente sección se muestra cómo toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="bf861-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="bf861-230">Habilitar Always Encrypted en la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="bf861-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="bf861-231">Agregar Hola después de la cadena de conexión de palabra clave tooyour.</span><span class="sxs-lookup"><span data-stu-id="bf861-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="bf861-232">Habilitar Always Encrypted con SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="bf861-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="bf861-233">Hola el siguiente código muestra cómo tooenable Always Encrypted estableciendo [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) demasiado[habilitado](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="bf861-234">Registrar proveedor de almacén de claves de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="bf861-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="bf861-235">Hello código siguiente muestra cómo tooregister Hola proveedor de almacén de claves de Azure con controlador ADO.NET Hola.</span><span class="sxs-lookup"><span data-stu-id="bf861-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

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



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="bf861-236">Aplicación de consola de ejemplo de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="bf861-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="bf861-237">En este ejemplo se muestra cómo:</span><span class="sxs-lookup"><span data-stu-id="bf861-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="bf861-238">Modifique su tooenable de cadena de conexión siempre se cifran.</span><span class="sxs-lookup"><span data-stu-id="bf861-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="bf861-239">Registrar el almacén de claves de Azure como Hola proveedor de almacén de claves de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf861-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="bf861-240">Insertar datos en columnas de hello cifrado.</span><span class="sxs-lookup"><span data-stu-id="bf861-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="bf861-241">Seleccionar un registro mediante el filtrado de un valor específico de una columna cifrada.</span><span class="sxs-lookup"><span data-stu-id="bf861-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="bf861-242">Reemplace el contenido de Hola de **Program.cs** con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="bf861-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="bf861-243">Reemplace la cadena de conexión de hello para la variable global connectionString de hello en línea hello que precede directamente el método Main de hello con la cadena de conexión válida de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf861-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="bf861-244">Se trata de hello cambio solo se necesita toomake toothis código.</span><span class="sxs-lookup"><span data-stu-id="bf861-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="bf861-245">Ejecutar toosee de aplicación Hola Always Encrypted en acción.</span><span class="sxs-lookup"><span data-stu-id="bf861-245">Run hello app toosee Always Encrypted in action.</span></span>

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
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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
                throw new InvalidOperationException("Failed tooobtain hello access token");
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



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="bf861-246">Compruebe que se cifren los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="bf861-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="bf861-247">Puede comprobar fácilmente que se cifran datos reales de hello en servidor hello consultando los datos de los pacientes Hola con SSMS (mediante la conexión actual donde **Column Encryption Setting** todavía no está habilitado).</span><span class="sxs-lookup"><span data-stu-id="bf861-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="bf861-248">Ejecute hello después de consulta en la base de datos de hello Clinic.</span><span class="sxs-lookup"><span data-stu-id="bf861-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="bf861-249">Puede ver que columnas Hola cifra no contienen los datos de texto simple.</span><span class="sxs-lookup"><span data-stu-id="bf861-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="bf861-251">toouse SSMS tooaccess Hola datos de texto simple, puede agregar hello *Column Encryption Setting = habilitado* conexión toohello de parámetro.</span><span class="sxs-lookup"><span data-stu-id="bf861-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="bf861-252">En SSMS, haga clic con el botón derecho en el servidor en el **Explorador de objetos** y elija **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="bf861-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="bf861-253">Haga clic en **conectar** > **motor de base de datos** tooopen hello **conectar tooServer** ventana y haga clic en **opciones**.</span><span class="sxs-lookup"><span data-stu-id="bf861-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="bf861-254">Haga clic en **Parámetros de conexión adicionales** y escriba **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="bf861-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="bf861-256">Ejecute hello después de consulta en la base de datos de hello Clinic.</span><span class="sxs-lookup"><span data-stu-id="bf861-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="bf861-257">Ahora puede ver datos de texto simple de hello en columnas de hello cifrado.</span><span class="sxs-lookup"><span data-stu-id="bf861-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="bf861-259">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf861-259">Next steps</span></span>
<span data-ttu-id="bf861-260">Después de crear una base de datos que usa Always Encrypted, puede que desee siguiente de Hola toodo:</span><span class="sxs-lookup"><span data-stu-id="bf861-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="bf861-261">[Rotar y limpiar las claves](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="bf861-262">[Migrar los datos que ya están cifrados con Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf861-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="bf861-263">Información relacionada</span><span class="sxs-lookup"><span data-stu-id="bf861-263">Related information</span></span>
* [<span data-ttu-id="bf861-264">Always Encrypted (desarrollo de clientes)</span><span class="sxs-lookup"><span data-stu-id="bf861-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="bf861-265">Cifrado de datos transparente</span><span class="sxs-lookup"><span data-stu-id="bf861-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="bf861-266">Cifrado de SQL Server</span><span class="sxs-lookup"><span data-stu-id="bf861-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="bf861-267">Asistente de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="bf861-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="bf861-268">Blog de Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="bf861-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

