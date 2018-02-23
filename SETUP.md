# Create new project from SDK


* Clone origin repo
```
git clone https://github.com/grandlyon/glsdk-project.git PROJECT
cd PROJECT
# Init submodule
npm run init
```

* Change repositories URL

Main repository
```
git remote set-url origin NEW_URL_PROJECT
```

SubMobule repository via editing file ``` .gitmodules ```
```
[submodule "glsdk-server"]
        path = server
        url = NEW_URL_PROJECT_SERVER
        branch = master
[submodule "glsdk-client"]
        path = webapp
        url = NEW_URL_PROJECT_CLIENT
        branch = master
[submodule "glsdk-proxy"]
        path = proxy
        url = NEW_URL_PROJECT_PROXY
        branch = master
```

* change docker image name generated on each ```.travis.yml```
```
export REPO=grandlyon/PROJECT
```