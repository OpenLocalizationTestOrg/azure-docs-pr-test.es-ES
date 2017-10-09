---
title: "aaaImport y exportación de una zona de dominio archivo tooAzure DNS mediante Azure CLI 1.0 | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooimport y exportar un DNS de zona DNS del archivo tooAzure mediante el uso de Azure CLI 1.0"
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
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="d651f-103">Importar y exportar un archivo de zona DNS mediante Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d651f-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="d651f-104">Este artículo le guiará a través de cómo tooimport y exportación de archivos de zona DNS para el uso de DNS de Azure Hola 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="d651f-105">Migración de zona tooDNS de introducción</span><span class="sxs-lookup"><span data-stu-id="d651f-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="d651f-106">Un archivo de zona DNS es un archivo de texto que contiene los detalles de cada registro de sistema de nombres de dominio (DNS) en la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="d651f-107">Sigue un formato estándar, por lo que es adecuado para transferir registros DNS entre distintos sistemas DNS.</span><span class="sxs-lookup"><span data-stu-id="d651f-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="d651f-108">Mediante un archivo de zona es una rápida, confiable y cómodamente tootransfer una zona DNS dentro o fuera de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="d651f-109">DNS de Azure admite la importación y exportación de archivos de zona mediante el uso de hello Azure interfaz de línea de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="d651f-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="d651f-110">Importación de archivos de zona es **no** admiten a través de Azure PowerShell u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="d651f-111">Hola 1.0 de CLI de Azure es una herramienta de línea de comandos multiplataforma utilizada para administrar los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="d651f-112">Está disponible para plataformas de Windows, Mac y Linux de Hola de hello [página de descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d651f-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="d651f-113">La compatibilidad multiplataforma es importante para importar y exportar archivos de zona, porque Hola software más comunes del servidor de nombre, [enlazar](https://www.isc.org/downloads/bind/), normalmente se ejecuta en Linux.</span><span class="sxs-lookup"><span data-stu-id="d651f-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="d651f-114">Actualmente hay dos versiones de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="d651f-115">CLI1.0 se basa en Node.js y tiene comandos que comienzan por "azure".</span><span class="sxs-lookup"><span data-stu-id="d651f-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="d651f-116">CLI2.0 se basa en Python y tiene comandos que empiezan por "az".</span><span class="sxs-lookup"><span data-stu-id="d651f-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="d651f-117">Aunque se admite la importación de archivos de zona en ambas versiones, se recomienda usar comandos CLI1.0 hello, como se describe en esta página.</span><span class="sxs-lookup"><span data-stu-id="d651f-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="d651f-118">Obtención del archivo de zona DNS existente</span><span class="sxs-lookup"><span data-stu-id="d651f-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="d651f-119">Antes de importar un archivo de zona DNS en DNS de Azure, deberá tooobtain una copia del archivo de zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="d651f-120">origen de Hola de este archivo depende de donde se hospeda actualmente la zona DNS Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="d651f-121">Si la zona DNS está hospedada por un servicio de socios comerciales (como un registrador de dominios, un proveedor de hospedaje de DNS dedicado o un proveedor alternativo en la nube), que el servicio debe proporcionar el archivo de zona DNS de hello capacidad toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="d651f-122">Si la zona DNS está hospedada en el DNS de Windows, carpeta de archivos de zona de Hola de hello predeterminada es **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="d651f-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="d651f-123">archivo de zona de tooeach de ruta de acceso completa de Hello también se muestra en hello **General** ficha de consola DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="d651f-124">Si la zona DNS está hospedada por mediante un enlace, la ubicación de Hola Hola del archivo de zona para cada zona se especifica en el archivo de configuración de enlace de hello **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="d651f-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="d651f-125">Los archivos de zona descargados de GoDaddy tienen un formato ligeramente diferente al estándar.</span><span class="sxs-lookup"><span data-stu-id="d651f-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="d651f-126">Necesita toocorrect esto antes de importar estos archivos de zona DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="d651f-127">Se especifican nombres DNS en hello RDATA de cada registro DNS como nombres completos, pero no tienen una finalización "." Esto significa que otros sistemas DNS los interpretan como nombres relativos.</span><span class="sxs-lookup"><span data-stu-id="d651f-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="d651f-128">Debe terminar de tooedit Hola zona archivo tooappend Hola "." tootheir nombres antes de importarlos en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="d651f-129">Por ejemplo, hello registro CNAME "" www 3600 en contoso.com CNAME"debe cambiarse demasiado"www 3600 CNAME en contoso.com."</span><span class="sxs-lookup"><span data-stu-id="d651f-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="d651f-130">(con una terminación ".").</span><span class="sxs-lookup"><span data-stu-id="d651f-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="d651f-131">Importación de un archivo de zona DNS a DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="d651f-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="d651f-132">Si aún no existe, al importar un archivo de zona se crea una nueva zona DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="d651f-133">Si ya existe una zona de hello, hello conjuntos de registros de archivo de zona de hello deben combinarse con conjuntos de registros existentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="d651f-134">Comportamiento de combinación</span><span class="sxs-lookup"><span data-stu-id="d651f-134">Merge behavior</span></span>

* <span data-ttu-id="d651f-135">De forma predeterminada, se combinan los conjuntos de registros nuevos y existentes.</span><span class="sxs-lookup"><span data-stu-id="d651f-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="d651f-136">Los registros idénticos dentro de un conjunto de registros combinado se desduplican.</span><span class="sxs-lookup"><span data-stu-id="d651f-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="d651f-137">O bien, mediante la especificación de hello `--force` opción, Hola reemplaza de proceso de importación conjuntos de registro existente con nuevos conjuntos de registros.</span><span class="sxs-lookup"><span data-stu-id="d651f-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="d651f-138">Conjuntos de registros existentes que no tienen un registro correspondiente establecido en el archivo de zona importado hello no se quitará.</span><span class="sxs-lookup"><span data-stu-id="d651f-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="d651f-139">Cuando se combinan los conjuntos de registros, hello tiempo toolive (TTL) de conjuntos de registros preexistentes se usa.</span><span class="sxs-lookup"><span data-stu-id="d651f-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="d651f-140">Cuando `--force` es utilizado, se usa Hola TTL del nuevo conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="d651f-141">Inicio de parámetros de autoridad (SOA) (excepto `host`) siempre se toman del archivo de zona importado hello, independientemente de si `--force` se utiliza.</span><span class="sxs-lookup"><span data-stu-id="d651f-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="d651f-142">De forma similar, para establecer en vértice de la zona de Hola Hola registro de servidor de nombres, hello TTL siempre se toma del archivo de zona importado Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="d651f-143">Un registro CNAME importado no reemplaza un CNAME existente grabar con hello mismo nombre, a menos que hello `--force` se especifica el parámetro.</span><span class="sxs-lookup"><span data-stu-id="d651f-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="d651f-144">Cuando se produce un conflicto entre un registro CNAME y otro registro de hello mismo nombre pero es diferente, escriba (sin tener en cuenta que es existente o nueva), se conserva el registro existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="d651f-145">Este valor es independiente del uso de Hola de `--force`.</span><span class="sxs-lookup"><span data-stu-id="d651f-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="d651f-146">Información adicional sobre la importación</span><span class="sxs-lookup"><span data-stu-id="d651f-146">Additional information about importing</span></span>

<span data-ttu-id="d651f-147">Hello notas siguientes proporcionan detalles técnicos adicionales acerca de la zona de hello el proceso de importación.</span><span class="sxs-lookup"><span data-stu-id="d651f-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="d651f-148">Hola `$TTL` directiva es opcional y se admite.</span><span class="sxs-lookup"><span data-stu-id="d651f-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="d651f-149">Si no `$TTL` recibe la directiva, se importan los registros sin un TTL explícito establecer tooa TTL predeterminado de 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="d651f-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="d651f-150">Cuando dos registros en hello mismo conjunto de registros especifica TTLs diferentes, se usa un valor inferior Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="d651f-151">Hola `$ORIGIN` directiva es opcional y se admite.</span><span class="sxs-lookup"><span data-stu-id="d651f-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="d651f-152">Si no `$ORIGIN` se establece, el valor predeterminado de hello valor utilizado es el nombre de la zona de hello según se especifica en la línea de comandos de hello (además de terminación de Hola ".").</span><span class="sxs-lookup"><span data-stu-id="d651f-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="d651f-153">Hola `$INCLUDE` y `$GENERATE` no se admiten directivas.</span><span class="sxs-lookup"><span data-stu-id="d651f-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="d651f-154">Se admiten los tipos de registro siguientes: A, AAAA, CNAME, MX, NS, SOA, SRV y TXT.</span><span class="sxs-lookup"><span data-stu-id="d651f-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="d651f-155">Hola registro SOA DNS de Azure se crea automáticamente cuando se crea una zona.</span><span class="sxs-lookup"><span data-stu-id="d651f-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="d651f-156">Cuando se importa un archivo de zona, todos los parámetros SOA se toman del archivo de zona de hello *excepto* hello `host` parámetro.</span><span class="sxs-lookup"><span data-stu-id="d651f-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="d651f-157">Este parámetro usa valor Hola proporcionada por DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="d651f-158">Esto es porque este parámetro debe hacer referencia a servidor de nombre principal de toohello proporcionado por DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="d651f-159">registro de servidor de nombres Hola establecido en vértice de la zona de hello también se crea automáticamente DNS de Azure cuando se crea la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="d651f-160">Solo hello TTL de este conjunto de registros se importa.</span><span class="sxs-lookup"><span data-stu-id="d651f-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="d651f-161">Estos registros contienen nombres de servidor de nombre de hello proporcionados por DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="d651f-162">valores de hello contenidos en el archivo de zona importado hello no sobrescribe los datos de registro de Hello.</span><span class="sxs-lookup"><span data-stu-id="d651f-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="d651f-163">Durante la versión preliminar pública, DNS de Azure admite solamente registros TXT de cadena única.</span><span class="sxs-lookup"><span data-stu-id="d651f-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="d651f-164">MultiString registros TXT se pueden too255 concatenados y el truncado caracteres.</span><span class="sxs-lookup"><span data-stu-id="d651f-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="d651f-165">Valores y formato de la CLI</span><span class="sxs-lookup"><span data-stu-id="d651f-165">CLI format and values</span></span>

<span data-ttu-id="d651f-166">formato de Hola de tooimport de comando de CLI de Azure de hello una zona DNS es:</span><span class="sxs-lookup"><span data-stu-id="d651f-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="d651f-167">Valores:</span><span class="sxs-lookup"><span data-stu-id="d651f-167">Values:</span></span>

* <span data-ttu-id="d651f-168">`<resource group>`es el nombre de Hola Hola del grupo de recursos para la zona de hello en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="d651f-169">`<zone name>`es el nombre de Hola de zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="d651f-170">`<zone file name>`es Hola/nombre de ruta de hello zona archivo toobe importado.</span><span class="sxs-lookup"><span data-stu-id="d651f-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="d651f-171">Si una zona con este nombre no existe en el grupo de recursos de hello, se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d651f-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="d651f-172">Si hello zona ya existe, hello conjuntos de registros importados se combinan con los conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="d651f-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="d651f-173">toooverwrite Hola existente conjuntos de registros, usar hello `--force` opción.</span><span class="sxs-lookup"><span data-stu-id="d651f-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="d651f-174">formato de hello tooverify de un archivo de zona sin realmente importarlo, use hello `--parse-only` opción.</span><span class="sxs-lookup"><span data-stu-id="d651f-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="d651f-175">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="d651f-175">Step 1.</span></span> <span data-ttu-id="d651f-176">Importación de un archivo de zona</span><span class="sxs-lookup"><span data-stu-id="d651f-176">Import a zone file</span></span>

<span data-ttu-id="d651f-177">un archivo de zona para la zona de hello tooimport **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d651f-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="d651f-178">Inicie sesión en tooyour suscripción de Azure mediante Hola 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="d651f-179">Seleccione la suscripción de Hola donde desea toocreate la nueva zona DNS.</span><span class="sxs-lookup"><span data-stu-id="d651f-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="d651f-180">DNS de Azure es un servicio de Azure solo el Administrador de recursos, por lo que Hola CLI de Azure debe ser el modo de administrador tooResource desactivados.</span><span class="sxs-lookup"><span data-stu-id="d651f-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="d651f-181">Antes de usar el servicio DNS de Azure de hello, debe registrar el proveedor de recursos de Microsoft.Network de suscripción toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="d651f-182">(Se trata de una operación única para cada suscripción).</span><span class="sxs-lookup"><span data-stu-id="d651f-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="d651f-183">Si no tiene ninguno todavía, también deberá toocreate un grupo de recursos del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="d651f-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="d651f-184">zona de hello tooimport **contoso.com** desde archivo hello **contoso.com.txt** en una nueva zona DNS en el grupo de recursos de hello **myresourcegroup**, ejecute el comando de hello `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="d651f-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="d651f-185">Este comando carga el archivo de zona de hello y analizarlo.</span><span class="sxs-lookup"><span data-stu-id="d651f-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="d651f-186">una serie de comandos ejecuta el comando de Hello en zona de hello Azure DNS servicio toocreate hello y todos los registros de Hola se establece en la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="d651f-187">Hola comando informa del progreso en la ventana de la consola de hello, junto con los errores o advertencias.</span><span class="sxs-lookup"><span data-stu-id="d651f-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="d651f-188">Como conjuntos de registros se crean en serie, puede tardar unos tooimport minutos un archivo de zona de gran tamaño.</span><span class="sxs-lookup"><span data-stu-id="d651f-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="d651f-189">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="d651f-189">Step 2.</span></span> <span data-ttu-id="d651f-190">Compruebe la zona de Hola</span><span class="sxs-lookup"><span data-stu-id="d651f-190">Verify hello zone</span></span>

<span data-ttu-id="d651f-191">tooverify Hola zona de DNS después de importar el archivo hello, puede usar cualquiera de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="d651f-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="d651f-192">Puede enumerar los registros de hello mediante Hola siguiente comando de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="d651f-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="d651f-193">Puede enumerar los registros de hello mediante cmdlet de PowerShell de hello `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="d651f-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="d651f-194">Puede usar `nslookup` tooverify la resolución de nombres para los registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="d651f-195">Como zona de hello no delega todavía, deberá servidores de nombres de DNS de Azure correcta de toospecify Hola explícitamente.</span><span class="sxs-lookup"><span data-stu-id="d651f-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="d651f-196">Hello en el ejemplo siguiente muestra cómo nombres de servidor de nombre de tooretrieve Hola asignan toohello zona.</span><span class="sxs-lookup"><span data-stu-id="d651f-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="d651f-197">TI también muestra cómo grabar utilizando tooquery Hola "www" `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="d651f-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="d651f-198">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="d651f-198">Step 3.</span></span> <span data-ttu-id="d651f-199">Actualización de la delegación de DNS</span><span class="sxs-lookup"><span data-stu-id="d651f-199">Update DNS delegation</span></span>

<span data-ttu-id="d651f-200">Después de comprobar que la zona de Hola se ha importado correctamente, necesita tooupdate Hola DNS delegación toopoint toohello servidores de nombres DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="d651f-201">Para obtener más información, vea el artículo de hello [actualizar delegación DNS de hello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="d651f-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="d651f-202">Exportación de un archivo de zona DNS de DNS de Azure</span><span class="sxs-lookup"><span data-stu-id="d651f-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="d651f-203">formato de Hola de tooimport de comando de CLI de Azure de hello una zona DNS es:</span><span class="sxs-lookup"><span data-stu-id="d651f-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="d651f-204">Valores:</span><span class="sxs-lookup"><span data-stu-id="d651f-204">Values:</span></span>

* <span data-ttu-id="d651f-205">`<resource group>`es el nombre de Hola Hola del grupo de recursos para la zona de hello en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="d651f-206">`<zone name>`es el nombre de Hola de zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="d651f-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="d651f-207">`<zone file name>`es Hola/nombre de ruta de toobe de archivo de zona Hola exportado.</span><span class="sxs-lookup"><span data-stu-id="d651f-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="d651f-208">Como con la importación de la zona de hello, primero debe toosign en, elija su suscripción y configurar el modo de administrador de recursos de toouse de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="d651f-209">tooexport un archivo de zona</span><span class="sxs-lookup"><span data-stu-id="d651f-209">tooexport a zone file</span></span>

1. <span data-ttu-id="d651f-210">Inicie sesión en tooyour suscripción de Azure mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="d651f-211">Seleccione la suscripción de Hola donde desea toocreate la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="d651f-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="d651f-212">DNS de Azure es un servicio exclusivo del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d651f-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="d651f-213">Hola CLI de Azure debe ser el modo de administrador tooResource desactivados.</span><span class="sxs-lookup"><span data-stu-id="d651f-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="d651f-214">tooexport Hola zona DNS de Azure existente **contoso.com** en grupo de recursos **myresourcegroup** toohello archivo **contoso.com.txt** (en la carpeta actual de hello), ejecute `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="d651f-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="d651f-215">Este comando llama Hola tooenumerate del servicio DNS de Azure conjuntos de registros en la zona de Hola y Exportar archivo de zona de hello resultados tooa compatible con el enlace.</span><span class="sxs-lookup"><span data-stu-id="d651f-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
