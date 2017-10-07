---
title: "asociados de aaaCreate para mensajes de negocio a negocio (B2B): las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooyour integración de tooadd asociados cuenta con hello paquete de integración empresarial y las aplicaciones lógicas"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a>Incorporación o actualización de asociados de contratos de negocio a negocio del flujo de trabajo

Los asociados son entidades que participan en transacciones de negocio a negocio (B2B) e intercambian mensajes entre ellos. Antes de poder crear asociados que le representen a usted y a otra organización en estas transacciones, debe compartir la información que identifica y valida los mensajes enviados por cada uno. Después de que analizan estos detalles y toostart preparado su relación de negocios, puede crear socios en su toorepresent de cuenta de integración que ambos.

## <a name="what-roles-do-partners-have-in-your-integration-account"></a>¿Qué roles tienen los asociados en la cuenta de integración?

toodefine obtener más información acerca de los mensajes de Hola intercambiados entre los asociados, crear acuerdos entre los socios. Sin embargo, antes de poder crear un acuerdo, debe haber agregado cuenta de integración de tooyour de al menos dos socios comerciales. Su organización debe formar parte del contrato de Hola Hola **socio del host**. Hola otro asociado o **socio invitado** representa Hola organización que intercambia mensajes con su organización. Socio invitado de Hello puede ser otra compañía, o incluso un departamento de su propia organización.

Después de agregar a estos asociados, puede crear un contrato.

Recepción y configuración de envío se orientan de hello punto de vista de hello Hosted asociado. Por ejemplo, hello configuración de recepción de un acuerdo determinar cómo asociado Hola hospedado recibe los mensajes enviados desde un socio invitado. Del mismo modo, configuración de envío Hola acuerdo Hola indica cómo asociado Hola hospedado envía a socio invitado de toohello de mensajes.

## <a name="how-toocreate-a-partner"></a>¿Cómo toocreate un socio?

1. Hola portal de Azure, seleccione **examinar**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. En el cuadro de búsqueda del filtro de hello, escriba **integración**, a continuación, seleccione **cuentas de integración** en la lista de resultados de Hola.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Seleccione la cuenta de integración de Hola donde desea tooadd sus socios.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Seleccione hello **socios** icono.

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. En la hoja de socios de hello, elija **agregar**.

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. Escriba un nombre para el asociado y, a continuación, seleccione un **Calificador**. Por último, especifique un **valor** toohelp identificar documentos que acompañan a las aplicaciones.

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. progreso de hello toosee para el proceso de creación de socios comerciales, seleccione hello *campana* icono de notificación.

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. tooconfirm que los socios nueva estaban correctamente agregado, seleccione hello **socios** icono.

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    Después de seleccionar el icono de socios de hello, también verá recién agregados asociados en la hoja de socios de Hola.

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a>Cómo los partners de tooedit existente en su cuenta de integración

1. Seleccione hello **socios** icono.
2. Después de abre la hoja de socios de hello, seleccione a socio comercial de hello desea tooedit.
3. En hello **actualización asociado** icono, realice los cambios.
4. Cuando haya terminado, elija **guardar**, o toocancel los cambios, seleccione **descartar**.

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a>¿Cómo toodelete un socio

1. Seleccione hello **socios** icono.
2. Después de abre la hoja de socio comercial de hello, seleccione a socio comercial de Hola que desea toodelete.
3. Elija **Eliminar**.

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre los contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  

