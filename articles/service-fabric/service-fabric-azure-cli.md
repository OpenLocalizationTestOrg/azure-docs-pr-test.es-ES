---
title: aaaGetting a trabajar con Azure Service Fabric XPlat CLI
description: "Getting started with Azure Service Fabric XPlat CLI (Introducción a la CLI de XPlat de Azure Service Fabric)"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="11f6e-103">Uso de hello XPlat CLI toointeract con un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="11f6e-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="11f6e-104">Puede interactuar con el clúster de Service Fabric de máquinas de Linux con hello XPlat CLI en Linux.</span><span class="sxs-lookup"><span data-stu-id="11f6e-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="11f6e-105">primer paso de Hello es obtener última versión de Hola de Hola CLI desde rep de git de Hola y establezca, configúrelo en su ruta de acceso mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="11f6e-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="11f6e-106">Para cada comando, lo admite, puede escribir nombre de Hola de hello comando tooobtain Hola de ayuda para ese comando.</span><span class="sxs-lookup"><span data-stu-id="11f6e-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="11f6e-107">Se admite la finalización automática para los comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f6e-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="11f6e-108">Por ejemplo, hello después proporciona comandos ayuda para todos los comandos de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="11f6e-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="11f6e-109">Puede filtrar aún más el comando específico de hello ayuda tooa, como Hola siguiente ejemplo se muestra:</span><span class="sxs-lookup"><span data-stu-id="11f6e-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="11f6e-110">características de Autocompletar tooenable Hola CLI, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="11f6e-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="11f6e-111">Hola, siga los comandos conectar toohello clúster y mostrar Hola nodos de clúster de Hola:</span><span class="sxs-lookup"><span data-stu-id="11f6e-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="11f6e-112">toouse parámetros con nombre y encontrar qué son, puede escribir--ayuda después de un comando.</span><span class="sxs-lookup"><span data-stu-id="11f6e-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="11f6e-113">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="11f6e-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="11f6e-114">Cuando se conecta el clúster de varios equipos tooa desde un equipo **que no forma parte del clúster de hello**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="11f6e-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="11f6e-115">Reemplace la etiqueta de PublicIPorFQDN de hello con hello real IP o FQDN según corresponda.</span><span class="sxs-lookup"><span data-stu-id="11f6e-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="11f6e-116">Cuando se conecta el clúster de varios equipos tooa desde un equipo **que forma parte del clúster de hello**, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="11f6e-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="11f6e-117">Puede usar PowerShell o CLI toointeract con el clúster de Service Fabric de Linux creadas a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="11f6e-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="11f6e-118">Estos clústeres no están seguros, por lo tanto, puede abrir su cuadro de uno mediante la adición de la dirección IP pública hello en el manifiesto de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f6e-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="11f6e-119">Uso de clúster de Service Fabric de XPlat CLI tooconnect tooa Hola</span><span class="sxs-lookup"><span data-stu-id="11f6e-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="11f6e-120">Hola, siga los comandos de CLI de Azure describe cómo tooconnect tooa proteger clústeres.</span><span class="sxs-lookup"><span data-stu-id="11f6e-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="11f6e-121">Detalles del certificado Hola deben coincidir con un certificado en nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f6e-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="11f6e-122">Si el certificado tiene entidades de certificación (CA), deberá tooadd parámetro de ruta de certificado de ca de--hello como el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="11f6e-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="11f6e-123">Si tiene varias CA, use una coma como delimitador de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f6e-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="11f6e-124">Si el nombre común de certificado de hello no coincide con el extremo de la conexión de hello, podría utilizar el parámetro hello `--strict-ssl-false` toobypass Hola comprobación tal y como se muestra en el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="11f6e-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="11f6e-125">Si desea que la comprobación de hello CA tooskip, podría agregar hello: parámetro de false no autorizado rechazar tal y como se muestra en el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="11f6e-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="11f6e-126">Después de conectarse, debe ser capaz de toorun otro toointeract de comandos CLI con clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="11f6e-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="11f6e-127">Implementación de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="11f6e-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="11f6e-128">Ejecute hello siga los comandos toocopy, registrar e iniciar la aplicación de tejido de servicio de hello:</span><span class="sxs-lookup"><span data-stu-id="11f6e-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="11f6e-129">Actualización de la aplicación</span><span class="sxs-lookup"><span data-stu-id="11f6e-129">Upgrading your application</span></span>

<span data-ttu-id="11f6e-130">proceso de Hello es similar toohello [procesos de Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="11f6e-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="11f6e-131">Compile, copie, registre y cree su aplicación desde el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="11f6e-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="11f6e-132">Si la instancia de la aplicación se denomina `fabric:/MySFApp`y es de tipo hello MySFApp, comandos de hello sería como sigue:</span><span class="sxs-lookup"><span data-stu-id="11f6e-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="11f6e-133">Asegúrese de hello tooyour aplicación de cambios y volver a generar servicio Hola modificado.</span><span class="sxs-lookup"><span data-stu-id="11f6e-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="11f6e-134">Hola actualización había modificado archivo de manifiesto del servicio (ServiceManifest.xml) con las versiones de hello actualizado para hello servicio (y código o configuración o datos según corresponda).</span><span class="sxs-lookup"><span data-stu-id="11f6e-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="11f6e-135">También modificar el manifiesto de la aplicación hello (ApplicationManifest.xml) con el número de versión de Hola actualizado para aplicación hello y Hola servicio modificado.</span><span class="sxs-lookup"><span data-stu-id="11f6e-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="11f6e-136">Ahora, copiar y registrar la aplicación actualizada con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="11f6e-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="11f6e-137">Ahora, puede iniciar la actualización de la aplicación hello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="11f6e-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="11f6e-138">Ahora puede supervisar la actualización de la aplicación hello mediante SFX.</span><span class="sxs-lookup"><span data-stu-id="11f6e-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="11f6e-139">En unos minutos, habría actualizó la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="11f6e-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="11f6e-140">También intente una aplicación actualizada con un error y comprobar la funcionalidad de reversión automática de hello en el tejido de servicio.</span><span class="sxs-lookup"><span data-stu-id="11f6e-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="11f6e-141">Convertir de PFX tooPEM y viceversa.</span><span class="sxs-lookup"><span data-stu-id="11f6e-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="11f6e-142">Tendrá que tooinstall un certificado de los clústeres seguros de tooaccess máquina local (con Windows o Linux) que pueden estar en un entorno diferente.</span><span class="sxs-lookup"><span data-stu-id="11f6e-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="11f6e-143">Por ejemplo, al tener acceso a un clúster de Linux seguro desde un equipo Windows y viceversa deberá tooconvert el certificado del PFX tooPEM y viceversa.</span><span class="sxs-lookup"><span data-stu-id="11f6e-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="11f6e-144">tooconvert desde un archivo PFX de PEM archivo tooa, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="11f6e-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="11f6e-145">tooconvert desde un archivo PEM de tooa del archivo PFX, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="11f6e-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="11f6e-146">Consulte demasiado[OpenSSL documentación](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="11f6e-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="11f6e-147">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="11f6e-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="11f6e-148">Copia del paquete de aplicación hello no se realiza correctamente</span><span class="sxs-lookup"><span data-stu-id="11f6e-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="11f6e-149">Compruebe si `openssh` está instalado.</span><span class="sxs-lookup"><span data-stu-id="11f6e-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="11f6e-150">De forma predeterminada, el escritorio Ubuntu no lo tiene instalado.</span><span class="sxs-lookup"><span data-stu-id="11f6e-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="11f6e-151">Instalar mediante el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="11f6e-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="11f6e-152">Si persiste el problema de hello, pruebe a deshabilitar PAM para ssh cambiando hello `sshd_config` archivo mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="11f6e-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="11f6e-153">Si Hola problema todavía persiste, intente creciente número de Hola de ssh sesiones mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="11f6e-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="11f6e-154">Usar claves de ssh autenticación (como toopasswords opuestos) aún no se admite (como plataforma de hello utiliza ssh toocopy paquetes), por lo que utilice autenticación de contraseña en su lugar.</span><span class="sxs-lookup"><span data-stu-id="11f6e-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11f6e-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11f6e-155">Next steps</span></span>

[<span data-ttu-id="11f6e-156">Configurar el entorno de desarrollo de hello e implementar un clúster de Service Fabric aplicación tooa Linux.</span><span class="sxs-lookup"><span data-stu-id="11f6e-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="11f6e-157">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="11f6e-157">Related articles</span></span>

* <span data-ttu-id="11f6e-158">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Introducción a Service Fabric y la CLI de Azure 2.0)</span><span class="sxs-lookup"><span data-stu-id="11f6e-158">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md)</span></span>
