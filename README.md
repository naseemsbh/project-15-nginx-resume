# Project 15 – Nginx Custom Domain Resume Website

## 1. Project Overview

This project demonstrates how to host a personal resume website using Nginx inside Ubuntu on WSL2 and access it through a custom local domain from a Windows browser.

Website addresses:

- http://www.naseem.local
- http://naseem.local

This is a local development project. The domain is not publicly registered, and the website is not publicly accessible.

## 2. Technologies Used

- Ubuntu 26.04.1 LTS on WSL2
- Nginx 1.28.3
- HTML5 and CSS3
- Windows hosts file
- Linux command-line tools

## 3. Project Structure

```text
project-15-nginx-resume/
├── website/
│   ├── index.html
│   └── style.css
├── nginx/
│   └── naseem-resume.conf
├── screenshots/
│   ├── resume-website.png
│   ├── resume-website-domain.png
│   ├── nginx-test.txt
│   └── http-response.txt
└── README.md
```

## 4. Nginx Configuration

The Nginx server block uses:

- HTTP port: 80
- Server names: www.naseem.local and naseem.local
- Document root: /var/www/naseem-resume
- Default page: index.html

Configuration file:

`nginx/naseem-resume.conf`

Active configuration:

`/etc/nginx/sites-available/naseem-resume`

Enabled configuration:

`/etc/nginx/sites-enabled/naseem-resume`

## 5. Windows Hosts File Configuration

The following entries were added to the Windows hosts file:

```text
127.0.0.1    www.naseem.local
127.0.0.1    naseem.local
```

Hosts file location:

`C:\Windows\System32\drivers\etc\hosts`

The DNS cache was flushed using this command in Windows PowerShell:

```powershell
ipconfig /flushdns
```

## 6. How the Request Works

1. The user enters www.naseem.local in Chrome.
2. Windows checks the hosts file and resolves the domain to 127.0.0.1.
3. WSL localhost forwarding delivers the request to Nginx inside Ubuntu.
4. Nginx listens on port 80 and selects the matching server block using the requested hostname.
5. Nginx serves index.html and its associated CSS file.

## 7. Website Deployment

The deployed website files are stored at:

`/var/www/naseem-resume`

The portfolio copy is stored separately in this repository under `website/`.

The Nginx server block points to the deployed directory, not directly to the portfolio folder.

## 8. Verification and Testing

### Nginx configuration test

Command:

```bash
sudo nginx -t
```

Verified result:

```text
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

### HTTP response test

Command:

```bash
curl -I http://www.naseem.local
```

Verified response:

```text
HTTP/1.1 200 OK
Server: nginx/1.28.3 (Ubuntu)
Content-Type: text/html
```

### Browser test

The website was successfully opened in Chrome using:

`http://www.naseem.local`

## 9. Screenshots and Test Evidence

| File | Evidence |
|---|---|
| resume-website.png | Full resume website |
| resume-website-domain.png | Website accessed through the custom domain |
| nginx-test.txt | Nginx configuration test output |
| http-response.txt | HTTP response showing 200 OK |

## 10. Learning Outcomes

Through this project, I practised:

- Installing and configuring Nginx.
- Hosting a static website on Linux.
- Creating and enabling Nginx server blocks.
- Configuring website document roots.
- Mapping custom domains using the Windows hosts file.
- Understanding WSL2 localhost forwarding.
- Testing Nginx configuration.
- Verifying HTTP responses using curl.
- Troubleshooting local website access.

## 11. Limitations

- The .local domain is used only for this local setup.
- The website is not deployed to a public domain.
- Public DNS is not configured.
- HTTPS is not configured.
