## <a name="prepare-for-akv-integration"></a>Preparación para la integración de AKV
toouse tooconfigure de integración del almacén de claves de Azure la VM de SQL Server, hay varios requisitos previos: 

1. [Instalar Azure Powershell](#install-azure-powershell)
2. [Crear un directorio de Azure Active Directory](#create-an-azure-active-directory)
3. [Creación de un Almacén de claves](#create-a-key-vault)

Hello las secciones siguientes describen estos requisitos previos y la información de hello necesaria cmdlets de PowerShell de toocollect toolater ejecutar Hola.

### <a name="install-azure-powershell"></a>Azure PowerShell
Asegúrese de que ha instalado Hola SDK más reciente de PowerShell de Azure. Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Crear un directorio de Azure Active Directory
En primer lugar, debe toohave una [Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) en su suscripción. Entre muchas ventajas, esto le permite almacén de claves de tooyour de permiso y toogrant para determinados usuarios y aplicaciones.

A continuación, registre una aplicación con AAD. Esto le dará una cuenta de entidad de servicio que tenga acceso tooyour almacén de claves que se necesita la máquina virtual. En el artículo de almacén de claves de Azure de hello, puede encontrar estos pasos en hello [registrar una aplicación con Azure Active Directory](../articles/key-vault/key-vault-get-started.md#register) sección, también puede ver pasos Hola con capturas de pantalla de hello **obtener una identidad de aplicación hello sección** de [esta entrada de blog](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Antes de completar estos pasos, tenga en cuenta que debe hello toocollect siguiente información durante este registro que se necesita más adelante cuando se habilita la integración de almacén de claves de Azure en la VM de SQL.

* Después de agrega la aplicación hello, encontrar Hola **Id. de cliente** en hello **configurar** ficha.   ![Identificador de cliente de Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    se asigna el identificador de cliente de Hello toohello posterior **$spName** parámetro (nombre Principal de servicio) en tooenable de secuencia de comandos de PowerShell de hello integración del almacén de claves de Azure. 
* Además, durante estos pasos cuando se crea la clave, copiar Hola el secreto para su clave tal y como se muestra en la siguiente captura de pantalla de Hola. Esta clave secreta se asigna una versión posterior toohello **$spSecret** parámetro (secreto Principal de servicio) en la secuencia de comandos de PowerShell de Hola.  
    ![Secreto de Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* Debe autorizar este nuevo Hola de toohave de Id. de cliente los siguientes permisos de acceso: **cifrar**, **descifrar**, **wrapKey**, **unwrapKey**, **inicio de sesión**, y **comprobar**. Esto se hace con hello [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) cmdlet. Para obtener más información, consulte [Authorize Hola aplicación toouse Hola clave o el secreto](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Creación de un Almacén de claves
En toouse el almacén de claves de Azure toostore hello las claves de ordenación que va a utilizar para el cifrado en la máquina virtual, es necesario el almacén de claves de acceso tooa. Si aún no ha establecido su almacén de claves, cree una siguiendo los pasos de Hola Hola [Introducción al almacén de claves de Azure](../articles/key-vault/key-vault-get-started.md) tema. Antes de completar estos pasos, tenga en cuenta que hay alguna información que necesita toocollect durante esta configuración que se necesita más adelante cuando se habilita la integración de almacén de claves de Azure en la VM de SQL.

Al obtener toohello crear un paso de almacén de claves, Hola Nota devuelve **vaultUri** propiedad, que es la dirección URL del almacén de claves de Hola. En el ejemplo de Hola incluido en este paso, que se muestra a continuación, nombre de almacén de claves de hello es ContosoKeyVault, por lo tanto, dirección URL de almacén de claves de hello sería https://contosokeyvault.vault.azure.net/.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

dirección URL del almacén de claves de Hola se asigna posterior toohello **$akvURL** parámetro en tooenable de secuencia de comandos de PowerShell de hello integración del almacén de claves de Azure.

