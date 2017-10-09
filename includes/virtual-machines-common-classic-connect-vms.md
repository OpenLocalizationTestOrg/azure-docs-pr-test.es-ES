

![Máquinas virtuales en un servicio en la nube independiente](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

Si coloca las máquinas virtuales en una red virtual, puede decidir cuántos servicios en la nube que desee toouse para cargar los conjuntos de disponibilidad y equilibrio. Además, puede organizar las máquinas virtuales hello en subredes Hola misma forma en que el entorno local y conectarse tooyour de red virtual de hello local red. Este es un ejemplo:

![Máquinas virtuales en una red virtual](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

Las redes virtuales son Hola recomendada máquinas de manera tooconnect virtuales en Azure. Hola práctica recomendada es tooconfigure cada nivel de la aplicación en un servicio de nube diferente. Sin embargo, puede que necesite toocombine algunas máquinas virtuales de diferentes niveles de aplicaciones en hello mismo tooremain de servicio dentro de máximo de Hola de 200 servicios en la nube por suscripción de nube. tooreview este y otros límites, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../articles/azure-subscription-service-limits.md).

## <a name="connect-vms-in-a-virtual-network"></a>Conexión de máquinas virtuales en una red virtual
máquinas virtuales que tooconnect en una red virtual:

1. Crear red virtual de hello en hello [portal de Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) y especifique 'implementación clásica'.
2. Crear conjunto de hello de servicios en la nube para su implementación tooreflect el diseño para conjuntos de disponibilidad y equilibrio de carga. Hola portal de Azure, haga clic en **nuevo > proceso > servicio de nube** para cada servicio en la nube.

  Rellene los detalles de servicio de nube de hello, elegir Hola mismo _grupo de recursos_ usada con la red virtual de Hola.

3. cada nueva virtual toocreate automático, haga clic en **nuevo > proceso**, a continuación, seleccione Hola imagen VM apropiada de hello **aplicaciones destacadas**.

  Hola VM **Fundamentos** hoja, elija Hola mismo _grupo de recursos_ usada con la red virtual de Hola.

  ![Hoja Básico de la máquina virtual cuando se usa una red virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. Tal y como se rellene Hola VM **configuración**, elija Hola correcto _servicio en la nube_ o _red virtual_ para hello máquina virtual.

  Azure seleccionará Hola otro elementos en función de la selección.

  ![Hoja Configuración de la máquina virtual cuando se usa una red virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>Conexión de máquinas virtuales en un servicio en la nube independiente
tooconnect las máquinas virtuales en un servicio de nube independiente:

1. Crear el servicio de nube de Hola Hola [portal de Azure](http://portal.azure.com). Haga clic en **Nuevo > Proceso > Servicio en la nube**. O bien, puede crear servicio en la nube hello para la implementación cuando se crea la primera máquina virtual.
2. Al crear máquinas virtuales de hello, elija hello usa el mismo grupo de recursos con servicio de nube de Hola.

  ![Agregar un servicio de nube de máquina virtual tooan existente](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  Rellene detalles de la máquina virtual de hello, Elegir nombre de hello del servicio de nube que creó en el primer paso de Hola.

  ![Selección de un servicio en la nube para una máquina virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
