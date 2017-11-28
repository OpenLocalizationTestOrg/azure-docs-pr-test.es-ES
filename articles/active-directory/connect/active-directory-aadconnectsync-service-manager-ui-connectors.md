---
title: Conectores de la interfaz de usuario de Synchronization Service Manager de Azure AD | Microsoft Docs
description: "Conozca la pestaña Conectores de Synchronization Service Manager para Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0fae4b1755ca95466eeffb5ce61c1c7855d7381
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="beaa6-103">Uso de conectores con Sync Service Manager de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="beaa6-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="beaa6-105">La pestaña Conectores se usa para administrar todos los sistemas a los que está conectado el motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="beaa6-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="beaa6-106">Acciones del conector</span><span class="sxs-lookup"><span data-stu-id="beaa6-106">Connector actions</span></span>
| <span data-ttu-id="beaa6-107">Acción</span><span class="sxs-lookup"><span data-stu-id="beaa6-107">Action</span></span> | <span data-ttu-id="beaa6-108">Comentario</span><span class="sxs-lookup"><span data-stu-id="beaa6-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="beaa6-109">Crear</span><span class="sxs-lookup"><span data-stu-id="beaa6-109">Create</span></span> |<span data-ttu-id="beaa6-110">No usar.</span><span class="sxs-lookup"><span data-stu-id="beaa6-110">Do not use.</span></span> <span data-ttu-id="beaa6-111">Para conectarse a los bosques de AD adicionales, use el Asistente para instalación.</span><span class="sxs-lookup"><span data-stu-id="beaa6-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="beaa6-112">Propiedades</span><span class="sxs-lookup"><span data-stu-id="beaa6-112">Properties</span></span> |<span data-ttu-id="beaa6-113">Se usa para el filtrado por dominio y unidad organizativa.</span><span class="sxs-lookup"><span data-stu-id="beaa6-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="beaa6-114">Eliminar</span><span class="sxs-lookup"><span data-stu-id="beaa6-114">Delete</span></span>](#delete) |<span data-ttu-id="beaa6-115">Se usa para eliminar los datos en el espacio del conector o eliminar la conexión a un bosque.</span><span class="sxs-lookup"><span data-stu-id="beaa6-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="beaa6-116">Configurar perfiles de ejecución</span><span class="sxs-lookup"><span data-stu-id="beaa6-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="beaa6-117">A excepción del filtrado de dominio, no es necesario configurar ninguna otra opción.</span><span class="sxs-lookup"><span data-stu-id="beaa6-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="beaa6-118">Puede utilizar esta acción para ver los perfiles de ejecución ya configurados.</span><span class="sxs-lookup"><span data-stu-id="beaa6-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="beaa6-119">Ejecute</span><span class="sxs-lookup"><span data-stu-id="beaa6-119">Run</span></span> |<span data-ttu-id="beaa6-120">Se usa para iniciar una ejecución única de un perfil.</span><span class="sxs-lookup"><span data-stu-id="beaa6-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="beaa6-121">Detención</span><span class="sxs-lookup"><span data-stu-id="beaa6-121">Stop</span></span> |<span data-ttu-id="beaa6-122">Detiene un conector que esté ejecutando un perfil.</span><span class="sxs-lookup"><span data-stu-id="beaa6-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="beaa6-123">Exportar conector</span><span class="sxs-lookup"><span data-stu-id="beaa6-123">Export Connector</span></span> |<span data-ttu-id="beaa6-124">No usar.</span><span class="sxs-lookup"><span data-stu-id="beaa6-124">Do not use.</span></span> |
| <span data-ttu-id="beaa6-125">Importar conector</span><span class="sxs-lookup"><span data-stu-id="beaa6-125">Import Connector</span></span> |<span data-ttu-id="beaa6-126">No usar.</span><span class="sxs-lookup"><span data-stu-id="beaa6-126">Do not use.</span></span> |
| <span data-ttu-id="beaa6-127">Actualizar conector</span><span class="sxs-lookup"><span data-stu-id="beaa6-127">Update Connector</span></span> |<span data-ttu-id="beaa6-128">No usar.</span><span class="sxs-lookup"><span data-stu-id="beaa6-128">Do not use.</span></span> |
| <span data-ttu-id="beaa6-129">Actualizar esquema</span><span class="sxs-lookup"><span data-stu-id="beaa6-129">Refresh Schema</span></span> |<span data-ttu-id="beaa6-130">Actualiza el esquema en caché.</span><span class="sxs-lookup"><span data-stu-id="beaa6-130">Refreshes the cached schema.</span></span> <span data-ttu-id="beaa6-131">Es preferible usar la opción en el Asistente para la instalación, ya que también actualizará las reglas de sincronización.</span><span class="sxs-lookup"><span data-stu-id="beaa6-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="beaa6-132">Espacio del conector de búsqueda</span><span class="sxs-lookup"><span data-stu-id="beaa6-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="beaa6-133">Se usa para buscar objetos y realizar un [seguimiento de un objeto y sus datos a través del sistema](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="beaa6-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="beaa6-134">Eliminar</span><span class="sxs-lookup"><span data-stu-id="beaa6-134">Delete</span></span>
<span data-ttu-id="beaa6-135">La acción de eliminación se usa para dos objetivos diferentes.</span><span class="sxs-lookup"><span data-stu-id="beaa6-135">The delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="beaa6-137">Con la opción **Delete connector space only** (Eliminar solo el espacio del conector) se eliminarán todos los datos, pero se mantendrá la configuración.</span><span class="sxs-lookup"><span data-stu-id="beaa6-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="beaa6-138">Con la opción **Delete Connector and connector space** (Eliminar el conector y el espacio del conector) se eliminarán los datos y la configuración.</span><span class="sxs-lookup"><span data-stu-id="beaa6-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="beaa6-139">Esta opción se usa cuando no se desea volver a conectarse a un bosque.</span><span class="sxs-lookup"><span data-stu-id="beaa6-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="beaa6-140">Ambas sincronizarán todos los objetos y actualizarán los objetos del metaverso.</span><span class="sxs-lookup"><span data-stu-id="beaa6-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="beaa6-141">Se trata de una operación de larga duración.</span><span class="sxs-lookup"><span data-stu-id="beaa6-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="beaa6-142">Configurar perfiles de ejecución</span><span class="sxs-lookup"><span data-stu-id="beaa6-142">Configure Run Profiles</span></span>
<span data-ttu-id="beaa6-143">Esta opción permite ver los perfiles de ejecución configurados para un conector.</span><span class="sxs-lookup"><span data-stu-id="beaa6-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="beaa6-145">Espacio del conector de búsqueda</span><span class="sxs-lookup"><span data-stu-id="beaa6-145">Search Connector Space</span></span>
<span data-ttu-id="beaa6-146">La acción del espacio del conector de búsqueda es útil para buscar objetos y solucionar problemas de datos.</span><span class="sxs-lookup"><span data-stu-id="beaa6-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="beaa6-148">Empiece seleccionando un **ámbito**.</span><span class="sxs-lookup"><span data-stu-id="beaa6-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="beaa6-149">Puede buscar según los datos (RDN, DN, delimitador, subárbol) o el estado del objeto (todas las demás opciones).</span><span class="sxs-lookup"><span data-stu-id="beaa6-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="beaa6-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="beaa6-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="beaa6-151">Por ejemplo, si hace una búsqueda de un subárbol, obtiene todos los objetos de una unidad organizativa.</span><span class="sxs-lookup"><span data-stu-id="beaa6-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="beaa6-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="beaa6-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="beaa6-153">En esta cuadrícula, puede seleccionar un objeto, elegir las **propiedades** y [realizar un seguimiento](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) desde el espacio del conector de origen, a través del metaverso, y hasta el espacio del conector de destino.</span><span class="sxs-lookup"><span data-stu-id="beaa6-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="beaa6-154">Cambio de la contraseña de la cuenta de AD DS</span><span class="sxs-lookup"><span data-stu-id="beaa6-154">Changing the AD DS account password</span></span>
<span data-ttu-id="beaa6-155">Si cambia la contraseña de la cuenta, el servicio de sincronización ya no podrá importar o exportar cambios a las instancias locales de AD.</span><span class="sxs-lookup"><span data-stu-id="beaa6-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="beaa6-156">Verá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="beaa6-156">You may see the following:</span></span>

- <span data-ttu-id="beaa6-157">Se produce un error en el paso de importación y exportación para el conector de AD con el error "no-start-credentials".</span><span class="sxs-lookup"><span data-stu-id="beaa6-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="beaa6-158">En el Visor de eventos de Windows, el registro de eventos de aplicación contiene un error con el identificador de evento 6000 y mensaje “El agente de administración "contoso.com" no se pudo ejecutar porque las credenciales no eran válidas”.</span><span class="sxs-lookup"><span data-stu-id="beaa6-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="beaa6-159">Para resolver el problema, actualice la cuenta de usuario de AD DS mediante lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="beaa6-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="beaa6-160">Inicie el Synchronization Service Manager (INICIO → Synchronization Service).</span><span class="sxs-lookup"><span data-stu-id="beaa6-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="beaa6-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="beaa6-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="beaa6-162">Vaya a la pestaña **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="beaa6-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="beaa6-163">Seleccione el conector de AD que está configurado para usar la cuenta de AD DS.</span><span class="sxs-lookup"><span data-stu-id="beaa6-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="beaa6-164">En Acciones, seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="beaa6-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="beaa6-165">En el cuadro de diálogo emergente, seleccione Connect to Active Directory Forest (Conectar con el bosque de Active Directory):</span><span class="sxs-lookup"><span data-stu-id="beaa6-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="beaa6-166">El nombre de bosque indica la instancia local de AD correspondiente.</span><span class="sxs-lookup"><span data-stu-id="beaa6-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="beaa6-167">El nombre de usuario indica la cuenta de AD DS que se usa para la sincronización.</span><span class="sxs-lookup"><span data-stu-id="beaa6-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="beaa6-168">Escriba la nueva contraseña de la cuenta de AD DS en el cuadro de texto Contraseña ![Utilidad de clave de cifrado de Azure AD Connect Sync](media/active-directory-aadconnectsync-encryption-key/key6.png).</span><span class="sxs-lookup"><span data-stu-id="beaa6-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="beaa6-169">Haga clic en Aceptar para guardar la nueva contraseña y reinicie Synchronization Service para quitar la contraseña antigua de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="beaa6-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="beaa6-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="beaa6-170">Next steps</span></span>
<span data-ttu-id="beaa6-171">Obtenga más información sobre la configuración de la [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="beaa6-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="beaa6-172">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="beaa6-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
