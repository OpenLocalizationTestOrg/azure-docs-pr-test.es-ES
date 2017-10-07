---
title: "aaaBack de portal clásico de tooAzure de las cargas de trabajo DPM | Documentos de Microsoft"
description: "Un toobacking de introducción de los servidores DPM con el servicio de copia de seguridad de Azure Hola"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: System Center Data Protection Manager, Data Protection Manager, copia de seguridad de DPM
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Preparar tooback una tooAzure de las cargas de trabajo con DPM
> [!div class="op_single_selector"]
> * [Servidor de Copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (clásico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (clásico)](backup-azure-dpm-introduction-classic.md)
>
>

Este artículo proporciona una tooprotect de copia de seguridad de Microsoft Azure toousing de introducción de los servidores de System Center Data Protection Manager (DPM) y las cargas de trabajo. Cuando lo lea, comprenderá:

* Cómo funciona la copia de seguridad de servidor DPM de Azure
* requisitos previos de Hello tooachieve una experiencia sin problemas de copia de seguridad
* Hola típicos errores detectados y cómo toodeal con ellos
* Escenarios admitidos

Datos de aplicación y archivo de copia de seguridad de System Center DMP. Datos de copia de seguridad tooDPM se pueden almacenar en cinta, en el disco, o copias de seguridad tooAzure con copia de seguridad de Microsoft Azure. DPM interactúa con Azure Backup de la manera siguiente:

* **DPM implementado como una máquina de virtual server o de forma local física** : Si DPM se implementa como un servidor físico o como máquina virtual de Hyper-V local puede realizar copias de seguridad de datos tooan de copia de seguridad de Azure además almacén toodisk y copia de seguridad en cinta.
* **DPM implementado como una máquina virtual de Azure** : desde System Center 2012 R2 con Update 3, DPM puede implementarse como una máquina virtual de Azure. Si DPM se implementa como una máquina virtual de Azure que puede realizar copias de los discos de datos tooAzure adjunta la máquina virtual de Azure de DPM de toohello o puede descargar el almacenamiento de datos de hello al hacer una copia de seguridad tooan el almacén de copia de seguridad de Azure.

## <a name="why-backup-your-dpm-servers"></a>¿Por qué crear una copia de seguridad de los servidores DPM?
ventajas empresariales de Hola de copia de seguridad de servidores DPM mediante copia de seguridad de Azure incluyen:

* Para la implementación local de DPM, puede usar copia de seguridad de Azure como un tootape de implementación toolong-término alternativo.
* Para las implementaciones de DPM en Azure, copia de seguridad de Azure permite almacenamiento toooffload de hello disco de Azure, permitiéndole tooscale seguridad almacenando datos antiguos en copia de seguridad de Azure y datos nuevos en el disco.

## <a name="how-does-dpm-server-backup-work"></a>Cómo funciona la copia de seguridad de servidor DPM
tooback una máquina virtual, primero se necesita una instantánea de tiempo de punto de datos de Hola. Hola copia de seguridad de Azure servicio inicia Hola trabajo de copia en hello fecha programada y desencadenadores Hola tootake una instantánea de copia de seguridad de extensión. coordenadas de extensión de copia de seguridad de Hello con hello en el invitado VSS tooachieve coherencia de servicio y API de instantánea de blob de Hola de hello servicio de almacenamiento de Azure, se invoca una vez que se ha alcanzado la coherencia. Se trata de hacer tooget una instantánea coherente de los discos de Hola de máquina virtual de hello, sin necesidad de tooshut lo hacia abajo.

Después de que ha tomado instantáneas de hello, datos de Hola se transfieren por el almacén copia de seguridad de copia de seguridad de Azure toohello servicio Hola. servicio de Hola se encarga de identificar y transferir sólo los bloques de Hola que han cambiado desde Hola última copia de seguridad que la red y almacenamiento de copias de seguridad de hello eficientes. Cuando se complete la transferencia de datos de hello, instantánea Hola se quita y se crea un punto de recuperación. Este punto de recuperación se puede ver en hello portal de Azure clásico.

> [!NOTE]
> Para las máquinas virtuales de Linux, solo es posible la copia de seguridad coherente con archivos.
>
>

## <a name="prerequisites"></a>Requisitos previos
Preparar la copia de seguridad de Azure tooback datos de DPM como se indica a continuación:

1. **Cree un almacén de Backup**. Si no ha creado un almacén de copia de seguridad en su suscripción, vea hello Azure portal versión de este artículo - [preparar tooback una tooAzure de las cargas de trabajo con DPM](backup-azure-dpm-introduction.md).

  > [!IMPORTANT]
  > A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.
  > Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell. **El 1 de noviembre de 2017**:
  >- Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
  >- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
  >

2. **Descargar las credenciales de almacén** : en Azure Backup, certificado de administración de Hola de carga que creó el almacén de toohello.
3. **Instalar hello Azure Backup Agent y registre el servidor de Hola** : instalar agente de hello en cada servidor DPM de Azure copia de seguridad y registrar el servidor DPM hello en el almacén de copia de seguridad Hola.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>Requisitos y limitaciones
* DPM se puede ejecutar como un servidor físico o como una máquina virtual de Hyper-V, instalado en System Center 2012 SP1 o System Center 2012 R2. También se puede ejecutar como una máquina virtual de Azure que ejecuta System Center 2012 R2 con al menos el paquete acumulativo de actualizaciones 3 para DPM 2012 R2, o como una máquina virtual de Windows en VMWare que se ejecuta en System Center 2012 R2 con al menos el paquete acumulativo de actualizaciones 5.
* Si ejecuta DPM con System Center 2012 SP1, debe instalar el paquete acumulativo de actualizaciones 2 para System Center Data Protection Manager SP1. Esto es necesario para poder instalar hello Azure Backup Agent.
* servidor DPM de Hello debe tener Windows PowerShell y .net Framework 4.5 instalado.
* DPM puede respaldar la mayoría de las cargas de trabajo de tooAzure copia de seguridad. Para obtener una lista completa de los elementos compatibles, vea Hola copia de seguridad de Azure admite los siguientes elementos.
* No se puede recuperar los datos almacenados en la copia de seguridad de Azure con la opción de "Copiar tootape" Hola.
* Necesitará una cuenta de Azure con la característica de copia de seguridad de Azure Hola habilitada. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Lea acerca de los [Precios de Backup](https://azure.microsoft.com/pricing/details/backup/).
* Mediante copia de seguridad de Azure requiere hello Azure Backup Agent toobe instalado en los servidores de hello que desea tooback. Cada servidor debe tener al menos el 10% del tamaño de Hola de datos de Hola que están haciendo copias de seguridad, disponible como espacio de almacenamiento local. Por ejemplo, la copia de seguridad de 100 GB de datos requiere un mínimo de 10 GB de espacio libre en la ubicación del borrador Hola. Aunque hello mínimo es 10%, se recomienda el 15% de toobe de espacio de almacenamiento local disponible para la ubicación de caché de Hola.
* Datos se almacenarán en hello almacén de Azure. No hay ninguna cantidad de toohello límite de datos que pueda respaldar el almacén de copia de seguridad de Azure tooan pero tamaño Hola de un origen de datos (por ejemplo una máquina virtual o una base de datos) no debe superar 54,400 GB.

Se admiten estos tipos de archivo de copia de seguridad tooAzure:

* Cifrados (solo copias de seguridad completas)
* Comprimidos (copias de seguridad incrementales compatibles)
* Dispersos (copias de seguridad incrementales compatibles)
* Comprimidos y dispersos (tratados como dispersos)

No se admiten los siguientes:

* Servidores de sistemas de archivos que distinguen entre mayúsculas y minúsculas.
* Vínculos físicos (omitidos)
* Puntos de reanálisis (omitidos)
* Cifrados y comprimidos (omitidos)
* Cifrados y dispersos (omitidos)
* Flujo comprimido
* Flujo disperso

> [!NOTE]
> Desde en System Center 2012 DPM con SP1 y versiones posteriores, puede hacer una copia seguridad de cargas de trabajo protegidas por tooAzure DPM mediante copia de seguridad de Microsoft Azure.
>
>
