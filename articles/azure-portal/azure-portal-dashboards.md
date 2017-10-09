---
title: aaaCreate y compartir los paneles del portal Azure | Documentos de Microsoft
description: "Este artículo explica cómo toocreate y editar paneles en Hola portal de Azure."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>Crear y compartir paneles en hello portal de Azure
Puede crear varios paneles y compartirlos con otras personas que tienen acceso tooyour Azure suscripciones.  En este artículo se lleva a cabo conceptos básicos de Hola de crear, modificar, publicar y administrar el acceso toodashboards.

## <a name="create-a-dashboard"></a>Creación de un panel
toocreate un panel, seleccione hello **nuevo panel** botón siguiente toohello actual del nombre del panel.  

![crear panel](./media/azure-portal-dashboards/new-dashboard.png)

Esta acción crea un panel nuevo, vacío y privado, y activa el modo de personalización, donde puede asignar un nombre al panel y agregar o reorganizar los iconos.  En este modo, Hola contraíble icono Galería toma a través del menú de navegación izquierdo de Hola.  Hello icono galería permite buscar iconos para los recursos de Azure de varias maneras: se puede examinar [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), por tipo de recurso, por [etiqueta](../azure-resource-manager/resource-group-using-tags.md), o busque el recurso por su nombre.  

![personalizar panel](./media/azure-portal-dashboards/customize-dashboard.png)

Agregar iconos arrastrándolos y colocándolos en la superficie del panel de hello siempre que lo desee.

Hay una nueva categoría denominada **General** para los iconos que no están asociados a ningún recurso concreto.  En este ejemplo, anclar mosaico de marcado de Hola.  Utilice este panel de icono tooadd tooyour contenido personalizado.  icono Hello admite texto sin formato, [sintaxis de Markdown](https://daringfireball.net/projects/markdown/syntax)y un conjunto limitado de HTML.  (Por motivos de seguridad, no puede hacer cosas como insertar `<script>` etiquetas o uso de ciertos elementos de estilo de CSS que pueden interferir con el portal de Hola.) 

![agregar Markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>Edición de paneles
Después de crear el panel, puede anclar iconos desde la Galería de mosaico de Hola o representación de icono de Hola de hojas. Vamos a anclar representación Hola de nuestro grupo de recursos. O bien, puede anclar al examinar hello, o de hoja de grupo de recursos de Hola. Ambos métodos tienen como resultado fijar la representación en forma de mosaico Hola Hola del grupo de recursos.

![Toodashboard de PIN](./media/azure-portal-dashboards/pin-to-dashboard.png)

Después de anclar elemento hello, aparece en el panel.

![ver panel](./media/azure-portal-dashboards/view-dashboard.png)

Ahora que tenemos un icono de marcado y un panel de toohello anclados del grupo de recursos, podemos cambiar el tamaño y reorganizar los mosaicos de hello en un diseño más adecuado.

Al mantener el mouse y seleccionando "..." o haciendo doble clic en un icono puede ver todos los comandos contextuales de Hola para ese icono. De forma predeterminada, hay dos elementos:

1. **Desanclar del panel** : quita Hola icono de panel de Hola
2. **Personalizar** : se activa el modo de personalización.

![personalizar icono](./media/azure-portal-dashboards/customize-tile.png)

Al seleccionar Personalizar, puede cambiar el tamaño de los iconos y reordenarlos. tooresize un icono, seleccione Hola nuevo tamaño del menú contextual de hello, como se muestra en hello después de la imagen.

![cambiar tamaño del icono](./media/azure-portal-dashboards/resize-tile.png)

O bien, si el icono de hello es compatible con cualquier tamaño, puede arrastrar Hola inferior derecho toohello deseado de tamaño de las esquinas.

![cambiar tamaño del icono](./media/azure-portal-dashboards/resize-corner.png)

Después de cambiar el tamaño de iconos, vea el panel de Hola.

![ver icono](./media/azure-portal-dashboards/view-tile.png)

Una vez haya terminado de personalizar un panel, simplemente seleccione hello **realiza personalizar** tooexit en el modo personalizar o pulse el botón derecho y seleccione **realiza personalizar** desde el menú contextual de Hola.

## <a name="publish-a-dashboard-and-manage-access-control"></a>Publicación de un panel y administración del control de acceso
Cuando se crea un panel, es privado de forma predeterminada, lo que significa que es Hola única persona que pueda ver los datos.  toomake se tooothers visibles, usar hello **recurso compartido** Hola de botón que aparece junto a otros comandos de panel.

![compartir panel](./media/azure-portal-dashboards/share-dashboard.png)

Se le preguntará toochoose en que un grupo de recursos y suscripción para su toobe panel publicado. tooseamlessly integrar paneles en el ecosistema de hello, hemos implementado los paneles compartidos como recursos de Azure (por lo que no se puede compartir escribiendo una dirección de correo electrónico).  Información de toohello de acceso mostrada por la mayoría de los iconos de hello en el portal de Hola se rigen por [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md). Desde una perspectiva de control de acceso, los paneles compartidos no son distintos de una máquina virtual o de una cuenta de almacenamiento.  

Supongamos que tiene una suscripción de Azure y los miembros del equipo se han asignado los roles de Hola de **propietario**, **colaborador**, o **lector** de suscripción de Hola.  Los usuarios que son propietarios o colaboradores son pueda toolist, ver, crear, modificar o eliminar paneles dentro de esa suscripción.  Los usuarios que son los lectores son capaz de toolist y ver los paneles, pero no pueden modificar ni eliminarlos.  Los usuarios con acceso de lectura son panel compartido del tooa toomake capaz de ediciones locales, pero son toopublish no se puede esos server toohello atrás de cambios.  Sin embargo, puede hacer una copia privada de panel de Hola para su propio uso.  Como siempre, iconos individuales en el panel de Hola aplican sus propias reglas de control de acceso basadas en corresponden a los recursos Hola.  

Para mayor comodidad, portal hello de la publicación guías de experiencia que hacia un patrón donde colocar paneles en un grupo de recursos denominado **paneles**.  

![publicar panel](./media/azure-portal-dashboards/publish-dashboard.png)

También puede elegir toopublish un panel tooa determinado grupo de recursos.  control de acceso de Hola para ese panel coincide con el control de acceso de Hola Hola para grupo de recursos.  Los usuarios que pueden administrar recursos de hello en ese grupo de recursos también tienen acceso toohello paneles.

![publicar panel tooresource grupo](./media/azure-portal-dashboards/publish-to-resource-group.png)

Una vez publicado el panel, Hola **compartir + acceso** se actualice y muestran información sobre el panel publicado hello, incluido un panel de toohello de acceso de usuario de vínculo toomanage panel de control.  Este vínculo inicia Hola Role Based Access Control hoja usa toomanage acceso estándar para los recursos de Azure.  Puede regresar siempre toothis vista seleccionando **recurso compartido**.

![administrar control de acceso](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>Pasos siguientes
* toomanage recursos, consulte [recursos de Azure administrar a través del portal de](../azure-resource-manager/resource-group-portal.md).
* toodeploy recursos, consulte [implementar los recursos con plantillas de administrador de recursos y el portal de Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

