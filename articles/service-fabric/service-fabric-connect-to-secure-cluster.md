---
title: "aaaConnect forma segura el clúster de Azure Service Fabric tooan | Documentos de Microsoft"
description: "Describe el proceso de clúster de Service Fabric tooa de acceso de cliente de tooauthenticate y cómo toosecure la comunicación entre clientes y un clúster."
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
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="bd6f0-103">Conectar el clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="bd6f0-104">Cuando un cliente conecta a nodo de clúster de Service Fabric tooa, cliente hello puede ser una comunicación segura y autenticada establecida usando la seguridad de certificado o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="bd6f0-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="bd6f0-105">Esta autenticación garantiza que sólo los usuarios autorizados pueden tener acceso a clúster de Hola y a las aplicaciones implementan y realizan tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="bd6f0-106">Certificado o la seguridad AAD debe haber previamente habilitado en clúster de hello cuando se creó el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="bd6f0-107">Para más información sobre escenarios de seguridad de clúster, consulte [Protección de un clúster de Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="bd6f0-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="bd6f0-108">Si va a conectar clúster tooa protegido con certificados, [configurar el certificado de cliente hello](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) en equipo Hola que conecta el clúster de toohello.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="bd6f0-109">Conectar con Azure Service Fabric CLI (sfctl) de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="bd6f0-110">Hay algunas maneras tooconnect tooa segura clúster mediante Hola CLI de tejido de servicio (sfctl).</span><span class="sxs-lookup"><span data-stu-id="bd6f0-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="bd6f0-111">Cuando se utiliza un certificado de cliente para la autenticación, certificado de hello detalles deben coincidir con un certificado implementa toohello nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="bd6f0-112">Si el certificado tiene entidades de certificación (CA), tendrá que tooadditionally especificar Hola entidades emisoras de certificados de confianza.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="bd6f0-113">Puede conectar clúster tooa con hello `sfctl cluster select` comando.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="bd6f0-114">Los certificados de cliente se pueden especificar de dos maneras diferentes, como un par de clave y certificado, o como un archivo pem único.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="bd6f0-115">Para protección por contraseña `pem` , se generarán automáticamente solicita contraseña de hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="bd6f0-116">certificado de cliente de hello toospecify como un archivo pem, especifique la ruta de acceso de archivo de Hola Hola `--pem` argumento.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="bd6f0-117">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="bd6f0-118">Archivos pem de protección por contraseña le solicitará contraseña anterior toorunning cualquier comando.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="bd6f0-119">toospecify un certificado, el par de claves usa hello `--cert` y `--key` argumentos toospecify Hola archivo correspondiente de tooeach de rutas de acceso de archivo.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="bd6f0-120">A veces los certificados usan toosecure prueba o desarrollo clústeres no superan la validación de certificado.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="bd6f0-121">toobypass certificado de comprobación, especifique hello `--no-verify` opción.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="bd6f0-122">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="bd6f0-123">No utilice hello `no-verify` opción al conectarse a clústeres de Service Fabric tooproduction.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="bd6f0-124">Además, puede especificar toodirectories de rutas de acceso de certificados de entidad emisora de certificados de confianza o certificados individuales.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="bd6f0-125">toospecify estas rutas de acceso, use hello `--ca` argumento.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="bd6f0-126">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="bd6f0-127">Después de conectarse, debe poder demasiado[ejecutar otros comandos sfctl](service-fabric-cli.md) toointeract con clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="bd6f0-128">Conectar el clúster tooa mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd6f0-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="bd6f0-129">Antes de realizar operaciones en un clúster a través de PowerShell, establezca primero un clúster de toohello de conexión.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="bd6f0-130">conexión de clúster de Hola se utiliza para todos los comandos subsiguientes en hello tiene la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="bd6f0-131">Conectar el clúster no segura tooan</span><span class="sxs-lookup"><span data-stu-id="bd6f0-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="bd6f0-132">tooconnect tooan no segura de clúster, proporcione toohello de dirección de punto de conexión de clúster de hello **Connect-ServiceFabricCluster** comando:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="bd6f0-133">Conectar con Azure Active Directory de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="bd6f0-134">tooconnect tooa clúster segura que utiliza el acceso de administrador de clúster de Azure Active Directory tooauthorize, proporcione la huella digital del certificado de clúster de Hola y usar hello *AzureActiveDirectory* marca.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="bd6f0-135">Conectar con un certificado de cliente de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="bd6f0-136">Hola ejecución siguiente comando de PowerShell tooconnect tooa segura de clúster que usa acceso de administrador de tooauthorize de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="bd6f0-137">Proporcione la huella digital del certificado de clúster de Hola y la huella digital de hello del certificado de cliente de Hola que se ha concedido permisos para la administración de clúster.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="bd6f0-138">Detalles del certificado Hola deben coincidir con un certificado en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="bd6f0-139">*Servercertthumbprint como mínimo* es Hola huella del certificado de servidor hello instalado en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="bd6f0-140">*FindValue* es Hola huella del certificado de cliente de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="bd6f0-141">Cuando se rellenan parámetros hello, comando hello aspecto Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="bd6f0-142">Conectar tooa clúster segura mediante Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd6f0-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="bd6f0-143">Si el clúster independiente se implementa mediante la seguridad de AD, conéctese toohello clúster agregando conmutador Hola "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="bd6f0-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="bd6f0-144">Conectar con hello FabricClient APIs de clúster de tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="bd6f0-145">Hola SDK del servicio de Fabric proporciona hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) clase para la administración de clúster.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="bd6f0-146">Hola toouse FabricClient APIs, obtener Hola paquete Microsoft.ServiceFabric NuGet.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="bd6f0-147">Conectar el clúster no segura tooan</span><span class="sxs-lookup"><span data-stu-id="bd6f0-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="bd6f0-148">tooconnect tooa remota segura de clúster, cree una instancia de FabricClient y proporcionar la dirección del clúster hello:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="bd6f0-149">Para el código que se ejecuta desde dentro de un clúster, por ejemplo, en un servicio confiable, cree un FabricClient *sin* especificar la dirección del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="bd6f0-150">FabricClient conecta la administración local de toohello puerta de enlace en el código de hello nodo Hola actualmente en ejecución, evitar un salto de red adicional.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="bd6f0-151">Conectar con un certificado de cliente de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="bd6f0-152">nodos de Hello en clúster de hello deben tener certificados válidos cuyo nombre común o nombre DNS de SAN aparece en hello [RemoteCommonNames propiedad](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) establecido en [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="bd6f0-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="bd6f0-153">Después de este proceso, permite la autenticación mutua entre el cliente de Hola y nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="bd6f0-154">Conectar con Azure Active Directory de forma interactiva de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="bd6f0-155">Hola siguiendo el ejemplo se usa Azure Active Directory para el certificado de identidad y el servidor de cliente para la identidad del servidor.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="bd6f0-156">Una ventana de cuadro de diálogo se abre automáticamente para un inicio de sesión interactivo al conectar toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="bd6f0-157">Conectar con Azure Active Directory de manera no interactiva de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="bd6f0-158">Hello siguiente ejemplo se basa en Microsoft.IdentityModel.Clients.ActiveDirectory, versión: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="bd6f0-159">Para más información sobre la obtención de tokens de AAD, vea [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd6f0-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="bd6f0-160">Conectar tooa de clúster segura sin conocimiento de los metadatos anteriores con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd6f0-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="bd6f0-161">Hello en el ejemplo siguiente se utiliza la adquisición de tokens no interactivo, pero hello mismo enfoque puede ser usado toobuild una experiencia de adquisición de tokens interactivos personalizados.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="bd6f0-162">lectura de los metadatos de Azure Active Directory Hola necesarios para la adquisición de tokens de configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="bd6f0-163">Conectarse mediante el Explorador de tejido de servicio de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="bd6f0-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) para un clúster determinado, seleccione el explorador para:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="bd6f0-165">dirección URL completa de Hello también está disponible en el panel de essentials de clúster Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="bd6f0-166">Conectar con Azure Active Directory de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="bd6f0-167">clúster de tooa tooconnect que está protegida con AAD, dirija el explorador:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="bd6f0-168">Automáticamente se pueden toolog solicitada con AAD.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="bd6f0-169">Conectar con un certificado de cliente de clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="bd6f0-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="bd6f0-170">tooconnect tooa clúster que está protegida con certificados, seleccione el explorador para:</span><span class="sxs-lookup"><span data-stu-id="bd6f0-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="bd6f0-171">Automáticamente se pueden tooselect solicitada un certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="bd6f0-172">Configurar un certificado de cliente en el equipo remoto hello</span><span class="sxs-lookup"><span data-stu-id="bd6f0-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="bd6f0-173">Al menos dos certificados deben utilizarse para proteger el clúster hello, uno para el certificado de servidor y un clúster de hello y otro para el acceso de cliente.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="bd6f0-174">Se recomienda utilizar también certificados secundarios adicionales y certificados de acceso de cliente.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="bd6f0-175">comunicación de hello toosecure entre un cliente y un nodo de clúster con certificados de seguridad, primero necesita tooobtain e instalar certificado de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="bd6f0-176">Hola certificado puede instalarse en hello (mi) almacén Personal del equipo local de Hola o del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="bd6f0-177">También debe huella digital de hello del certificado de servidor de Hola para que hello cliente puede autenticarse clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="bd6f0-178">Ejecute hello después tooset de cmdlet de PowerShell certificado de cliente de hello en equipo Hola desde el que se obtiene acceso a clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="bd6f0-179">Si es un certificado autofirmado, debe tooimport que "personas de confianza" la máquina tooyour almacenar para poder usar este clúster segura de certificado tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="bd6f0-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="bd6f0-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd6f0-180">Next steps</span></span>

* [<span data-ttu-id="bd6f0-181">Proceso de actualización del clúster de Service Fabric y expectativas del usuario</span><span class="sxs-lookup"><span data-stu-id="bd6f0-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="bd6f0-182">Administración de aplicaciones de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd6f0-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="bd6f0-183">Introducción al modelo de estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bd6f0-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="bd6f0-184">Seguridad de aplicaciones y RunAs</span><span class="sxs-lookup"><span data-stu-id="bd6f0-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="bd6f0-185">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bd6f0-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
