---
title: "Preguntas más frecuentes sobre el cifrado de disco aaaAzure | Documentos de Microsoft"
description: "Este artículo ofrecen respuestas toofrequently pregunta para Microsoft Azure disco cifrado para Windows y las máquinas virtuales de IaaS de Linux."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Preguntas frecuentes sobre Azure Disk Encryption (P+F)

En este artículo se responde a las preguntas más frecuentes sobre Azure Disk Encryption para las máquinas virtuales IaaS con Windows o Linux; para más información acerca de este servicio, lea [Azure Disk Encryption para máquinas virtuales IaaS con Windows o Linux](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Preguntas generales
**P.** ¿En qué región tiene disponibilidad general Azure Disk Encryption?

**R:** Azure Disk Encryption para máquinas virtuales IaaS Windows y Linux tiene disponibilidad general en todas las regiones públicas de Azure.

**P:** ¿Qué experiencias del usuario están disponibles con Azure Disk Encryption?

**R:** La disponibilidad general de Azure Disk Encryption admite plantillas de Azure Resource Manager, Azure PowerShell y CLI de Azure. Esto ofrece mucha flexibilidad, ya que dispone de tres opciones distintas para habilitar el cifrado de disco para las máquinas virtuales IaaS. Obtener más detalles sobre la experiencia del usuario de Hola y las instrucciones paso a paso está disponible en escenarios de implementación de cifrado del disco de Azure de Hola y experiencias.

**P:** ¿Cuánto cuesta Azure Disk Encryption?

**R:** El cifrado de discos de máquinas virtuales con Azure Disk Encryption no supone un cargo adicional.

**P:** ¿Qué niveles de máquina virtual se pueden usar con Azure Disk Encryption?

**R:** Azure Disk Encryption solo está disponible en máquinas virtuales de nivel estándar, como son [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) y máquinas virtuales IaaS de series sucesivas, incluidas las que tienen Premium Storage. No está disponible en las máquinas virtuales de nivel básico.

**P:** ¿Qué distribuciones de Linux son compatibles con Azure Disk Encryption?

**R:** cifrado de disco de Azure es compatible con hello siguiendo las distribuciones de Linux server y las versiones:

| Distribución de Linux | Versión | Tipo de volumen compatible con el cifrado|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | Sistema operativo y disco de datos |
| Ubuntu | 14.04.5-DAILY-LTS | Sistema operativo y disco de datos |
| RHEL | 7.3 | Sistema operativo y disco de datos |
| RHEL | 7,2 | Sistema operativo y disco de datos |
| RHEL | 6,8 | Sistema operativo y disco de datos |
| RHEL | 6.7 | Disco de datos |
| CentOS | 7.3 | Sistema operativo y disco de datos |
| CentOS | 7.2n | Sistema operativo y disco de datos |
| CentOS | 6,8 | Sistema operativo y disco de datos |
| CentOS | 7.1 | Disco de datos |
| CentOS | 7.0 | Disco de datos |
| CentOS | 6.7 | Disco de datos |
| CentOS | 6.6 | Disco de datos |
| CentOS | 6.5 | Disco de datos |
| openSUSE | 13.2 | Disco de datos |
| SLES | 12 SP1 | Disco de datos |
| SLES | Priority:12-SP1 | Disco de datos |
| SLES | HPC 12 | Disco de datos |
| SLES | Priority:11-SP4 | Disco de datos |
| SLES | 11 SP4 | Disco de datos |

**P:** ¿Cómo puedo empezar a usar Azure Disk Encryption?

**R:** los clientes pueden aprender cómo tooget iniciada por lectura Hola notas del producto cifrado del disco de Azure ubicados [aquí](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**P:** ¿Puedo cifrar los volúmenes de datos y arranque con Azure Disk Encryption?

**R:** Sí, puede cifrar los volúmenes de datos y de arranque para las máquinas virtuales IaaS de Windows y Linux. Para máquinas virtuales de Windows, no se puede cifrar los datos de hello sin primera encrpting Hola volumen del sistema operativo. Para máquinas virtuales de Linux, puede cifrar el volumen de datos de hello sin encryptinng Hola volumen del sistema operativo en primer lugar. Una vez que haya cifrado volumen Hola OS para Liux, no se admite la deshabilitación del cifrado en un volumen del sistema operativo para las máquinas virtuales de IaaS de Linux

**P:** ¿Permite Azure Disk Encryption habilitar la funcionalidad "traiga su propia clave" (BYOK)?

**R:** Sí, puede proporcionar sus propias claves de cifrado de claves. Dichas claves están protegidas en el almacén de claves de Azure, que es el almacén de claves de hello para el cifrado de disco de Azure. Para obtener más detalles sobre la clave de cifrado de claves de hello, admitir escenarios, consulte experiencias y escenarios de implementación de hello cifrado del disco de Azure

**P:** ¿Puedo usar una clave de cifrado de claves creada en Azure?

**R:** Sí, puede usar la clave de cifrado de claves toogenerate de almacén de Azure para su uso de cifrado de disco de Azure. Dichas claves están protegidas en el almacén de claves de Azure, que es el almacén de claves de hello para el cifrado de disco de Azure. Para obtener más detalles sobre la clave de cifrado de claves de hello, admitir escenarios, consulte experiencias y escenarios de implementación de hello cifrado del disco de Azure

**P: ¿** ¿puedo usar claves de cifrado local administración de claves toosafeguard de servicio/HSM Hola?

**R:** no se puede utilizar claves de cifrado de la Hola de servicio/HSM toosafeguard de hello local administración de claves con cifrado de disco de Azure. Sólo se pueden utilizar claves de cifrado de Hola de toosafeguard servicio de almacén de claves de Azure de Hola. Para obtener más detalles sobre la clave de cifrado de claves de hello, admitir escenarios, consulte experiencias y escenarios de implementación de hello cifrado del disco de Azure

**P: ¿** ¿qué cifrado de disco de Azure de tooconfigure de requisitos previos de hello?

**R:** hello Azure disco cifrado requisitos previos PowerShell toocreate AAD aplicación de script, cree el nuevo almacén de claves o almacén de claves existente para cifrado acceso tooenable cifrado y proteger secretos del disco y la clave de la instalación.  Para obtener más detalles sobre la clave de cifrado de claves de hello, admitir escenarios, consulte los requisitos previos de hello cifrado del disco de Azure y escenarios de implementación y las experiencias

**P: ¿** ¿dónde puedo obtener más información acerca de cómo toouse PowerShell para configurar el cifrado de disco de Azure?

**R:** Tenemos algunos artículos excelentes sobre cómo realizar tareas básicas de Azure Disk Encryption, así como escenarios más avanzados. Para las tareas básicas de Hola, eche un vistazo explorar [cifrado del disco de Azure con PowerShell de Azure, parte 1](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Para escenarios más avanzados, consulte [Azure Disk Encryption con Azure PowerShell, parte 2](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/).

**P:** ¿Qué versión de Azure PowerShell es compatible con Azure Disk Encryption?

**R:** usar versión más reciente de Hola de SDK de Azure PowerShell versión tooconfigure cifrado del disco de Azure. Descargar la versión más reciente de Hola de [Azure PowerShell](https://github.com/Azure/azure-powershell/releases). La versión 1.1.0 del SDK de Azure no admite Azure Disk Encryption.

> [!NOTE]
> Hola extensión de vista previa de cifrado de disco de Linux Azure está en desuso. Para obtener más información, consulte toodocumentation [aquí](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**P:** ¿Puedo aplicar Azure Disk Encryption en mi imagen personalizada de Linux?

**R:** No puede aplicar Azure Disk Encryption a una imagen personalizada de Linux. Se admiten imágenes de Linux de la Galería de hello sola para distribuciones de hello admitida mencionadas anteriormente. Actualmente no se admiten imágenes personalizadas de Linux.

**P: ¿** puedo aplicar actualizaciones tooa VM de Linux Red Hat utilizando Yum update?

**R:** Sí, puede realizar la actualización y aplicar una revisión a una máquina virtual Red Hat de Linux siguiendo los consejos que se documentan [aquí](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/).

**P: ¿** dónde puedo ir tooask pregunta o enviar comentarios

**R:** puede proporcionar preguntar preguntas o comentarios en el foro de cifrado de disco de Azure de hello [aquí](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Otras referencias
En este documento, aprendió a más hello más frecuentes preguntas relacionadas tooAzure cifrado del disco, para obtener más información acerca de este servicio y su capacidad de leer:

- [Aplicación de cifrado de discos en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Cifrado de una máquina virtual de Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Cifrado en reposo de datos de Azure](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
