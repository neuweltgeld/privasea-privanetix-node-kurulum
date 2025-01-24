## Sunucu gereksinimleri

Ubuntu

amd64 CPU ***ARM işlemcilerde çalışmaz***

100 GB disk

4GB RAM

<img width="500" alt="Pasted Graphic 3" src="https://github.com/user-attachments/assets/f3d08649-7a07-4655-9fb0-3c0ee56b42f3" />

Arbitrum sepolia eth ihtiyacınız var 

Elinizde sepolia eth varsa burdan bridge yapabilirsiniz

```
https://bridge.arbitrum.io/?destinationChain=arbitrum-sepolia&sourceChain=sepolia
```

Ayrıca sağ üstten Privasea DeepSea faucetten 1 TPRAI token alıyoruz.

<img width="500" alt="Arbitrum Faucet" src="https://github.com/user-attachments/assets/cc7ea910-9c0b-40fc-9557-9f1622201b00" />


Tokenin contract adresi ```0xe999b25Bc133C913b83D69aEC73ea47c1d451315```

## Kurulum adımları

Sunucu güncelleme ve docker kurulumu

```
sudo apt update & sudo apt upgrade -y
```
```
sudo apt install git && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
```
```
sudo systemctl start docker
sudo systemctl enable docker
```

Node kurulumu

```
docker pull privasea/acceleration-node-beta:latest
```

Keystore için klasör oluşturuyoruz

```
mkdir -p /privasea/config && cd /privasea
```

Bu kod bir keystore dosyası oluşturacak ve şifre soracak, şifreyi unutmayın Ayrıca bir node adresi verecek, bu node adresi kullanarak cüzdana ödül alacağız

```
docker run -it -v "/privasea/config:/app/config"  \
privasea/acceleration-node-beta:latest ./node-calc new_keystore
```

Config dosyasına giriyoruz.
```
cd /privasea/config && ls
```

Buradaki dosyanın adını değiştireceğiz, UTC ile başlayan dosyanın adını kopyalayın DOSYAADI ile değiştirin

```
mv DOSYAADI wallet_keystore
```

Dashboarda giriyoruz

https://deepsea-beta.privasea.ai/privanetixNode

Ödülleri claim etmek istediğiniz bir cüzdanla giriş yapın, ve nodunuzu oluşturun. 
Komisyon 1-25 arası girin
Node adresinizi girin ve ```setup my node``` tıklayın.

Sonrasında terminale dönüp nodu çalıştırıyoruz.

```
cd /privasea/
```
Sonra
KEYSTORE_PASSWORD=SIFRE yazan yere biraz önce oluşturduğunuz şifreyi yazın
```
docker run  -d   -v "/privasea/config:/app/config" -e KEYSTORE_PASSWORD=SIFRE privasea/acceleration-node-beta:latest
```

docker ps yazıp çalışan dockerları listeliyoruz, Container Id altındaki Id kopyalayıp CONTAINERID değiştirin

```docker logs -f CONTAINERID```

şu şekilde bir çıktı almanız lazım

<img width="500" alt="CONTAINER ID" src="https://github.com/user-attachments/assets/d83c04a3-b218-4a0a-abe4-126680cd6010" />


Node sayfasına girip detailse tıklıyoruz
Elimizdeki tokenleri stake ediyoruz.

```stake failed```hatası alırsanız cüzdandan gaz limitine bi kaç sıfır ekleyip tekrar deneyin


![image](https://github.com/user-attachments/assets/26b538e0-56ef-44a7-9f40-a5013be6c6aa)

Eksik görürseniz pr atabilirsiniz ya da telegram @avalanchezone pm atabilirsiniz.


