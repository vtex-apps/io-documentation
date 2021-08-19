## Uninstalling VTEX IO's CLI

According to your operating system, you can uninstall VTEX IO's CLI, and for that to happen, run the following on your command line.

>⚠️ *This will also remove all [plugins](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-plugins) from your system.*

<details>
  <summary><span class="fa fa-apple">&nbsp;</span>MacOS</summary>
  <br>
  
- Brew
  ```sh
   brew uninstall vtex
  ```
  
<br>
</details>

<details>
  <summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

  - Standalone

     ```sh
      curl -L https://vtex.io/vtexcli/uninstall | sh
     ```
 
   > The standalone is a tarball with a binary that contains its own node.js binary.
<br>
</details>

<details>
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

- Standalone.exe
  
  Follow the [Window's uninstall tutorial](https://support.microsoft.com/en-us/windows/uninstall-or-remove-apps-and-programs-in-windows-10-4b55f974-2cc6-2d2b-d092-5905080eaf98) to remove the VTEX IO's CLI from your programs list.

- Chocolatey

  ```sh
    choco uninstall vtex
  ```


<br>
</details>

### Uninstalling VTEX IO's CLI via NPM

If you have [installed VTEX IO's CLI via NPM](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-install), to uninstall it on your machine run the following in your command line:

```sh
  yarn global remove vtex
```
