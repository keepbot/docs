### Test bunch of hosts for open ports
```bash
cat > /tmp/ips-to-test.txt <<-EOF
1.1.1.1
2.2.2.2
3.3.3.3
4.4.4.4
5.5.5.5
6.6.6.6
EOF

for line in `cat /tmp/ips-to-test.txt`; do nc -z -v -w5 ${line} 443; sleep 1; done
```

### Common
```bash
sudo netstat -tunapl
```

### Which process uses port
#### Linux
```bash
# Find out PID via ss
ss -nltp | grep <port>
# Find out PID via deprecated netstat:
netstat -tulpn | grep <port>
# Find out particular binary
ls -l /proc/<pid>/exe
# Find out full run command
ps -ef | grep <PID>
```
#### AIX
```bash
lsof -i:<port>
ps -ef | grep <pid>
```
#### Windows
```bash
netstat -aon | findstr "<port>"
pslist <PID>
```

### Which port is used by a process
#### Unix
```bash
sudo lsof -i -P -n | grep LISTEN | grep <process>
# Remember about sudo: root access rights is required to see at non-current-user processes
sudo netstat -tulpn | grep LISTEN | grep <process>
# For FreeBSD or MacOS:
sudo netstat -anp tcp | grep LISTEN | grep <process>
sudo netstat -anp udp | grep LISTEN | grep <process>
# Use flags -T fot TCP -U for UDP or both. You can use any IP address instead localhost.
sudo nmap -sTU -O localhost
```
#### Windows
```bash
netstat -bano | findstr /R /C:"[LISTING]" | findstr /R /C:"<process>"
```
