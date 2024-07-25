### Tutorial Cara Mengerjakan Misi Swisstronik Ke 3 (Mint a ERC-721 Token)

## REMINDER

Sebelumnya Saya Ingatkan Untuk Menggunakan New Wallet, Terserah Masing - Masing, ini Hanya Saran.
Tutorial Yang Saya Berikan Adalah Kumpulan Dari Berbagai Sumber Yang Sudah Saya Rangkum Agar Lebih Mudah Di Pahami Bagi Mereka Yang Mau Mengerjakan ( DYOR )

Untuk Link Misinya Ada Disini : [Click!](https://www.swisstronik.com/testnet2/dashboard)

## Ikuti Langkah Demi Langkah

### 1. Copy Paste Link Di Bawah ini Ke Gitpod ( Diawali Https Tanpa Ada Huruf Git Clone )


```bash
git clone 
```

```
cd swisstronik-perc20-mint-token
```

### 2. Tambahkan File .env Lalu Kemudian Masukkan Private Key Wallet Kalian Yang Sudah Kalian Buat

create .env file in root project

```bash
PRIVATE_KEY="your private key"
```

### 3. Edit NFT Yang Akan Kalian Buat

- Buka Menu Contracts
- Buka File PERC20Sample.sol
- Silahkan Ubah Nama Dan Symbol Seperti Yang Kalian Inginkan

```bash
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "./PERC20.sol";

/**
 * @dev Sample implementation of the {PERC20} contract.
 */
contract PERC20Sample is PERC20 {
    constructor() PERC20("Percobaan", "PRC") {}

    /// @dev Wraps SWTR to PSWTR.
    receive() external payable {
        _mint(_msgSender(), msg.value);
    }

    /**
     * @dev Regular `balanceOf` function marked as internal, so we override it to extend visibility  
     */ 
    function balanceOf(address account) public view override returns (uint256) {
        // This function should be called by EOA using signed `eth_call` to make EVM able to
        // extract original sender of this request. In case of regular (non-signed) `eth_call`
        // msg.sender will be empty address (0x0000000000000000000000000000000000000000).
        require(msg.sender == account, "PERC20Sample: msg.sender != account");

        // If msg.sender is correct we return the balance
        return _balances[account];
    }

    /**
     * @dev Regular `allowance` function marked as internal, so we override it to extend visibility  
     */
    function allowance(address owner, address spender) public view virtual override returns (uint256) {
        // This function should be called by EOA using signed `eth_call` to make EVM able to
        // extract original sender of this request. In case of regular (non-signed) `eth_call`
        // msg.sender will be empty address (0x0000000000000000000000000000000000000000)
        require(msg.sender == spender, "PERC20Sample: msg.sender != account");
        
        // If msg.sender is correct we return the allowance
        return _allowances[owner][spender];
    }

    function mint() public {
        _mint(msg.sender, 10000*10**18);
    }

  }  
```

### 4. Compile Smart Contract

```bash
npm run compile
```

### 5. Deploy Smart Contract

```bash
npm run deploy
```

### 6. Mint Token

```bash
npm run mint
```

### 7. Transfer Token

```bash
npm run transfer
```

### 8. Selesai Dan Kalian Tinggal Copy Paste Misi Yang Sudah Dikerjakan

 Selesai Dan Kalian Tinggal Copy Paste Misi Yang Sudah Dikerjakan

- Buka Menu deployed-adddress.ts Untuk Misi Kontrak Pintar
- Buka Menu tx-hash.txt Untuk Mengetahui TX Hash
- Lalu Tinggal Copy Paste Ke Halaman Swisstronik Testnet 3

Untuk Link Misinya Ada Disini : [Click!](https://www.swisstronik.com/testnet2/dashboard)


### Terimakasih Dan Semoga Bermanfaat
