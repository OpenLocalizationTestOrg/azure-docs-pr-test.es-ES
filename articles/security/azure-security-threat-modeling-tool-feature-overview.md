---
title: aaaMicrosoft herramienta de modelado de amenazas - Azure | Documentos de Microsoft
description: "Obtenga información acerca de todas las características de hello disponibles en hello herramienta de modelado de amenazas"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Información general de las características de Threat Modeling Tool

Nos complace que eligió hello toouse herramienta de modelado de amenazas para sus necesidades de modelado de amenazas. Si lo ha hecho, visite  **[Introducción a la herramienta de modelado de amenazas de hello](./azure-security-threat-modeling-tool-getting-started.md)**  conceptos básicos de hello toolearn.

> Nuestra herramienta se actualiza con frecuencia, por lo que compruebe esta guía a menudo toosee nuestras características y mejoras más recientes.

Al hacer clic en el botón de "Crear un nuevo modelo de" Hola, abre una página de inicio en blanco, una imagen toohello similar a continuación:

![Página de inicio en blanco](./media/azure-security-threat-modeling-tool/tmtstart.png)

Utilizando el modelo de amenazas de hello creados por nuestro equipo de hello  **[Introducción](./azure-security-threat-modeling-tool-getting-started.md)**  ejemplo, vamos a desproteger todas las características de hello disponibles en la herramienta de hello hoy en día.

![Modelo de amenaza básica](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Navegación

Antes de profundizar en las características integradas de hello, repasemos componentes principales de Hola de herramienta Hola

### <a name="menu-items"></a>Elementos de menú

experiencia de Hello debe ser productos de Microsoft tooother similares. Vamos a empezar, vaya a través de los elementos de menú de nivel superior de hello:

![Elementos de menú](./media/azure-security-threat-modeling-tool/menuitems.png)

| Etiqueta                               | Detalles      |
| --------------------------------------- | ------------ |
| **Archivo** | <ul><li>Abrir, guardar y cerrar archivos</li><li>Iniciar y cerrar sesión en cuentas de OneDrive</li><li>Compartir vínculos (Vista + Edición)</li><li>Ver información de archivo</li><li>Aplicar la nueva plantilla tooExisting modelos</li></ul> |
| **Edición** | Acciones de deshacer/rehacer, además de copiar, pegar y eliminar |
| **Vista** | <ul><li>Cambiar entre las vistas **Análisis** y **Diseño**</li><li>Abrir las ventanas cerradas (por ejemplo, galerías de símbolos, propiedades de elementos y mensajes)</li><li>Restablecer la configuración de diseño toodefault.</li></ul> |
| **Diagrama** | Agregar o eliminar diagramas, y navegar a través de "pestañas" de diagramas |
| **Informes** | Crear tooshare de informes HTML con otras personas |
| **Ayuda** | Guía toohelp utilizar herramienta Hola |

iconos de Hello son accesos directos para los menús de nivel superior de hello:

| Icono                               | Detalles      |
| --------------------------------------- | ------------ |
| **Abrir** | Abre un nuevo archivo |
| **Guardar** | Guarda el archivo actual |
| **Diseño** | Entra en la vista de diseño, donde puede crear modelos |
| **Análisis** | Muestra las amenazas generadas y sus propiedades |
| **Agregar diagrama** | Agrega el nuevo diagrama (similar toonew fichas en Excel) |
| **Eliminar diagrama** | Elimina el diagrama actual |
| **Copiar/Cortar/Pegar** | Copia, corta o pega elementos |
| **Deshacer/Rehacer** | Deshace o rehace acciones |
| **Acercar/Alejar** | Amplía dentro y fuera de diagrama de Hola para obtener una mejor vista |
| **Comentarios** | Se abre Hola foro de MSDN |

### <a name="canvas"></a>Lienzo

espacio de Hola donde arrastrar y colocar elementos en. Arrastrar y colocar es más rápida de Hola y modelos de toobuild de manera más eficaces. También puede haga clic y seleccione del menú de hello, que agrega las versiones genéricas de los elementos de Hola que está usando, tal y como se muestra a continuación.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Eliminación de galería de símbolos de hello en el lienzo de Hola

![Colocación en el lienzo](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>Al hacer clic en la Galería de símbolos de Hola

![Propiedades del elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Galerías de símbolos

Donde puede encontrar todas las galerías de símbolos disponible toouse basado en plantilla Hola seleccionada. Si no encuentra los elementos adecuados de hello, intente usar otra plantilla o modificar una toofit sus necesidades. Por lo general, debe ser capaz de toofind una combinación de categorías como Hola que a continuación:

| Nombre de la galería de símbolos                               | Detalles      |
| --------------------------------------- | ------------ |
| **Proceso** | Aplicaciones, complementos de explorador, subprocesos, máquinas virtuales |
| **External Interactor** (Interactivo externo) | Proveedores de autenticación, exploradores, usuarios, aplicaciones web |
| **Almacén de datos** | Caché, almacenamiento, archivos de configuración, bases de datos, Registro |
| **Flujo de datos** | Binario, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Canalización con nombre, RPC/DCOM, SMB, UDP |
| **Trust Line/Border Boundary** (Línea de confianza/Línea de borde) | Redes corporativas, Internet, máquina, espacio aislado, modo Kernel/Usuario |

### <a name="notesmessages"></a>Notas/Mensajes

| Componente                               | Detalles      |
| --------------------------------------- | ------------ |
| **Mensajes** | Lógica de herramienta interna que alerta a los usuarios cada vez que hay un error, por ejemplo, cuando no hay flujos de datos entre los elementos |
| **Notas** | Notas manuales archivo toohello agregado por los equipos de ingeniería en su totalidad Hola diseño y proceso de revisión |

### <a name="element-properties"></a>Propiedades del elemento

Éstos varían según los elementos de hello seleccionados. Además de los límites de confianza, todos los demás elementos contienen tres selecciones generales:

| Propiedad de elemento                               | Detalles      |
| --------------------------------------- | ------------ |
| **Name** | Útil para asignar nombres a su toobe de procesos, almacenes, interactuadores y flujos reconocido con facilidad |
| **Out of Scope** (Fuera de ámbito) | Si se selecciona, el elemento de Hola se saca de matriz de generación de amenaza de hello (no recomendado) |
| **Reason for Out of Scope** (Motivo de elegir Fuera de ámbito) | Los usuarios de toolet de campo de justificación saben por qué se seleccionó fuera del ámbito |

Se cambian las propiedades de cada categoría de elemento. Haga clic en cada opciones disponibles de elemento tooinspect hello, o abra Hola plantilla toolearn más. Comencemos con características de Hola.

## <a name="welcome-screen"></a>Pantalla principal

pantalla de bienvenida de Hello es Hola primera cosa que verá cuando se abre la aplicación hello.

### <a name="open-a-model"></a>Abrir un modelo

Al mantener el mouse sobre el botón "Abrir un modelo", se muestran dos opciones ocultas: "Abrir desde este equipo" y "Abrir desde OneDrive". Hola abre por primera vez abrir archivo pantalla de bienvenida, mientras hello en segundo lugar le guiará por inicio de sesión de hello en proceso para OneDrive, permitiéndole toopick carpetas y archivos después de una autenticación correcta.

![Abrir modelo](./media/azure-security-threat-modeling-tool/openmodel.png)

![Abrir desde el equipo o desde OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Comentarios, sugerencias y problemas

Al seleccionar esta opción le permitirán toohello foros de MSDN para herramientas de SDL. Es un toocheck excelente manera a otras personas opinión acerca de la herramienta de hello, incluidas nuevas ideas y soluciones.

![Comentarios](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Vista de diseño

Cada vez que abra o cree un nuevo modelo, se le dirigirá toohello la vista de diseño.

### <a name="adding-elements"></a>Adición de elementos

Hay 2 formas tooadd elementos en la cuadrícula de hello:

- **Arrastrar y colocar** : arrastre Hola elemento deseado toohello cuadrícula, utilice la información adicional de hello elemento Propiedades tooprovide.
- **Haga clic en** : haga clic en cualquier parte en la cuadrícula de Hola y seleccione del menú desplegable de Hola. Una representación genérica de ese elemento aparecerá en la pantalla de bienvenida.

### <a name="connecting-elements"></a>Conexión de elementos

Hay 2 formas tooconnect elementos en la herramienta de hello:

- **Arrastrar y colocar** : arrastre cuadrícula de toohello de flujo de datos deseada de Hola y conectar ambos elementos correspondientes de toohello de extremos.
- **Haga clic en + MAYÚS** : haga clic en el primer elemento de hello (enviar datos), presione y mantenga presionada MAYÚS hello y, a continuación, segundo elemento de hello seleccione (recibir datos). Haga clic con el botón derecho y seleccione "Conectar". Si usa un flujo de datos bidireccional, orden de hello no es tan importante.

### <a name="properties"></a>Propiedades

Muestra todas las propiedades de Hola que pueden modificarse en galerías de símbolos de hello colocados en el diagrama de Hola. propiedades de hello toosee, haga clic en la Galería de símbolos de Hola y Hola se rellena en consecuencia. ejemplo de Hola siguiente se muestra antes y después de una galería de símbolos se arrastra hasta el diagrama de Hola de "base de datos":

#### <a name="before"></a>Antes

![Antes](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>Después

![Después](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>error de Hadoop

Si crea un modelo de amenazas y olvidarse de fluyen de datos de tooconnect tooelements, ventana de mensaje de Hola notifica tooact. Puede elegir tooignore lo o seguimiento Hola problema de instrucciones toofix Hola. 

![error de Hadoop](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Notas

Cambiar de fichas de tooNotes de mensajes permite tooadd notas tooyour diagrama toocapture todas sus ideas

## <a name="analysis-view"></a>Vista de análisis

Cuando haya finalizado de crear el diagrama, cambiar vista tooanalysis al toohello selecciones de menú superior y elegir la paleta de pintura de hello lupa siguiente toohello.

![Vista de análisis](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Selección de amenaza generada

Al hacer clic en una amenaza, puede sacar provecho de tres funciones únicas:

| Característica                               | Información      |
| --------------------------------------- | ------------ |
| **Indicador de leído** | <p>Amenaza ahora está marcada como lectura, que puede ayudarle fácilmente a realizar un seguimiento de elementos de hello que ha completado ya</p><p>![Indicador de leído o no leído](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Foco de interacción** | <p>Se resalta la interacción en el diagrama de Hola que pertenece la amenaza de toothat</p><p>![Foco de interacción](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **Thread Properties** (Propiedades de amenaza) | <p>Información adicional acerca de la amenaza de Hola se rellena en la ventana de propiedades de amenaza de Hola</p><p>![Thread Properties (Propiedades de amenaza)](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Priority change (Cambio de prioridad)

Nivel de prioridad de Hola de cada amenaza generado también se cambia su toomake de colores se tooidentify fácil amenazas de prioridad alta, Media y baja.

![Priority change (Cambio de prioridad)](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Campos modificables de las propiedades de amenaza

Tal como se muestra en la imagen de hello anterior, los usuarios pueden cambiar información Hola Hola herramienta generada un también agregar campos de toocertain de información, como la justificación. Estos campos son generados por la plantilla de hello, por lo que si necesita más información para cada amenaza, le recomienda toomake modificaciones.

![Thread Properties (Propiedades de amenaza)](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Informes

Una vez que haya terminado las prioridades cambiantes y actualización de Hola de estado de cada uno generado amenaza, puede guardar el archivo hello o imprimir un informe desde demasiado "informes" y, a continuación, "Crear informe completo." Se le preguntará tooname informe de Hola y cuando lo haga, debería ver algo similar imagen toohello siguiente:

![Informe](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Pasos siguientes

toocontribute una plantilla para la Comunidad de hello, vaya tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  página. **[Descargar](https://aka.ms/tmtpreview)**  Hola herramienta tooget comenzar hoy.
