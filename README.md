# My Personal Blog: Mars Studio

## ENV setup

### install node

#### dependencies
```
# install node
brew update && brew install node

# setup mainland registry to speed up
npm config set registry http://mirrors.cloud.tencent.com/npm/

# install packages in this project
npm install

# install hexo-cli globally
npm install hexo-cli
```

### create a new blog
```
# use hexo command to create a new blank post file
hexo new

# OR, create the post file manually
```

### preview
```
# use localhost address to preview the site by command
hexo server
```

### deploy
```
hexo generate deploy
```
