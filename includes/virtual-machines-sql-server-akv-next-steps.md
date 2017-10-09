## <a name="next-steps"></a><span data-ttu-id="7d8f6-101">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7d8f6-101">Next steps</span></span>

<span data-ttu-id="7d8f6-102">Después de habilitar la integración de Azure Key Vault, puede habilitar el cifrado de SQL Server en la máquina virtual de SQL.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="7d8f6-103">En primer lugar, deberá toocreate una clave asimétrica en el almacén de claves y una clave simétrica en SQL Server en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="7d8f6-104">A continuación, es posible que el cifrado de tooenable de instrucciones tooexecute capaz de T-SQL para bases de datos y las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="7d8f6-105">Hay varias formas de cifrado que puede aprovechar:</span><span class="sxs-lookup"><span data-stu-id="7d8f6-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="7d8f6-106">Cifrado de datos transparente (TDE)</span><span class="sxs-lookup"><span data-stu-id="7d8f6-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="7d8f6-107">Copias de seguridad cifradas</span><span class="sxs-lookup"><span data-stu-id="7d8f6-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="7d8f6-108">Cifrado de nivel de columna (CLE)</span><span class="sxs-lookup"><span data-stu-id="7d8f6-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="7d8f6-109">Hello secuencias de comandos de Transact-SQL siguientes proporcionan ejemplos de cada una de estas áreas.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="7d8f6-110">Requisitos previos para los ejemplos</span><span class="sxs-lookup"><span data-stu-id="7d8f6-110">Prerequisites for examples</span></span>

<span data-ttu-id="7d8f6-111">Cada ejemplo se basa en los requisitos previos de hello dos: una clave asimétrica desde el almacén de claves denominado **CONTOSO_KEY** y una credencial creados por la característica de integración de claves de hello denominada **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="7d8f6-112">Hello siguientes comandos de Transact-SQL estos requisitos previos de instalación para ejecutar los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

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

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="7d8f6-113">Cifrado de datos transparente (TDE) </span><span class="sxs-lookup"><span data-stu-id="7d8f6-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="7d8f6-114">Crear un toobe de inicio de sesión de SQL Server usado Hola motor de base de datos para TDE, a continuación, agregue Hola credencial tooit.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

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

1. <span data-ttu-id="7d8f6-115">Crear clave de cifrado de base de datos de Hola que se usará para TDE.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-115">Create hello database encryption key that will be used for TDE.</span></span>

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

### <a name="encrypted-backups"></a><span data-ttu-id="7d8f6-116">Copias de seguridad cifradas</span><span class="sxs-lookup"><span data-stu-id="7d8f6-116">Encrypted backups</span></span>

1. <span data-ttu-id="7d8f6-117">Crear un toobe de inicio de sesión de SQL Server utilizado por el motor de base de datos para cifrar las copias de seguridad de Hola y agregue Hola credencial tooit.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

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

1. <span data-ttu-id="7d8f6-118">Especificando cifrado con la clave asimétrica Hola almacenada en el almacén de claves de Hola la base de datos de copia de seguridad Hola.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="7d8f6-119">Cifrado de nivel de columna (CLE)</span><span class="sxs-lookup"><span data-stu-id="7d8f6-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="7d8f6-120">Este script crea una clave simétrica protegida mediante clave asimétrica de hello en el almacén de claves de hello y, a continuación, utiliza datos de tooencrypt clave simétrica de hello en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="7d8f6-121">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7d8f6-121">Additional resources</span></span>

<span data-ttu-id="7d8f6-122">Para obtener más información sobre cómo toouse estas características de cifrado, consulte [usar EKM con las características de cifrado de SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="7d8f6-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="7d8f6-123">Tenga en cuenta que los pasos de hello en este artículo se supone que ya tenga SQL Server que se ejecuta en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8f6-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="7d8f6-124">De lo contrario, consulte [Aprovisionamiento de una máquina virtual de SQL Server en Azure Portal](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="7d8f6-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="7d8f6-125">Para otros temas sobre la ejecución de SQL Server en máquinas virtuales de Azure, consulte [Información general de SQL Server en máquinas virtuales de Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7d8f6-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
