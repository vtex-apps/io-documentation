# Updating VTEX IO's CLI

According to your operating system, run the following on your command line to update VTEX IO’s CLI or how to handle a deprecated version of it on your machine.

<details>
  <summary><span class="fa fa-apple">&nbsp;</span>MacOS</summary>
  <br>
  
- Brew
  - Update
  ```sh
   brew upgrade vtex
  ```
  
  - Deprecated
  ```sh
   brew unlink vtex
   brew install vtex/vtex
  ```

<br>
</details>

<details>
  <summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

  - Standalone
  
    - Update
     ```sh
      vtex autoupdate
      ```
  
    - Deprecated
     ```sh
     vtex autoupdate
     ```
   > The standalone update is a tarball with a binary that contains its own node.js binary.
<br>
</details>

<details>
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

- Standalone.exe

  ```sh
  vtex autoupdate
  ```

- Chocolatey

  ```sh
  choco uninstall vtex
  choco install vtex
  ```


<br>
</details>

## Updating VTEX IO's CLI via NPM
 
 If you have [installed VTEX IO's CLI via NPM](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-install), to update or handle a deprecated version of it on your machine run the following in your command line:
 
 ```sh
  yarn global add vtex
 ```
