

## [get start](https://www.electronjs.org/zh/docs/latest/tutorial/quick-start/)

ELECTRON_MIRROR=https://npmmirror.com/mirrors/electron/ npm install --registry=https://registry.npmmirror.com -g electron

main.js
```js
const { app, BrowserWindow } = require('electron');

const createWindow = () => {
  const win = new BrowserWindow({
    width: 800,
    height: 600
  })

  win.loadFile('index.html')
}

app.whenReady().then(() => {
  createWindow()

  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) createWindow()
  })
})

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit()
})

```

html
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using io.js <script>document.write(process.version)</script>
    and Electron <script>document.write(process.versions['electron'])</script>.
  </body>
</html>
```

```sh
# start 
npx electron .

# build
# 将 Electron Forge 添加到您应用的开发依赖中，并使用其"import"命令设置 Forge 的脚手架：
npm install --save-dev @electron-forge/cli
npx electron-forge import

npm run make

```