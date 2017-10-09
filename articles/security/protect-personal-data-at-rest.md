---
title: "aaaAzure protección de datos personales en reposo con el cifrado | Documentos de Microsoft"
description: "Este artículo forma parte de una serie que ayudan a usar datos personales tooprotect de Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Tecnologías de cifrado de Azure: protección de datos personales en reposo con cifrado

En este artículo le ayuda a comprender y usar datos de toosecure de tecnologías de Azure cifrado en reposo.

El cifrado de datos en reposo es esencial como una mejor práctica tooprotect información personal o confidencial de datos y cumplimiento de normas de toomeet y requisitos de privacidad de datos.
El cifrado en reposo es atacante de hello tooprevent diseñada tengan acceso a datos de hello sin cifrar asegurándose de hello datos se cifran en el disco.

## <a name="scenario"></a>Escenario 

Una empresa cruise grandes, con sede en Estados Unidos, Hola está ampliando sus itinerarios toooffer de operaciones en hello Mediterráneo y Mar Báltico, así como Hola británicas. toosupport los esfuerzos, ha adquirido varias líneas cruise más pequeñas con sede en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido

la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola. Esto puede incluir empleado o la información de cliente, como:

- direcciones
- números de teléfono
- números de identificación fiscal
- Información médica
- información de tarjeta de crédito

empresa Hola debe proteger la privacidad de Hola de datos de clientes y empleados asegurándose de departamentos de toothose accesible de datos que lo necesiten. (por ejemplo, los departamentos de nóminas y reservas).

línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad que incluye información personal tootrack relaciones con los clientes actuales y pasados.

### <a name="problem-statement"></a>Declaración del problema

empresa Hola debe proteger la privacidad de Hola de datos personales de los empleados y los clientes al hacer que los departamentos de toothose accesible de datos que lo necesitan (por ejemplo, los departamentos de nóminas y reservas). Estos datos personales se almacenan fuera de centro de datos corporativos controlado de hello y no está bajo control físico de la compañía de Hola.

### <a name="company-goal"></a>Objetivo de la empresa

Como parte de una estrategia de varias capas de defensa en profundidad de seguridad, es un tooensure de objetivo de la empresa que se cifren todos los orígenes de datos que contienen datos personales, los que residen en el almacenamiento en nube incluidos. Si no está autorizado personas ganancia acceso toohello los datos personales, debe ser en un formulario que se representará ilegible. La aplicación del cifrado debería ser fácil y transparente tanto para los usuarios como para los administradores.

## <a name="solutions"></a>Soluciones

Los servicios de Azure proporcionan varios toohelp herramientas y tecnologías de proteger los datos personales en reposo cifrándolos.

### <a name="azure-key-vault"></a>Azure Key Vault

[Almacén de claves de Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) ofrece un almacenamiento seguro para las claves de hello utilizan tooencrypt datos en reposo en los servicios de Azure y se recomienda Hola soluciones de almacenamiento y administración de claves. Administración de claves de cifrado es esencial toosecuring almacena datos.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>¿Cómo se puede usar las claves de tooprotect del almacén de claves de Azure que cifran los datos personales?

toouse almacén de claves de Azure, necesita una cuenta de Azure tooan de suscripción. También necesita tener Azure Powershell instalado. Los pasos incluyen usando PowerShell cmdlets toodo Hola siguientes:

1. Conectar tooyour suscripciones

2. Creación de un Almacén de claves

3. Agregar una clave o un almacén de claves secretas toohello

4. Registrar las aplicaciones que va a usar el almacén de claves Hola con Azure Active Directory

5. Autorizar Hola aplicaciones toouse Hola clave o el secreto

toocreate un almacén de claves, use hello CmDlt de PowerShell New-AzureRmKeyVault. Asignará un nombre de almacén, un nombre de grupo de recursos y una ubicación geográfica. Deberá usar el nombre del almacén de hello al administrar claves a través de otros Cmdlets. Las aplicaciones que utilizan el almacén de Hola a través de la API de REST de hello usará el almacén de hello URI.

Azure Key Vault puede proporcionar una clave protegida mediante software o importar una clave ya existente de un archivo .PFX. También puede almacenar secretos (contraseñas) en el almacén de Hola.

También puede generar una clave de HSM local y transferir tooHSMs Hola servicio de almacén de claves, sin clave Hola dejando límite de HSM Hola.

Para obtener instrucciones detalladas sobre cómo usar el almacén de claves de Azure, siga los pasos de hello [empezar a trabajar con el almacén de claves de Azure.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Para obtener una lista de cmdlets de PowerShell que se usan con Azure Key Vault, consulte [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

### <a name="azure-disk-encryption-for-windows"></a>Azure Disk Encryption para Windows

[Azure Disk Encryption para máquinas virtuales de IaaS de Windows y Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protege los datos personales en reposo en las máquinas virtuales de Azure y se integra con Azure Key Vault. Cifrado de disco de Azure usa [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) en Windows y [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) en Linux tooencrypt ambos Hola hello y sistema operativo de los discos de datos. Azure Disk Encryption es compatible con Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, y con clientes de Windows 8 y Windows 10.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>¿Cómo se puede usar datos personales de tooprotect de cifrado del disco de Azure?

toouse cifrado del disco de Azure, necesita una cuenta de Azure tooan de suscripción. Cifrado de disco de Azure tooenable para Windows y las máquinas virtuales de Linux, Hola siguientes:

1. Use la plantilla del Administrador de recursos de cifrado de disco de Azure hello, PowerShell o cifrado de disco de tooenable de interfaz de línea de comandos (CLI) de Hola y especifique la configuración de cifrado. 

2. Conceder acceso toohello material de cifrado de la plataforma Azure tooread Hola desde el almacén de claves.

3. Proporcione un Azure Active Directory (AAD) aplicación identidad toowrite Hola cifrado tooyour material clave almacén de claves.

Azure actualizará Hola VM y la configuración de almacén de claves de Hola y configurar la máquina virtual cifrada.

Al configurar su toosupport de almacén de claves cifrado del disco de Azure, puede agregar una clave de cifrado de claves (KEK) para lograr una mayor seguridad y copia de seguridad de toosupport de máquinas virtuales cifradas.

![](media/protect-personal-data-at-rest/create-key.png)

En [Azure Disk Encryption para máquinas virtuales IaaS Linux y Windows](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) puede encontrar instrucciones detalladas sobre escenarios de implementación y experiencias de usuario específicas.

### <a name="azure-storage-service-encryption"></a>Cifrado del servicio Azure Storage

[Cifrado de servicio de almacenamiento de Azure (SSE) para los datos en reposo](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) le ayuda a proteger y proteger los datos toomeet los compromisos de seguridad y cumplimiento organizativos. Almacenamiento de Azure automáticamente cifra los datos mediante toostorage de toopersisting anteriores de cifrado de AES de 256 bits y los descifra tooretrieval anterior. Este servicio está disponible para los archivos y blobs de Azure.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>¿Cómo se puede usar datos personales de cifrado del servicio de almacenamiento tooprotect?

tooenable cifrado del servicio de almacenamiento, Hola siguientes:

1. Inicie sesión en hello portal de Azure.

2. Seleccione una cuenta de almacenamiento.

3. En configuración, en la sección de servicio Blob de hello, seleccione cifrado.

4. En hello sección de servicio de archivos, seleccione el cifrado.

Tras hacer clic en configuración de cifrado de hello, puede habilitar o deshabilitar el cifrado del servicio de almacenamiento.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

Los datos nuevos se cifrarán. Los datos en los archivos ya existentes de esta cuenta de almacenamiento permanecerán sin cifrar.

Después de habilitar el cifrado, copie la cuenta de almacenamiento de datos toohello mediante uno de los siguientes métodos de hello:

1. Copiar blobs o archivos con hello [utilidad de línea de comandos de AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).

2. [Montar un recurso compartido de archivos mediante SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) por lo que puede usar una utilidad como Robocopy toocopy archivos.

3. Copiar blob o archivo de datos tooand del almacenamiento de blobs o entre cuentas de almacenamiento mediante [bibliotecas de cliente de almacenamiento, como .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).

4.  Use un [Explorador de almacenamiento](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload tooyour cuenta de almacenamiento de blobs con el cifrado habilitado.

### <a name="transparent-data-encryption"></a>Cifrado de datos transparente

Cifrado de datos transparente (TDE) es una característica de SQL Azure mediante el cual se puede cifrar los datos en ambos niveles de base de datos y el servidor de Hola. TDE ahora está habilitado de forma predeterminada en todas las bases de datos recién creadas. TDE realiza el cifrado de E/S y descifrado de los archivos de datos y de registro de hello en tiempo real.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>¿Cómo se puede usar datos personales de TDE tooprotect?

Puede configurar TDE a través de hello portal de Azure, mediante el uso de API de REST de hello, o mediante PowerShell. Hola tooenable TDE en una base de datos existente mediante Hola Portal de Azure, después de:

1. Visite hello Azure portal en <https://portal.azure.com> e inicie sesión con su cuenta de administrador de Azure o colaborador.

2. En el encabezado de la izquierda hello, haga clic en tooBROWSE y, a continuación, haga clic en bases de datos SQL.

3. Con las bases de datos SQL seleccionadas en el panel izquierdo de hello, haga clic en la base de datos de usuario.

4. En la hoja de la base de datos de hello, haga clic en todas las configuraciones.

5. En la hoja de configuración de hello, haga clic en las hoja de cifrado de datos transparente cifrado parte tooopen Hola transparente de los datos.

6. En la hoja de cifrado de datos de hello, mover tooOn de botón de cifrado de datos de hello y, a continuación, haga clic en Guardar (al principio de Hola de página de hello) configuración de hello tooapply. estado de cifrado de Hello aproximará el progreso de Hola de cifrado de datos transparente de Hola.

![Habilitar el cifrado de datos](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Obtener instrucciones sobre cómo tooenable TDE y obtener información acerca de cómo descifrar las bases de datos protegida por TDE etc. pueden encontrarse en el artículo de Hola [cifrado de datos transparente con base de datos de SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>Resumen

empresa Hola puede lograr su objetivo de cifrar datos personales guardados en hello nube de Azure. Puede hacerlo mediante el cifrado de disco de Azure demasiado proteger volúmenes completos. Esto puede incluir archivos de sistema operativo de Hola y archivos de datos que contienen información de identificación personal y otros datos confidenciales. Cifrado de servicio de almacenamiento de Azure puede ser usado tooprotect datos personales que se almacenan en archivos y de blobs. Para los datos que se almacenan en instancias de Azure SQL Database, el cifrado de datos transparente ofrece protección frente a una exposición no autorizada de información personal.

tooprotect hello las claves usadas tooencrypt datos en Azure, la empresa de hello puede usar el almacén de claves de Azure. Esto simplifica el proceso de administración de claves de Hola y habilita Hola control toomaintain de empresa de claves que tienen acceso y cifrar los datos personales.

## <a name="next-steps"></a>Pasos siguientes

- [Guía de solución de problemas de Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Cifrado de una máquina virtual de Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Cifrado de datos en Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Cifrado de base de datos en reposo en Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
