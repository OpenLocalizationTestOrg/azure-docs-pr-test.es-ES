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
# <a name="container-security"></a>Seguridad del contenedor

Service Fabric proporciona un mecanismo para los servicios dentro de un contenedor tooaccess un certificado que esté instalado en los nodos de hello en un clúster de Windows o Linux (versión 5.7 o superior). Además, Service Fabric también admite gMSA (cuentas de servicio administradas de grupo) para los contenedores de Windows. 

## <a name="certificate-management-for-containers"></a>Administración de certificados para contenedores

Puede proteger los servicios de contenedor especificando un certificado. Hola certificado debe instalarse en los nodos de Hola de clúster de Hola. Hello certificado se proporciona información en el manifiesto de aplicación hello en hello `ContainerHostPolicies` etiqueta como Hola fragmento siguiente muestra:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Al iniciar la aplicación hello, en tiempo de ejecución de hello lee certificados hello y genera un archivo PFX y una contraseña para cada certificado. Este archivo PFX y la contraseña son accesibles dentro de contenedor de hello mediante Hola después de las variables de entorno: 

* **Certificate_[CodePackageName]_[CertName]_PFX**
* **Certificate_[CodePackageName]_[CertName]_Password**

servicio de contenedor de Hola o un proceso es responsable de importar el archivo PFX de hello en contenedor Hola. certificado de hello tooimport, puede usar `setupentrypoint.sh` ejecutar código personalizado en proceso del contenedor de Hola o secuencias de comandos. Código de ejemplo en C# para importar el archivo PFX de hello sigue:

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
Este certificado PFX puede usarse para la aplicación hello de autenticar, servicio o commmunication segura con otros servicios.


## <a name="set-up-gmsa-for-windows-containers"></a>Configuración de gMSA para contenedores de Windows

tooset una gMSA (grupo de cuentas de servicio administradas), un archivo de especificación de credenciales (`credspec`) se coloca en todos los nodos de clúster de Hola. archivo Hello puede copiarse en todos los nodos con una extensión de máquina virtual.  Hola `credspec` archivo debe contener la información de la cuenta gMSA Hola. Para obtener más información sobre hello `credspec` de archivos, consulte [las cuentas de servicio](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). especificación de la credencial de Hola y Hola `Hostname` etiqueta se especifican en el manifiesto de aplicación Hola. Hola `Hostname` etiqueta debe coincidir con el nombre de cuenta de gMSA Hola Hola se ejecuta de contenedor con.  Hola `Hostname` etiqueta permite Hola contenedor tooauthenticate propio servicios tooother en dominio hello mediante la autenticación Kerberos.  Un ejemplo de especificación de hello `Hostname` hello y `credspec` en hello manifiesto de aplicación se muestra en el siguiente fragmento de código de hello:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Pasos siguientes

* [Implementar un tooService de contenedor de Windows Fabric en Windows Server 2016](service-fabric-get-started-containers.md)
* [Implementar un tooService de contenedor de Docker Fabric en Linux](service-fabric-get-started-containers-linux.md)
