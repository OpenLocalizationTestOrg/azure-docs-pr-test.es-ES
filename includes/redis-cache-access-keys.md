instancia de caché en Redis de Azure de tooconnect tooan, los clientes de caché necesitan nombre de host de hello, puertos y las claves de caché de Hola. Algunos clientes pueden hacer referencia a elementos de toothese nombres ligeramente diferentes. Puede recuperar esta información en el portal de Azure de Hola o mediante herramientas de línea de comandos como CLI de Azure.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Recuperar el nombre de host, puertos y las teclas de acceso mediante Hola Portal de Azure
tooretrieve nombre de host, puertos y las teclas de acceso mediante Hola Portal de Azure, [examinar](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour caché Hola [portal de Azure](https://portal.azure.com) y haga clic en **las claves de acceso** y  **Propiedades** en hello **menú recursos**. 

![Configuración de caché en Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Recuperación del nombre de host, puertos y claves de acceso mediante la CLI de Azure
nombre de host de tooretrieve hello y puertos mediante Azure CLI 2.0 puede llamar a [presentación con redis az](https://docs.microsoft.com/cli/azure/redis#show)y puede llamar a las claves de Hola de tooretrieve [az redis claves de la lista](https://docs.microsoft.com/cli/azure/redis#list-keys). Hello script siguiente llama a estos dos comandos y eco hello nombre de host, puertos y la consola de toohello de claves.

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

Para obtener más información acerca de esta secuencia de comandos, consulte [obtener Hola hostname, puertos y las claves de caché en Redis de Azure](../articles/redis-cache/scripts/cache-keys-ports.md). Para más información sobre la CLI de Azure 2.0, consulte [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalación de la CLI de Azure 2.0) y [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Introducción a la CLI de Azure 2.0).
