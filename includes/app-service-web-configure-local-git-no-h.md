<span data-ttu-id="414d2-101">Configurar la implementación de Git local en la aplicación web con el comando [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git).</span><span class="sxs-lookup"><span data-stu-id="414d2-101">Configure local Git deployment to the web app with the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="414d2-102">App Service admite varias maneras de implementar contenido en una aplicación web, como FTP, Git local, GitHub, Visual Studio Team Services y Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="414d2-102">App Service supports several ways to deploy content to a web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="414d2-103">Para esta guía de inicio rápido, va a realizar la implementación mediante el uso de Git local.</span><span class="sxs-lookup"><span data-stu-id="414d2-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="414d2-104">Esto significa que va a realizar la implementación con un comando de Git para insertar desde un repositorio local en un repositorio de Azure.</span><span class="sxs-lookup"><span data-stu-id="414d2-104">That means you deploy by using a Git command to push from a local repository to a repository in Azure.</span></span> 

<span data-ttu-id="414d2-105">En el siguiente comando, reemplace  *\<app_name >* por el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="414d2-105">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="414d2-106">La salida tiene el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="414d2-106">The output has the following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="414d2-107">`<username>` es el [usuario de implementación](#configure-a-deployment-user) que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="414d2-107">The `<username>` is the [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="414d2-108">Copie el identificador URI que se muestra; se usará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="414d2-108">Copy the URI shown; you'll use it in the next step.</span></span>
