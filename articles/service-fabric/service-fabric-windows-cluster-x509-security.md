---
title: "Protección de un clúster de Azure Service Fabric en Windows con certificaciones | Microsoft Docs"
description: "En este artículo se describe cómo proteger la comunicación en el clúster independiente o privado, así como entre los clientes y el clúster."
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
ms.openlocfilehash: 71ece1e43cc3c4ac3350cd59633065de06672420
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="a23b1-103">Protección de un clúster independiente en Windows mediante certificados X.509</span><span class="sxs-lookup"><span data-stu-id="a23b1-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="a23b1-104">Este artículo describe cómo proteger la comunicación entre los diversos nodos del clúster de Windows independiente, así cómo autenticar a los clientes que se conectan a él, mediante certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="a23b1-104">This article describes how to secure the communication between the various nodes of your standalone Windows cluster, as well as how to authenticate clients connecting to this cluster, using X.509 certificates.</span></span> <span data-ttu-id="a23b1-105">Esto garantiza que solo los usuarios autorizados pueden tener acceso al clúster y a las aplicaciones implementadas, y realizar tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="a23b1-105">This ensures that only authorized users can access the cluster, the deployed applications and perform management tasks.</span></span>  <span data-ttu-id="a23b1-106">La seguridad basada en certificados se debe haber habilitado en el clúster al crearlo.</span><span class="sxs-lookup"><span data-stu-id="a23b1-106">Certificate security should be enabled on the cluster when the cluster is created.</span></span>  

<span data-ttu-id="a23b1-107">Para más información sobre la seguridad de clúster, como la seguridad de nodo a nodo, la seguridad de cliente a nodo y el control de acceso basado en roles, consulte [Escenarios de seguridad de los clústeres de Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="a23b1-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="a23b1-108">¿Qué certificados necesitará?</span><span class="sxs-lookup"><span data-stu-id="a23b1-108">Which certificates will you need?</span></span>
<span data-ttu-id="a23b1-109">Para empezar, [descargue el paquete de clúster independiente](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) en uno de los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-109">To start with, [download the standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) to one of the nodes in your cluster.</span></span> <span data-ttu-id="a23b1-110">En el paquete descargado, encontrará el archivo **ClusterConfig.X509.MultiMachine.json** .</span><span class="sxs-lookup"><span data-stu-id="a23b1-110">In the downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="a23b1-111">Abra el archivo y revise la sección **security** en la sección **properties**:</span><span class="sxs-lookup"><span data-stu-id="a23b1-111">Open the file and review the section for **security** under the **properties** section:</span></span>

```JSON
"security": {
    "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

<span data-ttu-id="a23b1-112">En esta sección se describen los certificados que necesita para proteger el clúster de Windows independiente.</span><span class="sxs-lookup"><span data-stu-id="a23b1-112">This section describes the certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="a23b1-113">Si va a especificar un certificado de clúster, establezca el valor de **ClusterCredentialType** en _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="a23b1-113">If you are specifying a cluster certificate, set the value of **ClusterCredentialType** to _**X509**_.</span></span> <span data-ttu-id="a23b1-114">Si va a especificar un certificado de servidor para conexiones externas, establezca **ServerCredentialType** en _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="a23b1-114">If you are specifying server certificate for outside connections, set the **ServerCredentialType** to _**X509**_.</span></span> <span data-ttu-id="a23b1-115">Si bien no es obligatorio, se recomienda tener ambos certificados para contar con un clúster protegido correctamente.</span><span class="sxs-lookup"><span data-stu-id="a23b1-115">Although not mandatory, we recommend to have both these certificates for a properly secured cluster.</span></span> <span data-ttu-id="a23b1-116">Si establece estos valores en *X509*, también debe especificar los certificados correspondientes. De lo contrario, Service Fabric generará una excepción.</span><span class="sxs-lookup"><span data-stu-id="a23b1-116">If you set these values to *X509* then you must also specify the corresponding certificates or Service Fabric will throw an exception.</span></span> <span data-ttu-id="a23b1-117">En algunos escenarios, es posible que solo desee especificar _ClientCertificateThumbprints_ o _ReverseProxyCertificate_.</span><span class="sxs-lookup"><span data-stu-id="a23b1-117">In some scenarios, you may only want to specify the _ClientCertificateThumbprints_ or _ReverseProxyCertificate_.</span></span> <span data-ttu-id="a23b1-118">En esos escenarios, no es necesario establecer _ClusterCredentialType_ o _ServerCredentialType_ en _X509_.</span><span class="sxs-lookup"><span data-stu-id="a23b1-118">In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ to _X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="a23b1-119">Una [huella digital](https://en.wikipedia.org/wiki/Public_key_fingerprint) es la identidad principal de un certificado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-119">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is the primary identity of a certificate.</span></span> <span data-ttu-id="a23b1-120">Consulte [Cómo recuperar la huella digital de un certificado](https://msdn.microsoft.com/library/ms734695.aspx) para averiguar la huella digital de los certificados que cree.</span><span class="sxs-lookup"><span data-stu-id="a23b1-120">Read [How to retrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) to find out the thumbprint of the certificates that you create.</span></span>
> 
> 

<span data-ttu-id="a23b1-121">En la siguiente tabla se enumeran los certificados que va a necesitar en su instalación del clúster:</span><span class="sxs-lookup"><span data-stu-id="a23b1-121">The following table lists the certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="a23b1-122">**Valor de CertificateInformation**</span><span class="sxs-lookup"><span data-stu-id="a23b1-122">**CertificateInformation Setting**</span></span> | <span data-ttu-id="a23b1-123">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="a23b1-123">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="a23b1-124">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="a23b1-124">ClusterCertificate</span></span> |<span data-ttu-id="a23b1-125">Se recomienda para el entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a23b1-125">Recommended for test environment.</span></span> <span data-ttu-id="a23b1-126">Este certificado es necesario para proteger la comunicación entre los nodos de un clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-126">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="a23b1-127">Puede utilizar dos certificados diferentes, uno principal y otro secundario para la actualización.</span><span class="sxs-lookup"><span data-stu-id="a23b1-127">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="a23b1-128">Establezca la huella digital del certificado principal en la sección **Thumbprint** y la del secundario en la variable**ThumbprintSecondary**.</span><span class="sxs-lookup"><span data-stu-id="a23b1-128">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="a23b1-129">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="a23b1-129">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="a23b1-130">Se recomienda para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a23b1-130">Recommended for production environment.</span></span> <span data-ttu-id="a23b1-131">Este certificado es necesario para proteger la comunicación entre los nodos de un clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-131">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="a23b1-132">Puede utilizar uno o dos nombres comunes del certificado de clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-132">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="a23b1-133">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="a23b1-133">ServerCertificate</span></span> |<span data-ttu-id="a23b1-134">Se recomienda para el entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a23b1-134">Recommended for test environment.</span></span> <span data-ttu-id="a23b1-135">Este certificado se presenta al cliente cuando intenta conectarse a este clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-135">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="a23b1-136">Para mayor comodidad, puede utilizar el mismo certificado para *ClusterCertificate* y *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="a23b1-136">For convenience, you can choose to use the same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="a23b1-137">Puede utilizar dos certificados de servidor diferentes, uno principal y otro secundario para la actualización.</span><span class="sxs-lookup"><span data-stu-id="a23b1-137">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="a23b1-138">Establezca la huella digital del certificado principal en la sección **Thumbprint** y la del secundario en la variable**ThumbprintSecondary**.</span><span class="sxs-lookup"><span data-stu-id="a23b1-138">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="a23b1-139">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="a23b1-139">ServerCertificateCommonNames</span></span> |<span data-ttu-id="a23b1-140">Se recomienda para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a23b1-140">Recommended for production environment.</span></span> <span data-ttu-id="a23b1-141">Este certificado se presenta al cliente cuando intenta conectarse a este clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-141">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="a23b1-142">Por comodidad, puede utilizar el mismo certificado para *ClusterCertificateCommonNames* y *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="a23b1-142">For convenience, you can choose to use the same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="a23b1-143">Puede utilizar uno o dos nombres comunes de certificado de servidor.</span><span class="sxs-lookup"><span data-stu-id="a23b1-143">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="a23b1-144">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="a23b1-144">ClientCertificateThumbprints</span></span> |<span data-ttu-id="a23b1-145">Se trata de un conjunto de certificados que desea instalar en los clientes autenticados.</span><span class="sxs-lookup"><span data-stu-id="a23b1-145">This is a set of certificates that you want to install on the authenticated clients.</span></span> <span data-ttu-id="a23b1-146">Puede tener varios certificados de cliente diferentes instalados en los equipos a los que desea permitir el acceso al clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-146">You can have a number of different client certificates installed on the machines that you want to allow access to the cluster.</span></span> <span data-ttu-id="a23b1-147">Establece la huella digital de cada certificado en la variable **CertificateThumbprint** .</span><span class="sxs-lookup"><span data-stu-id="a23b1-147">Set the thumbprint of each certificate in the **CertificateThumbprint** variable.</span></span> <span data-ttu-id="a23b1-148">Si establece **IsAdmin** en *True*, el cliente con este certificado instalado puede realizar actividades de administración en el clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-148">If you set the **IsAdmin** to *true*, then the client with this certificate installed on it can do administrator management activities on the cluster.</span></span> <span data-ttu-id="a23b1-149">Si **IsAdmin** es *false*, el cliente con este certificado solo puede realizar las acciones permitidas para los derechos de acceso de usuario, normalmente de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="a23b1-149">If the **IsAdmin** is *false*, the client with this certificate can only perform the actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="a23b1-150">Para más información sobre roles, consulte [Control de acceso basado en roles (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="a23b1-150">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="a23b1-151">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="a23b1-151">ClientCertificateCommonNames</span></span> |<span data-ttu-id="a23b1-152">Establezca el nombre común del primer certificado de cliente para **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="a23b1-152">Set the common name of the first client certificate for the **CertificateCommonName**.</span></span> <span data-ttu-id="a23b1-153">**CertificateIssuerThumbprint** es la huella digital del emisor de este certificado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-153">The **CertificateIssuerThumbprint** is the thumbprint for the issuer of this certificate.</span></span> <span data-ttu-id="a23b1-154">Consulte [Trabajar con certificados](https://msdn.microsoft.com/library/ms731899.aspx) para más información sobre los nombres comunes y el emisor.</span><span class="sxs-lookup"><span data-stu-id="a23b1-154">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) to know more about common names and the issuer.</span></span> |
| <span data-ttu-id="a23b1-155">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="a23b1-155">ReverseProxyCertificate</span></span> |<span data-ttu-id="a23b1-156">Se recomienda para el entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a23b1-156">Recommended for test environment.</span></span> <span data-ttu-id="a23b1-157">Se trata de un certificado opcional que se puede especificar si desea proteger el [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="a23b1-157">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="a23b1-158">Asegúrese de que reverseProxyEndpointPort está establecido en nodeTypes si usa este certificado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-158">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="a23b1-159">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="a23b1-159">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="a23b1-160">Se recomienda para el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a23b1-160">Recommended for production environment.</span></span> <span data-ttu-id="a23b1-161">Se trata de un certificado opcional que se puede especificar si desea proteger el [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="a23b1-161">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="a23b1-162">Asegúrese de que reverseProxyEndpointPort está establecido en nodeTypes si usa este certificado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-162">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="a23b1-163">Este es un ejemplo de configuración del clúster en el que se han proporcionado los certificados de clúster, servidor y cliente.</span><span class="sxs-lookup"><span data-stu-id="a23b1-163">Here is example cluster configuration where the Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="a23b1-164">Tenga en cuenta que, en lo que respecta a los certificados de clúster, servidor y reverseProxy, no se permite configurar conjuntamente huellas digitales ni nombres comunes para el mismo tipo de certificado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-164">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed to be configured together for the same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace the localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

## <a name="certificate-roll-over"></a><span data-ttu-id="a23b1-165">Sustitución de certificados</span><span class="sxs-lookup"><span data-stu-id="a23b1-165">Certificate roll over</span></span>
<span data-ttu-id="a23b1-166">Al utilizar el nombre común del certificado en lugar de la huella digital, el proceso de sustitución de certificados no precisa actualizar la configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-166">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="a23b1-167">Si la sustitución de certificados implica también a los de emisor, mantenga el antiguo certificado de emisor en el almacén de certificados, al menos, 2 horas después de instalar el nuevo certificado de emisor.</span><span class="sxs-lookup"><span data-stu-id="a23b1-167">If certificate roll over involves issuer roll over, please keep the old issuer cert in the cert store at least 2 hours after installing the new issuer cert.</span></span>

## <a name="acquire-the-x509-certificates"></a><span data-ttu-id="a23b1-168">Adquisición de certificados X.509</span><span class="sxs-lookup"><span data-stu-id="a23b1-168">Acquire the X.509 certificates</span></span>
<span data-ttu-id="a23b1-169">Para proteger la comunicación en el clúster, primero deberá obtener certificados X.509 para los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-169">To secure communication within the cluster, you will first need to obtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="a23b1-170">Además, para limitar la conexión a este clúster a los equipos o usuarios autorizados, debe obtener e instalar certificados para los equipos cliente.</span><span class="sxs-lookup"><span data-stu-id="a23b1-170">Additionally, to limit connection to this cluster to authorized machines/users, you will need to obtain and install certificates for the client machines.</span></span>

<span data-ttu-id="a23b1-171">Para los clústeres que ejecutan cargas de trabajo de producción, debe usar un certificado X.509 firmado por una [entidad de certificación (CA)](https://en.wikipedia.org/wiki/Certificate_authority) con el fin de proteger el clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-171">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate to secure the cluster.</span></span> <span data-ttu-id="a23b1-172">Para más información sobre cómo obtener estos certificados, consulte [Cómo obtener un certificado (WCF)](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="a23b1-172">For details on obtaining these certificates, go to [How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="a23b1-173">En los clústeres que se usan con fines de prueba, puede usar un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-173">For clusters that you use for test purposes, you can choose to use a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="a23b1-174">Opcional: Creación de un certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="a23b1-174">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="a23b1-175">Una forma de crear un certificado autofirmado que se puede proteger correctamente es usar el script *CertSetup.ps1* de la carpeta del SDK de Service Fabric en el directorio *C:\Archivos de programa\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="a23b1-175">One way to create a self-signed cert that can be secured correctly is to use the *CertSetup.ps1* script in the Service Fabric SDK folder in the directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="a23b1-176">Edite el archivo para cambiar el nombre predeterminado del certificado (busque el valor *CN=ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="a23b1-176">Edit this file to change the default name of the certificate (look for the value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="a23b1-177">Ejecute este script como `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="a23b1-177">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="a23b1-178">Ahora exporte el certificado a un archivo PFX con una contraseña protegida.</span><span class="sxs-lookup"><span data-stu-id="a23b1-178">Now export the certificate to a PFX file with a protected password.</span></span> <span data-ttu-id="a23b1-179">En primer lugar, obtenga la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-179">First get the thumbprint of the certificate.</span></span> <span data-ttu-id="a23b1-180">Desde el menú *Inicio*, ejecute *Administrar certificados de equipo*.</span><span class="sxs-lookup"><span data-stu-id="a23b1-180">From the *Start* menu, run the *Manage computer certificates*.</span></span> <span data-ttu-id="a23b1-181">Vaya a la carpeta **Equipo local\Personal** y busque el certificado recién creado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-181">Navigate to the **Local Computer\Personal** folder and find the certificate you just created.</span></span> <span data-ttu-id="a23b1-182">Haga doble clic en el certificado para abrirlo, seleccione la pestaña *Detalles* y desplácese hacia abajo hasta el campo *Huella digital*.</span><span class="sxs-lookup"><span data-stu-id="a23b1-182">Double-click the certificate to open it, select the *Details* tab and scroll down to the *Thumbprint* field.</span></span> <span data-ttu-id="a23b1-183">Copie el valor de la huella digital en el comando de PowerShell que aparece a continuación, sin espacios.</span><span class="sxs-lookup"><span data-stu-id="a23b1-183">Copy the thumbprint value into the PowerShell command below, after removing the spaces.</span></span>  <span data-ttu-id="a23b1-184">Cambie el valor `String` por una contraseña segura adecuada para protegerlo y ejecute el siguiente comando en PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a23b1-184">Change the `String` value to a suitable secure password to protect it and run the following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="a23b1-185">Para ver los detalles de un certificado instalado en el equipo, puede ejecutar el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a23b1-185">To see the details of a certificate installed on the machine you can run the following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="a23b1-186">Como alternativa, si tiene una suscripción de Azure, consulte la sección [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault) (Agregar certificados a Key Vault).</span><span class="sxs-lookup"><span data-stu-id="a23b1-186">Alternatively, if you have an Azure subscription, follow the section [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-the-certificates"></a><span data-ttu-id="a23b1-187">Instalación de los certificados</span><span class="sxs-lookup"><span data-stu-id="a23b1-187">Install the certificates</span></span>
<span data-ttu-id="a23b1-188">Cuando tenga los certificados, puede instalarlos en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-188">Once you have certificate(s), you can install them on the cluster nodes.</span></span> <span data-ttu-id="a23b1-189">Los nodos deben tener instalada la versión más reciente de Windows PowerShell 3.x.</span><span class="sxs-lookup"><span data-stu-id="a23b1-189">Your nodes need to have the latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="a23b1-190">Debe repetir estos pasos en cada nodo, para los certificados del clúster y el servidor y cualquier certificado secundario.</span><span class="sxs-lookup"><span data-stu-id="a23b1-190">You will need to repeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="a23b1-191">Copie los archivos .pfx en el nodo.</span><span class="sxs-lookup"><span data-stu-id="a23b1-191">Copy the .pfx file(s) to the node.</span></span>
2. <span data-ttu-id="a23b1-192">Abra una ventana de PowerShell como administrador y ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="a23b1-192">Open a PowerShell window as an administrator and enter the following commands.</span></span> <span data-ttu-id="a23b1-193">Reemplace *$pswd* por la contraseña que usó para crear este certificado.</span><span class="sxs-lookup"><span data-stu-id="a23b1-193">Replace the *$pswd* with the password that you used to create this certificate.</span></span> <span data-ttu-id="a23b1-194">Reemplace *$PfxFilePath* por la ruta de acceso completa del archivo .pfx copiado en este nodo.</span><span class="sxs-lookup"><span data-stu-id="a23b1-194">Replace the *$PfxFilePath* with the full path of the .pfx copied to this node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="a23b1-195">Ahora debe establecer el control de acceso de este certificado para que el proceso Service Fabric, que se ejecuta en la cuenta de servicio de red, pueda usarlo al ejecutar el script siguiente.</span><span class="sxs-lookup"><span data-stu-id="a23b1-195">Now set the access control on this certificate so that the Service Fabric process, which runs under the Network Service account, can use it by running the following script.</span></span> <span data-ttu-id="a23b1-196">Proporcione la huella digital del certificado y especifique "SERVICIO DE RED" para la cuenta de servicio.</span><span class="sxs-lookup"><span data-stu-id="a23b1-196">Provide the thumbprint of the certificate and "NETWORK SERVICE" for the service account.</span></span> <span data-ttu-id="a23b1-197">Para comprobar que las ACL del certificado son correctas, abra el certificado en *Inicio* > *Administrar certificados de equipo* y consulte *Todas las tareas* > *Administrar claves privadas*.</span><span class="sxs-lookup"><span data-stu-id="a23b1-197">You can check that the ACLs on the certificate are correct by opening the certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
   
    # Specify the user, the permissions and the permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of the machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get the current acl of the private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add the new ace to the acl of the private key
    $acl.SetAccessRule($accessRule)
   
    # Write back the new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe the access rights currently assigned to this certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="a23b1-198">Repita los pasos anteriores para cada certificado de servidor.</span><span class="sxs-lookup"><span data-stu-id="a23b1-198">Repeat the steps above for each server certificate.</span></span> <span data-ttu-id="a23b1-199">También puede usar estos pasos para instalar los certificados de cliente en las máquinas a las que desea permitir el acceso al clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-199">You can also use these steps to install the client certificates on the machines that you want to allow access to the cluster.</span></span>

## <a name="create-the-secure-cluster"></a><span data-ttu-id="a23b1-200">Creación del clúster seguro</span><span class="sxs-lookup"><span data-stu-id="a23b1-200">Create the secure cluster</span></span>
<span data-ttu-id="a23b1-201">Después de configurar la sección **security** del archivo **ClusterConfig.X509.MultiMachine.json**, puede continuar con la sección [Creación del clúster](service-fabric-cluster-creation-for-windows-server.md#createcluster) para configurar los nodos y crear el clúster independiente.</span><span class="sxs-lookup"><span data-stu-id="a23b1-201">After configuring the **security** section of the **ClusterConfig.X509.MultiMachine.json** file, you can proceed to [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section to configure the nodes and create the standalone cluster.</span></span> <span data-ttu-id="a23b1-202">Recuerde usar el archivo **ClusterConfig.X509.MultiMachine.json** al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-202">Remember to use the **ClusterConfig.X509.MultiMachine.json** file while creating the cluster.</span></span> <span data-ttu-id="a23b1-203">Por ejemplo, el comando podría ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="a23b1-203">For example, your command might look like the following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="a23b1-204">Una vez que el clúster de Windows independiente seguro se ejecuta correctamente y que ha configurado los clientes autenticados para conectarse a él, siga la sección [Conexión a un clúster seguro con PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) para conectarse a él.</span><span class="sxs-lookup"><span data-stu-id="a23b1-204">Once you have the secure standalone Windows cluster successfully running, and have setup the authenticated clients to connect to it, follow the section [Connect to a secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) to connect to it.</span></span> <span data-ttu-id="a23b1-205">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a23b1-205">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="a23b1-206">Luego puede ejecutar otros comandos de PowerShell para trabajar con este clúster.</span><span class="sxs-lookup"><span data-stu-id="a23b1-206">You can then run other PowerShell commands to work with this cluster.</span></span> <span data-ttu-id="a23b1-207">Por ejemplo, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) para mostrar una lista de los nodos en este clúster protegido.</span><span class="sxs-lookup"><span data-stu-id="a23b1-207">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) to show a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="a23b1-208">Para quitar el clúster, conéctese al nodo del clúster en el que descargó el paquete de Service Fabric, abra una línea de comandos y vaya a la carpeta del paquete.</span><span class="sxs-lookup"><span data-stu-id="a23b1-208">To remove the cluster, connect to the node on the cluster where you downloaded the Service Fabric package, open a command line and navigate to the package folder.</span></span> <span data-ttu-id="a23b1-209">Ahora ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="a23b1-209">Now run the following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="a23b1-210">Una configuración incorrecta de un certificado puede impedir que el clúster se muestre durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="a23b1-210">Incorrect certificate configuration may prevent the cluster from coming up during deployment.</span></span> <span data-ttu-id="a23b1-211">Para realizar un autodiagnóstico de los problemas de seguridad, consulte en el grupo del Visor de eventos *Registros de aplicaciones y servicios* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="a23b1-211">To self-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

