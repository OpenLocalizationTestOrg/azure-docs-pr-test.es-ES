---
title: "máquinas virtuales de Azure del centro de seguridad y de Windows del aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de la seguridad de máquinas virtuales Windows en Azure con Azure Security Center."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Supervisión de la seguridad de máquinas virtuales mediante Azure Security Center

Azure Security Center puede ayudarle a conocer mejor los procedimientos de seguridad de los recursos de Azure. Security Center ofrece una supervisión integrada de la seguridad. que puede detectar las amenazas que podrían pasar desapercibidas. En este tutorial, aprenderá no solo a usar Azure Security Center, sino también a:
 
> [!div class="checklist"]
> * Configuración de una recolección de datos
> * Configurar directivas de seguridad
> * Ver y corregir problemas de estado de la configuración
> * Revisar las amenazas que se detecten  

## <a name="security-center-overview"></a>Introducción a Security Center

Security Center identifica posibles problemas de configuración de máquinas virtuales (VM) y amenazas de seguridad dirigidas. Aquí se incluyen las máquinas virtuales que no tienen grupos de seguridad de red, los discos sin cifrar y ataques de RDP por fuerza bruta. Hola información se muestra en el panel del centro de seguridad de hello en gráficos de fácil de leer.

tooaccess Hola panel del centro de seguridad, en hello portal de Azure, en el menú de hello, seleccione **centro de seguridad**. En el panel de hello, puede ver el estado de seguridad de Hola de su entorno de Azure, buscar un recuento de las recomendaciones actuales y ver Hola el estado actual de las alertas de amenaza. Puede expandir cada toosee de alto nivel gráfico más detalle.

![Panel de Security Center](./media/tutorial-azure-security/asc-dash.png)

Centro de seguridad va más allá de las recomendaciones del tooprovide de detección de datos para los problemas que detecta. Por ejemplo, si se implementa una máquina virtual sin un grupo de seguridad de red conectado, Security Center mostrará una recomendación con los pasos que se pueden dar para aplicarla. Obtener la corrección automatizada sin dejar el contexto de hello del centro de seguridad.  

![Recomendaciones](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>Configuración de una recolección de datos

Antes de que pueda obtener visibilidad en las configuraciones de seguridad de máquina virtual, deberá tooset la recopilación de datos del centro de seguridad. Esto implica activar la recopilación de datos y crear una cuenta de almacenamiento de Azure toohold recopilan datos. 

1. En el panel del centro de seguridad de hello, haga clic en **directiva de seguridad**y, a continuación, seleccione la suscripción. 
2. En **Recopilación de datos**, seleccione **Activado**.
3. Seleccione una cuenta de almacenamiento, toocreate **elegir una cuenta de almacenamiento**. Después, seleccione **Aceptar**.
4. En hello **directiva de seguridad** hoja, seleccione **guardar**. 

agente de recopilación de datos de Hello centro de seguridad se instala en todas las máquinas virtuales y empiece la recopilación de datos. 

## <a name="set-up-a-security-policy"></a>Configuración de una directiva de seguridad

Las directivas de seguridad son elementos de Hola de toodefine usado para el que el centro de seguridad recopila los datos y hace recomendaciones. Puede aplicar toodifferent conjuntos de directivas de seguridad diferentes de recursos de Azure. Aunque de forma predeterminada los recursos de Azure se evalúan con respecto a todos los elementos de la directiva, es posible desactivar elementos individuales de la directiva tanto para todos los recursos de Azure como para un solo grupo de recursos. Para más información acerca de las directivas de seguridad de Security Center, consulte [Establecimiento de directivas de seguridad en Azure Security Center](../../security-center/security-center-policies.md). 

tooset una directiva de seguridad para todos los recursos de Azure:

1. En el panel del centro de seguridad de hello, seleccione **directiva de seguridad**y, a continuación, seleccione la suscripción.
2. Seleccione **Prevention policy** (Directiva de prevención).
3. Activar o desactivar elementos de directiva que desea tooapply tooall recursos de Azure.
4. Cuando haya terminado de seleccionar la configuración, haga clic en **Aceptar**.
5. En hello **directiva de seguridad** hoja, seleccione **guardar**. 

tooset una directiva para un grupo de recursos específico:

1. En el panel del centro de seguridad de hello, seleccione **directiva de seguridad**y, a continuación, seleccione un grupo de recursos.
2. Seleccione **Prevention policy** (Directiva de prevención).
3. Activar o desactivar elementos de directiva que desea que el grupo de recursos de tooapply toohello.
4. En **INHERITANCE** (HERENCIA), seleccione **Unique** (Único).
5. Cuando haya terminado de seleccionar la configuración, haga clic en **Aceptar**.
6. En hello **directiva de seguridad** hoja, seleccione **guardar**.  

En esta página también se puede desactivar la recopilación de datos de un grupo de recursos concreto.

En el siguiente ejemplo de Hola, se ha creado una directiva única para un grupo de recursos denominado *myResoureGroup*. En esta directiva, se han desactivado las recomendaciones tanto para el cifrado de disco como para el Firewall de aplicaciones web.

![Directiva única](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>Visualización del estado de configuración de una máquina virtual

Después de que ha activado la recopilación de datos y establecer una directiva de seguridad, el centro de seguridad empieza a las recomendaciones y tooprovide alertas. Tal y como se implementan máquinas virtuales, se instala el agente de recopilación de datos de Hola. Centro de seguridad, a continuación, se rellena con datos de hello nuevas máquinas virtuales. Para obtener información detallada acerca del estado de configuración de las máquinas virtuales, consulte [Protección de las máquinas virtuales en Azure Security Center](../../security-center/security-center-virtual-machine-recommendations.md). 

Tal y como se recopilan los datos, se agrega el estado de los recursos Hola para cada máquina virtual y los recursos relacionados de Azure. se muestra información de Hello en un gráfico de fácil de leer. 

estado de los recursos tooview:

1.  En el panel del centro de seguridad de hello, en **estado de seguridad del recurso**, seleccione **proceso**. 
2.  En hello **proceso** hoja, seleccione **máquinas virtuales**. Esta vista proporciona un resumen del estado de configuración de Hola para todas las máquinas virtuales.

![Estado de Compute](./media/tutorial-azure-security/compute-health.png)

toosee todas las recomendaciones para una máquina virtual, seleccione Hola máquina virtual. Recomendaciones y la corrección se tratan con más detalle en la siguiente sección de Hola de este tutorial.

## <a name="remediate-configuration-issues"></a>Corrección de los problemas de configuración

Después de que el centro de seguridad comience toopopulate con datos de configuración, las recomendaciones se realizan en función de directiva de seguridad de hello que configurar. Por ejemplo, si se configuró una máquina virtual sin un grupo de seguridad de red asociados, una actuación toocreate uno. 

toosee una lista de todas las recomendaciones: 

1. En el panel del centro de seguridad de hello, seleccione **recomendaciones**.
2. Seleccione una recomendación concreta. Aparece una lista de todos los recursos para el que se aplica la recomendación de Hola.
3. tooapply una recomendación, seleccione un recurso concreto. 
4. Siga las instrucciones de Hola de pasos de corrección. 

En muchos casos, el centro de seguridad proporciona procesables pasos que puede seguir una recomendación tooaddress sin abandonar el centro de seguridad. En el siguiente ejemplo de Hola, centro de seguridad detecta un grupo de seguridad de red que tenga una regla de entrada sin restricciones. En la página de la recomendación de hello, puede seleccionar hello **editar reglas de entrada** botón. aparece en la interfaz de usuario que es necesario toomodify Hola regla Hola. 

![Recomendaciones](./media/tutorial-azure-security/remediation.png)

A medida que se corrigen las recomendaciones, se marcan como resueltas. 

## <a name="view-detected-threats"></a>Visualización de amenazas detectadas

Además, tooresource recomendaciones para la configuración, el centro de seguridad muestra las alertas de detección de amenazas. característica de alertas de seguridad de Hello agrega los datos recopilados de cada máquina virtual, registros de red de Azure y socios conectados soluciones toodetect amenazas de seguridad en recursos de Azure. Para más información acerca de las funcionalidades de detección de amenazas de Security Center, consulte [Funcionalidades de detección de Azure Security Center](../../security-center/security-center-detection-capabilities.md).

característica de alertas de seguridad de Hello requiere precios toobe capa aumentado desde el centro de seguridad de hello *libre* demasiado*estándar*. 30 días **evaluación gratuita** está disponible cuando se mueve toothis mayor nivel de precios. 

nivel de precios de Hola toochange:  

1. En el panel del centro de seguridad de hello, haga clic en **directiva de seguridad**y, a continuación, seleccione la suscripción.
2. Seleccione **Plan de tarifa**.
3. Seleccione el nuevo nivel de hello y, a continuación, seleccione **seleccione**.
4. En hello **directiva de seguridad** hoja, seleccione **guardar**. 

Después de cambiar nivel de precios de hello, gráfico de alertas de seguridad de hello comienza toopopulate cuando se detectan amenazas de seguridad.

![Alertas de seguridad](./media/tutorial-azure-security/security-alerts.png)

Seleccione un alerta tooview la información. Por ejemplo, puede ver una descripción de la amenaza de hello, hora de detección de hello, todos los intentos de amenaza y Hola corrección recomendada. En el siguiente ejemplo de Hola, se detectó un ataque por fuerza bruta RDP con 294 intentos fallidos de RDP. Se proporciona una corrección recomendada.

![Ataque de RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configurará Azure Security Center y, luego, revisó las máquinas virtuales de Security Center. Ha aprendido a:

> [!div class="checklist"]
> * Configuración de una recolección de datos
> * Configurar directivas de seguridad
> * Ver y corregir problemas de estado de la configuración
> * Revisar las amenazas que se detecten

Avanzar toohello siguiente tutorial toolearn cómo toocreate un CD de elemento de configuración de canalización con Visual Studio Team Services y una VM de Windows que se ejecuta IIS.

> [!div class="nextstepaction"]
> [Canalización de CI/CD de Visual Studio Team Services](./tutorial-vsts-iis-cicd.md)
