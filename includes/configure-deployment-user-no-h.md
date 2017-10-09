<span data-ttu-id="12232-101">Crear credenciales de implementación con hello [conjunto de usuarios de implementación de aplicación Web de az](/cli/azure/webapp/deployment/user#set) comando.</span><span class="sxs-lookup"><span data-stu-id="12232-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="12232-102">Un usuario de implementación es necesario para FTP y Git implementación tooa la aplicación web local.</span><span class="sxs-lookup"><span data-stu-id="12232-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="12232-103">nombre de usuario de Hola y la contraseña son el nivel de cuenta.</span><span class="sxs-lookup"><span data-stu-id="12232-103">hello user name and password are account level.</span></span> <span data-ttu-id="12232-104">_Son diferentes de las credenciales de suscripción de Azure._</span><span class="sxs-lookup"><span data-stu-id="12232-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="12232-105">Hola siguiente comando, reemplace  *\<nombre de usuario >* y  *\<contraseña >* con un nuevo nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="12232-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="12232-106">nombre de usuario de Hello debe ser único.</span><span class="sxs-lookup"><span data-stu-id="12232-106">hello user name must be unique.</span></span> <span data-ttu-id="12232-107">Hello contraseña debe tener al menos ocho caracteres, con dos Hola después de tres elementos: letras, números y símbolos.</span><span class="sxs-lookup"><span data-stu-id="12232-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="12232-108">Si se produce un ` 'Conflict'. Details: 409` error, el nombre de usuario de cambio Hola.</span><span class="sxs-lookup"><span data-stu-id="12232-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="12232-109">Si se produce un error ` 'Bad Request'. Details: 400`, use una contraseña más segura.</span><span class="sxs-lookup"><span data-stu-id="12232-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="12232-110">Solo es necesario crear este usuario de implementación una vez, y puede usarlo en todas las implementaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="12232-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="12232-111">Nombre de usuario de Hola de registro y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="12232-111">Record hello user name and password.</span></span> <span data-ttu-id="12232-112">Necesite toodeploy hello web aplicación más tarde.</span><span class="sxs-lookup"><span data-stu-id="12232-112">You need them toodeploy hello web app later.</span></span>
>
>