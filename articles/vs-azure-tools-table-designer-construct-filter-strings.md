---
title: "aaaConstructing cadenas de filtro para el Diseñador de tablas de hello | Documentos de Microsoft"
description: "Crear cadenas de filtro para el Diseñador de tablas de Hola"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="f355c-103">Crear cadenas de filtro para hello Diseñador de tablas</span><span class="sxs-lookup"><span data-stu-id="f355c-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="f355c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f355c-104">Overview</span></span>
<span data-ttu-id="f355c-105">Hola a toofilter datos en una tabla de Azure que se muestra en Visual Studio **Diseñador de tablas**, construir una cadena de filtro y escríbala en el campo de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="f355c-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="f355c-106">sintaxis de cadena de filtro de Hola Hola WCF Data Services define y es similar tooa cláusula WHERE de SQL, pero se envían toohello servicio tabla a través de una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="f355c-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="f355c-107">Hola **Diseñador de tablas** identificadores Hola la codificación adecuada para usted, por lo que toofilter en un valor de propiedad, sólo necesita escribir el nombre de propiedad hello, operador de comparación, el valor de criterios, y si lo desea, filtre operador booleano en hello campo.</span><span class="sxs-lookup"><span data-stu-id="f355c-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="f355c-108">No es necesario tooinclude opción de consulta de hello $filter como si estuviese creando una tabla de hello tooquery de dirección URL a través de hello [referencia de API de REST de servicios de almacenamiento](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="f355c-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="f355c-109">Hola WCF Data Services se basan en hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="f355c-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="f355c-110">Para obtener más información sobre la opción de consulta de sistema de hello filter (**$filter**), vea hello [especificación OData URI Conventions](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="f355c-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="f355c-111">Operadores de comparación</span><span class="sxs-lookup"><span data-stu-id="f355c-111">Comparison Operators</span></span>
<span data-ttu-id="f355c-112">Hola se admiten los operadores lógicos siguientes para todos los tipos de propiedad:</span><span class="sxs-lookup"><span data-stu-id="f355c-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="f355c-113">Operador lógico</span><span class="sxs-lookup"><span data-stu-id="f355c-113">Logical operator</span></span> | <span data-ttu-id="f355c-114">Description</span><span class="sxs-lookup"><span data-stu-id="f355c-114">Description</span></span> | <span data-ttu-id="f355c-115">Ejemplo de cadena de filtro</span><span class="sxs-lookup"><span data-stu-id="f355c-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f355c-116">eq</span><span class="sxs-lookup"><span data-stu-id="f355c-116">eq</span></span> |<span data-ttu-id="f355c-117">Igual</span><span class="sxs-lookup"><span data-stu-id="f355c-117">Equal</span></span> |<span data-ttu-id="f355c-118">Ciudad eq "Redmond"</span><span class="sxs-lookup"><span data-stu-id="f355c-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="f355c-119">gt</span><span class="sxs-lookup"><span data-stu-id="f355c-119">gt</span></span> |<span data-ttu-id="f355c-120">Mayor que</span><span class="sxs-lookup"><span data-stu-id="f355c-120">Greater than</span></span> |<span data-ttu-id="f355c-121">Precio gt 20</span><span class="sxs-lookup"><span data-stu-id="f355c-121">Price gt 20</span></span> |
| <span data-ttu-id="f355c-122">ge</span><span class="sxs-lookup"><span data-stu-id="f355c-122">ge</span></span> |<span data-ttu-id="f355c-123">Mayor o igual demasiado</span><span class="sxs-lookup"><span data-stu-id="f355c-123">Greater than or equal too</span></span>|<span data-ttu-id="f355c-124">Precio ge 10</span><span class="sxs-lookup"><span data-stu-id="f355c-124">Price ge 10</span></span> |
| <span data-ttu-id="f355c-125">lt</span><span class="sxs-lookup"><span data-stu-id="f355c-125">lt</span></span> |<span data-ttu-id="f355c-126">Menor que</span><span class="sxs-lookup"><span data-stu-id="f355c-126">Less than</span></span> |<span data-ttu-id="f355c-127">Precio lt 20</span><span class="sxs-lookup"><span data-stu-id="f355c-127">Price lt 20</span></span> |
| <span data-ttu-id="f355c-128">le</span><span class="sxs-lookup"><span data-stu-id="f355c-128">le</span></span> |<span data-ttu-id="f355c-129">Menor o igual que</span><span class="sxs-lookup"><span data-stu-id="f355c-129">Less than or equal</span></span> |<span data-ttu-id="f355c-130">Precio le 100</span><span class="sxs-lookup"><span data-stu-id="f355c-130">Price le 100</span></span> |
| <span data-ttu-id="f355c-131">ne</span><span class="sxs-lookup"><span data-stu-id="f355c-131">ne</span></span> |<span data-ttu-id="f355c-132">No igual</span><span class="sxs-lookup"><span data-stu-id="f355c-132">Not equal</span></span> |<span data-ttu-id="f355c-133">Ciudad ne 'Londres'</span><span class="sxs-lookup"><span data-stu-id="f355c-133">City ne 'London'</span></span> |
| <span data-ttu-id="f355c-134">y</span><span class="sxs-lookup"><span data-stu-id="f355c-134">and</span></span> |<span data-ttu-id="f355c-135">y</span><span class="sxs-lookup"><span data-stu-id="f355c-135">And</span></span> |<span data-ttu-id="f355c-136">Precio le 200 and Precio gt 3,5</span><span class="sxs-lookup"><span data-stu-id="f355c-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="f355c-137">o</span><span class="sxs-lookup"><span data-stu-id="f355c-137">or</span></span> |<span data-ttu-id="f355c-138">o</span><span class="sxs-lookup"><span data-stu-id="f355c-138">Or</span></span> |<span data-ttu-id="f355c-139">Precio 3,5 or Precio gt 200</span><span class="sxs-lookup"><span data-stu-id="f355c-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="f355c-140">not</span><span class="sxs-lookup"><span data-stu-id="f355c-140">not</span></span> |<span data-ttu-id="f355c-141">not</span><span class="sxs-lookup"><span data-stu-id="f355c-141">Not</span></span> |<span data-ttu-id="f355c-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="f355c-142">not isAvailable</span></span> |

<span data-ttu-id="f355c-143">Al construir una cadena de filtro, hello las reglas siguientes son importantes:</span><span class="sxs-lookup"><span data-stu-id="f355c-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="f355c-144">Usar operadores lógicos de hello toocompare un valor de propiedad tooa.</span><span class="sxs-lookup"><span data-stu-id="f355c-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="f355c-145">Tenga en cuenta que no es posible toocompare un valor dinámico de propiedad tooa; un lado de la expresión de hello debe ser una constante.</span><span class="sxs-lookup"><span data-stu-id="f355c-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="f355c-146">Todas las partes de la cadena de filtro de hello distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f355c-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="f355c-147">valor constante de Hello debe ser de hello como propiedad Hola para resultados válidos de hello filtro tooreturn de tipo de datos mismas.</span><span class="sxs-lookup"><span data-stu-id="f355c-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="f355c-148">Para obtener más información acerca de los tipos de propiedad admitidos, consulte [Hola de entender el modelo de datos del servicio de tabla](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="f355c-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="f355c-149">Filtro por propiedades de cadena</span><span class="sxs-lookup"><span data-stu-id="f355c-149">Filtering on String Properties</span></span>
<span data-ttu-id="f355c-150">Cuando se filtra según las propiedades de cadena, encierre constante de cadena de hello en comillas simples.</span><span class="sxs-lookup"><span data-stu-id="f355c-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="f355c-151">Hola siguiente filtros de ejemplo de Hola **PartitionKey** y **RowKey** propiedades; adicional que no son de clave propiedades también podrían agregarse toohello la cadena de filtro:</span><span class="sxs-lookup"><span data-stu-id="f355c-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="f355c-152">Las expresiones de filtro se pueden escribir entre paréntesis, aunque no es obligatorio:</span><span class="sxs-lookup"><span data-stu-id="f355c-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="f355c-153">Tenga en cuenta que Hola servicio tabla no admite consultas con caracteres comodín y no se admiten en el Diseñador de tablas de Hola o.</span><span class="sxs-lookup"><span data-stu-id="f355c-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="f355c-154">Sin embargo, puede realizar mediante el uso de operadores de comparación en el prefijo que desees Hola de coincidencia de prefijos.</span><span class="sxs-lookup"><span data-stu-id="f355c-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="f355c-155">Hello en el ejemplo siguiente se devuelve entidades que tienen una propiedad LastName empieza con la letra "A" de hello:</span><span class="sxs-lookup"><span data-stu-id="f355c-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="f355c-156">Filtro por propiedades numéricas</span><span class="sxs-lookup"><span data-stu-id="f355c-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="f355c-157">toofilter en un entero o un número de punto flotante, especifique número Hola sin comillas.</span><span class="sxs-lookup"><span data-stu-id="f355c-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="f355c-158">Este ejemplo devuelve todas las entidades con una propiedad Age cuyo valor es mayor que 30:</span><span class="sxs-lookup"><span data-stu-id="f355c-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="f355c-159">Este ejemplo devuelve todas las entidades con una propiedad AmountDue cuyo valor es menor que o igual a too100.25:</span><span class="sxs-lookup"><span data-stu-id="f355c-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="f355c-160">Filtro por propiedades booleanas</span><span class="sxs-lookup"><span data-stu-id="f355c-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="f355c-161">toofilter en un valor booleano, especifique **true** o **false** sin comillas.</span><span class="sxs-lookup"><span data-stu-id="f355c-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="f355c-162">Hello en el ejemplo siguiente se devuelve todas las entidades donde IsActive propiedad Hola se establece demasiado**true**:</span><span class="sxs-lookup"><span data-stu-id="f355c-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="f355c-163">También puede escribir esta expresión de filtro sin el operador lógico Hola.</span><span class="sxs-lookup"><span data-stu-id="f355c-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="f355c-164">En el siguiente ejemplo de Hola Hola servicio tabla también devolverá todas las entidades donde IsActive sea **true**:</span><span class="sxs-lookup"><span data-stu-id="f355c-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="f355c-165">tooreturn todas las entidades donde IsActive sea false, puede usar Hola no operador:</span><span class="sxs-lookup"><span data-stu-id="f355c-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="f355c-166">Filtro por propiedades de fecha y hora</span><span class="sxs-lookup"><span data-stu-id="f355c-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="f355c-167">toofilter en un valor de fecha y hora, especifique hello **datetime** (palabra clave), seguida de hello constante de fecha y hora entre comillas simples.</span><span class="sxs-lookup"><span data-stu-id="f355c-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="f355c-168">constante de fecha y hora de Hello debe estar en formato UTC combinado, tal y como se describe en [dar formato a valores de propiedad de fecha y hora](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="f355c-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="f355c-169">Hola siguiente ejemplo devuelve las entidades donde hello cuya propiedad CustomerSince es igual tooJuly 10, 2008:</span><span class="sxs-lookup"><span data-stu-id="f355c-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
