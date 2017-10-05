---
title: Las cuotas en la pila de Azure | Documentos de Microsoft
description: "Los administradores establecer cuotas para restringir la cantidad máxima de recursos que los inquilinos tienen acceso a."
services: azure-stack
documentationcenter: 
author: mattmcg
manager: byronr
editor: 
ms.assetid: 955c6dd8-cefe-42f3-af88-e11d17d22725
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: mattmcg
ms.openlocfilehash: bbefca1a60f38f18838ee6563bd26b934cd02172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-view-quotas-in-azure-stack"></a>Establecer y ver las cuotas en la pila de Azure
Las cuotas de definen los límites de recursos que una suscripción de inquilino puede aprovisionar o consumir. Por ejemplo, una cuota puede permitir a un inquilino para crear máquinas virtuales hasta cinco. Para agregar un servicio a un plan, el administrador debe configurar los valores de cuota para ese servicio.

Las cuotas son configurables por el servicio y para cada ubicación, permitir a los administradores proporcionar un control granular sobre el consumo de recursos. Los administradores pueden crear uno o varios recursos de cuota y asociarlos a los planes, lo que significa que pueden proporcionar ofertas diferenciadas para sus servicios. Cuotas para un servicio determinado se pueden crear desde el **proveedor de recursos** módulo de administración para ese servicio.

Un inquilino que se suscribe a una oferta que contiene varios planes puede utilizar todos los recursos que están disponibles en cada plan.

## <a name="to-create-an-iaas-quota"></a>Para crear una cuota de IaaS
1. En un explorador, vaya a [https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/).
   
   Inicie sesión en el portal de la pila de Azure como administrador (mediante las credenciales que proporcionó durante la implementación).
2. Seleccione **New**, a continuación, **inquilino ofrece + planes**y seleccione **cuota**.
3. Seleccione el primer servicio para el que desea crear una cuota. Para una cuota de la infraestructura como servicio, siga estos pasos para los servicios de proceso, red y almacenamiento.
   En este ejemplo, primero se crea una cuota para el servicio de proceso. En el **Namespace** lista, seleccione la **Microsoft.Compute** espacio de nombres.
   
   > ![Crear una nueva cuota de proceso](./media/azure-stack-setting-quota/NewComputeQuota.PNG)
   > 
   > 
4. Elija la ubicación donde se define la cuota (por ejemplo, 'local').
5. En el **configuración de cuota** de elemento, dice **establecer la capacidad de cuota**. Haga clic en este elemento para establecer la configuración de cuota.
6. En el **establecer cuotas** hoja, verá todos los recursos de proceso para el que puede configurar los límites. Cada tipo tiene un valor predeterminado que tiene asociado. Puede cambiar estos valores o puede seleccionar la **Aceptar** situado en la parte inferior de la hoja para aceptar los valores predeterminados.
   
   > ![Establecer una cuota de proceso](./media/azure-stack-setting-quota/SetQuotasBladeCompute.PNG)
   > 
   > 
7. Una vez haya configurado los valores y hacer clic en **Aceptar**, el **configuración de cuota** elemento aparece como **configurado**. Haga clic en **Aceptar** para crear el **cuota** recursos.
   
   Verá una notificación que indica que se está creando la cuota del recurso.
8. Una vez creada correctamente la cuota establecida, recibirá una segunda notificación. La cuota de servicio de proceso ahora está lista para asociarse a un plan. Repita estos pasos con los servicios de red y almacenamiento y esté listo para crear un plan de IaaS.
   
   > ![Notificación cuando se realiza correctamente la creación de cuota](./media/azure-stack-setting-quota/QuotaSuccess.png)
   > 
   > 

## <a name="compute-quota-types"></a>Tipos de cuota de proceso
| **Tipo** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Número máximo de máquinas virtuales |50 |El número máximo de máquinas virtuales que puede crear una suscripción en esta ubicación. |
| Número máximo de núcleos de máquinas virtuales |100 |El número máximo de núcleos que puede crear una suscripción en esta ubicación (por ejemplo, una máquina virtual A3 tiene cuatro núcleos). |
| Cantidad máxima de memoria de máquina virtual (GB) |150 |La cantidad máxima de memoria RAM que se puede aprovisionar en megabytes (por ejemplo, una máquina virtual A1 consume 1,75 GB de RAM). |

> [!NOTE]
> Las cuotas de proceso no se aplican a esta versión preliminar técnica.
> 
> 

## <a name="storage-quota-types"></a>Tipos de cuotas de almacenamiento
| **Elemento** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Capacidad máxima (GB) |500 |Capacidad de almacenamiento total que puede consumir una suscripción en esta ubicación. |
| Número total de cuentas de almacenamiento |20 | |El número máximo de cuentas de almacenamiento que puede crear una suscripción en esta ubicación. |

## <a name="network-quota-types"></a>Tipos de cuota de red
| **Elemento** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Número máximo de direcciones IP públicas |50 |El número máximo de direcciones IP públicas que puede crear una suscripción en esta ubicación. |
| Número máximo de redes virtuales |50 |El número máximo de redes virtuales que puede crear una suscripción en esta ubicación. |
| Número máximo de puertas de enlace de red virtual |1 |El número máximo de puertas de enlace de red virtual (puertas de enlace de VPN) que puede crear una suscripción en esta ubicación. |
| Número máximo de conexiones de red |2 |El número máximo de conexiones de red (punto a punto o sitio a sitio) que puede crear una suscripción en todas las puertas de enlace de red virtual de esta ubicación. |
| Número máximo de equilibradores de carga |50 |El número máximo de equilibradores de carga que puede crear una suscripción en esta ubicación. |
| Nº máx. NIC |100 |El número máximo de interfaces de red que puede crear una suscripción en esta ubicación. |
| Número máximo de grupos de seguridad de red |50 |El número máximo de grupos de seguridad de red que puede crear una suscripción en esta ubicación. |

##<a name="view-an-existing-quota"></a>Visualización de una cuota existente
Para ver una cuota existente, haga clic en **más servicios**>**proveedores de recursos** y seleccione el servicio al que está asociada la cuota que desea ver. A continuación, haga clic en **cuotas**y seleccione la cuota que desea ver.
   > ![Ver una cuota existente](./media/azure-stack-setting-quota/ExistingQuota.PNG)
