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
# <a name="how-toouse-service-management-from-python"></a>¿Cómo toouse administración del servicio desde Python
Esta guía le mostrará cómo tooprogrammatically realizar tareas comunes de administración de servicio desde Python. Hola **ServiceManagementService** clase Hola [Azure SDK para Python](https://github.com/Azure/azure-sdk-for-python) admite el acceso mediante programación toomuch de hello servicio Administración funcionalidad relacionada con el que está disponible en hello [Portal de azure clásico] [ management-portal] (como **crear, actualizar y eliminar servicios en la nube, las implementaciones, los servicios de administración de datos y máquinas virtuales**). Esta funcionalidad puede ser útil en la creación de aplicaciones que necesitan la administración de tooservice de acceso mediante programación.

## <a name="WhatIs"></a>Qué es la administración de servicios
Hola API de administración de servicios proporciona acceso mediante programación toomuch de funcionalidad de administración de servicio de hello disponible a través de hello [portal de Azure clásico][management-portal]. Hello Azure SDK para Python permite toomanage sus cuentas de almacenamiento y servicios en la nube.

API de administración de servicios de hello toouse, necesita demasiado[crear una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"></a>Conceptos
Hello Azure SDK para Python ajusta hello [API de administración de servicios de Azure][svc-mgmt-rest-api], que es una API de REST. Todas las operaciones de la API se realizan mediante SSL y se autentican mutuamente con los certificados X.509 v3. puede tener acceso al servicio de administración de Hola desde dentro de un servicio que se ejecuta en Azure, o directamente a través de hello Internet desde cualquier aplicación que pueda enviar una solicitud HTTPS y recibir una respuesta HTTPS.

## <a name="Installation"></a>Instalación
Todas las características de Hola se describe en este artículo están disponibles en hello `azure-servicemanagement-legacy` paquete, que se puede instalar con pip. Para obtener más información acerca de la instalación (por ejemplo, si está tooPython nuevo), consulte este artículo: [instalar Python y hello Azure SDK](../python-how-to-install.md)

## <a name="Connect"></a>Cómo: conectar tooservice management
extremo de administración de servicios de tooconnect toohello, necesita el identificador de la suscripción de Azure y un certificado de administración válido. Puede obtener el identificador de suscripción a través de hello [portal de Azure clásico][management-portal].

> [!NOTE]
> Ahora es certificados toouse posibles que se crean con OpenSSL cuando se ejecuta en Windows.  Para ello, se requiere Python 2.7.4 o posterior. Se recomienda a los usuarios toouse OpenSSL en lugar de .pfx, desde el soporte técnico para .pfx certificados es probable que se quitará en futuras Hola.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Certificados de administración en Windows/Mac/Linux (OpenSSL)
Puede usar [OpenSSL](http://www.openssl.org/) toocreate su certificado de administración.  Necesita realmente toocreate dos certificados, uno para el servidor de hello (un `.cer` archivo) y otro para el cliente de hello (un `.pem` archivo). Hola toocreate `.pem` de archivos, ejecute:

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Hola toocreate `.cer` de certificados, ejecute:

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Para más información sobre los certificados de Azure, consulte [Introducción a los certificados para los servicios en la nube de Azure](cloud-services-certs-create.md). Para obtener una descripción completa de parámetros de OpenSSL, vea la documentación de hello en [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

Después de crear estos archivos, necesita hello tooupload `.cer` archivo tooAzure mediante una acción de "Cargar" hello de ficha "Configuración" Hola Hola [portal de Azure clásico][management-portal], y deberá toomake nota de donde guardó hello `.pem` archivo.

Después de haber obtenido el identificador de suscripción, ha creado un certificado y cargado hello `.cer` tooAzure de archivo, puede conectar el extremo de administración de Azure de toohello pasando el Id. de suscripción de Hola y Hola ruta de acceso toohello `.pem` archivo demasiado**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

En el anterior ejemplo, el Hola `sms` es un **ServiceManagementService** objeto. Hola **ServiceManagementService** clase es hello toomanage de clase principal que se usa servicios de Azure.

### <a name="management-certificates-on-windows-makecert"></a>Certificados de administración en Windows (MakeCert)
Puede crear un certificado de administración autofirmado en la máquina con `makecert.exe`.  Abra un **símbolo del sistema de Visual Studio** como un **administrador** y usar hello siguiente comando, reemplazando *AzureCertificate* con el nombre de certificado de hello le gustaría toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

comando de Hello crea hello `.cer` de archivo y lo instala en hello **Personal** almacén de certificados. Para obtener más información, consulte [Introducción a los certificados para Azure Cloud Services](cloud-services-certs-create.md).

Después de haber creado el certificado de hello, necesita hello tooupload `.cer` archivo tooAzure mediante una acción de "Cargar" hello de ficha "Configuración" Hola Hola [portal de Azure clásico][management-portal].

Después de haber obtenido el identificador de suscripción, ha creado un certificado y cargado hello `.cer` tooAzure de archivo, puede conectar el extremo de administración de Azure de toohello pasando el Id. de suscripción de Hola y la ubicación de hello del certificado de hello en su **Personal** almacén de certificados demasiado**ServiceManagementService** (de nuevo, reemplace *AzureCertificate* con el nombre de hello en el certificado de):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

En el anterior ejemplo, el Hola `sms` es un **ServiceManagementService** objeto. Hola **ServiceManagementService** clase es hello toomanage de clase principal que se usa servicios de Azure.

## <a name="ListAvailableLocations"></a>Enumeración de las ubicaciones disponibles
ubicaciones de hello toolist que están disponibles para hospedar servicios, usar hello **lista\_ubicaciones** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

Cuando se crea un servicio de nube o el servicio de almacenamiento debe tooprovide una ubicación válida. Hola **lista\_ubicaciones** método siempre devuelve una lista actualizada de ubicaciones disponibles actualmente Hola. Cuando se redactó este documento, ubicaciones de hello disponibles son:

* Europa occidental
* Europa del Norte
* Sudeste asiático
* Asia oriental
* Central EE. UU.:
* Centro-Norte de EE. UU
* Centro-Sur de EE. UU
* Oeste de EE. UU.
* Este de EE. UU.
* Este de Japón
* Oeste de Japón
* Sur de Brasil
* Australia Oriental
* Sudeste de Australia

## <a name="CreateCloudService"></a>Creación de un servicio en la nube
Cuando se crea una aplicación y ejecutarla en Azure, código de hello y configuración junto se denominan un Azure [servicio en la nube] [ cloud service] (conocido como un *servicio hospedado* en versiones anteriores Versiones de Azure). Hola **crear\_hospedado\_servicio** método le permite toocreate un nuevo servicio hospedado proporcionando un nombre de servicio hospedado (que debe ser único en Azure), una etiqueta (toobase64 automáticamente codificada), un Descripción y una ubicación.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

Puede enumerar todos los servicios de hello hospedado para su suscripción con hello **lista\_hospedado\_servicios** método:

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Si desea tooget información acerca de un servicio hospedado concreto, puede hacerlo pasando Hola hospedado servicio nombre toohello **obtener\_hospedado\_servicio\_propiedades** método:

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

Después de haber creado un servicio de nube, puede implementar su servicio de toohello de código con hello **crear\_implementación** método.

## <a name="DeleteCloudService"></a>Eliminación de un servicio en la nube
Puede eliminar un servicio de nube pasando Hola servicio nombre toohello **eliminar\_hospedado\_servicio** método:

    sms.delete_hosted_service('myhostedservice')

Antes de poder eliminar un servicio, primero deben eliminar todas las implementaciones para servicio de Hola. (Vea [Eliminación de una implementación](#DeleteDeployment) para obtener información detallada).

## <a name="DeleteDeployment"></a>Eliminación de una implementación
toodelete una implementación, use hello **eliminar\_implementación** método. Hello en el ejemplo siguiente se muestra cómo toodelete una implementación denominado `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"></a>Creación de un servicio de almacenamiento
A [servicio de almacenamiento](../storage/common/storage-create-storage-account.md) le proporcionan acceso tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tablas](../cosmos-db/table-storage-how-to-use-python.md), y [colas](../storage/queues/storage-python-how-to-use-queue-storage.md). toocreate un servicio de almacenamiento, necesita un nombre para el servicio de hello (entre 3 y 24 caracteres en minúsculas y único dentro de Azure), una descripción, una etiqueta (los caracteres de too100, toobase64 automáticamente codificado) y una ubicación. Hola de ejemplo siguiente muestra cómo toocreate un almacenamiento de servicio mediante la especificación de una ubicación.

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

Tenga en cuenta en el anterior ejemplo de Hola estado Hola de hello **crear\_almacenamiento\_cuenta** operación se puede recuperar pasando el resultado de hello devuelto por **crear\_almacenamiento \_cuenta** toohello **obtener\_operación\_estado** método.  

Puede enumerar las cuentas de almacenamiento y sus propiedades con hello **lista\_almacenamiento\_cuentas** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"></a>Eliminación de un servicio de almacenamiento
Puede eliminar un servicio de almacenamiento pasando toohello de nombre de servicio de almacenamiento de hello **eliminar\_almacenamiento\_cuenta** método. Al eliminar un servicio de almacenamiento, eliminan todos los datos almacenados en el servicio de hello (blobs, tablas y colas).

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"></a>Enumeración de los sistemas operativos disponibles
sistemas operativos de toolist Hola que están disponibles para hospedar servicios, usar hello **lista\_operativo\_sistemas** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

Como alternativa, puede usar hello **lista\_operativo\_system\_familias** método, que agrupa los sistemas operativos de Hola por familia:

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"></a>Creación de una imagen de sistema operativo
tooadd un repositorio de imágenes toohello de imagen de sistema operativo, use hello **agregar\_os\_imagen** método:

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

las imágenes de sistema operativo de hello toolist que están disponibles, usar hello **lista\_os\_imágenes** método. Se incluyen todas las imágenes de la plataforma y las imágenes de usuario:

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

## <a name="DeleteVMImage"></a>Eliminación de una imagen de sistema operativo
toodelete una imagen de usuario, use hello **eliminar\_os\_imagen** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"></a>Creación de una máquina virtual
toocreate una máquina virtual, primero debe toocreate una [servicio en la nube](#CreateCloudService).  A continuación, crear implementación de máquina virtual de hello mediante hello **crear\_virtuales\_máquina\_implementación** método:

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

## <a name="DeleteVM"></a>Eliminación de una máquina virtual
toodelete una máquina virtual, primero eliminar implementación hello mediante hello **eliminar\_implementación** método:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

servicio de nube de Hello, a continuación, puede eliminarse con hello **eliminar\_hospedado\_servicio** método:

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Creación de una máquina virtual a partir de una imagen de máquina virtual capturada.
toocapture una imagen de VM, llame primero a hello **capturar\_vm\_imagen** método:

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

Después, toomake seguro de que ha capturado correctamente imagen hello, usar hello **lista\_vm\_imágenes** api y asegúrese de que la imagen se muestra en los resultados de hello:

    images = sms.list_vm_images()

toofinally crear máquina virtual de hello mediante la imagen capturada hello, use hello **crear\_virtuales\_máquina\_implementación** método como antes, pero esta vez pasar en hello vm_image_name

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

Obtenga más información sobre toolearn toocapture una máquina Virtual de Linux, vea [cómo tooCapture una máquina Virtual Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

Obtenga más información sobre toolearn toocapture una máquina Virtual de Windows, vea [cómo tooCapture una máquina Virtual Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de administración del servicio, puede tener acceso a hello [documentación de referencia de API completa de hello Azure SDK de Python](http://azure-sdk-for-python.readthedocs.org/) y realizar complejo tareas fácilmente toomanage la aplicación de python.

Para obtener más información, vea hello [Centro para desarrolladores de Python](/develop/python/).

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
