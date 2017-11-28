---
title: "Sincronización de Azure AD Connect: Extensiones de directorio | Microsoft Docs"
description: "En este tema se describe la característica de extensiones de directorio en Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="9ebe8-103">Sincronización de Azure AD Connect: Extensiones de directorio</span><span class="sxs-lookup"><span data-stu-id="9ebe8-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="9ebe8-104">Las extensiones de directorio le permiten ampliar el esquema de Azure AD con sus propios atributos desde Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="9ebe8-105">Esta característica permite crear aplicaciones de LOB mediante el consumo de atributos que se siguen administrando de forma local.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="9ebe8-106">Estos atributos se pueden consumir mediante [extensiones de directorio de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) o [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="9ebe8-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="9ebe8-107">Puede ver los atributos disponibles mediante el [explorador de Azure AD Graph](https://graphexplorer.cloudapp.net) y el [explorador de Microsoft Graph](https://graphexplorer2.azurewebsites.net/), respectivamente.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="9ebe8-108">En la actualidad, ninguna carga de trabajo de Office 365 consume estos atributos.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="9ebe8-109">Configure qué atributos adicionales desea sincronizar en la ruta de acceso de configuración personalizada en el Asistente para instalación.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="9ebe8-110">![Asistente para la extensión de esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="9ebe8-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="9ebe8-111">La instalación muestra los atributos siguientes, que son candidatos válidos:</span><span class="sxs-lookup"><span data-stu-id="9ebe8-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="9ebe8-112">Tipos de objetos de usuario y de grupo</span><span class="sxs-lookup"><span data-stu-id="9ebe8-112">User and Group object types</span></span>
* <span data-ttu-id="9ebe8-113">Atributos de valor único: cadena, booleano, entero y binario</span><span class="sxs-lookup"><span data-stu-id="9ebe8-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="9ebe8-114">Atributos multivalor: cadena y binario</span><span class="sxs-lookup"><span data-stu-id="9ebe8-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="9ebe8-115">La lista de atributos se lee de la memoria caché de esquema creada durante la instalación de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="9ebe8-116">Si ha ampliado el esquema de Active Directory con atributos adicionales, [se debe actualizar el esquema](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) para que los nuevos atributos estén visibles.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="9ebe8-117">Un objeto de Azure AD puede tener hasta 100 atributos de extensiones de directorio.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="9ebe8-118">La longitud máxima es de 250 caracteres.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-118">The max length is 250 characters.</span></span> <span data-ttu-id="9ebe8-119">Si un valor de atributo es mayor, el motor de sincronización lo trunca.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="9ebe8-120">Durante la instalación de Azure AD Connect, se registra una aplicación donde estos atributos estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="9ebe8-121">Puede ver esta aplicación en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-121">You can see this application in the Azure portal.</span></span>  
![Aplicación de extensión de esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="9ebe8-123">Estos atributos están ahora disponibles en Graph: </span><span class="sxs-lookup"><span data-stu-id="9ebe8-123">These attributes are now available through Graph:</span></span>  
![Gráfico](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="9ebe8-125">Los atributos tienen el prefijo extension \_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="9ebe8-126">El AppClientId tiene el mismo valor en todos los atributos del directorio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ebe8-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ebe8-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9ebe8-127">Next steps</span></span>
<span data-ttu-id="9ebe8-128">Obtenga más información sobre la configuración de la [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="9ebe8-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="9ebe8-129">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9ebe8-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
