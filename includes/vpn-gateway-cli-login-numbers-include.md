1. <span data-ttu-id="bb46d-101">Inicie sesión en la suscripción de Azure con el comando [az login](/cli/azure/#login) y siga las instrucciones de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="bb46d-101">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="bb46d-102">Para más información, consulte [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)(Introducción a la CLI de Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="bb46d-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="bb46d-103">Si tiene más de una suscripción de Azure, enumere las suscripciones de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="bb46d-103">If you have more than one Azure subscription, list the subscriptions for the account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="bb46d-104">Especifique la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="bb46d-104">Specify the subscription that you want to use.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```