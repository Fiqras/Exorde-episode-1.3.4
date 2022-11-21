<h1 align="center">السلام عليكم </h1>


<p align="center">
  <img src="https://avatars.githubusercontent.com/u/5845056?v=4" width="200px" /></>
</p>
 <h2 </h2>

## Pemasangan menggunakan Docker

### Update apt

```
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    screen \
    git
```

### Tambahkan kunci GPG Docker resmi

```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```


### Setting repositori

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Unduh dan pasang Docker

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### Cek apakah Docker sudah terpasang

```
docker --version
```

> Jika keluar pesan seperti ini `Docker version 20.10.21, build baeda1f` artinya Docker sudah terpasang

### Unduh paket Exorde

Jalankan program :

   ```bash
   docker run \
   -d \
   --restart unless-stopped \
   --pull always \
   --name exorde-cli \
   rg.fr-par.scw.cloud/exorde-labs/exorde-cli \
   -m <ETH ADDRESSMU> \
   -l <LOGGING_LEVEL>
   ```

   Contoh :

   ```bash
   docker run \
   -d \
   --restart unless-stopped \
   --pull always \
   --name exorde-cli \
   rg.fr-par.scw.cloud/exorde-labs/exorde-cli \
   -m 0x0F67059ea5c125104E46B46769184dB6DC405C42 \
   -l 2
   ```
> disini agak lama, tungguin saja.

### Cek apakah Docker sudah terpasang

```
docker ps -a
```

```
docker logs -f [Container ID]
```
FYI : Restart modulmu 1/hari, Jika mendapatkan pesan seperti dibawah ini
```
[Faucet] Auto-Faucet n° 355  Failure... retrying.
[Faucet] Auto-Faucet critical Failure. Tried  10  times. Giving up. Please report this error.
```

# Info Tambahan

Jika mendapatkan pesan seperti ini, anda sudah dijalan yang benar.
```[Init Version Check] Current Module Version:  1.3.4
Could not read ConfigRegistry  4  times in a row. The Network might be in trouble, check Discord for any update.
```

### Logging_level

| Logging level | Keterangan |
|---------------|------------|
|0|Tidak ada log|
|1|Log biasa|
|2|Log validasi|
|3|Log validasi dan scrapping|
|4|Log validasi (detail) + log scrapping (untuk troubleshoot)

> Pakai log 2 atau 3 saja, ga usah jadi manusia perfect, kalau 5 gpp auto mining DANA/OVO

### Cara restart Docker
1. Cek dockernya dulu

    ```
    docker ps
    ```
    setelah muncul beberapa list :

    ``` 
    docker restart [Container ID] 
    ```

### Cara Update Docker image:

Jika menemukan error, dan ingin instal baru :
1. Stop dan hapus semua containers Exorde CLI:
   ```
   docker stop <container_name> && docker rm <container_name>
   ```
  
   Contoh :
   ```
   docker stop exorde-cli && docker rm exorde-cli
   ```

2. Jalankan containers baru :
   ```bash
   docker run \
   -d \
   --restart unless-stopped \
   --pull always \
   --name exorde-cli \
   rg.fr-par.scw.cloud/exorde-labs/exorde-cli \
   -m <YOUR_MAIN_ADDRESS> \
   -l <LOGGING_LEVEL>
   ```

   Contoh :

   ```bash
   docker run \
   -d \
   --restart unless-stopped \
   --pull always \
   --name exorde-cli \
   rg.fr-par.scw.cloud/exorde-labs/exorde-cli \
   -m 0x0F67059ea5c125104E46B46769184dB6DC405C42 \
   -l 2
   ```
 
