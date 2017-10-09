Cuando ya no necesita un disco de datos que es un equipo virtual tooa conectados, puede separar fácilmente. Separar un disco quita el disco de saludo de la máquina virtual de hello, pero no elimina el disco de Hola Hola cuenta de almacenamiento de Azure.

Si desea volver a datos existentes de toouse hello en el disco de hello, puede adjuntarla toohello misma máquina virtual, u otro.  

> [!NOTE]
> toodetach un disco del sistema operativo, primero debe máquina virtual de toodelete Hola.
>

## <a name="find-hello-disk"></a>Encuentra el disco de Hola
Si no conoce el nombre hello de Hola disco o desea tooverify, antes de separarla, siga estos pasos.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. Haga clic en **máquinas virtuales**, y, a continuación, seleccione Hola VM adecuado.

3. Haga clic en **discos** a lo largo de hello borde izquierdo del panel de la máquina virtual de hello, en **configuración**.

 panel de la máquina virtual de Hello muestra hello nombre y tipo de todos los discos conectados. Por ejemplo, esta pantalla muestra una máquina virtual con un disco de sistema operativo y un disco de datos:

    ![Buscar disco de datos](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a>Desconectar el disco de Hola
1. En el portal de Azure hello, haga clic en **máquinas virtuales**y, a continuación, haga clic en nombre de Hola de máquina virtual de Hola que tiene un disco de datos de hello desea toodetach.

2. Haga clic en **discos** a lo largo de hello borde izquierdo del panel de la máquina virtual de hello, en **configuración**.

3. Haga clic en el disco de Hola que desee toodetach.

  ![Identificar Hola disco toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. En la barra de comandos de hello, haga clic en **separar**.

  ![Busque Hola detach, comando](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. En la ventana de confirmación de hello, haga clic en **Sí** disco de hello toodetach.

  ![Confirmar desconectando el disco Hola](./media/howto-detach-disk-windows-linux/confirmdetach.png)

disco de Hello permanece en el almacenamiento pero ya no es máquina virtual de tooa adjunto.
