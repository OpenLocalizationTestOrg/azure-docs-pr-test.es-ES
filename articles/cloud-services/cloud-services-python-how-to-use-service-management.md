---
title: "aaaHow API (Python) - Guía de características de administración de servicios de hello toouse"
description: "Obtenga información acerca de cómo tooprogrammatically realizar tareas comunes de administración de servicio desde Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="7d4d5-103">¿Cómo toouse administración del servicio desde Python</span><span class="sxs-lookup"><span data-stu-id="7d4d5-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="7d4d5-104">Esta guía le mostrará cómo tooprogrammatically realizar tareas comunes de administración de servicio desde Python.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="7d4d5-105">Hola **ServiceManagementService** clase Hola [Azure SDK para Python](https://github.com/Azure/azure-sdk-for-python) admite el acceso mediante programación toomuch de hello servicio Administración funcionalidad relacionada con el que está disponible en hello [Portal de azure clásico] [ management-portal] (como **crear, actualizar y eliminar servicios en la nube, las implementaciones, los servicios de administración de datos y máquinas virtuales**).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="7d4d5-106">Esta funcionalidad puede ser útil en la creación de aplicaciones que necesitan la administración de tooservice de acceso mediante programación.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="7d4d5-107"><a name="WhatIs"></a>Qué es la administración de servicios</span><span class="sxs-lookup"><span data-stu-id="7d4d5-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="7d4d5-108">Hola API de administración de servicios proporciona acceso mediante programación toomuch de funcionalidad de administración de servicio de hello disponible a través de hello [portal de Azure clásico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="7d4d5-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="7d4d5-109">Hello Azure SDK para Python permite toomanage sus cuentas de almacenamiento y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="7d4d5-110">API de administración de servicios de hello toouse, necesita demasiado[crear una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="7d4d5-111"><a name="Concepts"></a>Conceptos</span><span class="sxs-lookup"><span data-stu-id="7d4d5-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="7d4d5-112">Hello Azure SDK para Python ajusta hello [API de administración de servicios de Azure][svc-mgmt-rest-api], que es una API de REST.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="7d4d5-113">Todas las operaciones de la API se realizan mediante SSL y se autentican mutuamente con los certificados X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="7d4d5-114">puede tener acceso al servicio de administración de Hola desde dentro de un servicio que se ejecuta en Azure, o directamente a través de hello Internet desde cualquier aplicación que pueda enviar una solicitud HTTPS y recibir una respuesta HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="7d4d5-115"><a name="Installation"></a>Instalación</span><span class="sxs-lookup"><span data-stu-id="7d4d5-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="7d4d5-116">Todas las características de Hola se describe en este artículo están disponibles en hello `azure-servicemanagement-legacy` paquete, que se puede instalar con pip.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="7d4d5-117">Para obtener más información acerca de la instalación (por ejemplo, si está tooPython nuevo), consulte este artículo: [instalar Python y hello Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="7d4d5-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="7d4d5-118"><a name="Connect"></a>Cómo: conectar tooservice management</span><span class="sxs-lookup"><span data-stu-id="7d4d5-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="7d4d5-119">extremo de administración de servicios de tooconnect toohello, necesita el identificador de la suscripción de Azure y un certificado de administración válido.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="7d4d5-120">Puede obtener el identificador de suscripción a través de hello [portal de Azure clásico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="7d4d5-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="7d4d5-121">Ahora es certificados toouse posibles que se crean con OpenSSL cuando se ejecuta en Windows.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="7d4d5-122">Para ello, se requiere Python 2.7.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="7d4d5-123">Se recomienda a los usuarios toouse OpenSSL en lugar de .pfx, desde el soporte técnico para .pfx certificados es probable que se quitará en futuras Hola.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="7d4d5-124">Certificados de administración en Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="7d4d5-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="7d4d5-125">Puede usar [OpenSSL](http://www.openssl.org/) toocreate su certificado de administración.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="7d4d5-126">Necesita realmente toocreate dos certificados, uno para el servidor de hello (un `.cer` archivo) y otro para el cliente de hello (un `.pem` archivo).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="7d4d5-127">Hola toocreate `.pem` de archivos, ejecute:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="7d4d5-128">Hola toocreate `.cer` de certificados, ejecute:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="7d4d5-129">Para más información sobre los certificados de Azure, consulte [Introducción a los certificados para los servicios en la nube de Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="7d4d5-130">Para obtener una descripción completa de parámetros de OpenSSL, vea la documentación de hello en [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="7d4d5-131">Después de crear estos archivos, necesita hello tooupload `.cer` archivo tooAzure mediante una acción de "Cargar" hello de ficha "Configuración" Hola Hola [portal de Azure clásico][management-portal], y deberá toomake nota de donde guardó hello `.pem` archivo.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="7d4d5-132">Después de haber obtenido el identificador de suscripción, ha creado un certificado y cargado hello `.cer` tooAzure de archivo, puede conectar el extremo de administración de Azure de toohello pasando el Id. de suscripción de Hola y Hola ruta de acceso toohello `.pem` archivo demasiado**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="7d4d5-133">En el anterior ejemplo, el Hola `sms` es un **ServiceManagementService** objeto.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="7d4d5-134">Hola **ServiceManagementService** clase es hello toomanage de clase principal que se usa servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="7d4d5-135">Certificados de administración en Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="7d4d5-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="7d4d5-136">Puede crear un certificado de administración autofirmado en la máquina con `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="7d4d5-137">Abra un **símbolo del sistema de Visual Studio** como un **administrador** y usar hello siguiente comando, reemplazando *AzureCertificate* con el nombre de certificado de hello le gustaría toouse.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="7d4d5-138">comando de Hello crea hello `.cer` de archivo y lo instala en hello **Personal** almacén de certificados.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="7d4d5-139">Para obtener más información, consulte [Introducción a los certificados para Azure Cloud Services](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="7d4d5-140">Después de haber creado el certificado de hello, necesita hello tooupload `.cer` archivo tooAzure mediante una acción de "Cargar" hello de ficha "Configuración" Hola Hola [portal de Azure clásico][management-portal].</span><span class="sxs-lookup"><span data-stu-id="7d4d5-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="7d4d5-141">Después de haber obtenido el identificador de suscripción, ha creado un certificado y cargado hello `.cer` tooAzure de archivo, puede conectar el extremo de administración de Azure de toohello pasando el Id. de suscripción de Hola y la ubicación de hello del certificado de hello en su **Personal** almacén de certificados demasiado**ServiceManagementService** (de nuevo, reemplace *AzureCertificate* con el nombre de hello en el certificado de):</span><span class="sxs-lookup"><span data-stu-id="7d4d5-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="7d4d5-142">En el anterior ejemplo, el Hola `sms` es un **ServiceManagementService** objeto.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="7d4d5-143">Hola **ServiceManagementService** clase es hello toomanage de clase principal que se usa servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="7d4d5-144"><a name="ListAvailableLocations"></a>Enumeración de las ubicaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="7d4d5-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="7d4d5-145">ubicaciones de hello toolist que están disponibles para hospedar servicios, usar hello **lista\_ubicaciones** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="7d4d5-146">Cuando se crea un servicio de nube o el servicio de almacenamiento debe tooprovide una ubicación válida.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="7d4d5-147">Hola **lista\_ubicaciones** método siempre devuelve una lista actualizada de ubicaciones disponibles actualmente Hola.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="7d4d5-148">Cuando se redactó este documento, ubicaciones de hello disponibles son:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="7d4d5-149">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="7d4d5-149">West Europe</span></span>
* <span data-ttu-id="7d4d5-150">Europa del Norte</span><span class="sxs-lookup"><span data-stu-id="7d4d5-150">North Europe</span></span>
* <span data-ttu-id="7d4d5-151">Sudeste asiático</span><span class="sxs-lookup"><span data-stu-id="7d4d5-151">Southeast Asia</span></span>
* <span data-ttu-id="7d4d5-152">Asia oriental</span><span class="sxs-lookup"><span data-stu-id="7d4d5-152">East Asia</span></span>
* <span data-ttu-id="7d4d5-153">Central EE. UU.:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-153">Central US</span></span>
* <span data-ttu-id="7d4d5-154">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="7d4d5-154">North Central US</span></span>
* <span data-ttu-id="7d4d5-155">Centro-Sur de EE. UU</span><span class="sxs-lookup"><span data-stu-id="7d4d5-155">South Central US</span></span>
* <span data-ttu-id="7d4d5-156">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-156">West US</span></span>
* <span data-ttu-id="7d4d5-157">Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-157">East US</span></span>
* <span data-ttu-id="7d4d5-158">Este de Japón</span><span class="sxs-lookup"><span data-stu-id="7d4d5-158">Japan East</span></span>
* <span data-ttu-id="7d4d5-159">Oeste de Japón</span><span class="sxs-lookup"><span data-stu-id="7d4d5-159">Japan West</span></span>
* <span data-ttu-id="7d4d5-160">Sur de Brasil</span><span class="sxs-lookup"><span data-stu-id="7d4d5-160">Brazil South</span></span>
* <span data-ttu-id="7d4d5-161">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="7d4d5-161">Australia East</span></span>
* <span data-ttu-id="7d4d5-162">Sudeste de Australia</span><span class="sxs-lookup"><span data-stu-id="7d4d5-162">Australia Southeast</span></span>

## <span data-ttu-id="7d4d5-163"><a name="CreateCloudService"></a>Creación de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="7d4d5-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="7d4d5-164">Cuando se crea una aplicación y ejecutarla en Azure, código de hello y configuración junto se denominan un Azure [servicio en la nube] [ cloud service] (conocido como un *servicio hospedado* en versiones anteriores Versiones de Azure).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="7d4d5-165">Hola **crear\_hospedado\_servicio** método le permite toocreate un nuevo servicio hospedado proporcionando un nombre de servicio hospedado (que debe ser único en Azure), una etiqueta (toobase64 automáticamente codificada), un Descripción y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="7d4d5-166">Puede enumerar todos los servicios de hello hospedado para su suscripción con hello **lista\_hospedado\_servicios** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="7d4d5-167">Si desea tooget información acerca de un servicio hospedado concreto, puede hacerlo pasando Hola hospedado servicio nombre toohello **obtener\_hospedado\_servicio\_propiedades** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="7d4d5-168">Después de haber creado un servicio de nube, puede implementar su servicio de toohello de código con hello **crear\_implementación** método.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="7d4d5-169"><a name="DeleteCloudService"></a>Eliminación de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="7d4d5-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="7d4d5-170">Puede eliminar un servicio de nube pasando Hola servicio nombre toohello **eliminar\_hospedado\_servicio** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="7d4d5-171">Antes de poder eliminar un servicio, primero deben eliminar todas las implementaciones para servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="7d4d5-172">(Vea [Eliminación de una implementación](#DeleteDeployment) para obtener información detallada).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="7d4d5-173"><a name="DeleteDeployment"></a>Eliminación de una implementación</span><span class="sxs-lookup"><span data-stu-id="7d4d5-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="7d4d5-174">toodelete una implementación, use hello **eliminar\_implementación** método.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="7d4d5-175">Hello en el ejemplo siguiente se muestra cómo toodelete una implementación denominado `v1`.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="7d4d5-176"><a name="CreateStorageService"></a>Creación de un servicio de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="7d4d5-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="7d4d5-177">A [servicio de almacenamiento](../storage/common/storage-create-storage-account.md) le proporcionan acceso tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tablas](../cosmos-db/table-storage-how-to-use-python.md), y [colas](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="7d4d5-178">toocreate un servicio de almacenamiento, necesita un nombre para el servicio de hello (entre 3 y 24 caracteres en minúsculas y único dentro de Azure), una descripción, una etiqueta (los caracteres de too100, toobase64 automáticamente codificado) y una ubicación.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="7d4d5-179">Hola de ejemplo siguiente muestra cómo toocreate un almacenamiento de servicio mediante la especificación de una ubicación.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="7d4d5-180">Tenga en cuenta en el anterior ejemplo de Hola estado Hola de hello **crear\_almacenamiento\_cuenta** operación se puede recuperar pasando el resultado de hello devuelto por **crear\_almacenamiento \_cuenta** toohello **obtener\_operación\_estado** método.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="7d4d5-181">Puede enumerar las cuentas de almacenamiento y sus propiedades con hello **lista\_almacenamiento\_cuentas** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="7d4d5-182"><a name="DeleteStorageService"></a>Eliminación de un servicio de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="7d4d5-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="7d4d5-183">Puede eliminar un servicio de almacenamiento pasando toohello de nombre de servicio de almacenamiento de hello **eliminar\_almacenamiento\_cuenta** método.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="7d4d5-184">Al eliminar un servicio de almacenamiento, eliminan todos los datos almacenados en el servicio de hello (blobs, tablas y colas).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="7d4d5-185"><a name="ListOperatingSystems"></a>Enumeración de los sistemas operativos disponibles</span><span class="sxs-lookup"><span data-stu-id="7d4d5-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="7d4d5-186">sistemas operativos de toolist Hola que están disponibles para hospedar servicios, usar hello **lista\_operativo\_sistemas** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="7d4d5-187">Como alternativa, puede usar hello **lista\_operativo\_system\_familias** método, que agrupa los sistemas operativos de Hola por familia:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="7d4d5-188"><a name="CreateVMImage"></a>Creación de una imagen de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="7d4d5-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="7d4d5-189">tooadd un repositorio de imágenes toohello de imagen de sistema operativo, use hello **agregar\_os\_imagen** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="7d4d5-190">las imágenes de sistema operativo de hello toolist que están disponibles, usar hello **lista\_os\_imágenes** método.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="7d4d5-191">Se incluyen todas las imágenes de la plataforma y las imágenes de usuario:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="7d4d5-192"><a name="DeleteVMImage"></a>Eliminación de una imagen de sistema operativo</span><span class="sxs-lookup"><span data-stu-id="7d4d5-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="7d4d5-193">toodelete una imagen de usuario, use hello **eliminar\_os\_imagen** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="7d4d5-194"><a name="CreateVM"></a>Creación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7d4d5-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="7d4d5-195">toocreate una máquina virtual, primero debe toocreate una [servicio en la nube](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="7d4d5-196">A continuación, crear implementación de máquina virtual de hello mediante hello **crear\_virtuales\_máquina\_implementación** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="7d4d5-197"><a name="DeleteVM"></a>Eliminación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7d4d5-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="7d4d5-198">toodelete una máquina virtual, primero eliminar implementación hello mediante hello **eliminar\_implementación** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="7d4d5-199">servicio de nube de Hello, a continuación, puede eliminarse con hello **eliminar\_hospedado\_servicio** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="7d4d5-200">Creación de una máquina virtual a partir de una imagen de máquina virtual capturada.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="7d4d5-201">toocapture una imagen de VM, llame primero a hello **capturar\_vm\_imagen** método:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="7d4d5-202">Después, toomake seguro de que ha capturado correctamente imagen hello, usar hello **lista\_vm\_imágenes** api y asegúrese de que la imagen se muestra en los resultados de hello:</span><span class="sxs-lookup"><span data-stu-id="7d4d5-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="7d4d5-203">toofinally crear máquina virtual de hello mediante la imagen capturada hello, use hello **crear\_virtuales\_máquina\_implementación** método como antes, pero esta vez pasar en hello vm_image_name</span><span class="sxs-lookup"><span data-stu-id="7d4d5-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="7d4d5-204">Obtenga más información sobre toolearn toocapture una máquina Virtual de Linux, vea [cómo tooCapture una máquina Virtual Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="7d4d5-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="7d4d5-205">Obtenga más información sobre toolearn toocapture una máquina Virtual de Windows, vea [cómo tooCapture una máquina Virtual Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="7d4d5-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="7d4d5-206"><a name="What's Next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7d4d5-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="7d4d5-207">Ahora que conoce los fundamentos de Hola de administración del servicio, puede tener acceso a hello [documentación de referencia de API completa de hello Azure SDK de Python](http://azure-sdk-for-python.readthedocs.org/) y realizar complejo tareas fácilmente toomanage la aplicación de python.</span><span class="sxs-lookup"><span data-stu-id="7d4d5-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="7d4d5-208">Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="7d4d5-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
