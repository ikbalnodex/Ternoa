<p style="font-size:14px" align="right">
<a href="https://t.me/Bal33671" target="_blank">Reach me on telegram <img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/></a>
<a href="https://twitter.com/Bal3367" target="_blank">Visit my twitter <img src="https://user-images.githubusercontent.com/110718880/204088136-3e807cf8-1fc4-4a7d-a833-d58180e36413.png" width="30"/></a>
</p>

![image](https://user-images.githubusercontent.com/119092888/204531524-554634bb-6a7c-46fd-b470-f4bac420cabb.png)

# Ternoa

Dokumen Official :
> [Doc Offical](https://docs.ternoa.network/for-node-operators/system-requirements")

# Hardware Recommendations

- For the minimum specification, we recommend:

2 core machine (with a newish server CPU)

4 GB DDR4/DDR5 ECC RAM

80GB SSD storage.

- For optimal server we recommend:

4 core machine (with a newish server CPU)

4GB DDR4/DDR5 ECC RAM

160GB SSD storage.

# Install Basic
```console
sudo apt update
sudoapt upgrade
sudo apt install screen
```

# Install Ternoa Node

```console
wget https://ternoa.s3.fr-par.scw.cloud/chain/alphanet/Release%201.0.0-rc1/ternoa -O /usr/bin/ternoa
```

# Beri Izin Ternoa Client Binary
```console
chmod u+x /usr/bin/ternoa
```

# Cek Versi Node Kalian
```console
/usr/bin/ternoa --version
```
- output seharusnya ternoa 1.0.0

# Buat Folder
 ```console
 mkdir -p /opt/node-data
 ```
 
 # Jalankan Node
 
 - Jalakan Di Screen
 ```console
 screen -R ternoa
 ```
 ```console
 /usr/bin/ternoa --name < Nama Kalian > --chain alphanet --base-path /opt/node-data --validator --state-cache-size 0 --execution wasm
 ```
 
 - Lalu Klik CTRL + A D
 
 - Silahkan Cek Explorer
 
 [EXplorer](https://telemetry.polkadot.io/#list/0x18bcdb75a0bba577b084878db2dc2546eb21504eaad4b564bb7d47f9d02b6ace)
 
 - Jika Berhasul Maka Node Kalian Akan Muncul
 
 ![image](https://user-images.githubusercontent.com/119092888/204540401-5daeacdc-827b-4d78-988e-87bdc06c4a57.png)

# Sambungkan Dengan Server 
```console
ssh -o "ServerAliveInterval 60" root@< Ip VPS Kalian >
```
- Silahkan pilih YES
- Lalu masukan password vps kalian

# Membuat Session keys
```console
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933 &> session_keys.txt
```
- Untuk memastikan bahwa berjalan
```console
cat session_keys.txt
 ```

- Maka akan ada file baru yang bernama `session_keys.txt` di folder vps kalian

# Edit File
```console
nano /etc/systemd/system/ternoa.service
```
- Silahkan isi dengan text dibawah
```console
[Unit]
Description=Ternoa Validator Node By Ternoa.com
 
[Service]
ExecStart=/usr/bin/ternoa --name MarkoPoloNode --chain alphanet --base-path /opt/node-data --validator --state-cache-size 0 --execution wasm
WorkingDirectory=/usr/bin
KillSignal=SIGINT
User=root
Restart=on-failure
LimitNOFILE=10240
SyslogIdentifier=ternoa
 
[Install]
WantedBy=multi-user.target
```
- CRTL + X lalu Y dan ENTER

# Cek Apakah Berjalan
```console
systemctl status ternoa.service
```
![image](https://user-images.githubusercontent.com/119092888/204547719-07c243f9-d6f4-47af-9479-ba6d00f6e506.png)
 
