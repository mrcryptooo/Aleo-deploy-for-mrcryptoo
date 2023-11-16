discord: mrcryptoo
# Aleo-deploy-for-mrcryptoo
Aleo deploy for mrcryptoo
First prepare the prerequisites and enter the following codes after starting.
start:
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustup install stable
rustup update stable
rustup default stable
git clone https://github.com/AleoHQ/leo
cd leo
apt install clang gcc libssl-dev pkg-config
cargo install --path .
git clone https://github.com/AleoHQ/snarkOS.git --depth 1
cd snarkOS
./build_ubuntu.sh
cargo install --path .
-------------------------------------------------------------
At this point, you must have received Faucet via Twitter or SMS.
-------------------------------------------------------------
cd $HOME
mkdir demo_deploy_Leo_app && cd demo_deploy_Leo_app
WALLETADDRESS="your_wallet_address"
APPNAME=helloworld_"${WALLETADDRESS:4:6}"
leo new "${APPNAME}"
PATHTOAPP=$(realpath -q $APPNAME)
cd $PATHTOAPP && cd ..
PRIVATEKEY="your_private_key"
RECORD="your_record"
snarkos developer deploy "${APPNAME}.aleo" --private-key "${PRIVATEKEY}" --query "https://vm.aleo.org/api" --path "./${APPNAME}/build/" --broadcast "https://vm.aleo.org/api/testnet3/transaction/broadcast" --fee 600000 --record "${RECORD}"
