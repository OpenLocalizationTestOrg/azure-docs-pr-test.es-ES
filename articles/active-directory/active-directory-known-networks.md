---
title: "Redes aaaKnown Hola portal de Azure clásico | Documentos de Microsoft"
description: "Al configurar redes conocidas, puede evitar tener direcciones IP que pertenecen a su organización incluido en hello inicios de sesión desde varias zonas geográficas y los inicios de sesión desde direcciones IP con informes de actividad sospechosa."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>Redes conocidas

> [!div class="op_single_selector"]
> * [Portal de Azure clásico](active-directory-known-networks.md)
> * [Portal de Azure](active-directory-known-networks-azure-portal.md)
> 
> 


Puede usar el acceso de Active Directory de Azure y visibilidad de toogain de informes de uso de integridad de Hola y seguridad del directorio de su organización. Con esta información, administradores de directorios pueden determinar mejor dónde puede haber posibles riesgos de seguridad para que se pueden planificar adecuadamente toomitigate esos riesgos.

Es posible que Hola "*inicios de sesión desde varias zonas geográficas*"y"*inicios de sesión desde direcciones IP con actividad sospechosa*" informes marca incorrectamente las direcciones IP que realmente pertenecen a su organización. 

Por ejemplo, esto puede ocurrir cuando: 

* Ha iniciado sesión un usuario en la oficina de Boston en forma remota tooyour centro de datos en San Francisco desencadenadores Hola informes "Inicios de sesión desde varias zonas geográficas" 
* Intenta usar un usuario de su organización toosign en varias veces una contraseña incorrecta desencadenadores donde aparece hello con informes de "Inicios de sesión desde direcciones IP con actividad sospechosa" 

informa de estos casos de la seguridad puede inducir a error de generación de tooprevent, debe agregar conocidos intervalos toohello lista de direcciones IP la dirección IP pública de su organización.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>intervalos de tooadd la dirección IP pública de su organización, lleve a cabo Hola pasos:

1. Inicio de sesión toohello [portal de administración de Azure](https://manage.windowsazure.com).

2. En el panel izquierdo de hello, haga clic en **Active Directory**. 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-01.png)

3. Hola **Directory** ficha, seleccione el directorio.

4. En el menú de hello en la parte superior de hello, haga clic en **configurar**. 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-02.png)

5. En la ficha configurar de hello, vaya demasiado**los intervalos de direcciones IP públicos de las organizaciones** 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-03.png)

6. Haga clic en **Agregar intervalos de direcciones IP conocidas**.

7. Agregar los intervalos de direcciones en el cuadro de diálogo de Hola que aparece y, a continuación, haga clic en botón de comprobación de hello cuando haya terminado. 

    ![Redes conocidas](./media/active-directory-known-networks/known-netwoks-04.png)

**Recursos adicionales:**

* [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md)
* [Inicios de sesión desde direcciones IP con actividad sospechosa](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Inicios de sesión desde varias ubicaciones geográficas](active-directory-reporting-sign-ins-from-multiple-geographies.md)

