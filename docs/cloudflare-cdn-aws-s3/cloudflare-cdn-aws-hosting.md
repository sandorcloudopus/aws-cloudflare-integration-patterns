## Static Hosting in AWS and CDN in Cloudflare
Integrating AWS S3 Website Endpoint and Cloudflare Anycast network provides a great user and developer experience and also cost effective.

Proxying the traffic through Cloudflare network adds endless options how to furhter enhance the user experience and protect our website.

## YouTube video
[Cloudflare + AWS | Host Static Websites](https://youtu.be/Q5Q5JOXu2-M)

## High Level Architecture Overview
![Clouflare + AWS | Host Static Websites](./S3%20Hosting%20with%20Cloudflare%202(1).png)

### Components
1. S3 Bucket
    1. Bucketname should match the Cloudflare "hostname"
    1. Website Hosting Capability should be enabled
        1. Also set the `index` document
    1. Make the Bucket Public!
    1. Create a bucket policy [link below](#Bucket-Policy)
1. Cloudflare Website
    1. Create Website for your domain/hostname
    1. Create the appropriate DNS Record
        1. CNAME Type - name is the desired hostname (example.com, www.example.com), value is the "S3 Bucket Website Endpoint"
    1. Enable Proxy (very important)
    1. Optionally configure caching
    1. Optionally configure DDoS
    1. Optionally configure WAF

### Resources
#### Bucket Policy
```json
 {
  "Sid": "AllowPublicAccessFromCloudflare",
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": ["arn:aws:s3:::<hostname/bucketname>", "arn:aws:s3:::<hostname/bucketname>/*"],
  "Condition": {
    "IpAddress": {
      "aws:SourceIp": [
          "103.21.244.0/22",
          "103.22.200.0/22",
          "103.31.4.0/22",
          "104.16.0.0/13",
          "104.24.0.0/14",
          "108.162.192.0/18",
          "131.0.72.0/22",
          "141.101.64.0/18",
          "162.158.0.0/15",
          "172.64.0.0/13",
          "173.245.48.0/20",
          "188.114.96.0/20",
          "190.93.240.0/20",
          "197.234.240.0/22",
          "198.41.128.0/17"
      ]
    }
  }
}
```

#### Cloudflare IPs
[Cloudflare IP Addresses](https://www.cloudflare.com/ips/)
