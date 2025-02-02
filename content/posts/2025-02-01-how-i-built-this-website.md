---
title: How I built this website (v.1.0.1)
date: 2025-02-01
---
# Introduction

I’m building my minium-viable-product personal website A.K.A v.1.0.1 using **Hugo** from scratch, a fast and flexible static site generator. This project is mainly inspired by the these websites:
- [Derek Sivers’s site](https://sive.rs/) 
- [Jared White’s site](https://jaredwhite.com/)
- [Luke Smith’s site](https://lukesmith.xyz/)

What resonated with me from these websites is that they are all direct and distraction-free, emphasizing on the content which is big plus!


In the future (v2.0.1), I plan to incorporate elements of **Swiss Design** for a clean, modern aesthetic. And design a more seamless Obsidian to Hugo integration as per NetworkChuck [YT Video](https://www.youtube.com/watch?v=dnE7c0ELEH8).

After distilling and organizing my original notes, this walkthrough follows the [official Hugo documentation](https://gohugo.io/getting-started/quick-start/) and Cloud's Cannon, not sponsored, [begginer tutorial series](https://www.youtube.com/watch?v=SVvihs0WfhQ&list=PLrxYIq_0LFJfimciGTP5bQhYSEu5EdAuA). Let’s get started!

---

# 1. Prerequisites Section - Basic Software

Before using Hugo, ensure you have the following tools installed:

1. **Git**: Follow the [installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
2. **Go**: Verify the installation with `go version`. Try a simple [[# Hello World in Go]] program to test it:
3. **Dart Sass**: Install via Chocolatey. You need to have chocolatey installed, checkout my [[#Chocolatey Instalation Guide]]
```bash
choco install sass        
```  
4. Hugo: Install hugo via chocolatey. And if you have issues with not seing Hugo inside VS Code add the hugo.exe path to the environment variables. You can always check if its downloaded correctly running `hugo version` in the terminal
```bash
choco install hugo-extended
```


I think it is good practice to use a file versioning system, by that I mean git & gitbhub. You can follow my brief guide for begginers on [[#File versioning made easy]]

---

# 2. Building the Website

## 2.1 Initial Setup
1. Create a new repository on GitHub (e.g., `personal-website`).
2. Clone the repo locally:   
3. Create a new Hugo site with the CLI tool (you need to CD into the parent's dir):
```bash
hugo new site personal-website    
```
    
4. Start the Hugo server. As no theme is used, this is expected to be broken. Don't worry about it
```bash
hugo server    
```
  
## 2.2 Adding Content

### Build the home page
1. In a new file 'content/\_index.html', create the home page: 
```markdown
---
title: Home
---
Hello World! This is my first page. 🔝
```
2. In a new file 'layouts/\_default/list.html', create the needed layouts
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ .Page.Title}}</title>
</head>
<body>
    {{ .Content }}
</body>
</html>
```
3. Render the page
```bash
hugo serve
```
### Add an about section
1. In a new file 'content/about.html', create the about page: 
```markdown
---
title: About
---
Imagine this is a Lorem Ipsum
```
2. Refactor the layouts
- Now 'layouts/\_default/baseof.html' is:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ .Page.Title}}</title>
</head>
<body>
    {{ block "main" .}}
    {{ end }}
</body>
</html>
```
- Now 'layouts/\_default/list.html' is: 
```html
{{ define "main"}}
    {{ .Content}}
{{ end}}
```
- This has defined a 'main block' where we are passing the context '.'
- I understand that Hugo renders both the Home and About .md files with the baseof layou that then calls the main content frmom the list.html base layout. That is, it renders (? translates the .md to the index.html for each page, you can audit this in the public directory) the text below the YAML in each .md file 
3.  Write some awesome styles (Imagine this css is more impresive)
```scss
body {
    width: 400px;
    margin: 0 auto;
    font-family: sans-serif;
  }
```
4. Add the newly writen styles globaly to all the webpages (as all pages use first the base layout they'll inherit this unless otherwise specified?)
- Now 'layouts/\_default/baseof.html' is:
```html
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ .Page.Title}}</title>
    {{ $styles := resources.Get "sass/main.scss" | css.Sass | minify }}
    <link rel="stylesheet" href="{{ $styles.Permalink }}" media="screen">
</head>
<body>
    {{ block "main" .}}
    {{ end }}
</body>
</html>
```
- For more detail check Asset Management ( [Go Pipes](https://gohugo.io/hugo-pipes/introduction/) ). Hugo recomends:
```html
{{ $style := resources.Get "sass/main.scss" | css.Sass | resources.Minify | resources.Fingerprint }} <link rel="stylesheet" href="{{ $style.Permalink }}">
```
### Add a navbar and footer
This uses Hugo partials. The following part asumes you have already deployed with github pages
1. Modify the hugo.toml to include your page's url
- Modificar el base URL
```toml
baseURL = 'https://notyetfound404.github.io/personal-website/'
languageCode = 'en-us'
title = 'My New Hugo Site'
```

2. Create 'layouts/partials' and 'layouts/partials/nav.html'. Note that we are using absURL, this calls upon the baseURL modified in the previous step
```html
<nav>
    <ul>
        <li> <a href= {{ absURL "" }} > Home </a> </li>
        <li> <a href= {{ absURL "about/" }}> About </a> </li>
    </ul>
</nav>
```
3. Create a partial (named meta for convenience) to clean the sass import. Now 'layouts/partials/meta.html' is:
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>{{ .Page.Title}}</title>
{{ $styles := resources.Get "sass/main.scss" | css.Sass | resources.Minify }}
<link rel="stylesheet" href="{{ $styles.Permalink }}" media="screen">
```
4. Create a simple footer inside partials. Now 'layouts/partials/footer.html' is:
```html
{{ with .Params.hide_footer }}
 <!-- No footer here! -->
{{ else }}
 <footer>
    Copyright © {{ now.Year }} | {{ .Site.Params.name }} | All rights reserved
    <br>
    Powered by <a href="https://gohugo.io/">Hugo</a>
 </footer>
{{ end }}
```
The use of `.Params.hide_footer` calls upon the yaml defined `hide_footer` parameter
5. Include the meta, navbar and footer in the base layouts. Now 'layouts/\_default/baseof.html' is:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    {{ partial "meta.html" . }}
</head>
<body>
    {{ partial "nav.html"}}    
    {{ block "main" .}}
    {{ end }}
    {{ partial "footer.html" .}}
</body>
</html>
```
### Setup Hugo with blogging capabilities

1. **Create a new folder** `content/posts/` to store all blog posts.
2. **Create** `_index.md` inside the `posts/` folder.
3. **Set up a layout for blog posts:**
    - Create `layouts/posts/` (same name as step 1).
4. **Create `layouts/posts/list.html`**, the default layout used by `_index.md`:
```html
{{ define "main" }}
    <h1>My Posts</h1>
    <ul>
    {{ range .Page}}
        <li>
            <a href="{{ .Permalink }}"> {{ .Title }} </a> - {{ .Date.Format "January 2, 2006"}}
        </li>
    </ul>
{{ end }}
```

5. **Create `single.html`**, the layout for individual blog posts:

```html
{{ define "main" }}
    <h1>{{ .Params.Title }}</h1>
    <p>{{ .Date.Format "January 2, 2006" }}</p>
    {{ .Content }}
{{ end }}

```

6. **Create a new post!** Don't forget the front matter (YAML metadata) required in step 5.

```html
---
title: I Like to Roar
date: 2022-04-03
---

Up next,  

I'm going to include all the documentation on how I built this site:

```

7. **Clean the site before deployment:**

```bash
hugo --cleanDestinationDir --minify
```

## 2.3 Publish with Github Pages
Follow [along](https://gohugo.io/hosting-and-deployment/hosting-on-github/) 
1. Visit your GitHub repository. From the main menu choose **Settings** > **Pages**. > deploy from a branch changed to github actions
2. Create a file named `hugo.yaml` in a directory named `.github/workflows`. and add the sample config
3. Commit and push the new hugo config


# Other / Miscelaneous

## File versioning made easy
If you've never made a Github repo and don't care to learn about git commands, but want to have an organized codebase. You are likely a beginner, like me.

I will briefly explain how to setup a basic Github Repo and how to connect to it with VS code and make changes (A.K.A commits). I would still highly recomend you look into the [oficial docs](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories) (As the Arch Linux community would say, READ THE DOCS!!). Also, it is good practice being familiar with the [terminal](https://www.softwaretestinghelp.com/windows-cmd-commands/) and learning some basic [git](https://git-scm.com/docs/git) commands.

This is by no means and exhaustive guide. I'm assuming you already have installed Git, have created a Github Accoun (try to secure it with [2FA](https://www.microsoft.com/en-ie/security/business/security-101/what-is-two-factor-authentication-2fa#:~:text=Two%2Dfactor%20authentication%20(2FA),most%20vulnerable%20information%20and%20networks.)), and setup your Git's [mail and name](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup).


### A. Initial GitHub Setup
1. Create a new github repo
2. Copy the URL
![[20250131074948.png]]

### B. Local Machine
1. Open VS Code
2. CD into your Desktop
3. In VS code's start page you'll see the following
![[20250131080612.png]]
4. Clone Git Repo > Paste the URL
5. When you are done. Go to VS Code left tab, then source control, find the commit and add some text and add the changes to your repo!
6. By now, the changes you have made should be displayed in your Github's online repo. Check if they are by opening the repo on your preferred search engine.












---

## Hello World in Go
This is the explanation of  Programing Journey project [31.01.2025](https://github.com/NotYetFound404/programming-journey/tree/main/31.01.2025) code

```go
package main
import "fmt"
func main() {
    fmt.Println("Hello, World!")
}
```
- You can run it with:
```bash
go run hello_world.go
```
- Don't forget to comit the changes to the repo!
## Chocolatey Instalation Guide


Follows Chocolatey [install](https://community.chocolatey.org/courses/installation/installing?method=installing-chocolatey#powershell)
- In the powershell do the following
```PowerShell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

![[20250131091903.png]]