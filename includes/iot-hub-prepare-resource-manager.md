## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Preparar tooauthenticate solicitudes del Administrador de recursos de Azure
Debe autenticar todas las operaciones de Hola que se realizan en los recursos con hello [Azure Resource Manager] [ lnk-authenticate-arm] con Azure Active Directory (AD). Hola tooconfigure de manera más sencilla es toouse PowerShell o CLI de Azure.

Instalar hello [cmdlets de PowerShell de Azure] [ lnk-powershell-install] antes de continuar.

Hola siguientes pasos muestran cómo tooset la autenticación de contraseña para una aplicación de AD con PowerShell. Puede ejecutar estos comandos en una sesión de PowerShell estándar.

1. Inicie sesión en tooyour suscripción de Azure con hello siguiente comando:

    ```powershell
    Login-AzureRmAccount
    ```

1. Si tiene varias suscripciones de Azure, iniciar sesión en tooAzure concede acceso tooall hello Azure suscripciones asociadas con sus credenciales. Usar hello siguiente comando toolist hello Azure suscripciones disponibles para usted toouse:

    ```powershell
    Get-AzureRMSubscription
    ```

    Usar hello después de suscripción de tooselect de comando que desea toouse toorun Hola comandos toomanage su centro de IoT. Puede usar el nombre de la suscripción de Hola o Id. de salida de hello del comando anterior hello:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Anote los valores de **TenantId** y **SubscriptionId**. Los necesitará más adelante.
3. Cree una nueva aplicación de Azure Active Directory mediante Hola siguiente comando, reemplazando los marcadores de posición de hello:
   
   * **{Nombre para mostrar}**: nombre para mostrar de la aplicación, por ejemplo, **MySampleApp**.
   * **{URL de la página de inicio}:** Hola como dirección URL de página de inicio de saludo de la aplicación **http://mysampleapp/home**. Esta dirección URL no es necesario toopoint real de tooa la aplicación.
   * **{Identificador de aplicación}**: identificador único, por ejemplo, **http://mysampleapp**. Esta dirección URL no es necesario toopoint real de tooa la aplicación.
   * **{Password}:** una contraseña que se utiliza tooauthenticate con la aplicación.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Tome nota de hello **ApplicationId** de aplicación Hola que ha creado. Lo necesitará más adelante.
5. Crear una nueva entidad de servicio con hello siguiente comando, reemplazando **{MyApplicationId}** con hello **ApplicationId** del paso anterior hello:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Configurar una asignación de roles con hello siguiente comando, reemplazando **{MyApplicationId}** con su **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Ahora ha terminado de crear aplicación de Azure AD de Hola que le permite tooauthenticate desde su aplicación personalizada de C#. Necesita Hola siguiendo los valores más adelante en este tutorial:

* TenantId
* SubscriptionId
* ApplicationId
* Password

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
