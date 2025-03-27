# Free Proxy List

This repository contains regularly updated lists of free proxies in both JSON and TXT formats.

## Structure

- `/data/latest/` - Contains the most recent proxy lists
  - `proxies.json` - Complete proxy details in JSON format
  - `proxies.txt` - Simple IP:PORT format, one proxy per line
  - `/types/` - Proxies organized by type
    - `/http/` - HTTP proxies
    - `/socks4/` - SOCKS4 proxies
    - `/socks5/` - SOCKS5 proxies

- `/data/YYYY-MM/DD/HH-MM/` - Historical proxy lists organized by timestamp

## Usage

### TXT Format (IP:PORT)
Simply grab the raw version of the TXT file:
- Latest proxies: https://raw.githubusercontent.com/USERNAME/free-proxy-list/main/data/latest/proxies.txt
- Latest HTTP proxies: https://raw.githubusercontent.com/USERNAME/free-proxy-list/main/data/latest/types/http/proxies.txt
- Latest SOCKS4 proxies: https://raw.githubusercontent.com/USERNAME/free-proxy-list/main/data/latest/types/socks4/proxies.txt
- Latest SOCKS5 proxies: https://raw.githubusercontent.com/USERNAME/free-proxy-list/main/data/latest/types/socks5/proxies.txt

### JSON Format
JSON files contain complete proxy details including:
- IP address and port
- Country
- Speed
- Protocol support details
- Last checked time

## Updates
The proxy lists are automatically updated every 6 hours.

## License
This data is free to use for any purpose.

## 🔄 Latest Update

Our proxy lists are automatically updated every 6 hours. Each update is organized in date-based folders containing both `.txt` and `.json` formats for easy integration into your projects.

## 📋 Proxy Types Available

Our free list includes a mix of:
- HTTP/HTTPS proxies
- SOCKS4/SOCKS5 proxies
- Anonymous proxies
- Transparent proxies

## 📊 Proxy Formats

Each proxy in our list includes:
- IP Address
- Port
- Protocol type
- Country
- Anonymity level
- Response time

## 🚀 How to Use

### Direct Download
Simply download the latest proxies from the most recent date folder:
- `proxies.txt` - Line by line format
- `proxies.json` - Structured JSON format

### Via API (Coming Soon)
We're developing a simple API to fetch the latest proxies programmatically.

### Implementation Examples

#### Python Example
```python
import requests
import json

# Load proxies from JSON file
with open('YYYY-MM-DD/proxies.json', 'r') as f:
    proxies = json.load(f)

# Use a proxy
proxy_url = f"{proxies[0]['protocol']}://{proxies[0]['ip']}:{proxies[0]['port']}"
response = requests.get('https://httpbin.org/ip', proxies={'http': proxy_url, 'https': proxy_url})
print(response.json())
```

#### JavaScript Example
```javascript
fetch('YYYY-MM-DD/proxies.json')
  .then(response => response.json())
  .then(proxies => {
    const proxy = proxies[0];
    console.log(`Using proxy: ${proxy.ip}:${proxy.port}`);
    // Your implementation here
  });
```

## ⚠️ Limitations of Free Proxies

Free proxies come with inherent limitations:
- **Reliability**: May go offline without notice
- **Speed**: Generally slower than premium proxies
- **Security**: Lower level of anonymity
- **Restrictions**: May be blocked by certain websites

## 🔒 Need More Reliable Proxies?

For professional, business, or high-volume usage, check out our premium proxy solutions at [ProxyProvider.net](https://proxyprovider.net).

### Premium Benefits at ProxyProvider.net:
- **Residential Proxies**: Access the internet through real residential IPs from 195+ countries
- **Unlimited Residential Plans**: Unlimited bandwidth for large-scale operations
- **Datacenter Proxies**: High-speed dedicated IPs for maximum performance
- **ISP Proxies**: The perfect balance of speed and legitimacy
- **IPv6 Proxies**: Next-generation IP addresses with enhanced capabilities
- **24/7 Support**: Dedicated technical assistance
- **99.9% Uptime**: Guaranteed reliability for mission-critical tasks
- **Rotating or Static Options**: Flexible configuration for your specific needs

## 📈 Use Cases

Our proxies are perfect for:
- Web scraping and data collection
- Market research and competitor analysis
- Ad verification
- Social media management
- SEO monitoring
- Price comparison
- Game automation
- Accessing geo-restricted content

## 📜 License

This repository and the proxy lists are provided for educational purposes only. Check the legal regulations in your country before using proxies.

## 🤝 Contributing

Found a bug or want to contribute? Open an issue or submit a pull request!

## 📞 Contact

For questions or premium proxy inquiries:
- Website: [ProxyProvider.net](https://proxyprovider.net)
- Email: support@proxyprovider.net

---

⭐ **Star this repository if it's useful!** ⭐

*Note: The free proxy lists provided here are collected from public sources. While we strive to keep the lists up-to-date and working, we cannot guarantee their performance or availability.*
