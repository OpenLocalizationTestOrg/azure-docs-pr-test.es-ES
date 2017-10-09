---
title: aaaManage DNS registrar conjuntos y los registros con DNS de Azure | Documentos de Microsoft
description: DNS de Azure proporciona registro DNS de hello capacidad toomanage establece y registra al hospedar el dominio.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="9bcbf-103">Administrar registros DNS y los conjuntos de registros mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9bcbf-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bcbf-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9bcbf-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="9bcbf-105">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9bcbf-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="9bcbf-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9bcbf-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="9bcbf-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bcbf-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="9bcbf-108">Este artículo muestra cómo toomanage conjuntos de registros y los registros para la zona DNS mediante el uso de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="9bcbf-109">Es importante toounderstand Hola diferencia entre los conjuntos de registros de DNS y los registros DNS individuales.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="9bcbf-110">Un conjunto de registros es una colección de registros de una zona que tengan Hola mismo nombre y están Hola mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="9bcbf-111">Para obtener más información, consulte [Hola a conjuntos de registros de DNS de crear y registros mediante el portal de Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9bcbf-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="9bcbf-112">Creación de un nuevo conjunto de registros y un registro</span><span class="sxs-lookup"><span data-stu-id="9bcbf-112">Create a new record set and record</span></span>

<span data-ttu-id="9bcbf-113">toocreate un conjunto de registros de hello portal de Azure, consulte [Hola de registros DNS crear mediante el portal de Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9bcbf-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="9bcbf-114">Visualización de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="9bcbf-114">View a record set</span></span>

1. <span data-ttu-id="9bcbf-115">Hola portal de Azure, vaya toohello **zona DNS** hoja.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="9bcbf-116">Busque el conjunto de registros de Hola y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-116">Search for hello record set and select it.</span></span> <span data-ttu-id="9bcbf-117">Se abren propiedades de conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-117">This opens hello record set properties.</span></span>

    ![Buscar un conjunto de registros](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="9bcbf-119">Agregar un nuevo conjunto de registros de registros tooa</span><span class="sxs-lookup"><span data-stu-id="9bcbf-119">Add a new record tooa record set</span></span>

<span data-ttu-id="9bcbf-120">Puede agregar una conjunto de registros too20 registros tooany.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="9bcbf-121">Un conjunto de registros no puede contener dos registros idénticos.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="9bcbf-122">Conjuntos de registros vacíos (con cero registros) se pueden crear, pero no aparecen en los servidores de nombres DNS de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="9bcbf-123">Los conjuntos de registros de tipo CNAME pueden contener, como máximo, un registro.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="9bcbf-124">En hello **propiedades de conjunto de registros** hoja para la zona DNS, haga clic en el registro de hello establecer que desea tooadd un registro a.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![Seleccionar un conjunto de registros](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="9bcbf-126">Especificar propiedades de conjunto de registros de hello rellenando los campos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![Incorporación de un registro](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="9bcbf-128">Haga clic en **guardar** en Hola parte superior de hello hoja toosave su configuración.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="9bcbf-129">A continuación, cierre la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-129">Then close hello blade.</span></span>
4. <span data-ttu-id="9bcbf-130">En la esquina de hello, verá que está guardando el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-130">In hello corner, you will see that hello record is saving.</span></span>

    ![Guardar el conjunto de registros](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="9bcbf-132">Una vez guardado el registro de hello, Hola valores en hello **zona DNS** hoja reflejará el nuevo registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="9bcbf-133">Actualización de un registro</span><span class="sxs-lookup"><span data-stu-id="9bcbf-133">Update a record</span></span>

<span data-ttu-id="9bcbf-134">Cuando se actualiza un registro en un conjunto de registros existente, campos de hello que puede actualizar dependen de tipo de Hola de registro que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="9bcbf-135">En hello **propiedades de conjunto de registros** hoja para el conjunto de registros, busque el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="9bcbf-136">Modifique el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-136">Modify hello record.</span></span> <span data-ttu-id="9bcbf-137">Cuando se modifica un registro, puede cambiar opciones de configuración disponibles de hello para el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="9bcbf-138">En el siguiente ejemplo de Hola Hola **dirección IP** campo está seleccionado, y dirección IP de hello está en proceso de Hola de que se está modificando.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![Modificar un registro](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="9bcbf-140">Haga clic en **guardar** en Hola parte superior de hello hoja toosave su configuración.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="9bcbf-141">En hello esquina superior derecha, verá una notificación de Hola que se ha guardado el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![Agregar conjunto de registros](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="9bcbf-143">Una vez guardado el registro de hello, los valores de hello para el registro de hello establecidos en hello **zona DNS** hoja reflejará el registro de hello actualizado.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="9bcbf-144">Eliminación de un registro de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="9bcbf-144">Remove a record from a record set</span></span>

<span data-ttu-id="9bcbf-145">Puede usar registros de hello Azure tooremove portal desde un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="9bcbf-146">Tenga en cuenta que al quitar el último registro de hello desde un conjunto de registros, no se eliminan conjunto de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="9bcbf-147">En hello **propiedades de conjunto de registros** hoja para el conjunto de registros, busque el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="9bcbf-148">Haga clic en registro de hello que desea tooremove.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="9bcbf-149">A continuación, seleccione **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-149">Then select **Remove**.</span></span>

    ![Quitar un registro](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="9bcbf-151">Haga clic en **guardar** en Hola parte superior de hello hoja toosave su configuración.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="9bcbf-152">Después de quitar el registro de hello, Hola valores de registro de hello en hello **zona DNS** hoja reflejará la eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="9bcbf-153"><a name="delete"></a>Eliminación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="9bcbf-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="9bcbf-154">En hello **propiedades de conjunto de registros** hoja para el conjunto de registros, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Eliminación de un conjunto de registros](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="9bcbf-156">Aparecerá un mensaje preguntando si desea que el conjunto de registros toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="9bcbf-157">Compruebe que el registro de hello de coincidencias de nombres Hola establecido que desee toodelete y, a continuación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="9bcbf-158">En hello **zona DNS** hoja, compruebe que el conjunto de registros de hello ya no está visible.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="9bcbf-159">Trabajo con registros NS y SOA</span><span class="sxs-lookup"><span data-stu-id="9bcbf-159">Work with NS and SOA records</span></span>

<span data-ttu-id="9bcbf-160">Los registros NS y SOA creados automáticamente se administran de forma diferente de otros tipos de registros.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="9bcbf-161">Modificación de registros SOA</span><span class="sxs-lookup"><span data-stu-id="9bcbf-161">Modify SOA records</span></span>

<span data-ttu-id="9bcbf-162">No se puede agregar o quitar registros de hello creado automáticamente el registro SOA establecido en vértice de la zona de hello (nombre = "@").</span><span class="sxs-lookup"><span data-stu-id="9bcbf-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="9bcbf-163">Sin embargo, puede modificar cualquiera de los parámetros de hello en hello registro SOA (excepto el "Host") y registro de hello establecer TTL.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="9bcbf-164">Modificar los registros NS en vértice de la zona de Hola</span><span class="sxs-lookup"><span data-stu-id="9bcbf-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="9bcbf-165">registro de NS de Hello establecido en vértice de la zona de Hola se crea automáticamente con cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="9bcbf-166">Contiene los nombres de Hola de zona de hello Azure DNS nombre servidores toohello asignado.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="9bcbf-167">Puede agregar nombre adicionales servidores toothis NS conjunto de registros, toosupport alojar conjuntamente dominios con más de un proveedor DNS.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="9bcbf-168">También puede modificar Hola TTL y los metadatos para este conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="9bcbf-169">Sin embargo, no se puede quitar o modificar servidores de nombres DNS de Azure previamente rellenados Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="9bcbf-170">Tenga en cuenta que esto se aplica solo toohello NS conjunto de registros en vértice de la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="9bcbf-171">Otros conjuntos de registros NS en su zona (como las zonas secundarias de toodelegate usado) pueden modificarse sin restricción.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="9bcbf-172">Eliminación de conjuntos de registros SOA o NS</span><span class="sxs-lookup"><span data-stu-id="9bcbf-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="9bcbf-173">No se puede eliminar Hola SOA y NS conjuntos de registros en vértice de la zona de hello (nombre = "@") que se crean automáticamente cuando se crea la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="9bcbf-174">Se eliminan automáticamente cuando se elimina la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="9bcbf-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bcbf-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9bcbf-175">Next steps</span></span>

* <span data-ttu-id="9bcbf-176">Para obtener más información acerca de DNS de Azure, vea hello [Introducción a DNS de Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bcbf-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="9bcbf-177">Para obtener más información acerca de la automatización de DNS, consulte [zonas DNS de creación y conjuntos de registros mediante Hola .NET SDK](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="9bcbf-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="9bcbf-178">Para más información acerca de los registros de DNS inversos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bcbf-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
