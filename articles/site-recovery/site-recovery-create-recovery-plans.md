---
title: "planes de recuperación de aaaCreate conmutación por error y recuperación en Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo toocreate y personalizar planes de recuperación en Azure Site Recovery, toofail a través y recuperar las máquinas virtuales y servidores físicos"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>Creación de planes de recuperación


En este artículo se proporciona información sobre cómo crear y personalizar planes de recuperación en [Azure Site Recovery](site-recovery-overview.md).

Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

 Crear Hola de toodo de planes de recuperación siguientes:

* Definen grupos de máquinas que conmutan por error juntas y también se inician juntas.
* Modelan dependencias entre máquinas, agrupándolas en un grupo de planes de recuperación. Por ejemplo, toofail sobre y abrirá una aplicación específica, se agrupan todas las máquinas virtuales de Hola para esa aplicación en hello mismo grupo de plan de recuperación.
* Ejecutar una conmutación por error. Puede ejecutar una conmutación por error de prueba, planeada o no planeada en un plan de recuperación.


## <a name="create-a-recovery-plan"></a>Creación de un plan de recuperación

1. Haga clic en **Planes de recuperación** > **Crear plan de recuperación**.
   Especifique un nombre para el plan de recuperación de hello y un origen y de destino. ubicación de origen de Hello debe tener máquinas virtuales que están habilitadas para conmutación por error y recuperación.

    - Para la replicación de tooVMM VMM, seleccione **tipo de origen de** > **VMM**y Hola de origen y destino en servidores VMM. Haga clic en **Hyper-V** toosee nubes que están protegidas.
    - Para tooAzure VMM, seleccione **tipo de origen de** > **VMM**.  Servidor VMM de origen de hello seleccione, y **Azure** como destino de Hola.
    - Para tooAzure de replicación de Hyper-V (sin WMM), seleccione **tipo de origen de** > **sitio Hyper-V**. Sitio de hello seleccione como origen de hello, y **Azure** como destino de Hola.
    - Para una VM VMware o físico local tooAzure de servidor, seleccione un servidor de configuración como origen de Hola y **Azure** como destino de Hola.
    - Para un plan de recuperación de Azure tooAzure, seleccione una región de Azure como origen de hello y una región secundaria de Azure como destino de Hola. regiones de Azure secundario Hola son que solo aquellas máquinas virtuales de toowhich están protegidos.
2. En **seleccionar las máquinas virtuales**, seleccione las máquinas virtuales hello (o grupo de replicación) que desea que el grupo predeterminado de toohello tooadd (grupo 1) en el plan de recuperación de Hola.

## <a name="customize-and-extend-recovery-plans"></a>Personalización y extensión de planes de recuperación

Puede personalizar y extender los planes de recuperación:

- **Agregar grupos nuevos**: Agregar grupo predeterminado toohello grupos (arriba tooseven) de plan de recuperación adicionales y, a continuación, agregue más máquinas o replicación grupos toothose grupos de planes de recuperación. Los grupos se numeran en orden de hello en las que agregar. Solo se puede incluir una máquina virtual o un grupo de replicación en un grupo de planes de recuperación.
- **Agregar una acción manual**: puede agregar acciones manuales que se ejecuten antes o después de un grupo de planes de recuperación. Cuando se ejecuta el plan de recuperación de hello, se detiene en el punto de hello en el que se inserta acción manual Hola. Un cuadro de diálogo le pide que toospecify que se ha completado la acción manual de Hola.
- **Agregar un script**: puede agregar scripts que se ejecutan antes o después de un grupo de planes recuperación. Cuando se agrega una secuencia de comandos, agrega un nuevo conjunto de acciones para el grupo de Hola. Por ejemplo, se creará un conjunto de pasos previos para el grupo 1 con el nombre de hello: grupo 1: pasos previos. Dentro de este conjunto se enumerarán todos los pasos previos. Solo puede agregar una secuencia de comandos en el sitio principal de hello si tiene un servidor VMM implementado.
- **Agregar runbooks de Azure**: puede extender planes de recuperación con runbooks de Azure. Por ejemplo, las tareas de tooautomate o recuperación de toocreate paso a paso. [Más información](site-recovery-runbook-automation.md).

## <a name="add-scripts"></a>Incorporación de scripts

Puede usar scripts de PowerShell en los planes de recuperación.

 - Asegúrese de que las secuencias de comandos utilizan bloques try-catch para que las excepciones de Hola se controlan correctamente.
    - Si se produce una excepción en el script de Hola, deje de ejecutarse y tarea hello muestra como error.
    - Si se produce un error, no se ejecuta ninguna parte restante del script de Hola.
    - Si se produce un error al ejecutar una conmutación por error no planeada, plan de recuperación de hello continúa.
    - Si se produce un error al ejecutar una conmutación por error planeada, detiene el plan de recuperación de Hola. Necesita script de Hola toofix, compruebe que se ejecuta según lo previsto y vuelva a ejecutar nuevo plan de recuperación de Hola.
- Hola comando Write-Host no funciona en un script de plan de recuperación, y se producirá un error de script de Hola. toocreate de salida, cree un script de proxy que a su vez se ejecuta el script principal. Asegúrese de que todos los resultados se canalizan mediante hello >> comando.
  * Hola script agota el tiempo si no devuelve en 600 segundos.
  * Si se escribe algo tooSTDERR, el script de Hola se clasifica como no superado. Esta información se muestra en los detalles de ejecución de script de Hola.

Si utiliza VMM en la implementación:

* Las secuencias de comandos en un plan de recuperación que se ejecutan en contexto de Hola de hello cuenta de servicio de VMM. Asegúrese de que esta cuenta tiene permisos de lectura para el recurso compartido remoto de hello en qué Hola se encuentra el script. Probar toorun de script de Hola en hello nivel de privilegios de cuenta de servicio VMM.
* Los cmdlets de VMM se entregan en un módulo de Windows PowerShell. Hola módulo se instala al instalar la consola VMM Hola. Se puede cargar en el script, mediante el siguiente comando de script de Hola de hello:
   - Import-Module -Name virtualmachinemanager. [Más información](https://technet.microsoft.com/library/hh875013.aspx).
* Asegúrese de que tiene al menos un servidor de biblioteca en la implementación de VMM. De forma predeterminada, ruta de acceso del recurso compartido de biblioteca de Hola para un servidor VMM se encuentra localmente en hello servidor VMM, con el nombre de carpeta de hello MSCVMMLibrary.
    * Si la ruta de acceso del recurso compartido de biblioteca es remoto (o local, pero no se comparte con MSCVMMLibrary), configurar recursos compartidos de hello como sigue (usando \\libserver2.contoso.com\share\ como ejemplo):
      * Abra el Editor del registro de hello y navegue demasiado**HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure sitio Recovery\Registration**.
      * Editar valor hello **ScriptLibraryPath** y colóquelo como \\libserver2.contoso.com\share\. Especificar nombre de dominio completo de Hola. Proporcionar permisos toohello ubicación del recurso compartido.
      * Asegúrese de probar el script de Hola con una cuenta de usuario que ha Hola misma cuenta de servicio permisos como Hola VMM. Este comando comprueba que independiente probados secuencias se ejecutan en Hola misma manera que lo harían en los planes de recuperación. En el servidor VMM hello, configure toobypass de directiva de ejecución de hello como sigue:
        * Abra la consola de Windows PowerShell de 64 bits de hello con privilegios elevados.
        * Escriba: **Set-executionpolicy bypass**. [Más información](https://technet.microsoft.com/library/ee176961.aspx).

## <a name="add-a-script-or-manual-action-tooa-plan"></a>Agregar un script o un plan de acción manual tooa

Puede agregar un grupo de plan de recuperación de secuencia de comandos toohello predeterminada después de que has agregado máquinas virtuales o tooit de grupos de replicación y el plan de Hola se creó.

1. Plan de recuperación de hello abierto.
2. Haga clic en un elemento de hello **paso** lista y, a continuación, haga clic en **Script** o **acción Manual**.
3. Especifique si el script de Hola tooadd toowant o acción antes o después de hello selecciona elemento. Hola de uso **Subir** y **mover hacia abajo** botones, posición de hello toomove del script de Hola hacia arriba o hacia abajo.
4. Si agrega una secuencia de comandos VMM, seleccione **secuencia de comandos de conmutación por error tooVMM**. En **ruta del Script**, recurso compartido de toohello de tipo hello ruta de acceso relativa. En el ejemplo VMM de Hola a continuación, especificar ruta de acceso de hello: **\RPScripts\RPScript.PS1**.
5. Si agrega una automatización de Azure ejecutar libro, especifique la cuenta de automatización de Azure de hello en qué Hola runbook es el script de runbook de Azure adecuada de hello encuentra y, a continuación, seleccione.
6. Realice una conmutación por error del plan de recuperación de hello, que la secuencia de comandos de hello toomake funciona según lo previsto.


### <a name="add-a-vmm-script"></a>Adición de un script de VMM

Si tiene un sitio de origen VMM, puede crear una secuencia de comandos en el servidor VMM de Hola e incluirlo en el plan de recuperación.

1. Cree una carpeta nueva en el recurso compartido de biblioteca de Hola. Por ejemplo, \<nombreDeServidorVMM>\MSSCVMMLibrary\RPScripts. Coloque en el origen de Hola y servidores VMM de destino.
2. Crear script de Hola (por ejemplo, RPScript) y comprobar que funciona según lo previsto.
3. Coloque el script de Hola en la ubicación de hello \<Nombreservidorvmm > \MSSCVMMLibrary en los servidores VMM de origen y destino de Hola.


## <a name="next-steps"></a>Pasos siguientes

[Aprenda más](site-recovery-failover.md) sobre la ejecución de conmutaciones por error.
