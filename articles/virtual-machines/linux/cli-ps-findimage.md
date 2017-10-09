---
title: "aaaSelect imágenes de VM de Linux con hello CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola publicador de hello toodetermine, oferta, SKU y versión para imágenes de máquina virtual de Marketplace de CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>Cómo toofind imágenes de VM de Linux de hello Azure Marketplace con hello CLI de Azure
Este tema describe cómo toouse Hola imágenes de máquina virtual de Azure CLI 2.0 toofind en hello Azure Marketplace. Utilice este toospecify una imagen de Marketplace de información cuando se crea una VM de Linux.

Asegúrese de que ha instalado hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) y se registran en tooan cuenta de Azure (`az login`).

## <a name="terminology"></a>Terminología

Imágenes de Marketplace se identifican en hello CLI y otras herramientas de Azure según la jerarquía de tooa:

* **Publicador** -Hola organización que creó la imagen de Hola. Ejemplo: Canonical
* **Oferta**: grupo de imágenes relacionadas creado por un publicador. Ejemplo: Ubuntu Server
* **SKU**: instancia de una oferta, por ejemplo, una versión principal de una distribución. Ejemplo: 16.04-LTS
* **Versión** -Hola número de versión de una imagen de SKU. Al especificar la imagen de hello, puede reemplazar número de versión de Hola con "más reciente", que selecciona la versión más reciente de Hola de distribución de Hola.

toospecify una imagen de Marketplace, se utiliza normalmente Hola imagen *URN*. Hola URN combina estos valores, separados por caracteres de dos puntos (:) de hello: *Publisher*:*ofrecen*:*Sku*:*versión*. 


## <a name="list-popular-images"></a>Enumeración de imágenes populares

Ejecute hello [lista de imágenes de máquina virtual de az](/cli/azure/vm/image#list) comando sin hello `--all` opción, toosee imágenes de una lista de VM popular de hello Azure Marketplace. Por ejemplo, ejecute hello después comando toodisplay una lista almacenados en memoria caché de imágenes populares en formato de tabla:

```azurecli
az vm image list --output table
```

salida de Hello incluye Hola URN (Hola valor Hola *Urn* columna), que se utiliza toospecify Hola imagen. Al crear una máquina virtual con una de estas imágenes de Marketplace populares, o bien puede especificar alias URN de hello, como *UbuntuLTS*.

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a>Búsqueda de imágenes específicas

toofind una imagen de máquina virtual específica en hello Marketplace, usar hello `az vm image list` comando con hello `--all` opción. Esta versión del comando hello toma algunas toocomplete tiempo y puede devolver una salida larga, por lo que normalmente filtrar lista Hola por `--publisher` o de otro parámetro. 

Por ejemplo, hello siguiente comando muestra todas las ofertas de Debian (Recuerde que sin hello `--all` cambia, sólo busca en memoria caché local de Hola de imágenes comunes):

```azurecli
az vm image list --offer Debian --all --output table 

```

Salida parcial: 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

Aplicar filtros similar con hello `--location`, `--publisher`, y `--sku` opciones. Incluso puede realizar coincidencias parciales en un filtro, como la búsqueda de `--offer Deb` toofind todas las imágenes de Debian.

Si no se especifica una ubicación concreta con hello `--location` valores de hello de, las opciones `westus` se devuelven de forma predeterminada. (Establezca una ubicación predeterminada distinta ejecutando `az configure --defaults location=<location>`).

Por ejemplo, hello siguiente comando muestra todas las SKU de 8 Debian en `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

Salida parcial:

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a>Navegar por imágenes de Hola 
Otra manera toofind una imagen en una ubicación es hello de toorun [imagen de máquina virtual de az lista-publicadores](/cli/azure/vm/image#list-publishers), [lista de imagen de vm az-ofertas](/cli/azure/vm/image#list-offers), y [imagen de máquina virtual de az lista-SKU](/cli/azure/vm/image#list-skus) comandos en secuencia. Con estos comandos, determine estos valores:

1. Editores de imagen de Hola de lista.
2. Para un publicador determinado, enumeración de sus ofertas.
3. Para una oferta determinada, enumeración de sus SKU.


Por ejemplo, hello comando siguiente muestra publicadores de imagen de Hola Hola ubicación oeste de Estados Unidos:

```azurecli
az vm image list-publishers --location westus --output table
```

Salida parcial:

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
Use que este toofind información ofrece a una editorial específica. Por ejemplo, si canónica es un publicador de la imagen en hello ubicación oeste de Estados Unidos, puede buscar sus ofertas ejecutando `azure vm image list-offers`. Pase la ubicación de Hola y el publicador de hello como en el siguiente ejemplo de Hola:

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

Salida:

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
Verá que en la región del oeste de Estados Unidos de hello, canónica publica hello **UbuntuServer** ofrecen en Azure. Pero ¿qué SKU? tooget esos valores, ejecute `azure vm image list-skus` y establecer la ubicación de hello, publisher y oferta que ha detectado:

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

Salida:

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

Por último, utilice hello `az vm image list` comando toofind una versión específica de hello SKU que desee, por ejemplo, **16.04 LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

Salida:

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a>Pasos siguientes
Ahora puede elegir exactamente Hola imagen que desee toouse por tomar nota de hello valor URN. Pase este valor con hello `--image` parámetro cuando se crea una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando. Recuerde que, opcionalmente, puede reemplazar número de versión de Hola Hola URN con "más reciente". Esta versión es siempre hello más reciente de distribución de Hola. toocreate una máquina virtual rápidamente mediante la información de URN de hello, consulte [crear y administrar máquinas virtuales de Linux con hello Azure CLI](tutorial-manage-vm.md).
