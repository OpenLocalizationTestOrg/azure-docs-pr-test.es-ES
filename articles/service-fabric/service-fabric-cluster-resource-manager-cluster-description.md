---
title: "Descripción de clúster del Administrador de recursos aaaCluster | Documentos de Microsoft"
description: "Que describe un clúster de Service Fabric mediante la especificación de dominios de error, dominios de actualización, propiedades de nodo y las capacidades de nodo para Hola, Administrador de recursos del clúster."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>Descripción de un clúster de Service Fabric
Hola, Administrador de recursos de clúster de tejido de servicio proporciona varios mecanismos para la descripción de un clúster. En tiempo de ejecución, Hola, Administrador de recursos del clúster utiliza esta información tooensure servicios de alta disponibilidad Hola ejecutando en el clúster de Hola. Al aplicar estas reglas importantes, también intenta toooptimize consumo de recursos de hello en clúster de Hola.

## <a name="key-concepts"></a>Conceptos clave
Hola, Administrador de recursos del clúster es compatible con varias características que describen un clúster:

* Dominios de error
* Dominios de actualización
* Propiedades del nodo
* Capacidades de nodo

## <a name="fault-domains"></a>Dominios de error
Un dominio de error es cualquier área de error coordinado. Una única máquina es un dominio de error (ya que se puede producir un error en sus propio para diversas razones, de firmware de alimentación de alimentación errores toodrive errores toobad NIC). Las máquinas conectada toohello son el mismo conmutador Ethernet en Hola mismo dominio de error, como son equipos que comparten un único origen de energía o en una sola ubicación. Puesto que es natural que toooverlap de errores de hardware, dominios de error son inherentemente jerárquicos y se representan como URI de Service Fabric.

Es importante que los dominios de error se configuran correctamente porque Service Fabric usa los servicios de contexto de toosafely de esta información. Service Fabric no le interese tooplace de servicios de modo que la pérdida de Hola de un dominio de error (causado por error de Hola de algún componente) hace que un servicio toogo hacia abajo. Hola entorno Azure Service Fabric utiliza información de dominio de error de hello proporcionada por hello entorno toocorrectly configurar los nodos de hello en clúster de hello en su nombre. Para Service Fabric independientes, dominios de error están definidos en el momento de hello ese clúster Hola está configurado 

> [!WARNING]
> Es importante que Hola información de dominio de error proporcionado tooService tejido es precisa. Por ejemplo, supongamos que los nodos del clúster de Service Fabric se ejecutan dentro de 10 máquinas virtuales, en cinco hosts físicos. En este caso, a pesar de que hay 10 máquinas virtuales, hay solo 5 dominios de error (nivel superior) diferentes. Uso compartido de hello hace del mismo host físico tooshare de máquinas virtuales Hola mismo dominio raíz del error, puesto que Hola experiencia de las máquinas virtuales coordinada error si se produce un error en su host físico.  
>
> Puesto que espera Service Fabric Hola dominio de error de un nodo no toochange. Otros mecanismos de garantizar la alta disponibilidad de hello las máquinas virtuales, como [máquinas virtuales de alta disponibilidad](https://technet.microsoft.com/en-us/library/cc967323.aspx), usar la migración transparente de las máquinas virtuales de un host tooanother. Estos mecanismos no volver a configurar o notificar Hola ejecutan código dentro de hello máquina virtual. Por lo tanto, **no se admiten** como entornos para ejecutar clústeres de Service Fabric. Service Fabric deben ser la tecnología de alta disponibilidad solo de hello empleada. Los mecanismos como la migración en vivo de VM, SAN u otros no son necesarios. Si se usa junto con Service Fabric, estos mecanismos _reducen_ la confiabilidad y la disponibilidad de las aplicaciones, ya que agregan una complejidad adicional, añaden orígenes centralizados de errores y utilizan estrategias de confiabilidad y disponibilidad que entran en conflicto con las de Service Fabric. 
>
>

En el siguiente gráfico de Hola se colores todas las entidades de Hola que contribuyen tooFault dominios y lista de que todos los diferentes dominios de error que son el resultado de hello. En este ejemplo, tenemos centros de datos (DC), bastidores (R) y servidores blade (B). Es posible que, si cada hoja contiene más de una máquina virtual, podría haber otra capa Hola jerarquía de dominios de error.

<center>
![Nodos organizados a través de dominios de error][Image1]
</center>

En tiempo de ejecución, Hola, Administrador de recursos de clúster de Service Fabric considera que los dominios de error de hello en clúster de Hola y planes de diseños. Hola réplicas con estado o instancias sin estado para un servicio determinado se distribuyen por lo que están en distintos dominios de error. Distribuir servicio Hola entre dominios de error garantiza la disponibilidad de hello del servicio de hello no se vean comprometida cuando se produce un error en un dominio de error en cualquier nivel de jerarquía de Hola.

Administrador de recursos de clúster del servicio de Fabric no le importa cuántos niveles hay Hola jerarquía de dominios de error. Sin embargo, lo intenta con tooensure que pérdida de Hola de cualquier una parte de la jerarquía de hello no afecta a servicios que se ejecutan en él. 

Es mejor si hay Hola el mismo número de nodos en cada nivel de profundidad en hello jerarquía de dominios de error. Si no está equilibrada en el clúster Hola "árbol" de dominios de error, dificulta que hello toofigure de administrador de recursos del clúster out mejor asignación de hello de servicios. Desequilibrado diseños de dominios de error significan pérdida Hola de algunos dominios de disponibilidad de Hola de impacto de los servicios más de otros dominios. Como resultado, se anula Hola, Administrador de recursos de clúster entre dos objetivos: desea toouse máquinas de hello en ese dominio "intensa" mediante la colocación de servicios en ellos, y lo servicios tooplace en otros dominios para que la pérdida de Hola de un dominio no causa problemas. 

¿Qué aspecto tienen los dominios desequilibrados? En el diagrama de hello siguiente, se muestran dos distintos diseños de clúster. En el primer ejemplo de Hola, los nodos de Hola se distribuyen uniformemente en hello dominios de error. En el segundo ejemplo de Hola, un dominio de error tiene muchos más nodos de hello otros dominios de error. 

<center>
![Dos diseños de clúster distintos][Image2]
</center>

En Azure, de los cuales el dominio de error contiene un nodo de elección de Hola se administra automáticamente. Sin embargo, según el número de Hola de nodos que se aprovisiona puede seguir terminará con dominios de error con más nodos en ellos que otros usuarios. Por ejemplo, supongamos que tiene cinco dominios de error en el clúster de hello pero aprovisionar siete nodos para un determinado valor de NodeType. En este caso, hello primero dos dominios de error acabar con varios nodos. Si sigues toodeploy más NodeTypes con sólo algunas instancias, Hola problema empeora. Por este motivo, recomienda que Hola número de nodos de cada tipo de nodo es un múltiplo del número de Hola de dominios de error.

## <a name="upgrade-domains"></a>Dominios de actualización
Dominios de actualización son otra característica que ayuda a Hola servicio Administrador de recursos del clúster de tejido entender Hola diseño del clúster de Hola. Dominios de actualización definen conjuntos de nodos que se actualizan al Hola mismo tiempo. Dominios Hola de Ayuda de administrador de recursos del clúster de entender y coordinar las operaciones de administración como las actualizaciones de la actualización.

Los dominios de actualización son muy similares a los dominios de error, pero con algunas diferencias clave. En primer lugar, las áreas de los errores de hardware coordinados definen los dominios de error. Dominios de actualización, en Hola otra parte, se definen por la directiva. Obtener toodecide cuántas desea, en lugar de que se dicte entorno Hola. Puede tener tantos dominios de actualización como ocurre con los nodos. Otra diferencia entre los dominios de error y los dominios de actualización es que los dominios de actualización no son jerárquicos. En su lugar, son más parecidos a una etiqueta sencilla. 

Hello siguiente diagrama muestra tres que dominios de actualización se dividen en tres dominios de error. También se muestra una posible selección de ubicación de tres réplicas diferentes de un servicio con estado, donde cada una de ellas terminan con diferentes dominios de error y de actualización. Esta ubicación permite pérdida de Hola de un dominio de error mientras se encuentra en medio de Hola de una actualización de servicio y seguir teniendo una copia del código de hello y los datos.  

<center>
![Selección de ubicación con dominios de error y de actualización][Image3]
</center>

Hay ventajas y desventajas toohaving gran número de dominios de actualización. Más dominios de actualización significa que cada paso de actualización de hello es más detallado y, por tanto, afecta a un número menor de nodos o servicios. Como resultado, servicios menos tienen toomove a la vez, la introducción de menos actividad en sistema Hola. Esto suele tooimprove confiabilidad, ya que menos del servicio de Hola se ve afectado por cualquier problema introducido durante la actualización de Hola. Dominios de actualización más también significa que necesita menos búfer disponible en impacto nodos toohandle Hola de hello actualizar. Por ejemplo, si tiene cinco dominios de actualización, nodos de hello en cada uno están controlando aproximadamente 20% del tráfico. Si necesita tootake hacia abajo de ese dominio de actualización para realizar una actualización, que carga normalmente no es necesaria en algún lugar toogo. Puesto que tiene cuatro dominios de actualización restante, cada uno debe tener espacio aproximadamente el 5% del tráfico total de Hola. Dominios de actualización más significa que necesita menos búfer en nodos de hello en clúster de Hola. Por ejemplo, considere si había 10 dominios de actualización en su lugar. En ese caso, cada UD solo puede controlar aproximadamente el 10% del tráfico total de Hola. Cuando una actualización recorre clúster hello, cada dominio solo tendría sala toohave aproximadamente 1.1% del total de tráfico que Hola. Dominios de actualización más general permiten toorun los nodos en una mayor utilización, puesto que necesita capacidad reservada menor. Hello mismo puede decirse de dominios de error.  

inconveniente de Hola de disponer de varios dominios de actualización es que las actualizaciones suelen tootake más. Tejido de servicio espera un breve período de tiempo después de un dominio de actualización se ha completado y realiza comprobaciones antes de iniciar tooupgrade Hola siguiente. Estos retrasos permiten detectar problemas introducidos por la actualización de Hola para poder continuar con la actualización Hola. contrapartida de Hello es aceptable porque evita cambios incorrectos afecte a un exceso de servicio de Hola a la vez.

Usar demasiado pocos dominios de actualización también tiene muchos efectos secundarios: mientras que cada dominio de actualización esté inactivo y actualizándose, una gran parte de la capacidad general no estará disponible. Por ejemplo, si solo dispone de tres dominios de actualización, estará inactiva un tercio de la capacidad general del servicio o del clúster al mismo tiempo. Tener gran parte de su servicio hacia abajo al mismo tiempo no es deseable ya que tiene suficiente capacidad de toohave en el resto de saludo de la carga de trabajo de clúster toohandle Hola. Mantener el búfer implica que durante el funcionamiento normal, los nodos se carguen menos de lo que deberían. Esto aumenta el costo de Hola de su servicio en ejecución.

No hay ningún límite real toohello total de errores o dominios de actualización en un entorno o restricciones en la manera en se superponen. Es decir, hay varios patrones comunes:

- Asignación 1:1 de dominios de error y de actualización
- Un dominio de actualización por nodo (instancia del sistema operativo física o virtual)
- Un modelo de "seccionado" o "matriz" donde hello dominios de error y dominios de actualización forman una matriz con máquinas que se ejecutan normalmente hacia abajo diagonales Hola

<center>
![Diseños de dominio de error y de actualización][Image4]
</center>

No hay que ningún mejor responder qué toochoose de diseño, cada uno tiene algunas ventajas y desventajas. Por ejemplo, modelo de hello 1FD:1UD depende de tooset simple. Hello 1 dominio de actualización por modelo de nodo es más se asemeje a qué usuarios se utilizan para. Durante las actualizaciones, cada nodo se actualiza de forma independiente. Esto es similar toohow conjuntos pequeños de máquinas se actualizaron manualmente en hello anterior. 

modelo más común de Hello es matriz de FD/UD hello, donde hello FD y ud forma una tabla y se colocan nodos empezando a lo largo de hello diagonal. Se trata de modelo de hello utilizada de forma predeterminada en clústeres de Service Fabric en Azure. Para los clústeres con muchos nodos todo termina sería similar al modelo de matriz densa de hello anterior.

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>Restricciones de dominio de error y de actualización y el comportamiento resultante
Hola, Administrador de recursos del clúster trata el deseo de hello tookeep un servicio están equilibrados en los dominios de error y actualización como una restricción. Para más información sobre las restricciones, vea [este artículo](service-fabric-cluster-resource-manager-management-integration.md). Hola error y actualización del dominio de estado de restricciones: "para una partición de servicio determinado nunca habrá una diferencia *mayor que uno* en número de Hola de objetos de servicio (instancias de servicio sin estado o réplicas de servicio con estado) entre dos dominios." Esto evita determinados movimientos o disposiciones que infringen esta restricción.

Veamos un ejemplo. Supongamos que tenemos un clúster con 6 nodos, configurado con 5 dominios de error y 5 dominios de actualización.

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

Ahora supongamos que creamos un servicio con un TargetReplicaSetSize (o, para un servicio sin estado un InstanceCount) de cinco. réplicas de Hello llegará a N1 N5. De hecho, nunca se usará N6, independientemente del número de servicios como este que cree. Pero ¿por qué? Echemos un vistazo a diferencia de hello entre el diseño actual de Hola y lo que sucedería si se elige N6.

Este es el diseño de Hola se obtuvo y Hola número total de réplicas por error y actualización del dominio:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Este diseño se equilibra en términos de nodos por dominio de error y de actualización. También lo está equilibrada en cuanto al número de Hola de réplicas por error y actualización del dominio. Cada dominio tiene Hola el mismo número de nodos y Hola el mismo número de réplicas.

Ahora, echemos un vistazo a lo que sucedería si hubiéramos utilizado N6 en lugar de N2. ¿Cómo réplicas Hola se distribuyen a continuación?

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

Este diseño infringe la definición de hello restricciones de dominio de error. FD0 tiene dos réplicas, mientras que FD1 tiene cero, hacer diferencia Hola entre FD0 y FD1 un total de dos. Hola, Administrador de recursos del clúster no permite este tipo de organización. De forma similar, si se ha seleccionado N2 y N6 (en lugar de N1 y N2), obtendríamos lo siguiente:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Este diseño se equilibra en cuanto a dominios de error. Sin embargo, ahora está infracción de restricción de la actualización del dominio de Hola. Esto es porque UD0 tiene cero réplicas, mientras que UD1 tiene dos. Por lo tanto, este diseño también es válido y no pueden seleccionar por Hola, Administrador de recursos del clúster. 

## <a name="configuring-fault-and-upgrade-domains"></a>Configuración de dominios de error y de actualización
La definición de dominios de error y de actualización se realiza automáticamente en las implementaciones de Service Fabric hospedadas en Azure. Service Fabric recoge y usa información del entorno Hola de Azure.

Si va a crear su propio clúster (o quiere toorun una determinada topología en desarrollo), puede proporcionar información de dominio de error y actualización del dominio de Hola. En este ejemplo, definimos un clúster de desarrollo local de nueve nodos que abarca tres centros de datos (cada uno con tres bastidores). Este clúster también tiene tres dominios de actualización seccionados en esos tres centros de datos. Es un ejemplo de configuración de Hola a continuación: 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

a través de ClusterConfig.json para las implementaciones independientes

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> Al definir los clústeres a través de Azure Resource Manager, Azure asigna dominios de error y dominios de actualización. Por lo tanto, la definición de Hola de los tipos de nodos y conjuntos de escalas de máquina Virtual en la plantilla de administrador de recursos de Azure no incluye información de actualización del dominio o dominio de error.
>

## <a name="node-properties-and-placement-constraints"></a>Restricciones de ubicación y propiedades de nodo
A veces (de hecho, la mayoría de las veces de Hola) que vaya tooensure toowant que ciertas cargas de trabajo se ejecutan únicamente de determinados tipos de nodos de clúster de Hola. Por ejemplo, algunas cargas de trabajo pueden requerir GPU o SSD, al contrario que otras. Un buen ejemplo de destinar las cargas de trabajo tooparticular de hardware está disponible casi cada arquitectura de n niveles. Determinadas máquinas sirven como Hola front-end o API que sirve al lado de la aplicación hello y son clientes toohello expuesto u Hola internet. Equipos diferentes, a menudo con recursos de hardware diferente, controlan trabajo Hola de capas de compute o almacenamiento de Hola. Estos suelen ser _no_ directamente expuestos tooclients u Hola internet. Tejido de servicio espera que hay casos en que las cargas de trabajo concretas tenga toorun en las configuraciones de hardware determinado. Por ejemplo:

* una aplicación de n niveles existente se ha transferido "tal cual" a un entorno de Service Fabric;
* una carga de trabajo desea toorun en hardware específico por motivos de aislamiento de seguridad, de escala o de rendimiento
* una carga de trabajo debe estar aislada de otras por una directiva o a causa del consumo de recursos.

Servicio de estos tipos de configuraciones, toosupport tejido tiene una noción de primera clase de etiquetas que pueden ser toonodes aplicada. Estas etiquetas se denominan **propiedades del nodo**. **Las restricciones de posición** son instrucciones de hello adjuntos tooindividual servicios que seleccione para una o más propiedades de nodo. Las restricciones de posición definen dónde deben ejecutarse los servicios. Hola conjunto de restricciones es extensible; puede trabajar cualquier par de clave/valor. 

<center>
![Diferentes cargas de trabajo por diseño de clúster][Image5]
</center>

### <a name="built-in-node-properties"></a>Propiedades del nodo integradas
Service Fabric define algunas propiedades de nodo predeterminado que se pueden usar automáticamente sin que tenga toodefine de usuario de hello ellos. propiedades predeterminadas de Hello definidas en cada nodo son hello **NodeType** hello y **NodeName**. Por ejemplo, podría escribir una restricción de selección de ubicación como `"(NodeType == NodeType03)"`. Por lo general encontramos NodeType toobe una de las propiedades de hello más frecuente. Es útil, ya que corresponde a 1:1 con un tipo de una máquina. Cada tipo de máquina corresponde tooa tipo de carga de trabajo en una aplicación de n niveles tradicional.

<center>
![Restricciones de selección de ubicación y propiedades de nodo][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>Restricciones de colocación y sintaxis de propiedades de nodo 
valor de Hello especificado en la propiedad de nodo de hello puede ser una cadena, bool, o long con signo. declaración de Hello en el servicio de Hola se denomina una colocación *restricción* puesto que restringe donde puede ejecutar el servicio hello en clúster de Hola. restricción de Hello puede ser cualquier instrucción booleano que opera en las propiedades de otro nodo de hello en clúster de Hola. selectores válido de Hello en estas instrucciones booleanos son:

1) comprobaciones condicionales para crear instrucciones concretas

| Instrucción | Sintaxis |
| --- |:---:|
| "equal to" | "==" |
| "not equal to" | "!=" |
| "greater than" | ">" |
| "greater than or equal to" | ">=" |
| "less than" | "<" |
| "less than or equal to" | "<=" |

2) Instrucciones booleanas para operaciones lógicas y de agrupación

| Instrucción | Sintaxis |
| --- |:---:|
| "and" | "&&" |
| "or" | "&#124;&#124;" |
| "not" | "!" |
| "group as single statement" | "()" |

Estos son algunos ejemplos de instrucciones de restricción básicas.

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

Sólo los nodos donde hello general colocación restricción instrucción da como resultado demasiado "True" pueden tener servicio Hola colocado en él. Los nodos que no tengan definida ninguna propiedad no coinciden con ninguna restricción de selección de ubicación que contenga esa propiedad.

Supongamos que Hola siguiente nodo propiedades se definen para un tipo de nodo determinado:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure. 

> [!NOTE]
> En el nodo de Azure Resource Manager plantilla Hola tipo normalmente tiene parámetros. Tendría el siguiente aspecto "[parameters('vmNodeType1Name')]", en lugar de "NodeType01".
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

Puede crear *restricciones* de selección de ubicación para un servicio de forma parecida a esta:

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

Si todos los nodos de NodeType01 son válidos, también puede seleccionar ese tipo de nodo con la restricción de hello "(NodeType == NodeType01)".

Una de hello cosas interesantes sobre las restricciones de posición de un servicio es que se puede actualizar dinámicamente en tiempo de ejecución. Por lo que si necesita, puede moverse un servicio en clúster de hello, agregar y quitar los requisitos, etcetera. Tejido de servicio se encarga de asegurarse de que servicio Hola mantiene la seguridad y disponibles incluso cuando se realizan estos tipos de cambios.

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Powershell:

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

Las restricciones de colocación se especifican para cada instancia de servicio con nombre diferente. Siempre producirán actualizaciones Hola de (sobrescribir) lo que especificó previamente.

definición del clúster Hola define propiedades de hello en un nodo. Cambiar las propiedades de un nodo requiere una actualización de la configuración del clúster. Actualizar propiedades de un nodo requiere cada tooreport de toorestart nodo afectado sus nuevas propiedades. Service Fabric administra estas actualizaciones sucesivas.

## <a name="describing-and-managing-cluster-resources"></a>Descripción y administración de recursos de clúster
Uno de los más importantes de trabajos de cualquier orchestrator es toohelp Hola administrar el consumo de recursos en clúster de Hola. La administración de recursos de clúster puede significar un par de cosas diferentes. En primer lugar, hay es asegurarse de que las máquinas no estén sobrecargadas. Esto significa asegurarse de que las máquinas no estén ejecutando más servicios de los que puede administrar. En segundo lugar, no hay equilibrio y la optimización que es crítica toorunning servicios eficazmente. Ofertas de servicio con información confidencial eficaces o rendimiento costos no permiten algunos toobe nodos activa mientras que otros están inactivos. Los nodos activos provocar contención tooresource y un rendimiento bajo y nodos inactivos representan desaprovechado recursos y aumentar los costos. 

Service Fabric representa los recursos como `Metrics`. Las métricas son cualquier recurso físico o lógico que desea toodescribe tooService tejido. Algunos ejemplos de métricas son elementos como "WorkQueueDepth" o "MemoryInMb". Para obtener información acerca de los recursos físicos de Hola que puede administrar el tejido de servicio en los nodos, consulte [regulador de recursos](service-fabric-resource-governance.md). Para obtener información sobre la configuración de métricas personalizadas y sus usos, vea [este artículo](service-fabric-cluster-resource-manager-metrics.md).

Las métricas se diferencian de las restricciones de selección ubicación y de las propiedades de nodo Propiedades de nodo son estáticos descriptores de nodos de Hola por sí mismos. Las métricas describen recursos que tienen nodos y que los servicios usan cuando se ejecutan en un nodo. Una propiedad de nodo podría ser "HasSSD" y puede establecerse tootrue o false. cantidad de Hola de espacio disponible en ese SSD y cuánto se consume Services sería una métrica como "DriveSpaceInMb". 

Es importante toonote que al igual que para las restricciones de posición y las propiedades de nodo, Hola, Administrador de recursos de clúster de servicio de Fabric no comprende qué nombres Hola de Media de las métricas de Hola. ya que son simplemente cadenas. Es un unidades de toodeclare recomendable como parte de los nombres de métrica de Hola que crea al pueden ser ambigua.

## <a name="capacity"></a>Capacity
Si desactivó todo el *equilibrio*de recursos, la utilidad Cluster Resource Manager de Service Fabric aún podría asegurarse de que ningún nodo terminara superando su capacidad. Es posible administrar saturaciones de capacidad a menos que el clúster de hello está demasiado lleno o cargas de trabajo de hello es mayor que cualquier nodo. La capacidad es otro *restricción* ese administrador de recursos del clúster de hello usa toounderstand la cantidad de un recurso de un nodo tiene. Capacidad restante es también realiza un seguimiento para clúster Hola como un todo. Capacidad de Hola y el consumo de hello en el nivel del servicio de Hola se expresan en términos de métricas. Por ejemplo, métrica Hola podría ser "ClientConnections" y un nodo determinado puede tener una capacidad de "ClientConnections" de 32768. Otros nodos pueden tener otros límites algún servicio que se ejecuta en ese nodo puede decir está actualmente consumiendo 32256 de métrica de Hola "ClientConnections".

En tiempo de ejecución, Hola, Administrador de recursos del clúster realiza un seguimiento de capacidad restante en el clúster de Hola y en los nodos. En orden tootrack Hola capacidad Administrador de recursos del clúster resta el uso de cada servicio en la capacidad del nodo donde se ejecuta el servicio de Hola. Con esta información, Hola, Administrador de recursos de clúster de tejido de servicio puede averiguar dónde tooplace o mover las réplicas para que los nodos no pasan por la capacidad.

<center>
![Nodos del clúster y capacidad][Image7]
</center>

C#:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

Puede ver las capacidades definidas en el manifiesto de clúster de hello:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure. 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

Normalmente, una carga de un servicio cambia de forma dinámica. Supongamos que carga la réplica de "ClientConnections" cambia de 1024 too2048, pero aparece un nodo de Hola se estaba ejecutando en, a continuación, solo pudiera guiarse por 512 capacidad restante para esa métrica. Ahora, esa selección de ubicación de la instancia o réplica no es válida porque no hay suficiente espacio en ese nodo. Hola, Administrador de recursos del clúster tiene tookick y obtenga Hola nodo bajo su capacidad. Reduce la carga en el nodo de Hola que está por encima de la capacidad moviendo una o varias de las réplicas de Hola o instancias de ese nodo tooother nodos. Al mover las réplicas, Hola, Administrador de recursos del clúster intenta costo de hello toominimize los movimientos. Coste del movimiento se explica en [este artículo](service-fabric-cluster-resource-manager-movement-cost.md) y más sobre Hola Administrador de recursos del clúster de nuevo equilibrio estrategias y reglas se describen [aquí](service-fabric-cluster-resource-manager-metrics.md).

## <a name="cluster-capacity"></a>Capacidad del clúster
Entonces, ¿cómo hello general de administrador de recursos de clúster de tejido de servicio tenga Hola de clúster está demasiado llena? Con la carga dinámica no hay mucho que pueda hacer. Servicios pueden tener su pico de carga independientemente de las acciones realizadas por Hola, Administrador de recursos del clúster. Como resultado, un clúster con espacio de sobra hoy puede quedarse corto cuando se haga famoso mañana, Dicho esto, hay algunos controles que se incorporen un concepto de tooprevent problemas. Hola primera cosa que podemos hacer es impedir la creación de hello de nuevas cargas de trabajo que provocaría Hola clúster toobecome completa.

Supongamos que crea un servicio sin estado y tiene cierta carga asociado a él, y que Supongamos que se ocupa de servicio Hola acerca de la métrica de Hola "DiskSpaceInMb". Supongamos también que es continuo tooconsume cinco unidades de "DiskSpaceInMb" para cada instancia del servicio de Hola. Desea toocreate tres instancias de servicio de Hola. Estupendo. Por lo que significa que se necesitan 15 unidades de "DiskSpaceInMb" toobe presenta clúster hello en orden para que podamos tooeven ser capaz de toocreate estas instancias de servicio. Hola, Administrador de recursos del clúster calcula continuamente capacidad de Hola y el consumo de cada métrica para que pueda determinar la capacidad restante de hello en clúster de Hola. Si no hay suficiente espacio, Hola Hola de rechazos de administrador de recursos de clúster crear llamadas de servicio.

Puesto que el requisito de hello está solo podrá 15 unidades, podría asignarse a este espacio de muchas maneras diferentes. por ejemplo, podría ser una unidad de capacidad restante en 15 nodos diferentes o las tres unidades de capacidad que quedan en 5 nodos diferentes. Si Hola, Administrador de recursos del clúster puede reorganizar cosas así que no hay cinco unidades en tres nodos, coloca servicio Hola. La reorganización clúster Hola normalmente es posible a menos que el clúster de hello está casi lleno o no se pueden consolidar los servicios existentes Hola por algún motivo.

## <a name="buffered-capacity"></a>Capacidad de búfer
Capacidad almacenado en búfer es otra característica del programa Hola a Administrador de recursos del clúster. Permite una reserva de alguna parte del programa Hola capacidad total de nodo. Este búfer de capacidad es servicios solo tooplace usado durante las actualizaciones y los errores de nodo. Capacidad de búfer se especifica globalmente por métrica para todos los nodos. valor de Hello que elegir para la capacidad de hello reservado es una función del número de Hola de error y dominios de actualización tiene en clúster de Hola. Más dominios de error y de actualización significa que puede elegir un número menor para la capacidad de búfer. Si tiene varios dominios, puede esperar pequeñas cantidades de su toobe de clúster no está disponible durante las actualizaciones y los errores. Capacidad de almacenamiento en búfer solo tiene sentido especificar si también tiene capacidad de nodos de hello especificado para una métrica.

Este es un ejemplo de cómo toospecify almacenado en búfer capacidad:

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

a través de ClusterConfig.json para las implementaciones independientes o Template.json para los clústeres hospedados en Azure:

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

Error al crear el Hola de nuevos servicios una vez clúster Hola sin capacidad de almacenado en búfer para una métrica. Evitar la creación de Hola de nuevo búfer de hello toopreserve de servicios garantiza que las actualizaciones y los errores no provocan nodos toogo sobre capacidad. La capacidad de búfer es opcional, pero se recomienda en los clústeres que definen una capacidad de una métrica.

Hola, Administrador de recursos del clúster expone esta información de carga. Para cada métrica, esta información incluye: 
  - Hola almacenado en búfer la configuración de capacidad
  - capacidad total de Hola
  - consumo actual de Hola
  - si cada métrica se considera equilibrada o no
  - estadísticas acerca de la desviación estándar de Hola
  - nodos de Hola que tienen Hola mayoría y menos carga  
  
A continuación podemos ver un ejemplo del resultado:

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>Pasos siguientes
* Para obtener información sobre el flujo de información y arquitectura de hello en hello Administrador de recursos del clúster, visite [este artículo](service-fabric-cluster-resource-manager-architecture.md)
* Definir métricas de desfragmentación es tooconsolidate una manera de carga en los nodos en lugar de propagarse. toolearn cómo tooconfigure la desfragmentación, consulte demasiado[este artículo](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Desde el principio de Hola y [obtener un servicio Administrador de recursos del clúster de tejido de toohello de introducción](service-fabric-cluster-resource-manager-introduction.md)
* toofind out acerca de cómo Hola, Administrador de recursos del clúster administra y equilibra la carga en el clúster de hello, desproteger artículo hello en [equilibrio de carga](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
