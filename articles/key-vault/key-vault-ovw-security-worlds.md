---
ms.assetid: 
title: "espacios de seguridad del almacén de claves de aaaAzure | Documentos de Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="0647f-102">Espacios de seguridad y límites geográficos de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="0647f-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="0647f-103">Azure Key Vault es un servicio multiinquilino y usa un grupo de módulos de seguridad de hardware (HSM) en cada ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="0647f-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="0647f-104">Todos los HSM en Azure ubicaciones de hello mismo recurso compartido de la región geográfica Hola mismo límite criptográfico (mundo de seguridad de Thales).</span><span class="sxs-lookup"><span data-stu-id="0647f-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="0647f-105">Por ejemplo, UU y oeste de EE. UU. compartir Hola a todos de seguridad mismo porque pertenecen ubicación geográfica de toohello Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="0647f-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="0647f-106">De forma similar, todas las ubicaciones de Azure en el recurso compartido de Japón Hola mundo de la misma seguridad y todas las ubicaciones de Azure en Australia, India y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="0647f-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="0647f-107">Tareas de copia de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="0647f-107">Backup and restore behavior</span></span>

<span data-ttu-id="0647f-108">Una copia de seguridad de una clave de un almacén de claves en una ubicación de Azure se pueden restaura tooa en otra ubicación de Azure, el almacén de claves, siempre que ambas condiciones son verdaderas:</span><span class="sxs-lookup"><span data-stu-id="0647f-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="0647f-109">Ambos hello Azure ubicaciones pertenecen toohello misma ubicación geográfica</span><span class="sxs-lookup"><span data-stu-id="0647f-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="0647f-110">Ambos almacenes de claves de hello pertenecen toohello misma suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="0647f-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="0647f-111">Por ejemplo, una copia de seguridad realizada por una suscripción determinada de una clave en un almacén de claves de la India occidental, solo puede ser restaurada tooanother el almacén de claves en hello misma suscripción y ubicación geográfica; India occidental, India Central o India sur.</span><span class="sxs-lookup"><span data-stu-id="0647f-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="0647f-112">Productos y regiones</span><span class="sxs-lookup"><span data-stu-id="0647f-112">Regions and products</span></span>

- [<span data-ttu-id="0647f-113">Regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="0647f-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="0647f-114">Productos de Microsoft por región</span><span class="sxs-lookup"><span data-stu-id="0647f-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="0647f-115">Las regiones son mundos toosecurity asignado, se muestra como encabezados principales en tablas de hello:</span><span class="sxs-lookup"><span data-stu-id="0647f-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="0647f-116">En los productos de hello en el artículo de la región, por ejemplo, hello **Americas** ficha contiene este US, CENTRAL EE. UU., oeste de Estados Unidos todos los asignación toohello Americas región.</span><span class="sxs-lookup"><span data-stu-id="0647f-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="0647f-117">Una excepción es que el Departamento de Defensa del este y del centro de Estados Unidos tienen sus propios ámbitos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0647f-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="0647f-118">De forma similar, en hello **Europa** ficha, Europa del Norte y Europa occidental asignan toohello región de Europa.</span><span class="sxs-lookup"><span data-stu-id="0647f-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="0647f-119">Hello mismo también es cierto en hello **Asia-Pacífico** ficha.</span><span class="sxs-lookup"><span data-stu-id="0647f-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



