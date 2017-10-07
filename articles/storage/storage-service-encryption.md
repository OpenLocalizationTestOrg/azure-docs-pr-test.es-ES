---
title: Cifrado del servicio de almacenamiento de datos en reposo aaaAzure | Documentos de Microsoft
description: "Use Hola cifrado del servicio de almacenamiento de Azure característica tooencrypt el almacenamiento de blobs de Azure en el lado del servicio de hello al almacenar los datos de Hola y descifrarlo cuando se recuperan datos de Hola."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 304f1c21200f86f2084ce98788b2fc7ca893d1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>Cifrado del servicio Almacenamiento de Azure para datos en reposo (versión preliminar)
Cifrado de servicio de almacenamiento de Azure (SSE) para los datos en reposo le ayuda a proteger y proteger su toomeet de datos de la seguridad de la organización y los compromisos de cumplimiento de normas. Con esta característica, el almacenamiento de Azure cifra su toostorage toopersisting anteriores de datos automáticamente y descifra tooretrieval anterior. Hola cifrado, descifrado y administración de claves son toousers totalmente transparente.

Hello secciones siguientes proporcionan instrucciones detalladas sobre cómo admite las características de cifrado de servicio de almacenamiento de toouse hello, así como Hola escenarios y las experiencias de usuario.

## <a name="overview"></a>Información general
Almacenamiento de Azure proporciona un conjunto completo de capacidades de seguridad que juntos permiten a los desarrolladores de aplicaciones seguras toobuild. Los datos se pueden proteger en tránsito entre una aplicación y Azure usando [cifrado de cliente](storage-client-side-encryption.md), HTTPs o SMB 3.0. El cifrado del servicio de almacenamiento proporciona cifrado en reposo, una administración de claves, cifrado y descifrado de manera completamente transparente. Todos los datos se cifran con 256 bits [el cifrado AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), uno de bloque más fuerte Hola cifrados disponibles.

SSE funciona mediante el cifrado de datos de hello cuando se escribe tooAzure almacenamiento y puede utilizarse para almacenamiento de blobs de Azure y almacenamiento de archivos. Funciona para siguiente hello:

* Almacenamiento estándar: cuentas de almacenamiento de uso general para Blob Storage y File Storage y cuentas de Blob Storage
* Premium Storage 
* Todos los niveles de redundancia (LRS, ZRS, GRS y RA-GRS)
* Cuentas de almacenamiento de Azure Resource Manager (pero no el clásico) 
* Todas las regiones.

toolearn más información, consulte toohello preguntas más frecuentes.

tooenable o deshabilitar el cifrado del servicio de almacenamiento para una cuenta de almacenamiento, inicie sesión en hello [portal de Azure](https://portal.azure.com) y seleccione una cuenta de almacenamiento. En la hoja de configuración de hello, busque Hola sección servicio Blob como se muestra en esta captura de pantalla y haga clic en el cifrado.

![Captura de pantalla del portal que muestra la opción de cifrado](./media/storage-service-encryption/image1.png)
<br/>*Ilustración 1: Habilitar SSE en Blob service (paso 1)*

![Captura de pantalla del Portal que muestra la opción de cifrado](./media/storage-service-encryption/image3.png)
<br/>*Ilustración 2: Habilitar SSE en servicio de archivo (paso 1)*

Tras hacer clic en configuración de cifrado de hello, puede habilitar o deshabilitar el cifrado del servicio de almacenamiento.

![Captura de pantalla del Portal que muestra las propiedades de cifrado](./media/storage-service-encryption/image2.png)
<br/>*Ilustración 3: Habilitar SSE en Blob y File Service (paso 2)*

## <a name="encryption-scenarios"></a>Escenarios de cifrado
Cifrado del servicio de Almacenamiento se puede habilitar en el nivel de la cuenta de almacenamiento. Una vez habilitada, los clientes elegir qué tooencrypt de servicios. Admite Hola cliente los escenarios siguientes:

* Cifrado de Blob Storage y File Storage en cuentas de Resource Manager.
* Cifrado de Blob y servicio de archivos en las cuentas de almacenamiento clásico una vez había migrado las cuentas de almacenamiento de administrador de tooResource.

SSE tiene Hola siguientes limitaciones:

* No se admite el cifrado de cuentas de almacenamiento clásico.
* Los datos existentes - SSE solo cifran los datos recién creadas después de que está habilitado el cifrado de Hola. Si por ejemplo crear una nueva cuenta de almacenamiento de administrador de recursos, pero no activar el cifrado y, a continuación, cargar blobs o archivado cuenta de almacenamiento de toothat de discos duros virtuales y, a continuación, activar SSE, no se cifrarán los blobs a menos que se copian o volver a escribir.
* Compatibilidad de Marketplace: habilitar el cifrado de las máquinas virtuales creado a partir de Hola Marketplace mediante hello [portal de Azure](https://portal.azure.com), PowerShell y la CLI de Azure. imagen base del disco duro virtual de Hello permanecerá sin cifrar; Sin embargo, se cifrarán las escrituras realizadas después de que se active Hola VM.
* Los datos de la tabla y de las colas no se cifrarán.

## <a name="getting-started"></a>Introducción
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Paso 1: [Crear una cuenta de almacenamiento nueva](storage-create-storage-account.md).
### <a name="step-2-enable-encryption"></a>Paso 2: Habilitar el cifrado.
Puede habilitar el cifrado mediante hello [portal de Azure](https://portal.azure.com).

> [!NOTE]
> Si desea que tooprogrammatically habilitar o deshabilitar Hola cifrado del servicio de almacenamiento en una cuenta de almacenamiento, puede usar hello [API de REST de proveedor de recursos de almacenamiento de Azure](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [biblioteca de cliente del proveedor de recursos de almacenamiento para .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), o hello [CLI de Azure](storage-azure-cli.md).
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>Paso 3: Copia de cuentas de toostorage de datos
Si habilita SSE para hello servicio Blob, se cifrarán todos los blobs escritos toothat cuenta de almacenamiento. No se cifrarán los blobs que ya se encuentren en esa cuenta de almacenamiento hasta que se vuelvan a escribir. Puede copiar datos de Hola de tooone de almacenamiento de una cuenta con SSE cifrado, o incluso habilitar SSE y copiar blobs de Hola desde un contenedor tooanother toosure cifrado de los datos anteriores. Puede usar cualquiera de hello después herramientas tooaccomplish esto. Esto es Hola mismo comportamiento para el almacenamiento de archivo también.

#### <a name="using-azcopy"></a>Uso de AzCopy
AzCopy es una utilidad de línea de comandos de Windows diseñada para copiar datos tooand de almacenamiento de blobs de Microsoft Azure, el archivo y la tabla mediante comandos sencillos con un rendimiento óptimo. Puede usar este toocopy los blobs o archivos desde un tooanother de cuenta de almacenamiento que tiene SSE habilitado. 

toolearn más información, visite [transferir datos con la utilidad de línea de comandos de AzCopy hello](storage-use-azcopy.md).

#### <a name="using-smb"></a>Uso de SMB
Almacenamiento de archivos de Azure ofrece recursos compartidos de archivos en la nube de hello mediante el protocolo SMB estándar de Hola. Un recurso compartido de archivos se puede montar desde un cliente local o en Azure. Una vez montado, herramientas, como Robocopy pueden ser archivos usados toocopy sobre tooAzure que uso compartido de archivos. Para obtener más información, consulte [cómo toomount Azure recurso compartido de archivos en Windows](storage-file-how-to-use-files-windows.md) y [cómo compartir toomount archivos de Azure en Linux](storage-how-to-use-files-linux.md).


#### <a name="using-hello-storage-client-libraries"></a>Uso de bibliotecas de cliente de almacenamiento de Hola
Puede copiar blob o el archivo tooand de datos desde almacenamiento de blobs o entre cuentas de almacenamiento mediante nuestro amplio conjunto de bibliotecas de cliente de almacenamiento incluido. NET, C++, Java, Android, Node.js, PHP, Python y Ruby.

toolearn más información, visite nuestro [Introducción al almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md).

#### <a name="using-a-storage-explorer"></a>Uso de un explorador de almacenamiento
Puede usar una cuenta de almacenamiento de toocreate de explorador de almacenamiento, cargar y descargar datos, ver contenido de blobs y navegar por los directorios. Puede usar una de estas cuentas de almacenamiento tooupload tooyour de blobs con el cifrado habilitado. Con algunos exploradores de almacenamiento, también puede copiar datos de existente tooa otro contenedor de almacenamiento blob de cuenta de almacenamiento de Hola o una cuenta de almacenamiento que tenga habilitado de SSE.

toolearn más información, visite [exploradores de almacenamiento de Azure](storage-explorers.md).

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>Paso 4: Consultar el estado del programa Hola Hola de datos cifrados
Se ha implementado una versión actualizada de las bibliotecas de cliente de almacenamiento de Hola que le permite tooquery estado de Hola de un objeto toodetermine si está cifrada o no. Actualmente solo está disponible para Blob Storage. Compatibilidad con el almacenamiento de archivo se encuentra en la guía básica de Hola. 

Hola mientras tanto, puede llamar a [obtener propiedades de la cuenta](https://msdn.microsoft.com/library/azure/mt163553.aspx) tooverify que Hola cuenta de almacenamiento tiene habilitado el cifrado o la vista Hola propiedades de la cuenta de almacenamiento en hello portal de Azure.

## <a name="encryption-and-decryption-workflow"></a>Flujo de trabajo del cifrado y el descifrado
Esta es una breve descripción del flujo de trabajo de cifrado y descifrado de hello:

* cliente de Hello habilita el cifrado en la cuenta de almacenamiento de Hola.
* Cuando el cliente de Hola escribe nuevo tooBlob de datos (PUT Blob, coloque el bloque, PUT Page, colocar archivos etc.) o el almacenamiento de archivos; cada escritura se cifra con 256 bits [el cifrado AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), uno de bloque más fuerte Hola cifrados disponibles.
* Cuando cliente hello necesita que los datos de tooaccess (GET Blob, etc.), los datos se descifra automáticamente antes de devolver el usuario toohello.
* Si el cifrado está deshabilitado, nuevas escrituras ya no están cifradas y los datos cifrados permanecen cifrados hasta reescrito por usuario de Hola. Mientras está habilitado el cifrado, escribe tooBlob o almacenamiento de archivos se cifrarán. estado de Hola de datos no cambia con usuario Hola alternar entre la habilitación o deshabilitación del cifrado para la cuenta de almacenamiento de Hola.
* Microsoft almacena, cifra y administra todas las claves de cifrado.

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Preguntas más frecuentes acerca de Cifrado del servicio de Almacenamiento para datos en reposo
**P: Ya tengo una cuenta de almacenamiento clásico. ¿Puedo habilitar SSE en ella?**

R: No. SSE solo es compatible con las cuentas de almacenamiento de Resource Manager.

**P: ¿Cómo puedo cifrar datos en mi cuenta de almacenamiento clásico?**

R: puede crear una nueva cuenta de almacenamiento de administrador de recursos y copiar los datos mediante [AzCopy](storage-use-azcopy.md) de la cuenta de almacenamiento clásico existente tooyour recién creado cuenta de almacenamiento de administrador de recursos. 

Si va a migrar su tooa de cuenta de almacenamiento clásicas cuenta de almacenamiento de administrador de recursos, esta operación es instantánea, se cambia el tipo de saludo de la cuenta, pero no afecta a los datos existentes. Se cifrarán todos los datos nuevos escritos después de habilitar el cifrado. Para obtener más información, consulte [admite la migración de IaaS recursos de la plataforma de clásico tooResource Manager](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/). Tenga en cuenta que esto solo es compatible con Blob y File Service.

**P: Ya tengo una cuenta de almacenamiento de Resource Manager. ¿Puedo habilitar SSE en ella?**

R: Sí, pero solo se cifrarán los datos recién escritos. No vuelve atrás y cifra datos que ya estaban presentes. Esto no se admite todavía para hello vista previa del archivo de almacenamiento.

**P: ¿Me gustaría datos actuales de hello tooencrypt en una cuenta de almacenamiento de administrador de recursos existente?**

R: Puede habilitar SSE en cualquier momento en una cuenta de almacenamiento de Resource Manager. Sin embargo, no se cifrarán los datos que ya estaban presentes. tooencrypt los datos existentes, puede copiarlos tooanother nombre o en otro contenedor y, a continuación, quitará las versiones de hello sin cifrar.

**P: Uso Premium Storage. ¿Puedo usar SSE?**

R: Sí, SSE es compatible tanto con el almacenamiento estándar como con el Almacenamiento premium.  Almacenamiento Premium no se admite para hello servicio de archivos.

**P: Si creo una cuenta de almacenamiento nueva, habilito SSE y, luego, creo una VM nueva con esa cuenta de almacenamiento, ¿la VM queda cifrada?**

R: Sí. Los discos creados que usan la nueva cuenta de almacenamiento Hola se cifrarán, siempre y cuando se crean después de habilita SSE. Si va a permanecer sin cifrar; Hola que máquina virtual se creó utilizando el contexto de mercado de Azure, imagen base del disco duro virtual de Hola Sin embargo, se cifrarán las escrituras realizadas después de que se active Hola VM.

**P: ¿Puedo crear cuentas de almacenamiento con SSE habilitado a través de Azure PowerShell y la CLI de Azure?**

R: Sí.

**P: ¿El costo de Almacenamiento de Azure sube si se habilita SSE?**

R: No hay costo adicional.

**P: ¿a quién administra las claves de cifrado de hello?**

R: Microsoft administra las claves de Hola.

**P: ¿Puedo usar mis propias claves de cifrado?**

R: estamos trabajando en ofrece capacidades de los clientes toobring sus propias claves de cifrado.

**P: ¿puedo revocar el acceso a claves de cifrado de toohello?**

R: no en este momento; las claves de Hello están totalmente administradas por Microsoft.

**P: ¿SSE está habilitado de manera predeterminada cuando creo una cuenta de almacenamiento?**

R: SSE no está habilitado de forma predeterminada; Puede usar hello tooenable de portal de Azure. Mediante programación, puede habilitar esta característica con hello API de REST de proveedor de recursos de almacenamiento.

**P: ¿Qué diferencia tiene con Azure Disk Encryption?**

R: esta característica es tooencrypt usa datos en el almacenamiento de blobs de Azure. Hola cifrado del disco de Azure es discos de sistema operativo y datos tooencrypt usado en las máquinas virtuales IaaS. Para obtener más detalles, visite nuestra [Guía de seguridad para almacenamiento](storage-security-guide.md).

**P: ¿qué ocurre si habilito SSE y, a continuación, ir en y habilitar el cifrado de disco de Azure en discos de hello?**

R: Funcionará sin problemas. Ambos métodos cifrarán los datos.

**P: ¿Mi cuenta de almacenamiento se configura toobe replicada geográfica innecesariamente. Si habilito SSE, ¿también se cifrará la copia redundante?**

R: Sí, se cifran todas las copias de la cuenta de almacenamiento de Hola y todas las opciones de redundancia: almacenamiento redundante local (LRS), almacenamiento de redundancia de zona (ZRS), almacenamiento con redundancia geográfica (GRS) y almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS): se admiten.

**P: No puedo habilitar el cifrado en mi cuenta de almacenamiento.**

R: ¿Es una cuenta de almacenamiento de Resource Manager? Las cuentas de almacenamiento clásico no son compatibles. 

**P: ¿SSE solo se permite en regiones específicas?**

R: Hola SSE está disponible en todas las regiones de almacenamiento de blobs. Compruebe si Hola sección de disponibilidad para el almacenamiento de archivo. 

**P: ¿cómo póngase en contacto con alguien si tiene algún problema o desea tooprovide comentarios?**

R: póngase en contacto con [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) para ver los problemas relacionados con tooStorage cifrado del servicio.

## <a name="next-steps"></a>Pasos siguientes
Almacenamiento de Azure proporciona un conjunto completo de capacidades de seguridad que juntos permiten a los desarrolladores de aplicaciones seguras toobuild. Para obtener más detalles, visite hello [Guía de seguridad de almacenamiento](storage-security-guide.md).

