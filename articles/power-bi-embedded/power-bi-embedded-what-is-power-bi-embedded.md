---
title: "¿aaaWhat es Microsoft Power BI Embedded?"
description: "Power BI Embedded permite toointegrate informes de Power BI en la web o aplicaciones móviles de forma que no deba soluciones personalizadas de toobuild."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>¿Qué es Microsoft Power BI Embedded?
Con **Power BI Embedded**, puede integrar informes de Power BI directamente en las aplicaciones web o móviles.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI Embedded es un **servicio de Azure** que permite a los ISV y experiencias de aplicación a los desarrolladores toosurface datos de Power BI dentro de sus aplicaciones. Como desarrollador, ha creado aplicaciones y esas aplicaciones tienen sus propios usuarios y un diferente conjunto de características. Esas aplicaciones también pueden ocurrir toohave algunos elementos de datos integrados, como gráficos e informes que ahora se pueden apagar por Microsoft Power BI Embedded. No es necesario un toouse de cuenta de Power BI la aplicación. Puede continuar toosign en aplicación tooyour igual que antes y ver e interactuar con hello experiencia de informes de Power BI sin necesidad de cualquier licencia adicional.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Licencias de Microsoft Power BI Embedded
Hola **Microsoft Power BI Embedded** modelo de uso, licencias de Power BI no es responsabilidad de hello del usuario final de Hola.  En su lugar, **sesiones** se adquieren por programador Hola de aplicación hello que consume objetos visuales de Hola y se encargan de suscripción toohello que pertenece a esos recursos. Puede encontrar información adicional en hello [página de precios](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Modelo conceptual de Microsoft Power BI Embedded

![](media/powerbi-embedded-whats-is/model.png)

Como cualquier otro servicio en Azure, los recursos de Power BI Embedded se aprovisionan mediante hello [API del Administrador de recursos de Azure](https://msdn.microsoft.com/library/mt712306.aspx). En este caso, es el recurso de Hola que se aprovisiona un **colección de área de trabajo de Power BI**.

## <a name="workspace-collection"></a>Colección de áreas de trabajo
A **colección de área de trabajo** es hello Azure contenedor de nivel superior para los recursos que contiene 0 o más **áreas de trabajo**.  A **área de trabajo** **colección** tiene todas las propiedades de Azure estándar hello, así como siguiente hello:

* **Las claves de acceso** – claves que se utilizan cuando se llama de forma segura Hola API de Power BI (descrito en una sección posterior).
* **Los usuarios** : colección de área de trabajo de Power BI Hola a los usuarios de Azure Active Directory (AAD) que tienen toomanage de derechos de administrador a través de Hola portal de Azure o la API del Administrador de recursos de Azure.
* **Región** : como parte del aprovisionamiento de un **colección de área de trabajo**, puede seleccionar una toobe región aprovisionado en. Para más información, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Área de trabajo
Un **área de trabajo** es un contenedor de contenido de Power BI, que puede incluir conjuntos de datos e informes. Un **área de trabajo** está vacío cuando se crea por primera vez. Podrá crear contenido con Power BI Desktop y va a implementar mediante programación hello PBIX en el área de trabajo con hello [API de importación de Power BI](https://msdn.microsoft.com/library/mt711504.aspx). También puede crear mediante programación un conjunto de datos y, después, crear informes en la aplicación, en lugar de usar Power BI Desktop.

## <a name="using-workspace-collections-and-workspaces"></a>Uso de colecciones de áreas de trabajo y áreas de trabajo
**Colecciones de área de trabajo** y **áreas de trabajo** son contenedores de contenido que se usan y se organizan en la forma que mejor se adapte a diseño Hola de aplicación Hola va a compilar. Habrá muchas maneras diferentes que puede organizar el contenido de hello dentro de ellos. Puede elegir tooput todo el contenido dentro de un área de trabajo y, a continuación, toofurther de tokens de aplicación de uso posterior subdividir contenido Hola entre sus clientes. También puede elegir tooput todos sus clientes en áreas de trabajo independientes para que no haya cierta separación entre ellos. O bien, puede elegir los usuarios de tooorganize por región, en lugar de por el cliente. Este diseño flexible le permite toochoose Hola mejor manera tooorganize contenido.

## <a name="cached-datasets"></a>Conjuntos de datos en caché
Se pueden usar los conjuntos de datos en caché.  Sin embargo, no puede actualizar los datos en caché una vez que se han cargado en **Microsoft Power BI Embedded**. Un conjunto de datos almacenados en memoria caché significa que ha importado datos de hello en Power BI Desktop en lugar de usar DirectQuery.

## <a name="authentication-and-authorization-with-app-tokens"></a>Autenticación y autorización con tokens de aplicación
**Microsoft Power BI Embedded** aplaza tooyour aplicación tooperform todos los necesarios Hola autenticación y autorización. No hay ningún requisito explícito por el que los usuarios finales tengan que ser clientes de Azure Active Directory (Azure AD).  En su lugar, la aplicación se expresa demasiado**Microsoft Power BI Embedded** toorender de autorización mediante el uso de un informe de Power BI **Tokens de autenticación de aplicación (aplicación Tokens)**.  Estos **aplicación Tokens** se crean según sea necesario cuando la aplicación desea toorender un informe.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**Tokens de autenticación de aplicación (aplicación Tokens)** son tooauthenticate utilizado en **Microsoft Power BI Embedded**.  Existen tres tipos de **tokens de aplicación**:

1. Aprovisionar tokens: se usa al aprovisionar una nueva **área de trabajo** en una **colección de áreas de trabajo**
2. Tokens de desarrollo - utilizados al realizar llama directamente a toohello **API de REST de Power BI**
3. Incrustar los símbolos (tokens) - utilizado cuando realiza llamadas toorender un informe en hello incrusta iframe

Estos tokens se usan para hello distintas fases de las interacciones con **Microsoft Power BI Embedded**.  tokens de Hello están diseñados para que puede delegar permisos de su tooPower aplicación BI. Para obtener más información, consulte el artículo sobre el [flujo del token de aplicación](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Creación o modificación de informes en la aplicación

Ahora puede editar existen informes o crear nuevos informes directamente en la aplicación sin necesidad de toouse Power BI Desktop. Esto requiere que exista un conjunto de datos en el área de trabajo.

## <a name="see-also"></a>Consulte también

[Common Microsoft Power BI Embedded scenarios (Escenarios comunes de Microsoft Power BI Embedded)](power-bi-embedded-scenarios.md)  
[Introducción a Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)](power-bi-embedded-get-started-sample.md)  
[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)  
[Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)  
[Repositorio GIT PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Repositorio GIT PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)
