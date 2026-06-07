# sockscan
SOCKS5-friendly port scanner

Ever tried port scanning with nmap through proxychains? If you have, you know it takes until the heat death of the universe.
Nmap maintains a dynamic RTT estimator per host that increases when it sees slow responses. Through SOCKS5 the RTT estimator gets confused because proxy latency is inconsistent, often causing it to be pessimistic and wait longer.

That's why I made this little script. It is similar to the nmap -sT mode, but with:
- aggressive fixed timeouts instead of adaptive ones
- no retries
- no result correlation or state tracking

# Features:
- --proxy "socks5://..." to scan through a proxy
- top 8000-something popular ports built in - use `-p top1000`, `-p top2000` etc.
- only dependency is PySocks
- new service definitions unlike nmap's ancient ones: find things like Docker, IoT, Kubernetes and so on
- `--randomize` to look a little less suspicious (probably won't help you)
- banner grabbing (add `-b`) with support for HTTP
- pretty colors

# Usage

`sockscan.py -p- -oC portscan_results.csv -T50 --proxy socks5://localhost:5004 192.168.100.0/24 --randomize`
