## <a name="next-steps"></a>Pasos siguientes

Después de habilitar la integración de Azure Key Vault, puede habilitar el cifrado de SQL Server en la máquina virtual de SQL. En primer lugar, deberá toocreate una clave asimétrica en el almacén de claves y una clave simétrica en SQL Server en la máquina virtual. A continuación, es posible que el cifrado de tooenable de instrucciones tooexecute capaz de T-SQL para bases de datos y las copias de seguridad.

Hay varias formas de cifrado que puede aprovechar:

* [Cifrado de datos transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Copias de seguridad cifradas](https://msdn.microsoft.com/library/dn449489.aspx)
* [Cifrado de nivel de columna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

Hello secuencias de comandos de Transact-SQL siguientes proporcionan ejemplos de cada una de estas áreas.

### <a name="prerequisites-for-examples"></a>Requisitos previos para los ejemplos

Cada ejemplo se basa en los requisitos previos de hello dos: una clave asimétrica desde el almacén de claves denominado **CONTOSO_KEY** y una credencial creados por la característica de integración de claves de hello denominada **Azure_EKM_TDE_cred**. Hello siguientes comandos de Transact-SQL estos requisitos previos de instalación para ejecutar los ejemplos de hello.

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a>Cifrado de datos transparente (TDE) 

1. Crear un toobe de inicio de sesión de SQL Server usado Hola motor de base de datos para TDE, a continuación, agregue Hola credencial tooit.

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. Crear clave de cifrado de base de datos de Hola que se usará para TDE.

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a>Copias de seguridad cifradas

1. Crear un toobe de inicio de sesión de SQL Server utilizado por el motor de base de datos para cifrar las copias de seguridad de Hola y agregue Hola credencial tooit.

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. Especificando cifrado con la clave asimétrica Hola almacenada en el almacén de claves de Hola la base de datos de copia de seguridad Hola.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Cifrado de nivel de columna (CLE)

Este script crea una clave simétrica protegida mediante clave asimétrica de hello en el almacén de claves de hello y, a continuación, utiliza datos de tooencrypt clave simétrica de hello en la base de datos de Hola.

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a>Recursos adicionales

Para obtener más información sobre cómo toouse estas características de cifrado, consulte [usar EKM con las características de cifrado de SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Tenga en cuenta que los pasos de hello en este artículo se supone que ya tenga SQL Server que se ejecuta en una máquina virtual de Azure. De lo contrario, consulte [Aprovisionamiento de una máquina virtual de SQL Server en Azure Portal](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Para otros temas sobre la ejecución de SQL Server en máquinas virtuales de Azure, consulte [Información general de SQL Server en máquinas virtuales de Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
