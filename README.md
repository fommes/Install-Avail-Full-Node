# Avail Goldberg Full-Node

  *** 
X1.** Install Rust**

```
sudo apt-get update
sudo apt install build-essential
sudo apt install --assume-yes git clang curl libssl-dev protobuf-compiler
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustup default stable
rustup update
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

2.**After ensuring you have Rust installed, you can run the Avail Node using the following command:**

```
git clone https://github.com/availproject/avail.git
cd avail
mkdir -p output
mkdir -p data
git checkout v1.8.0.3
cargo run --locked --release -- --chain goldberg --validator -d ./output 
```


3. **Create Systemd**
```
sudo touch /etc/systemd/system/availd.service
sudo nano /etc/systemd/system/availd.service
```

**Change your Validator name and copy/paste it**

```
[Unit] 
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0
[Service] 
User=root 
ExecStart= /root/avail/target/release/data-avail -d ./output --chain goldberg --validator --name "Dinhcongtac221"
Restart=always 
RestartSec=120
[Install] 
WantedBy=multi-user.target

```
**Save it: CTRL+X** .

P/s: My username is root what I used to login my Vps.

 data-avail file in this directory. 




**To enable this to autostart on bootup run:**

```systemctl enable availd.service```

Start it manually with:

```systemctl start availd.service```

You can check that it's working with:

```systemctl status availd.service```

You can tail the logs with journalctllike so:

```journalctl -f -u availd```

Check your node on https://telemetry.avail.tools
![image](https://github.com/DinhCongTac221/Install-Avail-Full-Node/assets/27664184/c70aaf66-ccbc-485e-ae9e-c09674425772)


