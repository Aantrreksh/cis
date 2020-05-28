---

copyright:
  years: 2018, 2020
lastupdated: "2020-05-12"

keywords: Caching, IBM Cloud Internet Services, Web Application Firewall

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}


# About {{site.data.keyword.cis_full_notm}}
{:#about-ibm-cloud-internet-services-cis}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}), powered by Cloudflare, provides a fast, highly performant, reliable, and secure internet service for customers running their business on {{site.data.keyword.cloud_notm}}.
{:shortdesc}

IBM {{site.data.keyword.cis_short_notm}} gets you going quickly by establishing defaults for you, which you can change easily using the API or UI. 

## Web Application Firewall (WAF)
{:#about-waf}

IBM {{site.data.keyword.cis_short_notm}} provides Web Application Firewall (WAF) capability, which examines web traffic to look for suspicious activity. It can filter out illegitimate traffic automatically — based on rule sets — to look at GET and POST-based web requests. You can use various rule sets to determine which traffic to block, challenge, or let pass. Our WAF can block comment spam, cross-site scripting attacks, and SQL injections.

You can enable or disable the WAF at your discretion. We recommend that you always leave it on.

## Protection from DDoS attacks
{:#ddos-protection}

IBM {{site.data.keyword.cis_short_notm}} supplies DDoS protection that stands between your website and attackers, regardless of the attack's size or duration.

## Load Balancing
{:#about-load-balancing}

IBM {{site.data.keyword.cis_short_notm}} Load Balancing operates at the Authoritative DNS level. It incorporates advanced health checks to monitor the health of the origins, and dynamically adjusts DNS responses. Additionally, you can configure Geo policies for Global Load Balancing (GLB).

### Health checks
{:#about-health-checks}

Load Balancing Health Checks are performed on specific URLs through periodic HTTP or HTTPS requests, and they are configured with customizable intervals, timeouts, and status codes. When an origin server is marked as unhealthy, visitors are routed away from failures, using our fast failover routes.

### Geo Policies and Global Load Balancing (GLB)
{: #geo-policies-and-glb}

Geo policies give you control of the origin servers to which a given client is directed, based on the geographic location of that client. For instance, you could configure your Geo policies so that visitors in Europe are sent to the nearest European origin for your website or application, U.S. visitors are sent to a North American origin, and so forth.

## Caching
{:#about-caching}

Caching is a way to store your static web content closest to your site visitors, thus significantly enhancing the performance of the website. Our globally distributed delivery environment enables web content owners to provide a seamless experience, worldwide.  

## Encryption with TLS
{:#encryption-with-tls}

Encrypt communication to and from your website using Transport Layer Security (TLS). It may take up to 24 hours after the site becomes active for your new certificates to be issued.

You can find more details about TLS in [TLS options](/docs/cis?topic=cis-cis-tls-options).
