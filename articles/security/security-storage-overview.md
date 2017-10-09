---
title: "características de aaaSecurity que pueden utilizarse con el almacenamiento de Azure | Documentos de Microsoft"
description: " Este artículo proporciona información general de características de seguridad de Azure de hello básicas que puede usarse con el almacenamiento de Azure. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Información general sobre seguridad de Azure Storage
Almacenamiento de Azure es la solución de almacenamiento de hello en la nube para aplicaciones modernas que se basan en las necesidades de escalabilidad toomeet Hola de sus clientes, la disponibilidad y la durabilidad. Azure Storage proporciona un conjunto completo de funcionalidades de seguridad:

* cuenta de almacenamiento de Hola se puede proteger mediante el Control de acceso basado en roles y Azure Active Directory.
* Los datos se pueden proteger en tránsito entre una aplicación y Azure usando cifrado de cliente, HTTPS o SMB 3.0.
* Se pueden establecer datos toobe cifrada automáticamente cuando escribe tooAzure con cifrado de almacenamiento del servicio de almacenamiento.
* Discos de sistema operativo y los datos utilizados por máquinas virtuales se pueden establecer toobe cifrada mediante el cifrado de disco de Azure.
* Se pueden conceder acceso delegado toohello objetos de datos en el almacenamiento de Azure mediante firmas de acceso compartido.
* método de autenticación de Hello usado por alguien cuando tienen acceso a almacenamiento puede realizar el seguimiento mediante el análisis de almacenamiento.

Para obtener una visión más detallada de seguridad en el almacenamiento de Azure, vea hello [Guía de seguridad de almacenamiento de Azure](../storage/common/storage-security-guide.md). Esta guía proporciona profundización en las características de seguridad de hello del almacenamiento de Azure como claves de cuenta de almacenamiento, cifrado de datos en tránsito y en rest y análisis de almacenamiento.

Este artículo ofrece una visión general de las características de seguridad de Azure que se pueden usar con Azure Storage. Se proporcionan vínculos tooarticles que proporcionan detalles de cada característica, por lo que puede obtener más información.

A continuación, incluimos Hola core características toobe tratado en este artículo:

* Control de acceso basado en roles
* Acceso delegado toostorage objetos
* Cifrado en tránsito
* Cifrado en reposo/Cifrado del servicio de Almacenamiento
* Azure Disk Encryption
* Azure Key Vault

## <a name="role-based-access-control-rbac"></a>Control de acceso basado en rol (RBAC)
Puede proteger su cuenta de almacenamiento con el control de acceso basado en rol (RBAC). Restringir el acceso en función de hello [necesita tooknow](https://en.wikipedia.org/wiki/Need_to_know) y [privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principios de seguridad es fundamental para las organizaciones que desean tooenforce las directivas de seguridad de acceso a datos. Estos derechos de acceso se conceden mediante la asignación de hello adecuado RBAC rol toogroups y las aplicaciones en un ámbito determinado. Puede usar [funciones integradas de RBAC](../active-directory/role-based-access-built-in-roles.md), como colaborador de la cuenta de almacenamiento, tooassign privilegios toousers.

Más información:

* [Control de acceso basado en roles de Azure Active Directory](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>Acceso delegado toostorage objetos
Una firma de acceso compartido (SAS) proporciona acceso delegado tooresources en su cuenta de almacenamiento. Hola SAS significa que puede conceder a que un cliente están limitadas tooobjects permisos en su cuenta de almacenamiento durante un periodo de tiempo y con un conjunto de permisos especificado. Puede conceder estos permisos limitados sin necesidad de tooshare las claves de acceso de cuenta. Hola SAS es un URI que abarca el proceso en sus parámetros de consulta toda la información de hello necesaria para el recurso de almacenamiento de tooa de acceso autenticado. recursos de almacenamiento de tooaccess con hello SAS, cliente hello solo necesita tooprovide Hola SAS toohello adecuado constructor o un método.

Más información:

* [Modelo de descripción Hola SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Firmas de acceso compartido, Parte 2: Creación y uso de una SAS con Blob Storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Cifrado en tránsito
Cifrado en tránsito es un mecanismo para proteger datos cuando se transmiten a través de redes. Con Azure Storage, puede proteger los datos mediante:

* [Cifrado de nivel de transporte](../storage/common/storage-security-guide.md#encryption-in-transit), como HTTPS para transferir datos a Azure Storage o desde este servicio.
* [Cifrado en el cable](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), como el cifrado SMB 3.0 para recursos compartidos de Azure File.
* [Cifrado en el cliente](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), datos de hello tooencrypt antes de transferirse a almacenamiento y toodecrypt datos de hello después de que se transfiere fuera de almacenamiento.

Más información acerca del cifrado de cliente:

* [Cifrado del lado cliente para el Almacenamiento de Microsoft Azure (vista previa)](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Cloud security controls series: Encrypting Data in Transit (Serie de controles de seguridad en la nube: cifrado de datos en tránsito)](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Cifrado en reposo
Para muchas organizaciones, el [cifrado de los datos en reposo](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) es un paso obligatorio en lo que respecta a la privacidad de los datos, el cumplimiento y la soberanía de los datos. Hay tres características de Azure que proporcionan cifrado de datos "en reposo":

* [Cifrado de almacenamiento del servicio](../storage/common/storage-security-guide.md#encryption-at-rest) permite que el servicio de almacenamiento de hello cifrar automáticamente los datos al escribir tooAzure almacenamiento de toorequest.
* [Cifrado en el cliente](../storage/common/storage-security-guide.md#client-side-encryption) también proporciona características de Hola de cifrado en reposo.
* [Cifrado del disco Azure](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) permite tooencrypt discos de hello OS y discos de datos usados por una máquina virtual de IaaS.

Más información acerca del Cifrado de servicio de almacenamiento:

* [Cifrado del servicio Azure Storage](https://azure.microsoft.com/services/storage/) está disponible para [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/). Para más información sobre otros tipos de almacenamiento de Azure, consulte [File Storage](https://azure.microsoft.com/services/storage/files/), [Premium Storage (disco)](https://azure.microsoft.com/services/storage/premium-storage/), [Table Storage](https://azure.microsoft.com/services/storage/tables/) y [Queue Storage](https://azure.microsoft.com/services/storage/queues/).
* [Cifrado del servicio Azure Storage para datos en reposo (versión preliminar)](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Azure Disk Encryption
Azure Disk Encryption para máquinas virtuales (VM) le ayuda a solucionar los aspectos de seguridad y cumplimiento normativo de su organización, ya que cifra los discos de las máquinas virtuales (incluidos los discos de arranque y de datos) con claves y directivas que usted controla en [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

Cifrado de discos para máquinas virtuales funciona en sistemas operativos Linux y Windows. También utiliza el almacén de claves toohelp proteger, administrar y auditar el uso de las claves de cifrado de disco. Todos los datos de hello en los discos de máquina virtual se cifran en reposo mediante la tecnología de cifrado estándar del sector de las cuentas de almacenamiento de Azure. Hola soluciones de cifrado del disco para Windows se basa en [el cifrado de unidad BitLocker de Microsoft](https://technet.microsoft.com/library/cc732774.aspx), y Hola solución Linux se basa en [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Más información:

* [Azure Disk Encryption for Windows and Linux Azure Virtual Machines (Azure Disk Encryption para máquinas virtuales IaaS de Linux y Windows)](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Azure Key Vault
Cifrado de disco de Azure usa [el almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/) toohelp controlar y administrar claves de cifrado de disco y secretos en su suscripción de almacén de claves, asegurándose de que todos los datos en discos de máquina virtual de Hola se cifran en reposo en Azure Almacenamiento de información. Debe usar las claves de tooaudit del almacén de claves y el uso de directivas.

Más información:

* [¿Qué es el Almacén de claves de Azure?](../key-vault/key-vault-whatis.md)
* [Introducción al Almacén de claves de Azure](../key-vault/key-vault-get-started.md)
