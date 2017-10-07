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
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>Always Encrypted: Proteger los datos confidenciales en la base de datos SQL y almacenar las claves de cifrado en el almacén de certificados de Windows hello

Este artículo muestra cómo toosecure datos confidenciales en una instancia de SQL de base de datos con el cifrado de base de datos mediante el uso de hello [Asistente para Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) en [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). También muestra cómo toostore las claves de cifrado en los certificados de Windows hello almacenan.

Always Encrypted es una nueva tecnología de cifrado de datos en la base de datos de SQL Azure y SQL Server que ayuda a proteger los datos confidenciales almacenados en el servidor de hello, durante el movimiento entre cliente y servidor y garantizar que los datos confidenciales nunca aparece mientras Hola están en uso, como texto no cifrado en el sistema de bases de datos de Hola. Después de cifrar datos, solo las aplicaciones cliente o servidores de aplicaciones que tienen teclas de acceso toohello pueden tener acceso a datos de texto simple. Para más información, consulte [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx).

Después de configurar toouse de base de datos de hello Always Encrypted, creará una aplicación de cliente en C# con toowork de Visual Studio con datos cifrado de saludo.

Siga los pasos de hello en este artículo toolearn cómo tooset seguridad Always Encrypted para una base de datos de SQL Azure. En este artículo, aprenderá cómo hello tooperform siguientes tareas:

* Asistente de Always Encrypted Hola de uso en SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
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

## <a name="create-a-blank-sql-database"></a>Crear una instancia en blanco en SQL Database
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **Nuevo** > **Datos y almacenamiento** > **SQL Database**.
3. Cree una base de datos **en blanco** denominada **Clinic** en un servidor nuevo o existente. Para obtener instrucciones detalladas sobre cómo crear una base de datos en hello portal de Azure, consulte [la primera base de datos de SQL Azure](sql-database-get-started-portal.md).
   
    ![Crear una base de datos en blanco](./media/sql-database-always-encrypted/create-database.png)

Necesitará la cadena de conexión de hello más adelante en el tutorial Hola. Después de crea la base de datos de hello, vaya toohello nueva Clinic base de datos y copia Hola cadena de conexión. Puede obtener la cadena de conexión de Hola en cualquier momento, pero resulta fácil toocopy cuando se encuentra en hello portal de Azure.

1. Haga clic en **Bases de datos SQL** > **Clinic** > **Mostrar las cadenas de conexión de la base de datos**.
2. Copie la cadena de conexión de Hola para **ADO.NET**.
   
    ![Copie la cadena de conexión de Hola](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Conectar la base de datos de toohello con SSMS
Abra SSMS y conecte el servidor de toohello con base de datos de hello Clinic.

1. Abra SSMS. (Haga clic en **conectar** > **motor de base de datos** tooopen hello **conectar tooServer** ventana si no está abierto).
2. Escriba su nombre del servidor y las credenciales. nombre del servidor Hello puede encontrarse en la hoja de base de datos SQL de Hola y de cadena de conexión de Hola copió anteriormente. Tipo hello servidor completo nombre incluidos *database.windows.net*.
   
    ![Copie la cadena de conexión de Hola](./media/sql-database-always-encrypted/ssms-connect.png)

Si hello **nueva regla de Firewall** ventana se abre, inicie sesión en tooAzure y SSMS permiten crear una nueva regla de firewall para usted.

## <a name="create-a-table"></a>Creación de una tabla
En esta sección, creará un paciente de datos de toohold tabla. Se trata de una tabla normal inicialmente--que va a configurar el cifrado en la sección siguiente Hola.

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
SSMS proporciona un asistente tooeasily configurar Always Encrypted mediante la configuración de hello CMK, CEK y las columnas cifradas para usted.

1. Expandaa **Bases de datos** > **Clinic** > **Tablas**.
2. Menú contextual hello **pacientes** de tabla y seleccione **cifrar columnas** Asistente para Always Encrypted de tooopen Hola:
   
    ![Cifrar columnas](./media/sql-database-always-encrypted/encrypt-columns.png)

Asistente para Always Encrypted Hello incluye hello las secciones siguientes: **selección de columna**, **Master Key Configuration** (CMK), **validación**, y  **Resumen de**.

### <a name="column-selection"></a>Selección de columnas
Haga clic en **siguiente** en hello **Introducción** Hola de página tooopen **selección de columna** página. En esta página, seleccionará las columnas que desee tooencrypt, [Hola tipo de cifrado y qué clave de cifrado de columna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Cifre la información **SSN** y **BirthDate** de cada paciente. Hola **SSN** columna usará el cifrado determinista, que admite búsquedas de igualdad, combinaciones y group by. Hola **BirthDate** va a usar el cifrado aleatorio, que no admite operaciones de columna.

Conjunto hello **tipo de cifrado** para hello **SSN** columna demasiado**Deterministic** hello y **BirthDate** columna demasiado **Aleatorio**. Haga clic en **Siguiente**.

![Cifrar columnas](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>Configuración de la clave maestra
Hola **Master Key Configuration** página es donde se configura la las CMK y el proveedor de almacén de claves de hello seleccione hello CMK se almacenarán. Actualmente, puede almacenar una CMK de almacén de certificados de Windows hello, almacén de claves de Azure o un módulo de seguridad de hardware (HSM). Este tutorial muestra cómo toostore las claves de certificado de Windows hello almacenan.

Compruebe que el **almacén de certificados de Windows** esté seleccionado y haga clic en **Siguiente**.

![Configuración de la clave maestra](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>Validación
Puede cifrar columnas Hola ahora o guardar una toorun de secuencia de comandos de PowerShell más adelante. Para este tutorial, seleccione **continuar ahora toofinish** y haga clic en **siguiente**.

### <a name="summary"></a>Resumen
Compruebe que configuración de hello es correctos y haga clic en **finalizar** el programa de instalación hello toocomplete para Always Encrypted.

![Resumen](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>Comprobar acciones del Asistente de Hola
Una vez finalizado el Asistente de hello, la base de datos se configura para Always Encrypted. Asistente para realizar de Hola Hola siguientes acciones:

* Crea un CMK.
* Crea un CMK.
* Hola configurado seleccionado columnas para el cifrado. Su **pacientes** tabla actualmente no tiene datos, pero ahora se cifran los datos existentes en las columnas de hello seleccionado.

Puede comprobar la creación de hello de claves de hello en SSMS yendo demasiado**Clinic** > **seguridad** > **Always Encrypted Keys**. Ahora puede ver claves nuevas Hola que Hola genera automáticamente con un asistente.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Crear una aplicación cliente que funciona con datos cifrado de saludo
Ahora que Always Encrypted está configurado, puede compilar una aplicación que realiza *inserta* y *selecciona* en hello las columnas cifradas. toosuccessfully al ejecutar la aplicación de ejemplo de Hola, debe ejecutarla en hello mismo equipo donde se ejecutó el Asistente de Always Encrypted Hola. aplicación de hello toorun en otro equipo, debe implementar el equipo que toohello certificados Always Encrypted ejecuta la aplicación de cliente de hello.  

> [!IMPORTANT]
> La aplicación debe utilizar [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objetos al pasar el servidor de toohello de datos de texto simple con columnas siempre cifradas. Se generará una excepción al pasar valores literales sin usar objetos SqlParameter.
> 
> 

1. Abra Visual Studio y cree una nueva aplicación de consola C#. Asegúrese de que el proyecto se establece demasiado**.NET Framework 4.6** o una versión posterior.
2. Proyecto de hello Name **AlwaysEncryptedConsoleApp** y haga clic en **Aceptar**.

![Nueva aplicación de consola](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modificar su tooenable de cadena de conexión Always Encrypted
Esta sección se explica cómo tooenable siempre cifrado en la cadena de conexión de base de datos. Se modificará la aplicación de consola de hello que acaba de crear en la siguiente sección hello, "Aplicación de consola de ejemplo de cifrado siempre".

tooenable Always Encrypted, necesita hello tooadd **Column Encryption Setting** conexión tooyour de palabra clave de cadena y establézcalo demasiado**habilitado**.

Puede establecer directamente en la cadena de conexión de hello, o se puede establecer mediante una [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). aplicación de ejemplo de Hola Hola siguiente sección se muestra cómo toouse **SqlConnectionStringBuilder**.

> [!NOTE]
> Se trata de hello cambio solo necesario en una aplicación de cliente específico tooAlways cifrada. Si tiene una aplicación existente que almacena la cadena de conexión externamente (es decir, en un archivo de configuración), es posible que pueda tooenable Always Encrypted sin cambiar ningún código.
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Habilitar Always Encrypted en la cadena de conexión de Hola
Agregue Hola después de la cadena de conexión de palabra clave tooyour:

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>Habilitar Always Encrypted con un SqlConnectionStringBuilder
Hello código siguiente muestra cómo Hola tooenable Always Encrypted estableciendo [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) demasiado[habilitado](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>Aplicación de consola de ejemplo de Always Encrypted
En este ejemplo se muestra cómo:

* Modifique su tooenable de cadena de conexión siempre se cifran.
* Insertar datos en columnas de hello cifrado.
* Seleccionar un registro mediante el filtrado de un valor específico de una columna cifrada.

Reemplace el contenido de Hola de **Program.cs** con el siguiente código de hello. Reemplace la cadena de conexión de hello para la variable de connectionString global de hello en línea hello directamente encima de hello método Main con la cadena de conexión válida de hello portal de Azure. Se trata de hello cambio solo se necesita toomake toothis código.

Ejecutar toosee de aplicación Hola Always Encrypted en acción.

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


## <a name="verify-that-hello-data-is-encrypted"></a>Compruebe que se cifren los datos de Hola
Puede comprobar fácilmente que se cifran datos reales de hello en servidor hello consultando hello **pacientes** datos con SSMS. (Use donde todavía no está habilitado el valor de cifrado de columnas de hello de la conexión actual).

Ejecute hello después de consulta en la base de datos de hello Clinic.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Puede ver que columnas Hola cifra no contienen los datos de texto simple.

   ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess Hola datos de texto simple, puede agregar hello **Column Encryption Setting = habilitado** conexión toohello de parámetro.

1. En SSMS, haga clic con el botón derecho en el servidor en el **Explorador de objetos** y haga clic en **Desconectar**.
2. Haga clic en **conectar** > **motor de base de datos** tooopen hello **conectar tooServer** ventana y, a continuación, haga clic en **opciones**.
3. Haga clic en **Parámetros de conexión adicionales** y escriba **Column Encryption Setting=enabled**.
   
    ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. Ejecución hello consulta en hello siguiente **Clinic** base de datos.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Ahora puede ver datos de texto simple de hello en columnas de hello cifrado.

    ![Nueva aplicación de consola](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> Si se conecta con SSMS (o cualquier cliente) en un equipo diferente, no tendrá acceso a claves de cifrado de toohello y no será capaz de toodecrypt datos de Hola.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Después de crear una base de datos que usa Always Encrypted, puede que desee siguiente de Hola toodo:

* Ejecutar este ejemplo desde un equipo diferente. No tendrá acceso a claves de cifrado de toohello, por lo que no tendrá acceso a datos de texto simple de toohello y no se ejecutará correctamente.
* [Rotar y limpiar las claves](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migrar los datos que ya están cifrados con Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).
* [Implementar máquinas del cliente de Always Encrypted certificados tooother](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (consulte la sección "Hacer que los certificados disponibles tooApplications y los usuarios" de hello).

## <a name="related-information"></a>Información relacionada
* [Always Encrypted (desarrollo de clientes)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Cifrado de datos transparente](https://msdn.microsoft.com/library/bb934049.aspx)
* [Cifrado de SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Asistente de Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog de Always Encrypted](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

