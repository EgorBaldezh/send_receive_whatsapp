# send_receive_whatsapp

Здесь я опишу установку библиотеки yowsup, которой я пользовался, а также регистрацию номера whatsapp в этой библиотеке.

Я работал в Ubuntu, поэтому терминальные команды буду писать для нее.

Для начала нужно установить библиотеку yowsup. Я писал на python 3.6, поэтому
<pre><code class="bash">pip3 install yowsup</code></pre>

Теперь в терминале регистрируем номер телефона. Номер не должен быть никак связан с whatsapp. 
<pre><code class="bash">yowsup-cli registration --requestcode sms --phone 7xxxxxxxxxx --cc 7 --mcc 250 --mnc xx --env android</code></pre>

<blockquote> phone — ваш номер телефона, начинающийся с 7 <br>
cc — country code — это код страны (для России это 7) <br>
mcc — mobile country code — это другой код страны (для России это 250) <br>
mnc — mobile network code — это код вашего оператора. (01 — МТС, 02 — мегафон, 20 — теле2, 99 — билайн) <br>
</blockquote>

В ответ придет смс с кодом вида XXX-XXX, который используем для подтверждения регистрации.
<pre><code class="bash">yowsup-cli registration --register xxx-xxx --phone 7хххxxxxxxx --cc 7</code></pre>

Сервер сообщит об удачной регистрации.

Далее в файле <pre><code class="bash">run.py</code></pre> необходимо в переменной CREDENTIALS поменять номер на свой.
Скрипт готов к запуску.
Чтобы отослать сообщение по номеру, пишем команду
<pre><code class="bash">python3 run.py send 7xxxxxxxxxx 'message'</code></pre>
где 7xxxxxxxxxx - номер на который отсылается сообщение,
'message' - само сообщение.

Чтобы принимать сообщения в фоне, пишем
<pre><code class="bash">python3 run.py recv</code></pre>
Скрипт будет записывать все сообщения и адрес, откуда они пришли. После того как мы закроем процесс (CTRL+C, например), программа выведет нам список всех адресантов и сообщений.
