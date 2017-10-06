---
title: "requisitos previos de implementación del Kit de desarrollo de la pila de aaaAzure | Documentos de Microsoft"
description: Ver los requisitos de entorno y hardware de hello para el Kit de desarrollo de pila de Azure (operador de nube).
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 32a21d9b-ee42-417d-8e54-98a7f90f7311
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/11/2017
ms.author: erikje
ms.openlocfilehash: 126c851651354b6f3d61c4627ab0c1de9da12ba9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-deployment-prerequisites"></a>Requisitos previos de implementación de Azure Stack
Antes de implementar Azure pila [Kit de desarrollo de](azure-stack-poc.md), asegúrese de que el equipo cumple Hola según los requisitos:


## <a name="hardware"></a>Hardware
| Componente | Mínima | Recomendado |
| --- | --- | --- |
| Unidades de disco: sistema operativo |Un disco del sistema operativo con un mínimo de 200 GB disponibles para la partición del sistema (SSD o HDD) |Un disco del sistema operativo con un mínimo de 200 GB disponibles para la partición del sistema (SSD o HDD) |
| Unidades de disco: datos generales del kit de desarrollo* |Cuatro discos. Cada disco proporciona un mínimo de 140 GB de capacidad (SSD o HDD). Se utilizarán todos los discos disponibles. |Cuatro discos. Cada disco proporciona un mínimo de 250 GB de capacidad (SSD o HDD). Se utilizarán todos los discos disponibles. |
| Proceso: CPU |Socket dual: 12 núcleos físicos (total) |Socket dual: 16 núcleos físicos (total) |
| Proceso: memoria |96 GB de RAM |128 GB de RAM (Esto es proveedores de recursos de hello toosupport mínimo PaaS).|
| Proceso: BIOS |Hyper-V habilitado (con compatibilidad para SLAT) |Hyper-V habilitado (con compatibilidad para SLAT) |
| Red: NIC |Certificación de Windows Server 2012 R2 necesaria para NIC; no se necesitan características especializadas |Certificación de Windows Server 2012 R2 necesaria para NIC; no se necesitan características especializadas |
| Certificación del logotipo de hardware |[Certificado para Windows Server 2012 R2](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |[Certificado para Windows Server 2012 R2](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |

\*Necesitará más esta capacidad opción recomendada si piensa sobre cómo agregar muchos hello [elementos del marketplace](azure-stack-download-azure-marketplace-item.md) de Azure.

**Configuración de unidad de disco de datos:** Hola a todos los datos de unidades de disco deben ser del mismo tipo (todas unidades SAS o todas unidades SATA) y capacidad. Si se utilizan unidades de disco SAS, las unidades de disco de hello debe estar conectadas a través de una ruta de acceso única (no se indica ningún MPIO, compatibilidad con múltiples rutas de acceso).

**Opciones de configuración HBA**

* (Opción preferida) HBA simple
* HBA RAID: el adaptador debe configurarse en modo "pass through"
* HBA de RAID: los discos deben configurarse como único disco, RAID-0

**Combinaciones de tipos de medios y bus admitidas**

* SATA HDD
* SAS HDD
* RAID HDD
* SSD de RAID (si el tipo de medio de hello es desconocido o no se especifica\*)
* SATA SSD + SATA HDD
* SAS SSD + SAS HDD

\*Controladoras RAID sin la funcionalidad de acceso directo no reconocen el tipo de medio de Hola. Estos controladores marcarán tanto HDD como SSD como No especificado. En ese caso, Hola SSD se utilizará como el almacenamiento persistente en lugar de almacenamiento en caché de los dispositivos. Por lo tanto, puede implementar el kit de desarrollo de hello en los SSD.

**HBA de ejemplo**: LSI 9207 8i, LSI-9300-8i o LSI-9265-8i en modo Paso a través

Están disponibles configuraciones de OEM de ejemplo.

## <a name="operating-system"></a>Sistema operativos
|  | **Requisitos** |
| --- | --- |
| **Versión del SO.** |Windows Server 2012 R2 o posterior. versión del sistema operativo Hello no es crítica antes de inicia la implementación de hello, podrá arrancar equipo de host de hello en el disco duro virtual que se incluye en la instalación de la pila de Azure de Hola Hola. Hola sistema operativo y todas las revisiones necesarias ya están integradas en la imagen de Hola. No use cualquier tooactivate de claves que se usan las instancias de servidor de Windows en el kit de desarrollo de Hola. |

## <a name="deployment-requirements-check-tool"></a>Herramienta de comprobación de requisitos de implementación
Después de instalar el sistema operativo de hello, puede usar hello [Comprobador de implementación para la pila de Azure](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b) tooconfirm que el hardware cumple todos los requisitos de Hola.

## <a name="account-requirements"></a>Requisitos de cuenta
Normalmente, implementar el kit de desarrollo de hello con conectividad a internet, donde puede conectarse tooMicrosoft Azure. En este caso, debe configurar un kit de desarrollo de Azure Active Directory (Azure AD) cuenta toodeploy Hola.

Si su entorno no está conectado toohello internet, o no desea toouse Azure AD, puede implementar la pila de Azure mediante los servicios de federación de Active Directory (AD FS). kit de desarrollo de Hello incluye sus propias instancias de AD FS y los servicios de dominio de Active Directory. Si implementa mediante el uso de esta opción, no tienes tooset cuentas antes de tiempo.

>[!NOTE]
Si implementa con opción de hello AD FS, debe volver a implementar Azure pila tooswitch tooAzure AD.

### <a name="azure-active-directory-accounts"></a>Cuentas de Azure Active Directory
toodeploy pila de Azure mediante una cuenta de Azure AD, debe preparar una cuenta de Azure AD antes de ejecutar el script de PowerShell de implementación de Hola. Esta cuenta se convierte en hello administrador Global para el inquilino de Azure AD Hola. Ha utilizado tooprovision y delegado aplicaciones y entidades de servicio para todos los servicios de Azure pila que interactúan con Azure Active Directory y la API Graph. También sirve como propietario de Hola de suscripción de proveedor predeterminado de hello (que puede cambiar más adelante). Puede registrar en el portal del administrador del sistema de tooyour pila de Azure mediante el uso de esta cuenta.

1. Crear una cuenta de Azure AD que es administrador de directorios de Hola para al menos un anuncio de Azure. Si ya tiene una, puede usarla. En caso contrario, puede crear una de forma gratuita en [http://azure.microsoft.com/en-us/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (en China, visite <http://go.microsoft.com/fwlink/?LinkID=717821> en su lugar). Si tiene previsto toolater [registrar pila de Azure con Azure](azure-stack-register.md), también debe tener una suscripción en el recién creado cuenta.
   
    Guardar estas credenciales para su uso en el paso 6 de [implementar el kit de desarrollo de hello](azure-stack-run-powershell-script.md#deploy-the-development-kit). Los *administradores de servicios* pueden configurar y administrar recursos en la nube, cuentas de usuario, planes de inquilinos, cuotas y precios. En el portal de hello, puede crear nubes de sitios Web, nubes privadas de máquinas virtuales, crear planes y administrar las suscripciones de usuario.
2. [Crear](azure-stack-add-new-user-aad.md) al menos una cuenta para que puede iniciar sesión en el kit de desarrollo de toohello como un inquilino.
   
   | **Cuenta de Azure Active Directory** | **¿Admitida?** |
   | --- | --- |
   | Cuenta profesional o educativa con una suscripción de Azure pública válida |Sí |
   | Cuenta de Microsoft con una suscripción de Azure pública válida |Sí |
   | Cuenta profesional o educativa con una suscripción de Azure China válida |Sí |
   | Cuenta profesional o educativa con una suscripción de Azure Gobierno de Estados Unidos válida |Sí |

## <a name="network"></a>Red
### <a name="switch"></a>Switch
Un puerto disponible en un conmutador de máquina de kit de desarrollo de Hola.  

máquina de kit de desarrollo de Hello es compatible con el puerto de acceso de conexión tooa conmutador o puerto de tronco. No hay funciones especializadas son obligatorios en conmutador Hola. Si está utilizando un puerto de tronco o si necesita tooconfigure un identificador de VLAN, tendrá que tooprovide Hola Id. de VLAN como un parámetro de implementación. Puede ver ejemplos de hello [lista de parámetros de implementación](azure-stack-run-powershell-script.md).

### <a name="subnet"></a>Subred
No se conectan kit de desarrollo de hello máquina toohello siguientes:

* 192.168.200.0/24
* 192.168.100.0/27
* 192.168.101.0/26
* 192.168.102.0/24
* 192.168.103.0/25
* 192.168.104.0/25

Estas subredes están reservadas para las redes internas en el entorno del kit de desarrollo de Hola Hola.

### <a name="ipv4ipv6"></a>IPv4/IPv6
Se admite solo IPv4. No se pueden crear redes IPv6.

### <a name="dhcp"></a>DHCP
Asegúrese de que hay un servidor DHCP disponible en la red de Hola que Hola A que NIC se conecta. Si DHCP no está disponible, debe preparar una red de IPv4 estática adicional además de hello utilizado por el host. Debe proporcionar esa dirección IP y la puerta de enlace como parámetro de implementación. Puede ver ejemplos de hello [lista de parámetros de implementación](azure-stack-run-powershell-script.md).

### <a name="internet-access"></a>Acceso a Internet
Pila de Azure requiere toohello de acceso a Internet, ya sea directamente o a través de un proxy transparente. Pila de Azure no admite la configuración de Hola de un tooenable de proxy web acceso a Internet. IP de host de Hola y Hola nueva IP asignan toohello que bgpnat01 MAS (mediante DHCP o direcciones IP estáticas) debe ser capaz de tooaccess Internet. Usan los puertos 80 y 443 con hello graph.windows.net y login.microsoftonline.com dominios.

## <a name="telemetry"></a>Telemetría

La telemetría nos ayuda a dar forma a versiones futuras de Azure Stack. Nos permite responder rápidamente toofeedback, proporciona características nuevas y mejorar la calidad. Microsoft Azure Stack incluye Windows Server 2016 y SQL Server 2014. Ninguno de estos productos se cambian en la configuración predeterminada y ambos se describen en hello declaración de privacidad de Microsoft Enterprise. Pila de Azure también contiene software de código abierto que no ha sido modificado toosend telemetría tooMicrosoft. Estos son algunos ejemplos de datos de telemetría de Azure Stack:

- información de registro de implementación
- cuándo se abre y se cierra una alerta
- número de Hola de recursos de red

flujo de datos de telemetría de toosupport, el puerto 443 (HTTPS) debe estar abierto en la red. punto de conexión de cliente de Hello es https://vortex-win.data.microsoft.com.

Si no desea tooprovide telemetría para la pila de Azure, se puede desactivar en el host de kit de desarrollo de Hola y Hola infraestructura virtual máquinas como se explica a continuación.

### <a name="turn-off-telemetry-on-hello-development-kit-host-optional"></a>Desactiva la telemetría en el host de kit de desarrollo de hello (opcional)

>[!NOTE]
Si desea tooturn desactivar la telemetría para host de kit de desarrollo de hello, debe hacerlo antes de ejecutar el script de implementación de Hola.

Antes de [ejecutar script de Hola asdk installer.ps1]() host del kit de desarrollo de toodeploy hello, arrancar para capturar hello CloudBuilder.vhdx y siguiente ejecución hello secuencia de comandos en una ventana de PowerShell con privilegios elevados:
```powershell
### Get current AllowTelmetry value on DVM Host
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
### Set & Get updated AllowTelemetry value for ASDK-Host 
Set-ItemProperty-Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name "AllowTelemetry" -Value '0'  
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
```

Establecer **AllowTelemetry** too0 desactiva la telemetría para la implementación de Windows y pila de Azure. Solo los eventos de seguridad críticas del sistema operativo de Hola se envían. configuración de Hello controla la telemetría de Windows a través de todos los hosts y máquinas virtuales de infraestructura y es toonew a aplicar los nodos y las máquinas virtuales cuando se producen operaciones de escalado horizontal.


### <a name="turn-off-telemetry-on-hello-infrastructure-virtual-machines-optional"></a>Desactiva la telemetría en máquinas virtuales de infraestructura de hello (opcional)

Después de hello implementación es correcta, ejecute hello siguiente secuencia de comandos en una ventana de PowerShell con privilegios elevados (como Hola AzureStack\AzureStackAdmin usuario) en el host de kit de desarrollo de hello:

```powershell
$AzSVMs= get-vm |  where {$_.Name -like "AzS-*"}
### Show current AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
### Set & Get updated AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {Set-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name "AllowTelemetry" -Value '0'}
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
```

tooconfigure telemetría de SQL Server, vea [cómo tooconfigure SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft).

### <a name="usage-reporting"></a>Informes de uso

A través del registro, la pila de Azure también es tooAzure de información de uso de tooforward configurado. Los informes de uso se controlan de forma independiente de la telemetría. Puede desactivar los informes cuando de uso [registrar](azure-stack-register.md) mediante script de Hola en Github. Solo un conjunto hello **$reportUsage** parámetro demasiado**$false**.

Datos de uso se da formato como Hola detallada en [tooAzure de datos de uso de informes Azure pila](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting). No se cobra a los usuarios de Azure Stack Development Kit. Esta funcionalidad se incluye en el kit de desarrollo de Hola para que pueda probar toosee funcionamiento de informes de uso. 


## <a name="next-steps"></a>Pasos siguientes
[Descargar el paquete de implementación del kit de desarrollo de hello pila de Azure](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

[Implementación de Azure Stack Development Kit](azure-stack-run-powershell-script.md)

