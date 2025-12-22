## cURL (Client URL)

| Command | Description |
|--------|------------|
| `curl -O` | Download a page or file and save output to disk |
| `curl -u user:pass` | Authenticate using username and password |
| `curl -h` | Display available cURL options |
| `curl -k` | Skip SSL certificate verification |
| `curl -v` | Show full HTTP request and response |
| `curl -vvv` | Extremely verbose HTTP output |
| `curl -I` | Check HTTP headers information |

## cURL Examples

| Command | Description |
|--------|------------|
| `curl -X POST -d '{"search":"flag"}' -b 'PHPSESSID=<cookie>' -H 'Content-Type: application/json' http://target:port/query.php` | POST request with JSON body and session cookie |
| `curl -u username:password http://target:port/query.php?name=flag` | GET request using basic authentication |

## CRUD API

| Operation | HTTP Method |
|----------|-------------|
| Create | `POST` |
| Read | `GET` |
| Update | `PUT` |
| Delete | `DELETE` |

## CRUD API Examples

| Command | Description |
|--------|------------|
| `curl -X PUT http://target:port/api.php/city/Boston -d '{"city_name":"flag"}' -H 'Content-Type: application/json'` | Update resource |
| `curl -X DELETE http://target:port/api.php/city/anycity` | Delete resource |
| `curl -X GET http://target:port/api.php/city/flag` | Read resource |

## NSLOOKUP

| Command | Description |
|--------|------------|
| `nslookup example.com` | Resolve domain to IP |
| `nslookup -type=A example.com` | Retrieve A record |
| `nslookup -type=NS example.com` | Retrieve NS records |

## DIG

| Command | Description |
|--------|------------|
| `dig example.com` | Query DNS records |
| `dig A example.com` | Retrieve A record |
| `dig AAAA example.com` | Retrieve IPv6 record |
| `dig MX example.com` | Retrieve mail servers |
| `dig AXFR @targetIP example.com` | Attempt DNS zone transfer |

## DNSEnum

| Command | Description |
|--------|------------|
| `dnsenum --enum inlanefreight.com -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt` | Enumerate subdomains |

## GoBuster

| Command | Description |
|--------|------------|
| `gobuster vhost -u http://targetIP:port -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 500 --append-domain` | Virtual host brute-force |
| `gobuster dir -u http://target/admin -w wordlist.txt` | Enumerate deeper directories 
| `gobuster vhost -u http://sub vhost:port -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 500 --append-domain` | Brute-force for sub-vhosts too! |

## Certificate Transparency Logs

| Command | Description |
|--------|------------|
| `curl -s "https://crt.sh/?q=facebook.com&output=json" \| jq -r '.[] \| select(.name_value \| contains(\"dev\")) \| .name_value' \| sort -u` | Enumerate dev subdomains from CT logs |

## Robots.txt 

| Command | Description |
|--------|------------|
| `curl http://target/robots.txt`| Retrieve robots.txt file to try and find any hidden directories, panels, flags |

## ReconSpider

| Command | Description |
|--------|------------|
| `pip3 install scrapy` | install Scrapy |
| `wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip` | Download ReconSpider |
| `unzip ReconSpider.zip` | Unzip the file |
| `python3 reconspider.py http://target` | Crawl website to enumerate URLs, endpoints, and parameters. Downloaded on files |

## Skills Assessment
| Command | Description |
|--------|------------|
| `sudo nano /etc/hosts` | Add a line mapping target IP to vhost name NO PORT |
| `whois target` | Used for recon good for organization, country, registrar info |
| `curl web1337.inlanefreight.htb:53710/robots.txt` | Shows hidden paths |
| `curl web1337.inlanefreight.htb:53710/admin_h1dd3n/` | Disallowed path INCLUDE the / | `gobuster vhost -u http://web1337.inlanefreight.htb:53710 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 500 --append-domain | Brute force for the sub-vhost |
| `python3 ReconSpider.py http://dev.web1337.inlanefreight.htb:53710` | Crawl to find Emails/Links |




