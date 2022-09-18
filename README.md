# Lehighur Website

This site is based on [Hugo](https://gohugo.io/)

## Installation: 

- [Hugo](https://gohugo.io/getting-started/installing/)
  - Install on Windows: [link](https://gohugo.io/getting-started/installing/#windows)
- [Git bash](https://git-scm.com/) (Recommended on Windows)

- `git clone --recurse-submodules https://github.com/Lehigh-Underwater-Robotics/Lehighur-Website.git`

## Get Started

To make life simple, you can preview the website locally using `hugo` before you commit and push them online. In the `Lehihgur-Website` folder, run: 

```hugo server -D
hugo server -D
```

The output is like this: 

```$ hugo server -D
Start building sites …
hugo v0.96.0-2fd4a7d3d6845e75f8b8ae3a2a7bd91438967bbb windows/amd64 BuildDate=2022-03-26T09:15:58Z VendorInfo=gohugoio

                   | EN
-------------------+-----
  Pages            | 34
  Paginator pages  |  0
  Non-page files   |  0
  Static files     | 64
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Built in 266 ms
Watching for changes in C:\Users\weiha\Desktop\temp\Lehighur-Website\{archetypes,content,data,layouts,static,themes}
Watching for config changes in C:\Users\weiha\Desktop\temp\Lehighur-Website\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Open a browse and go to `http://localhost:1313/`. Note that at this point, it is only local preview. If you are satisfied with the change, git add, commit, and push the changes to github. We used [vercel](https://vercel.com/) to deploy the website, this action is done automatically as soon as you push the changes to github. 



## What You Can Do

### Add sections and sub-sections

The `config.toml` is the site config file. To add more sections, follow this pattern and grammar. 

![s](https://raw.githubusercontent.com/baboonSTW/Blog-img/main/202209181429708.png)

After you create the new section, create the folder under `content/` with the same name as `<URL>`, or the website will not know where to redirect and you will get `404 page not found` error. 

### 

In `content/<section>/`, there are two files normally. `_index.md` is the meta description of the section. You can change the title of this section. `<other>.md` contains the content of this section. 

