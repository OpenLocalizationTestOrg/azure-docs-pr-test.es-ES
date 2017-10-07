---
title: "Preparar el destino (tooAzure físico) | Documentos de Microsoft"
description: "Este artículo se describe cómo tooprepare su toostart de entorno de Azure replicar servidores físicos que ejecutan tooAzure de Windows o Linux."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Preparar el destino (tooAzure de VMware)
> [!div class="op_single_selector"]
> * [TooAzure de VMware](./site-recovery-prepare-target-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-prepare-target-physical-to-azure.md)

Este artículo se describe cómo tooprepare su toostart de entorno de Azure replicar servidores físicos (x 64) con Windows o Linux en Azure.

## <a name="prerequisites"></a>Requisitos previos

artículo de Hello supone siguiente hello:
- Ha creado un tooprotect de almacén de servicios de recuperación de los servidores físicos. Puede crear un almacén de servicios de recuperación de hello [portal de Azure](http://portal.azure.com "portal de Azure").
- Tiene [configurar su entorno local](./site-recovery-set-up-physical-to-azure.md) tooreplicate tooAzure de servidores físicos.

## <a name="prepare-target"></a>Preparación del destino

Después de completar hello **objetivo de protección de paso 1:Select** y **paso 2: preparar origen**, se toman demasiado**paso 3: destino**

![Preparación del destino](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. **Suscripción:** de hello menú desplegable, seleccione Hola suscripción que quiere tooreplicate sus servidores físicos a.
2. **Modelo de implementación:** modelo de implementación de hello seleccione (Classic o administrador de recursos)

En función de hello elegido el modelo de implementación, una validación se ejecuta tooensure que tienen al menos una cuenta de almacenamiento compatibles y la red virtual en tooreplicate de suscripción de destino de Hola y de conmutación por error de los servidores físicos para.

Una vez validaciones de Hola se completan correctamente, haga clic en Aceptar toogo toohello siguiente paso.

Si no tiene una cuenta de almacenamiento compatible con el Administrador de recursos o la red virtual, o quiere que tooadd más, puede hacerlo haciendo clic en hello **+ cuenta de almacenamiento** o **+ red** botones en la parte superior de Hola Hola hoja.

## <a name="next-steps"></a>Pasos siguientes
[Configuración de las opciones de replicación](./site-recovery-setup-replication-settings-vmware.md).
