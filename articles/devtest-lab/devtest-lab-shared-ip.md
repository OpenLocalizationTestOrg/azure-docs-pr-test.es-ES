---
title: aaaUnderstand compartido direcciones IP en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtener información sobre cómo laboratorios de desarrollo y pruebas de Azure usa compartido IP direcciones toominimize Hola pública IP direcciones necesarios tooaccess el laboratorio, máquinas virtuales."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Direcciones IP compartidas en Azure DevTest Labs

Laboratorio de permite los laboratorios de desarrollo y pruebas Azure recurso compartido de las máquinas virtuales Hola pública IP dirección toominimize Hola tantos pública IP direcciones necesarios tooaccess el laboratorio individual de las máquinas virtuales.  En este artículo se describe cómo funcionan las direcciones IP compartidas y sus opciones de configuración relacionadas.

## <a name="shared-ip-setting"></a>Configuración de IP compartidas

Cuando se crea un laboratorio, reside en una subred de una red virtual.  De forma predeterminada, esta subred se crea con **habilitar la IP pública compartida** establecido demasiado*Sí*.  Esta configuración crea una dirección IP pública para la subred todo Hola.  Para obtener más información sobre cómo configurar redes virtuales y subredes, vea [Configuración de una red virtual en Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Nueva subred de laboratorio](media/devtest-lab-shared-ip/lab-subnet.png)

Para habilitar esta opción en laboratorios existentes, seleccione **Configuration and policies (Directivas y configuración) > Redes virtuales**. A continuación, seleccione una red virtual de lista de Hola y elija **habilitar IP pública compartido** para una subred seleccionada. También puede deshabilitar esta opción en cualquier laboratorio si no desea tooshare una dirección IP pública a través de las máquinas virtuales del laboratorio.

Todas las máquinas virtuales crean en este toousing de manera predeterminada de laboratorio una dirección IP compartida.  Al crear Hola VM, esta configuración se puede observar en hello **configuración avanzada** hoja bajo **configuración de dirección IP**.

![Nueva máquina virtual](media/devtest-lab-shared-ip/new-vm.png)

- **Compartido:** todas las máquinas virtuales creadas como **Compartido** se colocan en un solo grupo de recursos. Se asigna una dirección IP única para que RG y todas las máquinas virtuales en hello RG usará esa dirección IP.
- **Público:** todas las máquinas virtuales que se crean tienen su propia dirección IP y se crean en su propio grupo de recursos.
- **Privado:** todas las máquinas virtuales que se crean usan una dirección IP privada. Es posible no que pueda tooconnect toothis VM directamente desde Hola internet con Escritorio remoto.

Siempre que una máquina virtual con la dirección IP compartida habilitado se agrega toohello subred, laboratorios de desarrollo y pruebas agrega equilibrador de carga de hello VM tooa automáticamente y se asigna a un número de puerto TCP en la dirección IP pública de hello, toohello de reenvío de puerto de RDP en hello VM.  

## <a name="using-hello-shared-ip"></a>Usar Hola compartidos IP

- **Los usuarios de Linux:** SSH toohello VM mediante el uso de la dirección IP de Hola o nombre de dominio completo, seguido de dos puntos, seguido por puerto Hola. Por ejemplo, en la imagen de hello siguiente, Hola RDP direcciones toohello tooconnect VM es `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Ejemplo de máquina virtual](media/devtest-lab-shared-ip/vm-info.png)

- **Los usuarios de Windows:** Hola seleccione **conectar** situado en hello toodownload portal Azure un archivo RDP configurado previamente y tener acceso a Hola máquina virtual.

## <a name="next-steps"></a>Pasos siguientes

* [Definición de directivas de laboratorio en Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Configuración de una red virtual en Azure DevTest Labs](devtest-lab-configure-vnet.md)





