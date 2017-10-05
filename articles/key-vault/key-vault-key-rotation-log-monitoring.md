---
title: "Configuración de Azure Key Vault con la auditoría y la rotación de claves de un extremo a otro | Microsoft Docs"
description: "Utilice este tutorial para establecer la configuración con rotación de claves y supervisar los registros del almacén de claves."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: 38c342802ed687985ac6f84f5a590a1a0dcc6c6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="6a933-103">Configuración de Azure Key Vault con la auditoría y la rotación de claves de un extremo a otro</span><span class="sxs-lookup"><span data-stu-id="6a933-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="6a933-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="6a933-104">Introduction</span></span>
<span data-ttu-id="6a933-105">Una vez que haya creado el almacén de claves, podrá utilizarlo para guardar las claves y los secretos.</span><span class="sxs-lookup"><span data-stu-id="6a933-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span></span> <span data-ttu-id="6a933-106">Ya no será necesario que las claves y secretos se guarden en las aplicaciones, sino que las aplicaciones solicitarán las claves al almacén cuando lo necesiten.</span><span class="sxs-lookup"><span data-stu-id="6a933-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span></span> <span data-ttu-id="6a933-107">De este modo, puede actualizar las claves y los secretos sin que esto afecte al rendimiento de la aplicación, lo que brinda un amplio abanico de posibilidades en lo que respecta a la administración de las claves y los secretos.</span><span class="sxs-lookup"><span data-stu-id="6a933-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="6a933-108">En este artículo, se explica paso a paso un ejemplo sobre el uso de Azure Key Vault para guardar un secreto. En este caso, se trata de una clave de la cuenta de Azure Storage a la que accede una aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a933-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="6a933-109">El artículo también incluye una demostración de la implementación de una rotación programada de dicha clave.</span><span class="sxs-lookup"><span data-stu-id="6a933-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="6a933-110">Por último, se explica paso a paso cómo supervisar los registros de auditoría del almacén de claves y cómo generar alertas cuando se realizan solicitudes inesperadas.</span><span class="sxs-lookup"><span data-stu-id="6a933-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="6a933-111">En este tutorial no se explica en detalle la configuración inicial del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span></span> <span data-ttu-id="6a933-112">Para obtener información, consulte [Introducción al Almacén de claves de Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6a933-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="6a933-113">Para obtener instrucciones acerca de la interfaz de la línea de comandos para todas las plataformas, consulte [Administración del almacén de claves mediante CLI](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="6a933-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="6a933-114">Configuración del Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="6a933-114">Set up Key Vault</span></span>
<span data-ttu-id="6a933-115">Para que una aplicación pueda recuperar un secreto de Key Vault, primero debe crear el secreto y guardarlo en el almacén.</span><span class="sxs-lookup"><span data-stu-id="6a933-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span></span> <span data-ttu-id="6a933-116">Para ello, abra una sesión de Azure PowerShell e inicie sesión en su cuenta de Azure con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6a933-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6a933-117">En la ventana emergente del explorador, escriba el nombre de usuario y la contraseña de su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a933-117">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="6a933-118">PowerShell obtendrá todas las suscripciones asociadas a esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="6a933-118">PowerShell will get all the subscriptions that are associated with this account.</span></span> <span data-ttu-id="6a933-119">PowerShell utiliza la primera de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6a933-119">PowerShell uses the first one by default.</span></span>

<span data-ttu-id="6a933-120">Si tiene varias suscripciones, es posible que deba especificar la que se usó para crear el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span></span> <span data-ttu-id="6a933-121">Escriba lo siguiente para ver las suscripciones de su cuenta:</span><span class="sxs-lookup"><span data-stu-id="6a933-121">Enter the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6a933-122">Para especificar la suscripción asociada al almacén de claves que registrará, escriba:</span><span class="sxs-lookup"><span data-stu-id="6a933-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="6a933-123">Dado que en este artículo se explica cómo se guarda una clave de cuenta de almacenamiento como un secreto, debe obtener dicha clave.</span><span class="sxs-lookup"><span data-stu-id="6a933-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="6a933-124">Una vez recuperado el secreto (en este caso, la clave de la cuenta de almacenamiento), debe convertir la clave en una cadena segura y crear un secreto con ese valor en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="6a933-125">A continuación, obtenga el identificador URI para el secreto que creó.</span><span class="sxs-lookup"><span data-stu-id="6a933-125">Next, get the URI for the secret you created.</span></span> <span data-ttu-id="6a933-126">Este se utilizará en un paso posterior, cuando llame al almacén de claves para recuperar el secreto.</span><span class="sxs-lookup"><span data-stu-id="6a933-126">This is used in a later step when you call the key vault to retrieve your secret.</span></span> <span data-ttu-id="6a933-127">Ejecute el siguiente comando de PowerShell y anote el valor de identificación, que es el URI del secreto:</span><span class="sxs-lookup"><span data-stu-id="6a933-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-the-application"></a><span data-ttu-id="6a933-128">Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6a933-128">Set up the application</span></span>
<span data-ttu-id="6a933-129">Ahora que tiene un secreto almacenado, puede utilizar el código para recuperarlo y utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="6a933-129">Now that you have a secret stored, you can use code to retrieve and use it.</span></span> <span data-ttu-id="6a933-130">Existen varios pasos obligatorios para conseguirlo.</span><span class="sxs-lookup"><span data-stu-id="6a933-130">There are a few steps required to achieve this.</span></span> <span data-ttu-id="6a933-131">El primero y más importante consiste en registrar la aplicación con Azure Active Directory y proporcionar a Key Vault la información de la aplicación para que pueda permitir que se realicen solicitudes desde dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a933-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="6a933-132">La aplicación debe crearse en el mismo inquilino de Azure Active Directory que el del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="6a933-133">Abra la pestaña Aplicaciones de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a933-133">Open the applications tab of Azure Active Directory.</span></span>

![Abra las aplicaciones de Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="6a933-135">Elija **AGREGAR** para agregar una aplicación a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a933-135">Choose **ADD** to add an application to your Azure Active Directory.</span></span>

![Elija AGREGAR](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="6a933-137">Deje el tipo de aplicación como **APLICACIÓN WEB Y/O API WEB** y asigne un nombre a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a933-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Asigne un nombre a la aplicación](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="6a933-139">Especifique un valor en **URL DE INICIO DE SESIÓN** y en **URI DE ID DE APLICACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="6a933-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="6a933-140">En esta demostración, puede especificar los valores que desee y cambiarlos más adelante si es necesario.</span><span class="sxs-lookup"><span data-stu-id="6a933-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Especifique los identificadores URI necesarios](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="6a933-142">Una vez que la aplicación se ha agregado a Azure Active Directory, accederá automáticamente a la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a933-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span></span> <span data-ttu-id="6a933-143">Una vez aquí, deberá hacer clic en la pestaña **Configurar** para buscar y copiar el valor de **ID de cliente**.</span><span class="sxs-lookup"><span data-stu-id="6a933-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span></span> <span data-ttu-id="6a933-144">Anote este valor, ya que lo necesitará posteriormente.</span><span class="sxs-lookup"><span data-stu-id="6a933-144">Make note of the client ID for later steps.</span></span>

<span data-ttu-id="6a933-145">A continuación, genere una clave para su aplicación para que pueda interactuar con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a933-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="6a933-146">Puede crear esta clave en la sección **Claves** de la pestaña **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="6a933-146">You can create this under the **Keys** section in the **Configuration** tab.</span></span> <span data-ttu-id="6a933-147">No olvide anotar esta nueva clave de la aplicación de Azure Active Directory, ya que la necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="6a933-147">Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Claves de aplicaciones de Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="6a933-149">Antes de definir en el almacén de claves las llamadas que se realizarán desde la aplicación, debe proporcionar al almacén de claves los datos de la aplicación y sus permisos.</span><span class="sxs-lookup"><span data-stu-id="6a933-149">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span></span> <span data-ttu-id="6a933-150">El comando siguiente toma el nombre del almacén y el identificador de cliente de la aplicación de Azure Active Directory y concede a la aplicación acceso **Get** al almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-150">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="6a933-151">Llegados a este punto, ya tiene todo listo para empezar a crear las llamadas a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a933-151">At this point, you are ready to start building your application calls.</span></span> <span data-ttu-id="6a933-152">En primer lugar, deberá instalar en la aplicación los paquetes NuGet necesarios para poder interactuar con Azure Key Vault y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a933-152">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="6a933-153">En la Consola del Administrador de paquetes de Visual Studio, escriba los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="6a933-153">From the Visual Studio Package Manager console, enter the following commands.</span></span> <span data-ttu-id="6a933-154">Cuando se redactó este artículo, la versión más reciente del paquete de Azure Active Directory era la 3.10.305231913; por tanto, debe confirmar que se trata de la última versión y actualizar en caso necesario.</span><span class="sxs-lookup"><span data-stu-id="6a933-154">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="6a933-155">En el código de la aplicación, cree una clase que contenga el método de autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a933-155">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="6a933-156">En este ejemplo, la clase se llama **Utils**.</span><span class="sxs-lookup"><span data-stu-id="6a933-156">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="6a933-157">Agregue la siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="6a933-157">Add the following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="6a933-158">A continuación, agregue el método siguiente para recuperar el token JWT de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a933-158">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span></span> <span data-ttu-id="6a933-159">Es posible que, para facilitar el mantenimiento, quiera trasladar los valores de cadena codificados de forma rígida a la configuración del sitio web o la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a933-159">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="6a933-160">Agregue el código necesario para llamar a Key Vault y recuperar el valor del secreto.</span><span class="sxs-lookup"><span data-stu-id="6a933-160">Add the necessary code to call Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="6a933-161">Lo primero que debe hacer es agregar la siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="6a933-161">First you must add the following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="6a933-162">Agregue las llamadas de método para invocar a Key Vault y recuperar el secreto.</span><span class="sxs-lookup"><span data-stu-id="6a933-162">Add the method calls to invoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="6a933-163">En este método, proporcione el URI del secreto que guardó en un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="6a933-163">In this method, you provide the secret URI that you saved in a previous step.</span></span> <span data-ttu-id="6a933-164">Observe el uso del método **GetToken** en la clase **Utils** que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6a933-164">Note the use of the **GetToken** method from the **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="6a933-165">Cuando ejecute la aplicación, debería estar autenticado en Azure Active Directory y recuperar el valor del secreto de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6a933-165">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="6a933-166">Rotación de claves mediante Azure Automation</span><span class="sxs-lookup"><span data-stu-id="6a933-166">Key rotation using Azure Automation</span></span>
<span data-ttu-id="6a933-167">Existen varias opciones para implementar una estrategia de rotación de los valores que se guardan como secretos del Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a933-167">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="6a933-168">Los secretos pueden rotarse mediante un proceso manual, mediante programación a través de llamadas a API o mediante un script de automatización.</span><span class="sxs-lookup"><span data-stu-id="6a933-168">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="6a933-169">En este artículo, utilizaremos Azure PowerShell y Azure Automation para cambiar una clave de acceso de la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6a933-169">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span></span> <span data-ttu-id="6a933-170">A continuación, podrá actualizar un secreto del almacén de claves con esa nueva clave.</span><span class="sxs-lookup"><span data-stu-id="6a933-170">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="6a933-171">Para que Azure Automation pueda establecer los valores del secreto en el almacén de claves, deberá obtener el identificador de cliente de la conexión AzureRunAsConnection que se creó al establecer la instancia de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="6a933-171">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="6a933-172">Para encontrar este identificador, seleccione **Recursos** en la instancia de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="6a933-172">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="6a933-173">A continuación, seleccione **Conexiones** y el nombre principal de servicio **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="6a933-173">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="6a933-174">Anote el **Identificador de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="6a933-174">Take note of the **Application ID**.</span></span>

![Identificador de cliente de Azure Automation](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="6a933-176">En **Recursos**, elija **Módulos**.</span><span class="sxs-lookup"><span data-stu-id="6a933-176">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="6a933-177">En **Módulos**, seleccione **Galería** y, a continuación, busque e **importe** las versiones actualizadas de cada uno de los siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="6a933-177">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="6a933-178">Cuando se redactó este artículo, los módulos que aparecen arriba eran los únicos que debían actualizarse para el script que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="6a933-178">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span></span> <span data-ttu-id="6a933-179">Si se produce algún error en el trabajo de automatización, confirme que ha importado todos los módulos necesarios y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="6a933-179">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="6a933-180">Una vez que haya recuperado el identificador de aplicación de la conexión de Azure Automation, debe notificar al almacén de claves que la aplicación tiene acceso para actualizar los secretos del almacén.</span><span class="sxs-lookup"><span data-stu-id="6a933-180">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span></span> <span data-ttu-id="6a933-181">Para ello, puede utilizar el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6a933-181">This can be accomplished with the following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="6a933-182">A continuación, seleccione **Runbooks** en la instancia de Azure Automation y, después, seleccione **Agregar un runbook**.</span><span class="sxs-lookup"><span data-stu-id="6a933-182">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="6a933-183">Seleccione **Creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="6a933-183">Select **Quick Create**.</span></span> <span data-ttu-id="6a933-184">Asigne un nombre al runbook y seleccione **PowerShell** como tipo del runbook.</span><span class="sxs-lookup"><span data-stu-id="6a933-184">Name your runbook and select **PowerShell** as the runbook type.</span></span> <span data-ttu-id="6a933-185">Tiene la opción de agregar una descripción.</span><span class="sxs-lookup"><span data-stu-id="6a933-185">You have the option to add a description.</span></span> <span data-ttu-id="6a933-186">Por último, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6a933-186">Finally, click **Create**.</span></span>

![Creación de runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="6a933-188">En el panel del editor del nuevo runbook, pegue el siguiente script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6a933-188">Paste the following PowerShell script in the editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get the connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in to Azure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set the following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for the storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="6a933-189">Si desea probar el script, seleccione **Panel de prueba**.</span><span class="sxs-lookup"><span data-stu-id="6a933-189">From the editor pane, choose **Test pane** to test your script.</span></span> <span data-ttu-id="6a933-190">Una vez que el script se ejecuta sin errores, puede seleccionar **Publicar** y aplicar después una programación para el runbook desde el panel de configuración.</span><span class="sxs-lookup"><span data-stu-id="6a933-190">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="6a933-191">Canalización de auditorías de Key Vault</span><span class="sxs-lookup"><span data-stu-id="6a933-191">Key Vault auditing pipeline</span></span>
<span data-ttu-id="6a933-192">Cuando configure un almacén de claves, puede habilitar la auditoría para que se recopilen registros de las solicitudes de acceso a dicho almacén.</span><span class="sxs-lookup"><span data-stu-id="6a933-192">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span></span> <span data-ttu-id="6a933-193">Estos registros se guardan en una cuenta de Azure Storage designada y pueden extraerse, supervisarse y analizarse.</span><span class="sxs-lookup"><span data-stu-id="6a933-193">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="6a933-194">El siguiente escenario usa instancias de Azure Functions, Azure Logic Apps y Key Vault para crear una canalización que envía un correo electrónico cuando una aplicación cuyo identificador coincide con el de la aplicación web recupera los secretos del almacén.</span><span class="sxs-lookup"><span data-stu-id="6a933-194">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span></span>

<span data-ttu-id="6a933-195">En primer lugar, debe habilitar los registros en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-195">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="6a933-196">Para ello, puede utilizar los siguientes comandos de PowerShell (consulte una explicación detallada en [key-vault-logging](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="6a933-196">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="6a933-197">Una vez habilitado, comenzarán a recopilarse registros de auditoría en la cuenta de almacenamiento designada.</span><span class="sxs-lookup"><span data-stu-id="6a933-197">After this is enabled, audit logs start collecting into the designated storage account.</span></span> <span data-ttu-id="6a933-198">Estos registros incluirán eventos acerca de qué usuario, cómo y cuándo ha obtenido acceso a los almacenes de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-198">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="6a933-199">Puede acceder a la información de registro 10 minutos después de la operación del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-199">You can access your logging information 10 minutes after the key vault operation.</span></span> <span data-ttu-id="6a933-200">Normalmente, tardará menos.</span><span class="sxs-lookup"><span data-stu-id="6a933-200">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="6a933-201">El siguiente paso consiste en la [creación de una cola de Azure Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="6a933-201">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="6a933-202">En ella se insertan los registros de auditoría del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-202">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="6a933-203">Cuando los mensajes de registro de auditoría se encuentran en la cola, la aplicación lógica los recopila y actúa sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="6a933-203">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span></span> <span data-ttu-id="6a933-204">Realice los siguientes pasos para crear una instancia de Service Bus:</span><span class="sxs-lookup"><span data-stu-id="6a933-204">Create a service bus with the following steps:</span></span>

1. <span data-ttu-id="6a933-205">Cree un espacio de nombres de Service Bus. Si ya tiene uno que quiera usar, puede saltar al paso 2.</span><span class="sxs-lookup"><span data-stu-id="6a933-205">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span></span>
2. <span data-ttu-id="6a933-206">Busque la instancia de Service Bus en Azure Portal y seleccione el espacio de nombres en el que quiere crear la cola.</span><span class="sxs-lookup"><span data-stu-id="6a933-206">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span></span>
3. <span data-ttu-id="6a933-207">Seleccione **Nuevo**, **Service Bus -> Cola** y especifique los datos necesarios.</span><span class="sxs-lookup"><span data-stu-id="6a933-207">Select **New** and choose **Service Bus > Queue** and enter the required details.</span></span>
4. <span data-ttu-id="6a933-208">Seleccione la información de la conexión de Service Bus. Para ello, elija el espacio de nombres y haga clic en **Información de conexión**.</span><span class="sxs-lookup"><span data-stu-id="6a933-208">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="6a933-209">Va a necesitar esta información en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="6a933-209">You will need this information for the next section.</span></span>

<span data-ttu-id="6a933-210">A continuación, debe [crear una función de Azure](../azure-functions/functions-create-first-azure-function.md) para sondear los registros del almacén de claves incluidos en la cuenta de almacenamiento y recopilar nuevos eventos.</span><span class="sxs-lookup"><span data-stu-id="6a933-210">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span></span> <span data-ttu-id="6a933-211">Esta función se desencadenará en función de una programación.</span><span class="sxs-lookup"><span data-stu-id="6a933-211">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="6a933-212">Cree una función de Azure. Para ello, elija **Nuevo -> Function App** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6a933-212">To create an Azure function, choose **New > Function App** in the Azure portal.</span></span> <span data-ttu-id="6a933-213">Durante el proceso de creación, puede usar un plan de hospedaje existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="6a933-213">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="6a933-214">También puede utilizar un plan de hospedaje dinámico.</span><span class="sxs-lookup"><span data-stu-id="6a933-214">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="6a933-215">Encontrará más información sobre las opciones de hospedaje de funciones en [Escalado de Azure Functions](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="6a933-215">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="6a933-216">Una vez creada la función de Azure, acceda a ella y elija una función de temporizador y C\#.</span><span class="sxs-lookup"><span data-stu-id="6a933-216">When the Azure function is created, navigate to it and choose a timer function and C\#.</span></span> <span data-ttu-id="6a933-217">A continuación, haga clic en **Crear esta función**.</span><span class="sxs-lookup"><span data-stu-id="6a933-217">Then click **Create this function**.</span></span>

![Hoja de inicio de Azure Functions](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="6a933-219">En la pestaña **Desarrollar**, sustituya el código de run.csx por el siguiente:</span><span class="sxs-lookup"><span data-stu-id="6a933-219">On the **Develop** tab, replace the run.csx code with the following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting to now.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required to order by time as they may not be in the file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending to ServiceBus, use the payloadStream and set keeporiginal to true
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="6a933-220">No olvide reemplazar las variables del código anterior para que apunten a la cuenta de almacenamiento en la que se escriben los registros de Key Vault, al Service Bus que creó anteriormente y a la ruta de acceso específica de los registros de almacenamiento del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-220">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span></span>
>
>

<span data-ttu-id="6a933-221">La función selecciona el archivo de registro más reciente de la cuenta de almacenamiento en la que se escriben los registros del almacén de claves, recopila los últimos eventos de ese archivo y los inserta en una cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6a933-221">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span></span> <span data-ttu-id="6a933-222">Como un único archivo puede tener varios eventos, debe crear un archivo sync.txt. La función también consultará este archivo para determinar la marca de tiempo del último evento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="6a933-222">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span></span> <span data-ttu-id="6a933-223">De este modo, se asegura de que no se inserta el mismo evento varias veces.</span><span class="sxs-lookup"><span data-stu-id="6a933-223">This ensures that you don't push the same event multiple times.</span></span> <span data-ttu-id="6a933-224">Este archivo sync.txt contiene la marca de tiempo del último evento encontrado.</span><span class="sxs-lookup"><span data-stu-id="6a933-224">This sync.txt file contains a timestamp for the last encountered event.</span></span> <span data-ttu-id="6a933-225">Cuando los registros se han cargado, deben ordenarse con arreglo a la marca de tiempo para garantizar que el orden es el correcto.</span><span class="sxs-lookup"><span data-stu-id="6a933-225">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span></span>

<span data-ttu-id="6a933-226">En esta función, vamos a hacer referencia a un par de bibliotecas adicionales que no están disponibles de forma predeterminada en Funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a933-226">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span></span> <span data-ttu-id="6a933-227">Para incluir estas bibliotecas, necesitamos que Azure Functions las extraiga mediante NuGet.</span><span class="sxs-lookup"><span data-stu-id="6a933-227">To include these, we need Azure Functions to pull them using NuGet.</span></span> <span data-ttu-id="6a933-228">Elija la opción **Ver archivos**.</span><span class="sxs-lookup"><span data-stu-id="6a933-228">Choose the **View Files** option.</span></span>

![Opción Ver archivos](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="6a933-230">Y agregue un archivo denominado project.json con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="6a933-230">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="6a933-231">Cuando haga clic en **Guardar**, Azure Functions descargará los binarios necesarios.</span><span class="sxs-lookup"><span data-stu-id="6a933-231">Upon **Save**, Azure Functions will download the required binaries.</span></span>

<span data-ttu-id="6a933-232">Cambie a la pestaña **Integrar** y asigne al parámetro del temporizador un nombre descriptivo para usarlo en la función.</span><span class="sxs-lookup"><span data-stu-id="6a933-232">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span></span> <span data-ttu-id="6a933-233">En el código anterior, el nombre esperado para el temporizador es *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="6a933-233">In the preceding code, it expects the timer to be called *myTimer*.</span></span> <span data-ttu-id="6a933-234">Especifique una [expresión CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) del modo siguiente: 0 \* \* \* \* \* para el temporizador que hará que la función se ejecute una vez por minuto.</span><span class="sxs-lookup"><span data-stu-id="6a933-234">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span></span>

<span data-ttu-id="6a933-235">En la misma pestaña **Integrar**, agregue una entrada que sea del tipo **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="6a933-235">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span></span> <span data-ttu-id="6a933-236">Esta entrada apuntará al archivo sync.txt , que contiene la marca de tiempo del último evento que consultó la función.</span><span class="sxs-lookup"><span data-stu-id="6a933-236">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span></span> <span data-ttu-id="6a933-237">El parámetro name se encargará de que esté disponible en la función.</span><span class="sxs-lookup"><span data-stu-id="6a933-237">This will be available within the function by the parameter name.</span></span> <span data-ttu-id="6a933-238">En el código anterior, la entrada de Azure Blob Storage espera que el parámetro name sea *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="6a933-238">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span></span> <span data-ttu-id="6a933-239">Elija la cuenta de almacenamiento donde residirá el archivo sync.txt (puede ser la misma o una diferente).</span><span class="sxs-lookup"><span data-stu-id="6a933-239">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span></span> <span data-ttu-id="6a933-240">En el campo ruta de acceso, proporcione la ruta donde se encuentra el archivo en el formato {nombre-contenedor}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="6a933-240">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="6a933-241">Agregue una salida que sea de tipo *Azure Blob Storage*.</span><span class="sxs-lookup"><span data-stu-id="6a933-241">Add an output of the type *Azure Blob Storage* output.</span></span> <span data-ttu-id="6a933-242">Esta salida también apuntará al archivo sync.txt que definió en la entrada.</span><span class="sxs-lookup"><span data-stu-id="6a933-242">This will point to the sync.txt file you defined in the input.</span></span> <span data-ttu-id="6a933-243">La función utilizará esta salida para escribir la marca de tiempo del último evento que consultó.</span><span class="sxs-lookup"><span data-stu-id="6a933-243">This is used by the function to write the timestamp of the last event looked at.</span></span> <span data-ttu-id="6a933-244">En el código anterior, el nombre esperado para esta parámetro es *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="6a933-244">The preceding code expects this parameter to be called *outputBlob*.</span></span>

<span data-ttu-id="6a933-245">Llegados a este punto, la función ya está lista.</span><span class="sxs-lookup"><span data-stu-id="6a933-245">At this point, the function is ready.</span></span> <span data-ttu-id="6a933-246">No olvide volver a la pestaña **Desarrollar** y guardar el código.</span><span class="sxs-lookup"><span data-stu-id="6a933-246">Make sure to switch back to the **Develop** tab and save the code.</span></span> <span data-ttu-id="6a933-247">Compruebe en la ventana de salida si hay algún error de compilación y, de ser así, corrija los errores como corresponda.</span><span class="sxs-lookup"><span data-stu-id="6a933-247">Check the output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="6a933-248">Si el código se compila correctamente, debería ya comprobar cada minuto los registros del almacén de claves e insertar los nuevos eventos en la cola de Service Bus definida.</span><span class="sxs-lookup"><span data-stu-id="6a933-248">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span></span> <span data-ttu-id="6a933-249">Cada vez que la función se desencadena, debería aparecer la información de los registros en la ventana del registro.</span><span class="sxs-lookup"><span data-stu-id="6a933-249">You should see logging information write out to the log window every time the function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="6a933-250">Aplicación lógica de Azure</span><span class="sxs-lookup"><span data-stu-id="6a933-250">Azure logic app</span></span>
<span data-ttu-id="6a933-251">Ahora, debe crear una aplicación lógica de Azure que seleccione los eventos que la función inserta en la cola de Service Bus, analice el contenido y envíe un correo electrónico si se cumple una determinada condición.</span><span class="sxs-lookup"><span data-stu-id="6a933-251">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="6a933-252">[Cree una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) en **Nuevo -> Aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="6a933-252">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span></span>

<span data-ttu-id="6a933-253">Una vez creada, acceda a ella y elija **editar**.</span><span class="sxs-lookup"><span data-stu-id="6a933-253">Once the logic app is created, navigate to it and choose **edit**.</span></span> <span data-ttu-id="6a933-254">En el editor de la aplicación lógica, elija la **cola de Service Bus** y especifique las credenciales de Service Bus para conectarla a la cola.</span><span class="sxs-lookup"><span data-stu-id="6a933-254">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span></span>

![Bus de servicio de la aplicación lógica de Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="6a933-256">A continuación, elija **Agregar una condición**.</span><span class="sxs-lookup"><span data-stu-id="6a933-256">Next choose **Add a condition**.</span></span> <span data-ttu-id="6a933-257">En la condición, cambie al editor avanzado y escriba el código siguiente (no olvide cambiar APP_ID por el valor real de APP_ID de la aplicación web):</span><span class="sxs-lookup"><span data-stu-id="6a933-257">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="6a933-258">En esencia, esta expresión devolverá **false** si la propiedad *appid* del evento entrante (que es el cuerpo del mensaje de Service Bus) no es el *appid* de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6a933-258">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span></span>

<span data-ttu-id="6a933-259">Ahora, cree una acción en la opción **If no, do nothing** (Si no, no hacer nada).</span><span class="sxs-lookup"><span data-stu-id="6a933-259">Now, create an action under **If no, do nothing**.</span></span>

![Elegir una acción en la aplicación lógica de Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="6a933-261">En la acción, elija **Office 365 - send email**(Office 365 - enviar correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="6a933-261">For the action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="6a933-262">Rellene los campos para crear el correo electrónico que se enviará cuando la condición definida devuelva **false**.</span><span class="sxs-lookup"><span data-stu-id="6a933-262">Fill out the fields to create an email to send when the defined condition returns **false**.</span></span> <span data-ttu-id="6a933-263">Si no tiene Office 365, puede buscar otras alternativas para conseguir los mismos resultados.</span><span class="sxs-lookup"><span data-stu-id="6a933-263">If you do not have Office 365, you could look at alternatives to achieve the same results.</span></span>

<span data-ttu-id="6a933-264">En este momento, tiene una canalización integral que, una vez por minuto, busca nuevos registros de auditoría del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="6a933-264">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="6a933-265">Inserta los nuevos registros que encuentra en una cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6a933-265">It pushes new logs it finds to a service bus queue.</span></span> <span data-ttu-id="6a933-266">La aplicación lógica se activa cuando un nuevo mensaje llega a la cola.</span><span class="sxs-lookup"><span data-stu-id="6a933-266">The logic app is triggered when a new message lands in the queue.</span></span> <span data-ttu-id="6a933-267">Si el *appid* dentro del evento no coincide con el identificador de la aplicación de la aplicación que llama, envía un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="6a933-267">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span></span>
