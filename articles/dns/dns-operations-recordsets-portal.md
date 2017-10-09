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
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>Administrar registros DNS y los conjuntos de registros mediante Hola portal de Azure

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [CLI de Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [CLI de Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Este artículo muestra cómo toomanage conjuntos de registros y los registros para la zona DNS mediante el uso de Hola portal de Azure.

Es importante toounderstand Hola diferencia entre los conjuntos de registros de DNS y los registros DNS individuales. Un conjunto de registros es una colección de registros de una zona que tengan Hola mismo nombre y están Hola mismo tipo. Para obtener más información, consulte [Hola a conjuntos de registros de DNS de crear y registros mediante el portal de Azure](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Creación de un nuevo conjunto de registros y un registro

toocreate un conjunto de registros de hello portal de Azure, consulte [Hola de registros DNS crear mediante el portal de Azure](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Visualización de un conjunto de registros

1. Hola portal de Azure, vaya toohello **zona DNS** hoja.
2. Busque el conjunto de registros de Hola y selecciónelo. Se abren propiedades de conjunto de registros de Hola.

    ![Buscar un conjunto de registros](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>Agregar un nuevo conjunto de registros de registros tooa

Puede agregar una conjunto de registros too20 registros tooany. Un conjunto de registros no puede contener dos registros idénticos. Conjuntos de registros vacíos (con cero registros) se pueden crear, pero no aparecen en los servidores de nombres DNS de Azure Hola. Los conjuntos de registros de tipo CNAME pueden contener, como máximo, un registro.

1. En hello **propiedades de conjunto de registros** hoja para la zona DNS, haga clic en el registro de hello establecer que desea tooadd un registro a.

    ![Seleccionar un conjunto de registros](./media/dns-operations-recordsets-portal/selectset500.png)

2. Especificar propiedades de conjunto de registros de hello rellenando los campos de Hola.

    ![Incorporación de un registro](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Haga clic en **guardar** en Hola parte superior de hello hoja toosave su configuración. A continuación, cierre la hoja de Hola.
4. En la esquina de hello, verá que está guardando el registro de hello.

    ![Guardar el conjunto de registros](./media/dns-operations-recordsets-portal/saving150.png)

Una vez guardado el registro de hello, Hola valores en hello **zona DNS** hoja reflejará el nuevo registro de hello.

## <a name="update-a-record"></a>Actualización de un registro

Cuando se actualiza un registro en un conjunto de registros existente, campos de hello que puede actualizar dependen de tipo de Hola de registro que está trabajando.

1. En hello **propiedades de conjunto de registros** hoja para el conjunto de registros, busque el registro de hello.
2. Modifique el registro de hello. Cuando se modifica un registro, puede cambiar opciones de configuración disponibles de hello para el registro de hello. En el siguiente ejemplo de Hola Hola **dirección IP** campo está seleccionado, y dirección IP de hello está en proceso de Hola de que se está modificando.

    ![Modificar un registro](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Haga clic en **guardar** en Hola parte superior de hello hoja toosave su configuración. En hello esquina superior derecha, verá una notificación de Hola que se ha guardado el registro de hello.

    ![Agregar conjunto de registros](./media/dns-operations-recordsets-portal/saved150.png)

Una vez guardado el registro de hello, los valores de hello para el registro de hello establecidos en hello **zona DNS** hoja reflejará el registro de hello actualizado.

## <a name="remove-a-record-from-a-record-set"></a>Eliminación de un registro de un conjunto de registros

Puede usar registros de hello Azure tooremove portal desde un conjunto de registros. Tenga en cuenta que al quitar el último registro de hello desde un conjunto de registros, no se eliminan conjunto de registros de Hola.

1. En hello **propiedades de conjunto de registros** hoja para el conjunto de registros, busque el registro de hello.
2. Haga clic en registro de hello que desea tooremove. A continuación, seleccione **Quitar**.

    ![Quitar un registro](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Haga clic en **guardar** en Hola parte superior de hello hoja toosave su configuración.
4. Después de quitar el registro de hello, Hola valores de registro de hello en hello **zona DNS** hoja reflejará la eliminación de Hola.

## <a name="delete"></a>Eliminación de un conjunto de registros

1. En hello **propiedades de conjunto de registros** hoja para el conjunto de registros, haga clic en **eliminar**.

    ![Eliminación de un conjunto de registros](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Aparecerá un mensaje preguntando si desea que el conjunto de registros toodelete Hola.
3. Compruebe que el registro de hello de coincidencias de nombres Hola establecido que desee toodelete y, a continuación, haga clic en **Sí**.
4. En hello **zona DNS** hoja, compruebe que el conjunto de registros de hello ya no está visible.

## <a name="work-with-ns-and-soa-records"></a>Trabajo con registros NS y SOA

Los registros NS y SOA creados automáticamente se administran de forma diferente de otros tipos de registros.

### <a name="modify-soa-records"></a>Modificación de registros SOA

No se puede agregar o quitar registros de hello creado automáticamente el registro SOA establecido en vértice de la zona de hello (nombre = "@"). Sin embargo, puede modificar cualquiera de los parámetros de hello en hello registro SOA (excepto el "Host") y registro de hello establecer TTL.

### <a name="modify-ns-records-at-hello-zone-apex"></a>Modificar los registros NS en vértice de la zona de Hola

registro de NS de Hello establecido en vértice de la zona de Hola se crea automáticamente con cada zona DNS. Contiene los nombres de Hola de zona de hello Azure DNS nombre servidores toohello asignado.

Puede agregar nombre adicionales servidores toothis NS conjunto de registros, toosupport alojar conjuntamente dominios con más de un proveedor DNS. También puede modificar Hola TTL y los metadatos para este conjunto de registros. Sin embargo, no se puede quitar o modificar servidores de nombres DNS de Azure previamente rellenados Hola.

Tenga en cuenta que esto se aplica solo toohello NS conjunto de registros en vértice de la zona de Hola. Otros conjuntos de registros NS en su zona (como las zonas secundarias de toodelegate usado) pueden modificarse sin restricción.

### <a name="delete-soa-or-ns-record-sets"></a>Eliminación de conjuntos de registros SOA o NS

No se puede eliminar Hola SOA y NS conjuntos de registros en vértice de la zona de hello (nombre = "@") que se crean automáticamente cuando se crea la zona de Hola. Se eliminan automáticamente cuando se elimina la zona de Hola.

## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información acerca de DNS de Azure, vea hello [Introducción a DNS de Azure](dns-overview.md).
* Para obtener más información acerca de la automatización de DNS, consulte [zonas DNS de creación y conjuntos de registros mediante Hola .NET SDK](dns-sdk.md).
* Para más información acerca de los registros de DNS inversos, consulte [Introducción a DNS inverso y compatibilidad en Azure](dns-reverse-dns-overview.md).
