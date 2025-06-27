# 🔧 Recuperando GRUB2 tras borrar `grub.cfg` (a propósito)  

---

En esta práctica nos vamos a meter en un pequeño "lío controlado": vamos a **"borrar accidentalmente"** el archivo `grub.cfg`, lo que nos impedirá arrancar el sistema de forma automática. Pero no te preocupes, lo haremos manualmente desde la terminal de GRUB y lo recuperaremos en unos segundos 🛠️.

---

## 💥 Algunas consideraciones previas del `grub.cfg`

- `grub.cfg` es el **archivo de configuración principal** de GRUB2.
- ⚠️ **No debería editarse directamente.** En su lugar, debemos modificar `/etc/default/grub` y luego regenerar el archivo.
- Este archivo contiene las entradas del sistema, con sus respectivas directivas `menuentry` y sus opciones.
- Si falta, **GRUB no puede iniciar el sistema automáticamente**. Tendremos que arrancarlo **manualmente desde la terminal de GRUB**.

---

## 🚀 ¡A la acción!  
Borramos `grub.cfg` y reiniciamos el sistema. Llegamos a la terminal de GRUB. Aquí empieza lo interesante...

---

## 📘 Teoría para recuperar GRUB2

1. 🔍 Localizar la **partición raíz** del sistema.
2. 🧩 Identificar dos archivos clave:  
   - `vmlinuz` (el kernel)  
   - `initrd` o `initramfs` (imagen del disco RAM inicial)  
3. 💡 Puedes revisar conceptos en: *[dmesg, vmlinuz y initramfs: Mensajes del arranque del sistema]*

---

## 🧪 Práctica paso a paso

### 1. 🔍 Localizar la partición raíz  

Para identificarla:

```bash
ls (hd0,msdos1)/
```

> (la barra final `/` es importante para listar el contenido)

Una vez localizada, la establecemos como partición raíz:

```bash
set root=(hd0,msdos1)
```

---

### 2. 🧠 Cargar el kernel  

Puede estar en `/boot`, pero en muchos casos está directamente en la raíz:

```bash
linux /vmlinuz root=/dev/sda1
```

> Asegúrate de conocer el nombre del dispositivo en Linux (`/dev/sda1`, por ejemplo).

---

### 3. 🧵 Cargar el `initrd` o `initramfs`  

Suele estar en el mismo directorio que el kernel:

```bash
initrd /initrd.img
```

---

### 4. 🎬 Arrancar el sistema  

Cuando todo esté listo:

```bash
boot
```

¡Y cruza los dedos para que lo hayas hecho todo bien! De lo contrario, tendrás que hacerlo todo otra vez. 🤞

---

## 🔄 Tras iniciar el sistema  

Una vez el sistema haya arrancado, es **fundamental regenerar `grub.cfg`** para que GRUB vuelva a funcionar de forma automática.

En sistemas basados en Debian (como Ubuntu), el comando habitual es:

```bash
update-grub
```

📌 Revisa el manual de tu distro si usas otra.
