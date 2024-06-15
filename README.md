# Free Windows Server With RDP For Lifetime
This repository is all about getting free windows server with rdp using github jobs & ngrok tunnel. In this github repositoyr i added the step by step guide to have a free windows vsp server thorugh github and accessing it via remote desktop connection.

[![MasterHead](https://github.com/MSRTanim/all-REDME/blob/b0ae2efd0f8da673eab449ab29c88fc58f810a39/coding.gif)](http://www.msrtanim.xyz)

## Watch Full Video Guide on My YouTube Channel

[![alt text](https://i9.ytimg.com/vi_webp/i28V6YQ0fFk/maxresdefault.webp?v=666d2bb2&sqp=CODbtLMG&rs=AOn4CLB48EZckioPkuGKEuyZhJbDFpZaFw)](https://youtu.be/LrjrFWa64Mw)

## Steps To Create Windows Server
* Sign Up a GitHub Account : https://github.com/
* Create a Private Repository, Go to repository settings > Secrets and variables > Actions > New Repository Secrets
* Sign Up a Ngrok Account : https://ngrok.com/
* Copy the auth key from ngrok and add to github repository secrets
* Setup New Workflow Manually the Put the following code in main.yml and commit changes 
```
name: CI

on: [push, workflow_dispatch]

jobs:
  build:

    runs-on: windows-latest

    steps:
    - name: Download
      run: Invoke-WebRequest https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-windows-amd64.zip -OutFile ngrok.zip
    - name: Extract
      run: Expand-Archive ngrok.zip
    - name: Auth
      run: .\ngrok\ngrok.exe authtoken $Env:NGROK_AUTH_TOKEN
      env:
        NGROK_AUTH_TOKEN: ${{ secrets.NGROK_AUTH_TOKEN }}
    - name: Enable TS
      run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server'-name "fDenyTSConnections" -Value 0
    - run: Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
    - run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" -Value 1
    - run: Set-LocalUser -Name "runneradmin" -Password (ConvertTo-SecureString -AsPlainText "P@ssw0rd!" -Force)
    - name: Create Tunnel
      run: .\ngrok\ngrok.exe tcp 3389

```
* Run The WorkFlow and take note of credentials (runneradmin:P@ssw0rd!)
### USER

```
runneradmin
```

### Password
```
P@ssw0rd!
```

* Get the ngrok endpoint url and use it as ip or address in Remote Desktop Connection with credentials

<h3 align="left">Connect with me:</h3>
<p align="left">
<a href="https://fb.com/msrtanim.py" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/facebook.svg" alt="msrtanim1" height="30" width="40" /></a>
<a href="https://instagram.com/msrtanim.py" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/instagram.svg" alt="msrtanim1" height="30" width="40" /></a>
<a href="https://www.youtube.com/@CodeWithTanim" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/youtube.svg" alt="msrtanim" height="30" width="40" /></a>
<a href="https://twitter.com/msrtanim_" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/twitter.svg" alt="msrtanim_" height="30" width="40" /></a>
<a href="https://codepen.io/msrtanim" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/codepen.svg" alt="msrtanim" height="30" width="40" /></a>
<a href="https://discord.gg/4Y4KUUADMC" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/discord.svg" alt="4292" height="30" width="40" /></a>
</p>

## Thanks!
