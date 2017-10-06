---
title: tendencia de costo laboratorio estimado mensual de aaaView de hello en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información sobre el gráfico de tendencias de coste estimado mensual de hello laboratorios de desarrollo y pruebas de Azure."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>Tendencia de costo laboratorio estimado mensual de vista de hello en los laboratorios de desarrollo y pruebas de Azure
característica de administración de costos de Hola de laboratorios de desarrollo y pruebas le ayuda a controlar el costo de hello del laboratorio. Este artículo se explica cómo hello toouse **tendencia de costo estimado mensual** tooview gráfico estimado costo hasta la fecha del mes natural actual de Hola y Hola costo proyectado de fin de mes de hello mes natural actual. En este artículo, aprenderá cómo tooview Hola gráfico de tendencias de coste estimado mensual en hello portal de Azure.

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>Ver gráfico de tendencia de costo mensual estimado Hola
Hola tooview gráfico de tendencia de costo mensual estimado, siga estos pasos: 

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
3. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.   
4. En la hoja del laboratorio de hello, seleccione **costo configuración**.
5. En el laboratorio de hello **costo configuración** hoja, seleccione **tendencia de costo de laboratorio**.
6. Hello captura de pantalla siguiente muestra un ejemplo de un gráfico de costo. 
   
    ![Gráfico de costos](./media/devtest-lab-configure-cost-management/graph.png)

Hola **costo estimado** valor es Hola estimado costo hasta la fecha del mes natural actual. Hola **costo previsto** se hello costo estimado de toda Hola mes actual del calendario, calcula con costo de laboratorio de Hola para hello cinco días anteriores.

Hola costo cantidades se redondean hacia arriba toohello siguiente número de entero. Por ejemplo: 

* 5.01 se redondea hacia arriba too6 
* 5.50 se redondea hacia arriba too6
* 5.99 se redondea hacia arriba too6

Como indica anteriormente gráfico hello, los costos de Hola que se ven en el gráfico de hello son *estimado* cuesta mediante [pago por uso](https://azure.microsoft.com/offers/ms-azr-0003p/) ofrecer tarifas.
Además, es siguiente hello *no* incluido en el cálculo del costo de hello:

* Las suscripciones de Dreamspark y CSP no se admiten como laboratorios de desarrollo y pruebas de Azure usa hello [API de facturación de Azure](../billing/billing-usage-rate-card-overview.md) laboratorio de hello toocalculate un costo, que no admite las suscripciones de CSP o Dreamspark.
* Las tarifas de su oferta. Actualmente, no es capaz de toouse las tarifas de oferta (se muestra en su suscripción) que se han negociado asociados con Microsoft o Microsoft. Se usan tarifas de pago por uso.
* Los impuestos
* Los descuentos
* La divisa de facturación. Actualmente, el costo de laboratorio de Hola se muestra únicamente en la moneda USD.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Entradas blogs relacionadas
* [Dos tookeep cosas más el costo por el buen camino en los laboratorios de desarrollo y pruebas](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [Why Cost Thresholds? (¿Por qué los umbrales de costo?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>Pasos siguientes
A continuación le presentamos algunas tootry cosas:

* [Definir directivas de laboratorio](devtest-lab-set-lab-policy.md) -Obtenga información acerca de cómo tooset Hola varias directivas se usan toogovern cómo se usan el laboratorio y sus máquinas virtuales. 
* [Creación de una imagen personalizada](devtest-lab-create-template.md): cuando cree una máquina virtual, deberá especificar una base, que puede ser una imagen personalizada o una imagen de Marketplace. Este artículo explica cómo toocreate personalizado de la imagen desde un archivo de disco duro virtual.
* [Configuración de imágenes de Marketplace](devtest-lab-configure-marketplace-images.md): DevTest Labs admite la creación de máquinas virtuales basadas en imágenes de Azure Marketplace. Este artículo se explica cómo toospecify que, si lo hay, imágenes de Azure Marketplace se pueden usar al crear máquinas virtuales en un laboratorio.
* [Crear una máquina virtual en un laboratorio](devtest-lab-add-vm-with-artifacts.md) -ilustra cómo toocreate una máquina virtual desde una imagen base (ya sea personalizado o Marketplace) y cómo toowork con los artefactos en la máquina virtual.

