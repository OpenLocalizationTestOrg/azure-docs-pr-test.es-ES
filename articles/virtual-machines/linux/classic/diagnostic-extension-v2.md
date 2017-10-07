---
title: "aaaMonitoring una VM de Linux con una extensión de VM | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola extensión de diagnóstico de Linux toomonitor Hola datos de rendimiento y diagnóstico de una VM de Linux en Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Usar Hola extensión de diagnóstico de Linux toomonitor Hola datos de rendimiento y diagnóstico de una VM de Linux

Este documento describe la versión 2.3 de hello extensión de diagnóstico de Linux.

> [!IMPORTANT]
> Esta versión está en desuso y puede eliminarse en cualquier momento a partir del 30 de junio de 2018. La sustituye la versión 3.0. Para obtener más información, vea hello [documentación con la versión 3.0 de hello extensión de diagnóstico de Linux](../diagnostic-extension.md).

## <a name="introduction"></a>Introducción

(**Nota**: Hola extensión de diagnóstico de Linux es código abierto en [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) donde se publica información más reciente de hello en extensión de Hola por primera vez. Es recomendable hello toocheck [página de GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) primer.)

Hola extensión de diagnóstico de Linux ayuda a un Hola de monitor de usuario máquinas virtuales de Linux que se ejecutan en Microsoft Azure. Tiene Hola siguientes capacidades:

* Recopila y carga la información de rendimiento del sistema de Hola de tabla de almacenamiento de información del usuario de hello VM de Linux toohello, incluida la información de diagnóstico y registro del sistema.
* Permite a los usuarios toocustomize hello las métricas de datos que se recopilan y cargan.
* Permite que los usuarios tooupload registro especificado archivos tooa almacenamiento designadas tabla.

En la versión actual de hello 2.3, datos de hello incluyen:

* Todos los registros de Linux Rsyslog, incluidos los relacionados con el sistema, la seguridad y las aplicaciones.
* Todos los datos del sistema que se especifica en [sitio de soluciones de plataforma cruzada de System Center de hello](https://scx.codeplex.com/wikipage?title=xplatproviders).
* Archivos de registro especificados por el usuario.

Esta extensión funciona con hello clásico y modelos de implementación del Administrador de recursos.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Versión actual de la extensión de Hola y degradación de las versiones anteriores

Hola la versión más reciente de extensión de hello es **2.3**, y **cualquier versión anterior (2.0, 2.1 y 2.2) se en desuso y se anuló la publicación al final de este año (2017)**. Si instaló Hola extensión de diagnóstico de Linux con la actualización de versión secundaria automática deshabilitada, se recomienda encarecidamente que desinstalar la extensión de Hola y vuelva a instalarlo con la actualización de versión secundaria automática habilitada. En clásico (ASM) máquinas virtuales, puede conseguirlo mediante la especificación de '2.*' como versión de Hola si va a instalar la extensión de Hola a través de Azure XPLAT CLI o Powershell. En máquinas virtuales de ARM, puede conseguirlo mediante la inclusión ' "autoUpgradeMinorVersion": true' en la plantilla de implementación de VM de Hola. Además, cualquier instalación nueva de extensión de hello debe tener versión secundaria de hello automática Actualizar opción activada.

## <a name="enable-hello-extension"></a>Habilitar la extensión de Hola

Puede habilitar esta extensión mediante hello [portal de Azure](https://portal.azure.com/#), Azure PowerShell o secuencias de comandos de CLI de Azure.

tooview y configurar el sistema de Hola y los datos de rendimiento directamente de hello portal de Azure, siguen [estos pasos en el blog de Azure de hello](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

En este artículo se centra en cómo tooenable y configurar la extensión de Hola mediante comandos de CLI de Azure. Esto le permite tooread y ver los datos de hello directamente desde la tabla de almacenamiento de Hola.

Tenga en cuenta que los métodos de configuración de Hola que se describen aquí no funcionarán para hello portal de Azure. tooview y configurar datos de rendimiento del sistema y de saludo directamente desde el portal de Azure hello, extensión de hello debe estar habilitada a través del portal de Hola.

## <a name="prerequisites"></a>Requisitos previos

* **Versión 2.0.6 o posterior del agente Linux de Azure**.

  Tenga en cuenta que la mayoría de las imágenes de la galería de máquina virtual Linux de Azure incluyen la versión 2.0.6 o posterior. Puede ejecutar **WAAgent-versión** tooconfirm qué versión está instalada en hello máquina virtual. Si Hola VM está ejecutando una versión anterior a 2.0.6, puede seguir [estas instrucciones en GitHub](https://github.com/Azure/WALinuxAgent "instrucciones") tooupdate lo.
* **CLI de Azure** Siga [esta guía para la instalación de CLI](../../../cli-install-nodejs.md) tooset el entorno de CLI de Azure de hello en su equipo. Después de instalar la CLI de Azure, puede usar hello **azure** línea de comandos desde las interfaz de línea de comandos (intensiva de errores, Terminal o símbolo) tooaccess hello Azure comandos de CLI. Por ejemplo:

  * Ejecute **azure vm extension set --help** para obtener información de ayuda detallada.
  * Ejecutar **inicio de sesión azure** toosign en tooAzure.
  * Ejecutar **lista vm de azure** toolist todos Hola máquinas virtuales que tengan en Azure.
* Un almacenamiento cuenta toostore Hola de datos. Necesitará un nombre de cuenta de almacenamiento que creó anteriormente y un almacén de tooyour de datos de access tooupload clave Hola.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Usar hello Azure CLI comando tooenable hello extensión de diagnóstico de Linux

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Escenario 1. Habilitar la extensión de hello con conjunto de datos predeterminado de Hola

En la versión 2.3 o posterior, los datos de valor predeterminado de Hola que se van a recopilar incluyen:

* Todas la información de Rsyslog, incluidos los registros del sistema, seguridad y aplicaciones.  
* Un conjunto de datos del sistema base. Tenga en cuenta que Hola conjunto de datos completo se describe en hello [sitio de soluciones de plataforma cruzada de System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Si desea que tooenable datos adicionales, continúe con los pasos de hello en los escenarios 2 y 3.

Paso 1. Cree un archivo denominado PrivateConfig.json con hello siguiente contenido:

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

Paso 2: Ejecute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Escenario 2. Personalizar las métricas de supervisión de rendimiento de Hola

Esta sección describe cómo toocustomize Hola rendimiento y la tabla de datos de diagnóstico.

Paso 1. Cree un archivo denominado PrivateConfig.json con contenido de Hola que se describe en el escenario 1. Cree también un archivo llamado "PublicConfig.json". Especificar datos determinado de Hola que desee toocollect.

Para todos los proveedores y las variables, hacen referencia a hello [sitio de soluciones de plataforma cruzada de System Center](https://scx.codeplex.com/wikipage?title=xplatproviders). Puede tener varias consultas y almacenarlas en varias tablas mediante la anexión de secuencia de comandos de más consultas toohello.

De forma predeterminada, siempre se recopila datos Rsyslog Hola.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


Paso 2: Ejecute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

### <a name="scenario-3-upload-your-own-log-files"></a>Escenario 3. Carga de sus propios archivos de registro

Esta sección describe cómo tooyour cuenta de almacenamiento de los archivos de toocollect y la carga de registro concreto. Necesita toospecify ambos Hola ruta de acceso tooyour registro hello y archivo de nombre de tabla Hola donde desea toostore el registro. Puede crear varios archivos de registro mediante la adición de varios toohello de script de las entradas de archivo o tabla.

Paso 1. Cree un archivo denominado PrivateConfig.json con contenido de Hola que se describe en el escenario 1. A continuación, crea otro archivo denominado PublicConfig.json con hello siguiente contenido:

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

Paso 2: Ejecute `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.

Tenga en cuenta que con esta configuración en hello extensión versiones anteriores too2.3, todos los registros que se escriban demasiado`/var/log/mysql.err` que puede estar duplicado demasiado`/var/log/syslog` (o `/var/log/messages` según la distribución de Linux de hello) también. Si desea que tooavoid este duplicado en el registro, puede excluir el registro de `local6` registros de instalación en la configuración de rsyslog. Depende de distribución de Linux de hello, pero en un sistema de Ubuntu 14.04 forma Hola archivo toomodify `/etc/rsyslog.d/50-default.conf` y pueden reemplazar línea hello `*.*;auth,authpriv.none -/var/log/syslog` demasiado`*.*;auth,authpriv,local6.none -/var/log/syslog`. Este problema se corregirá en la versión de revisión más reciente de Hola de 2.3 (2.3.9007), por lo que si tiene la extensión de hello versión 2.3, no debería ocurrir este problema. Si todavía existe incluso después de reiniciar la máquina virtual, póngase en contacto con nosotros y Ayúdenos a averiguar por qué no se instala automáticamente la versión más reciente de la revisión de Hola.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Escenario 4. Detener la extensión de Hola de recopilación de registros

Esta sección describe cómo extensión de hello toostop recopilación de registros. Tenga en cuenta que el proceso de agente de supervisión de Hola estará todavía activa y en funcionamiento incluso con este cambio de configuración. Si desea que hello toostop por completo, el proceso de agente de supervisión, puede hacerlo deshabilitando extensión Hola. Hola comando toodisable Hola extensión es `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

Paso 1. Cree un archivo denominado PrivateConfig.json con contenido de Hola que se describe en el escenario 1. Cree otro archivo denominado PublicConfig.json con hello siguiente contenido:

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


Paso 2: Ejecute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

## <a name="review-your-data"></a>Revisión de los datos

Hola datos de rendimiento y diagnóstico se almacenan en una tabla de almacenamiento de Azure. Revisión [cómo toouse almacenamiento de tablas de Azure de Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn cómo tabla tooaccess datos de hello en el almacenamiento de hello mediante secuencias de comandos de CLI de Azure.

Además, puede usar después de datos de saludo de tooaccess de herramientas de interfaz de usuario:

1. Explorador de servidores de Visual Studio. Vaya tooyour cuenta de almacenamiento. Después de hello VM se ejecuta durante aproximadamente cinco minutos, podrá ver tablas predeterminadas de hello cuatro: "LinuxCpu", "LinuxDisk", "LinuxMemory" y "Linuxsyslog". Haga doble clic en datos de saludo tabla nombres tooview Hola.
1. [Explorador de almacenamiento de Azure](https://azurestorageexplorer.codeplex.com/ "Explorador de almacenamiento de Azure").

![imagen](./media/diagnostic-extension/no1.png)

Si ha habilitado la fileCfg o perfCfg (como se describe en los escenarios 2 y 3), puede usar datos de no predeterminadas de tooview de explorador de servidores de Visual Studio y el Explorador de almacenamiento de Azure.

## <a name="known-issues"></a>Problemas conocidos

* Hola Rsyslog información y el archivo de registro especificado por el cliente solo puede obtenerse mediante el scripting.
