---
title: "Configuring a secure Load Balancer with Let's Encrypt (EN)"
excerpt: "Discover how to configure a secure Public Cloud Load Balancer with Let's Encrypt"
updated: 2023-11-06
---

## Objective

Our Load Balancer as a Service (LBaaS) solution is based on [OpenStack Octavia](https://wiki.openstack.org/wiki/Octavia) and is fully integrated into the Public Cloud universe. 

After setting up your Load Balancer, you can configure it with a certificate in order to process HTTPS connections.

**This tutorial explains how to configure a secure Public Cloud Load Balancer with Let's Encrypt.**

## Requirements

- A [Public Cloud project](https://www.ovhcloud.com/es-es/public-cloud/) in your OVHcloud account
- [Preparing your environment for using the OpenStack API](/pages/public_cloud/compute/prepare_the_environment_for_using_the_openstack_api)
- [OpenStack Octavia client](https://docs.openstack.org/python-octaviaclient/latest/install/index.html) and [OpenStack Barbican](https://docs.openstack.org/python-barbicanclient/latest/install/index.html) set up
- A Load Balancer running in your project

If you are not yet familiar with creating a Load Balancer, please follow our guide on [Getting started with Load Balancer on Public Cloud](/pages/public_cloud/public_cloud_network_services/getting-started-01-create-lb-service) before you continue with this tutorial.

## Instructions

### Creating an instance for Let's Encrypt

You can create an instance in your project in the region where your Load Balancer is located. Read about the details in our [guide](/pages/public_cloud/compute/public-cloud-first-steps) if necessary. The d2-2 instance type will be sufficient for this operation. We recommend that you use Ubuntu as your operating system. 

Once you have created your instance, you can refer to the [Let's Encrypt documentation](https://certbot.eff.org/instructions?ws=other&os=ubuntufocal) to install *Certbot*.

### Attaching a Floating IP address to a Load Balancer

This is how to attach a Floating IP address to a Load Balancer:

```bash
openstack floating ip create Ext-Net
openstack floating ip set --port <my_load_balancer_vip_port_id> <floating_ip>
```

> [!primary]
>
> To retrieve the VIP port ID of your Load Balancer, use `openstack loadbalancer show my_load_balancer`.

Please note that you must add an A record in the DNS Zone of your domain name that points to the Floating IP. 

If you are using DNS servers managed by OVHcloud, please consult this [guide](/pages/web_cloud/domains/dns_zone_edit).

### Configuring your Load Balancer

In this step, create a first Listener which will listen on port 80 (HTTP) and will take care of redirecting HTTP to HTTPS. It will also contain a redirection rule to the Let's Encrypt instance for certificate verification.

```bash
openstack loadbalancer listener create --protocol-port 80 --protocol HTTP --name http-listener my_load_balancer

openstack loadbalancer pool create --name pool-letsencrypt --lb-algorithm ROUND_ROBIN --listener http-listener --protocol HTTP

openstack loadbalancer member create --subnet-id my_subnet --address <private_ip_letsencrypt_instance>  --protocol-port 80 pool-letsencrypt
```

We will now create the redirection rules:

```bash
openstack loadbalancer l7policy create --action REDIRECT_TO_POOL --redirect-pool pool-letsencrypt --name letsencrypt-redirection http-listener --position 1
openstack loadbalancer l7rule create --compare-type STARTS_WITH --type PATH --value /.well-known/acme-challenge letsencrypt-redirection
```

### Generating a certificate

From the Let's Encrypt instance, you can now launch the certificate generation.

```bash
ubuntu@letsencrypt:~$ sudo certbot certonly -d <domain.tld> --standalone -m <email> --agree-tos
```

Once the process is completed, your certificate will be located in `/etc/letsencrypt/live/domain.tld`. You will then need to merge the certificate with its certificate private key:

```bash
ubuntu@letsencrypt:~$ sudo cat /etc/letsencrypt/live/domain.tld/fullchain.pem /etc/letsencrypt/live/domain.tld/privkey.pem | sudo tee /etc/ssl/domain.tld.pem
```

Now that you have your certificate, you can add a Secure Listener and associate a pool and its members with it :

```bash
ubuntu@letsencrypt:~$ sudo openssl pkcs12 -export -inkey /etc/ssl/domain.tld.pem -in /etc/ssl/domain.tld.pem -out /etc/ssl/domain.tld.p12
```

You have to download this file directly to your local device in order to send it to OpenStack Barbican ("Secret as a Service").

```bash
openstack secret store --name='LetsEncrypt-cert-domain.tld' -t 'application/octet-stream' -e 'base64' --payload="$(base64 < domain.tld.p12)"
```

### Configuring the secure Listener on the Load Balancer

With your certificate now created, you can add a secure Listener:

```bash
openstack loadbalancer listener create --protocol-port 443 --protocol TERMINATED_HTTPS --name https-listener --default-tls-container=$(openstack secret list | awk '/ LetsEncrypt-cert-domain.tld / {print $2}') my_load_balancer

openstack loadbalancer pool create --name pool-tls --lb-algorithm ROUND_ROBIN --listener https-listener --protocol HTTP

openstack loadbalancer member create --subnet-id my_subnet --address <private_ip_instance_1> --protocol-port 80 pool-tls

openstack loadbalancer member create --subnet-id my_subnet --address <private_ip_instance_2> --protocol-port 80 pool-tls
```

You can now securely access your Load Balancer with Let's Encrypt. Be careful, you will need to renew the certificate every 3 months.

## Go further

[Official documentation of OpenStack Octavia](https://docs.openstack.org/octavia/latest/)

[Cookbook OpenStack Octavia](https://docs.openstack.org/octavia/latest/user/guides/basic-cookbook.html)

[Getting started with Load Balancer on Public Cloud](/pages/public_cloud/public_cloud_network_services/getting-started-01-create-lb-service)

If you need training or technical assistance to implement our solutions, contact your sales representative or click on [this link](https://www.ovhcloud.com/es-es/professional-services/) to get a quote and ask our Professional Services experts for assisting you on your specific use case of your project.

Join our community of users on <https://community.ovh.com/en/>.