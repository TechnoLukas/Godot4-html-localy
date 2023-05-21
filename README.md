

# ❓How to run godot4 html project locally?

- got to https://httpd.apache.org/download.cgi
  
  <img src="https://i.imgur.com/Y0hDeRv.png"  width="100%" height="10%">
  <img src="https://i.imgur.com/d1KibUO.png"  width="60%" height="30%">
  
  select site to download, in my case it was https://www.apachelounge.com/download/
  
  <img src="https://i.imgur.com/AOrZ7k5.png"  width="100%" height="10%">

- Unzip and put `Apache24` to your stable folder.

- Now we need to modify config file. Got to your new Apache24 folder and go to conf/httpd.conf
  
  - after this `Define SRVROOT` you should paste the path to your new Apache24 folder.
      `Define SRVROOT "C:/Users/xxxx/Desktop/Apache24"`
  
  - setup your favorite port here http server (you will connect to it later) `Listen 8080`, in my case  it is 8080
  
  - enable loading `headers-module` by uncommenting 
      `LoadModule headers_module modules/mod_headers.so`
  
  - uncomment and modify `#ServerName www.example.com:80`  to `ServerName 127.0.0.1:8080` with chosen port. You should specify 127.0.0.1 as localhost. 
  
  - Inside `<Directory "${SRVROOT}/htdocs">` add `Header add Access-Control-Allow-Origin "localhost"` (Very important 🙂)
  
  - At any place (for instance at the end) add this block 
    
    ```
    <IfModule mod_headers.c>
    Header set Cross-Origin-Embedder-Policy "require-corp"
    Header set Cross-Origin-Opener-Policy "same-origin"
    </IfModule>
    ```
    
    - See below what you should get as a result.

Updating config file is done.

- Now we have to install and start the server

- [!] All the commands should be executed with Admin Rights

- first, run cmd as admin and go to your `Apache24/bin` folder, and run `httpd.exe -k install` and you will see windows popup window, you should allow the acces. Don't close cmd window.
  
  <img src="https://i.imgur.com/lh0kHc4.png"  width="60%" height="30%">

- Now we need to start the server by executing in cmd `httpd.exe -k start`

- We need to check if all this works, click this link http://localhost:8080 or enter `localhost:8080` in your browser. You should see this:
  
  <img src="https://i.imgur.com/RsrlkqH.png"  width="60%" height="30%">

- We have created the server now, we need to put our game there. Go to your `Apache/htdocs` folder, then create folder `game1` (name of your game, up to you) and put our web files, like on the image below. Main .html file should be named index.html **!Very important!**
  ![[Pasted image 20230521103103.png]]

- Now if we will go to http://localhost:8080/game1 (after "/" in should be name of the folder that we have created in previous step) your game will load :)

- You can also add second game following the same steps. Create folder, put web file (very important index.html)

- Now we want to store links to our main server page. Go to your `Apache/htdocs` and create `index.html`, paste code below and to add more links you need to just replace xxxx on your link.
  
  ```
  <p><a href="http://localhost:8080/game1">http://localhost:8080/game1</a></p>
  
  <p><a href="http://localhost:8080/game2">http://localhost:8080/game2</a></p>
  
  <p><a href="xxxx">xxxx</a></p>
  ```

---

Also useful commands:

- http.exe -V
- http.exe -k restart
- http.exe -k stop
- http.exe -k start
- http.exe -k install
- http.exe -k deinstall
