# GitHub Wiki Source

This folder contains ready-to-publish pages for the GitHub Wiki.

## Pages Included

- Home.md
- Quick-Start.md
- CLI-Reference.md
- GUI-Guide.md
- Browser-Extension.md
- Security-Model.md
- Troubleshooting.md
- Development-Guide.md
- _Sidebar.md

## Publish To GitHub Wiki

Replace `<owner>` and `<repo>` below with your repository values.

```bash
git clone https://github.com/<owner>/<repo>.wiki.git
cd <repo>.wiki
cp -r ../<repo>/gh-pages/wiki/* .
git add .
git commit -m "Add initial Soteria wiki"
git push
```

On Windows PowerShell:

```powershell
git clone https://github.com/<owner>/<repo>.wiki.git
Set-Location <repo>.wiki
Copy-Item -Path ..\<repo>\gh-pages\wiki\* -Destination . -Recurse -Force
git add .
git commit -m "Add initial Soteria wiki"
git push
```

After pushing, open:

`https://github.com/<owner>/<repo>/wiki`
