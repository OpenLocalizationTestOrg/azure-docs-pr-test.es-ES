---
ms.assetid: 
title: Espacios de seguridad de Azure Key Vault | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 921bbd109c9ea98d8b5c286a7512bed026412d26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="c569f-102">Espacios de seguridad y límites geográficos de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c569f-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="c569f-103">Azure Key Vault es un servicio multiinquilino y usa un grupo de módulos de seguridad de hardware (HSM) en cada ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="c569f-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="c569f-104">Todos los HSM en ubicaciones de Azure de la misma región geográfica comparten el mismo límite criptográfico (Thales Security World).</span><span class="sxs-lookup"><span data-stu-id="c569f-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="c569f-105">Por ejemplo, las regiones de este de EE. UU. y oeste de EE. UU. comparten en mismo espacio de seguridad porque pertenecen a la ubicación geográfica de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="c569f-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="c569f-106">Del mismo modo, todas las ubicaciones de Azure en Japón comparten el mismo entorno de seguridad, así como todas las ubicaciones de Azure en Australia, India, etc.</span><span class="sxs-lookup"><span data-stu-id="c569f-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="c569f-107">Tareas de copia de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="c569f-107">Backup and restore behavior</span></span>

<span data-ttu-id="c569f-108">Una copia de seguridad tomada de una clave en una instancia de Key Vault de una ubicación de Azure puede restaurarse en una instancia de Key Vault de otra ubicación de Azure, siempre que se den estas dos condiciones:</span><span class="sxs-lookup"><span data-stu-id="c569f-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="c569f-109">Las dos ubicaciones de Azure pertenecen a la misma ubicación geográfica</span><span class="sxs-lookup"><span data-stu-id="c569f-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="c569f-110">Las dos instancias de Key Vault pertenecen a la misma suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="c569f-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="c569f-111">Por ejemplo, una copia de seguridad tomada por una suscripción determinada de una clave en una instancia de Key Vault de oeste de la Indica solo se puede restaurar en otra instancia de Key Vault de la misma suscripción y ubicación geográfica: oeste de la India, centro de la India o India del Sur.</span><span class="sxs-lookup"><span data-stu-id="c569f-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="c569f-112">Productos y regiones</span><span class="sxs-lookup"><span data-stu-id="c569f-112">Regions and products</span></span>

- [<span data-ttu-id="c569f-113">Regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="c569f-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="c569f-114">Productos de Microsoft por región</span><span class="sxs-lookup"><span data-stu-id="c569f-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="c569f-115">Las regiones se asignan a los ámbitos de seguridad, que se muestran como encabezados principales en las tablas:</span><span class="sxs-lookup"><span data-stu-id="c569f-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="c569f-116">En el artículo de productos por región, por ejemplo, la pestaña **América** contiene Este de EE. UU. , Centro de EE. UU. y Oeste de EE. UU. y todo ello se asigna a la región América.</span><span class="sxs-lookup"><span data-stu-id="c569f-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="c569f-117">Una excepción es que el Departamento de Defensa del este y del centro de Estados Unidos tienen sus propios ámbitos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c569f-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="c569f-118">De igual forma, en la pestaña **Europa**, tanto Europa del Norte como Europa occidental se asignan a la región de Europa.</span><span class="sxs-lookup"><span data-stu-id="c569f-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="c569f-119">Lo mismo sirve también para la pestaña **Asia-Pacífico**.</span><span class="sxs-lookup"><span data-stu-id="c569f-119">The same is also true on the **Asia Pacific** tab.</span></span>



