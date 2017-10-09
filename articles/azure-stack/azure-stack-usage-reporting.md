---
title: tooAzure de datos de uso de Azure pila aaaReport | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset los datos de uso de informes en la pila de Azure."
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
ms.openlocfilehash: deecd66d9022b2e0c274ff4e0276d3b2e3bcc99e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="report-azure-stack-usage-data-tooazure"></a>Informe tooAzure de datos de uso de la pila de Azure 

Datos de uso, también denominado como datos de consumo representan la cantidad de Hola de recursos que usa. En la pila de Azure, el uso de datos deben ser notifica tooAzure para facturar el propósito. Los administradores de la nube de Azure pila deben configurar su tooAzure de datos de uso de Azure pila instancia tooreport.

> [!NOTE]
> Informes de datos de uso no es necesaria para hello Kit de desarrollo de pila de Azure y los usuarios no se le cobrará para consumir recursos. Sin embargo, los administradores de la nube de Azure Stack pueden probar esta característica y proporcionar comentarios sobre ella. Cuando varios nodos de la pila de Azure deja de estar disponible con carácter general, todos los entornos de varios nodos de hello deben notificar tooAzure de datos de uso.

![flujo de facturación](media/azure-stack-usage-reporting/billing-flow.png)

Datos de uso se envían desde tooAzure de pila de Azure a través de hello puente de Azure. En Azure, procesos del sistema de comercio de Hola Hola datos de uso y genera la factura de Hola. Cuando se genera la factura de hello, propietario de la suscripción de Azure de hello puede ver y descargar de hello [centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions). toolearn acerca de cómo se autoriza el uso de la pila de Azure, consulte toohello [Azure pila empaquetar y precios documento](https://go.microsoft.com/fwlink/?LinkId=842847&clcid=0x409).

## <a name="set-up-usage-data-reporting"></a>Configuración de informes de datos de uso

tooset los datos de uso de informes en la pila de Azure, debe [registrar la instancia de la pila de Azure con Azure](azure-stack-register.md). Como parte del proceso de registro de hello, pila de Azure se configura con puente de Azure, que se conecta a Azure pila tooAzure y envía datos de uso de Hola Hola. Hola después de los datos de uso se envía desde tooAzure de pila de Azure:

* **Id. del panel de instrumentos** : identificador único para el recurso de hello consumido.
* **Cantidad**: Cantidad de datos de uso de recursos que se ha producido en un período de tiempo determinado.
* **Ubicación** : ubicación donde se implementa el recurso de Azure pila actual de Hola.
* **URI de recurso** – completo URI del recurso de hello para el que se notifica el uso. 
* **Id. de suscripción** : Id. de suscripción de usuario de la pila de Azure de Hola.
* **Tiempo** – hora inicial y final de los datos de uso de Hola. Hay un determinado retardo entre tiempo hello cuando se usan estos recursos en la pila de Azure y cuando los datos de uso de hello toocommerce notificado. Pila de Azure agrega datos de uso para cada 24 horas y reporting toocommerce de datos de uso de la canalización en Azure toma otra pocas horas. Por lo tanto, puede aparecer el uso que se produce en breve antes de medianoche en Azure Hola siguiente día.

## <a name="test-usage-data-reporting"></a>Prueba de informes de datos de uso 

1. datos de uso de tootest informes, crear solo unos pocos recursos en la pila de Azure. Por ejemplo, puede crear un [cuenta de almacenamiento](azure-stack-provision-storage-account.md), [VM de Windows Server](azure-stack-provision-vm.md) y una VM de Linux con Basic y SKU estándar toosee cómo se informa del uso de núcleo. se informa de los datos de uso de Hola para diferentes tipos de recursos en diferentes metros.  

2. Deje que los recursos se ejecuten durante horas. Información de uso se recopila aproximadamente una vez cada hora. Después de recopilar, estos datos se tooAzure transmitido y procesan en hello sistema de comercio de Azure. Este proceso puede tardar hasta tooa pocas horas.  

3. Inicie sesión en toohello [centro de cuentas de Azure](https://account.windowsazure.com/Subscriptions) como hello Azure cuenta de administrador y seleccione Hola suscripción de Azure que usa tooregister Hola pila de Azure. Puede ver datos de uso de Azure pila hello, importe de hello cobra por cada uno de hello recursos que utiliza como se muestra en hello después de imagen:  
   ![flujo de facturación](media/azure-stack-usage-reporting/pricng-details.png)

Para hello Kit de desarrollo de pila de Azure, los recursos de la pila de Azure no se le cobrará por lo tanto, se muestra el precio de hello como $0,00. Cuando varios nodos de la pila de Azure deja de estar disponible con carácter general, puede ver Hola real de costo para cada uno de estos recursos. 

## <a name="which-azure-stack-instances-are-charged"></a>¿Qué instancias de Azure Stack se cobran?
El uso de recursos está disponible para las instancias de Azure Stack Development Kit. 

En disponibilidad general, los sistemas de varios nodos de pila de Azure se cobran mientras que el entorno del kit de desarrollo de hello sigue estando disponible sin costo alguno. Para los sistemas de varios nodos, se cobran las máquinas virtuales de la carga de trabajo, Storage services y App Services. 

## <a name="are-users-charged-for-hello-infrastructure-vms"></a>¿Se le cobrará a los usuarios para la infraestructura de hello las máquinas virtuales?
No, los datos de uso de hello para la infraestructura de la pila de Azure VM, que se crean durante la implementación están notificado tooAzure, pero no hay ningún cargo para estas máquinas virtuales. infraestructura de Hello máquinas virtuales incluyen máquinas virtuales de hello creados por el script de implementación de pila de Azure de Hola y Hola máquinas virtuales que se ejecutan como proveedores de recursos propios de Microsoft de proceso, almacenamiento, SQL.

## <a name="what-azure-meters-are-used-when-reporting-usage-data"></a>¿Los medidores de Azure se usan cuando se informa de los datos de uso?
continuación de Hola se muestran dos conjuntos de contadores que se utilizan en informes de datos de uso de hello:  

* **Medidores de precio total**: Utilizados para los recursos asociados a las cargas de trabajo del usuario.  
* **Medidores de administración**: Utilizados para los recursos de infraestructura. Estos medidores no tienen costo.

## <a name="which-subscription-is-charged-for-hello-resources-consumed"></a>¿Qué suscripción se cobra por recursos Hola utilizados?
Hola suscripción que se proporciona cuando [el registro de pila de Azure con Azure](azure-stack-register.md) se cobra.

## <a name="what-types-of-subscriptions-are-supported-for-usage-data-reporting"></a>¿Qué tipos de suscripciones se admiten para informar de los datos de uso?
Para las suscripciones de MSDN, contrato Enterprise (EA), pago por uso y Kit de desarrollo de Azure pila Hola admite informes de datos de uso. 

## <a name="does-usage-data-reporting-work-in-sovereign-clouds"></a>¿El informe de datos de uso funciona en las nubes soberanas?
Hola Kit de desarrollo de pila de Azure, informes de datos de uso requieren que las suscripciones que se crean en el sistema de Azure global de Hola. Las suscripciones creadas en una de las nubes soberano hello (Hola administración pública de Azure y Azure en Alemania, Azure China nubes) no se puede registrar con Azure, por lo que no admiten informes de datos de uso. 

## <a name="can-an-administrator-test-usage-data-reporting-before-ga"></a>¿Puede probar un administrador informes de datos de uso antes de la disponibilidad general?
Sí, los administradores de la pila de Azure pueden probar la generación de informes de datos de uso de hello [registrar](azure-stack-register.md) instancia del kit de desarrollo de hello con Azure. Después de registrar, datos de uso inician fluyen desde su tooyour de instancia de la pila de Azure suscripción de Azure. 

## <a name="how-can-users-identify-azure-stack-usage-data-in-hello-azure-billing-portal"></a>¿Cómo los usuarios pueden identificar datos de uso de la pila de Azure en hello Azure portal de facturación?
Los usuarios pueden ver datos de uso de Azure pila hello en el archivo de detalles de uso de hello. tooknow acerca de cómo uso de hello tooget detalles de archivo, consulte toohello [Descargar archivo de uso de hello Azure Account Center](../billing/billing-download-azure-invoice-daily-usage-date.md#download-usage-from-the-account-center-csv) artículo. archivo de detalles de uso de Hello contiene metros de pila de Azure de Hola que identifican el almacenamiento de la pila de Azure y máquinas virtuales. Todos los recursos usados en la pila de Azure se notifican en la región de hello denominada "Pila de Azure".

## <a name="why-doesnt-hello-usage-reported-in-azure-stack-match-hello-report-generated-from-azure-account-center"></a>¿Por qué no informa del uso de hello en pila de Azure coincide con informes de hello generados a partir de centro de cuentas de Azure?
Hay un retraso entre cuando los datos de uso de Hola se generan en la pila de Azure frente a cuando llega el comercio tooAzure enviado. retraso de Hello es Hola datos de uso de tooupload de tiempo necesario de comercio de tooAzure de pila de Azure. Debido toothis retraso, puede aparecer el uso que se produce en breve antes de medianoche en Azure Hola siguiente día. Si usas hello [API de uso de Azure pila](azure-stack-provider-resource-api.md)y comparar resultados de hello informa del uso de toohello en Hola portal de facturación de Azure, puede ver una diferencia.

## <a name="next-steps"></a>Pasos siguientes

* [API de uso de proveedor](azure-stack-provider-resource-api.md)  
* [API de uso de inquilino](azure-stack-tenant-resource-usage-api.md)
* [Preguntas más frecuentes sobre uso](azure-stack-usage-related-faq.md)