---
title: "Importación y exportación de un archivo de zona de dominio en DNS de Azure mediante la CLI de Azure 1.0 | Microsoft Docs"
description: Aprenda a importar y exportar un archivo de zona DNS en DNS de Azure mediante la CLI de Azure 1.0
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="49690-103">Importación y exportación de un archivo de zona DNS mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="49690-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="49690-104">Este artículo le guiará a través de la importación y exportación de archivos de zona DNS para DNS de Azure con la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="49690-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="49690-105">Introducción a la migración de zona DNS</span><span class="sxs-lookup"><span data-stu-id="49690-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="49690-106">Un archivo de zona DNS es un archivo de texto que contiene los detalles de cada registro DNS (Sistema de nombres de dominio) de la zona.</span><span class="sxs-lookup"><span data-stu-id="49690-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="49690-107">Sigue un formato estándar, por lo que es adecuado para transferir registros DNS entre distintos sistemas DNS.</span><span class="sxs-lookup"><span data-stu-id="49690-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="49690-108">Usar un archivo de zona es una manera rápida, confiable y cómoda de transferir una zona DNS a DNS de Azure o desde él.</span><span class="sxs-lookup"><span data-stu-id="49690-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="49690-109">DNS de Azure admite la importación y la exportación de archivos de zona mediante la interfaz de la línea de comandos (CLI) de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="49690-110">La importación de archivos de zona **no** se permite actualmente mediante Azure PowerShell o el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="49690-111">La CLI de Azure 1.0 es una herramienta de línea de comandos multiplataforma que se usa para administrar servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="49690-112">Está disponible para las plataformas Windows, Mac y Linux en la [página de descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="49690-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="49690-113">La compatibilidad multiplataforma es importante para la importación y la exportación de archivos de zona, porque el software de servidor de nombres más común, [BIND](https://www.isc.org/downloads/bind/), se suele ejecutar en Linux.</span><span class="sxs-lookup"><span data-stu-id="49690-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="49690-114">Actualmente hay dos versiones de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="49690-115">CLI1.0 se basa en Node.js y tiene comandos que comienzan por "azure".</span><span class="sxs-lookup"><span data-stu-id="49690-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="49690-116">CLI2.0 se basa en Python y tiene comandos que empiezan por "az".</span><span class="sxs-lookup"><span data-stu-id="49690-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="49690-117">Aunque se admite la importación de archivos de zona en ambas versiones, se recomienda utilizar los comandos CLI1.0, como se describe en esta página.</span><span class="sxs-lookup"><span data-stu-id="49690-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="49690-118">Obtención del archivo de zona DNS existente</span><span class="sxs-lookup"><span data-stu-id="49690-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="49690-119">Antes de importar un archivo de zona DNS a DNS de Azure, debe obtener una copia del archivo de zona.</span><span class="sxs-lookup"><span data-stu-id="49690-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="49690-120">El origen de este archivo varía en función de dónde se hospede la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="49690-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="49690-121">Si la zona DNS se hospeda en un servicio de colaboradores (como un registrador de dominios, un proveedor de hospedaje DNS dedicado o un proveedor de nube alternativo), ese servicio debería ofrecer la posibilidad de descargar el archivo de zona DNS.</span><span class="sxs-lookup"><span data-stu-id="49690-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="49690-122">Si la zona DNS se hospeda en DNS de Windows, la carpeta predeterminada para los archivos de zona es **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="49690-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="49690-123">También se muestra la ruta de acceso completa de cada archivo de zona en la pestaña **General** de la consola de DNS.</span><span class="sxs-lookup"><span data-stu-id="49690-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="49690-124">Si la zona DNS se hospeda con BIND, la ubicación del archivo de zona para cada zona se especifica en el archivo de configuración de BIND **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="49690-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="49690-125">Los archivos de zona descargados de GoDaddy tienen un formato ligeramente diferente al estándar.</span><span class="sxs-lookup"><span data-stu-id="49690-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="49690-126">Debe corregir esto antes de importar estos archivos de zona a DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="49690-127">Se especifican los nombres DNS en el campo RDATA de cada registro DNS como nombres completos, pero no terminan en ".". Esto significa que otros sistemas DNS los interpretan como nombres relativos.</span><span class="sxs-lookup"><span data-stu-id="49690-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="49690-128">Debe editar el archivo de zona para anexar el carácter final "." a los nombres antes de importarlos a DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="49690-129">Por ejemplo, el registro CNAME "www 3600 IN CNAME contoso.com" debe cambiarse a "www 3600 IN CNAME contoso.com."</span><span class="sxs-lookup"><span data-stu-id="49690-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="49690-130">(con una terminación ".").</span><span class="sxs-lookup"><span data-stu-id="49690-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="49690-131">Importación de un archivo de zona DNS a DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="49690-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="49690-132">Si aún no existe, al importar un archivo de zona se crea una nueva zona DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="49690-133">Si la zona ya existe, los conjuntos de registros de la zona deben combinarse con los conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="49690-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="49690-134">Comportamiento de combinación</span><span class="sxs-lookup"><span data-stu-id="49690-134">Merge behavior</span></span>

* <span data-ttu-id="49690-135">De forma predeterminada, se combinan los conjuntos de registros nuevos y existentes.</span><span class="sxs-lookup"><span data-stu-id="49690-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="49690-136">Los registros idénticos dentro de un conjunto de registros combinado se desduplican.</span><span class="sxs-lookup"><span data-stu-id="49690-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="49690-137">También puede especificar la opción `--force`, para que el proceso de importación reemplace los conjuntos de registros existentes por otros nuevos.</span><span class="sxs-lookup"><span data-stu-id="49690-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="49690-138">os conjuntos de registros existentes que no tengan un registro correspondiente en el archivo de zona importado no se eliminan.</span><span class="sxs-lookup"><span data-stu-id="49690-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="49690-139">Cuando se combinan conjuntos de registros, se usa el período de vida (TTL) de los conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="49690-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="49690-140">Cuando se usa `--force`, se utiliza el TTL del nuevo conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="49690-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="49690-141">Los parámetros de inicio de autoridad (SOA), a excepción de `host`, siempre se toman del archivo de zona importado, independientemente de si se usa `--force` o no.</span><span class="sxs-lookup"><span data-stu-id="49690-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="49690-142">De forma similar, para el conjunto de registros de servidor de nombres en el ápice de zona, el TTL siempre se toma del archivo de zona importado.</span><span class="sxs-lookup"><span data-stu-id="49690-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="49690-143">Un registro CNAME importado no reemplaza a un registro CNAME existente con el mismo nombre, a menos que se especifique el parámetro `--force`.</span><span class="sxs-lookup"><span data-stu-id="49690-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="49690-144">Cuando surge un conflicto entre un registro CNAME y otro registro del mismo nombre pero de distinto tipo (sin importar cuál sea el existente y cuál el nuevo), se conserva el registro existente.</span><span class="sxs-lookup"><span data-stu-id="49690-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="49690-145">Esto sucede con independencia del uso de `--force`.</span><span class="sxs-lookup"><span data-stu-id="49690-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="49690-146">Información adicional sobre la importación</span><span class="sxs-lookup"><span data-stu-id="49690-146">Additional information about importing</span></span>

<span data-ttu-id="49690-147">En las notas siguientes, se ofrecen detalles técnicos adicionales sobre el proceso de importación de zona.</span><span class="sxs-lookup"><span data-stu-id="49690-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="49690-148">La directiva `$TTL` es opcional y se admite.</span><span class="sxs-lookup"><span data-stu-id="49690-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="49690-149">Cuando no se indica ninguna directiva `$TTL`, los registros sin TTL explícito se importan con un TTL predeterminado de 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="49690-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="49690-150">Cuando dos registros del mismo conjunto de registros especifican diferentes TTL, se usa el valor más bajo.</span><span class="sxs-lookup"><span data-stu-id="49690-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="49690-151">La directiva `$ORIGIN` es opcional y se admite.</span><span class="sxs-lookup"><span data-stu-id="49690-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="49690-152">Cuando no se establece ninguna directiva `$ORIGIN` , el valor predeterminado que se usa es el nombre de la zona según lo especificado en la línea de comandos (terminado en ".").</span><span class="sxs-lookup"><span data-stu-id="49690-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="49690-153">No se admiten las directivas `$INCLUDE` ni `$GENERATE`.</span><span class="sxs-lookup"><span data-stu-id="49690-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="49690-154">Se admiten los tipos de registro siguientes: A, AAAA, CNAME, MX, NS, SOA, SRV y TXT.</span><span class="sxs-lookup"><span data-stu-id="49690-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="49690-155">DNS de Azure crea automáticamente el registro SOA cuando se crea una zona.</span><span class="sxs-lookup"><span data-stu-id="49690-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="49690-156">Cuando se importa un archivo de zona, todos los parámetros SOA se toman del archivo de zona *excepto* el parámetro `host`.</span><span class="sxs-lookup"><span data-stu-id="49690-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="49690-157">Este parámetro usa el valor proporcionado por DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="49690-158">Esto se debe a que este parámetro debe hacer referencia al servidor de nombres principal proporcionado por DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="49690-159">DNS de Azure también crea automáticamente el conjunto de registros de servidor de nombres en el ápice de zona al crear la zona.</span><span class="sxs-lookup"><span data-stu-id="49690-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="49690-160">Solo se importa el TTL de este conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="49690-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="49690-161">Estos registros contienen los nombres de servidores de nombres proporcionados por DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="49690-162">No se sobrescriben los datos del registro con los valores contenidos en el archivo de zona importado.</span><span class="sxs-lookup"><span data-stu-id="49690-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="49690-163">Durante la versión preliminar pública, DNS de Azure admite solamente registros TXT de cadena única.</span><span class="sxs-lookup"><span data-stu-id="49690-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="49690-164">Los registros TXT multicadena se concatenan y se truncan tras 255 caracteres.</span><span class="sxs-lookup"><span data-stu-id="49690-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="49690-165">Valores y formato de la CLI</span><span class="sxs-lookup"><span data-stu-id="49690-165">CLI format and values</span></span>

<span data-ttu-id="49690-166">El formato del comando de CLI de Azure para importar una zona DNS es:</span><span class="sxs-lookup"><span data-stu-id="49690-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="49690-167">Valores:</span><span class="sxs-lookup"><span data-stu-id="49690-167">Values:</span></span>

* <span data-ttu-id="49690-168">`<resource group>` es el nombre del grupo de recursos para la zona en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="49690-169">`<zone name>` es el nombre de la zona.</span><span class="sxs-lookup"><span data-stu-id="49690-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="49690-170">`<zone file name>` es la ruta de acceso y el nombre del archivo de zona que se va a importar.</span><span class="sxs-lookup"><span data-stu-id="49690-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="49690-171">Si no existe una zona con este nombre en el grupo de recursos, se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="49690-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="49690-172">Si la zona ya existe, los conjuntos de registros importados se combinan con conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="49690-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="49690-173">Para sobrescribir los conjuntos de registros existentes, use la opción `--force` .</span><span class="sxs-lookup"><span data-stu-id="49690-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="49690-174">Para comprobar el formato de un archivo de zona sin importarlo, use la opción `--parse-only` .</span><span class="sxs-lookup"><span data-stu-id="49690-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="49690-175">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="49690-175">Step 1.</span></span> <span data-ttu-id="49690-176">Importación de un archivo de zona</span><span class="sxs-lookup"><span data-stu-id="49690-176">Import a zone file</span></span>

<span data-ttu-id="49690-177">Para importar un archivo de zona para la zona **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="49690-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="49690-178">Inicie sesión en su suscripción de Azure mediante la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="49690-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="49690-179">Seleccione la suscripción en la que quiere crear la nueva zona DNS.</span><span class="sxs-lookup"><span data-stu-id="49690-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="49690-180">DNS de Azure es un servicio exclusivo del Administrador de recursos de Azure, así que se debe cambiar la CLI de Azure al modo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="49690-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="49690-181">Antes de usar el servicio DNS de Azure, debe registrar la suscripción para que utilice el proveedor de recursos Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="49690-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="49690-182">(Se trata de una operación única para cada suscripción).</span><span class="sxs-lookup"><span data-stu-id="49690-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="49690-183">Si todavía no tiene uno, debe crear también un grupo de recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49690-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="49690-184">Para importar la zona **contoso.com** del archivo **contoso.com.txt** a una nueva zona DNS en el grupo de recursos **myresourcegroup**, ejecute el comando `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="49690-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="49690-185">Con este comando se carga el archivo de zona y se analiza.</span><span class="sxs-lookup"><span data-stu-id="49690-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="49690-186">El comando ejecuta una serie de comandos en el servicio DNS de Azure para crear la zona y todos los conjuntos de registros de la zona.</span><span class="sxs-lookup"><span data-stu-id="49690-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="49690-187">El comando notifica el progreso en la ventana de la consola, junto con los errores o las advertencias.</span><span class="sxs-lookup"><span data-stu-id="49690-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="49690-188">Puesto que los conjuntos de registros se crean en serie, puede tardar unos minutos en importar un archivo de zona de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="49690-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="49690-189">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="49690-189">Step 2.</span></span> <span data-ttu-id="49690-190">Comprobación de la zona</span><span class="sxs-lookup"><span data-stu-id="49690-190">Verify the zone</span></span>

<span data-ttu-id="49690-191">Para comprobar la zona DNS después de importar el archivo, puede utilizar cualquiera de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="49690-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="49690-192">Puede mostrar una lista de los registros mediante el siguiente comando de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="49690-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="49690-193">Puede enumerar los registros mediante el cmdlet de PowerShell `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="49690-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="49690-194">O puede utilizar `nslookup` para comprobar la resolución de nombres para los registros.</span><span class="sxs-lookup"><span data-stu-id="49690-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="49690-195">Como la zona aún no está delegada, debe especificar explícitamente los servidores de nombres DNS de Azure correctos.</span><span class="sxs-lookup"><span data-stu-id="49690-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="49690-196">En el ejemplo siguiente se muestra cómo recuperar los nombres de servidores de nombres asignados a la zona.</span><span class="sxs-lookup"><span data-stu-id="49690-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="49690-197">También muestra cómo consultar el registro "www" mediante `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="49690-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="49690-198">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="49690-198">Step 3.</span></span> <span data-ttu-id="49690-199">Actualización de la delegación de DNS</span><span class="sxs-lookup"><span data-stu-id="49690-199">Update DNS delegation</span></span>

<span data-ttu-id="49690-200">Una vez que haya comprobado que la zona se importó correctamente, debe actualizar la delegación de DNS para que apunte a los servidores de nombres DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="49690-201">Para más información, consulte el artículo [Delegación de un dominio en DNS de Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="49690-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="49690-202">Exportación de un archivo de zona DNS de DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="49690-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="49690-203">El formato del comando de CLI de Azure para importar una zona DNS es:</span><span class="sxs-lookup"><span data-stu-id="49690-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="49690-204">Valores:</span><span class="sxs-lookup"><span data-stu-id="49690-204">Values:</span></span>

* <span data-ttu-id="49690-205">`<resource group>` es el nombre del grupo de recursos para la zona en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="49690-206">`<zone name>` es el nombre de la zona.</span><span class="sxs-lookup"><span data-stu-id="49690-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="49690-207">`<zone file name>` es la ruta de acceso y el nombre del archivo de zona que se va a exportar.</span><span class="sxs-lookup"><span data-stu-id="49690-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="49690-208">Al igual que con la importación de zona, en primer lugar necesita iniciar sesión, elegir su suscripción y configurar la CLI de Azure para que use el modo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="49690-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="49690-209">Para exportar un archivo de zona</span><span class="sxs-lookup"><span data-stu-id="49690-209">To export a zone file</span></span>

1. <span data-ttu-id="49690-210">Inicie sesión en su suscripción de Azure mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="49690-211">Seleccione la suscripción en la que desee crear la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="49690-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="49690-212">DNS de Azure es un servicio exclusivo del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="49690-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="49690-213">Se debe cambiar la CLI de Azure al modo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="49690-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="49690-214">Para exportar la zona DNS de Azure existente **contoso.com** en el grupo de recursos **myresourcegroup** al archivo **contoso.com.txt** (en la carpeta actual), ejecute `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="49690-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="49690-215">Este comando llama al servicio DNS de Azure para enumerar los conjuntos de registros de la zona y exportar los resultados a un archivo de zona compatible con BIND.</span><span class="sxs-lookup"><span data-stu-id="49690-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
