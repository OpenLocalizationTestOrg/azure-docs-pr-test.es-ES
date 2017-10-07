---
title: aaaQuotas en la pila de Azure | Documentos de Microsoft
description: "Los administradores establecer cuotas toorestrict Hola máximo de recursos que los inquilinos tienen acceso a."
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
ms.openlocfilehash: 9770802960af102a6d497b47d95cd6ec63ce219c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-view-quotas-in-azure-stack"></a>Establecer y ver las cuotas en la pila de Azure
Las cuotas de definen límites de Hola de recursos que una suscripción de inquilino puede aprovisionar o consumir. Por ejemplo, una cuota puede permitir un inquilino crear una toofive máquinas virtuales. tooadd un plan de tooa de servicio, el administrador debe configurar los valores de cuota de Hola para ese servicio.

Las cuotas son configurables por el servicio y para cada ubicación, habilitar los administradores tooprovide control detallado de consumo de recursos de Hola. Los administradores pueden crear uno o varios recursos de cuota y asociarlos a los planes, lo que significa que pueden proporcionar ofertas diferenciadas para sus servicios. Se pueden crear cuotas para un servicio determinado de hello **proveedor de recursos** módulo de administración para ese servicio.

Un inquilino que se suscribe tooan oferta que contiene varios planes puede utilizar todos los recursos que están disponibles en cada plan.

## <a name="toocreate-an-iaas-quota"></a>toocreate una cuota de IaaS
1. En un explorador, vaya a [https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/).
   
   Inicie sesión en toohello portal de la pila de Azure como administrador (mediante el uso de credenciales de Hola que proporcionó durante la implementación).
2. Seleccione **New**, a continuación, **inquilino ofrece + planes**y seleccione **cuota**.
3. Seleccione servicio primera hello para el que desea toocreate una cuota. Para una cuota de IaaS, siga estos pasos para los servicios de proceso, red y almacenamiento de Hola.
   En este ejemplo, primero se crea una cuota para el servicio de proceso de Hola. Hola **Namespace** lista, seleccione hello **Microsoft.Compute** espacio de nombres.
   
   > ![Crear una nueva cuota de proceso](./media/azure-stack-setting-quota/NewComputeQuota.PNG)
   > 
   > 
4. Elegir ubicación de Hola donde se define la cuota de hello (por ejemplo, 'local').
5. En hello **configuración de cuota** de elemento, dice **establecer la capacidad de cuota**. Haga clic en esta configuración de cuota de elemento tooconfigure Hola.
6. En hello **establecer cuotas** hoja, verá todos los recursos de proceso de hello para el que puede configurar los límites. Cada tipo tiene un valor predeterminado que tiene asociado. Puede cambiar estos valores o puede seleccionar hello **Aceptar** situado en parte inferior de Hola de hello hoja tooaccept Hola los valores predeterminados.
   
   > ![Establecer una cuota de proceso](./media/azure-stack-setting-quota/SetQuotasBladeCompute.PNG)
   > 
   > 
7. Una vez haya configurado los valores de hello y hace clic en **Aceptar**, hello **configuración de cuota** elemento aparece como **configurado**. Haga clic en **Aceptar** crear hello **cuota** recursos.
   
   Verá una notificación que indica que se está creando el recurso de cuota Hola.
8. Después de que se ha creado correctamente el conjunto de cuota de hello, recibirá una segunda notificación. cuota de servicio de proceso de Hello está ahora listo toobe asociado a un plan. Repita estos pasos con hello red y servicios de almacenamiento y está listo toocreate un plan de IaaS.
   
   > ![Notificación cuando se realiza correctamente la creación de cuota](./media/azure-stack-setting-quota/QuotaSuccess.png)
   > 
   > 

## <a name="compute-quota-types"></a>Tipos de cuota de proceso
| **Tipo** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Número máximo de máquinas virtuales |50 |número máximo de Hola de máquinas virtuales que puede crear una suscripción en esta ubicación. |
| Número máximo de núcleos de máquinas virtuales |100 |Hola número máximo de núcleos que puede crear una suscripción en esta ubicación (por ejemplo, una máquina virtual de A3 tiene cuatro núcleos). |
| Cantidad máxima de memoria de máquina virtual (GB) |150 |cantidad máxima de Hola de RAM que se puede aprovisionar en megabytes (por ejemplo, una máquina virtual A1 consume 1,75 GB de RAM). |

> [!NOTE]
> Las cuotas de proceso no se aplican a esta versión preliminar técnica.
> 
> 

## <a name="storage-quota-types"></a>Tipos de cuotas de almacenamiento
| **Elemento** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Capacidad máxima (GB) |500 |Capacidad de almacenamiento total que puede consumir una suscripción en esta ubicación. |
| Número total de cuentas de almacenamiento |20 | |número máximo de Hola de cuentas de almacenamiento que se puede crear una suscripción en esta ubicación. |

## <a name="network-quota-types"></a>Tipos de cuota de red
| **Elemento** | **Valor predeterminado** | **Descripción** |
| --- | --- | --- |
| Número máximo de direcciones IP públicas |50 |número máximo de Hola de direcciones IP públicas que puede crear una suscripción en esta ubicación. |
| Número máximo de redes virtuales |50 |número máximo de Hola de redes virtuales que puede crear una suscripción en esta ubicación. |
| Número máximo de puertas de enlace de red virtual |1 |número máximo de Hola de red virtual puertas de enlace (puertas de enlace de VPN) que puede crear una suscripción en esta ubicación. |
| Número máximo de conexiones de red |2 |número máximo de Hola de conexiones de red (punto a punto o sitio a sitio) que puede crear una suscripción a través de todas las puertas de enlace de red virtual en esta ubicación. |
| Número máximo de equilibradores de carga |50 |número máximo de Hola de equilibradores de carga que puede crear una suscripción en esta ubicación. |
| Nº máx. NIC |100 |número máximo de Hola de interfaces de red que puede crear una suscripción en esta ubicación. |
| Número máximo de grupos de seguridad de red |50 |número máximo de Hola de grupos de seguridad de red que puede crear una suscripción en esta ubicación. |

##<a name="view-an-existing-quota"></a>Visualización de una cuota existente
tooview una cuota existente, haga clic en **más servicios**>**proveedores de recursos** y seleccione servicio Hola qué Hola cuota desee tooview está asociado. A continuación, haga clic en **cuotas**y seleccione Hola cuota que desee tooview.
   > ![Ver una cuota existente](./media/azure-stack-setting-quota/ExistingQuota.PNG)
