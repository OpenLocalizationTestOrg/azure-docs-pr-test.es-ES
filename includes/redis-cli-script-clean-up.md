## <a name="clean-up-deployment"></a><span data-ttu-id="63cd9-101">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="63cd9-101">Clean up deployment</span></span> 

<span data-ttu-id="63cd9-102">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos, las instancias de Azure Redis Cache y todos los recursos relacionados en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="63cd9-102">After the script sample has been run, the follow command can be used to remove the resource group, Azure Redis Cache instance, and any related resources in the resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```