---
title: aaaConnectors en hello Azure AD Synchronization Service Manager UI | Documentos de Microsoft
description: Conocer la ficha conectores Hola Hola Synchronization Service Manager para Azure AD Connect.
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
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="9aaaa-103">Uso de conectores con hello Azure AD Connect Sync Service Manager</span><span class="sxs-lookup"><span data-stu-id="9aaaa-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="9aaaa-105">ficha de conectores de Hello es usado toomanage motor de sincronización de todos los sistemas Hola está conectado a.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="9aaaa-106">Acciones del conector</span><span class="sxs-lookup"><span data-stu-id="9aaaa-106">Connector actions</span></span>
| <span data-ttu-id="9aaaa-107">Acción</span><span class="sxs-lookup"><span data-stu-id="9aaaa-107">Action</span></span> | <span data-ttu-id="9aaaa-108">Comentario</span><span class="sxs-lookup"><span data-stu-id="9aaaa-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="9aaaa-109">Crear</span><span class="sxs-lookup"><span data-stu-id="9aaaa-109">Create</span></span> |<span data-ttu-id="9aaaa-110">No usar.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-110">Do not use.</span></span> <span data-ttu-id="9aaaa-111">Para conectar los bosques de AD tooadditional, usar a Asistente para la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="9aaaa-112">Propiedades</span><span class="sxs-lookup"><span data-stu-id="9aaaa-112">Properties</span></span> |<span data-ttu-id="9aaaa-113">Se usa para el filtrado por dominio y unidad organizativa.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="9aaaa-114">Eliminar</span><span class="sxs-lookup"><span data-stu-id="9aaaa-114">Delete</span></span>](#delete) |<span data-ttu-id="9aaaa-115">Tooeither usado eliminar datos de Hola Hola conector espacio o toodelete conexión tooa bosque.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="9aaaa-116">Configurar perfiles de ejecución</span><span class="sxs-lookup"><span data-stu-id="9aaaa-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="9aaaa-117">Excepción de filtrado, nada de dominio tooconfigure aquí.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="9aaaa-118">Esta acción se puede utilizar perfiles de ejecución de toosee ya configurado.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="9aaaa-119">Ejecute</span><span class="sxs-lookup"><span data-stu-id="9aaaa-119">Run</span></span> |<span data-ttu-id="9aaaa-120">Usar toostart ejecutar único de un perfil.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="9aaaa-121">Detención</span><span class="sxs-lookup"><span data-stu-id="9aaaa-121">Stop</span></span> |<span data-ttu-id="9aaaa-122">Detiene un conector que esté ejecutando un perfil.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="9aaaa-123">Exportar conector</span><span class="sxs-lookup"><span data-stu-id="9aaaa-123">Export Connector</span></span> |<span data-ttu-id="9aaaa-124">No usar.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-124">Do not use.</span></span> |
| <span data-ttu-id="9aaaa-125">Importar conector</span><span class="sxs-lookup"><span data-stu-id="9aaaa-125">Import Connector</span></span> |<span data-ttu-id="9aaaa-126">No usar.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-126">Do not use.</span></span> |
| <span data-ttu-id="9aaaa-127">Actualizar conector</span><span class="sxs-lookup"><span data-stu-id="9aaaa-127">Update Connector</span></span> |<span data-ttu-id="9aaaa-128">No usar.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-128">Do not use.</span></span> |
| <span data-ttu-id="9aaaa-129">Actualizar esquema</span><span class="sxs-lookup"><span data-stu-id="9aaaa-129">Refresh Schema</span></span> |<span data-ttu-id="9aaaa-130">Actualiza el esquema en caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="9aaaa-131">Es toouse preferido Hola opción en el Asistente para la instalación de hello en su lugar, desde el que también las actualizaciones de sincronización las reglas.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="9aaaa-132">Espacio del conector de búsqueda</span><span class="sxs-lookup"><span data-stu-id="9aaaa-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="9aaaa-133">Usar objetos de toofind y demasiado[siga un objeto y sus datos a través del sistema de hello](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="9aaaa-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="9aaaa-134">Eliminar</span><span class="sxs-lookup"><span data-stu-id="9aaaa-134">Delete</span></span>
<span data-ttu-id="9aaaa-135">acción de eliminación de Hello sirve para dos cosas distintas.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-135">hello delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="9aaaa-137">Hola opción **eliminar solo el espacio del conector** quita todos los datos, pero mantener Hola configuración.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="9aaaa-138">Hola opción **espacio conector eliminar y el conector** quita los datos de Hola y configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="9aaaa-139">Esta opción se usa cuando no desea tooconnect tooa bosque ya.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="9aaaa-140">Ambas opciones sincronización todos los objetos y actualización los objetos de metaverso de Hola.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="9aaaa-141">Se trata de una operación de larga duración.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="9aaaa-142">Configurar perfiles de ejecución</span><span class="sxs-lookup"><span data-stu-id="9aaaa-142">Configure Run Profiles</span></span>
<span data-ttu-id="9aaaa-143">Esta opción permite hello toosee configurados para un conector de perfiles de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="9aaaa-145">Espacio del conector de búsqueda</span><span class="sxs-lookup"><span data-stu-id="9aaaa-145">Search Connector Space</span></span>
<span data-ttu-id="9aaaa-146">acción de espacio de conector de búsqueda de Hello es útil toofind objetos y solucionar problemas de datos.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="9aaaa-148">Empiece seleccionando un **ámbito**.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="9aaaa-149">Puede buscar la base de datos (RDN, DN, delimitador, subárbol), o de estado del objeto de hello (todas las demás opciones).</span><span class="sxs-lookup"><span data-stu-id="9aaaa-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="9aaaa-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="9aaaa-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="9aaaa-151">Por ejemplo, si hace una búsqueda de un subárbol, obtiene todos los objetos de una unidad organizativa.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="9aaaa-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="9aaaa-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="9aaaa-153">En esta cuadrícula puede seleccionar un objeto, seleccione **propiedades**, y [seguirlo](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) de espacio del conector de origen de hello, mediante el metaverso hello y el espacio de conector de destino toohello.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="9aaaa-154">Cambiar la contraseña de la cuenta de hello AD DS</span><span class="sxs-lookup"><span data-stu-id="9aaaa-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="9aaaa-155">Si cambia la contraseña de la cuenta de hello, Hola servicio de sincronización ya no será capaz de tooimport y exportación de cambios tooon local AD.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="9aaaa-156">Puede ver la siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="9aaaa-156">You may see hello following:</span></span>

- <span data-ttu-id="9aaaa-157">se produce un error en el paso de importación y exportación de Hola para hello conector AD con error de "credenciales de inicio no".</span><span class="sxs-lookup"><span data-stu-id="9aaaa-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="9aaaa-158">En el Visor de eventos de Windows, registro de eventos de aplicación Hola contiene un error con 6000 de Id. de evento y el mensaje "hello toorun de agente"contoso.com"Error de administración porque las credenciales de hello no eran válidas."</span><span class="sxs-lookup"><span data-stu-id="9aaaa-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="9aaaa-159">Hola tooresolve emitir, cuenta de usuario de actualización Hola AD DS con hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="9aaaa-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="9aaaa-160">Iniciar Hola Synchronization Service Manager (servicio de sincronización de inicio →).</span><span class="sxs-lookup"><span data-stu-id="9aaaa-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="9aaaa-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="9aaaa-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="9aaaa-162">Vaya toohello **conectores** ficha.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="9aaaa-163">Seleccione Hola conector de AD que es configurado toouse hello cuenta AD DS.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="9aaaa-164">En Acciones, seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="9aaaa-165">En el cuadro de diálogo emergente de hello, seleccione Conectar tooActive directorio de bosque:</span><span class="sxs-lookup"><span data-stu-id="9aaaa-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="9aaaa-166">nombre de bosque de Hello indica Hola correspondiente local AD.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="9aaaa-167">nombre de usuario de Hello indica la cuenta de hello AD DS usada para la sincronización.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="9aaaa-168">Escriba Hola nueva contraseña de cuenta de hello AD DS en el cuadro de texto de contraseña de hello ![Azure AD conectarse sincronización de cifrado de clave de utilidad](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="9aaaa-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="9aaaa-169">Haga clic en Aceptar toosave Hola nueva contraseña y reinicie Hola Synchronization Service tooremove Hola contraseña antigua de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="9aaaa-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9aaaa-170">Next steps</span></span>
<span data-ttu-id="9aaaa-171">Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.</span><span class="sxs-lookup"><span data-stu-id="9aaaa-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="9aaaa-172">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9aaaa-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
