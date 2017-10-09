
Cada punto de conexión cuenta con un *puerto público* y un *puerto privado*:

* Puerto público Hola se usa por toolisten de equilibrador de carga de Azure de Hola para entrante máquina virtual de toohello de tráfico de hello Internet.
* puerto privado Hola se usa por toolisten de máquina virtual de Hola para entrante tráfico, normalmente destino tooan aplicación o servicio que se ejecuta en la máquina virtual de Hola.

Valores predeterminados de Hola protocolo IP y puertos TCP o UDP para los protocolos de red conocidos se proporcionan al crear los puntos de conexión con hello portal de Azure. Para los puntos de conexión personalizados, necesitará toospecify Hola correcta IP protocolo (TCP o UDP) y puertos públicos y privados de Hola. toodistribute el tráfico entrante al azar entre varias máquinas virtuales, deberá toocreate un conjunto de equilibrio de carga que consta de varios puntos de conexión.

Después de crear un punto de conexión, puede usar un reglas de toodefine de lista (ACL) de control de acceso que permitan o denieguen el tráfico entrante hello toohello puerto público de extremo de hello en función de su dirección IP de origen. Sin embargo, si la máquina virtual de hello está en una red virtual de Azure, debe usar grupos de seguridad de red en su lugar. Para obtener más información, consulte [Información sobre los grupos de seguridad de red](../articles/virtual-network/virtual-networks-nsg.md).

> [!NOTE]
> La configuración del firewall para máquinas virtuales de Azure se realiza automáticamente para los puertos asociados con los puntos de conexión de conectividad remotos que Azure configura automáticamente. Para los puertos especificados para todos los demás extremos, ninguna configuración se realiza automáticamente toohello firewall de máquina virtual de Hola. Cuando se crea un punto de conexión de máquina virtual de hello, necesitará tooensure que Hola firewall de máquina virtual de hello también permite el tráfico de hello para el protocolo de Hola y configuración de punto de conexión de puerto privado correspondiente toohello. tooconfigure Hola firewall, vea la documentación de Hola o la Ayuda en línea de sistema operativo hello en la máquina virtual de Hola.
>
>

## <a name="create-an-endpoint"></a>Creación de un extremo
1. Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **máquinas virtuales**y, a continuación, haga clic en nombre de Hola de máquina virtual de Hola que desea tooconfigure.
3. Haga clic en **extremos** en hello **configuración** grupo. Hola **extremos** página enumera todos los extremos de hello actual para la máquina virtual de Hola. (Este ejemplo es una VM Windows. Una VM Linux mostrará de forma predeterminada un punto de conexión para SSH).

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![Puntos de conexión](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. En la barra de comandos de Hola por encima de las entradas de punto de conexión de hello, haga clic en **agregar**.
5. En hello **Agregar extremo** página, escriba un nombre de extremo de hello en **nombre**.
6. En **Protocolo**, elija **TCP** o **UDP**.
7. En **puerto público**, escriba Hola el número de puerto para el tráfico entrante desde Internet Hola Hola. En **puerto privado**, escriba número de puerto de hello en qué Hola está escuchando la máquina virtual. Estos números de puerto pueden ser diferentes. Asegúrese de que Hola firewall en la máquina virtual de hello ha sido configurado tooallow Hola tráfico toohello protocolo correspondiente (en el paso 6) y puerto privado.
10. Haga clic en **Aceptar**.

nuevo punto de conexión de Hola se enumerarán en hello **extremos** página.

![Creación correcta del extremo](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>Administrar Hola ACL en un punto de conexión
conjunto de hello toodefine de equipos que pueden enviar tráfico, Hola ACL en un punto de conexión puede restringir el tráfico en función de la dirección IP de origen. Siga estos pasos tooadd, modificar o quitar una ACL en un punto de conexión.

> [!NOTE]
> Si el punto de conexión de hello forma parte de un conjunto de equilibrio de carga, los cambios que realice toohello ACL en un punto de conexión son extremos tooall aplicados en el conjunto de Hola.
>
>

Si la máquina virtual de hello está en una red virtual de Azure, se recomienda grupos de seguridad de red en lugar de la ACL. Para obtener más información, consulte [Información sobre los grupos de seguridad de red](../articles/virtual-network/virtual-networks-nsg.md).

1. Si aún no lo ha hecho, inicie sesión en toohello portal de Azure.
2. Haga clic en **máquinas virtuales**y, a continuación, haga clic en nombre de Hola de máquina virtual de Hola que desea tooconfigure.
3. Haga clic en **Extremos**. En lista de hello, seleccione el punto de conexión adecuado de Hola. la lista ACL Hello es final Hola de página Hola.

   ![Especificar los detalles de ACL](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. Filas en tooadd de lista de hello, eliminar o editar reglas se utilizan para una ACL y cambiar su orden. Hola **subred remota** valor es un intervalo de direcciones IP para el tráfico entrante de hello Internet que Hola toopermit de usos de equilibrador de carga de Azure o denegar el tráfico de hello en función de su dirección IP de origen. Ser seguro toospecify Hola intervalo de direcciones IP en formato CIDR, también conocido como formato de prefijo de dirección. Un ejemplo es `10.1.0.0/8`.

 ![Nueva entrada de ACL](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


Puede usar reglas tooallow solo el tráfico desde equipos específicos correspondiente equipos tooyour sobre el tráfico de Internet y toodeny de hello en intervalos de direcciones específicas, que se conoce.

Hola reglas se evalúan en orden, comenzando por la primera regla de Hola y terminando con la regla del último Hola. Esto significa que las reglas deben estar ordenadas de menos restrictivo toomost restrictivo. Para obtener ejemplos y más información, consulte [¿Qué es una lista de control de acceso (ACL) de extremo?](../articles/virtual-network/virtual-networks-acl.md)
