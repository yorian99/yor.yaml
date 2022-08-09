# yor.yaml
--- proxy-groups: - name: Gaming   type: select   disable-udp: false   proxies:   - DIRECT   - LINKGO   - '20'   url: http://www.gstatic.com/generate_204   interval: '300' - name: Umum   type: fallback   disable-udp: false   proxies:   - LINKGO   - '20'   url: http://www.gstatic.com/generate_204   interval: '300' - name: Sosmed   type: fallback   disable-udp: false   proxies:   - LINKGO   - '20'   url: http://www.gstatic.com/generate_204   interval: '300'   tolerance: '150' - name: Streaming   type: fallback   disable-udp: false   proxies:   - LINKGO   - '20'   url: http://www.gstatic.com/generate_204   interval: '300'   tolerance: '150' - name: Youtube   type: fallback   disable-udp: false   proxies:   - LINKGO   - '20'   url: http://www.gstatic.com/generate_204   interval: '300' - name: Reject   type: select   disable-udp: false   proxies:   - REJECT - name: Load Balance   type: load-balance   strategy: round-robin   disable-udp: false   proxies:   - LINKGO   - '20'   url: http://www.gstatic.com/generate_204   interval: '300' redir-port: 7892 port: 7890 socks-port: 7891 mixed-port: 7893 mode: rule log-level: silent allow-lan: true external-controller: 0.0.0.0:9090 secret: yori bind-address: "*" external-ui: "/usr/share/openclash/dashboard" dns:   enable: true   ipv6: false   enhanced-mode: fake-ip   listen: 127.0.0.1:7874   nameserver:   - 10.106.197.125   - dhcp://"wwan0"   - 114.114.114.114   - 119.29.29.29   - https://doh.pub/dns-query   - https://dns.alidns.com/dns-query   fallback:   - https://cloudflare-dns.com/dns-query   - https://dns.google/dns-query   - https://1.1.1.1/dns-query   - tls://8.8.8.8:853   tproxy-port: 7895   fake-ip-filter:   - "+.*"   default-nameserver:   - 10.76.197.65   - 114.114.114.114   - 119.29.29.29   - 10.129.204.9   - 8.8.8.8   - 8.8.4.4   - 10.106.197.125   fake-ip-range: 198.18.0.1/16 ipv6: false profile:   store-selected: true   store-fake-ip: true rules: - DST-PORT,7895,REJECT - DST-PORT,7892,REJECT - SRC-IP-CIDR,192.168.1.1/32,DIRECT - SRC-IP-CIDR,198.18.0.1/32,DIRECT - RULE-SET,Umum,Umum - RULE-SET,Sosmed,Sosmed - RULE-SET,Streaming,Streaming - RULE-SET,Youtube,Youtube - RULE-SET,Gaming,Gaming - RULE-SET,Reject,Reject - RULE-SET,Load Balance,Load Balance - IP-CIDR,198.18.0.1/16,REJECT,no-resolve - MATCH,GLOBAL rule-providers:   Umum:     type: http     behavior: classical     path: "./rule_provider/umum.yaml"     url: https://raw.githubusercontent.com/latifangren/RULE-PROVIDER/main/umum.yaml     interval: 86400   Sosmed:     type: http     behavior: classical     path: "./rule_provider/sosmed.yaml"     url: https://raw.githubusercontent.com/latifangren/RULE-PROVIDER/main/sosmed.yaml     interval: 86400   Streaming:     type: http     behavior: classical     path: "./rule_provider/streaming.yaml"     url: https://raw.githubusercontent.com/latifangren/RULE-PROVIDER/main/streaming.yaml     interval: 86400   Youtube:     type: http     behavior: classical     path: "./rule_provider/youtube.yaml"     url: https://raw.githubusercontent.com/latifangren/RULE-PROVIDER/main/youtube.yaml     interval: 86400   Gaming:     type: http     behavior: classical     path: "./rule_provider/gaming.yaml"     url: https://raw.githubusercontent.com/latifangren/RULE-PROVIDER/main/gaming.yaml     interval: 86400   Reject:     type: http     behavior: classical     path: "./rule_provider/reject.yaml"     url: https://raw.githubusercontent.com/latifangren/RULE-PROVIDER/main/reject.yaml     interval: 86400   Load Balance:     type: http     behavior: classical     path: "./rule_provider/Load Balance.yaml"     url: https://raw.githubusercontent.com/latifangren/RULE-PROVIDER/main/Load Balance.yaml     interval: 86400 proxies: - name: LINKGO   type: trojan   server: id2.skr-sshvpn.my.id   port: 443   password: yorii   udp: true   sni: cos.image.joox.com   skip-cert-verify: true - name: '20'   type: vmess   server: id-lb.sshkit.org   port: 443   uuid: 6fea1649-425b-4092-bf53-29792152c925   alterId: 0   cipher: auto   udp: true   skip-cert-verify: true   tls: true   servername: cos.image.joox.com   network: ws   ws-opts:     path: "/sshkit/gaspol/62ce468ee0c95/" tproxy-port: 7895
