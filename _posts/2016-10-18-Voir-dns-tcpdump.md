tcpdump -lvi any "udp port 53" 2>/dev/null|grep -E 'A\?'|awk '{print $(NF-1)}'
