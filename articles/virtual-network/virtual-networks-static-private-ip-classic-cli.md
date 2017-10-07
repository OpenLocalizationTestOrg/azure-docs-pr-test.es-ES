---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales (clásicas) - 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure de direcciones IP privadas de máquinas virtuales (clásicas) mediante hello Azure interfaz de línea de comandos (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Configurar las direcciones IP privadas para una máquina virtual (clásica) mediante Hola 1.0 de CLI de Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación clásica de Hola. También puede [administrar una dirección IP privada estática en el modelo de implementación del Administrador de recursos de hello](virtual-networks-static-private-ip-arm-cli.md).

comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado. Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>¿Cómo toospecify una privada de direcciones IP estáticas al crear una máquina virtual
toocreate una nueva máquina virtual denominada *DNS01* en un nuevo servicio de nube denominado *TestService* en función de escenario de hello anterior, siga estos pasos:

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello **crear servicio de azure** comando servicio en la nube toocreate Hola.
   
        azure service create TestService --location uscentral
   
    Resultado esperado:
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Ejecute hello **azure crear vm** comando toocreate hello máquina virtual. Observe el valor de Hola para una dirección IP privada estática. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    Resultado esperado:
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (o --location)**. Región de Azure donde se creará Hola máquina virtual. En este escenario, *centralus*.
   * **-n (o --vm-name)**. Nombre de hello VM toobe creado.
   * **-w (o --virtual-network-name)**. Nombre de red virtual donde se creará Hola VM hello. 
   * **-S (o --static-ip)**. Privada dirección IP estática para hello máquina virtual.
   * **TestService**. Nombre del servicio de nube de Hola donde se creará Hola máquina virtual.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**. Imagen que se utiliza toocreate hello máquina virtual.
   * **adminuser**. Administrador local para la máquina virtual de Windows hello.
   * **AdminP@ssw0rd**. Contraseña de administrador local para la máquina virtual de Windows hello.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>¿Cómo tooretrieve dirección IP estática privada información de dirección de una máquina virtual
información de hello máquinas virtuales crean con script de Hola anterior, ejecutar el siguiente comando de CLI de Azure de Hola de direcciones IP privada estático de tooview hello y observe el valor de hello para *StaticIP red*:

    azure vm static-ip show DNS01

Resultado esperado:

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>¿Cómo tooremove una privada de direcciones IP estáticas de una máquina virtual
tooremove Hola privada dirección IP estática agregado toohello VM en script de Hola anteriormente, Hola ejecución siguiente comando de CLI de Azure:

    azure vm static-ip remove DNS01

Resultado esperado:

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>¿Cómo tooadd un tooan IP estática privada VM existente
tooadd una toohello de dirección IP privada estática máquinas virtuales creadas con script de Hola anteriormente, ejecución el siguiente comando:

    azure vm static-ip set DNS01 192.168.1.101

Resultado esperado:

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .
* Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).

