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
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a>Always Encrypted: protección de datos confidenciales en Base de datos SQL y almacenamiento de las claves de cifrado en Almacén de claves de Azure

Este artículo muestra cómo toosecure datos confidenciales en una instancia de SQL de base de datos con cifrado de datos con hello [Asistente para Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) en [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). También se incluyen instrucciones que le mostrará cómo toostore cada clave de cifrado en el almacén de claves de Azure.

Always Encrypted es una nueva tecnología de cifrado de datos en la base de datos de SQL Azure y SQL Server que ayuda a proteger los datos confidenciales almacenados en el servidor de hello, durante un movimiento entre cliente y servidor, y mientras Hola están en uso. Siempre cifrado garantiza que los datos confidenciales nunca aparecen como texto no cifrado en el sistema de bases de datos de Hola. Después de configurar el cifrado de datos, solo las aplicaciones cliente o servidores de aplicaciones que tienen teclas de acceso toohello pueden tener acceso a datos de texto simple. Para más información, consulte [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx).

Después de configurar toouse de base de datos de hello Always Encrypted, creará una aplicación de cliente en C# con toowork de Visual Studio con datos cifrado de saludo.

Siga los pasos de hello en este artículo y obtenga información acerca de cómo tooset seguridad Always Encrypted para una base de datos de SQL Azure. En este artículo aprenderá cómo hello tooperform siguientes tareas:

* Asistente de Always Encrypted Hola de uso en SSMS toocreate [claves de Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Crear una [clave maestra de columna (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Crear una [clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).
* Crear una tabla de base de datos y cifrar columnas.
* Crear una aplicación que inserta, se selecciona y muestra los datos de columnas de hello cifrado.

## <a name="prerequisites"></a>Requisitos previos
Para este tutorial, necesitará:

* Una cuenta y una suscripción de Azure. Si no tiene una, suscríbase para [una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versión 13.0.700.242 o posterior.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) o posterior (en el equipo de cliente hello).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* [Azure PowerShell](/powershell/azure/overview), versión 1.0 o posterior. Tipo **(Get-Module azure - ListAvailable). Versión** toosee qué versión de PowerShell está ejecutando.

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a>Habilitar el servicio de base de datos SQL de cliente aplicación tooaccess Hola
Debe habilitar el servicio de base de datos SQL de cliente aplicación tooaccess hello mediante la configuración de autenticación necesaria de Hola y Hola adquisición *ClientId* y *secreto* que necesitará tooauthenticate la aplicación en el siguiente código de hello.

1. Abra hello [portal de Azure clásico](http://manage.windowsazure.com).
2. Seleccione **Active Directory** y haga clic en la instancia de Active Directory de Hola que va a usar la aplicación.
3. Haga clic en **Aplicaciones** y luego en **AGREGAR**.
4. Escriba un nombre para la aplicación (por ejemplo: *myClientApp*), seleccione **aplicación WEB**y haga clic en hello flecha toocontinue.
5. Para hello **dirección URL de inicio de sesión** y **APP ID URI** puede escribir una dirección URL válida (por ejemplo, *http://myClientApp*) y continuar.
6. Haga clic en **CONFIGURAR**.
7. Copie el **ID. DE CLIENTE**. (Necesitará este valor en el código más adelante).
8. Hola **claves** sección, seleccione **1 año** de hello **seleccione duración** lista desplegable. (Copiará clave Hola después de guardar en el paso 13.)
9. Desplácese hacia abajo y haga clic en **Agregar aplicación**.
10. Deje **mostrar** establecido demasiado**Microsoft Apps** y seleccione **API de administración de servicios de Microsoft Azure**. Haga clic en hello toocontinue de marca de verificación.
11. Seleccione **tener acceso a la administración de servicios de Azure...**  de hello **permisos delegados** lista desplegable.
12. Haga clic en **GUARDAR**.
13. Después de hello guardar finalice, copie el valor de clave de Hola Hola **claves** sección. (Necesitará este valor en el código más adelante).

## <a name="create-a-key-vault-toostore-your-keys"></a>Crear un almacén de claves toostore las claves
Ahora que se configura la aplicación cliente y tener su ID de cliente, es hora toocreate un almacén de claves y configurar la directiva de acceso para usted y su aplicación pueden acceder a los secretos del almacén de hello (claves de Always Encrypted Hola). Hola *crear*, *obtener*, *lista*, *inicio de sesión*, *comprobar*, *wrapKey*, y *unwrapKey* permisos son necesarios para crear una nueva clave maestra de columna y para configurar el cifrado con SQL Server Management Studio.

Puede crear rápidamente un almacén de claves mediante la ejecución de hello siguiente secuencia de comandos. Para obtener una explicación detallada de estos cmdlets y más información sobre cómo crear y configurar un almacén de claves, consulte [Introducción a Azure Key Vault](../key-vault/key-vault-get-started.md).

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




## <a name="create-a-blank-sql-database"></a>Crear una instancia en blanco en SQL Database
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Vaya demasiado**New** > **datos + almacenamiento** > **base de datos SQL**.
3. Cree una base de datos **en blanco** denominada **Clinic** en un servidor nuevo o existente. Para obtener instrucciones detalladas sobre cómo toocreate una base de datos en hello portal de Azure, vea [la primera base de datos de SQL Azure](sql-database-get-started-portal.md).
   
    ![Crear una base de datos en blanco](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

Se necesita Hola cadena de conexión más adelante en el tutorial de hello, por lo que después de crear la base de datos de hello, busque toohello nueva Clinic base de datos y copia Hola cadena de conexión. Puede obtener la cadena de conexión de Hola en cualquier momento, pero resulta fácil toocopy en hello portal de Azure.

1. Vaya demasiado**bases de datos SQL** > **Clinic** > **mostrar cadenas de conexión de base de datos**.
2. Copie la cadena de conexión de Hola para **ADO.NET**.
   
    ![Copie la cadena de conexión de Hola](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Conectar la base de datos de toohello con SSMS
Abra SSMS y conecte el servidor de toohello con base de datos de hello Clinic.

1. Abra SSMS. (Vaya demasiado**conectar** > **motor de base de datos** tooopen hello **conectar tooServer** ventana si no está abierto.)
2. Escriba su nombre del servidor y las credenciales. nombre del servidor Hello puede encontrarse en la hoja de base de datos SQL de Hola y de cadena de conexión de Hola copió anteriormente. Nombre completo del servidor de tipo hello, incluidos los *database.windows.net*.
   
    ![Copie la cadena de conexión de Hola](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

Si hello **nueva regla de Firewall** ventana se abre, inicie sesión en tooAzure y SSMS permiten crear una nueva regla de firewall para usted.

## <a name="create-a-table"></a>Creación de una tabla
En esta sección, creará un paciente de datos de toohold tabla. No es inicialmente cifra--que va a configurar el cifrado en la sección siguiente de Hola.

1. Expanda **Bases de datos**.
2. Menú contextual hello **Clinic** la base de datos y haga clic en **nueva consulta**.
3. Hola pegar después de Transact-SQL (T-SQL) en la nueva ventana de consulta de Hola y **Execute** lo.

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


## <a name="encrypt-columns-configure-always-encrypted"></a>Cifrado de columnas (configurar Always Encrypted)
SSMS proporciona a un asistente que le ayuda a configurar Always Encrypted fácilmente mediante la configuración de la clave maestra de columna de hello, clave de cifrado de columna y las columnas cifradas para usted.

1. Expandaa **Bases de datos** > **Clinic** > **Tablas**.
2. Menú contextual hello **pacientes** de tabla y seleccione **cifrar columnas** Asistente para Always Encrypted de tooopen Hola:
   
    ![Cifrar columnas](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

Asistente para Always Encrypted Hello incluye hello las secciones siguientes: **selección de columna**, **Master Key Configuration**, **validación**, y **resumen** .

### <a name="column-selection"></a>Selección de columnas
Haga clic en **siguiente** en hello **Introducción** Hola de página tooopen **selección de columna** página. En esta página, seleccionará las columnas que desee tooencrypt, [Hola tipo de cifrado y qué clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Cifre la información **SSN** y **BirthDate** de cada paciente. columna de Hello SSN usará el cifrado determinista, que admite búsquedas de igualdad, combinaciones y group by. columna de fecha de nacimiento de Hello usará el cifrado aleatorio, que no admite las operaciones.

Conjunto hello **tipo de cifrado** de columna Hola SSN demasiado**Deterministic** y Hola columna BirthDate demasiado**aleatorio**. Haga clic en **Siguiente**.

![Cifrar columnas](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a>Configuración de la clave maestra
Hola **Master Key Configuration** página es donde se configura la las CMK y el proveedor de almacén de claves de hello seleccione hello CMK se almacenarán. Actualmente, puede almacenar una CMK de almacén de certificados de Windows hello, almacén de claves de Azure o un módulo de seguridad de hardware (HSM).

Este tutorial se muestra cómo toostore las claves en el almacén de claves de Azure.

1. Seleccione **Almacén de claves de Azure**.
2. Seleccione el almacén de claves deseado Hola de lista desplegable de Hola.
3. Haga clic en **Siguiente**.

![Configuración de la clave maestra](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a>Validación
Puede cifrar columnas Hola ahora o guardar una toorun de secuencia de comandos de PowerShell más adelante. Para este tutorial, seleccione **continuar ahora toofinish** y haga clic en **siguiente**.

### <a name="summary"></a>Resumen
Compruebe que configuración de hello es correctos y haga clic en **finalizar** el programa de instalación hello toocomplete para Always Encrypted.

![Resumen](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a>Comprobar acciones del Asistente de Hola
Una vez finalizado el Asistente de hello, la base de datos se configura para Always Encrypted. Asistente para realizar de Hola Hola siguientes acciones:

* Creación de una clave maestra de columna (CMK) y almacenamiento en Almacén de claves de Azure.
* Creación de una clave de cifrado de columna (CMK) y almacenamiento en Almacén de claves de Azure.
* Hola configurado seleccionado columnas para el cifrado. tabla de pacientes Hello no tiene actualmente ningún dato, pero ahora se cifran los datos existentes en las columnas de hello seleccionado.

Puede comprobar la creación de hello de claves de hello en SSMS expandiendo **Clinic** > **seguridad** > **Always Encrypted Keys**.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Crear una aplicación cliente que funciona con datos cifrado de saludo
Ahora que Always Encrypted está configurado, puede compilar una aplicación que realiza *inserta* y *selecciona* en hello las columnas cifradas.  

> [!IMPORTANT]
> La aplicación debe utilizar [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objetos al pasar el servidor de toohello de datos de texto simple con columnas siempre cifradas. Se generará una excepción al pasar valores literales sin usar objetos SqlParameter.
> 
> 

1. Abra Visual Studio y cree una nueva **Aplicación de consola** de C# (Visual Studio 2015 y versiones anteriores) o una **Aplicación de consola (.NET Framework)** (Visual Studio 2017 y versiones posteriores). Asegúrese de que el proyecto se establece demasiado**.NET Framework 4.6** o una versión posterior.
2. Proyecto de hello Name **AlwaysEncryptedConsoleAKVApp** y haga clic en **Aceptar**.
3. Instalar Hola siguientes paquetes de NuGet yendo demasiado**herramientas** > **Administrador de paquetes de NuGet** > **Package Manager Console**.

Ejecute estas dos líneas de código en la consola de administrador de paquetes de saludo.

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modificar su tooenable de cadena de conexión Always Encrypted
Esta sección se explica cómo tooenable siempre cifrado en la cadena de conexión de base de datos.

tooenable Always Encrypted, necesita hello tooadd **Column Encryption Setting** conexión tooyour de palabra clave de cadena y establézcalo demasiado**habilitado**.

Puede establecer directamente en la cadena de conexión de hello, o se puede establecer mediante [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). aplicación de ejemplo de Hola Hola siguiente sección se muestra cómo toouse **SqlConnectionStringBuilder**.

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Habilitar Always Encrypted en la cadena de conexión de Hola
Agregar Hola después de la cadena de conexión de palabra clave tooyour.

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a>Habilitar Always Encrypted con SqlConnectionStringBuilder
Hola el siguiente código muestra cómo tooenable Always Encrypted estableciendo [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) demasiado[habilitado](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a>Registrar proveedor de almacén de claves de Azure Hola
Hello código siguiente muestra cómo tooregister Hola proveedor de almacén de claves de Azure con controlador ADO.NET Hola.

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



## <a name="always-encrypted-sample-console-application"></a>Aplicación de consola de ejemplo de Always Encrypted
En este ejemplo se muestra cómo:

* Modifique su tooenable de cadena de conexión siempre se cifran.
* Registrar el almacén de claves de Azure como Hola proveedor de almacén de claves de la aplicación.  
* Insertar datos en columnas de hello cifrado.
* Seleccionar un registro mediante el filtrado de un valor específico de una columna cifrada.

Reemplace el contenido de Hola de **Program.cs** con el siguiente código de hello. Reemplace la cadena de conexión de hello para la variable global connectionString de hello en línea hello que precede directamente el método Main de hello con la cadena de conexión válida de hello portal de Azure. Se trata de hello cambio solo se necesita toomake toothis código.

Ejecutar toosee de aplicación Hola Always Encrypted en acción.

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



## <a name="verify-that-hello-data-is-encrypted"></a>Compruebe que se cifren los datos de Hola
Puede comprobar fácilmente que se cifran datos reales de hello en servidor hello consultando los datos de los pacientes Hola con SSMS (mediante la conexión actual donde **Column Encryption Setting** todavía no está habilitado).

Ejecute hello después de consulta en la base de datos de hello Clinic.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Puede ver que columnas Hola cifra no contienen los datos de texto simple.

   ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

toouse SSMS tooaccess Hola datos de texto simple, puede agregar hello *Column Encryption Setting = habilitado* conexión toohello de parámetro.

1. En SSMS, haga clic con el botón derecho en el servidor en el **Explorador de objetos** y elija **Desconectar**.
2. Haga clic en **conectar** > **motor de base de datos** tooopen hello **conectar tooServer** ventana y haga clic en **opciones**.
3. Haga clic en **Parámetros de conexión adicionales** y escriba **Column Encryption Setting=enabled**.
   
    ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. Ejecute hello después de consulta en la base de datos de hello Clinic.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Ahora puede ver datos de texto simple de hello en columnas de hello cifrado.

    ![Nueva aplicación de consola](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a>Pasos siguientes
Después de crear una base de datos que usa Always Encrypted, puede que desee siguiente de Hola toodo:

* [Rotar y limpiar las claves](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migrar los datos que ya están cifrados con Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).

## <a name="related-information"></a>Información relacionada
* [Always Encrypted (desarrollo de clientes)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Cifrado de datos transparente](https://msdn.microsoft.com/library/bb934049.aspx)
* [Cifrado de SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Asistente de Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog de Always Encrypted](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

