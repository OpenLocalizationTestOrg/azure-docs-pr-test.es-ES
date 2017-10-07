---
title: las aplicaciones de PaaS aaaSecuring con almacenamiento de Azure | Documentos de Microsoft
description: " Obtenga información sobre los procedimientos recomendados de seguridad de Azure Storage para proteger aplicaciones web y móviles PaaS. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>Protección de aplicaciones web y móviles PaaS con Azure Storage
En este artículo se explican una serie de procedimientos recomendados de seguridad de Azure Storage para proteger aplicaciones web y móviles PaaS. Estas prácticas recomendadas se derivan de nuestra experiencia con Azure y experiencias de Hola de clientes como usted mismo.

Hola [Guía de seguridad de almacenamiento de Azure](../storage/common/storage-security-guide.md) es una excelente fuente para obtener información detallada sobre la seguridad y el almacenamiento de Azure.  Este artículo tratan en un nivel alto algunos de los conceptos de Hola que se encuentran en la Guía de seguridad de Hola y Guía de seguridad de toohello de vínculos, así como otros orígenes, para obtener más información.

## <a name="azure-storage"></a>Azure Storage
Azure hace posible almacenamiento toodeploy y el uso de maneras no fácilmente alcanzables en local. Gracias a Azure Storage, se pueden alcanzar altos niveles de escalabilidad y disponibilidad con relativamente poco esfuerzo. No sólo es foundation Hola de almacenamiento de Azure para Windows y máquinas virtuales Linux de Azure, también puede admitir aplicaciones distribuidas de gran tamaño.

El almacenamiento de Azure proporciona Hola siguientes cuatro servicios: almacenamiento de blobs, el almacenamiento de tabla, almacenamiento en la cola y el almacenamiento de archivos. más información, consulte toolearn [Introducción tooMicrosoft almacenamiento de Azure](../storage/storage-introduction.md).

## <a name="best-practices"></a>Prácticas recomendadas
Este artículo trata Hola seguir las prácticas recomendadas:

- Protección de acceso:
   - Firmas de acceso compartido (SAS)
   - Disco administrado
   - Control de acceso basado en rol (RBAC)

- Cifrado de almacenamiento:
   - Cifrado del lado cliente para datos de gran valor
   - Azure Disk Encryption para máquinas virtuales (VM)
   - Cifrado del servicio de almacenamiento

## <a name="access-protection"></a>Protección de acceso
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>Uso de la firma de acceso compartido en lugar de una clave de cuenta de almacenamiento

En una solución de IaaS, normalmente máquinas virtuales Linux o Windows en ejecución, los archivos están protegidos contra la divulgación y las amenazas de alteración a través de mecanismos de control de acceso. En Windows se usaría las [listas de control de acceso (ACL)](../virtual-network/virtual-networks-acl.md) y, en Linux, probablemente [chmod](https://en.wikipedia.org/wiki/Chmod). Básicamente, esto es exactamente lo que haría actualmente si estuviese protegiendo archivos de un servidor de su propio centro de datos.

Pero con PaaS es diferente. Uno de los archivos de toostore de maneras más comunes de hello en Microsoft Azure es toouse [almacenamiento de blobs de Azure](../storage/storage-dotnet-how-to-use-blobs.md). Una diferencia entre el almacenamiento de blobs y otro almacenamiento de archivo es Hola de E/S de archivos y los métodos de protección de Hola que vienen con E/S de archivos.

El control de acceso es fundamental. toohelp controlar acceso tooAzure almacenamiento, Hola sistema generará dos claves de cuenta de almacenamiento de 512 bits (SAKs) cuando se [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md). nivel de Hola de redundancia clave hace posible interrupción servicio tooavoid durante la rotación de claves de rutina.

Teclas de acceso de almacenamiento son secretos de prioridad alta y solo deben ser accesible toothose responsable de control de acceso de almacenamiento. Si equivocados Hola obtener acceso a claves de toothese, se tienen control total del almacenamiento y podría reemplazar, eliminar o agregar archivos toostorage. Por ejemplo, software malintencionado y otro tipo de contenido que puede poner en peligro a sus clientes u organización.

Necesitará un tooobjects de acceso de manera tooprovide en almacenamiento. acceso tooprovide más granular que puede aprovechar las ventajas de [firma de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Hola SAS permite que se tooshare objetos específicos en el almacenamiento para un intervalo de tiempo predefinido y con permisos específicos. Una firma de acceso compartido permite toodefine:

- intervalo de Hola durante qué hello es válida, incluidos la hora de expiración de Hola y la hora de inicio de hello SAS.
- permisos de Hello concedidos por hello SAS. Por ejemplo, una SAS en un blob puede conceder a un usuario a leer y escribir permisos toothat blob, pero no eliminar permisos.
- Una dirección IP opcional o intervalo de direcciones IP desde la que acepta el almacenamiento de Azure Hola SAS. Por ejemplo, puede especificar un intervalo de direcciones IP que pertenezcan tooyour organización. Esto proporciona otra medida de seguridad para su SAS.
- Protocolo de Hello en el cual el almacenamiento de Azure acepta Hola SAS. Puede usar este tooclients de acceso de parámetro opcional toorestrict mediante HTTPS.

SAS permite tooshare Hola contenido que quieras tooshare sin dar las claves de cuenta de almacenamiento. Usar SAS siempre en la aplicación es un tooshare de forma segura los recursos de almacenamiento sin poner en peligro sus claves de cuenta de almacenamiento.

más información, consulte toolearn [utilizando firmas de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). más información acerca de posible toomitigate los riesgos y las recomendaciones de toolearn esos riesgos, vea [de procedimientos recomendados al usar SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="use-managed-disks-for-vms"></a>Uso de discos administrados para máquinas virtuales

Cuando eliges [discos de Azure administrados](../storage/storage-managed-disks-overview.md), Azure administra las cuentas de almacenamiento de Hola que usas para los discos de máquina virtual. Todo lo que necesita toodo es elegir tipo de Hola de disco (Premium o estándar) y el tamaño de disco de hello; Almacenamiento de Azure realizará Hola rest. No es necesario tooworry acerca de los límites de escalabilidad que podrían haber requerido en caso contrario, las cuentas de almacenamiento de toomultiple tooyou.

más información, consulte toolearn [Frequently Asked Questions aproximadamente administrados y discos premium](../storage/storage-faq-for-disks.md).

### <a name="use-role-based-access-control"></a>Uso del control de acceso basado en rol

Anteriormente analizamos utilizando tooobjects de acceso de toogrant limitado de firma de acceso compartido (SAS) en los clientes de tooother cuenta de almacenamiento, sin exponer su clave de cuenta de almacenamiento de información de cuenta. A veces los riesgos de hello asociados con una operación determinada en su cuenta de almacenamiento superan a las ventajas de Hola de SAS. A veces resulta más fácil acceso toomanage de otras maneras.

Acceso a otra forma toomanage es toouse [Azure Role-Based el Control de acceso](../active-directory/role-based-access-control-what-is.md) (RBAC). Con RBAC, para centrarse en lo que proporciona los empleados que necesitan, los permisos exactos Hola basada en hello necesidad tooknow y principios de seguridad de privilegios mínimos. Demasiados permisos pueden exponer un tooattackers de cuenta. Si se conceden muy pocos, los empleados no podrán realizar su trabajo de manera eficaz. RBAC ayuda a abordar este problema, ya que es posible realizar una administración avanzada del acceso para Azure. Esto es necesario para las organizaciones que desean tooenforce las directivas de seguridad de acceso a datos.

Puede aprovechar las funciones integradas de RBAC en Azure tooassign privilegios toousers. Considere el uso de colaborador de la cuenta de almacenamiento para los operadores en la nube que necesitan cuentas de almacenamiento de toomanage y cuentas de almacenamiento clásicas de toomanage de rol de colaborador clásico de cuenta de almacenamiento. Para los operadores de nube que necesitan toomanage máquinas virtuales, pero no en red virtual Hola o toowhich de la cuenta de almacenamiento que están conectados, considere la posibilidad de adición de rol de colaborador de la máquina Virtual de toohello.

Es posible que las organizaciones que no apliquen el control de acceso a los datos mediante funcionalidades como RBAC estén concediendo más privilegios de los necesarios a sus usuarios. Esto puede provocar toodata riesgo al permitir que algunos toodata de acceso de los usuarios que no deberían tener en primer lugar en Hola.

toolearn que más información sobre RBAC vea:

- [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md)
- [Roles integrados para el control de acceso basado en rol de Azure](../active-directory/role-based-access-built-in-roles.md)
- [Guía de seguridad de almacenamiento de Azure](../storage/common/storage-security-guide.md) para obtener detalles sobre cómo toosecure su cuenta de almacenamiento, con RBAC

## <a name="storage-encryption"></a>Cifrado de almacenamiento
### <a name="use-client-side-encryption-for-high-value-data"></a>Uso del cifrado del lado cliente para datos de gran valor

Habilita el cifrado en el cliente tooprogrammatically se cifran datos en tránsito antes de cargar tooAzure almacenamiento y descifrar mediante programación los datos cuando se recuperan desde el almacenamiento.  De este modo, se cifran tanto los datos en tránsito como los que están en reposo.  Cifrado en el cliente es el método más seguro de Hola de cifrar los datos pero requieren la aplicación de tooyour de toomake cambios mediante programación y coloque los procesos de administración de claves en su lugar.

Cifrado en el cliente también le permite toohave control exclusivo sobre las claves de cifrado.  Puede generar y administrar sus propias claves de cifrado.  Cifrado en el cliente utiliza una técnica de envoltura donde hello biblioteca de cliente de almacenamiento de Azure genera una contenido clave de cifrado (CEK) que, a continuación, se ajusta (cifrada) con clave de cifrado de claves de Hola (de claves KEK). Hello KEK se identifica mediante un identificador de clave y puede ser un par de claves asimétricas o una clave simétrica y se puede administrar de forma local o almacenado en [el almacén de claves de Azure](../key-vault/key-vault-whatis.md).

Cifrado en el cliente se integra en bibliotecas de cliente de almacenamiento de .NET de Hola y Hola Java.  Consulte [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](../storage/storage-client-side-encryption.md) para obtener información sobre cómo cifrar los datos en las aplicaciones cliente, y generar y administrar claves de cifrado.

### <a name="azure-disk-encryption-for-vms"></a>Azure Disk Encryption para máquinas virtuales
Azure Disk Encryption es una funcionalidad que permite cifrar los discos de las máquinas virtuales IaaS con Windows y Linux. Cifrado del disco Azure aprovecha característica BitLocker Hola sector estándar de Windows y la característica de DM Crypt de Hola de cifrado del volumen de tooprovide de Linux para hello OS y discos de datos de Hola. solución de Hola se integra con el almacén de claves de Azure toohelp controlar y administrar claves de cifrado del disco de Hola y secretos en su suscripción de almacén de claves. solución de Hello también garantiza que todos los datos en discos de máquina virtual de Hola se cifran en reposo en el almacenamiento de Azure.

Consulte [Azure Disk Encryption para máquinas virtuales IaaS Linux y Windows](azure-security-disk-encryption.md).

### <a name="storage-service-encryption"></a>Cifrado del servicio de almacenamiento
Cuando [cifrado del servicio de almacenamiento](../storage/storage-service-encryption.md) para almacenamiento de archivos está habilitado, los datos de Hola se cifran automáticamente con el cifrado AES-256. Microsoft encarga de todos los Hola cifrado, descifrado y administración de claves. Esta característica está disponible en los tipos de redundancia LRS y GRS.

## <a name="next-steps"></a>Pasos siguientes
En este artículo se introdujo tooa colección de prácticas recomendadas de seguridad de almacenamiento de Azure para proteger su PaaS aplicaciones web y móviles. toolearn más acerca de cómo proteger las implementaciones de PaaS, vea:

- [Protección de implementaciones de PaaS](security-paas-deployments.md)
- [Protección de aplicaciones web y móviles PaaS con Azure App Services](security-paas-applications-using-app-services.md)
- [Protección de bases de datos PaaS en Azure](security-paas-applications-using-sql.md)
