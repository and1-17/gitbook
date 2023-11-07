# 🏳 Grandpa

<figure><img src="../../../../.gitbook/assets/381683fd107da11f1dc916401ae8aee0.png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="227">Datos</th><th width="288.3333333333333"> </th><th>Notas</th></tr></thead><tbody><tr><td>Nombre de la máquina: </td><td><a href="https://app.hackthebox.com/machines/13">Grandpa</a></td><td></td></tr><tr><td>IP de la máquina:</td><td>10.10.10.14</td><td></td></tr><tr><td>Sistema simulado: </td><td>Windows Server 2003</td><td></td></tr><tr><td>Servicio vulnerado: </td><td>Microsoft-IIS 6.0</td><td></td></tr><tr><td>CVEs:</td><td><a href="https://nvd.nist.gov/vuln/detail/CVE-2017-7269">2017-7269</a></td><td></td></tr></tbody></table>

### 1. Enumeración y descubrimiento

Comenzamos enumerando todos los puertos de la máquina mediante NMAP y buscando que servicios se encuentran desplegados en la máquina. Recuerda que esta enumeración la podemos hacer sin filtros ya que estamos en un entorno controlado en el que no vamos a tirar a abajo ningún servicio o llamar la atención, es por ello que enumeramos de esta manera.

```bash
nmap -sC -sV -sT 10.10.10.14 -p-
```

<figure><img src="../../../../.gitbook/assets/1 (4).png" alt=""><figcaption></figcaption></figure>

Tras esto entramos desde el navegador a la web, la cual ya podíamos ver en el nmap que está "under construction" y vemos:

<figure><img src="../../../../.gitbook/assets/2 (5).png" alt=""><figcaption></figcaption></figure>

También con NMAP hemos visto que tenemos montado, como en la máquina Granny, un servicio Microsoft-IIS 6.0 aunque parecer que la vulnerabilidad se comporta de otra manera. En este punto buscaremos con que exploit trabajaremos...&#x20;

### 2. Explotación

En esta máquina usaremos, no como en  [Granny](granny.md), metasploit para obtener acceso a la máquina.

Comenzaremos escogiendo el exploit `iis_webdav_scstoragepathfromurl` . Comenzaremos indicando los diferentes datos para configurar el exploit. Es importante revisar las opciones dle exploit al comenzar.

<figure><img src="../../../../.gitbook/assets/1 (7).png" alt=""><figcaption></figcaption></figure>

Iniciamos el exploit y conseguiremos acceso a la máquina.

<figure><img src="../../../../.gitbook/assets/2 (9).png" alt=""><figcaption></figcaption></figure>

En este punto nos damos cuenta de que tenemos una shell un poco inestable, por eso vamos a migrar esta a otro proceso. Para ello usamos ps para ver los procesos activos.

<figure><img src="../../../../.gitbook/assets/3 (4).png" alt=""><figcaption></figcaption></figure>

Nosotros usaremos el proceso `w3wp.exe` y nos migraremos a ello por eso utilizaremos `migrate`.

<figure><img src="../../../../.gitbook/assets/4 (6).png" alt=""><figcaption></figcaption></figure>

### 3. Escalada de privilegios

En este punto vamos a poner en background la sesión de meterpreter y usar un exploit suggester para ganar acceso como root. Comenzamos poniendo en background la sesión.&#x20;

<figure><img src="../../../../.gitbook/assets/5 (3).png" alt=""><figcaption></figcaption></figure>

Usaremos el `multi/recon/local_exploit_suggester` y configuraremos la sesión seleccionando la sessión 1 que es la que yo tengo activa en background.

<figure><img src="../../../../.gitbook/assets/6 (6).png" alt=""><figcaption></figcaption></figure>

Iniciamos la búsqueda de exploits que nos puedan ayudar a explotar la escalada de privilegios.&#x20;

<figure><img src="../../../../.gitbook/assets/7 (6).png" alt=""><figcaption></figcaption></figure>

Usaremos el exploit : `windows/local/ms14_058_track_popup_menu` y lo configuraremos.

<figure><img src="../../../../.gitbook/assets/10 (4).png" alt=""><figcaption></figcaption></figure>

Iniciamos el exploit y volvemos a nuestra sesión.

<figure><img src="../../../../.gitbook/assets/11 (1).png" alt=""><figcaption></figcaption></figure>

Vemos nuestro usuario y ya hemos alcanzado nuestro objetivo.

<figure><img src="../../../../.gitbook/assets/12 (2).png" alt=""><figcaption></figcaption></figure>

En este punto somos root y tenemos acceso a las flags de usuario y root finalizando la máquina.&#x20;

{% hint style="info" %}
Si te he ayudado sígueme y apóyame en [Hack The Box ](https://app.hackthebox.com/profile/819073)
{% endhint %}
