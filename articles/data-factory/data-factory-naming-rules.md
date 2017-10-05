---
title: Reglas para asignar nombres a entidades de Azure Data Factory | Microsoft Docs
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
ms.openlocfilehash: d447bbceb4ab344e011311eaf143b20f0a0400d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="3b0d2-103">Azure Data Factory: reglas de nomenclatura</span><span class="sxs-lookup"><span data-stu-id="3b0d2-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="3b0d2-104">La tabla siguiente proporciona las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-104">The following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="3b0d2-105">Nombre</span><span class="sxs-lookup"><span data-stu-id="3b0d2-105">Name</span></span> | <span data-ttu-id="3b0d2-106">Exclusividad del nombre</span><span class="sxs-lookup"><span data-stu-id="3b0d2-106">Name Uniqueness</span></span> | <span data-ttu-id="3b0d2-107">Comprobaciones de validación</span><span class="sxs-lookup"><span data-stu-id="3b0d2-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b0d2-108">Factoría de datos</span><span class="sxs-lookup"><span data-stu-id="3b0d2-108">Data Factory</span></span> |<span data-ttu-id="3b0d2-109">Único en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="3b0d2-110">Los nombres no distinguen mayúsculas de minúsculas, es decir, `MyDF` y `mydf` hacen referencia a la misma factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer to the same data factory.</span></span> |<ul><li><span data-ttu-id="3b0d2-111">Cada factoría de datos está asociada exactamente a una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-111">Each data factory is tied to exactly one Azure subscription.</span></span></li><li><span data-ttu-id="3b0d2-112">Los nombres de objeto deben comenzar por una letra o un número, y pueden contener solo letras, números y el carácter de guión (-).</span><span class="sxs-lookup"><span data-stu-id="3b0d2-112">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span></span></li><li><span data-ttu-id="3b0d2-113">Los caracteres de guión (-) debe estar inmediatamente precedidos y seguidos por una letra o un número.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="3b0d2-114">No se permiten guiones consecutivos en los nombres de contenedor.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="3b0d2-115">El nombre puede tener entre 3 y 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="3b0d2-116">Servicios, tablas o canalizaciones vinculados</span><span class="sxs-lookup"><span data-stu-id="3b0d2-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="3b0d2-117">Único en una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-117">Unique with in a data factory.</span></span> <span data-ttu-id="3b0d2-118">Los nombres no distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="3b0d2-119">Número máximo de caracteres incluido en un nombre de tabla: 260.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="3b0d2-120">Los nombres de objeto deben empezar con una letra, un número o un carácter de subrayado (_).</span><span class="sxs-lookup"><span data-stu-id="3b0d2-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="3b0d2-121">No se permiten los caracteres siguientes: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="3b0d2-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="3b0d2-122">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3b0d2-122">Resource Group</span></span> |<span data-ttu-id="3b0d2-123">Único en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="3b0d2-124">Los nombres no distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="3b0d2-125">Número máximo de caracteres: 1000.</span><span class="sxs-lookup"><span data-stu-id="3b0d2-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="3b0d2-126">El nombre puede contener letras, dígitos y los siguientes caracteres: “-”, “_”, “,” y “.”</span><span class="sxs-lookup"><span data-stu-id="3b0d2-126">Name can contain letters, digits, and the following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

