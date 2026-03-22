#Nix #インストール
# インストール
```zsh
curl -sSfL https://artifacts.nixos.org/nix-installer | sh -s -- install
```
インストールを上記コマンドで実行する

## 確認
```zsh
source /nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh
nix --version
```
[参考](https://zenn.dev/trifolium/books/1c0373f3570334/viewer/common-05)
[深掘り](https://zenn.dev/trifolium/articles/da11a428c53f65)