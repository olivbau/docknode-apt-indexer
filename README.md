# Docknode APT Indexer

## Install

0. VPS config (optional)

```bash
apt update && apt upgrade -y && apt install -y git build-essential pkg-config libssl-dev libpq-dev

# install rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
. "$HOME/.cargo/env"

# install docker https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
```

1. Clone the repository and

```bash
git clone --recursive https://github.com/olivbau/docknode-apt-indexer.git
cd docknode-apt-indexer
```

2. Configure environement variables

```bash
cp .env.example .env

# Generate users passwords for basic auth
docker run --rm caddy:2-alpine caddy hash-password --plaintext 'password'

# Set users and passwords for basic auth
# Set the host
nano .env
```

3. Setup UFW

```bash
ufw allow ssh && ufw deny 5432
ufw enable
```

4. Run

```bash
docker compose pull
docker compose up -d
cargo run --manifest-path ./aptos-indexer-processors/rust/processor/Cargo.toml --release -- -c ./config.yaml

docker compose down
```
