# Web Application Security plus DDoS protection utilizing Cloudflare
Proxying the traffic through Cloudflare network adds additional capabilites: WAF, DDoS, Bot Protection ETC,.

## Managed WAF Rules (Free Tier)
1. Log4J rules matching payloads in the URI and HTTP headers;
1. Shellshock rules; [Shellshock Document](https://blog.cloudflare.com/inside-shellshock/)
1. Rules matching very common WordPress exploits;

[Documentation](https://blog.cloudflare.com/waf-for-everyone/)

## Unmetered DDoS Protection (Free Tier)
[Documentation](https://blog.cloudflare.com/unmetered-mitigation/)


## Available DDoS alert notifications
- HTTP DDoS Attack Alert
- Layer 3/4 DDoS Attack Alert
- Advanced HTTP DDoS Attack Alert
- Advanced Layer 3/4 DDoS Attack Alert

[Documentation](https://developers.cloudflare.com/learning-paths/prevent-ddos-attacks/baseline/set-up-alerts/)


## Protect Admin pages with custom WAF Rule.
- [Documentation](https://developers.cloudflare.com/waf/custom-rules/use-cases/site-admin-only-known-ips/)
- Expression: `not ip.src in {10.20.30.40 192.168.1.0/24} and starts_with(lower(http.request.uri.path), "/wp-admin"))`
- Action: `Block`

## Bot Fight Mode
Bot Fight Mode is a simple, free product that helps detect and mitigate bot traffic on your domain. When enabled, the product:

1. Identifies traffic matching patterns of known bots
1. Issues computationally expensive challenges in response to these bots
1. Notifies Bandwidth Alliance partners (if applicable) to disable bots

Cannot be skipped by Rules

## Scrape Shield
1. [Email Address Obfuscation](https://developers.cloudflare.com/waf/tools/scrape-shield/email-address-obfuscation/)
1. [Server Side Excludes](https://developers.cloudflare.com/waf/tools/scrape-shield/server-side-excludes/)
1. [Hotlink Protection](https://developers.cloudflare.com/waf/tools/scrape-shield/hotlink-protection/)

## YouTube video
[Link to the Video](https://youtu.be/AnI684MAITA)

## High Level Architecture Overview
![High Level Overview](./Cloudflare%20Web%20Application%20Security.png)


### Components
1. Web Application Running on AWS with Public Hostname or IP Address
    1. Cloudflare signed/or 3rd party signed TLS/SSL Certificate is installed on the reverse proxy to enable "End-To-End Encryption"
    1. Security Group exposing the port 443 for the Cloudflare IPs
1. DNS Managed by Cloudflare - `PROXY` Enabled
1. Cloudflare WAF
    1. Custom Rules Added

### Resources
#### WAF Block Python User Agents
1. `(http.user_agent contains "python")`

#### Allow Admin Access from IP
1. `(http.host eq "<hostname>" and http.request.uri.path contains "/admin" and ip.src eq 84.1.222.29)`

#### Allow API and Uploads folder reqeuests
`(http.host eq "<hostname>" and http.request.uri.path contains "/api/pictures") or (http.host eq "<hostname>" and http.request.uri.path contains "/uploads")`

#### Block All requests
`(http.host eq "<hostname>")`