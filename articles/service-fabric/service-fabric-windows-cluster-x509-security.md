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
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>Protección de un clúster independiente en Windows mediante certificados X.509
Este artículo describe cómo toosecure Hola comunican Hola varios nodos de un clúster de Windows independiente, así como el modo clientes tooauthenticate que se conectan clúster toothis, mediante certificados X.509. Esto garantiza que sólo los usuarios autorizados pueden tener acceso a los clúster hello, hello las aplicaciones implementadas y realizar tareas de administración.  Seguridad de certificado debe estar habilitado en clúster de hello cuando se crea un clúster Hola.  

Para más información sobre la seguridad de clúster, como la seguridad de nodo a nodo, la seguridad de cliente a nodo y el control de acceso basado en roles, consulte [Escenarios de seguridad de los clústeres de Service Fabric](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>¿Qué certificados necesitará?
toostart, [Descargar paquete de clúster de hello independiente](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone de nodos de hello en el clúster. Hola descargó paquete, encontrará un **ClusterConfig.X509.MultiMachine.json** archivo. Abra el archivo hello y revise la sección de Hola para **seguridad** en hello **propiedades** sección:

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

En esta sección se describe los certificados de Hola que necesita para proteger un clúster de Windows independiente. Si va a especificar un certificado de clúster, establezca el valor de Hola de **ClusterCredentialType** too_**X509**_. Si va a especificar el certificado de servidor para conexiones externas, establezca hello **ServerCredentialType** demasiado_**X509**_. Aunque no es obligatorio, se recomienda toohave ambos estos certificados para un clúster protegido correctamente. Si establece estos valores demasiado*X509* , a continuación, también debe especificar Hola certificados correspondientes o Service Fabric se iniciará una excepción. En algunos casos, podría desear sólo hello toospecify _ClientCertificateThumbprints_ o _ReverseProxyCertificate_. En esos escenarios, no es necesario definir _ClusterCredentialType_ o _ServerCredentialType_ too_X509_.


> [!NOTE]
> A [huella digital](https://en.wikipedia.org/wiki/Public_key_fingerprint) es Hola identidad principal de un certificado. Lectura [cómo tooretrieve huella digital de un certificado](https://msdn.microsoft.com/library/ms734695.aspx) toofind out huella digital de Hola de certificados de Hola que cree.
> 
> 

Hello tabla siguiente enumeran los certificados de Hola que necesita la configuración de clúster:

| **Valor de CertificateInformation** | **Descripción** |
| --- | --- |
| ClusterCertificate |Se recomienda para el entorno de prueba. Este certificado es necesario toosecure Hola comunicación entre los nodos de hello en un clúster. Puede utilizar dos certificados diferentes, uno principal y otro secundario para la actualización. Establecer la huella digital de hello del certificado principal de Hola Hola **huella digital** sección y el de hello secundario en hello **ThumbprintSecondary** variables. |
| ClusterCertificateCommonNames |Se recomienda para el entorno de producción. Este certificado es necesario toosecure Hola comunicación entre los nodos de hello en un clúster. Puede utilizar uno o dos nombres comunes del certificado de clúster. |
| ServerCertificate |Se recomienda para el entorno de prueba. Este certificado se presenta a toohello cliente cuando intente tooconnect toothis clúster. Para mayor comodidad, puede elegir toouse Hola mismo certificado para *ClusterCertificate* y *ServerCertificate*. Puede utilizar dos certificados de servidor diferentes, uno principal y otro secundario para la actualización. Establecer la huella digital de hello del certificado principal de Hola Hola **huella digital** sección y el de hello secundario en hello **ThumbprintSecondary** variables. |
| ServerCertificateCommonNames |Se recomienda para el entorno de producción. Este certificado se presenta a toohello cliente cuando intente tooconnect toothis clúster. Para mayor comodidad, puede elegir toouse Hola mismo certificado para *ClusterCertificateCommonNames* y *ServerCertificateCommonNames*. Puede utilizar uno o dos nombres comunes de certificado de servidor. |
| ClientCertificateThumbprints |Se trata de un conjunto de certificados que desea tooinstall en los clientes de hello autenticado. Puede tener un número diferente de certificados de cliente instalado en los equipos de Hola que desea que el clúster de tooallow acceso toohello. Establecer Hola huella digital de cada certificado en hello **CertificateThumbprint** variable. Si establece hello **IsAdmin** demasiado*true*, cliente hello con este certificado instalado en él puede realice administrador actividades de administración de clúster de Hola. Si hello **IsAdmin** es *false*, cliente hello con este certificado solo puede realizar acciones de hello permitidas para los derechos de acceso de usuario, normalmente de solo lectura. Para más información sobre roles, consulte [Control de acceso basado en roles (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Hola de conjunto de nombre común del certificado de cliente primera Hola para hello **CertificateCommonName**. Hola **CertificateIssuerThumbprint** es la huella digital de Hola para emisor Hola de este certificado. Lectura [trabajar con certificados](https://msdn.microsoft.com/library/ms731899.aspx) tooknow más información acerca de los nombres comunes y el emisor de Hola. |
| ReverseProxyCertificate |Se recomienda para el entorno de prueba. Se trata de un certificado opcional que se puede especificar si desea que toosecure su [un Proxy inverso](service-fabric-reverseproxy.md). Asegúrese de que reverseProxyEndpointPort está establecido en nodeTypes si usa este certificado. |
| ReverseProxyCertificateCommonNames |Se recomienda para el entorno de producción. Se trata de un certificado opcional que se puede especificar si desea que toosecure su [un Proxy inverso](service-fabric-reverseproxy.md). Asegúrese de que reverseProxyEndpointPort está establecido en nodeTypes si usa este certificado. |

Aquí es ejemplo de configuración de clúster donde se han proporcionado los certificados de cliente, servidor y clúster de Hola. Tenga en cuenta que para clúster / server / reverseProxy certificados, la huella digital y nombre común no se permiten toobe juntos para hello misma configuración tipo de certificado.

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

## <a name="certificate-roll-over"></a>Sustitución de certificados
Al utilizar el nombre común del certificado en lugar de la huella digital, el proceso de sustitución de certificados no precisa actualizar la configuración de clúster.
Si trata de la reversión de certificado emisor se sustituyen, tenga certificado emisor de la antigua hello en el almacén de certificados de hello al menos 2 horas después de instalar el nuevo certificado de emisor de Hola.

## <a name="acquire-hello-x509-certificates"></a>Adquirir certificados X.509 Hola
comunicación toosecure en clúster de hello, primero deberá tooobtain los certificados X.509 para los nodos del clúster. Asimismo, toolimit conexión toothis tooauthorized/users/máquinas del clúster, se necesita tooobtain e instalar certificados para equipos cliente de Hola.

Para los clústeres que ejecutan cargas de trabajo de producción, debe usar un [entidad de certificación (CA)](https://en.wikipedia.org/wiki/Certificate_authority) firmados de clúster de Hola de toosecure de certificado X.509. Para obtener más información acerca de cómo conseguir estos certificados, vaya demasiado[Cómo: obtener un certificado](http://msdn.microsoft.com/library/aa702761.aspx).

Para los clústeres que use para fines de prueba, puede elegir toouse un certificado autofirmado.

## <a name="optional-create-a-self-signed-certificate"></a>Opcional: Creación de un certificado autofirmado
Una manera de toocreate un certificado autofirmado que se pueden proteger correctamente es hello de toouse *CertSetup.ps1* script en carpeta de SDK del servicio Fabric hello en el directorio de hello *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Editar este nombre de archivo toochange Hola predeterminado del certificado de hello (Buscar valor hello *CN = ServiceFabricDevClusterCert*). Ejecute este script como `.\CertSetup.ps1 -Install`.

Exportar archivo de hello certificado tooa PFX con una contraseña protegida. Obtenga primero la huella digital de hello del certificado de Hola. De hello *iniciar* menú, ejecute hello *administrar certificados de equipo*. Navegue toohello **equipo Local/personal** crear carpeta ni Hola certificado que acaba de búsqueda. Haga doble clic en hello certificado tooopen él, seleccione hello *detalles* ficha y desplácese hacia abajo toohello *huella digital* campo. Copiar valor de huella digital de hello en el comando de PowerShell de Hola a continuación, después de quitar los espacios de Hola.  Hola de cambio `String` valor tooa contraseña segura adecuado tooprotect se y ejecución Hola siguiente en PowerShell:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

detalles de hello toosee de un certificado instalado en hello automático se puede ejecutar el siguiente comando de PowerShell de hello:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

O bien, si tiene una suscripción de Azure, siga la sección de hello [agregar certificados tooKey almacén](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Instalar certificados de Hola
Una vez que tenga certificados, puede instalarlas en nodos de clúster de Hola. Los nodos deben toohave Hola más reciente de Windows PowerShell 3.x instalado en ellos. Necesitará toorepeat estos pasos en cada nodo de clúster y el servidor de certificados y los certificados secundarios.

1. Nodo de toohello de los archivos de copia Hola pfx.
2. Abra una ventana de PowerShell como administrador y escriba Hola siga los comandos. Reemplace hello *$pswd* con contraseña hello usa toocreate este certificado. Reemplace hello *$PfxFilePath* con ruta de acceso completa de hello del nodo de hello .pfx toothis copiada.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Configurar ahora el control de acceso de hello en este certificado para que el proceso de Service Fabric hello, que se ejecuta con hello cuenta de servicio de red, puede usar mediante la ejecución de la siguiente secuencia de comandos de Hola. Proporcione la huella digital de Hola de certificado de Hola y "Servicio de red" para la cuenta de servicio de Hola. Puede comprobar que hello las ACL en el certificado de Hola son correctos, abra el certificado de hello en *iniciar* > *administrar certificados de equipo* y examinando *todas las tareas*  >  *Administrar claves privadas*.
   
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
4. Repita los pasos de hello anteriormente para cada certificado de servidor. También puede utilizar estos pasos tooinstall Hola certificados de cliente en equipos de Hola que desea que el clúster de tooallow acceso toohello.

## <a name="create-hello-secure-cluster"></a>Crear clúster segura Hola
Después de configurar hello **seguridad** sección de hello **ClusterConfig.X509.MultiMachine.json** archivo, puede continuar demasiado[Creae el clúster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure de sección Hola nodos y crear clúster de hello independiente. Recuerde hello toouse **ClusterConfig.X509.MultiMachine.json** archivo al crear el clúster de Hola. Por ejemplo, el comando sería Hola siguiente:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Una vez que tenga Hola segura independiente de Windows clúster que se ejecuta correctamente y configuró Hola de clientes autenticados tooconnect tooit, siga la sección de hello [conectar tooa clúster segura mediante PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. Por ejemplo:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

A continuación, puede ejecutar otro toowork de comandos de PowerShell con este clúster. Por ejemplo, [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow una lista de nodos de este clúster segura.


clúster de Hola de tooremove, conectar toohello nodo en clúster de Hola donde descargó el paquete de Service Fabric hello, abra una línea de comandos y desplazarse por las carpetas de paquete toohello. Ahora ejecute hello siguiente comando:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Configuración de un certificado incorrecto puede impedir que el clúster de hello salga durante la implementación. tooself-diagnosticar problemas de seguridad, consulte en el grupo del Visor de eventos *registros de aplicaciones y servicios* > *Microsoft Service Fabric*.
> 
> 

