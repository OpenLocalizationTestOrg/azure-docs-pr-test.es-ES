---
title: "los costos de aaaManage eficazmente para SQL Server en máquinas virtuales de Azure | Documentos de Microsoft"
description: Proporciona recomendaciones para elegir el modelo de precios Hola derecho SQL Server virtual machine.
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Orientación de precios de SQL Server para máquinas virtuales de Azure

En este tema se proporciona una guía sobre precios de máquinas virtuales de SQL Server en Azure. Hay varias opciones que afectan al costo y es importante toopick Hola imagen de la derecha que equilibra los costes con los requisitos empresariales.

## <a name="free-licensed-sql-server-editions"></a>Ediciones de SQL Server con licencia gratuita

Si desea toodevelop, probar, o crear una prueba de concepto y luego usar hello licencia libre **edition de SQL Server Developer**. Esta edición tiene todo lo que en SQL Server Enterprise edition, lo que se puede usar toobuild cualquier aplicación que desee. Pero no se permite toorun en producción. Una máquina virtual para desarrolladores de SQL Server solo se le cobrará por costo de Hola de Hola de máquina virtual, no para las licencias de SQL Server.

Si desea que toorun una carga de trabajo ligera en producción (< 4 núcleos, < 1 GB de memoria, < 10 GB/base de datos), a continuación, usar hello licencia libre **SQL Server Express edition**. Una VM de SQL Express solo le cobrará por costo de Hola de Hola de máquina virtual, no licencias de SQL.

Para estas cargas de trabajo de producción ligeras o de desarrollo y pruebas, también puede ahorrar dinero si elige un tamaño de máquina virtual menor apto para estas cargas de trabajo. Hola DS1v2 podría ser una buena elección para estas cargas de trabajo.

toocreate una VM de Azure de SQL Server 2016 con una de estas imágenes, vea Hola siguientes vínculos:

- [Máquina virtual de Azure en SQL Server 2016 Developer](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [Máquina virtual de Azure en SQL Server 2016 Express](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Ediciones de pago de SQL Server

Si tiene una carga de trabajo de producción no ligero, utilice uno de hello siguientes ediciones de SQL Server:

| Edición de SQL Server | Carga de trabajo |
|-----|-----|
| Web | Sitios web pequeños |
| Estándar | Cargas de trabajo pequeño toomedium |
| Enterprise | Cargas de trabajo grandes o críticas|

Tiene dos toopay de opciones de licencia de SQL Server para estas ediciones: *pagar por uso* o *traiga su propia licencia*.

### <a name="pay-per-usage"></a>Pago por uso

**Licencia de SQL Server Hola pago por uso** significa que el costo por minuto de Hola de hello Azure VM en ejecución incluye costo de Hola de licencia de SQL Server de Hola. Puede ver precios Hola Hola diferentes ediciones de SQL Server (Web, Standard, Enterprise) en hello [página de precios de VM de Azure](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Hello costo es Hola iguales para todas las versiones de SQL Server (2008 R2 too2016). Como con SQL Server, por lo general, licencias Hola costo de las licencias por minuto depende en hello número de núcleos de la máquina virtual.

Pagar Hola SQL Server por el uso de licencias se recomiendan para:

- Cargas de trabajo temporales o periódicas. Por ejemplo, una aplicación que necesita toosupport un evento para un par de meses cada año, o el análisis de negocios el lunes.
- Cargas de trabajo con una duración o escala desconocidas. Por ejemplo, una aplicación que puede no ser necesaria en unos meses, o que puede requerir más o menos capacidad de proceso, según la demanda.

toocreate una VM de Azure de SQL Server 2016 con una de estas imágenes de pago por uso, vea Hola siguientes vínculos:

- [Máquina virtual de Azure en SQL Server 2016 Web](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [Máquina virtual de Azure en SQL Server 2016 Standard](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [Máquina virtual de Azure en SQL Server 2016 Enterprise](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Al crear una máquina virtual de SQL Server en hello portal de Azure, Hola estimado costo mensual que se muestran en hello **elegir un tamaño de** hoja no incluye los costos de licencias de SQL Server. Este es el costo de Hola de hello VM independiente.
>
> ![Hoja Elegir un tamaño](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Para hello libre ediciones con licencias Express y Developer de SQL Server, se trata de costo estimado total de Hola. Pero para Enterprise, Standard y Web, buscar Hola los costos de licencia de SQL adicionales en hello [máquinas virtuales de Windows página de precios](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). En la página de precios de hello, seleccione la edición de destino de SQL Server.

### <a name="bring-your-own-license-byol"></a>Traiga su propia licencia (BYOL)

**Volver a poner su propia licencia de SQL Server a través de portabilidad de licencia**, también denominada tooas **BYOL**, medios mediante una licencia de volumen existente de SQL Server con Software Assurance en una máquina virtual de Azure. Una VM de SQL Server mediante BYOL solo le cobrará por costo de Hola de ejecutar Hola de máquina virtual, no para las licencias de SQL Server, dado que ya han adquirido licencias y Software Assurance a través de un programa de licencias por volumen.

Se recomienda traer su propia licencia de SQL a través de License Mobility para:

- Cargas de trabajo continuas. Por ejemplo, una aplicación que necesita las operaciones empresariales toosupport 24 x 7.
- Cargas de trabajo con una duración y escala desconocidas. Por ejemplo, una aplicación que será necesaria para año todo de Hola y qué petición se ha previsto.

toouse BYOL con una VM de SQL Server, debe tener una licencia para SQL Server Standard o Enterprise y [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), que es una opción necesaria a través de algunas [licencias por volumen](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programas y opcional adquirir con otros usuarios.  Hola proporcionados a través de programas de licencias por volumen de niveles de precios varía según tipo hello de hello y acuerdo cantidad y o compromiso tooSQL Server. Pero como regla general, volver a poner su propia licencia para las cargas de trabajo de producción continua tiene Hola siguientes ventajas:

| Ventaja de BYOL | Descripción |
|-----|-----|
| **Ahorros en costos** | Traer su propia licencia de SQL Server resulta más rentable que pagar por uso si una carga de trabajo va a ejecutar continuamente SQL Server Standard o Enterprise durante *más de diez meses*. |
| **Ahorros a largo plazo** | En promedio, es *30% más barato por año* toobuy o renovar una licencia de SQL Server para hello primera 3 años. Además, después de 3 años, no es necesario, ya licencia de toorenew Hola pago solo para Software Assurance. En ese momento, resulta un *200 % más barato*. |
| **Réplica secundaria pasiva gratuita** | Otra ventaja de seguir usando su propia licencia es hello [liberar licencias para una réplica secundaria pasiva](https://azure.microsoft.com/pricing/licensing-faq/) por SQL Server para fines de alta disponibilidad. Esta forma se reduce en mitad Hola coste de una implementación de SQL Server de alta disponibilidad (por ejemplo, mediante grupos de disponibilidad AlwaysOn) de las licencias. Hola derechos toorun Hola pasivo base de datos secundaria se proporcionan a través de hello beneficio de Software Assurance de servidores de conmutación por error. |

toocreate una VM de Azure de SQL Server 2016 con una de estas imágenes bring-your-posee-licencia, ver máquinas virtuales de hello precedidas con "{BYOL}":

- [Máquina virtual de Azure en SQL Server 2016 Enterprise](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [Máquina virtual de Azure en SQL Server 2016 Standard](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Infórmenos dentro de diez días de cuántas licencias de SQL Server usará en Azure. Hello vínculos toohello anterior imágenes tienen instrucciones sobre cómo toodo esto.

## <a name="avoid-unecessary-costs"></a>Evitar costos innecesarios

Si usas las cargas de trabajo que no se ejecutan continuamente, considere la posibilidad de apagar máquina virtual de Hola durante los períodos de hello inactiva. Pague solo por lo que usa.

Por ejemplo, si simplemente está tratando de SQL Server en una máquina virtual de Azure, no desearía tooincur cargos accidentalmente dejando ejecutándolo en semanas. Una solución es hello toouse [característica de detención automática](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Parada automática de máquinas virtual de SQL](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

La parada automática forma parte de un conjunto mayor de características similares proporcionadas por [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Para otros flujos de trabajo, considere la posibilidad de parar y reiniciar automáticamente las máquinas virtuales con una solución de scripting, como [Azure Automation](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> Apagar y cancelar la asignación de la máquina virtual son Hola solo forma tooavoid se cobra. Basta con detener o utilizando tooshut de opciones de energía hacia abajo Hola VM tendrá un coste de uso.

## <a name="next-steps"></a>Pasos siguientes

Para consultar una guía de precios general de Azure, vea [Prevención de costos inesperados con la administración de costos y facturación de Azure](../../../billing/billing-getting-started.md).

Para hello las máquinas virtuales más reciente sobre los precios, incluido SQL Server, vea hello [página de precios de VM de Azure](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Revise otros temas de la máquina virtual de SQL Server en [Información general de SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).
