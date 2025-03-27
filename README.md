# Free Proxy List

![Proxy List](https://img.shields.io/badge/Proxies-Updated_Every_6_Hours-brightgreen)
![GitHub stars](https://img.shields.io/github/stars/thenasty1337/free-proxy-list?style=social)
![GitHub forks](https://img.shields.io/github/forks/thenasty1337/free-proxy-list?style=social)

🔥 **Need Reliable Premium Proxies?** [Get Enterprise-Grade Proxies at ProxyProvider.net](https://proxyprovider.net) 🔥

Simple, clean proxy lists updated every 6 hours. No registration, no limits.

## Quick Access

### Plain Text Lists (IP:PORT)

- [All Proxies](https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/proxies.txt)
- [HTTP Proxies](https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/http/proxies.txt)
- [SOCKS4 Proxies](https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/socks4/proxies.txt) 
- [SOCKS5 Proxies](https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/socks5/proxies.txt)

## API Access

Easily access proxies via our API:

```
http://api.proxyprovider.net/api/free-proxies/all
```

Response format:
```json
{
  "data": [
    {
      "ip": "216.229.112.25",
      "port": "8080",
      "ipPort": "216.229.112.25:8080",
      "country": "US",
      "proxy_level": "elite",
      "type": "http",
      "supports_https": false,
      "supports_get": true,
      "supports_post": true,
      "country_name": "United States"
    },
    ...
  ],
  "meta": {
    "total": 5
  }
}
```

### Need Premium API Access?

For high-volume requests, 99.9% uptime SLA, and dedicated support, check out our [Premium API Plans](https://proxyprovider.net/api)

## Batch Download

### Linux/macOS
```bash
# Download all proxy lists
mkdir -p proxies && cd proxies
curl -s https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/proxies.txt -o all.txt
curl -s https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/http/proxies.txt -o http.txt
curl -s https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/socks4/proxies.txt -o socks4.txt
curl -s https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/socks5/proxies.txt -o socks5.txt
```

### Windows (PowerShell)
```powershell
# Download all proxy lists
New-Item -Path "proxies" -ItemType Directory -Force
cd proxies
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/proxies.txt" -OutFile "all.txt"
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/http/proxies.txt" -OutFile "http.txt"
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/socks4/proxies.txt" -OutFile "socks4.txt"
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest/types/socks5/proxies.txt" -OutFile "socks5.txt"
```

## Why Premium Proxies?

While these free proxies are great for basic testing, they have limitations:
- **Limited Speed**: Free proxies are often overloaded
- **Unreliable Uptime**: May go offline without notice
- **Shared IPs**: Used by many other users
- **Limited Location Options**: Mostly from a few countries

**[Upgrade to Premium Proxies](https://proxyprovider.net)** for:
- ✅ 99.9% Uptime Guarantee
- ✅ Lightning-Fast Speeds (100Mbps+)
- ✅ Dedicated IPs (not shared)
- ✅ 195+ Countries Available
- ✅ 24/7 Technical Support
- ✅ Unlimited Bandwidth

## Automation Tools

### Proxy Rotation Script (Python)
```python
import requests
import random
import time

def get_proxies(proxy_type='all'):
    """Fetch the latest proxies from the repo"""
    base_url = "https://raw.githubusercontent.com/thenasty1337/free-proxy-list/main/data/latest"
    
    if proxy_type == 'http':
        url = f"{base_url}/types/http/proxies.txt"
    elif proxy_type == 'socks4':
        url = f"{base_url}/types/socks4/proxies.txt"
    elif proxy_type == 'socks5':
        url = f"{base_url}/types/socks5/proxies.txt"
    else:
        url = f"{base_url}/proxies.txt"
    
    response = requests.get(url)
    if response.status_code == 200:
        return [line.strip() for line in response.text.splitlines() if line.strip()]
    return []

def test_proxy(proxy, test_url="https://api.ipify.org/"):
    """Test if a proxy is working"""
    try:
        ip, port = proxy.split(':')
        proxies = {
            'http': f'http://{proxy}',
            'https': f'http://{proxy}'
        }
        response = requests.get(test_url, proxies=proxies, timeout=5)
        return response.status_code == 200
    except:
        return False

def get_working_proxy(proxy_type='all', max_attempts=10):
    """Get a working proxy with retries"""
    proxies = get_proxies(proxy_type)
    random.shuffle(proxies)
    
    for _ in range(max_attempts):
        if not proxies:
            proxies = get_proxies(proxy_type)
            if not proxies:
                return None
        
        proxy = proxies.pop(0)
        if test_proxy(proxy):
            return proxy
            
    return None

# Example usage
proxy = get_working_proxy('http')
if proxy:
    print(f"Found working proxy: {proxy}")
    # Use the proxy
    proxies = {
        'http': f'http://{proxy}',
        'https': f'http://{proxy}'
    }
    response = requests.get("https://api.ipify.org/", proxies=proxies)
    print(f"Current IP: {response.text}")
```

## Usage Examples

### cURL
```bash
curl -x 216.229.112.25:8080 https://api.ipify.org/
```

### Python
```python
import requests

proxies = {
    'http': 'http://216.229.112.25:8080',
    'https': 'http://216.229.112.25:8080',
}

response = requests.get('https://api.ipify.org/', proxies=proxies)
print(response.text)
```

### Node.js
```javascript
const axios = require('axios');

const proxy = {
  host: '216.229.112.25',
  port: 8080
};

axios.get('https://api.ipify.org/', { proxy })
  .then(response => console.log(response.data));
```

### PHP
```php
<?php
$proxy = '216.229.112.25:8080';
$context = stream_context_create([
    'http' => [
        'proxy' => "tcp://$proxy",
        'request_fulluri' => true,
    ],
]);
echo file_get_contents('https://api.ipify.org/', false, $context);
?>
```

### Wget
```bash
wget -e use_proxy=yes -e http_proxy=216.229.112.25:8080 https://api.ipify.org/
```

### Go
```go
package main

import (
    "fmt"
    "io/ioutil"
    "net/http"
    "net/url"
)

func main() {
    proxyURL, _ := url.Parse("http://216.229.112.25:8080")
    client := &http.Client{
        Transport: &http.Transport{
            Proxy: http.ProxyURL(proxyURL),
        },
    }
    resp, _ := client.Get("https://api.ipify.org/")
    body, _ := ioutil.ReadAll(resp.Body)
    fmt.Println(string(body))
}
```

## Formats Available

### Plain Text (IP:PORT)
One proxy per line:
```
216.229.112.25:8080
168.196.214.187:80
41.219.117.1:80
```

### JSON (Detailed Information)
For advanced use cases, JSON files include:
- IP address and port
- Country
- Proxy type (HTTP, SOCKS4, SOCKS5)
- Performance metrics
- Support details

## Updates

Proxies are automatically verified and updated every 6 hours, so you always have fresh working proxies.

---

### 🚀 Need enterprise-grade proxies for mission-critical applications?

[ProxyProvider.net](https://proxyprovider.net) offers premium residential, datacenter, and mobile proxies with guaranteed uptime, dedicated support, and advanced features.

**Special offer:** Use code `GITHUB10` for 10% off your first order!

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
