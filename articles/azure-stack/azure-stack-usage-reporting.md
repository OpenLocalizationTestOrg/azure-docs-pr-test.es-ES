---
title: Notificar los datos de uso de Azure Stack a Azure | Microsoft Docs
description: "Aprenda cómo configurar datos de uso de informes en Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun;AlfredoPizzirani
ms.openlocfilehash: 9bc202fe6aad70cb0f10a2da08e37428f78630d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="report-azure-stack-usage-data-to-azure"></a>Notificar los datos de uso de Azure Stack a Azure 

Los datos de uso, también denominados datos de consumo, representan la cantidad de recursos usados. En Azure Stack, los datos de uso deben indicarse a Azure a efectos de facturación. Los administradores de la nube de Azure Stack deben configurar su instancia de Azure Stack para informar de los datos de uso a Azure.

> [!NOTE]
> Los informes de datos de uso no son necesarios para Azure Stack Development Kit y a los usuarios no se les cobrará por consumir recursos. Sin embargo, los administradores de la nube de Azure Stack pueden probar esta característica y proporcionar comentarios sobre ella. Cuando varios nodos de Azure Stack comienzan a estar disponibles con carácter general, todos los entornos de varios nodos deben notificar los datos de uso a Azure.

![flujo de facturación](media/azure-stack-usage-reporting/billing-flow.png)

Los datos de uso se envían desde Azure Stack a Azure a través de Azure Bridge. En Azure, el sistema commerce procesa los datos de uso y genera la factura. Cuando se genera la factura, el propietario de la suscripción de Azure puede verla y descargarla desde el [Centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions). Para aprender cómo se autoriza el uso de Azure Stack, consulte el [documento de precios y empaquetado de Azure Stack](https://go.microsoft.com/fwlink/?LinkId=842847&clcid=0x409).

## <a name="set-up-usage-data-reporting"></a>Configuración de informes de datos de uso

Para configurar los informes de datos de uso en Azure Stack, debe [registrar la instancia de la Azure Stack con Azure](azure-stack-register.md). Como parte del proceso de registro, Azure Stack se configura con Azure Bridge, que conecta Azure Stack a Azure y envía los datos de uso. Los siguientes datos de uso se envían desde Azure Stack a Azure:

* **Id. de medidor**: Identificador único del recurso que se consumió.
* **Cantidad**: Cantidad de datos de uso de recursos que se ha producido en un período de tiempo determinado.
* **Ubicación**: Ubicación donde se implementa el recurso actual de Azure Stack.
* **URI de recurso**: URI completo del recurso para el que se notifica el uso. 
* **Id. de suscripción**: Identificador de suscripción del usuario de Azure Stack.
* **Tiempo**: Hora de inicio y finalización de los datos de uso. Hay un retraso determinado entre el momento en que se usan estos recursos en Azure Stack y el momento en que se notifican los datos de uso a commerce. Azure Stack agrega los datos de uso para cada 24 horas y los datos de uso de informes para la canalización del comercio en Azure llevan algunas horas más. Por lo tanto, el uso que se produce brevemente antes de medianoche puede aparecer en Azure al día siguiente.

## <a name="test-usage-data-reporting"></a>Prueba de informes de datos de uso 

1. Para probar los informes de datos de uso, cree unos pocos recursos en Azure Stack. Por ejemplo, puede crear una [cuenta de almacenamiento](azure-stack-provision-storage-account.md), una [máquina virtual Windows Server](azure-stack-provision-vm.md) y una máquina virtual Linux con SKU estándar y básico para ver cómo se informa del uso del núcleo. Los datos de uso para diferentes tipos de recursos se notifican en medidores diferentes.  

2. Deje que los recursos se ejecuten durante horas. Información de uso se recopila aproximadamente una vez cada hora. Después de recopilarse, estos datos se transmiten a Azure y se procesan en el sistema Azure commerce. Este proceso puede tardar varias horas.  

3. Inicie sesión en el [Centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions) como administrador de cuenta de Azure y seleccione la suscripción de Azure que usa para registrar Azure Stack. Puede ver los datos de uso de Azure Stack, la cantidad que se cobra por cada uno de los recursos usados, como se muestra en la siguiente imagen:  
   ![flujo de facturación](media/azure-stack-usage-reporting/pricng-details.png)

Para Azure Stack Development Kit, los recursos de Azure Stack tampoco se cobran; el precio se muestra como 0,00 USD. Cuando varios nodos de Azure Stack comienzan a estar disponibles con carácter general, puede ver el costo real para cada uno de estos recursos. 

## <a name="which-azure-stack-instances-are-charged"></a>¿Qué instancias de Azure Stack se cobran?
El uso de recursos está disponible para las instancias de Azure Stack Development Kit. 

Según la disponibilidad general, se cobran los sistemas de varios nodos de Azure Stack mientras que el entorno del kit de desarrollo sigue estando disponible sin costo alguno. Para los sistemas de varios nodos, se cobran las máquinas virtuales de la carga de trabajo, Storage services y App Services. 

## <a name="are-users-charged-for-the-infrastructure-vms"></a>¿Se les cobrará a los usuarios la infraestructura de las máquinas virtuales?
No, se informa a Azure de los datos de uso para las máquinas virtuales de la infraestructura de Azure Stack, que se crean durante la implementación, pero no hay ningún cargo para estas máquinas virtuales. La infraestructura de máquinas virtuales incluye las máquinas virtuales que se crean mediante el script de implementación de Azure Stack, y las máquinas virtuales que se ejecutan como proveedores de recursos propios de Microsoft, como proceso, almacenamiento, SQL.

## <a name="what-azure-meters-are-used-when-reporting-usage-data"></a>¿Los medidores de Azure se usan cuando se informa de los datos de uso?
Estos son los dos conjuntos de medidores que se utilizan al informar de los datos de uso:  

* **Medidores de precio total**: Utilizados para los recursos asociados a las cargas de trabajo del usuario.  
* **Medidores de administración**: Utilizados para los recursos de infraestructura. Estos medidores no tienen costo.

## <a name="which-subscription-is-charged-for-the-resources-consumed"></a>¿Qué suscripción se cobra por los recursos consumidos?
La suscripción que se proporciona cuando [se registra Azure Stack con Azure](azure-stack-register.md) se cobra.

## <a name="what-types-of-subscriptions-are-supported-for-usage-data-reporting"></a>¿Qué tipos de suscripciones se admiten para informar de los datos de uso?
Para Azure Stack Development Kit, las suscripciones a MSDN, el pago por uso y el Contrato Enterprise (EA) son compatibles con los informes de datos de uso. 

## <a name="does-usage-data-reporting-work-in-sovereign-clouds"></a>¿El informe de datos de uso funciona en las nubes soberanas?
En Azure Stack Development Kit, los informes de datos de uso requieren suscripciones creadas en el sistema global de Azure. No se pueden registrar las suscripciones creadas en una de las nubes soberanas (nubes del Azure Government, Azure Germany y Azure China) con Azure, por lo que no admiten informes de datos de uso. 

## <a name="can-an-administrator-test-usage-data-reporting-before-ga"></a>¿Puede probar un administrador informes de datos de uso antes de la disponibilidad general?
Sí, los administradores de Azure Stack pueden probar los datos de uso que se notifican al [registrar](azure-stack-register.md) la instancia del kit de desarrollo con Azure. Después del registro, los datos de uso inician el flujo de la instancia de Azure Stack a su suscripción de Azure. 

## <a name="how-can-users-identify-azure-stack-usage-data-in-the-azure-billing-portal"></a>¿Cómo pueden identificar los usuarios los datos de uso de Azure Stack en el portal de facturación de Azure?
Los usuarios pueden ver los datos de uso del Azure Stack en el archivo de detalles de uso. Para saber cómo obtener el archivo de detalles de uso, consulte el artículo [Descargar archivo de uso desde el Centro de cuentas de Azure](../billing/billing-download-azure-invoice-daily-usage-date.md#download-usage-from-the-account-center-csv). El archivo de detalles de uso contiene los medidores de Azure Stack que identifican las máquinas virtuales y el almacenamiento en Azure Stack. Todos los recursos usados en Azure Stack se notifican en la región denominada "Azure Stack".

## <a name="why-doesnt-the-usage-reported-in-azure-stack-match-the-report-generated-from-azure-account-center"></a>¿Por qué el uso notificado en Azure Stack no coincide con el informe generado a partir del Centro de cuentas de Azure?
Hay un retraso entre cuando los datos de uso se generan en Azure Stack frente a cuando se envía a Azure commerce. El retraso es el tiempo necesario para cargar datos de uso de Azure Stack en Azure commerce. Debido a este retraso, el uso que se produce brevemente antes de medianoche puede aparecer en Azure al día siguiente. Puede ver la diferencia si usa la [API de uso de Azure Stack](azure-stack-provider-resource-api.md)y compara los resultados con el uso notificado en el portal de facturación de Azure.

## <a name="next-steps"></a>Pasos siguientes

* [API de uso de proveedor](azure-stack-provider-resource-api.md)  
* [API de uso de inquilino](azure-stack-tenant-resource-usage-api.md)
* [Preguntas más frecuentes sobre uso](azure-stack-usage-related-faq.md)