Test 10G network latency - more details here: https://blog.cloudflare.com/how-to-achieve-low-latency/

- Clone this repo
<pre>
cd ~/projects
git clone https://github.com/mslavescu/dump
</pre>

- Build udpclient and udpserver, do this on both client and server machines
<pre>
cd ~/projects/dump/how-to-receive-a-packet
./build.sh
</pre>

- Run on server
<pre>
cd ~/projects/dump/how-to-receive-a-packet
taskset -c 1 ./udpserver --polling
[*] Starting udpreceiver on 0.0.0.0:4321, polling=1, busy_poll=0, threads=1, reuseport=0
</pre>

- Run on client (with sample output), change IP to match server IP
<pre>
cd ~/projects/dump/how-to-receive-a-packet
taskset -c 1 ./udpclient 192.168.1.41:4321  --polling  --timestamp
[*] Sending to 192.168.1.41:4321, polling=1, src_port=65500
pps= 15230 avg= 65.338us dev= 43.086us min= 0.000us  (packet=1.987us/0.385)  
pps= 15352 avg= 64.822us dev= 35.948us min=61.151us  (packet=1.994us/0.212)  
pps= 15495 avg= 64.221us dev= 25.941us min=51.811us  (packet=1.972us/0.259)  
pps= 15244 avg= 65.287us dev= 42.988us min=56.351us  (packet=1.979us/0.254)  
pps= 15403 avg= 64.605us dev= 28.233us min=51.221us  (packet=1.974us/0.208)  
pps= 15270 avg= 65.172us dev= 37.634us min=54.731us  (packet=1.982us/0.283)  
</pre>
