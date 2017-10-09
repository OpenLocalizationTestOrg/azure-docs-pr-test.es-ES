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
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="82e77-103">Cómo toofind imágenes de VM de Linux de hello Azure Marketplace con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="82e77-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="82e77-104">Este tema describe cómo toouse Hola imágenes de máquina virtual de Azure CLI 2.0 toofind en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="82e77-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="82e77-105">Utilice este toospecify una imagen de Marketplace de información cuando se crea una VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="82e77-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="82e77-106">Asegúrese de que ha instalado hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) y se registran en tooan cuenta de Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="82e77-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="82e77-107">Terminología</span><span class="sxs-lookup"><span data-stu-id="82e77-107">Terminology</span></span>

<span data-ttu-id="82e77-108">Imágenes de Marketplace se identifican en hello CLI y otras herramientas de Azure según la jerarquía de tooa:</span><span class="sxs-lookup"><span data-stu-id="82e77-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="82e77-109">**Publicador** -Hola organización que creó la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e77-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="82e77-110">Ejemplo: Canonical</span><span class="sxs-lookup"><span data-stu-id="82e77-110">Example: Canonical</span></span>
* <span data-ttu-id="82e77-111">**Oferta**: grupo de imágenes relacionadas creado por un publicador.</span><span class="sxs-lookup"><span data-stu-id="82e77-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="82e77-112">Ejemplo: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="82e77-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="82e77-113">**SKU**: instancia de una oferta, por ejemplo, una versión principal de una distribución.</span><span class="sxs-lookup"><span data-stu-id="82e77-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="82e77-114">Ejemplo: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="82e77-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="82e77-115">**Versión** -Hola número de versión de una imagen de SKU.</span><span class="sxs-lookup"><span data-stu-id="82e77-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="82e77-116">Al especificar la imagen de hello, puede reemplazar número de versión de Hola con "más reciente", que selecciona la versión más reciente de Hola de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e77-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="82e77-117">toospecify una imagen de Marketplace, se utiliza normalmente Hola imagen *URN*.</span><span class="sxs-lookup"><span data-stu-id="82e77-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="82e77-118">Hola URN combina estos valores, separados por caracteres de dos puntos (:) de hello: *Publisher*:*ofrecen*:*Sku*:*versión*.</span><span class="sxs-lookup"><span data-stu-id="82e77-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="82e77-119">Enumeración de imágenes populares</span><span class="sxs-lookup"><span data-stu-id="82e77-119">List popular images</span></span>

<span data-ttu-id="82e77-120">Ejecute hello [lista de imágenes de máquina virtual de az](/cli/azure/vm/image#list) comando sin hello `--all` opción, toosee imágenes de una lista de VM popular de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="82e77-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="82e77-121">Por ejemplo, ejecute hello después comando toodisplay una lista almacenados en memoria caché de imágenes populares en formato de tabla:</span><span class="sxs-lookup"><span data-stu-id="82e77-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="82e77-122">salida de Hello incluye Hola URN (Hola valor Hola *Urn* columna), que se utiliza toospecify Hola imagen.</span><span class="sxs-lookup"><span data-stu-id="82e77-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="82e77-123">Al crear una máquina virtual con una de estas imágenes de Marketplace populares, o bien puede especificar alias URN de hello, como *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="82e77-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

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

## <a name="find-specific-images"></a><span data-ttu-id="82e77-124">Búsqueda de imágenes específicas</span><span class="sxs-lookup"><span data-stu-id="82e77-124">Find specific images</span></span>

<span data-ttu-id="82e77-125">toofind una imagen de máquina virtual específica en hello Marketplace, usar hello `az vm image list` comando con hello `--all` opción.</span><span class="sxs-lookup"><span data-stu-id="82e77-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="82e77-126">Esta versión del comando hello toma algunas toocomplete tiempo y puede devolver una salida larga, por lo que normalmente filtrar lista Hola por `--publisher` o de otro parámetro.</span><span class="sxs-lookup"><span data-stu-id="82e77-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="82e77-127">Por ejemplo, hello siguiente comando muestra todas las ofertas de Debian (Recuerde que sin hello `--all` cambia, sólo busca en memoria caché local de Hola de imágenes comunes):</span><span class="sxs-lookup"><span data-stu-id="82e77-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="82e77-128">Salida parcial:</span><span class="sxs-lookup"><span data-stu-id="82e77-128">Partial output:</span></span> 
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

<span data-ttu-id="82e77-129">Aplicar filtros similar con hello `--location`, `--publisher`, y `--sku` opciones.</span><span class="sxs-lookup"><span data-stu-id="82e77-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="82e77-130">Incluso puede realizar coincidencias parciales en un filtro, como la búsqueda de `--offer Deb` toofind todas las imágenes de Debian.</span><span class="sxs-lookup"><span data-stu-id="82e77-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="82e77-131">Si no se especifica una ubicación concreta con hello `--location` valores de hello de, las opciones `westus` se devuelven de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="82e77-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="82e77-132">(Establezca una ubicación predeterminada distinta ejecutando `az configure --defaults location=<location>`).</span><span class="sxs-lookup"><span data-stu-id="82e77-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="82e77-133">Por ejemplo, hello siguiente comando muestra todas las SKU de 8 Debian en `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="82e77-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="82e77-134">Salida parcial:</span><span class="sxs-lookup"><span data-stu-id="82e77-134">Partial output:</span></span>

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

## <a name="navigate-hello-images"></a><span data-ttu-id="82e77-135">Navegar por imágenes de Hola</span><span class="sxs-lookup"><span data-stu-id="82e77-135">Navigate hello images</span></span> 
<span data-ttu-id="82e77-136">Otra manera toofind una imagen en una ubicación es hello de toorun [imagen de máquina virtual de az lista-publicadores](/cli/azure/vm/image#list-publishers), [lista de imagen de vm az-ofertas](/cli/azure/vm/image#list-offers), y [imagen de máquina virtual de az lista-SKU](/cli/azure/vm/image#list-skus) comandos en secuencia.</span><span class="sxs-lookup"><span data-stu-id="82e77-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="82e77-137">Con estos comandos, determine estos valores:</span><span class="sxs-lookup"><span data-stu-id="82e77-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="82e77-138">Editores de imagen de Hola de lista.</span><span class="sxs-lookup"><span data-stu-id="82e77-138">List hello image publishers.</span></span>
2. <span data-ttu-id="82e77-139">Para un publicador determinado, enumeración de sus ofertas.</span><span class="sxs-lookup"><span data-stu-id="82e77-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="82e77-140">Para una oferta determinada, enumeración de sus SKU.</span><span class="sxs-lookup"><span data-stu-id="82e77-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="82e77-141">Por ejemplo, hello comando siguiente muestra publicadores de imagen de Hola Hola ubicación oeste de Estados Unidos:</span><span class="sxs-lookup"><span data-stu-id="82e77-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="82e77-142">Salida parcial:</span><span class="sxs-lookup"><span data-stu-id="82e77-142">Partial output:</span></span>

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
<span data-ttu-id="82e77-143">Use que este toofind información ofrece a una editorial específica.</span><span class="sxs-lookup"><span data-stu-id="82e77-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="82e77-144">Por ejemplo, si canónica es un publicador de la imagen en hello ubicación oeste de Estados Unidos, puede buscar sus ofertas ejecutando `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="82e77-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="82e77-145">Pase la ubicación de Hola y el publicador de hello como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="82e77-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="82e77-146">Salida:</span><span class="sxs-lookup"><span data-stu-id="82e77-146">Output:</span></span>

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
<span data-ttu-id="82e77-147">Verá que en la región del oeste de Estados Unidos de hello, canónica publica hello **UbuntuServer** ofrecen en Azure.</span><span class="sxs-lookup"><span data-stu-id="82e77-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="82e77-148">Pero ¿qué SKU? tooget esos valores, ejecute `azure vm image list-skus` y establecer la ubicación de hello, publisher y oferta que ha detectado:</span><span class="sxs-lookup"><span data-stu-id="82e77-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="82e77-149">Salida:</span><span class="sxs-lookup"><span data-stu-id="82e77-149">Output:</span></span>

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

<span data-ttu-id="82e77-150">Por último, utilice hello `az vm image list` comando toofind una versión específica de hello SKU que desee, por ejemplo, **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="82e77-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="82e77-151">Salida:</span><span class="sxs-lookup"><span data-stu-id="82e77-151">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="82e77-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82e77-152">Next steps</span></span>
<span data-ttu-id="82e77-153">Ahora puede elegir exactamente Hola imagen que desee toouse por tomar nota de hello valor URN.</span><span class="sxs-lookup"><span data-stu-id="82e77-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="82e77-154">Pase este valor con hello `--image` parámetro cuando se crea una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="82e77-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="82e77-155">Recuerde que, opcionalmente, puede reemplazar número de versión de Hola Hola URN con "más reciente".</span><span class="sxs-lookup"><span data-stu-id="82e77-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="82e77-156">Esta versión es siempre hello más reciente de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="82e77-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="82e77-157">toocreate una máquina virtual rápidamente mediante la información de URN de hello, consulte [crear y administrar máquinas virtuales de Linux con hello Azure CLI](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="82e77-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
