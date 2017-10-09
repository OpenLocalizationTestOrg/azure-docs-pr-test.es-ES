1. <span data-ttu-id="f3914-101">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="f3914-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="f3914-102">Para más información, consulte [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)(Introducción a la CLI de Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="f3914-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="f3914-103">Si tiene más de una suscripción de Azure, mostrar las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="f3914-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="f3914-104">Especifique que desea toouse de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3914-104">Specify hello subscription that you want toouse.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```