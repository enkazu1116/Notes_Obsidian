#Nix #HomeManager 
# 設定ファイル
- home.nix
- flake.nix
## home.nix
```shell
{ config, pkgs, ... }:

{
  home.username = "endouikki";
  home.homeDirectory = "/home/endouikki";
  home.stateVersion = "25.11";

  home.packages = [
  ];

  home.file = {
  };

  home.sessionVariables = {
  };

  programs.home-manager.enable = true;
}

```
ここにユーザー環境へ入れたいパッケージなどを記述していきます
## flake.nix
```shell
{ 
	description = "Home Manager configuration of endouikki"; 
	inputs = { 
		# Specify the source of Home Manager and Nixpkgs. 
		nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable"; 
		home-manager = { 
			url = "github:nix-community/home-manager"; 
			inputs.nixpkgs.follows = "nixpkgs"; 
		}; 
	}; 
	outputs = { nixpkgs, home-manager, ... }: 
	let 
		system = "aarch64-darwin"; 
		pkgs = nixpkgs.legacyPackages.${system}; 
	in 
	{ 
		homeConfigurations."endouikki" = 
		home-manager.lib.homeManagerConfiguration { 
			inherit pkgs; 
			# Specify your home configuration modules here, for example, 
			# the path to your home.nix. 
			modules = [ ./home.nix ]; 
			# Optionally use extraSpecialArgs 
			# to pass through arguments to home.nix 
		}; 
	}; 
}
```
### inputs
利用するHome Managerのソースをどこから取得するかを定義
### homeConfigurations
flake.nixの下側にあるhomeConfigurationsにて、どの設定ファイルを追加で読み込むかを定義
## 設定ファイル関連のファイル
dotfilesリポジトリに
- home.nix
- flake.nix
- flake.lock
がある。
これは、flake.nixを利用したNixの処理の過程で生成されるファイル。
inputsに定義した情報をベースにして、参照先を固定するのに利用される。
このロックファイルにより、Home Manager本体や導入するパッケージのバージョンが固定