---
title: "Notas de la versión de Data Management Gateway | Microsoft Docs"
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
ms.openlocfilehash: c052d7e9f757164429ce867201b96305e405dce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="552fb-103">Notas de la versión de Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="552fb-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="552fb-104">Uno de los desafíos de la integración de datos moderna es la migración de datos entre la ubicación local y la nube.</span><span class="sxs-lookup"><span data-stu-id="552fb-104">One of the challenges for modern data integration is to move data to and from on-premises to cloud.</span></span> <span data-ttu-id="552fb-105">Data Factory realiza la integración con Data Management Gateway, un agente que se puede instalar de forma local para permitir la migración de datos híbridos.</span><span class="sxs-lookup"><span data-stu-id="552fb-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span></span>

<span data-ttu-id="552fb-106">En los siguientes artículos se proporciona información detallada sobre Data Management Gateway y cómo utilizarlo:</span><span class="sxs-lookup"><span data-stu-id="552fb-106">See the following articles for detailed information about Data Management Gateway and how to use it:</span></span>

*  [<span data-ttu-id="552fb-107">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="552fb-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="552fb-108">Movimiento de datos entre una ubicación local y la nube mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="552fb-109">VERSIÓN ACTUAL (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="552fb-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="552fb-110">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="552fb-110">Enhancements-</span></span>
- <span data-ttu-id="552fb-111">Puede agregar entradas DNS a la lista de Service Bus permitidos en vez de incluir todas las direcciones IP de Azure en la lista de permitidas del firewall (en caso necesario).</span><span class="sxs-lookup"><span data-stu-id="552fb-111">You can add DNS entries to whitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="552fb-112">Puede encontrar la entrada DNS correspondiente en Azure Portal (Data Factory -> "Crear e implementar" -> "Puertas de enlace" -> "serviceUrls" (en JSON)</span><span class="sxs-lookup"><span data-stu-id="552fb-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="552fb-113">El conector HDFS admite ahora certificados públicos autofirmados para poder omitir la validación de SSL.</span><span class="sxs-lookup"><span data-stu-id="552fb-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="552fb-114">Solucionado: problema con la puerta de enlace sin conexión durante la actualización (debido a la distorsión del reloj)</span><span class="sxs-lookup"><span data-stu-id="552fb-114">Fixed: Issue with gateway offline during update (due to clock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="552fb-115">Versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="552fb-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="552fb-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="552fb-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="552fb-117">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="552fb-117">Enhancements-</span></span>
-   <span data-ttu-id="552fb-118">Puede agregar entradas DNS a la lista blanca de Service Bus en vez de incluir todas las direcciones IP de Azure en la lista blanca del firewall (en caso necesario).</span><span class="sxs-lookup"><span data-stu-id="552fb-118">You can add DNS entries to whitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="552fb-119">Más detalles aquí.</span><span class="sxs-lookup"><span data-stu-id="552fb-119">More details here.</span></span>
-   <span data-ttu-id="552fb-120">Ahora puede copiar hasta 4,75 TB de datos (tamaño máximo admitido para blob en bloques) en un único blob en bloques, y viceversa</span><span class="sxs-lookup"><span data-stu-id="552fb-120">You can now copy data to/from a single block blob up to 4.75 TB, which is the max supported size of block blob.</span></span> <span data-ttu-id="552fb-121">(el límite anterior era 195 GB).</span><span class="sxs-lookup"><span data-stu-id="552fb-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="552fb-122">Problema solucionado: memoria agotada al descomprimir varios archivos pequeños durante la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="552fb-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="552fb-123">Problema solucionado: índice fuera de rango al copiar de Document DB a una instancia de SQL Server local con la característica de idempotencia.</span><span class="sxs-lookup"><span data-stu-id="552fb-123">Fixed: Index out of range issue while copying from Document DB to an on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="552fb-124">Problema solucionado: el script de limpieza SQL no funciona en la instancia de SQL Server local desde el Asistente para copia.</span><span class="sxs-lookup"><span data-stu-id="552fb-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="552fb-125">Problema solucionado: nombre de columna con espacio al final no funciona en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="552fb-125">Fixed: Column name with space at the end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="552fb-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="552fb-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="552fb-127">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="552fb-127">Enhancements-</span></span>
- <span data-ttu-id="552fb-128">Problema solucionado: falta de credenciales durante el reinicio de máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="552fb-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="552fb-129">Solucionado: problema de registro durante la restauración de la puerta de enlace mediante un archivo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="552fb-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="552fb-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="552fb-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="552fb-131">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="552fb-131">Enhancements-</span></span>
- <span data-ttu-id="552fb-132">Problema solucionado: lectura incorrecta de valor NULL decimal desde Oracle como origen.</span><span class="sxs-lookup"><span data-stu-id="552fb-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="552fb-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="552fb-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="552fb-134">Novedades</span><span class="sxs-lookup"><span data-stu-id="552fb-134">What’s new</span></span>
- <span data-ttu-id="552fb-135">Los clientes pueden proporcionar comentarios en la experiencia de registro de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="552fb-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="552fb-136">Nuevo formato de compresión compatible: ZIP (Deflate).</span><span class="sxs-lookup"><span data-stu-id="552fb-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="552fb-137">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="552fb-137">Enhancements-</span></span>
- <span data-ttu-id="552fb-138">Mejora del rendimiento del origen de HDFS y el receptor de Oracle.</span><span class="sxs-lookup"><span data-stu-id="552fb-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="552fb-139">Corrección de errores de la capacidad de procesamiento en paralelo y la actualización automática de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="552fb-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="552fb-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="552fb-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="552fb-141">Mejoras</span><span class="sxs-lookup"><span data-stu-id="552fb-141">Enhancements</span></span>
- <span data-ttu-id="552fb-142">Experiencia de registro de la puerta de enlace mejorada y más sólida: ahora puede realizar el seguimiento del estado del progreso durante el proceso de registro de la puerta de enlace, con lo que la experiencia de registro tiene una mayor capacidad de respuesta.</span><span class="sxs-lookup"><span data-stu-id="552fb-142">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span></span>
- <span data-ttu-id="552fb-143">Mejora del proceso de restauración de la puerta de enlace: puede recuperar la puerta de enlace incluso si no tiene el archivo de copia de seguridad de la puerta de enlace con esta actualización.</span><span class="sxs-lookup"><span data-stu-id="552fb-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span></span> <span data-ttu-id="552fb-144">Esto requeriría restablecer credenciales de servicio vinculado en el Portal.</span><span class="sxs-lookup"><span data-stu-id="552fb-144">This would require you to reset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="552fb-145">Corrección de errores.</span><span class="sxs-lookup"><span data-stu-id="552fb-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="552fb-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="552fb-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="552fb-147">Novedades</span><span class="sxs-lookup"><span data-stu-id="552fb-147">What’s new</span></span>

- <span data-ttu-id="552fb-148">Ahora puede almacenar localmente las credenciales de origen de datos.</span><span class="sxs-lookup"><span data-stu-id="552fb-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="552fb-149">Las credenciales se cifran.</span><span class="sxs-lookup"><span data-stu-id="552fb-149">The credentials are encrypted.</span></span> <span data-ttu-id="552fb-150">Las credenciales del origen de datos se pueden recuperar y restaurar usando el archivo de copia de seguridad que se puede exportar desde la puerta de enlace existente, todo de manera local.</span><span class="sxs-lookup"><span data-stu-id="552fb-150">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="552fb-151">Mejoras-</span><span class="sxs-lookup"><span data-stu-id="552fb-151">Enhancements-</span></span>

- <span data-ttu-id="552fb-152">Experiencia de registro de puerta de enlace mejorada y más eficaz.</span><span class="sxs-lookup"><span data-stu-id="552fb-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="552fb-153">Compatibilidad con detección automática de la configuración de QuoteChar para formato de texto en el Asistente para copia y mejorar la precisión de la detección de formato general.</span><span class="sxs-lookup"><span data-stu-id="552fb-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="552fb-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="552fb-154">2.3.6100.2</span></span>

- <span data-ttu-id="552fb-155">Compatibilidad con la detección automática de firstRowAsHeader y SkipLineCount en el Asistente para copia para archivos de texto en el sistema de archivos local y HDFS.</span><span class="sxs-lookup"><span data-stu-id="552fb-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="552fb-156">Mejora de la estabilidad de la conexión de red entre la puerta de enlace y Service Bus</span><span class="sxs-lookup"><span data-stu-id="552fb-156">Enhance the stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="552fb-157">Unas pocas correcciones de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="552fb-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="552fb-158">2.2.6072.1</span></span>

*  <span data-ttu-id="552fb-159">Admite la configuración de proxy HTTP para la puerta de enlace con el Administrador de configuración de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="552fb-159">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span></span> <span data-ttu-id="552fb-160">Si está configurado, se accede a Blob de Azure, Tabla de Azure, Azure Data Lake y DocumentDB a través del proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="552fb-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="552fb-161">Admite el control de encabezados para TextFormat al copiar datos en Blob de Azure, Azure Data Lake Store, el sistema de archivos local y el HDFS local como origen y destino.</span><span class="sxs-lookup"><span data-stu-id="552fb-161">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="552fb-162">Admite la copia de datos desde blobs en anexos y blobs en páginas junto con los blobs en bloques que ya eran compatibles.</span><span class="sxs-lookup"><span data-stu-id="552fb-162">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span></span>
*  <span data-ttu-id="552fb-163">Introduce un nuevo estado de puerta de enlace **Online (Limited)**(En línea [limitado]), lo que indica que se puede utilizar sin problemas la funcionalidad principal de la puerta de enlace, pero la operación interactiva del Asistente para copia.</span><span class="sxs-lookup"><span data-stu-id="552fb-163">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="552fb-164">Mejora la estabilidad del registro de puerta de enlace mediante la clave de registro.</span><span class="sxs-lookup"><span data-stu-id="552fb-164">Enhances the robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="552fb-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="552fb-165">2.1.6040.</span></span>

*  <span data-ttu-id="552fb-166">El controlador DB2 se incluye ahora en el paquete de instalación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="552fb-166">DB2 driver is included in the gateway installation package now.</span></span> <span data-ttu-id="552fb-167">No es necesario instalarlo por separado.</span><span class="sxs-lookup"><span data-stu-id="552fb-167">You do not need to install it separately.</span></span>
*  <span data-ttu-id="552fb-168">El controlador DB2 ahora admite z/OS y DB2 para i (AS / 400) junto con las plataformas ya admitidas (Linux, Unix y Windows).</span><span class="sxs-lookup"><span data-stu-id="552fb-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="552fb-169">Admite el uso de Azure Cosmos DB como origen o destino para almacenes de datos locales</span><span class="sxs-lookup"><span data-stu-id="552fb-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="552fb-170">Admite la copia de datos desde/a blobs de almacenamiento en frío y en caliente junto con la cuenta de almacenamiento general ya admitida.</span><span class="sxs-lookup"><span data-stu-id="552fb-170">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="552fb-171">Le permite conectarse a la instancia local de SQL Server a través de la puerta de enlace con privilegios de inicio de sesión remoto.</span><span class="sxs-lookup"><span data-stu-id="552fb-171">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="552fb-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="552fb-172">2.0.6013.1</span></span>

*  <span data-ttu-id="552fb-173">Puede seleccionar el idioma o la referencia cultural que utilizará una puerta de enlace durante la instalación manual.</span><span class="sxs-lookup"><span data-stu-id="552fb-173">You can select the language/culture to be used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="552fb-174">Cuando la puerta de enlace no funciona del modo previsto, puede optar por enviar los registros de la puerta de enlace de los últimos 7 días a Microsoft para que pueda solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="552fb-174">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span></span> <span data-ttu-id="552fb-175">Si la puerta de enlace no está conectada al servicio en la nube, puede guardar y archivar los registros de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="552fb-175">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span></span>  

*  <span data-ttu-id="552fb-176">Mejoras de la interfaz de usuario del Administrador de configuración de puertas de enlace:</span><span class="sxs-lookup"><span data-stu-id="552fb-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="552fb-177">Mayor visibilidad del estado de la puerta de enlace en la pestaña Inicio.</span><span class="sxs-lookup"><span data-stu-id="552fb-177">Make gateway status more visible on the Home tab.</span></span>

    *  <span data-ttu-id="552fb-178">Controles reorganizados y simplificados.</span><span class="sxs-lookup"><span data-stu-id="552fb-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="552fb-179">Puede copiar datos desde un almacenamiento mediante la [herramienta de vista previa de código abierto](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="552fb-179">You can copy data from a storage using the [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="552fb-180">Para obtener más información general sobre esta característica consulte [Copias almacenadas provisionalmente](data-factory-copy-activity-performance.md#staged-copy) .</span><span class="sxs-lookup"><span data-stu-id="552fb-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="552fb-181">Puede utilizar Data Management Gateway para transferir los datos directamente de la base de datos de SQL Server local a Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="552fb-181">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="552fb-182">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-182">Performance improvements</span></span>

    * <span data-ttu-id="552fb-183">Se ha mejorado el rendimiento al visualizar los esquemas y la vista previa en SQL Server mediante la herramienta de vista previa de copia sin código.</span><span class="sxs-lookup"><span data-stu-id="552fb-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="552fb-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="552fb-184">1.12.5953.1</span></span>

*  <span data-ttu-id="552fb-185">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="552fb-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="552fb-186">1.11.5918.1</span></span>

*  <span data-ttu-id="552fb-187">El tamaño máximo del registro de eventos de puerta de enlace ha aumentado de 1 MB a 40 MB.</span><span class="sxs-lookup"><span data-stu-id="552fb-187">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span></span>

*  <span data-ttu-id="552fb-188">En caso de que se requiera un reinicio durante la actualización automática de la puerta de enlace, se muestra un cuadro de diálogo de advertencia.</span><span class="sxs-lookup"><span data-stu-id="552fb-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="552fb-189">Puede elegir reiniciar en ese mismo momento o más adelante.</span><span class="sxs-lookup"><span data-stu-id="552fb-189">You can choose to restart right then or later.</span></span>

*  <span data-ttu-id="552fb-190">En caso de error en la actualización automática, el instalador de puerta de enlace volverá a intentar esta operación 3 veces al máximo.</span><span class="sxs-lookup"><span data-stu-id="552fb-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="552fb-191">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-191">Performance improvements</span></span>

    * <span data-ttu-id="552fb-192">Rendimiento mejorado para la carga de tablas de gran tamaño desde el servidor local en un escenario de copia sin código.</span><span class="sxs-lookup"><span data-stu-id="552fb-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="552fb-193">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="552fb-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="552fb-194">1.10.5892.1</span></span>

*  <span data-ttu-id="552fb-195">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-195">Performance improvements</span></span>

*  <span data-ttu-id="552fb-196">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="552fb-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="552fb-197">1.9.5865.2</span></span>

*  <span data-ttu-id="552fb-198">Funcionalidad de actualización automática sin intervención del usuario</span><span class="sxs-lookup"><span data-stu-id="552fb-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="552fb-199">Icono de bandeja de nuevo con indicadores de estado de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="552fb-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="552fb-200">Capacidad para "Actualizar ahora" desde el cliente</span><span class="sxs-lookup"><span data-stu-id="552fb-200">Ability to “Update now” from the client</span></span>
*  <span data-ttu-id="552fb-201">Capacidad para establecer la hora de programación de las actualizaciones</span><span class="sxs-lookup"><span data-stu-id="552fb-201">Ability to set update schedule time</span></span>
*  <span data-ttu-id="552fb-202">Script de PowerShell para activar y desactivar la actualización automática</span><span class="sxs-lookup"><span data-stu-id="552fb-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="552fb-203">Compatibilidad con formato JSON</span><span class="sxs-lookup"><span data-stu-id="552fb-203">Support for JSON format</span></span>  
*  <span data-ttu-id="552fb-204">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-204">Performance improvements</span></span>
*  <span data-ttu-id="552fb-205">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="552fb-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="552fb-206">1.8.5822.1</span></span>

*  <span data-ttu-id="552fb-207">Mejora de la solución de problemas</span><span class="sxs-lookup"><span data-stu-id="552fb-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="552fb-208">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-208">Performance improvements</span></span>
*  <span data-ttu-id="552fb-209">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="552fb-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="552fb-210">1.7.5795.1</span></span>

*  <span data-ttu-id="552fb-211">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-211">Performance improvements</span></span>
*  <span data-ttu-id="552fb-212">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="552fb-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="552fb-213">1.7.5764.1</span></span>

*  <span data-ttu-id="552fb-214">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-214">Performance improvements</span></span>
*  <span data-ttu-id="552fb-215">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="552fb-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="552fb-216">1.6.5735.1</span></span>

*  <span data-ttu-id="552fb-217">Compatibilidad origen y receptor HDFS locales</span><span class="sxs-lookup"><span data-stu-id="552fb-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="552fb-218">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-218">Performance improvements</span></span>
*  <span data-ttu-id="552fb-219">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="552fb-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="552fb-220">1.6.5696.1</span></span>

*  <span data-ttu-id="552fb-221">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-221">Performance improvements</span></span>
*  <span data-ttu-id="552fb-222">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="552fb-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="552fb-223">1.6.5676.1</span></span>

*  <span data-ttu-id="552fb-224">Compatibilidad con herramientas de diagnóstico de Administrador de configuración</span><span class="sxs-lookup"><span data-stu-id="552fb-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="552fb-225">Columnas de la tabla de soporte técnico para orígenes de datos tabulares de la Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-226">Compatibilidad con SQL DW para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-227">Compatibilidad con Reclusive en BlobSource y FileSource para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-228">Compatibilidad con CopyBehavior - MergeFiles, PreserveHierarchy y FlattenHierarchy en BlobSink y FileSink con copia binaria para Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-229">Compatibilidad con los informes de progreso de la actividad de copia para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-230">Compatibilidad con la validación de conectividad de origen de datos para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-231">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="552fb-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="552fb-232">1.6.5672.1</span></span>

*  <span data-ttu-id="552fb-233">Compatibilidad con nombre de tabla de origen de datos ODBC para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-234">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-234">Performance improvements</span></span>
*  <span data-ttu-id="552fb-235">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="552fb-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="552fb-236">1.6.5658.1</span></span>

*  <span data-ttu-id="552fb-237">Compatibilidad con receptor de archivos para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-238">Compatibilidad con la conservación jerarquía en copia binaria para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-239">Compatibilidad con idempotencia de la actividad de copia para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-240">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="552fb-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="552fb-241">1.6.5640.1</span></span>

*  <span data-ttu-id="552fb-242">Compatibilidad con tres orígenes de datos más para Factoría de datos de Azure (ODBC, OData y HDFS)</span><span class="sxs-lookup"><span data-stu-id="552fb-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="552fb-243">Compatibilidad con carácter de comillas en el analizador de archivos .csv para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-244">Compatibilidad con compresión (BZip2)</span><span class="sxs-lookup"><span data-stu-id="552fb-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="552fb-245">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="552fb-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="552fb-246">1.5.5612.1</span></span>

*  <span data-ttu-id="552fb-247">Compatibilidad con cinco bases de datos relacionales para Data Factory de Azure (MySQL, PostgreSQL, DB2, Teradata y Sybase)</span><span class="sxs-lookup"><span data-stu-id="552fb-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="552fb-248">Compatibilidad de compresión (Gzip y Deflate)</span><span class="sxs-lookup"><span data-stu-id="552fb-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="552fb-249">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-249">Performance improvements</span></span>
*  <span data-ttu-id="552fb-250">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="552fb-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="552fb-251">1.4.5549.1</span></span>

*  <span data-ttu-id="552fb-252">Incorporación de compatibilidad de origen de datos Oracle para Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="552fb-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="552fb-253">Mejoras en el rendimiento</span><span class="sxs-lookup"><span data-stu-id="552fb-253">Performance improvements</span></span>
*  <span data-ttu-id="552fb-254">Corrección de errores</span><span class="sxs-lookup"><span data-stu-id="552fb-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="552fb-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="552fb-255">1.4.5492.1</span></span>

*  <span data-ttu-id="552fb-256">Binario unificado que admite los servicios Factoría de datos de Microsoft Azure y Office 365 Power BI</span><span class="sxs-lookup"><span data-stu-id="552fb-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="552fb-257">Restricción de la interfaz de usuario de configuración y del proceso de registro</span><span class="sxs-lookup"><span data-stu-id="552fb-257">Refine the Configuration UI and registration process</span></span>
*  <span data-ttu-id="552fb-258">Factoría de datos de Azure: compatibilidad de entrada y salida de Azure con origen de datos SQL Server</span><span class="sxs-lookup"><span data-stu-id="552fb-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="552fb-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="552fb-259">1.2.5303.1</span></span>

*  <span data-ttu-id="552fb-260">Corrección del problema del tiempo de espera para admitir más conexiones de orígenes de datos que requieren mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="552fb-260">Fix timeout issue to support more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="552fb-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="552fb-261">1.1.5526.8</span></span>

*  <span data-ttu-id="552fb-262">Requiere .NET Framework 4.5.1 como requisito previo durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="552fb-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="552fb-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="552fb-263">1.0.5144.2</span></span>

*  <span data-ttu-id="552fb-264">No hay cambios que afecten a los escenarios de Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="552fb-264">No changes that affect Azure Data Factory scenarios.</span></span>
