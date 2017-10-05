---
title: "Conexión segura a un clúster de Azure Service Fabric | Microsoft Docs"
description: "Se describe cómo autenticar el acceso de cliente a un clúster de Service Fabric y cómo proteger la comunicación entre los clientes y un clúster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: d6a13ceb8ccd9207ecacc166247535d496d5dec7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="8acae-103">Conexión a un clúster seguro</span><span class="sxs-lookup"><span data-stu-id="8acae-103">Connect to a secure cluster</span></span>

<span data-ttu-id="8acae-104">Cuando un cliente se conecta a un nodo del clúster de Service Fabric, se puede autenticar al cliente y establecer la comunicación segura mediante la seguridad basada en certificados o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="8acae-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="8acae-105">Esta autenticación garantiza que solo los usuarios autorizados pueden tener acceso al clúster, y a las aplicaciones implementadas, y realizar tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="8acae-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="8acae-106">Con anterioridad se debe haber habilitado la seguridad basada en certificados o AAD en el clúster cuando se creó este.</span><span class="sxs-lookup"><span data-stu-id="8acae-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="8acae-107">Para más información sobre escenarios de seguridad de clúster, consulte [Protección de un clúster de Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="8acae-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="8acae-108">Si se conecta a un clúster protegido con certificados, [configure el certificado de cliente](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) en el equipo que se conectará al clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="8acae-109">Conexión a un clúster seguro con la CLI de Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="8acae-109">Connect to a secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="8acae-110">Hay varias maneras distintas de conectarse a un clúster seguro con la CLI de Service Fabric (sfctl).</span><span class="sxs-lookup"><span data-stu-id="8acae-110">There are a few different ways to connect to a secure cluster using the Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="8acae-111">Cuando se utiliza un certificado de cliente para la autenticación, los detalles del certificado deben coincidir con un certificado implementado en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-111">When using a client certificate for authentication, the certificate details must match a certificate deployed to the cluster nodes.</span></span> <span data-ttu-id="8acae-112">Si el certificado tiene entidades de certificación (CA), debe especificar además las entidades de certificación de confianza.</span><span class="sxs-lookup"><span data-stu-id="8acae-112">If your certificate has Certificate Authorities (CAs), you need to additionally specify the trusted CAs.</span></span>

<span data-ttu-id="8acae-113">Puede conectarse a un clúster con el comando `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="8acae-113">You can connect to a cluster using the `sfctl cluster select` command.</span></span>

<span data-ttu-id="8acae-114">Los certificados de cliente se pueden especificar de dos maneras diferentes, como un par de clave y certificado, o como un archivo pem único.</span><span class="sxs-lookup"><span data-stu-id="8acae-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="8acae-115">Para archivos `pem` protegidos mediante contraseña, se le solicitará automáticamente que escriba la contraseña.</span><span class="sxs-lookup"><span data-stu-id="8acae-115">For password protected `pem` files, you will be prompted automatically to enter the password.</span></span>

<span data-ttu-id="8acae-116">Para especificar el certificado de cliente como un archivo pem, especifique la ruta de acceso de archivo en el argumento `--pem`.</span><span class="sxs-lookup"><span data-stu-id="8acae-116">To specify the client certificate as a pem file, specify the file path in the `--pem` argument.</span></span> <span data-ttu-id="8acae-117">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8acae-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="8acae-118">Los archivos pem protegidos mediante contraseña le solicitarán una contraseña para ejecutar cualquier comando.</span><span class="sxs-lookup"><span data-stu-id="8acae-118">Password protected pem files will prompt for password prior to running any command.</span></span>

<span data-ttu-id="8acae-119">Para especificar un certificado, el par de claves usa los argumentos `--cert` y `--key` para especificar las rutas de acceso de archivo en cada archivo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="8acae-119">To specify a cert, key pair use the `--cert` and `--key` arguments to specify the file paths to each respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="8acae-120">A veces los certificados utilizados para proteger clústeres de prueba o desarrollo generan un error en la validación de certificados.</span><span class="sxs-lookup"><span data-stu-id="8acae-120">Sometimes certificates used to secure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="8acae-121">Para omitir la comprobación del certificado, especifique la opción `--no-verify`.</span><span class="sxs-lookup"><span data-stu-id="8acae-121">To bypass certificate verification, specify the `--no-verify` option.</span></span> <span data-ttu-id="8acae-122">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8acae-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="8acae-123">No utilice la opción `no-verify` al conectarse a clústeres de Service Fabric de producción.</span><span class="sxs-lookup"><span data-stu-id="8acae-123">Do not use the `no-verify` option when connecting to production Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="8acae-124">Además, puede especificar rutas de acceso a directorios de certificados de entidad emisora de certificados de confianza y certificados individuales.</span><span class="sxs-lookup"><span data-stu-id="8acae-124">In addition, you can specify paths to directories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="8acae-125">Para especificar estas rutas de acceso, use el argumento `--ca`.</span><span class="sxs-lookup"><span data-stu-id="8acae-125">To specify these paths, use the `--ca` argument.</span></span> <span data-ttu-id="8acae-126">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8acae-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="8acae-127">Después de conectarse, debería poder [ejecutar otros comandos sfctl](service-fabric-cli.md) para interactuar con el clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-127">After you connect, you should be able to [run other sfctl commands](service-fabric-cli.md) to interact with the cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="8acae-128">Conexión a un clúster con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8acae-128">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="8acae-129">Antes de realizar operaciones en un clúster a través de PowerShell, primero establezca una conexión al clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-129">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="8acae-130">La conexión de clúster se utiliza para todos los comandos subsiguientes en la sesión de PowerShell determinada.</span><span class="sxs-lookup"><span data-stu-id="8acae-130">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="8acae-131">Conexión a un clúster no seguro</span><span class="sxs-lookup"><span data-stu-id="8acae-131">Connect to an unsecure cluster</span></span>

<span data-ttu-id="8acae-132">Para conectarse a un clúster no seguro, proporcione la dirección del punto de conexión del clúster al comando **Connect-ServiceFabricCluster**:</span><span class="sxs-lookup"><span data-stu-id="8acae-132">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="8acae-133">Conexión a un clúster seguro mediante la CLI de Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8acae-133">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="8acae-134">Para conectarse a un clúster segura que utiliza Azure Active Directory para autorizar el acceso de administrador de clústeres, proporcione la huella digital del certificado del clúster y use la marca *AzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="8acae-134">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="8acae-135">Conexión a un clúster seguro mediante un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="8acae-135">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="8acae-136">Ejecute el siguiente comando de PowerShell para conectarse a un clúster seguro que utiliza certificados de cliente para autorizar el acceso de administrador.</span><span class="sxs-lookup"><span data-stu-id="8acae-136">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="8acae-137">Proporcione la huella digital del certificado del clúster y la huella digital del certificado de cliente al que se han concedido permisos para administrar el clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-137">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="8acae-138">Los detalles del certificado deben corresponder a un certificado de los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-138">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="8acae-139">*ServerCertThumbprint* es la huella digital del certificado de servidor instalado en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-139">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="8acae-140">*FindValue* es la huella digital del certificado de cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="8acae-140">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="8acae-141">Cuando los parámetros están rellenos, el comando es parecido al del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8acae-141">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="8acae-142">Conexión a un clúster seguro mediante Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="8acae-142">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="8acae-143">Si el clúster independiente se implementa mediante la seguridad de AD, conéctese a este agregando el modificador "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="8acae-143">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="8acae-144">Conexión a un clúster mediante las API de FabricClient</span><span class="sxs-lookup"><span data-stu-id="8acae-144">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="8acae-145">El SDK de Service Fabric proporciona la clase [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) para la administración de clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-145">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="8acae-146">Para usar las API de FabricClient, obtenga el paquete de NuGet Microsoft.ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="8acae-146">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="8acae-147">Conexión a un clúster no seguro</span><span class="sxs-lookup"><span data-stu-id="8acae-147">Connect to an unsecure cluster</span></span>

<span data-ttu-id="8acae-148">Para conectarse a un clúster remoto no seguro, cree una instancia de FabricClient y proporcionar la dirección del clúster:</span><span class="sxs-lookup"><span data-stu-id="8acae-148">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="8acae-149">Para el código que se ejecuta desde dentro de un clúster, por ejemplo, en un servicio confiable, cree una clase FabricClient *sin* especificar la dirección del clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="8acae-150">FabricClient se conecta a la puerta de enlace de administración local en el nodo que está ejecutando actualmente el código, de modo que se evita un salto de red adicional.</span><span class="sxs-lookup"><span data-stu-id="8acae-150">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="8acae-151">Conexión a un clúster seguro mediante un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="8acae-151">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="8acae-152">Los nodos del clúster deben tener certificados válidos cuyo nombre común o nombre DNS de SAN aparezca en la [propiedad RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) establecida en [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="8acae-152">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="8acae-153">La realización de este proceso permite la autenticación mutua entre el cliente y los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-153">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="8acae-154">Conexión interactiva a un clúster seguro con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8acae-154">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="8acae-155">En el ejemplo siguiente se usa Azure Active Directory para el certificado de servidor y la identidad de clientes para la identidad del servidor.</span><span class="sxs-lookup"><span data-stu-id="8acae-155">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="8acae-156">Una ventana de diálogo se abre automáticamente para un inicio de sesión interactivo al conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-156">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="8acae-157">Conexión no interactiva a un clúster seguro con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8acae-157">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="8acae-158">El ejemplo siguiente se basa en Microsoft.IdentityModel.Clients.ActiveDirectory, versión: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="8acae-158">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="8acae-159">Para más información sobre la obtención de tokens de AAD, vea [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="8acae-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="8acae-160">Conexión a un clúster seguro sin conocer los metadatos anteriores con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8acae-160">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="8acae-161">En el ejemplo siguiente se utiliza la obtención de tokens no interactivos, pero puede utilizarse el mismo enfoque para crear una experiencia de obtención de tokens interactivos personalizados.</span><span class="sxs-lookup"><span data-stu-id="8acae-161">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="8acae-162">Los metadatos de Azure Active Directory necesarios para la obtención de tokens se leen desde la configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-162">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="8acae-163">Conexión a un clúster seguro mediante Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="8acae-163">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="8acae-164">Para acceder a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) para un clúster determinado, dirija el explorador a:</span><span class="sxs-lookup"><span data-stu-id="8acae-164">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="8acae-165">La dirección URL completa también está disponible en el panel de elementos esenciales del clúster del portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8acae-165">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="8acae-166">Conexión a un clúster seguro mediante la CLI de Azure con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8acae-166">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="8acae-167">Para conectarse a un clúster que está protegido con AAD, dirija el explorador a:</span><span class="sxs-lookup"><span data-stu-id="8acae-167">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="8acae-168">Se le pedirá automáticamente que inicie sesión con AAD.</span><span class="sxs-lookup"><span data-stu-id="8acae-168">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="8acae-169">Conexión a un clúster seguro mediante un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="8acae-169">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="8acae-170">Para conectarse a un clúster que está protegido con certificados, dirija el explorador a:</span><span class="sxs-lookup"><span data-stu-id="8acae-170">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="8acae-171">Automáticamente se le pedirá que seleccione un certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="8acae-171">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="8acae-172">Configuración de un certificado de cliente en el equipo remoto</span><span class="sxs-lookup"><span data-stu-id="8acae-172">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="8acae-173">Deben utilizarse, al menos, dos certificados para proteger el clúster, uno para el certificado de servidor y clúster, y otro para el acceso de cliente.</span><span class="sxs-lookup"><span data-stu-id="8acae-173">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="8acae-174">Se recomienda utilizar también certificados secundarios adicionales y certificados de acceso de cliente.</span><span class="sxs-lookup"><span data-stu-id="8acae-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="8acae-175">Para proteger la comunicación entre un cliente y un nodo del clúster mediante la seguridad basada en certificados, primero debe obtener e instalar el certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="8acae-175">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="8acae-176">El certificado se puede instalar en el almacén personal (Mi) del equipo local o en el almacén personal del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="8acae-176">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="8acae-177">También necesitará la huella digital del certificado de servidor para que el cliente pueda autenticar el clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-177">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="8acae-178">Ejecute el siguiente cmdlet de PowerShell para configurar el certificado de cliente en el equipo que usará para acceder al clúster.</span><span class="sxs-lookup"><span data-stu-id="8acae-178">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="8acae-179">Si es un certificado autofirmado, debe importarlo al almacén "TrustedPeople" de la máquina para poder usar este certificado para conectarse a un clúster seguro.</span><span class="sxs-lookup"><span data-stu-id="8acae-179">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="8acae-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8acae-180">Next steps</span></span>

* [<span data-ttu-id="8acae-181">Proceso de actualización del clúster de Service Fabric y expectativas del usuario</span><span class="sxs-lookup"><span data-stu-id="8acae-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="8acae-182">Administración de aplicaciones de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8acae-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="8acae-183">Introducción al modelo de estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8acae-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="8acae-184">Seguridad de aplicaciones y RunAs</span><span class="sxs-lookup"><span data-stu-id="8acae-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="8acae-185">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8acae-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
