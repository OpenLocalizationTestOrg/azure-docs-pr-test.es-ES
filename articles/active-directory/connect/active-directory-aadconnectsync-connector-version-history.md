---
title: Historial de versiones aaaConnector | Documentos de Microsoft
description: En este tema se enumera todas las versiones de conectores de Hola para Forefront Identity Manager (FIM) y Microsoft Identity Manager (MIM)
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="746b0-103">Historial de versiones de conectores</span><span class="sxs-lookup"><span data-stu-id="746b0-103">Connector Version Release History</span></span>
<span data-ttu-id="746b0-104">Conectores de Hola para Forefront Identity Manager (FIM) y Microsoft Identity Manager (MIM) se actualizan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="746b0-104">hello Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="746b0-105">Este tema solo está disponible en FIM y MIM.</span><span class="sxs-lookup"><span data-stu-id="746b0-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="746b0-106">No se admite la instalación de estos conectores en Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="746b0-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="746b0-107">Conectores de lanzamiento se preinstalado en AADConnect al actualizar toospecified compilación.</span><span class="sxs-lookup"><span data-stu-id="746b0-107">Released Connectors are preinstalled on AADConnect when upgrading toospecified Build.</span></span>

<span data-ttu-id="746b0-108">En este tema se enumeran todas las versiones de hello conectores que se han liberado.</span><span class="sxs-lookup"><span data-stu-id="746b0-108">This topic list all versions of hello Connectors that have been released.</span></span>

<span data-ttu-id="746b0-109">Vínculos relacionados:</span><span class="sxs-lookup"><span data-stu-id="746b0-109">Related links:</span></span>

* [<span data-ttu-id="746b0-110">Descargar los últimos conectores</span><span class="sxs-lookup"><span data-stu-id="746b0-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="746b0-111">[conector LDAP genérico](active-directory-aadconnectsync-connector-genericldap.md)</span><span class="sxs-lookup"><span data-stu-id="746b0-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="746b0-112">[conector SQL genérico](active-directory-aadconnectsync-connector-genericsql.md)</span><span class="sxs-lookup"><span data-stu-id="746b0-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="746b0-113">[conector de servicios web](http://go.microsoft.com/fwlink/?LinkID=226245)</span><span class="sxs-lookup"><span data-stu-id="746b0-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="746b0-114">[conector PowerShell](active-directory-aadconnectsync-connector-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="746b0-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="746b0-115">[conector Lotus Domino](active-directory-aadconnectsync-connector-domino.md)</span><span class="sxs-lookup"><span data-stu-id="746b0-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="746b0-116">1.1.604.0 (AADConnect pendiente de publicación)</span><span class="sxs-lookup"><span data-stu-id="746b0-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="746b0-117">Problemas corregidos:</span><span class="sxs-lookup"><span data-stu-id="746b0-117">Fixed issues:</span></span>

* <span data-ttu-id="746b0-118">Servicios Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="746b0-118">Generic Web Services:</span></span>
  * <span data-ttu-id="746b0-119">Se corrigió un problema que impedía la creación de un proyecto SOAP cuando había dos o más puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="746b0-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="746b0-120">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-120">Generic SQL:</span></span>
  * <span data-ttu-id="746b0-121">En la operación de Hola de importación hello GSQL no se convertir la hora correctamente, cuando guarda tooconnector espacio.</span><span class="sxs-lookup"><span data-stu-id="746b0-121">In hello operation of import hello GSQL was not converting time correctly, when saved tooconnector space.</span></span> <span data-ttu-id="746b0-122">Hello formato de fecha y hora predeterminado para el espacio de conector de hello GSQL cambió de 'aaaa-MM-dd ssZ' too'yyyy-MM-dd ssZ '.</span><span class="sxs-lookup"><span data-stu-id="746b0-122">hello default date and time format for connector space of hello GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' too'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="746b0-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="746b0-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="746b0-124">Problemas corregidos:</span><span class="sxs-lookup"><span data-stu-id="746b0-124">Fixed issues:</span></span>

* <span data-ttu-id="746b0-125">Servicios Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="746b0-125">Generic Web Services:</span></span>
  * <span data-ttu-id="746b0-126">herramienta de Hello Wsconfig no convirtió correctamente matriz Json de Hola de "solicitud de ejemplo" para el método de servicio REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="746b0-126">hello Wsconfig tool did not convert correctly hello Json array from "sample request" for hello REST service method.</span></span> <span data-ttu-id="746b0-127">Esto causaba problemas con la serialización de esta matriz Json de solicitud REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="746b0-127">This caused problems with serialization this Json array for hello REST request.</span></span>
  * <span data-ttu-id="746b0-128">La herramienta de configuración del conector de servicio web no admite el uso de espacios en nombres de atributo JSON</span><span class="sxs-lookup"><span data-stu-id="746b0-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="746b0-129">Un patrón de sustitución se puede agregar manualmente archivos de WSConfigTool.exe.config de toohello, p. ej.```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="746b0-129">A Substitution pattern can be added manually toohello WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="746b0-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="746b0-130">Lotus Notes:</span></span>
  * <span data-ttu-id="746b0-131">Hola cuando la opción **permitir los certificadores personalizados para las unidades de organización/organización** está deshabilitado Hola conector se produce un error durante la exportación (actualización) después de exportación de hello fluir todos los atributos son tooDomino exportado, pero en tiempo de presentación de exportar un KeyNotFoundException se devuelve tooSync.</span><span class="sxs-lookup"><span data-stu-id="746b0-131">When hello option **Allow custom certifiers for Organization/Organizational Units** is disabled then hello connector fails during export (Update) After hello export flow all attributes are exported tooDomino but at hello time of export a KeyNotFoundException is returned tooSync.</span></span> 
    * <span data-ttu-id="746b0-132">Esto sucede porque Hola cambiar el nombre de operación se produce un error cuando intente toochange DN (atributo de nombre de usuario) cambiando uno de los atributos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="746b0-132">This happens because hello rename operation fails when it tries toochange DN (UserName attribute) by changing one of hello attributes below:</span></span>  
      - <span data-ttu-id="746b0-133">Apellidos</span><span class="sxs-lookup"><span data-stu-id="746b0-133">LastName</span></span>
      - <span data-ttu-id="746b0-134">Nombre</span><span class="sxs-lookup"><span data-stu-id="746b0-134">FirstName</span></span>
      - <span data-ttu-id="746b0-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="746b0-135">MiddleInitial</span></span>
      - <span data-ttu-id="746b0-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="746b0-136">AltFullName</span></span>
      - <span data-ttu-id="746b0-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="746b0-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="746b0-138">ou</span><span class="sxs-lookup"><span data-stu-id="746b0-138">ou</span></span>
      - <span data-ttu-id="746b0-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="746b0-139">altcommonname</span></span>

  * <span data-ttu-id="746b0-140">Cuando la opción **Allow custom certifiers for Organization/Organizational Units** (Permitir certificadores personalizados para la organización/unidades organizativas) está habilitada pero los certificadores necesarios siguen vacíos, se produce una excepción KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="746b0-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="746b0-141">Mejoras:</span><span class="sxs-lookup"><span data-stu-id="746b0-141">Enhancements:</span></span>

* <span data-ttu-id="746b0-142">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-142">Generic SQL:</span></span>
  * <span data-ttu-id="746b0-143">**Escenario: rediseñado implementado:** característica "*"</span><span class="sxs-lookup"><span data-stu-id="746b0-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="746b0-144">**Descripción de la solución:** se cambió el enfoque para el [control de los atributos de referencia multivalor](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="746b0-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="746b0-145">Problemas corregidos:</span><span class="sxs-lookup"><span data-stu-id="746b0-145">Fixed issues:</span></span>

* <span data-ttu-id="746b0-146">Servicios Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="746b0-146">Generic Web Services:</span></span>
  * <span data-ttu-id="746b0-147">No se puede importar la configuración del servidor si está presente el conector de WebService</span><span class="sxs-lookup"><span data-stu-id="746b0-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="746b0-148">El conector de WebService no funciona con varios servicios web</span><span class="sxs-lookup"><span data-stu-id="746b0-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="746b0-149">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-149">Generic SQL:</span></span>
  * <span data-ttu-id="746b0-150">No hay tipos de objeto para atributos de referencia de un único valor</span><span class="sxs-lookup"><span data-stu-id="746b0-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="746b0-151">La importación diferencial en la estrategia de Change Tracking elimina el objeto cuando se quita el valor de la tabla multivalor</span><span class="sxs-lookup"><span data-stu-id="746b0-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="746b0-152">OverflowException en conector GSQL con DB2 en AS/400</span><span class="sxs-lookup"><span data-stu-id="746b0-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="746b0-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="746b0-153">Lotus:</span></span>
  * <span data-ttu-id="746b0-154">Tooenable\disable ha agregado la opción Buscar las unidades organizativas antes de abrir la página de GlobalParameters</span><span class="sxs-lookup"><span data-stu-id="746b0-154">Added option tooenable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="746b0-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="746b0-155">1.1.443.0</span></span>

<span data-ttu-id="746b0-156">Publicación: marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="746b0-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="746b0-157">Mejoras</span><span class="sxs-lookup"><span data-stu-id="746b0-157">Enhancements</span></span>

* <span data-ttu-id="746b0-158">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-158">Generic SQL:</span></span></br><span data-ttu-id="746b0-159">
  **Síntomas de escenario:** es una limitación conocida con hello conector de SQL donde sólo permiten un tipo de objeto de referencia tooone y requieren una referencia cruzada con los miembros.</span><span class="sxs-lookup"><span data-stu-id="746b0-159">
  **Scenario Symptoms:**  It is a well-known limitation with hello SQL Connector where we only allow a reference tooone object type and require cross reference with members.</span></span> </br><span data-ttu-id="746b0-160">
**Descripción de la solución:** en el paso de procesamiento de Hola para las referencias eran "*" se elige la opción, se devolverán todas las combinaciones de tipos de objeto toohello atrás motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="746b0-160">
**Solution description:** In hello processing step for references were "*" option is chosen, ALL combinations of object types will be returned back toohello sync engine.</span></span>

>[!Important]
- <span data-ttu-id="746b0-161">Con esto se crearán muchos marcadores de posición</span><span class="sxs-lookup"><span data-stu-id="746b0-161">This will create many placeholders</span></span>
- <span data-ttu-id="746b0-162">Es necesario toomake seguro Hola de nomenclatura es único entre los tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="746b0-162">It is required toomake sure hello naming is unique cross object types.</span></span>


* <span data-ttu-id="746b0-163">LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-163">Generic LDAP:</span></span></br><span data-ttu-id="746b0-164">
 **Escenario:** cuando se seleccionan sólo algunos contenedores de partición específica, a continuación, búsqueda de hello todavía se realizará en toda partición.</span><span class="sxs-lookup"><span data-stu-id="746b0-164">
**Scenario:** When only few containers are selected in specific partition, then hello search still will be done in whole partition.</span></span> <span data-ttu-id="746b0-165">El servicio de sincronización filtrará la partición específica, pero MA no lo hará, lo que podría provocar una degradación del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="746b0-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="746b0-166">**Descripción de la solución:** toomake de código del conector GLDAP cambiado se pueden pasar por todos los contenedores y buscar objetos en cada uno de ellos, en lugar de buscar en toda partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="746b0-166">**Solution description:** Changed GLDAP connector's code toomake it possible go through all containers and search objects in each of them, instead of searching in hello whole partition.</span></span>


* <span data-ttu-id="746b0-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="746b0-167">Lotus Domino:</span></span>

  <span data-ttu-id="746b0-168">**Escenario:** compatibilidad de la eliminación de correo de Domino para la eliminación de una persona durante una exportación.</span><span class="sxs-lookup"><span data-stu-id="746b0-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="746b0-169">
  **Solución:** configuración de eliminación de correo configurable para la eliminación de una persona durante una exportación.</span><span class="sxs-lookup"><span data-stu-id="746b0-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="746b0-170">Problemas corregidos:</span><span class="sxs-lookup"><span data-stu-id="746b0-170">Fixed issues:</span></span>
* <span data-ttu-id="746b0-171">Servicios Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="746b0-171">Generic Web Services:</span></span>
 * <span data-ttu-id="746b0-172">Al cambiar la dirección URL del servicio de Hola de forma predeterminada en los proyectos wsconfig SAP a través de la herramienta de configuración de servicio Web, a continuación, Hola tras error ocurre: no se encontró una parte de la ruta de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="746b0-172">When changing hello service URL in Default SAP wsconfig projects through WebService Configuration Tool then hello following error happens: Could not find a part of hello path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="746b0-173">LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-173">Generic LDAP:</span></span>
 * <span data-ttu-id="746b0-174">Conector GLDAP no ve todos los atributos en AD LDS</span><span class="sxs-lookup"><span data-stu-id="746b0-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="746b0-175">Asistente para saltos cuando ningún atributo UPN se ha detectado en el esquema de directorio LDAP de Hola</span><span class="sxs-lookup"><span data-stu-id="746b0-175">Wizard breaks when no UPN attributes are detected from hello LDAP directory schema</span></span>
 * <span data-ttu-id="746b0-176">Error de importaciones diferenciales cuando no hay errores de detección durante la importación completa, cuando no se selecciona el atributo "objectclass"</span><span class="sxs-lookup"><span data-stu-id="746b0-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="746b0-177">Una página de configuración "Configurar particiones y jerarquías", no muestra ningún objeto de qué tipo es la partición de toohello igual para los servidores Novel Hola genérico</span><span class="sxs-lookup"><span data-stu-id="746b0-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal toohello partition for Novel servers in hello Generic</span></span>  
<span data-ttu-id="746b0-178">genérico.</span><span class="sxs-lookup"><span data-stu-id="746b0-178">LDAP MA.</span></span> <span data-ttu-id="746b0-179">Solo se muestran objetos desde la partición RootDSE.</span><span class="sxs-lookup"><span data-stu-id="746b0-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="746b0-180">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-180">Generic SQL:</span></span>
 * <span data-ttu-id="746b0-181">Corrección para el error en que el atributo multivalor de importación diferencial de límite de SQL genérico no se puede importar</span><span class="sxs-lookup"><span data-stu-id="746b0-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="746b0-182">Cuando se exportan valores eliminados o agregados del atributo multivalor, no se eliminan ni agregan en el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="746b0-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="746b0-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="746b0-183">Lotus Notes:</span></span>
 * <span data-ttu-id="746b0-184">Un campo específico "Nombre completo" se muestra en el metaverso Hola correctamente sin embargo cuando tooNotes exportar Hola valor de atributo de hello es nulo o está vacío.</span><span class="sxs-lookup"><span data-stu-id="746b0-184">A specific field "Full Name" is shown in hello metaverse correctly however when exporting tooNotes hello value for hello attribute is Null or Empty.</span></span>
 * <span data-ttu-id="746b0-185">Corrección para error de certificador duplicado</span><span class="sxs-lookup"><span data-stu-id="746b0-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="746b0-186">Cuando se selecciona Hola objeto sin ningún dato en hello conector para Lotus Domino con otros objetos que recibimos error de detección de hello al realizar la importación completa.</span><span class="sxs-lookup"><span data-stu-id="746b0-186">When hello Object without any data is selected on hello Lotus Domino Connector with other objects then we receive hello Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="746b0-187">Una vez importación diferencial que se ejecuta en hello conector para Lotus Domino, final Hola de esa ejecución, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe servicio a veces devuelve un Error de aplicación.</span><span class="sxs-lookup"><span data-stu-id="746b0-187">When Delta Import is being running on hello Lotus Domino Connector, at hello end of that run, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="746b0-188">La pertenencia al grupo global funciona correctamente y se mantiene, excepto cuando se ejecuta Hola exportación tootry tooremove un usuario de pertenencia se muestra como correcto con una actualización, pero usuario Hola realmente no se quitan de la pertenencia a Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="746b0-188">Group membership overall works fine and is maintained, except when running hello export tootry tooremove a user from membership it shows as successful with an update, but hello user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="746b0-189">Un modo de toochoose oportunidad de exportación como "Anexado el elemento final" se agregó en configuración del agente de administración de GUI de Lotus tooappend nuevos elementos en parte inferior durante la exportación de Hola para los atributos con varios valores.</span><span class="sxs-lookup"><span data-stu-id="746b0-189">An opportunity toochoose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA tooappend new items at bottom during hello export for multi-valued attributes.</span></span>
 * <span data-ttu-id="746b0-190">Conector agregará Hola necesita Id. de almacén y del archivo de Hola de toodelete de lógica de hello carpeta de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="746b0-190">Connector will add hello needed logic toodelete hello file from hello Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="746b0-191">La eliminación de pertenencias no funciona entre los miembros de NAB.</span><span class="sxs-lookup"><span data-stu-id="746b0-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="746b0-192">Los valores se deben eliminar correctamente del atributo multivalor</span><span class="sxs-lookup"><span data-stu-id="746b0-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="746b0-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="746b0-193">1.1.117.0</span></span>
<span data-ttu-id="746b0-194">Publicación: marzo de 2016</span><span class="sxs-lookup"><span data-stu-id="746b0-194">Released: 2016 March</span></span>

<span data-ttu-id="746b0-195">**Nuevo conector**</span><span class="sxs-lookup"><span data-stu-id="746b0-195">**New Connector**</span></span>  
<span data-ttu-id="746b0-196">Versión de hello inicial [conector de SQL genérico](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="746b0-196">Initial release of hello [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="746b0-197">**Nuevas características:**</span><span class="sxs-lookup"><span data-stu-id="746b0-197">**New features:**</span></span>

* <span data-ttu-id="746b0-198">Conector LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="746b0-199">Se agregó compatibilidad para la importación diferencial con Isode.</span><span class="sxs-lookup"><span data-stu-id="746b0-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="746b0-200">Conector de servicios web:</span><span class="sxs-lookup"><span data-stu-id="746b0-200">Web Services Connector:</span></span>
  * <span data-ttu-id="746b0-201">Hola actualizada csEntryChangeResult actividad y setImportErrorCode actividad tooallow objeto errores en el nivel toobe toohello atrás devuelto motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="746b0-201">Updated hello csEntryChangeResult activity and setImportErrorCode activity tooallow object level errors toobe returned back toohello sync engine.</span></span>
  * <span data-ttu-id="746b0-202">Hola actualizada SAP6 y SAP6User plantillas toouse Hola nuevo error nivel funcionalidad del objeto.</span><span class="sxs-lookup"><span data-stu-id="746b0-202">Updated hello SAP6 and SAP6User templates toouse hello new object level error functionality.</span></span>
* <span data-ttu-id="746b0-203">Conector Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="746b0-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="746b0-204">Al exportar, necesita un certificador por cada libreta de direcciones.</span><span class="sxs-lookup"><span data-stu-id="746b0-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="746b0-205">Puede ahora use Hola misma contraseña para todos los certificadores toomake Hola la administración sea más fácil.</span><span class="sxs-lookup"><span data-stu-id="746b0-205">You can now use hello same password for all certifiers toomake hello management easier.</span></span>

<span data-ttu-id="746b0-206">**Problemas corregidos:**</span><span class="sxs-lookup"><span data-stu-id="746b0-206">**Fixed issues:**</span></span>

* <span data-ttu-id="746b0-207">Conector LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="746b0-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="746b0-208">En el caso de IBM Tivoli DS, no se detectaban correctamente algunos atributos de referencia.</span><span class="sxs-lookup"><span data-stu-id="746b0-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="746b0-209">Para LDAP abierto durante una importación delta, se truncan los espacios en blanco al principio de Hola y al final de cadenas.</span><span class="sxs-lookup"><span data-stu-id="746b0-209">For Open LDAP during a delta import, whitespaces at hello beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="746b0-210">Para Novell y NetIQ, una exportación que mueve un objeto entre las unidades organizativas o contenedores y en hello mismo tiempo objeto Hola cuyo nombre ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="746b0-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at hello same time renamed hello object failed.</span></span>
* <span data-ttu-id="746b0-211">Conector de servicios web:</span><span class="sxs-lookup"><span data-stu-id="746b0-211">Web Services Connector:</span></span>
  * <span data-ttu-id="746b0-212">Si el servicio web de hello tuviera varios extremos para el mismo enlace, a continuación, hello conector no correctamente detectó estos extremos.</span><span class="sxs-lookup"><span data-stu-id="746b0-212">If hello web service had multiple end-points for same binding, then hello Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="746b0-213">Conector Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="746b0-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="746b0-214">Una exportación de hello fullName atributo tooa correo electrónico de base de datos no funcionaron.</span><span class="sxs-lookup"><span data-stu-id="746b0-214">An export of hello fullName attribute tooa mail-in database did not work.</span></span>
  * <span data-ttu-id="746b0-215">Una exportación que tanto agregar y quitar a miembros de un grupo solo Hola exportado había agregado a los miembros.</span><span class="sxs-lookup"><span data-stu-id="746b0-215">An export which both added and removed member from a group only exported hello added members.</span></span>
  * <span data-ttu-id="746b0-216">Si un documento de notas no es válido (Hola atributo isValid establecido toofalse), Hola, a continuación, se produce un error de conector.</span><span class="sxs-lookup"><span data-stu-id="746b0-216">If a Notes Document is invalid (hello attribute isValid set toofalse), then hello Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="746b0-217">Versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="746b0-217">Older releases</span></span>
<span data-ttu-id="746b0-218">Antes de marzo de 2016, Hola conectores se publicaron como temas de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="746b0-218">Before March 2016, hello Connectors were released as support topics.</span></span>

<span data-ttu-id="746b0-219">**LDAP genérico**</span><span class="sxs-lookup"><span data-stu-id="746b0-219">**Generic LDAP**</span></span>

* <span data-ttu-id="746b0-220">[KB3078617](https://support.microsoft.com/kb/3078617) : 1.0.0597, septiembre de 2015</span><span class="sxs-lookup"><span data-stu-id="746b0-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="746b0-221">[KB3044896](https://support.microsoft.com/kb/3044896) : 1.0.0549, marzo de 2015</span><span class="sxs-lookup"><span data-stu-id="746b0-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="746b0-222">[KB3031009](https://support.microsoft.com/kb/3031009) : 1.0.0534, enero de 2015</span><span class="sxs-lookup"><span data-stu-id="746b0-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="746b0-223">[KB3008177](https://support.microsoft.com/kb/3008177) : 1.0.0419, septiembre de 2014</span><span class="sxs-lookup"><span data-stu-id="746b0-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="746b0-224">[KB2936070](https://support.microsoft.com/kb/2936070) : 4.3.1082, marzo de 2014</span><span class="sxs-lookup"><span data-stu-id="746b0-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="746b0-225">**Servicios web**</span><span class="sxs-lookup"><span data-stu-id="746b0-225">**WebServices**</span></span>

* <span data-ttu-id="746b0-226">[KB3008178](https://support.microsoft.com/kb/3008178) : 1.0.0419, septiembre de 2014</span><span class="sxs-lookup"><span data-stu-id="746b0-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="746b0-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="746b0-227">**PowerShell**</span></span>

* <span data-ttu-id="746b0-228">[KB3008179](https://support.microsoft.com/kb/3008179) : 1.0.0419, septiembre de 2014</span><span class="sxs-lookup"><span data-stu-id="746b0-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="746b0-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="746b0-229">**Lotus Domino**</span></span>

* <span data-ttu-id="746b0-230">[KB3096533](https://support.microsoft.com/kb/3096533) : 1.0.0597, septiembre de 2015</span><span class="sxs-lookup"><span data-stu-id="746b0-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="746b0-231">[KB3044895](https://support.microsoft.com/kb/3044895) : 1.0.0549, marzo de 2015</span><span class="sxs-lookup"><span data-stu-id="746b0-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="746b0-232">[KB2977286](https://support.microsoft.com/kb/2977286) : 5.3.0712, agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="746b0-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="746b0-233">[KB2932635](https://support.microsoft.com/kb/2932635) : 5.3.1003, febrero de 2014</span><span class="sxs-lookup"><span data-stu-id="746b0-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="746b0-234">[KB2899874](https://support.microsoft.com/kb/2899874) : 5.3.0721, octubre de 2013</span><span class="sxs-lookup"><span data-stu-id="746b0-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="746b0-235">[KB2875551](https://support.microsoft.com/kb/2875551) : 5.3.0534, agosto de 2013</span><span class="sxs-lookup"><span data-stu-id="746b0-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="746b0-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="746b0-236">Next steps</span></span>
<span data-ttu-id="746b0-237">Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.</span><span class="sxs-lookup"><span data-stu-id="746b0-237">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="746b0-238">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="746b0-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
