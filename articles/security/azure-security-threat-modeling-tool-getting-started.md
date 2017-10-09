---
title: aaaGetting iniciado - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
description: "Se trata de una descripción más profunda resaltado Hola herramienta de modelado de amenazas en acción."
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
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Introducción a la herramienta de modelado de amenazas de Hola

equipo de nube y herramientas de seguridad de la empresa de Hello publicó Hola vista previa de herramienta de modelado de amenazas anteriormente este año como una segunda  **[haga clic en para descargar](https://aka.ms/tmtpreview)**. cambio de Hello en el mecanismo de entrega nos permite toopush hello más recientes mejoras y correcciones de errores toocustomers cada vez que abran herramienta hello, lo que sea más fácil toomaintain y uso.
Este artículo le guiará por el proceso de Hola de cómo empezar a usar el enfoque de modelado de amenazas de SDL Microsoft hello y muestra cómo los modelos de amenazas excepcionales de toouse Hola herramienta toodevelop como una red troncal del proceso de seguridad.

En este artículo se basa en los conocimientos de enfoque de modelado de amenazas SDL Hola. Para una revisión rápida, consulte demasiado**[aplicaciones Web de modelado de amenazas](https://msdn.microsoft.com/library/ms978516.aspx)**  y una versión archivada de  **[Hola ayudan a solucionar errores de seguridad mediante enfoque STRIDE](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)**  Artículo de MSDN se publica en el año 2006.

resumir tooquickly, enfoque de hello implica la creación de un diagrama, identificar amenazas, corregirlos y validar cada mitigación. Este es un diagrama que esquematiza este proceso:

![Proceso SDL](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>Iniciar el proceso de modelado de amenazas de Hola

Al iniciar Hola herramienta de modelado de amenazas, observará algunas cosas, como se muestra en la imagen de hello:

![Página de inicio en blanco](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>Sección del modelo de amenaza

| Componente                                   | Detalles                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Botón de comentarios, sugerencias y problemas** | Toma Hola  **[foro de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)**  todo lo SDL. Proporciona un tooread de oportunidad por lo que otros usuarios hacen, junto con soluciones alternativas y recomendaciones. Si todavía no encuentra lo está buscando, enviar por correo electrónico tmtextsupport@microsoft.com para nuestro toohelp del equipo de soporte técnico                                                                                                                            |
| **Creación de un modelo**                          | Abre un lienzo en blanco para toodraw el diagrama. Asegúrese de tooselect seguro de qué plantilla desea toouse para el modelo                                                                                                                                                                                                                                                                                                                                                                       |
| **Plantilla para los modelos nuevos**                 | Debe seleccionar qué toouse plantilla antes de crear un modelo. La plantilla principal es hello plantilla de modelo de amenaza de Azure, que contiene galerías de símbolos específicas de Azure, las amenazas y mitigaciones. Para los modelos genéricos, seleccione Hola SDL TM Knowledge Base desde el menú desplegable de Hola. Desea toocreate su propia plantilla o enviar una nueva contraseña para todos los usuarios? Visite nuestro  **[plantilla repositorio](https://github.com/Microsoft/threat-modeling-templates)**  GitHub Page toolearn más                              |
| **Abrir un modelo**                            | <p>Se abren los modelos de amenazas guardados previamente. característica de modelos abierto recientemente Hello es fantástico si necesita tooopen los archivos más recientes. Cuando mantenga el mouse sobre la selección de hello, encontrará 2 formas tooopen modelos:</p><p><ul><li>Abrir desde este equipo: modo clásico de abrir un archivo usando el almacenamiento local</li><li>Abrir desde OneDrive – equipos pueden usar carpetas en OneDrive toosave y compartir sus modelos de amenazas en una sola ubicación toohelp aumento de productividad y colaboración para</li></ul></p> |
| **Guía de introducción**                   | Se abre hello  **[herramienta de modelado de amenazas de Microsoft](./azure-security-threat-modeling-tool.md)**  página principal                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>Sección de plantilla

| Componente               | Detalles                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Crear nueva plantilla** | Se abre una plantilla en blanco para toobuild en. A menos que tenga amplios conocimientos en la creación de plantillas desde el principio, le recomendamos que toobuild de las existentes |
| **Abrir plantilla**       | Se abre existente plantillas para usted toomake cambios demasiado                                                                                                             |

equipo de la herramienta de modelado de amenazas de Hello está trabajando constantemente experiencia y la funcionalidad de la herramienta de tooimprove. Algunos cambios menores pueden tener lugar durante Hola de año de hello, pero todos los cambios principales requieren guía Hola de escribir de nuevo. Consulte tooit a menudo tooensure obtener anuncios de Hola más recientes.

## <a name="building-a-model"></a>Generación de un modelo

En esta sección, seguimos a:

- Cristina (programadora)
- Ricardo (administrador de programas) y
- Ashish (evaluador)

Están pasando por proceso de hello sobre el desarrollo de su primer modelo de amenazas.

> Ricardo: Hola Cristina, trabajé en el diagrama del modelo de amenaza de Hola y deseaba toomake seguro tenemos detalles Hola derecho. ¿Podrías ayudarme a comprobarlo?
> Cristina: Por supuesto. Vamos a echar un vistazo.
> Ricardo abre la herramienta de Hola y comparte la pantalla con Cristina.

![Modelo de amenaza básica](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina: Bien, parece sencillo, pero ¿puedes guiarme para comprobarlo?
> Ricardo: Claro. Este es el desglose de hello:
> - El usuario se dibuja como una entidad externa: un cuadrado
> - Está enviando al servidor Web de comandos tooour: círculo Hola
> - servidor Web de Hello es consultar una base de datos (dos líneas paralelas)

Lo que Ricardo ha mostrado a Cristina es un DFD, abreviatura de  **[diagrama de flujo de datos](https://en.wikipedia.org/wiki/Data_flow_diagram)**. Hola herramienta de modelado de amenazas permite límites de confianza de los usuarios toospecify, indicados por líneas de puntos de hello rojo, tooshow donde son distintas entidades en el control. Por ejemplo, los administradores de TI requieren un sistema de Active Directory para la autenticación, por lo que Hola Active Directory está fuera de su control.

> Cristina: Busca toome derecho. ¿Qué amenazas Hola?
> Ricardo: Permíteme que te lo muestre.

## <a name="analyzing-threats"></a>Análisis de las amenazas

Una vez que el usuario hace clic en la vista de análisis de Hola de selección de menú de icono de hello (archivo con lupa), que se toma tooa lista de amenazas generado hello herramienta de modelado de amenazas se encuentra en función de la plantilla predeterminada de hello, que utiliza el método SDL Hola denominado  **[ STRIDE (suplantación de identidad, manipulación, revelación de información, denegación de servicio y elevación de privilegios)](https://en.wikipedia.org/wiki/STRIDE_(security))**. idea de Hello es que el software proviene en un conjunto de predicción de amenazas, que se puede encontrar el uso de estas 6 categorías.

Este enfoque es como la protección de su casa asegurándose de cada puerta y ventana tiene un mecanismo de bloqueo en su lugar antes de agregar un sistema de alarma o adherencias después ladrón Hola.

![Amenazas básicas](./media/azure-security-threat-modeling-tool/basicthreats.png)

Ricardo comienza seleccionando el primer elemento en la lista de Hola de Hola. Esto es lo que sucede:

En primer lugar, se mejora la interacción de hello entre dos galerías de símbolos de Hola

![Interacción](./media/azure-security-threat-modeling-tool/interaction.png)

Segundo, información adicional acerca de la amenaza de hello aparece en la ventana de propiedades de la amenaza de Hola

![Información de interacción](./media/azure-security-threat-modeling-tool/interactioninfo.png)

amenaza Hola genera le ayudará a comprender los posibles errores de diseño. categorización de Hello STRIDE le da una idea de los vectores de ataque potencial, mientras Hola descripción adicional le indica exactamente qué ha incorrecto, junto con posibles toomitigate de maneras. Puede utilizar notas de toowrite de los campos editables en detalles de la justificación de Hola o cambiar las clasificaciones de prioridad dependiendo de la barra de error de su organización.

Plantillas de Azure tienen los usuarios de toohelp detalles adicionales entender no solo cuál es el problema, sino también cómo toofix, mediante la adición de documentación específica de tooAzure descripciones, ejemplos e hipervínculos.

Descripción de Hello lo hizo comprender la importancia de Hola de agregar los usuarios un tooprevent de mecanismo de autenticación de suplantación, revelar Hola primera amenaza toobe ha trabajado. Unos minutos en conversaciones de hello con Cristina, que comprendan la importancia de saludo de la implementación del control de acceso y roles. Ricardo rellena algunos toomake notas rápidas se implementaban seguro.

Como Ricardo se incluyó en las amenazas de hello en la divulgación de información, se dio cuenta de plan de control de acceso de hello requiere algunas cuentas de solo lectura para auditoría y generación de informes. Preguntado si debe ser una amenaza para la nueva, pero Hola mitigaciones estaban Hola iguales, por lo que indica amenaza hello en consecuencia.
También a pensar acerca de la divulgación de información en un poco más y percibe que las cintas de copia de seguridad de hello iba tooneed cifrado, un trabajo para el equipo de operaciones de Hola.

Amenazas de diseño de toohello no es aplicable de vencimiento tooexisting mitigaciones o seguridad garantiza puede cambiarse demasiado "No aplicable" desde Hola estado de lista desplegable. Hay otras tres opciones: no iniciado: selección predeterminada, es necesario investigación: agotado toofollow en elementos y mitigado: una vez que está totalmente en funcionamiento.

## <a name="reports--sharing"></a>Informes y uso compartido

Una vez Ricardo pasa a través de la lista de hello con Cristina y agrega notas importantes, mitigaciones/justificación, prioridad y el estado cambia, selecciona Informes -> Crear informe completo -> Guardar el informe, que imprime un "nice" de informes para él toogo a través con se implementa el trabajo de compañeros tooensure Hola seguridad apropiada.

![Información de interacción](./media/azure-security-threat-modeling-tool/report.png)

Si Ricardo desea archivo de hello tooshare en su lugar, puede hacerlo fácilmente guardándolo en la cuenta de OneDrive de su organización. Una vez que lo hace, puede copiar vínculo de documento de Hola y compartirlo con sus compañeros. 

## <a name="threat-modeling-meetings"></a>Herramienta de modelado de amenazas

Cuando Ricardo envía su colega de toohis de modelo de amenaza con OneDrive, Ashish, evaluador hello, se underwhelmed. Parecía que Ricardo y Cristina habían olvidado algunos casos importantes más complejos, que podían verse comprometidos fácilmente. Su escepticismo es los modelos de toothreat de un complemento.

En este escenario, una vez Ashish ha asumido modelo de amenazas de hello, llama para dos de las reuniones de modelado de amenazas: toosynchronize de reuniones en proceso de Hola y recorrido a través de los diagramas de hello y, a continuación, una segunda reunión de revisión de amenaza y cierre de sesión.

En la primera reunión hello, Ashish había dedicado a recorrer todo el mundo a través del proceso de modelado de amenazas SDL Hola de 10 minutos. A continuación, a había levantado diagrama del modelo de amenaza de Hola y explicar detalladamente inició. Tras cinco minutos, se había identificado un importante componente que faltaba.

Unos minutos más adelante, Ashish y Ricardo entraron en una descripción detallada de cómo se creó el servidor Web de Hola. No era ideales Hola para una tooproceed de reunión, pero todos los usuarios finalmente acordado que detectar pronto discrepancia de hello iba toosave que su tiempo en el futuro de Hola.

Segunda reunión, equipo Hola pasará a través de las amenazas de hello, trata algunos tooaddress formas firmado y usarlas en hello desactivado en el modelo de amenazas de Hola. Se protegen documento hello en el control de origen y continúa con el desarrollo.

## <a name="thinking-about-assets"></a>Evaluación de los recursos

Algunos lectores que hayan modelado una amenaza pueden darse cuenta de que no hablaron sobre todos los recursos. Hemos descubierto que muchos de los ingenieros de software comprenden mejor el tema que entiendan el concepto de Hola de activos y los activos de un atacante podrían estar interesado en su software.

Si se va a toothreat una casa del modelo, puede comenzar por pensar acerca de su familias, irreemplazables fotografías o ilustraciones valiosos. Quizás podría empezar por pensar en el sistema de seguridad actual de Hola y que pueden provocar errores. O puede comenzar teniendo en cuenta Hola características físicas, como grupo de Hola o porche frontal Hola. Estas son análogo toothinking sobre activos, los atacantes o diseño de software. Cualquiera de estos tres enfoques funcionan.

modelado de Hello enfoque toothreat que hemos aquí expuesta es mucho más sencillo que lo que Microsoft ha hecho en hello anterior. Encontramos que el enfoque de diseño de software de hello funciona bien para muchos equipos. Esperamos que sea el caso del suyo.

## <a name="next-steps"></a>Pasos siguientes

Envíe sus preguntas, comentarios y preocupaciones tootmtextsupport@microsoft.com. **[Descargar](https://aka.ms/tmtpreview)**  tooget de la herramienta de modelado de amenazas de hello iniciado.
