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
# <a name="connect-tooa-secure-cluster"></a>Conectar el clúster segura tooa

Cuando un cliente conecta a nodo de clúster de Service Fabric tooa, cliente hello puede ser una comunicación segura y autenticada establecida usando la seguridad de certificado o Azure Active Directory (AAD). Esta autenticación garantiza que sólo los usuarios autorizados pueden tener acceso a clúster de Hola y a las aplicaciones implementan y realizan tareas de administración.  Certificado o la seguridad AAD debe haber previamente habilitado en clúster de hello cuando se creó el clúster de Hola.  Para más información sobre escenarios de seguridad de clúster, consulte [Protección de un clúster de Service Fabric](service-fabric-cluster-security.md). Si va a conectar clúster tooa protegido con certificados, [configurar el certificado de cliente hello](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) en equipo Hola que conecta el clúster de toohello. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>Conectar con Azure Service Fabric CLI (sfctl) de clúster segura tooa

Hay algunas maneras tooconnect tooa segura clúster mediante Hola CLI de tejido de servicio (sfctl). Cuando se utiliza un certificado de cliente para la autenticación, certificado de hello detalles deben coincidir con un certificado implementa toohello nodos del clúster. Si el certificado tiene entidades de certificación (CA), tendrá que tooadditionally especificar Hola entidades emisoras de certificados de confianza.

Puede conectar clúster tooa con hello `sfctl cluster select` comando.

Los certificados de cliente se pueden especificar de dos maneras diferentes, como un par de clave y certificado, o como un archivo pem único. Para protección por contraseña `pem` , se generarán automáticamente solicita contraseña de hello tooenter.

certificado de cliente de hello toospecify como un archivo pem, especifique la ruta de acceso de archivo de Hola Hola `--pem` argumento. Por ejemplo:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Archivos pem de protección por contraseña le solicitará contraseña anterior toorunning cualquier comando.

toospecify un certificado, el par de claves usa hello `--cert` y `--key` argumentos toospecify Hola archivo correspondiente de tooeach de rutas de acceso de archivo.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

A veces los certificados usan toosecure prueba o desarrollo clústeres no superan la validación de certificado. toobypass certificado de comprobación, especifique hello `--no-verify` opción. Por ejemplo:

> [!WARNING]
> No utilice hello `no-verify` opción al conectarse a clústeres de Service Fabric tooproduction.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

Además, puede especificar toodirectories de rutas de acceso de certificados de entidad emisora de certificados de confianza o certificados individuales. toospecify estas rutas de acceso, use hello `--ca` argumento. Por ejemplo:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

Después de conectarse, debe poder demasiado[ejecutar otros comandos sfctl](service-fabric-cli.md) toointeract con clúster de Hola.

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>Conectar el clúster tooa mediante PowerShell
Antes de realizar operaciones en un clúster a través de PowerShell, establezca primero un clúster de toohello de conexión. conexión de clúster de Hola se utiliza para todos los comandos subsiguientes en hello tiene la sesión de PowerShell.

### <a name="connect-tooan-unsecure-cluster"></a>Conectar el clúster no segura tooan

tooconnect tooan no segura de clúster, proporcione toohello de dirección de punto de conexión de clúster de hello **Connect-ServiceFabricCluster** comando:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Conectar con Azure Active Directory de clúster segura tooa

tooconnect tooa clúster segura que utiliza el acceso de administrador de clúster de Azure Active Directory tooauthorize, proporcione la huella digital del certificado de clúster de Hola y usar hello *AzureActiveDirectory* marca.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Conectar con un certificado de cliente de clúster segura tooa
Hola ejecución siguiente comando de PowerShell tooconnect tooa segura de clúster que usa acceso de administrador de tooauthorize de certificados de cliente. Proporcione la huella digital del certificado de clúster de Hola y la huella digital de hello del certificado de cliente de Hola que se ha concedido permisos para la administración de clúster. Detalles del certificado Hola deben coincidir con un certificado en nodos de clúster de Hola.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*Servercertthumbprint como mínimo* es Hola huella del certificado de servidor hello instalado en nodos de clúster de Hola. *FindValue* es Hola huella del certificado de cliente de administración de Hola.
Cuando se rellenan parámetros hello, comando hello aspecto Hola siguiente ejemplo: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>Conectar tooa clúster segura mediante Windows Active Directory
Si el clúster independiente se implementa mediante la seguridad de AD, conéctese toohello clúster agregando conmutador Hola "WindowsCredential".

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>Conectar con hello FabricClient APIs de clúster de tooa
Hola SDK del servicio de Fabric proporciona hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) clase para la administración de clúster. Hola toouse FabricClient APIs, obtener Hola paquete Microsoft.ServiceFabric NuGet.

### <a name="connect-tooan-unsecure-cluster"></a>Conectar el clúster no segura tooan

tooconnect tooa remota segura de clúster, cree una instancia de FabricClient y proporcionar la dirección del clúster hello:

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

Para el código que se ejecuta desde dentro de un clúster, por ejemplo, en un servicio confiable, cree un FabricClient *sin* especificar la dirección del clúster Hola. FabricClient conecta la administración local de toohello puerta de enlace en el código de hello nodo Hola actualmente en ejecución, evitar un salto de red adicional.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Conectar con un certificado de cliente de clúster segura tooa

nodos de Hello en clúster de hello deben tener certificados válidos cuyo nombre común o nombre DNS de SAN aparece en hello [RemoteCommonNames propiedad](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) establecido en [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Después de este proceso, permite la autenticación mutua entre el cliente de Hola y nodos de clúster de Hola.

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>Conectar con Azure Active Directory de forma interactiva de clúster segura tooa

Hola siguiendo el ejemplo se usa Azure Active Directory para el certificado de identidad y el servidor de cliente para la identidad del servidor.

Una ventana de cuadro de diálogo se abre automáticamente para un inicio de sesión interactivo al conectar toohello clúster.

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>Conectar con Azure Active Directory de manera no interactiva de clúster segura tooa

Hello siguiente ejemplo se basa en Microsoft.IdentityModel.Clients.ActiveDirectory, versión: 2.19.208020213.

Para más información sobre la obtención de tokens de AAD, vea [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Conectar tooa de clúster segura sin conocimiento de los metadatos anteriores con Azure Active Directory

Hello en el ejemplo siguiente se utiliza la adquisición de tokens no interactivo, pero hello mismo enfoque puede ser usado toobuild una experiencia de adquisición de tokens interactivos personalizados. lectura de los metadatos de Azure Active Directory Hola necesarios para la adquisición de tokens de configuración de clúster.

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>Conectarse mediante el Explorador de tejido de servicio de clúster segura tooa
tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) para un clúster determinado, seleccione el explorador para:

`http://<your-cluster-endpoint>:19080/Explorer`

dirección URL completa de Hello también está disponible en el panel de essentials de clúster Hola de hello portal de Azure.

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Conectar con Azure Active Directory de clúster segura tooa

clúster de tooa tooconnect que está protegida con AAD, dirija el explorador:

`https://<your-cluster-endpoint>:19080/Explorer`

Automáticamente se pueden toolog solicitada con AAD.

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Conectar con un certificado de cliente de clúster segura tooa

tooconnect tooa clúster que está protegida con certificados, seleccione el explorador para:

`https://<your-cluster-endpoint>:19080/Explorer`

Automáticamente se pueden tooselect solicitada un certificado de cliente.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>Configurar un certificado de cliente en el equipo remoto hello
Al menos dos certificados deben utilizarse para proteger el clúster hello, uno para el certificado de servidor y un clúster de hello y otro para el acceso de cliente.  Se recomienda utilizar también certificados secundarios adicionales y certificados de acceso de cliente.  comunicación de hello toosecure entre un cliente y un nodo de clúster con certificados de seguridad, primero necesita tooobtain e instalar certificado de cliente de Hola. Hola certificado puede instalarse en hello (mi) almacén Personal del equipo local de Hola o del usuario actual de Hola.  También debe huella digital de hello del certificado de servidor de Hola para que hello cliente puede autenticarse clúster Hola.

Ejecute hello después tooset de cmdlet de PowerShell certificado de cliente de hello en equipo Hola desde el que se obtiene acceso a clúster Hola.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

Si es un certificado autofirmado, debe tooimport que "personas de confianza" la máquina tooyour almacenar para poder usar este clúster segura de certificado tooconnect tooa.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Pasos siguientes

* [Proceso de actualización del clúster de Service Fabric y expectativas del usuario](service-fabric-cluster-upgrade.md)
* [Administración de aplicaciones de Service Fabric en Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Introducción al modelo de estado de Service Fabric](service-fabric-health-introduction.md)
* [Seguridad de aplicaciones y RunAs](service-fabric-application-runas-security.md)
* [Introducción a la CLI de Service Fabric](service-fabric-cli.md)
