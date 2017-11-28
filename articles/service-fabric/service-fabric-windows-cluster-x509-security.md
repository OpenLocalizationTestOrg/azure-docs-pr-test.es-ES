---
title: "aaaSecure un tejido de Azure servicio de clúster en Windows con certificados | Documentos de Microsoft"
description: "Este artículo describe cómo toosecure comunicación dentro de hello independiente o privada del clúster así como entre los clientes y el clúster de Hola."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="c7197-103">Protección de un clúster independiente en Windows mediante certificados X.509</span><span class="sxs-lookup"><span data-stu-id="c7197-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="c7197-104">Este artículo describe cómo toosecure Hola comunican Hola varios nodos de un clúster de Windows independiente, así como el modo clientes tooauthenticate que se conectan clúster toothis, mediante certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="c7197-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="c7197-105">Esto garantiza que sólo los usuarios autorizados pueden tener acceso a los clúster hello, hello las aplicaciones implementadas y realizar tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="c7197-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="c7197-106">Seguridad de certificado debe estar habilitado en clúster de hello cuando se crea un clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="c7197-107">Para más información sobre la seguridad de clúster, como la seguridad de nodo a nodo, la seguridad de cliente a nodo y el control de acceso basado en roles, consulte [Escenarios de seguridad de los clústeres de Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="c7197-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="c7197-108">¿Qué certificados necesitará?</span><span class="sxs-lookup"><span data-stu-id="c7197-108">Which certificates will you need?</span></span>
<span data-ttu-id="c7197-109">toostart, [Descargar paquete de clúster de hello independiente](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone de nodos de hello en el clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="c7197-110">Hola descargó paquete, encontrará un **ClusterConfig.X509.MultiMachine.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="c7197-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="c7197-111">Abra el archivo hello y revise la sección de Hola para **seguridad** en hello **propiedades** sección:</span><span class="sxs-lookup"><span data-stu-id="c7197-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

<span data-ttu-id="c7197-112">En esta sección se describe los certificados de Hola que necesita para proteger un clúster de Windows independiente.</span><span class="sxs-lookup"><span data-stu-id="c7197-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="c7197-113">Si va a especificar un certificado de clúster, establezca el valor de Hola de **ClusterCredentialType** too_**X509**_. Si va a especificar el certificado de servidor para conexiones externas, establezca hello **ServerCredentialType** demasiado_**X509**_. Aunque no es obligatorio, se recomienda toohave ambos estos certificados para un clúster protegido correctamente. Si establece estos valores demasiado*X509* , a continuación, también debe especificar Hola certificados correspondientes o Service Fabric se iniciará una excepción. En algunos casos, podría desear sólo hello toospecify _ClientCertificateThumbprints_ o _ReverseProxyCertificate_. En esos escenarios, no es necesario definir _ClusterCredentialType_ o _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="c7197-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="c7197-114">A [huella digital](https://en.wikipedia.org/wiki/Public_key_fingerprint) es Hola identidad principal de un certificado.</span><span class="sxs-lookup"><span data-stu-id="c7197-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="c7197-115">Lectura [cómo tooretrieve huella digital de un certificado](https://msdn.microsoft.com/library/ms734695.aspx) toofind out huella digital de Hola de certificados de Hola que cree.</span><span class="sxs-lookup"><span data-stu-id="c7197-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="c7197-116">Hello tabla siguiente enumeran los certificados de Hola que necesita la configuración de clúster:</span><span class="sxs-lookup"><span data-stu-id="c7197-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="c7197-117">**Valor de CertificateInformation**</span><span class="sxs-lookup"><span data-stu-id="c7197-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="c7197-118">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="c7197-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c7197-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="c7197-119">ClusterCertificate</span></span> |<span data-ttu-id="c7197-120">Se recomienda para el entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c7197-120">Recommended for test environment.</span></span> <span data-ttu-id="c7197-121">Este certificado es necesario toosecure Hola comunicación entre los nodos de hello en un clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="c7197-122">Puede utilizar dos certificados diferentes, uno principal y otro secundario para la actualización.</span><span class="sxs-lookup"><span data-stu-id="c7197-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="c7197-123">Establecer la huella digital de hello del certificado principal de Hola Hola **huella digital** sección y el de hello secundario en hello **ThumbprintSecondary** variables.</span><span class="sxs-lookup"><span data-stu-id="c7197-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="c7197-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="c7197-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="c7197-125">Se recomienda para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c7197-125">Recommended for production environment.</span></span> <span data-ttu-id="c7197-126">Este certificado es necesario toosecure Hola comunicación entre los nodos de hello en un clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="c7197-127">Puede utilizar uno o dos nombres comunes del certificado de clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="c7197-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="c7197-128">ServerCertificate</span></span> |<span data-ttu-id="c7197-129">Se recomienda para el entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c7197-129">Recommended for test environment.</span></span> <span data-ttu-id="c7197-130">Este certificado se presenta a toohello cliente cuando intente tooconnect toothis clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="c7197-131">Para mayor comodidad, puede elegir toouse Hola mismo certificado para *ClusterCertificate* y *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="c7197-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="c7197-132">Puede utilizar dos certificados de servidor diferentes, uno principal y otro secundario para la actualización.</span><span class="sxs-lookup"><span data-stu-id="c7197-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="c7197-133">Establecer la huella digital de hello del certificado principal de Hola Hola **huella digital** sección y el de hello secundario en hello **ThumbprintSecondary** variables.</span><span class="sxs-lookup"><span data-stu-id="c7197-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="c7197-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="c7197-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="c7197-135">Se recomienda para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c7197-135">Recommended for production environment.</span></span> <span data-ttu-id="c7197-136">Este certificado se presenta a toohello cliente cuando intente tooconnect toothis clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="c7197-137">Para mayor comodidad, puede elegir toouse Hola mismo certificado para *ClusterCertificateCommonNames* y *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="c7197-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="c7197-138">Puede utilizar uno o dos nombres comunes de certificado de servidor.</span><span class="sxs-lookup"><span data-stu-id="c7197-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="c7197-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="c7197-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="c7197-140">Se trata de un conjunto de certificados que desea tooinstall en los clientes de hello autenticado.</span><span class="sxs-lookup"><span data-stu-id="c7197-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="c7197-141">Puede tener un número diferente de certificados de cliente instalado en los equipos de Hola que desea que el clúster de tooallow acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="c7197-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="c7197-142">Establecer Hola huella digital de cada certificado en hello **CertificateThumbprint** variable.</span><span class="sxs-lookup"><span data-stu-id="c7197-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="c7197-143">Si establece hello **IsAdmin** demasiado*true*, cliente hello con este certificado instalado en él puede realice administrador actividades de administración de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="c7197-144">Si hello **IsAdmin** es *false*, cliente hello con este certificado solo puede realizar acciones de hello permitidas para los derechos de acceso de usuario, normalmente de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="c7197-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="c7197-145">Para más información sobre roles, consulte [Control de acceso basado en roles (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="c7197-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="c7197-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="c7197-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="c7197-147">Hola de conjunto de nombre común del certificado de cliente primera Hola para hello **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="c7197-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="c7197-148">Hola **CertificateIssuerThumbprint** es la huella digital de Hola para emisor Hola de este certificado.</span><span class="sxs-lookup"><span data-stu-id="c7197-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="c7197-149">Lectura [trabajar con certificados](https://msdn.microsoft.com/library/ms731899.aspx) tooknow más información acerca de los nombres comunes y el emisor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="c7197-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="c7197-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="c7197-151">Se recomienda para el entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c7197-151">Recommended for test environment.</span></span> <span data-ttu-id="c7197-152">Se trata de un certificado opcional que se puede especificar si desea que toosecure su [un Proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="c7197-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="c7197-153">Asegúrese de que reverseProxyEndpointPort está establecido en nodeTypes si usa este certificado.</span><span class="sxs-lookup"><span data-stu-id="c7197-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="c7197-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="c7197-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="c7197-155">Se recomienda para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c7197-155">Recommended for production environment.</span></span> <span data-ttu-id="c7197-156">Se trata de un certificado opcional que se puede especificar si desea que toosecure su [un Proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="c7197-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="c7197-157">Asegúrese de que reverseProxyEndpointPort está establecido en nodeTypes si usa este certificado.</span><span class="sxs-lookup"><span data-stu-id="c7197-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="c7197-158">Aquí es ejemplo de configuración de clúster donde se han proporcionado los certificados de cliente, servidor y clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="c7197-159">Tenga en cuenta que para clúster / server / reverseProxy certificados, la huella digital y nombre común no se permiten toobe juntos para hello misma configuración tipo de certificado.</span><span class="sxs-lookup"><span data-stu-id="c7197-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a><span data-ttu-id="c7197-160">Sustitución de certificados</span><span class="sxs-lookup"><span data-stu-id="c7197-160">Certificate roll over</span></span>
<span data-ttu-id="c7197-161">Al utilizar el nombre común del certificado en lugar de la huella digital, el proceso de sustitución de certificados no precisa actualizar la configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="c7197-162">Si trata de la reversión de certificado emisor se sustituyen, tenga certificado emisor de la antigua hello en el almacén de certificados de hello al menos 2 horas después de instalar el nuevo certificado de emisor de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="c7197-163">Adquirir certificados X.509 Hola</span><span class="sxs-lookup"><span data-stu-id="c7197-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="c7197-164">comunicación toosecure en clúster de hello, primero deberá tooobtain los certificados X.509 para los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="c7197-165">Asimismo, toolimit conexión toothis tooauthorized/users/máquinas del clúster, se necesita tooobtain e instalar certificados para equipos cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="c7197-166">Para los clústeres que ejecutan cargas de trabajo de producción, debe usar un [entidad de certificación (CA)](https://en.wikipedia.org/wiki/Certificate_authority) firmados de clúster de Hola de toosecure de certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="c7197-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="c7197-167">Para obtener más información acerca de cómo conseguir estos certificados, vaya demasiado[Cómo: obtener un certificado](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7197-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="c7197-168">Para los clústeres que use para fines de prueba, puede elegir toouse un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="c7197-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="c7197-169">Opcional: Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="c7197-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="c7197-170">Una manera de toocreate un certificado autofirmado que se pueden proteger correctamente es hello de toouse *CertSetup.ps1* script en carpeta de SDK del servicio Fabric hello en el directorio de hello *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="c7197-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="c7197-171">Editar este nombre de archivo toochange Hola predeterminado del certificado de hello (Buscar valor hello *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="c7197-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="c7197-172">Ejecute este script como `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="c7197-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="c7197-173">Exportar archivo de hello certificado tooa PFX con una contraseña protegida.</span><span class="sxs-lookup"><span data-stu-id="c7197-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="c7197-174">Obtenga primero la huella digital de hello del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="c7197-175">De hello *iniciar* menú, ejecute hello *administrar certificados de equipo*.</span><span class="sxs-lookup"><span data-stu-id="c7197-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="c7197-176">Navegue toohello **equipo Local/personal** crear carpeta ni Hola certificado que acaba de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c7197-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="c7197-177">Haga doble clic en hello certificado tooopen él, seleccione hello *detalles* ficha y desplácese hacia abajo toohello *huella digital* campo.</span><span class="sxs-lookup"><span data-stu-id="c7197-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="c7197-178">Copiar valor de huella digital de hello en el comando de PowerShell de Hola a continuación, después de quitar los espacios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="c7197-179">Hola de cambio `String` valor tooa contraseña segura adecuado tooprotect se y ejecución Hola siguiente en PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c7197-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="c7197-180">detalles de hello toosee de un certificado instalado en hello automático se puede ejecutar el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="c7197-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="c7197-181">O bien, si tiene una suscripción de Azure, siga la sección de hello [agregar certificados tooKey almacén](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="c7197-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="c7197-182">Instalar certificados de Hola</span><span class="sxs-lookup"><span data-stu-id="c7197-182">Install hello certificates</span></span>
<span data-ttu-id="c7197-183">Una vez que tenga certificados, puede instalarlas en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="c7197-184">Los nodos deben toohave Hola más reciente de Windows PowerShell 3.x instalado en ellos.</span><span class="sxs-lookup"><span data-stu-id="c7197-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="c7197-185">Necesitará toorepeat estos pasos en cada nodo de clúster y el servidor de certificados y los certificados secundarios.</span><span class="sxs-lookup"><span data-stu-id="c7197-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="c7197-186">Nodo de toohello de los archivos de copia Hola pfx.</span><span class="sxs-lookup"><span data-stu-id="c7197-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="c7197-187">Abra una ventana de PowerShell como administrador y escriba Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="c7197-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="c7197-188">Reemplace hello *$pswd* con contraseña hello usa toocreate este certificado.</span><span class="sxs-lookup"><span data-stu-id="c7197-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="c7197-189">Reemplace hello *$PfxFilePath* con ruta de acceso completa de hello del nodo de hello .pfx toothis copiada.</span><span class="sxs-lookup"><span data-stu-id="c7197-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="c7197-190">Configurar ahora el control de acceso de hello en este certificado para que el proceso de Service Fabric hello, que se ejecuta con hello cuenta de servicio de red, puede usar mediante la ejecución de la siguiente secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="c7197-191">Proporcione la huella digital de Hola de certificado de Hola y "Servicio de red" para la cuenta de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="c7197-192">Puede comprobar que hello las ACL en el certificado de Hola son correctos, abra el certificado de hello en *iniciar* > *administrar certificados de equipo* y examinando *todas las tareas*  >  *Administrar claves privadas*.</span><span class="sxs-lookup"><span data-stu-id="c7197-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="c7197-193">Repita los pasos de hello anteriormente para cada certificado de servidor.</span><span class="sxs-lookup"><span data-stu-id="c7197-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="c7197-194">También puede utilizar estos pasos tooinstall Hola certificados de cliente en equipos de Hola que desea que el clúster de tooallow acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="c7197-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="c7197-195">Crear clúster segura Hola</span><span class="sxs-lookup"><span data-stu-id="c7197-195">Create hello secure cluster</span></span>
<span data-ttu-id="c7197-196">Después de configurar hello **seguridad** sección de hello **ClusterConfig.X509.MultiMachine.json** archivo, puede continuar demasiado[Creae el clúster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure de sección Hola nodos y crear clúster de hello independiente.</span><span class="sxs-lookup"><span data-stu-id="c7197-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="c7197-197">Recuerde hello toouse **ClusterConfig.X509.MultiMachine.json** archivo al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c7197-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="c7197-198">Por ejemplo, el comando sería Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7197-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="c7197-199">Una vez que tenga Hola segura independiente de Windows clúster que se ejecuta correctamente y configuró Hola de clientes autenticados tooconnect tooit, siga la sección de hello [conectar tooa clúster segura mediante PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="c7197-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="c7197-200">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c7197-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="c7197-201">A continuación, puede ejecutar otro toowork de comandos de PowerShell con este clúster.</span><span class="sxs-lookup"><span data-stu-id="c7197-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="c7197-202">Por ejemplo, [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow una lista de nodos de este clúster segura.</span><span class="sxs-lookup"><span data-stu-id="c7197-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="c7197-203">clúster de Hola de tooremove, conectar toohello nodo en clúster de Hola donde descargó el paquete de Service Fabric hello, abra una línea de comandos y desplazarse por las carpetas de paquete toohello.</span><span class="sxs-lookup"><span data-stu-id="c7197-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="c7197-204">Ahora ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c7197-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="c7197-205">Configuración de un certificado incorrecto puede impedir que el clúster de hello salga durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="c7197-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="c7197-206">tooself-diagnosticar problemas de seguridad, consulte en el grupo del Visor de eventos *registros de aplicaciones y servicios* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="c7197-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

