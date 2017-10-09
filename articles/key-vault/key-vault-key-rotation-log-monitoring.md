---
title: "aaaSet el almacén de claves de Azure con la rotación de clave-to-end y auditoría | Documentos de Microsoft"
description: "Utilice este tootoohelp de cómo que obtener configurar con la rotación de claves y supervisión de los registros de almacén de claves."
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
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="7bcac-103">Configuración de Azure Key Vault con la auditoría y la rotación de claves de un extremo a otro</span><span class="sxs-lookup"><span data-stu-id="7bcac-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="7bcac-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="7bcac-104">Introduction</span></span>
<span data-ttu-id="7bcac-105">Después de crear el almacén de claves, será capaz de toostart con ese almacén toostore sus claves y secretos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="7bcac-106">Las aplicaciones ya no necesitan toopersist los secretos o claves, pero en su lugar solicitan desde el almacén de claves de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7bcac-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="7bcac-107">Esto le permite tooupdate claves y secretos sin afectar al comportamiento de saludo de la aplicación, lo que abre una amplia gama de posibilidades alrededor de la clave y la administración de secretos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="7bcac-108">Este artículo le guía a través de un ejemplo del uso de almacén de claves de Azure toostore un secreto, en este caso, una clave de cuenta de almacenamiento de Azure que se tiene acceso a una aplicación.</span><span class="sxs-lookup"><span data-stu-id="7bcac-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="7bcac-109">El artículo también incluye una demostración de la implementación de una rotación programada de dicha clave.</span><span class="sxs-lookup"><span data-stu-id="7bcac-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="7bcac-110">Por último, le guía a través de una demostración de cómo toomonitor Hola registros de auditoría de almacén de claves y generar alertas cuando se realizan las solicitudes inesperadas.</span><span class="sxs-lookup"><span data-stu-id="7bcac-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="7bcac-111">Este tutorial no está previsto tooexplain en detalle Hola inicial el programa de instalación de su almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7bcac-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="7bcac-112">Para obtener información, consulte [Introducción al Almacén de claves de Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7bcac-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="7bcac-113">Para obtener instrucciones acerca de la interfaz de la línea de comandos para todas las plataformas, consulte [Administración del almacén de claves mediante CLI](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="7bcac-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="7bcac-114">Configuración del Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="7bcac-114">Set up Key Vault</span></span>
<span data-ttu-id="7bcac-115">tooenable un tooretrieve un secreto de aplicación desde el almacén de claves, primero debe crear Hola secreto y cargarlo en el almacén de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7bcac-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="7bcac-116">Esto puede realizarse a partir de una sesión de PowerShell de Azure y firma en tooyour cuenta de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7bcac-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="7bcac-117">En la ventana emergente del explorador de hello, escriba el nombre de usuario de cuenta de Azure y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="7bcac-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="7bcac-118">PowerShell obtendrá todas las suscripciones de Hola que están asociadas a esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="7bcac-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="7bcac-119">PowerShell utiliza Hola primera de ellas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="7bcac-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="7bcac-120">Si tiene varias suscripciones, podría tener que toospecify Hola uno que estaba toocreate usa el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7bcac-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="7bcac-121">Escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:</span><span class="sxs-lookup"><span data-stu-id="7bcac-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="7bcac-122">suscripción de hello toospecify que esté asociada con el almacén de claves de hello iniciará la sesión, escriba:</span><span class="sxs-lookup"><span data-stu-id="7bcac-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="7bcac-123">Dado que en este artículo se explica cómo se guarda una clave de cuenta de almacenamiento como un secreto, debe obtener dicha clave.</span><span class="sxs-lookup"><span data-stu-id="7bcac-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="7bcac-124">Después de recuperar el secreto (en este caso, la clave de cuenta de almacenamiento), debe convertir esa cadena segura tooa y, a continuación, crear un secreto con ese valor en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7bcac-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="7bcac-125">A continuación, obtener Hola URI secreto Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="7bcac-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="7bcac-126">Cuando se llama a tooretrieve de almacén de claves de Hola la clave secreta se utiliza en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="7bcac-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="7bcac-127">Ejecute el siguiente comando de PowerShell de Hola y tome nota del valor de identificador hello, que es el secreto de hello URI:</span><span class="sxs-lookup"><span data-stu-id="7bcac-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="7bcac-128">Configurar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="7bcac-128">Set up hello application</span></span>
<span data-ttu-id="7bcac-129">Ahora que tiene un secreto almacenado, puede usar código tooretrieve y usarlo.</span><span class="sxs-lookup"><span data-stu-id="7bcac-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="7bcac-130">Hay unos pocos pasos a necesario tooachieve esto.</span><span class="sxs-lookup"><span data-stu-id="7bcac-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="7bcac-131">Hello paso primero y el más importante es registrando su aplicación con Azure Active Directory y, a continuación, que el almacén de claves se indica en la información de la aplicación para que pueden permitir que las solicitudes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7bcac-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="7bcac-132">La aplicación debe crearse en hello mismo inquilino de Azure Active Directory como su almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7bcac-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="7bcac-133">Abra la ficha de hello aplicaciones de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcac-133">Open hello applications tab of Azure Active Directory.</span></span>

![Abra las aplicaciones de Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="7bcac-135">Elija **agregar** tooadd una tooyour de aplicación Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcac-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![Elija AGREGAR](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="7bcac-137">Deje el tipo de aplicación Hola como **aplicación WEB Y/O API de WEB** y asigne un nombre a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7bcac-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Aplicación hello nombre](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="7bcac-139">Especifique un valor en **URL DE INICIO DE SESIÓN** y en **URI DE ID DE APLICACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="7bcac-140">En esta demostración, puede especificar los valores que desee y cambiarlos más adelante si es necesario.</span><span class="sxs-lookup"><span data-stu-id="7bcac-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Especifique los identificadores URI necesarios](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="7bcac-142">Después de agrega tooAzure Active Directory de la aplicación hello, aparecerá en la página de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="7bcac-143">Haga clic en hello **configurar** ficha y, a continuación, busque y copie hello **Id. de cliente** valor.</span><span class="sxs-lookup"><span data-stu-id="7bcac-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="7bcac-144">Tome nota del identificador de cliente de hello en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="7bcac-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="7bcac-145">A continuación, genere una clave para su aplicación para que pueda interactuar con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcac-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="7bcac-146">Puede crear en hello **claves** sección Hola **configuración** ficha. Tome nota de la clave de hello recién generado desde su aplicación de Azure Active Directory para su uso en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="7bcac-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Claves de aplicaciones de Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="7bcac-148">Antes de establecer las llamadas desde la aplicación en el almacén de claves de hello, debe indicar el almacén de claves de hello acerca de la aplicación y sus permisos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="7bcac-149">Hello comando siguiente toma el nombre del almacén de Hola y Hola Id. de cliente de la aplicación de Azure Active Directory y concede **obtener** almacén de claves de tooyour de acceso para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7bcac-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="7bcac-150">En este punto, está listo toostart compilar su aplicación llama.</span><span class="sxs-lookup"><span data-stu-id="7bcac-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="7bcac-151">En su aplicación, debe instalar paquetes de NuGet hello toointeract necesario con el almacén de claves de Azure y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcac-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="7bcac-152">Desde la consola de administrador de paquetes de Visual Studio de hello, escriba Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="7bcac-153">En la escritura de Hola de este artículo, versión actual de hello del paquete de Azure Active Directory hello es 3.10.305231913, por lo que podría desea la versión más reciente de tooconfirm hello y actualizar en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="7bcac-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="7bcac-154">En el código de aplicación, cree un método de clase toohold hello para la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcac-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="7bcac-155">En este ejemplo, la clase se llama **Utils**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="7bcac-156">Agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="7bcac-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="7bcac-157">A continuación, agregue Hola siguiendo el token de JWT de método tooretrieve Hola de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bcac-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="7bcac-158">Para el mantenimiento, puede que desee valores de cadena codificados de forma rígida de hello toomove en su configuración de aplicación o web.</span><span class="sxs-lookup"><span data-stu-id="7bcac-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="7bcac-159">Agregar Hola código necesario toocall el almacén de claves y recuperar su valor secreto.</span><span class="sxs-lookup"><span data-stu-id="7bcac-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="7bcac-160">En primer lugar debe agregar la siguiente Hola instrucción using:</span><span class="sxs-lookup"><span data-stu-id="7bcac-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="7bcac-161">Agregar tooinvoke de llamadas de método hello el almacén de claves y recuperar la clave secreta.</span><span class="sxs-lookup"><span data-stu-id="7bcac-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="7bcac-162">En este método, se proporcione el secreto de hello URI que guardó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="7bcac-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="7bcac-163">Tenga en cuenta use Hola de hello **GetToken** método de hello **Utils** clase creada previamente.</span><span class="sxs-lookup"><span data-stu-id="7bcac-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="7bcac-164">Al ejecutar la aplicación, ahora se deben autenticar tooAzure Active Directory y, a continuación, recuperar el valor secreto desde el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bcac-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="7bcac-165">Rotación de claves mediante Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7bcac-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="7bcac-166">Existen varias opciones para implementar una estrategia de rotación de los valores que se guardan como secretos del Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bcac-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="7bcac-167">Los secretos pueden rotarse mediante un proceso manual, mediante programación a través de llamadas a API o mediante un script de automatización.</span><span class="sxs-lookup"><span data-stu-id="7bcac-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="7bcac-168">Para fines de Hola de este artículo, estará usando Azure PowerShell combinado con automatización de Azure toochange una tecla de acceso de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bcac-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="7bcac-169">A continuación, podrá actualizar un secreto del almacén de claves con esa nueva clave.</span><span class="sxs-lookup"><span data-stu-id="7bcac-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="7bcac-170">tooallow automatización de Azure tooset secretos valores en el almacén de claves, debe obtener Id. de cliente de Hola para conexión de hello denominada AzureRunAsConnection, que se creó cuando se establece la instancia de automatización de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bcac-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="7bcac-171">Para encontrar este identificador, seleccione **Recursos** en la instancia de Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="7bcac-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="7bcac-172">Desde allí, elija **conexiones** y, a continuación, seleccione hello **AzureRunAsConnection** principal de servicio.</span><span class="sxs-lookup"><span data-stu-id="7bcac-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="7bcac-173">Tome nota de hello **identificador de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-173">Take note of hello **Application ID**.</span></span>

![Identificador de cliente de Azure Automation](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="7bcac-175">En **Recursos**, elija **Módulos**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="7bcac-176">De **módulos**, seleccione **galería**y, a continuación, busque y **importación** versiones actualizadas de cada uno de hello siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="7bcac-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="7bcac-177">En la escritura de Hola de este artículo, solo hello toobe módulos se indicó anteriormente que necesita se actualiza para hello siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="7bcac-178">Si se produce algún error en el trabajo de automatización, confirme que ha importado todos los módulos necesarios y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="7bcac-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="7bcac-179">Después de recuperar los Id. de aplicación de hello para la conexión de automatización de Azure, debe indicar que el almacén de claves que esta aplicación tiene acceso tooupdate secretos en el almacén.</span><span class="sxs-lookup"><span data-stu-id="7bcac-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="7bcac-180">Esto puede realizarse con hello siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7bcac-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="7bcac-181">A continuación, seleccione **Runbooks** en la instancia de Azure Automation y, después, seleccione **Agregar un runbook**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="7bcac-182">Seleccione **Creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-182">Select **Quick Create**.</span></span> <span data-ttu-id="7bcac-183">Nombre del runbook y seleccione **PowerShell** como tipo de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="7bcac-184">Tener Hola opción tooadd una descripción.</span><span class="sxs-lookup"><span data-stu-id="7bcac-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="7bcac-185">Por último, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-185">Finally, click **Create**.</span></span>

![Creación de runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="7bcac-187">Pegue el siguiente script de PowerShell en el panel del editor de hello para el nuevo runbook de hello:</span><span class="sxs-lookup"><span data-stu-id="7bcac-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
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

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="7bcac-188">En el panel del editor de hello, elija **panel prueba** tootest la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="7bcac-189">Una vez que se ejecuta el script de Hola sin errores, puede seleccionar **publicar**, y, a continuación, puede aplicar una programación de runbook de hello en el panel de configuración de runbook de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="7bcac-190">Canalización de auditorías de Key Vault</span><span class="sxs-lookup"><span data-stu-id="7bcac-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="7bcac-191">Al configurar un almacén de claves, puede activar la auditoría de registros toocollect en las solicitudes de acceso realizadas toohello el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7bcac-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="7bcac-192">Estos registros se guardan en una cuenta de Azure Storage designada y pueden extraerse, supervisarse y analizarse.</span><span class="sxs-lookup"><span data-stu-id="7bcac-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="7bcac-193">Hello siguiente escenario utiliza las funciones de Azure, las aplicaciones de Azure lógica y toocreate de registros de auditoría de almacén de claves un toosend canalización un correo electrónico cuando una aplicación que coinciden con el identificador de la aplicación hello de aplicación web de hello recupera los secretos del almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="7bcac-194">En primer lugar, debe habilitar los registros en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7bcac-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="7bcac-195">Esto puede hacerse a través de hello siga los comandos de PowerShell (se pueden ver detalles completos en [clave de registro de almacén](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="7bcac-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="7bcac-196">Después de que esta opción está habilitada, los registros de auditoría comenzar a recopilar en hello designado de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7bcac-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="7bcac-197">Estos registros incluirán eventos acerca de qué usuario, cómo y cuándo ha obtenido acceso a los almacenes de claves.</span><span class="sxs-lookup"><span data-stu-id="7bcac-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="7bcac-198">Puede tener acceso a la información de registro de 10 minutos tras la operación de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="7bcac-199">Normalmente, tardará menos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="7bcac-200">paso siguiente Hello es demasiado[crear una cola de Service Bus de Azure](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="7bcac-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="7bcac-201">En ella se insertan los registros de auditoría del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="7bcac-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="7bcac-202">Una vez mensajes de registro de auditoría de hello en cola hello, aplicación de lógica de hello ellos recoge y actúa sobre ellos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="7bcac-203">Cree un bus de servicio con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="7bcac-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="7bcac-204">Crear un espacio de nombres de Bus de servicio (si ya tiene una que desee toouse para ello, omitir tooStep 2).</span><span class="sxs-lookup"><span data-stu-id="7bcac-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="7bcac-205">Examinar bus de servicio toohello Hola portal de Azure y espacio de nombres de hello seleccione en que desea toocreate cola de hello.</span><span class="sxs-lookup"><span data-stu-id="7bcac-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="7bcac-206">Seleccione **New** y elija **Bus de servicio > cola** y escriba los detalles de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="7bcac-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="7bcac-207">Seleccione la información de conexión de Bus de servicio de hello eligiendo el espacio de nombres de Hola y haga clic en **información de conexión**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="7bcac-208">Necesitará esta información para la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="7bcac-209">Después, [crea una función Azure](../azure-functions/functions-create-first-azure-function.md) toopoll registros de almacén de claves en Hola cuenta de almacenamiento y recogida de los nuevos eventos.</span><span class="sxs-lookup"><span data-stu-id="7bcac-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="7bcac-210">Esta función se desencadenará en función de una programación.</span><span class="sxs-lookup"><span data-stu-id="7bcac-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="7bcac-211">toocreate una función de Azure, elija **nuevo > aplicación de la función** Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bcac-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="7bcac-212">Durante el proceso de creación, puede usar un plan de hospedaje existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="7bcac-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="7bcac-213">También puede utilizar un plan de hospedaje dinámico.</span><span class="sxs-lookup"><span data-stu-id="7bcac-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="7bcac-214">Se pueden encontrar más detalles en función de opciones de hospedaje en [cómo tooscale funciones de Azure](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7bcac-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="7bcac-215">Cuando se crea la función Azure hello, navegar tooit y elegir un temporizador de función y C\#.</span><span class="sxs-lookup"><span data-stu-id="7bcac-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="7bcac-216">A continuación, haga clic en **Crear esta función**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-216">Then click **Create this function**.</span></span>

![Hoja de inicio de Azure Functions](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="7bcac-218">En hello **desarrollar** ficha, reemplace el código de hello run.csx por siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="7bcac-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

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
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
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

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
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

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="7bcac-219">Asegúrese de variables de hello tooreplace seguro en hello anterior cuenta de almacenamiento de código toopoint tooyour donde se escriben los registros de almacén de claves de hello, bus de servicio de Hola que creó anteriormente, y Hola registros de almacenamiento de almacén de claves de toohello de ruta de acceso específica.</span><span class="sxs-lookup"><span data-stu-id="7bcac-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="7bcac-220">función Hello recoge Hola último archivo de registro de cuenta de almacenamiento de Hola donde se escriben los registros de almacén de claves de hello, grabs Hola los eventos más recientes de ese archivo, y los envía tooa cola de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="7bcac-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="7bcac-221">Dado que un único archivo puede tener varios eventos, debe crear un archivo de sync.txt que función hello también busca en marca de tiempo de hello toodetermine de evento último Hola que ha recogido.</span><span class="sxs-lookup"><span data-stu-id="7bcac-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="7bcac-222">Esto garantiza que no insertará Hola mismo evento varias veces.</span><span class="sxs-lookup"><span data-stu-id="7bcac-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="7bcac-223">Este archivo sync.txt contiene una marca de tiempo para el último suceso de encontró Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="7bcac-224">registros, cuando carga, Hello tienen toobe ordenado según hello tooensure de marca de tiempo que están ordenados correctamente.</span><span class="sxs-lookup"><span data-stu-id="7bcac-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="7bcac-225">Para esta función, se hacen referencia a un par de bibliotecas adicionales que no están disponibles fuera del cuadro de hello en funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bcac-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="7bcac-226">tooinclude estos, necesitamos toopull de funciones de Azure mediante NuGet.</span><span class="sxs-lookup"><span data-stu-id="7bcac-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="7bcac-227">Elija hello **ver archivos** opción.</span><span class="sxs-lookup"><span data-stu-id="7bcac-227">Choose hello **View Files** option.</span></span>

![Opción Ver archivos](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="7bcac-229">Y agregue un archivo denominado project.json con el contenido siguiente:</span><span class="sxs-lookup"><span data-stu-id="7bcac-229">And add a file called project.json with following content:</span></span>

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
<span data-ttu-id="7bcac-230">Tras **guardar**, funciones de Azure descargará los archivos binarios de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="7bcac-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="7bcac-231">Cambiar toohello **integrar** pestaña y asigne un toouse nombre descriptivo en función de Hola de parámetro de temporizador de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="7bcac-232">En el anterior código de hello, espera Hola temporizador toobe llama *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="7bcac-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="7bcac-233">Especifique un [expresión CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) como sigue: 0 \* \* \* \* \* temporizador Hola que causará Hola función toorun una vez por minuto.</span><span class="sxs-lookup"><span data-stu-id="7bcac-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="7bcac-234">Hola en mismo **integrar** ficha, agregue una entrada de tipo hello **almacenamiento de blobs de Azure**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="7bcac-235">Esto señala toohello sync.txt archivo que contiene la marca de tiempo de hello del último evento de hello examinado por función hello.</span><span class="sxs-lookup"><span data-stu-id="7bcac-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="7bcac-236">Esta opción estará disponible en función de Hola por nombre de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="7bcac-237">En el anterior código de hello, proporcionados por el almacenamiento de blobs de Azure Hola espera toobe de nombre de parámetro de Hola *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="7bcac-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="7bcac-238">Elegir cuenta de almacenamiento de Hola dónde se ubicará el archivo de hello sync.txt (podría ser Hola misma o a una cuenta de almacenamiento diferente).</span><span class="sxs-lookup"><span data-stu-id="7bcac-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="7bcac-239">En el campo de ruta de acceso de hello, proporcione la ruta de acceso de Hola donde reside el archivo hello en formato de Hola {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="7bcac-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="7bcac-240">Agregar una salida de tipo hello *almacenamiento de blobs de Azure* salida.</span><span class="sxs-lookup"><span data-stu-id="7bcac-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="7bcac-241">Esto señala toohello sync.txt archivo definido en la entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="7bcac-242">Se utiliza por hello función toowrite Hola marca de tiempo del último evento de hello examinado.</span><span class="sxs-lookup"><span data-stu-id="7bcac-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="7bcac-243">código anterior Hello espera este toobe parámetro denominado *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="7bcac-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="7bcac-244">En este momento, la función hello está listo.</span><span class="sxs-lookup"><span data-stu-id="7bcac-244">At this point, hello function is ready.</span></span> <span data-ttu-id="7bcac-245">Realizar tooswitch seguro atrás toohello **desarrollar** pestaña y guarde el código de hello.</span><span class="sxs-lookup"><span data-stu-id="7bcac-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="7bcac-246">Consulte la ventana de salida de hello para los errores de compilación y corríjalos según corresponda.</span><span class="sxs-lookup"><span data-stu-id="7bcac-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="7bcac-247">Si se compila el código de hello, código de hello debe ahora puede comprobar los registros de almacén de claves de hello cada minuto y e inserta los nuevos eventos en hello define la cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7bcac-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="7bcac-248">Debería ver la información del registro escribir toohello la ventana de registro cada vez que se desencadene la función hello.</span><span class="sxs-lookup"><span data-stu-id="7bcac-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="7bcac-249">Aplicación lógica de Azure</span><span class="sxs-lookup"><span data-stu-id="7bcac-249">Azure logic app</span></span>
<span data-ttu-id="7bcac-250">A continuación debe crear una aplicación de Azure lógica que recoge los eventos de Hola que función hello insertando toohello cola de Bus de servicio, analiza el contenido de Hola y envía un correo electrónico basado en una condición que se buscan coincidencias.</span><span class="sxs-lookup"><span data-stu-id="7bcac-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="7bcac-251">[Crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md) yendo demasiado**nuevo > aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="7bcac-252">Una vez que se crea la aplicación de la lógica de hello, navegar tooit y elegir **editar**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="7bcac-253">Editor de aplicación lógica de hello, elija **cola de Service Bus** y escriba su tooconnect de credenciales de Bus de servicio se toohello cola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Bus de servicio de la aplicación lógica de Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="7bcac-255">A continuación, elija **Agregar una condición**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="7bcac-256">En la condición de hello, cambie toohello advanced editor y escriba Hola siguiente código, reemplazando id_aplicación con hello id_aplicación real de la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="7bcac-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="7bcac-257">Esta expresión devuelve básicamente **false** si hello *appid* de hello evento de entrada (que es el cuerpo de Hola de mensajes de bienvenida del Bus de servicio) no es Hola *appid* de hello aplicación.</span><span class="sxs-lookup"><span data-stu-id="7bcac-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="7bcac-258">Ahora, cree una acción en la opción **If no, do nothing** (Si no, no hacer nada).</span><span class="sxs-lookup"><span data-stu-id="7bcac-258">Now, create an action under **If no, do nothing**.</span></span>

![Elegir una acción en la aplicación lógica de Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="7bcac-260">Para la acción de hello, elija **Office 365: enviar correo electrónico**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="7bcac-261">Rellene Hola campos toocreate un toosend de correo electrónico cuando Hola define la condición devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="7bcac-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="7bcac-262">Si no tiene Office 365, puede mirar alternativas tooachieve Hola los mismos resultados.</span><span class="sxs-lookup"><span data-stu-id="7bcac-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="7bcac-263">En este punto, tiene una canalización de tooend final que comprueba si hay nuevos registros de auditoría de almacén de claves una vez por minuto.</span><span class="sxs-lookup"><span data-stu-id="7bcac-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="7bcac-264">Inserta nuevos registros encuentra tooa cola de bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="7bcac-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="7bcac-265">aplicación de la lógica de Hola se desencadena cuando se llega a un nuevo mensaje de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bcac-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="7bcac-266">Si hello *appid* dentro de hello eventos no coincide con Id. de aplicación Hola de hello llamar a la aplicación, envía un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="7bcac-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
