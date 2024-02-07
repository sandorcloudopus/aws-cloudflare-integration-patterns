# Cloudflare ZTNA to AWS VPC
Cloudflare Zero Trust Network Access can provide secure access to AWS VPC, it can replace traditional VPN solutions.

## Cloudflare ZTNA Overview
![Cloudflare Zero Trust Network](./Cloudflare%20Zero%20Truse%20Network.png)

Zero Trust Network Access (ZTNA) technologies create secure boundaries around applications. When resources are protected with ZTNA, users are only allowed to access resources after verifying the identity, context, and policy adherence of each specific request.

### Features
#### Global Edge Network
Cloudflare’s global Anycast network not only makes user connections faster than a VPN, but also ensures that remote workforces of any size can securely and swiftly connect to corporate resources as needed — without requiring additional time-consuming configuration by administrators.

#### Lightweight client
The Cloudflare WARP client utilizes the more modern Wireguard protocol, which runs in user space to support a broader set of OS options with faster user experience than traditional options. Cloudflare’s WARP client can be configured on Windows, MacOS, iOS, Android, and soon Linux devices.

#### DDoS by default
Cloudflare’s network provides built-in DDoS protection for any ZTNA mode, defending networks against the largest
volumetric attacks.

#### Built-in network firewall
Cloudflare enables administrators to enforce network firewall policies at the edge, giving them fine-grained control over
which data is allowed in and out of their network and improving visibility into how traffic flows through it.

## AWS VPC Overview
With Amazon Virtual Private Cloud (Amazon VPC), you can launch AWS resources in a logically isolated virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS.

### Connectivity Challenges of AWS VPC
1. How can I access a private Database?
1. How can I access a private EKS Cluster
1. How can I access part of the network?
1. How can I access multiple VPC? (Without changing VPN Config and Hub and Spoke topology?)
1. How can I create a secure bastion?
    1. How can I rotate the bastion ssh-key?
    1. How can I configure bastion remotely? programatically?
1. How can I provide Zero Trust Access to my developers, business people and 3rd party?
1. How can I expose an internal developer tool securely?

## Integrating Cloudflare ZTNA with AWS VPC
Integrating Cloudflare ZTNA with AWS VPC is a straightforward process.

1. Create a Tunnel Within the VPC Network.
    1. Create an EC2 within a public access to the Internet
        1. You can restrict incoming traffic with Security Groups, there is no incoming traffic.
        1. You can restrict outgoing traffic with OS Firewall based on Cloudflare Hostnames (firewalld)
            1. [Outgoing Traffic to Cloudflare](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/deploy-tunnels/tunnel-with-firewall/)
    1. Install the Cloudflared Software on EC2
        1. [cloudflared](https://pkg.cloudflare.com/index.html)
    1. Install the Tunnel (follow from the Cloudflare console)
1. Create a Route for the Tunnel
    1. Determine the CIDR Range within the VPC
1. Enable ZTNA with Identity Providers
    1. SAML
    1. One Time Password
    1. GitHub
    1. ETC...
1. Configure WARP Client Authentication
1. Configure Gateway Network Policies
1. (optionally you can configure split tunneling)

### Overview
![Overview](./Zero%20Trust%20Access%20-%20High%20Level%20Overview.png)

### Split Tunneling
![Split Tunneling](./Zero%20Trust%20Access%20Split%20tunneling.png)

### VPC DNS Resolver
![DNS Resolver](./Zero%20Trust%20Access%20-%20VPC%20DNS%20Resolver.png)

## Additional Resources
1. #### [Roadmap to Zero Trust Netwrok](https://zerotrustroadmap.org/)
