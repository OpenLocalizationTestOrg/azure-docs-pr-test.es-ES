---
title: "Administración del conjunto de registros de DNS y registros con Azure DNS | Microsoft Docs"
description: Azure DNS proporciona la funcionalidad de administrar registros y conjuntos de registros de DNS al hospedar un dominio.
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
ms.openlocfilehash: 001b80ccba43beab44f6a598f820df65a85a345f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="13af8-103">Administración de registros y conjuntos de registros DNS mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="13af8-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="13af8-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="13af8-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="13af8-105">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="13af8-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="13af8-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="13af8-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="13af8-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13af8-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="13af8-108">En este artículo se explica cómo administrar conjuntos de registros y registros para la zona DNS mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="13af8-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="13af8-109">Es importante comprender la diferencia entre los conjuntos de registros de DNS y los registros DNS individuales.</span><span class="sxs-lookup"><span data-stu-id="13af8-109">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="13af8-110">Un conjunto de registros es una colección de registros de una zona con el mismo nombre y el mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="13af8-110">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="13af8-111">Para más información, consulte [Creación de registros y conjuntos de registros de DNS mediante el Portal de Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="13af8-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="13af8-112">Creación de un nuevo conjunto de registros y un registro</span><span class="sxs-lookup"><span data-stu-id="13af8-112">Create a new record set and record</span></span>

<span data-ttu-id="13af8-113">Para crear un conjunto de registros en el Portal de Azure, consulte [Creación de registros y conjuntos de registros de DNS mediante el Portal de Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="13af8-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="13af8-114">Visualización de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="13af8-114">View a record set</span></span>

1. <span data-ttu-id="13af8-115">En el Portal de Azure, vaya a la hoja **Zona DNS** .</span><span class="sxs-lookup"><span data-stu-id="13af8-115">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="13af8-116">Busque el conjunto de registros y selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="13af8-116">Search for the record set and select it.</span></span> <span data-ttu-id="13af8-117">De este modo se abrirán las propiedades del conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="13af8-117">This opens the record set properties.</span></span>

    ![Buscar un conjunto de registros](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="13af8-119">Incorporación de un nuevo registro a un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="13af8-119">Add a new record to a record set</span></span>

<span data-ttu-id="13af8-120">Puede agregar hasta 20 registros a cualquier conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="13af8-120">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="13af8-121">Un conjunto de registros no puede contener dos registros idénticos.</span><span class="sxs-lookup"><span data-stu-id="13af8-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="13af8-122">Se pueden crear conjuntos de registros vacíos (sin ningún registro), pero no aparecen en los servidores de nombres DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="13af8-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="13af8-123">Los conjuntos de registros de tipo CNAME pueden contener, como máximo, un registro.</span><span class="sxs-lookup"><span data-stu-id="13af8-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="13af8-124">En la hoja **Record set properties** (Propiedades del conjunto de registros) de la zona DNS, haga clic en el conjunto de registros al que desea agregar un registro.</span><span class="sxs-lookup"><span data-stu-id="13af8-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![Seleccionar un conjunto de registros](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="13af8-126">Especifique las propiedades del conjunto de registros rellenando los campos.</span><span class="sxs-lookup"><span data-stu-id="13af8-126">Specify the record set properties by filling in the fields.</span></span>

    ![Incorporación de un registro](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="13af8-128">Haga clic en **Guardar** en la parte superior de la hoja para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="13af8-128">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="13af8-129">A continuación, cierre la hoja.</span><span class="sxs-lookup"><span data-stu-id="13af8-129">Then close the blade.</span></span>
4. <span data-ttu-id="13af8-130">En la esquina, verá que el registro se está guardando.</span><span class="sxs-lookup"><span data-stu-id="13af8-130">In the corner, you will see that the record is saving.</span></span>

    ![Guardar el conjunto de registros](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="13af8-132">Una vez que se ha guardado el registro, los valores de la hoja **Zona DNS** reflejarán el nuevo registro.</span><span class="sxs-lookup"><span data-stu-id="13af8-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="13af8-133">Actualización de un registro</span><span class="sxs-lookup"><span data-stu-id="13af8-133">Update a record</span></span>

<span data-ttu-id="13af8-134">Cuando se actualiza un registro en un conjunto de registros existente, los campos que puede actualizar dependen del tipo de registro con el que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="13af8-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="13af8-135">En la hoja **Record set properties** (Propiedades del conjunto de registros) correspondiente al conjunto de registros, busque el registro.</span><span class="sxs-lookup"><span data-stu-id="13af8-135">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="13af8-136">Modifique el registro.</span><span class="sxs-lookup"><span data-stu-id="13af8-136">Modify the record.</span></span> <span data-ttu-id="13af8-137">Cuando se modifica un registro, puede cambiar la configuración disponible para dicho registro.</span><span class="sxs-lookup"><span data-stu-id="13af8-137">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="13af8-138">En el ejemplo siguiente, se hizo clic en el campo **Dirección IP** y la dirección IP se encuentra en proceso de modificación.</span><span class="sxs-lookup"><span data-stu-id="13af8-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![Modificar un registro](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="13af8-140">Haga clic en **Guardar** en la parte superior de la hoja para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="13af8-140">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="13af8-141">En la esquina superior derecha verá la notificación de que el registro se ha guardado.</span><span class="sxs-lookup"><span data-stu-id="13af8-141">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![Agregar conjunto de registros](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="13af8-143">Una vez que se ha guardado el registro, los valores del conjunto de registros de la **Hoja DNS** reflejarán el registro actualizado.</span><span class="sxs-lookup"><span data-stu-id="13af8-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="13af8-144">Eliminación de un registro de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="13af8-144">Remove a record from a record set</span></span>

<span data-ttu-id="13af8-145">Puede usar el Portal de Azure para quitar registros de un conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="13af8-145">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="13af8-146">Tenga en cuenta que al eliminar el último registro de un conjunto de registros no se elimina el conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="13af8-146">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="13af8-147">En la hoja **Record set properties** (Propiedades del conjunto de registros) correspondiente al conjunto de registros, busque el registro.</span><span class="sxs-lookup"><span data-stu-id="13af8-147">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="13af8-148">Haga clic en el registro que desea quitar.</span><span class="sxs-lookup"><span data-stu-id="13af8-148">Click the record that you want to remove.</span></span> <span data-ttu-id="13af8-149">A continuación, seleccione **Quitar**.</span><span class="sxs-lookup"><span data-stu-id="13af8-149">Then select **Remove**.</span></span>

    ![Quitar un registro](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="13af8-151">Haga clic en **Guardar** en la parte superior de la hoja para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="13af8-151">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="13af8-152">Una vez quitado el registro, los valores del registro de la hoja **Zona DNS** reflejarán la eliminación.</span><span class="sxs-lookup"><span data-stu-id="13af8-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <span data-ttu-id="13af8-153"><a name="delete"></a>Eliminación de un conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="13af8-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="13af8-154">En la hoja **Record set properties** (Propiedades del conjunto de registros) correspondiente al conjunto de registros, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="13af8-154">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Eliminación de un conjunto de registros](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="13af8-156">Aparece un mensaje en el que se pregunta si desea eliminar el conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="13af8-156">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="13af8-157">Compruebe que el nombre coincide con el conjunto de registros que desea eliminar y después haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="13af8-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="13af8-158">En la hoja de **Zona DNS** , compruebe que el conjunto de registros ya no está visible.</span><span class="sxs-lookup"><span data-stu-id="13af8-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="13af8-159">Trabajo con registros NS y SOA</span><span class="sxs-lookup"><span data-stu-id="13af8-159">Work with NS and SOA records</span></span>

<span data-ttu-id="13af8-160">Los registros NS y SOA creados automáticamente se administran de forma diferente de otros tipos de registros.</span><span class="sxs-lookup"><span data-stu-id="13af8-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="13af8-161">Modificación de registros SOA</span><span class="sxs-lookup"><span data-stu-id="13af8-161">Modify SOA records</span></span>

<span data-ttu-id="13af8-162">No puede agregar ni eliminar registros del conjunto de registros SOA creado automáticamente en el vértice de zona (nombre = "@").</span><span class="sxs-lookup"><span data-stu-id="13af8-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span></span> <span data-ttu-id="13af8-163">Sin embargo, puede modificar cualquiera de los parámetros del registro SOA (excepto "Host") y del conjunto de registros TTL.</span><span class="sxs-lookup"><span data-stu-id="13af8-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="13af8-164">Modificación de los registros NS en el vértice de zona</span><span class="sxs-lookup"><span data-stu-id="13af8-164">Modify NS records at the zone apex</span></span>

<span data-ttu-id="13af8-165">El conjunto de registros NS en el vértice de zona se crea automáticamente con cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="13af8-165">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="13af8-166">Este conjunto de registros contiene los nombres de los servidores de nombres de Azure DNS asignados a la zona.</span><span class="sxs-lookup"><span data-stu-id="13af8-166">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="13af8-167">Puede agregar más servidores de nombres a este conjunto de registros NS, para admitir dominios de hospedaje conjunto con más de un proveedor DNS.</span><span class="sxs-lookup"><span data-stu-id="13af8-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="13af8-168">También puede modificar el TTL y los metadatos de este conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="13af8-168">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="13af8-169">Sin embargo, no puede quitar ni modificar los servidores de nombres de Azure DNS rellenados previamente.</span><span class="sxs-lookup"><span data-stu-id="13af8-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="13af8-170">Tenga en cuenta que esto solo se aplica al conjunto de registros NS en el vértice de zona.</span><span class="sxs-lookup"><span data-stu-id="13af8-170">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="13af8-171">Otros conjuntos de registros NS de su zona (como los que se usan para delegar zonas secundarias) se pueden modificar sin restricciones.</span><span class="sxs-lookup"><span data-stu-id="13af8-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="13af8-172">Eliminación de conjuntos de registros SOA o NS</span><span class="sxs-lookup"><span data-stu-id="13af8-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="13af8-173">No puede eliminar conjuntos de registros SOA ni NS en el vértice de zona (nombre = @) que se crean automáticamente cuando se crea la zona.</span><span class="sxs-lookup"><span data-stu-id="13af8-173">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="13af8-174">Se eliminan automáticamente al eliminar la zona.</span><span class="sxs-lookup"><span data-stu-id="13af8-174">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13af8-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13af8-175">Next steps</span></span>

* <span data-ttu-id="13af8-176">Para más información acerca de DNS de Azure, consulte la [Introducción a DNS de Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13af8-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="13af8-177">Para más información acerca de la automatización de DNS, consulte [Creación de conjuntos de registros y zonas DNS con el SDK de .NET](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="13af8-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="13af8-178">Para más información acerca de los registros de DNS inversos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13af8-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
