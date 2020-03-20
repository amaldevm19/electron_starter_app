# electron_starter_app
  <p> How to setup an Electron dev environment and developing a basic electron app in windows OS.</p>
  <b>Pre-requesties</b>
  <p>Node js</p>
  <p>NPM Package manager</p>
  <p>VS CODE</p>
  <p>Open powershell in your workfoder</p>
  <pre>node -v</pre>
  <pre>npm -v</pre>
  <p>An Electron App structured</p>
  <pre>
  your-app/
      -package.json
      -main.js
      -index.html
  </pre>
  <p>Run </p>
<pre>npm init</pre>
<p>now your package.json will looks like</p>
<pre>
    {
        "name": "electron_starter_app",
        "version": "1.0.0",
        "description": "Starter App",
        "main": "main.js",
        "dependencies": {
          "electron": "^8.1.1"
        },
        "devDependencies": {},
        "scripts": {
          "test": "echo \"Error: no test specified\" && exit 1"
        },
        "author": "Amaldev",
        "license": "ISC"
      }
</pre>
<p>modify script tag</p>
<pre>
    "scripts": {
        "start": "electron ."
      }
</pre>
<p>Install Electron</p>
<pre>npm install --save-dev electron</pre>
<p>create main.js in root folder and add electron to main.js</p>
<pre>
    const { app, BrowserWindow } = require('electron')
</pre>
<p>Add a create window function</p>
<p>create new instance of BrowserWindow class in createwindow() </p>
<pre>
    function createWindow() {
        let win = new BrowserWindow({
            width:800,
            height:600,
            webPreferences:{
                nodeIntegration:true
            }
        });
        win.loadFile("index.html");
    }
</pre>
<p>Now call createWindow function when app is ready</p>
<pre>
    app.whenReady().then(createWindow)
</pre>
<p>Add an Index.html page with a welcome message</p>

<p>Run start script</p>
<pre>
    npm start
</pre>
<p>To open dev tools</p>
<pre>
    win.webContents.openDevTools()
</pre>

<p>On macOS it is common for applications and their menu bar to stay active until the user quits explicitly with Cmd + Q </p>

<pre>
    app.on('window-all-closed', () => {
        if (process.platform !== 'darwin') {
          app.quit()
        }
    })
</pre>

<p>On macOS it's common to re-create a window in the app when the dock icon is clicked and there are no other windows open.</p>

<pre>
    app.on('activate', () => {
        if (BrowserWindow.getAllWindows().length === 0) {
        createWindow()
        }
    })
</pre>

<p>Add some html to index.html</p>

<pre>
    <p> We are using node <script>document.write(process.versions.node)</script>,
        Chrome <script>document.write(process.versions.chrome)</script>,
        and Electron <script>document.write(process.versions.electron)</script>.</p>
</pre>

<p>Add some inline style to HTML</p>
<pre>
    h1, p{
        color: #fff;
    }
   style="background-color: #555;"
</pre>

<p>npm start to run your app</p>
-----------------------------------------------------------------------------
<p> Distribute an elctron app using electron-packager</p>

<p>Install electron-packager cli globally</p>
<pre>
    npm install electron-packager -g
</pre>
<p>Package your app</p>
<p>run electron-packager from your app folder </p>
<pre>
    electron-packager .
</pre>
------------------------------------------------------------------------
<p>Install electron-wininstaller</p>
<pre>
    npm install electron-winstaller
</pre>

<p>create a folder called myapp-source-built-installers in your root folder</p>
<p>create bundle.js</p>
<pre>
    // C:\Users\sdkca\Desktop\electron-workspace\build.js
    var electronInstaller = require('electron-winstaller');
    
    // In this case, we can use relative paths
    var settings = {
        // Specify the folder where the built app is located
        appDirectory: './electron_starter_app-win32-x64',
        // Specify the existing folder where 
        outputDirectory: './myapp-source-built-installers',
        // The name of the Author of the app (the name of your company)
        authors: 'Amaldev',
        // The name of the executable of your built
        exe: './electron_starter_app.exe'
    };
    
    resultPromise = electronInstaller.createWindowsInstaller(settings);
     
    resultPromise.then(() => {
        console.log("The installers of your application were succesfully created !");
    }, (e) => {
        console.log(`Well, sometimes you are not so lucky: ${e.message}`)
    });
</pre>
<p>run bundle.js</p>
<pre>
    node bundle.js
</pre>

<p>
    Finally, open the installers folder (in this case located in your work space) and you will find there 3 installers (msi installer, executable installer and a nuGET package):
</p>
