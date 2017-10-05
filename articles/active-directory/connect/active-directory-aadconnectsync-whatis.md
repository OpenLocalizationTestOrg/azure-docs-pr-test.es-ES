---
title: "Sincronización de Azure AD Connect: descripción y personalización de la sincronización | Microsoft Docs"
description: "Se explica cómo funciona la sincronización de Azure AD Connect y cómo personalizarla."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 4edac05325ad12596d982d113df0db7461124b12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a><span data-ttu-id="d72cd-103">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="d72cd-103">Azure AD Connect sync: Understand and customize synchronization</span></span>
<span data-ttu-id="d72cd-104">Los servicios de sincronización de Azure Active Directory Connect (sincronización de Azure AD Connect) es un componente principal de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d72cd-104">The Azure Active Directory Connect synchronization services (Azure AD Connect sync) is a main component of Azure AD Connect.</span></span> <span data-ttu-id="d72cd-105">Se encargan de todas las operaciones relacionadas con la sincronización de datos de identidad entre el entorno local y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d72cd-105">It takes care of all the operations that are related to synchronize identity data between your on-premises environment and Azure AD.</span></span> <span data-ttu-id="d72cd-106">Sincronización de Azure AD Connect es el sucesor de DirSync, Sincronización de Azure AD y Forefront Identity Manager con Conector Azure Active Directory configurado.</span><span class="sxs-lookup"><span data-stu-id="d72cd-106">Azure AD Connect sync is the successor of DirSync, Azure AD Sync, and Forefront Identity Manager with the Azure Active Directory Connector configured.</span></span>

<span data-ttu-id="d72cd-107">Este tema es la principal referencia sobre la **sincronización de Azure AD Connect** (que también se conoce como **motor de sincronización**) y en el que se muestran vínculos a todos los otros demás temas relacionados con ella.</span><span class="sxs-lookup"><span data-stu-id="d72cd-107">This topic is the home for **Azure AD Connect sync** (also called **sync engine**) and lists links to all other topics related to it.</span></span> <span data-ttu-id="d72cd-108">Para obtener vínculos para Azure AD Connect, consulte [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d72cd-108">For links to Azure AD Connect, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="d72cd-109">El servicio de sincronización consta de dos componentes, el componente de **sincronización de Azure AD Connect** local y el lado del servicio en Azure AD llamado **servicio de sincronización de Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="d72cd-109">The sync service consists of two components, the on-premises **Azure AD Connect sync** component and the service side in Azure AD called **Azure AD Connect sync service**.</span></span> <span data-ttu-id="d72cd-110">El servicio es común para DirSync, Sincronización de Azure AD y Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d72cd-110">The service is common for DirSync, Azure AD Sync, and Azure AD Connect.</span></span>

## <a name="azure-ad-connect-sync-topics"></a><span data-ttu-id="d72cd-111">Temas de sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d72cd-111">Azure AD Connect sync topics</span></span>
| <span data-ttu-id="d72cd-112">Tema.</span><span class="sxs-lookup"><span data-stu-id="d72cd-112">Topic</span></span> | <span data-ttu-id="d72cd-113">¿Qué aspectos cubre y cuándo debe leerlo?</span><span class="sxs-lookup"><span data-stu-id="d72cd-113">What it covers and when to read</span></span> |
| --- | --- |
| <span data-ttu-id="d72cd-114">**Fundamentos de la sincronización de Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="d72cd-114">**Azure AD Connect sync fundamentals**</span></span> | |
| [<span data-ttu-id="d72cd-115">Comprensión de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="d72cd-115">Understanding the architecture</span></span>](active-directory-aadconnectsync-understanding-architecture.md) |<span data-ttu-id="d72cd-116">Para quienes no estén familiarizados con el motor de sincronización y quieran obtener información sobre la arquitectura y los términos empleados.</span><span class="sxs-lookup"><span data-stu-id="d72cd-116">For those of you who are new to the sync engine and want to learn about the architecture and the terms used.</span></span> |
| [<span data-ttu-id="d72cd-117">Conceptos técnicos</span><span class="sxs-lookup"><span data-stu-id="d72cd-117">Technical concepts</span></span>](active-directory-aadconnectsync-technical-concepts.md) |<span data-ttu-id="d72cd-118">Una versión abreviada del tema de la arquitectura que explica brevemente los términos empleados.</span><span class="sxs-lookup"><span data-stu-id="d72cd-118">A short version of the architecture topic and briefly explains the terms used.</span></span> |
| [<span data-ttu-id="d72cd-119">Topologías de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d72cd-119">Topologies for Azure AD Connect</span></span>](active-directory-aadconnect-topologies.md) |<span data-ttu-id="d72cd-120">Describe las distintas topologías y escenarios que admite el motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="d72cd-120">Describes the different topologies and scenarios the sync engine supports.</span></span> |
| <span data-ttu-id="d72cd-121">**Configuración personalizada**</span><span class="sxs-lookup"><span data-stu-id="d72cd-121">**Custom configuration**</span></span> | |
| [<span data-ttu-id="d72cd-122">Sincronización de Azure AD Connect: ejecución por segunda vez del Asistente para la instalación</span><span class="sxs-lookup"><span data-stu-id="d72cd-122">Running the installation wizard again</span></span>](active-directory-aadconnectsync-installation-wizard.md) |<span data-ttu-id="d72cd-123">Explica qué opciones tiene disponibles si ejecuta de nuevo el Asistente para instalación de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d72cd-123">Explains what options you have available when you run the Azure AD Connect installation wizard again.</span></span> |
| [<span data-ttu-id="d72cd-124">Conocimiento del aprovisionamiento declarativo</span><span class="sxs-lookup"><span data-stu-id="d72cd-124">Understanding Declarative Provisioning</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |<span data-ttu-id="d72cd-125">Describe el modelo de configuración denominado aprovisionamiento declarativo.</span><span class="sxs-lookup"><span data-stu-id="d72cd-125">Describes the configuration model called declarative provisioning.</span></span> |
| [<span data-ttu-id="d72cd-126">Explicación de las expresiones declarativas de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="d72cd-126">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |<span data-ttu-id="d72cd-127">Describe la sintaxis para el lenguaje de expresiones que se usa en el aprovisionamiento declarativo.</span><span class="sxs-lookup"><span data-stu-id="d72cd-127">Describes the syntax for the expression language used in declarative provisioning.</span></span> |
| [<span data-ttu-id="d72cd-128">Introducción a la configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="d72cd-128">Understanding the default configuration</span></span>](active-directory-aadconnectsync-understanding-default-configuration.md) |<span data-ttu-id="d72cd-129">Describe las reglas no incluidas y la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d72cd-129">Describes the out-of-box rules and the default configuration.</span></span> <span data-ttu-id="d72cd-130">También describe cómo colaboran las reglas para que los escenarios no incluidos funcionen.</span><span class="sxs-lookup"><span data-stu-id="d72cd-130">Also describes how the rules work together for the out-of-box scenarios to work.</span></span> |
| [<span data-ttu-id="d72cd-131">Descripción de usuarios y contactos</span><span class="sxs-lookup"><span data-stu-id="d72cd-131">Understanding Users and Contacts</span></span>](active-directory-aadconnectsync-understanding-users-and-contacts.md) |<span data-ttu-id="d72cd-132">Continúa desde el tema anterior y describe cómo la configuración de los usuarios y contactos funciona conjuntamente, especialmente en un entorno de bosques múltiples.</span><span class="sxs-lookup"><span data-stu-id="d72cd-132">Continues on the previous topic and describes how the configuration for users and contacts works together, in particular in a multi-forest environment.</span></span> |
| [<span data-ttu-id="d72cd-133">How to make a change to the default configuration (Realización de un cambio en la configuración predeterminada)</span><span class="sxs-lookup"><span data-stu-id="d72cd-133">How to make a change to the default configuration</span></span>](active-directory-aadconnectsync-change-the-configuration.md) |<span data-ttu-id="d72cd-134">En él se explica cómo cambiar una configuración común para los flujos de atributo.</span><span class="sxs-lookup"><span data-stu-id="d72cd-134">Walks you through how to make a common configuration change to attribute flows.</span></span> |
| [<span data-ttu-id="d72cd-135">Prácticas recomendadas de cambio de la configuración predeterminada</span><span class="sxs-lookup"><span data-stu-id="d72cd-135">Best practices for changing the default configuration</span></span>](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |<span data-ttu-id="d72cd-136">En él se describen las limitaciones de compatibilidad y se proporcionan directrices para realizar cambios en la configuración de fábrica.</span><span class="sxs-lookup"><span data-stu-id="d72cd-136">Support limitations and for making changes to the out-of-box configuration.</span></span> |
| [<span data-ttu-id="d72cd-137">Configuración del filtrado</span><span class="sxs-lookup"><span data-stu-id="d72cd-137">Configure Filtering</span></span>](active-directory-aadconnectsync-configure-filtering.md) |<span data-ttu-id="d72cd-138">Describe las distintas opciones para limitar qué objetos se sincronizan con Azure AD y cómo configurar estas opciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="d72cd-138">Describes the different options for how to limit which objects are being synchronized to Azure AD and step-by-step how to configure these options.</span></span> |
| <span data-ttu-id="d72cd-139">**Características y escenarios**</span><span class="sxs-lookup"><span data-stu-id="d72cd-139">**Features and scenarios**</span></span> | |
| [<span data-ttu-id="d72cd-140">Evitar eliminaciones accidentales</span><span class="sxs-lookup"><span data-stu-id="d72cd-140">Prevent accidental deletes</span></span>](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |<span data-ttu-id="d72cd-141">En él se describe la característica para *evitar eliminaciones accidentales* y se explica cómo configurarla.</span><span class="sxs-lookup"><span data-stu-id="d72cd-141">Describes the *prevent accidental deletes* feature and how to configure it.</span></span> |
| [<span data-ttu-id="d72cd-142">Programador</span><span class="sxs-lookup"><span data-stu-id="d72cd-142">Scheduler</span></span>](active-directory-aadconnectsync-feature-scheduler.md) |<span data-ttu-id="d72cd-143">En él se describe el programador integrado que permite importar, sincronizar y exportar datos.</span><span class="sxs-lookup"><span data-stu-id="d72cd-143">Describes the built-in scheduler, which is importing, synchronizing, and exporting data.</span></span> |
| [<span data-ttu-id="d72cd-144">Implementación de la sincronización de contraseñas</span><span class="sxs-lookup"><span data-stu-id="d72cd-144">Implement password synchronization</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md) |<span data-ttu-id="d72cd-145">Describe cómo funciona la sincronización de contraseñas, cómo implementarla y cómo utilizarla y solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="d72cd-145">Describes how password synchronization works, how to implement, and how to operate and troubleshoot.</span></span> |
| [<span data-ttu-id="d72cd-146">Escritura diferida de dispositivos</span><span class="sxs-lookup"><span data-stu-id="d72cd-146">Device writeback</span></span>](active-directory-aadconnect-feature-device-writeback.md) |<span data-ttu-id="d72cd-147">Describe cómo funciona la reescritura de dispositivos en Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d72cd-147">Describes how device writeback works in Azure AD Connect.</span></span> |
| [<span data-ttu-id="d72cd-148">Extensiones de directorio</span><span class="sxs-lookup"><span data-stu-id="d72cd-148">Directory extensions</span></span>](active-directory-aadconnectsync-feature-directory-extensions.md) |<span data-ttu-id="d72cd-149">Describe cómo extender el esquema de Azure AD con sus propios atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="d72cd-149">Describes how to extend the Azure AD schema with your own custom attributes.</span></span> |
| <span data-ttu-id="d72cd-150">**Servicio de sincronización**</span><span class="sxs-lookup"><span data-stu-id="d72cd-150">**Sync Service**</span></span> | |
| [<span data-ttu-id="d72cd-151">Características del servicio de sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d72cd-151">Azure AD Connect sync service features</span></span>](active-directory-aadconnectsyncservice-features.md) |<span data-ttu-id="d72cd-152">Describe el lado del servicio de sincronización y cómo cambiar la configuración de sincronización de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d72cd-152">Describes the sync service side and how to change sync settings in Azure AD.</span></span> |
| [<span data-ttu-id="d72cd-153">Resistencia de atributos duplicados</span><span class="sxs-lookup"><span data-stu-id="d72cd-153">Duplicate attribute resiliency</span></span>](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |<span data-ttu-id="d72cd-154">En él se describe cómo habilitar y usar la resistencia de valores de atributos duplicados de **userPrincipalName** y **proxyAddresses**.</span><span class="sxs-lookup"><span data-stu-id="d72cd-154">Describes how to enable and use **userPrincipalName** and **proxyAddresses** duplicate attribute values resiliency.</span></span> |
| <span data-ttu-id="d72cd-155">**Operaciones e interfaz de usuario**</span><span class="sxs-lookup"><span data-stu-id="d72cd-155">**Operations and UI**</span></span> | |
| [<span data-ttu-id="d72cd-156">Synchronization Service Manager</span><span class="sxs-lookup"><span data-stu-id="d72cd-156">Synchronization Service Manager</span></span>](active-directory-aadconnectsync-service-manager-ui.md) |<span data-ttu-id="d72cd-157">En él se describe la interfaz de usuario de Synchronization Service Manager, incluidas las pestañas [Operations](active-directory-aadconnectsync-service-manager-ui-operations.md) (Operaciones), [Connectors](active-directory-aadconnectsync-service-manager-ui-connectors.md) (Conectores), [Metaverse Designer](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md) (Diseñador de metaverso) y [Metaverse Search](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) (Búsqueda de metaverso).</span><span class="sxs-lookup"><span data-stu-id="d72cd-157">Describes the Synchronization Service Manager UI, including [Operations](active-directory-aadconnectsync-service-manager-ui-operations.md), [Connectors](active-directory-aadconnectsync-service-manager-ui-connectors.md), [Metaverse Designer](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), and [Metaverse Search](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) tabs.</span></span> |
| [<span data-ttu-id="d72cd-158">Tareas y consideraciones operativas</span><span class="sxs-lookup"><span data-stu-id="d72cd-158">Operational tasks and considerations</span></span>](active-directory-aadconnectsync-operations.md) |<span data-ttu-id="d72cd-159">Describe las preocupaciones operativas, como la recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="d72cd-159">Describes operational concerns, such as disaster recovery.</span></span> |
| <span data-ttu-id="d72cd-160">**Procedimiento para:**</span><span class="sxs-lookup"><span data-stu-id="d72cd-160">**How To...**</span></span> | |
| [<span data-ttu-id="d72cd-161">Restablecer la cuenta de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d72cd-161">Reset the Azure AD account</span></span>](active-directory-aadconnectsync-howto-azureadaccount.md) |<span data-ttu-id="d72cd-162">Procedimiento para restablecer las credenciales de la cuenta de servicio usada para conectarse desde el servicio de sincronización de Azure AD Connect a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d72cd-162">How to reset the credentials of the service account used to connect from Azure AD Connect sync to Azure AD.</span></span> |
| <span data-ttu-id="d72cd-163">**Más información y referencias**</span><span class="sxs-lookup"><span data-stu-id="d72cd-163">**More information and references**</span></span> | |
| [<span data-ttu-id="d72cd-164">Puertos</span><span class="sxs-lookup"><span data-stu-id="d72cd-164">Ports</span></span>](active-directory-aadconnect-ports.md) |<span data-ttu-id="d72cd-165">Enumera los puertos que necesita abrir entre el motor de sincronización y los directorios locales y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d72cd-165">Lists which ports you need to open between the sync engine and your on-premises directories and Azure AD.</span></span> |
| [<span data-ttu-id="d72cd-166">Atributos sincronizados con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d72cd-166">Attributes synchronized to Azure Active Directory</span></span>](active-directory-aadconnectsync-attributes-synchronized.md) |<span data-ttu-id="d72cd-167">Enumera todos los atributos que se sincronizan entre los AD locales y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d72cd-167">Lists all attributes being synchronized between on-premises AD and Azure AD.</span></span> |
| [<span data-ttu-id="d72cd-168">Referencia de funciones</span><span class="sxs-lookup"><span data-stu-id="d72cd-168">Functions Reference</span></span>](active-directory-aadconnectsync-functions-reference.md) |<span data-ttu-id="d72cd-169">Enumera todas las funciones disponibles en el aprovisionamiento declarativo.</span><span class="sxs-lookup"><span data-stu-id="d72cd-169">Lists all functions available in declarative provisioning.</span></span> |

## <a name="additional-resources"></a><span data-ttu-id="d72cd-170">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d72cd-170">Additional Resources</span></span>
* [<span data-ttu-id="d72cd-171">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d72cd-171">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
