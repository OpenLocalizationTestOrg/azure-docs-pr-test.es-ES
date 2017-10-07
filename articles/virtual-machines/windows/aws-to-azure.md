---
title: "aaaMove una tooAzure de las máquinas virtuales de Windows AWS | Documentos de Microsoft"
description: "Mover un tooAzure de instancia de Amazon Web Services (AWS) EC2 Windows máquinas virtuales con PowerShell de Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Mover una máquina virtual de Windows de tooAzure de Amazon Web Services (AWS) mediante PowerShell

Si va a evaluar máquinas virtuales de Azure para hospedar las cargas de trabajo, puede exportar una instancia existente de la máquina virtual de Windows de Amazon Web Services (AWS) EC2 luego cargar hello tooAzure de disco duro virtual (VHD). Una vez Hola generalizada, puede crear una nueva máquina virtual en Azure de hello VHD. 

Este tema cubre la migración de una sola máquina virtual desde AWS tooAzure. Si desea que las máquinas virtuales de toomove de AWS tooAzure a escala, vea [Migre máquinas virtuales de Amazon Web Services (AWS) tooAzure con Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Preparar Hola VM 
 
Puede cargar tooAzure de discos duros virtuales especializada y generalizada. Cada tipo requiere que preparar Hola VM antes de exportar desde AWS. 

- **VHD generalizado**: Se ha quitado toda la información de cuenta personal con Sysprep de un VHD generalizado. Si piensa toouse Hola VHD como una imagen toocreate nuevas máquinas virtuales desde, debe: 
 
    * [Preparación de una máquina virtual Windows](prepare-for-upload-vhd-image.md).  
    * Generalice la máquina virtual de hello mediante Sysprep.  

 
- **Especializado VHD** -un disco duro virtual especializado mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original. Si piensa toouse Hola VHD como-es toocreate una nueva máquina virtual, asegúrese de que se completa Hola pasos.  
    * [Preparar una tooAzure de tooupload de disco duro virtual de Windows](prepare-for-upload-vhd-image.md). **No** generalizar Hola VM con Sysprep. 
    * Quite todas las herramientas de virtualización de invitado y los agentes instalados en hello VM (es decir, herramientas de VMware). 
    * Asegúrese de hello VM es toopull configurado su dirección IP y la configuración de DNS a través de DHCP. Esto garantiza que el servidor hello Obtiene una dirección IP dentro de la red virtual de hello cuando se inicia.  


## <a name="export-and-download-hello-vhd"></a>Exportar y descargar Hola VHD 

Exportar Hola EC2 instancia tooa disco duro virtual en un depósito de S3 de Amazon. Siga los pasos de hello descritos en el tema de documentación de Amazon hello [exportar como una máquina virtual usando VM importación y exportación de una instancia](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) ejecución hello y [crear instancia-export-tareas](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) comando tooexport hello EC2 archivo de disco duro virtual de tooa de instancia. 

Hello VHD archivo exportado se guarda en el cubo de hello Amazon S3 que especifique. Hello sintaxis básica para exportar Hola VHD está por debajo, solo tiene que reemplazar texto de marcador de posición de hello en <brackets> con su información.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Una vez que se ha exportado Hola VHD, siga las instrucciones de hello en [cómo descargar un objeto de un depósito de S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) hello toodownload VHD de archivos de depósitos de hello S3. 

> [!IMPORTANT]
> AWS cargos por las cuotas de transferencia de datos para la descarga de hello VHD. Consulte [Precios de Amazon S3](https://aws.amazon.com/s3/pricing/) para más información.


## <a name="next-steps"></a>Pasos siguientes

Ahora puede cargar tooAzure de disco duro virtual de Hola y crear una nueva máquina virtual. 

- Si ha ejecutado Sysprep en el origen demasiado**generalizar** , antes de exportar, vea [cargar un disco duro virtual generalizado y utilizar toocreate un nuevas máquinas virtuales de Azure](upload-generalized-managed.md)
- Si no se ejecutó Sysprep antes de exportar, hello VHD se considera **especializada**, consulte [cargar un tooAzure especializada de VHD y crear una nueva máquina virtual](create-vm-specialized.md)

 
