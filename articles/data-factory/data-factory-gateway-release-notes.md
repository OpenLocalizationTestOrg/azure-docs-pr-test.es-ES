---
title: notas de la aaaRelease de Data Management Gateway | Documentos de Microsoft
description: "Notas de la versión de Data Management Gateway"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="44e53-103">Notas de la versión de Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="44e53-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="44e53-104">Uno de los desafíos de hello para la integración de datos modernas es toomove datos tooand desde toocloud local.</span><span class="sxs-lookup"><span data-stu-id="44e53-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="44e53-105">Factoría de datos hace que esta integración con Data Management Gateway, que es un agente que puede instalar el movimiento de datos local tooenable híbrida.</span><span class="sxs-lookup"><span data-stu-id="44e53-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="44e53-106">Vea Hola siguientes artículos para obtener información detallada acerca de la puerta de enlace de datos de administración y cómo toouse:</span><span class="sxs-lookup"><span data-stu-id="44e53-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="44e53-107">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="44e53-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="44e53-108">Movimiento de datos entre una ubicación local y la nube mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="44e53-109">VERSIÓN ACTUAL (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="44e53-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="44e53-110">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="44e53-110">Enhancements-</span></span>
- <span data-ttu-id="44e53-111">Puede agregar bus de servicio de toowhitelist de las entradas DNS en lugar de crear listas blancas con todas las direcciones IP de Azure desde el servidor de seguridad (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="44e53-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="44e53-112">Puede encontrar la entrada DNS correspondiente en Azure Portal (Data Factory -> "Crear e implementar" -> "Puertas de enlace" -> "serviceUrls" (en JSON)</span><span class="sxs-lookup"><span data-stu-id="44e53-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="44e53-113">El conector HDFS admite ahora certificados públicos autofirmados para poder omitir la validación de SSL.</span><span class="sxs-lookup"><span data-stu-id="44e53-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="44e53-114">Corregido: Problema con la puerta de enlace sin conexión durante la actualización (vence tooclock sesgo)</span><span class="sxs-lookup"><span data-stu-id="44e53-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="44e53-115">Versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="44e53-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="44e53-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="44e53-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="44e53-117">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="44e53-117">Enhancements-</span></span>
-   <span data-ttu-id="44e53-118">Puede agregar las entradas DNS toowhitelist Bus de servicio en lugar de crear listas blancas con todas las direcciones IP de Azure desde el servidor de seguridad (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="44e53-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="44e53-119">Más detalles aquí.</span><span class="sxs-lookup"><span data-stu-id="44e53-119">More details here.</span></span>
-   <span data-ttu-id="44e53-120">Ahora puede copiar datos de un blob en bloques solo seguridad too4.75 TB, que es el tamaño de hello max compatible de blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="44e53-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="44e53-121">(el límite anterior era 195 GB).</span><span class="sxs-lookup"><span data-stu-id="44e53-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="44e53-122">Problema solucionado: memoria agotada al descomprimir varios archivos pequeños durante la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="44e53-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="44e53-123">Problema corregido: Índice fuera del problema de intervalo mientras se copiaba del tooan de base de datos de documentos en SQL Server local con la característica de idempotencia.</span><span class="sxs-lookup"><span data-stu-id="44e53-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="44e53-124">Problema solucionado: el script de limpieza SQL no funciona en la instancia de SQL Server local desde el Asistente para copia.</span><span class="sxs-lookup"><span data-stu-id="44e53-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="44e53-125">Problema corregido: Nombre de la columna con espacio final hello no funciona en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="44e53-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="44e53-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="44e53-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="44e53-127">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="44e53-127">Enhancements-</span></span>
- <span data-ttu-id="44e53-128">Problema solucionado: falta de credenciales durante el reinicio de máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="44e53-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="44e53-129">Solucionado: problema de registro durante la restauración de la puerta de enlace mediante un archivo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="44e53-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="44e53-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="44e53-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="44e53-131">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="44e53-131">Enhancements-</span></span>
- <span data-ttu-id="44e53-132">Problema solucionado: lectura incorrecta de valor NULL decimal desde Oracle como origen.</span><span class="sxs-lookup"><span data-stu-id="44e53-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="44e53-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="44e53-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="44e53-134">Novedades</span><span class="sxs-lookup"><span data-stu-id="44e53-134">What’s new</span></span>
- <span data-ttu-id="44e53-135">Los clientes pueden proporcionar comentarios en la experiencia de registro de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="44e53-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="44e53-136">Nuevo formato de compresión compatible: ZIP (Deflate).</span><span class="sxs-lookup"><span data-stu-id="44e53-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="44e53-137">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="44e53-137">Enhancements-</span></span>
- <span data-ttu-id="44e53-138">Mejora del rendimiento del origen de HDFS y el receptor de Oracle.</span><span class="sxs-lookup"><span data-stu-id="44e53-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="44e53-139">Corrección de errores de la capacidad de procesamiento en paralelo y la actualización automática de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="44e53-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="44e53-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="44e53-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="44e53-141">Mejoras</span><span class="sxs-lookup"><span data-stu-id="44e53-141">Enhancements</span></span>
- <span data-ttu-id="44e53-142">Mejorada y más sólida puerta de enlace registro experiencia: ahora puede realizar el seguimiento del estado del progreso durante el proceso de registro de puerta de enlace de hello, lo que permite el registro de hello experimentar mayor capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="44e53-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="44e53-143">Mejora de la puerta de enlace restaurar proceso - que todavía puede recuperar la puerta de enlace incluso si no tiene archivos de copia de seguridad de puerta de enlace de hello con esta actualización.</span><span class="sxs-lookup"><span data-stu-id="44e53-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="44e53-144">Esto requeriría tooreset las credenciales de servicio vinculado en el Portal.</span><span class="sxs-lookup"><span data-stu-id="44e53-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="44e53-145">Corrección de errores.</span><span class="sxs-lookup"><span data-stu-id="44e53-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="44e53-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="44e53-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="44e53-147">Novedades</span><span class="sxs-lookup"><span data-stu-id="44e53-147">What’s new</span></span>

- <span data-ttu-id="44e53-148">Ahora puede almacenar localmente las credenciales de origen de datos.</span><span class="sxs-lookup"><span data-stu-id="44e53-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="44e53-149">Hola credenciales se cifran.</span><span class="sxs-lookup"><span data-stu-id="44e53-149">hello credentials are encrypted.</span></span> <span data-ttu-id="44e53-150">las credenciales del origen de datos de Hola se pueden recuperar y restauran con el archivo de copia de seguridad de hello que se pueden exportar desde Hola existente de la puerta de enlace local en todos los.</span><span class="sxs-lookup"><span data-stu-id="44e53-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="44e53-151">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="44e53-151">Enhancements-</span></span>

- <span data-ttu-id="44e53-152">Experiencia de registro de puerta de enlace mejorada y más eficaz.</span><span class="sxs-lookup"><span data-stu-id="44e53-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="44e53-153">Compatibilidad con detección automática de la configuración de QuoteChar texto sin formato en el Asistente para copiar y mejorar Hola precisión en la detección de formato general.</span><span class="sxs-lookup"><span data-stu-id="44e53-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="44e53-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="44e53-154">2.3.6100.2</span></span>

- <span data-ttu-id="44e53-155">Compatibilidad con la detección automática de firstRowAsHeader y SkipLineCount en el Asistente para copia para archivos de texto en el sistema de archivos local y HDFS.</span><span class="sxs-lookup"><span data-stu-id="44e53-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="44e53-156">Mejorar la estabilidad de Hola de conexión de red entre la puerta de enlace y el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="44e53-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="44e53-157">Unas pocas correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="44e53-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="44e53-158">2.2.6072.1</span></span>

*  <span data-ttu-id="44e53-159">Admite la configuración de proxy HTTP para el uso de la puerta de enlace de Hola Hola puerta de enlace de Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="44e53-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="44e53-160">Si está configurado, se accede a Blob de Azure, Tabla de Azure, Azure Data Lake y DocumentDB a través del proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="44e53-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="44e53-161">Encabezado de admite el control de TextFormat cuando se copian datos desde / tooAzure Blob, almacén de Azure Data Lake, sistema de archivos local y HDFS local.</span><span class="sxs-lookup"><span data-stu-id="44e53-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="44e53-162">Permite copiar los datos de Blob de anexar y Blob en páginas junto con hello ya admite Blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="44e53-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="44e53-163">Presenta un nuevo estado de puerta de enlace **en línea (limitado)**, lo que indica que esa funcionalidad principal de Hola de puerta de enlace de hello funciona excepto la compatibilidad con la operación interactiva de hello para el Asistente para copiar.</span><span class="sxs-lookup"><span data-stu-id="44e53-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="44e53-164">Mejora la solidez del saludo del registro de puerta de enlace con la clave de registro.</span><span class="sxs-lookup"><span data-stu-id="44e53-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="44e53-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="44e53-165">2.1.6040.</span></span>

*  <span data-ttu-id="44e53-166">Controlador de DB2 se incluye en el paquete de instalación de puerta de enlace de hello ahora.</span><span class="sxs-lookup"><span data-stu-id="44e53-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="44e53-167">No es necesario tooinstall lo por separado.</span><span class="sxs-lookup"><span data-stu-id="44e53-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="44e53-168">Controlador de DB2 ahora es compatible con z/OS y DB2 para (AS / 400) junto con plataformas de hello ya compatibles (Linux, Unix y Windows).</span><span class="sxs-lookup"><span data-stu-id="44e53-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="44e53-169">Admite el uso de Azure Cosmos DB como origen o destino para almacenes de datos locales</span><span class="sxs-lookup"><span data-stu-id="44e53-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="44e53-170">Permite la copia de almacenamiento de blobs de/toocold/activos de datos junto con hello ya admite la cuenta de almacenamiento general.</span><span class="sxs-lookup"><span data-stu-id="44e53-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="44e53-171">Le permite tooconnect tooon local SQL Server a través de puerta de enlace con privilegios de inicio de sesión remoto.</span><span class="sxs-lookup"><span data-stu-id="44e53-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="44e53-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="44e53-172">2.0.6013.1</span></span>

*  <span data-ttu-id="44e53-173">Puede seleccionar toobe de lenguaje o la referencia cultural de hello usa una puerta de enlace durante la instalación manual.</span><span class="sxs-lookup"><span data-stu-id="44e53-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="44e53-174">Cuando la puerta de enlace no funciona según lo previsto, puede elegir toosend registros de puerta de enlace de últimos siete días tooMicrosoft toofacilitate solución de problemas de emisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e53-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="44e53-175">Si la puerta de enlace no está conectado toohello servicio en la nube, puede elegir toosave y almacene los registros de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="44e53-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="44e53-176">Mejoras de la interfaz de usuario del Administrador de configuración de puertas de enlace:</span><span class="sxs-lookup"><span data-stu-id="44e53-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="44e53-177">Asegúrese de estado de la puerta de enlace más visible en la pestaña Inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="44e53-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="44e53-178">Controles reorganizados y simplificados.</span><span class="sxs-lookup"><span data-stu-id="44e53-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="44e53-179">Puede copiar los datos de un almacenamiento con hello [herramienta de vista previa de la copia sin código](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="44e53-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="44e53-180">Para obtener más información general sobre esta característica consulte [Copias almacenadas provisionalmente](data-factory-copy-activity-performance.md#staged-copy) .</span><span class="sxs-lookup"><span data-stu-id="44e53-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="44e53-181">Puede utilizar Data Management Gateway tooingress directamente los datos de una base de datos de SQL Server local en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="44e53-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="44e53-182">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-182">Performance improvements</span></span>

    * <span data-ttu-id="44e53-183">Se ha mejorado el rendimiento al visualizar los esquemas y la vista previa en SQL Server mediante la herramienta de vista previa de copia sin código.</span><span class="sxs-lookup"><span data-stu-id="44e53-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="44e53-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="44e53-184">1.12.5953.1</span></span>

*  <span data-ttu-id="44e53-185">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="44e53-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="44e53-186">1.11.5918.1</span></span>

*  <span data-ttu-id="44e53-187">Se ha aumentado el tamaño máximo del registro de eventos de puerta de enlace de Hola de 1 MB de too40 MB.</span><span class="sxs-lookup"><span data-stu-id="44e53-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="44e53-188">En caso de que se requiera un reinicio durante la actualización automática de la puerta de enlace, se muestra un cuadro de diálogo de advertencia.</span><span class="sxs-lookup"><span data-stu-id="44e53-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="44e53-189">Puede elegir toorestart derecha, a continuación, o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="44e53-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="44e53-190">En caso de error en la actualización automática, el instalador de puerta de enlace volverá a intentar esta operación 3 veces al máximo.</span><span class="sxs-lookup"><span data-stu-id="44e53-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="44e53-191">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-191">Performance improvements</span></span>

    * <span data-ttu-id="44e53-192">Rendimiento mejorado para la carga de tablas de gran tamaño desde el servidor local en un escenario de copia sin código.</span><span class="sxs-lookup"><span data-stu-id="44e53-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="44e53-193">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="44e53-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="44e53-194">1.10.5892.1</span></span>

*  <span data-ttu-id="44e53-195">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-195">Performance improvements</span></span>

*  <span data-ttu-id="44e53-196">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="44e53-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="44e53-197">1.9.5865.2</span></span>

*  <span data-ttu-id="44e53-198">Funcionalidad de actualización automática sin intervención del usuario</span><span class="sxs-lookup"><span data-stu-id="44e53-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="44e53-199">Icono de bandeja de nuevo con indicadores de estado de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="44e53-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="44e53-200">Capacidad demasiado "Actualizar ahora" desde el cliente de Hola</span><span class="sxs-lookup"><span data-stu-id="44e53-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="44e53-201">Hora de programación de actualización de capacidad tooset</span><span class="sxs-lookup"><span data-stu-id="44e53-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="44e53-202">Script de PowerShell para activar y desactivar la actualización automática</span><span class="sxs-lookup"><span data-stu-id="44e53-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="44e53-203">Compatibilidad con formato JSON</span><span class="sxs-lookup"><span data-stu-id="44e53-203">Support for JSON format</span></span>  
*  <span data-ttu-id="44e53-204">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-204">Performance improvements</span></span>
*  <span data-ttu-id="44e53-205">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="44e53-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="44e53-206">1.8.5822.1</span></span>

*  <span data-ttu-id="44e53-207">Mejora de la solución de problemas</span><span class="sxs-lookup"><span data-stu-id="44e53-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="44e53-208">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-208">Performance improvements</span></span>
*  <span data-ttu-id="44e53-209">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="44e53-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="44e53-210">1.7.5795.1</span></span>

*  <span data-ttu-id="44e53-211">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-211">Performance improvements</span></span>
*  <span data-ttu-id="44e53-212">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="44e53-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="44e53-213">1.7.5764.1</span></span>

*  <span data-ttu-id="44e53-214">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-214">Performance improvements</span></span>
*  <span data-ttu-id="44e53-215">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="44e53-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="44e53-216">1.6.5735.1</span></span>

*  <span data-ttu-id="44e53-217">Compatibilidad origen y receptor HDFS locales</span><span class="sxs-lookup"><span data-stu-id="44e53-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="44e53-218">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-218">Performance improvements</span></span>
*  <span data-ttu-id="44e53-219">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="44e53-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="44e53-220">1.6.5696.1</span></span>

*  <span data-ttu-id="44e53-221">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-221">Performance improvements</span></span>
*  <span data-ttu-id="44e53-222">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="44e53-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="44e53-223">1.6.5676.1</span></span>

*  <span data-ttu-id="44e53-224">Compatibilidad con herramientas de diagnóstico de Administrador de configuración</span><span class="sxs-lookup"><span data-stu-id="44e53-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="44e53-225">Columnas de la tabla de soporte técnico para orígenes de datos tabulares de la Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-226">Compatibilidad con SQL DW para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-227">Compatibilidad con Reclusive en BlobSource y FileSource para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-228">Compatibilidad con CopyBehavior - MergeFiles, PreserveHierarchy y FlattenHierarchy en BlobSink y FileSink con copia binaria para Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-229">Compatibilidad con los informes de progreso de la actividad de copia para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-230">Compatibilidad con la validación de conectividad de origen de datos para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-231">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="44e53-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="44e53-232">1.6.5672.1</span></span>

*  <span data-ttu-id="44e53-233">Compatibilidad con nombre de tabla de origen de datos ODBC para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-234">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-234">Performance improvements</span></span>
*  <span data-ttu-id="44e53-235">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="44e53-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="44e53-236">1.6.5658.1</span></span>

*  <span data-ttu-id="44e53-237">Compatibilidad con receptor de archivos para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-238">Compatibilidad con la conservación jerarquía en copia binaria para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-239">Compatibilidad con idempotencia de la actividad de copia para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-240">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="44e53-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="44e53-241">1.6.5640.1</span></span>

*  <span data-ttu-id="44e53-242">Compatibilidad con tres orígenes de datos más para Factoría de datos de Azure (ODBC, OData y HDFS)</span><span class="sxs-lookup"><span data-stu-id="44e53-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="44e53-243">Compatibilidad con carácter de comillas en el analizador de archivos .csv para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-244">Compatibilidad con compresión (BZip2)</span><span class="sxs-lookup"><span data-stu-id="44e53-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="44e53-245">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="44e53-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="44e53-246">1.5.5612.1</span></span>

*  <span data-ttu-id="44e53-247">Compatibilidad con cinco bases de datos relacionales para Data Factory de Azure (MySQL, PostgreSQL, DB2, Teradata y Sybase)</span><span class="sxs-lookup"><span data-stu-id="44e53-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="44e53-248">Compatibilidad de compresión (Gzip y Deflate)</span><span class="sxs-lookup"><span data-stu-id="44e53-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="44e53-249">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-249">Performance improvements</span></span>
*  <span data-ttu-id="44e53-250">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="44e53-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="44e53-251">1.4.5549.1</span></span>

*  <span data-ttu-id="44e53-252">Incorporación de compatibilidad de origen de datos Oracle para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44e53-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="44e53-253">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="44e53-253">Performance improvements</span></span>
*  <span data-ttu-id="44e53-254">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="44e53-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="44e53-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="44e53-255">1.4.5492.1</span></span>

*  <span data-ttu-id="44e53-256">Binario unificado que admite los servicios Factoría de datos de Microsoft Azure y Office 365 Power BI</span><span class="sxs-lookup"><span data-stu-id="44e53-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="44e53-257">Refinar el proceso de interfaz de usuario de configuración y el registro de hello</span><span class="sxs-lookup"><span data-stu-id="44e53-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="44e53-258">Factoría de datos de Azure: compatibilidad de entrada y salida de Azure con origen de datos SQL Server</span><span class="sxs-lookup"><span data-stu-id="44e53-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="44e53-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="44e53-259">1.2.5303.1</span></span>

*  <span data-ttu-id="44e53-260">Corregir toosupport de problema de tiempo de espera más conexiones que consumen muchos recursos de orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="44e53-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="44e53-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="44e53-261">1.1.5526.8</span></span>

*  <span data-ttu-id="44e53-262">Requiere .NET Framework 4.5.1 como requisito previo durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="44e53-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="44e53-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="44e53-263">1.0.5144.2</span></span>

*  <span data-ttu-id="44e53-264">No hay cambios que afecten a los escenarios de Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="44e53-264">No changes that affect Azure Data Factory scenarios.</span></span>
