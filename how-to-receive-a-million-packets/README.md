Test 10G network UDP throughput - more details here: https://blog.cloudflare.com/how-to-receive-a-million-packets/

- Clone this repo
<pre>
cd ~/projects
git clone https://github.com/mslavescu/dump
</pre>

- Build udpclient and udpserver, do this on both client and server machines
<pre>
cd ~/projects/dump/how-to-receive-a-million-packets
./build.sh
</pre>

- Run on server (with sample output, 1.155M pps means 1.155 milions of packets per second)
<pre>
cd ~/projects/dump/how-to-receive-a-million-packets
taskset -c 1 ./udpreceiver1 0.0.0.0:4321
[*] Starting udpreceiver on 0.0.0.0:4321, recv buffer 4KiB
  0.000M pps   0.000MiB /   0.000Mb
  0.651M pps  19.880MiB / 166.769Mb
  1.149M pps  35.079MiB / 294.263Mb
  1.151M pps  35.127MiB / 294.666Mb
  1.147M pps  35.010MiB / 293.688Mb
  1.137M pps  34.714MiB / 291.198Mb
  1.139M pps  34.752MiB / 291.524Mb
  1.155M pps  35.248MiB / 295.679Mb
  1.153M pps  35.190MiB / 295.194Mb
  1.137M pps  34.696MiB / 291.048Mb
</pre>

- Run on client (with sample output), change IP to match server IP
<pre>
cd ~/projects/dump/how-to-receive-a-million-packets
taskset -c 1,2 ./udpsender 192.168.1.41:4321 192.168.1.41:4321
[*] Sending to 192.168.1.41:4321, send buffer 1024 packets
[*] Sending to 192.168.1.41:4321, send buffer 1024 packets
</pre>
