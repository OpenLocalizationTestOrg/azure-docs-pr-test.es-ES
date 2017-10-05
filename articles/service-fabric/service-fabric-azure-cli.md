---
title: "Getting started with Azure Service Fabric XPlat CLI (Introducción a la CLI de XPlat de Azure Service Fabric)"
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
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="34afa-103">Uso de la CLI de XPlat para interactuar con un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="34afa-103">Using the XPlat CLI to interact with a Service Fabric cluster</span></span>

<span data-ttu-id="34afa-104">Puede interactuar con un clúster de Service Fabric desde máquinas virtuales con Linux mediante la CLI de XPlat en Linux.</span><span class="sxs-lookup"><span data-stu-id="34afa-104">You can interact with Service Fabric cluster from Linux machines using the XPlat CLI on Linux.</span></span>

<span data-ttu-id="34afa-105">El primer paso es obtener la versión más reciente de la CLI en el repositorio de Git y configurarla en su ruta de acceso mediante los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="34afa-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="34afa-106">Para cada comando que admite, puede escribir el nombre del comando para obtener ayuda sobre él.</span><span class="sxs-lookup"><span data-stu-id="34afa-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span>
<span data-ttu-id="34afa-107">Se admite la finalización automática de los comandos.</span><span class="sxs-lookup"><span data-stu-id="34afa-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="34afa-108">Por ejemplo, el comando siguiente le proporciona ayuda para todos los comandos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34afa-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="34afa-109">Puede filtrar aún más la ayuda para un comando específico, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="34afa-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="34afa-110">Para habilitar la finalización automática en la CLI, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="34afa-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="34afa-111">Los siguientes comandos permiten conectar al clúster y le muestran los nodos de este:</span><span class="sxs-lookup"><span data-stu-id="34afa-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="34afa-112">Para utilizar parámetros con nombre y averiguar lo que son, puede escribir --help después del comando.</span><span class="sxs-lookup"><span data-stu-id="34afa-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="34afa-113">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="34afa-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="34afa-114">Si se conecta a un clúster de varias máquinas virtuales desde una máquina **que no forma parte de este**, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="34afa-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="34afa-115">Reemplace la etiqueta PublicIPorFQDN por la dirección IP o FQDN real según corresponda.</span><span class="sxs-lookup"><span data-stu-id="34afa-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="34afa-116">Si se conecta a un clúster de varias máquinas virtuales desde una máquina **que forma parte de este**, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="34afa-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="34afa-117">Puede usar PowerShell o CLI para interactuar con su clúster de Service Fabric para Linux creado mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="34afa-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="34afa-118">Estos clústeres no son seguros, por tanto, puede abrir el clúster one-box agregando la dirección IP pública en el manifiesto de clúster.</span><span class="sxs-lookup"><span data-stu-id="34afa-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="34afa-119">Uso de la CLI de XPlat para conectarse a un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="34afa-119">Using the XPlat CLI to connect to a Service Fabric cluster</span></span>

<span data-ttu-id="34afa-120">Los siguientes comandos de la CLI de Azure describen cómo conectarse a un clúster seguro.</span><span class="sxs-lookup"><span data-stu-id="34afa-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="34afa-121">Los detalles del certificado deben corresponder a un certificado de los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="34afa-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="34afa-122">Si el certificado tiene entidades de certificación (CA), debe agregar el parámetro --ca-cert-path como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="34afa-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="34afa-123">Si tiene varias entidades de certificación, use una coma como delimitador.</span><span class="sxs-lookup"><span data-stu-id="34afa-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="34afa-124">Si el nombre común del certificado no coincide con el punto de conexión de la conexión, puede usar el parámetro `--strict-ssl-false` para omitir la comprobación como se muestra en el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="34afa-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="34afa-125">Si desea omitir la comprobación de la entidad de certificación, puede agregar el parámetro --reject-unauthorized-false como se muestra en el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="34afa-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="34afa-126">Después de conectarse, debería poder ejecutar otros comandos de la CLI para interactuar con el clúster.</span><span class="sxs-lookup"><span data-stu-id="34afa-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="34afa-127">Implementación de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="34afa-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="34afa-128">Ejecute los comandos siguientes para copiar, registrar e iniciar la aplicación de Service fabric:</span><span class="sxs-lookup"><span data-stu-id="34afa-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="34afa-129">Actualización de la aplicación</span><span class="sxs-lookup"><span data-stu-id="34afa-129">Upgrading your application</span></span>

<span data-ttu-id="34afa-130">El proceso es similar al [proceso en Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="34afa-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="34afa-131">Compile, copie, registre y cree su aplicación desde el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="34afa-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="34afa-132">Si la instancia de la aplicación se denomina `fabric:/MySFApp`, y el tipo es MySFApp, los comandos deben ser como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="34afa-132">If your application instance is named `fabric:/MySFApp`, and the type is MySFApp, the commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="34afa-133">Realice el cambio en la aplicación y vuelva a compilar el servicio modificado.</span><span class="sxs-lookup"><span data-stu-id="34afa-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="34afa-134">Actualice el archivo de manifiesto del servicio modificado (ServiceManifest.xml) con las versiones actualizadas para el servicio (y el código o la configuración o los datos según corresponda).</span><span class="sxs-lookup"><span data-stu-id="34afa-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="34afa-135">Modifique también el manifiesto de la aplicación (ApplicationManifest.xml) con el número de la versión actualizada de la aplicación y el servicio modificado.</span><span class="sxs-lookup"><span data-stu-id="34afa-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="34afa-136">Después, copie y registre la aplicación actualizada con los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="34afa-136">Now, copy and register your updated application using the following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="34afa-137">Con esto, ya puede iniciar la actualización de la aplicación con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="34afa-137">Now, you can start the application upgrade with the following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="34afa-138">Ya puede supervisar mediante SFX la actualización de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34afa-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="34afa-139">En unos minutos se habrá actualizado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34afa-139">In a few minutes, the application would have been updated.</span></span> <span data-ttu-id="34afa-140">También puede probar una aplicación actualizada con un error y comprobar la funcionalidad de reversión automática en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="34afa-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="34afa-141">Conversión de PFX a PEM y viceversa</span><span class="sxs-lookup"><span data-stu-id="34afa-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="34afa-142">Podría necesitar instalar un certificado en el equipo local (con Windows o Linux) para tener acceso a los clústeres seguros que pueden estar en un entorno diferente.</span><span class="sxs-lookup"><span data-stu-id="34afa-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="34afa-143">Por ejemplo, al acceder a un clúster de Linux seguro desde un equipo Windows y viceversa, debe convertir el certificado PFX a PEM y viceversa.</span><span class="sxs-lookup"><span data-stu-id="34afa-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="34afa-144">Para convertir un archivo PEM a uno PFX, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="34afa-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="34afa-145">Para convertir un archivo PFX en uno PEM, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="34afa-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="34afa-146">Consulte la [documentación de OpenSSL](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="34afa-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="34afa-147">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="34afa-147">Troubleshooting</span></span>


### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="34afa-148">La copia del paquete de aplicación no se realiza correctamente</span><span class="sxs-lookup"><span data-stu-id="34afa-148">Copying of the application package does not succeed</span></span>

<span data-ttu-id="34afa-149">Compruebe si `openssh` está instalado.</span><span class="sxs-lookup"><span data-stu-id="34afa-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="34afa-150">De forma predeterminada, el escritorio Ubuntu no lo tiene instalado.</span><span class="sxs-lookup"><span data-stu-id="34afa-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="34afa-151">Instálelo con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="34afa-151">Install it using the following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="34afa-152">Si el problema persiste, pruebe a deshabilitar PAM para ssh cambiando el archivo `sshd_config` mediante los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="34afa-152">If the problem persists, try disabling PAM for ssh by changing the `sshd_config` file using the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="34afa-153">Si aun así, el problema continúa, pruebe a aumentar el número de sesiones de ssh ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="34afa-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="34afa-154">El uso de claves para la autenticación ssh (en lugar de contraseñas) no se admite todavía (ya que la plataforma usa ssh para copiar los paquetes), así que use la autenticación de contraseña en su lugar.</span><span class="sxs-lookup"><span data-stu-id="34afa-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34afa-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34afa-155">Next steps</span></span>

[<span data-ttu-id="34afa-156">Configure el entorno de desarrollo e implementar una aplicación de Service Fabric en un clúster de Linux.</span><span class="sxs-lookup"><span data-stu-id="34afa-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="34afa-157">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="34afa-157">Related articles</span></span>

* <span data-ttu-id="34afa-158">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Introducción a Service Fabric y la CLI de Azure 2.0)</span><span class="sxs-lookup"><span data-stu-id="34afa-158">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md)</span></span>
