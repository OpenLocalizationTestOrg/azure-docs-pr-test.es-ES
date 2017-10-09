## <a name="set-up-azure-cli-for-azure-dns"></a>Configuración de la CLI de Azure para DNS de Azure

### <a name="before-you-begin"></a>Antes de empezar

Compruebe que dispone de hello siguientes elementos antes de comenzar la configuración.

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Instale Hola la versión más reciente de hello CLI de Azure, disponible para Windows, Linux o Mac. Hay disponible más información en [Install hello Azure CLI](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Inicie sesión en tooyour cuenta de Azure

Abra una ventana de consola y autentíquese con sus credenciales. Para obtener más información, vea [sesión tooAzure de hello CLI de Azure](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>Cambio del modo de CLI

La DNS de Azure usa el Administrador de recursos de Azure. Asegúrese de que cambiar comandos de CLI modo toouse Azure Resource Manager.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Seleccione la suscripción de Hola

Compruebe las suscripciones de hello para la cuenta de hello.

```azurecli
azure account list
```

Elija qué su toouse de las suscripciones de Azure.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Azure Resource Manager requiere que todos los grupos de recursos especifiquen una ubicación. Esto se utiliza como ubicación predeterminada de Hola para recursos de ese grupo de recursos. Sin embargo, dado que todos los recursos DNS son globales, no regionales, elección de Hola de ubicación del grupo de recursos tiene ningún impacto en el DNS de Azure.

Puede omitir este paso si utiliza un grupo de recursos existente.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>Registro del proveedor de recursos

Hola servicio DNS de Azure se administra mediante el proveedor de recursos de Microsoft.Network Hola. Su suscripción de Azure debe estar registrado toouse este proveedor de recursos antes de que se puede usar DNS de Azure. Se trata de una operación única para cada suscripción.

```azurecli
azure provider register --namespace Microsoft.Network
```

