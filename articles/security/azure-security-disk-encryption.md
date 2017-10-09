---
title: "aaaAzure cifrado del disco para Windows y las máquinas virtuales de Linux IaaS | Documentos de Microsoft"
description: "En este artículo se ofrece información general de Microsoft Azure Disk Encryption para máquinas virtuales IaaS con Windows y Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Cifrado de disco de Azure para máquinas virtuales IaaS Linux y Windows
Microsoft Azure es tooensuring firme compromiso de la privacidad de los datos, soberanía de datos y le permite toocontrol hospedado de Azure datos a través de una gama de tecnologías avanzadas tooencrypt, controlar y administrar claves de cifrado, auditoría y control de acceso de datos. Esto proporciona a los clientes de Azure solución Hola de toochoose de flexibilidad de Hola que mejor se adapte a sus necesidades empresariales. En este documento, le presentaremos tooa nueva solución tecnológica "Cifrado de disco de Azure para Windows y de Linux IaaS VM" toohelp proteger y proteger los datos toomeet los compromisos de seguridad y cumplimiento organizativos. papel de Hello proporciona instrucciones detalladas sobre la compatibilidad de características de cifrado de disco de Azure toouse Hola incluidos Hola escenarios y las experiencias de usuario de Hola.

> [!NOTE]
> Algunas de las recomendaciones pueden provocar un aumento del uso de datos, de la red o de recursos de proceso, lo que incrementará los costes de las licencias o suscripciones.

## <a name="overview"></a>Información general
Azure Disk Encryption es una nueva funcionalidad que permite cifrar los discos de las máquinas virtuales IaaS con Windows y Linux. Cifrado del disco Azure aprovecha estándar del sector hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) característica de Windows y hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) característica de cifrado de volumen de Linux tooprovide para discos de datos de Hola y Hola SO. solución de Hola se integra con [el almacén de claves de Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp controlar y administrar claves de cifrado del disco de Hola y secretos en su suscripción de almacén de claves. solución de Hello también garantiza que todos los datos en discos de máquina virtual de Hola se cifran en reposo en el almacenamiento de Azure.

Azure Disk Encryption para máquinas virtuales IaaS de Windows y Linux ahora tiene **disponibilidad general** en todas las regiones públicas de Azure y regiones de AzureGov para VM estándares y VM con Premium Storage.

### <a name="encryption-scenarios"></a>Escenarios de cifrado
Hola soluciones de cifrado del disco de Azure admite Hola cliente los escenarios siguientes:

* Habilitación del cifrado en las nuevas máquinas virtuales IaaS creadas a partir de un VHD precifrado y las claves de cifrado
* Habilitar el cifrado en nuevas máquinas virtuales de IaaS creado a partir de imágenes de la Galería de Azure de hello compatibles
* Habilitación del cifrado en las máquinas virtuales IaaS existentes que se ejecutan en Azure
* Deshabilitación del cifrado en máquinas virtuales IaaS de Windows
* Deshabilitación del cifrado en unidades de datos para máquinas virtuales IaaS con Linux
* Habilitación del cifrado en máquinas virtuales de discos administrados
* Actualización de la configuración del cifrado de una máquina virtual cifrada de un tipo de almacenamiento que no sea Premium Storage existente
* Restauración y copia de seguridad de VM cifradas, cifradas con clave de cifrado

solución de Hello admite Hola los escenarios siguientes para las máquinas virtuales IaaS cuando están habilitadas en Microsoft Azure:

* Integración con el Almacén de claves de Azure
* Máquinas virtuales de nivel estándar: [máquinas virtuales IaaS de las series A, D, DS, G, GS, F, etc.](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Habilitar el cifrado en Windows y las máquinas virtuales de IaaS de Linux y las máquinas virtuales de disco administrado de hello admite imágenes de la Galería de Azure
* Deshabilitación del cifrado en sistemas operativos y unidades de datos para máquinas virtuales IaaS de Windows y máquinas virtuales de discos administrados
* Deshabilitación del cifrado en unidades de datos para máquinas virtuales IaaS de Linux y máquinas virtuales de discos administrados
* Habilitación del cifrado en máquinas virtuales IaaS que ejecutan el sistema operativo cliente de Windows
* Habilitación del cifrado en volúmenes con rutas de montaje
* Habilitación del cifrado en máquinas virtuales de Linux configurado con seccionamiento de disco (RAID) mediante el uso de mdadm
* Habilitación del cifrado en máquinas virtuales de Linux mediante el uso de LVM para discos de datos
* Habilitación del cifrado en máquinas virtuales Windows configurado con espacios de almacenamiento
* Actualización de la configuración del cifrado de una máquina virtual cifrada de un tipo de almacenamiento que no sea Premium Storage existente
* Se admiten todas las regiones públicas de Azure y las regiones de AzureGov

solución de Hello no admite Hola siguientes escenarios, características y tecnologías:

* Máquinas virtuales IaaS de nivel básico
* Deshabilitación del cifrado en una unidad del sistema operativo para máquinas virtuales IaaS Linux
* Deshabilitar el cifrado en una unidad de datos si se cifra Hola unidad del SO para máquinas virtuales de Iaas de Linux
* Máquinas virtuales de IaaS que se crean mediante el método de creación de VM clásica de Hola
* NO se admite la habilitación del cifrado en imágenes personalizadas de cliente de máquinas virtuales IaaS Windows y Linux. En la actualidad no se admite la habilitación del cifrado en el disco del sistema operativo de LVM Linux. Se admitirá pronto.
* Integración con el Servicio de administración de claves local
* Azure Files (sistema de archivos compartido), Network File System (NFS), volúmenes dinámicos y máquinas virtuales Windows configuradas con sistemas RAID basadas en software
* Restaure y realice una copia de seguridad de máquinas virtuales cifradas sin clave de cifrado.
* Actualice la configuración del cifrado de una máquina virtual cifrada con Premium Storage existente.

> [!NOTE]
> Copia de seguridad y restauración de máquinas virtuales cifradas solo se admite para las máquinas virtuales que se cifran con la configuración de KEK Hola. No se admite en máquinas virtuales cifradas sin KEK. KEK es un parámetro opcional que habilita el cifrado de máquinas virtuales. Próximamente se agregará esta compatibilidad.
> No se admite la actualización de la configuración del cifrado de una máquina virtual cifrada con Premium Storage existente. Próximamente se agregará esta compatibilidad.

### <a name="encryption-features"></a>Características de cifrado
Al habilitar e implementar el cifrado del disco de Azure para máquinas virtuales de IaaS de Azure, hello siguientes funcionalidades están habilitadas, dependiendo de la configuración de hello proporcionada:

* Cifrado de volumen de arranque de hello SO volumen tooprotect hello en reposo en el sistema de almacenamiento
* Cifrado de datos volúmenes tooprotect Hola los volúmenes de datos en reposo en el sistema de almacenamiento
* Deshabilitar el cifrado de hello sistema operativo y datos de las unidades para las máquinas virtuales de IaaS de Windows
* Deshabilitar el cifrado de datos de hello las unidades para las máquinas virtuales de IaaS de Linux (sólo si OS unidad es no cifrado)
* Protección de claves de cifrado de Hola y secretos en su suscripción de almacén de claves
* Notificar el estado de cifrado de Hola de hello cifra IaaS VM
* Eliminación de opciones de configuración de cifrado del disco de máquina virtual de IaaS de Hola
* Copia de seguridad y restauración de máquinas virtuales cifradas mediante el servicio de copia de seguridad de Azure Hola

> [!NOTE]
> Copia de seguridad y restauración de máquinas virtuales cifradas solo se admite para las máquinas virtuales que se cifran con la configuración de KEK Hola. No se admite en máquinas virtuales cifradas sin KEK. KEK es un parámetro opcional que habilita el cifrado de máquinas virtuales.

La solución Azure Disk Encryption para máquinas virtuales IaaS para Windows y Linux incluye lo siguiente:

* extensión de cifrado del disco de Hola para Windows.
* extensión de cifrado del disco de Hola para Linux.
* cmdlets de PowerShell de Hello cifrado del disco.
* Hola cmdlets de Azure interfaz de línea de comandos (CLI) de cifrado del disco.
* Hola plantillas del Administrador de recursos de Azure de cifrado del disco.

Hola soluciones de cifrado del disco de Azure es compatible con las máquinas virtuales de IaaS que ejecutan Windows o el sistema operativo Linux. Para obtener más información sobre los sistemas operativos compatibles de hello, vea Hola "requisitos previos" sección.

> [!NOTE]
> No hay cargo adicional por el cifrado de discos de máquinas virtuales con Azure Disk Encryption.

### <a name="value-proposition"></a>Propuesta de valor
Cuando aplique una solución de administración de cifrado de disco de Azure hello, puede cumplir Hola siguiendo las necesidades del negocio:

* Las máquinas virtuales IaaS se protegen en reposo, porque se pueden usar cifrado estándar del sector tecnología tooaddress seguridad y cumplimiento de normas requisitos organizativos.
* Las máquinas virtuales IaaS arrancan bajo directivas y claves controladas por el cliente, y puede auditar su uso en su almacén de claves.

### <a name="encryption-workflow"></a>Flujo de trabajo de cifrado
cifrado del disco tooenable para Windows y las máquinas virtuales de Linux, Hola siguientes:

1. Elegir un escenario de cifrado entre Hola anteriores escenarios de cifrado.
2. Participar en el cifrado de disco tooenabling a través de la plantilla del Administrador de recursos de cifrado de disco de Azure hello, cmdlets de PowerShell o comando de CLI y especificar la configuración de cifrado de Hola.

   * Para escenario VHD de cifrado de cliente hello, cargue cuenta de almacenamiento de tooyour de disco duro virtual de hello cifrado y almacén de claves de tooyour material clave de cifrado de Hola. A continuación, proporciona cifrado de tooenable de configuración de cifrado de hello en una nueva VM de IaaS.
   * Para nuevas máquinas virtuales que se crean a partir de hello Marketplace y las máquinas virtuales existentes que se están ejecutando en Azure, proporcionan cifrado de tooenable de configuración de cifrado de hello en hello IaaS VM.

3. Conceder acceso toohello material de clave de cifrado de hello en tooread plataforma Windows Azure (claves de cifrado de BitLocker para los sistemas Windows) y la frase de contraseña de Linux de cifrado en hello IaaS VM tooenable almacén de claves.

4. Proporcionar hello Azure Active Directory (Azure AD) aplicación identidad toowrite Hola cifrado tooyour material clave almacén de claves. Si lo hace, habilita el cifrado en hello IaaS VM para escenarios de hello mencionados en el paso 2.

5. Azure actualiza el modelo de servicio VM de hello con cifrado y la configuración de almacén de claves de Hola y configura su VM cifrada.

 ![Microsoft Antimalware en Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Flujo de trabajo de descifrado
toodisable cifrado del disco para máquinas virtuales de IaaS, Hola completa siguiendo los pasos de alto nivel:

1. Elija toodisable cifrado (descifrado) en una VM en ejecución IaaS en Azure a través de la plantilla de administrador de recursos de cifrado de disco de Azure de Hola o los cmdlets de PowerShell y especificar la configuración de descifrado de Hola.

 Este paso deshabilita el cifrado de volumen de datos de sistema operativo u Hola Hola o ambos en hello ejecutando la máquina virtual de IaaS de Windows. Sin embargo, como se mencionó en la sección anterior de hello, deshabilitar el cifrado de disco de sistema operativo de Linux no se admite. paso de descifrado de Hello solo se permite para las unidades de datos en máquinas virtuales de Linux siempre y cuando no se cifra el disco del sistema operativo Hola.
2. Las actualizaciones de Azure Hola modelo de servicio VM y Hola IaaS VM se marca descifrada. contenido de Hola de hello VM ya no se cifra en reposo.

> [!NOTE]
> operación de cifrado de la deshabilitación de Hello no elimina la clave hello y el almacén de claves de cifrado (claves de cifrado de BitLocker para los sistemas Windows) o la frase de contraseña de Linux.
 > No se admite la deshabilitación del cifrado de disco del sistema operativo para Linux. paso de descifrado de Hello solo se permite para las unidades de datos en máquinas virtuales de Linux.
Deshabilitar el cifrado de disco de datos de Linux no se admite si se cifra Hola unidad del SO.

## <a name="prerequisites"></a>Requisitos previos
Antes de habilitar el cifrado de disco de Azure en máquinas virtuales de IaaS de Azure para escenarios de hello admite que se trataron en la sección "Introducción" Hola, vea Hola siguiendo los requisitos previos:

* Debe tener los recursos de toocreate de una suscripción válida de Azure en Azure en regiones de hello compatible.
* Cifrado de disco de Azure es compatible con hello siguientes versiones de Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 y Windows Server 2016.
* Cifrado de disco de Azure es compatible con Hola después de las versiones de cliente de Windows: Windows 10 y el cliente de Windows 8.

> [!NOTE]
> En el caso de Windows Server 2008 R2, debe tener .NET Framework 4.5 instalado para poder habilitar el cifrado en Azure. Puede instalarlo desde Windows Update mediante la instalación de actualización opcional Hola Microsoft .NET Framework 4.5.2 para sistemas basados en x64 de Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Se admite el cifrado de disco de Azure en hello después de la Galería de Azure según las distribuciones de Linux server y las versiones:

| Distribución de Linux | Versión | Tipo de volumen compatible con el cifrado|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | Sistema operativo y disco de datos |
| Ubuntu | 14.04.5-DAILY-LTS | Sistema operativo y disco de datos |
| Ubuntu | 12.10 | Disco de datos |
| Ubuntu | 12.04 | Disco de datos |
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
| SLES | 12-SP1 (Premium) | Disco de datos |
| SLES | HPC 12 | Disco de datos |
| SLES | 11-SP4 (Premium) | Disco de datos |
| SLES | 11 SP4 | Disco de datos |

* Cifrado del disco Azure requiere que el almacén de claves y las máquinas virtuales residan en hello misma región de Azure y la suscripción.

> [!NOTE]
> Configuración de recursos de hello en regiones independientes, produce un error en habilitar la característica de cifrado de disco de Azure de Hola.

* tooset una copia de seguridad y configurar el almacén de claves para el cifrado de disco de Azure, consulte la sección **establecer una copia de seguridad y configurar el almacén de claves de cifrado del disco de Azure** en hello *requisitos previos* sección de este artículo.
* tooset una copia de seguridad y configurar aplicación de Azure AD en Azure Active directory para el cifrado de disco de Azure, consulte la sección **Configurar aplicación hello Azure AD en Azure Active Directory** en hello *requisitos previos* sección de este artículo.
* tooset una copia de seguridad y configurar la directiva de acceso de almacén de claves de hello para la aplicación hello Azure AD, consulte la sección **configurar la directiva de acceso de almacén de claves de hello para la aplicación hello Azure AD** en hello *requisitos previos* sección de en este artículo.
* tooprepare un cifrado previamente VHD de Windows, consulte la sección **preparar un VHD de Windows cifrado previamente** en hello *apéndice*.
* tooprepare un VHD previamente cifradas de Linux, consulte la sección **preparar un VHD de Linux cifrado previamente** en hello *apéndice*.
* Hello plataforma Windows Azure necesita claves de cifrado de acceso toohello o secretos en el almacén de claves toomake su máquina virtual de toohello disponibles cuando inicia y se descifra el volumen de sistema operativo de la máquina virtual de Hola. plataforma de tooAzure toogrant permisos, conjunto hello **EnabledForDiskEncryption** propiedad en el almacén de claves de Hola. Para obtener más información, consulte **establecer una copia de seguridad y configurar el almacén de claves de cifrado del disco de Azure** Hola apéndice.
* El secreto del almacén de claves y las direcciones URL de KEK deben tener versiones. Azure exige esta restricción del control de versiones. Para secreta y KEK las direcciones URL, vea hello en los ejemplos siguientes:

  * Ejemplo de dirección URL de secreto válida: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Ejemplo de dirección URL de KEK válida: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* Azure Disk Encryption no admite que los números de puerto se especifiquen como parte de los secretos del almacén de claves y las direcciones URL de KEK. Para obtener ejemplos de direcciones URL de almacén de claves admitidos y no admitidos, vea Hola siguiente:

  * Dirección URL de almacén de claves no aceptable: *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Dirección URL de almacén de claves aceptable: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* característica de cifrado del disco de Azure de hello tooenable, hello las máquinas virtuales IaaS debe cumplir Hola según los requisitos de configuración de punto de conexión de red:
  * tooget un almacén de claves de tooyour tooconnect token, Hola IaaS VM debe ser capaz de tooconnect punto de conexión de Azure Active Directory de tooan, \[login.microsoftonline.com\].
  * toowrite Hola cifrado claves tooyour almacén de claves, Hola IaaS VM debe ser el punto de conexión de tooconnect puede toohello el almacén de claves.
  * Hola IaaS VM, debe ser capaz de tooconnect tooan almacenamiento de Azure extremo que hosts Hola repositorio de extensión de Azure y una cuenta de almacenamiento de Azure que hosts Hola archivos VHD.

  > [!NOTE]
  > Si la directiva de seguridad limita el acceso de máquinas virtuales de Azure toohello Internet, puede resolver Hola anterior URI y configurar una toohello de conectividad saliente de tooallow direcciones IP de regla concreta.
  >
  >tooconfigure y acceso del almacén de claves de Azure detrás de un firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)

* Use Hola última versión del SDK de Azure PowerShell versión tooconfigure cifrado del disco de Azure. Descargar la versión más reciente de Hola de [versión de PowerShell de Azure](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > En el [SDK de Azure PowerShell (versión 1.1.0)](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016) no se admite Azure Disk Encryption. Si recibe un error relacionado con toousing Azure PowerShell 1.1.0, consulte [tooAzure relacionados de Error de cifrado de Azure disco PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun cualquier comando de CLI de Azure y asociarlo con su suscripción de Azure, primero debe instalar la CLI de Azure:
  * tooinstall CLI de Azure y asociarlo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure CLI](../cli-install-nodejs.md).
  * toouse CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure, consulte [comandos de CLI de Azure en el modo de administrador de recursos](../virtual-machines/azure-cli-arm-commands.md).

* Cuando se cifra un disco administrado, es obligatorio tootake requisitos previos una instantánea del disco de hello administrada o una copia de seguridad del disco de hello fuera de cifrado de tooenabling anteriores de cifrado del disco de Azure.  Sin una copia de seguridad en su lugar, cualquier error inesperado durante el cifrado puede presentar disco hello y VM accesible sin una opción de recuperación.  AzureRmVMDiskEncryptionExtension de conjunto de copia de seguridad discos administrados actualmente no y se generará un error si se utilizan en un disco administrado a menos que se ha especificado el parámetro - skipVmBackup de hello.  Este parámetro es toouse unsafe, a menos que ya se hizo una copia de seguridad fuera de cifrado del disco de Azure.   Cuando se especifica el parámetro - skipVmBackup de hello, Hola cmdlet no realizará una copia de seguridad de hello administrado disco anterior tooencryption.  Por este motivo, se considera un toomake de requisitos previos obligatorio que necesite una copia de seguridad de disco administrado Hola que VM está en la posición anterior tooenabling cifrado del disco de Azure en caso de recuperación es posterior.  
> [!NOTE]
 > parámetro de Hello - skipVmBackup nunca debe utilizarse a menos que ya ha realizado una copia de seguridad o de instantáneas fuera de cifrado del disco de Azure. 

* Hola soluciones de cifrado del disco de Azure usa el protector de clave externo de hello BitLocker para máquinas virtuales de IaaS de Windows. Para las máquinas virtuales unidas en un dominio, NO cree ninguna directiva de grupo que exija protectores de TPM. Para obtener información acerca de la directiva de grupo de Hola "Permitir BitLocker sin un TPM compatible", consulte [referencia de directiva de grupo de BitLocker](https://technet.microsoft.com/library/ee706521).
* Directiva de BitLocker en las máquinas virtuales Unidos a un dominio con directiva de grupo personalizado debe incluir Hola después de configuración: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` cifrado del disco de Azure se producirá un error cuando la configuración de directiva de grupo personalizado para que Bitlocker no es compatibles. En equipos que no dispongan de hello pueden requerir configuración de directiva correcta, aplicar la nueva directiva de hello, forzar Hola nueva directiva tooupdate (gpupdate.exe /force) y, a continuación, reinicia el sistema.  
* toocreate una aplicación de Azure AD, crear un almacén de claves, o configurar un almacén de claves existente y habilitar el cifrado, vea hello [script de PowerShell de requisitos previos de cifrado del disco de Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* requisitos previos de cifrado del disco tooconfigure con hello CLI de Azure, consulte [esta secuencia de comandos de Bash](https://github.com/ejarvi/ade-cli-getting-started).
* tooback de servicio de copia de seguridad de Azure toouse Hola seguridad y restauración cifrado las máquinas virtuales, cuando está habilitado el cifrado con el cifrado de disco de Azure, cifran las máquinas virtuales mediante la configuración de clave de cifrado del disco de Azure de Hola. Hola servicio de copia de seguridad es compatible con las máquinas virtuales que se cifran mediante la configuración de la KEK solo. Vea [cómo tooback seguridad y restauración cifran las máquinas virtuales con cifrado de copia de seguridad de Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* Cuando se cifra un volumen de sistema operativo Linux, tenga en cuenta que un reinicio de máquina virtual actualmente al final de hello del proceso de Hola. Esto puede hacerse a través del portal de hello, powershell o CLI.   progreso de hello tootrack del cifrado, éstos sondeen periódicamente mensajes de estado de hello devuelto por Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.  Una vez completado el cifrado, el mensaje de estado de Hola Hola devuelta por este comando indicará esto.  Por ejemplo, "ProgressMessage: disco del sistema operativo cifrado correctamente, reinicie Hola máquina virtual" en este Hola de punto de VM se pueden reiniciar y usar.  

* Cifrado de disco de Azure para Linux requiere toohave de discos de datos un sistema de archivos montado en tooencryption anterior de Linux

* Hola cifrado del disco de Azure no admite discos de datos montados para Linux de forma recursiva. Por ejemplo, si hello sistema de destino monta un disco en /foo/bar y, a continuación, otro en /foo/bar/baz, cifrado de Hola de /foo/bar/baz se realizará correctamente, pero se producirá un error de cifrado de/foo/barra. 

* Cifrado de disco Azure solo es compatible con imágenes de la Galería de Azure compatible que cumplen los requisitos previos mencionados anteriormente de Hola. Imágenes personalizadas de cliente no se admiten debido a los esquemas de partición de toocustom y comportamientos de los procesos que puedan existir en estas imágenes. Además, incluso pueden no ser compatibles las máquinas virtuales basadas en imágenes de la galería que inicialmente cumplieran los requisitos previos, pero fueran modificadas después de su creación.  Para que motivo, Hola sugerido procedimiento para cifrar una VM Linux es toostart desde una imagen de galería limpia, cifrar Hola VM y, a continuación, agregar software personalizado o datos toohello VM según sea necesario.  

> [!NOTE]
> Copia de seguridad y restauración de máquinas virtuales cifradas solo se admite para las máquinas virtuales que se cifran con la configuración de KEK Hola. No se admite en máquinas virtuales cifradas sin KEK. KEK es un parámetro opcional que habilita las máquinas virtuales.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Configurar Hola aplicación de Azure AD en Azure Active Directory
Cuando necesite toobe cifrado habilitado en una máquina virtual en ejecución en Azure, el cifrado del disco de Azure genera y escribe el almacén de claves de tooyour de claves de cifrado de Hola. La administración de claves de cifrado en el almacén de claves necesita la autenticación de Azure AD.

Para ello, cree una aplicación de Azure AD. Encontrará pasos detallados para registrar una aplicación en la sección de "Obtener una identidad para hello aplicación" hello de entrada de blog de hello [almacén de claves de Azure - paso a paso](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Esta entrada también contiene varios ejemplos útiles sobre la instalación y la configuración del almacén de claves. Para realizar la autenticación, se pueden usar la autenticación basada en secreto de cliente o la autenticación de Azure AD basada en certificado del cliente.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Autenticación basada en secreto de cliente para Azure AD
secciones de Hello siguientes pueden ayudarle a configurar una autenticación basada en el secreto del cliente para Azure AD.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Creación de una aplicación de Azure AD mediante Azure PowerShell
Usar hello después toocreate de cmdlet de PowerShell una aplicación de Azure AD:

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId es hello Azure AD ClientID y $aadClientSecret es el secreto del cliente de Hola que debe usar tooenable posterior cifrado del disco de Azure. Proteger el secreto del cliente hello Azure AD adecuadamente.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Configurar identificador hello Azure AD y el secreto de hello portal de Azure clásico
También puede configurar el Id. de cliente de Azure AD y el secreto mediante el uso de hello [portal de Azure clásico]( https://manage.windowsazure.com). tooperform esta tarea, Hola siguientes:

1. Haga clic en hello **Active Directory** ficha.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Haga clic en **Agregar aplicación**y, a continuación, nombre de aplicación de tipo Hola.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Haga clic en el botón de flecha de hello y, a continuación, configurar propiedades de la aplicación hello.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Haga clic en la marca de verificación de hello en hello toofinish de esquina izquierda inferior. Aparecerá la página de configuración de aplicación Hola e Id. de cliente de AD Azure Hola se muestra en parte inferior de Hola de página de Hola.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Guardar el secreto del cliente hello Azure AD haciendo clic en hello **guardar** botón. Tenga en cuenta secreta de cliente hello Azure AD en el cuadro de texto de las claves de Hola. Protéjalo adecuadamente.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Hola anterior flujo no se admite en hello portal de Azure clásico.

##### <a name="use-an-existing-application"></a>Uso de una aplicación existente
tooexecute Hola siga los comandos, obtener y usar hello [módulo de PowerShell de Azure AD](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Hello siguientes comandos se deben ejecutar desde una nueva ventana de PowerShell. No utilice Azure PowerShell o comandos de hello Azure Resource Manager ventana tooexecute Hola. Se recomienda este enfoque porque estos cmdlets están en el módulo de MSOnline de Hola o PowerShell de Azure AD.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Autenticación basada en certificado para Azure AD
> [!NOTE]
> Actualmente no se admite la autenticación basada en certificado de Azure AD en máquinas virtuales con Linux.

Hola secciones siguientes muestran cómo tooconfigure una autenticación basada en certificados para Azure AD.

##### <a name="create-an-azure-ad-application"></a>Creación de una aplicación de Azure AD
toocreate una aplicación de Azure AD, ejecute hello siguientes cmdlets de PowerShell:

> [!NOTE]
> Reemplace Hola siguiente `yourpassword` cadena con su contraseña segura y la contraseña de Hola de medida de seguridad.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

Una vez finalizado este paso, cargar un almacén de claves de tooyour de archivo PFX y habilitar Hola acceso directiva necesaria toodeploy esa VM tooa de certificado.

##### <a name="use-an-existing-azure-ad-application"></a>Uso de una aplicación de Azure AD existente
Si va a configurar la autenticación basada en certificados para una aplicación existente, use cmdlets de PowerShell de Hola que se muestra aquí. Ser tooexecute seguro de ellas desde una nueva ventana de PowerShell.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

Una vez finalizado este paso, cargar un almacén de claves de tooyour de archivo PFX y habilitar Directiva de acceso de hello requerido toodeploy Hola certificado tooa máquina virtual.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Cargar un almacén de claves de tooyour de archivo PFX
Para obtener una explicación detallada de este proceso, consulte [Hola Blog oficial del equipo de almacén de claves de Azure](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). Sin embargo, Hola siguientes cmdlets de PowerShell es todo lo que necesita para la tarea hello. Ser tooexecute seguro desde la consola de PowerShell de Azure.

> [!NOTE]
> Reemplace Hola siguiente `yourpassword` cadena con su contraseña segura y la contraseña de Hola de medida de seguridad.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Implementar un certificado en su tooan de almacén de claves existente de la máquina virtual
Cuando termine de cargar Hola PFX, implemente un certificado en hello tooan de almacén de claves existente VM con siguiente hello:
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Configurar la directiva de acceso de almacén de claves de hello para la aplicación hello Azure AD
La aplicación de Azure AD necesita claves de derechos tooaccess Hola o secretos en el almacén de Hola. Hola de uso [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permisos toohello de aplicaciones, mediante el identificador de cliente de hello (que se generó cuando se registró la aplicación hello) como hello _– ServicePrincipalName_ valor del parámetro. toolearn más información, consulte Entrada de blog hello [almacén de claves de Azure - paso a paso](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Este es un ejemplo de cómo tooperform esta tarea a través de PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Cifrado de disco de Azure requiere hello tooconfigure tras la aplicación de cliente de acceso a las directivas tooyour Azure AD: _WrapKey_ y _establecer_ permisos.

## <a name="terminology"></a>Terminología
toounderstand algunos de los términos comunes que Hola utilizan esta tecnología, Hola uso terminología en la tabla siguiente:

| Terminología | Definición |
| --- | --- |
| Azure AD | Azure AD es [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Una cuenta de Azure AD es un requisito previo para autenticar, almacenar y recuperar secretos del almacén de claves. |
| Almacén de claves de Azure | Key Vault es un servicio de administración de claves criptográficas basado en módulos de seguridad de hardware validados por el Estándar federal de procesamiento de información (FIPS), que ayuda a proteger las claves criptográficas y los secretos confidenciales. Para obtener más información, consulte la documentación de [Key Vault](https://azure.microsoft.com/services/key-vault/). |
| ARM | Administrador de recursos de Azure |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) es una reconocido del sector volumen cifrado tecnología de Windows que ha utilizado el cifrado del disco tooenable en máquinas virtuales de IaaS de Windows. |
| BEK | Las claves de cifrado de BitLocker son volúmenes de datos y el volumen de arranque de hello OS tooencrypt usado. las claves de BitLocker de Hello están protegidas en un almacén de claves como secretos. |
| CLI | Vea [Instalación de la CLI de Azure](../cli-install-nodejs.md). |
| DM-Crypt |[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) es subsistema de cifrado de disco basadas en Linux, transparente de Hola que ha utilizado el cifrado del disco tooenable en máquinas virtuales de IaaS de Linux. |
| KEK | Clave de cifrado de claves es Hola clave asimétrica (RSA 2048) que puede usar tooprotect o ajustar el secreto de Hola. Se puede proporcionar una clave protegida mediante módulos de seguridad de hardware (HSM) o una clave protegida mediante software. Para obtener más información, consulte la documentación de [Azure Key Vault](https://azure.microsoft.com/services/key-vault/). |
| cmdlets de PS | Consulte [Cmdlets de Azure PowerShell](/powershell/azure/overview). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Instalación y configuración del almacén de claves para Azure Disk Encryption
Cifrado de disco de Azure le ayuda a claves de cifrado del disco de medida de seguridad hello y secretos en el almacén de claves. tooset de su almacén de claves de cifrado del disco de Azure, Hola completa los pasos en cada una de las siguientes secciones de Hola.

#### <a name="create-a-key-vault"></a>Creación de un Almacén de claves
toocreate un almacén de claves, use uno de hello siguientes opciones:

* [Plantilla de Resource Manager llamada "101-Key-Vault-Create"](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Cmdlets de almacén de claves de Azure PowerShell](/powershell/module/azurerm.keyvault/#key_vault)
* Administrador de recursos de Azure
* Cómo demasiado[proteger el almacén de claves](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Si ya ha configurado un almacén de claves de su suscripción, omitir toohello próxima sección.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Configuración de una clave de cifrado de claves (KEK) (opcional)
Si desea toouse una KEK para una capa adicional de seguridad para las claves de cifrado de BitLocker de hello, agregar un almacén de claves de tooyour KEK. Hola de uso [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate cmdlet una clave de cifrado de claves en el almacén de claves de Hola. También puede importar una KEK en el HSM de administración de claves local. Para obtener más información, consulte la [documentación de Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

Puede agregar Hola KEK yendo tooAzure el Administrador de recursos o mediante la interfaz de almacén de claves.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Configuración de los permisos del almacén de claves
Hello plataforma Windows Azure necesita claves de cifrado de acceso toohello o secretos en el almacén de claves toomake les toohello disponible de máquina virtual para arranque y descifrar los volúmenes de Hola. toogrant permisos toohello plataforma Windows Azure, conjunto hello **EnabledForDiskEncryption** del almacén de propiedad de clave de hello mediante cmdlet de PowerShell de almacén de claves de hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

También puede establecer hello **EnabledForDiskEncryption** propiedad visitando hello [Explorador de recursos de Azure](https://resources.azure.com).

Como se mencionó anteriormente, debe establecer hello **EnabledForDiskEncryption** propiedad en el almacén de claves. En caso contrario, se producirá un error de implementación de Hola.

Puede configurar directivas de acceso para la aplicación de Azure AD desde la interfaz del almacén de claves de hello, como se muestra aquí:

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

En hello **las directivas de acceso avanzado** ficha, asegúrese de que el almacén de claves está habilitado para el cifrado de disco de Azure:

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Escenarios de implementación del cifrado de disco y experiencias de usuario
Puede habilitar muchos escenarios de cifrado del disco y pasos de hello pueden variar escenario de toohello correspondiente. Hello las secciones siguientes tratan los escenarios de hello en mayor detalle.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Habilitar el cifrado en nuevas máquinas virtuales de IaaS que se crean a partir de hello Marketplace
Puede habilitar el cifrado de disco en la nueva máquina virtual de Windows de IaaS de hello Marketplace en Azure mediante el uso de hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. En la plantilla de hello Azure inicio rápido, haga clic en **implementar tooAzure**, especifique la configuración de cifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.

2. Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en una nueva VM de IaaS.

> [!NOTE]
> Esta plantilla crea una nueva VM de Windows cifrados que usa la imagen de la Galería de hello Windows Server 2012.

Puede habilitar el cifrado de disco en una nueva máquina virtual IaaS con RedHat Linux 7.2 con una matriz RAID-0 de 200 GB mediante esta [plantilla de Resource Manager](https://aka.ms/fde-rhel). Después de implementar la plantilla de hello, comprobar el estado de cifrado de VM de hello mediante hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, tal y como se describe en [SO cifrado de unidad en una VM de Linux ejecución](#encrypting-os-drive-on-a-running-linux-vm). Cuando la máquina de hello devuelve un estado de _VMRestartPending_, reinicie Hola máquina virtual.

Hello tabla siguiente enumeran los parámetros de plantilla de administrador de recursos de Hola para nuevas máquinas virtuales de escenario de Marketplace de hello mediante identificador de cliente de Azure AD:

| Parámetro | Descripción |
| --- | --- |
| adminUserName | Nombre de usuario de administrador de la máquina virtual de Hola. |
| adminPassword | Contraseña de usuario de administrador de la máquina virtual de Hola. |
| newStorageAccountName | Nombre de hello almacenamiento cuenta toostore sistema operativo y datos de discos duros virtuales. |
| vmSize | Tamaño del programa Hola a máquina virtual. Actualmente, solo se admiten las series A, D y G estándar. |
| virtualNetworkName | Nombre de red virtual que Hola VM NIC hello debe pertenecer a. |
| subnetName | Nombre de subred de Hola Hola ese Hola VM NIC de red virtual debe pertenecer a. |
| AADClientID | Id. de cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos tooyour el almacén de claves. |
| AADClientSecret | Secreto del cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos tooyour el almacén de claves. |
| keyVaultURL | Dirección URL de clave de Hola del almacén que BitLocker se debe cargar la clave en hello. Puede obtenerlo mediante el cmdlet de hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | Dirección URL de clave de cifrado de claves de Hola que es usado tooencrypt hello genera claves de BitLocker (opcional). |
| keyVaultResourceGroup | Grupo de recursos de almacén de claves de Hola. |
| vmName | Nombre de máquina virtual que Hola operación de cifrado de hello es toobe realizada en. |

> [!NOTE]
> _KeyEncryptionKeyURL_ es un parámetro opcional. Puede aportar tu propia clave de cifrado de KEK toofurther proteger Hola datos (frase de contraseña secreta) en el almacén de claves.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>Habilitación del cifrado en nuevas máquinas virtuales IaaS creadas a partir del VHD cifrado del cliente y las claves de cifrado
En este escenario, puede habilitar cifrado con la plantilla de administrador de recursos de hello, cmdlets de PowerShell o comandos de CLI. Hello las secciones siguientes se explican en la plantilla de administrador de recursos de mayor detalle hello y comandos de CLI.

Siga las instrucciones de Hola de una de estas secciones para preparar imágenes previamente cifradas que se pueden usar en Azure. Después de crea la imagen de hello, puede utilizar pasos hello en la siguiente sección toocreate una VM de Azure cifrados de Hola.

* [Preparación de un VHD con Windows precifrado](#preparing-a-pre-encrypted-windows-vhd)
* [Preparación de un VHD con Linux precifrado](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>Utilizando la plantilla de administrador de recursos de Hola
Puede habilitar el cifrado de disco en el disco duro virtual cifrado mediante el uso de hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. En la plantilla de hello Azure inicio rápido, haga clic en **implementar tooAzure**, especifique la configuración de cifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.

2. Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en Hola nueva VM de IaaS.

Hello tabla siguiente enumeran los parámetros de plantilla de administrador de recursos de hello para el disco duro virtual cifrado:

| Parámetro | Descripción |
| --- | --- |
| newStorageAccountName | Nombre del programa Hola toostore de cuenta de almacenamiento de hello cifra VHD de sistema operativo. Esta cuenta de almacenamiento debe ya se han creado en hello mismo grupo de recursos y la misma ubicación que Hola máquina virtual. |
| osVhdUri | URI de hello VHD de sistema operativo de la cuenta de almacenamiento de Hola. |
| osType | Tipo de producto de sistema operativo (Windows o Linux). |
| virtualNetworkName | Nombre de red virtual que Hola VM NIC hello debe pertenecer a. Hello nombre debe ya se han creado en hello mismo grupo de recursos y la misma ubicación que Hola máquina virtual. |
| subnetName | Nombre de subred de hello en hello ese Hola VM NIC de red virtual debe pertenecer a. |
| vmSize | Tamaño del programa Hola a máquina virtual. Actualmente, solo se admiten las series A, D y G estándar. |
| keyVaultResourceID | Hola ResourceID que identifica el recurso de almacén de claves de hello en el Administrador de recursos de Azure. Puede obtenerlo mediante el uso de cmdlet de PowerShell de hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | Dirección URL de la clave de cifrado del disco de Hola que se puede establecer en el almacén de claves de Hola. |
| keyVaultKekUrl | Dirección URL de la clave de cifrado de claves de Hola para cifrar la clave de cifrado del disco de hello generado. |
| vmName | Nombre del programa Hola IaaS VM. |

#### <a name="using-powershell-cmdlets"></a>Uso de cmdlets de PowerShell
Puede habilitar el cifrado de disco en el disco duro virtual cifrado mediante cmdlet de PowerShell de hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>Uso de comandos de la CLI
cifrado del disco tooenable para este escenario mediante comandos CLI, Hola siguientes:

1. Configure las directivas de acceso en el almacén de claves:

   * Conjunto hello **EnabledForDiskEncryption** marca:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Conjunto de permisos tooAzure AD aplicación toowrite secretos tooyour almacén de claves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. cifrado de tooenable en una máquina virtual existente o se está ejecutando, tipo:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Obtenga el estado de cifrado:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. cifrado de tooenable en una nueva máquina virtual de un VHD cifrado, Hola utilice parámetros con hello siguientes `azure vm create` comando:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Habilitación del cifrado en una máquina virtual IaaS con Windows existente o en ejecución en Azure
En este escenario, puede habilitar cifrado con la plantilla de administrador de recursos de hello, cmdlets de PowerShell o comandos de CLI. Hello las secciones siguientes se explican con más detalle cómo tooenable mediante Hola plantilla del Administrador de recursos y comandos de CLI.

#### <a name="using-hello-resource-manager-template"></a>Utilizando la plantilla de administrador de recursos de Hola
Puede habilitar el cifrado de disco en existente o ejecutar máquinas virtuales de Windows de IaaS en Azure con hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. En la plantilla de hello Azure inicio rápido, haga clic en **implementar tooAzure**, especifique la configuración de cifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.

2. Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en hello existente o ejecuta VM de IaaS.

Hello siguiente tabla enumeran parámetros de plantilla de administrador de recursos de Hola para existente o máquinas virtuales que usan un identificador de cliente de Azure AD en ejecución:

| Parámetro | Descripción |
| --- | --- |
| AADClientID | Id. de cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos toohello el almacén de claves. |
| AADClientSecret | Secreto del cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos toohello el almacén de claves. |
| keyVaultName | Nombre de clave de hello almacén que BitLocker se debe cargar la clave en hello. Puede obtenerlo mediante el cmdlet de hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | Dirección URL de clave de cifrado de claves de Hola que es usado tooencrypt hello genera la clave de BitLocker. Este parámetro es opcional si selecciona **nokek** en lista de hello UseExistingKek de lista desplegable. Si selecciona **kek** en la lista desplegable UseExistingKek hello, debe escribir hello _keyEncryptionKeyURL_ valor. |
| volumeType | Tipo de volumen que se realiza la operación de cifrado de hello en. Los valores válidos son _SO_, _Datos_ y _Todo_. |
| sequenceVersion | Versión de la secuencia de hello operación de BitLocker. Incrementar este número de versión cada vez que se realiza una operación de cifrado del disco en hello misma máquina virtual. |
| vmName | Nombre de máquina virtual que Hola operación de cifrado de hello es toobe realizada en. |

> [!NOTE]
> _KeyEncryptionKeyURL_ es un parámetro opcional. Puede aportar tu propia clave de cifrado de KEK toofurther proteger Hola datos (secreto de cifrado de BitLocker) en el almacén de claves de Hola.

#### <a name="using-powershell-cmdlets"></a>Uso de cmdlets de PowerShell
Para obtener información acerca de cómo habilitar el cifrado con cifrado de disco de Azure mediante el uso de cmdlets de PowerShell, vea las entradas de blog hello [explorar el cifrado del disco de Azure con PowerShell de Azure, parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) y [explorar cifrado del disco de Azure con Azure PowerShell, parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>Uso de comandos de la CLI
cifrado de tooenable en existente o ejecución de máquina virtual de Windows de IaaS de Azure mediante comandos de CLI, Hola siguientes:

1. directivas de acceso de tooset en el almacén de claves de hello:
   * Conjunto hello **EnabledForDiskEncryption** marca:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Conjunto de permisos tooAzure AD aplicación toowrite secretos tooyour almacén de claves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. cifrado de tooenable en una máquina virtual existente o se está ejecutando:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. estado de cifrado de tooget:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. cifrado de tooenable en una nueva máquina virtual de un VHD cifrado, Hola utilice parámetros con hello siguientes `azure vm create` comando:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Habilitación del cifrado en una máquina virtual IaaS con Linux existente o en ejecución en Azure
Puede habilitar el cifrado de disco en una VM de Linux IaaS existente o se está ejecutando en Azure mediante el uso de hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Haga clic en **implementar tooAzure** en la plantilla de hello inicio rápido de Azure, especifique la configuración de cifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.

2. Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en hello existente o ejecuta VM de IaaS.

Hello en la tabla siguiente enumera los parámetros de plantilla de administrador de recursos existente o máquinas virtuales que usan un identificador de cliente de Azure AD en ejecución:

| Parámetro | Descripción |
| --- | --- |
| AADClientID | Id. de cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos toohello el almacén de claves. |
| AADClientSecret | Secreto del cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos tooyour el almacén de claves. |
| keyVaultName | Nombre de clave de hello almacén que BitLocker se debe cargar la clave en hello. Puede obtenerlo mediante el cmdlet de hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | Dirección URL de clave de cifrado de claves de Hola que es usado tooencrypt hello genera la clave de BitLocker. Este parámetro es opcional si selecciona **nokek** en lista de hello UseExistingKek de lista desplegable. Si selecciona **kek** en la lista desplegable UseExistingKek hello, debe escribir hello _keyEncryptionKeyURL_ valor. |
| volumeType | Tipo de volumen que se realiza la operación de cifrado de hello en. Los valores válidos admitidos son _SO_ o _All_ (para RHEL 7.2, CentOS 7.2 y Ubuntu 16.04) y _Data_ (para todas las otras distribuciones). |
| sequenceVersion | Versión de la secuencia de hello operación de BitLocker. Incrementar este número de versión cada vez que se realiza una operación de cifrado del disco en hello misma máquina virtual. |
| vmName | Nombre de máquina virtual que Hola operación de cifrado de hello es toobe realizada en. |
| passPhrase | Escriba una frase de contraseña segura como clave de cifrado de datos de Hola. |

> [!NOTE]
> _KeyEncryptionKeyURL_ es un parámetro opcional. Puede aportar tu propia clave de cifrado de KEK toofurther proteger Hola datos (frase de contraseña secreta) en el almacén de claves.

#### <a name="cli-commands"></a>Comandos de la CLI
Puede habilitar el cifrado de disco en el disco duro virtual cifrado mediante la instalación y uso de hello [comando de CLI](../cli-install-nodejs.md). cifrado de tooenable ejecutan las máquinas virtuales de Linux de IaaS en Azure mediante comandos CLI, o existente Hola siguientes:

1. Establecer directivas de acceso en el almacén de claves de hello:

 * Conjunto hello **EnabledForDiskEncryption** marca:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * Conjunto de permisos tooAzure AD aplicación toowrite secretos tooyour almacén de claves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. cifrado de tooenable en una máquina virtual existente o se está ejecutando:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Obtenga el estado de cifrado:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. cifrado de tooenable en una nueva máquina virtual de un VHD cifrado, Hola utilice parámetros con hello siguientes `azure vm create` comando:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Obtener el estado de cifrado de Hola de una VM de IaaS cifrados
Puede obtener el estado de cifrado de hello mediante el Administrador de recursos de Azure, [cmdlets de PowerShell](/powershell/azure/overview), o comandos de CLI. Hola las secciones siguientes explica cómo toouse Hola portal de Azure clásico y tooget de comandos CLI Hola estado de cifrado.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Obtener estado de cifrado de Hola de una máquina virtual de Windows cifrados mediante el Administrador de recursos de Azure
Puede obtener estado de cifrado de Hola de hello IaaS VM de Azure Resource Manager haciendo Hola siguiente:

1. Inicie sesión en toohello [portal de Azure clásico](https://portal.azure.com/)y, a continuación, haga clic en **máquinas virtuales** en el panel izquierdo de hello toosee una vista resumida de las máquinas virtuales de hello en su suscripción. Puede filtrar la vista máquinas virtuales Hola seleccionando el nombre de la suscripción de Hola Hola **suscripción** lista desplegable.

2. En parte superior de Hola de hello **máquinas virtuales** página, haga clic en **columnas**.

3. En hello **elegir columna** hoja, seleccione **cifrado del disco**y, a continuación, haga clic en **actualización**. Debería ver estado de cifrado de hello cifrado del disco columna mostrando hello _habilitado_ o _no habilitado_ para cada máquina virtual, como se muestra en hello figura siguiente:

 ![Microsoft Antimalware en Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Obtener el estado de cifrado de Hola de una VM de IaaS (Windows o Linux) cifrada mediante cmdlet de PowerShell de cifrado del disco de Hola
Puede obtener estado de cifrado de Hola de hello IaaS VM del cmdlet de PowerShell de cifrado del disco de hello `Get-AzureRmVMDiskEncryptionStatus`. configuración de cifrado de hello tooget para la máquina virtual, escriba la siguiente de hello:

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

Puede inspeccionar la salida de hello de _AzureRmVMDiskEncryptionStatus Get_ para el cifrado de clave las direcciones URL.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Hola OSVolumeEncrypted y valores de configuración de DataVolumesEncrypted se establecen too_Encrypted_, que muestra que los volúmenes se cifran mediante el cifrado del disco de Azure. Para obtener información acerca de cómo habilitar el cifrado con cifrado de disco de Azure mediante el uso de cmdlets de PowerShell, vea las entradas de blog hello [explorar el cifrado del disco de Azure con PowerShell de Azure, parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) y [explorar cifrado del disco de Azure con Azure PowerShell, parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> En máquinas virtuales de Linux, toma tres minutos toofour hello `Get-AzureRmVMDiskEncryptionStatus` estado de cifrado de cmdlet tooreport Hola.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Obtener el estado de cifrado de Hola de hello IaaS VM de comando de CLI de cifrado del disco de Hola
Puede obtener estado de cifrado de Hola de hello IaaS VM mediante el uso de comandos CLI de cifrado del disco hello `azure vm show-disk-encryption-status`. configuración de cifrado de hello tooget para la máquina virtual, escriba la sesión de CLI de Azure:

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Deshabilitación del cifrado en máquinas virtuales IaaS con Windows en ejecución
Puede deshabilitar el cifrado en una ejecución de Windows o Linux VM de IaaS a través de la plantilla de administrador de recursos de cifrado de disco de Azure de Hola o los cmdlets de PowerShell y especificar la configuración de descifrado de Hola.

##### <a name="windows-vm"></a>Máquina virtual de Windows
paso de deshabilitar cifrado de Hello deshabilita el cifrado de hello SO, volumen de datos de Hola o ambos en hello ejecutando la máquina virtual de IaaS de Windows. No se puede deshabilitar el volumen del sistema operativo de Hola y dejar cifradas de volumen de datos de Hola. Cuando se realiza el paso de cifrado de la deshabilitación de hello, modelo de implementación clásica Azure Hola actualiza el modelo de servicio VM de Hola y Hola VM de IaaS de Windows se marca descifrada. contenido de Hola de hello VM ya no se cifra en reposo. descifrado de Hello no elimina la clave hello y el almacén de claves de cifrado (claves de cifrado de BitLocker para Windows y la frase de contraseña de Linux).

##### <a name="linux-vm"></a>Máquina virtual de Linux
paso de deshabilitar cifrado de Hello deshabilita el cifrado del volumen de datos de hello en hello ejecutando la máquina virtual de IaaS de Linux. Este paso solo funciona si el disco del sistema operativo de hello no está cifrado.

> [!NOTE]
> No se permite deshabilitar el cifrado en el disco del sistema operativo de hello en máquinas virtuales de Linux.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Deshabilitado del cifrado en una máquina virtual IaaS existente o en ejecución
Puede deshabilitar el cifrado de disco en la ejecución de máquinas virtuales de IaaS de Windows mediante el uso de hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. En la plantilla de hello Azure inicio rápido, haga clic en **implementar tooAzure**, escriba configuración de descifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.

2. Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en una nueva VM de IaaS.

Para máquinas virtuales de Linux, puede deshabilitar el cifrado mediante el uso de hello [deshabilitar el cifrado en una VM de Linux ejecución](https://aka.ms/decrypt-linuxvm) plantilla.

Hello tabla siguiente enumeran los parámetros de plantilla de administrador de recursos para deshabilitar el cifrado en una VM IaaS en ejecución:

| Parámetro | Descripción |
| --- | --- |
| vmName | Nombre de máquina virtual que Hola operación de cifrado de hello es toobe realizada en.
| volumeType | Tipo de volumen en que se realiza la operación de descifrado. Los valores válidos son _SO_, _Datos_ y _Todo_. No se puede deshabilitar el cifrado en la ejecución de volumen de arranque del SO/máquina virtual de IaaS de Windows sin necesidad de deshabilitar el cifrado en hello _datos_ volumen. Tenga en cuenta también que la deshabilitación del cifrado en el disco del sistema operativo de hello no se permite en máquinas virtuales de Linux. |
| sequenceVersion | Versión de la secuencia de hello operación de BitLocker. Incrementar este número de versión cada vez que se realiza una operación de descifrado de disco en hello misma máquina virtual. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Deshabilitado del cifrado en una máquina virtual IaaS existente o en ejecución
cifrado de toodisable en una VM de IaaS existente o se está ejecutando mediante Hola cmdlet de PowerShell, consulte [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). Este cmdlet admite máquinas virtuales Linux y Windows. cifrado de toodisable, instala una extensión en la máquina virtual de Hola. Si hello _nombre_ no se especifica el parámetro, una extensión con el nombre predeterminado de hello _AzureDiskEncryption para máquinas virtuales de Windows_ se crea.

En las máquinas virtuales de Linux, se utiliza hello AzureDiskEncryptionForLinux extensión.

> [!NOTE]
> Este cmdlet reinicia la máquina virtual de Hola.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Habilitar el cifrado en máquinas virtuales IaaS precifradas con el disco administrado de Azure
Usar hello Azure BRAZO del disco administrado plantilla toocreate una VM cifrada desde un disco duro virtual cifrado previamente con la plantilla de hello ARM se encuentra en   
[Crear un nuevo disco administrado cifrado desde un VHD cifrado previamente/blob de almacenamiento] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Habilitar el cifrado en máquinas virtuales IaaS nuevas de Linux con el disco administrado de Azure
Usar hello Azure BRAZO del disco administrado plantilla toocreate en que cifra una nueva máquina virtual de IaaS de Linux con plantilla de ARM Hola ubicado   
[Implementación de RHEL 7.2 con cifrado de disco completo] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Habilitar el cifrado en máquinas virtuales IaaS nuevas de Windows con el disco administrado de Azure
 Usar hello Azure BRAZO del disco administrado plantilla toocreate en que cifra una nueva máquina virtual de IaaS de Linux con plantilla de ARM Hola ubicado   
 [Crear una máquina virtual IaaS de disco administrado cifrado de Windows nueva a partir de una imagen de la galería] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >Es obligatorio toosnapshot y/o copia de seguridad un administrado basadas en disco instancia de máquina virtual fuera de y tooenabling anterior cifrado del disco de Azure.  Puede tomar una instantánea de disco administrado Hola desde el portal de Hola o copia de seguridad de Azure puede utilizarse.  Las copias de seguridad Asegúrese de que una opción de recuperación es posible en caso de hello de cualquier error inesperado durante el cifrado.  Una vez que se realiza una copia de seguridad, cmdlet hello AzureRmVMDiskEncryptionExtension conjunto puede ser usado tooencrypt administrado discos especificando el parámetro - skipVmBackup de hello.  Este comando producirá un error en las máquinas virtuales basadas en un disco administrado hasta que se realice una copia de seguridad y se especifique este parámetro.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Actualización de la configuración del cifrado de una máquina virtual cifrada no premium existente
  Use Hola disco de Azure admitido el cifrado las interfaces existentes para ejecutar máquinas virtuales [cmdlets de PS, plantillas CLI o ARM] tooupdate configuración de cifrado de hello como cliente AAD/secreto, del identificador de clave de cifrado de clave [KEK], clave de cifrado de BitLocker para la máquina virtual de Windows o la frase de contraseña para Configuración de cifrado de actualización de Linux VM etc. Hola solo se admite para las máquinas virtuales respaldadas por el almacenamiento no son premium. NO está admitido para máquinas virtuales respaldadas por Premium Storage.

## <a name="appendix"></a>Anexo
### <a name="connect-tooyour-subscription"></a>Conectar tooyour suscripción
Antes de continuar, revise hello *requisitos previos* sección en este artículo. Después de asegurarse de que se cumplen todos los requisitos previos, conecte tooyour suscripción haciendo Hola siguiente:

1. Iniciar una sesión de PowerShell de Azure e inicie sesión tooyour cuenta de Azure con hello siguiente comando:

    `Login-AzureRmAccount`

2. Si tiene varias suscripciones y desea toospecify una toouse, escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:

    `Get-AzureRmSubscription`

3. suscripción de hello toospecify desea toouse, tipo:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. tooverify que suscripción Hola configurada es correcta, escriba:

    `Get-AzureRmSubscription`

5. Hola tooconfirm cifrado de disco de Azure se instalan cmdlets, tipo:

    `Get-command *diskencryption*`

6. Hola después de salida confirma la instalación de PowerShell de cifrado de disco de Azure de hello:

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Preparación de un VHD con Windows precifrado
secciones Hola siguientes son necesario tooprepare un cifrado previamente VHD de Windows para la implementación como un disco duro virtual cifrado en IaaS de Azure. Utilice Hola información tooprepare y arrancar una máquina virtual de Windows nueva (VHD) en Azure Site Recovery o Azure.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Actualizar grupo Directiva tooallow sin TPM para la protección del sistema operativo
Configuración de directiva de grupo de BitLocker de hello **cifrado de unidad BitLocker**, que encontrará en **directiva de equipo Local** > **configuración del equipo**  >  **Plantillas administrativas** > **componentes de Windows**. Cambiar esta configuración demasiado**unidades de sistema operativo** > **requerir autenticación adicional al iniciar** > **Permitir BitLocker sin un TPM compatible**, tal y como se muestra en hello figura siguiente:

![Microsoft Antimalware en Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>Instalación de componentes de características de BitLocker
Para Windows Server 2012 y versiones posteriores, utilice Hola siguiente comando:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Para Windows Server 2008 R2, utilice Hola siguiente comando:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Prepare el volumen del sistema operativo de Hola para BitLocker mediante el`bdehdcfg`
toocompress Hola partición del sistema operativo y preparar la máquina de Hola para BitLocker, ejecute el siguiente comando de hello:

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>Proteger el volumen del sistema operativo hello mediante el uso de BitLocker
Hola de uso [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) cifrado de tooenable de comando en el volumen de arranque de hello mediante un protector de clave externo. Colocar la clave externa de hello (archivo .bek) en unidad externa de Hola o volumen. Cifrado está habilitado en el volumen de arranque o de sistema de hello después del reinicio siguiente Hola.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> Preparar Hola VM con datos o recursos independientes VHD para obtener la clave externa de hello mediante BitLocker.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Cifrado de la unidad del sistema operativo en una máquina virtual con Linux en ejecución
Cifrado de una unidad de sistema operativo en una ejecución VM de Linux es compatible con hello siguientes distribuciones:

* RHEL 7.2
* CentOS 7.2
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>Requisitos previos para el cifrado de disco del sistema operativo

* Hola VM se debe crear desde una imagen de Marketplace hello en el Administrador de recursos de Azure.
* La máquina virtual de Azure con al menos 4 GB de RAM (el tamaño recomendado es 7 GB).
* (Para RHEL y CentOS) Deshabilite SELinux. toodisable SELinux, vea "4.4.2. Deshabilitar SELinux"Hola [Guía del administrador y del usuario de SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) en hello máquina virtual.
* Después de deshabilitar SELinux, reinicie Hola VM al menos una vez.

##### <a name="steps"></a>Pasos
1. Crear una máquina virtual mediante una de las distribuciones de hello especificadas anteriormente.

 Para CentOS 7.2, se admite el cifrado de disco del sistema operativo a través de una imagen especial. toouse esta imagen, especifique "7.2n" como Hola SKU cuando creas Hola VM:
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Configure las necesidades tooyour VM correspondiente Hola. Si va a tooencrypt todas las unidades de hello (sistema operativo + datos), las unidades de datos de hello necesitan toobe especificado y pueda montar de/etc/fstab.

 > [!NOTE]
 > Usar UUID =... toospecify unidades de datos en/etcetera/fstab en lugar de especificar el nombre de dispositivo de bloque de hello (por ejemplo, / dev/sdb1). Durante el cifrado, cambia el orden de Hola de unidades en hello máquina virtual. Si la máquina virtual se basa en un orden específico de dispositivos de bloque, se producirá un error toomount tras su cifrado.

3. Cierre la sesión de las sesiones SSH de Hola.

4. Hola tooencrypt OS, especifique volumeType como **todos los** o **OS** cuando se [habilitar el cifrado](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Todos los procesos de espacio de usuario que no se ejecutan como servicios `systemd` deben terminarse con `SIGKILL`. Reinicie Hola máquina virtual. Al habilitar el cifrado del disco de sistema operativo en una máquina virtual en ejecución, tenga en cuenta el tiempo de inactividad de la máquina virtual.

5. Periódicamente supervisar el progreso de Hola de cifrado mediante el uso de instrucciones de Hola Hola [próxima sección](#monitoring-os-encryption-progress).

6. Después de Get-AzureRmVmDiskEncryptionStatus muestra "VMRestartPending", reinicie la máquina virtual debe iniciar sesión en tooit o mediante el portal de hello, PowerShell o CLI.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
Antes de reiniciar, se recomienda que guarde [diagnósticos de arranque](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) de hello máquina virtual.

#### <a name="monitoring-os-encryption-progress"></a>Supervisión del progreso de cifrado del sistema operativo
Hay tres maneras de supervisar el progreso de cifrado del sistema operativo:

* Hola de uso `Get-AzureRmVmDiskEncryptionStatus` cmdlet e inspeccionar el campo de Hola ProgressMessage:
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 Después de hello VM llega "Iniciarlo el cifrado de disco del sistema operativo", que tarda aproximadamente 40 minutos too50 en un almacenamiento Premium copia de máquina virtual.

 Debido al [problema 388](https://github.com/Azure/WALinuxAgent/issues/388) de WALinuxAgent, `OsVolumeEncrypted` y `DataVolumesEncrypted` se muestran como `Unknown` en algunas distribuciones. En WALinuxAgent versión 2.1.5 y versiones posteriores, este problema se ha corregido automáticamente. Si ve `Unknown` en la salida de hello, puede comprobar el estado de cifrado del disco mediante Hola Explorador de recursos de Azure.

 Vaya demasiado[Explorador de recursos de Azure](https://resources.azure.com/)y, a continuación, expanda esta jerarquía en el panel de selección de Hola a izquierda:

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 Hola InstanceView, desplácese hacia abajo de estado de cifrado de hello toosee de las unidades de disco.

 ![Vista de instancia de máquina virtual](./media/azure-security-disk-encryption/vm-instanceview.png)

* Fíjese en los [diagnósticos de arranque](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). Mensajes de Hola extensión de fachada deben agregarse como prefijo `[AzureDiskEncryption]`.

* Inicie sesión en toohello máquina virtual a través de SSH y obtener registros de extensión de Hola desde:

    /var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 Se recomienda no iniciar sesión toohello VM durante el cifrado del sistema operativo en curso. Copiar registros de hello solo cuando hello otros dos métodos han fallado.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Preparación de un VHD con Linux precifrado
##### <a name="ubuntu-16"></a>Ubuntu 16
Configurar el cifrado durante la instalación de la distribución de hello haciendo Hola siguiente:

1. Seleccione **configurar los volúmenes cifrados** al realizar particiones de los discos de Hola.

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Cree una unidad de arranque independiente, que no debe estar cifrada. Cifre la unidad raíz.

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Proporcione una frase de contraseña. Se trata de una frase de contraseña de Hola que cargar el almacén de claves toohello.

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Finalice la partición.

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Cuando se arranca Hola VM y se pide una frase de contraseña, utilice Hola frase de contraseña que proporcionó en el paso 3.

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Preparar Hola VM para cargar en Azure mediante [estas instrucciones](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). Aún no ejecutado último paso de hello (Hola desaprovisionamiento VM).

Configurar cifrado toowork con Azure haciendo Hola siguiente:

1. Cree un archivo bajo /usr/local/sbin/azure_crypt_key.sh, con contenido de Hola Hola siguiente secuencia de comandos. Preste atención toohello KeyFileName, porque es el nombre de archivo de frase de contraseña de hello usa Azure.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Cambiar la configuración de cifrado de hello en */etcetera/crypttab*. Debería ser parecido a este:
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Si está editando *azure_crypt_key.sh* en Windows y se copian tooLinux, ejecute `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Agregue permisos ejecutable toohello script:
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Edite */etc/initramfs-tools/modules* anexando líneas:
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Ejecutar `update-initramfs -u -k all` tooupdate Hola initramfs toomake Hola `keyscript` surta efecto.

7. Ahora puede cancelar el aprovisionamiento de hello máquina virtual.

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Continuar paso siguiente toohello y [cargar el disco duro virtual](#upload-encrypted-vhd-to-an-azure-storage-account) en Azure.

##### <a name="opensuse-132"></a>openSUSE 13.2
cifrado de tooconfigure durante la instalación de la distribución de hello, Hola siguientes:
1. Para crear particiones en discos de hello, seleccione **cifrar el grupo de volúmenes**y, a continuación, escriba una contraseña. Se trata de una contraseña de Hola que va a cargar el almacén de claves tooyour.

 ![Instalación de openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Hola máquina virtual con la contraseña de inicio.

 ![Instalación de openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Preparar Hola VM para cargar tooAzure siguiendo las instrucciones de hello en [preparar una máquina virtual SLES o openSUSE para Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). Aún no ejecutado último paso de hello (Hola desaprovisionamiento VM).

tooconfigure toowork de cifrado con Azure, Hola siguientes:
1. Editar /etc/dracut.conf hello y agregue Hola después de línea:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Comenta estas líneas end Hola de hello archivo /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Anexar Hola siguiente línea al principio de Hola de hello archivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:
 ```
    DRACUT_SYSTEMD=0
 ```
Y cambie todas las apariciones de:
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
a:
```
    if [ 1 ]; then
```
4. Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh y anexe demasiado "dispositivo de abrir LUKS #":

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Ejecutar `/usr/sbin/dracut -f -v` tooupdate Hola initrd.

6. Ahora puede cancelar el aprovisionamiento Hola VM y [cargar el disco duro virtual](#upload-encrypted-vhd-to-an-azure-storage-account) en Azure.

##### <a name="centos-7"></a>CentOS 7
cifrado de tooconfigure durante la instalación de la distribución de hello, Hola siguientes:
1. Seleccione **Encrypt my data** (Cifrar mis datos) al crear particiones en discos.

 ![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Asegúrese de que **Encrypt** (Cifrar) está seleccionado para la partición raíz.

 ![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Proporcione una frase de contraseña. Se trata de una frase de contraseña de Hola que va a cargar el almacén de claves tooyour.

 ![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Cuando se arranca Hola VM y se pide una frase de contraseña, utilice Hola frase de contraseña que proporcionó en el paso 3.

 ![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Preparar Hola VM para cargar en Azure mediante el uso de instrucciones de "CentOS 7.0 +" hello en [preparar una máquina virtual CentOS para Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). Aún no ejecutado último paso de hello (Hola desaprovisionamiento VM).

6. Ahora puede cancelar el aprovisionamiento Hola VM y [cargar el disco duro virtual](#upload-encrypted-vhd-to-an-azure-storage-account) en Azure.

tooconfigure toowork de cifrado con Azure, Hola siguientes:

1. Editar /etc/dracut.conf hello y agregue Hola después de línea:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Comenta estas líneas end Hola de hello archivo /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Anexar Hola siguiente línea al principio de Hola de hello archivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:
```
    DRACUT_SYSTEMD=0
```
Y cambie todas las apariciones de:
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
to
```
    if [ 1 ]; then
```
4. Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh y anexe esto después de hello "dispositivo de abrir LUKS #":
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Ejecute hello "/ usr/sbin/dracut - f - v" tooupdate Hola initrd.

![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Cargar cifrado cuenta de almacenamiento de Azure de tooan de disco duro virtual
Una vez que se habilita el cifrado de BitLocker o Crypt DM, Hola local cifra cuenta de almacenamiento de disco duro virtual necesidades toobe cargado tooyour.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Cargar el secreto de cifrado del disco de Hola para hello cifrado previamente VM tooyour almacén de claves
secreto de cifrado del disco de Hola que ha obtenido previamente se debe cargar como un secreto en el almacén de claves. almacén de claves de Hello necesita toohave cifrado del disco y permisos habilitados para el cliente de Azure AD.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>Secreto del cifrado de disco no cifrado con una KEK
tooset copias de seguridad secreto hello en el almacén de claves, use [AzureKeyVaultSecret conjunto](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). Si tiene una máquina virtual de Windows, archivo de hello bek se codifica como una cadena base64 y, a continuación, cargar el almacén de claves tooyour con hello `Set-AzureKeyVaultSecret` cmdlet. Para Linux, la frase de contraseña de Hola se codifica como una cadena base64 y, a continuación, carga el almacén de claves toohello. Además, asegúrese de que ese Hola después de las etiquetas se establecen cuando se crea el secreto de hello en el almacén de claves de Hola.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Hola de uso `$secretUrl` en el paso siguiente de Hola para [adjuntando el disco Hola OS sin usar KEK](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>Secreto del cifrado de disco cifrado con una KEK
Antes de cargar el almacén de claves secretas toohello hello, si lo desea puede cifrar mediante una clave de cifrado de claves. Ajuste de Hola de uso [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst cifrar secreto Hola con clave de cifrado de claves de Hola. resultado de esta operación de encapsulado de Hello es una cadena de dirección URL codificada en base64, que, a continuación, puede cargar como un secreto mediante hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Use `$KeyEncryptionKey` y `$secretUrl` en el paso siguiente de Hola para [adjuntando el disco Hola SO mediante KEK](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>Especificación de una dirección URL de secreto al adjuntar un disco del sistema operativo
#### <a name="without-using-a-kek"></a>Sin utilizar una KEK
Mientras que va a adjuntar disco de SO hello, necesita toopass `$secretUrl`. dirección URL de Hola se generó en la sección de "secreto de cifrado del disco que no se cifran con una KEK" Hola.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>Uso de una KEK
Cuando conecte un disco de SO hello, pasar `$KeyEncryptionKey` y `$secretUrl`. dirección URL de Hola se generó en la sección de "secreto de cifrado del disco que no se cifran con una KEK" Hola.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Descargar esta guía
Puede descargar esta guía de hello [Galería de TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Para obtener más información
[Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0) (Exploración de Azure Disk Encryption con Azure PowerShell - Parte 1)  
[Exploración de Azure Disk Encryption con Azure PowerShell, parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
