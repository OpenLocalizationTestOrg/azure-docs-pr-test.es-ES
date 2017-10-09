<span data-ttu-id="23ef2-101">Configurar Git implementación toohello la aplicación web local con hello [origen de implementación de aplicación Web en az config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando.</span><span class="sxs-lookup"><span data-stu-id="23ef2-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="23ef2-102">Servicio de aplicaciones admite varias maneras toodeploy tooa contenido aplicación web, como FTP, Git local, GitHub, Visual Studio Team Services y Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="23ef2-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="23ef2-103">Para esta guía de inicio rápido, va a realizar la implementación mediante el uso de Git local.</span><span class="sxs-lookup"><span data-stu-id="23ef2-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="23ef2-104">Esto significa que se implementan con un toopush de comandos de Git desde un repositorio de tooa de repositorio local en Azure.</span><span class="sxs-lookup"><span data-stu-id="23ef2-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="23ef2-105">Hola siguiente comando, reemplace  *\<app_name >* con el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="23ef2-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="23ef2-106">salida de Hello tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="23ef2-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="23ef2-107">Hola `<username>` es hello [usuario de implementación](#configure-a-deployment-user) que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="23ef2-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="23ef2-108">Copiar Hola URI se muestra; se usará en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="23ef2-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
