<span data-ttu-id="816a7-101">instancia de caché en Redis de Azure de tooconnect tooan, los clientes de caché necesitan nombre de host de hello, puertos y las claves de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="816a7-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="816a7-102">Algunos clientes pueden hacer referencia a elementos de toothese nombres ligeramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="816a7-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="816a7-103">Puede recuperar esta información en el portal de Azure de Hola o mediante herramientas de línea de comandos como CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="816a7-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="816a7-104">Recuperar el nombre de host, puertos y las teclas de acceso mediante Hola Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="816a7-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="816a7-105">tooretrieve nombre de host, puertos y las teclas de acceso mediante Hola Portal de Azure, [examinar](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour caché Hola [portal de Azure](https://portal.azure.com) y haga clic en **las claves de acceso** y  **Propiedades** en hello **menú recursos**.</span><span class="sxs-lookup"><span data-stu-id="816a7-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Configuración de caché en Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="816a7-107">Recuperación del nombre de host, puertos y claves de acceso mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="816a7-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="816a7-108">nombre de host de tooretrieve hello y puertos mediante Azure CLI 2.0 puede llamar a [presentación con redis az](https://docs.microsoft.com/cli/azure/redis#show)y puede llamar a las claves de Hola de tooretrieve [az redis claves de la lista](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="816a7-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="816a7-109">Hello script siguiente llama a estos dos comandos y eco hello nombre de host, puertos y la consola de toohello de claves.</span><span class="sxs-lookup"><span data-stu-id="816a7-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

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

<span data-ttu-id="816a7-110">Para obtener más información acerca de esta secuencia de comandos, consulte [obtener Hola hostname, puertos y las claves de caché en Redis de Azure](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="816a7-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="816a7-111">Para más información sobre la CLI de Azure 2.0, consulte [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalación de la CLI de Azure 2.0) y [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Introducción a la CLI de Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="816a7-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
