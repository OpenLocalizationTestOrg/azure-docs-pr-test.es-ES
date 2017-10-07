---
title: "aaaBoot diagnósticos para máquinas virtuales de Linux en Azure | Documento de Microsoft"
description: "Información general sobre Hola dos características de depuración para las máquinas virtuales de Linux en Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>¿Cómo toouse arrancar las máquinas virtuales Linux diagnósticos tootroubleshoot en Azure

Ahora se ofrece en Azure compatibilidad con dos características de depuración, Salida de la consola y Captura de pantalla, para el modelo de implementación de Resource Manager en máquinas virtuales de Azure. 

Al volver a poner su propia imagen tooAzure o incluso arranque uno de imágenes de la plataforma de hello, puede haber muchas razones, ¿por qué se obtiene una máquina Virtual en un estado no sean de arranque. Estos permiten características tooeasily, diagnosticar y recuperarse de las máquinas virtuales de los errores de arranque.

Para máquinas de virtuales de Linux, puede ver fácilmente salida de hello de su registro de la consola de hello Portal:

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
Sin embargo, Windows y máquinas virtuales de Linux, Azure también permite toosee una captura de pantalla de hello VM desde el hipervisor de hello:

![Error](./media/boot-diagnostics/screenshot2.png)

Ambas características son compatibles para las máquinas virtuales de Azure en todas las regiones. Tenga en cuenta, capturas de pantalla y salida pueden tardar hasta too10 minutos tooappear en su cuenta de almacenamiento.

## <a name="common-boot-errors"></a>Errores comunes de arranque

- [Problemas del sistema de archivos](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [Problemas de kernel](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [Errores de FSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Habilitación del diagnóstico en una nueva máquina virtual
1. Al crear una nueva máquina Virtual desde el Portal de vista previa de hello, seleccione hello **Azure Resource Manager** de lista desplegable de modelo de implementación de hello:
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. Configurar Hola cuenta de almacenamiento de hello en tooselect de supervisión opción que desee que tooplace estos archivos de diagnóstico.
 
    ![Creación de una máquina virtual](./media/boot-diagnostics/screenshot4.jpg)

3. Si va a implementar desde una plantilla de Azure Resource Manager, navegue tooyour recurso de máquina Virtual y anexar la sección de perfil de diagnóstico de Hola. Recuerde que el encabezado de la versión de API de "2015-06-15" toouse Hola.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. perfil de diagnóstico de Hello permite cuenta de almacenamiento de hello tooselect donde desea tooput estos registros.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>Actualización de una máquina virtual existente

diagnóstico de arranque de tooenable a través del portal de hello, también puede actualizar una máquina virtual existente a través del portal de Hola. Diagnóstico de arranque de hello seleccione opción y guardar. Reinicie el efecto de hello VM tootake.

![Actualización de una máquina virtual existente](./media/boot-diagnostics/screenshot5.png)