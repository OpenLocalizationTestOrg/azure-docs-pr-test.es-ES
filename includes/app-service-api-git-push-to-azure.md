<span data-ttu-id="b3597-101">Usar dirección URL de implementación remota de hello Azure CLI tooget hello para la API App.</span><span class="sxs-lookup"><span data-stu-id="b3597-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="b3597-102">Hola siguiente comando, reemplace  *\<app_name >* con el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b3597-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="b3597-103">Configure su local Git implementación toobe toopush pueda toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="b3597-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="b3597-104">Insertar toohello Azure toodeploy remoto de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3597-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="b3597-105">Se le pediremos que creó anteriormente cuando se creó el usuario de la implementación de Hola de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3597-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="b3597-106">Asegúrese de que escriba la contraseña de Hola que creó en versiones anteriores del tutorial de Hola y Hola una contraseña no usar toolog en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3597-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
