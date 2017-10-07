---
title: seguridad del contenedor de Service Fabric aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de los servicios de contenedor toosecure ahora."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a><span data-ttu-id="906ad-103">Seguridad del contenedor</span><span class="sxs-lookup"><span data-stu-id="906ad-103">Container security</span></span>

<span data-ttu-id="906ad-104">Service Fabric proporciona un mecanismo para los servicios dentro de un contenedor tooaccess un certificado que esté instalado en los nodos de hello en un clúster de Windows o Linux (versión 5.7 o superior).</span><span class="sxs-lookup"><span data-stu-id="906ad-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="906ad-105">Además, Service Fabric también admite gMSA (cuentas de servicio administradas de grupo) para los contenedores de Windows.</span><span class="sxs-lookup"><span data-stu-id="906ad-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="906ad-106">Administración de certificados para contenedores</span><span class="sxs-lookup"><span data-stu-id="906ad-106">Certificate management for containers</span></span>

<span data-ttu-id="906ad-107">Puede proteger los servicios de contenedor especificando un certificado.</span><span class="sxs-lookup"><span data-stu-id="906ad-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="906ad-108">Hola certificado debe instalarse en los nodos de Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="906ad-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="906ad-109">Hello certificado se proporciona información en el manifiesto de aplicación hello en hello `ContainerHostPolicies` etiqueta como Hola fragmento siguiente muestra:</span><span class="sxs-lookup"><span data-stu-id="906ad-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="906ad-110">Al iniciar la aplicación hello, en tiempo de ejecución de hello lee certificados hello y genera un archivo PFX y una contraseña para cada certificado.</span><span class="sxs-lookup"><span data-stu-id="906ad-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="906ad-111">Este archivo PFX y la contraseña son accesibles dentro de contenedor de hello mediante Hola después de las variables de entorno:</span><span class="sxs-lookup"><span data-stu-id="906ad-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="906ad-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span><span class="sxs-lookup"><span data-stu-id="906ad-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="906ad-113">**Certificate_[CodePackageName]_[CertName]_Password**</span><span class="sxs-lookup"><span data-stu-id="906ad-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="906ad-114">servicio de contenedor de Hola o un proceso es responsable de importar el archivo PFX de hello en contenedor Hola.</span><span class="sxs-lookup"><span data-stu-id="906ad-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="906ad-115">certificado de hello tooimport, puede usar `setupentrypoint.sh` ejecutar código personalizado en proceso del contenedor de Hola o secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="906ad-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="906ad-116">Código de ejemplo en C# para importar el archivo PFX de hello sigue:</span><span class="sxs-lookup"><span data-stu-id="906ad-116">Sample code in C# for importing hello PFX file follows:</span></span>

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
<span data-ttu-id="906ad-117">Este certificado PFX puede usarse para la aplicación hello de autenticar, servicio o commmunication segura con otros servicios.</span><span class="sxs-lookup"><span data-stu-id="906ad-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="906ad-118">Configuración de gMSA para contenedores de Windows</span><span class="sxs-lookup"><span data-stu-id="906ad-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="906ad-119">tooset una gMSA (grupo de cuentas de servicio administradas), un archivo de especificación de credenciales (`credspec`) se coloca en todos los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="906ad-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="906ad-120">archivo Hello puede copiarse en todos los nodos con una extensión de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="906ad-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="906ad-121">Hola `credspec` archivo debe contener la información de la cuenta gMSA Hola.</span><span class="sxs-lookup"><span data-stu-id="906ad-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="906ad-122">Para obtener más información sobre hello `credspec` de archivos, consulte [las cuentas de servicio](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="906ad-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="906ad-123">especificación de la credencial de Hola y Hola `Hostname` etiqueta se especifican en el manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="906ad-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="906ad-124">Hola `Hostname` etiqueta debe coincidir con el nombre de cuenta de gMSA Hola Hola se ejecuta de contenedor con.</span><span class="sxs-lookup"><span data-stu-id="906ad-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="906ad-125">Hola `Hostname` etiqueta permite Hola contenedor tooauthenticate propio servicios tooother en dominio hello mediante la autenticación Kerberos.</span><span class="sxs-lookup"><span data-stu-id="906ad-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="906ad-126">Un ejemplo de especificación de hello `Hostname` hello y `credspec` en hello manifiesto de aplicación se muestra en el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="906ad-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="906ad-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="906ad-127">Next steps</span></span>

* [<span data-ttu-id="906ad-128">Implementar un tooService de contenedor de Windows Fabric en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="906ad-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="906ad-129">Implementar un tooService de contenedor de Docker Fabric en Linux</span><span class="sxs-lookup"><span data-stu-id="906ad-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
