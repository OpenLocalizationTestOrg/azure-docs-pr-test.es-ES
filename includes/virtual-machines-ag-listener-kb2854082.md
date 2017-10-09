A continuación, si todos los servidores en clúster de hello están ejecutando Windows Server 2008 R2 o Windows Server 2012, también debe comprobar esa revisión hello [KB2854082](http://support.microsoft.com/kb/2854082) está instalado en cada uno de los servidores locales de Hola o máquinas virtuales de Azure que forman parte del clúster de Hola. Cualquier servidor o la máquina virtual en clúster de hello, pero no en grupo de disponibilidad de hello, también debe tener instalada esta revisión.

En hello sesión de escritorio remoto para cada uno de los nodos de clúster de hello, descargue [KB2854082](http://support.microsoft.com/kb/2854082) tooa de directorio local. A continuación, instale revisión de hello en cada nodo del clúster secuencialmente. Si el servicio de Cluster Server de saludo se está ejecutando en el nodo del clúster de hello, se reinicia servidor hello final Hola Hola la instalación de revisión.

> [!WARNING]
> Detener el servicio de Cluster Server de Hola o reiniciar el servidor de Hola afecta al estado de quórum de hello del grupo de disponibilidad hello y clúster, y podría hacer que su toogo de clúster sin conexión. toomaintain Hola alta disponibilidad del clúster durante la instalación, asegúrese de que:
> 
> * clúster de Hello está en estado de quórum óptimo. 
> * Antes de instalar la revisión de Hola en cualquier nodo, todos los nodos del clúster están en línea.
> * Antes de instalar Hola revisión en cualquier otro nodo de clúster de hello, permiten toocompletion de toorun de instalación de revisión de hello en un nodo, incluyendo la reinicialización completa servidor hello.
> 
> 

