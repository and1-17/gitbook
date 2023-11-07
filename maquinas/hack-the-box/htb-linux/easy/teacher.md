# 🏳 Teacher

<figure><img src="../../../../.gitbook/assets/0_qhjtinr-ij_ugB68.png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="227">Datos</th><th width="288.3333333333333"> </th><th>Notas</th></tr></thead><tbody><tr><td>Nombre de la máquina: </td><td><a href="https://app.hackthebox.com/machines/165">Teacher</a></td><td></td></tr><tr><td>IP de la máquina:</td><td>10.10.10.253</td><td></td></tr><tr><td>Sistema simulado: </td><td>Debian</td><td></td></tr><tr><td>Servicio vulnerado: </td><td>Moodle 3.9</td><td></td></tr><tr><td>CVEs:</td><td><a href="https://nvd.nist.gov/vuln/detail/CVE-2018-1133">CVE 2018-1133</a></td><td></td></tr></tbody></table>

### 1. Enumeración y descubrimiento

Comenzamos el ejercicio lanzando un nmap a la IP 10.10.10.153

<figure><img src="../../../../.gitbook/assets/1 (13).png" alt=""><figcaption></figcaption></figure>

Y buscamos la web en el navegador accediendo a un portal de un instituto.

<figure><img src="../../../../.gitbook/assets/2 (14).png" alt=""><figcaption></figcaption></figure>

Revisando el código de la web nos encontramos que existe un mensaje extraño dentro del código.

<figure><img src="../../../../.gitbook/assets/3 (13).png" alt=""><figcaption></figcaption></figure>

Al intentar entrar en la imagen nos encontramos que no podemos acceder.

<figure><img src="../../../../.gitbook/assets/4 (10).png" alt=""><figcaption></figcaption></figure>

Seguimos indagando y encontramos que no es una imagen realmente, lanzamos un curl a la web y encontramos el siguiente mensaje.

<figure><img src="../../../../.gitbook/assets/5 (10).png" alt=""><figcaption></figcaption></figure>

Accedemos a Moddle y descubrimos que Giovanni es un profesor con un curso de algebra. Lo primero que vamos a hacer por ello es generar un diccionario que cumpla las características que marca en el mensaje.

<figure><img src="../../../../.gitbook/assets/6 (8).png" alt=""><figcaption></figcaption></figure>

Utilizaremos el proxy de burpsuite para capturar la petición e insertar por fuerza bruta el diccionario de contraseñas que tenemos hasta dar con cual es la necesaria.

<figure><img src="../../../../.gitbook/assets/7 (8).png" alt=""><figcaption></figcaption></figure>

Tras hacer eso encontramos que la contraseña correcta es “Th4C00lTheacha#”. Con esto iniciamos sesión como el usuario de “Giovanni Chhatta”.

<figure><img src="../../../../.gitbook/assets/8 (8).png" alt=""><figcaption></figcaption></figure>

En este punto nos aprovecharemos del CVE 2018-1133 para conseguir acceso. Para ello crearemos un Quiz y lo editaremos añadiendo una pregunta de cálculo en la que pondremos como respuesta a la fórmula “/\*{a\*/\`$\_GET\[0]\`;//{x\}}\`”.

<figure><img src="../../../../.gitbook/assets/9 (7).png" alt=""><figcaption></figcaption></figure>

Al inyectar encodear el comando e inyectarlo en la URL, conseguimos generar una conexión con el netcat que tenemos desplegado en la IP 1337.

<figure><img src="../../../../.gitbook/assets/10 (9).png" alt=""><figcaption></figcaption></figure>

No podemos acceder con el usuario www-data al directorio home de Giovanni, por lo que se requiere más información para conseguir elevar privilegios. Buscamos en el archivo config.php de Moodle, en el cual es posible encontrar algunos usuarios y contraseñas.

<figure><img src="../../../../.gitbook/assets/11 (5).png" alt=""><figcaption></figcaption></figure>

Buscaremos iniciar sesión con esa contraseña como root en la base de datos y consultamos la base de datos de usuarios obteniendo el hash de la contraseña y con [crackstation](https://crackstation.net/) obtendremos la contraseña “expelled”.

<figure><img src="../../../../.gitbook/assets/12 (8).png" alt=""><figcaption></figcaption></figure>

Con esto podremos iniciar sesión como Giovanni pudiendo ver la flag del usuario.

<figure><img src="../../../../.gitbook/assets/13 (4).png" alt=""><figcaption></figcaption></figure>

### 2. Escalada de privilegios

En este punto tendremos que conseguir acceder a la máquina como root. Empezamos inspeccionando el directorio home de Giovanni, en concreto con el directorio “work”.

<figure><img src="../../../../.gitbook/assets/14 (3).png" alt=""><figcaption></figcaption></figure>

Tras analizar el archivo /usr/bin/backup.sh nos damos cuenta de que existe un script recursivo que proporciona permisos a una carpeta. Por ello lo que hacemos es mover los cursos a nuestra carpeta work y dentro de ahí conseguir vincularla a root adquiriendo permisos mediante el script. Con ello podremos ver la flag de root.

<figure><img src="../../../../.gitbook/assets/25 (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Si te he ayudado sígueme y apóyame en [Hack The Box ](https://app.hackthebox.com/profile/819073)
{% endhint %}
