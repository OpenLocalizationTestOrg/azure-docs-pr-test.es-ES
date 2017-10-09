## <a name="clean-up-deployment"></a><span data-ttu-id="b1be3-101">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="b1be3-101">Clean up deployment</span></span> 

<span data-ttu-id="b1be3-102">Después de ejecutar el ejemplo de secuencia de comandos de hello, el comando de seguimiento de hello puede ser grupo de recursos de hello tooremove usado, instancia de caché en Redis de Azure y cualquier recurso relacionado en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1be3-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```