# <a name="securing-docker-containers-in-azure-container-service"></a>Protección de contenedores de Docker en Azure Container Service

Este artículo presenta consideraciones y recomendaciones para proteger los contenedores de Docker implementados en Azure Container Service. Muchas de estas consideraciones aplican generalmente contenedores tooDocker implementados en Azure o en otros entornos. 

## <a name="image-security"></a>Seguridad de imágenes

Los contenedores se crean a partir de imágenes que están almacenadas en uno o varios repositorios. Estos repositorios pueden pertenecer toopublic o registros de contenedor privado. Un ejemplo de un registro público es [Docker Hub](https://hub.docker.com/). Un ejemplo de un registro privado es hello [registro de confianza de Docker](https://docs.docker.com/datacenter/dtr/2.0/), lo que puede ser instalado de forma local o en una nube privada virtual. También hay servicios de registro privado de contenedores basados en la nube, incluido [Azure Container Registry](../articles/container-registry/container-registry-intro.md).

### <a name="public-and-private-images"></a>Imágenes públicas y privadas
En general, al igual que con cualquier paquete de software publicado de forma pública, una imagen de contenedor disponible públicamente no garantiza la seguridad. Las imágenes de contenedor constan de varias capas de software, y cada capa de software podría tener vulnerabilidades. Sea toounderstand clave Hola origen de imagen del contenedor hello, incluyendo Hola propietario de imagen de hello (toodetermine si es un origen de confianza o no), Hola capas de software consta de y Hola versiones de software. 

Por ejemplo, si va toohello oficial [nginx repositorio](https://hub.docker.com/_/nginx/) en Docker Hub y navegue toohello **etiquetas** pestaña, vea vulnerabilidades codificado por colores en cada imagen. Cada color representa una vulnerabilidad de Hola de una capa de software de imagen de Hola. Para más información sobre el examen de vulnerabilidades en el Centro de Docker, consulte [Descripción de los repositorios oficiales en el Centro de Docker](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/).

![Imágenes nginx en el Centro de Docker](./media/container-service-security/docker-hub-nginx.png)

Las empresas se encarga profundamente sobre seguridad y tooprotect por sí mismos contra los ataques de seguridad deben almacenar y recuperar imágenes desde un registro privado, como registro de contenedor de Azure o el registro de confianza de Docker. En suma tooproviding un registro privado administrado, registro de contenedor de Azure es compatible con [autenticación basada en la entidad de seguridad del servicio](../articles/container-registry/container-registry-authentication.md) a través de Azure Active Directory para los flujos de autenticación básica, incluido el acceso basado en roles para de solo lectura, escritura y permisos de propietario.

### <a name="image-security-scanning"></a>Examen de seguridad de imágenes

Incluso cuando se usa un registro privado, es una imagen de toouse buena idea análisis soluciones para la validación de seguridad adicional. Cada capa de software en una imagen de contenedor es potencialmente propenso toovulnerabilities independiente de otras capas de imagen de contenedor de Hola. Como cada vez más empresas empezar a implementar sus cargas de trabajo de producción que se basa en tecnologías de contenedor, digitalización de imágenes se convierte en tooensure importante prevención de amenazas de seguridad en sus organizaciones. 

Supervisión y análisis como soluciones de seguridad [Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry) y [aguamarina seguridad](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry), entre otros, pueden tooscan usa imágenes de contenedor en un registro privada e identificar posibles vulnerabilidades. Es importante proporcionar profundidad de hello toounderstand de recorrido que Hola diferentes soluciones. Por ejemplo, algunas soluciones podrían verificar las capas de imagen en comparación con vulnerabilidades conocidas. Estas soluciones no sea capaz de tooverify software de capa de imagen creado a partir de determinado software de administrador de paquetes. Otras soluciones tienen una integración del análisis más profunda y pueden encontrar vulnerabilidades en cualquier software empaquetado.

### <a name="production-deployment-rules-and-audit"></a>Auditoría y reglas de implementación de producción
Una vez que una aplicación se implementa en producción, es esencial tooset tooensure algunas de las reglas que las imágenes que se usan en entornos de producción son seguras y no contener ninguna vulnerabilidad.

* Como norma, imágenes con vulnerabilidades, incluso los pequeños, no deberían estar permitidas toorun en un entorno de producción. Además, todas las imágenes implementadas en producción lo ideal es que se deben guardar en una instrucción select tooa accesible de registro privada solo algunos. También es importante tookeep número de Hola de producción imágenes pequeñas tooensure que puedan administrarse eficazmente.

* Puesto que es el origen de hello toopinpoint de disco duro de software desde una imagen de contenedor disponible públicamente, es una imagen de toobuild buenas prácticas a partir de datos de origen tooensure de origen de Hola de capa de Hola. Cuando superficies de una vulnerabilidad en una imagen de contenedor generada automáticamente, los clientes pueden encontrar una resolución más rápida de tooa de ruta de acceso. Con una imagen pública, los clientes tienen raíz hello toofind un toofix imágenes públicas, u obtener otra imagen segura del publicador de Hola.

* Una imagen digitalizada exhaustivamente implementada en producción no está garantizada toobe seguridad toodate dure Hola de aplicación hello. Se puede notificar las vulnerabilidades de seguridad para las capas de imagen de Hola que no se conocían anteriormente o se introdujeron después de la implementación de producción de hello. La auditoría periódica de imágenes implementadas en producción es necesario tooidentify imágenes que no están actualizados o no se han actualizado en unos instantes. Uno puede usar metodologías de implementación de verde azulado y distribuir imágenes de contenedor de mecanismos de actualización tooupdate sin tiempo de inactividad. Digitalización de imágenes puede realizarse con herramientas que se describen en la sección anterior de Hola. 

* Una canalización de integración continua (CI) toobuild imágenes y el examen de la seguridad integrada pueden ayudar a mantener seguros registros privados con imágenes de contenedor seguro. Hello examen de las vulnerabilidades integrado en la solución de integración continua de hello garantiza que las imágenes que superan todas las pruebas de Hola se insertan toohello privada registro de producción en donde se implementan las cargas de trabajo. Un error de canalización de CI garantiza que no se incluyen imágenes vulnerables en registro privada Hola usadas para las implementaciones de carga de trabajo de producción. También automatiza el examen de seguridad de imágenes si hay un número significativo de imágenes. De lo contrario, auditar las imágenes manualmente para buscar vulnerabilidades de seguridad puede ser bastante lento y estar propenso a errores.

## <a name="host-level-container-isolation"></a>Aislamiento de contenedor a nivel de host
Cuando un cliente implementa aplicaciones de contenedor en recursos de Azure, se implementan en un nivel de suscripción en grupos de recursos y no son tienen varios inquilinos. Esto significa que si un cliente comparte una suscripción con otros usuarios, no hay ningún límite que puede crearse entre dos implementaciones en hello misma suscripción. Por lo tanto, no se garantiza la seguridad a nivel de contenedor. 

También resulta crítico toounderstand que contenedores compartan kernel hello y recursos de Hola de host de hello (que en el servicio de contenedor de Azure es una VM de Azure en un clúster). Por lo tanto, los contenedores que se ejecutan en producción se deben ejecutar en modo de usuario sin privilegios. Ejecución de un contenedor con privilegios de raíz puede poner en peligro todo el entorno de Hola. Con acceso de nivel de raíz en un contenedor, un pirata informático puede tener acceso toohello privilegios de raíz completa en el host de Hola. Además, es importante toorun contenedores con sistemas de archivos de solo lectura. Esto evita que alguien que tenga acceso toohello en peligro contenedor toowrite scripts malintencionados toohello sistema de archivos y obtener acceso a archivos tooother. De igual forma, es importante toolimit Hola los recursos (por ejemplo, memoria, CPU y ancho de banda de red) asignados tooa contenedor. Esto ayuda a impedir que piratas informáticos de estar sobrecargando los recursos y que ejerzan actividades ilegales como fraude con tarjetas de crédito o de minería de datos de bitcoin, lo que podría impedir que se ejecuten en clúster o host Hola otros contenedores.

## <a name="orchestrator-considerations"></a>Consideraciones sobre el orquestador

Cada orquestador disponible en Azure Container Service tiene sus propias consideraciones de seguridad. Por ejemplo, debe limitar los nodos de tooorchestrator de acceso de directo SSH en el servicio de contenedor. En su lugar, debe usar la interfaz de usuario o herramientas de línea de comandos de cada orchestrator (como `kubectl` para Kubernetes) toomanage el entorno del contenedor de hello sin tener acceso a hosts de Hola. Para obtener más información, consulte [realizar una conexión remota tooa Kubernetes, DC/OS, Docker Swarm clúster o](../articles/container-service/kubernetes/container-service-connect.md).

Para obtener información de seguridad específicos de orchestrator adicional, vea Hola recursos siguientes:

* **Kubernetes**: [prácticas recomendadas de seguridad para la implementación de Kubernetes](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html)

* **DC/OS**: [cómo asegurar su clúster](https://dcos.io/docs/1.8/administration/securing-your-cluster/)

* **Docker Swarm**: [seguridad de Docker](https://www.docker.com/docker-security)

## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información acerca de la seguridad de arquitectura y el contenedor de Docker, consulte [Introducción tooContainer seguridad](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf).

* Para obtener información acerca de la seguridad de la plataforma Windows Azure, vea hello [Azure Security Center](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure).
