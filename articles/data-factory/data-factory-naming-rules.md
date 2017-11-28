---
title: "aaaRules para asignar nombres a las entidades de la factoría de datos de Azure | Documentos de Microsoft"
description: "Describe las reglas de nomenclatura para las entidades de Factoría de datos."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="a3d35-103">Azure Data Factory: reglas de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="a3d35-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="a3d35-104">Hello en la tabla siguiente proporciona las reglas de nomenclatura para los artefactos de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="a3d35-104">hello following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="a3d35-105">Nombre</span><span class="sxs-lookup"><span data-stu-id="a3d35-105">Name</span></span> | <span data-ttu-id="a3d35-106">Exclusividad del nombre</span><span class="sxs-lookup"><span data-stu-id="a3d35-106">Name Uniqueness</span></span> | <span data-ttu-id="a3d35-107">Comprobaciones de validación</span><span class="sxs-lookup"><span data-stu-id="a3d35-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a3d35-108">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="a3d35-108">Data Factory</span></span> |<span data-ttu-id="a3d35-109">Único en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d35-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="a3d35-110">Nombres distinguen mayúsculas de minúsculas, es decir, `MyDF` y `mydf` consulte toohello misma factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="a3d35-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer toohello same data factory.</span></span> |<ul><li><span data-ttu-id="a3d35-111">Cada factoría de datos es una suscripción a Azure tooexactly relacionados.</span><span class="sxs-lookup"><span data-stu-id="a3d35-111">Each data factory is tied tooexactly one Azure subscription.</span></span></li><li><span data-ttu-id="a3d35-112">Nombres de objeto deben comenzar con una letra o un número y pueden contener solo letras, números y caracteres de guión (-) Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d35-112">Object names must start with a letter or a number, and can contain only letters, numbers, and hello dash (-) character.</span></span></li><li><span data-ttu-id="a3d35-113">Los caracteres de guión (-) debe estar inmediatamente precedidos y seguidos por una letra o un número.</span><span class="sxs-lookup"><span data-stu-id="a3d35-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="a3d35-114">No se permiten guiones consecutivos en los nombres de contenedor.</span><span class="sxs-lookup"><span data-stu-id="a3d35-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="a3d35-115">El nombre puede tener entre 3 y 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a3d35-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="a3d35-116">Servicios, tablas o canalizaciones vinculados</span><span class="sxs-lookup"><span data-stu-id="a3d35-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="a3d35-117">Único en una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="a3d35-117">Unique with in a data factory.</span></span> <span data-ttu-id="a3d35-118">Los nombres no distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a3d35-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="a3d35-119">Número máximo de caracteres incluido en un nombre de tabla: 260.</span><span class="sxs-lookup"><span data-stu-id="a3d35-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="a3d35-120">Los nombres de objeto deben empezar con una letra, un número o un carácter de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="a3d35-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="a3d35-121">No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="a3d35-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="a3d35-122">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a3d35-122">Resource Group</span></span> |<span data-ttu-id="a3d35-123">Único en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d35-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="a3d35-124">Los nombres no distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a3d35-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="a3d35-125">Número máximo de caracteres: 1000.</span><span class="sxs-lookup"><span data-stu-id="a3d35-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="a3d35-126">Nombre puede contener letras, dígitos, hello y los caracteres siguientes: "-", "_",","y"."</span><span class="sxs-lookup"><span data-stu-id="a3d35-126">Name can contain letters, digits, and hello following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

