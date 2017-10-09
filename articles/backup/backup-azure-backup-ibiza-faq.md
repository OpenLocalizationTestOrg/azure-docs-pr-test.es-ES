---
title: "Preguntas más frecuentes del almacén de servicios de aaaRecovery | Documentos de Microsoft"
description: "Esta versión de hello preguntas más frecuentes sobre admite la versión de vista previa de Hola de hello servicio de copia de seguridad de Azure. Respuestas toofrequently preguntas más frecuentes sobre el agente de copia de seguridad de hello, copia de seguridad y retención, recuperación, seguridad y otras preguntas comunes sobre Hola soluciones de copia de seguridad de Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "solución de copia de seguridad; servicio de copia de seguridad"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>Almacén de Servicios de recuperación: preguntas más frecuentes
Este artículo proporciona el almacén de servicios de información tooRecovery específico y lo complementa hello [preguntas más frecuentes de copia de seguridad de Azure](backup-azure-backup-faq.md). Hola preguntas más frecuentes de copia de seguridad de Azure proporciona el conjunto completo de Hola de preguntas y respuestas sobre Hola servicio de copia de seguridad de Azure.  

Puede hacer preguntas sobre copias de seguridad de Azure en hello Disqus sección de este artículo o un artículo relacionado. También puede publicar preguntas sobre Hola servicio de copia de seguridad de Azure en hello [foro de discusión](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Los almacenes de Recovery Services se basan en Resource Manager. ¿Se admiten aún los almacenes de Backup (modo clásico)? <br/>
Sí, los almacenes de Copia de seguridad son todavía compatibles. Crear almacenes de copia de seguridad en hello [portal clásico](https://manage.windowsazure.com). Crear almacenes de servicios de recuperación en hello [portal de Azure](https://portal.azure.com). Sin embargo se recomienda encarecidamente toocreate servicios almacén de recuperación como todas las futuras mejoras estará disponible sólo en el almacén de servicios de recuperación.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>¿Puedo migrar un almacén de servicios de recuperación de tooa de almacén de copia de seguridad? <br/>
Lamentablemente no, en este momento no puede migrar contenido de Hola de un tooa de almacén de copia de seguridad que del almacén de servicios de recuperación. Estamos trabajando para agregar esta funcionalidad, pero no está disponible como parte de la versión previa pública.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>¿Admiten los almacenes de Servicios de recuperación máquinas virtuales implementadas con el modelo clásico o máquinas virtuales implementadas con Resource Manager? <br/>
Los almacenes de Servicios de recuperación admiten ambos modelos.  Puede realizar copias de seguridad de una máquina virtual creada en portal clásico de hello (que son máquinas virtuales de modo clásico), o una máquina virtual que se crea en hello portal de Azure (que son en función de administrador de recursos) del almacén de servicios de recuperación de tooa.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>He realizado copias de seguridad de mis máquinas virtuales clásicas en el almacén de Copia de seguridad. Ahora deseo toomigrate Mis máquinas virtuales desde el modo de administrador de tooResource de modo clásico.  ¿Cómo puedo realizar una copia de seguridad de ellas en el almacén de Servicios de recuperación?
Copias de seguridad de máquinas virtuales clásicas en el almacén de copia de seguridad no migran automáticamente toorecovery el almacén de servicios cuando se migra hello las máquinas virtuales de clásico tooResource modo de administrador de. Para realizar la migración de las copias de seguridad de máquinas virtuales, siga estos pasos:

1. En el almacén de copia de seguridad, vaya demasiado**elementos protegidos** pestaña y seleccione Hola máquina virtual. Haga clic en [Detener la protección](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deje la opción *Eliminar los datos de copia de seguridad asociados***desactivada**.
2. Hola [portal de Azure](https://portal.azure.com), vaya toohello **extensiones** menú Hola VM y desinstalar hello **VMSnapshot/VMSnapshotLinux** extensión.
3. Migrar máquina virtual de Hola de modo de administrador de tooResource de modo clásico. Garantizar la validez almacenamiento y red correspondiente máquina toovirtual también el modo de administrador tooResource migrados.
4. Crear un almacén de servicios de recuperación y configurar copia de seguridad en hello migrar máquina virtual usando **copia de seguridad** acción sobre el panel almacén. Más información acerca de cómo demasiado[habilitar copia de seguridad en el almacén de servicios de recuperación](backup-azure-vms-first-look-arm.md)
