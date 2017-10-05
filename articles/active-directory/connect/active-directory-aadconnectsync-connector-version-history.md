---
title: Historial de versiones de conectores | Microsoft Docs
description: En este tema se incluyen todas las versiones de los conectores para Forefront Identity Manager (FIM) y Microsoft Identity Manager (MIM).
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
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="81b9f-103">Historial de versiones de conectores</span><span class="sxs-lookup"><span data-stu-id="81b9f-103">Connector Version Release History</span></span>
<span data-ttu-id="81b9f-104">Los conectores de Forefront Identity Manager (FIM) y Microsoft Identity Manager (MIM) se actualizan con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="81b9f-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="81b9f-105">Este tema solo está disponible en FIM y MIM.</span><span class="sxs-lookup"><span data-stu-id="81b9f-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="81b9f-106">No se admite la instalación de estos conectores en Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="81b9f-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="81b9f-107">Los conectores publicados están preinstalados en ADDConnect al actualizarse a la compilación especificada.</span><span class="sxs-lookup"><span data-stu-id="81b9f-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="81b9f-108">En este tema se muestran todas las versiones de los conectores que se han publicado.</span><span class="sxs-lookup"><span data-stu-id="81b9f-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="81b9f-109">Vínculos relacionados:</span><span class="sxs-lookup"><span data-stu-id="81b9f-109">Related links:</span></span>

* [<span data-ttu-id="81b9f-110">Descargar los últimos conectores</span><span class="sxs-lookup"><span data-stu-id="81b9f-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="81b9f-111">[conector LDAP genérico](active-directory-aadconnectsync-connector-genericldap.md) </span><span class="sxs-lookup"><span data-stu-id="81b9f-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="81b9f-112">[conector SQL genérico](active-directory-aadconnectsync-connector-genericsql.md) </span><span class="sxs-lookup"><span data-stu-id="81b9f-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="81b9f-113">[conector de servicios web](http://go.microsoft.com/fwlink/?LinkID=226245) </span><span class="sxs-lookup"><span data-stu-id="81b9f-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="81b9f-114">[conector PowerShell](active-directory-aadconnectsync-connector-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="81b9f-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="81b9f-115">[conector Lotus Domino](active-directory-aadconnectsync-connector-domino.md) </span><span class="sxs-lookup"><span data-stu-id="81b9f-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="81b9f-116">1.1.604.0 (AADConnect pendiente de publicación)</span><span class="sxs-lookup"><span data-stu-id="81b9f-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="81b9f-117">Problemas corregidos:</span><span class="sxs-lookup"><span data-stu-id="81b9f-117">Fixed issues:</span></span>

* <span data-ttu-id="81b9f-118">Servicios Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="81b9f-118">Generic Web Services:</span></span>
  * <span data-ttu-id="81b9f-119">Se corrigió un problema que impedía la creación de un proyecto SOAP cuando había dos o más puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="81b9f-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="81b9f-120">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-120">Generic SQL:</span></span>
  * <span data-ttu-id="81b9f-121">En la operación de importación, GSQL no convertía el tiempo correctamente al guardarse en el espacio del conector.</span><span class="sxs-lookup"><span data-stu-id="81b9f-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="81b9f-122">El formato de fecha y hora predeterminado para el espacio del conector de GSQL se cambió de "aaaa-MM-dd hh:mm:ssZ" a "aaaa-MM-dd HH:mm:ssZ".</span><span class="sxs-lookup"><span data-stu-id="81b9f-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="81b9f-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="81b9f-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="81b9f-124">Problemas corregidos:</span><span class="sxs-lookup"><span data-stu-id="81b9f-124">Fixed issues:</span></span>

* <span data-ttu-id="81b9f-125">Servicios Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="81b9f-125">Generic Web Services:</span></span>
  * <span data-ttu-id="81b9f-126">La herramienta Wsconfig no convirtió correctamente la matriz JSON de "solicitud de ejemplo" para el método del servicio REST.</span><span class="sxs-lookup"><span data-stu-id="81b9f-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="81b9f-127">Esto generó problemas de serialización de esta matriz JSON para la solicitud de REST.</span><span class="sxs-lookup"><span data-stu-id="81b9f-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="81b9f-128">La herramienta de configuración del conector de servicio web no admite el uso de espacios en nombres de atributo JSON</span><span class="sxs-lookup"><span data-stu-id="81b9f-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="81b9f-129">Se puede agregar manualmente un patrón de sustitución al archivo WSConfigTool.exe.config, p. ej., ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="81b9f-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="81b9f-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="81b9f-130">Lotus Notes:</span></span>
  * <span data-ttu-id="81b9f-131">Cuando la opción **Allow custom certifiers for Organization/Organizational Units** (Permitir certificadores personalizados para la organización/unidades organizativas) está deshabilitada, el conector produce un error durante la exportación (Actualización) Después del flujo de exportación, se exportan todos los atributos a Domino, pero en el momento de la exportación se devuelve una excepción KeyNotFoundException a Sync.</span><span class="sxs-lookup"><span data-stu-id="81b9f-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="81b9f-132">Esto sucede porque se produce un error en la operación de cambio de nombre al intentar cambiar DN (atributo UserName) cambiando uno de los atributos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81b9f-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="81b9f-133">Apellidos</span><span class="sxs-lookup"><span data-stu-id="81b9f-133">LastName</span></span>
      - <span data-ttu-id="81b9f-134">Nombre</span><span class="sxs-lookup"><span data-stu-id="81b9f-134">FirstName</span></span>
      - <span data-ttu-id="81b9f-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="81b9f-135">MiddleInitial</span></span>
      - <span data-ttu-id="81b9f-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="81b9f-136">AltFullName</span></span>
      - <span data-ttu-id="81b9f-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="81b9f-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="81b9f-138">ou</span><span class="sxs-lookup"><span data-stu-id="81b9f-138">ou</span></span>
      - <span data-ttu-id="81b9f-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="81b9f-139">altcommonname</span></span>

  * <span data-ttu-id="81b9f-140">Cuando la opción **Allow custom certifiers for Organization/Organizational Units** (Permitir certificadores personalizados para la organización/unidades organizativas) está habilitada pero los certificadores necesarios siguen vacíos, se produce una excepción KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="81b9f-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="81b9f-141">Mejoras:</span><span class="sxs-lookup"><span data-stu-id="81b9f-141">Enhancements:</span></span>

* <span data-ttu-id="81b9f-142">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-142">Generic SQL:</span></span>
  * <span data-ttu-id="81b9f-143">**Escenario: rediseñado implementado:** característica "*"</span><span class="sxs-lookup"><span data-stu-id="81b9f-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="81b9f-144">**Descripción de la solución:** se cambió el enfoque para el [control de los atributos de referencia multivalor](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="81b9f-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="81b9f-145">Problemas corregidos:</span><span class="sxs-lookup"><span data-stu-id="81b9f-145">Fixed issues:</span></span>

* <span data-ttu-id="81b9f-146">Servicios Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="81b9f-146">Generic Web Services:</span></span>
  * <span data-ttu-id="81b9f-147">No se puede importar la configuración del servidor si está presente el conector de WebService</span><span class="sxs-lookup"><span data-stu-id="81b9f-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="81b9f-148">El conector de WebService no funciona con varios servicios web</span><span class="sxs-lookup"><span data-stu-id="81b9f-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="81b9f-149">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-149">Generic SQL:</span></span>
  * <span data-ttu-id="81b9f-150">No hay tipos de objeto para atributos de referencia de un único valor</span><span class="sxs-lookup"><span data-stu-id="81b9f-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="81b9f-151">La importación diferencial en la estrategia de Change Tracking elimina el objeto cuando se quita el valor de la tabla multivalor</span><span class="sxs-lookup"><span data-stu-id="81b9f-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="81b9f-152">OverflowException en conector GSQL con DB2 en AS/400</span><span class="sxs-lookup"><span data-stu-id="81b9f-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="81b9f-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="81b9f-153">Lotus:</span></span>
  * <span data-ttu-id="81b9f-154">Se ha agregado la opción para habilitar o deshabilitar la búsqueda de unidades organizativas antes de abrir la página de GlobalParameters</span><span class="sxs-lookup"><span data-stu-id="81b9f-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="81b9f-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="81b9f-155">1.1.443.0</span></span>

<span data-ttu-id="81b9f-156">Publicación: marzo de 2017</span><span class="sxs-lookup"><span data-stu-id="81b9f-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="81b9f-157">Mejoras</span><span class="sxs-lookup"><span data-stu-id="81b9f-157">Enhancements</span></span>

* <span data-ttu-id="81b9f-158">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-158">Generic SQL:</span></span></br><span data-ttu-id="81b9f-159">
  **Síntomas del escenario:** se trata de una limitación conocida con el Conector de SQL en la que solo se permite una referencia a un tipo de objeto y se requiere referencia cruzada con los miembros.</span><span class="sxs-lookup"><span data-stu-id="81b9f-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="81b9f-160">
**Descripción de la solución:** en el paso de procesamiento de las referencias en que se elige la opción "*", TODAS las combinaciones de tipos de objeto se devolverán al motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="81b9f-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="81b9f-161">Con esto se crearán muchos marcadores de posición</span><span class="sxs-lookup"><span data-stu-id="81b9f-161">This will create many placeholders</span></span>
- <span data-ttu-id="81b9f-162">Es necesario asegurarse de que la nomenclatura sea única entre todos los tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="81b9f-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="81b9f-163">LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-163">Generic LDAP:</span></span></br><span data-ttu-id="81b9f-164">
 **Escenario:** cuando solo se seleccionan algunos contenedores en una partición específica, la búsqueda se seguirá haciendo en toda la partición.</span><span class="sxs-lookup"><span data-stu-id="81b9f-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="81b9f-165">El servicio de sincronización filtrará la partición específica, pero MA no lo hará, lo que podría provocar una degradación del rendimiento.</span><span class="sxs-lookup"><span data-stu-id="81b9f-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="81b9f-166">**Descripción de la solución:** se modificó el código del conector GLDAP para permitir que pase por todos los contenedores y objetos de búsqueda de cada uno de ellos, en lugar de buscar en toda la partición.</span><span class="sxs-lookup"><span data-stu-id="81b9f-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="81b9f-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="81b9f-167">Lotus Domino:</span></span>

  <span data-ttu-id="81b9f-168">**Escenario:** compatibilidad de la eliminación de correo de Domino para la eliminación de una persona durante una exportación.</span><span class="sxs-lookup"><span data-stu-id="81b9f-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="81b9f-169">
  **Solución:** configuración de eliminación de correo configurable para la eliminación de una persona durante una exportación.</span><span class="sxs-lookup"><span data-stu-id="81b9f-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="81b9f-170">Problemas corregidos:</span><span class="sxs-lookup"><span data-stu-id="81b9f-170">Fixed issues:</span></span>
* <span data-ttu-id="81b9f-171">Servicios Web genéricos:</span><span class="sxs-lookup"><span data-stu-id="81b9f-171">Generic Web Services:</span></span>
 * <span data-ttu-id="81b9f-172">Cuando cambia la URL de servicio en proyectos wsconfig de SAP predeterminados mediante la herramienta de configuración WebService, aparece el error siguiente: No se pudo encontrar parte de la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="81b9f-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="81b9f-173">LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-173">Generic LDAP:</span></span>
 * <span data-ttu-id="81b9f-174">Conector GLDAP no ve todos los atributos en AD LDS</span><span class="sxs-lookup"><span data-stu-id="81b9f-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="81b9f-175">El asistente se interrumpe cuando no se detectan atributos de UPN desde el esquema de directorio de LDAP</span><span class="sxs-lookup"><span data-stu-id="81b9f-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="81b9f-176">Error de importaciones diferenciales cuando no hay errores de detección durante la importación completa, cuando no se selecciona el atributo "objectclass"</span><span class="sxs-lookup"><span data-stu-id="81b9f-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="81b9f-177">La página de configuración "Configurar particiones y jerarquías" no muestra ningún objeto en que el tipo sea igual a la partición de los servidores Novel en MA del LDAP</span><span class="sxs-lookup"><span data-stu-id="81b9f-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="81b9f-178">genérico.</span><span class="sxs-lookup"><span data-stu-id="81b9f-178">LDAP MA.</span></span> <span data-ttu-id="81b9f-179">Solo se muestran objetos desde la partición RootDSE.</span><span class="sxs-lookup"><span data-stu-id="81b9f-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="81b9f-180">SQL genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-180">Generic SQL:</span></span>
 * <span data-ttu-id="81b9f-181">Corrección para el error en que el atributo multivalor de importación diferencial de límite de SQL genérico no se puede importar</span><span class="sxs-lookup"><span data-stu-id="81b9f-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="81b9f-182">Cuando se exportan valores eliminados o agregados del atributo multivalor, no se eliminan ni agregan en el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="81b9f-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="81b9f-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="81b9f-183">Lotus Notes:</span></span>
 * <span data-ttu-id="81b9f-184">Un campo específico "Nombre completo" aparece correctamente en el metaverso; sin embargo, cuando se realiza la exportación a Notes, el valor del atributo es Null o Empty.</span><span class="sxs-lookup"><span data-stu-id="81b9f-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="81b9f-185">Corrección para error de certificador duplicado</span><span class="sxs-lookup"><span data-stu-id="81b9f-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="81b9f-186">Cuando se selecciona un objeto sin datos en el conector para Lotus Domino con otros objetos, se recibe el error de detección durante la importación completa.</span><span class="sxs-lookup"><span data-stu-id="81b9f-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="81b9f-187">Cuando la importación diferencial se ejecuta en el conector para Lotus Dominio, al final de esa ejecución, el servicio Microsoft.IdentityManagement.MA.LotusDomino.Service.exe a veces muestra un error de aplicación.</span><span class="sxs-lookup"><span data-stu-id="81b9f-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="81b9f-188">La pertenencia general a grupos funciona correctamente y se mantiene, excepto cuando se ejecuta la exportación para intentar quitar un usuario de la pertenencia; ahí se muestra como una acción correcta con una actualización, pero el usuario no se quita realmente de la pertenencia en Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="81b9f-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="81b9f-189">Se agregó una oportunidad para elegir el modo de exportación como "Append Item at bottom" (Anexar el elemento al final) en la GUI de configuración de Lotus MA para anexar elementos nuevos al final durante la exportación de atributos multivalor.</span><span class="sxs-lookup"><span data-stu-id="81b9f-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="81b9f-190">El conector agregará la lógica que se necesita para eliminar el archivo de la carpeta de correo y el almacén de id.</span><span class="sxs-lookup"><span data-stu-id="81b9f-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="81b9f-191">La eliminación de pertenencias no funciona entre los miembros de NAB.</span><span class="sxs-lookup"><span data-stu-id="81b9f-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="81b9f-192">Los valores se deben eliminar correctamente del atributo multivalor</span><span class="sxs-lookup"><span data-stu-id="81b9f-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="81b9f-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="81b9f-193">1.1.117.0</span></span>
<span data-ttu-id="81b9f-194">Publicación: marzo de 2016</span><span class="sxs-lookup"><span data-stu-id="81b9f-194">Released: 2016 March</span></span>

<span data-ttu-id="81b9f-195">**Nuevo conector**</span><span class="sxs-lookup"><span data-stu-id="81b9f-195">**New Connector**</span></span>  
<span data-ttu-id="81b9f-196">Versión inicial del [conector SQL genérico](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="81b9f-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="81b9f-197">**Nuevas características:**</span><span class="sxs-lookup"><span data-stu-id="81b9f-197">**New features:**</span></span>

* <span data-ttu-id="81b9f-198">Conector LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="81b9f-199">Se agregó compatibilidad para la importación diferencial con Isode.</span><span class="sxs-lookup"><span data-stu-id="81b9f-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="81b9f-200">Conector de servicios web:</span><span class="sxs-lookup"><span data-stu-id="81b9f-200">Web Services Connector:</span></span>
  * <span data-ttu-id="81b9f-201">Se han actualizado las actividades csEntryChangeResult y setImportErrorCode para permitir que los errores de nivel de objeto se devuelvan al motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="81b9f-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="81b9f-202">Se han actualizado las plantillas SAP6 y SAP6User para utilizar la nueva funcionalidad de error de nivel de objeto.</span><span class="sxs-lookup"><span data-stu-id="81b9f-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="81b9f-203">Conector Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="81b9f-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="81b9f-204">Al exportar, necesita un certificador por cada libreta de direcciones.</span><span class="sxs-lookup"><span data-stu-id="81b9f-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="81b9f-205">Ahora puede usar la misma contraseña para todos los certificadores a fin de facilitar la administración.</span><span class="sxs-lookup"><span data-stu-id="81b9f-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="81b9f-206">**Problemas corregidos:**</span><span class="sxs-lookup"><span data-stu-id="81b9f-206">**Fixed issues:**</span></span>

* <span data-ttu-id="81b9f-207">Conector LDAP genérico:</span><span class="sxs-lookup"><span data-stu-id="81b9f-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="81b9f-208">En el caso de IBM Tivoli DS, no se detectaban correctamente algunos atributos de referencia.</span><span class="sxs-lookup"><span data-stu-id="81b9f-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="81b9f-209">En el caso de Open LDAP durante una importación diferencial, se truncaban los espacios en blanco al principio y al final de las cadenas.</span><span class="sxs-lookup"><span data-stu-id="81b9f-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="81b9f-210">En el caso de Novell y NetIQ, se producía un error en las exportaciones que trasladaban un objeto entre UO/contenedores y, a la vez, cambiaban el nombre del objeto.</span><span class="sxs-lookup"><span data-stu-id="81b9f-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="81b9f-211">Conector de servicios web:</span><span class="sxs-lookup"><span data-stu-id="81b9f-211">Web Services Connector:</span></span>
  * <span data-ttu-id="81b9f-212">Si el servicio web tenía varios puntos de conexión para el mismo enlace, el conector no los detectaba correctamente.</span><span class="sxs-lookup"><span data-stu-id="81b9f-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="81b9f-213">Conector Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="81b9f-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="81b9f-214">No funcionaban las exportaciones del atributo fullName a una base de datos de recepción de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="81b9f-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="81b9f-215">Las exportaciones que agregaban y quitaban miembros de un grupo solo exportaban los miembros agregados.</span><span class="sxs-lookup"><span data-stu-id="81b9f-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="81b9f-216">Si un documento de notas no es válido (el atributo isValid se definía como false), se produce un error en el conector.</span><span class="sxs-lookup"><span data-stu-id="81b9f-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="81b9f-217">Versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="81b9f-217">Older releases</span></span>
<span data-ttu-id="81b9f-218">Antes de marzo de 2016, los conectores se publicaban como temas de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="81b9f-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="81b9f-219">**LDAP genérico**</span><span class="sxs-lookup"><span data-stu-id="81b9f-219">**Generic LDAP**</span></span>

* <span data-ttu-id="81b9f-220">[KB3078617](https://support.microsoft.com/kb/3078617) : 1.0.0597, septiembre de 2015</span><span class="sxs-lookup"><span data-stu-id="81b9f-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="81b9f-221">[KB3044896](https://support.microsoft.com/kb/3044896) : 1.0.0549, marzo de 2015</span><span class="sxs-lookup"><span data-stu-id="81b9f-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="81b9f-222">[KB3031009](https://support.microsoft.com/kb/3031009) : 1.0.0534, enero de 2015</span><span class="sxs-lookup"><span data-stu-id="81b9f-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="81b9f-223">[KB3008177](https://support.microsoft.com/kb/3008177) : 1.0.0419, septiembre de 2014</span><span class="sxs-lookup"><span data-stu-id="81b9f-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="81b9f-224">[KB2936070](https://support.microsoft.com/kb/2936070) : 4.3.1082, marzo de 2014</span><span class="sxs-lookup"><span data-stu-id="81b9f-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="81b9f-225">**Servicios web**</span><span class="sxs-lookup"><span data-stu-id="81b9f-225">**WebServices**</span></span>

* <span data-ttu-id="81b9f-226">[KB3008178](https://support.microsoft.com/kb/3008178) : 1.0.0419, septiembre de 2014</span><span class="sxs-lookup"><span data-stu-id="81b9f-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="81b9f-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="81b9f-227">**PowerShell**</span></span>

* <span data-ttu-id="81b9f-228">[KB3008179](https://support.microsoft.com/kb/3008179) : 1.0.0419, septiembre de 2014</span><span class="sxs-lookup"><span data-stu-id="81b9f-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="81b9f-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="81b9f-229">**Lotus Domino**</span></span>

* <span data-ttu-id="81b9f-230">[KB3096533](https://support.microsoft.com/kb/3096533) : 1.0.0597, septiembre de 2015</span><span class="sxs-lookup"><span data-stu-id="81b9f-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="81b9f-231">[KB3044895](https://support.microsoft.com/kb/3044895) : 1.0.0549, marzo de 2015</span><span class="sxs-lookup"><span data-stu-id="81b9f-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="81b9f-232">[KB2977286](https://support.microsoft.com/kb/2977286) : 5.3.0712, agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="81b9f-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="81b9f-233">[KB2932635](https://support.microsoft.com/kb/2932635) : 5.3.1003, febrero de 2014</span><span class="sxs-lookup"><span data-stu-id="81b9f-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="81b9f-234">[KB2899874](https://support.microsoft.com/kb/2899874) : 5.3.0721, octubre de 2013</span><span class="sxs-lookup"><span data-stu-id="81b9f-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="81b9f-235">[KB2875551](https://support.microsoft.com/kb/2875551) : 5.3.0534, agosto de 2013</span><span class="sxs-lookup"><span data-stu-id="81b9f-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="81b9f-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81b9f-236">Next steps</span></span>
<span data-ttu-id="81b9f-237">Obtenga más información sobre la configuración de la [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="81b9f-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="81b9f-238">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="81b9f-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
